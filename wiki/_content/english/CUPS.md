Related articles

*   [CUPS/Printer sharing](/index.php/CUPS/Printer_sharing "CUPS/Printer sharing")
*   [CUPS/Printer-specific problems](/index.php/CUPS/Printer-specific_problems "CUPS/Printer-specific problems")
*   [CUPS/Troubleshooting](/index.php/CUPS/Troubleshooting "CUPS/Troubleshooting")
*   [Samba](/index.php/Samba "Samba")
*   [LPRng](/index.php/LPRng "LPRng")

[CUPS](https://www.cups.org/) is the standards-based, open source printing system developed by Apple Inc. for macOS® and other UNIX®-like operating systems.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Socket activation](#Socket_activation)
*   [2 Connection Interfaces](#Connection_Interfaces)
    *   [2.1 USB](#USB)
    *   [2.2 Parallel port](#Parallel_port)
    *   [2.3 Network](#Network)
*   [3 Printer Drivers](#Printer_Drivers)
    *   [3.1 CUPS](#CUPS)
    *   [3.2 OpenPrinting CUPS filters](#OpenPrinting_CUPS_filters)
    *   [3.3 Foomatic](#Foomatic)
    *   [3.4 Gutenprint](#Gutenprint)
    *   [3.5 Manufacturer-specific drivers](#Manufacturer-specific_drivers)
*   [4 Printer URI](#Printer_URI)
    *   [4.1 USB](#USB_2)
    *   [4.2 Parallel port](#Parallel_port_2)
    *   [4.3 Network](#Network_2)
*   [5 Usage](#Usage)
    *   [5.1 CLI tools](#CLI_tools)
    *   [5.2 Web interface](#Web_interface)
    *   [5.3 GUI applications](#GUI_applications)
*   [6 Configuration](#Configuration)
    *   [6.1 cups-browsed](#cups-browsed)
    *   [6.2 Print servers and remote administration](#Print_servers_and_remote_administration)
    *   [6.3 Allowing admin authentication through PolicyKit](#Allowing_admin_authentication_through_PolicyKit)
    *   [6.4 Without a local CUPS server](#Without_a_local_CUPS_server)
*   [7 Troubleshooting](#Troubleshooting)
*   [8 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [cups](https://www.archlinux.org/packages/?name=cups) package.

If you intend to "print" into a PDF document, also install the [cups-pdf](https://www.archlinux.org/packages/?name=cups-pdf) package. By default, pdf files are stored in `/var/spool/cups-pdf/*username*/`. The location can be changed in `/etc/cups/cups-pdf.conf`.

[Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `org.cups.cupsd.service`.

### Socket activation

[cups](https://www.archlinux.org/packages/?name=cups) provides a `org.cups.cupsd.socket` unit. If `org.cups.cupsd.socket` is [enabled](/index.php/Enable "Enable") (and `org.cups.cupsd.service` is [disabled](/index.php/Disable "Disable")), systemd will not start CUPS immediately, it will just listen to the appropriate sockets. Then, whenever a program attempts to connect to one of these CUPS sockets, systemd will start `org.cups.cupsd.service` and transparently hand over control of these ports to the CUPS process.

This way, CUPS is only started once a program wants to make use of the service.

## Connection Interfaces

Additional steps for printer detection are listed below for various connection interfaces.

**Note:**

*   CUPS helper programs are run using the `cups` user and group. This allows the helper programs to access printer devices and read config files in `/etc/cups/`, which are owned by the `cups` group.
*   Prior to [cups](https://www.archlinux.org/packages/?name=cups) 2.2.6-2, the `lp` group [was used instead](https://git.archlinux.org/svntogit/packages.git/commit/trunk?h=packages/cups&id=a209bf21797a239c7ddb4614f0266ba1e5238622). After the upgrade, the files in `/etc/cups` should be owned by the `cups` group and `User 209` and `Group 209` set in `/etc/cups/cups-files.conf`.

### USB

To see if your USB printer is detected:

 `$ lsusb` 
```
(...)
Bus 001 Device 007: ID 03f0:1004 Hewlett-Packard DeskJet 970c/970cse

```

### Parallel port

To use a parallel port printer, the `lp`, `parport` and `parport_pc` [kernel modules](/index.php/Kernel_modules "Kernel modules") are required.

 `$ dmesg | grep -i parport` 
```
 parport0: Printer, Hewlett-Packard HP LaserJet 2100 Series
 lp0: using parport0 (polling)

```

### Network

To discover or share printers using DNS-SD/mDNS, setup [.local hostname resolution](/index.php/Avahi#Hostname_resolution "Avahi") with [Avahi](/index.php/Avahi "Avahi") and [restart](/index.php/Restart "Restart") `org.cups.cupsd.service`.

**Note:** DNS-SD is only supported when using [Avahi](/index.php/Avahi "Avahi"). CUPS does not support using [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved") for DNS-SD, see [CUPS issue 5452](https://github.com/apple/cups/issues/5452).

To share printers with [Samba](/index.php/Samba "Samba"), e.g. if the system is to be a print server for Windows clients, the [samba](https://www.archlinux.org/packages/?name=samba) package will be required.

## Printer Drivers

The drivers for a printer may come from any of the sources shown below. See [CUPS/Printer-specific problems](/index.php/CUPS/Printer-specific_problems "CUPS/Printer-specific problems") for an incomplete list of drivers that others have managed to get working.

To drive a printer, CUPS needs a PPD file and, for most printers, some [filters](https://www.cups.org/doc/man-filter.html). For details on how CUPS uses PPDs and filters, see [[1]](https://www.cups.org/doc/postscript-driver.html).

The [OpenPrinting Printer List](http://www.openprinting.org/printers) provides driver recommendations for many printers. It also supplies PPD files for each printer, but most are available through [foomatic](#Foomatic) or the recommended driver package.

When a PPD file is provided to CUPS, the CUPS server will regenerate the PPD files and save them in `/etc/cups/ppd/`.

### CUPS

CUPS includes support for [AirPrint](https://en.wikipedia.org/wiki/AirPrint "wikipedia:AirPrint") and [IPP Everywhere](http://www.pwg.org/ipp/everywhere.html) printers.

### OpenPrinting CUPS filters

The Linux Foundation's OpenPrinting workgroup provides [cups-filters](https://wiki.linuxfoundation.org/openprinting/cups-filters). Those are backends, filters, and other binaries that were once part of CUPS but are no longer maintained by Apple. They are available in the [cups-filters](https://www.archlinux.org/packages/?name=cups-filters) package that is a dependency of [cups](https://www.archlinux.org/packages/?name=cups).

Non-PDF printers require [ghostscript](https://www.archlinux.org/packages/?name=ghostscript) to be installed. For PostScript printers [gsfonts](https://www.archlinux.org/packages/?name=gsfonts) may also be required.

### Foomatic

The Linux Foundation's OpenPrinting workgroup's [foomatic](https://wiki.linuxfoundation.org/openprinting/database/foomatic) provides PPDs for many printer drivers, both free and nonfree. For more information about what foomatic does, see [Foomatic from the Developer's View](http://www.openprinting.org/download/kpfeifle/LinuxKongress2002/Tutorial/IV.Foomatic-Developer/IV.tutorial-handout-foomatic-development.html).

To use foomatic, install [foomatic-db-engine](https://www.archlinux.org/packages/?name=foomatic-db-engine) and at least one of:

*   [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db) - a collection of XML files used by foomatic-db-engine to generate PPD files.
*   [foomatic-db-ppds](https://www.archlinux.org/packages/?name=foomatic-db-ppds) - prebuilt PPD files.
*   [foomatic-db-nonfree](https://www.archlinux.org/packages/?name=foomatic-db-nonfree) - a collection of XML files from printer manufacturers under non-free licenses used by foomatic-db-engine to generate PPD files.
*   [foomatic-db-nonfree-ppds](https://www.archlinux.org/packages/?name=foomatic-db-nonfree-ppds) - prebuilt PPD files under non-free licenses.

The foomatic PPDs may require additional filters, such as [min12xxw](https://aur.archlinux.org/packages/min12xxw/).

### Gutenprint

The [Gutenprint project](http://gimp-print.sourceforge.net/) provides drivers for Canon, Epson, Lexmark, Sony, Olympus, and PCL printers for use with CUPS and [GIMP](/index.php/GIMP "GIMP").

Install [gutenprint](https://www.archlinux.org/packages/?name=gutenprint) and [foomatic-db-gutenprint-ppds](https://www.archlinux.org/packages/?name=foomatic-db-gutenprint-ppds).

**Note:** When the Gutenprint packages get updated, the printers using Gutenprint drivers will stop working until you run `cups-genppdupdate` as root and restart CUPS. *cups-genppdupdate* will update the PPD files of the configured printers, see [cups-genppdupdate(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cups-genppdupdate.8) for more details.

### Manufacturer-specific drivers

Many printer manufacturers supply their own Linux drivers. These are often available in the official Arch repositories or in the [AUR](/index.php/AUR "AUR").

Some of those drivers are described in more detail in [CUPS/Printer-specific problems](/index.php/CUPS/Printer-specific_problems "CUPS/Printer-specific problems").

## Printer URI

Listed below are additional steps to manually generate the URI if required. Some printers or drivers may need a special URI as described in [CUPS/Printer-specific problems](/index.php/CUPS/Printer-specific_problems "CUPS/Printer-specific problems").

### USB

CUPS should be able to automatically generate a URI for USB printers, for example `usb://HP/DESKJET%20940C?serial=CN16E6C364BH`.

If it does not, see [CUPS/Troubleshooting#USB printers](/index.php/CUPS/Troubleshooting#USB_printers "CUPS/Troubleshooting") for troubleshooting steps.

### Parallel port

The URI should be of the form `parallel:*device*`. For instance, if the printer is connected on `/dev/lp0`, use `parallel:/dev/lp0`. If you are using a USB to parallel port adapter, use `parallel:/dev/usb/lp0` as the printer URI.

### Network

If you have set up [Avahi](/index.php/Avahi "Avahi") as in [#Network](#Network), CUPS should detect the printer URI. You can also use `avahi-discover` to find the name of your printer and its address (for instance, `BRN30055C6B4C7A.local/10.10.0.155:631`).

The URI can also be generated manually, without using [Avahi](/index.php/Avahi "Avahi"). A list of the available URI schemes for networked printers is available in the [CUPS documentation](https://www.cups.org/doc/network.html#PROTOCOLS). As exact details of the URIs differ between printers, check either the manual of the printer or [CUPS/Printer-specific problems](/index.php/CUPS/Printer-specific_problems "CUPS/Printer-specific problems").

The URI for printers on [SMB](/index.php/SMB "SMB") shares is described in the [smbspool(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/smbspool.8) man page.

**Note:** Any special characters in the printer URIs need to be appropriately quoted, or, if your Windows printer name or user passwords have spaces, CUPS will throw a `lpadmin: Bad device-uri` error.

For example, `smb://BEN-DESKTOP/HP Color LaserJet CP1510 series PCL6` becomes `smb://BEN-DESKTOP/HP%20Color%20LaserJet%20CP1510%20series%20PCL6`.

This result string can be obtained by running the following command:

```
$ python -c 'from urllib.parse import quote; print("smb://" + quote("BEN-DESKTOP/HP Color LaserJet CP1510 series PCL6"))'

```

Remote CUPS print servers can be accessed through a URI of the form `ipp://*hostname*:631/printers/*queue_name*`. See [CUPS/Printer sharing#Printer sharing](/index.php/CUPS/Printer_sharing#Printer_sharing "CUPS/Printer sharing") for details on setting up the remote print server.

See [CUPS/Troubleshooting#Networking issues](/index.php/CUPS/Troubleshooting#Networking_issues "CUPS/Troubleshooting") for additional issues and solutions.

**Warning:** Avoid configuring both the server and the client with a printer filter - either the print queue on the client or the server should be 'raw'. This avoids sending a print job through the filters for a printer twice, which can cause problems (for instance, [[2]](https://bbs.archlinux.org/viewtopic.php?pid=1589908#p1589908)). See [#Usage](#Usage) for an example of setting a print queue to 'raw'.

## Usage

CUPS can be fully controlled using the lp* and cups* CLI tools. Alternatively, the [#Web interface](#Web_interface) or one of several [#GUI applications](#GUI_applications) can be used.

*   The *queue* name is a short but descriptive name used on the system to identify the queue. This name should not contain spaces or any special characters. For instance, a print queue corresponding to a HP LaserJet 5P could be named "hpljet5p". More than one queue can be associated with each physical printer.
*   The *location* is a description of the printer's physical location (for instance "bedroom", or "kitchen"). This is to aid in maintaining several printers.
*   The *description* is a full description of the print queue. A common use is a full printer name (like "HP LaserJet 5P").

### CLI tools

See [CUPS local documentation](http://localhost:631/help/options.html) for more tips on the command-line tools.

**Note:** Command-line switches cannot be grouped

	List the devices

```
# lpinfo -v
$ /usr/lib/cups/backend/snmp *ip_address*  # Use SNMP to find a URI

```

	List the models

```
$ lpinfo -m

```

	Add a new queue

```
# lpadmin -p *queue_name* -E -v *uri* -m *model*

```

The *queue_name* is up to you. Examples:

```
# lpadmin -p HP_DESKJET_940C -E -v "usb://HP/DESKJET%20940C?serial=CN16E6C364BH" -m drv:///HP/hp-deskjet_940c.ppd.gz
# lpadmin -p AirPrint -E -v "ipp://10.0.1.25/ipp/print" -m everywhere    # Driverless queue (Apple AirPrint or IPP Everywhere)
# lpadmin -p SHARED_PRINTER -m raw    # Raw queue; no PPD or filter
# lpadmin -p Test_Printer -E -v "ipp://10.0.1.3/ipp/print" -m pxlmono.ppd    # Specifying a PPD instead of a model

```

**Note:** When specifying the PPD, use just the file name and not the full path (for instance, `pxlmono.ppd` instead of `/usr/share/ppd/cupsfilters/pxlmono.ppd`). Alternatively, the full path can be used with the `-P` command line switch.

	Set the default printer

```
$ lpoptions -d *queue_name*

```

	Change the options

```
$ lpoptions -p *queue_name* -l # List the options
$ lpoptions -p *queue_name* -o *option*=*value* # Set an option

```

Example:

```
$ lpoptions -p HP_DESKJET_940C -o PageSize=A4

```

	Check the status

```
$ lpstat -s
$ lpstat -p *queue_name*

```

	Deactivate a printer

```
# cupsdisable *queue_name*

```

	Activate a printer

```
# cupsenable *queue_name*

```

	Set the printer to accept jobs

```
# cupsaccept *queue_name*

```

	Remove a printer

First set it to reject all incoming entries:

```
# cupsreject *queue_name*

```

Then disable it.

```
# cupsdisable *queue_name*

```

Finally remove it.

```
# lpadmin -x *queue_name*

```

	Print a file

```
$ lpr *file*
$ lpr -# 17 *file*            # print the file 17 times
$ echo 'Hello, world!' | lpr -p # print the result of a command. The -p switch adds a header.

```

	Check the queue

```
$ lpq
$ lpq -a # on all queues

```

	Clear the queue

```
# lprm   # remove last entry only
# lprm - # remove all entries

```

	View ink levels

Install [ink](https://aur.archlinux.org/packages/ink/).

Add your user to the `lp` [user group](/index.php/User_group "User group"):

```
# usermod -aG lp <user>

```

Log out and log in again.

For usage information, use:

```
$ ink

```

### Web interface

The CUPS server can be fully administered through the web interface, available on [http://localhost:631/](http://localhost:631/).

**Note:** If an HTTPS connection to CUPS is used, it *may* take a very long time before the interface appears the first time it is accessed. This is because the first request triggers the generation of SSL certificates which can be a time-consuming job.

To perform administrative tasks from the web interface authentication is required. Authenticate either as `root` or make sure your user is member of a group with printer administration privileges, see [#Configuration](#Configuration).

	Add a queue

Go to the **Administration** page.

	Modify existing queues

Go to the **Printers** page, and select a queue to modify.

	Test a queue

Go to the **Printers** page, and select a queue.

### GUI applications

If your user does not have sufficient privileges to administer CUPS, the applications will request the root password when they start. To give users administrative privileges without needing root access, see [#Configuration](#Configuration).

*   **GtkLP** — GTK interface for CUPS.

	[https://gtklp.sirtobi.com/index.shtml](https://gtklp.sirtobi.com/index.shtml) || [gtklp](https://aur.archlinux.org/packages/gtklp/)

*   **print-manager** — Tool for managing print jobs and printers ([KDE](/index.php/KDE "KDE")).

	[https://cgit.kde.org/print-manager.git](https://cgit.kde.org/print-manager.git) || [print-manager](https://www.archlinux.org/packages/?name=print-manager)

*   **system-config-printer** — GTK printer configuration tool and status applet.

	[http://cyberelk.net/tim/software/system-config-printer/](http://cyberelk.net/tim/software/system-config-printer/) || [system-config-printer](https://www.archlinux.org/packages/?name=system-config-printer)

## Configuration

The CUPS server configuration is located in `/etc/cups/cupsd.conf` and `/etc/cups/cups-files.conf` (see [cupsd.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cupsd.conf.5) and [cups-files.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cups-files.conf.5)). After editing either file, [restart](/index.php/Restart "Restart") `org.cups.cupsd.service` to apply any changes. The default configuration is sufficient for most users.

[User groups](/index.php/User_group "User group") with printer administration privileges are defined in `SystemGroup` in the `/etc/cups/cups-files.conf`. The `sys` and `root` and `wheel` [groups](/index.php/Groups "Groups") are used by default.

[cups](https://www.archlinux.org/packages/?name=cups) is built with [libpaper](https://www.archlinux.org/packages/?name=libpaper) support and libpaper defaults to the **Letter** paper size. To avoid having to change the paper size for each print queue you add, edit `/etc/papersize` and set your system default paper size. See [papersize(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/papersize.5).

By default, all logs are sent to files in `/var/log/cups/`. By changing the values of the `AccessLog`, `ErrorLog`, and `PageLog` directives in `/etc/cups/cups-files.conf` to `syslog`, CUPS can be made to log to the [systemd journal](/index.php/Systemd_journal "Systemd journal") instead. See [the fedora wiki page](https://fedoraproject.org/wiki/Changes/CupsJournalLogging) for information on the original proposed change.

### cups-browsed

CUPS can use [Avahi](/index.php/Avahi "Avahi") browsing to discover unknown shared printers in your network. This can be useful in large setups where the server is unknown. To use this feature, set up [.local hostname resolution](/index.php/Avahi#Hostname_resolution "Avahi"), and start both `avahi-daemon.service` and `cups-browsed.service`. Jobs are sent directly to the printer without any processing so the created queues may not work, however driverless printers such as those supporting [IPP Everywhere](http://www.pwg.org/ipp/everywhere.html) or [AirPrint](https://en.wikipedia.org/wiki/AirPrint "wikipedia:AirPrint") should work out of the box.

**Note:**

*   Searching for network printers [may significantly increase the time it takes for your computer to boot](https://bbs.archlinux.org/viewtopic.php?pid=1720219#p1720219).
*   `cups-browsed.service` is only needed to dynamically add and remove printers as they appear and disappear from a network. It is not required if you simply want to add a an DNS-SD/mDNS supporting network printer to CUPS.

### Print servers and remote administration

See [CUPS/Printer sharing](/index.php/CUPS/Printer_sharing "CUPS/Printer sharing") and [CUPS/Printer sharing#Remote administration](/index.php/CUPS/Printer_sharing#Remote_administration "CUPS/Printer sharing").

### Allowing admin authentication through PolicyKit

[PolicyKit](/index.php/PolicyKit "PolicyKit") can be configured to allow users to configure printers using a GUI without the admin password.

**Note:** You may need to install [cups-pk-helper](https://www.archlinux.org/packages/?name=cups-pk-helper) for working this rules.

Here is an example that allows members of the wheel [user group](/index.php/User_group "User group") to administer printers without a password:

 `/etc/polkit-1/rules.d/49-allow-passwordless-printer-admin.rules` 
```
polkit.addRule(function(action, subject) { 
    if (action.id == "org.opensuse.cupspkhelper.mechanism.all-edit" && 
        subject.isInGroup("wheel")){ 
        return polkit.Result.YES; 
    } 
});

```

### Without a local CUPS server

CUPS can be configured to directly connect to remote printer servers instead of running a local print server. This requires [installation](/index.php/Install "Install") of the [libcups](https://www.archlinux.org/packages/?name=libcups) package. Some applications will still require the [cups](https://www.archlinux.org/packages/?name=cups) package for printing.

**Warning:** Accessing remote printers without a local CUPS server is not recommended by the developers. [[3]](https://lists.cups.org/pipermail/cups/2015-October/027229.html)

To use a remote CUPS server, set the `CUPS_SERVER` [environment variable](/index.php/Environment_variable "Environment variable") to `printerserver.mydomain:port`. For instance, if you want to use a different print server for a single [Firefox](/index.php/Firefox "Firefox") instance (substitute `printserver.mydomain:port` with your print server name/port):

```
$ CUPS_SERVER=printserver.mydomain:port firefox

```

## Troubleshooting

See [CUPS/Troubleshooting](/index.php/CUPS/Troubleshooting "CUPS/Troubleshooting").

## See also

*   [Official CUPS documentation](http://localhost:631/help), *locally installed*
*   [Wikipedia:CUPS](https://en.wikipedia.org/wiki/CUPS "wikipedia:CUPS")
*   [OpenPrinting homepage](http://www.linuxfoundation.org/collaborate/workgroups/openprinting)
*   [OpenSuSE Concepts printing guide - explains the full printing workflow](https://en.opensuse.org/Concepts_printing)
*   [OpenSuSE CUPS in a Nutshell - a quick CUPS overview](https://en.opensuse.org/SDB:CUPS_in_a_Nutshell)
*   [Gentoo's printing guide](https://wiki.gentoo.org/wiki/Printing)
*   [Debian's Printing portal - detailed technical guides](https://wiki.debian.org/Printing "debian:Printing")
*   [Debian's printing overview - a basic view of the CUPS printing system](https://wiki.debian.org/SystemPrinting "debian:SystemPrinting")