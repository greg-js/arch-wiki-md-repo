This page describes how to install Valves _HLDS_ (Half-Life Dedicated Server) for installing and running a game server for classic Half-Life 1 games.

## Installation

First, install [hlds](https://aur.archlinux.org/packages/hlds/) from the [AUR](/index.php/AUR "AUR").

Now we begin download the game files, in this example for _Counter-Strike 1.6_, by executing this command (where username and password is your steam one):

```
$ su hlds -C "/opt/hlds/steam -command update -game cstrike -dir /opt/hlds -username <username> -password <password>"

```

## Configuration

Of couse you can define the server settings in the game directory itself, for example by editing /opt/hlds/cstrike/server.cfg. Alternatively you could set the startup parameters in _/etc/conf.d/hlds_:

 `/etc/conf.d/hlds` 

```
user=hlds # this setting won't work yet
workingdir=/opt/hlds # this setting won't work yet
params="-game cstrike -autoupdate +maxplayers 20 +port 27019 +map de_aztec"
```

Be sure you open or forwarded the port, e.g. 27019 UDP+TCP correctly!

## Start the server

Starting the server is easy!

```
$ systemctl start hlds

```

To enable autostart, issue following command:

```
$ systemctl enable hlds

```