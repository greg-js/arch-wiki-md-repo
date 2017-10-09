Related articles

*   [CUPS/Printer sharing](/index.php/CUPS/Printer_sharing "CUPS/Printer sharing")
*   [CUPS/Printer-specific problems](/index.php/CUPS/Printer-specific_problems "CUPS/Printer-specific problems")
*   [CUPS/Troubleshooting](/index.php/CUPS/Troubleshooting "CUPS/Troubleshooting")
*   [Samba](/index.php/Samba "Samba")
*   [LPRng](/index.php/LPRng "LPRng")

[CUPS](http://www.cups.org/) is the standards-based, open source printing system developed by Apple Inc. for macOS® and other UNIX®-like operating systems.

## Contents

*   [1 Installation](#Installation)
*   [2 Connection Interfaces](#Connection_Interfaces)
    *   [2.1 USB](#USB)
    *   [2.2 Parallel port](#Parallel_port)
    *   [2.3 Network](#Network)
*   [3 Printer Drivers](#Printer_Drivers)
    *   [3.1 CUPS](#CUPS)
    *   [3.2 Foomatic](#Foomatic)
    *   [3.3 Manufacturer-specific drivers](#Manufacturer-specific_drivers)
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

For GTK3 printing support, see [Gtk#Printers not shown in the GTK print dialog](/index.php/Gtk#Printers_not_shown_in_the_GTK_print_dialog "Gtk").

If you intend to "print" into a PDF document, also install the [cups-pdf](https://www.archlinux.org/packages/?name=cups-pdf) package. By default, pdf files are stored in `/var/spool/cups-pdf/$USER`. The location can be changed in `/etc/cups/cups-pdf.conf`.

[Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `org.cups.cupsd.service`.

## Connection Interfaces

Additional steps for printer detection are listed below for various connection interfaces.

**Note:** CUPS helper programs are run using the `lp` group and `daemon` user. This allows the helper programs to access printer devices **and** read config files in `/etc/cups/`, which all belong to the `lp` group. This default may conflict with non-printer parallel port device access:

*   Adding extra users to the `lp` group will allow those users to read CUPS files, and
*   CUPS helpers may gain access to any non-printer parallel port devices.

If this is a concern, consider using a [Udev](/index.php/Udev "Udev") rule to assign a different group for any non-printer parallel port device ([FS#50009](https://bugs.archlinux.org/task/50009)). The group and user that CUPS uses can be changed, but the permissions of some files may need to be manually fixed.

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

[Avahi](/index.php/Avahi "Avahi") can be used to scan for printers on the local network. To use [Avahi](/index.php/Avahi "Avahi") hostnames to connect to networked printers, set up [.local hostname resolution](/index.php/Avahi#Hostname_resolution "Avahi") and [restart](/index.php/Restart "Restart") `org.cups.cupsd.service`.

If the system is connected to a networked printer using the [Samba](/index.php/Samba "Samba") protocol, or if the system is to be a print server for Windows clients, install the [samba](https://www.archlinux.org/packages/?name=samba) package.

## Printer Drivers

The drivers for a printer may come from any of the sources shown below. See [CUPS/Printer-specific problems](/index.php/CUPS/Printer-specific_problems "CUPS/Printer-specific problems") for an incomplete list of drivers that others have managed to get working.

To drive a printer, CUPS needs a PPD file and, for most printers, some [filters](https://www.cups.org/doc/man-filter.html). For details on how CUPS uses PPDs and filters, see [[1]](https://www.cups.org/doc/postscript-driver.html).

The [OpenPrinting Printer List](http://www.openprinting.org/printers) provides driver recommendations for many printers. It also supplies PPD files for each printer, but most are available through [foomatic](#Foomatic) or the recommended driver package.

When a PPD file is provided to CUPS, the CUPS server will regenerate the PPD files and save them in `/etc/cups/ppd/`.

### CUPS

CUPS provides a few PPDs and filter binaries by default, which should work out of the box. CUPS also provides support for [AirPrint](https://en.wikipedia.org/wiki/AirPrint "wikipedia:AirPrint") and [IPP Everywhere](http://www.pwg.org/ipp/everywhere.html) printers.

### Foomatic

The [foomatic](https://wiki.linuxfoundation.org/openprinting/database/foomatic) project provides PPDs for many printer drivers, both free and nonfree. For more information about what foomatic does, see [Foomatic from the Developer's View](http://www.openprinting.org/download/kpfeifle/LinuxKongress2002/Tutorial/IV.Foomatic-Developer/IV.tutorial-handout-foomatic-development.html).

To use foomatic, install [foomatic-db-engine](https://www.archlinux.org/packages/?name=foomatic-db-engine), and at least one of [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db), [foomatic-db-ppds](https://www.archlinux.org/packages/?name=foomatic-db-ppds), [foomatic-db-nonfree-ppds](https://www.archlinux.org/packages/?name=foomatic-db-nonfree-ppds), or [foomatic-db-gutenprint-ppds](https://www.archlinux.org/packages/?name=foomatic-db-gutenprint-ppds).

The foomatic PPDs may require additional filters, such as [gutenprint](https://www.archlinux.org/packages/?name=gutenprint), [ghostscript](https://www.archlinux.org/packages/?name=ghostscript), or another source (for instance [min12xxw](https://aur.archlinux.org/packages/min12xxw/)). For [ghostscript](https://www.archlinux.org/packages/?name=ghostscript), [gsfonts](https://www.archlinux.org/packages/?name=gsfonts) may also be required.

### Manufacturer-specific drivers

Many printer manufacturers supply their own Linux drivers. These are often available in the official Arch repositories or in the [AUR](/index.php/AUR "AUR").

Some of those drivers are described in more detail in [CUPS/Printer-specific problems](/index.php/CUPS/Printer-specific_problems "CUPS/Printer-specific problems").

## Printer URI

Listed below are additional steps to manually generate the URI if required.

### USB

CUPS should be able to automatically generate a URI for USB printers, for example `usb://HP/DESKJET%20940C?serial=CN16E6C364BH`.

If it doesn't, see [CUPS/Troubleshooting#USB printers](/index.php/CUPS/Troubleshooting#USB_printers "CUPS/Troubleshooting") for troubleshooting steps.

### Parallel port

The URI should be of the form `parallel:*device*`. For instance, if the printer is connected on `/dev/lp0`, use `parallel:/dev/lp0`. If you are using a USB to parallel port adapter, use `parallel:/dev/usb/lp0` as the printer URI.

### Network

If you have set up [Avahi](/index.php/Avahi "Avahi") as in [#Network](#Network), CUPS should detect the printer URI. You can also use `avahi-discover` to find the name of your printer and its address (for instance, `BRN30055C6B4C7A.local/10.10.0.155:631`).

The URI can also be generated manually, without using [Avahi](/index.php/Avahi "Avahi"). A list of the available URI schemes for networked printers is available in the CUPS documentation [[2]](https://www.cups.org/doc/network.html#PROTOCOLS). As exact details of the URIs differ between printers, check either the manual of the printer or [CUPS/Printer-specific problems](/index.php/CUPS/Printer-specific_problems "CUPS/Printer-specific problems").

Remote CUPS print servers can be accessed through a URI of the form `ipp://*hostname*:631/printers/*queue_name*`. See [CUPS/Printer sharing#Between GNU/Linux systems](/index.php/CUPS/Printer_sharing#Between_GNU.2FLinux_systems "CUPS/Printer sharing") for details on setting up the remote print server.

See [CUPS/Troubleshooting#Networking issues](/index.php/CUPS/Troubleshooting#Networking_issues "CUPS/Troubleshooting") for additional issues and solutions.

**Warning:** Avoid configuring both the server and the client with a printer filter - either the print queue on the client or the server should be 'raw'. This avoids sending a print job through the filters for a printer twice, which can cause problems (for instance, [[3]](https://bbs.archlinux.org/viewtopic.php?pid=1589908#p1589908)). See [#Usage](#Usage) for an example of setting a print queue to 'raw'.

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
# lpinfo -v # 
$ /usr/lib/cups/backend/snmp *ip_address* # Use SNMP to find a URI

```

	List the models

```
$ lpinfo -m

```

	Add a new queue

```
# lpadmin -p *queue_name* -E -v *uri* -m *model*

```

The *queue_name* is up to you. Example:

```
# lpadmin -p HP_DESKJET_940C -E -v "usb://HP/DESKJET%20940C?serial=CN16E6C364BH" -m drv:///HP/hp-deskjet_940c.ppd.gz
# lpadmin -p AirPrint -E -v "ipp://10.0.1.25/ipp/print" -m everywhere    # Driverless queue (Apple AirPrint or IPP Everywhere)
# lpadmin -p SHARED_PRINTER -m raw    # Raw queue; no PPD or filter

```

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
$ echo "Hello, world!" | lpr -p # print the result of a command. The -p switch adds a header.

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

*   **print-manager** — A tool for managing print jobs and printers ([KDE](/index.php/KDE "KDE")).

	[https://projects.kde.org/projects/kde/kdeutils/print-manager](https://projects.kde.org/projects/kde/kdeutils/print-manager) || [print-manager](https://www.archlinux.org/packages/?name=print-manager)

*   **system-config-printer** — A CUPS printer configuration tool and status applet ([GNOME](/index.php/GNOME "GNOME") and others)

	[http://cyberelk.net/tim/software/system-config-printer/](http://cyberelk.net/tim/software/system-config-printer/) || [system-config-printer](https://www.archlinux.org/packages/?name=system-config-printer)

*   **gtklp** — GTK+ interface to CUPS.

	[http://gtklp.sirtobi.com/index.shtml](http://gtklp.sirtobi.com/index.shtml) || [gtklp](https://aur.archlinux.org/packages/gtklp/)

## Configuration

The CUPS server configuration is located in `/etc/cups/cupsd.conf` and `/etc/cups/cups-files.conf`. After editing either file, [restart](/index.php/Restart "Restart") `org.cups.cupsd.service` to apply any changes. The default configuration is sufficient for most users.

[Groups](/index.php/Groups "Groups") with printer administration privileges are defined in `SystemGroup` in the `/etc/cups/cups-files.conf`. The `sys` group is used by default.

[cups](https://www.archlinux.org/packages/?name=cups) is built with [libpaper](https://www.archlinux.org/packages/?name=libpaper) support and libpaper defaults to the **Letter** paper size. To avoid having to change the paper size for each print queue you add, edit `/etc/papersize` and set your system default paper size. See [papersize(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/papersize.5).

By default, all logs are sent to files in `/var/log/cups/`. By changing the values of the `AccessLog`, `ErrorLog`, and `PageLog` directives in `/etc/cups/cups-files.conf` to `syslog`, CUPS can be made to log to the [systemd journal](/index.php/Systemd_journal "Systemd journal") instead. See [the fedora wiki page](https://fedoraproject.org/wiki/Changes/CupsJournalLogging) for information on the original proposed change.

### cups-browsed

CUPS can use [Avahi](/index.php/Avahi "Avahi") browsing to discover unknown shared printers in your network. This can be useful in large setups where the server is unknown. To use this feature, set up [.local hostname resolution](/index.php/Avahi#Hostname_resolution "Avahi"), and start both `avahi-daemon.service` and `cups-browsed.service`. Jobs are sent directly to the printer without any processing so the created queues may not work, however driverless printers such as those supporting [IPP Everywhere](http://www.pwg.org/ipp/everywhere.html) or [AirPrint](https://en.wikipedia.org/wiki/AirPrint "wikipedia:AirPrint") should work out of the box.

**Note:** Searching for network printers [may significantly increase the time it takes for your computer to boot](https://bbs.archlinux.org/viewtopic.php?pid=1720219#p1720219).

### Print servers and remote administration

See [CUPS/Printer sharing](/index.php/CUPS/Printer_sharing "CUPS/Printer sharing") and [CUPS/Printer sharing#Remote administration](/index.php/CUPS/Printer_sharing#Remote_administration "CUPS/Printer sharing").

### Allowing admin authentication through PolicyKit

[PolicyKit](/index.php/PolicyKit "PolicyKit") can be configured to allow users to configure printers using a GUI without the admin password.

**Note:** You may need to install [cups-pk-helper](https://www.archlinux.org/packages/?name=cups-pk-helper) for working this rules.

Here's an example that allows members of the wheel [group](/index.php/Group "Group") to administer printers without a password:

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

**Warning:** Accessing remote printers without a local CUPS server is not recommended by the developers. [[4]](http://www.cups.org/pipermail/cups/2015-October/027229.html)

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