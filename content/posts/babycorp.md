---
title: "BabyCorp 1 - WriteUP"
date: 2026-10-17
author: "wvverez"
tags: ["Daemon", "Gitea", "Local File Inclusion", "Reverse Shell"]
categories: ["Cybersecurity", "CTF"]
cover:
    alt: "BabyCorp 1 - WriteUP"
    caption: ""
    relative: false
---

Vamos a empezar lanzando trazas `ICMP` con la máquina víctima para comprobar que tengamos conectividad con ella, para ello empleamos `ping`.

```sh
❯ ping -c2 192.168.91.226
PING 192.168.91.226 (192.168.91.226) 56(84) bytes of data.
64 bytes from 192.168.91.226: icmp_seq=1 ttl=64 time=0.357 ms
64 bytes from 192.168.91.226: icmp_seq=2 ttl=64 time=0.377 ms
--- 192.168.91.226 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1015ms
rtt min/avg/max/mdev = 0.357/0.367/0.377/0.010 ms
```

Vemos que efectivamente tenemos conectividad, basándonos en el ttl de `64` podemos
pensar de primeras que estamos ante una máquina con SO Linux. Normalmente suele ser 64
Linux y 128 Windows, aunque el ttl es manipulable pero en entornos controlados de
aprendizaje suele ser así.

Vamos a seguir con un escaneo de red para enumerar puertos abiertos servicios y versiones
de dichos puertos abiertos, lo haremos sobre TCP.

```sh
❯ scan
[+] Interfaces (ej: eth0,ens33): eth0
[+] Escaneando eth0
[sudo] contraseña para kali:
[+] IP: 192.168.91.226 | MAC: 00:0c:29:f6:10:6c
[+] 192.168.91.226 -> Linux
[+] ¿Escanear 192.168.91.226 con nmap? (y/n): y
[+] Escaneando 192.168.91.226...
PORT STATE SERVICE VERSION
22/tcp open OpenSSH 9.2p1 Debian 2+deb12u9 (protocol 2.0)
3000/tcp open Golang net/http server
5000/tcp open Werkzeug httpd 3.1.8 (Python 3.11.2)
9000/tcp open ?
[+] Escaneo completado
```

Vemos 4 puertos abiertos, el 22 donde corre ssh, el 3000 el 5000 y 9000 en este punto por ssh
no se puede hacer nada podemos revisar el puerto 5000 que al correr `Werkzeug` se puede
pensar en alguna aplicación con algún framework conocido como Flask.
Tenemos la siguiente página:

<img width="1094" height="650" alt="image" src="https://github.com/user-attachments/assets/410e0b54-7a75-4a51-8c2c-b92f5915d74b" />


Con distintos planes y distintas formaciones sobre guarderías y la educación infantil. 

Bajando sobre la última parte de el menú vemos una parte un tanto interesante que es la única que podemos interactuar que es para agregar notas.

<img width="1048" height="622" alt="image" src="https://github.com/user-attachments/assets/eae2ca8c-3458-4b7f-b817-9f28363ec6ec" />

Y vemos también que podemos exportar las notas. Pero para esto nos indica abajo que
tenemos que estar logueados con una cuenta gratuita . Vamos a revisar los otros puertos
antes de probar nada. Vamos a revisar el 3000 donde corre Gitea.

Vemos que el usuario wvverez tiene un repositorio subido que aparentemente parece ser todo
el código de la web que tenemos por el 5000.


# Directory Path Traversal 

```sh

```
