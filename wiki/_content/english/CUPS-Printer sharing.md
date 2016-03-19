See [CUPS](/index.php/CUPS "CUPS") for the main article.

This article contains instruction on sharing printers between systems, be it between two GNU/Linux systems or between a GNU/Linux system and Microsoft Windows.

## Contents

*   [1 Between GNU/Linux systems](#Between_GNU.2FLinux_systems)
    *   [1.1 Using the web interface](#Using_the_web_interface)
    *   [1.2 Manual setup](#Manual_setup)
    *   [1.3 Enabling browsing](#Enabling_browsing)
*   [2 Between GNU/Linux and Windows](#Between_GNU.2FLinux_and_Windows)
    *   [2.1 Linux server - Windows client](#Linux_server_-_Windows_client)
        *   [2.1.1 Sharing via IPP](#Sharing_via_IPP)
        *   [2.1.2 Sharing via Samba](#Sharing_via_Samba)
    *   [2.2 Windows server - Linux client](#Windows_server_-_Linux_client)
        *   [2.2.1 Sharing via LPD](#Sharing_via_LPD)
        *   [2.2.2 Sharing via IPP](#Sharing_via_IPP_2)
        *   [2.2.3 Sharing via Samba](#Sharing_via_Samba_2)
            *   [2.2.3.1 Configuration using the web interface](#Configuration_using_the_web_interface)
            *   [2.2.3.2 Manual configuration](#Manual_configuration)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Cannot print with GTK applications](#Cannot_print_with_GTK_applications)
    *   [3.2 Unable to add/modify a printer via SAMBA](#Unable_to_add.2Fmodify_a_printer_via_SAMBA)
*   [4 Other operating systems](#Other_operating_systems)

## Between GNU/Linux systems

The server can be configured using either the web interface or by manually editing `/etc/cups/cupsd.conf`. To configure the client, see [CUPS#Remote printers](/index.php/CUPS#Remote_printers "CUPS").

### Using the web interface

Open up the web interface to the server, select the *Administration* tab, look under the *Server* heading, and enable the "Share printers connected to this system" option. Save your change by clicking on the *Change Settings* button. The server will automatically restart.

For more complex configurations, you can directly edit the `/etc/cups/cupsd.conf` file by selecting *Edit Configuration File*. See [#Manual setup](#Manual_setup) for more information.

### Manual setup

On the server computer (the one directly connected to the printer), allow access to the server by modifying the location directive. For instance:

 `/etc/cups/cupsd.conf` 
```
<Location />
    Order allow,deny
    Allow localhost
    Allow 192.168.0.*
</Location>
...

```

Also make sure the server is listening on the IP address the client will be addressing:

 `/etc/cups/cupsd.conf` 
```
...
Listen <hostname>:631
...

```

There are more configuration possibilities, including automatic methods, which are described in detail in [Using Network Printers](http://localhost:631/help/network.html).

After making any modifications, restart CUPS.

### Enabling browsing

To enable browsing (shared printer discovery), [Avahi](/index.php/Avahi "Avahi") must be installed and running on the server. If you do not need printer discovery, Avahi is not required on either the server or the client.

**Note:** Browsing will only work if [Avahi](/index.php/Avahi "Avahi") is running before cupsd is started

To enable browsing, either select *Share printers connected to this system* in the web interface, or manually turn on Browsing and set the BrowseAddress:

 `/etc/cups/cupsd.conf` 
```
...
Browsing On
BrowseAddress 192.168.0.*:631
...

```

## Between GNU/Linux and Windows

### Linux server - Windows client

#### Sharing via IPP

The **preferred way** to connect a Windows client to a Linux print server is using [IPP](https://en.wikipedia.org/wiki/Internet_Printing_Protocol "wikipedia:Internet Printing Protocol"). It is a standard printer protocol based on HTTP, allowing you all ways to profit from port forwarding, tunneling etc. The configuration is **very easy** and this way is less error-prone than using Samba. IPP is natively supported by Windows **since Windows 2000**.

To configure the server side proceed as described in the section above to enable browsing.

On the Windows computer, go to the printer control panel and choose to 'Add a New Printer'. Next, choose to give a URL. For the URL, type in the location of the printer:

```
http://*host_ip_address*:631/printers/*printer_name*

```

(where *host_ip_address* is the GNU/Linux server's IP address and *printer_name* is the name of the printer being connected to, you can also use the server's fully qualified domain name, if it has one, but you may need to set `ServerAlias my_fully_qualified_domain_name` in *cupsd.conf* for this to work).

**Note:** The add printer dialog in windows is quite sensitive to the path to the printer, the dialogue box itself suggests:
```
http://servername:631/printers/printer_name/.printer

```

which will work in a web-browser but **not** in the add printer dialogue. (At least, not when using cups as an ipp server). The syntax suggested above:

```
http://host_ip_address:631/printers/printer_name

```

**will** work.

**Note**: If you are using **proxy** - check used proxy **exclusions** twice - it may result in failing to add a printer until reboot even if you will disable proxy at all afterwards (actual for Windows 7).

After this, install the native printer drivers for your printer on the Windows computer. If the CUPS server is set up to use its own printer drivers, then you can just select a generic postscript printer for the Windows client(e.g. 'HP Color LaserJet 8500 PS' or 'Xerox DocuTech 135 PS2'). Then test the print setup by printing a test page.

#### Sharing via Samba

If your client's Windows version is below Windows 2000 or if you experienced troubles with IPP you can also use Samba for sharing. Note of course that with Samba this involves another complex piece of software. This makes this way **more difficult to configure** and thus sometimes also **more error-prone**, mostly due to authentication problems.

To configure Samba on the Linux server, edit `/etc/samba/smb.conf` file to allow access to printers. File `smb.conf` can look something like this:

 `/etc/samba/smb.conf` 
```
[global]
workgroup=Heroes
server string=Arch Linux Print Server
security=user

[printers]
    comment=All Printers
    path=/var/spool/samba
    browseable=yes
    # to allow user 'guest account' to print.
    guest ok=no
    writable=no
    printable=yes
    create mode=0700
    write list=@adm root yourusername
```

That should be enough to share the printer, yet adding an individual printer entry may be desirable:

 `/etc/samba/smb.conf` 
```
[ML1250]
    comment=Samsung ML-1250 Laser Printer
    printer=ml1250
    path=/var/spool/samba
    printing=cups
    printable=yes
    printer admin=@admin root yourusername
    user client driver=yes
    # to allow user 'guest account' to print.
    guest ok=no
    writable=no
    write list=@adm root yourusername
    valid users=@adm root yourusername
```

Please note that this assumes configuration was made so that users must have a valid account to access the printer. To have a public printer, set *guest ok* to *yes*, and remove the *valid users* line. To add accounts, set up a regular GNU/Linux account and then set up a Samba password on the server. For instance:

```
# useradd yourusername
# smbpasswd -a yourusername

```

After this, restart the Samba daemon.

Obviously, there are a lot of tweaks and customizations that can be done with setting up a Samba print server, so it is advised to look at the Samba and CUPS documentation for more help. The `smb.conf.example` file also has some good samples that might warrant imitating.

### Windows server - Linux client

**Warning:** Any special characters in the printer URIs need to be appropriately quoted, or, if your Windows printer name or user passwords have spaces, CUPS will throw a "lpadmin: Bad device-uri" error.

For example: `smb://BEN-DESKTOP/HP Color LaserJet CP1510 series PCL6`

becomes:

`smb://BEN-DESKTOP/HP%20Color%20LaserJet%20CP1510%20series%20PCL6`

This result string can be obtained by running the following command:

```
$ python2 -c 'import urllib; print "smb://" + urllib.quote("BEN-DESKTOP/HP Color LaserJet CP1510 series PCL6")'

```

#### Sharing via LPD

Windows 7 has a built-in LPD server - using it will probably be the easiest approach as it does neither require an installation of *Samba* on the client nor heavy configuration on the server. It can be activated in the *Control Panel* under *Programs* -> *Activate Windows functions* in the section *Print services*. The printer must have *shared* activated in its properties. Use a share name without any special characters like spaces, commas, etc.

Then the printer can be added in CUPS, choosing LPD protocol. The printer address will look like this:

```
# lpd://windowspc/printersharename

```

Before adding the printer, you will most likely have to install an appropriate printer driver depending on your printer model. Generic PostScript or RAW drivers might also work.

#### Sharing via IPP

As above, IPP is also the **preferred** protocol for printer sharing. However this way might be a bit **more difficult** than the native Samba approach below, since you need a greater effort to set up an IPP-Server on Windows. The commonly chosen server software is Microsoft's Internet Information Services (IIS).

**Note:** This section is incomplete. Here is a description how to set up ISS in Windows XP and Windows 2000, unfortunately in German [[1]](http://www.heise.de/netze/artikel/Ueberall-drucken-221652.html)

#### Sharing via Samba

A **much simpler way** is using Window's native printer sharing via Samba. There is almost no configuration needed, and all of it can be done from the CUPS Backend. As above noted, if there are any problems the reason is mostly related to authentication trouble and Windows access restrictions.

On the server side enable sharing for your desired printer and ensure that the user on the client machine has the right to access the printer.

The following section describes how to set up the client, assuming that both daemons (cupsd and smbd) are running.

##### Configuration using the web interface

The Samba CUPS back-end is enabled by default, if for any reason it is not activate it by entering the following command and restarting CUPS.

```
# ln -s $(which smbspool) /usr/lib/cups/backend/smb

```

Next, simply log in on the CUPS web interface and choose to add a new printer. As a device choose "Windows Printer via SAMBA".

For the device location, enter:

```
smb://username:password@hostname/printer_name

```

Or without a password:

```
smb://username@hostname/printer_name

```

Make sure that the user actually has access to the printer on the Windows computer and select the appropriate drivers. If the computer is located on a domain, make sure the user-name includes the domain:

```
smb://username:password@domain/hostname/printer_name

```

If the network contains many printers you might want to set a preferred printer. To do so use the web interface, go into the printer tab, choose the desired printer and select 'Set as default' from the drop-down list.

##### Manual configuration

For manual configuration stop the CUPS daemon and add your printer to `/etc/cups/printers.conf`, which might for example look like this

 `/etc/cups/printers.conf` 
```
<DefaultPrinter MyPrinter>
AuthInfoRequired username,password
Info My printer via SAMBA
Location In my Office
MakeModel Samsung ML-1250 - CUPS+Gutenprint v5.2.7        # <= use 'lpinfo -m' to list available models
DeviceURI smb://username:password@hostname/printer_name   # <= server URI as described in previous section
State Idle
Type 4
Accepting Yes
Shared No
JobSheets none none
QuotaPeriod 0
PageLimit 0
KLimit 0
AllowUser yourusername                                    # <= do not forget to change this
OpPolicy default
ErrorPolicy stop-printer
</Printer>
```

Then restart the CUPS daemon an try to print a test page.

## Troubleshooting

See [CUPS/Troubleshooting](/index.php/CUPS/Troubleshooting "CUPS/Troubleshooting") for general troubleshooting tips.

### Cannot print with GTK applications

If you get "getting printer information failed" when you try to print from gtk-applications, add this line to your `/etc/hosts`:

```
 # serverip 	some.name.org 	ServersHostname

```

### Unable to add/modify a printer via SAMBA

When adding a or modifying a printer via SAMBA, the interface hangs at 100% CPU for about 30 seconds and then returns the message

```
Unable to get list of printer drivers: Success

```

This is a known bug in Gutenprint ([https://bugs.archlinux.org/task/43708](https://bugs.archlinux.org/task/43708)). The workaround is to uninstall Gutenprint and install only foomatic-db.

```
 lpinfo -m

```

should then return the list of drivers instead of just the "Success" message.

## Other operating systems

More information on interfacing CUPS with other printing systems can be found in the CUPS manual, e.g. on [http://localhost:631/help/network.html](http://localhost:631/help/network.html)