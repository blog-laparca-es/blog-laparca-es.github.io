---
title: Creación de paquetes Debian (1 de 3)
author: laparca
type: post
date: 2012-05-06T12:36:38+00:00
url: /2012/05/06/creacion-de-paquetes-debian-1-de-3/
categories:
  - Desarrollo
tags:
  - debian
  - distribucion
  - linux
  - paquetes

---
Como prometí en mi anterior entrada, voy a tratar el tema de creación de paquetes para distribuciones de tipo Debian. La explicación va a estar dividida en tres partes:

  1. Motivación de la creación de paquetes
  2. Creación de paquetes
  3. Distribución de paquetes

# Motivación

Mucha gente que usa Linux por primera vez se da cuanta enseguida de la gran cantidad de aplicaciones que hay a golpe de una pulsación de ratón. No son necesarios los números de serie, ni los típicos _cracks_. De hecho, en una distribución como Debian puede encontrarse cerca de 30.000 paquetes preparados para instalar.

Por desgracia no siempre está la herramienta que buscamos o la versión que hay es muy vieja y le faltan características. En ese momento es cuando se complica la cosa y toca preparar el programa por nosotros mismos. Esto suele suponer la ejecución de alguna secuencia de comandos terminada en «make ; make install». Cuando hacemos esto último corremos el riesgo de sobrescribir configuraciones, bibliotecas o programas si  querer. Muchas veces esto no tiene porque ser importante, pero si, por ejemplo, estamos instalando algo en un servidor esto puede suponer un grave problema en el futuro.

Por el motivo anterior en las distribuciones de Linux se utiliza una cosa llamada paquete. Un paquete es un fichero que contiene información sobre los requisitos para instalar su contenido, acciones a ejecutar durante la instalación y los ficheros a instalar. Toda esta información facilita la eliminación y/o sustitución del paquete y comprobación de posibles conflictos con otros paquetes.

Finalmente, utilizando un sistema de distribución de paquetes conseguiremos que al tratar de instalar el sistema sea capaz descargar las dependencias (de otro modo solo comprobaría si hay o no problemas).

En las siguientes entradas veremos el proceso de creación de un paquete y su posterior distribución.