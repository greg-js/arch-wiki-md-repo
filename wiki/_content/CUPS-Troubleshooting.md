# CUPS/Troubleshooting

**Note:** See [CUPS](/index.php/CUPS "CUPS") for the main article.

This article covers all non-specific (ie, not related to any one printer) troubleshooting of CUPS and printing drivers (but not problems related to printer sharing), including methods of determining the exact nature of the problem, and of solving the identified problem.

## Contents

*   [1 Introduction](#Introduction)
*   [2 Problems resulting from upgrades](#Problems_resulting_from_upgrades)
    *   [2.1 CUPS stops working](#CUPS_stops_working)
    *   [2.2 All jobs are "stopped"](#All_jobs_are_.22stopped.22)
    *   [2.3 All jobs are "The printer is not responding"](#All_jobs_are_.22The_printer_is_not_responding.22)
    *   [2.4 The PPD version is not compatible with gutenprint](#The_PPD_version_is_not_compatible_with_gutenprint)
*   [3 Networking issues](#Networking_issues)
    *   [3.1 CUPS identifies printer but cannot connect to it](#CUPS_identifies_printer_but_cannot_connect_to_it)
    *   [3.2 Finding URIs for Windows print servers](#Finding_URIs_for_Windows_print_servers)
*   [4 USB printers](#USB_printers)
*   [5 HP issues](#HP_issues)
    *   [5.1 HPLIP printer sends "/usr/lib/cups/backend/hp failed" error](#HPLIP_printer_sends_.22.2Fusr.2Flib.2Fcups.2Fbackend.2Fhp_failed.22_error)
    *   [5.2 HPLIP printer claims job is complete but printer does nothing](#HPLIP_printer_claims_job_is_complete_but_printer_does_nothing)
    *   [5.3 hp-setup asks to specify the PPD file for the discovered printer](#hp-setup_asks_to_specify_the_PPD_file_for_the_discovered_printer)
    *   [5.4 I have installed Qt, but hp-setup reports "Qt/PyQt 4 initialization failed"](#I_have_installed_Qt.2C_but_hp-setup_reports_.22Qt.2FPyQt_4_initialization_failed.22)
    *   [5.5 hp-setup finds the printer automatically but reports "Unable to communicate with device" when printing test page immediately afterwards](#hp-setup_finds_the_printer_automatically_but_reports_.22Unable_to_communicate_with_device.22_when_printing_test_page_immediately_afterwards)
    *   [5.6 hp-toolbox sends an error, "Unable to communicate with device"](#hp-toolbox_sends_an_error.2C_.22Unable_to_communicate_with_device.22)
    *   [5.7 CUPS returns '"foomatic-rip" not available/stopped with status 3' with a HP printer](#CUPS_returns_.27.22foomatic-rip.22_not_available.2Fstopped_with_status_3.27_with_a_HP_printer)
    *   [5.8 HPLIP 3.13: Plugin is installed, but HP Device Manager complains it is not](#HPLIP_3.13:_Plugin_is_installed.2C_but_HP_Device_Manager_complains_it_is_not)
    *   [5.9 Printer does not print with an "Filter failed" message on CUPS web interface (HP printer)](#Printer_does_not_print_with_an_.22Filter_failed.22_message_on_CUPS_web_interface_.28HP_printer.29)
        *   [5.9.1 Bad permissions](#Bad_permissions)
        *   [5.9.2 Avahi not enabled](#Avahi_not_enabled)
        *   [5.9.3 Out-of-date plugin](#Out-of-date_plugin)
    *   [5.10 CUPS prints only an empty and an error-message page on HP LaserJet](#CUPS_prints_only_an_empty_and_an_error-message_page_on_HP_LaserJet)
*   [6 Other](#Other)
    *   [6.1 Printer "Paused" or "Stopped" with Status "Rendering completed"](#Printer_.22Paused.22_or_.22Stopped.22_with_Status_.22Rendering_completed.22)
        *   [6.1.1 Explanation of the GID issue](#Explanation_of_the_GID_issue)
    *   [6.2 CUPS permission errors](#CUPS_permission_errors)
    *   [6.3 Printing fails with unauthorised error](#Printing_fails_with_unauthorised_error)
    *   [6.4 Unknown supported format: application/postscript](#Unknown_supported_format:_application.2Fpostscript)
    *   [6.5 Print-Job client-error-document-format-not-supported](#Print-Job_client-error-document-format-not-supported)
    *   [6.6 Unable to get list of printer drivers](#Unable_to_get_list_of_printer_drivers)
    *   [6.7 lp: Error - Scheduler Not Responding](#lp:_Error_-_Scheduler_Not_Responding)
    *   [6.8 "Using invalid Host" error message](#.22Using_invalid_Host.22_error_message)
    *   [6.9 Printer is not recognized by CUPS](#Printer_is_not_recognized_by_CUPS)
        *   [6.9.1 Conflict with SANE](#Conflict_with_SANE)
    *   [6.10 Cannot print from LibreOffice](#Cannot_print_from_LibreOffice)
    *   [6.11 Printer output shifted](#Printer_output_shifted)

## Introduction

The best way to get printing working is to set 'LogLevel' in `/etc/cups/cupsd.conf` to:

```
LogLevel debug

```

And then viewing the output from `/var/log/cups/error_log` like this:

```
# tail -n 100 -f /var/log/cups/error_log

```

The characters at the left of the output stand for:

*   D=Debug
*   E=Error
*   I=Information
*   And so on

These files may also prove useful:

*   `/var/log/cups/page_log` - Echoes a new entry each time a print is successful
*   `/var/log/cups/access_log` - Lists all cupsd http1.1 server activity

Of course, it is important to know how CUPS works if wanting to solve related issues:

1.  An application sends a .ps file (PostScript, a script language that details how the page will look) to CUPS when 'print' has been selected (this is the case with most programs).
2.  CUPS then looks at the printer's PPD file (printer description file) and figures out what filters it needs to use to convert the .ps file to a language that the printer understands (like PJL, PCL), usually GhostScript.
3.  GhostScript takes the input and figures out which filters it should use, then applies them and converts the .ps file to a format understood by the printer.
4.  Then it is sent to the back-end. For example, if the printer is connected to a USB port, it uses the USB back-end.

Print a document and watch `error_log` to get a more detailed and correct image of the printing process.

## Problems resulting from upgrades

_Issues that appeared after CUPS and related program packages underwent a version increment_

### CUPS stops working

The chances are that a new configuration file is needed for the new version to work properly. Messages such as "404 - page not found" may result from trying to manage CUPS via localhost:631, for example.

To use the new configuration, copy `/etc/cups/cupsd.conf.default` to `/etc/cups/cupsd.conf` (backup the old configuration if needed) and restart CUPS to employ the new settings.

### All jobs are "stopped"

If all jobs sent to the printer become "stopped", delete the printer and add it again. Using the [CUPS web interface](http://localhost:631), go to Printers > Delete Printer.

To check the printer's settings go to _Printers_, then _Modify Printer_. Copy down the information displayed, click 'Modify Printer' to proceed to the next page(s), and so on.

### All jobs are "The printer is not responding"

On networked printers, you should check that the name that CUPS uses as its connection URI resolves to the printer's IP via DNS, e.g. If your printer's connection looks like this:

```
lpd://BRN_020554/BINARY_P1

```

then the hostname 'BRN_020554' needs to resolve to the printer's IP from the server running CUPS

### The PPD version is not compatible with gutenprint

Run:

```
# /usr/bin/cups-genppdupdate

```

And restart CUPS (as pointed out in gutenprint's post-install message)

## Networking issues

### CUPS identifies printer but cannot connect to it

Enable debug logging. If you see `Executing backend "/usr/lib/cups/backend/dnssd"...` over and over switch from dnssd to socket in the printer configuration.

Example: `socket://192.168.11.6:9100`. The port number can be confirmed via [nmap](/index.php/Nmap "Nmap") or `telnet _your-printer-ip_ 9100`.

### Finding URIs for Windows print servers

Sometimes Windows is a little less than forthcoming about exact device URIs (device locations). If having trouble specifying the correct device location in CUPS, run the following command to list all shares available to a certain windows username:

```
$ smbtree -U _windowsusername_

```

This will list every share available to a certain Windows username on the local area network subnet, as long as Samba is set up and running properly. It should return something like this:

```
 WORKGROUP
	\\REGULATOR-PC   		
		\\REGULATOR-PC\Z              	
		\\REGULATOR-PC\Public         	
		\\REGULATOR-PC\print$         	Printer Drivers
		\\REGULATOR-PC\G              	
		\\REGULATOR-PC\EPSON Stylus CX8400 Series	EPSON Stylus CX8400 Series
```

What is needed here is first part of the last line, the resource matching the printer description. So to print to the EPSON Stylus printer, one would enter:

```
smb://username.password@REGULATOR-PC/EPSON Stylus CX8400 Series

```

as the URI into CUPS.

If you have special characters (eg *, \) in your username, password or server address, you need to urlencode them. For example,

```
 smb://WIN-DOMAIN.COM\username:passw*rd@WIN-DOMAIN.COM/domain.com/printer

```

must be written as

```
 smb://WIN-DOMAIN.COM%5Cusername:passw%2Ard@WIN-DOMAIN.COM/domain.com/printer

```

To encode the URI, one can use [an online service](http://www.url-encode-decode.com/), [python](https://docs.python.org/2/library/urllib.html#urllib.urlencode) or something else.

## USB printers

USB printers can be accessed using two methods: The usblp kernel module and libusb. The former is the classic way. It is simple: data is sent to the printer by writing it to a device file as a simple serial data stream. Reading the same device file allows bi-di access, at least for things like reading out ink levels, status, or printer capability information (PJL). It works very well for simple printers, but for multi-function devices (printer/scanner) it is not suitable and manufacturers like HP supply their own backends. Source: [here](http://lists.linuxfoundation.org/pipermail/printing-architecture/2012/002412.html).

**Warning:** As of [cups](https://www.archlinux.org/packages/?name=cups) version 1.6.0, it should no longer be necessary to blacklist the `usblp` kernel module. If you find out this is the only way to fix a remaining issue please report this upstream to the CUPS bug tracker and maybe also get in contact with Till Kamppeter (Debian CUPS maintainer). See [upstream bug](http://cups.org/str.php?L4128) for more info.

If you have problems getting your USB printer to work, you can try [blacklisting](/index.php/Blacklisting "Blacklisting") the `usblp` [kernel module](/index.php/Kernel_module "Kernel module"):

 `/etc/modprobe.d/blacklistusblp.conf` 

```
blacklist usblp

```

Custom kernel users may need to manually load the `usbcore` [kernel module](/index.php/Kernel_module "Kernel module") before proceeding.

Once the modules are installed, plug in the printer and check if the kernel detected it by running the following:

```
# journalctl -e

```

or

```
# dmesg

```

If you are using `usblp`, the output should indicate that the printer has been detected like so:

```
Feb 19 20:17:11 kernel: printer.c: usblp0: USB Bidirectional
printer dev 2 if 0 alt 0 proto 2 vid 0x04E8 pid 0x300E
Feb 19 20:17:11 kernel: usb.c: usblp driver claimed interface cfef3920
Feb 19 20:17:11 kernel: printer.c: v0.13: USB Printer Device Class driver

```

If you blacklisted `usblp`, you will see something like:

```
usb 3-2: new full speed USB device using uhci_hcd and address 3
usb 3-2: configuration #1 chosen from 1 choice

```

## HP issues

### HPLIP printer sends "/usr/lib/cups/backend/hp failed" error

Make sure dbus is installed and running. If the error persists, try starting avahi-daemon.

Try adding the printer as a Network Printer using the http:// protocol. Generate the printer URI with `hp-makeuri`.

**Note:** There might need to set permissions issues right. Follow indications here: [CUPS#Device node permissions](/index.php/CUPS#Device_node_permissions "CUPS").

### HPLIP printer claims job is complete but printer does nothing

This happens on HP printers when you select the (old) hpijs driver (e.g. the Deskjet D1600 series). Instead, use the hpcups driver when adding the printer.

Some HP printers (e.g HP LaserJet) require their firmware to be downloaded from the computer every time the printer is switched on. If there is an issue with udev (or equivalent) and the firmware download rule is never fired, you may experience this issue. As a workaround, you can manually download the firmware to the printer. Ensure the printer is plugged in and switched on, then enter

```
hp-firmware -n

```

### hp-setup asks to specify the PPD file for the discovered printer

Install CUPS before running hp-setup.

### I have installed Qt, but hp-setup reports "Qt/PyQt 4 initialization failed"

"hp-check -t" will not give you useful information to find the required package. You have to install all the "Dependent Packages" prefixed with "python2" in [hplip](https://www.archlinux.org/packages/?name=hplip)

### hp-setup finds the printer automatically but reports "Unable to communicate with device" when printing test page immediately afterwards

This at least happens to hplip 3.13.5-2 for HP Officejet 6500A through local network connection. To solve the problem, specify the IP address of the HP printer for hp-setup to locate the printer.

### hp-toolbox sends an error, "Unable to communicate with device"

If running hp-toolbox as a regular user results in:

```
# hp-toolbox
# error: Unable to communicate with device (code=12): hp:/usb/_printer id_

```

or, "`Unable to communicate with device"`", then it may be needed to [add the user to the lp and sys groups](/index.php/Groups#Group_management "Groups").

This can also be caused by printers such as the P1102 that provide a virtual CD-ROM drive for MS Windows drivers. The lp dev appears and then disappears. In that case, try the **usb-modeswitch** and **usb-modeswitch-data** packages, that lets one switch off the "Smart Drive" (udev rules included in said packages).

This can also occur with network attached printers if the [avahi-daemon](/index.php/Avahi "Avahi") is not running. Another possibility is the specification of the printer's IP address in _hp-setup_ fails to locate the printer because the IP address of the the printer changed due to DHCP. If this is the case, consider adding a DHCP reservation for the printer in the DHCP server's configuration.

### CUPS returns '"foomatic-rip" not available/stopped with status 3' with a HP printer

If receiving any of the following error messages in `/var/log/cups/error_log` while using a HP printer, with jobs appearing to be processed while they all end up not being completed with their status set to 'stopped':

```
Filter "foomatic-rip" for printer _printer_name_ not available: No such file or director

```

or:

```
PID 5771 (/usr/lib/cups/filter/foomatic-rip) stopped with status 3!

```

make sure [hplip](https://www.archlinux.org/packages/?name=hplip) has been [installed](/index.php/Pacman "Pacman"), in addition to packages mentioned in [CUPS#HP](/index.php/CUPS#HP "CUPS"). See [this forum post](https://bbs.archlinux.org/viewtopic.php?id=65615) for more information.

### HPLIP 3.13: Plugin is installed, but HP Device Manager complains it is not

The issue might have to do with the file permission change that had been made to `/var/lib/hp/hplip.state`. To correct the issue, a simple `chmod 644 /var/lib/hp/hplip.state` and `chmod 755 /var/lib/hp` should be sufficient. For further information, please read this [link](https://bugs.launchpad.net/hplip/+bug/1131596).

### Printer does not print with an "Filter failed" message on CUPS web interface (HP printer)

#### Bad permissions

Change the permissions of the printer USB port. Get the bus and device number from `lsusb`, then set the permission using:

 ` lsusb `  ` Bus <BUSID> Device <DEVID>: ID <PRINTERID>:<VENDOR> Hewlett-Packard DeskJet D1360` 

Then substitute the provided device information to the

```
# chmod 0666 /dev/bus/usb/<BUSID>/<DEVID>

```

To make the persistent permission change that will be triggered automatically each time the computer is rebooted, add the following line.

 `/etc/udev/rules.d/10-local.rules`  `SUBSYSTEM=="usb", ATTRS{idVendor}=="<VENDOR>", ATTRS{idProduct}=="<PRINTERID>", GROUP="lp", MODE:="666"` 

Each system may vary, so consult [udev#List attributes of a device](/index.php/Udev#List_attributes_of_a_device "Udev") wiki page.

#### Avahi not enabled

Start, enable, and restart the `avahi-daemon` service.

#### Out-of-date plugin

This error can also indicate that the plugin is out of date (version is mismatched). If you have installed [hplip-plugin](https://aur.archlinux.org/packages/hplip-plugin/), you will need to update the package.

### CUPS prints only an empty and an error-message page on HP LaserJet

There is a bug that causes CUPS to fail when printing images on HP LaserJet (in my case 3380). The bug has been reported and fixed by [Ubuntu](https://bugs.launchpad.net/ubuntu/+source/cups-filters/+bug/998087). The first page is empty, the second page contains the following error message:

```
 ERROR:
 invalidaccess
 OFFENDING COMMAND:
 filter
 STACK:
 /SubFileDecode
 endstream
 ...

```

In order to fix the issue, run the following command as root:

```
# lpadmin -p _printer_ -o pdftops-renderer-default=pdftops

```

## Other

### Printer "Paused" or "Stopped" with Status "Rendering completed"

When low on ink, some printers will get stuck in "Rendering completed" status and, if it is a network printer, the printer may even become unreachable from CUPS' perspective despite being properly connected to the network. Replacing the low/depleted ink cartridge(s) in this setting will return the printer to "Ready" status and, if it is a network printer, will make the printer available to CUPS again.

**Note:** If you use third-party ink cartridges, the ink levels reported by the printer may be inaccurate. If you use third-party ink and your printer used to work fine but is now getting stuck on "Rendering completed" status, replace the ink cartridges regardless of the reported ink levels before trying other fixes.

If low ink is not the issue, check the "Group ID" of files in `/etc/cups`, `/var/log/cups`, and, if you have "root" permission, `/var/spool/cups`. The files should have GID `lp`. If some files have GID `nobody`, then check the named groups in the "Group" and "SystemGroup" directives in the file `/etc/cups/cups-files.conf`. Typically there will be `Group lp` and `SystemGroup lpadmin sys root`. Make sure that the group in "Group" is NOT also in "SystemGroup". In particular, make sure that the name `lp` is NOT listed in the "SystemGroup" directive, when it is used in the "Group" directive. This is counter to recommendations made in the CUPS and KDE wiki pages in the past. If you had added `lp` to the "SystemGroup" directive, as had been suggested, remove `lp` from the "SystemGroup", or run the following command and change `lp` to `lpadmin` in the "SystemGroup" directive.

```
# groupadd -g107 lpadmin

```

#### Explanation of the GID issue

For security reasons, `cupsd` does not allow external CUPS helper programs, which are run with the GID selected with the "Group" directive, to run with any GID of the administrative groups, which are those GIDs listed in the "SystemGroup" directive. If the named group in the Group directive is also in the SystemGroup directive, then `cupsd` will instead run the helper programs with GID `nobody`, without warning. Note that the printer devices in `/dev/`, for instance `/dev/parport0`, are created with user `root` and group `lp`. When `cupsd` then tries to print, it "pauses" or "stops" because it does not have permission to write the printer device file, and does not provide any useful error message. The printer device files can be made "world writable" to bypass the problem, but that is insecure and is not the proper solution.

As of CUPS version 2.0.0-2, if the group in the Group directive is also in the SystemGroup directive, `cupsd` will exit immediately after starting, and, at a log level of "notice" or higher, will log an error message to the default error log, but not to the system log.

 `/var/log/cups/error_log`  `Group and SystemGroup cannot use the same groups.` 

This solves the problem of `cupsd` running in a non-functional state and failing to print without explanation.

At the default log level of "warn", no group collision error message is logged. To see this error message, increase the log level to "notice", "info", "debug", or "debug2".

 `/etc/cups/cupsd.conf`  `LogLevel notice` 

Error messages can be sent to the systemd-journald log instead of to the default `/var/log/cups/error_log`, but not to both, by explicitly setting the ErrorLog directive.

 `/etc/cups/cups-files.conf`  `ErrorLog syslog` 

Currently, even then, the command `systemctl status org.cups.cupsd.service` will not properly display the final group collision error message, but the error message can still be seen in the journal, with for instance, `sudo journalctl -f`.

### CUPS permission errors

Some users fixed 'NT_STATUS_ACCESS_DENIED' (Windows clients) errors by using a slightly different syntax:

```
smb://workgroup/username:password@hostname/printer_name

```

### Printing fails with unauthorised error

If the user has been added to the lp group, and allowed to print (set in `cupsd.conf`), then the problem lies in `/etc/cups/printers.conf`. This line could be the culprit:

```
AuthInfoRequired negotiate

```

Comment it out and restart CUPS.

### Unknown supported format: application/postscript

Comment the lines:

```
application/octet-stream        application/vnd.cups-raw        0      -

```

from `/etc/cups/mime.convs`, and:

```
application/octet-stream

```

in `/etc/cups/mime.types`.

### Print-Job client-error-document-format-not-supported

Try installing the foomatic packages and use a foomatic driver.

### Unable to get list of printer drivers

(Also applicable to error "-1 not supported!")

*   Check the `ServerName` in `/etc/cups/client.conf` is written without http://

```
ServerName localhost:631

```

*   Try to remove Foomatic drivers or refer to [CUPS/Printer-specific_problems#HPLIP_Driver](/index.php/CUPS/Printer-specific_problems#HPLIP_Driver "CUPS/Printer-specific problems") for a workaround.

### lp: Error - Scheduler Not Responding

If you get this error when printing a document using:

```
$ lp document-to-print

```

Try setting the `CUPS_SERVER` environment variable:

```
$ export CUPS_SERVER=localhost

```

If this solves your problem, make the solution permanent by adding the export line above to `~/.bash_profile`.

### "Using invalid Host" error message

Try adding `ServerAlias *` into `/etc/cups/cupsd.conf`.

### Printer is not recognized by CUPS

If your printer is not listed in the "Add Printers" page of the CUPS web interface, nor by `lpinfo -v`, try the following (suggested in [this thread](https://bbs.archlinux.org/viewtopic.php?pid=1037279#p1037279)):

*   Remove `usblp` from blacklist
*   Load `usblp` module

```
# modprobe usblp

```

*   Stop CUPS
*   Add the following udev rule in a new rule file:

 `/etc/udev/rules.d/10-cups_device_link.rules`  `KERNEL=="lp[0-9]", SYMLINK+="%k", GROUP="lp"` 

*   Reload udev rules:

```
# udevadm control --reload-rules

```

*   Unplug the printer, and plug it in again.
*   Wait a few seconds, and then start the CUPS service.

#### Conflict with SANE

If you are also running [SANE](/index.php/SANE "SANE"), it's possible that it is conflicting with CUPS.

To fix this create the following file:

 `/etc/udev/rules.d/99-printer.rules` 

```
# idProduct and idVendor needs to match your printer
ATTRS{idVendor}=="04e8", ATTRS{idProduct}=="341b", MODE="0664", GROUP="lp", ENV{libsane_matched}="yes"
```

### Cannot print from LibreOffice

If you can print a test page from the [CUPS](/index.php/CUPS "CUPS") web interface, but not from [LibreOffice](/index.php/LibreOffice "LibreOffice"), try to [install](/index.php/Install "Install") the [a2ps](https://www.archlinux.org/packages/?name=a2ps) package.

### Printer output shifted

This seems to be caused by the wrong page size being set in [CUPS](/index.php/CUPS "CUPS").

Retrieved from "[https://wiki.archlinux.org/index.php?title=CUPS/Troubleshooting&oldid=413981](https://wiki.archlinux.org/index.php?title=CUPS/Troubleshooting&oldid=413981)"