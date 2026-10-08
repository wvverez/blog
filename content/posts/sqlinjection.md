---
title: "SQL Injection"
date: 2026-10-08
author: "wvverez"
description: "Introducción a SQL Injection, cómo funciona y cómo prevenirla."
tags: ["SQL Injection", "SQL", "Web Security", "OWASP"]
categories: ["Cybersecurity", "Web Security"]
cover:
    image: "https://raw.githubusercontent.com/wvverez/blog/main/themes/PaperMod/images/sql.png"
    alt: "SQL Injection"
    caption: "Introducción a SQL Injection"
    relative: false
---

He creado este proyecto para cada mes postear información sobre `vulnerabilidades`, me presento mi nick es @wvverez y soy un chico joven y entusiasta de el pentesting y el desarrollo de malware, también la programación y en general me causa mucha curiosidad la tecnología.

En mi tiempo libre me gusta investigar de forma autódidacta. Dicho esto vamos con el primer post en el que voy a explicar las vulnerabilidades SQL Injection.

Las inyecciones `SQL` ocurren cuando un atacante es capaz de mandar querys (consultas) maliciosas desde algún campo de la página web. Es decir si hay ciertas entradas que no sanitizan correctamente la información de el usuario. Esa consulta **sql** se ejecuta en la base de datos, lo que permite consultar tablas, columnas bases de datos y información confidencial. Hay diferentes tipos de inyecciones `SQL`.

- Inyecciones SQL basadas en errores: 
