---
title: Mejora la terminal de Linux
layout: post
post-image: "/assets/images/Post/P22/P22i0.png"
description: Mejora tu productividad de la terminal configurandola y personalizandola.
tags:
- LINUX

---

Ahora veremos una personalización no muy díficil de nuestra terminal de linux pero que a su vez
nos ayudará bastante al momento de la navegación de la misma, falicitando y mejorando nuestra productividad.

### Indice



---

# Instalando Tilix 

Tilix es una gran emulador de la terminal, ya que nos permite dividir nuestra terminal en varias ventanas.
Otra ventaja es que podemos redimensionar y colocar varias terminales ya sea a la derecha o por debajo.

![P22i1](/assets/images/Post/P22/P22i1.png)

A continuación muestro la configuración de los *shortcuts* que más utilizo:

![P22i2](/assets/images/Post/P22/P22i2.png)

## Instalando zsh

ZSH es un un interprete de comandos pero con más funcionalidades como un navegador o historial de los comandos que utilizamos, así como la capacidad de agregar plugins etc.

Antes que nada actualizamos nuestro sistema:

```bash
sudo apt update
sudo apt upgrade -y
```
¨

Ahora instalamos zsh, adicional verificamos si la instalación tuvo éxito:

```bash
sudo apt install zsh -y

zsh --version
zsh 5.9 (x86_64-debian-linux-gnu)
```
¨

Procedemos a ejecutar `zsh` y presionamos la opción `0`

```shell
gmich4t@debian:~$ zsh
```
¨

![P22i5](/assets/images/Post/P22/P22i5.png)


1. Cerramos la terminal y la volvemos abrir, para ejecutar el siguiente comando `chsh -s /usr/bin/zsh` con eso establecemos por defecto zsh, en lugar de bash.
2. Cerramos y abrimos la terminal para la instalación de [oh my zsh](https://ohmyz.sh/#4install)

```shell
sudo apt install git -y
```
¨

Tenemos la posibilidad de instalar **oh my zsh** ya sea por `wget` o `curl`, solo tienes que copiar y pegar:

![P22i7](/assets/images/Post/P22/P22i7.png)

![P22i6](/assets/images/Post/P22/P22i6.png)

Antes de terminar la instalación nos pregunta si queremos configurar por defecto **zsh** respondemos con un `y`:

```shell
Time to change your default shell to zsh:
Do you want to change your default shell to zsh? [Y/n] y
Changing your shell to /usr/bin/zsh...

Shell successfully changed to '/usr/bin/zsh'.

         __                                     __   
  ____  / /_     ____ ___  __  __   ____  _____/ /_  
 / __ \/ __ \   / __ `__ \/ / / /  /_  / / ___/ __ \ 
/ /_/ / / / /  / / / / / / /_/ /    / /_(__  ) / / / 
\____/_/ /_/  /_/ /_/ /_/\__, /    /___/____/_/ /_/  
                        /____/                       ....is now installed!


Before you scream Oh My Zsh! look over the `.zshrc` file to select plugins, themes, and options.

• Follow us on Twitter: @ohmyzsh
• Join our Discord community: Discord server
• Get stickers, t-shirts, coffee mugs and more: Planet Argon Shop
```

### Instalando powerlevel10k

Instalamos un tema bastante agradable [powerlevel10k](https://github.com/romkatv/powerlevel10k) te dejo una captura de como es:

![P22i8](/assets/images/Post/P22/P22i8.png)

Clonamos el repositorio:

```shell
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```
¨

Listamos y buscamos el archivo `.zshrc`

```shell
➜  ~ ls -la
total 304
-rw-r--r--  1 gmich4t gmich4t     10 Apr  5 22:09 .shell.pre-oh-my-zsh
drwx------  2 gmich4t gmich4t   4096 Feb 26 22:24 .ssh
-rw-r--r--  1 gmich4t gmich4t   3866 Apr  5 22:09 .zshrc
-rw-r--r--  1 gmich4t gmich4t     29 Apr  5 21:58 .zshrc.pre-oh-my-zsh
```
¨

Editamos el archivo `/.zshrc`

```shell
nano .zshrc
```
¨

Ahora buscamos **ZSH_THEME**

![P22i9](/assets/images/Post/P22/P22i9.png)

Lo modificamos con `nano` y colocamos lo siguiente, guardamos.

```shell
ZSH_THEME="powerlevel10k/powerlevel10k"
```
¨

### Instalando Fonts

Una vez modificamos el archivo `.zshrc` salimos de la terminal y descargamos una fuente compatible con el tema powerlevel10k en este caso vamos a descargar la siguiente 
[nerdfonts](https://www.nerdfonts.com/font-downloads). Una vez descargado la fuente la extraemos y seleccionamos todas para su instalación:

![P22i10](/assets/images/Post/P22/P22i10.png)

Ahora vamos a establecer por defecto la fuente en tilix:

Seleccionamos en Preferencias

![P22i11](/assets/images/Post/P22/P22i11.png)

Ahora en perfiles

![P22i12](/assets/images/Post/P22/P22i12.png)

Marcamos la opción de fuentes personalizadas

![P22i13](/assets/images/Post/P22/P22i13.png)

Seleccionamos la fuente que descargamos:

![P22i14](/assets/images/Post/P22/P22i14.png)


Iniciamos la configuración del tema **powerlevel10k**

```shell
p10k configure
```
¨

### Instalando gestos

Vamos a instalar los autocompletados

```shell
git clone https://github.com/zsh-users/zsh-autosuggestions.git $ZSH_CUSTOM/plugins/zsh-autosuggestions 
```
¨

Ahora uno para resaltar los comandos que ya hemos usado

```shell
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
```
¨

Finalmente habilitamos todos los plugins en la `zshrc`, la editamos con nano y buscamos el apartado **Plugins**

![P22i15](/assets/images/Post/P22/P22i15.png)

```shell
plugins=(git zsh-autosuggestions zsh-syntax-highlighting)
```
¨

#### Coloreando los permisos de la terminal

Hay una forma muy sencilla de hacer esto y es por medio de `grc` que nos permite darle un formato con colores a los permisos:

```shell
sudo apt update
```
¨

Instalando `grc` 

```shell
sudo apt install grc
```
¨

Añadiendo `grc` para que se ejecute siempre que lanzamos una consola:

```shell
nano .zshrc
```
¨

Agregamos lo siguiente

```shell
alias ls='grc ls'
```

Eso es todo!

![P22i17](/assets/images/Post/P22/P22i17.png)







