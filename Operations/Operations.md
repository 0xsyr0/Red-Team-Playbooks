# Operations

## Table of Contents

- [Tooling](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Operations/Operations.md#Tooling)
- [Golden Rules](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Operations/Operations.md#Golden-Rules)
- [Meetings](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Operations/Operations.md#Meetings)
	- [Schedule](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Operations/Operations.md#Schedule)
- [Reporting](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Operations/Operations.md#Reporting)
	- [Folder Structure](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Operations/Operations.md#Folder-Structure)
	- [Collaborative Timeline](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Operations/Operations.md#Folder-Structure)
	- [Screenshot Naming Scheme](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Operations/Operations.md#Screenshot-Naming-Scheme)
	- [Report Structure](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Operations/Operations.md#Report-Structure)
- [Logging](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Operations/Operations.md#Logging)
	- [Basic logging and Documentation Handling](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Operations/Operations.md#Basic-Logging-and-Documentation-Handling)
- [Assessment Timeline](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Operations/Operations.md#Assessment-Timeline)
- [Operations Server Installation](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Operations/Operations.md#Operations-Server-Installation)

## Tooling

| Name | Description |  URL |
| --- | --- | --- |
| Atomic Red Team | Atomic Red Team™ is a library of tests mapped to the MITRE ATT&CK® framework. Security teams can use Atomic Red Team to quickly, portably, and reproducibly test their environments. | https://github.com/redcanaryco/atomic-red-team |
| OWASP Threat Dragon | Threat Dragon is a free, open-source, cross-platform threat modeling application including system diagramming and a rule engine to auto-generate threats/mitigations. | https://github.com/mike-goodwin/owasp-threat-dragon-desktop |
| Caldera | CALDERA™ is a cyber security platform designed to easily automate adversary emulation, assist manual red-teams, and automate incident response. | https://github.com/mitre/caldera |
| VECTR | VECTR is a tool that facilitates tracking of your red and blue team testing activities to measure detection and prevention capabilities across different attack scenarios. | https://github.com/SecurityRiskAdvisors/VECTR |
| Obsidian | Obsidian is a powerful knowledge base on top of a local folder of plain text Markdown files. | https://obsidian.md |
| XMind | Full-featured mind mapping and brainstorming app. | https://www.xmind.net |
| Ghostwriter | Ghostwriter is a Django-based web application designed to be used by an individual or a team of red team operators. | https://github.com/GhostManager/Ghostwriter |

## Golden Rules

- Slow and steady. Confidence is key.
- Use proxychains if applicable.
- Work out of Docker containers if possible to keey a low profile.
- After landing on the beachhead, always acting like a normal user (for example whoami /all or BloodHound collection method -ALL, use -dc-only instead).
- Don't interrupt infrastructre longer as needed.
- Cleanup after you finished. Don't let anykind of file laying around.
- Build back changes (DNS spoofing for example).
- Nmap -A -T4 is probably not a good idea. It's not a CTF!

## Meetings

### Schedule

| | Monday | Tuesday | Wednesday | Thursday | Friday | Saturday | Sunday |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Start | Assessment Kickoff | | Sync | | Weekly Review | | |
| Weekly | Planning | | Sync | | Weekly Review | | |
| Closing | Planning | | Sync | | Closing / Assessment Review | | |

## Reporting

## Folder Structure

```c
assessment_name
├── 0-operations
├── 1-osint
├── 2-recon
├── 3-targets
│   ├── domain_name
│   │   └── exfil
│   └── ip_hostname
│       └── exfil
├── 4-screenshots
│   └── YYYYMMDD_HHMM_IP_description.png
├── 5-payloads
├── 6-loot
├── 7-logs
└── README.md
```

### Collaborative Timeline

I highly recommend to dump a `timeline.md` with the following notation
into a internally hosted `Git Repository`.

```c
# <ASSESSMENT_NAME>

## Timeline

### Duration

#### YYYY-MM-DD

HH:MM <TASK>, <DESCRIPTION>
<COMMAND>
```

So it's easier to keep track of your actions and merge them later as
input for the report.

#### Example

```c
# RTA-01 Active Directory

## Timeline

### Duration 2022-08-01 - 2022-09-01

#### 2022-08-01

09:15 Reconnaissance, Port Scan Domain Controller
$ nmap 192.168.1.10

#### 2022-08-02

...
...
...
```

### Screenshot Naming Scheme

- 20220801_1508_10.10.1.106_nmap_tcp445.png
- 20220801_1508_10.10.1.106_smb_enumeration.png
- 20220801_1508_10.10.1.106_smb_password_file.png

### Report Structure

```c
# <ASSESSMENT_NAME> ASSESSMENT REPORT
#### <COMPANY>
##### <REPORTER>

## Table of Contents

* 1. Introduction
* 2. Executive Summary
	- 2.1 Scope of Work (SoW)
	- 2.2 Project Objectives
	- 2.3 Assumption
	- 2.4 Project Phases
	- 2.5 Project Duration
	- 2.6 Summary of Findings
		- 2.6.1 Overall Posture
		- 2.6.2 Risk Rating
- 3. Methodology
	- 3.1 Planning
	- 3.2 Exploitation
	- 3.3 Reporting
- 4. Deliverables
	- 4.1 Reconnaissance
	- 4.2 Weaponization
	- 4.3 Delivery
	- 4.4 Exploitation
	- 4.5 Installation
	- 4.6 Command and Control
	- 4.7 Actions on Objective
- 5. Recommendations
	- 5.1 Critical Risk
	- 5.2 High Risk
	- 5.3 Medium Risk
	- 5.4 Low Risk
- 6. References
	- Appendix A
	- Appendix B
	- Appendix C
```

## Logging

### Basic Logging and Documentation Handling

* Screenshot everything!
* Note every attempt even it's a failure
* Create and update a report storyboard during the process

For adding `time and date` and the current `IP address`, add the required commands to either the `.bashrc` or to the `.zshrc`.

### Bash: local IP address

```c
PS1="[`date  +"%Y-%m-%d %H:%M"`]\[\033[01;31m\] `ip a | grep -A 1 eth0 | grep inet | awk '{ print $2 }' | cut -d '/' -f 1`\[\033[00m\] \[\033[01;34m\]\w\[\033[00m\] \$ "
```

### Bash: external IP address

```c
PS1='[`date  +"%Y-%m-%d %H:%M"`]\[\033[01;31m\] `curl -s ifconfig.co`\[\033[00m\] \[\033[01;34m\]\w\[\033[00m\] \$ '
```

### ZSH: local IP address

```c
PS1="[20%D %T] %B%F{red}$(ip a | grep -A 1 eth0 | grep inet | awk '{ print $2 }' | cut -d '/' -f 1)%f%b %B%F{blue}%1~%f%b $ "
```

### ZSH: external IP address

```c
PS1="[20%D %T] %B%F{red}$(curl -s ifconfig.co)%f%b %B%F{blue}%1~%f%b $ "
```

### ZSH: Kali Linux prompt with local IP address

```c
PROMPT="%F{white,bold}%W %* $(ip a | grep -A 1 eth0 | grep inet | awk '{ print $2 }' | cut -d '/' -f 1)"$'%F{%(#.blue.green)}\n┌──${debian_chroot:+($debian_chroot)─}${VIRTUAL_ENV:+($(basename $VIRTUAL_ENV))─}(%B%F{%(#.red.blue)}%n'$prompt_symbol$'%m%b%F{%(#.blue.green)})-[%B%F{reset}%(6~.%-1~/…/%4~.%5~)%b%F{%(#.blue.green)}]\n└─%B%(#.%F{red}#.%F{blue}$)%b%F{reset} '
```

### PowerShell

For `PowerShell` paste it into the open terminal.

```c
$IPv4 = Test-Connection -ComputerName (hostname) -Count 1  | Select -ExpandProperty IPV4Address; function prompt{ "PS" + " [$(Get-Date)] $IPv4> $(get-location) " }
```

### Linux Logging Examples

#### Logging using tee

```c
command args | tee <FILE>.log
```

#### Append to an existing log file

```c
command args | tee -a <FILE>.log
```

#### All commands logging using script utility

```c
script <FILE>.log
```

#### Single command logging using script utility

```c
script -c 'command args' <FILE>.log
```

### Windows Logging Examples

```c
Get-ChildItem -Path D: -File -System -Recurse | Tee-Object -FilePath "C:\temp\<FILE>.txt" -Append | Out-File C:\temp\<FILE>.txt
```

### Metasploit spool command

```c
msf> spool <file>.log
```

## Assessment Timeline

<p align="center">
  <img src="https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Operations/files/assessment_template.png">
</p>

### Template

[assessment_template.xmind](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Operations/files/assessment_template.xmind)

## Operations Server Installation

### Update Server OS

```c
root@operations:~# apt-get update && apt-get upgrade && apt-get dist-upgrade && apt-get autoremove && apt-get autoclean
```

### Set Timezone

```c
root@operations:~# timedatectl set-timezone <COUNTRY>/<CITY>
```

### Packages

```c
root@operations:~# apt-get install apt-transport-https fail2ban git golang p7zip-full pst-utils python3-pip python3-tk tree zip
```

### User Configuration

```c
root@operations:~# useradd -m ops
root@operations:~# passwd ops
root@operations:~# usermod -aG sudo ops
root@operations:~# usermod -s /bin/bash ops
ops@operations:~$ ln /dev/null ~/.bash_history -sf
```

### Update fstab

```c
root@operations:~# vi /etc/fstab
proc  /proc       proc    defaults,hidepid=2    0    0
none  /dev/pts    devpts  rw,gid=5,mode=620    0    0
none  /run/shm    tmpfs   defaults    0    0
```

### SSH

```c
root@operations:~# chmod 644 /home/ops/.ssh/authorized_keys
root@operations:~# chown root /home/ops/.ssh/authorized_keys
```

### fail2ban

* Copy fail2ban.conf to /etc/fail2ban/
* Copy jail.local to /etc/fail2ban/
* Copy nginx-badbots.conf to /etc/fail2ban/filter.d/
* Copy nginx-noscript.conf /etc/fail2ban/filter.d/

### psad

* copy psad.conf to /etc/psad/ if you already have one

### iptables

```c
* Create iptables.sh in /root/.scripts/
root@operations:~/.scripts# cat iptables.sh
#!/bin/bash

/sbin/iptables -F
/sbin/iptables -P INPUT DROP
/sbin/iptables -P OUTPUT ACCEPT
/sbin/iptables -I INPUT -i lo -j ACCEPT
/sbin/iptables -A INPUT -p tcp --match multiport --dports 22 -j ACCEPT
/sbin/iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
/sbin/iptables -A INPUT -m conntrack --ctstate NEW,ESTABLISHED,RELATED -j ACCEPT
/usr/sbin/netfilter-persistent save
/usr/sbin/iptables-save > /root/custom-ip-tables-rules

root@operations:~# chmod +x iptables.sh
root@operations:~# ./iptables.sh
```

It is recommendet to only allow access from known `IP addresses`!

### tmux tpm

```c
ops@operations:~$ git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
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

### Caldera

```c
ops@operations:~$ git clone https://github.com/mitre/caldera.git --recursive
ops@operations:~$ cd caldera
ops@operations:~/opt/caldera$ pip3 install -r requirements.txt
ops@operations:~/opt/caldera$ python3 server.py --insecure
```

#### Error: AttributeError: module 'lib' has no attribute 'X509_V_FLAG_CB_ISSUER_CHECK'

```c
ops@operations:~$ pip3 install -U cryptography
ops@operations:~$ sudo apt-get remove python3-openssl -y
ops@operations:~$ sudo apt-get autoremove
ops@operations:~$ pip3 install -U cryptography
```

### VECTR

```c
root@operations:/# curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
root@operations:/# add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
root@operations:/# apt-get update
root@operations:/# apt-get install docker-ce docker-ce-cli containerd.io docker-compose unzip
root@operations:/# apt-get upgrade
root@operations:/# systemctl enable docker
ops@operations:~/opt$ mkdir vectr
ops@operations:~/opt/vectr$ wget https://github.com/SecurityRiskAdvisors/VECTR/releases/download/ce-8.4.3/sra-vectr-runtime-8.4.3-ce.zip
ops@operations:~/opt/vectr$ unzip sra-vectr-runtime-8.4.3-ce.zip
ops@operations:~/opt/vectr$ sudo docker-compose up -d
```

#### /etc/hosts

Related to the port forwarding, it is necessary to add the name of the configuration to
the `/etc/hosts` file.

```c
127.0.0.1   sravectr.internal
```

#### Access

```c
$ ssh -i ~/.ssh/id_rsa ops@<RHOST> -L 8081:localhost:8081 -N -f
```

### Ghostwriter

```C
ops@operations:~/opt$ git clone https://github.com/GhostManager/Ghostwriter.git
ops@operations:~/opt/Ghostwriter$ ./ghostwriter-cli-linux install
```

### Previous

- [Kickoff](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Kickoff/Kickoff.md)

### Next

- [1 Reconnaissance](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/1-Reconnaissance/1-Reconnaissance.md)
