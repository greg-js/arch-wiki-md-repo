*oidentd* is an [ident](https://en.wikipedia.org/wiki/Ident_protocol "wikipedia:Ident protocol") (RFC 1413 compliant) daemon that runs on Linux, Darwin, FreeBSD, OpenBSD, NetBSD and Solaris. *oidentd* can handle IP masqueraded/NAT connections on Linux, Darwin, FreeBSD (ipf only), OpenBSD and NetBSD. *oidentd* has a flexible mechanism for specifying ident responses. Users can be granted permission to specify their own ident responses. Responses can be specified according to host and port pairs.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Global configuration](#Global_configuration)
    *   [2.2 User configuration](#User_configuration)
*   [3 Starting oidentd](#Starting_oidentd)

## Installation

[Install](/index.php/Install "Install") the [oidentd](https://www.archlinux.org/packages/?name=oidentd) package.

## Configuration

With no global nor user configuration file(s), the users' ident replies will be that of their login name. This makes configuration files optional. See [oidentd.conf(5)](http://linux.die.net/man/5/oidentd.conf) for more detail.

### Global configuration

You may create the global configuration file `/etc/oidentd.conf`.

According to the manual, the following is suitable for a global configuration.

```
default {
     default {
          deny spoof
          deny spoof_all
          deny spoof_privport
          allow random
          allow random_numeric
          allow numeric
          allow hide
     }
}
user root {
     default {
          force reply "UNKNOWN"
     }
}

```

Which says, "Grant all users the ability to generate random numeric ident replies, the ability to generate numeric ident replies, and the ability to hide their identities on all ident queries. Explicitly deny the ability to spoof ident responses. And reply with `UNKNOWN' for all successful ident queries for root."

### User configuration

Additionally and/or alternatively, each user may create his own local configuration file, `$HOME/.oidentd.conf`.

A possible example follows.

```
global { reply "unknown" }
to irc.example.org { reply "example" }

```

Which says, "Reply with `unknown' to all successful ident lookups, but reply with `example' to ident lookups for connections to irc.example.org."

The global configuration file will dictate what works in the user's local configuration file.

## Starting oidentd

With *oidentd* installed and configured, [start](/index.php/Start "Start") `oidentd.socket` start the daemon. If you want to have *oidentd* start up automatically every time you start your computer, then you need to [enable](/index.php/Enable "Enable") `oidentd.socket`.