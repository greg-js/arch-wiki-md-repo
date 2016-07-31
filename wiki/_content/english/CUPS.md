[CUPS](http://www.cups.org/) is the standards-based, open source printing system developed by Apple Inc. for OS X® and other UNIX®-like operating systems.

## Contents

*   [1 Installation](#Installation)
*   [2 Connection Interfaces](#Connection_Interfaces)
    *   [2.1 USB](#USB)
    *   [2.2 Parallel port](#Parallel_port)
    *   [2.3 Local Network](#Local_Network)
*   [3 Printer Drivers](#Printer_Drivers)
    *   [3.1 CUPS Native Drivers](#CUPS_Native_Drivers)
    *   [3.2 Foomatic](#Foomatic)
    *   [3.3 Gutenprint](#Gutenprint)
    *   [3.4 OpenPrinting.org](#OpenPrinting.org)
    *   [3.5 Manufacturer-specific drivers](#Manufacturer-specific_drivers)
*   [4 Print Queues](#Print_Queues)
    *   [4.1 Remote CUPS servers](#Remote_CUPS_servers)
        *   [4.1.1 Local CUPS server](#Local_CUPS_server)
        *   [4.1.2 Without a local CUPS server](#Without_a_local_CUPS_server)
*   [5 Configuration](#Configuration)
    *   [5.1 Printer sharing](#Printer_sharing)
    *   [5.2 Remote administration](#Remote_administration)
    *   [5.3 Test the printer](#Test_the_printer)
*   [6 Usage](#Usage)
    *   [6.1 CLI tools](#CLI_tools)
    *   [6.2 GUI applications](#GUI_applications)
*   [7 Troubleshooting](#Troubleshooting)
*   [8 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [cups](https://www.archlinux.org/packages/?name=cups), [ghostscript](https://www.archlinux.org/packages/?name=ghostscript), and [gsfonts](https://www.archlinux.org/packages/?name=gsfonts) packages.

If the system is connected to a networked printer using the [Samba](/index.php/Samba "Samba") protocol, or if the system is to be a print server for Windows clients, also install the [samba](https://www.archlinux.org/packages/?name=samba) package.

If you intend to "print" into a PDF document, also install the [cups-pdf](https://www.archlinux.org/packages/?name=cups-pdf) package. By default, pdf files are stored in `/var/spool/cups-pdf/$USER`. The location can be changed in `/etc/cups/cups-pdf.conf`.

[Start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `org.cups.cupsd.service`. Optionally, CUPS can use [Avahi](/index.php/Avahi "Avahi") browsing to discover unknown shared printers in your network. This can be useful in large setups where the server is unknown. To use this feature, start `cups-browsed.service`.

## Connection Interfaces

Before CUPS can attempt to use a printer, it must be able to detect the printer. Additional steps for printer detection are listed below for various connection interfaces.

### USB

To see if your USB printer is detected:

 `lsusb` 
```
(...)
Bus 001 Device 007: ID 03f0:1004 Hewlett-Packard DeskJet 970c/970cse

```

### Parallel port

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

**Warning:** Helper programs are run using the `lp` group and `daemon` user. This allows the helper programs to access parallel port devices **and** read config files in `/etc/cups/`, which all belong to the `lp` group. Adding extra users to the `lp` group to allow them to access parallel port devices may expose sensitive information in those files. Consider using an [Udev](/index.php/Udev "Udev") rule instead. See [cups-files.conf(5)](http://man7.org/linux/man-pages/man5/cups-files.conf.5.html#) and `/etc/cups/cups-files.conf` for more information on CUPS groups and users.

### Local Network

Newer versions of CUPS tend to be good at detecting printers, and tend to pick the right hostname, but unless you have added the printer to your /etc/hosts, CUPS will fail to resolve for normal printer activities. Unless you want to make your printer ip static, Avahi can help autoresolve your printer hostname. Set up [Avahi](/index.php/Avahi "Avahi") and [.local hostname resolution](/index.php/Avahi#Hostname_resolution "Avahi") then restart CUPS by [restarting](/index.php/Restart "Restart") the `org.cups.cupsd.service` systemd unit.

You can use `avahi-discover` find the name of your printer and its address (ex. Address: BRN30055C6B4C7A.local/10.10.0.155:631) or just add .local to the hostname CUPS was using (ex. BRN30055C6B4C7A.local). Double check that everything is working with ping:

```
ping XXXXXX.local

```

should work, if it doesn't go back and make sure that Avahi is running and that you have the right hostname. After this, make sure that the hostname in the CUPS web interface is the .local hostname.

## Printer Drivers

The drivers for a printer may come from any of the sources shown below. See [CUPS/Printer-specific problems](/index.php/CUPS/Printer-specific_problems "CUPS/Printer-specific problems") for a non-comprehensive list of drivers that others have gotten to work.

Usually CUPS requires either a prebuilt PPD file including the driver or some XML data files + a PPD file generating engine to work. Even when a PPD file is provided to CUPS, the CUPS server will install its own regenerated PPD file into `/etc/cups/ppd/`

### CUPS Native Drivers

CUPS already includes a few printer drivers. In that case you can just select it in the list and your printer will likely work.

### Foomatic

[foomatic-db-engine](https://www.archlinux.org/packages/?name=foomatic-db-engine) + [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db) or [foomatic-db-nonfree](https://www.archlinux.org/packages/?name=foomatic-db-nonfree) are database-driven systems for integrating software printer drivers with common spoolers under Unix.

[foomatic-db-ppds](https://www.archlinux.org/packages/?name=foomatic-db-ppds) or [foomatic-db-nonfree-ppds](https://www.archlinux.org/packages/?name=foomatic-db-nonfree-ppds) provide prebuilt PPD files from manufacturers.

### Gutenprint

The [gutenprint](https://www.archlinux.org/packages/?name=gutenprint), [foomatic-db-gutenprint](https://www.archlinux.org/packages/?name=foomatic-db-gutenprint), [foomatic-db-gutenprint-ppds](https://www.archlinux.org/packages/?name=foomatic-db-gutenprint-ppds) drivers are high-quality, open source printer drivers for various Canon, Epson, HP, Lexmark, Sony, Olympus and PCL printers supporting CUPS. They also support ghostscript, The GIMP, and other applications.

### OpenPrinting.org

There might be a PPD available at the [OpenPrinting Printer List](http://www.openprinting.org/printers). Usually these driver files are included in the above foomatic packages. But searching for your printer model might help you decide which driver to chose from the list.

Select the brand and type/model of the printer to find out what driver the site recommends. Download the PPD file from the site. When the CUPS web interface asks for a printer driver/PPD, select "Or Provide a PPD File: Choose file".

The website will also suggest a driver. For instance, for the HP LaserJet 5P, the site recommends the `ljet4` driver. It is possible that this driver is already included with CUPS, otherwise you will need to install it through another source listed in this section.

### Manufacturer-specific drivers

Many printer manufacturers supply their own Linux drivers. These are often available in the official Arch repositories or in the [AUR](/index.php/AUR "AUR").

Some of those drivers are described in more detail in [CUPS/Printer-specific problems](/index.php/CUPS/Printer-specific_problems "CUPS/Printer-specific problems").

## Print Queues

To have the printer installed on the system, fire up a browser and point it to [http://localhost:631](http://localhost:631). The CUPS web interface should be displayed from which all administrative tasks can be performed.

**Note:** If an HTTPS connection to CUPS is used the first time the interface is accessed it *may* take a very long time before the page appears. This is because the first request triggers the generation of CUPS SSL certificates which can be a time-consuming job.

Go to Administration and enter the root login and password information your GNU/Linux system. Then, when the administrative interface has been reached, click on Add Printer. A new screen will be displayed allowing the following information to be entered:

*   The *spooler name*, a short but descriptive name used on the system to identify the printer. This name should not contain spaces or any special characters. For instance, for the HP LaserJet 5P could be titled `hpljet5p`.
*   The *location*, a description where the printer is physically located (for instance "bedroom", or "in the kitchen right next to the dish washer", etc.). This is to aid in maintaining several printers.
*   The *description* should contain a full description of the printer. A common use is the full printer name (like "HP LaserJet 5P").

The next screen requests the device the printer listens to.

If installing a remote printer, the URL to the printer will be queried:

*   An LPD printer server requires a `lpd://hostname/queue` syntax.
*   An HP JetDirect printer requires a `socket://hostname` syntax.
*   An IPP printer requires a `ipp://hostname/printers/printername` or `http://hostname:631/printers/printername` syntax.

Detection of local printers should be automatic, and the printer name should automatically be appended to the device name.

On the next screen, you can select the printer manufacturer along with the model type and number. Remember that you need to have downloaded/installed the correct printer driver in order to see your printer type among the others in the list. See the previous section on "Printer Drivers" to do this.

Once the driver is selected, CUPS will inform that the printer has been added successfully to the system. Navigate to the printer management page on the administration interface and select Configure Printer to change the printer's settings (resolution, page format, ...).

### Remote CUPS servers

**Note:** As of CUPS version 1.6, the client defaults to IPP 2.0\. If the server uses CUPS <= 1.5 / IPP <= 1.1, the client does not downgrade the protocol automatically and thus cannot communicate with the server. A workaround (undocumented as of 2013-05-07, but see [this bug report](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=704238)) is to put the following in `/etc/cups/client.conf`: ServerName HOSTNAME-OR-IP-ADDRESS[:PORT]/version=1.1

#### Local CUPS server

Remote print servers can be accessed by adding an IPP "printer" to the local CUPS server, with a URI of `ipp://192.168.0.101:631/printers/<name-of-printer>`. See [CUPS/Printer sharing#Between GNU/Linux systems](/index.php/CUPS/Printer_sharing#Between_GNU.2FLinux_systems "CUPS/Printer sharing") for details on setting up the remote print server.

**Note:** Avoid configuring both the server and the client with a printer filter - either the print queue on the client or the server should be 'raw'. This avoids sending a print job through the filters for a printer twice, which can cause problems (for instance, [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1589908#p1589908)). See [#Usage](#Usage) for an example of setting a print queue to 'raw'.

#### Without a local CUPS server

**Warning:** Accessing remote printers without a local CUPS server is not recommended by the developers [[2]](http://www.cups.org/pipermail/cups/2015-October/027229.html)

Install [libcups](https://www.archlinux.org/packages/?name=libcups). To print from some applications, you will also need to install [cups](https://www.archlinux.org/packages/?name=cups).

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

The remote system's default printer setting will be used by default.

## Configuration

The CUPS server configuration is located in `/etc/cups/cupsd.conf` and `/etc/cups/cups-files.conf`. After editing either file, [restart](/index.php/Restart "Restart") `org.cups.cupsd.service` to apply any changes. The default configuration is sufficient for most users.

[Groups](/index.php/Groups "Groups") with printer administration privileges are defined in `SystemGroup` in the `/etc/cups/cups-files.conf`. The `sys` group is used by default.

[cups](https://www.archlinux.org/packages/?name=cups) is built with [libpaper](https://www.archlinux.org/packages/?name=libpaper) support and libpaper defaults to **Letter** paper size. To avoid having to change paper size for each printer you add, edit `/etc/papersize` and set your system default paper size. See papersize(5).

### Printer sharing

See [CUPS/Printer sharing](/index.php/CUPS/Printer_sharing "CUPS/Printer sharing").

### Remote administration

Once the server is set up as described in [CUPS/Printer sharing#Between GNU/Linux systems](/index.php/CUPS/Printer_sharing#Between_GNU.2FLinux_systems "CUPS/Printer sharing"), it can also be configured so that it can be remotely administered. If this is needed, then access to the CUPS administration will need to be granted from more systems than the localhost. Add the allowed hosts to the `<Location /admin>` block in `/etc/cups/cupsd.conf`, using the same syntax as described in [CUPS/Printer sharing#Manual setup](/index.php/CUPS/Printer_sharing#Manual_setup "CUPS/Printer sharing"). Note that three levels of access can be granted:

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

### Test the printer

To verify if the printer is working correctly, go to the printer administration page, select the printer and click on Print Test Page.

If the printer does not work, see [CUPS/Troubleshooting](/index.php/CUPS/Troubleshooting "CUPS/Troubleshooting").

## Usage

CUPS can be fully controlled using the lp* and cups* command-line tools. Alternatively, several GUI applications exist.

### CLI tools

See [CUPS local documentation](http://localhost:631/help/options.html) for more tips on the command-line tools.

**Note:** Command-line switches cannot be grouped

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
# lpadmin -p *printer_name* -E -v *device* -P *ppd*

```

The *printer_name* is up to you. The device can be retrieved from the 'lpinfo -v' command. Example:

```
# lpadmin -p HP_DESKJET_940C -E -v "usb://HP/DESKJET%20940C?serial=CN16E6C364BH" -P /usr/share/ppd/HP/hp-deskjet_940c.ppd.gz

```

	Make the printer use the raw driver

```
# lpadmin -p *printer_name* -m raw

```

	Set the default printer

```
$ lpoptions -d *printer_name*

```

	Check the status

```
$ lpstat -s
$ lpstat -p *printer_name*

```

	Deactivate a printer

```
# cupsdisable *printer_name*

```

	Activate a printer

```
# cupsenable *printer_name*

```

	Remove a printer

First set it to reject all incoming entries:

```
# cupsreject *printer_name*

```

Then disable it.

```
# cupsdisable *printer_name*

```

Finally remove it.

```
# lpadmin -x *printer_name*

```

	Print a file

```
$ lpr *file*
$ lpr -# 17 *file*            # print the file 17 times
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

### GUI applications

If your user does not have sufficient privileges to administer CUPS, the applications will request the root passwords when they start. To give users administrative privileges without needing root access, see [#Configuration](#Configuration).

*   **print-manager** — A tool for managing print jobs and printers ([KDE](/index.php/KDE "KDE")).

	[https://projects.kde.org/projects/kde/kdeutils/print-manager](https://projects.kde.org/projects/kde/kdeutils/print-manager) || [print-manager](https://www.archlinux.org/packages/?name=print-manager)

*   **system-config-printer** — A CUPS printer configuration tool and status applet ([GNOME](/index.php/GNOME "GNOME") and others)

	[http://cyberelk.net/tim/software/system-config-printer/](http://cyberelk.net/tim/software/system-config-printer/) || [system-config-printer](https://www.archlinux.org/packages/?name=system-config-printer)

*   **gtklp** — GTK+ interface to CUPS.

	[http://gtklp.sirtobi.com/index.shtml](http://gtklp.sirtobi.com/index.shtml) || [gtklp](https://aur.archlinux.org/packages/gtklp/)

## Troubleshooting

See [CUPS/Troubleshooting](/index.php/CUPS/Troubleshooting "CUPS/Troubleshooting").

## See also

*   [Official CUPS documentation](http://localhost:631/help), *locally installed*
*   [Wikipedia:CUPS](https://en.wikipedia.org/wiki/CUPS "wikipedia:CUPS")
*   [OpenPrinting homepage](http://www.linuxfoundation.org/collaborate/workgroups/openprinting)
*   [OpenSuSE Concepts printing guide - explains the full printing workflow](https://en.opensuse.org/Concepts_printing)
*   [OpenSuSE CUPS in a Nutshell - a quick CUPS overwiev](https://en.opensuse.org/SDB:CUPS_in_a_Nutshell)
*   [Gentoo's printing guide](https://wiki.gentoo.org/wiki/Printing)