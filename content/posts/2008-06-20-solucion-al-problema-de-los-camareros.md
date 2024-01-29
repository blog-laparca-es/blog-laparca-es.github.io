---
title: Solución al problema de los camareros
author: laparca
type: post
date: 2008-06-20T13:31:52+00:00
url: /2008/06/20/solucion-al-problema-de-los-camareros/
categories:
  - Personal
tags:
  - acertijo
  - matematicas
  - solucion

---
Una amiga mia está publicando algunos acertijos matemáticos en su blog. En concreto voy a tratar de [explicar la solución al acertijo número 3][1].

La solución al problema es 10. La razón es que se quedan cerradas todas aquellas puertas cuya numeración corresponde con un cuadrado (1, 4, 9, etc.). El resto de puertas permanecerán abiertas al finalizar al proceso.

Para entender el porqué lo primero que hay que darse cuenta es que las puertas que son divisibles entre un número impar de números (contandose a sí mismas) permanecerán cerradas. Por ejemplo, la puerta 18 es divisible entre 2, 3, 6, 9 y 18.

Si nos fijamos en más detalle los número cuadrados son siempre divisibles entre un número par de factores.

Para demostrar esto vamos a ver cómo es un número. Un número, cualquiera, nos es más que el producto de una serie de factores. En esta caso, estos factores serán números primos elevados a una potencia:

<p align="center">
  [tex]b=p_1^{a_1}p_2^{a_2}&#8230;p_n^{a_n}[/tex]
</p>

Si sumamos todos los exponentes [tex]a_i[/tex] tendremos que para los números cuadrados siempre da un valor par, mientras que en el resto este valor será impar. De este modo podemos decir que los números que tienen al factorizarlo en primos una suma par de exponentes se quedarán cerrados.

Para profundizar un poco más en el tema, se debe a que a la hora de generar todos los divisores del número en cuestión, siempre saldrá una combinación impar, mientras que para los cuadrados, esta combinación será par. De hecho, el número de divisores puede ser calculado a partir de los exponentes de los primos que factorizan al número:

Para un número [tex]b[/tex] en la forma expresada anteriormente, tendrá tantos divisores como resulte de hacer la suma de todos los exponentes, más la suma de los productos de los exponentes tomados de dos en dos, más la suma de los exponentes tomados de tres en tres y así sucesivamente hasta [tex]n[/tex]:

<p align="center">
  [tex]d=\left(\sum_{i=0}^{n}a_i\right)+\left(\sum_{i=0}^{n}\sum_{j=i+1, j \neq i}^{n} a_{i}a_{j}\right)+\cdots+a_{1}a_{2} \cdots a_{n}[/tex]
</p>

Bueno, creo que con eso ya es suficiente tostón.

 [1]: http://trst-cronopia.blogspot.com/2008/06/acertijos-03.html