---
title: Punteros inteligentes en C++ (smart pointers) 2
author: laparca
type: post
date: 2007-08-05T10:39:23+00:00
url: /2007/08/05/punteros-inteligentes-en-c-smart-pointers-2/
wp-syntax-cache-content:
  - |
    a:5:{i:1;s:4885:"
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
    </pre></td><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #339900;">#include &lt;iostream&gt;</span>
    <span style="color: #0000ff;">using</span> std<span style="color: #008080;">::</span><span style="color: #0000dd;">cout</span><span style="color: #008080;">;</span>
    <span style="color: #0000ff;">using</span> std<span style="color: #008080;">::</span><span style="color: #007788;">endl</span><span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #666666;">// Aqui iría nuestra clase de puntero simple</span>
    <span style="color: #666666;">// template...</span>
    &nbsp;
    <span style="color: #666666;">// Clase de ejemplo para mostrar el uso de los punteros inteligentes</span>
    <span style="color: #0000ff;">class</span> UnaClase <span style="color: #008000;">&#123;</span>
       UnaClase<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
          <span style="color: #0000dd;">cout</span> <span style="color: #000080;">&lt;</span> <span style="color: #000080;">&lt;</span> <span style="color: #FF0000;">&quot;Soy UnaClase y me estan creando&quot;</span> <span style="color: #000080;">&lt;&lt;</span> endl<span style="color: #008080;">;</span>
       <span style="color: #008000;">&#125;</span>
       ~UnaClase<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
          <span style="color: #0000dd;">cout</span> <span style="color: #000080;">&lt;&lt;</span> <span style="color: #FF0000;">&quot;Soy UnaClase y me están destruyendo&quot;</span> <span style="color: #000080;">&lt;&lt;</span> endl<span style="color: #008080;">;</span>
       <span style="color: #008000;">&#125;</span>
       <span style="color: #0000ff;">void</span> hacerAlgo<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
          <span style="color: #0000dd;">cout</span> <span style="color: #000080;">&lt;&lt;</span> <span style="color: #FF0000;">&quot;Soy UnaClase y estoy haciendo algo útil&quot;</span> <span style="color: #000080;">&lt;&lt;</span> endl<span style="color: #008080;">;</span>
       <span style="color: #008000;">&#125;</span>
    <span style="color: #008000;">&#125;</span><span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #0000ff;">int</span> main<span style="color: #008000;">&#40;</span> <span style="color: #0000ff;">void</span> <span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
       PtrSimple<span style="color: #000080;">&lt;</span>UnaClase<span style="color: #000080;">&gt;</span> ptrUnaClase <span style="color: #000080;">=</span> <span style="color: #0000dd;">new</span> UnaClase<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    &nbsp;
       <span style="color: #666666;">// Llamamos al método hacerAlgo de UnaClase a través del puntero inteligente.</span>
       ptrUnaClase<span style="color: #000040;">-</span><span style="color: #000080;">&gt;</span>hacerAlgo<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    &nbsp;
       <span style="color: #666666;">// En este punto, C++ destruye la instancia a PtrSimple, eliminando automáticamente</span>
       <span style="color: #666666;">// la memoria ocupada por este.</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    <span style="color: #666666;">// Para evitar fallos en wordpress:</span>
    <span style="color: #666666;">// </span>
    <span style="color: #666666;">// &lt;/iostream&gt;</span></pre></td></tr></table><p class="theCode" style="display:none;">#include &lt;iostream&gt;
    using std::cout;
    using std::endl;
    
    // Aqui iría nuestra clase de puntero simple
    // template...
    
    // Clase de ejemplo para mostrar el uso de los punteros inteligentes
    class UnaClase {
       UnaClase() {
          cout &lt; &lt; &quot;Soy UnaClase y me estan creando&quot; &lt;&lt; endl;
       }
       ~UnaClase() {
          cout &lt;&lt; &quot;Soy UnaClase y me están destruyendo&quot; &lt;&lt; endl;
       }
       void hacerAlgo() {
          cout &lt;&lt; &quot;Soy UnaClase y estoy haciendo algo útil&quot; &lt;&lt; endl;
       }
    };
    
    int main( void ) {
       PtrSimple&lt;UnaClase&gt; ptrUnaClase = new UnaClase();
    
       // Llamamos al método hacerAlgo de UnaClase a través del puntero inteligente.
       ptrUnaClase-&gt;hacerAlgo();
    
       // En este punto, C++ destruye la instancia a PtrSimple, eliminando automáticamente
       // la memoria ocupada por este.
    }
    
    // Para evitar fallos en wordpress:
    // 
    // &lt;/iostream&gt;</p></div>
    ";i:2;s:894:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    2
    3
    4
    </pre></td><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #666666;">// Utilizamos nuestra clase UnaClase</span>
    <span style="color: #0000ff;">void</span> metodo<span style="color: #008000;">&#40;</span> UnaClase<span style="color: #000040;">&amp;</span> unaClase <span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
       unaClase.<span style="color: #007788;">hacerAlgo</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">// Utilizamos nuestra clase UnaClase
    void metodo( UnaClase&amp; unaClase ) {
       unaClase.hacerAlgo();
    }</p></div>
    ";i:3;s:1219:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    2
    3
    4
    5
    6
    </pre></td><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #666666;">// Utilizamos nuestra clase UnaClase</span>
    <span style="color: #0000ff;">void</span> metodo<span style="color: #008000;">&#40;</span> PtrSimple<span style="color: #000080;">&lt;</span>unaclase<span style="color: #000080;">&gt;</span><span style="color: #000040;">&amp;</span> unaClase <span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
       unaClase<span style="color: #000040;">-</span><span style="color: #000080;">&gt;</span>hacerAlgo<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    <span style="color: #666666;">// Para evitar problemas</span>
    <span style="color: #666666;">// &lt;/unaclase&gt;</span></pre></td></tr></table><p class="theCode" style="display:none;">// Utilizamos nuestra clase UnaClase
    void metodo( PtrSimple&lt;unaclase&gt;&amp; unaClase ) {
       unaClase-&gt;hacerAlgo();
    }
    // Para evitar problemas
    // &lt;/unaclase&gt;</p></div>
    ";i:4;s:2274:"
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
    </pre></td><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #339900;">#include &lt;vector&gt;</span>
    <span style="color: #0000ff;">using</span> std<span style="color: #008080;">::</span><span style="color: #007788;">vector</span><span style="color: #008080;">;</span>
    <span style="color: #666666;">// Nuestras definiciones</span>
    &nbsp;
    <span style="color: #666666;">// El codigo</span>
    <span style="color: #0000ff;">typedef</span> PtrSimple<span style="color: #000080;">&lt;</span>unaclase<span style="color: #000080;">&gt;</span> PtrUnaClase<span style="color: #008080;">;</span>
    <span style="color: #666666;">// Ojo que el worpress cambia algunas cosas (como mayúsculas a minúsculas :@)</span>
    vector<span style="color: #000080;">&lt;</span>ptrunaclase<span style="color: #000080;">&gt;</span> vectorPunteros<span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #666666;">// Utilizamos nuestra clase UnaClase</span>
    <span style="color: #0000ff;">void</span> metodo<span style="color: #008000;">&#40;</span> PtrUnaClase<span style="color: #000040;">&amp;</span> unaClase <span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
       vectorPunteros.<span style="color: #007788;">add</span><span style="color: #008000;">&#40;</span>unaClase<span style="color: #008000;">&#41;</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span>
    &nbsp;
    <span style="color: #666666;">// Para evitar problemas</span>
    <span style="color: #666666;">// &lt;/ptrunaclase&gt;&lt;/unaclase&gt;&lt;/vector&gt;</span></pre></td></tr></table><p class="theCode" style="display:none;">#include &lt;vector&gt;
    using std::vector;
    // Nuestras definiciones
    
    // El codigo
    typedef PtrSimple&lt;unaclase&gt; PtrUnaClase;
    // Ojo que el worpress cambia algunas cosas (como mayúsculas a minúsculas :@)
    vector&lt;ptrunaclase&gt; vectorPunteros;
    
    // Utilizamos nuestra clase UnaClase
    void metodo( PtrUnaClase&amp; unaClase ) {
       vectorPunteros.add(unaClase);
    }
    
    // Para evitar problemas
    // &lt;/ptrunaclase&gt;&lt;/unaclase&gt;&lt;/vector&gt;</p></div>
    ";i:5;s:7681:"
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
    </pre></td><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #0000ff;">template</span><span style="color: #000080;">&lt;</span><span style="color: #0000ff;">typename</span> _t<span style="color: #000080;">&gt;</span> <span style="color: #0000ff;">class</span> PtrSimple2 <span style="color: #008000;">&#123;</span>
    <span style="color: #0000ff;">private</span><span style="color: #008080;">:</span>
       _t <span style="color: #000040;">*</span>_ptr<span style="color: #008080;">;</span>
       <span style="color: #0000ff;">int</span> <span style="color: #000040;">*</span>_count<span style="color: #008080;">;</span> <span style="color: #666666;">// Copias del puntero</span>
    &nbsp;
    <span style="color: #0000ff;">public</span><span style="color: #008080;">:</span>
       <span style="color: #666666;">// Creamos el puntero a partir de una zona de memoria ya existente</span>
       PtrSimple2<span style="color: #008000;">&#40;</span> _t<span style="color: #000040;">*</span> ptr <span style="color: #000080;">=</span> <span style="color: #0000ff;">NULL</span> <span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
          _ptr <span style="color: #000080;">=</span> ptr<span style="color: #008080;">;</span>
          <span style="color: #0000ff;">if</span><span style="color: #008000;">&#40;</span> _ptr <span style="color: #000080;">==</span> <span style="color: #0000ff;">NULL</span> <span style="color: #008000;">&#41;</span>
             _count <span style="color: #000080;">=</span> <span style="color: #0000ff;">NULL</span><span style="color: #008080;">;</span>
          <span style="color: #0000ff;">else</span> <span style="color: #008000;">&#123;</span>
             _count <span style="color: #000080;">=</span> <span style="color: #0000dd;">new</span> <span style="color: #0000ff;">int</span><span style="color: #008080;">;</span>
             <span style="color: #000040;">*</span>_count <span style="color: #000080;">=</span> <span style="color: #0000dd;">0</span><span style="color: #008080;">;</span>
          <span style="color: #008000;">&#125;</span>
       <span style="color: #008000;">&#125;</span>
    &nbsp;
       <span style="color: #666666;">// Constructor de copia: tomamos un puntero ya existente e incrementamos</span>
       <span style="color: #666666;">// el contador de usos.</span>
       PtrSimple2<span style="color: #008000;">&#40;</span> <span style="color: #0000ff;">const</span> PtrSimple2<span style="color: #000080;">&lt;</span>_t<span style="color: #000080;">&gt;</span><span style="color: #000040;">&amp;</span> ptr <span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
          _ptr <span style="color: #000080;">=</span> ptr._ptr<span style="color: #008080;">;</span>
          _count <span style="color: #000080;">=</span> ptr._count<span style="color: #008080;">;</span>
          <span style="color: #0000ff;">if</span><span style="color: #008000;">&#40;</span> _count <span style="color: #000040;">!</span><span style="color: #000080;">=</span> <span style="color: #0000ff;">NULL</span> <span style="color: #008000;">&#41;</span>
             <span style="color: #008000;">&#40;</span><span style="color: #000040;">*</span>count<span style="color: #008000;">&#41;</span> <span style="color: #000080;">=</span> <span style="color: #008000;">&#40;</span><span style="color: #000040;">*</span>count<span style="color: #008000;">&#41;</span> <span style="color: #000040;">+</span> <span style="color: #0000dd;">1</span><span style="color: #008080;">;</span>
       <span style="color: #008000;">&#125;</span>
    &nbsp;
       ~PtrSimple2<span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
          <span style="color: #0000ff;">if</span><span style="color: #008000;">&#40;</span> _count <span style="color: #000040;">!</span><span style="color: #000080;">=</span> <span style="color: #0000ff;">NULL</span> <span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
             <span style="color: #008000;">&#40;</span><span style="color: #000040;">*</span>count<span style="color: #008000;">&#41;</span> <span style="color: #000080;">=</span> <span style="color: #008000;">&#40;</span><span style="color: #000040;">*</span>count<span style="color: #008000;">&#41;</span> <span style="color: #000040;">-</span> <span style="color: #0000dd;">1</span><span style="color: #008080;">;</span>
             <span style="color: #666666;">// Si nadie apunta a esta zona de memoria,</span>
             <span style="color: #666666;">// se libera la memoria</span>
             <span style="color: #0000ff;">if</span><span style="color: #008000;">&#40;</span> <span style="color: #008000;">&#40;</span><span style="color: #000040;">*</span>count<span style="color: #008000;">&#41;</span> <span style="color: #000080;">==</span> <span style="color: #0000dd;">0</span> <span style="color: #008000;">&#41;</span>
                <span style="color: #0000dd;">delete</span> _ptr<span style="color: #008080;">;</span>
          <span style="color: #008000;">&#125;</span>
       <span style="color: #008000;">&#125;</span>
    &nbsp;
       _t<span style="color: #000040;">*</span> operator<span style="color: #000040;">-</span><span style="color: #000080;">&gt;</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #0000ff;">const</span> <span style="color: #008000;">&#123;</span>
          <span style="color: #0000ff;">return</span> _ptr<span style="color: #008080;">;</span>
       <span style="color: #008000;">&#125;</span>
    &nbsp;
       _t<span style="color: #000040;">&amp;</span> operator<span style="color: #000040;">*</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #0000ff;">const</span> <span style="color: #008000;">&#123;</span>
          <span style="color: #0000ff;">return</span> <span style="color: #000040;">*</span>_ptr<span style="color: #008080;">;</span>
       <span style="color: #008000;">&#125;</span>
    <span style="color: #008000;">&#125;</span><span style="color: #008080;">;</span>
    &nbsp;
    <span style="color: #666666;">// Para evitar fallos en wordpress</span>
    <span style="color: #666666;">// &lt;/_t&gt;&lt;/typename&gt;</span></pre></td></tr></table><p class="theCode" style="display:none;">template&lt;typename _t&gt; class PtrSimple2 {
    private:
       _t *_ptr;
       int *_count; // Copias del puntero
    
    public:
       // Creamos el puntero a partir de una zona de memoria ya existente
       PtrSimple2( _t* ptr = NULL ) {
          _ptr = ptr;
          if( _ptr == NULL )
             _count = NULL;
          else {
             _count = new int;
             *_count = 0;
          }
       }
    
       // Constructor de copia: tomamos un puntero ya existente e incrementamos
       // el contador de usos.
       PtrSimple2( const PtrSimple2&lt;_t&gt;&amp; ptr ) {
          _ptr = ptr._ptr;
          _count = ptr._count;
          if( _count != NULL )
             (*count) = (*count) + 1;
       }
    
       ~PtrSimple2() {
          if( _count != NULL ) {
             (*count) = (*count) - 1;
             // Si nadie apunta a esta zona de memoria,
             // se libera la memoria
             if( (*count) == 0 )
                delete _ptr;
          }
       }
    
       _t* operator-&gt;() const {
          return _ptr;
       }
    
       _t&amp; operator*() const {
          return *_ptr;
       }
    };
    
    // Para evitar fallos en wordpress
    // &lt;/_t&gt;&lt;/typename&gt;</p></div>
    ";}
categories:
  - Desarrollo

---
<a href="http://blog.laparca.es/index.php/2007/08/04/punteros-inteligentes-en-c-smart-pointers/" target="_blank">En el artículo anterior</a> veíamos como crear una clase simple de puntero inteligente, pero no se mostró ningún ejemplo de su uso. Por este motivo, a continuación pasamos a poner un ejemplo y a ver las deficiencias de dicha clase:

<pre lang="cpp" line="1">#include &lt;iostream>
using std::cout;
using std::endl;

// Aqui iría nuestra clase de puntero simple
// template...

// Clase de ejemplo para mostrar el uso de los punteros inteligentes
class UnaClase {
   UnaClase() {
      cout &lt; &lt; "Soy UnaClase y me estan creando" &lt;&lt; endl;
   }
   ~UnaClase() {
      cout &lt;&lt; "Soy UnaClase y me están destruyendo" &lt;&lt; endl;
   }
   void hacerAlgo() {
      cout &lt;&lt; "Soy UnaClase y estoy haciendo algo útil" &lt;&lt; endl;
   }
};

int main( void ) {
   PtrSimple&lt;UnaClase> ptrUnaClase = new UnaClase();

   // Llamamos al método hacerAlgo de UnaClase a través del puntero inteligente.
   ptrUnaClase->hacerAlgo();

   // En este punto, C++ destruye la instancia a PtrSimple, eliminando automáticamente
   // la memoria ocupada por este.
}

// Para evitar fallos en wordpress:
// 
// &lt;/iostream> 
</pre>

Si hacemos la prueba, veremos como el destructor de UnaClase se llama automáticamente al término del programa. Con esto hemos conseguido nuestro primer objetivo, no tener que liberar nosotros mismos la memoria, pero ahora surgen otros problemas: ¿cómo utilizar el puntero en más partes de la aplicación que no sean el propio método?

Antes de continuar vamos a ver una cosita de C++ que nos ayudará mucho: el paso de parametros por referencia. Esto nos permite pasar a un método una referencia a un objeto y si lo modificamos estaremos modificando el objeto original. ¿Cómo se hace esto? pues muy fácil:

<pre lang="cpp" line="1">// Utilizamos nuestra clase UnaClase
void metodo( UnaClase& unaClase ) {
   unaClase.hacerAlgo();
}
</pre>

Como vemos, al poner los argumentos del método, justo después del tipo se ha añadido un símbolo &. Éste es el que indica que es por referencia. Si no se pone nada sería por valor y si se pusiera un * sería una dirección. De este modo, ya podríamos pasar sin peligro a un método un puntero inteligente:

<pre lang="cpp" line="1">// Utilizamos nuestra clase UnaClase
void metodo( PtrSimple&lt;unaclase>& unaClase ) {
   unaClase->hacerAlgo();
}
// Para evitar problemas
// &lt;/unaclase>
</pre>

Ahora imaginemos el siguiente caso:

<pre lang="cpp" line="1">#include &lt;vector>
using std::vector;
// Nuestras definiciones

// El codigo
typedef PtrSimple&lt;unaclase> PtrUnaClase;
// Ojo que el worpress cambia algunas cosas (como mayúsculas a minúsculas :@)
vector&lt;ptrunaclase> vectorPunteros;

// Utilizamos nuestra clase UnaClase
void metodo( PtrUnaClase& unaClase ) {
   vectorPunteros.add(unaClase);
}

// Para evitar problemas
// &lt;/ptrunaclase>&lt;/unaclase>&lt;/vector>
</pre>

Estamos haciendo uso de STL para el vector. Este código no funcionará, ya que la clase vector hace uso del constructor de copia de PtrSimple, que no lo hemos definido, por lo que utilizaría el contructor de copia por defecto. Esto derivaría en que en un momento dado el puntero podría liberarse mientras en el vector seguiría existiendo un puntero al mismo, lo que supondrá un fallo de segmentación. Para solventar esto, hay que hacer uso de contadores de uso de punteros, que nos permitirán saber cuantas copias hay del mismo para liberarlo en caso necesario:

<pre lang="cpp" line="1">template&lt;typename _t> class PtrSimple2 {
private:
   _t *_ptr;
   int *_count; // Copias del puntero

public:
   // Creamos el puntero a partir de una zona de memoria ya existente
   PtrSimple2( _t* ptr = NULL ) {
      _ptr = ptr;
      if( _ptr == NULL )
         _count = NULL;
      else {
         _count = new int;
         *_count = 0;
      }
   }

   // Constructor de copia: tomamos un puntero ya existente e incrementamos
   // el contador de usos.
   PtrSimple2( const PtrSimple2&lt;_t>& ptr ) {
      _ptr = ptr._ptr;
      _count = ptr._count;
      if( _count != NULL )
         (*count) = (*count) + 1;
   }

   ~PtrSimple2() {
      if( _count != NULL ) {
         (*count) = (*count) - 1;
         // Si nadie apunta a esta zona de memoria,
         // se libera la memoria
         if( (*count) == 0 )
            delete _ptr;
      }
   }

   _t* operator->() const {
      return _ptr;
   }

   _t& operator*() const {
      return *_ptr;
   }
};

// Para evitar fallos en wordpress
// &lt;/_t>&lt;/typename>
</pre>

Con la clase anterior, ya no debería haber problemas con el tema de STL ni de que hayan copias por ahí&#8230; ¿o no? Siguen existiendo casos conflictivos, por ejemplo, tener que pasar sólo la dirección (no el puntero) y luego desde otra parte del código tomar dicho puntero a una clase. Con este caso, perderiamos los contadores de uso que teníamos, por lo que perdemos el control.

A parte de lo anterior, también es constatable que nos faltan funcionalidades: y si quiero comparar dos puntero, y si quiero asignarle una dirección nueva al puntero cuando este ya tenía otra, etc. Esta y otras dudas, para el siguiente artículo.