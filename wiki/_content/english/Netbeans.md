**Netbeans** is an integrated development environment (IDE) for developing with Java, JavaScript, PHP, Python, Ruby, Groovy, C, C++, Scala, Clojure, and other languages.

From [Wikipedia article](https://en.wikipedia.org/wiki/Netbeans "wikipedia:Netbeans"):

	"*The NetBeans IDE is written in Java and can run anywhere a compatible JVM is installed, including Windows, Mac OS, Linux, and Solaris. A JDK is required for Java development functionality, but is not required for development in other programming languages.*"

## Contents

*   [1 Installation](#Installation)
*   [2 Tips and tricks](#Tips_and_tricks)
    *   [2.1 Font antialiasing in Netbeans](#Font_antialiasing_in_Netbeans)
        *   [2.1.1 Netbeans Specifically](#Netbeans_Specifically)
        *   [2.1.2 Java Generally](#Java_Generally)
    *   [2.2 Look and feel](#Look_and_feel)
    *   [2.3 Maven problems with small tmpfs](#Maven_problems_with_small_tmpfs)
*   [3 Integrate with tomcat](#Integrate_with_tomcat)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 OpenJDK vs Sun's JDK](#OpenJDK_vs_Sun.27s_JDK)
    *   [4.2 Glassfish server - Can`t download Glassfish server I/O Exception](#Glassfish_server_-_Can.60t_download_Glassfish_server_I.2FO_Exception)
    *   [4.3 Integrate Netbeans with kwallet](#Integrate_Netbeans_with_kwallet)

## Installation

[Install](/index.php/Install "Install") the [netbeans](https://www.archlinux.org/packages/?name=netbeans) package.

## Tips and tricks

**Note:** The global netbeans.conf `/usr/share/netbeans/etc/netbeans.conf` will be overwritten during updates. To keep changes add them to your local netbeans.conf `~/.netbeans/<ver>/etc/netbeans.conf` (you will need to create the etc dir and the .conf file).

*   Settings in local version of netbeans.conf override the same settings in the global copy of the file.
*   Command-line options override settings in either of the configuration files.

### Font antialiasing in Netbeans

#### Netbeans Specifically

Add `-J-Dswing.aatext=TRUE -J-Dawt.useSystemAAFontSettings=on` to the 'netbeans_default_options' line of your netbeans.conf file.

#### Java Generally

See [Java#Better font rendering](/index.php/Java#Better_font_rendering "Java").

### Look and feel

To change Netbeans look and feel, go to Tools>Options>Appearance>Look and Feel

To add dark look and feels install the Dark Look And Feel Themes plugin via Tools>Plugin>Available Plugins

### Maven problems with small tmpfs

If your system has a small tmpfs partition you will have problems unpacking the maven index (will continue downloading again after failing to unpack). To remedy this add `netbeans_default_options="-J-client -J-Xss2m -J-Xms32m -J-XX:PermSize=32m -J-Dapple.laf.useScreenMenuBar=true -J-Dapple.awt.graphics.UseQuartz=true -J-Dsun.java2d.noddraw=true -J-Dsun.java2d.dpiaware=true -J-Dsun.zip.disableMemoryMapping=true -J-Djava.io.tmpdir=/path/to/tmp/dir"` to the end of your netbeans.conf file.

## Integrate with tomcat

It is possible to debug web applications running on tomcat within netbeans:

First install [tomcat](/index.php/Tomcat "Tomcat").

You will need to create a configuration and deployment folder for your user, for example in `~/.tomcat7`.

Copy `/etc/tomcat7/` in `~/.tomcat7/conf`.

Make sure to configure `~/.tomcat7/conf/tomcat-users.xml` with a user having tomcat admin permissions so that netbeans can deploy applications.

Copy `/var/lib/tomcat7/webapps` to `~/.tomcat7/webapps`.

Then, in Netbeans go to Tools>Servers>Add Server and select Apache Tomcat.

In server location specify `/usr/share/tomcat7`

Check "Use Private Configuration Folder (Catalina Base)" and specify `~/.tomcat7`.

Finally, set the username and password you configured in `/etc/tomcat7/tomcat-users.xml`.

## Troubleshooting

### OpenJDK vs Sun's JDK

Netbeans 7.0-1 will not ALWAYS work with OpenJDK. Some reported issues are:

*   Starting - In some cases, netbeans will not start.
*   Installation - The .sh script provided by netbeans will not launch wizard (any proofs?).
*   JavaFX module does not work (see [FS#29843](https://bugs.archlinux.org/task/29843)).

### Glassfish server - Can`t download Glassfish server I/O Exception

If you are trying add new Glassfish server, you can`t download the server. Netbeans returns

```
I/O Exception: [http://java.net/download/glassgish/3.0.1/release/glassfish-3.0.1-ml.zip](http://java.net/download/glassgish/3.0.1/release/glassfish-3.0.1-ml.zip)

```

Solution is:

*   Download GlassFish Server Open Source Edition manualy from official site, actual link is [http://download.java.net/glassfish/3.0.1/release/glassfish-3.0.1-ml.zip](http://download.java.net/glassfish/3.0.1/release/glassfish-3.0.1-ml.zip)
*   Extract from zip to any location

### Integrate Netbeans with kwallet

Netbeans may need to store some passwords. It can do that in kwallet. See [this article](http://wiki.netbeans.org/FaqMasterPasswordDialog) in the Netbeans wiki.

However, you need to install and configure [qtchooser](https://www.archlinux.org/packages/?name=qtchooser) so that netbeans find the qdbus command:

```
$ ln -s /etc/xdg/qtchooser/4.conf ~/.config/qtchooser/default.conf

```

See forum discussion [[[1]](https://bbs.archlinux.org/viewtopic.php?pid=1374434#p1374434)]