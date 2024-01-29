---
title: 'Curso de plantillas en C++: uso en funciones'
author: laparca
type: post
date: 2020-01-13T15:26:25+00:00
url: /2020/01/13/curso-de-plantillas-en-c-uso-en-funciones/
categories:
  - Personal

---
Antes de continuar con las funciones quedó pendiente la sintaxis de las plantillas:

<pre class="wp-block-code"><code>template &lt; LISTA_DE_LA_PANTILLA > SOBRE_LO_QUE_APLICA_LA_PANTILLA</code></pre>

Bueno, creo que está claro: se usa la palabra reservada `<strong>template</strong>` y entre _brakets_ (los simbolitos &#8216;`<`&#8216; y &#8216;`>`&#8216;) se pone la lista de cosas que queremos que se puedan hacer plantilla. Finalmente va la parte sobre la que vamos a aplicar la plantilla, que puede ser una estructura o unión, una clase, una función, un renombrado de tipo con **`using`** (a partir del estándar de 2011) o una declaración de variable (a partir del estándar de 2014).

Y con esto se termina esta breve explicación. El resto lo iremos viendo con ejemplos.

## Ahora sí: Funciones {.wp-block-heading}

En el momento en el que podemos tener tipos como plantillas surge el problema de poder usarlos en funciones. En este punto la lógica es sencilla, si tengo que pasar a una función un tipo que es una plantilla, la función también debe ser una plantilla.

<pre class="wp-block-code"><code>template&lt;class T> struct mi_tipo {
   /* Da igual lo que vaya aquí para el ejemplo */
};

template&lt;class T>
void una_funcion(mi_tipo&lt;T> valor) {
   /* Esta funcion aceptará cualquier mi_tipo */
}</code></pre>

De este modo, desde una_funcion tendríamos acceso a todas las funciones miembro y variables miembro de `mi_tipo`. A partir de aquí lo usaríamos de forma normal como cualquier otra variable.

Hay otra forma de crear la plantilla para que acepte cualquier cosa:

<pre class="wp-block-code"><code>template&lt;class T>
void otra_funcion(T valor) {
   /* Esta funcion aceptara cualquier tipo, incluido mi_tipo */
}</code></pre>

Con este código, `otra_funcion` acepta cualquier tipo de dato. Si intentamos acceder a alguna variable miembro o función miembro de valor el compilador dará error si no está implementada en el tipo `T`.

## Un ejemplo práctico {.wp-block-heading}

Hasta ahora hemos visto un poco por encima cómo hacer plantillas sencillas, pero toca ver algo que tenga alguna utilidad. Por eso vamos hacer una clase que implemente un array que pueda devolver su tamaño con una función (como en java). 

Actualmente ya existe una clase que hace eso en el estándar. Es [std::array][1].

<pre class="wp-block-code"><code>/* Este codigo es compatible C++03 */
#include &lt;iostream>
#include &lt;stdexcept>

template&lt;class Tipo, int Tam> class array {
   public:
      Tipo& operator&#91;](int p) {
         if (p >= Tam) throw std::out_of_range(std::string("Te saliste del rango"));
         return valores_&#91;p];
      }
      int tam() const {
         return Tam;
      }
   private:
      Tipo valores_&#91;Tam];
};

int main() {
   array&lt;int, 5> valores;
   for (int i = 0; i &lt; valores.tam(); i++)
      valores&#91;i] = i*2;

   for (int i = 0; i &lt; valores.tam(); i++)
      std::cout &lt;&lt; valores&#91;i] &lt;&lt; std::endl;

   return 0;
}</code></pre>

En las siguientes entregas profundizaremos más en lo que se puede hacer con las plantillas.

 [1]: https://en.cppreference.com/w/cpp/container/array