---
title: Pseudo lambdas con C
author: laparca
type: post
date: 2015-02-11T12:31:24+00:00
url: /2015/02/11/pseudo-lambdas-con-c/
categories:
  - Desarrollo
tags:
  - c++
  - closure
  - Desarrollo
  - lambda
  - programacion

---
Últimamente se lleva mucho el tema de las funciones lambda y los _closures_ en los lenguajes modernos. Un ejemplo es que en C++, desde la versión de 2011, ya las incorpora. Igualmente, otros lenguajes, como Ruby, Groovy o Rust ya han sido diseñados con esta característica.

**Advertencia**: el código que vamos a mostrar a continuación hace uso de extensiones de GNU C. Para ser exactos, hace uso de <a title="Statement Expressions" href="https://gcc.gnu.org/onlinedocs/gcc/Statement-Exprs.html#Statement-Exprs" target="_blank">Statement Expressions</a> y de <a title="Nested Functions" href="https://gcc.gnu.org/onlinedocs/gcc/Nested-Functions.html#Nested-Functions" target="_blank">Nested Functions</a>. Estas extensiones solo son soportadas por unos pocos compiladores a parte de GNU C (ver <a title="Compiler support of GNU Statement Expression" href="http://stackoverflow.com/questions/6440021/compiler-support-of-gnu-statement-expression" target="_blank">Compiler support of GNU Statement Expressions en stackoverflow</a>).

Aunque en C no existe nada parecido es factible simularlo. Todo sea dicho, el código puede ser muy feo. En el siguiente ejemplo tenemos una función que recorre un conjunto de elementos. Esta función la llamamos proccess. Por cada elemento procesado llama a una función de _callback_. Lo normal es crear la función de _callback_ a parte, lo que hace que en ciertos casos sea incómodo el mantenimiento del código.

Otra opción es declarar la función de _callback_ _in situ_ justo en el momento que la necesitamos:

Como puede verse, nos aprovechamos de &#8216;({&#8216; y &#8216;})&#8217; para declarar un bloque de código que devuelve el valor de la última expresión para crear nuestra función de _callback_. Como en este caso el nombre no nos importa, la llamamos &#8216;_&#8217;. Lo mejor de todo es que podemos repetir este nombre sin que por ello suponga que vaya a haber conflicto en la compilación ni en la ejecución.

**Actualización 1**: incluimos advertencia sobre compiladores.