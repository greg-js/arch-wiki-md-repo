# Avahi

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

From [Wikipedia:Avahi (software)](https://en.wikipedia.org/wiki/Avahi_(software) "wikipedia:Avahi (software)"):

_"[Avahi](http://avahi.org/) is a free [Zero-configuration networking](https://en.wikipedia.org/wiki/Zero-configuration_networking "wikipedia:Zero-configuration networking") (zeroconf) implementation, including a system for multicast DNS/DNS-SD service discovery. It allows programs to publish and discover services and hosts running on a local network with no specific configuration. For example you can plug into a network and instantly find printers to print to, files to look at and people to talk to. It is licensed under the GNU Lesser General Public License (LGPL)."_

## Contents

*   [1 Installation](#Installation)
*   [2 Using Avahi](#Using_Avahi)
    *   [2.1 Hostname resolution](#Hostname_resolution)
        *   [2.1.1 Additional info about mdns](#Additional_info_about_mdns)
        *   [2.1.2 Tools](#Tools)
    *   [2.2 File sharing](#File_sharing)
        *   [2.2.1 NFS](#NFS)
        *   [2.2.2 Samba](#Samba)
        *   [2.2.3 Vsftpd](#Vsftpd)
    *   [2.3 Link-Local (Bonjour/Zeroconf) chat](#Link-Local_.28Bonjour.2FZeroconf.29_chat)
    *   [2.4 Airprint from Mobile Devices](#Airprint_from_Mobile_Devices)
    *   [2.5 Firewall](#Firewall)
    *   [2.6 Obtaining IPv4LL IP address](#Obtaining_IPv4LL_IP_address)
    *   [2.7 Customizing Avahi](#Customizing_Avahi)
        *   [2.7.1 Adding Services](#Adding_Services)
        *   [2.7.2 Modifying the service-types database](#Modifying_the_service-types_database)
            *   [2.7.2.1 Getting the Sources](#Getting_the_Sources)
            *   [2.7.2.2 Modify the Sources](#Modify_the_Sources)
            *   [2.7.2.3 Build and Install the New Database](#Build_and_Install_the_New_Database)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [avahi](https://www.archlinux.org/packages/?name=avahi) package.

You can manage the Avahi daemon with `avahi-daemon.service` [using systemd](/index.php/Systemd#Using_units "Systemd").

## Using Avahi

### Hostname resolution

Avahi provides local hostname resolution using a "_hostname_.local" naming scheme. To enable it, install the [nss-mdns](https://www.archlinux.org/packages/?name=nss-mdns) package and start `avahi-daemon.service`.

Then, edit the file `/etc/nsswitch.conf` and change the line:

```
hosts: files dns myhostname

```

to:

```
hosts: files mdns_minimal [NOTFOUND=return] dns myhostname

```

**Note:** If you experience slowdowns in resolving `.local` hosts try to use `mdns4_minimal` instead of `mdns_minimal`.

#### Additional info about mdns

The `mdns_minimal` module handles queries for the `.local` TLD only. Note the `[NOTFOUND=return]`, which specifies that if `mdns_minimal` cannot find `*.local`, it will not continue to search for it in `dns`, `myhostname`, etc. In case you have configured Avahi to use a different TLD, you should replace `mdns_minimal [NOTFOUND=return]` with the full `mdns` module. There also are IPv4-only and IPv6-only modules `mdns[46](_minimal)`.

#### Tools

Avahi includes several utilities which help you discover the services running on a network. For example, run

```
$ avahi-browse -alr

```

to discover services in your network.

The Avahi Zeroconf Browser (`avahi-discover` – note that it needs avahi's optional dependencies [pygtk](https://www.archlinux.org/packages/?name=pygtk) and [python2-dbus](https://www.archlinux.org/packages/?name=python2-dbus)) shows the various services on your network. You can also browse SSH and VNC Servers using `bssh` and `bvnc` respectively.

There's a good list of software with Avahi support at their website: [http://avahi.org/wiki/Avah4users](http://avahi.org/wiki/Avah4users)

### File sharing

#### NFS

If you have an [NFS](/index.php/NFS "NFS") share set up, you can use Avahi to be able to automount them in Zeroconf-enabled browsers (such as Konqueror on KDE and Finder on OS X).

Create a `.service` file in `/etc/avahi/services` with the following contents:

 `/etc/avahi/services/nfs_Zephyrus_Music.service` 

```
<?xml version="1.0" standalone='no'?>
<!DOCTYPE service-group SYSTEM "avahi-service.dtd">
<service-group>
  <name replace-wildcards="yes">NFS Music Share on %h</name>
  <service>
    <type>_nfs._tcp</type>
    <port>2049</port>
    <txt-record>path=/data/shared/Music</txt-record>
  </service>
</service-group>
```

The port is correct if you have _insecure_ as an option in your `/etc/exports`; otherwise, it needs to be changed (note that _insecure_ is needed for OS X clients). The path is the path to your export, or a subdirectory of it. For some reason the automount functionality has been removed from Leopard, however [a script is available](http://www.macosxhints.com/article.php?story=20071116042238744). This was based upon [this post](http://ubuntuforums.org/showthread.php?p=4387032#post4387032).

#### Samba

With the Avahi daemon running on both the server and client, the file manager on the client should automatically find the server.

#### Vsftpd

You can also auto-discover regular FTP servers, such as vsftpd. Install the [vsftpd](https://www.archlinux.org/packages/?name=vsftpd) package and change the settings of vsftpd according to your own personal preferences (see [this thread on ubuntuforums.org](http://ubuntuforums.org/showthread.php?t=218630) or `man vsftpd.conf`).

Create a `.service` file in `/etc/avahi/services` with the following contents:

 `/etc/avahi/services/ftp.service` 

```
<?xml version="1.0" standalone='no'?>
<!DOCTYPE service-group SYSTEM "avahi-service.dtd">
<service-group>
  <name>FTP file sharing</name>
  <service>
    <type>_ftp._tcp</type>
    <port>21</port>
  </service>
</service-group>

```

When you are done, [restart](/index.php/Restart "Restart") the `avahi-daemon.service` and `vsftpd.service` services.

The FTP server should now be advertised by Avahi. You should now be able to find the FTP server from a file manager on another computer in your network. You might need to enable [#Hostname resolution](#Hostname_resolution) on the client.

### Link-Local (Bonjour/Zeroconf) chat

Avahi can be used for bonjour protocol support under linux. Check [Wikipedia:Comparison of instant messaging clients](https://en.wikipedia.org/wiki/Comparison_of_instant_messaging_clients "wikipedia:Comparison of instant messaging clients") or [List of applications#Instant messaging](/index.php/List_of_applications#Instant_messaging "List of applications") for a list of clients supporting the bonjour protocol.

### Airprint from Mobile Devices

Avahi along with CUPS also provides the capability to print to just about any printer from airprint compatible mobile devices. In order to enable print capability from your device, simply create an avahi service file for your printer in /etc/avahi/services and restart avahi. An example of a generic services file for an HP-Laserjet printer would be similar to the following with the `name`, `rp`, `ty`, `adminurl` and `note` fields changed.

 `/etc/avahi/services/youFileName.service` 

```
<?xml version="1.0" standalone='no'?><!--*-nxml-*-->
<!DOCTYPE service-group SYSTEM "avahi-service.dtd">
<service-group>
  <name>yourPrnterName</name>
  <service>
    <type>_ipp._tcp</type>
    <subtype>_universal._sub._ipp._tcp</subtype>
    <port>631</port>
    <txt-record>txtver=1</txt-record>
    <txt-record>qtotal=1</txt-record>
    <txt-record>rp=printers/yourPrnterName</txt-record>
    <txt-record>ty=yourPrnterName</txt-record>
    <txt-record>adminurl=http://198.168.7.15:631/printers/yourPrnterName</txt-record>
    <txt-record>note=Office Laserjet 4100n</txt-record>
    <txt-record>priority=0</txt-record>
    <txt-record>product=(GPL Ghostscript)</txt-record>
    <txt-record>printer-state=3</txt-record>
    <txt-record>printer-type=0x801046</txt-record>
    <txt-record>Transparent=T</txt-record>
    <txt-record>Binary=T</txt-record>
    <txt-record>Fax=F</txt-record>
    <txt-record>Color=T</txt-record>
    <txt-record>Duplex=T</txt-record>
    <txt-record>Staple=F</txt-record>
    <txt-record>Copies=T</txt-record>
    <txt-record>Collate=F</txt-record>
    <txt-record>Punch=F</txt-record>
    <txt-record>Bind=F</txt-record>
    <txt-record>Sort=F</txt-record>
    <txt-record>Scan=F</txt-record>
    <txt-record>pdl=application/octet-stream,application/pdf,application/postscript,image/jpeg,image/png,image/urf</txt-record>
    <txt-record>URF=W8,SRGB24,CP1,RS600</txt-record>
  </service>
</service-group>

```

Alternatively, [https://raw.github.com/tjfontaine/airprint-generate/master/airprint-generate.py](https://raw.github.com/tjfontaine/airprint-generate/master/airprint-generate.py) can be used to generate Avahi service files. It depends on python2 and pycups. The script can be run using:

```
# python2 airprint-generate.py -d /etc/avahi/services

```

**Note:** If your printer under [http://localhost:631/printers](http://localhost:631/printers) is "Not Shared", this python script won't output any file to /etc/avahi/services; in that case, you'll need to "Modify Printer" under one of the CUPS drop-down menus to turn sharing on. If that doesn't work, check out the ArchWiki on [CUPS printer sharing](/index.php/CUPS_printer_sharing "CUPS printer sharing").

### Firewall

Be sure to open UDP port 5353 if you're using iptables:

```
 # iptables -A INPUT -p udp -m udp --dport 5353 -j ACCEPT

```

If you're following the more-than-useful [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall") format for your firewall:

```
 # iptables -A UDP -p udp -m udp --dport 5353 -j ACCEPT

```

### Obtaining IPv4LL IP address

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [dhcpcd](/index.php/Dhcpcd "Dhcpcd").**

**Notes:** should be merged into the main page (Discuss in [Talk:Avahi#](https://wiki.archlinux.org/index.php/Talk:Avahi))

By default, if you are getting IP using DHCP, you are using the [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) package. It can attempt to obtain an IPv4LL address if it failed to get one via DHCP. By default this option is disabled. To enable it, comment noipv4ll string:

 `/etc/dhcpcd.conf` 

```
...
#noipv4ll
...
```

Alternatively, run `avahi-autoipd`:

```
# avahi-autoipd -D

```

### Customizing Avahi

#### Adding Services

Avahi advertises the services whose `*.service` files are found in `/etc/avahi/services`. If you want to advertise a service for which there is no `*.service` file, it is very easy to create your own.

As an example, let's say you wanted to advertise a quote of the day (QOTD) service operating per [RFC865](http://tools.ietf.org/html/rfc865) on TCP port 17 which you are running on your machine

The first thing to do is to determine the `<type>`. `man avahi.service` indicates that the type should be "the DNS-SD service type for this service. e.g. '_http._tcp'". Since the [DNS-SD register was merged into the IANA register in 2010](http://www.dns-sd.org/ServiceTypes.html), we look for the service name on the [IANA register](http://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml) or in `/etc/services` file. The service name shown there is `qotd`. Since we're running QOTD on tcp, we now know the service is `_qotd._tcp` and the port (per IANA and RFC865) is 17.

Our `qotd.service` file is thus:

```
<?xml version="1.0" standalone='no'?><!--*-nxml-*-->
<!DOCTYPE service-group SYSTEM "avahi-service.dtd">

<!--
  This file is part of avahi.

  avahi is free software; you can redistribute it and/or modify it
  under the terms of the GNU Lesser General Public License as
  published by the Free Software Foundation; either version 2 of the
  License, or (at your option) any later version.

  avahi is distributed in the hope that it will be useful, but
  WITHOUT ANY WARRANTY; without even the implied warranty of
  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU
  General Public License for more details.

  You should have received a copy of the GNU Lesser General Public
  License along with avahi; if not, write to the Free Software
  Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA
  02111-1307 USA.
-->

<!-- See avahi.service(5) for more information about this configuration file -->

<service-group>

  <name replace-wildcards="yes">%h</name>

  <service>
    <type>_qotd._tcp</type>
    <port>17</port>
  </service>

</service-group>

```

For more complicated scenarios, such as advertising services running on a different server, DNS sub-types and so on, consult `man avahi.service`.

#### Modifying the service-types database

As noted above, avahi comes with tools to browse advertised services. Both `avahi-browse` and `avahi-discover` use a database file to furnish descriptions of the relevant service. That database contains the names of many, but not all, services.

Sadly, it doesn't contain the QOTD service we just created. Thus `avahi-browse -a` would show the following ugly entry

```
+ wlp2s0 IPv4 MyServer                                        _qotd._tcp local

```

##### Getting the Sources

First, download the files `build-db.in` and `service-types` files from the `service-type-database` subdirectory in the [the avahi github mirror](https://github.com/Distrotech/avahi) to a build directory.

```
wget [https://raw.githubusercontent.com/Distrotech/avahi/distrotech-avahi/service-type-database/build-db.in](https://raw.githubusercontent.com/Distrotech/avahi/distrotech-avahi/service-type-database/build-db.in)
wget [https://raw.githubusercontent.com/Distrotech/avahi/distrotech-avahi/service-type-database/service-types](https://raw.githubusercontent.com/Distrotech/avahi/distrotech-avahi/service-type-database/service-types)

```

##### Modify the Sources

Second, create the following script:

```
#!/bin/bash
sed -e 's,@PYTHON\@,/usr/bin/python2.7,g' \
    -e 's,@DBM\@,gdbm,g' < build-db.in > build-db
chmod +x build-db

```

This mimics what the Makefile would do if one were building all of avahi. It creates a file named build-db.

```
$./whatever_you_named_the_script.sh
$ ls
build-db build-db.in service-types whatever_you_named_the_script.sh

```

Third, make the changes needed to add your new QOTD service to the `service-types` file. This file has one entry per line, with the entries in the format `type:Human Readable Description`. Note that the human readable description can contain spaces.

In our example, we add the following entry to the end of the file:

```
_qotd._tcp:Quote of the Day (QOTD) Server

```

##### Build and Install the New Database

Now run the `build-db` python script (be sure to use python2 not python3). This will build the `service-types.db` file. Check to make sure it's been built and use `gdbmtools` to make sure the new database is loadable and contains the new entry:

```
$/usr/bin/python2.7 build-db
$ls
build-db build-db.in service-types service-types.db whatever_you_named_the_script.sh
$gdbmtool service-types.db

Welcome to the gdbm tool.  Type ? for help.

gdbmtool>fetch _qotd._tcp
Quote of the Day (QOTD) Server
gdbmtool>quit

```

Now copy the old database to a backup location, move the new database to the live directory and use `avahi-browse` database dump command to make sure avahi sees the new entry:

```
$cp /usr/lib/avahi/service-types.db /backup-directory
$sudo cp /build-directory/service-types.db /usr/lib/avahi/service-types.db
$avahi-browse -b | grep QOTD
Quote of the Day (QOTD) Server

```

The entry in `avahi-browse` should now be:

```
+ wlp2s0 IPv4 MyServer                                        Quote of the Day (QOTD) Server local

```

## See also

*   [Avahi](http://avahi.org/) - Official project website
*   [Wikipedia entry](http://en.wikipedia.org/wiki/Avahi_%28software%29)
*   [Bonjour for Windows](http://www.apple.com/support/downloads/bonjourforwindows.html) - Enable Zeroconf on Windows
*   [http://www.zeroconf.org/](http://www.zeroconf.org/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Avahi&oldid=413078](https://wiki.archlinux.org/index.php?title=Avahi&oldid=413078)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Networking](/index.php/Category:Networking "Category:Networking")

Hidden category:

*   [Pages or sections flagged with Template:Merge](/index.php/Category:Pages_or_sections_flagged_with_Template:Merge "Category:Pages or sections flagged with Template:Merge")