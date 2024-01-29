---
title: Concurso de C «a pelo»
author: laparca
type: post
date: 2014-09-04T19:34:49+00:00
url: /2014/09/04/concurso-de-c-a-pelo/
categories:
  - Desarrollo
  - Personal
tags:
  - c++
  - concurso
  - nostdlib
  - oreilly
  - programacion

---
Recientemente surgió en una _newsletter_ de O&#8217;Reilly un concurso que me pareció bastante curioso. Las bases eran las siguientes:

> It seems like a new language is spawned every day, but the old tried-and-true warriors of the code world continue to soldier on. This week, the specification for C++ version 14 was frozen, and it includes such features as enhanced lambda expressions (because all the cool languages are doing it). In honor of this momentous event, we&#8217;re running a little contest to test your chops with the bare C. Sure, anyone can create awesome code using all the libraries that modern operating systems come with, but what can you do close to the metal?
> 
> Your challenge is to create a nontrivially useful application that will compile on a Linux system using the following command:
> 
> <pre>gcc -nostdlib -o sample sample.c startstub.S</pre>
> 
> startstub.S is an i386 assembler file that can call main() without the standard libraries and can be downloaded <a href="http://post.oreilly.com/rd/9z1zl2pjf7k32f7q4a95o39a0gurq0mgglunpmekvm8" target="_blank">here</a>. You need to have a function main defined as «int main()» that can return a value, which will end up in $?. Only C is allowed, no assembler or other funny business. Entries will be judged on two criteria: binary size and functionality of the program. For reference, a program that does nothing weighs in at 1502 bytes.

Básicamente dice que hay que hacer un programa en C, que no va a poder enlazar con biblioteca de funciones alguna (no hay libc) y que no se puede hacer uso de ensamblador. Esto último es importante, porque con esta restricción se pierde la capacidad de hacer llamadas al sistema: no se puede reservar memoria con _malloc_, ni leer ni escribir en disco, etc. Eso sí, el programa debe tener alguna utilidad y te dicen que puede devolver un valor que será podrá ser consultado con $? (variable de la shell con el resultado del último programa ejecutado). Eso sí, el _startstub.S_ que suministran no permite dicho uso (¿despiste quizá?).

Estas premisas tan restrictivas me animaron a tratar de crear algo para el concurso. Tras varias ideas descartadas decidí hacer una aplicación que devolviese la posición de una palabra en una lista de palabras (no parece muy útil) y que con una opción permitiese devolver la palabra de la lista más parecida a la buscada (puede resultar algo más útil).

El problema es que con lo suministrado por la gente de O&#8217;Reilly, la función _main_ no recibe argumentos. Así que no tenemos un mecanismo sencillo para comprobar los parámetros.

La solución al problema anterior es tener en cuenta que Linux, cuando ejecuta un programa y pasa le pasa el control deja en la cima de la pila _argc_, luego _argv_ y después _env_. Como la función __start_ suministrada no mueve los punteros de la pila, _main_ tendrá esos mismos datos. Así que sólo hay que buscar un mecanismo para obtener un puntero a la cima de la pila.

En la arquitectura i386, los argumentos de las funciones se pasan por pila. Así, si tenemos una función que sólo acepta un parámetro, en el momento en que entramos en la función nos encontraremos esto en la cima de la pila:

<pre>0x000000 Dirección de Retorno
0x000004 Parámetro</pre>

Por tanto, la dirección de memoria del primer parámetro será una posición en la pila. En este caso sabemos que se correspondería con _argc_.

El problema es que en las arquitecturas de 64 bits, no se comporta de este modo: los 6 primeros parámetros son registros de procesador. En este caso, si es una arquitectura de este tipo, creamos una función que acepta 7 parámetros. Los seis primeros que serán registros (y los ignoramos) y el séptimo que ya se encuentra en la pila.

El resto del programa ya no tiene más misterios y lo podéis ver a continuación: