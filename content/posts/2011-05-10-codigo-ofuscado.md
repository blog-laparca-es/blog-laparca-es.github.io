---
title: Código ofuscado
author: laparca
type: post
date: 2011-05-10T10:36:27+00:00
url: /2011/05/10/codigo-ofuscado/
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:883:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="c" style="font-family:monospace;"><span style="color: #993333;">int</span> main<span style="color: #009900;">&#40;</span><span style="color: #993333;">void</span><span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>
       <span style="color: #000066;">printf</span><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">&quot;Hola, mundo&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
       <span style="color: #b1b100;">return</span> <span style="color: #0000dd;">0</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">int main(void)
    {
       printf(&quot;Hola, mundo&quot;);
       return 0;
    }</p></div>
    ";i:2;s:1951:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="c" style="font-family:monospace;"><span style="color: #339933;">#define __ main</span>
    <span style="color: #339933;">#define ___ printf</span>
    <span style="color: #993333;">int</span>
    __<span style="color: #009900;">&#40;</span><span style="color: #993333;">int</span> _<span style="color: #339933;">,</span> <span style="color: #993333;">char</span> <span style="color: #339933;">**</span>b<span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>
       <span style="color: #b1b100;">return</span> <span style="color: #009900;">&#40;</span>_ <span style="color: #339933;">&amp;</span>gt<span style="color: #339933;">;</span> <span style="color: #0000dd;">0</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">?</span> <span style="color: #009900;">&#40;</span><span style="color: #009900;">&#40;</span>_<span style="color: #339933;">==</span><span style="color: #0000dd;">1</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">?</span>__<span style="color: #009900;">&#40;</span>_<span style="color: #339933;">-</span><span style="color: #0000dd;">1</span><span style="color: #339933;">,</span> <span style="color: #0000dd;">0</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">:</span><span style="color: #0000dd;">0</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">:</span>___<span style="color: #009900;">&#40;</span><span style="color: #ff0000;">&quot;Hola, mundo&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">#define __ main
    #define ___ printf
    int
    __(int _, char **b)
    {
       return (_ &amp;gt; 0)? ((_==1)?__(_-1, 0):0):___(&quot;Hola, mundo&quot;);
    }</p></div>
    ";}
categories:
  - Desarrollo
  - Personal
tags:
  - c++
  - codigo
  - ofuscado

---
Muchos de los que leen este blog seguro que ya saben a qué me refiero por código ofuscado. Si es ese el caso, probablemente lo que cuente a continuación ya lo sepas. Para los demás, si os apetece ver las cosas que un friki de la programación puede hacer cuando se aburre, continúa leyendo.

El código ofuscado es, según la Wikipedia el «[..] acto deliberado de realizar un cambio no destructivo, ya sea en el [código fuente][1] de un [programa informático][2] o [código máquina][3]cuando el programa está en forma [compilada][4] o binaria, con el fin de que no sea fácil de entender o leer». De cara al programado que quiere echarse unas risas es hacer un programa correcto pero que no pueda entenderse leyéndolo. ¿Y eso por qué? Porque podemos.

Imaginemos algo sencillo: en C hacer un programa que muestre por pantalla un «Hola, mundo» es algo tan aburrido como lo siguiente:

<pre lang="c">int main(void)
{
   printf("Hola, mundo");
   return 0;
}</pre>

Sin duda algo muy soso, sería más divertido una cosa como la siguiente:

<pre lang="c">#define __ main
#define ___ printf
int
__(int _, char **b)
{
   return (_ &gt; 0)? ((_==1)?__(_-1, 0):0):___("Hola, mundo");
}</pre>

Ahora mismo no sé si funciona, pero como podéis comprobar es muuuucho más clarooooo (entiendase el sarcasmo). Ya lo único que le faltaría es ocultar el mensaje de algún modo estrafalario.

A parte de las connotaciones divertidas que pueda tener la ofuscación de código (hay códigos con forma de avión, círculos, etc.), también sirve para reducir el tamaño del código de ciertos programas. Por ejemplo, en el mundo de la web, los códigos javascript se suelen comprimir utilizando técnicas de sustitución parecidas a las de la ofuscación para que ocupen menos y se transmitan más rápido por la red.

También hay quien utiliza este tipo de códigos para evitar que se copien los algoritmos utilizados y que no se pueda hacer ingeniería inversa.

 [1]: http://es.wikipedia.org/wiki/C%C3%B3digo_fuente
 [2]: http://es.wikipedia.org/wiki/Programa_inform%C3%A1tico
 [3]: http://es.wikipedia.org/wiki/C%C3%B3digo_m%C3%A1quina "Código máquina"
 [4]: http://es.wikipedia.org/wiki/Compilador "Compilador"