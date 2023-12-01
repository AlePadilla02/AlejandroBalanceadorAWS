# AlejandroBalanceadorAWS

# Índice
1. [Introducción](#introducción)
2. [Infraestructura](#infraestructura)
   - [VPCs](#vpcs)
   - [Subredes](#subredes)
3. [Configuración de la máquina MariaDB](#configuración-de-la-máquina-mariadb)
   - [Instalación de MariaDB](#instalación-de-mariadb)
4. [Resultado](#resultado)

## Introducción
#### En esta práctica se realizará el lanzamiento de una PilaLAMP en 3 niveles, con un balanceador de carga de capa 1, dos servidores Apache en una red privada de capa 2 y una base de datos en otra red privada en capa 3. Todo esto se realiza en un entorno de AWS, el cual se va a configurar previamente toda su infraestructura antes de empezar a configurar el lanzamiento de nuestra aplicación.

## Infraestructura
### VPCs
#### Creamos las 2 VPCs, una para la red 192.168.1.0/24 y otra para la red 172.16.1.0/24:
#### 192.168.1.0
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/390c28d9-8286-4e52-a3aa-99fce7b344dd)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/e8a43ffe-f151-44a4-a485-f1f01ba66aab)

#### 176.16.1.0
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/40df2ff2-5f1f-440c-8893-55f670580158)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/43975c7e-341b-40b7-af64-d9bf59c11506)
### Subredes
#### Para la 192.168.1.0 tendremos 2 subredes una para el balanceador y otra para los servidores Apache y para la 172.16.1.0 exactamente igual.
#### 192.168.1.0/25 Subred 1
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/e5395a40-0436-45b9-b05b-cc3b5155b57d)

#### 192.168.1.128/25 Subred 2
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/2065ac57-3e25-4330-9434-b93232285d9c)

#### 172.16.1.0/25 Subred 1
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/97743857-2b47-424a-985d-0059b0f4b5be)

#### 172.16.1.128/25 Subred 2
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/3db92318-1b5a-498a-a20b-3664f98e4092)


### Interfaces de red
#### 

### Instancias
#### Una vez creadas las VPCs, a continuación se procederá a crear las instancias de cada servidor:
#### Balanceador
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/8e1d31a5-4e6e-4895-a92d-b57ddb1fcf46)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/98559998-7841-422f-a650-2a2a89b3a04c)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/54afc801-5036-4f47-8c75-106eebf74ffb)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/2822ebdf-cb3c-4685-8895-055154a9208b)

#### Apache 1
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/ed20d0f2-0835-440f-8d9f-7db501d70b63)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/eb813770-29fe-4deb-9231-dda4620b8473)
![image](https://github.com/AlePadilla02/AlejandroBalanceadorAWS/assets/146703765/deb75d9d-040e-4cc4-8658-2f0634d20df6)









