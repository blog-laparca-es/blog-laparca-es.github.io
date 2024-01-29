---
title: 'Controladores en espacio de usuario: ¡por fin!'
author: laparca
type: post
date: 2007-07-22T08:53:33+00:00
url: /2007/07/22/controladores-en-espacio-de-usuario-por-fin/
categories:
  - Personal

---
Estaba esta mañana leyendo las noticias en <a href="http://www.osnews.com/" title="Noticias sobre sistemas operativos" target="_blank">OS News</a> y me he encontrado con la grata noticia de que por fin se podrán incluir <a href="http://liquidat.wordpress.com/2007/07/21/linux-kernel-2623-to-have-stable-userspace-driver-api/" target="_blank">controladores en espacio de usuario en el núcleo Linux</a>.

Sé que hay gente que no entiende muy bien la motivación de este tipo de controladores, pero a mi me parece una de las carencias más significativas dentro del núcleo. Con el sistema actual, si quieres recompilar el núcleo, también debes recompilar los módulos del mismo. Con el modelo nuevo, sólo será necesario recompilar el núcleo.

La idea es que convivirán ambos modelos, de tal modo que se podrá utilizar el que más convenga. Hay que tener en cuenta que los controladores en espacio de usuario son más lentos que su homologos en espacio de núcleo. Por lo que he leido, está bastante orientado al uso de controladores propietarios, que pueden no ser mantenidos en el tiempo y que de este modo podrán utilizarse con menos dificultades (pero con un rendimiento inferior).

Sé que hay gente que la idea de los controladores propietarios le disgustará: si no los quieres, no compres hardware que lo use. De todos modos, en el ámbito empresarial hay mucho hardware que, por desgracia, puede no tener controlador libre, lo que significaría que las empresas tendría menos temores a hacer controladores para linux y con ello facilitaría la entrada de linux aún más al mundo empresarial.