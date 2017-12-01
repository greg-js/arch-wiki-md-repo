Related articles

*   [Java Package Guidelines](/index.php/Java_Package_Guidelines "Java Package Guidelines")
*   [Java Runtime Environment Fonts](/index.php/Java_Runtime_Environment_Fonts "Java Runtime Environment Fonts")

From the [Wikipedia article](https://en.wikipedia.org/wiki/Java_(programming_language) "wikipedia:Java (programming language)"):

	Java is a programming language originally developed by Sun Microsystems and released in 1995 as a core component of Sun Microsystems' Java platform. The language derives much of its syntax from C and C++ but has a simpler object model and fewer low-level facilities. Java applications are typically compiled to bytecode that can run on any Java virtual machine ([JVM](https://en.wikipedia.org/wiki/Java_virtual_machine "wikipedia:Java virtual machine")) regardless of computer architecture.

Arch Linux officially supports the open source [OpenJDK](http://openjdk.java.net/) versions 7, 8, and 9\. All these JVM can be installed without conflict and switched between using helper script `archlinux-java`. Several other Java environments are available in [AUR](/index.php/AUR "AUR") but are not officially supported.

## Contents

*   [1 Installation](#Installation)
*   [2 Flagging packages as out-of-date](#Flagging_packages_as_out-of-date)
*   [3 Switching between JVM](#Switching_between_JVM)
    *   [3.1 List compatible Java environments installed](#List_compatible_Java_environments_installed)
    *   [3.2 Change default Java environment](#Change_default_Java_environment)
    *   [3.3 Unsetting the default Java environment](#Unsetting_the_default_Java_environment)
    *   [3.4 Fixing the default Java environment](#Fixing_the_default_Java_environment)
    *   [3.5 Launching an application with the non-default java version](#Launching_an_application_with_the_non-default_java_version)
*   [4 Package pre-requisites to support archlinux-java](#Package_pre-requisites_to_support_archlinux-java)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 MySQL](#MySQL)
    *   [5.2 Impersonate another window manager](#Impersonate_another_window_manager)
    *   [5.3 Illegible fonts](#Illegible_fonts)
    *   [5.4 Missing text in some applications](#Missing_text_in_some_applications)
    *   [5.5 Applications not resizing with WM, menus immediately closing](#Applications_not_resizing_with_WM.2C_menus_immediately_closing)
    *   [5.6 System freezes when debugging JavaFX Applications](#System_freezes_when_debugging_JavaFX_Applications)
*   [6 Tips and tricks](#Tips_and_tricks)
    *   [6.1 Better font rendering](#Better_font_rendering)
    *   [6.2 Silence 'Picked up _JAVA_OPTIONS' message on command line](#Silence_.27Picked_up_JAVA_OPTIONS.27_message_on_command_line)
    *   [6.3 GTK LookAndFeel](#GTK_LookAndFeel)
    *   [6.4 Better 2D performance](#Better_2D_performance)
    *   [6.5 Non-reparenting window managers / Grey window / Programs not drawing properly](#Non-reparenting_window_managers_.2F_Grey_window_.2F_Programs_not_drawing_properly)
*   [7 See also](#See_also)

## Installation

**Note:**

*   Installing a JDK will automatically pull its JRE dependency.
*   After installation, the Java environment will need to be recognized by the shell (`$PATH` variable). This can be done by sourcing `/etc/profile` from the command line or by logging out/in again of a Desktop Environment.

Two *common* packages are respectively pulled as dependency, named [java-runtime-common](https://www.archlinux.org/packages/?name=java-runtime-common) (containing common files for Java Runtime Environments) and [java-environment-common](https://www.archlinux.org/packages/?name=java-environment-common) (containing common files for Java Development Kits). The provided environment file `/etc/profile.d/jre.sh` points to a linked location `/usr/lib/jvm/default/bin`, set by the `archlinux-java` helper script. The links `/usr/lib/jvm/default` and `/usr/lib/jvm/default-runtime` should **always** be edited with `archlinux-java`. This is used to display and point to a working default Java environment in `/usr/lib/jvm/java-${JAVA_MAJOR_VERSION}-${VENDOR_NAME}` or a Java runtime in `/usr/lib/jvm/java-${JAVA_MAJOR_VERSION}-${VENDOR_NAME}/jre`.

Most executables of the Java installation are provided by direct links in `/usr/bin`, while others are available in `$PATH`.

**Warning:** File `/etc/profile.d/jdk.sh` is not provided any more by any package.

The following packages are available:

**OpenJDK 7** — The open-source implementation of the seventh edition of Java SE.

	[http://openjdk.java.net/projects/jdk7/](http://openjdk.java.net/projects/jdk7/) || [jre7-openjdk-headless](https://www.archlinux.org/packages/?name=jre7-openjdk-headless) [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk) [jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk) [openjdk7-doc](https://www.archlinux.org/packages/?name=openjdk7-doc) [openjdk7-src](https://www.archlinux.org/packages/?name=openjdk7-src)

**OpenJDK 8** — The open-source implementation of the eight edition of Java SE.

	[http://openjdk.java.net/projects/jdk8/](http://openjdk.java.net/projects/jdk8/) || [jre8-openjdk-headless](https://www.archlinux.org/packages/?name=jre8-openjdk-headless) [jre8-openjdk](https://www.archlinux.org/packages/?name=jre8-openjdk) [jdk8-openjdk](https://www.archlinux.org/packages/?name=jdk8-openjdk) [openjdk8-doc](https://www.archlinux.org/packages/?name=openjdk8-doc) [openjdk8-src](https://www.archlinux.org/packages/?name=openjdk8-src)

**OpenJFX 8** — The open-source implementation of JavaFX. You [do not need](https://wiki.openjdk.java.net/display/OpenJFX/Repositories+and+Releases) to install this package if you are making use of Java SE (the Oracle's implementation of JRE and JDK described below). This package only concerns users of the open source implementation of Java (OpenJDK project).

	[http://openjdk.java.net/projects/openjfx/](http://openjdk.java.net/projects/openjfx/) || [java-openjfx](https://www.archlinux.org/packages/?name=java-openjfx) [java-openjfx-doc](https://www.archlinux.org/packages/?name=java-openjfx-doc) [java-openjfx-src](https://www.archlinux.org/packages/?name=java-openjfx-src)

**OpenJDK 9** — The open-source implementation of the ninth edition of Java SE.

	[http://openjdk.java.net/projects/jdk9/](http://openjdk.java.net/projects/jdk9/) || [jre9-openjdk-headless](https://www.archlinux.org/packages/?name=jre9-openjdk-headless) [jre9-openjdk](https://www.archlinux.org/packages/?name=jre9-openjdk) [jdk9-openjdk](https://www.archlinux.org/packages/?name=jdk9-openjdk) [openjdk9-doc](https://www.archlinux.org/packages/?name=openjdk9-doc) [openjdk9-src](https://www.archlinux.org/packages/?name=openjdk9-src)

**OpenJ9** — Formerly IBM, now Eclipse's implementation of JRE.

	[https://www.eclipse.org/openj9/](https://www.eclipse.org/openj9/) || [jdk8-j9-bin](https://aur.archlinux.org/packages/jdk8-j9-bin/) [jdk8-openj9-bin](https://aur.archlinux.org/packages/jdk8-openj9-bin/) [jdk9-openj9-bin](https://aur.archlinux.org/packages/jdk9-openj9-bin/)

**Java SE** — Oracle's implementation of JRE and JDK.

	[http://www.oracle.com/technetwork/java/javase/downloads/index.html](http://www.oracle.com/technetwork/java/javase/downloads/index.html) || [jre](https://aur.archlinux.org/packages/jre/) [jre6](https://aur.archlinux.org/packages/jre6/) [jre7](https://aur.archlinux.org/packages/jre7/) [jre8](https://aur.archlinux.org/packages/jre8/) [jre-devel](https://aur.archlinux.org/packages/jre-devel/) [jdk](https://aur.archlinux.org/packages/jdk/) [jdk5](https://aur.archlinux.org/packages/jdk5/) [jdk6](https://aur.archlinux.org/packages/jdk6/) [jdk7](https://aur.archlinux.org/packages/jdk7/) [jdk8](https://aur.archlinux.org/packages/jdk8/) [jdk-devel](https://aur.archlinux.org/packages/jdk-devel/)

**Parrot VM** — a VM with experimental support for Java [[1]](http://trac.parrot.org/parrot/wiki/Languages) through two different methods: either as a [Java VM bytecode translator](http://code.google.com/p/parrot-jvm/), or as a [Java compiler targeting the Parrot VM](https://github.com/chrisdolan/perk).

	[http://www.parrot.org/](http://www.parrot.org/) || [parrot](https://www.archlinux.org/packages/?name=parrot)

**Note:** 32-bit versions of Java SE can be found by prefixing `bin32-`, e.g. [bin32-jre](https://aur.archlinux.org/packages/bin32-jre/) and [bin32-jdk](https://aur.archlinux.org/packages/bin32-jdk/). They use [java32-runtime-common](https://aur.archlinux.org/packages/java32-runtime-common/), which functions as [java-runtime-common](https://www.archlinux.org/packages/?name=java-runtime-common) by suffixing with `32`, e.g. `java32`.

## Flagging packages as out-of-date

Although the Arch Linux package releases may contain a reference to the proprietary versions the packages are based on, the open-source project has its own versioning scheme:

*   [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk), [jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk), and [jre7-openjdk-headless](https://www.archlinux.org/packages/?name=jre7-openjdk-headless) should be flagged as out-of-date based on the [*IcedTea* version](http://icedtea.wildebeest.org/download/source) (e.g. `2.4.3`), rather than on the Oracle reference version (e.g. `u45` in the release `7.u45_2.4.3-1`).
*   [icedtea-web](https://www.archlinux.org/packages/?name=icedtea-web) should be flagged as out-of-date based on the [*IcedTea Web* version](http://icedtea.wildebeest.org/download/source) (e.g. `1.4.1`). This is independent of the *IcedTea* version.

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

If an invalid Java environment link is set, calling the `archlinux-java fix` command tries to fix these. Also note that if no default Java environment is set, this will look for valid ones and try to set it for you. Officially supported packages "OpenJDK 7" and "OpenJDK 8" will be considered first in this order, then un-official packages from [AUR](/index.php/AUR "AUR").

```
# archlinux-java fix

```

### Launching an application with the non-default java version

If you want to launch an application with another version of java than the default one (for example if you have both version jre7 and jre8 installed on your system), you can wrap your application in a small bash script to locally change the default PATH of java. For example if the default version is jre7 and you want use jre8:

```
#!/bin/sh 

export PATH=/usr/lib/jvm/java-8-openjdk/jre/bin/:$PATH
exec /path/to/application "$@"

```

## Package pre-requisites to support `archlinux-java`

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

Due to the fact that the JDBC-drivers often use the port in the URL to establish a connection to the database, it is considered "remote" (i.e., MySQL does not listen to the port as per its default settings) despite the fact that they are possibly running on the same host, Thus, to use JDBC and MySQL you should enable remote access to MySQL, following the instructions in [MySQL#Grant remote access](/index.php/MySQL#Grant_remote_access "MySQL").

### Impersonate another window manager

You may use the [wmname](https://www.archlinux.org/packages/?name=wmname) from [suckless.org](http://tools.suckless.org/x/wmname) to make the JVM believe you are running a different window manager. This may solve a rendering issue of Java GUIs occurring in window managers like [Awesome](/index.php/Awesome "Awesome") or [Dwm](/index.php/Dwm "Dwm") or [Ratpoison](/index.php/Ratpoison "Ratpoison").

```
$ wmname LG3D

```

You must restart the application in question after issuing the wmname command.

This works because the JVM contains a hard-coded list of known, non-re-parenting window managers. For maximum irony, some users prefer to impersonate `LG3D`, the non-re-parenting window manager [written by Sun, in Java](https://en.wikipedia.org/wiki/Project_Looking_Glass "wikipedia:Project Looking Glass").

### Illegible fonts

In addition to the suggestions mentioned below in [#Better font rendering](#Better_font_rendering), some fonts may still not be legible afterwards. If this is the case, there is a good chance Microsoft fonts are being used. Install [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) from the [AUR](/index.php/AUR "AUR").

### Missing text in some applications

If some applications are completely missing texts it may help to use the options under [#Tips and tricks](#Tips_and_tricks) as suggested in [FS#40871](https://bugs.archlinux.org/task/40871).

### Applications not resizing with WM, menus immediately closing

The standard Java GUI toolkit has a hard-coded list of "non-reparenting" window managers. If using one that is not on that list, there can be some problems with running some Java applications. One of the most common problems is "gray blobs", when the Java application renders as a plain gray box instead of rendering the GUI. Another one might be menus responding to your click, but closing immediately.

There are several things that may help:

*   For [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk) or [jre8-openjdk](https://www.archlinux.org/packages/?name=jre8-openjdk), append the line `export _JAVA_AWT_WM_NONREPARENTING=1` in `/etc/profile.d/jre.sh`. Then, source the file `/etc/profile.d/jre.sh` or log out and log back in.
*   For Oracle's JRE/JDK, use [SetWMName.](https://wiki.haskell.org/Xmonad/Frequently_asked_questions#Using_SetWMName) However, its effect may be canceled when also using `XMonad.Hooks.EwmhDesktops`. In this case, appending

```
>> setWMName "LG3D"

```

to the `LogHook` may help.

See [[2]](http://wiki.haskell.org/Xmonad/Frequently_asked_questions#Problems_with_Java_applications.2C_Applet_java_console) for more information.

### System freezes when debugging JavaFX Applications

If your system freezes while debugging a JavaFX Application, you can try to supply the JVM option `-Dsun.awt.disablegrab=true`.

See [http://bugs.java.com/view_bug.do?bug_id=6714678](http://bugs.java.com/view_bug.do?bug_id=6714678)

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

Setting the _JAVA_OPTIONS environment variables makes java (openjdk) write to stderr messages of the form: 'Picked up _JAVA_OPTIONS=...'. To supress those mesages in your terminal you can unset the environment variable in your shell startup files and alias java to pass those same options as command line arguments:

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

**Note:** Forcing Java to use GTK may break some applications. The JRE/JDK is linked against GTK2 while many desktop applications use GTK3\. If a GTK3 app has Java plugins with GUI, the app is likely to crash when opening the Java GUI, as mixing GTK2 and GTK3 in the same process is not supported. Libreoffice 5.0 is an example of this.

### Better 2D performance

Switching to OpenGL-based hardware acceleration pipeline will improve 2D performance

```
export _JAVA_OPTIONS='-Dsun.java2d.opengl=true'

```

### Non-reparenting window managers / Grey window / Programs not drawing properly

Non-reparenting window managers user should set the following environment variable in their `.xinitrc`

```
export _JAVA_AWT_WM_NONREPARENTING=1

```

Not setting this may result in java programs not being drawn properly.

## See also

*   [Introduction to Programming Using Java](http://math.hws.edu/javanotes/)