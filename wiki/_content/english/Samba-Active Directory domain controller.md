Related articles

*   [Active Directory Integration](/index.php/Active_Directory_Integration "Active Directory Integration")
*   [Samba](/index.php/Samba "Samba")
*   [SOGo](/index.php/SOGo "SOGo")

This article explains how to setup an Active Directory domain controller using [Samba](/index.php/Samba "Samba"). It is assumed that all configuration files are in their unmodified, post-installation state. This article was written and tested on a fresh installation, with no modifications other than setting up a static IPv4 network connection, and adding openssh and vim (which should have no effect on the Samba configuration). Finally, most of the commands below will require elevated privileges. Despite conventional wisdom, it may be easier to run these short few commands from a root session as opposed to obtaining rights on an as needed basis.

## Contents

*   [1 Installation](#Installation)
*   [2 Creating a new directory](#Creating_a_new_directory)
    *   [2.1 Provisioning](#Provisioning)
        *   [2.1.1 Argument explanations](#Argument_explanations)
        *   [2.1.2 Interactive provision explanations](#Interactive_provision_explanations)
    *   [2.2 Configuring daemons](#Configuring_daemons)
        *   [2.2.1 NTPD](#NTPD)
        *   [2.2.2 BIND](#BIND)
        *   [2.2.3 Kerberos client utilities](#Kerberos_client_utilities)
        *   [2.2.4 DNS](#DNS)
        *   [2.2.5 Samba](#Samba)
    *   [2.3 Testing the installation](#Testing_the_installation)
        *   [2.3.1 DNS](#DNS_2)
        *   [2.3.2 NT authentication](#NT_authentication)
        *   [2.3.3 Kerberos](#Kerberos)
    *   [2.4 Additional configuration](#Additional_configuration)
        *   [2.4.1 DNS](#DNS_3)
        *   [2.4.2 TLS](#TLS)
*   [3 Adding a second domain controller to an existing domain](#Adding_a_second_domain_controller_to_an_existing_domain)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 DHCP with dynamic DNS updates](#DHCP_with_dynamic_DNS_updates)
    *   [4.2 Transferring users from one directory to another](#Transferring_users_from_one_directory_to_another)
    *   [4.3 Password Complexity](#Password_Complexity)

## Installation

**Note:** Make sure you can access the machines in your network via their hostname. See [Network configuration#Local network hostname resolution](/index.php/Network_configuration#Local_network_hostname_resolution "Network configuration") for more information.

A fully functional samba domain controller requires several programs beyond those included with the Samba distribution. [Install](/index.php/Install "Install") the [bind-tools](https://www.archlinux.org/packages/?name=bind-tools), [krb5](https://www.archlinux.org/packages/?name=krb5), [ntp](https://www.archlinux.org/packages/?name=ntp), [openresolv](https://www.archlinux.org/packages/?name=openresolv) and [samba](https://www.archlinux.org/packages/?name=samba) packages.

Samba contains its own fully functional DNS server, but if you need to maintain DNS zones for external domains, you are strongly encouraged to use [BIND](/index.php/BIND "BIND") instead. If you need to share printers, you will also need [CUPS](/index.php/CUPS "CUPS"). If needed, install the [bind](https://www.archlinux.org/packages/?name=bind) and/or [cups](https://www.archlinux.org/packages/?name=cups) packages.

## Creating a new directory

### Provisioning

The first step to creating an Active Directory domain is provisioning. This involves setting up the internal [LDAP](/index.php/LDAP "LDAP"), [Kerberos](/index.php/Kerberos "Kerberos"), and DNS servers and performing all of the basic configuration needed for the directory. If you have set up a directory server before, you are undoubtedly aware of the potential for errors in making these individual components work together as a single unit. The difficulty in doing so is the very reason that the Samba developers chose provide internal versions of these programs. The server packages above were installed only for the client utilities. Provisioning is quite a bit easier with Samba. Just issue the following command:

```
# samba-tool domain provision --use-rfc2307 --interactive

```

#### Argument explanations

	--use-rfc2307

	this argument adds POSIX attributes (UID/GID) to the AD Schema. This will be necessary if you intend to authenticate Linux, BSD, or macOS clients (including the local machine) in addition to Microsoft Windows.

	--interactive

	this parameter forces the provision script to run interactively. Alternately, you can review the help for the provision step by running `samba-tool domain provision --help`.

#### Interactive provision explanations

	Realm

	**INTERNAL.DOMAIN.COM** - This should be the same as the DNS domain in all caps. It is common to use an internal-only sub-domain to separate your internal domain from your external DNS domains, but it is not required.

	Domain

	**INTERNAL** - This will be the NetBIOS domain name, usually the leftmost DNS sub-domain but can be anything you like. For example, the name INTERNAL would not be very descriptive. Perhaps company name or initials would be appropriate. This should be entered in all caps, and should have a 15 character maximum length for compatibility with older clients.

	Server Role

	**dc** - This article assumes that your are installing the first DC in a new domain. If you select anything different, the rest of this article will likely be useless to you.

	DNS Backend

	**BIND9_DLZ** or **SAMBA_INTERNAL** - This is down to personal preference of the server admin. Again, if you are hosting DNS for external domains, you are strongly encouraged to use the **BIND9_DLZ** backend so that flat zone files can continue to be used and existing transfer rules can co-exist with the internal DNS server. If unsure, use the **SAMBA_INTERNAL** backend.

	Administrator password

	**xxxxxxxx** - You must select a *strong* password for the administrator account. The minimum requirements are one upper case letter, one number, and at least eight characters. If you attempt to use a password that does not meet the complexity requirements, provisioning will fail.

### Configuring daemons

#### NTPD

Create a suitable NTP configuration for your network time server. See [Network Time Protocol daemon](/index.php/Network_Time_Protocol_daemon "Network Time Protocol daemon") for explanations of, and additional configuration options.

Modify the `/etc/ntp.conf` file with the following contents:

 `/etc/ntp.conf` 
```
# Please consider joining the pool:
#
#     http://www.pool.ntp.org/join.html
#
# For additional information see:
# - https://wiki.archlinux.org/index.php/Network_Time_Protocol_daemon
# - http://support.ntp.org/bin/view/Support/GettingStarted
# - the ntp.conf man page

# Associate to Arch's NTP pool
server 0.arch.pool.ntp.org
server 1.arch.pool.ntp.org
server 2.arch.pool.ntp.org
server 3.arch.pool.ntp.org

# Restrictions
restrict default kod limited nomodify notrap nopeer mssntp
restrict 127.0.0.1
restrict ::1
restrict 0.arch.pool.ntp.org mask 255.255.255.255 nomodify notrap nopeer noquery
restrict 1.arch.pool.ntp.org mask 255.255.255.255 nomodify notrap nopeer noquery
restrict 2.arch.pool.ntp.org mask 255.255.255.255 nomodify notrap nopeer noquery
restrict 3.arch.pool.ntp.org mask 255.255.255.255 nomodify notrap nopeer noquery

# Location of drift file
driftfile /var/lib/ntp/ntpd.drift

# Location of the update directory
ntpsigndsocket /var/lib/samba/ntp_signd/

```

Create the state directory and set permissions:

```
# install -d /var/lib/samba/ntp_signd
# chown root:ntp /var/lib/samba/ntp_signd
# chmod 0750 /var/lib/samba/ntp_signd

```

Enable and start the `ntpd.service` unit.

#### BIND

If you elected to use the **BIND9_DLZ** DNS backend, [Install](/index.php/Install "Install") the [bind](https://www.archlinux.org/packages/?name=bind) package and create the following BIND configuration. See [BIND](/index.php/BIND "BIND") for explanations of, and additional configuration options. Be sure to replace the **x** characters with suitable values:

Create the `/etc/named.conf` file:

 `/etc/named.conf` 
```
options {
    directory "/var/named";
    pid-file "/run/named/named.pid";

    // Uncomment these to enable IPv6 connections support
    // IPv4 will still work:
    //  listen-on-v6 { any; };
    // Add this for no IPv4:
    //  listen-on { none; };

    auth-nxdomain yes;
    datasize default;
    empty-zones-enable no;
    tkey-gssapi-keytab "/var/lib/samba/private/dns.keytab";
    forwarders { **xxx.xxx.xxx.xxx**; **xxx.xxx.xxx.xxx**; };

    //  Add any subnets or hosts you want to allow to use this DNS server (use "; " delimiter)
    allow-query     { **xxx.xxx.xxx.xxx/xx**; 127.0.0.0/8; };

    //  Add any subnets or hosts you want to allow to use recursive queries
    allow-recursion { **xxx.xxx.xxx.xxx/xx**; 127.0.0.0/8; };

    //  Add any subnets or hosts you want to allow dynamic updates from
    allow-update    { **xxx.xxx.xxx.xxx/xx**; 127.0.0.0/8; };

    allow-transfer { none; };
    version none;
    hostname none;
    server-id none;
};

zone "localhost" IN {
    type master;
    file "localhost.zone";
};

zone "0.0.127.in-addr.arpa" IN {
    type master;
    file "127.0.0.zone";
};

zone "1.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.ip6.arpa" {
    type master;
    file "localhost.ip6.zone";
};

zone "255.in-addr.arpa" IN {
    type master;
    file "empty.zone";
};

zone "0.in-addr.arpa" IN {
    type master;
    file "empty0.zone";
};

zone "." IN {
    type hint;
    file "root.hint";
};

//Load AD integrated zones
dlz "AD DNS Zones" {
    database "dlopen /usr/lib/samba/bind9/dlz_bind9_10.so";
};

//zone "example.org" IN {
//    type slave;
//    file "example.zone";
//    masters {
//        192.168.1.100;
//    };
//    allow-query { any; };
//    allow-transfer { any; };
//};
//
logging {
    channel xfer-log {
        file "/var/log/named.log";
            print-category yes;
            print-severity yes;
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

Fix for recent versions of bind:

```
# copy /var/named/empty.zone /var/named/empty0.zone
# chown root:named /var/named/empty0.zone

```

Enable and start the `named.service` unit.

Good values for forwarders are your ISP's DNS servers. Google (8.8.8.8, 8.8.4.4, 2001:4860:4860::8888, and 2001:4860:4860::8844) and OpenDNS (208.67.222.222, 208.67.220.220, 2620:0:ccc::2 and 2620:0:ccd::2) provide suitable public DNS servers free of charge. Appropriate values for subnets are specific to your network.

#### Kerberos client utilities

The provisioning step above created a perfectly valid krb5.conf file for use with a Samba domain controller. Install it with the following commands:

```
# mv /etc/krb5.conf{,.default}
# cp /var/lib/samba/private/krb5.conf /etc

```

#### DNS

You will need to begin using the local DNS server now. Reconfigure resolvconf to use only localhost for DNS lookups. Create the `/etc/resolv.conf.tail` (do not forget to substitute **internal.domain.tld** with your internal domain):

```
# Samba configuration
search **internal.domain.tld**
# If using IPv6, uncomment the following line
#nameserver ::1
nameserver 127.0.0.1

```

Set permissions and regenerate the new `/etc/resolv.conf` file:

```
# chmod 644 /etc/resolv.conf.tail
# resolvconf -u

```

#### Samba

Enable and start the `samba.service` unit. If you intend to use the LDB utilities, you will also need create the `/etc/profile.d/sambaldb.sh` file to set **LDB_MODULES_PATH**:

```
export LDB_MODULES_PATH="${LDB_MODULES_PATH}:/usr/lib/samba/ldb"

```

Set permissions on the file and source it:

```
# chmod 0755 /etc/profile.d/sambaldb.sh
# . /etc/profile.d/sambaldb.sh

```

### Testing the installation

#### DNS

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

#### NT authentication

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

#### Kerberos

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

### Additional configuration

#### DNS

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

#### TLS

TLS support is not enabled by default, however, a default certificate was created when the DC was brought up. With the release of Samba 4.3.8 and 4.2.2, unsecured LDAP binds are disabled by default, and you must configure TLS to use Samba as an authentication source (without reducing the security of your Samba installation). To use the default keys, append the following lines to the "**[global]**" section of the `/etc/samba/smb.conf` file:

```
        tls enabled  = yes
        tls keyfile  = tls/key.pem
        tls certfile = tls/cert.pem
        tls cafile   = tls/ca.pem

```

If a trusted certificate is needed, create a signing key and a certificate request (see [OpenSSL](/index.php/OpenSSL "OpenSSL") for detailed instructions). Get the request signed by your chosen certificate authority, and put into this directory. If your certificate authority also needs an intermediate certificate, concatenate the certs (server cert first, then intermediate) and leave **tls cafile** blank.

Restart `samba` for the changes to take effect.

## Adding a second domain controller to an existing domain

TBA...

## Tips and tricks

### DHCP with dynamic DNS updates

It should be noted that using this method will affect functionality of windows clients, as they will still attempt to update DNS on their own. When this occurs, the machine will be denied permission to do so as the record will be owned by the dhcp user rather than the machine account. While this is essentially harmless, it will generate warnings in the system log of the offending machine. You should create a GPO to overcome this, but unfortunately, Samba does not yet have a command line utility to modify GPOs. You will need a Windows PC with the RSAT tools installed. Simply create a dedicated GPO with the Group Policy Editor, and apply only to OUs that contain workstations (so that servers can still update using 'ipconfig /registerdns') and configure the following settings:

```
Computer Configuration
  Policies
    Administrative Templates
      Network
        DNS Client
          Dynamic Update = Disabled
          Register PTR Records = Disabled
```

[Install](/index.php/Install "Install") the [dhcp](https://www.archlinux.org/packages/?name=dhcp) package and the [samba-dhcpd-update](https://aur.archlinux.org/packages/samba-dhcpd-update/) package.

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
NAMESERVER="**server**.${DOMAIN}"
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

subnet **192.168.1.0** netmask **255.255.255.0** {
  range **192.168.1.100** **192.168.1.199**;
  option subnet-mask **255.255.255.0**;
  option routers **192.168.1.254**;
  option domain-name "**internal.domain.tld**";
  option domain-name-servers **192.168.1.1**;
  option broadcast-address **192.168.1.255**;
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

### Transferring users from one directory to another

Unfortunately, there is no built-in utility to export users from one directory to another. This is one way, albeit exceptionally ugly, to get the user specific fields out of your existing SAM and into a suitable LDIF format for ldbmodify:

```
ldbsearch -H /var/lib/samba/private/sam.ldb \
    -s sub -b cn=Users,dc=**internal**,dc=**domain**,dc=**tld** '(objectClass=user)' | \
    grep -e "^\# record" -e "^accountExpires:" -e "^c:" -e "^cn:" -e "^co:" -e "^codePage:" \
         -e "^comment:" -e "^company:" -e "^countryCode:" -e "^department:" \
         -e "^description:" -e "^displayName" -e "^displayNamePrintable:" \
         -e "^distinguishedName" -e "^division:" -e "^dn:" -e "^employeeID:" \
         -e "^facsimileTelephoneNumber:" -e "^generationQualifier:" \
         -e "^givenName" -e "^homeDirectory:" -e "^homeDrive:" -e "^homePhone:" \
         -e "^homePostalAddress:" -e "^info:" -e "^initials:" \
         -e "^internationalISDNNumber:" -e "^ipPhone:" -e "^l:" -e "^mail:" \
         -e "^manager:" -e "^middleName:" -e "^mobile:" -e "^name:" -e "^o:" \
         -e "^objectClass" -e "^otherFacsimileTelephoneNumber:" \
         -e "^otherHomePhone:" -e "^otherIpPhone:" -e "^otherMailbox:" \
         -e "^otherMobile:" -e "^otherPager:" -e "^otherTelephone:" -e "^pager:" \
         -e "^personalTitle:" -e "^physicalDeliveryOfficeName:" -e "^postalAddress:" \
         -e "^postalCode:" -e "^postOfficeBox:" -e "^proxyAddresses\: SMTP" \
         -e "^proxyAddresses: smtp" -e "^referredDeliveryMethod:" \
         -e "^primaryInternationalISDNNumber:" -e "^primaryTelexNumber:" \
         -e "^profilePath:" -e "^registeredAddress:" -e "^sAMAccountName:" \
         -e "^scriptPath:" -e "^sn:" -e "^st:" -e "^street:" -e "^streetAddress:" \
         -e "^telephoneNumber:" -e "^teletexTerminalIdentifier:" \
         -e "^telexNumber:" -e "^title:" -e "^userAccountControl:" -e "^userPrincipalName:"\
         -e "^url:" -e "^userSharedFolder:" -e "^userSharedFolderOther:" -e "^wWWHomePage:" | \
    sed '/^dn:.*/ a\changetype: add' | sed '/^# record/ i\
' > user-export.ldif

```

Explanation: Run an ldbsearch in the users container only, using sub-tree search for objectclass=user. If you need the whole directory, you can modify the search base to use the root or some other OU. The output from ldbsearch is then piped into a really long grep command that returns only appropriate attributes to keep in the new directory. This is obviously subjective, and probably should be tailored to your specific use case. Finally, we use sed to insert the changetype line (needed to tell ldbmodify that we are adding a user), and prefix with a blank line (to make it easier to read) for each exported object.

**Note:** You will need to modify the output file and remove any objects that you don't want transferred. The output file will contain objects (service users, built-ins, etc.) that can break your new directory if you fail to remove them! It will also contain the old domain in both the "dn" and "distinguishedName" attributies that must be changed before import.

To import, after editing the file and transferring to the new server, simply run the following command on your new samba domain controller:

```
ldbmodify -H /var/lib/samba/private/sam.ldb user-export.ldif

```

### Password Complexity

By default, Samba requires strong passwords. To disable the complexity check, issue the following command:

 `# samba-tool domain passwordsettings set --complexity=off`