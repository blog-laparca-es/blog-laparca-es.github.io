---
title: Java reflection y los tipos genéricos (y II)
author: laparca
type: post
date: 2007-12-15T11:48:15+00:00
url: /2007/12/15/java-reflection-y-los-tipos-genericos-y-ii/
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:1856:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="cpp" style="font-family:monospace;"><span style="color: #ff0000; font-style: italic;">/**
    * Clase abstracta que define los dos métodos necesarios para poder
    * seriar cualquier clase por un canal de almacenamiento o de
    * comunicaciones.
    */</span>
    <span style="color: #0000ff;">class</span> Serializable <span style="color: #008000;">&#123;</span>
       <span style="color: #ff0000; font-style: italic;">/**
       * Seria el objeto a través de flujo os.
       */</span>
       <span style="color: #0000ff;">void</span> writeObject<span style="color: #008000;">&#40;</span>OutputStream <span style="color: #000040;">&amp;</span>os<span style="color: #008000;">&#41;</span> <span style="color: #000080;">=</span> <span style="color: #0000dd;">0</span><span style="color: #008080;">;</span>
       <span style="color: #ff0000; font-style: italic;">/**
       * Lee los datos del objeto desde el flujo is.
       */</span>
       <span style="color: #0000ff;">void</span> readObject<span style="color: #008000;">&#40;</span>InputStream <span style="color: #000040;">&amp;</span>is<span style="color: #008000;">&#41;</span> <span style="color: #000080;">=</span> <span style="color: #0000dd;">0</span><span style="color: #008080;">;</span>
    <span style="color: #008000;">&#125;</span><span style="color: #008080;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">/**
    * Clase abstracta que define los dos métodos necesarios para poder
    * seriar cualquier clase por un canal de almacenamiento o de
    * comunicaciones.
    */
    class Serializable {
       /**
       * Seria el objeto a través de flujo os.
       */
       void writeObject(OutputStream &amp;os) = 0;
       /**
       * Lee los datos del objeto desde el flujo is.
       */
       void readObject(InputStream &amp;is) = 0;
    };</p></div>
    ";i:2;s:2232:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">abstract</span> <span style="color: #000000; font-weight: bold;">class</span> VectorSeriable <span style="color: #009900;">&#123;</span>
       <span style="color: #000066; font-weight: bold;">void</span> readObject<span style="color: #009900;">&#40;</span><span style="color: #003399;">InputStream</span> is<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
       <span style="color: #666666; font-style: italic;">/* Leo utilizando el tipo del generíco como se dijo en la anterior entrada */</span>
       <span style="color: #009900;">&#125;</span>
       <span style="color: #000066; font-weight: bold;">void</span> writeObject<span style="color: #009900;">&#40;</span><span style="color: #003399;">OutputStream</span> os<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
       <span style="color: #666666; font-style: italic;">/* Grabo los objetos */</span>
       <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #008000; font-style: italic; font-weight: bold;">/**
    * Al heredar de este modo, estamos creando una clase VectorSimulaciones
    * que es idéntica a VectorSerializable, pero que ya conoce cual es el tipo
    * de su genérico.
    */</span>
    <span style="color: #000000; font-weight: bold;">class</span> VectorSimulaciones <span style="color: #000000; font-weight: bold;">extends</span> VectorSeriable <span style="color: #009900;">&#123;</span><span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">abstract class VectorSeriable {
       void readObject(InputStream is) {
       /* Leo utilizando el tipo del generíco como se dijo en la anterior entrada */
       }
       void writeObject(OutputStream os) {
       /* Grabo los objetos */
       }
    }
    
    /**
    * Al heredar de este modo, estamos creando una clase VectorSimulaciones
    * que es idéntica a VectorSerializable, pero que ya conoce cual es el tipo
    * de su genérico.
    */
    class VectorSimulaciones extends VectorSeriable {}</p></div>
    ";}
categories:
  - Desarrollo

---
Después de mucho pegarme con esto conseguí que me funcionase. Debo decir que no me gusta nada el hecho de no poder saber el tipo con el que se ha creado un genérico.

Para que se comprenda qué es lo que he hecho y para qué lo necesitba tengo que decir que en la beca tengo una aplicación realizada en C++ que tiene impletentado su propio tipo de seriado (La palabra en español para _serializar_ es <a rel="nofollow" href="http://buscon.rae.es/draeI/SrvltConsulta?TIPO_BUS=3&LEMA=seriar" target="_blank">seriado</a>. Como en C++ no hay mecanismos de introspección (como java reflection, system.reflection, etc.), el modo de hacerlo es un poco más feo.

## Seriado en C++

El mecanismo de seriado que he utilizado en C++ ha consistido en crear una clase abstracta con dos métodos abstractos, uno se seria los datos a un canal (puede ser un fichero, la red, MPI, etc.) y otro que realiza la operación inversa:

<pre lang="cpp">/**
* Clase abstracta que define los dos métodos necesarios para poder
* seriar cualquier clase por un canal de almacenamiento o de
* comunicaciones.
*/
class Serializable {
   /**
   * Seria el objeto a través de flujo os.
   */
   void writeObject(OutputStream &os) = 0;
   /**
   * Lee los datos del objeto desde el flujo is.
   */
   void readObject(InputStream &is) = 0;
};
</pre>

Es importante hacer notar que cualquier mecanismo de seriado exige que la clase seriable tenga un constructor vacío, para permitir regenerar todos los datos a partir del mecanismo de seriado.

El problema del mecanismo anterior es que el programador debe saber qué es lo que se va a transmitir y, por tanto, sabe qué tipo de dato le va a llegar. Esto no sucede con el sistema de seriado de java, que transmite el tipo de dato a través del canal.

Cuando quise ponerme a realizar esto mismo en java pensé que si ya tenía un mecanismo que me decía qué era lo que tenía que leer, no sería necesario implementar _readObject_ y _writeObject_ en cada clase, ya que puedo consultar cuales son los atributos de la clase. Pero el problema sobrevino cuando llegaron los genéricos.

## Los genéricos en Java

Los genéricos en Java funcionan igual que las plantillas de C++, pero con una salvedad. En C++ las plantillas se transforman en una implementación distinta para cada tipo con el que se generase la plantilla, en Java sólo existe una implementación con el tipo más simple de la plantilla (si no se especifica nada, es Object).

Lo anterior significa que si yo tengo un vector de simulaciones, en C++ se creará una implemtanción específica de vector que sólo trabaja con simulaciones (y ningún otro tipo). En Java no sucede lo mismo. En Java sólo hay una implementación que será de tipo Object (todos heredan de Object) pero el control de que sea una simulación se realiza en tiempo de compilación. Esto supone que cuando se ejecute la aplicación ya no conoce si es correcto el dato que se le está pasando, ha sido el compilador el que hico la comprobación. Esto supone que no puedo regenerar de la forma deseada el vector.

## Solución actual

En estos momentos he conseguido que funcione. Lo primero que hice fue ponerlo todo igual que lo tenía en C++, pero en Java. De este modo, todas las clases seriables deberán tener un readObject y un writeObject. Y para solucionar el tema de los genéricos hice lo siguiente:

Cree el tipo vector genérico que es seriable por este mecanismo. Para garantizar que funcionará he formazado a la clase a ser abstracta. Con lo que comenté en la anterior entrada sobre cómo obtener el tipo genérico, que dije que no funcionaba, pues sí funciona, pero no como yo esperaba. Para que funcione hay que heredar de la clase genérica de este modo:

<pre lang="java">abstract class VectorSeriable {
   void readObject(InputStream is) {
   /* Leo utilizando el tipo del generíco como se dijo en la anterior entrada */
   }
   void writeObject(OutputStream os) {
   /* Grabo los objetos */
   }
}

/**
* Al heredar de este modo, estamos creando una clase VectorSimulaciones
* que es idéntica a VectorSerializable, pero que ya conoce cual es el tipo
* de su genérico.
*/
class VectorSimulaciones extends VectorSeriable {}
</pre>

Como se puede apreciar, esto es igual que utilizat _typedef_ en C++. De este modo he conseguido que funcione. Ahora debería ser posible eliminar los metodos readObject y writeObject para automatizar todo ya que es bastante feo tenerlos en cada clase.