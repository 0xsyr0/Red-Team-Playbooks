# Operations

| Name | Description |  URL |
| --- | --- | --- |
| Atomic Red Team | Atomic Red Team™ is a library of tests mapped to the MITRE ATT&CK® framework. Security teams can use Atomic Red Team to quickly, portably, and reproducibly test their environments. | https://github.com/redcanaryco/atomic-red-team |
| OWASP Threat Dragon | Threat Dragon is a free, open-source, cross-platform threat modeling application including system diagramming and a rule engine to auto-generate threats/mitigations. | https://github.com/mike-goodwin/owasp-threat-dragon-desktop |
| Caldera | CALDERA™ is a cyber security platform designed to easily automate adversary emulation, assist manual red-teams, and automate incident response. | https://github.com/mitre/caldera |
| VECTR | VECTR is a tool that facilitates tracking of your red and blue team testing activities to measure detection and prevention capabilities across different attack scenarios. | https://github.com/SecurityRiskAdvisors/VECTR |
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

## Folder Structure on operations server

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

### Examples of screenshots

- 20220801_1508_10.10.1.106_nmap_tcp445.png
- 20220801_1508_10.10.1.106_smb_enumeration.png
- 20220801_1508_10.10.1.106_smb_password_file.png

## Logging

### Basic Logging and Documentation Handling

* Screenshot everything!
* Note every attempt even it's a failure
* Create and update a report storyboard during the process

### .bashrc Logging Prompt

```c
PS1='[`date  +"%d-%b-%y %T"`]\[\033[01;31m\] `ifconfig eth0 2>/dev/null | sed -n 2,2p | cut -d" " -f 10`\[\033[00m\] \[\033[01;34m\]\w\[\033[00m\] \$ '
```

### Adding IP address to .bashrc Logging Prompt

```c
PS1='[`date  +"%d-%b-%y %T"`]\[\033[01;31m\] `curl -s ifconfig.co`\[\033[00m\] \[\033[01;34m\]\w\[\033[00m\] \$ '
```

### .zshrc Logging Prompt

```c
PROMPT="%{$fg_bold[grey]%}[%{$reset_color%}%{$fg_bold[${host_color}]%}%n@%m%{$reset_color%}%{$fg_bold[grey]%}]%{$reset_color%} %{$fg_bold[blue]%}%10c %W %t $(ifconfig | grep -A 1 wlp4s0 | grep inet | tr -s ' ' | cut -d ' ' -f 3) %{$reset_color%} $(git_prompt_info) $(git_remote_status)
%{$fg_bold[cyan]%}❯%{$reset_color%} "
```

### Adding IP address to .zshrc Logging Prompt

```c
PROMPT="%{$fg_bold[grey]%}[%{$reset_color%}%{$fg_bold[${host_color}]%}%n@%m%{$reset_color%}%{$fg_bold[grey]%}]%{$reset_color%} %{$fg_bold[blue]%}%10c %W %t $(curl -s http://ipecho.net/plain; echo) %{$reset_color%} $(git_prompt_info) $(git_remote_status)
#%{$fg_bold[cyan]%}❯%{$reset_color%} "
```

### Linux Logging Examples

#### Logging using tee

```c
command args | tee <file>.log
```

#### Append to an existing log file

```c
command args | tee -a <file>.log
```

#### All commands logging using script utility

```c
script <file>.log
```

#### Single command logging using script utility

```c
script -c 'command args' <file>.log
```

### Windows Logging Examples

```c
Get-ChildItem -Path D: -File -System -Recurse | Tee-Object -FilePath "C:\temp\<file>.txt" -Append | Out-File C:\temp\<file>.txt
```

### Metasploit spool command

```c
msf> spool <file>.log
```

### Previous

- [Kickoff](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Kickoff/Kickoff.md)

### Next

- [1 Enumeration](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/1-Reconnaissance/1-Enumeration.md)
