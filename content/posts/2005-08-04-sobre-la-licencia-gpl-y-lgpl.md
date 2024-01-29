---
title: Sobre la licencia GPL y LGPL
author: laparca
type: post
date: 2005-08-04T13:21:40+00:00
url: /2005/08/04/sobre-la-licencia-gpl-y-lgpl/
categories:
  - Derechos de autor
  - Software libre

---
Para hacer un final contundente sobre lo de las dobles licencias y la posibilidad de hacer software propietario con la GPL, expongo a continuación un fragmento de la licencia GPL, para ser más exacto, el punto 2.b:

<pre>You must cause any work that you distribute or publish,
that in whole or in part contains or is derived from the Program
or any part thereof, to be licensed as a whole at no charge to all
third parties under the terms of this License.
</pre>

Que traducido dice:

<pre>Debe hacer que cualquier trabajo que distribuya o publique y
que en todo o en parte contenga o sea derivado del Programa
o de cualquier parte de él sea licenciada como un todo, sin carga
alguna, a todas las terceras partes y bajo los términos de esta Licencia.
</pre>

Como _Programa_ se entiende (ver punto 0 de la licencia):

<pre>This License applies to any program or other work which contains
a notice placed by the copyright holder saying it may be distributed
under the terms of this General Public License. The "Program",
below, refers to any such program or work, and a "work based on the
Program" means either the Program or any derivative work under
copyright law: that is to say, a work containing the Program or a
portion of it, either verbatim or with modifications and/or
translated into another language. (Hereinafter, translation is
included without limitation in the term "modification".) Each licensee
is addressed as "you".
</pre>

O dicho de otro modo, en la licencia GPL, Programa es toda aquella aplicación bajo los términos de la licencia.

Con esta información, se entiende que si se enlaza un programa propietario a una librería bajo los términos de la licencia GPL, este debe ser también GPL ya que utilizará partes con GPL.

Para salvar esta situación, se incluye en la licencia lo siguiente:

<pre>These requirements apply to the modified work as a whole.
If identifiable sections of that work are not derived from the
Program, and can be reasonably considered independent and
separate works in themselves, then this License, and its terms,
do not apply to those sections when you distribute them as
separate works. But when you distribute the same sections as
part of a whole which is a work based on the Program, the
distribution of the whole must be on the terms of this License,
whose permissions for other licensees extend to the entire
whole, and thus to each and every part regardless of who wrote it. 
</pre>

Que traducido queda como:

<pre>Estos requisitos se aplican al trabajo modificado como un
todo. Si partes identificables de ese trabajo no son derivadas
del Programa, y pueden, razonablemente, ser consideradas
trabajos independientes y separados por ellos mismos,
entonces esta Licencia y sus términos no se aplican a esas
partes cuando sean distribuidas como trabajos separados.
Pero cuando distribuya esas mismas secciones como partes
de un todo que es un trabajo basado en el Programa, la
distribución del todo debe ser según los términos de esta
licencia, cuyos permisos para otros licenciatarios se
extienden al todo completo, y por lo tanto a todas y cada una
de sus partes, con independencia de quién la escribió.
</pre>

De este modo, si enlazo con la librería, no hace falta convertir a GPL el programa, porque no es un todo&#8230; ¿O sí? Supongo que eso dependerá de varios fatores:

  * Si se enlaza estáticamente, si sería un todo, por lo que debe convertirse en GPL
  * Si se enlaza dinámicamente y si siempre distribuyes tu aplicación con dichas librerías, ¿sería un todo o solo la suma de las partes?

Este segundo punto queda un poco oscuro y supongo que dependerá de la interpretación de cada cual.

La licencia LGPL surgió como mecanismo para evitar problemas de este tipo. Con ella, se puede enlazar (siempre que sea dinámicamente) con librerías y nunca habrá problemas de licencia. Está pensada precisamente para ello.

Volviendo al punto que empezó esto, las QT: si la licencia es GPL (sin modificaciones), me da igual que mi aplicación sea o no propietaria, puedo enlazarla sin que tenga que pagar a trolltech. Igualmente pasa con MySQL. La única razón que estas (MySQL y Trolltech) tendrían para obligarte a pagar sería la interpretación del segundo punto anterior, ya que de otro modo, la licencia GPL te eximiría del cambio de licencia de tu aplicación.

De todos modos, esto creo que es mejor que nos lo explique un abogado o estudiante de derecho (Sergio, ¿te apuntas?).

Enlaces:

  * [Licencia pública GNU GPL][1]
  * [Licencia pública GNU LGPL][2]
  * [Traducción no oficial de la licencia GNU GPL][3]

 [1]: http://www.gnu.org/licenses/gpl.html
 [2]: http://www.gnu.org/licenses/lgpl.html
 [3]: http://www.es.gnu.org/licencias/gples.html