# AlejandroBalanceadorAWS

# Índice
1. [Introducción](#introducción)
2. [Infraestructura](#infraestructura)
   - [VPC](#vpc)
   - [Subredes y Gateways](#subredes-y-gateways)
   - [Grupos de seguridad](#grupos-de-seguridad)
3. [Configuración del balanceador](#configuración-del-balanceador)
4. [Configuración de la base de datos](#configuración-de-la-base-de-datos)
5. [Configuración de los servidores Apache](#configruación-de-los-servidores-apache)
6. [Conclusión](#conclusión)
7. [Vídeo](#vídeo)

## Introducción
#### En esta práctica se realizará el lanzamiento de una PilaLAMP en 3 niveles con 2 subredes, una pública y otra privada, en la capa 1 habrá un balanceador de carga con una subred pública con la IP (192.168.1.20) y en la capa 2 dos servidores Apache con las IPs (192.168.1.179 y 192.168.1.221) y una base de datos en la capa 3 con la IP (192.168.1.160) en la subred privada. Todo esto se realiza en un entorno de AWS, el cual se va a configurará previamente toda su infraestructura antes del lanzamiento de la aplicación web.

## Infraestructura
### VPCs
#### Creamos la VPC con la dirección de red 192.168.1.0/24:
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/390c28d9-8286-4e52-a3aa-99fce7b344dd)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/e8a43ffe-f151-44a4-a485-f1f01ba66aab)

### Subredes y Gateways
#### Para la 192.168.1.0 tendremos 2 subredes una para el balanceador y otra para los servidores Apache y el servidor de base de datos.
#### 192.168.1.0/25 Subred 1
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/7a4b2758-f4d3-456d-ad9d-77abcb7e4435)
#### Gateway a internet:
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/cec4edb7-2568-4148-95e3-4fb0b06501ea)

#### 192.168.1.128/25 Subred 2
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/327bdd37-1393-4dd4-9b6c-7113fd712217)
#### Gateway NAT:
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/43895bca-9a0b-4779-bf0f-b88697e17072)

### Grupos de seguridad
#### Grupo de seguridad del balanceador, permite las peticiones HTTP y HTTPS, el acceso ssh y ping con las máquinas backend:
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/d309de06-a2fb-435a-8366-f04bc7b0c582)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/8c26f5f3-8f93-4f51-b0d6-a1a2e35f8175)

#### Grupo de seguridad de los servidores Apache, permite las peticiones HTTP y HTTPS, el acceso ssh, ping tanto con el balanceador como con la base de datos y acceso a la base de datos:
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/59d732a3-c659-4ba2-8dc9-eb487957206d)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/9d2f1f0f-b764-4e98-bedb-69d4e15c4f90)

#### Grupo de seguridad base de datos, permite el ping con las máquinas backend, el acceso ssh y el acceso a la base de datos por parte de las máquinas Apache.
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/96ae6a2b-80ff-4702-be62-9339c3509495)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/436218b2-b490-427f-940d-eb35162b0cad)


## Configuración del balanceador
#### Hay que conectarse vía ssh al balanceador desde la máquina anfitrión. A partir de ahí empieza la configuración del balanceador:
#### Se actualizan los repositorios con sudo apt update, instalar apache y habilitar los módulos siguientes:
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/4309c609-2c9d-4193-9dea-bc3c171ba7ce)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/66e210e7-bdae-4fa4-bb70-55d64acb0cee)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/0f87b90f-dc9f-4d8d-bc83-6a742524152a)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/1d61388b-8492-48be-8098-5b2d480bf0c8)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/7959ca7f-62bb-41b9-ba8f-e58aac59cd20)

#### Registrar un dominio en este caso en la página noip asociado a la IP elástica de nuestro balanceador:
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/8624150e-7939-40e5-92ca-99cf8d189f74)

#### Una vez realizado todo lo anterior, se debe descargar el paquete snap con el cual permitirá la descarga del paquete core para poder instalar certbot y obtener el certificado siguiendo sus respectivos pasos:

![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/19e2192e-e98b-4488-a991-bd8b77329019)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/56e281f9-15fb-4280-9463-d59ffef069bb)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/55c2a254-7869-4a96-b0ba-001077e8c9be)
#### En este caso ya estaba creado pero aparecen una serie de preguntas para realizar el certificado:
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/fa82e0ed-d6f5-4c8b-b6e2-97862df658b9)

#### Hacer una copia de dicho certificado y modificarlo de la siguiente manera, añadiendo las IPs de los servidores backend además de comentar el DocumentRoot y editar la línea ServerAdmin para poner el correo del admin:
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/5d11ef53-a924-4f86-b3be-6126cc5acb09)
#### Reiniciar el servicio Apache y comprobar que funciona dicho dominio:
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/3e236ed5-6493-4c8d-94d3-7f2535f3e5dd)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/190da803-ae4b-428e-8a75-ed41345b2708)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/a4afbf03-2ce7-4e74-95bc-5f4338c773ea)
## Configuración de los servidores Apache
#### Desde el balanceador, mandaremos vía scp la clave para poder conectarnos vía ssh. Una vez ahí, con los grupos de seguridad, estarán configurados para tener acceso a Internet para descargar Apache y el paquete git, que una vez instalado se realizarán las configuraciones necesarias para quitarles el acceso a Internet:
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/6b2e6539-e7aa-4c7e-a71b-c36547607b8c)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/a95714bc-f1df-460c-af38-b2030446a871)

#### Hacer uso de git clone del repositorio de la aplición de usuarios y configurar en el directorio src el fichero config.php de la siguiente manera:
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/269fa412-38cc-4e05-ae44-83bce870c1f0)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/ebb54135-bded-4c5b-8f36-f10bec0e8a15)

#### Hacer una copia del fichero 000-default.conf en /etc/apache2/sites-available y editar el DocumentRoot con la ruta de la aplicación de usuarios:
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/1bbfa3ca-712a-4d20-a415-462b3cb79b6b)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/29f5ac57-b603-47c1-9746-c46816b62415)

#### Todos estos pasos se realizan en ambos Apache y una vez realizados, tocaría reiniciar el servicio Apache y comprobar que funciona dicha aplicación
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/a4411d36-ac45-4054-9c30-9c758e0b47ef)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/9953dab4-ae3f-409b-8f80-bd0906bd4a0c)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/afe42e89-4077-45d7-8143-ee5a5cd39763)

## Configuración de la base de datos
#### Desde el balanceador, mandaremos vía scp la clave para poder conectarnos vía ssh. Una vez ahí, con los grupos de seguridad, estarán configurados para tener acceso a Internet para descargar mariadb-server, que una vez instalado se realizarán las configuraciones necesarias para quitarles el acceso a Internet:
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/a5027937-54a9-4c23-987b-96c9ef7fb8fe)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/ea076536-2fc1-4e95-a630-dc5c1b8479a8)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/a0326deb-5614-4e79-a5c4-1c6ccd032396)

#### Una vez instalado todo, hay que crear la base de datos y el usuario para que pueda acceder desde ambos Apache, dándole los permisos necesarios para que esto suceda:
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/a5250370-af31-44f4-87f1-b62bfb266197)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/9eeef40a-def1-4eca-b0b1-244ab22fe6a0)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/93a4e1d5-00e3-431e-9764-0d99efd9a615)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/998e241d-caf3-40c1-8990-ad2449d8c423)

#### Por último quedaría configurar el bind-address de la base de datos en /etc/mysql/mariadb.conf.d/50-server.cnf y poner la IP del servidor de base de datos para que puedan conectarse las máquinas Apache:
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/9b318a1e-59c5-4b17-97c2-f39bbed1c6c1)

#### Reniciar el servicio mariadb:
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/7e2f851a-012f-4146-ba1d-4ffa6fe8c25f)

## Conclusión
## Vídeo




