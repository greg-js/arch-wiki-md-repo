This document defines a proposed standard for packaging Java programs under Arch Linux. Java programs are notoriously difficult to package cleanly without overlapping dependencies. This document describes a way to remedy this situation. These guidelines are flexible in order to cover the many different scenarios that arise when dealing with Java applications.

## Contents

*   [1 介绍](#.E4.BB.8B.E7.BB.8D)
*   [2 典型的Java应用软件的结构](#.E5.85.B8.E5.9E.8B.E7.9A.84Java.E5.BA.94.E7.94.A8.E8.BD.AF.E4.BB.B6.E7.9A.84.E7.BB.93.E6.9E.84)
*   [3 Arch下的Java打包](#Arch.E4.B8.8B.E7.9A.84Java.E6.89.93.E5.8C.85)
    *   [3.1 目录树结构实例](#.E7.9B.AE.E5.BD.95.E6.A0.91.E7.BB.93.E6.9E.84.E5.AE.9E.E4.BE.8B)
    *   [3.2 依赖关系](#.E4.BE.9D.E8.B5.96.E5.85.B3.E7.B3.BB)
*   [4 针对Arch64 用户](#.E9.92.88.E5.AF.B9Arch64_.E7.94.A8.E6.88.B7)

## 介绍

Arch Linux packagers cannot seem to agree on how to handle Java packages. Various methods are used in `PKGBUILD`s across the official and unofficial repositories and in the [AUR](https://aur.archlinux.org/). These solutions include placing the whole mess in `/opt` with shell scripts in `/usr/bin` or profiles placed in `/etc/profile`. Others are placed in directories in `/usr/share` with scripts placed in `/usr/bin`. Many add unnecessary files to the system `CLASSPATH` and `PATH`.

## 典型的Java应用软件的结构

大部分的桌面Java应用程序结构简单，它们经常独立于系统安装（但依赖于java软件包）。This usually installs everything in a single directory with subdirectories called `bin`, `lib`, `jar`, `conf`, etc. There is usually a main jar file containing the main executable classes. A shellscript is usually provided to run the main class so users do not have to invoke the Java interpreter directly. This shell script is usually quite complex, as it is generic across distros, and often includes special cases for different systems (ie: CYGWIN).

The `lib` directory, often contains bundled jar files that satisfy dependencies of the Java application. This makes it simple for a user to install the program (all dependencies included), but is a package developer's nightmare. It is a waste of space when several packages bundle the same dependency. This was not a big issue in the past when there were fewer desktop Java applications and libraries, and those that existed tended to be very large anyway. Things are different now...

Other files necessary to run the program are usually stored in the same folder as the main jar file, or a subdirectory thereof. Since Java programs don't know where their classes were loaded from, they usually need to be run from within this directory (i.e. the shell script should `cd` into the directory), or an environment variable is set to indicate the directory's location.

## Arch下的Java打包

Packaging Java applications in Arch is going to take quite a bit more work for packagers than it currently does. The effort will be worth it, however, resulting in a cleaner filesystem and fewer bundled dependencies (as more and more Java libraries are refactored into their own packages, packaging will become easier). The following guidelines should be followed in creating an Arch Linux Java package:

*   If a Java library has a generic name, the package name should be prepended with the title `java-` to help distinguish it from other libraries. This is not necessary with uniquely named packages (like JUnit), end-user programs (like Eclipse), or libraries that can be uniquely described with another prefix (like jakarta-commons-collections or apache-ant).

*   You do not need to compile Java applications from source. Very little optimization goes into the compile process, as with gcc created binaries. If the source package provides an easy way to build from source go ahead and use it, but if its easier to just grab a binary release of a jar file or an installer you may use that as well.

*   Place all jar files (and no other files) distributed with the program in a `/usr/share/java/myprogram` directory. This includes all dependency jar files distributed with the application. However, effort should be made to place common or large dependency libraries into their own packages. This can only happen if the program does not depend on a specific version of a dependency library.

This rule makes it possible to iteratively refactor dependencies. That is, the package and all its dependencies can be placed into one directory at first. After this has been tested, major dependencies can be refactored out one at a time. Note that some applications include bundled dependencies inside the main jar file. That is, they unjar the bundled dependencies and include them in the main jar. Such dependencies are usually very small and there is little point in refactoring them.

*   If the program is meant to be run by the user, write a custom shell script that runs the main jar file. This script should be placed in `/usr/bin`. Libraries generally don't require shell scripts. Write the shell script from scratch, rather than using one that is bundled with the program. Remove code that tests for custom environments (like CYGWIN), and code that tries to determine if `JAVA_HOME` has been set (The J2RE package ensures `JAVA_HOME` has been properly set, so we do not need to test for it).

*   Set the `CLASSPATH` using the `-cp` option to the Java interpreter unless there is an explicit reason not to (ie: the `CLASSPATH` is used as a plugin mechanism). The `CLASSPATH` should include all jar files in the `/usr/share/java/myprogram` direcory, as well as jar files that are from dependency libraries that have been refactored to other directories. You can use something like the following code:

```
for name in /usr/share/java/myprogram/*.jar ; do
  CP=$CP:$name
done
CP=$CP:/usr/share/java/dep1/dep1.jar
java -cp $CP myprogram.java.MainClass

```

*   Make sure the shellscript is executable!

*   Other files distributed with the package should be stored in a directory named after the package under `/usr/share`. You may need to set the location of this directory in a variable like `MYPROJECT_HOME` inside the shellscript. This guideline assumes that the program expects all files to be in the same directory (as is standard with Java packages). If it seems more natural to put a configuration file elsewhere (for example, a daemon in `/etc/rc.d` or logs in `/var/log`), then feel free to do so.

Bear in mind that `/usr` may be mounted as read-only on some systems. If there are files in the shared directory that need to be written by the application, they may have to be relocated to `/etc`, `/var`, or the user's home directory.

*   As is standard with Arch Linux packages, if the above standards cannot be adhered to without a serious amount of work, the package should be installed in its preferred manner, with the resulting directory located in `/opt`. This is useful for programs that bundle JREs or include customized versions of dependencies, or do other strange or painful tasks.

### 目录树结构实例

To clarify, here is an example directory structure for a hypothetical program called `foo`. Since `foo` is a common name, the package is named `java-foo`, but notice this is not reflected in the directory structure:

*   `/usr/share/java/foo/`
*   `/usr/share/java/foo/foo.jar`
*   `/usr/share/java/foo/bar.jar` (included dependency of `java-foo`)
*   `/usr/share/foo/`
*   `/usr/share/foo/*.*` (some general files required by `java-foo`)
*   `/usr/bin/foo` (executable shell script)

### 依赖关系

Java包会根据需要，会依赖于'java-runtime' 或者'java-environment'。

For most packages, `java-runtime` is what is needed to simply run software written in Java. `java-runtime` is a virtual dependency provided by:

*   [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk) (free)
*   [java-gcj-compat](https://aur.archlinux.org/packages/java-gcj-compat/) (free)
*   [jre](https://aur.archlinux.org/packages/jre/) (non-free)

`java-environment` (e.g. JDK) is needed by packages that will need to compile Java source code into bytecode. `java-environment` is a virtual dependency provided by:

*   [jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk) (free)
*   [jdk](https://aur.archlinux.org/packages/jdk/) (non-free)

## 针对Arch64 用户

This does not appear to be available for 64-bit.