# Java (Español)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:Java (Español)#](https://wiki.archlinux.org/index.php/Talk:Java_(Espa%C3%B1ol)))

Originario de [Wikipedia article](https://en.wikipedia.org/wiki/Java_(programming_language) "wikipedia:Java (programming language)"):

Java es un lenguaje de programación desarrollado originalmente por Sun Microsystems lanzado en 1995 como un componente central de Sun Microsystems' Java Platform. El lenguaje se deriva en gran parte de la sintaxis de C y C++ pero tiene un modelo de objetos más sencillo y menos facilidades de bajo nivel. Las aplicaciones java son normalmente compiladas en códigos de bytes que pueden correr en alguna máquina virtual java (JVM por sus siglas en inglés) independientemente de la arquitectura de la computadora.

Arch Linux oficialmente soporta el paquete de código abierto [OpenJDK](http://openjdk.java.net/) versión 7 y 8\. Todas las JVM pueden ser instaladas sin conflictos e intercambiadas antes de usar con la ayuda de un script `archlinux-java`. Otros ambientes java están disponibles en [AUR](/index.php/AUR "AUR") pero no son oficialmente soportados.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
    *   [1.1 OpenJDK 7](#OpenJDK_7)
    *   [1.2 OpenJDK 8](#OpenJDK_8)
    *   [1.3 OpenJFX](#OpenJFX)

## Instalación

**Note:** Installing a JDK will automatically pull its JRE dependency.

**Note:** After installation, the Java environment will need to be recognized by the shell (`$PATH` variable). This can be done by sourcing `/etc/profile` from the command line or by logging out/in again of a Desktop Environment.

Two _common_ packages named [java-runtime-common](https://www.archlinux.org/packages/?name=java-runtime-common) and [java-environment-common](https://www.archlinux.org/packages/?name=java-environment-common) are automatically pulled as dependency and provide environment file `/etc/profile.d/jre.sh`. This file contains all JVM common environment variables. Package [java-runtime-common](https://www.archlinux.org/packages/?name=java-runtime-common) also provides a utility script `archlinux-java` that can display and change the default Java environment. This script sets links `/usr/lib/jvm/default` and `/usr/lib/jvm/default-runtime` to point at a valid non-conflicting Java environment installed and Java runtime in `/usr/lib/jvm/java-${JAVA_MAJOR_VERSION}-${VENDOR_NAME`}. Most executable provided by the Java environment set have direct links from `/usr/bin`, others are available in `$PATH`.

**Warning:** File `/etc/profile.d/jdk.sh` is not provided any more by any package.

The following packages are available in the [official repositories](/index.php/Official_repositories "Official repositories"):

### OpenJDK 7

<table class="wikitable">

<tbody>

<tr>

<th>Package name</th>

<th>Use</th>

</tr>

<tr>

<td>[jre7-openjdk-headless](https://www.archlinux.org/packages/?name=jre7-openjdk-headless)</td>

<td>Java runtime environment (_JRE_) without any graphical tool - version 7</td>

</tr>

<tr>

<td>[jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk)</td>

<td>Complete Java Runtime Environment (_JRE_) - version 7</td>

</tr>

<tr>

<td>[jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk)</td>

<td>Java Development Kit (_JDK_) - version 7</td>

</tr>

<tr>

<td>[openjdk7-doc](https://www.archlinux.org/packages/?name=openjdk7-doc)</td>

<td>OpenJDK javadoc - version 7</td>

</tr>

<tr>

<td>[openjdk7-src](https://www.archlinux.org/packages/?name=openjdk7-src)</td>

<td>OpenJDK sources - version 7</td>

</tr>

</tbody>

</table>

### OpenJDK 8

<table class="wikitable">

<tbody>

<tr>

<th>Package name</th>

<th>Use</th>

</tr>

<tr>

<td>[jre8-openjdk-headless](https://www.archlinux.org/packages/?name=jre8-openjdk-headless)</td>

<td>Java runtime environment (_JRE_) without any graphical tool - version 8</td>

</tr>

<tr>

<td>[jre8-openjdk](https://www.archlinux.org/packages/?name=jre8-openjdk)</td>

<td>Complete Java Runtime Environment (_JRE_) - version 8</td>

</tr>

<tr>

<td>[jdk8-openjdk](https://www.archlinux.org/packages/?name=jdk8-openjdk)</td>

<td>Java Development Kit (_JDK_) - version 8</td>

</tr>

<tr>

<td>[openjdk8-doc](https://www.archlinux.org/packages/?name=openjdk8-doc)</td>

<td>OpenJDK javadoc - version 8</td>

</tr>

<tr>

<td>[openjdk8-src](https://www.archlinux.org/packages/?name=openjdk8-src)</td>

<td>OpenJDK sources - version 8</td>

</tr>

</tbody>

</table>

### OpenJFX

JavaFX is also available from the official repositories. It requires the OpenJDK 8\.

<table class="wikitable">

<tbody>

<tr>

<th>Package name</th>

<th>Use</th>

</tr>

<tr>

<td>[java-openjfx](https://www.archlinux.org/packages/?name=java-openjfx)</td>

<td>Java OpenJFX 8 client application platform (open-source implementation of JavaFX)</td>

</tr>

<tr>

<td>[java-openjfx-doc](https://www.archlinux.org/packages/?name=java-openjfx-doc)</td>

<td>OpenJFX javadoc</td>

</tr>

<tr>

<td>[java-openjfx-src](https://www.archlinux.org/packages/?name=java-openjfx-src)</td>

<td>OpenJFX sources</td>

</tr>

</tbody>

</table>

Retrieved from "[https://wiki.archlinux.org/index.php?title=Java_(Español)&oldid=417079](https://wiki.archlinux.org/index.php?title=Java_(Español)&oldid=417079)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Programming languages (Español)](/index.php/Category:Programming_languages_(Espa%C3%B1ol) "Category:Programming languages (Español)")

Hidden category:

*   [Pages or sections flagged with Template:Out of date](/index.php/Category:Pages_or_sections_flagged_with_Template:Out_of_date "Category:Pages or sections flagged with Template:Out of date")