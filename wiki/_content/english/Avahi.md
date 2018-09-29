From [Wikipedia:Avahi (software)](https://en.wikipedia.org/wiki/Avahi_(software) "wikipedia:Avahi (software)"):

	[Avahi](http://avahi.org/) is a free [Zero-configuration networking](https://en.wikipedia.org/wiki/Zero-configuration_networking "wikipedia:Zero-configuration networking") (zeroconf) implementation, including a system for multicast DNS/DNS-SD service discovery. It allows programs to publish and discover services and hosts running on a local network with no specific configuration. For example you can plug into a network and instantly find printers to print to, files to look at and people to talk to. It is licensed under the GNU Lesser General Public License (LGPL).

## Contents

*   [1 Installation](#Installation)
*   [2 Using Avahi](#Using_Avahi)
    *   [2.1 Hostname resolution](#Hostname_resolution)
        *   [2.1.1 Configuring mDNS for custom TLD](#Configuring_mDNS_for_custom_TLD)
        *   [2.1.2 Tools](#Tools)
    *   [2.2 Firewall](#Firewall)
    *   [2.3 Link-Local (Bonjour/Zeroconf) chat](#Link-Local_.28Bonjour.2FZeroconf.29_chat)
    *   [2.4 Obtaining IPv4LL IP address](#Obtaining_IPv4LL_IP_address)
*   [3 Adding services](#Adding_services)
    *   [3.1 SSH](#SSH)
    *   [3.2 File sharing](#File_sharing)
        *   [3.2.1 NFS](#NFS)
        *   [3.2.2 Samba](#Samba)
        *   [3.2.3 Vsftpd](#Vsftpd)
    *   [3.3 AirPrint from Mobile Devices](#AirPrint_from_Mobile_Devices)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Hostname changes with appending incrementing numbers](#Hostname_changes_with_appending_incrementing_numbers)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [avahi](https://www.archlinux.org/packages/?name=avahi) package.

You can manage the Avahi daemon with `avahi-daemon.service` [using systemd](/index.php/Systemd#Using_units "Systemd").

**Note:** [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved") has a built-in multicast DNS service, make sure to disable systemd-resolved's mDNS resolver and responder or [disable](/index.php/Disable "Disable") `systemd-resolved.service` entirely before using Avahi. For details, refer to [resolved.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolved.conf.5).

## Using Avahi

### Hostname resolution

Avahi provides local hostname resolution using a "*hostname*.local" naming scheme. To enable it, install the [nss-mdns](https://www.archlinux.org/packages/?name=nss-mdns) package and [start](/index.php/Start "Start") `avahi-daemon.service`.

Then, edit the file `/etc/nsswitch.conf` and change the `hosts` line to include `mdns_minimal [NOTFOUND=return]` before `resolve` and `dns`:

```
hosts: ... **mdns_minimal [NOTFOUND=return]** resolve [!UNAVAIL=return] dns ...

```

**Note:** If you experience slowdowns in resolving `.local` hosts try to use `mdns4_minimal` instead of `mdns_minimal`.

#### Configuring mDNS for custom TLD

The `mdns_minimal` module handles queries for the `.local` TLD only. Note the `[NOTFOUND=return]`, which specifies that if `mdns_minimal` cannot find `*.local`, it will not continue to search for it in `dns`, `myhostname`, etc.

In case you want Avahi to support other TLDs, you should:

*   replace `mdns_minimal [NOTFOUND=return]` with the full `mdns` module. There also are IPv4-only and IPv6-only modules `mdns[46](_minimal)`
*   customize `/etc/avahi/avahi-daemon.conf` with the `domain-name` of your choice
*   whitelist Avahi custom TLDs in `/etc/mdns.allow`

#### Tools

Avahi includes several utilities which help you discover the services running on a network. For example, run

```
$ avahi-browse -alr

```

to discover services in your network.

The Avahi Zeroconf Browser (`avahi-discover` – note that it needs avahi's optional dependencies [gtk3](https://www.archlinux.org/packages/?name=gtk3), [python-dbus](https://www.archlinux.org/packages/?name=python-dbus) and [python-gobject](https://www.archlinux.org/packages/?name=python-gobject)) shows the various services on your network. You can also browse SSH and VNC Servers using `bssh` and `bvnc` respectively.

### Firewall

Be sure to open UDP port `5353` if you're using a [firewall](/index.php/Firewall "Firewall").

### Link-Local (Bonjour/Zeroconf) chat

Avahi can be used for bonjour protocol support under linux. Check [Wikipedia:Comparison of instant messaging clients](https://en.wikipedia.org/wiki/Comparison_of_instant_messaging_clients "wikipedia:Comparison of instant messaging clients") or [List of applications#Instant messaging clients](/index.php/List_of_applications#Instant_messaging_clients "List of applications") for a list of clients supporting the bonjour protocol.

### Obtaining IPv4LL IP address

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

## Adding services

Avahi advertises the services whose `*.service` files are found in `/etc/avahi/services`. Files in this directory must be readable by the `avahi` user/group.

If you want to advertise a service for which there is no `*.service` file, it is very easy to create your own. As an example, let's say you wanted to advertise a quote of the day (QOTD) service operating per RFC 865 on TCP port `17` which you are running on your machine

The first thing to do is to determine the `<type>`. [avahi.service(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/avahi.service.5) indicates that the type should be "the DNS-SD service type for this service. e.g. '_http._tcp'". Since the [DNS-SD register was merged into the IANA register in 2010](http://www.dns-sd.org/ServiceTypes.html), we look for the service name on the [IANA register](http://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml) or in `/etc/services` file. The service name shown there is `qotd`. Since we're running QOTD on tcp, we now know the service is `_qotd._tcp` and the port (per IANA and RFC 865) is `17`.

Our service file is thus:

 `qotd.service` 
```
<?xml version="1.0" standalone='no'?><!--*-nxml-*-->
<!DOCTYPE service-group SYSTEM "avahi-service.dtd">

<service-group>

  <name replace-wildcards="yes">%h</name>

  <service>
    <type>_qotd._tcp</type>
    <port>17</port>
  </service>

</service-group>

```

For more complicated scenarios, such as advertising services running on a different server, DNS sub-types and so on, consult [avahi.service(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/avahi.service.5).

### SSH

Avahi comes with an example service file to advertise a SSH server. To enable it:

```
# cp /usr/share/doc/avahi/ssh.service /etc/avahi/services/

```

### File sharing

#### NFS

If you have an [NFS](/index.php/NFS "NFS") share set up, you can use Avahi to be able to automount them in Zeroconf-enabled browsers (such as Konqueror on KDE and Finder on macOS) or file managers such as [GNOME/Files](/index.php/GNOME/Files "GNOME/Files").

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

The port is correct if you have *insecure* as an option in your `/etc/exports`; otherwise, it needs to be changed (note that *insecure* is needed for macOS clients). The path is the path to your export, or a subdirectory of it. For some reason the automount functionality has been removed from Leopard, however [a script is available](http://www.macosxhints.com/article.php?story=20071116042238744). This was based upon [this post](http://ubuntuforums.org/showthread.php?p=4387032#post4387032).

#### Samba

With the Avahi daemon running on both the server and client, the file manager on the client should automatically find the server.

#### Vsftpd

You can also auto-discover regular FTP servers, such as [vsftpd](/index.php/Vsftpd "Vsftpd"). Install the [vsftpd](https://www.archlinux.org/packages/?name=vsftpd) package and change the settings of vsftpd according to your own personal preferences (see [this thread on ubuntuforums.org](http://ubuntuforums.org/showthread.php?t=218630) or [vsftpd.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vsftpd.conf.5)).

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

The FTP server should now be advertised by Avahi. You should now be able to find the FTP server from a file manager on another computer in your network. You might need to enable [#Hostname resolution](#Hostname_resolution) on the client.

### AirPrint from Mobile Devices

Avahi along with [CUPS](/index.php/CUPS "CUPS") also provides the capability to print to just about any printer from airprint compatible mobile devices. In order to enable print capability from your device, simply create an Avahi service file for your printer in `/etc/avahi/services/`. An example of a generic services file for an HP-Laserjet printer would be similar to the following with the `name`, `rp`, `ty`, `adminurl` and `note` fields changed.

 `/etc/avahi/services/airprint.service` 
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

Alternatively, [https://raw.github.com/tjfontaine/airprint-generate/master/airprint-generate.py](https://raw.github.com/tjfontaine/airprint-generate/master/airprint-generate.py) can be used to generate Avahi service files. It depends on [python2](https://www.archlinux.org/packages/?name=python2) and [python2-pycups](https://www.archlinux.org/packages/?name=python2-pycups). The script can be run using:

```
# python2 airprint-generate.py -d /etc/avahi/services

```

**Note:** If your printer under [http://localhost:631/printers](http://localhost:631/printers) is "Not Shared", this python script won't output any file to /etc/avahi/services; in that case, you'll need to "Modify Printer" under one of the CUPS drop-down menus to turn sharing on. If that doesn't work, check out the ArchWiki on [CUPS printer sharing](/index.php/CUPS_printer_sharing "CUPS printer sharing").

## Troubleshooting

### Hostname changes with appending incrementing numbers

This is a [known bug](https://github.com/lathiat/avahi/issues/117) that is caused by a hostname race condition. As a temporary workaround [disabling IPv6 will make the bug less common](https://github.com/lathiat/avahi/issues/117#issuecomment-302849130).

## See also

*   [Avahi](http://avahi.org/) - Official project website
*   [Wikipedia:Avahi (software)](https://en.wikipedia.org/wiki/Avahi_(software) "wikipedia:Avahi (software)")
*   [iTunes (includes Bonjour)](https://www.apple.com/itunes/download/) - Enable Zeroconf on Windows
*   [http://www.zeroconf.org/](http://www.zeroconf.org/)