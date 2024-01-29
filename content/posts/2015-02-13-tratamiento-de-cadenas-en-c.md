---
title: Tratamiento de cadenas en C
author: laparca
type: post
date: 2015-02-13T12:22:48+00:00
url: /2015/02/13/tratamiento-de-cadenas-en-c/
categories:
  - Desarrollo
tags:
  - c++
  - cadenas
  - Desarrollo
  - programacion
  - tratamiento

---
Cuando empezamos a programar en C una de las cosas que probablemente más nos cuesta controlar es el tratamiento de cadenas.

El lenguaje C es de bastante bajo nivel, por lo que sus tipos de datos básicos son muy cercanos a lo que la máquina puede utilizar. Los ordenadores no entienden de cadenas, pero sí de direcciones de memoria. De hecho, no existe un tipo de cadena, sino que se usan <a title="Array" href="http://es.wikipedia.org/wiki/Vector_%28inform%C3%A1tica%29" target="_blank">arrays</a> de bytes. Y lo mejor de todo, ¡en C es el programador el que debe conocer la longitud del array! (cuanto bien, y a la vez cuánto mal, han hecho los lenguajes modernos).

Todas las funciones del estándar de C presuponen que una cadena es un array de bytes donde el último carácter es un nulo.

No voy a entrar en más detalles sobre que son las cadenas. Si quieres aprender cómo se programa con ellas puedes leer <a title="Cadenas de caracteres" href="http://es.wikibooks.org/wiki/Programaci%C3%B3n_en_C/Cadenas_de_caracteres" target="_blank">Cadenas de caracteres</a> del manual <a title="Programación en C" href="http://es.wikibooks.org/wiki/Programaci%C3%B3n_en_C" target="_blank">Programación en C</a> de  wikibooks.

Quien más y quien menos habrá visto que muchos problemas de seguridad en bibliotecas en C viene precisamente del tratamiento de cadenas. Casi se podría decir que si tienes que hacer un programa que tenga que manejar cadenas es aconsejable que mires cualquier otra cosa que no sea C. Aún así, esto no siempre será posible.

En el lugar en el que trabajo hemos empezado a cambiar el modo en que utilizamos las cadenas. Para facilitar su uso y reducir la cantidad de errores que pueden producirse, hemos creado un nuevo tipo de cadena. Bueno, se parece más a un <a title="Java String Builder" href="http://docs.oracle.com/javase/7/docs/api/java/lang/StringBuilder.html" target="_blank">StringBuilder</a> de java. Las motivaciones son varias:

  * Queremos un tratamiento de cadenas más rápido (tener que recorrer una cadena cada vez que quieres conocer su longitud no es óptimo).
  * Queremos poder trabajar con cadenas sin preocuparnos por reasignar constantemente memoria. ¿Habéis probado un _strcat_ cuando estás usando arrays y el _buffer_ de destino es más pequeño que la cadena a concatenar?
  * Para ciertas operatorias queremos poder tener cadenas con caracteres nulos. Las cadenas de C no se llevan bien con esto, pero nosotros creamos cadenas para mandar a dispositivos que no sólo aceptan el nulo, sino que ciertas operaciones lo requieren. Con las funciones estándar sería muy complicado esto.

Personalmente no creo que seamos los primeros en hacer algo así; no tengo la más mínima duda de que hay muchas personas con los mismos problemas.

Las ventajas de usar esta biblioteca son inmediatas:

  * Simplificamos el código por no tener que preocuparnos en si hay o no espacio para almacenar la cadena y en la gestión de este espacio.
  * Minimizamos errores pues no nos pasaremos nunca del _buffer_ (siempre podemos quedarnos sin memoria).
  * Agilizamos el desarrollo al poder escribir directamente código que haga lo que queremos (es una consecuencia del primer punto).
  * Se pueden optimizar ciertas operaciones. Esto se debe a que no hay que estar constantemente recorriendo cadenas para medirlas o que al «liberar» una cadena, no hacemos _free_ y _malloc_, sino que marcamos la cadena como de longitud 0 (que es más rápido y permite aprovechar la memoria).

**¡Mucho ojo con esto!** Que en el día a día de mi trabajo esta haya sido una buena solución no significa que lo sea para todos los casos. Siempre hay que evaluar convenientemente cada situación antes de decantarse por una u otra solución.