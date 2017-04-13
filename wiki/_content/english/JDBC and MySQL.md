This document describes how to set up your Arch system so that MySQL databases can be accessed via Java programs.

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

To allow for network access, make sure that `/etc/mysql/my.cnf` has the following line commented out, as shown here:

```
#skip-networking

```

Then, start the MySQL [service](/index.php/Daemon "Daemon").

### Installing JDBC

Install a JDBC driver according to your MySQL variant:

*   [mariadb-jdbc](https://aur.archlinux.org/packages/mariadb-jdbc/) - for the Arch Linux endorsed server
*   [mysql-jdbc](https://aur.archlinux.org/packages/mysql-jdbc/) - for the Oracle variant

If you use the AUR packages, you will need to link the driver(s) to your JRE's external libraries directory, as follows:

For mariadb-jdbc:

```
# ln -s /usr/share/java/mariadb-jdbc/mariadb-java-client.jar /usr/lib/jvm/default/lib/ext/

```

For mysql-jdbc:

```
# ln -s /usr/share/java/mysql-jdbc/mysql-connector-java-bin.jar /usr/lib/jvm/default/lib/ext/

```

## Testing

To access MySQL's command line tool, run:

```
$ mysql

```

### Creating the test database

The following commands create a database *test*, and grant all privileges to user *foo* identified by password *bar*. Change the variables at your discretion.

```
create database *test*;
grant all privileges on *test*.* to *user*@localhost identified by "*bar*";
flush privileges;

```

Afterwards, use `Ctrl + d` to exit the command line tool.

### Creating the test program

Use a text editor to create the file `DBDemo.java` with the following code in it. You will need to change the username and password accordingly.

```
import java.sql.*;

public class DBDemo {
  public static void main(String[] args) throws SQLException, ClassNotFoundException {
    // Load the JDBC driver
    Class.forName("org.mariadb.jdbc.Driver");
    System.out.println("Driver loaded");

    // Try to connect
    Connection connection = DriverManager.getConnection
      ("jdbc:mysql://localhost/*test*", "*foo*", "*bar*");

    System.out.println("It works!");

    connection.close();
  }
}
```

If using Oracle MySQL (as opposed to MariaDB), the above class name should be set to `com.mysql.jdbc.Driver`.

### Running the program

To compile and run the program, execute:

```
$ javac DBDemo.java
$ java DBDemo

```

If all was configured correctly, you should see:

```
Driver loaded
It works!

```