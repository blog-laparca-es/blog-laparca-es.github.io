---
title: Curiosidades de C++
author: laparca
type: post
date: 2014-04-24T09:02:41+00:00
url: /2014/04/24/curiosidades-de-c/
categories:
  - Desarrollo
  - Personal
tags:
  - c++
  - cpp
  - curiosidad
  - Desarrollo
  - error
  - programacion

---
Ayer trasteando con el compilador de C++ descubrí una cosa nueva sobre cómo funciona por dentro.

Si compilamos el siguiente programa y lo ejecutamos veremos que falla con un bonito [SIGSEGV][1]:

El motivo es que, para empezar, hay dos estructuras que son diferentes pero se llaman igual. El constructor de dichas estructuras no deja de ser una función, por lo que en cada fichero objeto se generará una función para construir la estructura. Sí, la función se llamará igual en ambos objetos.

Cuando enlazamos se queda con la primera función que encuentre (en este caso con la de a.cpp). Así que cuando desde run\_example\_b se trata de instanciar la estructura lo hace con el constructor de a.cpp.

Hasta ayer por la tarde no caí en porque esto funciona así, pero es bastante lógico. Hay muchas clases en las bibliotecas estándar (y de terceros) cuyos constructores están implementados en la propia cabecera. Esto significa que cada fuente que tengamos tendrá su propia implementación del constructor y luego, al enlazar, se reduce a sólo uno.

Si el ejemplo anterior lo compilamos todo con &#8216;-O2&#8217;, el constructor lo convierte en _inline_ para optimizar y funciona correctamente.

**Nota mental**: hay que mejorar los nombres de funciones in clases según su utilidad y contexto (debe ser más semántico).

 [1]: http://es.wikipedia.org/wiki/SIGSEGV "Error de acceso a memoria"