# Autopsy en Windows

## Requisitos: Emplear la plataforma de TryHackme


1. Tener una cuenta en **TryHackMe**, si no la tiene tiene que crearse la cuenta desde este enlace <https://tryhackme.com/> (con la opción Join Me) 

![image](https://user-images.githubusercontent.com/50930193/136242833-6864e2e6-188b-4d59-9048-4bd9eb7dd45b.png)

2. Una vez que tengan una cuenta ingresar a la plataforma

![image](https://user-images.githubusercontent.com/50930193/136242775-612816cc-bfbd-464e-a560-c2095a145d3c.png)

3. Instalar el cliente openvpn  <https://openvpn.net/downloads/openvpn-connect-v3-windows.msi> que te permitirá probar las máquinas de la plataforma **TryHackMe**

![image](https://user-images.githubusercontent.com/50930193/136242890-d376dd23-646c-44a1-a0ee-e731d55fc7e4.png)

4. Desde https://tryhackme.com/access descargar el archivo de conexión VPN

![image](https://user-images.githubusercontent.com/50930193/136242946-af65ba5a-ff58-459d-ad97-8b992eb3df0e.png)

5. Importar el archivo descargado al cliente openvpn GUI

![image](https://user-images.githubusercontent.com/50930193/136243054-c39ef544-a8cb-406a-be0c-dfdc8babfe13.png)
![image](https://user-images.githubusercontent.com/50930193/136243117-16edef2e-8239-4465-8ab3-e9947bf567ff.png)

5. Ingresar a este enlace <https://tryhackme.com/room/autopsy2ze0>

![image](https://user-images.githubusercontent.com/50930193/136243181-b53563fc-9b5d-443d-985a-718794c0a2d1.png)

6. Iniciar la maquina que vamos a utilizar

![image](https://user-images.githubusercontent.com/50930193/136244942-23fbd6a3-1351-499e-8aa1-4a724aa2ce49.png)

7. Desde incio de Windows ejecutar el comando **mstsc.exe**

![image](https://user-images.githubusercontent.com/50930193/136277829-4e4483b0-4b7c-4cf1-92c6-00b78d32667e.png)

8. Conectarse con estos datos

![image](https://user-images.githubusercontent.com/50930193/136277853-447ddc71-e81d-4dd5-8c77-edbf7d7b00a8.png)

![image](https://user-images.githubusercontent.com/50930193/136277878-2c555fb4-c809-48fe-adc2-41cc0c2c4b45.png)

![image](https://user-images.githubusercontent.com/50930193/136278223-8be5a7ea-2c05-48d5-b616-8bd2bc28935e.png)

9. Tendrán como resultado esta consola donde trabajaremos 

![image](https://user-images.githubusercontent.com/50930193/136278318-7953e646-d9b4-4c81-8f17-ef8cece7cbbf.png)

10.En esa computadora tendrán estos recursos

![image](https://user-images.githubusercontent.com/50930193/136278857-04995292-b991-4af7-b499-1670351ce6f8.png)

11. Abrimos autopsy y elegimos **New Case**

![image](https://user-images.githubusercontent.com/50930193/136279367-bf700bdd-0c55-4e2d-8cce-61bf981994bc.png)

12. Ingresamos los datos del caso

![image](https://user-images.githubusercontent.com/50930193/136280086-681885ce-ab26-4b2c-a6c7-3bc4a54455e1.png)

![image](https://user-images.githubusercontent.com/50930193/136280279-ea2d9fa7-f622-4296-8d54-c5a5ae77c4eb.png)

13. Adiciona el origen de datos, es decir debemos hacer referencia a la imagen forense

![image](https://user-images.githubusercontent.com/50930193/136280458-342de477-bd87-421f-b401-173d8f765376.png)

![image](https://user-images.githubusercontent.com/50930193/136280687-38f46089-c769-4797-84c1-157816f5ac20.png)

14. Del mismo modo selecciona los módulos de ingesta necesarios

![image](https://user-images.githubusercontent.com/50930193/136282438-838cff24-5447-41ae-95d6-95118f3fedcc.png)

![image](https://user-images.githubusercontent.com/50930193/136280881-004f2384-8fda-477c-a652-a89808570fd7.png)

15. En la práctica este proceso anterior podría demorar dependiendo de los recursos que se dispongan, en ese sentido se recomienda que se cierre el caso y se abra el que ya existe en el equipo

![image](https://user-images.githubusercontent.com/50930193/136287389-3928ac2f-544a-41cc-924f-43adb9bcbc5f.png)


## Respuesta a las preguntas del caso


**1. What is the MD5 hash of the E01 image?**



![image](https://user-images.githubusercontent.com/50930193/136288950-1928d233-2ae7-451e-99ce-bdb7da0b7851.png)

**Respuesta:** 3f08c518adb3b5c1359849657a9b2079
-----------

**2. What is the computer account name?**

Buscar en Extracted Content -->Operating System Information section

![image](https://user-images.githubusercontent.com/50930193/136288890-56a053e5-f65c-4406-9094-317f8a625f00.png)

**Respuesta:** DESKTOP-0R59DJ3

-----------

**3. List all the user accounts. (alphabetical order)**
Check the Operating System User Account section:-

![image](https://user-images.githubusercontent.com/50930193/136288841-9cbdd898-a258-4cfd-90d3-d9ab4ca5ba65.png)

-----------

**4. Who was the last user to log into the computer? Sort by “Date Accessed”**



![image](https://user-images.githubusercontent.com/50930193/136288807-b06a0e88-9b26-47e0-a05d-bfbb203b2366.png)

**Respuesta:** sivapriya

-----------

**5. What was the IP address of the computer?**

Ir a Look@LAN in Program Files(x86) files . Look@Lan es una herramienta avanzada de monitoreo.

![image](https://user-images.githubusercontent.com/50930193/136299074-7d5f2391-0b4a-494e-bcec-936167f501de.png)


**Respuesta:** 192.168.130.216


-----------

**6. What was the MAC address of the computer? (XX-XX-XX-XX-XX-XX)**

![image](https://user-images.githubusercontent.com/50930193/136299096-3f58636c-352d-442b-869f-b427488ecd11.png)

**Respuesta:** 08–00–27–2c-c4-b9

-----------

**7. Name the network cards on this computer.**

Buscar **Ethernet** in **Keyword Search:**

![image](https://user-images.githubusercontent.com/50930193/136299125-9cafc2f2-e9b0-4b42-ac4b-6f7e7b3c9661.png)


**Respuesta:** Intel(R) PRO/1000 MT Desktop Adapter

-----------

**8. What is the name of the network monitoring tool?**

**Respuesta:** Look@LAN

-----------

**9. A user bookmarked a Google Maps location. What are the coordinates of the location?**

 Ir a la sección web bookmarker 

![image](https://user-images.githubusercontent.com/50930193/136299198-2e27b8a0-2b41-47c8-982c-64197e4c6a02.png)

**Respuesta:** 12°52'23.0"N 80°13'25.0"E

-----------

**10. A user has his full name printed on his desktop wallpaper. What is the user’s full name?**

En google buscar **donde se guardan los archivos de wallpaper**

![image](https://user-images.githubusercontent.com/50930193/136314830-2882a0e8-b5b6-4763-88fd-f5561a6ac5fe.png)

Luego navegar usuario por usario hasta ver un wallpaper que tenga esta información

Users -> shreya -> AppData -> Roaming -> Microsoft -> Windows -> Themes -> TranscodedWallpaper.jpg

![image](https://user-images.githubusercontent.com/50930193/136299299-0596ae22-cfb8-4138-a266-7d1aa6c341f9.png)


**Respuesta:** Anto Joshwa

-----------

**11. A user had a file on her desktop. It had a flag but she changed the flag using PowerShell. What was the first flag?**



En google buscar **donde se guardan el historial del powershell**

![image](https://user-images.githubusercontent.com/50930193/136294181-a879e1af-15e6-4dbb-a492-7453a5e63b19.png)

Revisar powershell history para cada usuario, para ello navegar usuario por usario hasta ver un wallpaper que tenga esta información

Users -> shreya -> AppData -> Roaming -> Microsoft -> Windows -> PowerShell -> PSReadLine -> ConsoleHost_history.txt

![image](https://user-images.githubusercontent.com/50930193/136294085-b6461153-ea53-46d8-aaca-78f641116c2f.png)

**Respuesta:** flag{HarleyQuinnForQueen}


-----------

**12. The same user found an exploit to escalate privileges on the computer. What was the message to the device owner?**

Ir al Destop de Shreya’s Desktop 

![image](https://user-images.githubusercontent.com/50930193/136314564-6ad5a4df-288b-47cb-96d1-faad3b147f2f.png)


**Respuesta:** flag{I-hacked-you}

-----------

**13. Two (2) hack tools focused on passwords were found in the system. What are the names of these tools? (alphabetical order)**

Normalmente Windows defender ubica ello, por eso ir a google buscar **donde se guardan el historial de windows defender**

![image](https://user-images.githubusercontent.com/50930193/136295597-1555a9dd-a3ae-45a6-898f-8e6547622f49.png)

Luego ir hasta esa ruta y ubicar los programas maliciosos
![image](https://user-images.githubusercontent.com/50930193/136295497-a4d321db-e8e1-444c-bff2-7bf52e9ecf1e.png)

**Respuesta:** Lazagne, Mimikatz

-----------

**14. There is a YARA file on the computer. Inspect the file. What is the name of the author?**

Buscar cual es la extensión de un archivo yara en google y luego Buscar archivos con extensión **.yar** o **.yara** usando **Keyword Search**

![image](https://user-images.githubusercontent.com/50930193/136298954-60411c0d-da68-429a-a296-c45b233e864d.png)



Si va a la ruta donde hacer referencia el archivo yar, no lo encontrará asi que queda buscar por otras palabras clave asociada al archivo que iubicó

Buscar archivos con extensión **.mimikatz_trunc** usando **Keyword Search**

![image](https://user-images.githubusercontent.com/50930193/136297308-68d545d6-5c18-4165-8afe-8e158e67291d.png)

**Respuesta:** Benjamin DELPY (gentilkiwi)

-----------

**15.  One of the users wanted to exploit a domain controller with an MS-NRPC based exploit. What is the filename of the archive that you found? (include the spaces in your answer)**
Check the Recent Documents section to find a document about Zerologon.

Buscar en que consiste la vulnerabilidad NSRPC 
![image](https://user-images.githubusercontent.com/50930193/136314715-ccd9214d-1faf-4b66-a1d2-8f716aefbdfa.png)


Buscar archivos con extensión **zerologon** usando **Keyword Search**

![image](https://user-images.githubusercontent.com/50930193/136297789-9db48f9e-a794-4171-8142-a02950d993b5.png)

**Respuesta:** 2.2.0 20200918 Zerologon encrypted.zip







