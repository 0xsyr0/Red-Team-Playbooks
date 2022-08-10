# 6 Command and Control

| Name | Description | URL |
| --- | --- | --- |
| Mythic | A cross-platform, post-exploit, red teaming framework built with python3, docker, docker-compose, and a web browser UI. | https://github.com/its-a-feature/Mythic |
| silver | Sliver is an open source cross-platform adversary emulation/red team framework, it can be used by organizations of all sizes to perform security testing. | https://github.com/BishopFox/sliver |
| Empire | Empire 4 is a post-exploitation framework that includes a pure-PowerShell Windows agents, Python 3.x Linux/OS X agents, and C# agents. | https://github.com/BC-SECURITY/Empire |
| DeathStart | DeathStar is a Python script that uses Empire's RESTful API to automate gaining Domain and/or Enterprise Admin rights in Active Directory environments using some of the most common offensive TTPs. | https://github.com/byt3bl33d3r/DeathStar |

## C2 Installation

Ansible playbook for this setup is planned but not yet started.

### Set Timezone

```c
root@c2:~# timedatectl set-timezone <COUNTRY>/<CITY>
```

### Update Server OS

```c
root@c2:~# apt-get update && apt-get upgrade && apt-get dist-upgrade && apt-get autoremove && apt-get autoclean
```

### Packages

```c
root@c2:~# apt-get install apt-transport-https curl fail2ban fuse gdb git golang iptables-persistent maven netcat nmap p7zip-full proxychains psad python3-tk ruby ruby-dev snap snapd software-properties-common tmux tor vim
```

### User Configuration

```c
root@c2:~# useradd -m c2ops
root@c2:~# passwd c2ops
root@c2:~# usermod -aG sudo c2ops
root@c2:~# usermod -s /bin/bash c2ops
root@c2:~# ln /dev/null ~/.bash_history -sf
c2ops@c2:~$ ln /dev/null ~/.bash_history -sf
```

### SSH

```c
* Copy authorized_keys to the .ssh folder in the home directory of root and c2ops
* Change the permission of the authorized_keys file
root@c2:~# chmod 644 /home/c2ops/.ssh/authorized_keys
root@c2:~# chown root /home/c2ops/.ssh/authorized_keys
* Copy sshd_config to /etc/ssh/
```

### iptables

```c
* Create iptables.sh in /root/.scripts/
root@c2:~/.scripts# cat iptables.sh
#!/bin/bash

/sbin/iptables -F
/sbin/iptables -P INPUT DROP
/sbin/iptables -P OUTPUT ACCEPT
/sbin/iptables -I INPUT -i lo -j ACCEPT
/sbin/iptables -A INPUT -p tcp --match multiport --dports 2342 -j ACCEPT
/sbin/iptables -A INPUT -p tcp --match multiport --dports 80 -j ACCEPT
/sbin/iptables -A INPUT -p tcp --match multiport --dports 443 -j ACCEPT
/sbin/iptables -A INPUT -p tcp --match multiport --dports 53 -j ACCEPT
/sbin/iptables -A INPUT -p udp --match multiport --dports 53 -j ACCEPT
/sbin/iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
/sbin/iptables -A INPUT -m conntrack --ctstate NEW,ESTABLISHED,RELATED -j ACCEPT
/usr/sbin/netfilter-persistent save
/usr/sbin/iptables-save > /root/custom-ip-tables-rules

root@c2:~# chmod +x iptables.sh
root@c2:~# ./iptables.sh
```

It is recommendet to only allow access from known `IP addresses`!

### OOB DNS

```c
root@c2:~/opt/01_information_gathering# git clone https://github.com/JuxhinDB/OOB-Server
root@c2:~/opt/01_information_gathering/OOB-Server# ./setup
```

### crontab

```c
root@c2:~# crontab -e
0 */12 * * * certbot renew --pre-hook "service nginx stop" --post-hook "service nginx start"
```

### Update fstab

```c
root@c2:~# vi /etc/fstab
proc  /proc       proc    defaults,hidepid=2    0    0
none  /dev/pts    devpts  rw,gid=5,mode=620    0    0
none  /run/shm    tmpfs   defaults    0    0
```

### Services cleanup

```c
root@c2:~# systemctl disable apache2
root@c2:~# systemctl disable exim4
root@c2:~# apt-get purge exim4
root@c2:~# apt-get purge apache2
```

### Nginx

```c
root@c2:~# add-apt-repository ppa:nginx/stable
root@c2:~# apt-get install nginx
```

* Copy nginx.conf /etc/nginx/
* Copy website to /etc/nginx/sites-available/
* Set symlink ln -s /etc/nginx/sites-available/website /etc/nginx/sites-enabled/
* Copy index.html to /var/www/html
* Create files folder in /var/www/html
* Download the following binaries:

```c
root@c2:/var/www/html/files# wget https://raw.githubusercontent.com/411Hall/JAWS/master/jaws-enum.ps1
root@c2:/var/www/html/files# wget https://github.com/carlospolop/PEASS-ng/releases/download/20220515/linpeas.sh
root@c2:/var/www/html/files# wget https://github.com/carlospolop/PEASS-ng/releases/download/20220515/winPEAS.bat
root@c2:/var/www/html/files# wget https://github.com/carlospolop/PEASS-ng/releases/download/20220515/winPEASx64.exe
root@c2:/var/www/html/files# wget https://github.com/carlospolop/PEASS-ng/releases/download/20220515/winPEASx86.exe
root@c2:/var/www/html/files# wget https://eternallybored.org/misc/netcat/netcat-win32-1.12.zip
- Unzip netcat-win32-1.12.zip
root@c2:/var/www/html/files# wget https://github.com/3ndG4me/socat/releases/download/v1.7.3.3/socatx64.bin
root@c2:/var/www/html/files# wget https://github.com/3ndG4me/socat/releases/download/v1.7.3.3/socatx64.exe
root@c2:/var/www/html/files# wget https://github.com/3ndG4me/socat/releases/download/v1.7.3.3/socatx86.bin
root@c2:/var/www/html/files# wget https://github.com/3ndG4me/socat/releases/download/v1.7.3.3/socatx86.exe
root@c2:/var/www/html/files# wget https://github.com/3ndG4me/socat/releases/download/v1.7.3.3/socat_macOS.bin
root@c2:/var/www/html/files# wget https://github.com/DominicBreuker/pspy/releases/download/v1.2.0/pspy32
root@c2:/var/www/html/files# wget https://github.com/DominicBreuker/pspy/releases/download/v1.2.0/pspy64
root@c2:/var/www/html/files# wget https://github.com/BloodHoundAD/BloodHound/raw/master/Collectors/SharpHound.exe
root@c2:/var/www/html/files# wget https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/master/Recon/PowerView.ps1
root@c2:/var/www/html/files# wget https://github.com/gentilkiwi/mimikatz/releases/download/2.2.0-20210810-2/mimikatz_trunk.7z
```

* Unzip mimikatz_trunk.7z

### Let's Encrypt

Only necessary if the server got installed from a backup!

```c
root@c2:~# apt-get install letsencrypt
```

* Copy letsencrypt to /etc/
* Set symlinks:

```c
root@c2:~# cd /etc/letsencrypt/live/example.com
root@c2:/etc/letsencrypt/live/example.com# rm cert.pem chain.pem fullchain.pem privkey.pem
root@c2:~$tc/letsencrypt/live/example.com# ln -s ../../archive/example.com/cert2.pem cert.pem
root@c2:~$tc/letsencrypt/live/example.com# ln -s ../../archive/example.com/chain2.pem chain.pem
root@c2:~$tc/letsencrypt/live/example.com# ln -s ../../archive/example.com/fullchain2.pem fullchain.pem
root@c2:~$tc/letsencrypt/live/example.com# ln -s ../../archive/example.com/privkey2.pem privkey.pem
```

### fail2ban

* Copy fail2ban.conf to /etc/fail2ban/
* Copy jail.local to /etc/fail2ban/
* Copy nginx-badbots.conf to /etc/fail2ban/filter.d/
* Copy nginx-noscript.conf /etc/fail2ban/filter.d/

### psad

* copy psad psad.conf

### Services

```c
root@c2:~# systemctl enable psad
root@c2:~# systemctl enable fail2ban
root@c2:~# systemctl enable bind9
root@c2:~# systemctl enable nginx
root@c2:~# systemctl start psad
root@c2:~# systemctl start fail2ban
root@c2:~# systemctl start bind9
root@c2:~# systemctl start nginx
root@c2:~# systemctl restart sshd
root@c2:~# systemctl reboot
```

### tmux tpm

```c
c2ops@c2:~$ git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

#### .tmux.conf

```c
set -g default-terminal screen-256color
set -g history-limit 10000
set -g base-index 1
set -g mouse on
set -g terminal-overrides "xterm*:XT:smcup@:rmcup@:"
set -g renumber-windows on
set -g set-clipboard on
set -g status-interval 3
set -sg escape-time 0
setw -g mode-keys vi
set-option -g allow-rename off
set-window-option -g automatic-rename off
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'
set -g @plugin 'tmux-plugins/tmux-resurrect'
run '~/.tmux/plugins/tpm/tpm'
run-shell ~/clone/path/resurrect.tmux
```

### Metasploit

```c
c2ops@c2:~/opt/frameworks/Metasploit$ curl https://raw.githubusercontent.com/rapid7/metasploit-omnibus/master/config/templates/metasploit-framework-wrappers/msfupdate.erb > msfinstall && \
  chmod 755 msfinstall && \
  ./msfinstall
c2ops@c2:~/opt/frameworks$ msfconsole
```

### Empire & Death Star

```c
c2ops@c2:~/opt/frameworks$ git clone --recursive https://github.com/BC-SECURITY/Empire.git
c2ops@c2:~/opt/frameworks/Empire$ sudo ./setup/install.sh
```

* Install all stagers

```c
c2ops@c2:~$ python3 -m pip install --user pipx
c2ops@c2:~$ sudo apt-get install python3.8-venv
c2ops@c2:~$ .local/bin/pipx install deathstar-empire
```

### Swaks

```c
c2ops@c2:~/opt/basics/swaks$ curl -O https://jetmore.org/john/code/swaks/files/swaks-20201014.0/swaks
c2ops@c2:~/opt/basics/swaks$ chmod +x swaks
```

### Amass

```c
c2ops@c2:~$ sudo snap install amass
```

### Subfinder

```c
c2ops@c2:~/opt/01_information_gathering/subfinder$ wget https://github.com/projectdiscovery/subfinder/releases/download/v2.5.1/subfinder_2.5.1_linux_amd64.zip
c2ops@c2:~/opt/01_information_gathering/subfinder$ unzip subfinder_2.5.1_linux_amd64.zip
```

### naabu

```c
c2ops@c2:~/opt/01_information_gathering/naabu$ wget https://github.com/projectdiscovery/naabu/releases/download/v2.0.7/naabu_2.0.7_linux_amd64.zip
c2ops@c2:~/opt/01_information_gathering/naabu$ unzip naabu_2.0.7_linux_amd64.zip
```

### enum4linux-ng

```c
c2ops@c2:~/opt/01_information_gathering$ git clone https://github.com/cddmp/enum4linux-ng.git
```

### Nuclei

```c
c2ops@c2:~/opt/02_vulnerability_analysis/nuclei$ wget https://github.com/projectdiscovery/nuclei/releases/download/v2.7.0/nuclei_2.7.0_linux_amd64.zip
c2ops@c2:~/opt/02_vulnerability_analysis/nuclei$ unzip nuclei_2.7.0_linux_amd64.zip
```

### Nuclei-Templates

```c
c2ops@c2:~/opt/02_vulnerability_analysis$ git clone https://github.com/projectdiscovery/nuclei-templates.git
```

### Dalfox

```c
c2ops@c2:~$ sudo snap install dalfox
```

### Shodan

```c
c2ops@c2:~$ pip3 install shodan
c2ops@c2:~$ shodan init <API_KEY>
```

### Gobuster

```c
c2ops@c2:~/opt/03_web_application_analysis/gobuster$ wget https://github.com/OJ/gobuster/releases/download/v3.1.0/gobuster-linux-amd64.7z
c2ops@c2:~/opt/03_web_application_analysis/gobuster$ 7z e gobuster-linux-amd64.7z
c2ops@c2:~/opt/03_web_application_analysis/gobuster$ chmod +x gobuster
```

### ffuf

```c
c2ops@c2:~/opt/03_web_application_analysis$ git clone https://github.com/ffuf/ffuf ; cd ffuf ; go get ; go build
```

### TruffleHog

```c
c2ops@c2:~/opt/03_web_application_analysis$ git clone https://github.com/trufflesecurity/trufflehog.git
c2ops@c2:~/opt/03_web_application_analysis/trufflehog$ go install
```

### WPScan

```c
root@c2:/home/c2ops# gem install wpscan
```

### CrackMapExec

```c
c2ops@c2:~$ pipx install crackmapexec
```

### John

```c
root@c2:/home/c2ops# apt-get install g++ git qtbase5-dev
c2ops@c2:~/opt/05_password_attacks$ git clone https://github.com/shinnok/johnny.git && cd johnny
c2ops@c2:~/opt/05_password_attacks/johnny$ git checkout v2.2
c2ops@c2:~/opt/05_password_attacks/johnny$ export QT_SELECT=qt5
c2ops@c2:~/opt/05_password_attacks/johnny$ qmake && make -j$(nproc)
```

### hashcat

```c
c2ops@c2:~/opt/05_password_attacks/hashcat$ wget https://hashcat.net/files/hashcat-6.2.5.7z
c2ops@c2:~/opt/05_password_attacks/hashcat$ 7z e hashcat-6.2.5.7z
```

### sqlmap

```c
c2ops@c2:~/opt/04_database_assessment$ git clone --depth 1 https://github.com/sqlmapproject/sqlmap.git
c2ops@c2:~/opt/04_database_assessment/sqlmap$ python3 sqlmap.py
```

### peda

```c
c2ops@c2:~$ git clone https://github.com/longld/peda.git ~/peda
c2ops@c2:~$ echo "source ~/peda/peda.py" >> ~/.gdbinit
```

### lsassy

```c
c2ops@c2:~$ python3 -m pip install lsassy
```

### JNDI-Exploit-Kit

```c
c2ops@c2:~/opt/08_exploitation_tools$ git clone https://github.com/welk1n/JNDI-Injection-Exploit.git
c2ops@c2:~/opt/08_exploitation_tools/JNDI-Injection-Exploit$ mvn clean package -DskipTests
```

### Ghostpack-CompiledBinaries

```c
c2ops@c2:~/opt/08_exploitation_tools$ git clone https://github.com/r3motecontrol/Ghostpack-CompiledBinaries.git
```

### Impacket

```c
c2ops@c2:~/opt/08_exploitation_tools$ git clone https://github.com/SecureAuthCorp/impacket.git
c2ops@c2:~/opt/08_exploitation_tools/impacket$ python3 -m pip install .
```

### Evil-WinRM

```c
root@c2:/home/c2ops# gem install evil-winrm
```

### GoPhish

```c
c2ops@c2:~/opt/13_social_engineering_tools/gophish$ wget https://github.com/gophish/gophish/releases/download/v0.11.0/gophish-v0.11.0-linux-64bit.zip
c2ops@c2:~/opt/13_social_engineering_tools/gophish$ unzip gophish-v0.11.0-linux-64bit.zip
c2ops@c2:~/opt/13_social_engineering_tools/gophish$ chmod +x gophish
c2ops@c2:~/opt/13_social_engineering_tools/gophish$ sudo ./gophish
```

#### Access

```
$ ssh -i ~/.ssh/id_rsa c2ops@<RHOST> -L 3333:localhost:3333 -N -f
```

> https://localhost:3333/login?next=%2F

### theHarvester

```c
c2ops@c2:~/opt/osint$ git clone https://github.com/laramies/theHarvester
c2ops@c2:~/opt/osint/theHarvester$ python3 -m pip install -r requirements/dev.txt
```

### PowerShell

```c
c2ops@c2:~/opt/05_password_attacks/hashcat$ sudo snap install powershell --classic
```

### nishang

```c
c2ops@c2:~/opt/payloads$ git clone https://github.com/samratashok/nishang.git
```

### PowerSharpPack

```c
c2ops@c2:~/opt/payloads$ git clone https://github.com/S3cur3Th1sSh1t/PowerSharpPack.git
```

### phpgcc

```c
c2ops@c2:~/opt/payloads$ git clone https://github.com/ambionics/phpggc.git
```

### Shikata Ga Nai

```c
c2ops@c2:~/opt/payloads$ git clone https://github.com/EgeBalci/sgn.git
```

### ysoserial

```c
c2ops@c2:~/opt/payloads$ git clone https://github.com/frohoff/ysoserial.git
```

### marshallsec

```c
c2ops@c2:~/opt/payloads$ git clone https://github.com/mbechler/marshalsec.git
```

### YSoSerial.Net

```c
c2ops@c2:~/opt/payloads$ git clone https://github.com/pwntester/ysoserial.net.git
```

### Unicorn

```c
c2ops@c2:~/opt/payloads$ git clone https://github.com/trustedsec/unicorn.git
```

### Web-Shells

```c
c2ops@c2:~/opt/payloads$ git clone https://github.com/TheBinitGhimire/Web-Shells.git
```

### rockyou.txt

```c
c2ops@c2:~/opt/wordlists/rockyou$ wget https://gitlab.com/kalilinux/packages/wordlists/-/raw/kali/master/rockyou.txt.gz
c2ops@c2:~/opt/wordlists/rockyou$ gunzip rockyou.txt.gz
```

### SecLists

```c
c2ops@c2:~/opt/wordlists$ git clone https://github.com/danielmiessler/SecLists.git
```

### Previous

- [5 Installation](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/5-Installation/5-Installation.md)
- [5.1 Persistence](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/5-Installation/5.1-Persistence.md)
- [5.2 Situational Awareness](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/5-Installation/5.2-Situational-Awareness.md)

### Next

- [7 Actions-on-Objective](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/7-Actions-on-Objective/7-Actions-on-Objective.md)
- [7.1 Post Exploitation](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/7-Actions-on-Objective/7.1-Post-Exploitation.md)
- [7.2 Exfiltration](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/7-Actions-on-Objective/7.2-Exfiltration.md)
