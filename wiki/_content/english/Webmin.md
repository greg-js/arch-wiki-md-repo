From the project [home page](http://www.webmin.com/):

	*Webmin is a web-based interface for system administration for Unix. Using any modern web browser, you can setup user accounts, Apache, DNS, file sharing and much more. Webmin removes the need to manually edit Unix configuration files like `/etc/passwd`, and lets you manage a system from the console or remotely. See the [standard modules](http://www.webmin.com/standard.html) page for a list of all the functions built into Webmin, or check out the [screenshots](http://www.webmin.com/demo.html).*

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Starting](#Starting)
*   [4 Usage](#Usage)

## Installation

[Install](/index.php/Install "Install") the [webmin](https://aur.archlinux.org/packages/webmin/) package from the [AUR](/index.php/AUR "AUR"). Webmin requires [perl-net-ssleay](https://www.archlinux.org/packages/?name=perl-net-ssleay) for [HTTPS](https://en.wikipedia.org/wiki/https "wikipedia:https") support.

## Configuration

To allow access to Webmin from a remote computer, configure your firewall to allow access to TCP port 10000\. You may want to configure firewall to restrict access only from certain IP addresses.

## Starting

Start webmin [service](/index.php/Daemon "Daemon") using [systemd](/index.php/Systemd "Systemd"). Enable it if you wish to load webmin at boot.

## Usage

In a web browser, enter the https address of the server with the port number 10000 to access Webmin:

```
https://*host*:10000

```

You will need to enter the root password of the server running Webmin to use the Webmin interface and administer the server.