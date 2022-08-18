# 5 Installation

| Name | Description | URL |
| --- | --- | --- |
| Donut | Donut is a position-independent code that enables in-memory execution of VBScript, JScript, EXE, DLL files and dotNET assemblies. | https://github.com/TheWover/donut |
| ScareCrow | ScareCrow is a payload creation framework for side loading (not injecting) into a legitimate Windows process (bypassing Application Whitelisting controls). | https://github.com/optiv/ScareCrow |
| OffensiveNim | Experiments in weaponizing Nim for implant development and general offensive operations. | https://github.com/byt3bl33d3r/OffensiveNim |
| OffensiveRust | Experiments in weaponizing Rust for implant development and general offensive operations. | https://github.com/trickster0/OffensiveRust |

## Windows Defender

Windows Defender seems like to have issues with the following function in Visual Basic Scripts.

```c
Private Declare PtrSafe Function VirtualProtectEx Lib "kernel32" ( _
    ByVal hProcess As LongPtr, _
    ByVal lpAddress As LongPtr, _
    ByVal dwSize As Long, _
    ByVal flNewProtect As Long, _
    ByRef lpflOldProtect As LongPtr _
) As Long
```

Also with:

- CreateProcess
- VirtualAllocEx
- GetProcAddress
- LoadLibrary

### Previous

- [4 Exploitation](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/4-Exploitation/4-Exploitation.md)
- [4.1 Defense Evasion](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/4-Exploitation/4.1-Defense-Evasion.md)
- [4.2 Credential Dumping](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/4-Exploitation/4.2-Credential-Dumping.md)
- [4.3 Privilege Escalation](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/4-Exploitation/4.3-Privilege-Escalation.md)
- [4.4 Lateral Movement](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/4-Exploitation/4.4-Lateral-Movement.md)

### Next

- [5.1 Persistence](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/5-Installation/5.1-Persistence.md)
- [5.2 Situational Awareness](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/5-Installation/5.2-Situational-Awareness.md)
