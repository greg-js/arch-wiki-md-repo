Tomcat is an open source Java [Servlet container](https://en.wikipedia.org/wiki/Java_Servlet#Servlet_containers "wikipedia:Java Servlet") developed by the Apache Software Foundation. For more information about basic configuration, see:[Tomcat and Apache](/index.php/Tomcat_and_Apache "Tomcat and Apache")

**Note:** Tomcat currently exists under two stable branches: [7](http://tomcat.apache.org/download-70.cgi) and [8](https://tomcat.apache.org/download-80.cgi). None of these version deprecates the preceding. Instead, [each branch is the implementation of a couple of the "Servlet" and "JSP" Java standards](http://tomcat.apache.org/whichversion.html#Apache_Tomcat_Versions). All versions are officially supported in Arch Linux: [tomcat7](https://www.archlinux.org/packages/?name=tomcat7) and [tomcat8](https://www.archlinux.org/packages/?name=tomcat8). Check the version you need depending on your web applications requirements. If you just want to try out tomcat or just do not want to spend more time figuring out, there are good chances you will want to try tomcat7\. This wiki page refers to tomcat7 but most of its content can be applied to tomcat8.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Filesystem hierarchy](#Filesystem_hierarchy)
*   [2 Initial configuration](#Initial_configuration)
*   [3 Start/stop Tomcat](#Start.2Fstop_Tomcat)
    *   [3.1 Alternate "manual" way](#Alternate_.22manual.22_way)
*   [4 Deploy and handle web applications](#Deploy_and_handle_web_applications)
    *   [4.1 The GUI way](#The_GUI_way)
    *   [4.2 The CLI way](#The_CLI_way)
    *   [4.3 Hosting files outside the webapps folder](#Hosting_files_outside_the_webapps_folder)
*   [5 Logging](#Logging)
*   [6 Further setup](#Further_setup)
    *   [6.1 Migrating from previous versions of Tomcat](#Migrating_from_previous_versions_of_Tomcat)
    *   [6.2 Using Tomcat with a different JRE/JDK](#Using_Tomcat_with_a_different_JRE.2FJDK)
    *   [6.3 Security configuration](#Security_configuration)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Tomcat service is started, but page is not loaded](#Tomcat_service_is_started.2C_but_page_is_not_loaded)

## Installation

Install one of [tomcat7](https://www.archlinux.org/packages/?name=tomcat7), or [tomcat8](https://www.archlinux.org/packages/?name=tomcat8).

If deploying Tomcat onto a production environment, consider installing [tomcat-native](https://www.archlinux.org/packages/?name=tomcat-native). The native library for Tomcat configures the server to use the Apache Portable Runtime (APR) library's network connection (socket) and RNG implementations. It uses native 32- or 64-bit code to enhance performance and is sometimes used in production environments where speed is crucial. No configuration is necessary for default Tomcat installations. More information is availble in the [official Tomcat docs](http://tomcat.apache.org/native-doc/).

Using tomcat-native will remove the following warning in `catalina.err`:

```
INFO: The APR based Apache Tomcat Native library which allows optimal performance in production environments was not found on the java.library.path [...]

```

### Filesystem hierarchy

Replace the `*` with your installed version (7 or 8).

| Pathname | Use |
| `/etc/tomcat*` | Configuration files. Among some: `tomcat-users.xml` (defines users allowed to use administration tools and their roles), `server.xml` (Main Tomcat configuration file), `catalina.policy` (security policies configuration file) |
| `/usr/share/tomcat*` | Main Tomcat folder containing scripts and links to other directories |
| `/usr/share/java/tomcat*` | Tomcat Java libraries (jars) |
| `/var/log/tomcat*` | Log files **not** handled by `systemd` (see [#Logging](#Logging)) |
| `/var/lib/tomcat*/webapps` | Where Tomcat deploys your web applications |
| `/var/tmp/tomcat*` | Where Tomcat store your webapps' data |

## Initial configuration

In order to be able to use the manager webapp and the admin webapp you need to edit the following file: `/etc/tomcat7/tomcat-users.xml`

Uncomment the "role and user" XML declaration and modify it to enable roles `tomcat`, `admin-{gui,script}` and/or `manager-{gui,script,jmx,status}` depending on your needs (see [Configuring Manager Application Access](http://tomcat.apache.org/tomcat-7.0-doc/manager-howto.html#Configuring_Manager_Application_Access)). To keep it short, `tomcat` is the mandatory role used to run, `manager-*` are roles able to administer web applications and `admin-*` are full right administrator roles on the Tomcat server.

Here is a bare configuration file that declares some of these roles along with usernames and passwords (Be sure to change the following [CHANGE_ME] passwords to something secure):

 `/etc/tomcat7/tomcat-users.xml` 
```
<?xml version='1.0' encoding='utf-8'?>
<tomcat-users>
  <role rolename="tomcat"/>
  <role rolename="manager-gui"/>
  <role rolename="manager-script"/>
  <role rolename="manager-jmx"/>
  <role rolename="manager-status"/>
  <role rolename="admin-gui"/>
  <role rolename="admin-script"/>
  <user username="tomcat" password="**[CHANGE_ME]**" roles="tomcat"/>
  <user username="manager" password="**[CHANGE_ME]**" roles="manager-gui,manager-script,manager-jmx,manager-status"/>
  <user username="admin" password="**[CHANGE_ME]**" roles="admin-gui"/>
</tomcat-users>
```

Keep in mind that Tomcat must be restarted each time a modification is made to this file.

This [blog post](http://blog.techstacks.com/2010/07/new-manager-roles-in-tomcat-7-are-wonderful.html) gives a good description of these roles.

To have read permissions on the configuration files and work well with some IDEs, you must add your user to the `tomcat7` (respectively `tomcat8`) group:

```
 gpasswd -a <user> tomcat<number>

```

## Start/stop Tomcat

[Start](/index.php/Start "Start") the `tomcat7` service.

Once Tomcat is started, you can visit this page to see the result: [http://localhost:8080](http://localhost:8080). If a nice Tomcat local home page is displayed this means your Servlet container is up and running and ready to host you web apps. If the startup script failed or you can only see a Java error displayed in you browser, have a look at startup logs using [systemd's journalctl](/index.php/Systemd#Journal "Systemd"). Google is full of answers on recurrent issues found in Tomcat logs.

**Note:** To improve security, Arch Linux's Tomcat packages use the [jsvc](http://commons.apache.org/daemon/jsvc.html) binary from Apache's [common-daemons](http://commons.apache.org/daemon/). Tomcat's `systemd` service runs this Apache binary with root privileges which itself starts Tomcat with an underprivileged user (`tomcat7:tomcat7` in Arch Linux). This prevents malicious code that could be executed in a bad web application from causing too much damage. This also enables the use of ports under 1024 if needed. See `man jsvc` for options available and pass them through the `CATALINA_OPTS` environment variable declared in `/etc/conf.d/tomcat7`.

### Alternate "manual" way

Tomcat can also be controlled directly using upstream scripts:

```
/usr/share/tomcat/bin/{startup.sh,shutdown.sh,..}

```

This can be useful to debug applications or even debug Tomcat, but do not use it to start Tomcat for the first time as doing so can set some permissions wrongly and stop web apps from working. In order to be able to use these scripts, some further configuration may be needed. Be aware that using these scripts prevents the jsvc security advantage described above.

## Deploy and handle web applications

Tomcat 7 is bundled with 5 already deployed web applications (change localhost with your server's FQDN if needed):

*   The default home page: [http://localhost:8080/](http://localhost:8080/)
*   Tomcat 7's local documentation: [http://localhost:8080/docs/](http://localhost:8080/docs/)
*   Examples of Servlets and JSP: [http://localhost:8080/examples/](http://localhost:8080/examples/)
*   The host-manager to handle virtual hosts: [http://localhost:8080/host-manager/](http://localhost:8080/host-manager)
*   The manager to administer web applications: [http://localhost:8080/manager/html/](http://localhost:8080/manager/html)

### The GUI way

Probably the easiest way is to use the manager webapp [http://localhost:8080/manager/html](http://localhost:8080/manager/html). Use the username/password you defined as `manager` in `tomcat-users.xml`. Once logged in you can see five already deployed web applications. Add yours through the "Deploy" area and then stop/start/undeploy it with the "Applications" area.

### The CLI way

One can also just copy the WAR file of the application to directory `/usr/share/tomcat7/webapps`. For that later, be sure that the `autoDeploy` option is still set for the right host as shown here:

 `/etc/tomcat7/server.xml` 
```
...
<Host name="localhost"  appBase="webapps"
      unpackWARs="true" **autoDeploy="true"**>
...
```

### Hosting files outside the webapps folder

If you want to keep your project outside the webapps folder this is possible by creating a `Context`. Go to `/etc/tomcat<number>/Catalina/localhost/` and create your context. A context is a simple xml file which specifies where tomcat should look for the project. The basic format of the file is

 `/etc/tomcat7/Catalina/localhost/whatShouldFollowLocalhost.xml`  `<Context path="/whatSholdFollwLocalhost" docBase="/where/your/project/is/" reloadable="true"/>` 

A working example is as follows. This assumes that the project is hosted somewhere in the users /home-folder.

 `/etc/tomcat7/Catalina/localhost/myProject.xml`  `<Context path="/myProject" docBase="/home/archie/code/jsp/myProject" reloadable="true"/>` 

The files can now be hosted in `/home/archie/code/jsp/myProject/`. To see the project in your webbrowser, go to [http://localhost:8080/myProject](http://localhost:8080/myProject). If tomcat is unable to load the files, it might be an issue with permissions. `chmod o+x /home/archie/code/jsp/myProject` should fix the issue.

## Logging

Tomcat when used with official Arch Linux packages uses [systemd's journalctl](/index.php/Systemd#Journal "Systemd") **for startup log**. This means that files `/var/log/tomcat7/catalina.err` and `/var/log/tomcat7/catalina.out` are **not** used. Other logs such as access logs and business logs defined in `/etc/tomcat7/server.xml` as `Valve` will still by default end up in `/var/log/tomcat7/`.

To restore upstream style logging, copy systemd file `/lib/systemd/system/tomcat7.service` to `/etc/systemd/system/tomcat7.service` and change both `SYSLOG` for the absolute paths of log files.

## Further setup

Basic configuration can be made through the virtual host manager web application: [http://localhost:8080/host-manager/html](http://localhost:8080/host-manager/html). Provide the username/password you set in `tomcat-users.xml`. Other options are tweaked in configuration files in `/etc/tomcat7`, the most important being `server.xml`. Using these files is out of the scope of this 101 wiki page. Please have a look at the [official Tomcat 7 documentation](http://tomcat.apache.org/tomcat-7.0-doc/index.html) for more details.

### Migrating from previous versions of Tomcat

As said in the introduction, **Tomcat 8 does not deprecate Tomcat 7**. They are all three, implementations of Servlet/JSP standards. Hence you must first determine [which version](http://tomcat.apache.org/whichversion.html#Apache_Tomcat_Versions) of Tomcat you need depending on the versions of Servlet/JSP your application uses. If you need to migrate, the official website gives [instructions on how to handle such a process](http://tomcat.apache.org/migration.html).

### Using Tomcat with a different JRE/JDK

Apart from installing the desired JRE/JDK, the only requirement is to set the TOMCAT_JAVA_HOME variable in Tomcat's `systemd` service file.

The variable can be overridden by a custom configuration, as described in [Systemd#Editing provided units](/index.php/Systemd#Editing_provided_units "Systemd"):

1.  create the directory */etc/systemd/system/tomcat7.service.d*
2.  in that directory, save a *start.conf* file with this content (for the Oracle JDK package [jdk](https://aur.archlinux.org/packages/jdk/), use instead */usr/lib/jvm/java-8-jdk*):

```
[Service]
Environment=TOMCAT_JAVA_HOME=/usr/lib/jvm/java-8-openjdk

```

Alternatively, copy the service file */usr/lib/systemd/system/tomcat7.service*, to */etc/systemd/system/* and replace this line:

```
Environment=TOMCAT_JAVA_HOME=/usr/lib/jvm/java-7-openjdk

```

by (e.g. for Oracle JDK)

```
Environment=TOMCAT_JAVA_HOME=/opt/java

```

### Security configuration

This page gives the bare minimum to get your first web application to run on Tomcat. It is not intended to be the definitive guide to administering Tomcat (it is a job of its own). The official Tomcat website will provide all necessary official matter. One could also refer to [this O'Reilly page](http://oreilly.com/java/archive/tomcat-tips.html) and this [last one](http://www.unidata.ucar.edu/projects/THREDDS/tech/reference/TomcatSecurity.html). Still, here are some security tips to get you started:

*   Keep your Tomcat installation up to date to get the latest fixes to security issues
*   Remove unwanted default applications such as `examples`, `docs`, default home page `ROOT` ("_" in the `manager` webapp). This prevents potential security holes to be exploited. Use the `manager` for that.

For more security you could even remove the host-manager and manager web applications. Keep in mind that the later is useful to deploy web applications.

*   Disable the WAR auto-deploy option. This would prevent someone who gained restricted access to the server to copy a WAR into the `/usr/share/java/webapps` directory to get it running. Edit `server.xml` and set the `autoDeploy` to `false`:

 `/etc/tomcat7/server.xml` 
```
...
<Host name="localhost"  appBase="webapps"
      unpackWARs="true" **autoDeploy="false"**>
...
```

*   Anonymize Tomcat's default error page to prevent potential attackers to retrieve Tomcat's version. To see what Tomcat says by default, just visit an nonexistent page such as [http://localhost:8080/I_dont_exist](http://localhost:8080/I_dont_exist). You get a 404 error page with Tomcat's version at the bottom.

To anonymize this, edit/open the following JAR (Editors like `vim` can edit zips directly)

```
/usr/share/tomcat7/lib/catalina.jar

```

And edit the following file

 `org/apache/catalina/util/ServerInfo.properties` 
```
...
server.info=
server.number=
server.built=
...
```

*   Disable unused `connectors` in `server.xml`
*   Keep restricted access to `/etc/tomcat7/server.xml`. Only `tomcat` user and/or `root` should be able to read and write this.
*   Keep `jsvc` usage. Do not use upstream startup scripts unless particular reason as explained in the security note above.
*   Use strong different passwords for each user in `tomcat-users.xml`, give roles to users who really need them and even disable usernames/roles you do not use/need.

One can even crypt `tomcat-users.xml` passwords using the following upstream script:

```
/usr/share/tomcat7/bin/digest.sh -a SHA NEW_PASSWORD

```

This will output something like:

```
NEW_PASSWORD:b7bbb48a5b7749f1f908eb3c0c021200c72738ce

```

Paste the hashed part in place of the clear password in `tomcat-users.xml` and add the following to `server.xml`:

 `/etc/tomcat7/server.xml` 
```
<Host
  ...
  <Realm
    ...
    **className="org.apache.catalina.realm.MemoryRealm" digest="SHA"**
    ...
  />
  ...
/>
```

Note that this may not be relevant because only root and/or tomcat is supposed to have read/write access to that file. If an intruder manages to gain root access then he would not need such passwords to mess with your applications/data anyway. Be sure to keep restricted RW access to that file!

*   Always know what you are deploying

## Troubleshooting

### Tomcat service is started, but page is not loaded

First check `/etc/tomcat7/tomcat-users.xml` for any syntax error. If everything is fine and `tomcat7` is correctly running, type `journalctl -r` to check the logs for any exception thrown (see [Logging](https://wiki.archlinux.org/index.php/Tomcat#Logging)). If you read anything like `java.lang.Exception: Socket bind failed: [98] Address already in use`, this is due to some other service listening on the same port. For instance, it is possible that [Apache](https://wiki.archlinux.org/index.php/Apache_HTTP_Server) and Tomcat are listening on the same port (if for example you have Apache running on port 8080 with [Nginx](https://wiki.archlinux.org/index.php/Nginx) serving it as a proxy on port 80). If this is the case, edit the `/etc/tomcat7/server.xml` file and change the Connector port to something else under `<Service name="Catalina">`:

 `/etc/tomcat7/server.xml` 
```
<?xml version='1.0' encoding='utf-8'?>
...
...
<Service name="Catalina">
    <Connector executor="tomcatThreadPool"
                 port="8090" protocol="HTTP/1.1"
                 connectionTimeout="20000"
                 redirectPort="8443" />
...
...
</Service>
```

Finally [restart](https://wiki.archlinux.org/index.php/Systemd#Using_units) `tomcat7` and `httpd` services.