*The LPRng software is an enhanced, extended, and portable implementation of the Berkeley LPR print spooler functionality. While providing the same interface and meeting RFC1179 requirements, the implementation is completely new and provides support for the following features: lightweight (no databases needed) lpr, lpc, and lprm programs; dynamic redirection of print queues; automatic job holding; highly verbose diagnostics; multiple printers serving a single queue; client programs do not need to run SUID root; greatly enhanced security checks; and a greatly improved permission and authorization mechanism.*[[1]](http://www.lprng.org/)

[LPRng](http://www.lprng.com/) is mature and stable and incorporates a flexible print filtering mechanism. It excels as a print server but can be used as a print client. It can also print from [CUPS](/index.php/CUPS "CUPS") clients installed on other machines with minor hand configuration on the CUPS side.

**Note:** A disadvantage of LPRng is that Gnome3/GTK3 (including chrome and chromium) and KDE do not support lpr printing from their GUI. However, printing to a file and then using lpr works, though it is inconvenient.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Control files](#Control_files)
        *   [2.1.1 Local configuration](#Local_configuration)
        *   [2.1.2 Remote configuration](#Remote_configuration)
        *   [2.1.3 Server configuration](#Server_configuration)
    *   [2.2 Configure printer settings (filters)](#Configure_printer_settings_.28filters.29)
        *   [2.2.1 Postscript printers](#Postscript_printers)
        *   [2.2.2 Foomatic system](#Foomatic_system)
        *   [2.2.3 Ghostscript drivers](#Ghostscript_drivers)
    *   [2.3 Printcap file](#Printcap_file)
        *   [2.3.1 Examples](#Examples)
        *   [2.3.2 Network printing advice](#Network_printing_advice)
    *   [2.4 Start the lpd daemon](#Start_the_lpd_daemon)
*   [3 Usage](#Usage)
*   [4 CUPS and LPRng](#CUPS_and_LPRng)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Gnome2/GTK2](#Gnome2.2FGTK2)
    *   [5.2 LXDE](#LXDE)
    *   [5.3 Postscript printing](#Postscript_printing)
        *   [5.3.1 Double-Sided PS](#Double-Sided_PS)

## Installation

*   Install the [lprng](https://aur.archlinux.org/packages/lprng/) package from the AUR.
*   Install optional filter packages:
    *   [poppler](https://www.archlinux.org/packages/?name=poppler)
    *   [enscript](https://www.archlinux.org/packages/?name=enscript)
    *   [ghostscript](https://www.archlinux.org/packages/?name=ghostscript)
    *   [hplip](https://www.archlinux.org/packages/?name=hplip)
    *   [foomatic-filters-lprng](https://aur.archlinux.org/packages/foomatic-filters-lprng/)

## Configuration

Configuration consists of the following steps:

*   Set up control files
*   Configure filters
*   Create a printcap file and spool directories
*   Enable and start the lpd daemon using systemctl

### Control files

#### Local configuration

Two control files must be configured:

```
/etc/lprng/lpd/lpd.conf
/etc/lprng/lpd/lpd.perms

```

#### Remote configuration

The default configurations in `/usr/share/doc/lprng` are adequate for a client computer printing to a remote printer. Copy these to `/etc/lprng/lpd/`

```
cp /usr/share/doc/lprng /etc/lprng/lpd

```

and edit it.

#### Server configuration

For a server receiving requests across the Internet, uncomment the last line in `/etc/lprng/lpd/lpd.conf` and configure permissions as documented in the comments of `/etc/lprng/lpd/lpd.perms`.

**Note:** The files `lpd.conf.sample` and `lpd.perms.sample`, located in `/usr/share/doc/lprng`, document more complex situations.

### Configure printer settings (filters)

It's fine if you just pick one of the following filter (settings) instructions. Just decide which way you want to go.

#### Postscript printers

If you have a network Postscript printer you are in luck. The sample postscript filter `/usr/share/doc/lprng/psfilter` converts PDF and text files to Postscript. Other file types are rejected.

Copy this file to `/usr/lib/lprng/lpd` and rename it as desired. Then edit it to set your paper type and your choice of single-sided/double-sided printing.

If you wish to have separate single-sided and double-sided print queues, make two copies with different names and edit appropriately.

#### Foomatic system

Another mechanism for print filtering is via the Foomatic system. This system used by [CUPS](/index.php/CUPS "CUPS"). Install [foomatic-filters-lprng](https://aur.archlinux.org/packages/foomatic-filters-lprng/) as the `foomatic-rip` program in the CUPS installation has been modified to remove LPRng support).

Use `foofilter` as described above, editing for your desired `.ppd file`. Install the `.ppd` file in conformance with the path specified in `foofilter`. (`/etc/lprng/lpd` is a good location.)

To use Hewlett Packard printers, install [hplip](https://www.archlinux.org/packages/?name=hplip) from the main distribution. This package has `.ppd` files for virtually all Hewlett Packard printers.

#### Ghostscript drivers

If you have a printer that has a Ghostscript driver, copy and edit `gsfilter` as above to set the appropriate driver and the paper type. You can discover the drivers available in your version of Ghostscript by typing the command

 `$ gs -h` 

Note that support for various printer features is typically limited and out of date with this option.

### Printcap file

The `/etc/lprng/printcap` file tells LPRng about the printers you have and the print filters that need to be used.

#### Examples

The `printcap.sample` file (in `/usr/share/doc/lprng`) provides a short tutorial as to how to set up a printcap file. The printcap fragments `printcap_server` and `printcap_client` in this directory provide additional information.

An example file may look like this for two local printers:

```
DCPJ4120DW:\
     :mx=0:\
     :sd=/var/spool/lpd/DCPJ4120DW:\
     :sh:\
     :lp=/dev/usb/lp1:\
     :if=/opt/brother/Printers/dcpj4120dw/lpd/filterdcpj4120dw:
HL2035:\
     :mx=0:\
     :sd=/var/spool/lpd/HL2035:\
     :sh:\
     :lp=/dev/usb/lp0:\
     :if=/opt/brother/Printers/brhl2035/lpd/filterHL2030:

```

#### Network printing advice

Generally, one computer should be designated as the server for one or more printers. Other client computers should send their print jobs to the server rather than the printer directly.

The rather non-obvious server setup in `printcap_server` is needed to make print filtering work on network printers, as opposed to printers attached directly to the server computer via, say, a USB port. (See the reference manual[[2]](http://www.lprng.org/LPRng-Reference/LPRng-Reference.html).)

After creating the printcap file, run the command as root

 `$ /usr/bin/checkpc -f` 

This will check your configuration and create spool directories in `/var/spool/lpd`. If `checkpc` complains about something, address the issue and rerun.

### Start the lpd daemon

LPRng runs a daemon in background called `lpd` to manage print requests. Enable and start this daemon using [systemd](/index.php/Systemd "Systemd"). If these commands complete without complaint, you should be good to go.

```
systemctl start lpd.service
systemctl enable lpd.service

```

If any configuration files are changed, one must restart `lpd`.

## Usage

The `lpr` command is the printing tool in LPRng. The general form of use is

 `$ lpr [options] [file_to_be_printed]` 

If no file is specified, input is accepted on the standard input. The most useful options are `-P printer` and `-K number_of_copies`. In the absence of the printer option, setting the environment variable `PRINTER` to the name of the printer will tell LPRng which printer to use.

Other useful commands are `lpq` (examine the print queue) and `lprm` (remove a print job from the queue). See the man pages for `lpr`, `lpq`, and `lprm`.

## CUPS and LPRng

[CUPS](/index.php/CUPS "CUPS") may be used to access a printer on a server from a client machine on which LPRng is not installed. The trick is to configure CUPS to access the printer via the `lpd` protocol. This is easy to do using the web interface to CUPS. Also, since the server as set up here does all necessary print filtering, tell CUPS to use the `raw` filter. Alternative divisions between filtering responsibilities can be devised, depending on your needs.

## Troubleshooting

### Gnome2/GTK2

Gnome2/GTK2 applications (including Firefox, Mate, LXDE, and XFCE4) still support `lpr` printing. To make this work, create the file `~/.gtkrc-2.0` in your home directory containing a single line

```
 gtk-print-backends = "file,lpr"

```

### LXDE

LXDE may create its own `~/.gtkrc-2.0` file if the look and feel of the desktop are altered -- look in this file for instructions as to how to proceed.

### Postscript printing

The filter `pdftops` from the [poppler](https://www.archlinux.org/packages/?name=poppler) package is used to create Postscript from PDF files in the print filters.

Occasionally, `pdftops` produces bad or no output. An alternative filter, `pdf2ps` from the [ghostscript](https://www.archlinux.org/packages/?name=ghostscript) package, can be substituted, but this filter has its own problems.

For a one-shot case, just use `pdf2ps` or some other converter to produce Postscript and send that to the printer.

#### Double-Sided PS

Double-sided printing of Postscript files is effected in the example filters by inserting a line of Postscript code right after the first line. For some Postscript files, this doesn't work.

In this case, send the Postscript file to a single-side print queue. The print filter `psfilter` set up for single-sided printing does no filtering of Postscript files.