---
title: Sobre las conversiones «sucias» de C en 64 bits
author: laparca
type: post
date: 2006-08-10T19:48:46+00:00
url: /2006/08/10/sobre-las-conversiones-sucias-de-c-en-64-bits/
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:8104:"
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
    </pre></td><td class="code"><pre class="c" style="font-family:monospace;"><span style="color: #339933;">#include &lt;stdio .h&gt;</span>
    <span style="color: #339933;">#include &lt;stdlib .h&gt;</span>
    &nbsp;
    <span style="color: #339933;">#define SIZEOF(x) printf( &quot;sizeof( %s ) = %d Bytes (%d bits)\n&quot;, #x, sizeof(x), sizeof(x)*8 )</span>
    <span style="color: #993333;">int</span> main<span style="color: #009900;">&#40;</span> <span style="color: #993333;">void</span> <span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>
            <span style="color: #993333;">void</span> <span style="color: #339933;">*</span>ptr<span style="color: #339933;">;</span>
            <span style="color: #993333;">int</span> valor<span style="color: #339933;">;</span>
    &nbsp;
            <span style="color: #808080; font-style: italic;">/* Compruebo que se pueda pasar de entero sin signo a puntero.
            * A grandes rasgos consiste en hacer creer al compilador que el
            * entero es una dirección de memoria. */</span>
    &nbsp;
            valor <span style="color: #339933;">=</span> <span style="color: #0000dd;">5</span><span style="color: #339933;">;</span>
            <span style="color: #000066;">printf</span><span style="color: #009900;">&#40;</span> <span style="color: #ff0000;">&quot;Valor inicial antes de la transformacion: %d<span style="color: #000099; font-weight: bold;">\n</span>&quot;</span><span style="color: #339933;">,</span> valor <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            ptr <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span><span style="color: #993333;">void</span> <span style="color: #339933;">*</span><span style="color: #009900;">&#41;</span>valor<span style="color: #339933;">;</span>
            valor <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span><span style="color: #993333;">int</span><span style="color: #009900;">&#41;</span>ptr<span style="color: #339933;">;</span>
            <span style="color: #000066;">printf</span><span style="color: #009900;">&#40;</span> <span style="color: #ff0000;">&quot;Valor tras la transformacion: %d<span style="color: #000099; font-weight: bold;">\n</span>&quot;</span><span style="color: #339933;">,</span> valor <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
            <span style="color: #808080; font-style: italic;">/* Compruebo que se pueda pasar de entero con signo a puntero.
            * A grandes rasgos consiste en hacer creer al compilador que el
            * entero es una dirección de memoria. */</span>
    &nbsp;
            valor <span style="color: #339933;">=</span> <span style="color: #339933;">-</span><span style="color: #0000dd;">5</span><span style="color: #339933;">;</span>
            <span style="color: #000066;">printf</span><span style="color: #009900;">&#40;</span> <span style="color: #ff0000;">&quot;Valor inicial antes de la transformacion: %d<span style="color: #000099; font-weight: bold;">\n</span>&quot;</span><span style="color: #339933;">,</span> valor <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            ptr <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span><span style="color: #993333;">void</span> <span style="color: #339933;">*</span><span style="color: #009900;">&#41;</span>valor<span style="color: #339933;">;</span>
            valor <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span><span style="color: #993333;">int</span><span style="color: #009900;">&#41;</span>ptr<span style="color: #339933;">;</span>
            <span style="color: #000066;">printf</span><span style="color: #009900;">&#40;</span> <span style="color: #ff0000;">&quot;Valor tras la transformacion: %d<span style="color: #000099; font-weight: bold;">\n</span>&quot;</span><span style="color: #339933;">,</span> valor <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
            <span style="color: #808080; font-style: italic;">/* Compruebo los tamaños de los distintos tipo de datos. El tipo 'void *'
            * es un puntero. Todos los puntero tienen el mismo tamaño en memoria,
            * por lo que no pruebo todas las combinaciones. */</span>
    &nbsp;
            SIZEOF<span style="color: #009900;">&#40;</span><span style="color: #993333;">void</span> <span style="color: #339933;">*</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            SIZEOF<span style="color: #009900;">&#40;</span><span style="color: #993333;">char</span> <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            SIZEOF<span style="color: #009900;">&#40;</span><span style="color: #993333;">short</span> <span style="color: #993333;">int</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            SIZEOF<span style="color: #009900;">&#40;</span><span style="color: #993333;">int</span> <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            SIZEOF<span style="color: #009900;">&#40;</span><span style="color: #993333;">long</span> <span style="color: #993333;">int</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            SIZEOF<span style="color: #009900;">&#40;</span><span style="color: #993333;">float</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            SIZEOF<span style="color: #009900;">&#40;</span><span style="color: #993333;">double</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            SIZEOF<span style="color: #009900;">&#40;</span><span style="color: #993333;">long</span> <span style="color: #993333;">double</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #b1b100;">return</span> <span style="color: #0000dd;">0</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    <span style="color: #339933;">&lt;/</span>stdlib<span style="color: #339933;">&gt;&lt;/</span>stdio<span style="color: #339933;">&gt;</span></pre></td></tr></table><p class="theCode" style="display:none;">#include &lt;stdio .h&gt;
    #include &lt;stdlib .h&gt;
    
    #define SIZEOF(x) printf( &quot;sizeof( %s ) = %d Bytes (%d bits)\n&quot;, #x, sizeof(x), sizeof(x)*8 )
    int main( void )
    {
            void *ptr;
            int valor;
    
            /* Compruebo que se pueda pasar de entero sin signo a puntero.
            * A grandes rasgos consiste en hacer creer al compilador que el
            * entero es una dirección de memoria. */
    
            valor = 5;
            printf( &quot;Valor inicial antes de la transformacion: %d\n&quot;, valor );
            ptr = (void *)valor;
            valor = (int)ptr;
            printf( &quot;Valor tras la transformacion: %d\n&quot;, valor );
    
            /* Compruebo que se pueda pasar de entero con signo a puntero.
            * A grandes rasgos consiste en hacer creer al compilador que el
            * entero es una dirección de memoria. */
    
            valor = -5;
            printf( &quot;Valor inicial antes de la transformacion: %d\n&quot;, valor );
            ptr = (void *)valor;
            valor = (int)ptr;
            printf( &quot;Valor tras la transformacion: %d\n&quot;, valor );
    
            /* Compruebo los tamaños de los distintos tipo de datos. El tipo 'void *'
            * es un puntero. Todos los puntero tienen el mismo tamaño en memoria,
            * por lo que no pruebo todas las combinaciones. */
    
            SIZEOF(void *);
            SIZEOF(char );
            SIZEOF(short int);
            SIZEOF(int );
            SIZEOF(long int);
            SIZEOF(float);
            SIZEOF(double);
            SIZEOF(long double);
            return 0;
    }
    &lt;/stdlib&gt;&lt;/stdio&gt;</p></div>
    ";}
categories:
  - Desarrollo
  - Personal

---
Esta entrada viene por un comentario realizado por <a target="_bank" href="http://planet.gentoo.org/developers/ferdy">ferdy</a> en <a target="_blank" href="http://blog.laparca.es/?p=96#comment-916">un comentario anterior</a>.

Para comprobar si lo que dije funcionaba, he hecho el siguiente programa:

<pre lang="c" line="1">#include &lt;stdio .h>
#include &lt;stdlib .h>

#define SIZEOF(x) printf( "sizeof( %s ) = %d Bytes (%d bits)\n", #x, sizeof(x), sizeof(x)*8 )
int main( void )
{
        void *ptr;
        int valor;

        /* Compruebo que se pueda pasar de entero sin signo a puntero.
        * A grandes rasgos consiste en hacer creer al compilador que el
        * entero es una dirección de memoria. */

        valor = 5;
        printf( "Valor inicial antes de la transformacion: %d\n", valor );
        ptr = (void *)valor;
        valor = (int)ptr;
        printf( "Valor tras la transformacion: %d\n", valor );

        /* Compruebo que se pueda pasar de entero con signo a puntero.
        * A grandes rasgos consiste en hacer creer al compilador que el
        * entero es una dirección de memoria. */

        valor = -5;
        printf( "Valor inicial antes de la transformacion: %d\n", valor );
        ptr = (void *)valor;
        valor = (int)ptr;
        printf( "Valor tras la transformacion: %d\n", valor );

        /* Compruebo los tamaños de los distintos tipo de datos. El tipo 'void *'
        * es un puntero. Todos los puntero tienen el mismo tamaño en memoria,
        * por lo que no pruebo todas las combinaciones. */

        SIZEOF(void *);
        SIZEOF(char );
        SIZEOF(short int);
        SIZEOF(int );
        SIZEOF(long int);
        SIZEOF(float);
        SIZEOF(double);
        SIZEOF(long double);
        return 0;
}
&lt;/stdlib>&lt;/stdio></pre>

No aconsejo a nadie utilizar este tipo de conversiones de tipos, ya que pueden dar problemas. Además, hacen que el código sea menos legible.

El resultado del código anterior sobre un procesador AMD Turion ML-28 con Debian Sid pure 64 es el siguiente:

<verbatim>  
Valor inicial antes de la transformacion: 5  
Valor tras la transformacion: 5  
Valor inicial antes de la transformacion: -5  
Valor tras la transformacion: -5  
sizeof( void * ) = 8 Bytes (64 bits)  
sizeof( char ) = 1 Bytes (8 bits)  
sizeof( short int ) = 2 Bytes (16 bits)  
sizeof( int ) = 4 Bytes (32 bits)  
sizeof( long int ) = 8 Bytes (64 bits)  
sizeof( float ) = 4 Bytes (32 bits)  
sizeof( double ) = 8 Bytes (64 bits)  
sizeof( long double ) = 16 Bytes (128 bits)  
</verbatim>

De este modo podemos ver que se podría, en teoría, convertir cualquier tipo de dato en puntero y almacenarlo en este (a excepción del tipo &#8216;long double&#8217;).

Como recomendación, es preferible realizar asignación dinámica de memoria para almacenar el entero (que es, supongo, la propuesta de ferdy) y luego transformar el puntero a entero a puntero genérico.

Con esto creo que ya está todo, pero si creéis que falta algo, decidlo.