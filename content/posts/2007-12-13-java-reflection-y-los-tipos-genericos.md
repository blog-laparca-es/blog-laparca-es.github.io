---
title: Java reflection y los tipos genéricos
author: laparca
type: post
date: 2007-12-13T14:06:05+00:00
url: /2007/12/13/java-reflection-y-los-tipos-genericos/
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:2037:"
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
    </pre></td><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> Lista<span style="color: #339933;">&lt;</span>tipo<span style="color: #339933;">&gt;</span> <span style="color: #009900;">&#123;</span>
       <span style="color: #666666; font-style: italic;">/* para evitar problemas con wordpress: &lt;/tipo&gt; */</span>
       tipo leeElementoEnPosicion<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> posicion<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          tipo rtn <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #339933;">;</span>
          <span style="color: #666666; font-style: italic;">/* Buscamos el elemento y lo devolvemos */</span>
          <span style="color: #000000; font-weight: bold;">return</span> rtn<span style="color: #339933;">;</span>
       <span style="color: #009900;">&#125;</span>
    &nbsp;
       <span style="color: #000066; font-weight: bold;">void</span> agregarElemento<span style="color: #009900;">&#40;</span>TipoElemento elm<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #666666; font-style: italic;">/* Insertamos el elemento */</span>
       <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">public class Lista&lt;tipo&gt; {
       /* para evitar problemas con wordpress: &lt;/tipo&gt; */
       tipo leeElementoEnPosicion(int posicion) {
          tipo rtn = null;
          /* Buscamos el elemento y lo devolvemos */
          return rtn;
       }
    
       void agregarElemento(TipoElemento elm) {
          /* Insertamos el elemento */
       }
    }</p></div>
    ";i:2;s:757:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">Class</span> leerTipoElementoLista<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
       <span style="color: #000000; font-weight: bold;">return</span> tipo.<span style="color: #000000; font-weight: bold;">class</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">public Class leerTipoElementoLista() {
       return tipo.class;
    }</p></div>
    ";i:3;s:1166:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">Class</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#40;</span><span style="color: #009900;">&#40;</span>ParameterizedType<span style="color: #009900;">&#41;</span> getClass<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getGenericSuperclass</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getActualTypeArguments</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#91;</span><span style="color: #cc66cc;">0</span><span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">(Class) ((ParameterizedType) getClass().getGenericSuperclass()).getActualTypeArguments()[0];</p></div>
    ";}
categories:
  - Desarrollo
  - Opinión

---
Por temas del trabajo llevo unos días pegandome con java reflection y los tipos de genéricos. Debo reconocer que las dos cosas están muy bien, pero entre ellas no se llevan bien. Para facilitar un poco la cosa voy a poner un ejemplo de un tipo genérico:

<pre lang="java" line="1">public class Lista&lt;tipo> {
   /* para evitar problemas con wordpress: &lt;/tipo> */
   tipo leeElementoEnPosicion(int posicion) {
      tipo rtn = null;
      /* Buscamos el elemento y lo devolvemos */
      return rtn;
   }

   void agregarElemento(TipoElemento elm) {
      /* Insertamos el elemento */
   }
}
</pre>

El código anterior no hace nada, pero nos permite ver que creamos una clase Lista que es genérica. El hecho de que sea genérica significa que podemos decir que la lista podrá almacenar cualquier tipo de dato y que se lo indicaremo al crearla (antiguamente en java sólo se podía almacenar un tipo de dato: Object).

Mi problema empieza cuando yo necesito desde una instancia de la clase Lista cuál es el tipo de dato que almacena. Inicialmente sería tan sencillo como hace lo siguiente:

<pre lang="java">public Class leerTipoElementoLista() {
   return tipo.class;
}
</pre>

El problema es que, según parece, en la práctica java no utiliza genéricos, sino que sólo los comprueba en tiempo de compilación. Esto significa que una vez compilado el programa, _tipo_ deja de ser un tipo conocido y pasa a ser algo completamente indeterminado, o dicho de otro modo, se convierte en un Object. A causa de esto, la sentencia anterior (tipo.class) genera un error de compilación.

Buscando por el gran Google encontré una referencia a <a rel="nofollow" href="http://www.hibernate.org/" target="_blank">Hibernate</a> donde <a rel="nofollow" href="http://www.hibernate.org/328.html" target="_blank">comentaban un modo de hacerlo</a>:

<pre lang="java">(Class) ((ParameterizedType) getClass().getGenericSuperclass()).getActualTypeArguments()[0];
</pre>

Lo he estado probando y lo único que puedo decir es que falla en la ejecución. La sentencia anterior genera una _CastException_, así que nada.

Y yo necesito poder saber el tipo del genérico :'(