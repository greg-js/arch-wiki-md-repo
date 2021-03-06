Related articles

*   [Java Package Guidelines](/index.php/Java_Package_Guidelines "Java Package Guidelines")
*   [Java Runtime Environment fonts](/index.php/Java_Runtime_Environment_fonts "Java Runtime Environment fonts")

From the [Wikipedia article](https://en.wikipedia.org/wiki/Java_(programming_language) "wikipedia:Java (programming language)"):

	Java is a programming language originally developed by Sun Microsystems and released in 1995 as a core component of Sun Microsystems' Java platform. The language derives much of its syntax from C and C++ but has a simpler object model and fewer low-level facilities. Java applications are typically compiled to bytecode that can run on any Java virtual machine ([JVM](https://en.wikipedia.org/wiki/Java_virtual_machine "wikipedia:Java virtual machine")) regardless of computer architecture.

Arch Linux officially supports the open source [OpenJDK](https://openjdk.java.net/) versions 7, 8, 10, 11, and 13\. All these JVM can be installed without conflict and switched between using helper script `archlinux-java`. Several other Java environments are available in [AUR](/index.php/AUR "AUR") but are not officially supported.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 OpenJDK](#OpenJDK)
    *   [1.2 OpenJFX](#OpenJFX)
    *   [1.3 Other implementations](#Other_implementations)
    *   [1.4 Development tools](#Development_tools)
        *   [1.4.1 Decompilers](#Decompilers)
*   [2 Switching between JVM](#Switching_between_JVM)
    *   [2.1 List compatible Java environments installed](#List_compatible_Java_environments_installed)
    *   [2.2 Change default Java environment](#Change_default_Java_environment)
    *   [2.3 Unsetting the default Java environment](#Unsetting_the_default_Java_environment)
    *   [2.4 Fixing the default Java environment](#Fixing_the_default_Java_environment)
    *   [2.5 Launching an application with the non-default java version](#Launching_an_application_with_the_non-default_java_version)
*   [3 Package pre-requisites to support archlinux-java](#Package_pre-requisites_to_support_archlinux-java)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 MySQL](#MySQL)
    *   [4.2 IntelliJ IDEA](#IntelliJ_IDEA)
    *   [4.3 Impersonate another window manager](#Impersonate_another_window_manager)
    *   [4.4 Illegible fonts](#Illegible_fonts)
    *   [4.5 Missing text in some applications](#Missing_text_in_some_applications)
    *   [4.6 Gray window, applications not resizing with WM, menus immediately closing](#Gray_window,_applications_not_resizing_with_WM,_menus_immediately_closing)
    *   [4.7 System freezes when debugging JavaFX Applications](#System_freezes_when_debugging_JavaFX_Applications)
    *   [4.8 JavaFX's MediaPlayer constructor throws an exception](#JavaFX's_MediaPlayer_constructor_throws_an_exception)
    *   [4.9 Java applications cannot open external links](#Java_applications_cannot_open_external_links)
    *   [4.10 Error initializing QuantumRenderer: no suitable pipeline found](#Error_initializing_QuantumRenderer:_no_suitable_pipeline_found)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Better font rendering](#Better_font_rendering)
    *   [5.2 Silence 'Picked up _JAVA_OPTIONS' message on command line](#Silence_'Picked_up_JAVA_OPTIONS'_message_on_command_line)
    *   [5.3 GTK LookAndFeel](#GTK_LookAndFeel)
        *   [5.3.1 GTK3 Support](#GTK3_Support)
    *   [5.4 Better 2D performance](#Better_2D_performance)
*   [6 See also](#See_also)

## Installation

**Note:**

*   Arch Linux officially only supports the [OpenJDK](#OpenJDK) implementation.
*   After installation, the Java environment will need to be recognized by the shell (`$PATH` variable). This can be done by sourcing `/etc/profile` from the command line or by logging out/in again of a Desktop Environment.

Two *common* packages are respectively pulled as dependency, named [java-runtime-common](https://www.archlinux.org/packages/?name=java-runtime-common) (containing common files for Java Runtime Environments) and [java-environment-common](https://www.archlinux.org/packages/?name=java-environment-common) (containing common files for Java Development Kits). The provided environment file `/etc/profile.d/jre.sh` points to a linked location `/usr/lib/jvm/default/bin`, set by the `archlinux-java` helper script. The links `/usr/lib/jvm/default` and `/usr/lib/jvm/default-runtime` should **always** be edited with `archlinux-java`. This is used to display and point to a working default Java environment in `/usr/lib/jvm/java-${JAVA_MAJOR_VERSION}-${VENDOR_NAME}` or a Java runtime in `/usr/lib/jvm/java-${JAVA_MAJOR_VERSION}-${VENDOR_NAME}/jre`.

Most executables of the Java installation are provided by direct links in `/usr/bin`, while others are available in `$PATH`. The script `/etc/profile.d/jdk.sh` is no longer provided any package.

### OpenJDK

[OpenJDK](https://en.wikipedia.org/wiki/OpenJDK "wikipedia:OpenJDK") is an open-source implementation of the Java Platform, Standard Edition (Java SE).

	Headless JRE

	The minimal Java runtime - needed for executing non-GUI Java programs.

	Full JRE

	Full Java runtime environment - needed for executing Java GUI programs, depends on headless JRE.

	JDK

	[Java Development Kit](https://en.wikipedia.org/wiki/Java_Development_Kit "wikipedia:Java Development Kit") - needed for Java development, depends on full JRE.

| Version | Headless JRE | Full JRE | JDK | Documentation | Sources |
| [OpenJDK 13](https://openjdk.java.net/projects/jdk/13/) | [jre-openjdk-headless](https://www.archlinux.org/packages/?name=jre-openjdk-headless) | [jre-openjdk](https://www.archlinux.org/packages/?name=jre-openjdk) | [jdk-openjdk](https://www.archlinux.org/packages/?name=jdk-openjdk) | [openjdk-doc](https://www.archlinux.org/packages/?name=openjdk-doc) | [openjdk-src](https://www.archlinux.org/packages/?name=openjdk-src) |
| [OpenJDK 11](https://openjdk.java.net/projects/jdk/11/) | [jre11-openjdk-headless](https://www.archlinux.org/packages/?name=jre11-openjdk-headless) | [jre11-openjdk](https://www.archlinux.org/packages/?name=jre11-openjdk) | [jdk11-openjdk](https://www.archlinux.org/packages/?name=jdk11-openjdk) | [openjdk11-doc](https://www.archlinux.org/packages/?name=openjdk11-doc) | [openjdk11-src](https://www.archlinux.org/packages/?name=openjdk11-src) |
| [OpenJDK 10](https://openjdk.java.net/projects/jdk/10/) | [jre10-openjdk-headless](https://www.archlinux.org/packages/?name=jre10-openjdk-headless) | [jre10-openjdk](https://www.archlinux.org/packages/?name=jre10-openjdk) | [jdk10-openjdk](https://www.archlinux.org/packages/?name=jdk10-openjdk) | [openjdk10-doc](https://www.archlinux.org/packages/?name=openjdk10-doc) | [openjdk10-src](https://www.archlinux.org/packages/?name=openjdk10-src) |
| [OpenJDK 8](https://openjdk.java.net/projects/jdk8/) | [jre8-openjdk-headless](https://www.archlinux.org/packages/?name=jre8-openjdk-headless) | [jre8-openjdk](https://www.archlinux.org/packages/?name=jre8-openjdk) | [jdk8-openjdk](https://www.archlinux.org/packages/?name=jdk8-openjdk) | [openjdk8-doc](https://www.archlinux.org/packages/?name=openjdk8-doc) | [openjdk8-src](https://www.archlinux.org/packages/?name=openjdk8-src) |
| [OpenJDK 7](https://openjdk.java.net/projects/jdk7/) | [jre7-openjdk-headless](https://www.archlinux.org/packages/?name=jre7-openjdk-headless) | [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk) | [jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk) | [openjdk7-doc](https://www.archlinux.org/packages/?name=openjdk7-doc) | [openjdk7-src](https://www.archlinux.org/packages/?name=openjdk7-src) |

**OpenJDK GA** — Latest OpenJDK General-Availability Release build from Oracle.

	[https://jdk.java.net](https://jdk.java.net) || [java-openjdk-bin](https://aur.archlinux.org/packages/java-openjdk-bin/)

**OpenJDK EA** — Latest OpenJDK Early-Access build for development version from Oracle.

	[https://jdk.java.net](https://jdk.java.net) || [java-openjdk-ea-bin](https://aur.archlinux.org/packages/java-openjdk-ea-bin/)

**IcedTea-Web** — Java Web Start and the deprecated Java browser plugin.

	[https://icedtea.classpath.org/wiki/IcedTea-Web](https://icedtea.classpath.org/wiki/IcedTea-Web) || [icedtea-web](https://www.archlinux.org/packages/?name=icedtea-web)

### OpenJFX

[OpenJFX](https://wiki.openjdk.java.net/display/OpenJFX/Main) is the open-source implementation of [JavaFX](https://en.wikipedia.org/wiki/JavaFX "wikipedia:JavaFX"). You [do not need](https://wiki.openjdk.java.net/display/OpenJFX/Repositories+and+Releases) to install this package if you are making use of Java SE (the Oracle's implementation of JRE and JDK described below). This package only concerns users of the open source implementation of Java (OpenJDK project).

| Version | Runtime and Developement | Documentation | Sources |
| [OpenJFX 13](https://wiki.openjdk.java.net/display/OpenJFX/Main) | [java-openjfx](https://www.archlinux.org/packages/?name=java-openjfx) | [java-openjfx-doc](https://www.archlinux.org/packages/?name=java-openjfx-doc) | [java-openjfx-src](https://www.archlinux.org/packages/?name=java-openjfx-src) |
| [OpenJFX 11](https://wiki.openjdk.java.net/display/OpenJFX/Main) | [java11-openjfx](https://www.archlinux.org/packages/?name=java11-openjfx) | [java11-openjfx-doc](https://www.archlinux.org/packages/?name=java11-openjfx-doc) | [java11-openjfx-src](https://www.archlinux.org/packages/?name=java11-openjfx-src) |
| [OpenJFX 8](https://wiki.openjdk.java.net/display/OpenJFX/Main) | [java8-openjfx](https://www.archlinux.org/packages/?name=java8-openjfx) | [java8-openjfx-doc](https://www.archlinux.org/packages/?name=java8-openjfx-doc) | [java8-openjfx-src](https://www.archlinux.org/packages/?name=java8-openjfx-src) |

**OpenJFX GA** — Latest OpenJFX General-Availability Release build from Gluon.

	[https://openjfx.io/](https://openjfx.io/) || [java-openjfx-bin](https://aur.archlinux.org/packages/java-openjfx-bin/)

**OpenJFX EA** — Latest OpenJFX Early-Access build for development version from Gluon.

	[https://openjfx.io/](https://openjfx.io/) || [java-openjfx-ea-bin](https://aur.archlinux.org/packages/java-openjfx-ea-bin/)

### Other implementations

**Java SE** — Oracle's implementation of JRE and JDK.

	[https://www.oracle.com/technetwork/java/javase/downloads/index.html](https://www.oracle.com/technetwork/java/javase/downloads/index.html) || [jre](https://aur.archlinux.org/packages/jre/) [jre9](https://aur.archlinux.org/packages/jre9/) [jre8](https://aur.archlinux.org/packages/jre8/) [jre7](https://aur.archlinux.org/packages/jre7/) [jre6](https://aur.archlinux.org/packages/jre6/) [jdk](https://aur.archlinux.org/packages/jdk/) [jdk9](https://aur.archlinux.org/packages/jdk9/) [jdk8](https://aur.archlinux.org/packages/jdk8/) [jdk7](https://aur.archlinux.org/packages/jdk7/) [jdk6](https://aur.archlinux.org/packages/jdk6/) [jdk5](https://aur.archlinux.org/packages/jdk5/) [jdk-devel](https://aur.archlinux.org/packages/jdk-devel/)

**OpenJ9** — Eclipse's implementation of JRE, contributed by IBM.

	[https://www.eclipse.org/openj9/](https://www.eclipse.org/openj9/) || [jdk-openj9-bin](https://aur.archlinux.org/packages/jdk-openj9-bin/) [jdk13-openj9-bin](https://aur.archlinux.org/packages/jdk13-openj9-bin/) [jdk12-openj9-bin](https://aur.archlinux.org/packages/jdk12-openj9-bin/) [jdk11-openj9-bin](https://aur.archlinux.org/packages/jdk11-openj9-bin/) [jdk10-openjdk-openj9-bin](https://aur.archlinux.org/packages/jdk10-openjdk-openj9-bin/) [jdk9-openj9-bin](https://aur.archlinux.org/packages/jdk9-openj9-bin/) [jdk8-openj9-bin](https://aur.archlinux.org/packages/jdk8-openj9-bin/)

**IBM J9** — IBM's implementation of the eighth edition of JRE.

	[https://developer.ibm.com/javasdk/](https://developer.ibm.com/javasdk/) || [jdk8-j9-bin](https://aur.archlinux.org/packages/jdk8-j9-bin/) [jdk7-j9-bin](https://aur.archlinux.org/packages/jdk7-j9-bin/) [jdk7r1-j9-bin](https://aur.archlinux.org/packages/jdk7r1-j9-bin/)

**Parrot VM** — a VM with experimental support for Java [[1]](http://trac.parrot.org/parrot/wiki/Languages) through two different methods: either as a [Java VM bytecode translator](https://code.google.com/p/parrot-jvm/), or as a [Java compiler targeting the Parrot VM](https://github.com/chrisdolan/perk).

	[http://www.parrot.org/](http://www.parrot.org/) || [parrot](https://aur.archlinux.org/packages/parrot/)

**Note:** 32-bit versions of Java SE can be found by prefixing `bin32-`, e.g. [bin32-jre](https://aur.archlinux.org/packages/bin32-jre/) and [bin32-jdk](https://aur.archlinux.org/packages/bin32-jdk/). They use [java32-runtime-common](https://aur.archlinux.org/packages/java32-runtime-common/), which functions as [java-runtime-common](https://www.archlinux.org/packages/?name=java-runtime-common) by suffixing with `32`, e.g. `java32`. The same analogy applies to [java32-environment-common](https://aur.archlinux.org/packages/java32-environment-common/), which is only used by 32-bit JDK packages.

### Development tools

For integrated development environments, see [List of applications#Integrated development environments](/index.php/List_of_applications#Integrated_development_environments "List of applications") and the *Java IDEs* subsection specifically.

To discourage reverse engineering an obfuscator like [proguard](https://aur.archlinux.org/packages/proguard/) can be used.

#### Decompilers

*   **Bytecode Viewer** — Java reverse engineering suite, including a decompiler, editor and debugger.

	[https://bytecodeviewer.com](https://bytecodeviewer.com) || [bytecode-viewer](https://aur.archlinux.org/packages/bytecode-viewer/)

*   **CFR** — Java decompiler, supporting modern features of Java 9, 10 and beyond.

	[https://www.benf.org/other/cfr/](https://www.benf.org/other/cfr/) || [cfr](https://aur.archlinux.org/packages/cfr/)

*   **Fernflower** — Analytical decompiler for Java, developed as part of [IntelliJ IDEA](/index.php/IntelliJ_IDEA "IntelliJ IDEA").

	[https://github.com/JetBrains/intellij-community/tree/master/plugins/java-decompiler/engine](https://github.com/JetBrains/intellij-community/tree/master/plugins/java-decompiler/engine) || [fernflower-git](https://aur.archlinux.org/packages/fernflower-git/)

*   **[JAD](https://en.wikipedia.org/wiki/JAD_(software) "wikipedia:JAD (software)")** — Unmaintained Java decompiler.

	[https://varaneckas.com/jad](https://varaneckas.com/jad) || [jad](https://www.archlinux.org/packages/?name=jad)

*   **JD-Core-java** — Thin-wrapper for the [Java Decompiler](https://en.wikipedia.org/wiki/Java_Decompiler "wikipedia:Java Decompiler").

	[https://github.com/nviennot/jd-core-java](https://github.com/nviennot/jd-core-java) || [jd-core-java](https://aur.archlinux.org/packages/jd-core-java/)

*   **Krakatau** — Java decompiler, assembler, and disassembler.

	[https://github.com/Storyyeller/Krakatau](https://github.com/Storyyeller/Krakatau) || [krakatau-git](https://aur.archlinux.org/packages/krakatau-git/)

*   **Procyon decompiler** — Experimental Java decompiler, inspired by ILSpy and Mono.Cecil.

	[https://bitbucket.org/mstrobel/procyon/wiki/Java%20Decompiler](https://bitbucket.org/mstrobel/procyon/wiki/Java%20Decompiler) || [procyon-decompiler](https://aur.archlinux.org/packages/procyon-decompiler/), GUI: [luyten](https://aur.archlinux.org/packages/luyten/)

## Switching between JVM

The helper script `archlinux-java` provides such functionalities:

```
archlinux-java <COMMAND>

COMMAND:
	status		List installed Java environments and enabled one
	get		Return the short name of the Java environment set as default
	set <JAVA_ENV>	Force <JAVA_ENV> as default
	unset		Unset current default Java environment
	fix		Fix an invalid/broken default Java environment configuration

```

### List compatible Java environments installed

```
$ archlinux-java status

```

Example:

```
$ archlinux-java status
Available Java environments:
  java-7-openjdk (default)
  java-8-openjdk/jre

```

Note the *(default)* denoting that `java-7-openjdk` is currently set as default. Invocation of `java` and other binaries will rely on this Java install. Also note on the previous output that only the *JRE* part of OpenJDK 8 is installed here.

### Change default Java environment

```
# archlinux-java set <JAVA_ENV_NAME>

```

Example:

```
# archlinux-java set java-8-openjdk/jre

```

**Tip:** To see possible `<JAVA_ENV_NAME>` names, use `archlinux-java status`.

Note that `archlinux-java` will not let you set an invalid Java environment. In the previous example, [jre8-openjdk](https://www.archlinux.org/packages/?name=jre8-openjdk) is installed but [jdk8-openjdk](https://www.archlinux.org/packages/?name=jdk8-openjdk) is **not** so trying to set `java-8-openjdk` will fail:

```
# archlinux-java set java-8-openjdk
'/usr/lib/jvm/java-8-openjdk' is not a valid Java environment path

```

### Unsetting the default Java environment

There should be no need to unset a Java environment as packages providing them should take care of this. Still should you want to do so, just use command `unset`:

```
# archlinux-java unset

```

### Fixing the default Java environment

If an invalid Java environment link is set, calling the `archlinux-java fix` command tries to fix it. Also note that if no default Java environment is set, this will look for valid ones and try to set it for you. Officially supported package "OpenJDK 8" will be considered first in this order, then other installed environments.

```
# archlinux-java fix

```

### Launching an application with the non-default java version

If you want to launch an application with another version of java than the default one (for example if you have both version jre7 and jre8 installed on your system), you can wrap your application in a small bash script to locally change the default PATH of java. For example if the default version is jre7 and you want to use jre8:

```
#!/bin/sh

export PATH="/usr/lib/jvm/java-8-openjdk/jre/bin/:$PATH"
exec /path/to/application "$@"

```

## Package pre-requisites to support `archlinux-java`

**Note:** This info also applies to `archlinux32-java` for 32-bit Java packages, with the proper inclusion of `32` to the package/executable names, where applicable.

This section is targeted at packager willing to provide packages in [AUR](/index.php/AUR "AUR") for an alternate JVM and be able to integrate with Arch Linux JVM scheme to use `archlinux-java`. To do so, packages should:

*   Place all files under `/usr/lib/jvm/java-${JAVA_MAJOR_VERSION}-${VENDOR_NAME}`
*   Ensure all executables for which [java-runtime-common](https://www.archlinux.org/packages/extra/any/java-runtime-common/files/) and [java-environment-common](https://www.archlinux.org/packages/extra/any/java-environment-common/files/) provide links are available in the corresponding package
*   Ship links from `/usr/bin` to executables, only if these links do not already belong to [java-runtime-common](https://www.archlinux.org/packages/extra/any/java-runtime-common/files/) and [java-environment-common](https://www.archlinux.org/packages/extra/any/java-environment-common/files/)
*   Suffix man pages with `-${VENDOR_NAME}${JAVA_MAJOR_VERSION}` to prevent conflicts (see [jre8-openjdk file list](https://www.archlinux.org/packages/extra/x86_64/jre8-openjdk/files/) where man pages are suffixed with `-openjdk8`)
*   Do not declare any [conflicts](/index.php/PKGBUILD#conflicts "PKGBUILD") nor [replaces](/index.php/PKGBUILD#replaces "PKGBUILD") with other JDKs, `java-runtime`, `java-runtime-headless` nor `java-environment`
*   Use script `archlinux-java` in *install functions* to set the Java environment as default **if no other valid Java environment is already set** (ie: package should not **force** install as default). See [officially supported Java environment package sources](https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/java7-openjdk) for examples

Also please note that:

*   Packages that need **any** Java environment should declare dependency on `java-runtime`, `java-runtime-headless` or `java-environment` as usual
*   Packages that need a **specific Java vendor** should declare dependency on the corresponding package
*   OpenJDK packages now declare `provides="java-runtime-openjdk=${pkgver}"` etc. This enables a third-party package to declare dependency on an OpenJDK without specifying a version

## Troubleshooting

### MySQL

Due to the fact that the JDBC-drivers often use the port in the URL to establish a connection to the database, it is considered "remote" (i.e., MySQL does not listen to the port as per its default settings) despite the fact that they are possibly running on the same host, Thus, to use JDBC and MySQL you should enable remote access to MySQL, following the instructions in [MariaDB#Grant remote access](/index.php/MariaDB#Grant_remote_access "MariaDB").

### IntelliJ IDEA

If IntelliJ IDEA outputs `The selected directory is not a valid home for JDK` with the system Java SDK path, you may have to install a different JDK package and select it as IDEA's JDK.

### Impersonate another window manager

You may use the [wmname](https://www.archlinux.org/packages/?name=wmname) from [suckless.org](https://tools.suckless.org/x/wmname) to make the JVM believe you are running a different window manager. This may solve a rendering issue of Java GUIs occurring in window managers like [Awesome](/index.php/Awesome "Awesome") or [Dwm](/index.php/Dwm "Dwm") or [Ratpoison](/index.php/Ratpoison "Ratpoison"). Try set "compiz" or "LG3D"

```
$ wmname compiz

```

You must restart the application in question after issuing the wmname command.

This works because the JVM contains a hard-coded list of known, non-re-parenting window managers. For maximum irony, some users prefer to impersonate `LG3D`, the non-re-parenting window manager [written by Sun, in Java](https://en.wikipedia.org/wiki/Project_Looking_Glass "wikipedia:Project Looking Glass").

### Illegible fonts

In addition to the suggestions mentioned below in [#Better font rendering](#Better_font_rendering), some fonts may still not be legible afterwards. If this is the case, there is a good chance Microsoft fonts are being used. Install [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/).

### Missing text in some applications

If some applications are completely missing texts it may help to use the options under [#Tips and tricks](#Tips_and_tricks) as suggested in [FS#40871](https://bugs.archlinux.org/task/40871).

### Gray window, applications not resizing with WM, menus immediately closing

The standard Java GUI toolkit has a hard-coded list of "non-reparenting" window managers. If using one that is not on that list, there can be some problems with running some Java applications. One of the most common problems is "gray blobs", when the Java application renders as a plain gray box instead of rendering the GUI. Another one might be menus responding to your click, but closing immediately.

There are several things that may help:

*   For [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk) or [jre8-openjdk](https://www.archlinux.org/packages/?name=jre8-openjdk), append the line `export _JAVA_AWT_WM_NONREPARENTING=1` in `/etc/profile.d/jre.sh`. Then, source the file `/etc/profile.d/jre.sh` or log out and log back in.
*   For last version of JDK append line `export AWT_TOOLKIT=MToolkit` in `~/.xinitrc` before exec window manager.
*   Also, we can try to use [wmname](https://www.archlinux.org/packages/?name=wmname) with line `wmname compiz` in your `~/.xinitrc`.
*   For Oracle's JRE/JDK, use [SetWMName.](https://wiki.haskell.org/Xmonad/Frequently_asked_questions#Using_SetWMName) However, its effect may be canceled when also using `XMonad.Hooks.EwmhDesktops`. In this case, appending `>> setWMName "LG3D"` to the `LogHook` may help.

See [[2]](https://wiki.haskell.org/Xmonad/Frequently_asked_questions#Problems_with_Java_applications.2C_Applet_java_console) for more information.

### System freezes when debugging JavaFX Applications

If your system freezes while debugging a JavaFX Application, you can try to supply the JVM option `-Dsun.awt.disablegrab=true`.

See [https://bugs.java.com/view_bug.do?bug_id=6714678](https://bugs.java.com/view_bug.do?bug_id=6714678)

### JavaFX's MediaPlayer constructor throws an exception

Creating instance of MediaPlayer class from JavaFX's sound modules might throw following exception (both Oracle JDK and OpenJDK)

```
... (i.e. FXMLLoader construction exceptions) ...
Caused by: MediaException: UNKNOWN : com.sun.media.jfxmedia.MediaException: Could not create player! : com.sun.media.jfxmedia.MediaException: Could not create player!
 at javafx.scene.media.MediaException.exceptionToMediaException(MediaException.java:146)
 at javafx.scene.media.MediaPlayer.init(MediaPlayer.java:511)
 at javafx.scene.media.MediaPlayer.<init>(MediaPlayer.java:414)
 at <constructor call>
...

```

which is a result of some incompatibilities of JavaFX with modern [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg) build delivered within Arch Linux repository.

Working solution is to install [ffmpeg-compat-55](https://aur.archlinux.org/packages/ffmpeg-compat-55/).

See [https://www.reddit.com/r/archlinux/comments/70o8o6/using_a_javafx_mediaplayer_in_arch/](https://www.reddit.com/r/archlinux/comments/70o8o6/using_a_javafx_mediaplayer_in_arch/)

### Java applications cannot open external links

If a Java application is not able to open a link to, for example, your web browser, install [gvfs](https://www.archlinux.org/packages/?name=gvfs). This is required by the Desktop.Action.BROWSE method. See [[3]](https://bugs.launchpad.net/ubuntu/+source/openjdk-8/+bug/1574879/comments/2)

### Error initializing QuantumRenderer: no suitable pipeline found

Possible issues / solutions:

*   GTK2 is missing. Install [gtk2](https://www.archlinux.org/packages/?name=gtk2)
*   OpenJFX is missing. Install [java-openjfx](https://www.archlinux.org/packages/?name=java-openjfx)

## Tips and tricks

**Note:** Suggestions in this section are applicable to all applications, using explicitly installed (external) Java runtime. Some applications are bundled with own (private) runtime or use own mechanics for GUI, font rendering, etc., so none of written below is guaranteed to work.

Behavior of most Java applications can be controlled by supplying predefined variables to Java runtime. From [this forum post](https://bbs.archlinux.org/viewtopic.php?id=72892), a way to do it consists of adding the following line in your `~/.bashrc` (or `/etc/profile.d/jre.sh` to affect programs that are not run by sourcing `~/.bashrc`, e.g., launching a program from Gnome's Applications view):

```
export _JAVA_OPTIONS="-D**<option 1>** -D**<option 2>**..."

```

For example, to use system anti-aliased fonts and make swing use the GTK look and feel:

```
export _JAVA_OPTIONS='-Dawt.useSystemAAFontSettings=on -Dswing.aatext=true -Dswing.defaultlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel'

```

### Better font rendering

Both closed source and open source implementations of Java are known to have improperly implemented anti-aliasing of fonts. This can be fixed with the following options: `-Dawt.useSystemAAFontSettings=on`, `-Dswing.aatext=true`

See [Java Runtime Environment fonts](/index.php/Java_Runtime_Environment_fonts "Java Runtime Environment fonts") for more detailed information.

### Silence 'Picked up _JAVA_OPTIONS' message on command line

Setting the _JAVA_OPTIONS environment variables makes java (openjdk) write to stderr messages of the form: 'Picked up _JAVA_OPTIONS=...'. To suppress those messages in your terminal you can unset the environment variable in your shell startup files and alias java to pass those same options as command line arguments:

```
_SILENT_JAVA_OPTIONS="$_JAVA_OPTIONS"
unset _JAVA_OPTIONS
alias java='java "$_SILENT_JAVA_OPTIONS"'

```

### GTK LookAndFeel

If your Java programs look ugly, you may want to set up the default look and feel for the swing components:

`swing.defaultlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel`.

Some Java programs insist on using the cross platform Metal look and feel. In some of these cases you can force these apps to use the GTK look and feel by setting the following property:

`swing.crossplatformlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel`.

#### GTK3 Support

In Java releases prior to version 9, the GTK LookAndFeel is linked against GTK2, whilst many newer desktop applications use GTK3\. This incompatibility between GTK versions may break applications utilizing Java plugins with GUI, as the mixing of GTK2 and GTK3 in the same process is not supported (for example, LibreOffice 5.0).

Since [Java 9](https://openjdk.java.net/jeps/283), the GTK LookAndFeel can be run against GTK versions `2`, `2.2` and `3`, defaulting to GTK2\. This can be overridden by setting the following property:

`jdk.gtk.version=3`

### Better 2D performance

Switching to OpenGL-based hardware acceleration pipeline will improve 2D performance

```
export _JAVA_OPTIONS='-Dsun.java2d.opengl=true'

```

**Note:** Enabling this option may cause the UI of software like JetBrains IDEs misbehave, making them drawing windows, popups and toolbars partially.

## See also

*   [Introduction to Programming Using Java](https://math.hws.edu/javanotes8/)