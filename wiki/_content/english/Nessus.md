[Nessus](https://en.wikipedia.org/wiki/Nessus_(software) is a proprietary [vulnerability scanner](https://en.wikipedia.org/wiki/Vulnerability_scanner "wikipedia:Vulnerability scanner") available free of charge for personal use. There are [over 40,000 plugins](http://www.tenable.com/plugins/) covering a large range of both local and remote flaws.

## Contents

*   [1 Installation](#Installation)
*   [2 Post-installation setup](#Post-installation_setup)
*   [3 Usage](#Usage)
*   [4 Removal](#Removal)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [nessus](https://aur.archlinux.org/packages/nessus/) package.

**Note:** As of April 26, 2016, it is no longer required to agree and download the Nessus rpm. A script will run and download the rpm from the Nessus site automatically. If it appears that nothing is happening, please be patient as the script runs wget silently. The installation will proceed after the rpm is downloaded.

## Post-installation setup

Register your email at [[1]](http://www.tenable.com/products/nessus/nessus-plugins/obtain-an-activation-code) and wait for your key to be emailed to you.

## Usage

The [nessus](https://aur.archlinux.org/packages/nessus/) package provides a `nessusd.service` unit file, see [systemd#Using units](/index.php/Systemd#Using_units "Systemd") for details.

Access the web interface at [https://localhost:8834](https://localhost:8834) and/or use the commandline interface (`/opt/nessus/sbin/nessuscli`). In most browsers, you will need to manually accept the SSL certificate you created for the server.

## Removal

The package can be removed with [pacman](/index.php/Pacman#Removing_packages "Pacman"), but files created by Nessus, such as the plugin database it downloads, must be removed manually:

**Note:** This will delete your Nessus configuration files.

```
# rm -r /opt/nessus

```

## See also

*   [The multilanguage official documentation](http://www.tenable.com/products/nessus/documentation)