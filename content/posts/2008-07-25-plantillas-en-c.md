---
title: Plantillas en C++
author: laparca
type: post
date: 2008-07-25T10:55:28+00:00
url: /2008/07/25/plantillas-en-c/
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:2550:"
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
    </pre></td><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #0000ff;">template</span><span style="color: #000080;">&lt;</span><span style="color: #0000ff;">typename</span> T, <span style="color: #0000ff;">int</span> S<span style="color: #000080;">&gt;</span>
    <span style="color: #0000ff;">class</span> array
    <span style="color: #008000;">&#123;</span>
    <span style="color: #0000ff;">private</span><span style="color: #008080;">:</span>
       T <span style="color: #000040;">*</span>ptr<span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #0000ff;">public</span><span style="color: #008080;">:</span>
       array<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span>
       <span style="color: #008000;">&#123;</span>
          ptr <span style="color: #000080;">=</span> <span style="color: #0000dd;">new</span> T<span style="color: #008000;">&#91;</span>S<span style="color: #008000;">&#93;</span><span style="color: #008080;">;</span>
       <span style="color: #008000;">&#125;</span>
    &nbsp;
       T<span style="color: #000040;">&amp;</span> operator<span style="color: #008000;">&#91;</span><span style="color: #008000;">&#93;</span><span style="color: #008000;">&#40;</span><span style="color: #0000ff;">int</span> idx<span style="color: #008000;">&#41;</span>
       <span style="color: #008000;">&#123;</span>
          <span style="color: #0000ff;">return</span> T<span style="color: #008000;">&#91;</span>idx<span style="color: #008000;">&#93;</span><span style="color: #008080;">;</span>
       <span style="color: #008000;">&#125;</span>
    &nbsp;
       <span style="color: #0000ff;">int</span> size<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span>
       <span style="color: #008000;">&#123;</span>
          <span style="color: #0000ff;">return</span> S<span style="color: #008080;">;</span>
       <span style="color: #008000;">&#125;</span>
    <span style="color: #008000;">&#125;</span><span style="color: #008080;">;</span>
    <span style="color: #666666;">//&lt;/typename&gt;</span></pre></td></tr></table><p class="theCode" style="display:none;">template&lt;typename T, int S&gt;
    class array
    {
    private:
       T *ptr;
    
    public:
       array()
       {
          ptr = new T[S];
       }
    
       T&amp; operator[](int idx)
       {
          return T[idx];
       }
    
       int size()
       {
          return S;
       }
    };
    //&lt;/typename&gt;</p></div>
    ";i:2;s:1901:"
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
    </pre></td><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #0000ff;">int</span> main<span style="color: #008000;">&#40;</span><span style="color: #0000ff;">void</span><span style="color: #008000;">&#41;</span>
    <span style="color: #008000;">&#123;</span>
       <span style="color: #0000ff;">using</span> <span style="color: #0000ff;">namespace</span> std<span style="color: #008080;">;</span>
    &nbsp;
       array<span style="color: #000080;">&lt;</span><span style="color: #0000ff;">int</span> , <span style="color: #0000dd;">5</span><span style="color: #000080;">&gt;</span> a<span style="color: #008080;">;</span>
       <span style="color: #0000dd;">cout</span> <span style="color: #000080;">&lt;</span> <span style="color: #000080;">&lt;</span> <span style="color: #FF0000;">&quot;Tamaño del array: &quot;</span> <span style="color: #000080;">&lt;&lt;</span> a.<span style="color: #007788;">size</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #000080;">&lt;&lt;</span> endl<span style="color: #008080;">;</span>
       a<span style="color: #008000;">&#91;</span><span style="color: #0000dd;">1</span><span style="color: #008000;">&#93;</span> <span style="color: #000080;">=</span> <span style="color: #0000dd;">5</span><span style="color: #008080;">;</span>
    &nbsp;
       <span style="color: #0000ff;">return</span> <span style="color: #0000dd;">0</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">int main(void)
    {
       using namespace std;
    
       array&lt;int , 5&gt; a;
       cout &lt; &lt; &quot;Tamaño del array: &quot; &lt;&lt; a.size() &lt;&lt; endl;
       a[1] = 5;
    
       return 0;
    }</p></div>
    ";i:3;s:1132:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    2
    3
    4
    5
    6
    </pre></td><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #0000ff;">template</span><span style="color: #000080;">&lt;</span><span style="color: #0000ff;">typename</span> T<span style="color: #000080;">&gt;</span>
    T<span style="color: #000040;">&amp;</span> mayor<span style="color: #008000;">&#40;</span>T<span style="color: #000040;">&amp;</span> a, T<span style="color: #000040;">&amp;</span> b<span style="color: #008000;">&#41;</span>
    <span style="color: #008000;">&#123;</span>
       <span style="color: #0000ff;">return</span> a <span style="color: #000080;">&gt;=</span> b <span style="color: #008080;">?</span> a <span style="color: #008080;">:</span> b<span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    <span style="color: #666666;">//&lt;/typename&gt;</span></pre></td></tr></table><p class="theCode" style="display:none;">template&lt;typename T&gt;
    T&amp; mayor(T&amp; a, T&amp; b)
    {
       return a &gt;= b ? a : b;
    }
    //&lt;/typename&gt;</p></div>
    ";}
categories:
  - Desarrollo
tags:
  - c++
  - cpp
  - Desarrollo
  - plantillas
  - programacion
  - templates

---
Recuerdo cuando empecé a aprender C++ que la cosa que menos entendía era el uso de plantillas. Debo reconocer que me ha costado mucho comprender como funciona porque era algo completamente diferente a lo que hasta entonces había visto.

Por otro lado, hemos visto en los últimos tiempos como gran cantidad de arquitecturas han copiado el modelo para implementarlo a su modo. Aquí es donde vemos los genéricos de Java y de .Net. El problema es que no tienen ni de cerca la misma potencia que el sistema de C++, pero que como ventaja consumen menos espacio de ejecutable.

Para entrar un poco en materia, comentar que las plantillas de C++ son como documentos en los que dejamos lineas en blanco y luego las rellenamos cuando ya sabemos qué queremos poner en ahí. Pero en C++ no ha líneas en blanco, estas tienen nombre.

La principal ventaja de este sistema es que permite programar clases genéricas, como pueda ser una clase lista que automáticamente se adapte al tipo que debe contener. La segunda ventaja es el rendimiento, por el mismo motivo anterior.

Para empezar a ver un poco como va la cosa vamos a ver un ejemplo sencillo de plantilla:

<pre lang="cpp" line="1">template&lt;typename T, int S>
class array
{
private:
   T *ptr;

public:
   array()
   {
      ptr = new T[S];
   }

   T& operator[](int idx)
   {
      return T[idx];
   }

   int size()
   {
      return S;
   }
};
//&lt;/typename>
</pre>

Como vemos, hemos utilizado la palabra reservada _template_ para indicar que se trata de una plantilla y luego, entre los símbolos < y > hemos introducido la lista de elementos de la plantilla. Estos elementos son los tipos y nombres de los valores a sustituir. En este caso son _T_ de tipo _typename_ y _S_ de tipo _int_. Esto significa que cada vez que dentro de la clase aparezca _T_ deberá sustituirse por su corresponditente valor pasado en la plantilla y que necesariamente deberá ser un tipo de dato (por ejemplo un _int_, una clase, etc.) y que cada vez que aparezca _S_ deberá sustituirse por su valor que deberá ser un número entero. Para utilizar la plantilla sólo deberemos hacer lo siguiente:

<pre lang="cpp" line="1">int main(void)
{
   using namespace std;

   array&lt;int , 5> a;
   cout &lt; &lt; "Tamaño del array: " &lt;&lt; a.size() &lt;&lt; endl;
   a[1] = 5;

   return 0;
}
</pre>

Como vemos, lo único que hemos hecho ha sido añadir al nombre del la clase la lista de argumentos. En este caso concreto, deberá devolver que el tamaño es 5, que es el indicado en el parámetro de la plantilla.

Si nos fijamos en bibliotecas como STL o Boost, hacen un uso intensivo de las plantillas. El principal motivo es que C++ está optimizado para funcionar con plantillas, así que se prefieren al uso de mecanismos como la herencia. Además, la herencia hace que las llamadas a métodos sean más lentos, por lo que también se evita. Es en este momento cuando nos podemos preguntar el cómo hace C++ entonces para garantizar que se implementan ciertas funcionalidades. Por ejemplo, si queremos tener una lista ordenada, nos interesa que los elementos de la lista puedan compararse entre ellos con el operador _<=_. Pues la respuesta es sencilla: en la clase de plantilla simplemente utilizamos ese método y en tiempo de compilación se comprueba si está o no. Por ejemplo:

<pre lang="cpp" line="1">template&lt;typename T>
T& mayor(T& a, T& b)
{
   return a >= b ? a : b;
}
//&lt;/typename>
</pre>

Hemos creado una función _mayor_ que devuelve el mayor de dos elementos de tipo _T_. Los elementos de tipo _T_ deben sobrecargar el operador _>=_ para que funcione. Como se ve, no es necesario hacer herencia de ningún tipo, el compilador detecta automáticamente si está o no sobrecargado y dará el correspondiente error en caso necesario (si miramos el caso de Java o de .Net veremos como sí es necesario hacer herencia para que el mecanismo de genéricos funcione de este modo).

Debo decir que el tema de las plantillas está muy bien y se puede hacer muchas cosas interesantes, como la clase array, que funciona igual que un array y que tiene un rendimiento muy parecido (benditos métodos _inline_ de C++).

Otro día, seguiré hablando sobre plantillas, que dan para mucho.</int>