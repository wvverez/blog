---
title: "Primeros pasos en AD"
date: 2026-10-06
draft: false
categories:
  - Active Directory
tags:
  - AD
  - Active Directory
  - Windows
  - Pentesting
---

Bienvenido a mi blog. Este será el primer post en el que vamos a introducir en directorio activo o `AD`.

`Active Directory (AD)` es un sistema creado por `Microsoft` que ayuda a las organizaciones a administrar y organizar sus ordenadores, usuarios y otros recursos también como impresoras y archivos. 

Realiza un seguimiento de quién es quién (nombres de usuario o contraseñas), también que dispositivos están en la red y a que ciertos recursos tiene acceso cada persona. 

En un caso real, AD se encarga de que ciertos empleados ejecuten ciertos programas o abran ciertos archivos, también permite que los usuarios inicien sesión una única vez, en resumen AD ayuda a mantener todo organizado y centralizado y seguro y fácil de gestionar.

Para este caso trabajaremos sobre esta máquina:

- https://go.microsoft.com/fwlink/p/?LinkID=2195167&clcid=0x409&culture=en-us&country=US
- RAM: 4GB
- CPU: 2 núcleos

Esto dependerá los recursos de cada uno y la plataforma de virtualización, personalmente trabajaré sobre `VMware` por comodidad.

El almacenamiento es muy relativo, si vas a darle mucha utilidad recomiendo entre [60-80GB] en adaptador dejaremos NAT y dejaremos la virtualización anidada habilitada
