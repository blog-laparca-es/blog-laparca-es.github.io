---
title: Punteros inteligentes en C++ (smart pointers)
author: laparca
type: post
date: 2007-08-04T20:57:41+00:00
url: /2007/08/04/punteros-inteligentes-en-c-smart-pointers/
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:3755:"
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
    </pre></td><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #ff0000; font-style: italic;">/**
    * PtrSimple permite el manejo de la memoria de forma sencilla dentro de un cuerpo de sentencias.
    * Los punteros manejados por el no deben ser liberados por el programador ni deberían utilizarse
    * de otro modo que no sea a través de esta clase.
    */</span>
    <span style="color: #0000ff;">template</span><span style="color: #000080;">&lt;</span><span style="color: #0000ff;">typename</span> _T<span style="color: #000080;">&gt;</span> <span style="color: #0000ff;">class</span> PtrSimple <span style="color: #008000;">&#123;</span>
    <span style="color: #0000ff;">private</span><span style="color: #008080;">:</span>
       _T <span style="color: #000040;">*</span>_ptr<span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #0000ff;">public</span><span style="color: #008080;">:</span>
       PtrSimple<span style="color: #008000;">&#40;</span> _T<span style="color: #000040;">*</span> ptr <span style="color: #000080;">=</span> <span style="color: #0000ff;">NULL</span> <span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
          _ptr <span style="color: #000080;">=</span> ptr<span style="color: #008080;">;</span>
       <span style="color: #008000;">&#125;</span>
       ~PtrSimple<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
          <span style="color: #0000ff;">if</span><span style="color: #008000;">&#40;</span> _ptr <span style="color: #000040;">!</span><span style="color: #000080;">=</span> <span style="color: #0000ff;">NULL</span> <span style="color: #008000;">&#41;</span>
             <span style="color: #0000dd;">delete</span> _ptr<span style="color: #008080;">;</span>
       <span style="color: #008000;">&#125;</span>
    &nbsp;
       T<span style="color: #000040;">*</span> operator<span style="color: #000040;">-</span><span style="color: #000080;">&gt;</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
          <span style="color: #0000ff;">return</span> _ptr<span style="color: #008080;">;</span>
       <span style="color: #008000;">&#125;</span>
    &nbsp;
       T<span style="color: #000040;">&amp;</span> operator<span style="color: #000040;">*</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
          <span style="color: #0000ff;">return</span> <span style="color: #000040;">*</span>_ptr<span style="color: #008080;">;</span>
       <span style="color: #008000;">&#125;</span>
    <span style="color: #008000;">&#125;</span><span style="color: #008080;">;</span>
    <span style="color: #666666;">// Esto es para que no me falle en wordpress :P : &lt;/typename&gt;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * PtrSimple permite el manejo de la memoria de forma sencilla dentro de un cuerpo de sentencias.
    * Los punteros manejados por el no deben ser liberados por el programador ni deberían utilizarse
    * de otro modo que no sea a través de esta clase.
    */
    template&lt;typename _T&gt; class PtrSimple {
    private:
       _T *_ptr;
    
    public:
       PtrSimple( _T* ptr = NULL ) {
          _ptr = ptr;
       }
       ~PtrSimple() {
          if( _ptr != NULL )
             delete _ptr;
       }
    
       T* operator-&gt;() {
          return _ptr;
       }
    
       T&amp; operator*() {
          return *_ptr;
       }
    };
    // Esto es para que no me falle en wordpress :P : &lt;/typename&gt;</p></div>
    ";}
categories:
  - Desarrollo

---
Para mucha gente, la lacra de programar en C/C++ frente a otros lenguajes es el tener que liberar memoria y controlar donde se libera ésta. Es cierto que el control que dan estos lenguajes al programador es mucho y permite hacer cosas magnificas, pero hay que reconocerlo: somos vagos. En este sentido, se puede hacer en C++ una cosa denominada punteros inteligentes que pueden liberar memoria cuando esta ya no sea necesaria.

Los punteros inteligentes son un tipo de clase que haciendo uso de plantillas son capaces de comportarse como punteros y, segun su implementación, liberar la memoria cuando haga falta. Por contra, esto supone un decremento del rendimiento de la aplicación que habrá que considerar antes de utilizarlos.

<a href="http://www.google.es/search?q=smart+pointers&#038;ie=utf-8&#038;oe=utf-8&#038;aq=t&#038;rls=com.ubuntu:en-US:official&#038;client=firefox-a" target="_blank">Hay una gran cantidad de implementaciones en internet</a>, pero aquí sólo me voy a centrar en la idea básica de todas ellas. Para empezar podemos considerar tres tipos de políticas de manejo de punteros:

  * **Agresivas**: que consisten en mantener un contador de copias por cada puntero en el sistema (es el mecanismo más lento).
  * **Simple**: sólo se considera un puntero, no puede asignarse a otros, por lo que no se necesita ningún tipo de contador (es el mecanismo más rápido).
  * **Intermedio**: cualquier política de uso que se encuentre entre simple y agresiva (su rendimiento será dependiente del tipo de política).

Como ejemplo de puntero que sigue una política simple podemos considerar el siguiente:

<pre lang="cpp" line="1">/**
* PtrSimple permite el manejo de la memoria de forma sencilla dentro de un cuerpo de sentencias.
* Los punteros manejados por el no deben ser liberados por el programador ni deberían utilizarse
* de otro modo que no sea a través de esta clase.
*/
template&lt;typename _T> class PtrSimple {
private:
   _T *_ptr;

public:
   PtrSimple( _T* ptr = NULL ) {
      _ptr = ptr;
   }
   ~PtrSimple() {
      if( _ptr != NULL )
         delete _ptr;
   }

   T* operator->() {
      return _ptr;
   }

   T& operator*() {
      return *_ptr;
   }
};
// Esto es para que no me falle en wordpress :P : &lt;/typename>
</pre>

Sin duda este es el tipo de puntero más sencillo que se puede hacer, ya que sólo controla un único puntero, no pudiendo ser asignado a otra clase, lo que limita mucho sus posibilidades a su uso en un único método. A partir de este se puede empezar a trabajar para añadirle funcionalidades (cosa que dejaré para otra entrada).

De momento lo dejo aquí para no alargar más la cosa. A ver si en un par de días saco otro artículo para seguir con el tema. Ahora a esperar que ferdy me crucifique 😛