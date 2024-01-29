---
title: Diseño de sistema operativo
author: laparca
type: post
date: 2007-10-28T22:46:12+00:00
url: /2007/10/29/diseno-de-sistema-operativo/
categories:
  - Opinión
  - Personal

---
El otro día estaba hablando con un amig y este me comentaba que siendo Linus sólo un estudiante había ganado la batalla contra Taembaum sobre los núcleos. En realidad yo no lo veo así. De hecho veo justo lo contrario: conforme  pasa el tiempo, cada vez Linux está más lejos de ganar esa batalla. Es más grande e inmanejable, efecto que en un núcleo monolítico no hubiese pasado.

Es cierto que en su momento un núclero monolítico era mejor solución: son algo más rápidos. Pero ¿qué sucede con las nuevas arquitecturas de CPU con mútiples cores? ¿Es posible que un núcleo monolítico pueda se menos eficiente que uno de tipo micronúcleo? Personalmente apuesto por esto último, aunque claro, siempre puedes hacer que el núcleo se bifurque en distintos hilos de ejecución, pero haciendo eso ¿no estás conviertiendo tu núcleo poco a poco en un sitemo de tipo micronúcleo?

Ciertamente parece que Linux va en ese camino, ya que los grandes avances que se están consiguiendo son casi todos en el espacio de usuario y cada vez más los subsistemas se alejan del núcleo. De hecho, leía hace poco en una lista de correo a uno de los suscriptores que se quejaba porque le parecía una aberración el que los nuevos escritorios de Linux no utilizasen el sistema de ficheros virutal que este traía y, en su lugar, implementasen los suyos propios. Pero nada más lejos de la realidad, en un sistema en el que cada vez que compilas una parte del núcleo estás obligado a compilar el resto, depender de una parte de este núcleo para un entorno de escritorio es un suicido. De hecho, se ve como está empezando a tener mucha relevancia FUSE, que lo que hace es precisamente menter los controladores de sistema de ficheros en el espacio de usuario. De este modo se consigue que sea menos traumático el cambio de núcleo.

Será grande el día que el tener que cambiar una cosa el núcleo no obligue a tener que compilarlo todo (núcleo y módulos).