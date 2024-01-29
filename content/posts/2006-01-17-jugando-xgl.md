---
title: Jugando con Xgl
author: laparca
type: post
date: 2006-01-17T09:06:31+00:00
url: /2006/01/17/jugando-xgl/
categories:
  - Opinión
  - Software libre

---
Molesto con que no funcione la extensión Composite de las Xorg en mi ATI Radeon del portátil, me puse a investigar y encontré algo que creo es bastante interesante: [un servidor de XWindow que aprovecha la aceleración 3D][1].

He estado probandolo un poco y tiene buen aspeco, pero no termina de funcionar bien (puede ser por problemas con x86-64). El caso es que espero que pronto lo tengo todo funcionando. De momento he conseguido que me muestre las sombritas (que pijo que soy :-P).

Lo que me gustaría hacer funcionar, pero no lo consigo es glxcompmgr, un gestor de composición que permite añadir efectos sobre las ventanas (al estilo de luminocity). Pero soy incapaz de que funcione. Más o menos he visto [los pasos a seguir][2], pero creo que falta algo (sobre todo en el tema del parcheo y compilación de Mesa).

Si consigo hacerlo funcionar bien, ya diré más cositas.

 [1]: http://www.freedesktop.org/wiki/Software_2fXgl
 [2]: http://www.hboeck.de/item/266