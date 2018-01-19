**Netbeans** is an integrated development environment (IDE) for developing with Java, JavaScript, PHP, Python, Ruby, Groovy, C, C++, Scala, Clojure, and other languages.

From [Wikipedia article](https://en.wikipedia.org/wiki/Netbeans "wikipedia:Netbeans"):

	"*The NetBeans IDE is written in Java and can run anywhere a compatible JVM is installed, including Windows, Mac OS, Linux, and Solaris. A JDK is required for Java development functionality, but is not required for development in other programming languages.*"

## Contents

*   [1 Installation](#Installation)
*   [2 Tips and tricks](#Tips_and_tricks)
    *   [2.1 Font antialiasing in Netbeans](#Font_antialiasing_in_Netbeans)
    *   [2.2 Look and feel](#Look_and_feel)
    *   [2.3 Integrate with the Apache Tomcat Servlet Container](#Integrate_with_the_Apache_Tomcat_Servlet_Container)
    *   [2.4 Integrate Netbeans with kwallet](#Integrate_Netbeans_with_kwallet)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Maven problems with small tmpfs](#Maven_problems_with_small_tmpfs)
    *   [3.2 Wrong Directory for JDK/JRE](#Wrong_Directory_for_JDK.2FJRE)

## Installation

As you can see on the [download page](https://netbeans.org/downloads/index.html) , Netbeans is actually segmented into different flavors, each made for a specific use case. There is also a version gathering all the different flavors together.

If you want to install all the flavors at once, [install](/index.php/Install "Install") the [netbeans](https://www.archlinux.org/packages/?name=netbeans) package or [netbeans-nightly](https://aur.archlinux.org/packages/netbeans-nightly/).

If you want a specific flavor, in order to have a minimal installation for example, install one of the following packages:

*   Java SE: [netbeans-javase](https://aur.archlinux.org/packages/netbeans-javase/) or [netbeans-javase-nightly](https://aur.archlinux.org/packages/netbeans-javase-nightly/);
*   Java EE: [netbeans-javaee](https://aur.archlinux.org/packages/netbeans-javaee/) or [netbeans-javaee-nightly](https://aur.archlinux.org/packages/netbeans-javaee-nightly/);
*   HTML5/Javascript or PHP: [netbeans-php](https://aur.archlinux.org/packages/netbeans-php/) or [netbeans-php-nightly](https://aur.archlinux.org/packages/netbeans-php-nightly/);

	The versions provider either for the flavor HTML5/Javascript or the flavor PHP are actually the same package.

*   C/C++: [netbeans-cpp](https://aur.archlinux.org/packages/netbeans-cpp/) or [netbeans-cpp-nightly](https://aur.archlinux.org/packages/netbeans-cpp-nightly/).

Please note the `-nightly` versions are actually binaries versions compiled everyday from the trunk branch from the development repository.

## Tips and tricks

**Note:** The global netbeans.conf `/usr/share/netbeans/etc/netbeans.conf` will be overwritten during updates. To keep changes add them to your local netbeans.conf `~/.netbeans/*version*/etc/netbeans.conf` (you will need to create the etc dir and the .conf file).

*   Settings in local version of netbeans.conf override the same settings in the global copy of the file.
*   Command-line options override settings in either of the configuration files.

### Font antialiasing in Netbeans

As Netbeans is written in [Java](/index.php/Java "Java"), the font rendering is managed by Java itself and also by Netbeans. Modifying the font antialiasing parameters can thus happen at two levels:

*   [Java](/index.php/Java#Better_font_rendering "Java").
*   In the Netbeans configuration. If the file is missing, you may need to create it.

 `~/.netbeans/*version*/etc/netbeans.conf` 
```
*[...]*
netbeans_default_options="*[...]*-J-Dswing.aatext=TRUE -J-Dawt.useSystemAAFontSettings=on"
*[...]*
```

### Look and feel

To change Netbeans look and feel, go to *Tools > Options > Appearance > Look and Feel*

To add a dark look and feel to the GUI but also to the colorschemes used in the code, you can install one of the following certified extension from the plugin directory which can be reached from *Tools > Plugins > Available Plugins*:

*   *Dark Look And Feel Themes*
*   *Darcula LAF for NetBeans*: which, as of January 2017, better integrates with current [desktop environments](/index.php/Desktop_environments "Desktop environments") and mimic the default Darcula look and feel from used in IntelliJ IDEA or [Android Studio](/index.php/Android_Studio "Android Studio").

### Integrate with the Apache Tomcat Servlet Container

It is possible to debug web applications running on [Tomcat](/index.php/Tomcat "Tomcat") from within Netbeans, using stock Arch packages for both Netbeans and Tomcat. While this section is written for `tomcat7`, this applies to all versions of Tomcat currently in the repositories. (To check which are available, run `pacman -Ss tomcat`)

*   First install your desired version of Tomcat, such as `pacman -S tomcat7` (see also [Tomcat](/index.php/Tomcat "Tomcat")).
*   While you can modify the configuration files in `/etc/tomcat7` to work with Netbeans debugging, it is recommended you create local copies and use those instead. That way, you still can run Tomcat as an ongoing system service, while debuggging with a different instance:
    *   Pick a location for the local configuration files, such as `~/.tomcat7` and create that directory.
    *   Copy `/etc/tomcat7/` to `~/.tomcat7/conf`, e.g. `sudo cp -r /etc/tomcat7 ~/.tomcat7/conf` and `sudo chown -R $(id -un):$(id -gn) ~/.tomcat7`
*   Clean up the Tomcat users and permission file, so Netbeans can insert what it needs. Edit the tomcat user file without any user and role information in it:

 `~/.tomcat7/conf/tomcat-users.xml` 
```
<?xml version='1.0' encoding='utf-8'?>
<tomcat-users xmlns="[http://tomcat.apache.org/xml](http://tomcat.apache.org/xml)"
              xmlns:xsi="[http://www.w3.org/2001/XMLSchema-instance](http://www.w3.org/2001/XMLSchema-instance)"
              xsi:schemaLocation="[http://tomcat.apache.org/xml](http://tomcat.apache.org/xml) tomcat-users.xsd"
              version="1.0">
</tomcat-users>
```

*   Make the "manager" app accessible from your local configuration: `mkdir ~/.tomcat7/webapps` and `ln -s /var/lib/tomcat7/webapps/manager ~/.tomcat7/webapps/manager`
*   Provide a temp directory: `mkdir ~/.tomcat7/temp`
*   If needed, change the port at which Tomcat runs by editing `~/.tomcat7/conf/server.xml`
*   Have Tomcat write its logs somewhere else than `/var/log/tomcat7`
*   Unfortunately, Netbeans refuses to continue unless you make file `/etc/tomcat7/server.xml` readable to it. So `sudo chmod 644 /etc/tomcat7/server.xml` temporarily, and change it back later.

Then, in Netbeans:

*   Go to *Tools > Servers > Add Server* and select *Apache Tomcat*. Click *Next*.
*   In *Server location*, specify `/usr/share/tomcat7`
*   Check *Use Private Configuration Folder (Catalina Base)* and specify the full path to directory `~/.tomcat7`. This must be the full path, as Netbeans does not recognize the meaning of `~`.
*   Finally, pick a username and password. Check *Create user if it does not exist*. This will configure Netbeans, but also add the user information to the `tomcat-users.xml` file.

Note that this local instance of Tomcat will write its logs to `~/.tomcat7/logs`, not `/var/log/tomcat7`.

### Integrate Netbeans with kwallet

Netbeans may need to store some passwords. It can do that in kwallet. See [this article](http://wiki.netbeans.org/FaqMasterPasswordDialog) in the Netbeans wiki.

However, you need to install and configure [qtchooser](https://aur.archlinux.org/packages/qtchooser/) so that netbeans find the qdbus command:

```
$ ln -s /etc/xdg/qtchooser/4.conf ~/.config/qtchooser/default.conf

```

See forum discussion [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1374434#p1374434)

## Troubleshooting

### Maven problems with small tmpfs

If your system has a small tmpfs partition you will have problems unpacking the maven index (will continue downloading again after failing to unpack). To fix this issue, append the following pieces of informations in the Netbeans configuration file accordingly.

 `~/.netbeans/*version*/etc/netbeans.conf` 
```
*[...]*
netbeans_default_options="*[...]*-J-client -J-Xss2m -J-Xms32m -J-XX:PermSize=32m -J-Dapple.laf.useScreenMenuBar=true -J-Dapple.awt.graphics.UseQuartz=true -J-Dsun.java2d.noddraw=true -J-Dsun.java2d.dpiaware=true -J-Dsun.zip.disableMemoryMapping=true -J-Djava.io.tmpdir=/path/to/tmp/dir"
*[...]*
```

### Wrong Directory for JDK/JRE

It might be that after installation, netbeans_jdkhome is set incorrectly:

 `/usr/share/netbeans/etc/netbeans.conf` 
```
*[...]*
netbeans_jdkhome="/tmp/yaourt-tmp-x230a/aur-netbeans-cpp/pkg/netbeans-cpp/usr/share/netbeans/bin/jre" (example)
*[...]*
```

Just comment out this line, netbeans will find the proper path on startup. Since netbeans.conf might be overwritten during an update, this procedure might need to be done again after an update, or you put netbeans_jdkhome into the config in your home directory (see above).