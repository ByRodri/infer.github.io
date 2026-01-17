---
title: Primer post
date: 2026-01-17
categories: [Hacking, HackTheBox]
tags: [es]     # TAG names should always be lowercase
---

## Enumeración

Para empezar con el lab lo primero que voy a hacer es enumerar la ip que tenemos, para ello lo voy a hacer de la siguiente comando
```
sudo nmap -sS -sV -sC -p- --open --min-rate 5000 -oA nmap-report IP
```

Explicación del comando usado con el **nmap**:
***-sS*** -->  Esta opción especifica un escaneo de tipo SYN (TCP SYN scan), que envía un paquete SYN a los puertos de destino para determinar si están abiertos
***-sV*** --> Esta opción activa la detección de versiones de servicios en los puertos encontrados, intentando determinar qué servicios y versiones están corriendo en los puertos abiertos
***-sC*** --> Esta opción activa el escaneo de scripts de Nmap, que pueden proporcionar información adicional sobre los servicios encontrados
***-p-*** --> Escanea todos los puertos (1-65535) en lugar de solo los puertos comunes
***--open*** --> Muestra solo los puertos que están abiertos, lo que puede ayudar a reducir la cantidad de información mostrada en el resultado
***--min-rate 5000*** --> Establece la velocidad mínima de paquetes por segundo para el envío de paquetes. En este caso, se están enviando al menos 5000 paquetes por segundo
***-oA nmap-report*** --> Guarda la salida del escaneo en tres formatos diferentes: XML, gnmap (formato de Nmap) y formato de texto plano
***IP*** --> Ip a analizar

Al tirar el comando recibimos la siguiente información:
```
# Nmap 7.94SVN scan initiated Wed Apr 10 20:15:50 2024 as: nmap -sS -sV -sC -p- --open --min-rate 5000 -oA nmap-report 10.10.40.43
Nmap scan report for jack.thm (10.10.200.98)
Host is up (0.048s latency).
Not shown: 65533 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 3e:79:78:08:93:31:d0:83:7f:e2:bc:b6:14:bf:5d:9b (RSA)
|   256 3a:67:9f:af:7e:66:fa:e3:f8:c7:54:49:63:38:a2:93 (ECDSA)
|_  256 8c:ef:55:b0:23:73:2c:14:09:45:22:ac:84:cb:40:d2 (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Jack&#039;s Personal Site &#8211; Blog for Jacks writing adven...
| http-robots.txt: 1 disallowed entry 
|_/wp-admin/
|_http-generator: WordPress 5.3.2
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Wed Apr 10 20:16:11 2024 -- 1 IP address (1 host up) scanned in 20.70 seconds
```

Como podemos ver tenemos dos puerto abiertos, el puerto **22** y el puerto **80**, lo que destacaría de la búsqueda es que el nmap ya nos esta diciendo que tenemos un **wp-admin** asique ya podemos intuir que estamos frente a un WordPress.