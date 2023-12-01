---
title: Subnetting de Redes
layout: post
post-image: /assets/images/Post/P12/P12i0.png
description: División de redes en subredes más pequeñas
tags:
- REDES

---

La técnica de subnetting es fundamental  para dividir una red en subredes más pequeñas mejorando asi el manejo de la misma.
Esta práctica de división de redes se lográ mediante **máscaras de red**, que permiten definir dos cosas importantes:

- Bits correspondientes a la red
- Bits correspondientes al host


### Indice


---

# Dirección IPv4

La dirección IPv4 consiste en cuatro octetos separados por puntos. Con una longitud máxima de 32 bits.

![Rango](/assets/images/Post/P12/P12i2.png)

## Clases y Rangos

Cada dirección IPv4 esta definida por rangos de red en los que opera. Estos rangos de red están determinados por un prefijo de red `/`. 

Ejemplo:

```shell
192.168.0.22/24 # En donde `/24` es el prefijo de red 
```
_

En la siguiente tabla se observa un rango de valores para cada rango de direcciones IP, en donde el rango de valores se define por el primer octeto:

![Rango](/assets/images/Post/P12/P12i1.png)

---

## Interpretar una máscara de red

Sabemos que una máscara de red tiene bits que corresponden a la red y bits que corresponden a la parte del host.

Para definir qué parte de una dirección IP pertenece a la red y cuál parte pertenece a los hosts dentro de esa red.

**Se representan como una secuencia de bits**

- Bits en **1** indican la parte de **red**.
- Bits en **0** indican la parte de los **hosts**.

![Máscara de Red](/assets/images/Post/P12/P12i3.png)

Una máscara de subred será siempre más pequeña que una máscara de red.

---

## CIDR

Notación de enrutamiento entre dominios CIDR o sin clase, es una forma de representar direcciones IP más eficiente y flexible.

![CIDR](/assets/images/Post/P12/P12i4.png)

## Cálculo General por CIDR
---

Para calcular por notación CIDR necesitamos dos cosas:

1. Dirección IP 
2. Prefijo de Red

A continuación un ejemplo general del cálculo por notación CIDR

¿ Cuál es la dirección de red y la máscara de subred (en nominación CIDR) de la subred oculta.
Toda la red tiene una dirección de red y una máscara de subred de:

```shell
192.168.0.0/23
```
_

#### 1 CALCULAR DIRECCIÓN IP Y MÁSCARA DE RED EN BINARIO

**192.168.0.0**

- Decimal a Binario

```shell
❯ echo "$(echo "obase=2; 192" | bc)."   
11000000.

❯ echo "$(echo "obase=2; 168" | bc)."
10101000.
```

- Representación IP en binario

```shell
  192   .  168   .   0    .   0
11000000.10101000.00000000.00000000
```

- Representación del prefijo de red a binario, en donde el prefijo "/23" representan la parte de red que será 1 y los ceros la parte de los hosts:

```shell
# Máscara de Red Clase "C"
   255  .  255   .  255   .    0
11111111.11111111.11111111.00000000
# Cálculo prefijo de red "/23"
11111111.11111111.11111110.00000000
  255   .   255  .   254  .    0
```
_

#### 2 OPERACIÓN AND

Se comparan los bits de la dirección IP con los de la Máscara de Red. 

En donde los bits iguales a 1 son 1 y todos los bits no coincidentes son iguales a 0:

```shell
11000000.10101000.00000000.00000000 # (Dirección IP - 192.168.0.0)
11111111.11111111.11111110.00000000 # (Máscara de Red - 255.255.254.0)
-----------------------------------
11000000.10101000.00000000.00000000 # (Resultado AND Network ID - 192.168.0.0 - first ip)	
```
_

#### 2 CÁLCULO DE HOSTS A REPARTIR

Tomamos los bits en cero del prefijo de red y le aplicamos la siguiente fórmula:

`2^(n)-2` 

- `n` es el número de bits disponibles para el host.
- `-2` se restan las direcciones reservadas al broadcast y a la red.

**Aplicando la fórmula**

`2⁹-2` = 510


### 3 CÁLCULO DEL BROADCAST ADDRESS

Los bits correspondientes al host se ponen en uno el resto se queda igual:

```shell
  192   .  168   .   0    .   0        
11000000.10101000.00000000.00000000   # Network  ID - first ip
-----------------------------------
11000000.10101000.00000001.11111111  # Broadcast Address - last ip
```

- Binario a Decimal

```shell
❯ echo "$(echo "ibase=2;00000001 " | bc)."
1.

❯ echo "$(echo "ibase=2;11111111 " | bc)." 
255.
```

- Resultado Broadcast address

```shell
192.168.1.254
```

## Resumen

```shell
192.168.0.0 # Dirección IP
255.255.254.0 # Máscara de Red
192.168.0.0 # Network ID - first IP
192.168.1.254 # Broadcast Address - Last IP
510 # total de hosts
```



### Verificando Respuestas

[Página de ayuda y práctica](https://blog.jodies.de/ipcalc?host=192.168.0.0&mask1=23&mask2=)

![CIDR](/assets/images/Post/P12/P12i5.png)


