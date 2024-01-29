---
title: 'Curso de plantillas en C++: primeros pasos'
author: laparca
type: post
date: 2019-10-25T20:56:10+00:00
url: /2019/10/25/curso-de-plantillas-en-c-primeros-pasos/
categories:
  - Personal
tags:
  - c++
  - curso
  - formacion
  - introduccion
  - software

---
En la entrada anterior introdujimos por encima las plantillas. Seguro que generó más dudas que otra cosa, así que vamos a empezar a ver <s>chicha</s> código.

## ¿Qué resuelven las plantillas? {.wp-block-heading}

En lenguajes como C o Pascal implementamos algo tan básico como una lista enlazada tal que así:

<pre class="wp-block-code"><code>/* Caso 1: Lista para un tipo concreto */
struct ListaPersona
{
   struct Lista* siguiente;
   /* El dato almacena un elemento de la lista puede ser un puntero (suele serlo */
   Persona dato;
};

/* Caso 2: Lista genérica para cualquier cosa */
struct Lista
{
   struct Lista* siguiente;
   void* dato;
};</code></pre>

En el caso 1, el problema es que hay que hacer una implementación por cada tipo de dato que queramos. Esto es bastante esfuerzo y, sobre todo, mucho trabajo de mantenimiento en caso de problemas.

En el caso 2 podemos hacer cualquier cosa, lo que puede acarrear problemas. Estos problemas vendrían, principalmente, por no poder validar el tipo de los datos que almacenamos. Por ejemplo:

<pre class="wp-block-code"><code>/* No hagáis esto en casa */
typedef void*(*crea_instancia_t)();
int i;
struct Lista* lista;
crea_instancia_t crea_instancia&#91;3] = { crea_persona, crea_pedido, crea_cualquier_cosa_guay };

for (i = 0; i &lt; 100; i++)
{
   lista = lista_agregar(lista, crea_instancia&#91;rand()%3]());
}
/* ¿Qué hay en cada entrada de la lista? */</code></pre>

Vale, es muy cogido por los pelos, pero siempre puede pasarnos que nos despistemos al programar y metamos lo que no es. Y lo mejor, depura a ver qué ha pasado.

## ¿Cómo resolvemos esto en C++? {.wp-block-heading}

Esta sería la parte más sencillas de las plantillas de C++. En este caso, lo que podemos hacer es poner algo que identifique el tipo que queremos y se sustituya por el que queremos:

<pre class="wp-block-code"><code>template&lt;typename T>
struct Lista
{
   Lista* siguiente;
   T dato;
};</code></pre>

Ya está, ahora ya podemos aprovechar las ventajas del sistema de tipos para garantizar que metemos en la lista los tipos adecuados.

Ojo, a efectos prácticos es lo mismo que hacer una versión para cada tipo que le indiquemos a la lista. El compilador genera una versión para cada tipo.

En la próxima entrada empezaremos a ver cómo se integran los tipos de plantillas para pasarlos a funciones.