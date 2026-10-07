---
title: "Bash scripting desde cero"
date: 2026-10-06
draft: false
categories:
  - Bash Scripting
tags:
  - Bash Scripting
  - Funciones
  - Linux
  - Variables
---

En este primer post de este nuevo blog voy a empezar hablando sobre la importancia de Bash para automatizar tareas y en ciberseguridad. 

En todo el ecosistema `Linux`, `Bash` (Bourne Again Shell) no es solo una interfaz para poder ejecutar comandos, es un motor para automatizaciones muy potente. Aprender a programar en Bash significa es pasar de ser un usuario estándar a alguien con la capacidad de gestionar sistemas o tareas complejas con simples archivos con texto.

El objetivo de este post es que cojas las bases para poder seguir aprendiendo y automatizando tareas con Bash.

# El Shebang 

Todos los scripts deberían comenzar con el **Shebang**. Esta línea le indica al propio kernel de `Linux` el interprete que tiene que usar para ejecutar el archivo.

```sh
#!/bin/bash
```

Mucha gente tiene dudas con esto por que en bash normalmente una `#` hace referencia a un comentario, y los comentarios son ignorados, por eso la gente duda de por que no se ignora el Shebang.

Lo que pasa es que para lenguajes como `Bash` o `Python` todo lo que siga a `#` es comentado. Pero para el `kernel` de Linux los primeros bytes que tiene un archivo son su identidad.

Cuando ejecutas un archivo