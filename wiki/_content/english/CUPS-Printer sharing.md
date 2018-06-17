Related articles

*   [Samba](/index.php/Samba "Samba")
*   [CUPS](/index.php/CUPS "CUPS")

This article contains instruction on sharing printers between systems, be it between two GNU/Linux systems or between a GNU/Linux system and Microsoft Windows.

## Contents

*   [1 Creating class for multiple printers](#Creating_class_for_multiple_printers)
*   [2 Between GNU/Linux systems](#Between_GNU.2FLinux_systems)
    *   [2.1 Using the web interface](#Using_the_web_interface)
    *   [2.2 Manual setup](#Manual_setup)
    *   [2.3 Enabling browsing](#Enabling_browsing)
*   [3 Between GNU/Linux and Windows](#Between_GNU.2FLinux_and_Windows)
    *   [3.1 Linux server - Windows client](#Linux_server_-_Windows_client)
        *   [3.1.1 Sharing via Bonjour](#Sharing_via_Bonjour)
        *   [3.1.2 Sharing via IPP](#Sharing_via_IPP)
        *   [3.1.3 Sharing via Samba](#Sharing_via_Samba)
    *   [3.2 Windows server - Linux client](#Windows_server_-_Linux_client)
        *   [3.2.1 Sharing via LPD](#Sharing_via_LPD)
        *   [3.2.2 Sharing via IPP](#Sharing_via_IPP_2)
        *   [3.2.3 Sharing via Samba](#Sharing_via_Samba_2)
            *   [3.2.3.1 Configuration using the web interface](#Configuration_using_the_web_interface)
            *   [3.2.3.2 Manual configuration](#Manual_configuration)
            *   [3.2.3.3 Finding URIs for Windows print servers](#Finding_URIs_for_Windows_print_servers)
*   [4 Remote administration](#Remote_administration)
    *   [4.1 Kerberos](#Kerberos)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Cannot print with GTK applications](#Cannot_print_with_GTK_applications)
    *   [5.2 Permission errors on Windows](#Permission_errors_on_Windows)
*   [6 Other operating systems](#Other_operating_systems)

## Creating class for multiple printers

'Class' in CUPS have meaning of a group. When you have multiple printers connected to single CUPS server you may want them to be balanced (printing jobs are automatically queued to different printers). This is also give an advantage that users on remote machine dealing with single 'printer'. Which is especially useful when one printer from class must be taken for repair, you just exclude it from class, yet for end users nothing have changed, printing jobs queued to another printer by CUPS server. Creating and managing classes can be done from CUPS Web GUI

## Between GNU/Linux systems

The server can be configured using either the web interface or by manually editing `/etc/cups/cupsd.conf`. To configure the client, see [CUPS](/index.php/CUPS "CUPS").

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

Also make sure the server is listening on the IP address the client will use:

 `/etc/cups/cupsd.conf` 
```
...
Listen <hostname>:631
...

```

There are more configuration possibilities, including automatic methods, which are described in detail in [Using Network Printers](https://www.cups.org/doc/network.html) and [cupsd.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cupsd.conf.5).

After making any modifications, [restart](/index.php/Restart "Restart") the `org.cups.cupsd` service.

If CUPS is started using socket activation, create a [drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet") for `org.cups.cupsd.socket` so that socket activation also works for remote connections:

 `/etc/systemd/system/org.cups.cupsd.socket.d/override.conf` 
```
[Socket]
ListenStream=631

```

### Enabling browsing

To enable browsing (shared printer discovery), [Avahi](/index.php/Avahi "Avahi") must be installed and running on the server. If you do not need printer discovery, Avahi is not required on either the server or the client.

To enable browsing, either select *Share printers connected to this system* in the web interface, or manually turn on Browsing and set the BrowseAddress:

 `/etc/cups/cupsd.conf` 
```
...
Browsing On
BrowseAddress 192.168.0.*:631
...

```

and [restart](/index.php/Restart "Restart") the `org.cups.cupsd` service.

Note that "browsing" at the print server is a different thing from "browsing" at a remote networked host. On the print server, `cupsd` provides the DNS-SD protocol support which the `avahi-daemon` broadcasts. The `cups-browsed` service is unnecessary on the print server, unless also broadcasting the old CUPS protocol, or the print server is also "browsing" for other networked printers. On the remote networked host, the `cups-browsed` service is *required* to "browse" for network broadcasts of print services, and running `cups-browsed` will also automatically start `cupsd`.

The `org.cups.cupsd.service` service will be automatically started when a USB printer is plugged in, however this may not be the case for other connection types. If `cupsd` is not running, `avahi-daemon` does not broadcast the print services, so in that case the systemd unit service file must be modified to start on boot, and then the service must again be "enabled/installed" with the new dependency. To do this, [edit](/index.php/Edit "Edit") the service file `[Install]` section to add a `WantedBy=default.target` dependency, and then [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `org.cups.cupsd.service` service.

## Between GNU/Linux and Windows

### Linux server - Windows client

Sharing to Windows clients can be achieved using [#Sharing via Bonjour](#Sharing_via_Bonjour), [#Sharing via IPP](#Sharing_via_IPP), or [#Sharing via Samba](#Sharing_via_Samba).

After setting up the server, install the native printer drivers for your printer on the Windows computer. If the CUPS server's print queue is set up to use its own printer drivers instead of as a `raw` queue, you can just select a generic postscript printer driver for the Windows client (e.g. 'HP Color LaserJet 8500 PS' or 'Xerox DocuTech 135 PS2' or 'Microsoft PS Class driver').

#### Sharing via Bonjour

[Bonjour Printing Services](https://support.apple.com/kb/dl999) allows Windows to easily connect to Unix printers shared in the local network using [Avahi](/index.php/Avahi "Avahi").

#### Sharing via IPP

The [Internet Printing Protocol](https://en.wikipedia.org/wiki/Internet_Printing_Protocol "wikipedia:Internet Printing Protocol") is a widely supported standard among operating systems that is simple to configure. It features port forwarding, tunnelling, etc.

**Note:** You may have to add the Internet Printing Client to Windows (*Control Panel > Programs > Turn Windows features on or off > Print and Document Services*)

First, configure the server as described in the section [#Between GNU/Linux systems](#Between_GNU.2FLinux_systems).

On the Windows computer, go to *Control Panel > Devices and Printers* and choose 'Add a printer'. If on Windows 10, click "The printer that I want isn't listed". Next, choose 'Select a shared printer by name' and type in the location of the printer:

```
http://*hostname*:631/printers/*printer_name*

```

(where *hostname* is the GNU/Linux server's hostname or IP address and *printer_name* is the name of the print queue being connected to. You can also use the server's fully qualified domain name, if it has one, but you may need to set `ServerAlias my_fully_qualified_domain_name` in `/etc/cups/cupsd.conf` for this to work).

**Note:**

*   The 'Add Printer' dialog in Windows suggests the format `http://computername/printers/printername/.printer`, which it will not accept. Instead, use the syntax suggested above.
*   If you are using a proxy carefully check any used proxy **exclusions**. A wrong setting here may result in you being unable to add a printer until the next reboot even if you disable the proxy afterwards (at least on Windows 7).

#### Sharing via Samba

[Samba](/index.php/Samba "Samba") is an implementation of the Windows file and printer sharing protocols, even the most vintage ones.

Note that printer sharing using Samba is usually **more difficult** to configure and maintain.

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
$ python -c 'from urllib.parse import quote; print("smb://" + quote("BEN-DESKTOP/HP Color LaserJet CP1510 series PCL6"))'

```

#### Sharing via LPD

Windows 7, 8 and 10 have a built-in LPD server - using it will probably be the easiest approach as it does neither require an installation of *Samba* on the client nor heavy configuration on the server. It can be activated in the *Control Panel* under *Programs* -> *Activate Windows functions* in the section *Print services*. The printer must have *shared* activated in its properties. Use a share name without any special characters like spaces, commas, etc.

Then the printer can be added in CUPS, choosing LPD protocol. The printer address will look like this:

```
# lpd://windowspc/printersharename

```

Before adding the printer, you will most likely have to install an appropriate printer driver depending on your printer model. Generic PostScript or RAW drivers might also work.

#### Sharing via IPP

As above, IPP is also the **preferred** protocol for printer sharing although it **only works with Windows Server versions**. Windows Server versions (e.g. Server 2016) include IPP support ("Print and Document Services" role, "Internet Printing" service). Client versions (e.g. Windows 10), only include the IPP client, and **do not support sharing through IPP**.

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

Make sure that the user actually has access to the printer on the Windows computer and select the appropriate drivers. If the computer is located on a domain, make sure the URI includes the domain:

```
smb://username:password@domain/hostname/printer_name

```

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

Then restart the CUPS daemon and try to print a test page.

##### Finding URIs for Windows print servers

Sometimes Windows is a little less than forthcoming about exact device URIs (device locations). If having trouble specifying the correct device location in CUPS, run the following command to list all shares available to a certain windows username:

```
$ smbtree -U *windowsusername*

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

## Remote administration

Once the server is set up as described in [#Between GNU/Linux systems](#Between_GNU.2FLinux_systems), it can also be configured so that it can be remotely administered. Add the allowed hosts to the `<Location /admin>` block in `/etc/cups/cupsd.conf`, using the same syntax as described in [#Manual setup](#Manual_setup). Note that three levels of access can be granted:

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

Deny statements can also be used. For example, to give full access to all hosts on your local network interfaces, edit `/etc/cups/cupsd.conf` to include this:

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

### Kerberos

[Kerberos](/index.php/Kerberos "Kerberos") can be used to authenticate users accessing a remote CUPS server. This assumes that your machine has a keytab and it will need a ticket for "HTTP". Instead of using `http://localhost:631` you must use `https://host.example.co.uk:631` - encryption is required for auth (hence https) and the full hostname is needed so that Kerberos/Negotiate can work. In addition, the server must be configured in `/etc/cups/cupsd.conf` to use a `DefaultAuthType` of `Negotiate`.

If you are using [Samba](/index.php/Samba "Samba")'s winbind NSS support, you can add an AD group name to `/etc/cups/cups-files.conf` - in the following example `sysadmin` might be an AD group:

```
SystemGroup sys root sysadmin

```

## Troubleshooting

See [CUPS/Troubleshooting](/index.php/CUPS/Troubleshooting "CUPS/Troubleshooting") for general troubleshooting tips.

### Cannot print with GTK applications

If you get a *getting printer information failed* message when you try to print from GTK applications, add this line to your `/etc/hosts`:

```
 # serverip 	some.name.org 	ServersHostname

```

### Permission errors on Windows

Some users fixed 'NT_STATUS_ACCESS_DENIED' (Windows clients) errors by using a slightly different syntax:

```
smb://workgroup/username:password@hostname/printer_name

```

## Other operating systems

More information on interfacing CUPS with other printing systems can be found in the CUPS manual, e.g. on [http://localhost:631/help/network.html](http://localhost:631/help/network.html)