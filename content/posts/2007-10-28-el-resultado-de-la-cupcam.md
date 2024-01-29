---
title: El resultado de la CUPCAM
author: laparca
type: post
date: 2007-10-28T09:40:22+00:00
url: /2007/10/28/el-resultado-de-la-cupcam/
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:9211:"
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
    49
    50
    51
    52
    </pre></td><td class="code"><pre class="c" style="font-family:monospace;"><span style="color: #339933;">#include stdlib.h</span>
    <span style="color: #339933;">#include stdio.h</span>
    &nbsp;
    <span style="color: #339933;">#define MAX 1001</span>
    &nbsp;
    <span style="color: #993333;">int</span> T<span style="color: #009900;">&#91;</span>MAX<span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> <span style="color: #009900;">&#123;</span> <span style="color: #339933;">-</span><span style="color: #0000dd;">1</span> <span style="color: #009900;">&#125;</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #993333;">int</span> max<span style="color: #009900;">&#40;</span><span style="color: #993333;">int</span> a<span style="color: #339933;">,</span> <span style="color: #993333;">int</span> b<span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>
       <span style="color: #b1b100;">return</span> a<span style="color: #339933;">&gt;=</span>b <span style="color: #339933;">?</span> a <span style="color: #339933;">:</span> b<span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;">/**
    * Pasamos cuanto espacio tenemos y el ultimo libro de la lista a comprobar.
    * Devuelve el maximo espacio que puede ocupar.
    */</span>
    <span style="color: #993333;">int</span> A<span style="color: #009900;">&#40;</span><span style="color: #993333;">int</span> espacio<span style="color: #339933;">,</span> <span style="color: #993333;">int</span> libros<span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>
       <span style="color: #993333;">int</span> a<span style="color: #339933;">,</span> b<span style="color: #339933;">;</span>
    &nbsp;
       <span style="color: #808080; font-style: italic;">/* Si el espacio libre es 0 o no hay libros que colocar, el espacio
       * que ocupamos es 0 */</span>
       <span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span> <span style="color: #339933;">!</span>espacio <span style="color: #339933;">||</span> <span style="color: #339933;">!</span>libros<span style="color: #009900;">&#41;</span> <span style="color: #b1b100;">return</span> <span style="color: #0000dd;">0</span><span style="color: #339933;">;</span>
    &nbsp;
       <span style="color: #808080; font-style: italic;">/* El libro ocupa mas que el espacio que tengo libre,
       * por lo que sigo sin tenerlo en cuenta */</span>
       <span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span> T<span style="color: #009900;">&#91;</span>libros<span style="color: #009900;">&#93;</span> <span style="color: #339933;">&gt;</span> espacio <span style="color: #009900;">&#41;</span> <span style="color: #b1b100;">return</span> A<span style="color: #009900;">&#40;</span>espacio<span style="color: #339933;">,</span> libros<span style="color: #339933;">-</span><span style="color: #0000dd;">1</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
       <span style="color: #808080; font-style: italic;">/* Si nuestro libro cabe, devolvemos el maximo entre poner
       * el libro actual e intentarlo con el resto o directamente
       * intentarlo con el resto sin tener en cuenta el libro
       * actual */</span>
       <span style="color: #b1b100;">return</span> max<span style="color: #009900;">&#40;</span> A<span style="color: #009900;">&#40;</span>espacio<span style="color: #339933;">,</span> libros<span style="color: #339933;">-</span><span style="color: #0000dd;">1</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">,</span> T<span style="color: #009900;">&#91;</span>libros<span style="color: #009900;">&#93;</span><span style="color: #339933;">+</span>A<span style="color: #009900;">&#40;</span>espacio<span style="color: #339933;">-</span>T<span style="color: #009900;">&#91;</span>libros<span style="color: #009900;">&#93;</span><span style="color: #339933;">,</span> libros<span style="color: #339933;">-</span><span style="color: #0000dd;">1</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #993333;">int</span> main<span style="color: #009900;">&#40;</span><span style="color: #993333;">void</span><span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>
       <span style="color: #993333;">int</span> i<span style="color: #339933;">;</span>
       <span style="color: #993333;">int</span> espacio<span style="color: #339933;">;</span>
       <span style="color: #993333;">int</span> num_libros<span style="color: #339933;">;</span>
    &nbsp;
       <span style="color: #b1b100;">while</span><span style="color: #009900;">&#40;</span><span style="color: #0000dd;">1</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #000066;">scanf</span><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">&quot;%d %d&quot;</span><span style="color: #339933;">,</span> <span style="color: #339933;">&amp;</span>espacio<span style="color: #339933;">,</span> <span style="color: #339933;">&amp;</span>num_libros<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span> espacio <span style="color: #339933;">==</span> <span style="color: #0000dd;">0</span> <span style="color: #339933;">&amp;&amp;</span> num_libros <span style="color: #339933;">==</span> <span style="color: #0000dd;">0</span> <span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">break</span><span style="color: #339933;">;</span>
    &nbsp;
          <span style="color: #b1b100;">for</span><span style="color: #009900;">&#40;</span>i <span style="color: #339933;">=</span> <span style="color: #0000dd;">1</span><span style="color: #339933;">;</span> i <span style="color: #339933;">&amp;</span>lt<span style="color: #339933;">;=</span> num_libros<span style="color: #339933;">;</span> i<span style="color: #339933;">++</span> <span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
             <span style="color: #000066;">scanf</span><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">&quot;%d&quot;</span><span style="color: #339933;">,</span> <span style="color: #339933;">&amp;</span><span style="color: #009900;">&#40;</span>T<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span>
          <span style="color: #000066;">printf</span><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">&quot;%d<span style="color: #000099; font-weight: bold;">\n</span>&quot;</span><span style="color: #339933;">,</span> espacio<span style="color: #339933;">-</span>A<span style="color: #009900;">&#40;</span>espacio<span style="color: #339933;">,</span> num_libros<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
       <span style="color: #009900;">&#125;</span>
       <span style="color: #b1b100;">return</span> <span style="color: #0000dd;">0</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">#include stdlib.h
    #include stdio.h
    
    #define MAX 1001
    
    int T[MAX] = { -1 };
    
    int max(int a, int b)
    {
       return a&gt;=b ? a : b;
    }
    
    /**
    * Pasamos cuanto espacio tenemos y el ultimo libro de la lista a comprobar.
    * Devuelve el maximo espacio que puede ocupar.
    */
    int A(int espacio, int libros)
    {
       int a, b;
    
       /* Si el espacio libre es 0 o no hay libros que colocar, el espacio
       * que ocupamos es 0 */
       if( !espacio || !libros) return 0;
    
       /* El libro ocupa mas que el espacio que tengo libre,
       * por lo que sigo sin tenerlo en cuenta */
       if( T[libros] &gt; espacio ) return A(espacio, libros-1);
    
       /* Si nuestro libro cabe, devolvemos el maximo entre poner
       * el libro actual e intentarlo con el resto o directamente
       * intentarlo con el resto sin tener en cuenta el libro
       * actual */
       return max( A(espacio, libros-1), T[libros]+A(espacio-T[libros], libros-1) );
    }
    
    int main(void)
    {
       int i;
       int espacio;
       int num_libros;
    
       while(1) {
          scanf(&quot;%d %d&quot;, &amp;espacio, &amp;num_libros);
          if( espacio == 0 &amp;&amp; num_libros == 0 ) break;
    
          for(i = 1; i &amp;lt;= num_libros; i++ ) {
             scanf(&quot;%d&quot;, &amp;(T[i]));
          }
          printf(&quot;%d\n&quot;, espacio-A(espacio, num_libros));
       }
       return 0;
    }</p></div>
    ";i:2;s:10189:"
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
    49
    50
    51
    52
    53
    </pre></td><td class="code"><pre class="c" style="font-family:monospace;"><span style="color: #339933;">#include stdlib.h</span>
    <span style="color: #339933;">#include stdio.h</span>
    &nbsp;
    <span style="color: #339933;">#define MAX 1001</span>
    &nbsp;
    <span style="color: #993333;">int</span> T<span style="color: #009900;">&#91;</span>MAX<span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> <span style="color: #009900;">&#123;</span> <span style="color: #339933;">-</span><span style="color: #0000dd;">1</span> <span style="color: #009900;">&#125;</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #993333;">int</span> max<span style="color: #009900;">&#40;</span><span style="color: #993333;">int</span> a<span style="color: #339933;">,</span> <span style="color: #993333;">int</span> b<span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>
       <span style="color: #b1b100;">return</span> a<span style="color: #339933;">&gt;=</span>b <span style="color: #339933;">?</span> a <span style="color: #339933;">:</span> b<span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;">/**
    * Pasamos la lista de libros, el espacio que queda libre y el total de libros en la lista.
    */</span>
    <span style="color: #993333;">int</span> A<span style="color: #009900;">&#40;</span><span style="color: #993333;">int</span> <span style="color: #339933;">*</span>tamanos<span style="color: #339933;">,</span> <span style="color: #993333;">int</span> espacio<span style="color: #339933;">,</span> <span style="color: #993333;">int</span> libros<span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>
       <span style="color: #993333;">int</span> c<span style="color: #339933;">;</span>
       <span style="color: #993333;">int</span> resultado <span style="color: #339933;">=</span> espacio<span style="color: #339933;">;</span>
       <span style="color: #993333;">int</span> temporal<span style="color: #339933;">;</span>
    &nbsp;
       <span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span> <span style="color: #339933;">!</span>libros <span style="color: #009900;">&#41;</span> <span style="color: #b1b100;">return</span> espacio<span style="color: #339933;">;</span>
    &nbsp;
       <span style="color: #808080; font-style: italic;">/* Calculamos el espacio libre teniendo en cuenta que usamos el libro actual */</span>
       <span style="color: #b1b100;">for</span><span style="color: #009900;">&#40;</span>c<span style="color: #339933;">=</span><span style="color: #0000dd;">1</span><span style="color: #339933;">;</span> c <span style="color: #339933;">&lt;</span> libros<span style="color: #339933;">;</span> c<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          temporal <span style="color: #339933;">=</span> A<span style="color: #009900;">&#40;</span>tamanos<span style="color: #009900;">&#91;</span>c<span style="color: #009900;">&#93;</span><span style="color: #339933;">,</span> espacio<span style="color: #339933;">-</span>tamanos<span style="color: #009900;">&#91;</span><span style="color: #0000dd;">0</span><span style="color: #009900;">&#93;</span><span style="color: #339933;">,</span> libros<span style="color: #339933;">-</span><span style="color: #0000dd;">1</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span>temporal<span style="color: #339933;">&lt;</span>resultado <span style="color: #009900;">&#41;</span> resultado <span style="color: #339933;">=</span> temporal<span style="color: #339933;">;</span>    
       <span style="color: #009900;">&#125;</span>
       <span style="color: #808080; font-style: italic;">/* Calculamos el espacio libre sin tener en cuenta que usamos el libro actual */</span>
       <span style="color: #b1b100;">for</span><span style="color: #009900;">&#40;</span>c<span style="color: #339933;">=</span><span style="color: #0000dd;">1</span><span style="color: #339933;">;</span> c <span style="color: #339933;">&lt;</span> libros<span style="color: #339933;">;</span> c<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          temporal <span style="color: #339933;">=</span> A<span style="color: #009900;">&#40;</span>tamanos<span style="color: #009900;">&#91;</span>c<span style="color: #009900;">&#93;</span><span style="color: #339933;">,</span> espacio<span style="color: #339933;">,</span> libros<span style="color: #339933;">-</span><span style="color: #0000dd;">1</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span>temporal <span style="color: #339933;">&lt;</span> resultado <span style="color: #009900;">&#41;</span> resultado <span style="color: #339933;">=</span> temporal<span style="color: #339933;">;</span>
       <span style="color: #009900;">&#125;</span>
       <span style="color: #b1b100;">return</span> resultado<span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #993333;">int</span> main<span style="color: #009900;">&#40;</span><span style="color: #993333;">void</span><span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>
       <span style="color: #993333;">int</span> i<span style="color: #339933;">;</span>
       <span style="color: #993333;">int</span> espacio<span style="color: #339933;">;</span>
       <span style="color: #993333;">int</span> num_libros<span style="color: #339933;">;</span>
    &nbsp;
       <span style="color: #b1b100;">while</span><span style="color: #009900;">&#40;</span><span style="color: #0000dd;">1</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #000066;">scanf</span><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">&quot;%d %d&quot;</span><span style="color: #339933;">,</span> <span style="color: #339933;">&amp;</span>espacio<span style="color: #339933;">,</span> <span style="color: #339933;">&amp;</span>num_libros<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span> espacio <span style="color: #339933;">==</span> <span style="color: #0000dd;">0</span> <span style="color: #339933;">&amp;&amp;</span> num_libros <span style="color: #339933;">==</span> <span style="color: #0000dd;">0</span> <span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">break</span><span style="color: #339933;">;</span>
    &nbsp;
          <span style="color: #b1b100;">for</span><span style="color: #009900;">&#40;</span>i <span style="color: #339933;">=</span> <span style="color: #0000dd;">1</span><span style="color: #339933;">;</span> i <span style="color: #339933;">&amp;</span>lt<span style="color: #339933;">;=</span> num_libros<span style="color: #339933;">;</span> i<span style="color: #339933;">++</span> <span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
             <span style="color: #000066;">scanf</span><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">&quot;%d&quot;</span><span style="color: #339933;">,</span> <span style="color: #339933;">&amp;</span>a<span style="color: #009900;">&#40;</span>T<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span>
          <span style="color: #000066;">printf</span><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">&quot;%d<span style="color: #000099; font-weight: bold;">\n</span>&quot;</span><span style="color: #339933;">,</span> A<span style="color: #009900;">&#40;</span>espacio<span style="color: #339933;">,</span> num_libros<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
       <span style="color: #009900;">&#125;</span>
       <span style="color: #b1b100;">return</span> <span style="color: #0000dd;">0</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">#include stdlib.h
    #include stdio.h
    
    #define MAX 1001
    
    int T[MAX] = { -1 };
    
    int max(int a, int b)
    {
       return a&gt;=b ? a : b;
    }
    
    /**
    * Pasamos la lista de libros, el espacio que queda libre y el total de libros en la lista.
    */
    int A(int *tamanos, int espacio, int libros)
    {
       int c;
       int resultado = espacio;
       int temporal;
    
       if( !libros ) return espacio;
    
       /* Calculamos el espacio libre teniendo en cuenta que usamos el libro actual */
       for(c=1; c &lt; libros; c++) {
          temporal = A(tamanos[c], espacio-tamanos[0], libros-1);
          if(temporal&lt;resultado ) resultado = temporal;    
       }
       /* Calculamos el espacio libre sin tener en cuenta que usamos el libro actual */
       for(c=1; c &lt; libros; c++) {
          temporal = A(tamanos[c], espacio, libros-1);
          if(temporal &lt; resultado ) resultado = temporal;
       }
       return resultado;
    }
    
    int main(void)
    {
       int i;
       int espacio;
       int num_libros;
    
       while(1) {
          scanf(&quot;%d %d&quot;, &amp;espacio, &amp;num_libros);
          if( espacio == 0 &amp;&amp; num_libros == 0 ) break;
    
          for(i = 1; i &amp;lt;= num_libros; i++ ) {
             scanf(&quot;%d&quot;, &amp;a(T[i]));
          }
          printf(&quot;%d\n&quot;, A(espacio, num_libros));
       }
       return 0;
    }</p></div>
    ";}
categories:
  - Desarrollo
  - Personal

---
Y al final todo llega y nosotros no hicimos buen papel 🙁 Fuimos un total de 19 grupos a participar y nosotros quedamos en el puesto 11 :'(. De todos modos volveremos el año próximo y venceremos.

De momento decir que me quedé pillado con un problema y analizando la solución era igual que la mia, solo que yo no me di cuenta de una cosa y hacía que el tiempo de ejecución de m algoritmo tendiese a infinito 🙁

La solución del problema es la siguiente. Muchos reconocerán en ella el algoritmo de la mochila o de la estantería. El caso es que yo nunca había oído hablar de él.

<pre lang="c" line="1">#include stdlib.h
#include stdio.h

#define MAX 1001

int T[MAX] = { -1 };

int max(int a, int b)
{
   return a>=b ? a : b;
}

/**
* Pasamos cuanto espacio tenemos y el ultimo libro de la lista a comprobar.
* Devuelve el maximo espacio que puede ocupar.
*/
int A(int espacio, int libros)
{
   int a, b;

   /* Si el espacio libre es 0 o no hay libros que colocar, el espacio
   * que ocupamos es 0 */
   if( !espacio || !libros) return 0;

   /* El libro ocupa mas que el espacio que tengo libre,
   * por lo que sigo sin tenerlo en cuenta */
   if( T[libros] > espacio ) return A(espacio, libros-1);

   /* Si nuestro libro cabe, devolvemos el maximo entre poner
   * el libro actual e intentarlo con el resto o directamente
   * intentarlo con el resto sin tener en cuenta el libro
   * actual */
   return max( A(espacio, libros-1), T[libros]+A(espacio-T[libros], libros-1) );
}

int main(void)
{
   int i;
   int espacio;
   int num_libros;

   while(1) {
      scanf("%d %d", &espacio, &num_libros);
      if( espacio == 0 && num_libros == 0 ) break;

      for(i = 1; i &lt;= num_libros; i++ ) {
         scanf("%d", &(T[i]));
      }
      printf("%d\n", espacio-A(espacio, num_libros));
   }
   return 0;
}
</pre>

La solución que yo hice era más como la que sigue:

<pre lang="c" line="1">#include stdlib.h
#include stdio.h

#define MAX 1001

int T[MAX] = { -1 };

int max(int a, int b)
{
   return a>=b ? a : b;
}

/**
* Pasamos la lista de libros, el espacio que queda libre y el total de libros en la lista.
*/
int A(int *tamanos, int espacio, int libros)
{
   int c;
   int resultado = espacio;
   int temporal;

   if( !libros ) return espacio;

   /* Calculamos el espacio libre teniendo en cuenta que usamos el libro actual */
   for(c=1; c &lt; libros; c++) {
      temporal = A(tamanos[c], espacio-tamanos[0], libros-1);
      if(temporal&lt;resultado ) resultado = temporal;    
   }
   /* Calculamos el espacio libre sin tener en cuenta que usamos el libro actual */
   for(c=1; c &lt; libros; c++) {
      temporal = A(tamanos[c], espacio, libros-1);
      if(temporal &lt; resultado ) resultado = temporal;
   }
   return resultado;
}

int main(void)
{
   int i;
   int espacio;
   int num_libros;

   while(1) {
      scanf("%d %d", &#038;espacio, &#038;num_libros);
      if( espacio == 0 &#038;&#038; num_libros == 0 ) break;

      for(i = 1; i &lt;= num_libros; i++ ) {
         scanf("%d", &#038;a(T[i]));
      }
      printf("%d\n", A(espacio, num_libros));
   }
   return 0;
}
</pre>

Ahora no recuerdo muy bien si era esactamente así, pero sí se que funcionaba. Como podéis comprobar, nuestro gran fallo (bueno, mi gran fallo) fue que pasaba muchas veces por las mismas convinaciones :@ El bucle ese fue mortal y no nos dismo cuenta ninguno que se podía quitar :'(

La próxima vez lo haremos mejor.