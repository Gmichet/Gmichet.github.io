---
title: Fundamentos SQL
layout: post
post-image: /assets/images/Post/P15/P15i0.jpg
description: Consultas en la base de datos chinook
tags:
- BASE DE DATOS

---

Anteriormente instalamos todo lo necesario para correr `SQL` [Instalación Mysql/MySQL-workbench](https://chispudo.github.io/blog/SQL)
Ahora llego el momento de la práctica antes que nada verificamos si tenemos corriendo el mysql:

---

### Indice

- [Recapitulación del post anterior](#recapitulación)
- [Realizar consultas básicas SQL](#consultas-sql-básicas)
- [Uso de consultas Select y From](#explicación-y-uso-de-select-from)
- [Ejemplos practicos de Select y From](#práctica-select-from)
- [Uso de 'Order by' para ordenar los registros](#uso-order-by)
- [Uso de la cláusula 'Where'](#uso-de-where)
- [Operadores de comparación](#operadores-de-comparación)
- [Operador 'Between' para datos numéricos](#operador-between)
- [Uso de operadores lógicos 'And' 'Or' y 'Not'](#información-adicional-filtros-and-or-not)
- [Combinación de operadores lógicos](#combinación-operadores-lógicos)
- [Filtrar por patrones](#filtrado-por-patrones)


#### Recapitulación

```shell
sudo service mysql status
```

- Si todo esta correcto y estoy seguro que sí, iniciamos `mysql` desde la consola de comandos (terminal):

```shell
mysql -u tu_usuario -p
```
- Dentro de **mysql** es hora de listar las bases de datos en este caso solo **chinook**:

```sql
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| Chinook            |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.01 sec)
```
- Seleccionando la base de datos a usar:

```sql
#USE nombre_base_de_datos;

mysql> USE Chinook;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
```
- Mostrar las tablas pertenecientes a esa base de datos:

```sql
mysql> SHOW TABLES;
+-------------------+
| Tables_in_Chinook |
+-------------------+
| Album             |
| Artist            |
| Customer          |
| Employee          |
| Genre             |
| Invoice           |
| InvoiceLine       |
| MediaType         |
| Playlist          |
| PlaylistTrack     |
| Track             |
+-------------------+
11 rows in set (0.01 sec)
```
---

## Consultas SQL básicas

Podemos ver varias tablas que podemos consultar de la base de datos **chinook**:

```sql
+-------------------+
| Tables_in_Chinook |
+-------------------+
| Album             |
| Artist            |
| Customer          |
| Employee          |
| Genre             |
| Invoice           |
| InvoiceLine       |
| MediaType         |
| Playlist          |
| PlaylistTrack     |
| Track             |
+-------------------+
```

* Ejemplo necesito consultar toda la tabla de clientes (**Customer**) de la base de datos **chinook**:

```sql
SELECT * FROM Customer;
```
-

### Explicación y Uso de SELECT, FROM

Cada vez que desee consultar una base de datos **SQL** utilizará lo siguiente:

* **SELECT**: Indica la columna a consultar de una tabla.
* **FROM**: Indica que tabla quiero consultar.

Entonces que sucedio cuando ejecute lo anterior, coloque **SELECT** indicando que quiero seleccionar algo ese algo es el `*` el asterisco es un comodín que sustituye varios caracteres. Entonces sustituyo todos los caracteres de acuerdo a la tabla que especificamos con el parámetro **FROM** que en este caso la tabla es **Customers** y la salida tendría que mostrar la tabla **Customers** y todas las columnas que pertenecen a esa tabla:

>Resumiendo: Selecciona (**SELECT**) todas `*` las columnas de la (**FROM**) tabla **Customer**

```sql
mysql> SELECT * FROM Customer;
+------------+------------+---------------+---------------------------------------------------+-------------------------------------------+-----------------------+--------+----------------+------------+---------------------+--------------------+-------------------------------+--------------+
| CustomerId | FirstName  | LastName      | Company                                           | Address                                   | City                  | State  | Country        | PostalCode | Phone               | Fax                | Email                         | SupportRepId |
+------------+------------+---------------+---------------------------------------------------+-------------------------------------------+-----------------------+--------+----------------+------------+---------------------+--------------------+-------------------------------+--------------+
|          1 | Luís       | Gonçalves     | Embraer - Empresa Brasileira de Aeronáutica S.A.  | Av. Brigadeiro Faria Lima, 2170           | São José dos Campos   | SP     | Brazil         | 12227-000  | +55 (12) 3923-5555  | +55 (12) 3923-5566 | luisg@embraer.com.br          |            3 |
|          2 | Leonie     | Köhler        | NULL                                              | Theodor-Heuss-Straße 34                   | Stuttgart             | NULL   | Germany        | 70174      | +49 0711 2842222    | NULL               | leonekohler@surfeu.de         |            5 |
|          3 | François   | Tremblay      | NULL                                              | 1498 rue Bélanger                         | Montréal              | QC     | Canada         | H2G 1A7    | +1 (514) 721-4711   | NULL               | ftremblay@gmail.com           |            3 |
|          4 | Bjørn      | Hansen        | NULL                                              | Ullevålsveien 14                          | Oslo                  | NULL   | Norway         | 0171       | +47 22 44 22 22     | NULL               | bjorn.hansen@yahoo.no         |            4 |
|          5 | František  | Wichterlová   | JetBrains s.r.o.                                  | Klanova 9/506                             | Prague                | NULL   | Czech Republic | 14700      | +420 2 4172 5555    | +420 2 4172 5555   | frantisekw@jetbrains.com      |            4 |
|          6 | Helena     | Holý          | NULL                                              | Rilská 3174/6                             | Prague                | NULL   | Czech Republic | 14300      | +420 2 4177 0449    | NULL               | hholy@gmail.com               |            5 |
|          7 | Astrid     | Gruber        | NULL                                              | Rotenturmstraße 4, 1010 Innere Stadt      | Vienne                | NULL   | Austria        | 1010       | +43 01 5134505      | NULL               | astrid.gruber@apple.at        |            5 |
|          8 | Daan       | Peeters       | NULL                                              | Grétrystraat 63                           | Brussels              | NULL   | Belgium        | 1000       | +32 02 219 03 03    | NULL               | daan_peeters@apple.be         |            4 |
|          9 | Kara       | Nielsen       | NULL                                              | Sønder Boulevard 51                       | Copenhagen            | NULL   | Denmark        | 1720       | +453 3331 9991      | NULL               | kara.nielsen@jubii.dk         |            4 |
|         10 | Eduardo    | Martins       | Woodstock Discos                                  | Rua Dr. Falcão Filho, 155                 | São Paulo             | SP     | Brazil         | 01007-010  | +55 (11) 3033-5446  | +55 (11) 3033-4564 | eduardo@woodstock.com.br      |            4 |
|         11 | Alexandre  | Rocha         | Banco do Brasil S.A.                              | Av. Paulista, 2022                        | São Paulo             | SP     | Brazil         | 01310-200  | +55 (11) 3055-3278  | +55 (11) 3055-8131 | alero@uol.com.br              |            5 |
|         12 | Roberto    | Almeida       | Riotur                                            | Praça Pio X, 119                          | Rio de Janeiro        | RJ     | Brazil         | 20040-020  | +55 (21) 2271-7000  | +55 (21) 2271-7070 | roberto.almeida@riotur.gov.br |            3 |
|         13 | Fernanda   | Ramos         | NULL                                              | Qe 7 Bloco G                              | Brasília              | DF     | Brazil         | 71020-677  | +55 (61) 3363-5547  | +55 (61) 3363-7855 | fernadaramos4@uol.com.br      |            4 |
|         14 | Mark       | Philips       | Telus                                             | 8210 111 ST NW                            | Edmonton              | AB     | Canada         | T6G 2C7    | +1 (780) 434-4554   | +1 (780) 434-5565  | mphilips12@shaw.ca            |            5 |
|         15 | Jennifer   | Peterson      | Rogers Canada                                     | 700 W Pender Street                       | Vancouver             | BC     | Canada         | V6C 1G8    | +1 (604) 688-2255   | +1 (604) 688-8756  | jenniferp@rogers.ca           |            3 |
|         16 | Frank      | Harris        | Google Inc.                                       | 1600 Amphitheatre Parkway                 | Mountain View         | CA     | USA            | 94043-1351 | +1 (650) 253-0000   | +1 (650) 253-0000  | fharris@google.com            |            4 |
|         17 | Jack       | Smith         | Microsoft Corporation                             | 1 Microsoft Way                           | Redmond               | WA     | USA            | 98052-8300 | +1 (425) 882-8080   | +1 (425) 882-8081  | jacksmith@microsoft.com       |            5 |
#etc
```
---

### Práctica SELECT, FROM

* **SELECT**: La palabra clave SELECT indica qué columnas devolver.
* **FROM**: Indica qué tabla consultar.
* **Saltos de línea**: Para poder visualizar mejor las consultas podemos utilizar un salto de línea, estos se pueden realizar presionando `ENTER` después de terminar los parámetros cada palabra clave _ejemplo_:

```sql
SELECT *
FROM customers;
``` 

* **;** El punto y coma indica que quiero finalizar la consulta.
.

**USO DE `,`**

La coma sirve para hacer distinciones sobre lo que quiero mostrar.

_Ejemplo: puedo ejecutar esta consulta para devolver los siguientes datos:_

* CustomerId: Identificador del cliente.
* FirstName: Primer nombre.
* City: Cuidad.
* Country: País.

```sql
mysql> SELECT CustomerId, FirstName, City, Country
    -> FROM Customer;
+------------+------------+-----------------------+----------------+
| CustomerId | FirstName  | City                  | Country        |
+------------+------------+-----------------------+----------------+
|          1 | Luís       | São José dos Campos   | Brazil         |
|          2 | Leonie     | Stuttgart             | Germany        |
|          3 | François   | Montréal              | Canada         |
|          4 | Bjørn      | Oslo                  | Norway         |
|          5 | František  | Prague                | Czech Republic |
|          6 | Helena     | Prague                | Czech Republic |
|          7 | Astrid     | Vienne                | Austria        |
|          8 | Daan       | Brussels              | Belgium        |
|          9 | Kara       | Copenhagen            | Denmark        |
|         10 | Eduardo    | São Paulo             | Brazil         |
#etc...
```
---

### Uso ORDER BY

El uso de la palabra clave **ORDER BY** es importante para organizar los datos que extrae de una tabla.

```sql
SELECT columnas
FROM tabla
ORDER BY columna1 [ASC|DESC], columna2 [ASC|DESC], ...
```

* **ORDER BY**: Ordena los registros en función de la columna especificada por defecto los ordena en orden ascendente:

```sql
mysql> SELECT CustomerId, City, Country
    -> FROM Customer
    -> ORDER BY CustomerId;
+------------+-----------------------+----------------+
| CustomerId | City                  | Country        |
+------------+-----------------------+----------------+
|          1 | São José dos Campos   | Brazil         |
|          2 | Stuttgart             | Germany        |
|          3 | Montréal              | Canada         |
|          4 | Oslo                  | Norway         |
|          5 | Prague                | Czech Republic |
|          6 | Prague                | Czech Republic |
|          7 | Vienne                | Austria        |
|          8 | Brussels              | Belgium        |
|          9 | Copenhagen            | Denmark        |
|         10 | São Paulo             | Brazil         |
#etc...
```
* En orden **descendente** seria así:

```sql
mysql> SELECT CustomerId, City, Country
    -> FROM Customer
    -> ORDER BY CustomerId DESC;
+------------+-----------------------+----------------+
| CustomerId | City                  | Country        |
+------------+-----------------------+----------------+
|         59 | Bangalore             | India          |
|         58 | Delhi                 | India          |
|         57 | Santiago              | Chile          |
|         56 | Buenos Aires          | Argentina      |
|         55 | Sidney                | Australia      |
|         54 | Edinburgh             | United Kingdom |
|         53 | London                | United Kingdom |
|         52 | London                | United Kingdom |
|         51 | Stockholm             | Sweden         |
|         50 | Madrid                | Spain          |
#etc...
```
---

### Uso de WHERE

La cláusula **WHERE** se usa para aplicar un filtro. 

>La cláusula **WHERE** indica el seleccionar el **nombre de una columna** e indicar a SQL que devuelva solo aquellos que contienen la **palabra clave de esa columna**.

_Ejemplo: En la tabla Customer quiero filtrar por el país de Canada_.

```sql
mysql> SELECT CustomerId, City, Country 
    -> FROM Customer 
    -> WHERE Country = 'Canada';
+------------+-------------+---------+
| CustomerId | City        | Country |
+------------+-------------+---------+
|          3 | Montréal    | Canada  |
|         14 | Edmonton    | Canada  |
|         15 | Vancouver   | Canada  |
|         29 | Toronto     | Canada  |
|         30 | Ottawa      | Canada  |
|         31 | Halifax     | Canada  |
|         32 | Winnipeg    | Canada  |
|         33 | Yellowknife | Canada  |
+------------+-------------+---------+
```

* _Ejemplo 2: Seleccionamos todas las columnas de la **Employee**, pero solo se incluirán en los resultados aquellos registros cuyo **Title** sean "IT Staff"._

```sql
mysql> SHOW TABLES;
+-------------------+
| Tables_in_Chinook |
+-------------------+
| Album             |
| Artist            |
| Customer          |
| Employee          |
| Genre             |
| Invoice           |
| InvoiceLine       |
| MediaType         |
| Playlist          |
| PlaylistTrack     |
| Track             |
+-------------------+
11 rows in set (0.00 sec)

mysql> SELECT * FROM Employee;
+------------+----------+-----------+---------------------+-----------+---------------------+---------------------+-----------------------------+------------+-------+---------+------------+-------------------+-------------------+--------------------------+
| EmployeeId | LastName | FirstName | Title               | ReportsTo | BirthDate           | HireDate            | Address                     | City       | State | Country | PostalCode | Phone             | Fax               | Email                    |
+------------+----------+-----------+---------------------+-----------+---------------------+---------------------+-----------------------------+------------+-------+---------+------------+-------------------+-------------------+--------------------------+
|          1 | Adams    | Andrew    | General Manager     |      NULL | 1962-02-18 00:00:00 | 2002-08-14 00:00:00 | 11120 Jasper Ave NW         | Edmonton   | AB    | Canada  | T5K 2N1    | +1 (780) 428-9482 | +1 (780) 428-3457 | andrew@chinookcorp.com   |
|          2 | Edwards  | Nancy     | Sales Manager       |         1 | 1958-12-08 00:00:00 | 2002-05-01 00:00:00 | 825 8 Ave SW                | Calgary    | AB    | Canada  | T2P 2T3    | +1 (403) 262-3443 | +1 (403) 262-3322 | nancy@chinookcorp.com    |
|          3 | Peacock  | Jane      | Sales Support Agent |         2 | 1973-08-29 00:00:00 | 2002-04-01 00:00:00 | 1111 6 Ave SW               | Calgary    | AB    | Canada  | T2P 5M5    | +1 (403) 262-3443 | +1 (403) 262-6712 | jane@chinookcorp.com     |
|          4 | Park     | Margaret  | Sales Support Agent |         2 | 1947-09-19 00:00:00 | 2003-05-03 00:00:00 | 683 10 Street SW            | Calgary    | AB    | Canada  | T2P 5G3    | +1 (403) 263-4423 | +1 (403) 263-4289 | margaret@chinookcorp.com |
|          5 | Johnson  | Steve     | Sales Support Agent |         2 | 1965-03-03 00:00:00 | 2003-10-17 00:00:00 | 7727B 41 Ave                | Calgary    | AB    | Canada  | T3B 1Y7    | 1 (780) 836-9987  | 1 (780) 836-9543  | steve@chinookcorp.com    |
|          6 | Mitchell | Michael   | IT Manager          |         1 | 1973-07-01 00:00:00 | 2003-10-17 00:00:00 | 5827 Bowness Road NW        | Calgary    | AB    | Canada  | T3B 0C5    | +1 (403) 246-9887 | +1 (403) 246-9899 | michael@chinookcorp.com  |
|          7 | King     | Robert    | IT Staff            |         6 | 1970-05-29 00:00:00 | 2004-01-02 00:00:00 | 590 Columbia Boulevard West | Lethbridge | AB    | Canada  | T1K 5N8    | +1 (403) 456-9986 | +1 (403) 456-8485 | robert@chinookcorp.com   |
|          8 | Callahan | Laura     | IT Staff            |         6 | 1968-01-09 00:00:00 | 2004-03-04 00:00:00 | 923 7 ST NW                 | Lethbridge | AB    | Canada  | T1H 1Y8    | +1 (403) 467-3351 | +1 (403) 467-8772 | laura@chinookcorp.com    |
+------------+----------+-----------+---------------------+-----------+---------------------+---------------------+-----------------------------+------------+-------+---------+------------+-------------------+-------------------+--------------------------+

```

* Mostrando solo "IT Staff":

```sql
mysql> SELECT * 
    -> FROM Employee
    -> WHERE Title = 'IT Staff';

+------------+----------+-----------+----------+-----------+---------------------+---------------------+-----------------------------+------------+-------+---------+------------+-------------------+-------------------+------------------------+
| EmployeeId | LastName | FirstName | Title    | ReportsTo | BirthDate           | HireDate            | Address                     | City       | State | Country | PostalCode | Phone             | Fax               | Email                  |
+------------+----------+-----------+----------+-----------+---------------------+---------------------+-----------------------------+------------+-------+---------+------------+-------------------+-------------------+------------------------+
|          7 | King     | Robert    | IT Staff |         6 | 1970-05-29 00:00:00 | 2004-01-02 00:00:00 | 590 Columbia Boulevard West | Lethbridge | AB    | Canada  | T1K 5N8    | +1 (403) 456-9986 | +1 (403) 456-8485 | robert@chinookcorp.com |
|          8 | Callahan | Laura     | IT Staff |         6 | 1968-01-09 00:00:00 | 2004-03-04 00:00:00 | 923 7 ST NW                 | Lethbridge | AB    | Canada  | T1H 1Y8    | +1 (403) 467-3351 | +1 (403) 467-8772 | laura@chinookcorp.com  |
```
----

### Operadores de Comparación

Estos operadores de comparación sirven para el filtrado de datos numéricos y de fecha y hora, a continuación una tabla con los operadores:

| Operador | Usar |
| -------- | ---- | 
| < | Menos que  |
| > | Más grande que |
| = | Igual a | 
| <= | Menos que o igual a |
| >= | Mayor qué o igual a |
| <> | No igual a |
| != | No igual a | 

>Estos operadores de comparación se utilizan en la cláusula **WHERE** al final de una consulta.

_Ejemplo:  La siguiente consulta usa el operador `>` para filtrar la columna de fecha de nacimiento._

```sql
mysql> SELECT FirstName, LastName, BirthDate
    -> FROM Employee
    -> WHERE BirthDate > '1970-01-01';
+-----------+----------+---------------------+
| FirstName | LastName | BirthDate           |
+-----------+----------+---------------------+
| Jane      | Peacock  | 1973-08-29 00:00:00 |
| Michael   | Mitchell | 1973-07-01 00:00:00 |
| Robert    | King     | 1970-05-29 00:00:00 |
+-----------+----------+---------------------+
3 rows in set (0.00 sec)
```
---

### Operador BETWEEN

Este operador se suele utilizar para datos numéricos y también para datos de fecha y hora.

* **BETWEEN** (Entre): Filtra números o fechas dentro de un intervalo.

_Ejemplo: Quiero buscar los Artistas cuyo ID estén entre 100 y 110 de la base de datos Chinook:_

```sql
mysql> SELECT ArtistId, Name
    -> FROM Artist
    -> WHERE ArtistId BETWEEN '100' AND '110';
+----------+-------------------------+
| ArtistId | Name                    |
+----------+-------------------------+
|      100 | Lenny Kravitz           |
|      101 | Lulu Santos             |
|      102 | Marillion               |
|      103 | Marisa Monte            |
|      104 | Marvin Gaye             |
|      105 | Men At Work             |
|      106 | Motörhead               |
|      107 | Motörhead & Girlschool  |
|      108 | Mônica Marianno         |
|      109 | Mötley Crüe             |
|      110 | Nirvana                 |
+----------+-------------------------+
11 rows in set (0.00 sec)
```
---

### Información Adicional filtros AND, OR, NOT

* **AND**: Se utiliza para filtrar en dos condiciones. Especifica que ambas condiciones deben cumplirse simultáneamente.

```sql
mysql> SELECT * FROM Customer
    -> WHERE Country = 'Canada' AND SupportRepId = '3';
+------------+-----------+----------+---------------+------------------------+-------------+-------+---------+------------+-------------------+-------------------+------------------------+--------------+
| CustomerId | FirstName | LastName | Company       | Address                | City        | State | Country | PostalCode | Phone             | Fax               | Email                  | SupportRepId |
+------------+-----------+----------+---------------+------------------------+-------------+-------+---------+------------+-------------------+-------------------+------------------------+--------------+
|          3 | François  | Tremblay | NULL          | 1498 rue Bélanger      | Montréal    | QC    | Canada  | H2G 1A7    | +1 (514) 721-4711 | NULL              | ftremblay@gmail.com    |            3 |
|         15 | Jennifer  | Peterson | Rogers Canada | 700 W Pender Street    | Vancouver   | BC    | Canada  | V6C 1G8    | +1 (604) 688-2255 | +1 (604) 688-8756 | jenniferp@rogers.ca    |            3 |
|         29 | Robert    | Brown    | NULL          | 796 Dundas Street West | Toronto     | ON    | Canada  | M6J 1V1    | +1 (416) 363-8888 | NULL              | robbrown@shaw.ca       |            3 |
|         30 | Edward    | Francis  | NULL          | 230 Elgin Street       | Ottawa      | ON    | Canada  | K2P 1L7    | +1 (613) 234-3322 | NULL              | edfrancis@yachoo.ca    |            3 |
|         33 | Ellie     | Sullivan | NULL          | 5112 48 Street         | Yellowknife | NT    | Canada  | X1A 1N6    | +1 (867) 920-2233 | NULL              | ellie.sullivan@shaw.ca |            3 |
+------------+-----------+----------+---------------+------------------------+-------------+-------+---------+------------+-------------------+-------------------+------------------------+--------------+
5 rows in set (0.00 sec)
```

* **OR**: También conecta dos condiciones pero especifica que puede cumplirse cualquiera de ellas. Devuelve como resultado la condición que se cumple puede ser la primera condición, la segunda o ambas.

```sql
mysql> SELECT * FROM Customer
    -> WHERE Country = 'USA' OR Country = 'Canada';
+------------+-----------+------------+-----------------------+---------------------------+----------------+-------+---------+------------+-------------------+-------------------+--------------------------+--------------+
| CustomerId | FirstName | LastName   | Company               | Address                   | City           | State | Country | PostalCode | Phone             | Fax               | Email                    | SupportRepId |
+------------+-----------+------------+-----------------------+---------------------------+----------------+-------+---------+------------+-------------------+-------------------+--------------------------+--------------+
|          3 | François  | Tremblay   | NULL                  | 1498 rue Bélanger         | Montréal       | QC    | Canada  | H2G 1A7    | +1 (514) 721-4711 | NULL              | ftremblay@gmail.com      |            3 |
|         14 | Mark      | Philips    | Telus                 | 8210 111 ST NW            | Edmonton       | AB    | Canada  | T6G 2C7    | +1 (780) 434-4554 | +1 (780) 434-5565 | mphilips12@shaw.ca       |            5 |
|         15 | Jennifer  | Peterson   | Rogers Canada         | 700 W Pender Street       | Vancouver      | BC    | Canada  | V6C 1G8    | +1 (604) 688-2255 | +1 (604) 688-8756 | jenniferp@rogers.ca      |            3 |
|         16 | Frank     | Harris     | Google Inc.           | 1600 Amphitheatre Parkway | Mountain View  | CA    | USA     | 94043-1351 | +1 (650) 253-0000 | +1 (650) 253-0000 | fharris@google.com       |            4 |
|         17 | Jack      | Smith      | Microsoft Corporation | 1 Microsoft Way           | Redmond        | WA    | USA     | 98052-8300 | +1 (425) 882-8080 | +1 (425) 882-8081 | jacksmith@microsoft.com  |            5 |
|         18 | Michelle  | Brooks     | NULL                  | 627 Broadway              | New York       | NY    | USA     | 10012-2612 | +1 (212) 221-3546 | +1 (212) 221-4679 | michelleb@aol.com        |            3 |
|         19 | Tim       | Goyer      | Apple Inc.            | 1 Infinite Loop           | Cupertino      | CA    | USA     | 95014      | +1 (408) 996-1010 | +1 (408) 996-1011 | tgoyer@apple.com         |            3 |
|         20 | Dan       | Miller     | NULL                  | 541 Del Medio Avenue      | Mountain View  | CA    | USA     | 94040-111  | +1 (650) 644-3358 | NULL              | dmiller@comcast.com      |            4 |
|         21 | Kathy     | Chase      | NULL                  | 801 W 4th Street          | Reno           | NV    | USA     | 89503      | +1 (775) 223-7665 | NULL              | kachase@hotmail.com      |            5 |
|         22 | Heather   | Leacock    | NULL                  | 120 S Orange Ave          | Orlando        | FL    | USA     | 32801      | +1 (407) 999-7788 | NULL              | hleacock@gmail.com       |            4 |
|         23 | John      | Gordon     | NULL                  | 69 Salem Street           | Boston         | MA    | USA     | 2113       | +1 (617) 522-1333 | NULL              | johngordon22@yahoo.com   |            4 |
#etc...
```

* **NOT**: El operador 'NOT' sólo funciona con una condición y no con varias. El operador NOT niega una condición.
Devuelve todos los registros que no coincidan con la condición especificada en la consulta.

```sql
mysql> SELECT FirstName, Country, Email
    -> FROM Customer
    -> WHERE NOT Country = 'Canada';
+------------+----------------+-------------------------------+
| FirstName  | Country        | Email                         |
+------------+----------------+-------------------------------+
| Luís       | Brazil         | luisg@embraer.com.br          |
| Leonie     | Germany        | leonekohler@surfeu.de         |
| Bjørn      | Norway         | bjorn.hansen@yahoo.no         |
| František  | Czech Republic | frantisekw@jetbrains.com      |
| Helena     | Czech Republic | hholy@gmail.com               |
| Astrid     | Austria        | astrid.gruber@apple.at        |
| Daan       | Belgium        | daan_peeters@apple.be         |
| Kara       | Denmark        | kara.nielsen@jubii.dk         |
| Eduardo    | Brazil         | eduardo@woodstock.com.br      |
| Alexandre  | Brazil         | alero@uol.com.br              |
| Roberto    | Brazil         | roberto.almeida@riotur.gov.br |
| Fernanda   | Brazil         | fernadaramos4@uol.com.br      |
| Frank      | USA            | fharris@google.com            |
| Jack       | USA            | jacksmith@microsoft.com       |
| Michelle   | USA            | michelleb@aol.com             |
#etc...
```
.

* **RESUMEN OPERADORES**

	* El operador **AND** requiere que dos condiciones sean verdaderas simultáneamente, 
	* El operador **OR** requiere que una o ambas condiciones sean verdaderas. 
	* El operador **NOT** niega una condición. 

---

#### Combinación Operadores lógicos

Los operadores lógicos pueden combinarse en los filtros.

```sql
mysql> SELECT FirstName, Email, Country 
     -> FROM Customer 
     -> WHERE NOT Country = 'USA' AND NOT Country = 'Canada';
+------------+-------------------------------+----------------+
| FirstName  | Email                         | Country        |
+------------+-------------------------------+----------------+
| Luís       | luisg@embraer.com.br          | Brazil         |
| Leonie     | leonekohler@surfeu.de         | Germany        |
| Bjørn      | bjorn.hansen@yahoo.no         | Norway         |
| František  | frantisekw@jetbrains.com      | Czech Republic |
| Helena     | hholy@gmail.com               | Czech Republic |
| Astrid     | astrid.gruber@apple.at        | Austria        |
| Daan       | daan_peeters@apple.be         | Belgium        |
| Kara       | kara.nielsen@jubii.dk         | Denmark        |
| Eduardo    | eduardo@woodstock.com.br      | Brazil         |
| Alexandre  | alero@uol.com.br              | Brazil         |
| Roberto    | roberto.almeida@riotur.gov.br | Brazil         |
| Fernanda   | fernadaramos4@uol.com.br      | Brazil         |
| João       | jfernandes@yahoo.pt           | Portugal       |
#etc...
```
---

### Filtrado por Patrones

Se puede filtrar según cierto patrón "Ordenamiento de cosas que se repiten de manera lógica".
_Ejemplo: Podemos identificar entradas que comiencen o terminen con un carácter o caracteres determinados._ 

Para filtrar por patrones utilizamos **comodines**:

Muestra los comodines utilizados en SQL para el filtrado de patrones:

| Comodín | Descripción                                | Uso                                              |
| ------- | ------------------------------------------ | ------------------------------------------------ |
| %       | Representa cualquier conjunto de caracteres | **LIKE** 'patrón`%`' (coincidencia en base a la posición)      |
| _       | Representa un único carácter                | **LIKE** 'patr`_`n' (coincidencia en una posición)    |
| []      | Representa un conjunto de caracteres        | **LIKE** 'patr`[aeiou]`n' (coincidencia con vocales) |
| [^]     | Representa un conjunto negado de caracteres | **LIKE** 'patr`[^aeiou]`n' (exclusión de vocales)    |

Estos comodines se utilizan junto con la cláusula `LIKE` en SQL para realizar filtrados de patrones en consultas. Por ejemplo, si tienes una columna llamada "nombre" y deseas encontrar todos los registros cuyo nombre comienza con "A", puedes usar el comodín `%` de la siguiente manera:

```sql
SELECT * FROM tabla WHERE nombre LIKE 'A%';
```
.

Esto devolverá todos los registros cuyo nombre comienza con "A". Puedes combinar múltiples comodines y caracteres para crear patrones más complejos y específicos en tus consultas SQL.

* _Ejemplo: Si queremos buscar en la tabla **Customer** en la columna **State** cuya abreviatura sea "NY", "Nv", etc._

```sql
mysql> SELECT FirstName, State, Country
    -> FROM Customer
    -> WHERE State LIKE 'N_';
+-----------+-------+---------+
| FirstName | State | Country |
+-----------+-------+---------+
| Michelle  | NY    | USA     |
| Kathy     | NV    | USA     |
| Martha    | NS    | Canada  |
| Ellie     | NT    | Canada  |
+-----------+-------+---------+
4 rows in set (0.00 sec)
```

