# CUPS

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [CUPS/Printer sharing](/index.php/CUPS/Printer_sharing "CUPS/Printer sharing")
*   [CUPS/Printer-specific problems](/index.php/CUPS/Printer-specific_problems "CUPS/Printer-specific problems")
*   [CUPS/Troubleshooting](/index.php/CUPS/Troubleshooting "CUPS/Troubleshooting")
*   [Samba](/index.php/Samba "Samba")
*   [LPRng](/index.php/LPRng "LPRng")

[CUPS](https://en.wikipedia.org/wiki/CUPS "wikipedia:CUPS") is the standards-based, open source printing system developed by Apple Inc. for OS X® and other UNIX®-like operating systems.

## Contents

*   [1 Installation](#Installation)
*   [2 Printers](#Printers)
    *   [2.1 Detecting the printer](#Detecting_the_printer)
    *   [2.2 Installing the best driver](#Installing_the_best_driver)
*   [3 Configuration](#Configuration)
    *   [3.1 Local printers](#Local_printers)
        *   [3.1.1 Test the printer](#Test_the_printer)
    *   [3.2 Remote printers](#Remote_printers)
        *   [3.2.1 Local CUPS server](#Local_CUPS_server)
        *   [3.2.2 Without a local CUPS server](#Without_a_local_CUPS_server)
    *   [3.3 Printer sharing](#Printer_sharing)
    *   [3.4 Remote administration](#Remote_administration)
*   [4 Printing related applications](#Printing_related_applications)
*   [5 Usage](#Usage)
*   [6 Troubleshooting](#Troubleshooting)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [cups](https://www.archlinux.org/packages/?name=cups), [ghostscript](https://www.archlinux.org/packages/?name=ghostscript), and [gsfonts](https://www.archlinux.org/packages/?name=gsfonts) packages.

If the system is connected to a networked printer using the [Samba](/index.php/Samba "Samba") protocol, or if the system is to be a print server for Windows clients, also install the [samba](https://www.archlinux.org/packages/?name=samba) package.

If you intend to "print" into a PDF document, also install the [cups-pdf](https://www.archlinux.org/packages/?name=cups-pdf) package. By default, pdf files are stored in `/var/spool/cups-pdf/$USER`. The location can be changed in `/etc/cups/cups-pdf.conf`.

[Start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `org.cups.cupsd.service`. Optionally, CUPS can use [Avahi](/index.php/Avahi "Avahi") browsing to discover unknown shared printers in your network. This can be useful in large setups where the server is unknown. To use this feature, start `cups-browsed.service`.

## Printers

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Difficult to comprehend; needs a complete rewrite. Same for [#Configuration](#Configuration). Also, make clear that "printer detection" does not necessarily equal "working in CUPS" (Discuss in [Talk:CUPS#](https://wiki.archlinux.org/index.php/Talk:CUPS))

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [#Installation](#Installation).**

**Notes:** please use the second argument of the template to provide more detailed indications. (Discuss in [Talk:CUPS#Lost content](https://wiki.archlinux.org/index.php/Talk:CUPS#Lost_content))

### Detecting the printer

To see if your USB printer is detected:

 `lsusb` 

```
(...)
Bus 001 Device 007: ID 03f0:1004 Hewlett-Packard DeskJet 970c/970cse

```

To use a parallel port printer, the `lp`, `parport` and `parport_pc` [kernel modules](/index.php/Kernel_modules "Kernel modules") are required.

 `dmesg | grep -i print` 

```
 parport0: Printer, Hewlett-Packard HP LaserJet 2100 Series
 lp0: using parport0 (polling)

```

If you are using a USB to parallel port adapter, add the printer using a different connection type and then change DeviceID in `/etc/cups/printers.conf`:

```
DeviceID = parallel:/dev/usb/lp0

```

### Installing the best driver

CUPS already includes a few printer drivers. In that case you can just select it in the list and your printer will likely work.

If there is no driver for your printer included with CUPS, there might be a PPD available at the [OpenPrinting Printer List](http://www.openprinting.org/printers). Select the brand and type/model of the printer to find out what driver the site recommends. Download the PPD file from the site. When the CUPS web interface asks for a printer driver/PPD, select "Or Provide a PPD File: Choose file".

The website will also suggest a driver. For instance, for the HP LaserJet 5P, the site recommends the `ljet4` driver. It is possible that this driver is already included with CUPS, otherwise you will need to install it. If so, you can try out Foomatic or Gutenprint, or else find the driver in [CUPS/Printer-specific problems](/index.php/CUPS/Printer-specific_problems "CUPS/Printer-specific problems").

Foomatic

[foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db), [foomatic-db-engine](https://www.archlinux.org/packages/?name=foomatic-db-engine) and [foomatic-db-nonfree](https://www.archlinux.org/packages/?name=foomatic-db-nonfree) are database-driven systems for integrating free software printer drivers with common spoolers under Unix.

Gutenprint

The [gutenprint](https://www.archlinux.org/packages/?name=gutenprint) drivers are high-quality, open source printer drivers for various Canon, Epson, HP, Lexmark, Sony, Olympus and PCL printers supporting CUPS. They also support ghostscript, The GIMP, and other applications.

Manufacturer-specific drivers

A lot of printer manufacturers supply their own Linux drivers. Many are available in the official repositories or in the AUR. See [CUPS/Printer-specific problems](/index.php/CUPS/Printer-specific_problems "CUPS/Printer-specific problems") for a list of drivers.

## Configuration

The CUPS server configuration located in `/etc/cups/cupsd.conf`. After editing, [restart](/index.php/Restart "Restart") `org.cups.cupsd.service` to apply any changes. The default configuration is sufficient for most users.

[Groups](/index.php/Groups "Groups") with printer administration privileges are defined in `SystemGroup` in the `/etc/cups/cups-files.conf`. The `sys` group is used by default.

### Local printers

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:CUPS#](https://wiki.archlinux.org/index.php/Talk:CUPS))

To have the printer installed on the system, fire up a browser and point it to [http://localhost:631](http://localhost:631). The CUPS web interface should be displayed from which all administrative tasks can be performed.

**Note:** If an HTTPS connection to CUPS is used the first time the interface is accessed it _may_ take a very long time before the page appears. This is because the first request triggers the generation of CUPS SSL certificates which can be a time-consuming job.

Go to Administration and enter the root login and password information your GNU/Linux system. Then, when the administrative interface has been reached, click on Add Printer. A new screen will be displayed allowing the following information to be entered:

*   The _spooler name_, a short but descriptive name used on the system to identify the printer. This name should not contain spaces or any special characters. For instance, for the HP LaserJet 5P could be titled `hpljet5p`.
*   The _location_, a description where the printer is physically located (for instance "bedroom", or "in the kitchen right next to the dish washer", etc.). This is to aid in maintaining several printers.
*   The _description_ should contain a full description of the printer. A common use is the full printer name (like "HP LaserJet 5P").

The next screen requests the device the printer listens to. The choice of several devices will be presented. The next table covers a few possible devices, but the list is not exhaustive.

<table class="wikitable" style="text-align: left;">

<tbody>

<tr>

<th>Device</th>

<th>Description</th>

</tr>

<tr>

<td>AppSocket/HP JetDirect</td>

<td>This special device allows for network printers to be accessible through a HP JetDirect socket. Only specific printers include support for this option.</td>

</tr>

<tr>

<td>Internet Printing Protocol (IPP or HTTP)</td>

<td>Used reach the remote printer through the IPP protocol either directly (IPP) or through HTTP.</td>

</tr>

<tr>

<td>LPD/LPR Host or Printer</td>

<td>Select this option if the printer is remote and attached to a LPD/LPR server.</td>

</tr>

<tr>

<td>Parallel Port #1</td>

<td>Select when the printer is locally attached to a parallel port (LPT). When the printer is automatically detected its name will be appended to the device.</td>

</tr>

<tr>

<td>USB Printer #1</td>

<td>Select when the printer is locally attached to a USB port. The printer name should automatically be appended to the device name.</td>

</tr>

</tbody>

</table>

If installing a remote printer, the URL to the printer will be queried:

*   An LPD printer server requires a `lpd://hostname/queue` syntax.
*   An HP JetDirect printer requires a `socket://hostname` syntax.
*   An IPP printer requires a `ipp://hostname/printers/printername` or `http://hostname:631/printers/printername` syntax.

Next, select the printer manufacturer in the adjoining screen along with the model type and number in the subsequent screen. For many printers multiple drivers will be available. Select one now or search on [OpenPrinting Printer List](http://www.openprinting.org/printer_list.cgi) for a good driver. Drivers are easily able to be changed later.

Once the driver is selected, CUPS will inform that the printer has been added successfully to the system. Navigate to the printer management page on the administration interface and select Configure Printer to change the printer's settings (resolution, page format, ...).

#### Test the printer

To verify if the printer is working correctly, go to the printer administration page, select the printer and click on Print Test Page.

If the printer does not seem to work correctly, click on Modify Printer to reconfigure the printer. The same screens as during the first installation will appear but the defaults will now be the current configuration.

If the printer does not function, clues may be found by looking at the CUPS error log located at `/var/log/cups/error_log`. In the next example a permission error is discovered, probably due to a wrong Allow setting in the `/etc/cups/cupsd.conf` file.

```
tail /var/log/cups/error_log
 (...)
 E [11/Jun/2005:10:23:28 +0200] [Job 102] Unable to get printer status (client-error-forbidden)!

```

### Remote printers

#### Local CUPS server

Remote print servers can be accessed by adding an IPP "printer" to the local CUPS server, with a URI of `ipp://192.168.0.101:631/printers/<name-of-printer>`. See [CUPS/Printer sharing#Between GNU/Linux systems](/index.php/CUPS/Printer_sharing#Between_GNU.2FLinux_systems "CUPS/Printer sharing") for details on setting up the remote print server.

#### Without a local CUPS server

**Warning:** Accessing remote printers without a local CUPS server is not recommended by the developers [[1]](http://www.cups.org/pipermail/cups/2015-October/027229.html)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** Is Avahi really required? (Discuss in [Talk:CUPS#](https://wiki.archlinux.org/index.php/Talk:CUPS))

Install [libcups](https://www.archlinux.org/packages/?name=libcups), and set up Avahi's .local hostname resolution, otherwise the client will fail to print with an "Unable to locate printer" error. See [Avahi#Hostname resolution](/index.php/Avahi#Hostname_resolution "Avahi") for details.

There are currently two methods for accessing a remote print server. The first method involves setting `CUPS_SERVER` for each application, for instance for [Firefox](/index.php/Firefox "Firefox"):

```
# (Substitute printserver.mydomain with your print server name)
CUPS_SERVER=printserver.mydomain:port firefox
```

The second method involves editing `/etc/cups/client.conf` and setting the `ServerName` directive:

**Warning:** `/etc/cups/client.conf` is [deprecated](http://www.cups.org/documentation.php/doc-2.1/man-client.conf.html)

 `/etc/cups/client.conf` 

```
# (Substitute printserver.mydomain with your print server name)
ServerName printserver.mydomain

```

The remote system will have a default printer setting which will be used. To change the default printer, use the _lpoptions_ command.

First list the available printers:

 `lpstat -a` 

```
hpljet5p accepting requests since Jan 01 00:00
hpdjet510 accepting requests since Jan 01 00:00

```

Set the HP LaserJet 5P as the default printer:

```
lpoptions -d hpljet5p

```

### Printer sharing

See [CUPS/Printer sharing](/index.php/CUPS/Printer_sharing "CUPS/Printer sharing").

### Remote administration

If remote administration is needed, then access to the CUPS administration will need to be granted from more systems than the localhost. Add the allowed hosts to the `<Location /admin>` block in `/etc/cups/cupsd.conf`, using the same syntax as described in [CUPS/Printer sharing#Manual setup](/index.php/CUPS/Printer_sharing#Manual_setup "CUPS/Printer sharing"). Note that three levels of access can be granted:

```
<Location />           #access to the server
<Location /admin>	#access to the admin pages
<Location /admin/conf>	#access to configuration files

```

To give remote hosts access to one of these levels, add an `Allow` statement to that level's section. An `Allow` statement can take one or more of the forms listed below:

```
Allow from all
Allow from host.domain.com
Allow from *.domain.com
Allow from ip-address
Allow from ip-address/netmask
Allow from @LOCAL

```

Deny statements can also be used. For example, if wanting to give full access to all hosts on your local network interfaces, file `/etc/cups/cupsd.conf` would include this:

```
# Restrict access to the server...
# By default only localhost connections are possible
<Location />
   Order allow,deny
   **Allow from @LOCAL**
</Location>

# Restrict access to the admin pages...
<Location /admin>
   Order allow,deny
   **Allow from @LOCAL**
</Location>

# Restrict access to configuration files...
<Location /admin/conf>
   AuthType Basic
   Require user @SYSTEM
   Order allow,deny
   **Allow from @LOCAL**
</Location>

```

You might also need to add:

```
DefaultEncryption Never

```

This should avoid the error: 426 - Upgrade Required when using the CUPS web interface from a remote machine.

## Printing related applications

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [#Installation](#Installation).**

**Notes:** Or [#Usage](#Usage) maybe? (Discuss in [Talk:CUPS#](https://wiki.archlinux.org/index.php/Talk:CUPS))

*   **print-manager** — A tool for managing print jobs and printers ([KDE](/index.php/KDE "KDE")).

[https://projects.kde.org/projects/kde/kdeutils/print-manager](https://projects.kde.org/projects/kde/kdeutils/print-manager) || [print-manager](https://www.archlinux.org/packages/?name=print-manager)

*   **system-config-printer** — A CUPS printer configuration tool and status applet ([GNOME](/index.php/GNOME "GNOME") and others)

[http://cyberelk.net/tim/software/system-config-printer/](http://cyberelk.net/tim/software/system-config-printer/) || [system-config-printer](https://www.archlinux.org/packages/?name=system-config-printer)

*   **gtklp** — GTK+ interface to CUPS.

[http://gtklp.sirtobi.com/index.shtml](http://gtklp.sirtobi.com/index.shtml) || [gtklp](https://aur.archlinux.org/packages/gtklp/)<sup><small>AUR</small></sup>

If your user does not have sufficient privileges to administer the cups scheduler, system-config-printer will request the root password when it starts. To give users administrative privileges without needing root access, see [#Configuration](#Configuration).

## Usage

CUPS can be fully controlled from command-line with nice tools, _i.e._ the lp* and the cups* command families. Here follows a crash-course. See [CUPS local documentation](http://localhost:631/help/options.html) for more tips on command-line tools.

On Arch Linux, most commands support auto-completion with common shells. Also note that command-line switches cannot be grouped.

List the devices

```
# lpinfo -v

```

List the drivers

```
# lpinfo -m

```

Add a new printer

```
# lpadmin -p _printer_ -E -v _device_ -P _ppd_

```

The _printer_ is up to you. The device can be retrieved from the 'lpinfo -v' command. Example:

```
# lpadmin -p HP_DESKJET_940C -E -v "usb://HP/DESKJET%20940C?serial=CN16E6C364BH" -P /usr/share/ppd/HP/hp-deskjet_940c.ppd.gz

```

In the following, the _printer_ references the name you have used here to set up the printer.

Set the default printer

```
$ lpoptions -d _printer_

```

Check the status

```
$ lpstat -s
$ lpstat -p _printer_

```

Deactivate a printer

```
# cupsdisable _printer_

```

Activate a printer

```
# cupsenable _printer_

```

Remove a printer

First set it to reject all incoming entries:

```
# cupsreject _printer_

```

Then disable it.

```
# cupsdisable _printer_

```

Finally remove it.

```
# lpadmin -x _printer_

```

Print a file

```
$ lpr _file_
$ lpr -# 17 _file_            # print the file 17 times
$ echo "Hello, world!" | lpr -p # print the result of a command. The -p switch adds a header.

```

Check the printing queue

```
$ lpq
$ lpq -a # on all printers

```

Clear the printing queue

```
# lprm   # remove last entry only
# lprm - # remove all entries

```

## Troubleshooting

See [CUPS/Troubleshooting](/index.php/CUPS/Troubleshooting "CUPS/Troubleshooting").

## See also

*   [Official CUPS documentation](http://localhost:631/help), _locally installed_
*   [Official CUPS website](http://www.cups.org/)
*   [OpenPrinting homepage](http://www.linuxfoundation.org/collaborate/workgroups/openprinting)
*   [Gentoo's printing guide](https://wiki.gentoo.org/wiki/Printing)

Retrieved from "[https://wiki.archlinux.org/index.php?title=CUPS&oldid=409715](https://wiki.archlinux.org/index.php?title=CUPS&oldid=409715)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Printers](/index.php/Category:Printers "Category:Printers")