# AlejandroBalanceadorAWS

# Índice
1. [Introducción](#introducción)
2. [Infraestructura](#infraestructura)
   - [VPC](#vpc)
   - [Subredes y Gateway](#subredes-y-gateway)
   - [Grupos de seguridad](#grupos-de-seguridad)
3. [Configuración del balanceador](#configuración-del-balanceador)
4. [Configuración de los servidores Apache](#configruacio-de-los-servidores-apache)
5. [Configuración de la base de datos](#configuracion-de-la-base-de-datos)
6. [Conclusión](#conclusion)
7. [Vídeo](#video)

## Introducción
#### En esta práctica se realizará el lanzamiento de una PilaLAMP en 3 niveles con 2 subredes, una pública y otra privada, en la capa 1 habrá un balanceador de carga con una subred pública y en la capa 2 dos servidores Apache y una base de datos en la capa 3 en la subred privada. Todo esto se realiza en un entorno de AWS, el cual se va a configurará previamente toda su infraestructura antes del lanzamiento de nuestra aplicación.

## Infraestructura
### VPCs
#### Creamos la VPC con la dirección de red 192.168.1.0/24:
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/390c28d9-8286-4e52-a3aa-99fce7b344dd)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/e8a43ffe-f151-44a4-a485-f1f01ba66aab)

### Subredes y Gateways
#### Para la 192.168.1.0 tendremos 2 subredes una para el balanceador y otra para los servidores Apache y el servidor de base de datos.
#### 192.168.1.0/25 Subred 1
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/7a4b2758-f4d3-456d-ad9d-77abcb7e4435)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/cec4edb7-2568-4148-95e3-4fb0b06501ea)

#### 192.168.1.128/25 Subred 2
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/327bdd37-1393-4dd4-9b6c-7113fd712217)
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
## Configuración de los servidores Apache
## Configuración de la base de datos
## Conclusión
## Vídeo




