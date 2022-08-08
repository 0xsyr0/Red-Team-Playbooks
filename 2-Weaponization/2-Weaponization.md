# Introduction

## Tooling

| Name | Description | URL |
| --- | --- | --- |
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

- [1 Reconnaissance](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/1-Reconnaissance/1-Reconnaissance.md)
- [1.1 Scanning and Enumeration](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/1-Reconnaissance/1.1-Scanning-and-Enumeration.md)

### Next

- [2.1 Initial Access](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/2-Weaponization/2.1-Initial-Access.md)
