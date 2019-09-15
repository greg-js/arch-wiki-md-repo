Related articles

*   [Samba](/index.php/Samba "Samba")
*   [CUPS](/index.php/CUPS "CUPS")

This article contains instruction on sharing printers from a GNU/Linux system.

<caption>Client support</caption>
| Protocol | Linux | Windows | macOS |
| [Discovery (DNS-SD/mDNS)](https://en.wikipedia.org/wiki/Zero-configuration_networking#DNS-based_service_discovery "wikipedia:Zero-configuration networking") | [CUPS](/index.php/CUPS "CUPS") with [Avahi](/index.php/Avahi "Avahi") | Native support since [Windows 10](https://www.ctrl.blog/entry/windows-mdns-dnssd.html) | Bonjour |
| [Internet Printing Protocol](https://en.wikipedia.org/wiki/Internet_Printing_Protocol "wikipedia:Internet Printing Protocol") | [CUPS](/index.php/CUPS "CUPS") | *Control Panel > Programs > Turn Windows features on or off > Print and Document Services > Internet Printing Client* | Native support |
| [SMB](https://en.wikipedia.org/wiki/Server_Message_Block "wikipedia:Server Message Block") shared printer | [Samba](/index.php/Samba "Samba") with [CUPS](/index.php/CUPS "CUPS") | Native support | Native support |
| [Line Printer Daemon protocol](https://en.wikipedia.org/wiki/Line_Printer_Daemon_protocol "wikipedia:Line Printer Daemon protocol") | [CUPS](/index.php/CUPS "CUPS") | *Control Panel > Programs > Turn Windows features on or off > Print services >*
*LPD Print Service* and *LPR Port Monitor* | Native support |

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Creating class for multiple printers](#Creating_class_for_multiple_printers)
*   [2 Printer sharing](#Printer_sharing)
    *   [2.1 DNS-SD advertisement](#DNS-SD_advertisement)
    *   [2.2 Sharing via Internet Printing Protocol](#Sharing_via_Internet_Printing_Protocol)
    *   [2.3 Sharing via Samba](#Sharing_via_Samba)
    *   [2.4 Sharing via Line Printer Daemon protocol](#Sharing_via_Line_Printer_Daemon_protocol)
*   [3 Remote administration](#Remote_administration)
    *   [3.1 Kerberos](#Kerberos)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Cannot print with GTK applications](#Cannot_print_with_GTK_applications)
    *   [4.2 Permission errors on Windows](#Permission_errors_on_Windows)
*   [5 Other operating systems](#Other_operating_systems)

## Creating class for multiple printers

In CUPS, a class is a group of printers which appears to clients as a single printer. When a client selects to print to the class, CUPS selects any printer in the group to accept the print job. This may be especially useful when one printer from the class must be removed. If it is excluded from the class, end users will not notice any change because the print job will be queued to another printer in the class. Creating and managing classes can be done from CUPS Web GUI.

## Printer sharing

### DNS-SD advertisement

To announce the printer to the network over DNS-SD/mDNS (Bonjour in Apple world), [Avahi](/index.php/Avahi "Avahi") must be installed and running on the server.

To enable it, either select *Share printers connected to this system* in the web interface, or manually set `Browsing On` in `/etc/cups/cupsd.conf`:

 `/etc/cups/cupsd.conf` 
```
...
Browsing On
...

```

Afterwards [restart](/index.php/Restart "Restart") `org.cups.cupsd.service`.

Note that "browsing" at the print server is a different thing from "browsing" at a remote networked host. On the print server, `cupsd` provides the DNS-SD protocol support which the `avahi-daemon` broadcasts. The `cups-browsed` service is unnecessary on the print server, unless also broadcasting the old CUPS protocol, or the print server is also "browsing" for other networked printers. On the remote networked host, the `cups-browsed` service is *required* to "browse" for network broadcasts of print services, and running `cups-browsed` will also automatically start `cupsd`.

The `org.cups.cupsd.service` service will be automatically started when a USB printer is plugged in, however this may not be the case for other connection types. If `cupsd` is not running, `avahi-daemon` does not broadcast the print services, so in that case the systemd unit service file must be modified to start on boot, and then the service must again be "enabled/installed" with the new dependency. To do this, [edit](/index.php/Edit "Edit") the service file `[Install]` section to add a `WantedBy=default.target` dependency, and then [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `org.cups.cupsd.service` service.

### Sharing via Internet Printing Protocol

The server can be configured using either the web interface or by manually editing `/etc/cups/cupsd.conf`.

Open up the web interface to the server, select the *Administration* tab, look under the *Server* heading, and enable the "Share printers connected to this system" option. Save your change by clicking on the *Change Settings* button. The server will automatically restart.

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

After making any modifications, [restart](/index.php/Restart "Restart") `org.cups.cupsd.service`.

If CUPS is started using socket activation, create a [drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet") for `org.cups.cupsd.socket` so that socket activation also works for remote connections:

 `/etc/systemd/system/org.cups.cupsd.socket.d/override.conf` 
```
[Socket]
ListenStream=631
```

### Sharing via Samba

[Samba](/index.php/Samba "Samba") is an implementation of the Windows file and printer sharing protocols, even the most vintage ones.

To configure Samba on the Linux server, edit `/etc/samba/smb.conf` file to allow access to printers. File `smb.conf` can look something like this:

 `/etc/samba/smb.conf` 
```
[global]
...
printing = CUPS
...

[printers]
    comment = All Printers
    path = /var/spool/samba
    browseable = yes
    # to allow user 'guest account' to print.
    guest ok = no
    writable = no
    printable = yes
    create mode = 0700
    write list = root @adm @wheel *yourusername*
```

That should be enough to share the printer, yet adding an individual printer entry may be desirable:

 `/etc/samba/smb.conf` 
```
[ML1250]
    comment = Samsung ML-1250 Laser Printer
    printer = ml1250
    path = /var/spool/samba
    printing = cups
    printable = yes
    user client driver = yes
    # to allow user 'guest account' to print.
    guest ok = no
    writable = no
    write list = root @adm @wheel *yourusername*
    valid users = root @adm @wheel *yourusername*
```

Please note that this assumes configuration was made so that users must have a valid account to access the printer. To have a public printer, set `guest ok` to `yes`, and remove the `valid users` line. To add accounts, set up a regular GNU/Linux account and then set up a Samba password on the server. See [Samba#User Management](/index.php/Samba#User_Management "Samba").

After this, [restart](/index.php/Restart "Restart") `smb.service` and `nmb.service`.

See Samba's documentation [Setting up Samba as a Print Server](https://wiki.samba.org/index.php/Setting_up_Samba_as_a_Print_Server) for more details.

### Sharing via Line Printer Daemon protocol

**Warning:** *cups-lpd* does not perform any access control based on the settings in `/etc/cups/cupsd.conf`. Therefore, running *cups-lpd* on your server will allow any computer on your network (and perhaps the entire Internet) to print to your server.

[Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `org.cups.cups-lpd.socket`.

## Remote administration

Once the server is set up as described in [#Printer sharing](#Printer_sharing), it can also be configured so that it can be remotely administered. Add the allowed hosts to the `<Location /admin>` block in `/etc/cups/cupsd.conf`, using the same syntax as described in [#Sharing via Internet Printing Protocol](#Sharing_via_Internet_Printing_Protocol). Note that three levels of access can be granted:

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

You might also need to disable the HTTPS requirement, when using the default self-signed certificate generated by CUPS:

```
DefaultEncryption IfRequested

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
serverip 	some.name.org 	ServersHostname

```

### Permission errors on Windows

Some users fixed `NT_STATUS_ACCESS_DENIED` (Windows clients) errors by using a slightly different syntax:

```
smb://workgroup/username:password@hostname/printer_name

```

## Other operating systems

More information on interfacing CUPS with other printing systems can be found in the CUPS manual, e.g. on [http://localhost:631/help/network.html](http://localhost:631/help/network.html).