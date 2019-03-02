---
layout: post
title: "Empaquetamiento Scideb - Debian"
comments: true
description: "¿ Qué es un paquete ?"
keywords: "debian package scideb"
---
Un paquete es un conjunto de archivos que permite distribuir aplicaciones, librerías, procurando la automatización en la instalación, actualización, configuración y desintalación del software de manera consistente.

### Esqueman general de empaquetamiento

![alt text](/assets/images/overview-empaquetamiento.png
 "Empaquetamiento")

### Contenido

* [Empaquetamiento Manual](http://c3.itm.edu.co/wiki/Empaquetamiento001)
* [Empaquetamiento con Scripts](http://c3.itm.edu.co/wiki/Empaquetamiento002)
* [Explorando la carpeta ''debian''](http://c3.itm.edu.co/wiki/Empaquetamiento003)
* 004 - Modificando el archivo ''rules''
* 005 - Realizando parches con __quilt__
* [Empaquetamiento con control de versiones - Git](http://c3.itm.edu.co/wiki/controlversion006)
* 007 - Empaquetamiento con Docker
* 008 - Empaquetamiento con Vagrant

### Requerimientos conceptuales

*  Manejo de sistemas de administración de paquetes como __apt-get__, __aptitude__, __dpkg__, entre otros.
* Conocimiento de CLI/Scripting usando Bash y editores de texto como __nano__,__vim__. [Curso Bash](http://c3.itm.edu.co/wiki/tiki-index.php?page=cmake)
* Conocimiento de sistemas de construcción de software como __make__,__cmake__,__scons__, entre otros. [Curso Cmake](http://c3.itm.edu.co/wiki/tiki-index.php?page=cmake)
* Conocer [FHS](https://wiki.debian.org/es/FilesystemHierarchyStandard) - Filesystem Hierarchy Standard


### Requerimientos técnicos

* Sistema operativo con Debian - Testing / Experimental
* Instalar los paquetes `build-essential, devscripts, debhelper, dh-make, lintian`
> apt-get install build-essential devscripts debhelper dh-make lintian


### __Anexos :__
* __Creación clave gpg__
