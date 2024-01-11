# Infrastructure

## Table of Contents

- [Tooling](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#Tooling)
- [Requirements](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#Requirements)
- [Design](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#Design)
- [Deployment](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#Deployment)
- [VPN Gateway](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#VPN-Gateway)
- [Messenger Server](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#Messenger-Server)
- [Reporting Server](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#Reporting-Server)
- [Operations Server](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#Operations-Server)
- [Command and Control Server](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#Command-and-Control-Server)
- [Traffic-Redirector](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#Traffic-Redirector)
- [Phishing Server](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#Phishing-Server)
	- [Phishing Server Installation](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#Phishing-Server-Installation)
		- [Preparation](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#preparation)
			- [Add phisher User](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#add-phisher-user)
			- [Password Changes](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#password-changes)
	- [Basic Tooling & Updates](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#basic-tooling--updates)
		- [Set Timezone](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#set-timezone)
		- [SSH](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#ssh)
		- [Tmux](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#tmux)
		- [Nginx](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#nginx)
		- [Let's Encrypt](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#lets-encrypt)
	- [GoPhish](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#gophish)
		- [config.json](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#configjson)
		- [Port Forwarding Admin Panel](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#port-forwarding-admin-panel)
		- [Accessing Admin Panel](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#accessing-admin-panel)
		- [Configuration](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#configuration)
			- [Account Settings](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#account-settings)
			- [Landing Pages](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#landing-pages)
			- [Email Templates](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#email-templates)
			- [Users & Groups](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#users--groups)
			- [Campaigns](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#campaigns)
	- [Evilginx2](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#Evilginx2)
- [Malware Development Environment](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#malware-development-environment)
- [Lab Environment](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#lab-environment)
- [RedELK](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/Infrastructure.md#redelk)

## Tooling

### VPN Gateway

| Name | Description | URL |
| --- | --- | --- |
| WireGuard | WireGuard is an extremely simple yet fast and modern VPN that utilizes state-of-the-art cryptography. | https://www.wireguard.com |

### Messenger Server

| Name | Description | URL |
| --- | --- | --- |
| Element | A glossy Matrix collaboration client for the web. | https://github.com/element-hq/element-web |
| matrix | An open network for secure, decentralised communication | https://matrix.org |

### Reporting Server

| Name | Description | URL |
| --- | --- | --- |
| SySReptor | SysReptor is a fully customisable, offensive security reporting solution designed for pentesters, red teamers and other security-related people alike. | https://github.com/Syslifters/sysreptor |

### Command and Control

| Name | Description | URL |
| --- | --- | --- |
| Cobalt Strike | Adversary Simulation and Red Team Operations | https://www.cobaltstrike.com/ |
| Covenant | Covenant is a .NET command and control framework that aims to highlight the attack surface of .NET, make the use of offensive .NET tradecraft easier, and serve as a collaborative command and control platform for red teamers. | https://github.com/cobbr/Covenant |
| DeathStar | DeathStar is a Python script that uses Empire's RESTful API to automate gaining Domain and/or Enterprise Admin rights in Active Directory environments using some of the most common offensive TTPs. | https://github.com/byt3bl33d3r/DeathStar |
| Empire | Empire 4 is a post-exploitation framework that includes a pure-PowerShell Windows agents, Python 3.x Linux/OS X agents, and C# agents. | https://github.com/BC-SECURITY/Empire |
| Havoc | The Havoc Framework | https://github.com/HavocFramework/Havoc |
| Mythic | A cross-platform, post-exploit, red teaming framework built with python3, docker, docker-compose, and a web browser UI. It's designed to provide a collaborative and user friendly interface for operators, managers, and reporting throughout red teaming. | https://github.com/its-a-feature/Mythic |
| RedWarden | Cobalt Strike C2 Reverse proxy that fends off Blue Teams, AVs, EDRs, scanners through packet inspection and malleable profile correlation | https://github.com/mgeeky/RedWarden |
| Sliver | Sliver is an open source cross-platform adversary emulation/red team framework, it can be used by organizations of all sizes to perform security testing. | https://github.com/BishopFox/sliver |

### Malware Development Environment

| Name | Description | URL |
| --- | --- | --- |
| GitLab CE | GitLab Community Edition (CE) is an open source end-to-end software development platform with built-in version control, issue tracking, code review, CI/CD, and more. | https://gitlab.com/rluna-gitlab/gitlab-ce |
| Team City | Powerful continuous integration for DevOps-centric teams | https://www.jetbrains.com/teamcity |

### Phishing

| Name | Description | URL |
| --- | --- | --- |
| evilgophish | evilginx2 + gophish | https://github.com/fin3ss3g0d/evilgophish |
| Gophish | Open-Source Phishing Toolkit | https://github.com/gophish/gophish |

## Requirements

## Design

## Deployment

## VPN Gateway

## Messenger Server

## Reporting Server

## Operations Server

## Command and Control Server

### Preparation

#### Set Timezone

```c
root@c2:~# timedatectl set-timezone <COUNTRY>/<CITY>
```

#### Update Server OS

```c
root@c2:~# apt-get update && apt-get upgrade && apt-get dist-upgrade && apt-get autoremove && apt-get autoclean
```

#### Packages

```c
root@c2:~# apt-get install apt-transport-https curl fail2ban fuse gdb git golang iptables-persistent maven netcat nmap p7zip-full proxychains psad python3-tk ruby ruby-dev snap snapd software-properties-common tmux tor vim
```

#### User Configuration

```c
root@c2:~# useradd -m c2ops
root@c2:~# passwd c2ops
root@c2:~# usermod -aG sudo c2ops
root@c2:~# usermod -s /bin/bash c2ops
root@c2:~# ln /dev/null ~/.bash_history -sf
c2ops@c2:~$ ln /dev/null ~/.bash_history -sf
```

#### SSH

* Copy authorized_keys to the .ssh folder in the home directory of root and c2ops
* Change the permission of the authorized_keys file
* Copy sshd_config to /etc/ssh/

```c
root@c2:~# chmod 644 /home/c2ops/.ssh/authorized_keys
root@c2:~# chown root /home/c2ops/.ssh/authorized_keys
```

#### fail2ban

* Copy fail2ban.conf to /etc/fail2ban/
* Copy jail.local to /etc/fail2ban/
* Copy nginx-badbots.conf to /etc/fail2ban/filter.d/
* Copy nginx-noscript.conf /etc/fail2ban/filter.d/

#### psad

* copy psad.conf to /etc/psad/ if you already have one

#### crontab

```c
root@c2:~# crontab -e
0 */12 * * * certbot renew --pre-hook "service nginx stop" --post-hook "service nginx start"
```

#### Update fstab

```c
root@c2:~# cat /etc/fstab
proc  /proc       proc    defaults,hidepid=2    0    0
none  /dev/pts    devpts  rw,gid=5,mode=620    0    0
none  /run/shm    tmpfs   defaults    0    0
```

## Traffic Redirector

## Phishing Server

### Preparation

* Getting a domain from:
	* https://inwx.com
	* https://www.expireddomains.net/
* Create a droplet on https://digitalocean.com or https://aws.amazon.com/

After purchasing a domain, I recommend to add a `CAA` record for your upcoming `Let's Encrypt Certificate`.

Also it is needed to configure the `DNS servers` of `DigitalOcean`.

```c
ns1.digitalocean.com
ns2.digitalocean.com
ns3.digitalocean.com
```

```c
0 issue "letsencrypt.org"
```

### Add phisher User

```c
root@phishingserver:~# useradd -m phisher
root@phishingserver:~# passwd phisher
root@phishingserver:~# usermod -aG sudo phisher
root@phishingserver:~# usermod -s /bin/bash phisher
```

### Password Changes

```c
root@phishingserver:~# passwd root
```

### Basic Tooling & Updates

#### Installing Updates

```c
root@phishingserver:~# apt-get update && apt-get upgrade && apt-get dist-upgrade && apt-get autoremove && apt-get autoclean
```

#### Installing Packages

```c
root@phishingserver:~# apt-get install apt-transport-https fail2ban git golang letsencrypt python3-pip zip
```

### Set Timezone

```c
root@phishingserver:~# timedatectl set-timezone <COUNTRY>/<CITY>
```

### SSH

#### Changing Permissions of /home/phisher/.ssh

```c
root@phishingserver:~# chmod 644 /home/phisher/.ssh/authorized_keys
root@phishingserver:~# chown root /home/phisher/.ssh/authorized_keys
```

Add your `SSH Public Key` to the `authorized_keys` file.

#### sshd_config

```c
#	$OpenBSD: sshd_config,v 1.103 2018/04/09 20:41:22 tj Exp $

# This is the sshd server system-wide configuration file.  See
# sshd_config(5) for more information.

# This sshd was compiled with PATH=/usr/bin:/bin:/usr/sbin:/sbin

# The strategy used for options in the default sshd_config shipped with
# OpenSSH is to specify options with their default value where
# possible, but leave them commented.  Uncommented options override the
# default value.

Include /etc/ssh/sshd_config.d/*.conf

Port 22
#AddressFamily any
#ListenAddress 0.0.0.0
#ListenAddress ::

#HostKey /etc/ssh/ssh_host_rsa_key
#HostKey /etc/ssh/ssh_host_ecdsa_key
#HostKey /etc/ssh/ssh_host_ed25519_key

# Ciphers and keying
#RekeyLimit default none

# Logging
#SyslogFacility AUTH
#LogLevel INFO

# Authentication:

#LoginGraceTime 2m
PermitRootLogin yes
#StrictModes yes
#MaxAuthTries 6
#MaxSessions 10

PubkeyAuthentication yes

# Expect .ssh/authorized_keys2 to be disregarded by default in future.
AuthorizedKeysFile	.ssh/authorized_keys .ssh/authorized_keys2

#AuthorizedPrincipalsFile none

#AuthorizedKeysCommand none
#AuthorizedKeysCommandUser nobody

# For this to work you will also need host keys in /etc/ssh/ssh_known_hosts
#HostbasedAuthentication no
# Change to yes if you don't trust ~/.ssh/known_hosts for
# HostbasedAuthentication
#IgnoreUserKnownHosts no
# Don't read the user's ~/.rhosts and ~/.shosts files
#IgnoreRhosts yes

# To disable tunneled clear text passwords, change to no here!
PasswordAuthentication no
#PermitEmptyPasswords no

# Change to yes to enable challenge-response passwords (beware issues with
# some PAM modules and threads)
ChallengeResponseAuthentication no

# Kerberos options
#KerberosAuthentication no
#KerberosOrLocalPasswd yes
#KerberosTicketCleanup yes
#KerberosGetAFSToken no

# GSSAPI options
#GSSAPIAuthentication no
#GSSAPICleanupCredentials yes
#GSSAPIStrictAcceptorCheck yes
#GSSAPIKeyExchange no

# Set this to 'yes' to enable PAM authentication, account processing,
# and session processing. If this is enabled, PAM authentication will
# be allowed through the ChallengeResponseAuthentication and
# PasswordAuthentication.  Depending on your PAM configuration,
# PAM authentication via ChallengeResponseAuthentication may bypass
# the setting of "PermitRootLogin yes
# If you just want the PAM account and session checks to run without
# PAM authentication, then enable this but set PasswordAuthentication
# and ChallengeResponseAuthentication to 'no'.
UsePAM yes

#AllowAgentForwarding yes
#AllowTcpForwarding yes
#GatewayPorts no
X11Forwarding yes
#X11DisplayOffset 10
#X11UseLocalhost yes
#PermitTTY yes
PrintMotd no
#PrintLastLog yes
#TCPKeepAlive yes
#PermitUserEnvironment no
#Compression delayed
#ClientAliveInterval 0
#ClientAliveCountMax 3
#UseDNS no
#PidFile /var/run/sshd.pid
#MaxStartups 10:30:100
#PermitTunnel no
#ChrootDirectory none
#VersionAddendum none

# no default banner path
#Banner none

# Allow client to pass locale environment variables
AcceptEnv LANG LC_*

# override default of no subsystems
Subsystem sftp	/usr/lib/openssh/sftp-server

# Example of overriding settings on a per-user basis
#Match User anoncvs
#	X11Forwarding no
#	AllowTcpForwarding no
#	PermitTTY no
#	ForceCommand cvs server
```

#### Restart sshd Daemon

```c
root@phishingserver:~# systemctl restart sshd
```

#### Access

```c
$ ssh -i ~/.ssh/id_rsa phisher@<LHOST>
```

### Tmux

#### tmux tpm

> https://github.com/tmux-plugins/tpm

```c
phisher@phishingserver:~$ git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

#### tmux-resurrect

> https://github.com/tmux-plugins/tmux-resurrect

#### .tmux.conf

```c
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'
set -g @plugin 'tmux-plugins/tmux-resurrect'

run '~/.tmux/plugins/tpm/tpm'
```

### Nginx

```c
root@phishingserver:~# add-apt-repository ppa:nginx/stable
root@phishingserver:~# apt-get update && apt-get install nginx
```

#### nginx.conf

```c
user www-data;
worker_processes auto;
pid /run/nginx.pid;
include /etc/nginx/modules-enabled/*.conf;

events {
	worker_connections 768;
	# multi_accept on;
}

http {

	##
	# Basic Settings
	##

	sendfile on;
	tcp_nopush on;
	tcp_nodelay on;
	keepalive_timeout 65;
	types_hash_max_size 2048;
	server_tokens off;

	# server_names_hash_bucket_size 64;
	# server_name_in_redirect off;

	include /etc/nginx/mime.types;
	default_type application/octet-stream;

	##
	# Buffer Settings
	##

	client_body_buffer_size 1k;
	client_header_buffer_size 1k;
	client_max_body_size 1k;
	large_client_header_buffers 2 1k;

	##
	# Server Settings
	##

	add_header X-Frame-Options "SAMEORIGIN";
	add_header X-Content-Type-Options "nosniff";
	add_header Referrer-Policy "strict-origin";
	add_header Strict-Transport-Security "max-age=31536000; includeSubdomains; preload";
	add_header Content-Security-Policy "frame-ancestors 'none'";
	add_header Permissions-Policy "geolocation=();midi=();notifications=();push=();sync-xhr=();microphone=();camera=();magnetometer=();gyroscope=();speaker=(self);vibrate=();fullscreen=(self);payment=();";

	##
	# SSL Settings
	##

	ssl_protocols TLSv1.2 TLSv1.3; # Dropping SSLv3, ref: POODLE
	ssl_ciphers 'ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256';
	ssl_prefer_server_ciphers on;

	##
	# Logging Settings
	##

	access_log /var/log/nginx/access.log;
	error_log /var/log/nginx/error.log crit;

	##
	# Gzip Settings
	##

	gzip on;

	# gzip_vary on;
	# gzip_proxied any;
	# gzip_comp_level 6;
	# gzip_buffers 16 8k;
	# gzip_http_version 1.1;
	# gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;

	##
	# Virtual Host Configs
	##

	include /etc/nginx/conf.d/*.conf;
	include /etc/nginx/sites-enabled/*;
}


#mail {
#	# See sample authentication script at:
#	# http://wiki.nginx.org/ImapAuthenticateWithApachePhpScript
# 
#	# auth_http localhost/auth.php;
#	# pop3_capabilities "TOP" "USER";
#	# imap_capabilities "IMAP4rev1" "UIDPLUS";
# 
#	server {
#		listen     localhost:110;
#		protocol   pop3;
#		proxy      on;
#	}
# 
#	server {
#		listen     localhost:143;
#		protocol   imap;
#		proxy      on;
#	}
#}
```

#### /etc/nginx/sites-available/website

```c
server {
    listen 80;
    server_name <DOMAIN>;
    return 301 https://$server_name$request_uri;

    location / {
        limit_except GET HEAD POST { deny all; }
    }
}

server {
    listen 443 ssl;
    listen [::]:443 ssl;

    server_name <DOMAIN>;

    ssl_certificate /etc/letsencrypt/live/<DOMAIN>/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/<DOMAIN>/privkey.pem;

    root /var/www/html;
    index index.html index.htm;

    location / {
        limit_except GET HEAD POST { deny all; }
        proxy_pass http://127.0.0.1:8008;
    }

    access_log    /var/log/nginx/website.access.log;
}
```

#### Enable Configuration

```c
root@phishingserver:~# ln -s /etc/nginx/sites-available/website /etc/nginx/sites-enabled/
```

#### Let's Encrypt

```c
root@phishingserver:~# certbot certonly --rsa-key-size 2048 --standalone --agree-tos --no-eff-email --email <EMAIL> -d <DOMAIN>
```

#### Creating Cronjob

```c
0 */12 * * * certbot renew --pre-hook "service nginx stop" --post-hook "service nginx start"
```

### GoPhish

> https://github.com/gophish/gophish

```c
phisher@phishingserver:~/opt$ wget https://github.com/gophish/gophish/releases/download/v0.11.0/gophish-v0.11.0-linux-64bit.zip
phisher@phishingserver:~/opt$ unzip gophish-v0.11.0-linux-64bit.zip gophish/
phisher@phishingserver:~/opt/gophish$ chmod +x gophish 
phisher@phishingserver:~/opt/gophish$ ./gophish
```

#### config.json

```c
{
        "admin_server": {
                "listen_url": "127.0.0.1:3333",
                "use_tls": true,
                "cert_path": "gophish_admin.crt",
                "key_path": "gophish_admin.key"
        },
        "phish_server": {
                "listen_url": "0.0.0.0:8008",
                "use_tls": false,
                "cert_path": "example.crt",
                "key_path": "example.key"
        },
        "db_name": "sqlite3",
        "db_path": "gophish.db",
        "migrations_prefix": "db/db_",
        "contact_address": "",
        "logging": {
                "filename": "",
                "level": ""
        }
}
```

#### Port Forwarding Admin Panel

```c
$ ssh -i ~/.ssh/id_rsa phisher@<LHOST> -L 3333:localhost:3333 -N -f
```

#### Accessing Admin Panel

> https://localhost:3333/login?next=%2F

#### Accessing Campaign Websites

```c
https://<DOMAIN>/?rid=<RID>
```

#### Configuration

For this example I created an account on `outlook.com` which I needed for sending emails. I highly recommend to configure a local mail server!

For example by using `MailHog`.

> https://github.com/mailhog/MailHog

##### Account Settings

###### Reporting Settings

| Field | Value |
| --- | --- |
| IMAP Host: | imap.outlook.com |
| IMAP Port: | 993 |
| IMAP Username: | EXAMPLE@outlook.com | 
| IMAP Password: | ********************************* |
| Use TLS: | Check |

###### Sending Profile

| Field | Value |
| --- | --- |
| Name: | <ASSESSMENT_NAME> |
| SMTP From: | EXAMPLE@outlook.com |
| HOST: | smtp.outlook.com:587 |
| Username: | EXAMPLE@outlook.com |
| Password: | ********************************* |
| Ignore Certificate Errors: | Check |

Depedending on your `Rules of Engangement (ROE)` I would recommend to set custom `Email Headers`.

###### Landing Pages

| Field | Value |
| --- | --- |
| Name: | https://confluence.<DOMAIN> |
| Import: | https://confluence.<DOMAIN> |
| Capture | Submitted Data: Check |
| Capture Passwords: | Check |
| Redirecto to: | https://confluence.<DOMAIN> |

If your purchased `TLD` matches the domain of your company, the change is high that users do not raise
concern if they get redirected to the same `login page` you copied your landing page from.

####### Example

```c
Original domain: examplecompany.io
Fake domain: security-examplecompany.io
```

The may think they made a typo, try to login again after got redirected and everything works fine.
No need to worry ;)

###### Email Templates

| Field | Value |
| --- | --- |
| Name: | <ASSESSMENT_NAME> |
| Envelope Sender: | EXAMPLE@outlook.com |
| Subject: | Security Monitoring Report, Endpoints and Applications |
| Add Tracking Image: | Check |

If you be able to get a leaked sample of an internal email or by `Spear Phishing` someone, I would recommend to
use the signature and formatting for more authenticity.

Or you can use a sample like this.

```c
<!DOCTYPE html>
<html>
<head>
	<title></title>
</head>
<body>

<p>Dear colleagues, We would like to provide more transparency with regard to our current vulnerabilities scans and have provided a report on the use of the installed applications and websites accessed in Confluence.</p>

<p><a href="{{.URL}}">https://confluence.<DOMAIN>/Security-Monitoring-Report-July-2022</a></p>

<p>We plan to publish this report monthly to create a better awareness of information security within the company. If you have any questions, please do not hesitate to contact us.</p>

<p>&nbsp;</p>

<p>Kind regards</p>

<p>Security Team</p>

<p><COMPANY_DETAILS><br />
</p>

<p>{{.Tracker}}</p>
</body>
</html>
```

Enrich the email template with as much information as possible you gathered from OSINT. For example try `Spear Phishing` members of the marketing department after getting their email addresses from https://hunter.io, to get a valid email signature.

###### Users & Groups

I recommend to gather usernames from social media platforms like `LinkedIn`, `Instagram` and `Facebook`. The email address schema is also easy to figure out. For example by using `Maltego`, https://hunter.io or by simply checking their website for a `security.txt`.

```c
https://<DOMAIN>/security.txt
```

You may also find contact forms for your `sock puppets` to contact them and get a response.

The only necessary fields are `First Name`, `Last Name` and `Email`. The filed of `Position` is optional.

###### Campaigns

Time to add a new campaign. Pretty straight forward.

| Field | Value |
| --- | --- |
| Campaign name: | <ASSESSMENT_NAME> |
| Email Template: | <ASSESSMENT_NAME> |
| Landing Page: | https://confluence.<DOMAIN> |
| Launch Date: | Leave it as it is if you want to start directly after saving the campaign. |
| Send Emails By: | By setting a date you can scale the interval of sending emails. I recommend to add 5 days from the start to not get in trouble with outlook.com. |
| Sending Profile: | <ASSESSMENT_NAME> |
| Groups: | <ASSESSMENT_NAME> |
| Launch Campaign | |

<p align="center">
  <img src="https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Infrastructure/files/gophish_results.png">
</p>

### Evilginx2

> https://help.evilginx.com/docs/getting-started/building

> https://help.evilginx.com/docs/getting-started/quick-start

> https://help.evilginx.com/docs/guides/phishlets

#### Installation

```c
$ sudo apt-get install golang
$ git clone https://github.com/kgretzky/evilginx2.git
$ cd evilginx2
$ make
$ sudo ./build/evilginx -p ./phishlets
```

##### Alternatively with Redirectors

```c
$ sudo ./build/evilginx -p ./phishlets -t ./redirectors -developer
```

#### Basic Commands

```c
: phishlets
: lures
: sessions
```

#### Prepare Certificates

```c
$ sudo cp /root/.evilginx/crt/ca.crt /usr/local/share/ca-certificates/evilginx.crt
$ sudo update-ca-certificates
```

#### Domain Setup

```c
: config domain <DOMAIN>
: config ipv4 <LHOST>
```

#### Phishlets

> https://help.evilginx.com/docs/guides/phishlets

> https://github.com/An0nUD4Y/Evilginx2-Phishlets

```c
: phishlets hostname <PHISHLET> <DOMAIN>
: phishlets enable <PHISHLET>
```

#### Lures

> https://help.evilginx.com/docs/guides/lures

```c
: lures create <PHISHLET>
: lures get-url <ID>
```

#### Session Handling

```c
: sessions
: sessions <ID>
```

### Previous

- [Operations](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Operations/Operations.md)

### Next

- [1 Reconnaissance](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/1-Reconnaissance/1-Reconnaissance.md)