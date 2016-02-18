"*Java je programovací jazyk, původně vyvinutý společností Sun Microsystems a uvolněný v roce 1995 jako hlavní část Java platformy od Sun Microsystems. Jazyk odvozuje většinu své syntaxe z C a C++, ale má jednodušší objektový model a méně low-level prostředků. Java aplikace jsou obvykle kompilovány do mezikódu, který může běžet na libovolném Java virtuálním stoji (JVM = Java virtual machine) bez ohledu na architekturu počítače.*" [[1]](http://en.wikipedia.org/wiki/Java_(programming_language))

## Contents

*   [1 Instalace](#Instalace)
    *   [1.1 OpenJDK 7](#OpenJDK_7)
    *   [1.2 OpenJDK 8](#OpenJDK_8)
    *   [1.3 OpenJFX](#OpenJFX)

## Instalace

**Note:** Installing a JDK will automatically pull its JRE dependency.

**Note:** After installation, the Java environment will need to be recognized by the shell (`$PATH` variable). This can be done by sourcing `/etc/profile` from the command line or by logging out/in again of a Desktop Environment.

Two *common* packages named [java-runtime-common](https://www.archlinux.org/packages/?name=java-runtime-common) and [java-environment-common](https://www.archlinux.org/packages/?name=java-environment-common) are automatically pulled as dependency and provide environment file `/etc/profile.d/jre.sh`. This file contains all JVM common environment variables. Package [java-runtime-common](https://www.archlinux.org/packages/?name=java-runtime-common) also provides a utility script `archlinux-java` that can display and change the default Java environment. This script sets links `/usr/lib/jvm/default` and `/usr/lib/jvm/default-runtime` to point at a valid non-conflicting Java environment installed and Java runtime in `/usr/lib/jvm/java-${JAVA_MAJOR_VERSION}-${VENDOR_NAME`}. Most executable provided by the Java environment set have direct links from `/usr/bin`, others are available in `$PATH`.

**Warning:** File `/etc/profile.d/jdk.sh` is not provided any more by any package.

The following packages are available in the [official repositories](/index.php/Official_repositories "Official repositories"):

### OpenJDK 7

| Package name | Use |
| [jre7-openjdk-headless](https://www.archlinux.org/packages/?name=jre7-openjdk-headless) | Java runtime environment (*JRE*) without any graphical tool - version 7 |
| [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk) | Complete Java Runtime Environment (*JRE*) - version 7 |
| [jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk) | Java Development Kit (*JDK*) - version 7 |
| [openjdk7-doc](https://www.archlinux.org/packages/?name=openjdk7-doc) | OpenJDK javadoc - version 7 |
| [openjdk7-src](https://www.archlinux.org/packages/?name=openjdk7-src) | OpenJDK sources - version 7 |

### OpenJDK 8

| Package name | Use |
| [jre8-openjdk-headless](https://www.archlinux.org/packages/?name=jre8-openjdk-headless) | Java runtime environment (*JRE*) without any graphical tool - version 8 |
| [jre8-openjdk](https://www.archlinux.org/packages/?name=jre8-openjdk) | Complete Java Runtime Environment (*JRE*) - version 8 |
| [jdk8-openjdk](https://www.archlinux.org/packages/?name=jdk8-openjdk) | Java Development Kit (*JDK*) - version 8 |
| [openjdk8-doc](https://www.archlinux.org/packages/?name=openjdk8-doc) | OpenJDK javadoc - version 8 |
| [openjdk8-src](https://www.archlinux.org/packages/?name=openjdk8-src) | OpenJDK sources - version 8 |

### OpenJFX

JavaFX is also available from the official repositories. It requires the OpenJDK 8\.

| Package name | Use |
| [java-openjfx](https://www.archlinux.org/packages/?name=java-openjfx) | Java OpenJFX 8 client application platform (open-source implementation of JavaFX) |
| [java-openjfx-doc](https://www.archlinux.org/packages/?name=java-openjfx-doc) | OpenJFX javadoc |
| [java-openjfx-src](https://www.archlinux.org/packages/?name=java-openjfx-src) | OpenJFX sources |