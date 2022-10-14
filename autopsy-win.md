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
