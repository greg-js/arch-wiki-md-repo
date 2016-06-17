This document describes the steps needed to install Apache Tomcat. It also optionally describes how to integrate Tomcat with the Apache Web Server, and how to configure MySQL to work with Tomcat Servlets and JSPs.

## Contents

*   [1 Installation](#Installation)
*   [2 Configure Apache](#Configure_Apache)
    *   [2.1 Without mod_jk](#Without_mod_jk)
    *   [2.2 Using mod_jk](#Using_mod_jk)
*   [3 Configure MySQL](#Configure_MySQL)

## Installation

Install and configure Apache as in the [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server").

Install and configure Tomcat as described in [Tomcat](/index.php/Tomcat "Tomcat").

## Configure Apache

### Without mod_jk

If you have mod_proxy installed (default since Apache 2.0) you only need to include two directives in your `httpd.conf` file for each web application that you wish to forward to Tomcat 5\. For example, to forward an application at context path /myapp:

```
ProxyPass         /myapp  http://localhost:8080/myapp
ProxyPassReverse  /myapp  http://localhost:8080/myapp

```

**Note**: starting from Apache 2.2 included mod_proxy supports the AJP protocol and so it's a viable alternative to mod_jk (this package). It's far easier to configure in `httpd.conf` or inside a <VirtualHost>:

```
ProxyPass / ajp://127.0.0.1:8009/APPNAME
ProxyPassReverse / ajp://127.0.0.1:8009/APPNAME

```

Instead of / you can map APPNAME to an arbitrary web path. mod_jk (described below) should be used only if its advanced features are needed.

### Using mod_jk

[Install](/index.php/Install "Install") the [mod_jk](https://aur.archlinux.org/packages/mod_jk/) package.

Edit `/etc/httpd/conf/httpd.conf`
Add this line to the end of the LoadModule section:

```
LoadModule jk_module               modules/mod_jk.so

```

Add these lines below the LoadModule section:

```
<IfModule jk_module>
    JkWorkersFile   /etc/httpd/conf/workers.properties
    JkShmFile       /var/run/shm.file
    JkShmSize       1048576
</IfModule>

```

Create the file `/etc/httpd/conf/workers.properties`. It should contain the following:

```
# Define some properties
workers.apache_log=/var/log/httpd/
workers.tomcat_home=/opt/tomcat
workers.java_home=/opt/java
ps=/
worker.list=worker2
# Define worker's properties
worker.worker2.type=ajp13
worker.worker2.host=localhost
worker.worker2.port=8009
worker.worker2.mount=/jsp-examples /jsp-examples/*

```

Restart Apache (`httpd.service`).

Visit [http://localhost/jsp-examples](http://localhost/jsp-examples) The Tomcat JSP examples should be visible.

If you want to have URLs other than examples map to tomcat, modify the .mount attribute like

```
worker.worker2.mount=/jsp-examples /jsp-examples/* /someapp /someapp/* 

```

to your `workers.properties` file. The `someapp` will map [http://localhost/someapp/](http://localhost/someapp/) to `/opt/tomcat/webapps/someapp/` as interpreted by tomcat. There are more complex workers.properties configurations; search the website for more info. [http://tomcat.apache.org/connectors-doc/reference/workers.html](http://tomcat.apache.org/connectors-doc/reference/workers.html)

## Configure MySQL

Do this section only if you want to connect to MySQL from within Tomcat or the Java environment in general.

Review the MySQL documentation and download the driver. 3.0 is a good choice: [http://www.mysql.com/products/connector-j/](http://www.mysql.com/products/connector-j/)

Untar the driver and copy `=mysql-connector-java-3.0.11-stable-bin.jar` into `/opt/java/jre/lib/ext`

```
tar xfvz mysql-connector-java-3.0.11-stable.tar.gz
cp mysql-connector-java-3.0.11-stable/mysql-connector-java-3.0.11-stable-bin.jar /opt/java/jre/lib/ext

```

Restart MySQL (`mysqld.service`).

Test that the driver can be loaded:
Save this as `~TestMysql.java`

```
    public class TestMysql {
        public static void main(String[] args) {
            try {
                Class.forName("com.mysql.jdbc.Driver").newInstance();
            } catch (Exception e) {
                System.out.println("The driver couldn't be loaded");
                return;
            }
            System.out.println("The driver was loaded");
        }
    }

```

Compile the file:

```
$ javac TestMysql.java

```

Run the file

```
$ java -classpath :/opt/java/jre/lib/ext TestMysql

```

It will output "The driver was loaded" if the driver is available, otherwise "The driver couldn't be loaded"

You should be able to use the driver using DriverManager.getConnection() in Java programs now. It should also automatically be available to Tomcat servlets and JSPs. See The Mysql Connector/J documentation for more information.