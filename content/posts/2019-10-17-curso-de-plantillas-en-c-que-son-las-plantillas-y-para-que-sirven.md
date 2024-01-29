---
title: 'Curso de plantillas en C++: qué son las plantillas y para qué sirven'
author: laparca
type: post
date: 2019-10-17T08:09:12+00:00
url: /2019/10/17/curso-de-plantillas-en-c-que-son-las-plantillas-y-para-que-sirven/
categories:
  - Personal
tags:
  - c++
  - metaprogramacion
  - plantillas
  - templates

---
Las plantillas en C++ son un mecanismo que nos pertite crear tipos y funciones dependientes de otros tipos y valores no definidos. El mejor modo de entenderlo es pensando en un formulario, por ejemplo, el típico formulario de una administración pública, donde hay un montón de texto y huecos que rellenar. Cada hueco recibe un valor. La plantilla es parecido, es definir un tipo o función donde dejamos _huecos_ para ser rellenados más tarde.

Según wikipedia:

> **Templates** are a feature of the C++ programming language that allows functions and classes to operate with generic types. This allows a function or class to work on many different data types without being rewritten for each one.
> 
> <p style="text-align: right;">
>   Fuente: <a href="https://en.wikipedia.org/wiki/Template_%28C%2B%2B%29">Wikipedia</a>
> </p>

La utilidad principal de las plantillas es poder crear código genérico. Un caso típico son los contenedores (listas, arrays, mapas, etc.). Sabemos que en C hay dos formas de desarrollar listas:

  1. Almacenando la información con un puntero tipo `void*` o
  2. Haciendo una implementación nueva para cada tipo que necesitemos.

El primer modo tiene la ventaja de poder contener cualquier cosa, pero a cambio, no hay control de tipos. Esto podría implicar problemas a largo plazo si no se programa con cuidado.

El segundo mecanismo tiene la ventaja del control de tipado, pero incrementa de forma lineal el tiempo de desarrollo y mantenimiento. Si tenemos un problema en una función y está implentada para 10 tipos, habría que cambiarla 10 veces&#8230;

Otra de las cosas que nos ofrecen las plantillas es la capacidad de metaprogramar y realizar acciones en tiempo de compilación.

En las prómimas entradas vamos a ir viendo en detalle ejemplos de plantillas en C++03 y, finalmente, veremos qué cambios se han ido introduciendo las versiones modernas.