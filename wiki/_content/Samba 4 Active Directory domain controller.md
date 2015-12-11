# Samba 4 Active Directory domain controller

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Active Directory Integration](/index.php/Active_Directory_Integration "Active Directory Integration")
*   [OpenChange server](/index.php/OpenChange_server "OpenChange server")
*   [Samba](/index.php/Samba "Samba")
*   [Samba/Tips and tricks](/index.php/Samba/Tips_and_tricks "Samba/Tips and tricks")

This article explains how to setup a new Active Directory Domain Controller. It is assumed that all configuration files are in their unmodified, post-installation state. This article was written and tested on a fresh installation, with no modifications other than setting up a staic IPv4 network connection, assigning a hostname, and adding openssh and vim (which should have no effect on the Samba configuration). Finally, most of the commands below will require elevated privileges. Despite conventional wisdom, it may be easier to run these short few commands from a root session as opposed to obtaining rights on an as needed basis.

## Contents

*   [1 Installation](#Installation)
*   [2 Provisioning](#Provisioning)
    *   [2.1 Argument explanations](#Argument_explanations)
    *   [2.2 Interactive provision explanations](#Interactive_provision_explanations)
*   [3 Configuring daemons](#Configuring_daemons)
    *   [3.1 NTPD](#NTPD)
    *   [3.2 BIND](#BIND)
    *   [3.3 Kerberos client utilities](#Kerberos_client_utilities)
    *   [3.4 DNS](#DNS)
    *   [3.5 Samba](#Samba)
*   [4 Testing the installation](#Testing_the_installation)
    *   [4.1 DNS](#DNS_2)
    *   [4.2 NT authentication](#NT_authentication)
    *   [4.3 Kerberos](#Kerberos)
*   [5 Additional configuration](#Additional_configuration)
    *   [5.1 DNS](#DNS_3)
    *   [5.2 SSL](#SSL)
    *   [5.3 DHCP](#DHCP)
*   [6 What to do next](#What_to_do_next)

## Installation

A fully functional samba 4 DC requires several programs beyond those included with the Samba distribution. [Install](/index.php/Install "Install") the [bind-tools](https://www.archlinux.org/packages/?name=bind-tools), [krb5](https://www.archlinux.org/packages/?name=krb5), [ntp](https://www.archlinux.org/packages/?name=ntp), [openldap](https://www.archlinux.org/packages/?name=openldap), [openresolv](https://www.archlinux.org/packages/?name=openresolv) and [samba](https://www.archlinux.org/packages/?name=samba) packages.

Additionally, Samba contains its own fully functional DNS server, but many administrators prefer to use the ISC BIND package. If you need to maintain DNS zones for external domains, you are strongly encouraged to use [bind](https://www.archlinux.org/packages/?name=bind). If you need to share printers, you will also need [cups](https://www.archlinux.org/packages/?name=cups). If needed, install the [bind](https://www.archlinux.org/packages/?name=bind) and/or [cups](https://www.archlinux.org/packages/?name=cups) packages.

## Provisioning

The first step to creating an Active Directory domain is provisioning. If this is the first domain controller in a new domain (as this guide assumes), this involves setting up the internal LDAP, Kerberos, and DNS servers and performing all of the basic configuration needed for the directory. If you have set up a directory server before, you are undoubtedly aware of the potential for errors in making these individual components work together as a single unit. The difficulty in doing so is the very reason that the Samba developers chose not to use the MIT or Heimdal Kerberos server or OpenLDAP server, instead opting for internal versions of these programs. The server packages above were installed only for the client utilities. Provisioning is quite a bit easier with Samba 4\. Just issue the following command:

```
# samba-tool domain provision --use-rfc2307 --use-xattrs=yes --interactive

```

### Argument explanations

--use-rfc2307

this argument adds POSIX attributes (UID/GID) to the AD Schema. This will be necessary if you intend to authenticate Linux, BSD, or OS X clients (including the local machine) in addition to Microsoft Windows.

--use-xattrs=yes

this argument enables the use of unix extended attributes (ACLs) for files hosted on this server. If you intend not have file shares on the domain controller, you can omit this switch (but this is not recommended). You should also ensure that any filesystems that will host Samba shares are mounted with support for ACLs.

--interactive

this parameter forces the provision script to run interactively. Alternately, you can review the help for the provision step by running `samba-tool domain provision --help`.

### Interactive provision explanations

Realm

**INTERNAL.DOMAIN.COM** - This should be the same as the DNS domain in all caps. It is common to use an internal-only sub-domain to separate your internal domain from your external DNS domains, but it is not required.

Domain

**INTERNAL** - This will be the NetBIOS domain name, usually the leftmost DNS sub-domain but can be anything you like. For example, the name INTERNAL would not be very descriptive. Perhaps company name or initials would be appropriate. This should be entered in all caps, and should have a 15 character maximum length for compatibility with older clients.

Server Role

**dc** - This article assumes that your are installing the first DC in a new domain. If you select anything different, the rest of this article will likely be useless to you.

DNS Backend

**BIND9_DLZ** or **SAMBA_INTERNAL** - This is down to personal preference of the server admin. Again, if you are hosting DNS for external domains, you are strongly encouraged to use the **BIND9_DLZ** backend so that flat zone files can continue to be used and existing transfer rules can co-exist with the internal DNS server. If unsure, use the **SAMBA_INTERNAL** backend.

Administrator password

**xxxxxxxx** - You must select a _strong_ password for the administrator account. The minimum requirements are one upper case letter, one number, and at least eight characters. If you attempt to use a password that does not meet the complexity requirements, provisioning will fail.

## Configuring daemons

### NTPD

Create a suitable NTP configuration for your network time server. See [Network Time Protocol daemon](/index.php/Network_Time_Protocol_daemon "Network Time Protocol daemon") for explanations of, and additional configuration options. Create a backup copy of the default file:

```
# mv /etc/ntp.conf{,.default}

```

Create the `/etc/ntp.conf` file with the following contents:

 `/etc/ntp.conf` 

```
# Associate to the public NTP pool servers
server 0.pool.ntp.org
server 1.pool.ntp.org
server 2.pool.ntp.org

# Location of drift file
driftfile /var/lib/ntp/ntpd.drift

# Location of the log file
logfile /var/log/ntpd

# Location of the update directory
ntpsigndsocket /var/lib/samba/ntp_signd/

# Restrictions
restrict default kod limited nomodify notrap nopeer mssntp
restrict 127.0.0.1
restrict ::1
restrict 0.pool.ntp.org mask 255.255.255.255 nomodify notrap nopeer noquery
restrict 1.pool.ntp.org mask 255.255.255.255 nomodify notrap nopeer noquery
restrict 2.pool.ntp.org mask 255.255.255.255 nomodify notrap nopeer noquery

```

Create the state directory and set permissions:

```
# install -d /var/lib/samba/ntp_signd
# chown root:ntp /var/lib/samba/ntp_signd
# chmod 0750 /var/lib/samba/ntp_signd

```

Enable and start the `ntpd.service` unit.

### BIND

If you elected to use the **BIND9_DLZ** DNS backend, [Install](/index.php/Install "Install") the [bind](https://www.archlinux.org/packages/?name=bind) package and create the following BIND configuration. See [BIND](/index.php/BIND "BIND") for explanations of, and additional configuration options. Be sure to replace the **x** characters with suitable values: First, create a backup of the default configuration file:

```
# mv /etc/named.conf{,.default}

```

Create the `/etc/named.conf` file:

 `/etc/named.conf` 

```

// Global options
options {
 auth-nxdomain yes;
 datasize default;
 directory "/var/named";
 empty-zones-enable no;
 pid-file "/run/named/named.pid";
 tkey-gssapi-keytab "/var/lib/samba/private/dns.keytab";
 forwarders { '''xxx.xxx.xxx.xxx'''; '''xxx.xxx.xxx.xxx'''; };
//  Uncomment the next line to enable IPv6
//    listen-on-v6 { any; };
//  Add this for no IPv4:
//    listen-on { none; };
 notify no;
//  Add any subnets or hosts you want to allow to use this DNS server (use "; " delimiter)
 allow-query     { '''xxx.xxx.xxx.xxx/xx'''; 127.0.0.0/8; };
//  Add any subnets or hosts you want to allow to use recursive queries
 allow-recursion { '''xxx.xxx.xxx.xxx/xx'''; 127.0.0.0/8; };
//  Add any subnets or hosts you want to allow dynamic updates from
 allow-update    { '''xxx.xxx.xxx.xxx/xx'''; 127.0.0.0/8; };
 version none;
 hostname none;
 server-id none;
};

//Root servers (required zone for recursive queries)
zone "." IN {
 type hint;
 file "root.hint";
};

//Required localhost forward-/reverse zones
zone "localhost" IN {
 type master;
 file "localhost.zone";
//  allow-transfer { any; };
};
zone "0.0.127.in-addr.arpa" IN {
 type master;
 file "127.0.0.zone";
//  allow-transfer { any; };
};
// Uncomment the following zone for IPv6 support
//zone "1.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.ip6.arpa" IN {
//    type master;
//    file "localhost.ip6.zone";
//    allow-transfer { any; };
//};

//Load AD integrated zones
dlz "AD DNS Zones" {
 database "dlopen /usr/lib/samba/bind9/dlz_bind9_10.so";
};

//Log settings
logging {
channel xfer-log {
    file "/var/log/named.log";
    print-category yes;
    print-severity yes;
    print-time yes;
    severity info;
 };
 category xfer-in { xfer-log; };
 category xfer-out { xfer-log; };
 category notify { xfer-log; };
};

```

Set permissions:

```
# chgrp named /var/lib/samba/private/dns.keytab
# chmod g+r /var/lib/samba/private/dns.keytab
# touch /var/log/named.log
# chown root:named /var/log/named.log
# chmod 664 /var/log/named.log

```

Enable and start the `named.service` unit.

Good values for forwarders are your ISP's DNS servers. Google (8.8.8.8, 8.8.4.4, 2001:4860:4860::8888, and 2001:4860:4860::8844) and OpenDNS (208.67.222.222, 208.67.220.220, 2620:0:ccc::2 and 2620:0:ccd::2) provide suitable public DNS servers free of charge. Appropriate values for subnets are specific to your network.

### Kerberos client utilities

The provisioning step above created a perfectly valid krb5.conf file for use with a Samba 4 DC. Install it with the following commands:

```
# mv /etc/krb5.conf{,.default}
# cp /var/lib/samba/private/krb5.conf /etc

```

### DNS

You will need to begin using the local DNS server now. Reconfigure resolvconf to use only localhost for DNS lookups. Create the `/etc/resolv.conf.tail` (do not forget to substitute **internal.domain.tld** with your internal domain):

```
# Samba configuration
search **internal.domain.tld**
# If using IPv6, uncomment the following line
#nameserver ::1
nameserver 127.0.0.1

```

Set permissions and regenerate the new `/etc/resolv.conf` file

```
# chmod 644 /etc/resolv.conf.tail
# resolvconf -u

```

### Samba

Enable and start the `samba.service` unit. If you intend to use the LDB utilities, you will also need create the `/etc/profile.d/sambaldb.sh` file to set **LDB_MODULES_PATH**:

```
export LDB_MODULES_PATH="${LDB_MODULES_PATH}:/usr/lib/samba/ldb"

```

Set permissions on the file and source it:

```
# chmod 0755 /etc/profile.d/sambaldb.sh
# . /etc/profile.d/sambaldb.sh

```

## Testing the installation

### DNS

First, verify that DNS is working as expected. Execute the following commands substituting appropriate values for **internal.domain.com** and **server**:

```
# host -t SRV _ldap._tcp.**internal.domain.com**.
# host -t SRV _kerberos._udp.**internal.domain.com**.
# host -t A **server**.**internal.domain.com**.

```

You should receive output similar to the following:

```
_ldap._tcp.internal.domain.com has SRV record 0 100 389 server.internal.domain.com.
_kerberos._udp.internal.domain.com has SRV record 0 100 88 server.internal.domain.com.
server.internal.domain.com has address xxx.xxx.xxx.xxx
```

### NT authentication

Next, verify that password authentication is working as expected:

```
# smbclient //localhost/netlogon -U Administrator -c 'ls'

```

You will be prompted for a password (the one you selected earlier), and will get a directory listing like the following:

```
Domain=[INTERNAL] OS=[Unix] Server=[Samba 4.1.2]
  .                                   D        0  Wed Nov 27 23:59:07 2013
  ..                                  D        0  Wed Nov 27 23:59:12 2013

		50332 blocks of size 2097152\. 47185 blocks available
```

### Kerberos

Now verify that the KDC is working as expected. Be sure to replace **INTERNAL.DOMAIN.COM** and use upper case letters:

```
# kinit administrator@**INTERNAL.DOMAIN.COM**

```

You should be prompted for a password and get output similar to the following:

 `Warning: Your password will expire in 41 days on Wed 08 Jan 2014 11:59:11 PM CST` 

Verify that you actually got a ticket:

```
# klist

```

You should get output similar to below:

```
Ticket cache: FILE:/tmp/krb5cc_0
Default principal: administrator@INTERNAL.DOMAIN.COM

Valid starting       Expires              Service principal
11/28/2013 00:22:17  11/28/2013 10:22:17  krbtgt/INTERNAL.DOMAIN.COM@INTERNAL.DOMAIN.COM
	renew until 11/29/2013 00:22:14
```

As a final test, use smbclient with your recently acquired ticket. Replace **server** with the correct server name:

```
# smbclient //**server**/netlogon -k -c 'ls'

```

The output should be the same as when testing password authentication above.

## Additional configuration

### DNS

You will also need to create a reverse lookup zone for each subnet in your environment in DNS. It is important that this is kept in Samba's DNS as opposed to BIND to allow for dynamic updates by cleints. For each subnet, create a reverse lookup zone with the following commands. Replace **server**.**internal**.**domain**.**tld** and **xxx**.**xxx**.**xxx** with appropriate values. For **xxx**.**xxx**.**xxx**, use the first three octets of the subnet in reverse order (for example: 192.168.0.0/24 becomes 0.168.192):

```
# samba-tool dns zonecreate **server**.**internal**.**domain**.**tld** **xxx**.**xxx**.**xxx**.in-addr.arpa -U Administrator

```

Now, add a record for you server (if your server is multi-homed, add for each subnet) again substituting appropriate values as above. **zzz** will be replaced by the fourth octet of the IP for the server:

```
# samba-tool dns add **server**.**internal**.**domain**.**tld** **xxx**.**xxx**.**xxx**.in-addr.arpa **zzz** PTR **server**.**internal**.**domain**.**tld** -U Administrator

```

Restart the `samba` service. If using BIND for DNS, restart the `named` service as well.

Finally, test the lookup. Replace **xxx**.**xxx**.**xxx**.**xxx** with the IP of your server:

```
# host -t PTR **xxx**.**xxx**.**xxx**.**xxx**

```

You should get output similar to the following:

```
xxx.xxx.xxx.xxx.in-addr.arpa domain name pointer server.internal.domain.tld.

```

### SSL

By defualt, SSL support is not enabled, however, a default certificate was created when the DC was brought up. To use the default keys, append the following lines to the "**[global]**" section of the `/etc/samba/smb.conf` file:

```
        tls enabled  = yes
        tls keyfile  = tls/key.pem
        tls certfile = tls/cert.pem
        tls cafile   = tls/ca.pem

```

If a trusted certificate is needed, create a signing key and a certificate request with the following commands (make certain that the Common Name matches the FQDN of the server and do not enter a password):

```
# cd /var/lib/samba/private/tls
# openssl genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:2048 -out **NETBIOS**_KEY.pem
# openssl req -new -key **NETBIOS**_KEY.pem -out **NETBIOS**_CSR.pem

```

Get the CSR signed by your chosen certificate authority, name appropriately (**NETBIOS**_CERT.pem for this example), and put into this directory. If your certifiacte authority also needs an intermedia certificate, put it there as well and use the **tls cafile** parmeter (else leave **tls cafile** blank).

Restart `samba` for the changes to take effect.

### DHCP

It should be noted that using this method will affect functionality of windows clients, as they will still attempt to update DNS on their own. When this occurs, the machine will be denied permission to do so as the record will be owned by the dhcp user rather than the machine account. While this is essentially harmless, it will generate warnings in the system log. You should create a GPO to overcome this, but unfortunately, Samba 4 does not yet have a command line utility to modify GPOs. You will need a Windows PC with the RSAT tools installed. Simply create a dedicated GPO with the Group Policy Editor, and apply only to OUs that contain workstations (so that servers can still update using 'ipconfig /registerdns') and configure the following settings:

```
Computer Configuration
  Policies
    Administrative Templates
      Network
        DNS Client
          Dynamic Update = Disabled
          Register PTR Records = Disabled
```

[Install](/index.php/Install "Install") the [dhcp](https://www.archlinux.org/packages/?name=dhcp) package and the [samba-dhcpd-update](https://aur.archlinux.org/packages/samba-dhcpd-update/)<sup><small>AUR</small></sup> package.

Create an unprivileged user in AD for performing the updates. When prompted for password, use a secure password. 63 random, mixed case, alpha-numeric characters is sufficient. Optionally samba-tool also takes a random argument:

```
# samba-tool user create dhcp --description="Unprivileged user for DNS updates via DHCP server"

```

Since this is a service account, disabling password expiration on the user account is recommended, but not required:

```
# samba-tool user setexpiry dhcp --noexpiry

```

Give the user privileges to administer DNS:

```
# samba-tool group addmembers DnsAdmins dhcp

```

Export the users credentials to a private keytab:

```
# samba-tool domain exportkeytab --principal=dhcp@**INTERNAL**.**DOMAIN**.**TLD** dhcpd.keytab
# install -vdm 755 /etc/dhcpd
# mv dhcpd.keytab /etc/dhcpd
# chown root:root /etc/dhcpd/dhcpd.keytab
# chmod 400 /etc/dhcpd/dhcpd.keytab

```

Modify the `dhcpd-update-samba-dns.conf` file with the following commands (substituting correct values for **server**, **internal**.**domain**.**tld**, and **INTERNAL**.**DOMAIN**.**TLD**):

 `/etc/dhcpd/dhcpd-update-samba-dns.conf` 

```
# Variables
KRB5CC="/run/dhcpd4.krb5cc"
KEYTAB="/etc/dhcpd/dhcpd.keytab"
DOMAIN="**internal**.**domain**.**tld**"
REALM="**INTERNAL**.**DOMAIN**.**TLD**"
PRINCIPAL="dhcp@${REALM}"
NAMESERVER="'''server'''.${DOMAIN}"
ZONE="${DOMAIN}"

```

Configure the dhcpd server following the [dhcpd](/index.php/Dhcpd "Dhcpd") article and add the following to all subnet declarations in the `/etc/dhcpd.conf` file that provide DHCP service:

```
  on commit {
    set ClientIP = binary-to-ascii(10, 8, ".", leased-address);
    set ClientName = pick-first-value(option host-name, host-decl-name);
    execute("/usr/bin/dhcpd-update-samba-dns.sh", "add", ClientIP, ClientName);
  }

  on release {
    set ClientIP = binary-to-ascii(10, 8, ".", leased-address);
    set ClientName = pick-first-value(option host-name, host-decl-name);
    execute("/usr/bin/dhcpd-update-samba-dns.sh", "delete", ClientIP, ClientName);
  }

    on expiry {
    set ClientIP = binary-to-ascii(10, 8, ".", leased-address);
    set ClientName = pick-first-value(option host-name, host-decl-name);
    execute("/usr/bin/dhcpd-update-samba-dns.sh", "delete", ClientIP, ClientName);

```

Here is a complete example `/etc/dhcpd.conf` file for reference:

 `/etc/dhcpd.conf` 

```
# No DHCP service in the DMZ.
subnet 192.168.2.0 netmask 255.255.255.0 {
}

# Internal subnet
subnet 192.168.1.0 netmask 255.255.255.0 {
  range 192.168.1.100 192.168.1.199;
  option subnet-mask 255.255.255.0;
  option routers 192.168.1.254;
  option domain-name "internal.domain.tld";
  option domain-name-servers 192.168.1.1;
  option broadcast-address 192.168.1.255;
  default-lease-time 28800;
  max-lease-time 43200;
  authoritative;

  on commit {
    set ClientIP = binary-to-ascii(10, 8, ".", leased-address);
    set ClientName = pick-first-value(option host-name, host-decl-name);
    execute("/usr/bin/dhcpd-update-samba-dns.sh", "add", ClientIP, ClientName);
  }

  on release {
    set ClientIP = binary-to-ascii(10, 8, ".", leased-address);
    set ClientName = pick-first-value(option host-name, host-decl-name);
    execute("/usr/bin/dhcpd-update-samba-dns.sh", "delete", ClientIP, ClientName);
  }

    on expiry {
    set ClientIP = binary-to-ascii(10, 8, ".", leased-address);
    set ClientName = pick-first-value(option host-name, host-decl-name);
    execute("/usr/bin/dhcpd-update-samba-dns.sh", "delete", ClientIP, ClientName);
  }
}

```

Finally, enable and start (or restart) the `dhcpd4` service.

## What to do next

If you have made it this far without any unexpected output from the tests above, you are good to go. Congrats! Here are some related topics to extend your new AD server:

[Active Directory Integration](/index.php/Active_Directory_Integration "Active Directory Integration") - This article explains how to attach Linux clients to an Active Directory domain.

[OpenChange server](/index.php/OpenChange_server "OpenChange server") - The OpenChange project provides a Microsoft Exchange compatible mail server using only open source software.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Samba_4_Active_Directory_domain_controller&oldid=411462](https://wiki.archlinux.org/index.php?title=Samba_4_Active_Directory_domain_controller&oldid=411462)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Network sharing](/index.php/Category:Network_sharing "Category:Network sharing")