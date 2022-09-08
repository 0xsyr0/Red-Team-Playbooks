# 3 Delivery

## Table of Contents

- [Tooling](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#tooling)
- [Phishing Server Installation](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#phishing-server-installation)
- [Preparation](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#preparation)
	- [Add phisher User](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#add-phisher-user)
	- [Password Changes](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#password-changes)
- [Basic Tooling & Updates](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#basic-tooling--updates)
	- [Set Timezone](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#set-timezone)
	- [SSH](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#ssh)
	- [Tmux](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#tmux)
	- [Nginx](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#nginx)
	- [Let's Encrypt](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#lets-encrypt)
- [GoPhish](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#gophish)
	- [config.json](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#configjson)
	- [Port Forwarding Admin Panel](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#port-forwarding-admin-panel)
	- [Accessing Admin Panel](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#accessing-admin-panel)
	- [Configuration](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#configuration)
		- [Account Settings](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#account-settings)
		- [Landing Pages](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#landing-pages)
		- [Email Templates](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#email-templates)
		- [Users & Groups](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#users--groups)
		- [Campaigns](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#campaigns)

## Tooling

| Name | Description | URL |
| --- | --- | --- |
| Gophish | Open-Source Phishing Toolkit | https://github.com/gophish/gophish |
| evilgophish | evilginx2 + gophish | https://github.com/fin3ss3g0d/evilgophish |
| The Social-Engineer Toolkit (SET) | The Social-Engineer Toolkit (SET) repository from TrustedSec | https://github.com/trustedsec/social-engineer-toolkit |

# Phishing Server Installation

## Preparation

* Getting a domain from:
	* https://inwx.com
	* https://www.expireddomains.net/
* Create a droplet on https://digitalocean.com

After purchasing a domain, i recommend to add a `CAA` record for your upcoming `Let's Encrypt Certificate`.

Also it is needed to configure the `DNS servers` of `DigitalOcean`.

```c
ns1.digitalocean.com
ns2.digitalocean.com
ns3.digitalocean.com
```

```c
0 issue "letsencrypt.org"
```

## Add phisher User

```c
root@phishingserver:~# useradd -m phisher
root@phishingserver:~# passwd phisher
root@phishingserver:~# usermod -aG sudo phisher
root@phishingserver:~# usermod -s /bin/bash phisher
```

## Password Changes

```c
root@phishingserver:~# passwd root
```

## Basic Tooling & Updates

### Installing Updates

```c
root@phishingserver:~# apt-get update && apt-get upgrade && apt-get dist-upgrade && apt-get autoremove && apt-get autoclean
```

### Installing Packages

```c
root@phishingserver:~# apt-get install apt-transport-https fail2ban git golang letsencrypt python3-pip zip
```

## Set Timezone

```c
root@phishingserver:~# timedatectl set-timezone <COUNTRY>/<CITY>
```

## SSH

### Changing Permissions of /home/phisher/.ssh

```c
root@phishingserver:~# chmod 644 /home/phisher/.ssh/authorized_keys
root@phishingserver:~# chown root /home/phisher/.ssh/authorized_keys
```

Add your `SSH Public Key` to the `authorized_keys` file.

### sshd_config

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

### Restart sshd Daemon

```c
root@phishingserver:~# systemctl restart sshd
```

### Access

```c
$ ssh -i ~/.ssh/id_rsa phisher@<LHOST>
```

## Tmux

### tmux tpm

> https://github.com/tmux-plugins/tpm

```c
phisher@phishingserver:~$ git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

### tmux-resurrect

> https://github.com/tmux-plugins/tmux-resurrect

### .tmux.conf

```c
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'
set -g @plugin 'tmux-plugins/tmux-resurrect'

run '~/.tmux/plugins/tpm/tpm'
```

## Nginx

```c
root@phishingserver:~# add-apt-repository ppa:nginx/stable
root@phishingserver:~# apt-get update && apt-get install nginx
```

### nginx.conf

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

### /etc/nginx/sites-available/website

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

### Enable Configuration

```c
root@phishingserver:~# ln -s /etc/nginx/sites-available/website /etc/nginx/sites-enabled/
```

### Let's Encrypt

```c
root@phishingserver:~# certbot certonly --rsa-key-size 2048 --standalone --agree-tos --no-eff-email --email <EMAIL> -d <DOMAIN>
```

### Creating Cronjob

```c
0 */12 * * * certbot renew --pre-hook "service nginx stop" --post-hook "service nginx start"
```

## GoPhish

> https://github.com/gophish/gophish

```c
phisher@phishingserver:~/opt$ wget https://github.com/gophish/gophish/releases/download/v0.11.0/gophish-v0.11.0-linux-64bit.zip
phisher@phishingserver:~/opt$ unzip gophish-v0.11.0-linux-64bit.zip gophish/
phisher@phishingserver:~/opt/gophish$ chmod +x gophish 
phisher@phishingserver:~/opt/gophish$ ./gophish
```

### config.json

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

### Port Forwarding Admin Panel

```c
$ ssh -i ~/.ssh/id_rsa phisher@<LHOST> -L 3333:localhost:3333 -N -f
```

### Accessing Admin Panel

> https://localhost:3333/login?next=%2F

### Accessing Campaign Websites

```c
https://<DOMAIN>/?rid=<RID>
```

### Configuration

For this example i created an account on `outlook.com` which i needed for sending emails. I highly recommend to configure a local mail server!

For example by using `MailHog`.

> https://github.com/mailhog/MailHog

#### Account Settings

##### Reporting Settings

| Field | Value |
| --- | --- |
| IMAP Host: | imap.outlook.com |
| IMAP Port: | 993 |
| IMAP Username: | EXAMPLE@outlook.com | 
| IMAP Password: | ********************************* |
| Use TLS: | Check |

##### Sending Profile

| Field | Value |
| --- | --- |
| Name: | <ASSESSMENT_NAME> |
| SMTP From: | EXAMPLE@outlook.com |
| HOST: | smtp.outlook.com:587 |
| Username: | EXAMPLE@outlook.com |
| Password: | ********************************* |
| Ignore Certificate Errors: | Check |

Depedending on your `Rules of Engangement (ROE)` i would recommend to set custom `Email Headers`.

##### Landing Pages

| Field | Value |
| --- | --- |
| Name: | https://confluence.<TARGET_DOMAIN> |
| Import: | https://confluence.<TARGET_DOMAIN> |
| Capture | Submitted Data: Check |
| Capture Passwords: | Check | 
| Redirecto to: | https://confluence.<TARGET_DOMAIN> |

If your purchased `TLD` matches the domain of your company, the change is high that users do not raise
concern if they get redirected to the same `login page` you copied your landing page from.

###### Example

```c
Original domain: examplecompany.io
Fake domain: security-examplecompany.io
```

The may think they made a typo, try to login again after got redirected and everything works fine.
No need to worry ;)

##### Email Templates

| Field | Value |
| --- | --- |
| Name: | <ASSESSMENT_NAME> |
| Envelope Sender: | EXAMPLE@outlook.com | 
| Subject: | Security Monitoring Report, Endpoints and Applications |
| Add Tracking Image: | Check |

If you be able to get a leaked sample of an internal email or by `Spear Phishing` someone, i would recommend to
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

<p><a href="{{.URL}}">https://confluence.<TARGET_DOMAIN>/Security-Monitoring-Report-July-2022</a></p>

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

##### Users & Groups

I recommend to gather usernames from social media platforms like `LinkedIn`, `Instagram` and `Facebook`. The email address schema is also easy to figure out. For example by using `Maltego`, https://hunter.io or by simply checking their website for a `security.txt`.

```c
https://<TARGET_DOMAIN>/security.txt
```

You may also find contact forms for your `sock puppets` to contact them and get a response.

The only necessary fields are `First Name`, `Last Name` and `Email`. The filed of `Position` is optional.

##### Campaigns

Time to add a new campaign. Pretty straight forward.

| Field | Value |
| --- | --- |
| Campaign name: | <ASSESSMENT_NAME> |
| Email Template: | <ASSESSMENT_NAME> |
| Landing Page: | https://confluence.<TARGET_DOMAIN> |
| Launch Date: | Leave it as it is if you want to start directly after saving the campaign. |
| Send Emails By: | By setting a date you can scale the interval of sending emails. I recommend to add 5 days from the start to not get in trouble with outlook.com. |
| Sending Profile: | <ASSESSMENT_NAME> |
| Groups: | <ASSESSMENT_NAME> |
| Launch Campaign | |

<p align="center">
  <img src="https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/files/gophish_results.png">
</p>

### Previous

- [2 Weaponization](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/2-Weaponization/2-Weaponization.md)
- [2.1 Initial Access](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/2-Weaponization/2.1-Initial-Access.md)

### Next

- [4 Exploitation](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/4-Exploitation/4-Exploitation.md)
- [4.1 Defense Evasion](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/4-Exploitation/4.1-Defense-Evasion.md)
- [4.2 Credential Dumping](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/4-Exploitation/4.2-Credential-Dumping.md)
- [4.3 Privilege Escalation](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/4-Exploitation/4.3-Privilege-Escalation.md)
- [4.4 Lateral Movement](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/4-Exploitation/4.4-Lateral-Movement.md)