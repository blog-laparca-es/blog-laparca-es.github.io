---
title: Transformaciones AST para importar clases de IDL
author: laparca
type: post
date: 2010-05-31T09:28:34+00:00
url: /2010/05/31/transformaciones-ast-para-importar-clases-de-idl/
jd_tweet_this:
  - yes
wp_jd_clig:
  - http://cli.gs/hzRVJ
wp_jd_target:
  - http://cli.gs/hzRVJ
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:1478:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    2
    3
    4
    5
    </pre></td><td class="code"><pre class="groovy" style="font-family:monospace;">@IDLClass<span style="color: #66cc66;">&#40;</span>idlclass<span style="color: #66cc66;">=</span><span style="color: #ff0000;">&quot;CLASE_DE_IDL&quot;</span><span style="color: #66cc66;">&#41;</span>
    <span style="color: #000000; font-weight: bold;">class</span> MiClaseEnJava <span style="color: #000000; font-weight: bold;">extends</span> JIDLObject <span style="color: #66cc66;">&#123;</span>
       @IDLFunction<span style="color: #66cc66;">&#40;</span>name<span style="color: #66cc66;">=</span><span style="color: #ff0000;">&quot;FUNCION_IDL&quot;</span><span style="color: #66cc66;">&#41;</span>
       <span style="color: #993333;">float</span> miFuncion<span style="color: #66cc66;">&#40;</span><span style="color: #993333;">float</span> a, <span style="color: #993333;">float</span> b, <span style="color: #aaaadd; font-weight: bold;">String</span> cadena<span style="color: #66cc66;">&#41;</span> <span style="color: #66cc66;">&#123;</span><span style="color: #66cc66;">&#125;</span>
    <span style="color: #66cc66;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">@IDLClass(idlclass=&quot;CLASE_DE_IDL&quot;)
    class MiClaseEnJava extends JIDLObject {
       @IDLFunction(name=&quot;FUNCION_IDL&quot;)
       float miFuncion(float a, float b, String cadena) {}
    }</p></div>
    ";}
categories:
  - Desarrollo
  - Personal
tags:
  - ast
  - groovy
  - programacion

---
En la anterior entraba hablaba un poco sobre las transformaciones AST de Groovy y que me maravillaban (y si esto último no lo dije, lo digo ahora). Como me gustan y las veo útiles decidí ponerlas en práctica para un uso real.

En donde trabajo se utiliza un lenguaje de programación llamado IDL. Este lenguaje se utilizan en muchos entornos de investigación y para ser sinceros se haría un favor al mundo amputándole las manos a la persona o personas que lo diseñó/aron (pero dejemos esto para un posible futuro artículo). En IDL se pueden crear funciones y procedimientos o se puede crear clases con métodos y atributos. Cuando se necesita ofrecer a otro lenguaje de las funcionalidades que hemos creado en IDL se hace uso siempre de clases y objetos. Además provee de una herramientas denominada Export Bridge Assistant (EBA) para facilitar la tarea de generar los _bindings_ del lenguaje destino. Debo decir que me EBA hace cierto trabajo por el programador, concretamente genera una clase en java o .Net con los métodos seleccionados, pero en el caso de Java no hace distinción de los tipos de datos. Para él solo existe el JIDLNumber, pero está prohibido por el programador su uso, sino que debes utilizar JIDLFloat, JIDLLong, etc. Además, estos tipos de datos no son nativos de Java lo que supone un sobreesfuerzo para el programador.

En esta situación se me ocurrió crear una transformación AST que generase el código de los métodos usando datos nativos de Java. En lugar de llamar a EBA para generar el _binding_ se crea una clase de esta forma:

<pre lang="Groovy" line="1">@IDLClass(idlclass="CLASE_DE_IDL")
class MiClaseEnJava extends JIDLObject {
   @IDLFunction(name="FUNCION_IDL")
   float miFuncion(float a, float b, String cadena) {}
}
</pre>

Durante la compilación de la clase se detecta la nota IDLClass y se pasa el control a la transformación AST que añade un constructor por defecto necesario para los objetos que heredan de JIDLObject. Además se busca de nota IDLFunction y cuando se encuentra se interpretan los parámetros para generar el código con las transformaciones de tipos necesarias.

Sinceramente creo que esto es más óptimo que hacer uso de EBA, ya que de todos modos me termino creando métodos que realizan la transformación de tipos y de este modo me ahorro dicho trabajo.

Lo que más me ha costado es entender como funciona la generación de código ya que se basa en la estructura del compilador. Concretamente me ha constado 1 semana hacer la transformación.

En cuanto pueda publicaré el código para que lo pueda utilizar quien quiera, que seguro que mal no hará.