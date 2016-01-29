# Znc

**ZNC** is an advanced IRC bouncer that is left connected so an IRC client can disconnect/reconnect without losing the chat session.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Webadmin Module](#Webadmin_Module)
    *   [2.2 Control Panel Module](#Control_Panel_Module)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [znc](https://www.archlinux.org/packages/?name=znc) package. The installation script will create a group and user **znc**. The default home directory for this user is `/var/lib/znc`.

By default the **znc** user has a nologin shell. Assign a shell to the user before next step:

```
# usermod -s /bin/sh znc

```

Generate ZNC config as user **znc**.

```
# su - znc
$ znc --makeconf

```

Go through the wizard and setup your preferences.

**Warning:** Do not edit configuration files manually in a text editor while ZNC is running. There is a very good chance you will lose your configuration. Use the webadmin or controlpanel modules to change settings on-the-fly. They are both included in the package.

[Enable](/index.php/Enable "Enable") `znc.service` to make it start on boot. Start and stop the ZNC daemon as usual with [systemd](/index.php/Systemd "Systemd").

## Configuration

Though you can choose to modify your configuration files manually, this requires shutting down the server first. **Do not edit configuration files while ZNC is running**.

### Webadmin Module

If you enabled the web admin module, you can access it at `http://_yourhostname_:port`, the znc port number is the same as you defined for connecting to the bouncer.

### Control Panel Module

If you enabled the control panel module, `/msg *controlpanel help` for a list of settings while you are connected to the server.

## See also

*   [ZNC's website](http://wiki.znc.in/ZNC)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Znc&oldid=379583](https://wiki.archlinux.org/index.php?title=Znc&oldid=379583)"