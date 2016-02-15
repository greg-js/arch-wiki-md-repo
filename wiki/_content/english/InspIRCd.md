**InspIRCd** (Inspire IRC daemon) is a modular and lightweight IRC daemon written in C++. As it is one of the few IRCd projects written from scratch, it avoids a number of design flaws and speed issues that plague other more established IRCd projects with the same or less features, such as UnrealIRCd 3\. It's the IRCd used by the [Chatspike IRC network](http://www.chatspike.net/).

## Contents

*   [1 Installing InspIRCd](#Installing_InspIRCd)
*   [2 Configuring (mandatory)](#Configuring_.28mandatory.29)
*   [3 Loading modules](#Loading_modules)
    *   [3.1 Third-party modules](#Third-party_modules)
*   [4 Starting/Stopping the daemon](#Starting.2FStopping_the_daemon)
*   [5 External links](#External_links)

## Installing InspIRCd

**Note:** Before you begin, check that you do not have any user or group named `inspired` as the package will create and run using this user privileges (for security reasons).

Install [inspircd](https://aur.archlinux.org/packages.php?ID=22429) from the [AUR](/index.php/AUR "AUR"). Alternatively if your architecture is x86_64 you can use the binary package available [here](https://s3.amazonaws.com/sector5d/inspircd-2.0.5-1-x86_64.pkg.tar.xz). This can be installed via the following:

```
pacman -U [https://s3.amazonaws.com/sector5d/inspircd-2.0.5-1-x86_64.pkg.tar.xz](https://s3.amazonaws.com/sector5d/inspircd-2.0.5-1-x86_64.pkg.tar.xz)

```

## Configuring (mandatory)

This will depend a lot on your needs and system configuration so there's no default configuration. There is, however, an example (very well documented) configuration file located at `/etc/inspircd/inspircd.conf.example`. Read and edit this file carefully and when you're finished rename it to `inspircd.conf`. The `inspircd.conf`. file is formatted like an HTML document, which for most people is somewhat different to what they are used to. The format of an instruction within the configuration file looks like the following:

```
<tagname variable="value">

```

Note that are some `<die value="anything here">` lines in the example file to make sure you read the entire thing. You must remove these entries otherwise the server will not start. Further information is available at the [InspIRCd configuration](http://wiki.inspircd.org/Configuration) wiki page.

## Loading modules

By default, InspIRCd loads no modules. As every feature outside of [RFC 1459](http://tools.ietf.org/html/rfc1459) is actually a module, by loading no modules your ircd really won't do anything impressive. You can load modules by adding for instance:

```
<module name="m_silence.so">

```

This will load the m_silence module (which provides the somewhat standard SILENCE list facility). You must restart the daemon for changes to take effect. A list of the available modules is available at the [InspIRCd modules](http://wiki.inspircd.org/modules) wiki page.

### Third-party modules

To install a third-party module, save the `[module].cpp` within `[build-dir]/inspircd/src/inspircd/src/modules/` and continue the build process. If you have already built and installed InspIRCd and have the source files intact, compile the module with `./configure -modupdate; make` and copy to: `/usr/lib/inspircd/modules/`.

## Starting/Stopping the daemon

You can start and stop the InspIRCd daemon as usual by running:

```
sudo /etc/rc.d/inspircd {start|stop|restart}

```

The first start fails sometimes so try restarting until you get no errors. After this you shall have no further problems. The reason behind this is because of security reasons the daemon doesn't run as root as you normally would see, so the script must ensure that the user **irc** has permission to write/read the pid and log files. To start on boot just add (as always) [inspircd] to the [daemons] section in the **/etc/rc.conf file**.

## External links

*   [Inspire IRCd (website)](http://www.inspircd.org)
*   [Inspire IRCd (wiki)](http://wiki.inspircd.org/Main_Page)
*   [Inspire IRCd (irc channel)](irc://irc.inspircd.org/inspircd)