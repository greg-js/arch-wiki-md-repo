# UnrealIRCd

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**[UnrealIRCd](https://www.unrealircd.org/)** (Unreal IRC daemon) is an Open Source IRC Server. Development of UnrealIRCd began in May of 1999\. Unreal was created from the Dreamforge IRCd that was formerly used by the DALnet IRC Network. Over the years, many new and exciting features have been added to Unreal. It is hard to even see a resemblance between the current Unreal and Dreamforge.

## Installing UnrealIRCd

[Install](/index.php/Install "Install") the [unrealircd](https://www.archlinux.org/packages/?name=unrealircd) package.

## Configuring (mandatory)

Many of the settings you'll want to set are very dependent on how you will use your IRC server. There is a default configuration but it doesn't work out of the box.

From there you'll want to follow the [UnrealIRCd Configuration Docs](https://www.unrealircd.org/files/docs/unreal32docs.html#configuringyourunrealircdconf) making sure to configure all of the required fields such as `me`, `admin`, `class`, etc.

Place your SSL key/cert at `/etc/unrealircd/server.key.pem` and `/etc/unrealircd/server.cert.pem`. If you do not have a proper certificate, you can generate a self-signed one, as explained at [Apache HTTP Server#TLS/SSL](/index.php/Apache_HTTP_Server#TLS.2FSSL "Apache HTTP Server"). (note that the files have to be named slightly different for UnrealIRCd)

## Starting/Stopping the daemon

You can [start](/index.php/Start "Start") and [stop](/index.php/Stop "Stop") the UnrealIRCd daemon with the `unrealircd.service` systemd unit.

If you run into problems where the daemon will not start, try running:

```
# unrealircd

```

It will print out the errors and what line they occur on. Often errors are due to problems in your configuration.

Retrieved from "[https://wiki.archlinux.org/index.php?title=UnrealIRCd&oldid=379721](https://wiki.archlinux.org/index.php?title=UnrealIRCd&oldid=379721)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Internet Relay Chat](/index.php/Category:Internet_Relay_Chat "Category:Internet Relay Chat")