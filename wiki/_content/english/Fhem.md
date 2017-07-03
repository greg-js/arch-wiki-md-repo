[FHEM](http://fhem.org) (TM) is a GPL'd perl server for house automation. It is used to automate some common tasks in the household like switching lamps / shutters / heating / etc. and to log events like temperature / humidity / power consumption.

### Installation

Install the [fhem](https://aur.archlinux.org/packages/fhem/) package.

### Configuration

Since version 5.7, the FHEM package uses a different directory layout for its files:

*   `/usr/share/fhem` Perl modules and static content
*   `/var/lib/fhem` logs and state files, changing content
*   `/etc/fhem.cfg` main configuration file

If you have a legacy configuration, please adjust your paths by putting these lines into `/etc/fhem.cfg`

If you like to edit the configuration from the web frontend, make sure the user `fhem` has write access to `/etc/fhem.cfg`.

 `/etc/fhem.cfg` 
```
attr global logfile /var/lib/fhem/fhem-%Y-%m.log
attr global modpath /usr/share/fhem
attr global statefile /var/lib/fhem/fhem.save

[...]

define Logfile FileLog /var/lib/fhem/fhem-%Y-%m.log fakelog

define autocreate autocreate
attr autocreate filelog /var/lib/fhem/%NAME-%Y.log

define eventTypes eventTypes /var/lib/fhem/eventTypes.txt

```

Please visit the [FHEM reference documentation](http://fhem.de/commandref.html) for further information.

### Startup

Just [start/enable](/index.php/Start/enable "Start/enable") `fhem.service`.