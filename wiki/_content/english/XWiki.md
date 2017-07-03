[XWiki](http://www.xwiki.org) is an open-source enterprise-ready wiki written in Java, with a focus on extensibility.

You may also be interested in [Foswiki](/index.php/Foswiki "Foswiki"), which caters to similar needs, but is written in Perl.

## Installation

Feel free to follow along on the [XWiki Installation Guide](http://platform.xwiki.org/xwiki/bin/view/AdminGuide/Installation). These instructions assume you will be using [Tomcat](/index.php/Tomcat "Tomcat") and [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"). It should not be too difficult to apply these guidelines to other combinations.

*   Install [PostgreSQL](/index.php/PostgreSQL "PostgreSQL").
*   For easier PostgreSQL administration, install [phpPgAdmin](/index.php/PhpPgAdmin "PhpPgAdmin").
*   Install [Tomcat 7](/index.php/Tomcat "Tomcat"). (Do not forget `tomcat-native`.)
*   Download the XWiki WAR file.
*   Rename the WAR file to `xwiki`.
*   Move the WAR file into the `/var/lib/tomcat7/webapps` directory.
*   Tomcat should automatically extract the WAR file. If not, restart Tomcat.
*   At this point, you may find that a `data` directory has appeared in `/var/lib/tomcat7/webapps`. Delete it.
*   As root:

```
# cd /var/lib/tomcat7
# mkdir data
# chown tomcat:tomcat data

```

*   Inside the `/var/lib/tomcat7/webapps/xwiki/WEB-INF` directory:
    *   Open the `xwiki.cfg` file and alter the `xwiki.work.dir` field to read `/var/lib/tomcat7/data/xwiki`.
    *   Open the `xwiki.properties` file and alter the `container.persistentDirectory` field to read `/var/lib/tomcat7/data/xwiki`.
    *   Open the `hibernate.cfg.xml` file and:
        *   Comment-out the section entitled "Configuration for the default database".
        *   Uncomment the section entitled "PostgreSQL Configuration".
        *   Modify the database name (in `connection.url`), username, and password as desired.
*   Create a role and database in PostgreSQL to match the hibernate configuration.
*   Install [postgresql-jdbc](https://aur.archlinux.org/packages/postgresql-jdbc/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").
*   As root:

```
# cd /usr/share/java/tomcat7
# ln -s /usr/share/java/postgresql-jdbc/postgresql-jdbc4.jar

```

*   Restart Tomcat.
*   Launch the XWiki application by clicking on `/xwiki` in Tomcat Manager.
*   Download the XAR file for XWiki and upload it to populate the empty Wiki.

## Nginx proxy configuration

I found that instructing nginx to proxy to `[http://localhost:8080/xwiki/](http://localhost:8080/xwiki/)` did not work: the generated URLs were incorrect. Contrary to what is indicated in the [XWiki documentation](http://platform.xwiki.org/xwiki/bin/view/AdminGuide/Configuration#HReverseproxysetup), I could not make the URLs correct through the use of HTTP headers.

The only solution I'm aware of so far is to create a new `Host` element in Tomcat's `server.xml` file:

*   Duplicate the existing `Host` element and alter the `name` attribute to read `xwiki`.
*   Alter the `appBase` attribute to read `/var/lib/tomcat7/webapps-xwiki`.
*   Move the `xwiki` application from `/var/lib/tomcat7/webapps/xwiki` to `/var/lib/tomcat7/webapps-xwiki/ROOT`.
*   Restart Tomcat
*   Add `xwiki` as an alias to localhost in `/etc/hosts` (add it to the end of the 127.0.0.1 line).
*   Instruct Nginx to proxy to `[http://xwiki:8080/](http://xwiki:8080/)` instead.