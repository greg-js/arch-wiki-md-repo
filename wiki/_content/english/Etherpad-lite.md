Related articles

*   [Gobby](/index.php/Gobby "Gobby")

[Etherpad-Lite](http://etherpad.org) or just Etherpad, is a collaborative, multi-user web-editor based on [Node.js](/index.php/Node.js "Node.js") with the ability to import/export various office file formats.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Database](#Database)
    *   [2.2 Address](#Address)
*   [3 Starting](#Starting)
*   [4 Known issues](#Known_issues)
    *   [4.1 Crashes on some Pads](#Crashes_on_some_Pads)
        *   [4.1.1 Lighttpd (Solved)](#Lighttpd_.28Solved.29)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [etherpad-lite](https://aur.archlinux.org/packages/etherpad-lite/) package.

## Configuration

### Database

For testing purposes, the default database backend for Etherpad is the file-based DirtyDB. With that, you can run and test Etherpad-Lite without any further configuration.

If you want to use [MySQL](/index.php/MySQL "MySQL"), [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") or [SQLite](/index.php/SQLite "SQLite"), you can adjust those settings in the settings.json file. Further, you can set a password for the administrator interface on [http://localhost:9001/admin](http://localhost:9001/admin), change port and listening address, etc.

At least, don't forget to set a sessionkey, e.g. generate with [pwgen](https://www.archlinux.org/packages/?name=pwgen) and `pwgen --symbols 10 1` and write it down to:

 `/usr/share/webapps/etherpad-lite/settings.json` 
```

"sessionKey" : "",

```

Your Etherpad installation can be extended with plugins listed at the administrator interface.

### Address

the default IP is `0.0.0.0`, change it to 127.0.0.1 as assumed later.

 `/usr/share/webapps/etherpad-lite/settings.json` 
```

  //IP and port which etherpad should bind at
  "ip": "127.0.0.1",
  "port" : 9001,

```

## Starting

[Enable](/index.php/Enable "Enable") the `etherpad-lite.service` unit. You can then access Etherpad-Lite on `[http://127.0.0.1:9001](http://127.0.0.1:9001)` or directly access a pad on `[http://127.0.0.1:9001/p/padname](http://127.0.0.1:9001/p/padname)`

## Known issues

### Crashes on some Pads

[https://github.com/ether/etherpad-lite/issues/2516#issuecomment-79659984](https://github.com/ether/etherpad-lite/issues/2516#issuecomment-79659984)

#### Lighttpd (Solved)

Due to a bug in `socket.io`, using etherpad-lite with [lighttpd](https://www.archlinux.org/packages/?name=lighttpd) as reverse proxy did not work ([nginx](https://www.archlinux.org/packages/?name=nginx) and others are not affected). This is solved as of `socket.io` version 1.0\. [[1]](https://github.com/ether/etherpad-lite/issues/28)

## See also

*   [Official Etherpad website](https://etherpad.org)
*   [Developement page on GitHub](https://github.com/ether/etherpad-lite)