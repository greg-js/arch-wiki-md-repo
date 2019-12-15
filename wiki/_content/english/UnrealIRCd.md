**[UnrealIRCd](https://www.unrealircd.org/)** (Unreal IRC daemon) is an open source IRC Server. Development of UnrealIRCd began in May of 1999\. Unreal was created from the Dreamforge IRCd that was formerly used by the DALnet IRC Network. Over the years, many new and exciting features have been added to Unreal. It is hard to even see a resemblance between the current Unreal and Dreamforge.

## Installing UnrealIRCd

[Install](/index.php/Install "Install") the [unrealircd](https://www.archlinux.org/packages/?name=unrealircd) package.

## Configuring (mandatory)

Many of the settings you'll want to set are very dependent on how you will use your IRC server. There is a default configuration but it doesn't work out of the box.

From there you'll want to follow the [UnrealIRCd Configuration docs](https://www.unrealircd.org/docs/Configuration) making sure to configure all of the required fields such as `me`, `admin`, `class`, etc.

Place your TLS key/cert at `/etc/unrealircd/tls/server.key.pem` and `/etc/unrealircd/tls/server.cert.pem`. You can use [Certbot](/index.php/Certbot "Certbot") to obtain a key and certificate, or generate a self-signed one as explained at [Apache HTTP Server#TLS](/index.php/Apache_HTTP_Server#TLS "Apache HTTP Server").

## Starting/Stopping the daemon

You can [start](/index.php/Start "Start") and [stop](/index.php/Stop "Stop") the UnrealIRCd daemon with the `unrealircd.service` systemd unit.

If you run into problems where the daemon will not start, try running:

```
$ sudo -u ircd unrealircd

```

It will print out the errors and what line they occur on. Often errors are due to problems in your configuration.