[sslh](https://www.rutschle.net/tech/sslh/README.html) is a ssl/ssh multiplexer.

## Installation

[Install](/index.php/Install "Install") the [sslh](https://www.archlinux.org/packages/?name=sslh) package.

## Configuration

Basic configuration file is in `/usr/share/doc/sslh/basic.cfg`.

Make the directory `/etc/sslh` and copy basic configuration file into it as `sslh.cfg`.

Create pid file `/var/run/sslh/sslh.pid` and set `nobody` as owner.

Edit sslh configuration file to have pid file pointing to the one just created.

## Running

[Start/enable](/index.php/Start/enable "Start/enable") `sslh.service`.