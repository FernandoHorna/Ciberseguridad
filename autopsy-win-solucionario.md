
# Taller

## Caso de Estudio

El día 20 de Setiembre del Año 2004, una computadora Dell CPI notebook con número de serie #VLQLW, fue encontrada abandonada con una tarjeta inalámbrica PCMCIA y una antena externa casera 802.11b. Se sospecha que esta computadora fue utilizada para propósito de Hacking, sin embargo no puede ser ligada con el sospechoso de hacking, Greg Schardt.

Schardt también utiliza el sobrenombre en linea de “Mr. Evil” y algunos de sus socios han expresado que estacionaba su vehículo dentro del rango de Puntos de Acceso Inalámbricos (como Starbucks y otros hotspots T-Mobile) donde luego estaría interceptando tráfico, intentando capturar números de tarjetas de crédito, nombres de usuario y contraseñas.

La imagen de la evidencia tiene la descripción siguiente: **SCHARDT.dd** y los hashs siguientes:

**MD5:** aee4fcd9301c03b3b054623ca261959a

**SHA1:** da2fe30fe21711edf42310873af475859a68f300

Ud. es el perito que ha sido asignado al caso y se te ha proporcionado la imagen de la evidencia en el archivo **ImagenForense.zip** para que Ud. efectúe el análisis del caso.

Ud. Deberá responder las preguntas siguientes:

1.	¿Cuál es el hash de la imagen? ¿Coincide el hash de la imagen adquirida y verificada?
2.	¿Qué tipo de sistema operativo fue usado en la computadora?
3.	¿Cuándo fue realizada la fecha de instalación?
4.	¿Cuál es la zona de tiempo?
5.	¿Quién es el propietario registrado?
6.	¿Cuál es el nombre de la computadora?
7.	¿Cuáles son los usuarios de la computadora?
8.	¿Cuándo fue la última fecha que la computadora fue apagada?
9.	¿Cuántas cuentas están grabadas (número total)?
10.	¿Cuál es el nombre del usuario quien utiliza mayormente la computadora?
11.	¿Quién fue el último usuario que se logueo en la computadora?
12.	Una búsqueda por el nombre  de “Greg Schardt” revela múltiple hits. Uno de esas prueba que Greg Schardt es Mr. Evil and así mismo es Administrator de la computador. Hay que buscar una evidencia que relacione a ambos usuarios e identificar dicha evidencia y con qué programa se hizo.
13.	Liste las tarjetas de red usados en la computadora
14.	¿Cómo saber cuál fue el IP address and LANNIC. Cuáles son ellos?
15.	Buscar seis (06) programas instalados que son usados para hacking
16.	¿Cuál es la dirección electrónica de Mr. Evil?
17.	Hay un programa de internet llamado IRC (Internet Relay Chat) comunmente llamdo MIRC. ¿Cuáles son las configuraciones que el usuario había definido cuando el usuario estaba online
18.	El MIRC tenía la capacidad de realizar chats a través de los canales a los cuales se ingresaba. Liste 3 canales IRC channels que el usuario accedió
19.	Ethereal, un programa para realizar “sniffing” y que puede utilizarse en redes inalámbricas. ¿Cuál es el nombre del el archivo que contiene la información interceptada? 
20.	Al visualizar el archivo de texto revela una gran información sobre lo que se interceptó. ¿Cuál es el tipo de computadoras tenían las personas que estaban navegando en Internet? 
21.	¿A qué sitios web la victima estuvo accediendo?
22.	Ubique los principales usuarios que accedían a la web
23.	Ubique la dirección de correo electrónico de yahoo que tenía el usuario Mr Evil.
24.	¿Cuántos archivos ejecutables están en la papelera de reciclaje?
25.	¿Esos archivos fueron realmente borrados?

Descarga autopsy ir a http://www.sleuthkit.org/autopsy/download.php e instalelo

![image](https://user-images.githubusercontent.com/50930193/137214550-75ef943a-667d-4b78-ba66-8cf057341af1.png)


-----------


## Solucionario

### Creación del caso

Inicialice Autopsy y luego se apreciará la pantalla siguiente:

![image](https://user-images.githubusercontent.com/50930193/137215699-863a63df-0e14-4a25-a362-9eed458a29e5.png)

En este caso seleccionar  **New case** para crear un nuevo Caso, y luego ingrese los datos para el caso, de preferencia cree una carpeta llamado **C:\caso** o bien seleccione otra carpeta.

![image](https://user-images.githubusercontent.com/50930193/137215990-1b7c2b48-d22d-4a08-8087-bb2b11e3faba.png)

![image](https://user-images.githubusercontent.com/50930193/137216156-827abe1a-0332-41a3-966e-1d8f0959523b.png)

Presione **Finish** y luego seleccione las opciones tal cual se aprecian en la pantalla

![image](https://user-images.githubusercontent.com/50930193/137216369-ad62f073-2aec-478a-9558-6127b7ee05b7.png)

Dar click en **Next**

![image](https://user-images.githubusercontent.com/50930193/137216411-b8b56bde-1e24-4b8c-a207-e1b56878b688.png)

Dar click en **Next** y luego seleccione la ruta del archivo de imagen forense así como el Time Zone. Dar click en **Next**

![image](https://user-images.githubusercontent.com/50930193/137216660-db030a17-bb37-4be6-ac25-e0a0e1bf9daa.png)

![image](https://user-images.githubusercontent.com/50930193/137216878-ee6a4ed2-67d2-44bb-b5a3-e6caf5b04f4b.png)

Respecto a los módulos de ingesta marcar todos los que vamos a utilizar y leugo dar click en **Next**

![image](https://user-images.githubusercontent.com/50930193/137217167-7d8884fe-f1b1-4715-b7bf-f8db087f59f4.png)

Finalmente, dar click en **Finish**

![image](https://user-images.githubusercontent.com/50930193/137217259-aa91af89-805e-4003-81e8-23b6c90ca8f6.png)


### Resolución del preguntas



**1.	¿Cuál es el hash de la imagen? Coincide el hash de la imagen adquirida y verificada?**

+ **Panel izquierdo** Data Sources > SCHART.dd 
+ **Panel derecho superior** Tab Summary > Tab Container

![image](https://user-images.githubusercontent.com/50930193/137218954-15f0dd40-1ecd-48d1-a996-6e73aa6f4122.png)

De allí que los HASH si coinciden 

-----------

**2.	¿Qué tipo de sistema operativo fue usado en la computadora?**

OPCIÓN 1: 

+ **Panel izquierdo** Operating System Information 
+ **Panel derecho superior** Software 
+ **Panel derecho Inferior** Tab Data Artifacts

![image](https://user-images.githubusercontent.com/50930193/137218974-4a4f1673-75fd-414f-b3a8-c4d1917fae57.png)

OPCIÓN 2: 
+ **Panel izquierdo** Data Sources > SCHART.dd 
+ **Panel derecho superior** Summary  > Tab Types

![image](https://user-images.githubusercontent.com/50930193/137219003-ef88d5c4-5209-4095-ba80-ab442eba14a8.png)

-----------

**3.	¿Cuándo fue realizada la fecha de instalación?**


+ **Panel izquierdo** Operating System Information 
+ **Panel derecho superior** Software 
+ **Panel derecho Inferior** Source File Metadata

![image](https://user-images.githubusercontent.com/50930193/137219892-f931ae5a-c91f-4fb6-a5a0-3203077c0404.png)

-----------

**4.	¿Cuál es la zona de tiempo?**

+ **Panel izquierdo** Data Sources > SCHART.dd  > Vol 2  > Windows  > System32  >  config
+ **Panel derecho superior** System
+ **Panel derecho inferior** Application  > ControlSet001  > Control  > TimeZoneInformation

![image](https://user-images.githubusercontent.com/50930193/137221309-ed9fb77d-0bfa-4e98-8e1a-8e85655e329d.png)

-----------

**5.	¿Quién es el propietario registrado?**

+ **Panel izquierdo** Operating System Information 
+ **Panel derecho superior** Software 
+ **Panel derecho Inferior** Data Artifacts

![image](https://user-images.githubusercontent.com/50930193/137221480-a8606a45-ac0d-48b1-ac1e-0b769aee4146.png)

-----------

**6. ¿Cuál es el nombre de la computadora?**

+ **Panel izquierdo** Operating System Information 
+ **Panel derecho superior** Software 
+ **Panel derecho Inferior** Data Artifacts

![image](https://user-images.githubusercontent.com/50930193/137221801-52fe83a1-9d8e-4b8f-82ec-80374e5092ea.png)

-----------

**7.	¿Cuáles son los usuarios de la computadora?**

OPCIÓN 1: 

+ **Panel izquierdo** Data Sources > SCHART.dd  > Documents and Settings

![image](https://user-images.githubusercontent.com/50930193/137222276-e484af46-fe62-4083-91d7-6a01b5419f94.png)

OPCIÓN 2: 

+ **Panel izquierdo** OS Accounts

![image](https://user-images.githubusercontent.com/50930193/137256636-2730b6a5-e34f-4f56-ab7b-fe17056fdac6.png)

-----------

**8. ¿Cuándo fue la última fecha que la computadora fue apagada?**

+ **Panel izquierdo** Data Sources > SCHART.dd  > Vol 2  > Windows  > System32  >  config
+ **Panel derecho superior** System y luego clic derecho y pulsar **Extract File(s)** guardarlo en la carpeta del caso

![image](https://user-images.githubusercontent.com/50930193/137225529-0d540f74-6253-43a6-b592-a1359be5d817.png)

Usar regripper y haciendo referencia al archivo System previamente guardado revisar la información que guarda este artefacto. **Use Rip It**

![image](https://user-images.githubusercontent.com/50930193/137225766-ed4c8a6c-6ed6-4133-84fb-443151564c91.png)

-----------

**9. ¿Cuántas cuentas están grabadas (número total)?**

Según la pregunta 7 hay 5 usuarios

-----------

**10. ¿Cuál es el nombre del usuario quien utiliza mayormente la computadora?**


![image](https://user-images.githubusercontent.com/50930193/137224157-84e61fe8-aac9-4046-8c2f-3ef4c2100fca.png)

Usar regripper y haciendo referencia al archivo SAM previamente guardado revisar la información que guarta este artefacto. **Use Rip It**

![image](https://user-images.githubusercontent.com/50930193/137224369-185a793a-e0a6-4439-a068-5b6a8a3d1a0d.png)

Analicemos los resultados

![image](https://user-images.githubusercontent.com/50930193/137226591-a842737c-ed24-4bba-b3d8-01309bf7984f.png)

-----------

**11. ¿Quién fue el último usuario que se logueo en la computadora?**

Esto se puede apreciar en el reporte anterior, es necesariocomparar el campo Last Login Date y elegir el más reciente

 ![image](https://user-images.githubusercontent.com/50930193/137226716-356be9aa-5f4b-4e45-8ae8-43c7fe346d11.png)

-----------

**12. Una búsqueda por el nombre  of “Greg Schardt” revela múltiple hits. Uno de esas prueba que Greg Schardt es Mr. Evil and así mismo es administrator de la computador. Hay que buscar una evidencia que relacione a ambos usuarios e identificar dicha evidencia y con qué programa se hizo. Para ello, en el panel derecho superior puedes ubicar la opción Keyword Search ubicalo e ingresa la cadena Greg Schardt**

![image](https://user-images.githubusercontent.com/50930193/137226995-15e9ac28-b860-42d0-928c-76ba31e651a4.png)
 
La búsqueda retornará los registros siguientes:

![image](https://user-images.githubusercontent.com/50930193/137227074-a4cc69ae-4f19-4672-a8e1-ce44a99167fd.png)

Si nos vamos programa por programa veremos las coincidencias en cada caso

![image](https://user-images.githubusercontent.com/50930193/137227191-5fd2ec24-2666-4436-92b8-d93f97dac12c.png)

 Cuando se revisa el nombre **url.ini** del programa Look@LAN se puede distinguir que el propietario registrado en ese programa es Greg Schardt , Look@LAN es un software que se utiliza para escanear o hacer vigilancia de redes y detecta archivos en el host. Lo mas seguro es que se le pidió cuando se ingreso o se registro el nombre de Greg Schartd.

![image](https://user-images.githubusercontent.com/50930193/137227445-6d37e7de-f668-40cc-9c20-00e8539cbbd2.png)

Por otro lado en el tab de Strings podemos apreciar que el usuario LAN que de ese programa es 
MR. Evil, 

![image](https://user-images.githubusercontent.com/50930193/137227563-252a0723-b01d-477a-96b9-684beb5e4de6.png)


Por lo tanto encontramos una prueba que quien estaba usando el usuario Mr. Evil fue Greg Schard y él estaba usando el programa Look@LAN

-----------

**13.  Lista las tarjetas de red usados en la computadora**

Para ello hay que ir al archivo de reporte de colmena software.txt, buscar la cadena  NetworkCards, allí podremos identificar las tarjetas de red

 **Panel izquierdo** Data Sources > SCHART.dd  > Vol 2  > Windows  > System32  >  config
**Panel derecho superior** Software y luego clic derecho y pulsar **Extract File(s)** guardarlo en la carpeta del caso

![image](https://user-images.githubusercontent.com/50930193/137228231-59548213-423c-4df5-8bad-ba3bc7d9d11d.png)

Usar regripper y haciendo referencia al archivo Software previamente guardado revisar la información que guarda este artefacto. **Use Rip It**

![image](https://user-images.githubusercontent.com/50930193/137228447-eacfa9fe-53e4-4b7f-891e-0f1ab1519ab8.png)

Analicemos los resultados y buscamos **networkcards**

![image](https://user-images.githubusercontent.com/50930193/137228540-7360647a-fe5d-4a88-bad7-bc90724a16fc.png)

-----------

**14. ¿Cómo saber cual fue el IP address and LANNIC.?**

Esto se puede saber ingresando al archivo url.ini anteriormente analizado, en el panel inferior elegir el tab de Strings, allí podemos apreciar el IP address y su LANNIC 

![image](https://user-images.githubusercontent.com/50930193/137229960-4a450c6c-c8a8-49b9-883c-b3317d9925fb.png)
 
-----------

**15. Buscar seis (06) programas instalados que son usados para hacking**

+ **Panel izquierdo** Data Sources > SCHART.dd  > Vol 2  > Program FIles

![image](https://user-images.githubusercontent.com/50930193/137230282-5ec0b696-30cc-4581-877c-8ccd86f0ea84.png)

 
De allí se pueden mencionar los siguientes programas de hackeo

+	123WASP, para gestionar contraseñas
+	Anonymizer, permite anomizar las conexiones, ocultar rastros
+	Cain, , para hacer sniffing, recuperar contraseñas
+	Ethereal, para hacer sniffing, ataques de envenanmiento
+	Look@LAN, para scanear redes
+	Network Strumbler, se utiliza para atacar redes inalámbricas

-----------

**16. ¿Cuál es la dirección electrónica de Mr. Evil?**

+ **Panel izquierdo** Data Sources > SCHART.dd  > Vol 2  > Program FIles > Agent  >  Data
+ **Panel derecho superior** AGENT.INI
+ **Panel derecho inferior** Tab Indexed Text

![image](https://user-images.githubusercontent.com/50930193/137259873-79cd6e21-8405-423e-ae8c-a6d1c591cc41.png)

 -----------

**17. Hay un programa de internet llamado IRC (Internet Relay Chat) comunmente llamdo MIRC. ¿Cuáles son las configuraciones que el usuario había definido cuando el usuario estaba online**

+ **Panel izquierdo** Data Sources > SCHART.dd  > Vol 2  > Program FIles > mirc
+ **Panel derecho superior** mirc.ini
+ **Panel derecho inferior** Tab Text > Tab Indexed Text

![image](https://user-images.githubusercontent.com/50930193/137231449-81d68ebc-67ae-47b2-b01a-20e3c301f5f5.png)

 -----------
 
**18. el MIRC tenía la capacidad de realizar chats a través de los canales a los cuales se ingresaba. Liste 3 canales IRC channels que el usuario accedió**

+ **Panel izquierdo** Data Sources > SCHART.dd  > Vol 2  > Program FIles > mirc  > Logs
+ **Panel derecho superior** Todos los canales

![image](https://user-images.githubusercontent.com/50930193/137232079-5074a1d8-d5c2-4a35-a14a-e8e0431679de.png)


Nótese que el chat que se mantenía se podía apreciar toda la conversación

  -----------

**19. Ethereal, un programa para realizar “sniffing” y que puede utilizarse en redes inalámbricas. ¿Cuál es el nombre del el archivo que contiene la información interceptada?** 

+ **Panel izquierdo** Data Sources > SCHART.dd  > Vol 2  > Documents and setting > Application Data  > Ethereal
+ **Panel derecho superior** Recent
+ **Panel derecho inferior** Tab Text > Tab Indexed Text

![image](https://user-images.githubusercontent.com/50930193/137232353-53fd36d3-b1c2-480c-86ec-40c1a2eb71a0.png)

Allí se puede apreciar la ruta del archivo recientemente capturado, por ello hay que posicionarnos en el archivo  **C:\Documents and Settings\Mr. Evil\interception**

![image](https://user-images.githubusercontent.com/50930193/137232710-ad2c228c-d024-4796-8410-8de72da5108f.png)

-----------

**20. Al visualizar el archivo de texto revela una gran información sobre lo que se interceptó. ¿Cuál es el tipo de computadoras tenían las personas que estaban navegando en Internet?** 

En este caso, en el archivo anterior se puede apreciar que el sistema computadora utilizado fue Windows CE

 ![image](https://user-images.githubusercontent.com/50930193/137232848-d0398aca-0467-452e-a43b-867e566560b8.png)

-----------

**21. ¿ A qué sitios web la victima estuvo accediendo?**

En este caso, en el archivo anterior se puede apreciar los URL de los sitios web ubicando el texto referer:

![image](https://user-images.githubusercontent.com/50930193/137232912-d6fe6443-a734-49f0-badd-67d772e3909e.png)

Referer: 
+ http://mobile.msn.com
+ http://login.passport.net

-----------

**22. Ubique los principales usuarios que accedían a la web**

+ **Panel izquierdo** Web History
+ **Panel derecho superior** Columna Username

![image](https://user-images.githubusercontent.com/50930193/137233017-6412a6c4-7e54-493c-8ae9-1151ab331093.png)


Adicionalmente, en el panel derecho se pueden apreciar todo el historial web al cual se accedía 

Nótese los usuarios y los sitios web a donde accedía, en este caso solo tenemos registro para Mr. Evil

-----------

**23. Ubique la dirección de correo electrónico de yahoo que tenía el usuario Mr Evil.**

+ **Panel izquierdo**  Keyword Hits > Email Addresses
+ **Panel derecho superior** Aparece una expresión regular

![image](https://user-images.githubusercontent.com/50930193/137233285-c615dbe4-3058-43b6-aa2b-f6cab4d2b180.png)

Si se da doble click en dicho registro se accede en el mismo panel derecho a la siguiente pantalla se puede apreciar los archivos de las páginas y el contenido de cada una de ellas. Por favor navegue por cada registro

![image](https://user-images.githubusercontent.com/50930193/137233515-6cf5f32f-fa50-4d0a-9a06-9321951558bd.png)

Si se elige el tab de metadata se apreciará la ubicación de los archivos donde se hacen referencia

![image](https://user-images.githubusercontent.com/50930193/137233586-7c2e4ff4-aa48-4a24-94ab-8dd8215a7841.png)

-----------
 

**24. ¿Cuántos archivos ejecutables están en la papelera de reciclaje?**

+ **Panel izquierdo** Data Sources > SCHART.dd  > Vol 2  > RECYCLER

 
![image](https://user-images.githubusercontent.com/50930193/137233697-82a1a7a7-e49c-4510-b786-b7bb6b2db589.png)


 ----------- 

**25. ¿Esos archivos fueron realmente borrados?**

Antes de resónder, obtenga más información de donde se guarda la información en:

[Este enlace - Darc click aqui](https://www.forensafe.com/blogs/recyclebin.html)

En este caso, los archivos que fueron eliminados pueden aparecer en el archivo INFO2, en este caso no fueron realmente borrados.

 ![image](https://user-images.githubusercontent.com/50930193/137234344-2c1a3cc6-35f5-46a5-a84d-e47bef39fc87.png)

