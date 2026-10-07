---
title: "Bash scripting básico"
date: 2026-10-06
draft: false

categories:
  - Bash Scripting

tags:
  - Bash Scripting
  - Funciones
  - Linux
  - Variables

cover:
  image: "https://raw.githubusercontent.com/wvverez/blog/main/themes/PaperMod/images/bash.png"
  alt: "Bash scripting básico"
  caption: "Bash scripting básico"
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

Cuando ejecutas un archivo, el kernel busca ese `magic number`. En el caso de el shebang busca los bytes hexadecimales 0x23 (#) y 0x21 (!).

Si lo encuentra, el kernel ya sabe que es un archivo binario como por ejemplo un .exe si no que va a ser un script que requiera un interprete.

Todo esto es una evidencia de el propio código fuente de `Linux`. 

En el archivo de el código fuente `fs/binfmt_script.c` en la función `load_script` sobre la línea 25 hace esta comprobación

```sh
// Si el archivo no empieza con #!, el Kernel devuelve un error de ejecución
if ((bprm->buf[0] != '#') || (bprm->buf[1] != '!'))
    return -ENOEXEC;
```

Sin esa línea el sistema va a ejecutar el archivo con la shell que tenga el usuario que puede ser sh,zsh etc...

Es decir si no pones el shebang y funciona, realmente no es por el kernel, es por tu shell.

El problema es si creas un script para usarlo con tipos de shell como zsh sin el shebang. 

# Variables 

A diferencia de otros lenguajes en `Bash` no hay espacios después de el simbolo `=` al asignar variables. Por ejemplo:

```sh
#!/bin/bash
NOMBRE="wvverez"
echo $NOMBRE
```

También es importante los argumentos que se le pasan a un script a la hora de ejecutarlo, esto en código tenemos los siguientes tipos:

```sh
$1, $2 : Primer y segundo argumento pasados al script.

$#: Número total de argumentos que se le pasan

$?: Código de salida del último comando ejecutado (0 significa éxito y 1 error normalmente).
```

# Redirecciones / Pipes

Bash también puede direccionar a archivos es decir la entrada de un comando puede ser la salida de otro, tenemos lo siguiente:

```sh
Pipes (|): Envía la salida de un comando a otro. Ejemplo: cat wvverez.txt | sort | uniq

Redirecciones (>, >>): Envía la salida a un archivo (sobrescribiendo con uno (IMPORTANTE) o añadiendo con 2).

Manejo de Errores (2>): Redirige los errores a un archivo específico para auditoría. (para redirigir errores lo más común es 2>/dev/null)
```

# Control y Lógica 

La automatización que tiene necesita muchas veces tomar ciertas decisiones, estas condiciones en bash se hacen con []. Y en bash a diferencia de muchos otros tenemos que dejar espacios entre los corchetes obligatoriamente.

```sh
if [ -f "/etc/passwd" ]; then
    echo "[+] El archivo de usuarios existe."
else
    echo "[!] Archivo no encontrado."
fi
```

También tenemos bucles for (loops) fundamentales para tareas repetitivas como escanear ciertos puertos o HostDiscovering por ejemplo.

```sh
#!/bin/bash
for i in {1..254}; do ping -c1 -w1 192.168.0.$i >/dev/null && echo "[+] La ip 192.168.0.$i está activa"; done
```

Dejaré una lista con lo necesario para que puedas guiarte y **EMPEZAR** a aprender y investigar sobre este maravilloso lenguaje.

# Argumentos

```sh
|Variable   |Desc
_____________________________________________________________
|$0,        |Nombre del script
|$1 - $9,   |Argumentos posicionales
|$#,        |Número de argumentos pasados
|$@,        |Todos los argumentos como una lista
|$?,        |Estado de salida del último comando (0 = éxito)
|$$,        |PID (ID de proceso) del script actual
```

# Condiciones 

NOTA: Acuerdate que siempre entre [] y entre espacios

```sh
    -f archivo: True si el archivo existe y es regular.

    -d carpeta: True si el directorio existe.

    -r / -w / -x: True si el archivo tiene permisos de lectura / escritura / ejecución.

**Cadenas (Strings)**

    z $var: True si la cadena está vacía.

    n $var: True si la cadena no está vacía.

    $var1 == $var2: Igualdad.

**Números**

    -eq: Igual a (equal)

    -ne: No igual (not equal)

    -lt: Menor que (less than)

    -gt: Mayor que (greater than)
```

# Estructuras de control (importante)

**Condicional if/else**

```sh
if [ condition ]; then
    # código
elif [ condition ]; then
    # código
else
    # código
fi
```

**Bucle For**

```sh
for item in {1..5}; do
    echo "Iteración: $item"
done
```

**Bucle While**

```
while [ condition ]; do
    # código
done
```

# Redirecciones

```sh
|Operador	|Acción
_______________________________________________________________
| >	        |Redirige salida estándar (sobrescribe archivo)
|>>	        |Redirige salida estándar (añade al final)
|2>	        |Redirige errores estándar
|&>     	|Redirige tanto salida como errores
|/dev/null	|El "agujero negro" de Linux (descarta las salidas)
```

Esto es todo para este primer breve post, Salud ^^
