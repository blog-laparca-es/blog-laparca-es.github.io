---
title: La impresora y Debian
author: laparca
type: post
date: 2005-10-23T16:38:18+00:00
url: /2005/10/23/la-impresora-y-debian/
categories:
  - Opinión

---
Ya hace más de dos meses que la impresora me dejor de funcionar en Debian. Hoy me puse decidido a arreglar esta situación.

El problema estaba en udev, este no creaba el dispositivo parport de la impresora. La razón, había que tener el modulo ppdev.

Parece una tontería, pero la verdad, me parece una putada que Debian no ponga los modulos que necesita dependiendo del hardware que tiene instalado.