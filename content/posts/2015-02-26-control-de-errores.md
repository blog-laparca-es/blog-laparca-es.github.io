---
title: Control de errores
author: laparca
type: post
date: 2015-02-26T10:11:45+00:00
url: /2015/02/26/control-de-errores/
categories:
  - Desarrollo
tags:
  - control
  - control errores
  - Desarrollo
  - develop
  - error
  - error control
  - errores
  - programacion

---
Uno de los grandes problemas al programar es realizar el control de los errores. Por diversos motivos me ha tocado hacer un trabajo de estudio sobre qué opciones tenemos para realizar el control de los errores de una aplicación.

La verdad es que hubiese estado muy bien hacer una tormenta de ideas al respecto, pero en estos momentos estamos todos demasiado atareados.

El siguiente texto, sin pretender ser una guía exhaustiva de lo que es el control de errores, sí busca poner un punto de partida para todo aquel que quiera ver qué mecanismos hay para este fin.

<!--more-->

## Control de errores desde el lenguaje

Cuando empezamos a controlar errores lo único que tenemos son las propias herramientas del lenguaje. En lenguajes con C o Pascal tenemos _if_. Sí, esta sentencia de programación sirve para controlar errores. El _if_ es una herramienta muy potente ya que puede ser utilizada con el retorno de las funciones, con variables o con expresiones. En el estándar POSIX es habitual que las funciones devuelvan valores negativos (normalmente un -1) en caso de error.

En algunos casos, en lugar de _if_ se puede utilizar _switch/case/match_ (depende del lenguaje). Es igual que concatenar sentencias _if-else_ y permite hacer un tratamiento de error concreto a partir del retorno de la función:

Muchos lenguajes orientados a objetos incorporan esquemas _try-catch_ (o parecidos). Es parecido al _if_, pero permite separar el tratamiento de errores del código normal.

No tengo ninguna duda de que habrá lenguajes que dispongan de más tipos de tratamiento de error, pero también esto seguro que lo anterior abarca el 99% de lo que los lenguajes ofrecen para ese fin.

Por otra parte, algunos fabricantes pueden ofrecer extensiones al lenguaje. Por ejemplo, la versión de C de Microsoft soporta _try-catch_ (aunque de forma algo fea).

Algunos lenguajes se aprovechan de la flexibilidad que ofrecen sus tipos para realizar un control de errores consistente. En concreto <a title="Lenguaje Haskell" href="https://www.haskell.org/" target="_blank">haskell</a> ofrece un tratamiento de errores usando <a title="mónada" href="http://www.lcc.uma.es/~blas/pfHaskell/gentle/monads.html" target="_blank">mónadas</a> como <a title="Uso de mónada Either" href="https://www.fpcomplete.com/school/starting-with-haskell/basics-of-haskell/10_Error_Handling" target="_blank">Either</a>. Este control de errores ha sido posteriormente utilizado en otros lenguajes como <a title="Lenguaje de programación Rust" href="http://rust-lang.org/" target="_blank">Rust</a>. Incluso Java 8 ofrece un tipo <a title="Optional en Java" href="http://docs.oracle.com/javase/8/docs/api/java/util/Optional.html" target="_blank">Optional<T></a> que permite trabajar de forma parecida. En el caso de Rust, que es el que conozco algo más, se hace uso de _Option_, _Result_ y algunos tipos más concretos dependiendo del caso (se puede ver más en le <a title="Manual de Rust" href="http://doc.rust-lang.org/book/" target="_blank">manual</a> en el <a title="Manejo de errores en Rust" href="http://doc.rust-lang.org/book/error-handling.html" target="_blank">capítulo de manejo de errores</a>). Podemos ver como se van concatenando las acciones ante un resultado:

En la documentación de la API de Rust se puede ver <a title="Operaciones que pueden ser usadas con Option" href="http://doc.rust-lang.org/std/option/enum.Option.html" target="_blank">todas las operaciones que acepta Option</a>.

## Control de errores desde el sistema operativo

Un mecanismo habitual en entornos Unix/Linux para indicar a una aplicación que algo ha pasado son las señales. La señal es un sistema que permite interrumpir el funcionamiento habitual de la aplicación a causa de alguna circunstancia. Estas pueden ser debidas a eventos normales (se ha muerto un proceso hijo, se ha pulsado CTRL+C, etc.) o a errores (se ha producido un fallo de acceso a memoria, se ha tratado de ejecutar una instrucción errónea, etc.):

<a title="Manejo de señales en MS Windows" href="https://msdn.microsoft.com/en-us/library/xdkz3x12.aspx" target="_blank">Las señales están parcialmente soportadas por los sistemas operativos MS Windows</a>.

En el caso de los sistemas operativos MS Windows, se hace uso de <a title="Excepciones en MS Windows" href="https://msdn.microsoft.com/en-us/library/windows/desktop/ms680657%28v=vs.85%29.aspx" target="_blank">excepciones</a> (y por eso las extensiones de C para soportarlas en MS C):

## Control de errores desde API estándar

En la API POSIX de C existe unas funciones que permite realizar recuperación de errores. Estas funciones son <a title="setjmp" href="http://es.wikipedia.org/wiki/Setjmp.h" target="_blank"><em>setjmp</em> y <em>longjmp</em></a>.

_setjmp_ permite guardar el estado de la aplicación en un punto (registros y pila) para que en caso de error volver a ese punto. _longjmp_ permite volver al estado salvado por _setjmp_ pasando un valor informativo.

Estas funciones nos pueden permitir simular en C las excepciones de C++. En cualquier caso, estas funciones son complicadas de comprender y pueden ocasionar que se produzcan errores lógicos por dicho motivo.

Siento no poner ejemplos en otros lenguajes, pero C y C++ son los que en estos momentos domino más.

## Tipos de errores

Existen distintos tipos de errores. No desde el punto de vista de si es error de disco, error de operación, etc. Sino desde el punto de vista de cómo estos pueden afectar a nuestra aplicación.

En este punto podemos identificar varios casos claros:

### Errores que podemos ignorar porque no tienen efecto sobre el funcionamiento de la aplicación.

Este es el caso más sencillo de todos. Se produce un error, pero lo ignoramos.

Aunque rara vez deben ser ignorados los errores, es curioso cómo se abusa de esto en Java (especialmente durante la época de estudiante).

Podríamos poner aquí, como ejemplo, un sistema que envía datos a un notificador. Si la tasa de datos a enviar es muy alta, pero el valor del dato caduca en un tiempo muy breve, cabe la posibilidad de que si un dato da error al ser enviado no sea necesario tratarlo porque enseguida surgirá un nuevo dato que haga que este caduque.

### Errores que deberemos tratar para que no falle posteriormente la aplicación.

Lo más habitual cuando se produce un error es que este pueda afectar al funcionamiento posterior de la aplicación. Por ejemplo, si tratamos de abrir un fichero para guardar información y se produce un error es lógico pensar que la siguiente operación, la de escritura, también fallará. Por tanto, es necesario controlar el error de la apertura y actuar en consecuencia.

Lo más habitual en este tipo de errores es que se muestre al usuario un mensaje indicando la causa del error, pero no se haga anda más. Esto puede suceder al tratar de guardar un fichero de solo lectura o si no tenemos permisos para guardarlo en el lugar que le indicamos.

### Errores que tras tratarlos deberemos realizar uno o más reintentos.

Este es un subcaso del anterior. Esta vez, en lugar de devolver el error lo que hacemos es reintentar la operación hasta que funcione o hasta que se pase de un umbral de reintentos.

Por ejemplo, cuando se imprime en una impresora de _tickets_ (como las de los cajeros automáticos) estas a veces pueden tardar un poco entre operaciones. Si ante los intentos la impresora no devuelve error, sino un ocupada, podemos reintentar la operación hasta que esta finalmente sí sea posible o se produzca un error real.

Otro ejemplo normal es el que se da cuando se hace uso de las funciones POSIX. Muchas de estas funciones devuelven error en caso de que se produzca una señal durante su ejecución. Este caso se puede comprobar si la variable global _errno_ tiene el valor _EINTR_. Igualmente, si en _errno_ se encuentra el valor _EAGAIN_ se puede volver a intentar la operación.

### Errores que impedirán a al aplicación continuar.

Aunque podemos tratar de controlar y recuperarnos de todos los errores, siempre habrá errores que tras los cuales no podremos hacer nada. Uno muy habitual es cuando se produce una señal _SIGSEGV_. Esto significa que hemos accedido a una zona inválida de memoria. Lo normal es que cuando sucede esto sea el propio sistema operativo el que cancele el proceso.

Otros casos, más prácticos, pueden ser cuando se cae la conexión con una base de datos en ciertas aplicaciones.

## Tratamiento de errores

Hasta ahora hemos visto por encima qué herramientas tenemos directamente para tratar errores y los tipos de errores que hay, pero no es lo único que necesitamos. Es necesario saber cómo queremos reaccionar ante estos errores y cómo diseñar nuestras aplicaciones para lidiar con ellos.

Este tratamiento de errores es dependiente de las herramientas y bibliotecas que utilicemos.

Siempre es preferible ir a los casos más sencillos y no complicarse mucho la vida. Eso sí, lo que un día es lo más sencillo al siguiente puede ser lo más complicado del mundo por lo que no hay que olvidar hacer refactorizaciones de código de forma periódica.

He estado buscando información sobre patrones de tratamiento de errores. He encontrado bastantes cosas sobre excepciones (como <a title="Patrones sobre uso de excepciones" href="http://c2.com/cgi/wiki?ExceptionPatterns" target="_blank">este</a>), pero no es lo que andaba buscando (lo que no significa que no exista). Por ese motivo voy a ir nombrando los patrones según me venga en gana (sí, es así de feo).

Lo más sencillo es empezar por los patrones que ejemplifican los tipos de error (diríamos que es lo más directo) y luego ir a patrones más complejos. No voy a ser demasiado sistemático con el tratamiento (aunque el ideal sería seguir la base explicada en la wikipedia sobre <a title="Patrones de diseño" href="http://es.wikipedia.org/wiki/Patr%C3%B3n_de_dise%C3%B1o" target="_blank">patrones de diseño</a>).

### En caso de error, pánico

Este es el caso típico de error no recuperable. Encontramos un error que nos impide continuar y hacemos **una parada ordenada** de la aplicación. Remarco lo de parada ordenada porque hacer _exit_ es sencillo, pero eso puede ser aún peor solución que el error que se haya producido.

Personalmente, a mi no me gusta este patrón, pero está muy extendido.

<img loading="lazy" decoding="async" class="aligncenter wp-image-710 " src="https://blog.laparca.es/wp-content/uploads/2015/02/pattern_panic.svg" alt="pattern panic" width="558" height="290" /> Este patrón puede ser más o menos complejo dependiendo de la aplicación. Se puede implementar utilizando _atexit_ o usando mecanismos más sofisticados que permitan emular _atexit_, pero incluyendo funcionalidades de reordenación y eliminación de las funciones de salida.

### En caso de error, reintentar

Si tenemos un patrón para parar ante un error, también hay uno para reintentar hasta que se resuelva la situación de error:

###<img loading="lazy" decoding="async" class="aligncenter wp-image-716" src="https://blog.laparca.es/wp-content/uploads/2015/02/pattern_retry.svg" alt="pattern_retry" width="235" height="294" /> En caso de error, propagar

Por lo general las aplicaciones están desarrolladas por capas bien diferenciadas. Cada capa se encarga de una cosa y suelen estar organizadas de tal modo que las capas superiores son más abstractas que las inferiores.

<img loading="lazy" decoding="async" class="aligncenter wp-image-718" src="https://blog.laparca.es/wp-content/uploads/2015/02/capas_app.svg" alt="capas_app" width="172" height="194" /> 

En este tipo de aplicación es útil el este patrón que consiste en detectar el error, hacer el tratamiento específico de recuperación de la capa y propagamos el error a la capa superior para que haga lo propio. Esto es lo que hacen normalmente las funciones de sistema: si encuentran un error lo informan a quien las haya llamado.

Antes de informar de que se ha producido un error se pueden hacer dos cosas:

  * Podemos hacer una recuperación del error para dejar la aplicación/biblioteca/objetos implicados en un estado consistente.
  * Podemos no hacer nada.

La elección dependerá de nuestra aplicación, aunque personalmente prefiero que se haga algo, aunque sea poner un comentario de «no es necesario realizar tratamiento alguno del error».

### Tratamiento diferido

Puede suceder que cuando se produce el error no podamos comprobar éste o simplemente prefiramos dejar el tratamiento para un momento más adecuado. Esto es muy útil cuando estamos trabajando con tareas asíncronas como <a title="Manual de Linux Asynchronous I/O" href="http://man7.org/linux/man-pages/man7/aio.7.html" target="_blank">el sistema</a> <a title="Guía de uso de AIO" href="https://code.google.com/p/kernel/wiki/AIOUserGuide" target="_blank">AIO</a> de Linux.

<img loading="lazy" decoding="async" class="aligncenter wp-image-721 " src="https://blog.laparca.es/wp-content/uploads/2015/02/pattern_delay.svg" alt="pattern_delay" width="454" height="351" /> 

### En caso de error, informar y preguntar

Si consideramos que nuestra aplicación se ajusta al lo mostrado antes (que se encuentra dividida en capas) puede darse el caso en que dudemos cómo puede afectar el tratamiento de errores a las capas superiores. Hay que tener en cuenta que cada capa debe comportarse como una caja negra para el resto.

Imaginemos por un momento que somos unos maniáticos de la encapsulación y tenemos un servicio a muy bajo nivel que falla. Sabemos que es un servicio complejo y que tiene que realizar una gran cantidad de pasos para llevarse a cabo por completo, por lo que en caso de que falle una parte es preferible reintentar a tener que empezar de nuevo. El problema es que para reintentar necesitamos consentimiento del usuario (o simplemente queremos informarle) y esa parte del programa no sabe nada sobre interfaces de usuario, ni salida por pantalla ni de un largo etcétera. En este caso lo que podemos hacer es utilizar una llamada de _callback_. Esta si se encontrará programada en un nivel que sabe cómo va la cosa para informar al usuario e indicar la acción a tomar:

Esto nos permitirá desacoplar las funcionalidades de la aplicación, pero, en cambio, hará más complejo el código (sobre todo en C). En otros lenguajes sería más sencillo gracias al uso de funciones lambda:

Vemos que ahora el tratamiento del error queda más cerca del punto donde lógicamente debería estar. En cualquier caso se puede mejorar más (aún le queda mucha mejora semántica).

En cualquier caso, como se ve en el ejemplo, no eliminamos el mecanismo de propagación. Esto lo hacemos para garantizar la máxima compatibilidad.

Debo reconocer que con esta idea empezamos a pensar en una API específica de tratamiento de errores. El motivo principal es que en aplicaciones pequeñas este tipo de tratamiento es un dolor de cabeza, pero en el trabajo empezamos a tener problemas por la falta de encapsulación. En este punto este tipo de soluciones nos compensa bastante.

## ¿Y a partir de aquí?

Hasta ahora hemos visto lo que pasa cuando nuestra aplicación detecta errores. Además, se ha abarcado los errores desde el punto de vista de cómo pueden afectar a la aplicación, pero no desde el punto de vista de cómo detectarlos nosotros. Esto es, alguien nos ha dicho que hay un error, pero, por ejemplo, ¿cómo detectamos que los datos pueden estar corruptos?

Por otra parte, no se ha tenido en cuenta los efectos que puede tener la multitarea en la aplicación. ¿Qué hacemos si un thread falla? ¿Y si son dos procesos independientes?

Y hay cosas más divertidas como ¿puedo fiarme de lo que dice el microprocesador? Todos hemos oído hablar alguna vez del famoso <a title="Fallo de coma flotante en procesadores Intel Pentium" href="http://en.wikipedia.org/wiki/Pentium_FDIV_bug" target="_blank">fallo en coma flotante de los procesadores Intel Pentium</a>.

Y hay muchas más cosas. Casi todo esto entra en lo que se denomina <a title="Tolerancia a fallos" href="http://es.wikipedia.org/wiki/Tolerancia_a_fallos" target="_blank">tolerancia a fallos</a>. Es un campo muy amplio.