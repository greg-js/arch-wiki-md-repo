# Prosody

[Prosody](http://prosody.im/) (pronunciation: [1](http://www.merriam-webster.com/cgi-bin/audio.pl?prosod05.wav=prosody%27), [2](http://www.merriam-webster.com/cgi-bin/audio.pl?prosod04.wav=prosody%27)) is an [XMPP](http://xmpp.org/) server written in the [Lua](http://www.lua.org/) programming language. Prosody is designed to be lightweight and highly extensible. It is licensed under a permissive [MIT license](http://prosody.im/source/mit). Prosody is available for Arch Linux in the Community repository with some optional dependencies available from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

Previous experience with building and installing packages from the AUR and basic knowledge of XMPP will be very helpful when following the guide.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Optional dependencies](#Optional_dependencies)
*   [2 Configuration](#Configuration)
    *   [2.1 Logging](#Logging)
*   [3 Operation](#Operation)
    *   [3.1 Security](#Security)
        *   [3.1.1 User registration](#User_registration)
        *   [3.1.2 Stream encryption](#Stream_encryption)
    *   [3.2 Listing users](#Listing_users)
*   [4 Removal](#Removal)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Components](#Components)
        *   [5.1.1 Multi-User Chat](#Multi-User_Chat)
    *   [5.2 Prosody modules](#Prosody_modules)
    *   [5.3 Console](#Console)
*   [6 Troubleshooting](#Troubleshooting)
*   [7 Development](#Development)
*   [8 Communication](#Communication)
*   [9 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [prosody](https://www.archlinux.org/packages/?name=prosody) package.

### Optional dependencies

Prosody has optional depedencies that although not strictly required for its operation, provide useful features. These dependencies may also have to be built and installed from the AUR. If you are unfamiliar with how to build and install packages from the AUR please see [AUR User Guidelines#Installing packages](/index.php/AUR_User_Guidelines#Installing_packages "AUR User Guidelines").

NaN

NaN

NaN

**Warning:** Due to an open issue, when enabled luaevent, all s2s functionality breaks. A fix is expected in v0.10 [[1]](https://prosody.im/issues/issue/555)

NaN

NaN

## Configuration

**Note:** The `posix` module and `pidfile` setting contained in the default configuration file are required for Prosody's proper operation on Arch Linux. Please do not disable or alter them.

The main configuration file is located at `/etc/prosody/prosody.cfg.lua`, information on how to configure Prosody can be found in Prosody's [documentation](http://prosody.im/doc/configure). The syntax of the configuration file can be checked after any changes are made by running:

`$ luac5.1 -p /etc/prosody/prosody.cfg.lua`

No output means the syntax is correct.

### Logging

The Arch Linux Prosody package is pre-configured to log to syslog. Thus, by default, Prosody log messages are available in the [systemd journal](/index.php/Systemd_journal "Systemd journal").

## Operation

You can start Prosody through the included Systemd script:

`# systemctl start prosody`

To automatically start Prosody at boot execute:

`# systemctl enable prosody`

Prosody uses the default XMPP ports, 5222 and 5269, for client-to-server and server-to-server communications respectively. Configure your firewall as necessary.

You can manipulate Prosody users by using the `prosodyctl` program. To add a user:

`# prosodyctl adduser <JID>`

**Tip:** You will likely want to make at least one user an administrator by adding their Jabber ID to the `admins` list in the configuration file.

Issue `man prosodyctl` to see the man page for `prosodyctl`.

### Security

#### User registration

Prosody supports XMPP's in-band registration [standard](http://xmpp.org/extensions/xep-0077.html), which allows users to register with an XMPP client from within their client and change their passwords. While this is convenient for users it does not allow administrators to moderate the registration of new users. As such, the `register` module is enabled in the default configuration but `allow_registration` is set to `false`. This allows existing users to change their passwords from within their client but does not allow new users to register themselves.

**Tip:** If you do decide to support new in-band registrations, you will likely find the `watchregistrations` and `welcome` modules useful.

#### Stream encryption

Prosody can utilize TLS certificates to encrypt client-to-server communications (if the proper [dependencies](#Optional_dependencies) are installed). See the relevant sections of `prosody.cfg.lua` to configure Prosody to utilize these certificates.

To require encryption for client-to-server communications add the following to your configuration file:

 `/etc/prosody/prosody.cfg.lua` 

```
Host "*"

    c2s_require_encryption = true
```

Similarly, for server-to-server communications you may do:

 `/etc/prosody/prosody.cfg.lua` 

```
Host "*"

    s2s_require_encryption = true
```

While requiring client-to-server encryption is generally a good idea, please keep in mind that some popular XMPP services such as Google Talk/Gmail do not support server-to-server encryption.

### Listing users

A simple way to see a list of the registered users is

```
# ls -l /var/lib/prosody/*/accounts/*

```

alternatively, you can download the module [mod_listusers.lua](http://prosody.im/files/mod_listusers.lua), and use it as

```
# prosodyctl mod_listusers

```

## Removal

After normally uninstalling Prosody with pacman, the `/etc/prosody` and `/var/lib/prosody` directories may be left on your filesystem, and you may want to remove them if you do not plan on reinstalling Prosody.

## Tips and tricks

### Components

Prosody supports XMPP components, which provide extra services to clients. Components are either provided internally by special Prosody modules or externally using the protocol specified in [XEP-0114](http://xmpp.org/extensions/xep-0114.html).

**Note:** Components must use a different hostname from the `VirtualHost` names defined in `prosody.cfg.lua`. Attempting to host a component on the same hostname as a defined `VirtualHost` **will** result in errors.

By default, Prosody will listen for external components. If you do not plan to use any external components with Prosody you can disable this behavior by adding the following your configuration:

 `/etc/prosody/prosody.cfg.lua`  `component_ports = {}` 

#### Multi-User Chat

A common component used with XMPP servers is Multi-User Chat (MUC), which allows conferences between multiple users. MUC is provided as an internal component with Prosody. To enable MUC add the following to your configuration file:

 `/etc/prosody/prosody.cfg.lua` 

```
Component "conference.example.com" "muc"

```

This will enable the MUC component on host `conference.example.com`.

### Prosody modules

[Prosody Modules](http://code.google.com/p/prosody-modules/) is a collection of extra modules not distributed with Prosody. These modules are in various states of development from highly experimental to relatively stable. You should consult a given module's wiki page for more information. An example of an extra module is `[pastebin](http://code.google.com/p/prosody-modules/wiki/mod_pastebin)`, which when loaded will intercept long messages (for example, log file output) and replace them with a link to a pastebin hosted using Prosody's internal HTTP server (provided by the core module, `httpserver`).

To use an extra module download its raw file(s) from the source browser (when viewing a file, search for the link "View raw file"). Alternatively and likely easier, use Mercurial to clone the entire repository:

NaN

`$ hg clone https://hg.prosody.im/prosody-modules/ prosody-modules`

NaN

`$ hg clone http://0-8.prosody-modules.googlecode.com/hg/ prosody-modules`

Now you can copy the module (and any additional files it needs) to Prosody's module directory at `/usr/lib/prosody/modules`. To enable the module add it to your `modules_enabled` list in your `prosody.cfg.lua` for the host or component you wish to use it for. For example, to use the `pastebin` module on a MUC component:

 `/etc/prosody/prosody.cfg.lua` 

```
Component "conference.example.com" "muc"
    modules_enabled = { "pastebin" }
```

**Note:** An enforced Prosody convention is that modules are named `mod__foo_.lua` but simply enabled by adding `_foo_` to the `modules_enabled` list.

### Console

**Warning:** The console does not require any authentication so any user on a multi-user system can connect and issue commands on the console. Therefore it is **not** recommended to enable the `console` module on a multi-user system.

The `console` module provides a telnet console from which administrative operations and queries can be performed. You can connect to the console by issuing:

`$ telnet localhost 5582`

You of course need the `telnet` program provided by the `inetutils` package. Use the `help` command in the console to get usage help.

The console even allows you to execute Lua commands directly on the server by preceding a command with `>`. For example to see if a client connection is compressed:

`> full_sessions["romeo@montague.lit/Resource"].compressed`

Will return `true` if the connection is compressed or `nil` if it is not.

## Troubleshooting

One of Prosody's primary design principles is to be simple to use and configure. However, issues can still arise (and likely will as is the case with any complex software). If you encounter a problem there are a variety of steps you can take to narrow down the cause:

*   **Check for known issues**
    Look at the [release notes](http://prosody.im/doc/release) for your Prosody version to see if your issue is listed as a known issue. Also check the [issue tracker](http://code.google.com/p/lxmppd/issues/list) to see if your issue has already been reported.
*   **Check configuration syntax**
    Run `luac5.1 -p /etc/prosody/prosody.cfg.lua` to check for any syntax errors in your configuration file. If there is no output your syntax is fine.
*   **Check the log**
    Errors are only logged if there is a critical problem so always address those issues. If you think you have a very low level issue (like protocol compatibility between clients and servers with Prosody) then you can enable the very verbose debug level logging.
*   **Check permissions**
    The Prosody package should add a new `prosody` user and group to your system and set appropriate permissions, but it is always good to double check. Ensure that `/etc/prosody` and `/var/lib/prosody` are owned by the `prosody` user and that the user has appropriate permissions to read and write to those paths and all contained files.
*   **Check listening ports**
    When troubleshooting connection issues make sure that Prosody is actually listening for connections. You may do so by running `ss -tul` and making sure that `xmpp-client` (port 5222) and `xmpp-server` (port 5269) are listed.
*   **Restart**
    Like most things, it does not hurt to restart Prosody (`systemctl restart prosody`) to see if it resolves an issue.

If you are unable to resolve your issue yourself there are a variety of resources you can use to seek help. In order of immediacy with which you will likely receive help:

1.  XMPP Conference: `prosody@conference.prosody.im`
2.  Mailing List: [Web Interface](http://groups.google.co.uk/group/prosody-users), [Email](mailto:prosody-users@googlegroups.com)
3.  [Arch Forums](https://bbs.archlinux.org/viewforum.php?id=4) (for package issues)

## Development

Two development packages are maintained for Prosody in the AUR, [prosody-devel](https://aur.archlinux.org/packages/prosody-devel/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/prosody-devel)]</sup> and [prosody-hg](https://aur.archlinux.org/packages/prosody-hg/)<sup><small>AUR</small></sup>. `prosody-devel` tracks the latest source release of a development version (alpha, beta, release candidate) and will actually be behind the stable version if a final version of the development version is released. `prosody-hg` tracks the [Mercurial](http://www.selenic.com/mercurial/wiki/) repository tip for Prosody and will always contain the latest code as it is checked in. Both packages are built similarly to the stable package.

## Communication

*   Mailing Lists: [prosody-dev](http://groups.google.co.uk/group/prosody-dev), [prosody-users](http://groups.google.co.uk/group/prosody-users)
*   Conference: `prosody@conference.prosody.im`
*   Blog: [Prosodical Thoughts](http://blog.prosody.im/)

## See also

*   [Official documentation](https://prosody.im/doc)
*   [Prosodical Thoughts](http://blog.prosody.im/) (Blog)
*   [Issue Tracker](https://prosody.im/issues/)
*   [Prosody Modules](https://hg.prosody.im/prosody-modules/) (Extra Modules)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Prosody&oldid=414545](https://wiki.archlinux.org/index.php?title=Prosody&oldid=414545)"