[Eclipse](https://eclipse.org) is an open source community project, which aims to provide a universal development platform. The Eclipse project is most widely known for its cross-platform integrated development environment (IDE). The Arch Linux packages (and this guide) relate specifically to the IDE.

The Eclipse IDE is largely written in Java but can be used to develop applications in a number of languages, including Java, C/C++, PHP, Perl and Python. The IDE can also provide subversion support and task management.

## Contents

*   [1 Installation](#Installation)
*   [2 Plugins](#Plugins)
    *   [2.1 Add the default update site](#Add_the_default_update_site)
    *   [2.2 Eclipse Marketplace](#Eclipse_Marketplace)
    *   [2.3 Plugin manager](#Plugin_manager)
        *   [2.3.1 Updates via plugin manager](#Updates_via_plugin_manager)
    *   [2.4 List of plugins](#List_of_plugins)
*   [3 Enable javadoc integration](#Enable_javadoc_integration)
    *   [3.1 Online version](#Online_version)
    *   [3.2 Offline version](#Offline_version)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Ctrl+X closes Eclipse](#Ctrl.2BX_closes_Eclipse)
    *   [4.2 Dark theme](#Dark_theme)
    *   [4.3 Change Default Window Title Font Size](#Change_Default_Window_Title_Font_Size)
    *   [4.4 Disable GTK+ 3](#Disable_GTK.2B_3)
    *   [4.5 Freshplayerplugin](#Freshplayerplugin)
    *   [4.6 Eclipse 4.6 may not open the marketplace properly](#Eclipse_4.6_may_not_open_the_marketplace_properly)
    *   [4.7 Show in System Explorer does not work](#Show_in_System_Explorer_does_not_work)
    *   [4.8 Display issues under Wayland](#Display_issues_under_Wayland)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") one of the following packages:

*   [eclipse-jee](https://www.archlinux.org/packages/?name=eclipse-jee) for Java EE Developers
*   [eclipse-java](https://www.archlinux.org/packages/?name=eclipse-java) for Java Developers
*   [eclipse-cpp](https://www.archlinux.org/packages/?name=eclipse-cpp) for C/C++ Developers
*   [eclipse-php](https://www.archlinux.org/packages/?name=eclipse-php) for PHP Developers
*   [eclipse-javascript](https://www.archlinux.org/packages/?name=eclipse-javascript) for JavaScript and Web Developers

You cannot install multiple of these at the same time since they conflict, see [FS#45577](https://bugs.archlinux.org/task/45577): choose the package above which most immediately fulfills your needs, and then add support for any additionally required languages through [#Plugins](#Plugins).

## Plugins

Many plugins are easily installed using **pacman** (see [Eclipse plugin package guidelines](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") for further information). This will also keep them up-to-date. Alternatively, you can choose either the [Eclipse Marketplace](#Eclipse_Marketplace) or the internal [plugin manager](#Plugin_manager).

### Add the default update site

Make sure that you check that the default update site for your version of Eclipse is configured so that plugin dependencies can automatically be installed. The most current version of Eclipse is Photon and the default update site for it is: [http://download.eclipse.org/releases/photon](http://download.eclipse.org/releases/photon). Go to Help > Install new Software > Add, fill the name to easily identify the update site later - for instance, Photon Software Repository - and fill the location with the url.

### Eclipse Marketplace

**Note:** make sure you have followed the [Add the default update site](#Add_the_default_update_site) section.

To use the Eclipse Marketplace, install it first: go to Help > Install new software > Switch to the default update site > General Purpose Tools > Marketplace Client. Restart Eclipse and it will be available in Help > Eclipse Marketplace.

### Plugin manager

**Note:** make sure you have followed the [Add the default update site](#Add_the_default_update_site) section.

Use Eclipse's plugin manager to download and install plugins from their original repositories: in this case you have to find the needed repository in the plugin's website, then go to *Help > Install New Software...*, enter the repository in the *Work with* field, select the plugin to install from the list below and follow the instructions.

**Note:**

*   If you install plugins with Eclipse's plugin manager, you are advised to launch Eclipse as root: this way the plugins will be installed in `/usr/lib/eclipse/plugins/`; if you installed them as normal user, they would be stored in a version-dependent folder inside `~/.eclipse/`, and, after upgrading Eclipse, they would not be recognized any longer.
*   Do not use Eclipse as root for your everyday work.

#### Updates via plugin manager

Run Eclipse and select *Help > Check for Updates*. If you have installed them as root as advised in the section above, you have to run Eclipse as root.

For plugins to be updated, you should check to have their update repositories enabled in *Window > Preferences > Install/Update > Available Software Sites*: you can find each plugin's repository(es) on the respective project website. To add, edit, remove... repositories just use the buttons on the right of the *Available Software Sites* panel. For Eclipse 4.5 (Mars), check you have enabled this repository:

```
[http://download.eclipse.org/releases/mars](http://download.eclipse.org/releases/mars)

```

To receive update notifications, go to *Window > Preferences > Install/Update > Automatic Updates*. If you want to receive notifications for plugins installed as root, you should run Eclipse as root, go to *Window > Preferences > Install/Update > Available Software Sites*, select the repositories related to the installed plugins and *Export* them, then run Eclipse as normal user and *Import* them in the same panel.

### List of plugins

*   **AVR** — AVR microcontroller plugin.

	[http://avr-eclipse.sourceforge.net/wiki/index.php/The_AVR_Eclipse_Plugin](http://avr-eclipse.sourceforge.net/wiki/index.php/The_AVR_Eclipse_Plugin) || [eclipse-avr](https://aur.archlinux.org/packages/eclipse-avr/)

*   **Aptana** — HTML5/CSS3/JavaScript/Ruby/Rails/PHP/Pydev/Django support. Also available as standalone application.

	[http://www.aptana.com/](http://www.aptana.com/) || [aptana-studio](https://aur.archlinux.org/packages/aptana-studio/)

*   **IvyDE** — IvyDE dependency Manager.

	[https://ant.apache.org/ivy/ivyde/](https://ant.apache.org/ivy/ivyde/) || [eclipse-ivyde](https://aur.archlinux.org/packages/eclipse-ivyde/)

*   **Markdown** — Markdown editor plugin for Eclipse.

	[http://www.winterwell.com/software/markdown-editor.php](http://www.winterwell.com/software/markdown-editor.php) || [eclipse-markdown](https://aur.archlinux.org/packages/eclipse-markdown/)

*   **PyDev** — [Python](/index.php/Python "Python") support.

	[http://pydev.org/](http://pydev.org/) || [eclipse-pydev](https://aur.archlinux.org/packages/eclipse-pydev/)

*   **Subclipse** — [Subversion](/index.php/Subversion "Subversion") support.

	[https://github.com/subclipse/subclipse](https://github.com/subclipse/subclipse) || [eclipse-subclipse](https://aur.archlinux.org/packages/eclipse-subclipse/)

*   **Subversive** — Alternative Subversion support.

	[https://www.eclipse.org/subversive/](https://www.eclipse.org/subversive/) || [eclipse-subversive](https://aur.archlinux.org/packages/eclipse-subversive/)

*   **TestNG** — TestNG support.

	[http://testng.org/doc/eclipse.html](http://testng.org/doc/eclipse.html) || [eclipse-testng](https://aur.archlinux.org/packages/eclipse-testng/)

*   **TeXlipse** — [LaTeX](/index.php/LaTeX "LaTeX") support.

	[http://texlipse.sourceforge.net/](http://texlipse.sourceforge.net/) || [eclipse-texlipse](https://aur.archlinux.org/packages/eclipse-texlipse/)

*   **Checkstyle** — Eclipse Checkstyle support.

	[http://eclipse-cs.sourceforge.net/](http://eclipse-cs.sourceforge.net/) || [eclipse-checkstyle](https://aur.archlinux.org/packages/eclipse-checkstyle/)

## Enable javadoc integration

Want to see API entries when hovering the mouse pointer over standard Java methods?

### Online version

If you have constant Internet access on your machine, you can use the on-line documentation:

1.  Go to *Window > Preferences*, then go to *Java > Installed JREs*.
2.  There should be one named "java" with the type "Standard VM". Select this and click *Edit*.
3.  Select the `/opt/java/jre/lib/rt.jar` item under "JRE system libraries:", then click *Javadoc Location...*.
4.  Enter "[https://docs.oracle.com/javase/8/docs/api/](https://docs.oracle.com/javase/8/docs/api/)" in the "Javadoc location path:" text field.

### Offline version

You can store the documentation locally by installing the [openjdk8-doc](https://www.archlinux.org/packages/?name=openjdk8-doc) package. Eclipse may be able to find the javadocs automatically. If that does not work, set Javadoc location for rt.jar to `file:/usr/share/doc/java8-openjdk/api`.

## Troubleshooting

### Ctrl+X closes Eclipse

Part of [this](https://bugs.eclipse.org/bugs/show_bug.cgi?id=318177) bug. Just look in `~/workspace/.metadata/.plugins/org.eclipse.e4.workbench/workbench.xmi` and delete the wrong `Ctrl+X` combination. Usually it is the first one.

### Dark theme

Eclipse supplies a Dark theme which can be enabled in Window > Preferences > General > Appearance and selecting the 'Dark' theme.

The dark theme uses its own colours rather than the GTK theme colours, if you prefer it to fully respect GTK colour settings, then remove or move to backup sub folder all of the .css files from `/usr/share/eclipse/plugins/org.eclipse.ui.themes_1.0.0.xxxx/css/`.

### Change Default Window Title Font Size

You cannot change the window title font size using the Eclipse preferences, you must edit the actual theme .css files. Note, that you will have to redo this when you upgrade eclipse. They are located under

```
/usr/share/eclipse/plugins/org.eclipse.platform_4.3.<your version number>/css

```

Open the appropriate file with your text editor, ie e4_default_gtk.css if you are using the "GTK theme". Search for .MPartStack, and change the font-size to your desired size

```
.MPartStack {
       font-size: 9;
       swt-simple: false;
       swt-mru-visible: false;
}

```

### Disable GTK+ 3

When the SWT GTK+ 3 UI is buggy and sometimes unusable, You can try to disable the use of GTK+ 3 with the SWT_GTK3=0 [environment variable](/index.php/Environment_variable "Environment variable") when you start eclipse:

```
SWT_GTK3=0 eclipse

```

Another option to achieve the same effect is to add the following to `/usr/lib/eclipse/eclipse.ini`.

```
--launcher.GTK_version
2

```

Those two lines must be added **before**:

```
--launcher.appendVmargs

```

### Freshplayerplugin

Eclipse is not compatible with [freshplayerplugin](https://aur.archlinux.org/packages/freshplayerplugin/). See [https://github.com/i-rinat/freshplayerplugin/issues/298](https://github.com/i-rinat/freshplayerplugin/issues/298).

### Eclipse 4.6 may not open the marketplace properly

See [this](https://bugs.eclipse.org/bugs/show_bug.cgi?id=497729) bug. You can take following two steps to fix it:

```
eclipse -consoleLog -application org.eclipse.equinox.p2.director -uninstallIU org.apache.httpcomponents.httpclient/4.3.6.v201411290715
cd /usr/lib/eclipse/ && sudo rm plugins/org.apache.httpcomponents.httpclient_4.3.6.v201411290715.jar

```

### Show in System Explorer does not work

See [this](http://help.eclipse.org/luna/index.jsp?topic=%2Forg.eclipse.platform.doc.user%2Freference%2Fref-9.htm&cp=0_4_1_52) guide. Go to **Window** > **Preferences** > **General** > **Workspace** and change the command launching system explorer. As Xfce user you may like to change it to `thunar ${selected_resource_uri}` to open the selected folder with thunar.

### Display issues under Wayland

When running Eclipse on Wayland, you may encounter rendering issues such as slow response time to mouse events or chopped dialog windows (Bug report [[1]](https://bugs.eclipse.org/bugs/show_bug.cgi?id=483545)). A possible workaround for this issue is to force Eclipse to run under XWayland.

With the superuser, open the file `/usr/bin/eclipse` and append this line before the `exec` line :

```
   export GDK_BACKEND=x11

```

This will force the execution of Eclipse on XWayland.

## See also

*   [How to use Subversion with Eclipse](https://www.ibm.com/developerworks/library/os-ecl-subversion/)