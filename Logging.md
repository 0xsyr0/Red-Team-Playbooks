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
// Logging using tee
```c
command args | tee <file>.log
```
// Append to an existing log file
```c
command args | tee -a <file>.log
```
// All commands logging using script utility
```c
script <file>.log
```
// Single command logging using script utility
```c
script -c 'command args' <file>.log
```
// Metasploit spool command
```c
msf> spool <file>.log
```
### Windows Logging Examples
```c
Get-ChildItem -Path D: -File -System -Recurse | Tee-Object -FilePath "C:\temp\<file>.txt" -Append | Out-File C:\temp\<file>.txt
```
