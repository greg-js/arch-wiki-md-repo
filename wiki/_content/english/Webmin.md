From the project [home page](http://www.webmin.com/):

	Webmin is a web-based interface for system administration for Unix. Using any modern web browser, you can setup user accounts, Apache, DNS, file sharing and much more. Webmin removes the need to manually edit Unix configuration files like `/etc/passwd`, and lets you manage a system from the console or remotely. See the [standard modules](http://www.webmin.com/standard.html) page for a list of all the functions built into Webmin, or check out the [screenshots](http://www.webmin.com/demo.html).

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Missing Authen::PAM module](#Missing_Authen::PAM_module)

## Installation

[Install](/index.php/Install "Install") the [webmin](https://aur.archlinux.org/packages/webmin/) package from the [AUR](/index.php/AUR "AUR").

## Configuration

To allow access to Webmin from a remote computer, configure your firewall to allow access to TCP port 10000\. You may want to configure firewall to restrict access only from certain IP addresses.

## Usage

[Start](/index.php/Start "Start") `webmin.service` or [enable](/index.php/Enable "Enable") it if you wish to load webmin at boot.

In a web browser, enter the https address of the server with the port number 10000 to access Webmin:

```
https://*host*:10000

```

You will need to enter the root password of the server running Webmin to use the Webmin interface and administer the server.

## Troubleshooting

### Missing Authen::PAM module

If you did not install [webmin](https://aur.archlinux.org/packages/webmin/) via AUR then you may get an error when launching webmin such as

```
Perl module Authen::PAM needed for PAM is not installed : Can't locate Authen/PAM.pm in @INC (you may need to install the Authen::PAM module)

```

Install [perl-authen-pam](https://aur.archlinux.org/packages/perl-authen-pam/).