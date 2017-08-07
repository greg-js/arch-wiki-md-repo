[Openfire](http://www.igniterealtime.org/projects/openfire/) (previously known as Wildfire, and Jive Messenger) is an [XMPP](/index.php/XMPP "XMPP") server written in [Java](/index.php/Java "Java").

## Contents

*   [1 Installation on local PC in LAN](#Installation_on_local_PC_in_LAN)
    *   [1.1 Installation](#Installation)
    *   [1.2 Allowing connections to/from remote servers](#Allowing_connections_to.2Ffrom_remote_servers)
*   [2 Installation on remote server](#Installation_on_remote_server)
    *   [2.1 Create database on remote](#Create_database_on_remote)
    *   [2.2 Install & start Openfire on remote](#Install_.26_start_Openfire_on_remote)
    *   [2.3 Configuration (from PC)](#Configuration_.28from_PC.29)
    *   [2.4 Default settings of special interest](#Default_settings_of_special_interest)
    *   [2.5 Remote server after configuration](#Remote_server_after_configuration)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Add unix socket support](#Add_unix_socket_support)
    *   [3.2 Using multiple domains](#Using_multiple_domains)

## Installation on local PC in LAN

### Installation

Make sure the PC that is supposed to run the Openfire server is safe / behind a [firewall](/index.php/Firewall "Firewall") - as soon as it is started, the admin interfaces becomes available to anyone who has access to port 9090 and 9091.

For a local server on a PC, the integrated Database of Openfire will suffice under most circumstances. If an unusual amount of traffic is expected and the PC lacks RAM, a [MySQL](/index.php/MySQL "MySQL") database can be used instead (See [#Create database on remote](#Create_database_on_remote)).

[Install](/index.php/Install "Install") [openfire](https://www.archlinux.org/packages/?name=openfire) and start the `openfire.service`.

Open `127.0.0.1:9090` in a web browser to complete the setup process, then log in as `admin` and review the settings.

### Allowing connections to/from remote servers

Use a [Dynamic DNS](/index.php/Dynamic_DNS "Dynamic DNS") service.

## Installation on remote server

### Create database on remote

**Warning:** Changing database related settings later might require partial or complete reconfiguration even if migrated correctly.

Openfire can create its own flat file database (which is a list of mysql commands, executed and kept in RAM), that should be considered as an alternative because the java program does not support unix sockets out of the box. Check if TCP/IP is disabled:

 `$ grep -n skip-networking /etc/mysql/my.cnf`  `50:skip-networking` 

( comment out the option / use `bind-address = 127.0.0.1` instead to allow loopback TCP/IP or alternatively [#Add unix socket support](#Add_unix_socket_support) )

A working [MySQL](/index.php/MySQL "MySQL") server needs to be installed to create an external database for Openfire like this:

 `mysql` 
```
> CREATE DATABASE openfire_db;
> CREATE USER 'openfire_usr'@'localhost';
> GRANT ALL PRIVILEGES ON openfire_db.* TO 'openfire_usr'@'localhost' IDENTIFIED BY 'password';
> quit;
```

### Install & start Openfire on remote

Install the [openfire](https://www.archlinux.org/packages/?name=openfire) package.

The Openfire admin interface will listen on port `9090` and 9091 of your [server](/index.php/Server "Server") by default. Adding `<inteface>127.0.0.1</inteface>"` can probably (untested) be used to temporarily secure the server if the ports aren't properly [firewalled](/index.php/Firewall "Firewall").

 `/etc/openfire/openfire.xml` 
```
    <adminConsole>
        <!-- Disable either port by setting the value to -1 -->
        <port>9090</port>
        <securePort>9091</securePort>
        <inteface>127.0.0.1</inteface>
    </adminConsole>

```

[start](/index.php/Start "Start") `openfire.service` on the remote server. Test if the admin interface is accessible locally with [curl](https://www.archlinux.org/packages/?name=curl):

```
$ curl -v 127.0.0.1:9090 && echo Yay, it works!

```

### Configuration (from PC)

The server should not be accessible from the client yet:

```
$ curl -v example.com:9090 && echo Oh no, it works!

```

Start an [ssh](/index.php/Ssh "Ssh") tunnel from your PC to your server:

```
$ ssh -L -N 9090:localhost:9090 yourserver.example.com -p22

```

Now connecting to the remote web interface should work - use a web-browser to access `127.0.0.1:9090`, which should start setup and guide through the process.

Database for setup:

```
jdbc:mysql://localhost:3306/openfire_db?rewriteBatchedStatements=true

```

( use and the username / password as created earlier )

After the setup is complete, log in with the user name `admin` (just "admin". Not as the previous web form suggests "the email address for admin").

### Default settings of special interest

Openfire is configured "ready to go" by default. Before the server is exposed to the world, the following settings should be checked to make sure this is really what the instance is supposed to do / allow.

*   Server > Server Settings > Registration & Login:
    *   New users accounts can automatically be created by everyone through applications that support it
    *   Anonymous login without accounts is allowed
*   Server > Server Settings > Offline Messages:
    *   Each user can store up to 100kb of data
*   Server > Server Settings > File Transfer Settings:
    *   Openfire acts as a file transfer proxy

### Remote server after configuration

A list of ports can be found on the index page of the administration interface or with `netstat -tulpen | grep java`. Assuming no enabled components need UDP (like jingle media proxy?) and you don't want the admin web interface exposed to the world, the following [iptables](/index.php/Iptables "Iptables") rules should suffice to make Openfire work:

```
$ openfire_ports=(5222:5223 7070 7443 5269 5275:5276 5262:5263 7777 5229);
$ for port in $openfire_ports; do 
    echo iptables -A INPUT -p tcp --dport $port -j ACCEPT; done;
```

```
iptables -A INPUT -p tcp --dport 5222:5223 -j ACCEPT
iptables -A INPUT -p tcp --dport 7070 -j ACCEPT
iptables -A INPUT -p tcp --dport 7443 -j ACCEPT
iptables -A INPUT -p tcp --dport 5269 -j ACCEPT
iptables -A INPUT -p tcp --dport 5275:5276 -j ACCEPT
iptables -A INPUT -p tcp --dport 5262:5263 -j ACCEPT
iptables -A INPUT -p tcp --dport 7777 -j ACCEPT
iptables -A INPUT -p tcp --dport 5229 -j ACCEPT

```

## Tips and tricks

### Add unix socket support

Connecting to database via unix socket with a java application requires a jdbc driver with an implementation of socketFactory. [MariaDB] Connector/J supports auth over socket since version 1.4\. and can be install via [mariadb-jdbc](https://aur.archlinux.org/packages/mariadb-jdbc/), which also requires [jna](https://aur.archlinux.org/packages/jna/) (Java Native Access) to work with unix sockets. Install both.

 `/etc/systemd/system/openfire.service.d/override.conf` 
```
[Service]
#override ExecStart
ExecStart=
# added the 2 AUR packages to class path
ExecStart=/usr/bin/java -server -DopenfireHome=/usr/share/openfire -Dopenfire.lib.dir=/usr/lib/openfire -cp "/usr/lib/openfire/startup.jar:/usr/share/java/mariadb-jdbc/mariadb-java-client.jar:/usr/share/java/jna.jar" -jar /usr/lib/openfire/startup.jar
```

Instead this works for now (but is kind of ugly):

```
# ln /usr/share/java/mariadb-jdbc/mariadb-java-client.jar /usr/lib/openfire/
# ln /usr/share/java/jna.jar /usr/lib/openfire/

```

If openfire setup was already completed using a TCP/IP connection to the same database, switch to the new driver by changing the xml configuration:

 `/etc/openfire/openfire.xml` 
```
      <driver>org.mariadb.jdbc.Driver</driver>  
      <serverURL>jdbc:mariadb://localhost:3306/openfire_db?localSocket=/run/mysqld/mysqld.sock&writeBatchedStatements=true</serverURL>

```

When using the setup interface instead, choose "MySQK" and enter the values of driver and serverURL into the "JDBC Driver Class" and "Database URL" fields of the web form respectively.

Restart the `openfire.service` - it can be necessary to start the setup interface again ([#Configuration (from PC)](#Configuration_.28from_PC.29)) afterwards.

### Using multiple domains

Openfire does not support multiple domains / vhosts like [prosody](/index.php/Prosody "Prosody") does, but it works with an [LDAP](/index.php/LDAP "LDAP")-server that provides authentication for multiple domains.

Users from different domains can then login and communicate normally, but this is messy; side-effects may include but are not limited to:

*   unlisted users
*   need to create users manually
*   users from other domains showing up as members of default domain
*   users from other domains conflicting with same name users from other domains
*   SSL certificate errors (separate certificates for different domains not possible)