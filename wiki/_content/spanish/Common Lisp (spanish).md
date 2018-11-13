**Estado de la traducción**
Este artículo es una traducción de [Common Lisp](/index.php/Common_Lisp "Common Lisp"), revisada por última vez el **2018-10-29**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Common_Lisp&diff=0&oldid=552388) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Common Lisp](https://common-lisp.net/) es un lenguaje multi-paradigma altamente dinámico que enfatiza la interactividad y el rendimiento.

## Contents

*   [1 Implementaciones](#Implementaciones)
*   [2 Quicklisp](#Quicklisp)
*   [3 SLIME](#SLIME)
*   [4 Véase también](#Véase_también)

## Implementaciones

Hay múltiples implementaciones disponibles:

*   **[ABCL](https://en.wikipedia.org/wiki/Common_Lisp#List_of_implementations "wikipedia:Common Lisp")** — Armed Bear Common Lisp

	[https://common-lisp.net/project/armedbear/](https://common-lisp.net/project/armedbear/) || [abcl](https://aur.archlinux.org/packages/abcl/)

*   **[CCL](https://en.wikipedia.org/wiki/Clozure_CL "wikipedia:Clozure CL")** — Clozure Common Lisp

	[https://ccl.clozure.com/](https://ccl.clozure.com/) || [ccl](https://aur.archlinux.org/packages/ccl/)

*   **[CLISP](https://en.wikipedia.org/wiki/CLISP "wikipedia:CLISP")** — ANSI Common Lisp interpreter, compiler and debugger

	[https://clisp.sourceforge.io/](https://clisp.sourceforge.io/) || [clisp](https://www.archlinux.org/packages/?name=clisp)

*   **[CMUCL](https://en.wikipedia.org/wiki/CMU_Common_Lisp "wikipedia:CMU Common Lisp")** — CMU Common Lisp

	[https://www.cons.org/cmucl/](https://www.cons.org/cmucl/) || [cmucl](https://www.archlinux.org/packages/?name=cmucl)

*   **[ECL](https://en.wikipedia.org/wiki/Incrustar_Common_Lisp "wikipedia:Incrustar Common Lisp")** — Embeddable Common Lisp

	[https://common-lisp.net/project/ecl/](https://common-lisp.net/project/ecl/) || [ecl](https://www.archlinux.org/packages/?name=ecl)

*   **[SBCL](https://en.wikipedia.org/wiki/Steel_Bank_Common_Lisp "wikipedia:Steel Bank Common Lisp")** — Steel Bank Common Lisp

	[http://www.sbcl.org/](http://www.sbcl.org/) || [sbcl](https://www.archlinux.org/packages/?name=sbcl)

SBCL presenta un compilador de generación de código nativo altamente optimizado con orígenes que se remontan a principios de los 90\. Conocido por su precisa derivación de tipo y su estricta conformidad con el estándar ANSI, es particularmente adecuado para propósitos generales y la programación científica. SBCL es un fork de CMUCL. CMUCL es una implementación exclusiva de posix que se desarrolló originalmente en Carnegie Mellon. Por otro lado, tanto ECL como CLISP ofrecen una buena incrustabilidad e integración con C. Clozure es una implementación basada en Open Macintosh Common Lisp. Es conocido por sus rápidos tiempos de compilación. ABCL ejecuta la máquina virtual java.

## Quicklisp

[Quicklisp](https://www.quicklisp.org/beta/) ([quicklisp](https://aur.archlinux.org/packages/quicklisp/)) es un administrador de paquetes escrito en common lisp para cargar librerías common lisp. Funciona en todas las implementaciones importantes de common lisp, y es la opción dominante para mantener paquetes common lisp dentro de la comunidad de common lisp.

## SLIME

Para conocer la experiencia interactiva por la que se conoce a Common Lisp, vea [slime](/index.php/Slime "Slime").

## Véase también

*   [Wikipedia:Common Lisp](https://en.wikipedia.org/wiki/es:Common_Lisp "wikipedia:es:Common Lisp")
*   [Common Lisp Wiki](http://cliki.net)
*   [Online Specification / Hyperspec](http://www.lispworks.com/documentation/HyperSpec/Front)