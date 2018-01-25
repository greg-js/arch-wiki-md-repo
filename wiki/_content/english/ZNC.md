Related articles

*   [PsyBNC](/index.php/PsyBNC "PsyBNC")

[ZNC](https://wiki.znc.in/ZNC) is an advanced IRC bouncer that is left connected so an IRC client can disconnect/reconnect without losing the chat session.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Webadmin Module](#Webadmin_Module)
    *   [2.2 Control Panel Module](#Control_Panel_Module)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [znc](https://www.archlinux.org/packages/?name=znc) package. The installation script will create a group and user **znc**. The default home directory for this user is `/var/lib/znc`.

Generate ZNC config as user **znc**.

```
$ sudo -u znc znc --makeconf

```

Go through the wizard and setup your preferences. [Start/enable](/index.php/Start/enable "Start/enable") `znc.service`.

## Configuration

Though you can choose to modify your configuration files manually, this requires shutting down the server first. To load a module when `znc.service` starts, add `LoadModule = <modulename>` to the configuration file: `/var/lib/znc/.znc/configs/znc.conf`.

**Warning:** **Do not edit `/var/lib/znc/.znc/configs/znc.conf` while ZNC is running**. There is a very good chance you will lose your configuration. Use the webadmin or controlpanel modules to change settings on-the-fly. They are both included in the package.

### Webadmin Module

If you enabled the web admin module, you can access it at `http://*yourhostname*:port`*, the znc port number is the same as you defined for connecting to the bouncer.*

### Control Panel Module

If you enabled the control panel module, `/msg *controlpanel help` for a list of settings while you are connected to the server.

## See also

*   [ZNC's website](http://wiki.znc.in/ZNC)