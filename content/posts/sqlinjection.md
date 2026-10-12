---
title: "SQL Injection"
date: 2026-10-06
author: "wvverez"
tags: ["SQL Injection", "SQL", "Web Security", "OWASP"]
categories: ["Cybersecurity", "Web Security"]
cover:
    alt: "SQL Injection"
    caption: "Introducción a SQL Injection"
    relative: false
---

He creado este proyecto para cada mes postear información sobre `vulnerabilidades`, me presento mi nick es @wvverez y soy un chico joven y entusiasta de el pentesting y el desarrollo de malware, también la programación y en general me causa mucha curiosidad la tecnología.

En mi tiempo libre me gusta investigar de forma autódidacta. Dicho esto vamos con el primer post en el que voy a explicar las vulnerabilidades SQL Injection.

Las inyecciones `SQL` ocurren cuando un atacante es capaz de mandar querys (consultas) maliciosas desde algún campo de la página web. Es decir si hay ciertas entradas que no sanitizan correctamente la información de el usuario. Esa consulta **sql** se ejecuta en la base de datos, lo que permite consultar tablas, columnas bases de datos y información confidencial. Hay diferentes tipos de inyecciones `SQL`.

- Inyecciones SQL basadas en errores: Este tipo abusa de los errores de el código SQL para sacar información. Por ejemplo, si una consulta SQL produce un mensaje de error específico, ese mensaje puede ser utilizado por el atacante para obtener detalles adicionales sobre el sistema. Es decir si haces una comparativa y da el error puedes usarlo para sacar cierta información.

- Inyecciones SQL basadas en `tiempo`: en este caso lo que hace el atacante es mandar una query que crea un retraso a la hora de sacar información, y va sacando datos en función de el tiempo de respuesta de la `db`.

- Inyecciones SQL basadas en uniones: Aquí se usa `UNION` para combinar 2 querys SQL dentro de una misma.

Estos son las más comunes pero existen muchos más tipos como `second order` y muchos más. Pero estás son las más comunes que encuentres en las aplicaciones web actuales.

# Inyecciones SQL basadas en Uniones

Para empezar dentro de todos los tipos vamos a empezar por las inyecciones sql basadas en Uniones así que para empezar vamos a empezar con este archivo simple.

```sh
<?php
// pa Habilitar los mensajes de error
ini_set('display_errors', '1');
ini_set('error_reporting', E_ALL); 

$server = "127.0.0.1";
$username = getenv('MYSQL_USER');
$password = getenv('MYSQL_PASSWORD');
$database = getenv('MYSQL_DATABASE');

$conn = new mysqli($server, $username, $password, $database);

if ($conn->connect_error) die('Error al conectarse a la base de datos: ' . $conn->connect_error);

$id = $_GET['id'] ?? '';
$query = "SELECT name FROM users WHERE id=$id";
$res = mysqli_query($conn, $query);

if (mysqli_num_rows($res)) {
	$row = mysqli_fetch_assoc($res);
	echo "Name: " . $row['name'];
} else {
	echo "The user with ID $id does not exist.";
}

mysqli_close($conn);
```

