[Nessus](https://en.wikipedia.org/wiki/Nessus_(software) is a proprietary [vulnerability scanner](https://en.wikipedia.org/wiki/Vulnerability_scanner "wikipedia:Vulnerability scanner") available free of charge for personal use. There are [over 40,000 plugins](http://www.tenable.com/plugins/) covering a large range of both local and remote flaws.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Post-installation setup](#Post-installation_setup)
*   [3 Usage](#Usage)
*   [4 License](#License)
*   [5 Plugins update](#Plugins_update)
*   [6 Removal](#Removal)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [nessus](https://aur.archlinux.org/packages/nessus/) package.

## Post-installation setup

Register your email at [[1]](http://www.tenable.com/products/nessus/nessus-plugins/obtain-an-activation-code) and wait for your key to be emailed to you.

## Usage

The [nessus](https://aur.archlinux.org/packages/nessus/) package provides a `nessusd.service` unit file, see [systemd#Using units](/index.php/Systemd#Using_units "Systemd") for details.

Access the web interface at [https://localhost:8834](https://localhost:8834) and/or use the commandline interface (`/opt/nessus/sbin/nessuscli`). In most browsers, you will need to manually accept the SSL certificate you created for the server.

## License

Stop the nessus daemon before doing anything with `/nessuscli`.

```
# systemctl stop nessusd.service

```

Activate the license:

```
# nessuscli fetch --register <Activation Code>

```

View your current license activation code:

```
# nessuscli fetch --code-in-use

```

## Plugins update

Stop the nessus daemon before doing anything with `/nessuscli`.

```
# systemctl stop nessusd.service

```

Update the plugins:

```
# nessuscli update --plugins-only

```

## Removal

The package can be removed with [pacman](/index.php/Pacman#Removing_packages "Pacman"), but files created by Nessus, such as the plugin database it downloads, must be removed manually:

**Note:** This will delete your Nessus configuration files.

```
# rm -r /opt/nessus

```

## See also

*   [The multilanguage official documentation](http://www.tenable.com/products/nessus/documentation)