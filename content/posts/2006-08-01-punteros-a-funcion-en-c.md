---
title: Punteros a función en C
author: laparca
type: post
date: 2006-08-01T16:06:57+00:00
url: /2006/08/01/punteros-a-funcion-en-c/
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:8714:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17
    18
    19
    20
    21
    22
    23
    24
    25
    26
    27
    28
    29
    30
    31
    32
    33
    34
    35
    36
    37
    38
    39
    40
    41
    42
    43
    44
    45
    46
    47
    48
    </pre></td><td class="code"><pre class="c" style="font-family:monospace;"><span style="color: #808080; font-style: italic;">/**
    * Ordena los elementos de una lista de menor a mayor.
    * La lista es genérica y almacena sus elementos como punteros a cualquier cosa (void *).
    * Se utiliza una función de comparación a la que se le pasan dos elementos de la lista y nos
    * informa si el primero es mayor que el segundo.
    */</span>
    <span style="color: #993333;">void</span> ordenar<span style="color: #009900;">&#40;</span> lista_t lista<span style="color: #339933;">,</span> <span style="color: #993333;">int</span> <span style="color: #009900;">&#40;</span><span style="color: #339933;">*</span>cmp<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#40;</span><span style="color: #993333;">void</span> <span style="color: #339933;">*</span>elm1<span style="color: #339933;">,</span> <span style="color: #993333;">void</span> <span style="color: #339933;">*</span>elm2<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
       <span style="color: #993333;">void</span> <span style="color: #339933;">*</span>elem1<span style="color: #339933;">,</span> <span style="color: #339933;">*</span>elem2<span style="color: #339933;">,</span> <span style="color: #339933;">*</span>tmp<span style="color: #339933;">;</span>
       <span style="color: #993333;">int</span> numero_elementos <span style="color: #339933;">=</span> lista_numero_elementos<span style="color: #009900;">&#40;</span> lista <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
       <span style="color: #993333;">int</span> i<span style="color: #339933;">,</span> c<span style="color: #339933;">;</span>
    &nbsp;
       <span style="color: #b1b100;">for</span><span style="color: #009900;">&#40;</span> i <span style="color: #339933;">=</span> <span style="color: #0000dd;">0</span><span style="color: #339933;">;</span> i <span style="color: #339933;">&lt;</span> numero_elementos<span style="color: #339933;">;</span> i <span style="color: #339933;">++</span> <span style="color: #009900;">&#41;</span>
       <span style="color: #009900;">&#123;</span>
          <span style="color: #b1b100;">for</span><span style="color: #009900;">&#40;</span> c <span style="color: #339933;">=</span> <span style="color: #0000dd;">0</span><span style="color: #339933;">;</span> c <span style="color: #339933;">&lt;</span> numero_elementos<span style="color: #339933;">-</span>i<span style="color: #339933;">-</span><span style="color: #0000dd;">1</span><span style="color: #339933;">;</span> c <span style="color: #339933;">++</span> <span style="color: #009900;">&#41;</span>
          <span style="color: #009900;">&#123;</span>
             elem1 <span style="color: #339933;">=</span> lista_obtener_elemento<span style="color: #009900;">&#40;</span> lista<span style="color: #339933;">,</span> c <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
             elem2 <span style="color: #339933;">=</span> lista_obtener_elemento<span style="color: #009900;">&#40;</span> lista<span style="color: #339933;">,</span> c<span style="color: #339933;">+</span><span style="color: #0000dd;">1</span> <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
             <span style="color: #808080; font-style: italic;">/* Si elem1 &gt; elem2 Entonces los intercambiamos.
             * Para hacer esta comparación, utilizamos la función del usuario. */</span>
             <span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span> cmp<span style="color: #009900;">&#40;</span> elem1<span style="color: #339933;">,</span> elem2 <span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#41;</span>
             <span style="color: #009900;">&#123;</span>
                lista_asignar_elemento<span style="color: #009900;">&#40;</span> lista<span style="color: #339933;">,</span> c<span style="color: #339933;">,</span> elem2 <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                lista_asignar_elemento<span style="color: #009900;">&#40;</span> lista<span style="color: #339933;">,</span> c<span style="color: #339933;">+</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span> elem1 <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
             <span style="color: #009900;">&#125;</span> <span style="color: #808080; font-style: italic;">/* if( cmp( elem1, elem2 ) ) */</span>
          <span style="color: #009900;">&#125;</span> <span style="color: #808080; font-style: italic;">/* for( c = 0; c &lt; numero_elementos-i-1; c ++ ) */</span>
       <span style="color: #009900;">&#125;</span> <span style="color: #808080; font-style: italic;">/* for( i = 0; i &lt; numero_elementos; i ++ ) */</span>
    <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;">/**
    * Compara elm1 y elm2, teniendo en cuenta que estos deben ser enteros.
    * Si elm1 es mayor que elm2, devuelve un valor distinto que 0. En cualquier
    * otro caso, devolverá 0.
    */</span>
    <span style="color: #993333;">int</span> CompararEnteros<span style="color: #009900;">&#40;</span> <span style="color: #993333;">void</span> <span style="color: #339933;">*</span>elm1<span style="color: #339933;">,</span> <span style="color: #993333;">void</span> <span style="color: #339933;">*</span>elm2 <span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>
       <span style="color: #993333;">int</span> a<span style="color: #339933;">,</span> b<span style="color: #339933;">;</span>
       a <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span><span style="color: #993333;">int</span><span style="color: #009900;">&#41;</span>elm1<span style="color: #339933;">;</span>
       b <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span><span style="color: #993333;">int</span><span style="color: #009900;">&#41;</span>elm2<span style="color: #339933;">;</span>
       <span style="color: #b1b100;">return</span> a <span style="color: #339933;">&gt;</span> b<span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;">/* Código del usuario */</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;">/* Para ordenar la lista de enteros: */</span>
    ordenar<span style="color: #009900;">&#40;</span> lista<span style="color: #339933;">,</span> CompararEnteros <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    &nbsp;
    <span style="color: #808080; font-style: italic;">/* Código del usuario */</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Ordena los elementos de una lista de menor a mayor.
    * La lista es genérica y almacena sus elementos como punteros a cualquier cosa (void *).
    * Se utiliza una función de comparación a la que se le pasan dos elementos de la lista y nos
    * informa si el primero es mayor que el segundo.
    */
    void ordenar( lista_t lista, int (*cmp)(void *elm1, void *elm2) ) {
       void *elem1, *elem2, *tmp;
       int numero_elementos = lista_numero_elementos( lista );
       int i, c;
    
       for( i = 0; i &lt; numero_elementos; i ++ )
       {
          for( c = 0; c &lt; numero_elementos-i-1; c ++ )
          {
             elem1 = lista_obtener_elemento( lista, c );
             elem2 = lista_obtener_elemento( lista, c+1 );
             /* Si elem1 &gt; elem2 Entonces los intercambiamos.
             * Para hacer esta comparación, utilizamos la función del usuario. */
             if( cmp( elem1, elem2 ) )
             {
                lista_asignar_elemento( lista, c, elem2 );
                lista_asignar_elemento( lista, c+1, elem1 );
             } /* if( cmp( elem1, elem2 ) ) */
          } /* for( c = 0; c &lt; numero_elementos-i-1; c ++ ) */
       } /* for( i = 0; i &lt; numero_elementos; i ++ ) */
    }
    
    /**
    * Compara elm1 y elm2, teniendo en cuenta que estos deben ser enteros.
    * Si elm1 es mayor que elm2, devuelve un valor distinto que 0. En cualquier
    * otro caso, devolverá 0.
    */
    int CompararEnteros( void *elm1, void *elm2 )
    {
       int a, b;
       a = (int)elm1;
       b = (int)elm2;
       return a &gt; b;
    }
    
    /* Código del usuario */
    
    /* Para ordenar la lista de enteros: */
    ordenar( lista, CompararEnteros );
    
    
    /* Código del usuario */</p></div>
    ";}
categories:
  - Desarrollo

---
Bueno, unas de las cosas que me quedan en el tintero es poner ejemplos de código. Con esta entrada espero poner fin a esto hablando de los punteros a función en C.

Muchos de los que hayan programado en C sabrán lo infernal que puede resultar el uso de punteros. Hoy, para rizar el rizo, voy a hablaros de los punteros a función.

Como sucede con los punteros normales (a variables), un puntero a función no es más que un apuntador que nos dice donde se encuentra una función. La pregunta ahora es&#8230; ¿Y para qué nos puede servir esto? Pues la verdad es que para muchas cosas, por ejemplo, cuando se dispone de un algoritmo de ordenación en C y queremos que este nos sirva para cualquier cosa, lo interesante es tener un mecanismo que nos permita comparar dos elementos. Podemos hacer el algortimo de modo que sólo soporte un tipo de datos o podemos hacer que soporte cualquier tipo. Esto lo hacemos con punteros a funciones. Vamos a ver un ejemplo:

<pre lang="c" line="1">/**
* Ordena los elementos de una lista de menor a mayor.
* La lista es genérica y almacena sus elementos como punteros a cualquier cosa (void *).
* Se utiliza una función de comparación a la que se le pasan dos elementos de la lista y nos
* informa si el primero es mayor que el segundo.
*/
void ordenar( lista_t lista, int (*cmp)(void *elm1, void *elm2) ) {
   void *elem1, *elem2, *tmp;
   int numero_elementos = lista_numero_elementos( lista );
   int i, c;

   for( i = 0; i &lt; numero_elementos; i ++ )
   {
      for( c = 0; c &lt; numero_elementos-i-1; c ++ )
      {
         elem1 = lista_obtener_elemento( lista, c );
         elem2 = lista_obtener_elemento( lista, c+1 );
         /* Si elem1 > elem2 Entonces los intercambiamos.
         * Para hacer esta comparación, utilizamos la función del usuario. */
         if( cmp( elem1, elem2 ) )
         {
            lista_asignar_elemento( lista, c, elem2 );
            lista_asignar_elemento( lista, c+1, elem1 );
         } /* if( cmp( elem1, elem2 ) ) */
      } /* for( c = 0; c &lt; numero_elementos-i-1; c ++ ) */
   } /* for( i = 0; i &lt; numero_elementos; i ++ ) */
}

/**
* Compara elm1 y elm2, teniendo en cuenta que estos deben ser enteros.
* Si elm1 es mayor que elm2, devuelve un valor distinto que 0. En cualquier
* otro caso, devolverá 0.
*/
int CompararEnteros( void *elm1, void *elm2 )
{
   int a, b;
   a = (int)elm1;
   b = (int)elm2;
   return a > b;
}

/* Código del usuario */

/* Para ordenar la lista de enteros: */
ordenar( lista, CompararEnteros );


/* Código del usuario */

</pre>

Bueno, espero que no sea necesario que explique qué hacen las funciones de la lista. Como vemos, con este mecanismo podemos usar enteros, flotantes, estructuras o imágenes. En verdad ahora podríamos ordenar una lista de cualquier cosa. Esto se consigue precisamente por el uso de punteros a función. Los que hayan hecho porgramación orientada a objetos se darán cuenta que esto se podría haber hecho con herencia.

En la línea 7, tenemos _int (\*cmp)(void \*elm1, void *elm2)_. Esto es precisamente la declaración de una variable _cmp_ que será un puntero a una función que devolverá un entero y que acepta dos parámetros de tipo _void *_. Para utilizar el puntero, sólo hay que hacer como si fuera una función normal y corriente:

cmp( param1, param2 );

En general, la definición de todo puntero a función es de la forma:

tipo\_de\_retorno (*nombre\_de\_la_variable)( parametros ); 

Para asignar a un puntero a función la dirección de un puntero, no hay más que hacer una signación normal:

puntero\_a\_función = función;

La función sería sin los argumentos.

Esto es sólo un ejemplo de lo que se puede hacer. Los punteros a funciones también pueden emplearse para crear menús dinámicos en los que queremos que, cuando se les pulse, se llame a una función (esta se pasaría como puntero a función). En muchas prácticas de las asignaturas de sistemas operativos, al utilizar señales tipo UNIX, se utilizan punteros a funciones. Se utilizan cuando decimos: «pues cuando llegue la señal SIGXXXX, quiero que llames a esta función». Cuando se hace programación multihilo (o con _threads_), también se usan los punteros a función.

Bueno, esto ha sido una pequeña introducción. Si a alguien le interesa saber más, puede decirlo en los comentarios. Si se me ocurre poner algo más, ya lo haré. Espero que os haya servido de ayuda.