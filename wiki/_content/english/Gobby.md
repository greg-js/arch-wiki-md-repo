From the [project web page](https://gobby.github.io/):

	Gobby is a collaborative editor supporting multiple documents in one session and a multi-user chat.

## Installation

[Install](/index.php/Install "Install") the [gobby](https://www.archlinux.org/packages/?name=gobby) package. To run the Infininote server protocol without the Gobby front end install [libinfinity](https://www.archlinux.org/packages/?name=libinfinity)

## Infininote usage

To start the server portion, run

```
/usr/bin/infinoted-0.6 --security-policy=no-tls

```

The server only needs to be running on one machine.

Then, run the gobby client and connect to the server via IP or localhost.

If you would rather have encryption, TLS is available. Use:

```
infinoted-0.6 --create-key --create-certificate -k key.pem  -c cert.pem

```

The keys creation is automatic, and you can launch the server just using:

```
infinoted-0.6 -k key.pem  -c cert.pem

```

## See also

*   [Gooby GitHub wiki](https://github.com/gobby/gobby/wiki)