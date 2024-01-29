---
title: El testigo de Windows Vista
author: laparca
type: post
date: 2007-10-26T09:53:14+00:00
url: /2007/10/26/el-testigo-de-windows-vista/
categories:
  - Opinión
  - Software libre

---
Cuando empezaron a salir copias de MS Window Vista, después de que se demostrase que no traía nada nuevo y a tener en consideración, se empezó a especular de que sería linux quien tomase el testigo. El caso es que con el paso del tiempo creo que ha sido más bien MacOS X quien ha cogido dicho testigo ¿por qué?

Según yo lo veo, a linux aún le falta mucho para poder ser una opción completamente viable para el usuario. Sin duda alguna se han hecho grandes avances en este sentido, pero sigue abiendo un problema: a la mayor parte de desarrolladores de software libre les importa un pimiento los usuarios mortales. Además, el hecho de que no se facilite la inclusión de controladores no libres dentro del núcleo hace que muchas empresas rechacen la idea de dar soporte a dicho núcleo. Espero que con la aparición de los [controladores a nivel de usuario][1] este último punto pueda cambiar un poco esta última parte. ¿Y qué pasa con el resto del sistema?

Desde <a href="http://www.freedesktop.org/" target="_blank">freedesktop.org</a> están haciendo un gran esfuerzo en la parte de estandarizar la interfaz de los entornos gráficos de linux, pero más centrados en sus funcionalidades que en otra cosa. En mi opinión, creo que el mayor problema que sufre linux en este sentido es el servidor X, un sistema completamente anticuado y arcaico, al que le cuesta mucho incorporar nuevas mejoras. Además, la existencia de distintos escritorios también disminuye la atracción que sienten los usuario por este sistema. Es cierto, esta capacidad del usuario de poder elegir es una ventaja, pero también es cierto que el usuario es vago y no quiere elegir. Se debería unificar el sistema de desarrollo dentro del propio servidor, que dibujar un botón de el mismo resultado en KDE, en GNOME, en Motif, etc. y que sea el servidor de ventanas el encargado de dibujar dicho botón o un subsistema a parte. Tampoco importa mucho, el caso es que sea todo completamente homogéneo. Es curioso que los únicos que tratan de conseguir este objetivo son la gente de KDE, ampliamente criticados por la comunidad (supongo que por tratar de hacer las cosas bien [nooooo, no busco un flamewar, noooo ;-)]).

Otro ejemplo de como se hacen las cosas en Linux es el de la conectividade WiFi a través de los protocolos 802.11X, donde cada módulo era de su padre y de su madre y no había nada medianamente estandarizado, algo a lo que ahora, por fin, se está tratando de poner remedio. Y es que si en el propio núcleo las interfaces nos están claramente definidas, cómo se pueden hacer herramientas de calidad para dicho núcleo.

También hay que tener en cuenta un factor importante: el usuario es vago, tanto el usuario avanzado como en novel. No queremos tener que meternos en la consola a menos que sea necesario. Yo, cuando configuro un apache, me parece una burrada tener que abrir un editor de textos, sobre todo para hacer alguna tontería. Es cierto que en según que casos puede venir bien abrir el fichero, pero yo no veo bien el hecho de tener que hacerlo todo de ese modo, es incómodo en un mucho casos se pierde eficiencia por ello (a menos que seas un gurú de la configuración de apache). Y al igual que apache, con el resto de servicios pasa lo mismo: no deberían configurarse desde consola. Además, una interfaz puede ser menos propensa a fallos, ya que podría controlar los errores antes de meterlos. En este sentido, SuSE hizo un gran avance con su herramienta YaST, pero aún le faltaba algo, se quedaba muy escasa.

Podría seguir despotricando contra Linux, pero, por hoy, ya me he quedado agusto.

 [1]: http://blog.laparca.es/index.php/2007/07/22/controladores-en-espacio-de-usuario-por-fin/ "controladores a nivel de usuario en el núcleo Linux"