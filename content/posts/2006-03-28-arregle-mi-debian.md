---
title: Arreglé mi debian
author: laparca
type: post
date: 2006-03-27T23:43:51+00:00
url: /2006/03/28/arregle-mi-debian/
categories:
  - Personal

---
Bueno, no había comentado nada, pero llevaba dos semana sin poder actualizar porque me daba problemas libc6. Cascaba sin demasiados motivos en el script de pre-instalación.

Al final, para solucionarlo, depués de updates, upgrades, dist-upgrades y &#8211;forces varios, tuve que hacer lo siguiente:

dpkg -x /var/[..].deb /

en pocas palabras: un **super &#8211;force**. 😛