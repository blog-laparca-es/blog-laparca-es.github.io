---
title: Como hacer que tu código sea legible
author: laparca
type: post
date: 2017-01-31T08:59:26+00:00
url: /2017/01/31/como-hacer-que-tu-codigo-sea-legible/
categories:
  - Desarrollo
  - Personal
tags:
  - clean code
  - codigo limpio
  - consejo
  - consejos
  - legibilidad
  - legible
  - readable

---
Reconozco que no soy el mejor programador del mundo, pero intento mejorar cada día. Puede sonar tonto, pero una de las mayores complicaciones del trabajo de un programador es conseguir que el código que escribes un día sea entendible por otras personas !y nosotros mismos! en el futuro.

Casi todo lo que voy a contar a continuación lo he aprendido a partir de diversas lecturas y por propia experiencia.

Algunos de los consejos más útiles que creo que son importantes tener en cuenta son:

## Utiliza el inglés al programar

Puede resultar extraño para algunos que dominando un idioma (español, portugués, francés, etc.) tengan que programar en inglés. El motivo es sencillo, la mayor parte de la documentación en nuestro sector está en inglés por lo que acabamos mezclando idiomas. ¿A quién no le ha pasado tener funciones llamadas _setPeso_ o _getNombre_?

Por otra parte, el inglés permite abrirnos puertas en dos sentidos:

  * Para empezar como programadores que dominemos el inglés podremos acceder a más puestos de trabajo. La globalización no es sólo para las empresas; nosotros también podemos aprovecharnos de ella.
  * Podemos contratar programadores extranjeros que no tendrán problemas al leer el código.

## Utiliza normas de codificación

Esto en algunas metodologías se llama <a href="https://es.wikipedia.org/wiki/Gesti%C3%B3n_de_configuraci%C3%B3n_de_software" target="_blank">gestión de configuración del software</a>. También se puede encontrar como convención de codificación (_code convention_) o guías de estilo. La idea es tener una serie de normas que indica cómo debe ser la nomenclatura de codificación y tabulación para que todo el desarrollo sea consistente. Con esto conseguimos un programa más homogéneo y fácil de entender.

Tampoco es necesario inventarse una propia porque ya existen muchas. A modo de ejemplo:

  * <a href="http://www.oracle.com/technetwork/java/codeconvtoc-136057.html" target="_blank">Convención de codificación de Java de Oracle</a>.
  * <a href="https://google.github.io/styleguide/javaguide.html" target="_blank">Guía de estilo de Java de Google</a>.
  * <a href="https://google.github.io/styleguide/cppguide.html" target="_blank">Guía de estilo de C++ de Google</a>.
  * <a href="https://www.python.org/dev/peps/pep-0008/" target="_blank">Guía de estilo de Python de python.org</a>.

## Elige bien los nombre

La verdad es que el tema de los nombres es uno de los más complejos. Sobre todo para funciones y clases. Por norma los nombres de métodos, funciones, clases, etc. deben ser descriptivos y breves. Por ejemplo, un nombre como _ApplicationModelAbstractObjectFactory_ quizá sea un poco largo, pero parece descriptivo. Igualmente, algo como _EntraSola_ (caso real) es muy breve, pero no dice nada; no es posible determinar realmente su funcionalidad (además, puede inducir a tener pensamientos impuros).

## Utiliza comentarios

Este punto es bastante controvertido porque mucho programadores piensan eso de «el código bien escrito se entiende solo». Y es verdad. El problema es cuando el código no hace lo que toca.

No hay que llenar el código de comentarios, deben ser lo mínimo posible y sólo para cosas que claramente lo necesiten. Esto suele ser para aquellas construcciones que sean muy abstractas y que cueste mas comprender.

## Se organizado

Otro punto que quizá no sea obvio, pero es cierto que tener bien organizado el código ayuda mucho a su legibilidad. Es más fácil entender una función que está dividida en partes (preparación de datos, realización de acciones, generación de resultado) que otra en la que se vayan mezclando todas estas tareas.

## Refactoriza

Por mucho que nos esforcemos en que nuestro código sea claro y legible, con el tiempo acabará por convertirse todo en algo caótico. Es normal, porque conforme evoluciona un software se añaden nuevas funcionalidades para las que no estaba inicialmente pensado.

Para evitar esto hay que hacer ciclos de refactorización que mantengan el código limpio y optimizado.

## Conclusiones

Está claro que <del>una parte importante para evitar la deuda técnica reside en la calidad del código</del> un código más claro facilita el mantenimiento al poder ser entendido fácilmente (ojo, que a parte de esto es necesario un buen diseño del mismo). El uso de unas normas que permitan que éste sea entendible ayudan mucho para evitar este problema.

Finalmente me gustaría comentar que este artículo es meramente introductorio y faltan muchas cosas que contar. Estoy más que seguro que habrá discrepancias con algunas cosas; si es así, te animo a que dejes un comentario.

## Bibliografía

La mayor parte de lo que he expuesto aquí procede del libro <a href="http://shop.oreilly.com/product/9780596802301.do" target="_blank">The Art of Readable Code </a>de O&#8217;Relly.

## Errata

  * 2017-02-01: Corrijo la parte de la deuda técnica a sugerencia de Fioddor.