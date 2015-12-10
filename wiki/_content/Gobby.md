# Gobby

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

From the [project web page](http://gobby.0x539.de/trac/wiki):

_Gobby is a free collaborative editor supporting multiple documents in one session and a multi-user chat._ It uses GTK+ 2.6 as its windowing toolkit and thus integrates nicely into the GNOME desktop environment.

## Installation

Gobby .4 is in the community repo as package [gobby](https://www.archlinux.org/packages/?name=gobby). To run the Infininote server protocol without the Gobby front end install [libinfinity](https://www.archlinux.org/packages/?name=libinfinity)

The newer development version .5 (0.4.94-1 at the time of writing) is available in AUR as package [gobby-git](https://aur.archlinux.org/packages/gobby-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gobby-git)]</sup>

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

Retrieved from "[https://wiki.archlinux.org/index.php?title=Gobby&oldid=392209](https://wiki.archlinux.org/index.php?title=Gobby&oldid=392209)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Office](/index.php/Category:Office "Category:Office")