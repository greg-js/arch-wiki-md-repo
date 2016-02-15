From the [project web page](http://gobby.0x539.de/trac/wiki):

_Gobby is a free collaborative editor supporting multiple documents in one session and a multi-user chat._ It uses GTK+ 2 as its windowing toolkit and thus integrates nicely into the GNOME desktop environment.

## Installation

[Install](/index.php/Install "Install") the [gobby](https://www.archlinux.org/packages/?name=gobby) package. To run the Infininote server protocol without the Gobby front end install [libinfinity](https://www.archlinux.org/packages/?name=libinfinity)

## Infininote Usage

To start the server portion, run

```
/usr/bin/infinoted-0.6 --security-policy=no-tls

```

The server only needs to be running on one machine.

Then, run the gobby client and connect to the server via IP or localhost.

If you’d rather have encryption, TLS is available. Use:

```
infinoted-0.6 --create-key --create-certificate -k key.pem  -c cert.pem

```

The keys creation is automatic, and you can launch the server just using:

```
infinoted-0.6 -k key.pem  -c cert.pem

```

## See alse

*   [infinoted wiki](http://gobby.0x539.de/trac/wiki/Infinote/Infinoted)