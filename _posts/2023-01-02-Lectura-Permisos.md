---
title: Lectura de Permisos
layout: post
post-image: "/assets/images/Post/P3/P3.jpg"
description: En linux la lectura e interpretación de permisos es una parte fundamental.
search_exclude: false
tags: 
- LINUX
- PERMISOS

---

En este post se abordarán conceptos importantes como los diferentes tipos de permisos (usuario, grupo y otros) y cómo se combinan para determinar los niveles de acceso.

---

# Lectura de Permisos

Cuando estas en el interprete de comandos generalmente para listar archivos o directorios utilizamos el comando `ls -l` este comando nos arroja una lista de los directorios y archivos del sitio de donde estes ubicado. Los permisos se muestran de la siguiente forma `-rwx-wxr-x` esto puede variar dependiendo los permisos asignados.
A continuación una imagen de como leer los permisos de un directorio o archivo: 
![P3i1](/assets/images/Post/P3/P3i1.png)

---

# Interpretación de Permisos

Ahora bien ya conoces como leer los permisos de un archivo o directorio para poder intepretar mejor a que hace referencia esos permisos tenemos que revisar lo demás, con un gráfico lo entenderás mejor:

![P3i2](/assets/images/Post/P3/P3i2.png)

---

## Listar 

Ahora te dejo una pequeña lista sobre algunos comandos para listar archivos y directorios:

**Listar Archivos - Directorios**
Lista los archivos y directorios de un directorio específico. Si no se especifica ningún directorio, entonces se listará el contenido del directorio actual.

```shell
>ls               
Bash
```

**Listar en Formato largo**
Proporciona información detallada sobre los archivos y directorios, como el dueño, los permisos, etc.

```shell
> ls -l 
total 688
drwxr-xr-x 2 gabriel gabriel   4096 may  8 19:19 Cartas
drwxr-xr-x 3 gabriel gabriel   4096 mar  7 09:52 Clasificación de Cuentas
-rw-r--r-- 1 gabriel gabriel  17351 oct 16  2021 Doc.txt
-rw-r--r-- 1 gabriel gabriel 490640 nov 15  2022 DPI.pdf
```

**Listar en formato largo y elementos ocultos**
Mostrar todos los archivos, incluyendo los ocultos para obtener información.

```shell
> ls -la
total 8
drwxrwxr-x 3 usuario usuario  .
drwxr-xr-x 6 usuario usuario  ..
-rw-rw-r-- 1 usuario usuario  archivo1.txt
drwxrwxr-x 2 usuario usuario  directorio1
.hiddenfile 
```

**Listar en formato humano**
Este comando listará en formato largo todos los archivos y directorios del directorio actual con el tamaño de los archivos en formato humano.

```shell
> ls -lh 
total 688K
drwxr-xr-x 2 gabriel gabriel 4.0K may  8 19:19 Cartas
drwxr-xr-x 3 gabriel gabriel 4.0K mar  7 09:52 Clasificación de Cuentas
-rw-r--r-- 1 gabriel gabriel  17K oct 16  2021 Doc.txt
-rw-r--r-- 1 gabriel gabriel 480K nov 15  2022 DPI.pdf
```

Para saber más de este comando en su shell ingrese lo siguiente:

```shell
> man ls     
```

---
