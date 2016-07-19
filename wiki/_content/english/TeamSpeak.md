From [Wikipedia:TeamSpeak](https://en.wikipedia.org/wiki/TeamSpeak "wikipedia:TeamSpeak"):

	TeamSpeak is proprietary Voice over IP software that allows computer users to speak on a chat channel with fellow computer users, much like a telephone conference call.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Client](#Client)
    *   [1.2 Server](#Server)
*   [2 Server configuration and startup](#Server_configuration_and_startup)
    *   [2.1 Configuration](#Configuration)
    *   [2.2 First startup](#First_startup)
    *   [2.3 Regular startup](#Regular_startup)
    *   [2.4 Re-Initialising Teamspeak](#Re-Initialising_Teamspeak)
*   [3 See also](#See_also)

## Installation

### Client

[Install](/index.php/Install "Install") the [teamspeak3](https://www.archlinux.org/packages/?name=teamspeak3) package.

### Server

Install the [teamspeak3-server](https://aur.archlinux.org/packages/teamspeak3-server/) package.

## Server configuration and startup

### Configuration

*   You can configure the TeamSpeak server. If you are using [systemd](/index.php/Systemd "Systemd") please check `/usr/share/doc/teamspeak3-server/doc/server_quickstart.txt` for all available command line parameters.

*   If you possess a license file please copy it to `/var/lib/teamspeak3-server/licensekey.dat`.

### First startup

With the first startup TeamSpeak creates the SQLite database at `/var/lib/teamspeak3-server/ts3server.sqlitedb` and starts logging its standard output in files in: `/var/log/teamspeak3-server/`. Teamspeak also creates the first ServerQuery administration account (the superuser) and the first virtual server including a privilege key for the server administrator of this virtual server. The privilege key is only displayed once on standard output.

*   [Start](/index.php/Start "Start") the `teamspeak3-server` service.

*   To find the privilege key:

```
$ systemctl status teamspeak3-server

```

*   Scan the output for the privilege key:

 `Example output:` 
```
● teamspeak3-server.service - TeamSpeak3 Server
   Loaded: loaded (/usr/lib/systemd/system/teamspeak3-server.service; enabled; vendor preset: disabled)
   Active: active (running) since Sat 2015-09-05 23:34:42 BST; 49min ago
 Main PID: 20126 (teamspeak3-serv)
   CGroup: /system.slice/teamspeak3-server.service
           └─20126 /usr/bin/teamspeak3-server logpath=/var/log/teamspeak3-server/ dbsqlpath=/usr/share/teamspeak3-server/sql/

Sep 05 23:34:45 Your-Hostname teamspeak3-server[20126]: serveradmin rights for your virtualserver. please
Sep 05 23:34:45 Your-Hostname teamspeak3-server[20126]: also check the doc/privilegekey_guide.txt for details.
Sep 05 23:34:45 Your-Hostname teamspeak3-server[20126]: token=lcUEBG5YVxnhzPcS5hAmOkW1Zb6KbTZbkntbPFca                                                     
Sep 05 23:34:45 Your-Hostname teamspeak3-server[20126]: ------------------------------------------------------------------
Sep 05 23:34:45 Your-Hostname teamspeak3-server[20126]: 2015-09-05 22:34:45.322567|INFO    |CIDRManager   |   | updated query_ip_whitelist ips: 127.0.0.1,
Sep 05 23:34:45 Your-Hostname teamspeak3-server[20126]: 2015-09-05 22:34:45.323806|INFO    |Query         |   | listening on 0.0.0.0:10011
Sep 05 23:34:53 Your-Hostname systemd[1]: Started TeamSpeak3 Server.

```

*   The privilege key is what token is equal to.

*   Alternatively, you can navigate to the logs directory for teamspeak3-server and read the output log directly. (This is a persistent file and will still have the first startup output here even if you have restarted the server):

**Note:** You have to be have either be logged in as root or as the teamspeak user to access this directory!

```
$ cd /var/log/teamspeak3-server
$ cat ts3server_*.log

```

Open up a Teamspeak 3 client, connect to the server and copy and paste the privilege key into the client popup.

### Regular startup

Simply [enable](/index.php/Enable "Enable") the `teamspeak3-server` service.

### Re-Initialising Teamspeak

If you have used the initial privilege key and have lost server permissions (e.g. your teamspeak 3 client with superadmin rights was uninstalled) you will have to start from scratch.

**Warning:** These steps delete your current configured TeamSpeak servers, your users, permissions and all settings.

*   [Stop](/index.php/Stop "Stop") the `teamspeak3-server` service.

*   Remove `/var/lib/teamspeak3-server/ts3server.sqlitedb`:

```
$ rm /var/lib/teamspeak3-server/ts3server.sqlitedb

```

*   Clear `/var/log/teamspeak3-server/`:

```
$ rm /var/log/teamspeak3-server/*.log

```

*   Now follow the same instructions for a first time setup.

## See also

*   [Official documentation](http://www.teamspeak.com/?page=literature)