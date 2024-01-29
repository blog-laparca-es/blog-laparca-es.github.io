---
title: Haciendo memoria
author: laparca
type: post
date: 2010-04-16T14:33:32+00:00
url: /2010/04/16/haciendo-memoria/
jd_tweet_this:
  - yes
wp_jd_clig:
  - http://cli.gs/NQXVH
wp_jd_target:
  - http://cli.gs/NQXVH
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:551:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    2
    3
    </pre></td><td class="code"><pre class="groovy" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">class</span> ClaseDeEjemplo <span style="color: #66cc66;">&#123;</span>
        @Bindable <span style="color: #aaaadd; font-weight: bold;">String</span> prop
    <span style="color: #66cc66;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">class ClaseDeEjemplo {
        @Bindable String prop
    }</p></div>
    ";i:2;s:3999:"
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
    </pre></td><td class="code"><pre class="groovy" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">class</span> ClaseDeEjemplo <span style="color: #66cc66;">&#123;</span>
        <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #aaaadd; font-weight: bold;">String</span> prop
        <span style="color: #aaaadd; font-weight: bold;">PropertyChangeSupport</span> pcs <span style="color: #66cc66;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #aaaadd; font-weight: bold;">PropertyChangeSupport</span><span style="color: #66cc66;">&#40;</span><span style="color: #000000; font-weight: bold;">this</span><span style="color: #66cc66;">&#41;</span><span style="color: #66cc66;">;</span>
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #993333;">void</span> addPropertyChangeListener<span style="color: #66cc66;">&#40;</span><span style="color: #aaaadd; font-weight: bold;">PropertyChangeListener</span> l<span style="color: #66cc66;">&#41;</span> <span style="color: #66cc66;">&#123;</span>
            pcs.<span style="color: #006600;">add</span><span style="color: #66cc66;">&#40;</span>l<span style="color: #66cc66;">&#41;</span><span style="color: #66cc66;">;</span>
        <span style="color: #66cc66;">&#125;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #993333;">void</span> removePropertyChangeListener<span style="color: #66cc66;">&#40;</span><span style="color: #aaaadd; font-weight: bold;">PropertyChangeListener</span> l<span style="color: #66cc66;">&#41;</span> <span style="color: #66cc66;">&#123;</span>
            pcs.<span style="color: #006600;">remove</span><span style="color: #66cc66;">&#40;</span>l<span style="color: #66cc66;">&#41;</span><span style="color: #66cc66;">;</span>
        <span style="color: #66cc66;">&#125;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #aaaadd; font-weight: bold;">String</span> getProp<span style="color: #66cc66;">&#40;</span><span style="color: #66cc66;">&#41;</span> <span style="color: #66cc66;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">return</span> prop<span style="color: #66cc66;">;</span>
        <span style="color: #66cc66;">&#125;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #993333;">void</span> setProp<span style="color: #66cc66;">&#40;</span><span style="color: #aaaadd; font-weight: bold;">String</span> prop<span style="color: #66cc66;">&#41;</span> <span style="color: #66cc66;">&#123;</span>
            pcs.<span style="color: #006600;">firePropertyChanged</span><span style="color: #66cc66;">&#40;</span><span style="color: #ff0000;">&quot;prop&quot;</span>, <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006600;">prop</span>, <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006600;">prop</span> <span style="color: #66cc66;">=</span> prop<span style="color: #66cc66;">&#41;</span><span style="color: #66cc66;">;</span>
        <span style="color: #66cc66;">&#125;</span>
    <span style="color: #66cc66;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">class ClaseDeEjemplo {
        private String prop
        PropertyChangeSupport pcs = new PropertyChangeSupport(this);
        public void addPropertyChangeListener(PropertyChangeListener l) {
            pcs.add(l);
        }
    
        public void removePropertyChangeListener(PropertyChangeListener l) {
            pcs.remove(l);
        }
    
        public String getProp() {
            return prop;
        }
    
        public void setProp(String prop) {
            pcs.firePropertyChanged(&quot;prop&quot;, this.prop, this.prop = prop);
        }
    }</p></div>
    ";}
categories:
  - Desarrollo
  - Opinión
  - Personal
tags:
  - abuelo cebolleta
  - ast
  - Desarrollo
  - groovy
  - opinion
  - programacion

---
Esta semana he recordado uno de mis viejos proyectos de cuando era más joven (sería el año 97). En aquel momento tenía en mente la creación de un lenguaje que pudiese ser modificado en tiempo de compilación. Con esto me refiero a que pudiesen crearse reglas que permitieran modificar el cómo este compilaba o añadiese nuevas posibilidades al lenguaje.

En aquel momento yo no tenía conocimiento alguno de lenguajes, gramáticas o compiladores y el único curso que vi fue el de la revista Solo Programadores de varios años atrás y, la verdad, no me resolvió ninguna duda (esto se debe a que entonces no solía leer tanto y miraba solo por encima las cosas).

El caso es que me he encontrado que ya lo han inventado. En <a title="Lenguaje de programación Groovy" href="http://groovy.codehaus.org/" target="_blank">Groovy</a> existe una característica denominada <a href="http://groovy.codehaus.org/Compile-time+Metaprogramming+-+AST+Transformations" target="_blank">transformaciones AST</a> que permite modificar las reglas de compilación.  Debo reconocer que es una característica tan chula como difícil de utilizar (todo hay que decirlo).

En estos momentos me encuentro estudiando la documentación para ponerme a hacer pruebas y comprobar qué tal funciona. La verdad es que permite hacer cosas tan increíbles como <a href="http://code.google.com/p/groovypptest/" target="_blank">Groovy++</a>, que es un optimizador de Groovy (lo que hace es eliminar algunas características de Groovy para acelerar la ejecución de las aplicaciones).

He podido encontrar una gran cantidad de ejemplo y la verdad es que me sorprenden mucho. Por ejemplo se pueden automatizar patrones de diseño con este sistema tal y como se hace con la transformación _Bindable_. Ésta convierte un atributo de clase en un sistema que permite monitorizar los cambios del mismo (patron ). De este modo si tenemos algo como:

<pre lang="Groovy" line="1">class ClaseDeEjemplo {
    @Bindable String prop
}
</pre>

Se transformará de forma automática en:

<pre lang="Groovy" line="1">class ClaseDeEjemplo {
    private String prop
    PropertyChangeSupport pcs = new PropertyChangeSupport(this);
    public void addPropertyChangeListener(PropertyChangeListener l) {
        pcs.add(l);
    }

    public void removePropertyChangeListener(PropertyChangeListener l) {
        pcs.remove(l);
    }

    public String getProp() {
        return prop;
    }

    public void setProp(String prop) {
        pcs.firePropertyChanged("prop", this.prop, this.prop = prop);
    }
}</pre>

Con lo que evitamos tener que escribir un gran número de líneas de código. Sinceramente me parece un gran avance.