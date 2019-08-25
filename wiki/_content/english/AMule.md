[aMule](http://www.amule.org/) is an eMule-like client for the [eDonkey Network](https://en.wikipedia.org/wiki/eDonkey_Network "w:eDonkey Network") and [Kademlia](https://en.wikipedia.org/wiki/Kademlia "w:Kademlia") networks, supporting multiple platforms.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Services](#Services)
*   [3 Configuration](#Configuration)
*   [4 amuleweb](#amuleweb)
    *   [4.1 Create configuration files](#Create_configuration_files)
*   [5 amulegui](#amulegui)
    *   [5.1 Configuring notifications](#Configuring_notifications)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [amule](https://www.archlinux.org/packages/?name=amule) package.

`amuled` is a full featured aMule daemon, running without any user interface (GUI). It is controlled by remote access through aMuleGUI (GTK), aMuleWeb, or aMuleCmd.

## Services

The package provides two *systemd* [services](/index.php/Daemon "Daemon"): `amuled` and `amuleweb`. First you need to [configure](#Configuration) it. You need to provide passwords for external connection and admin password for `amuleweb`. Start `amuled` service and `amuleweb` if you require it. Enable them to start aMule every boot.

Once `amulweb` service is started, it is available at `[http://127.0.0.1:4711](http://127.0.0.1:4711)` (or with external address of your host).

## Configuration

At package installation time a new user account **amule** created. This account is used to run *systemd* services.

All configuration and temporary files are kept in amule home directory `/var/lib/amule` among them:

*   config file for amuled `/var/lib/amule/.aMule/amule.conf`
*   config file for amuleweb `/var/lib/amule/.aMule/remote.conf`

At the package instalation time *pacman* generates a simple `amule.conf` file with preset external connection password. The same password is used for *amuleweb* config file. One can use the password for connecting amule from other remote clients such as *amule-gui*.

To generate password, run:

```
$ echo -n *your password here* | md5sum | cut -d ' ' -f 1

```

The output of the above command is the encrypted password. Now you edit the config file by adding following lines under section `[ExternalConnect]`:

 `/var/lib/amule/.aMule/amule.conf` 
```
[ExternalConnect]
AcceptExternalConnections=1
ECPassword=<encrypted password>
```

Do not forget that all files under `/var/lib/amule` should be owned by **amule** user.

```
# chown amule:amule -R /var/lib/amule

```

## amuleweb

**Note:** *amuleweb* provides much less features than *amulegui* (and displays much less info on downloads), and it has to ask for password quite often (unless your browser could save it). It is therefore advisable to use amulegui instead (which starts up very fast as well), and if you decide to do so, you could skip this step.

### Create configuration files

Start *amuleweb* too using the user you just created to create the configuration file:

```
$ sudo -u amule amuleweb --write-config --password=*password here* --admin-pass=*web password here*

```

Note that here, the *password here* is the unencrypted password you used to configure amuled. *web password here* is the unencrypted for the log in on the web interface. This command will write configuration file as such.

**Tip:** If the default URL for nodes.dat for Kad network does not work, you can get URL from there: [[1]](http://nodes-dat.com)

## amulegui

Amulegui is a GTK interface for aMule.

### Configuring notifications

Some automatic actions settings are avaible through Settings → Events. The core command *notify-send* (requires [libnotify](https://www.archlinux.org/packages/?name=libnotify)) is useful to set notifications, using some amule variables. In example, set the *core command* in the section *Download completed* for a notification when a download is complete:

```
notify-send -i amule "%NAME completed (%SIZE bytes)"

```

The option "-i amule" includes the amule icon (a custom file may be specified adding its path between apostrophes, instead of "amule" icon filename).

## See also

*   [Getting_Started at aMule wiki](http://wiki.amule.org/wiki/Getting_Started).