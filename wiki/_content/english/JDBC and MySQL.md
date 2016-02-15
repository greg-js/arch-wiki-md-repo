This document describes how to set up your Arch system so MySQL Databases can be accessed via Java programs.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Installing MySQL](#Installing_MySQL)
    *   [1.2 Installing JDBC](#Installing_JDBC)
*   [2 Testing](#Testing)
    *   [2.1 Creating the test database](#Creating_the_test_database)
    *   [2.2 Creating the test program](#Creating_the_test_program)
    *   [2.3 Running the program](#Running_the_program)

## Installation

### Installing MySQL

[Install](/index.php/Install "Install") a [MySQL](/index.php/MySQL "MySQL") implementation.

There are now two "fixes" you have to make. Firstly edit the file `/etc/mysql/my.cnf` to allow network access. Find the line with skip_networking in and comment it out so it looks like this:

```
#skip-networking

```

Finally start _mysql_ [service](/index.php/Daemon "Daemon") up.

### Installing JDBC

Install a JDBC driver according to your MySQL variant:

*   [mariadb-jdbc](https://aur.archlinux.org/packages/mariadb-jdbc/) - For the Arch Linux endorsed server.
*   [mysql-jdbc](https://aur.archlinux.org/packages/mysql-jdbc/) - For the Oracle variant.

You can also download the latter from [http://www.mysql.com/products/connector-j/](http://www.mysql.com/products/connector-j/) and

```
( x=mysql-connector-java-*-bin.jar; install -D $x /usr/lib/jvm/default/jre/lib/ext/${x##*/} )

```

## Testing

To access MySQL's command line tool,

```
$ mysql

```

### Creating the test database

The following commands create a database and allow a user _user_. You will need to change the user name to whatever yours is.

```
create database emotherearth;
grant all privileges on emotherearth.* to _user_@localhost identified by "_user_";
flush privileges;

```

Now press `Ctrl+d` to exit the command line tool.

### Creating the test program

Use an editor to create a file `DBDemo.java` with the following code in it. You will need to change the username and password appropriately.

```
import java.sql.*;
import java.util.Properties;
public class DBDemo
{
    // The JDBC Connector Class.
    private static final String dbClassName = "com.mysql.jdbc.Driver";
    // Connection string. emotherearth is the database the program
    // is connecting to. You can include user and password after this
    // by adding (say) ?user=paulr&password=paulr. Not recommended!
    private static final String CONNECTION =
                          "jdbc:mysql://127.0.0.1/emotherearth";
    public static void main(String[] args) throws
                             ClassNotFoundException,SQLException
    {
        System.out.println(dbClassName);
        // Class.forName(xxx) loads the jdbc classes and
        // creates a drivermanager class factory
        Class.forName(dbClassName);
        // Properties for user and password. Here the user and password are both 'paulr'
        Properties p = new Properties();
        p.put("user","paulr");
        p.put("password","paulr");
        // Now try to connect
        Connection c = DriverManager.getConnection(CONNECTION,p);
        System.out.println("It works !");
        c.close();
    }
}
```

### Running the program

To compile and run the program enter:

```
javac DBDemo.java
java DBDemo

```

and hopefully, it should print out:

```
This is the database connection
com.mysql.jdbc.Driver
It works !

```