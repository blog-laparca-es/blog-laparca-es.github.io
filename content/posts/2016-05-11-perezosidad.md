---
title: Perezosidad
author: laparca
type: post
date: 2016-05-11T14:50:21+00:00
url: /2016/05/11/perezosidad/
categories:
  - Personal

---
Algo que me ha sorprendido mucho de haskell y, que aún me cuesta mucho lidiar con ello, es el hecho de que sea perezoso.

**¿Y eso qué significa?**

Significa que no va a ejecutar las cosas sin más, sino que se esperará hasta que no le quede más remedio.

Por ejemplo, si tenemos algo como esto:

Como se puede ver, se «crea» una lista de infinitos elementos que empiezan en 1 (_intinite_list_). Como no accedemos a ningún elemento, el compilador en realidad no crea nada en memoria.

Luego indicamos que queremos elevar todos los elementos al cuadra para después quedarnos con aquellos que no son múltiplos de dos ni de tres. Eso lo almacenamos en _values_. En haskell esto significa que _values_ representa esa operación, no que contenga dichos valores, así que aquí tampoco ha hecho nada: no ha elevado los infinitos elementos al cuadrado ni ha filtrado después.

Lo último que hacemos es un _take 10_. En este momento (si utilizamos _ghci_), en este momento intenta mostrar los 10 primeros elementos, lo que fuerza a hacer todo lo anterior. ¡Pero sólo lo hace sobre los 10 primeros! Ni elevamos la lista entera al cuadro, ni comprobamos los infinitos elementos. Sólo vamos a hacer esto las veces justas.

Esto lo hace todo el compilador por su cuenta.

**¿A dónde quieres ir a parar?**

Pues estaba hace poco mirando documentación de <a href="https://www.rust-lang.org/" target="_blank">Rust</a> y me he encontrado con algo muy parecido:

Básicamente hace lo miso y me sorprendió mucho porque Rust no es un lenguaje que haga evaluación perezosa.

**¿Entonces cómo lo hace?**

Pues simulando la evaluación perezosa. Para ello lo que hace es jugar con <a href="https://doc.rust-lang.org/book/iterators.html" target="_blank">iteradores</a> personalizados. Cada iterador tiene información de qué es lo que va a hacer cuando se llame a su función _next_. Así que cuando llamamos a _map_ lo que hace es crear en memoria la información necesaria para hacer la operación, pero no la ejecuta. Lo mismo sucede con los filtros. Cuando llamamos al _next_ de iterador resultante, este ejecuta el _next_ del iterador que contiene y luego comprueba o ejecuta la condición que tenga definida.

**Conclusión**

Sinceramente me ha encantado ver esta aproximación. Es una modo fantástico de lidiar con el problema de infinito de un modo sencillo. Esto permite tratar muchas cosas como iteradores que, aún dando listas potencialmente infinitas, no tengan un gran impacto en rendimiento (o sí, todo dependen de como esté diseñado).

Si quieres saber más sobre evaluación perezosa quizá te interese ver <a href="https://en.wikipedia.org/wiki/Lazy_evaluation" target="_blank">la entrada en Wikipedia</a>.