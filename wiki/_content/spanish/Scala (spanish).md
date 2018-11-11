**Estado de la traducción**
Este artículo es una traducción de [Scala](/index.php/Scala "Scala"), revisada por última vez el **2018-11-09**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Scala&diff=0&oldid=551804) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Java](/index.php/Java_(Espa%C3%B1ol) "Java (Español)")

De [Wikipedia](https://en.wikipedia.org/wiki/es:Scala_(lenguaje_de_programaci%C3%B3n) "wikipedia:es:Scala (lenguaje de programación)"):

	*Scala es un lenguaje de programación multi-paradigma diseñado para expresar patrones comunes de programación en forma concisa, elegante y con tipos seguros. Integra sutilmente características de lenguajes funcionales y orientados a objetos. La implementación actual corre en la máquina virtual de Java y es compatible con las aplicaciones Java existentes.*

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [scala](https://www.archlinux.org/packages/?name=scala) disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"). Además, puede instalar los paquetes [scala-docs](https://www.archlinux.org/packages/?name=scala-docs) y/o [scala-sources](https://www.archlinux.org/packages/?name=scala-sources) para futuras referencias.

Dado que Scala se ejecuta en una [JVM](https://en.wikipedia.org/wiki/es:M%C3%A1quina_virtual_Java (JRE) funcional para ejecutar o compilar sus programas.

## Utilización e IDEs

Al igual que en otros lenguajes de programación como [Python](/index.php/Python_(Espa%C3%B1ol) "Python (Español)"), puede interactuar con un intérprete

```
$ scala

Welcome to Scala version 2.*.* (OpenJDK Server VM, Java 1.*.*).
Type in expressions to have them evaluated.
Type :help for more information.

scala>

```

así como simplemente compilar y ejecutar sus programas desde la línea de comandos.

```
$ scalac HelloWorld.scala
$ scala HelloWorld

```

Muchos [IDEs](/index.php/IDE "IDE") diferentes como [Eclipse](/index.php/Eclipse_(Espa%C3%B1ol) "Eclipse (Español)") o [NetBeans](/index.php/Netbeans_(Espa%C3%B1ol) "Netbeans (Español)") ofrecen soporte para Scala. El paquete [eclipse-scala-ide](https://aur.archlinux.org/packages/eclipse-scala-ide/) por ejemplo está disponible en [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)"). También puede descargar un IDE optimizado para Scala y basado en Eclipse directamente desde [la página web oficial de Scala](https://scala-lang.org).

## Véase también

*   [Scala Lang](http://scala-lang.org) - página web oficial
*   [Tutorial de Scala](http://tutorials.jenkov.com/scala/index.html) - una serie de pequeños tutoriales de Scala
*   [Aprenda X=Scala en Y minutos](http://learnxinyminutes.com/docs/scala/)