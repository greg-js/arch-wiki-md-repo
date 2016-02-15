[Nessus](https://en.wikipedia.org/wiki/Nessus_(software) "wikipedia:Nessus (software)") is a proprietary [vulnerability scanner](https://en.wikipedia.org/wiki/Vulnerability_scanner "wikipedia:Vulnerability scanner") available free of charge for personal use. There are [over 40,000 plugins](http://www.tenable.com/plugins/) covering a large range of both local and remote flaws.

## Contents

*   [1 Installation](#Installation)
*   [2 Post-installation setup](#Post-installation_setup)
*   [3 Usage](#Usage)
*   [4 Removal](#Removal)
*   [5 See also](#See_also)

## Installation

Download and extract the [nessus](https://aur.archlinux.org/packages/nessus/) tarball available in the [AUR](/index.php/AUR "AUR").

Go to [http://tenable.com/products/nessus/nessus-download-agreement](http://tenable.com/products/nessus/nessus-download-agreement), agree to the license, and download the package `Nessus-6.5.2-fc20.x86_64.rpm`.

Move the RPM file into the `nessus` directory (i.e. the directory you extracted the tarball's contents to).

Then, [build and install](/index.php/Arch_User_Repository#Installing_packages "Arch User Repository") the package as usual.

## Post-installation setup

Register your email at [http://www.tenable.com/products/nessus/nessus-plugins/obtain-an-activation-code](http://www.tenable.com/products/nessus/nessus-plugins/obtain-an-activation-code) and wait for your key to be emailed to you.

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