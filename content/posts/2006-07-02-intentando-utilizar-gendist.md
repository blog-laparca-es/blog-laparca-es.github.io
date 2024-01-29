---
title: Intentando utilizar gendist
author: laparca
type: post
date: 2006-07-02T19:58:21+00:00
url: /2006/07/02/intentando-utilizar-gendist/
categories:
  - Desarrollo
  - GUL
  - Personal
  - Software libre

---
Bueno, esto está especialmente dirigido a tí, Jesús. El caso es que traté de instalarme gendist en Debian Sid y como que no (por lo menos con los repositorios estandar). A ver si mañana o pasado saco algo de tiempo y me instalo una <a target="_blank" title="Distribución GNU/Linux Ubuntu" href="http://www.ubuntu.com/">ubuntu</a> para probarlo.

Bueno, la idea que tengo, para el que lo quiera saber, es hacer una distro con <a target="_blank" title="Generador de distribuciones Live CD" href="https://forja.rediris.es/projects/gendist/">gendist</a> que tenga como escritorio <a target="_blank" title="Gestor de escritorio con un estilo semejante al de MS Windows XP" href="http://www.xpde.com/index.php">XPde</a>. Aunque a los amantes de GNU/Linux esto les puede revolver las tripas, creo que es un buen recurso para que la gente se acostumbre a utilizar GNU/Linux.

Si consigo algo, ya os lo contaré.

**Actualizado**: Bueno, ya he conseguido instalarlo y utilizarlo. La culpa era mía y del _<a target="_blank" href="http://en.wikipedia.org/wiki/Advanced_Packaging_Tool">apt</a>_ :@ La cosa era que cuando hacía _<a target="_blank" href="http://en.wikipedia.org/wiki/Dpkg">dpkg</a> -i gendist_ no instala las dependencias, pero luego el _apt_ no me dejaba actualizar. Así que todo pasaba por eliminar gendist, instalar a mano las dependencias y volver a instalar gendist. Ahora me da un fallo al tratar de hacer _<a target="_blank" href="http://en.wikipedia.org/wiki/Chroot">chroot</a>_.

**Actualizado**: Esto empieza a funcionar. El problema del _chroot_ parece que viene por el hecho de montar un directorio que se encuentra en un sistema montado a parte. Lo he hecho todo en la partición principal y ahora sí funciona :-). De momento estoy instalando las siguientes aplicaciones:

  * gimp
  * openoffice.org
  * totem
  * scribus
  * inkscape
  * XPde

No es gran cosa, pero para ir probando.