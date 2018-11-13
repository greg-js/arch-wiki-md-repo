[Network Information Service](https://en.wikipedia.org/wiki/Network_Information_Service "wikipedia:Network Information Service") (NIS) is a protocol developed by Sun to allow one to defer user authentication to a server. The server software is in the [ypserv](https://aur.archlinux.org/packages/ypserv/) package, and the client software is in the [yp-tools](https://aur.archlinux.org/packages/yp-tools/) package. [ypbind-mt](https://aur.archlinux.org/packages/ypbind-mt/) is also available, which is a multi threaded version of the client daemon.

**Note:** This article somewhat unfinished. In the future that will change, but in the meantime check the [More resources section](#More_resources).

## Contents

*   [1 NIS Server](#NIS_Server)
    *   [1.1 Install Packages](#Install_Packages)
    *   [1.2 Configuration](#Configuration)
        *   [1.2.1 /etc/hosts](#/etc/hosts)
        *   [1.2.2 /etc/nisdomainname](#/etc/nisdomainname)
        *   [1.2.3 /etc/ypserv.conf](#/etc/ypserv.conf)
        *   [1.2.4 /var/yp/Makefile](#/var/yp/Makefile)
        *   [1.2.5 /var/yp/securenets](#/var/yp/securenets)
        *   [1.2.6 /var/yp/ypservers](#/var/yp/ypservers)
        *   [1.2.7 Set your domain name](#Set_your_domain_name)
    *   [1.3 Start NIS Daemons](#Start_NIS_Daemons)
*   [2 NIS Client](#NIS_Client)
    *   [2.1 Install Packages](#Install_Packages_2)
    *   [2.2 Configuration](#Configuration_2)
        *   [2.2.1 Set your domain name](#Set_your_domain_name_2)
        *   [2.2.2 /etc/hosts](#/etc/hosts_2)
        *   [2.2.3 Start NIS Daemons](#Start_NIS_Daemons_2)
        *   [2.2.4 Early testing](#Early_testing)
        *   [2.2.5 /etc/nsswitch.conf](#/etc/nsswitch.conf)
        *   [2.2.6 /etc/pam.d/passwd](#/etc/pam.d/passwd)
        *   [2.2.7 Attention on Systemd V235 since 10/2017 (and V239 since 06/2018)](#Attention_on_Systemd_V235_since_10/2017_(and_V239_since_06/2018))
*   [3 More resources](#More_resources)

## NIS Server

### Install Packages

[Install](/index.php/Install "Install") the [ypbind-mt](https://aur.archlinux.org/packages/ypbind-mt/), [ypserv](https://aur.archlinux.org/packages/ypserv/), and [yp-tools](https://aur.archlinux.org/packages/yp-tools/) packages.

### Configuration

#### /etc/hosts

Add your server's **external** (not 127.0.0.1) IP address to the hosts file. Make sure it is the first non-commented line in the file, yes, even above the localhost line, like so:

```
#
# /etc/hosts: static lookup table for host names
#

#<ip-address>	<hostname.domain.org>	<hostname>
#::1		localhost.localdomain	localhost
192.168.1.10   nis_server.domain.com   nis_server
127.0.0.1	localhost.localdomain	localhost nis_server
# End of file

```

This is due to a peculiarity in ypinit (maybe it's a bug, maybe it's a feature), which will **always** add the first line in `/etc/hosts` to the list of ypservers.

#### /etc/nisdomainname

Add the domain name to `/etc/nisdomainname`:

```
# NISDOMAINNAME="nis-domain-name"

```

#### /etc/ypserv.conf

Add rules to /etc/ypserv.conf for your your nis clients of this form:

```
# ip-address-of-client : nis-domain-name : rule : security

```

For example:

```
# 192.168. : home-domain : * : port

```

For more information see `man ypserv.conf`.

#### /var/yp/Makefile

Add or remove files you would like NIS to use to /var/yp/Makefile under the "all" rule.

Default:

```
# all:  passwd group hosts rpc services netid protocols netgrp \
#         shadow # publickey networks ethers bootparams printcap mail \
#         # amd.home auto.master auto.home auto.local passwd.adjunct \
#         # timezone locale netmasks

```

After that you have to build your NIS database:

```
# cd /var/yp
# make

```

Or you can do it in a more automated fashion:

```
# /usr/lib/yp/ypinit -m

```

If you use this way you may skip manually adding lines to /var/yp/ypservers.

#### /var/yp/securenets

Add rules to /var/yp/securenets to restrict access:

```
# 255.255.0.0 192.168.0.0 # Gives access to anyone in 192.168.0.0/16

```

Be sure to comment out this line, as it gives access to anyone.

```
# 0.0.0.0      0.0.0.0

```

#### /var/yp/ypservers

Add your server to /var/yp/ypservers:

```
# your.nis.server

```

#### Set your domain name

```
# ypdomainname EXAMPLE.COM

```

Now edit the /etc/yp.conf file and add your ypserver or nis server.

```
ypserver nis_server

```

### Start NIS Daemons

**Note:** The daemons MUST be started in this order.

[Start/enable](/index.php/Start/enable "Start/enable") the following systemd units:

*   `rpcbind.service`
*   `ypbind.service`
*   `ypserv.service`
*   `yppasswdd.service` (to allow clients to change their password with `passwd`)

## NIS Client

### Install Packages

The first step is to install the tools that you need. This provides the configuration files and general tools needed to use NIS.

```
# pacman -S yp-tools ypbind-mt

```

**Warning:** To users of server-side port security: Due to a problem in libtirpc 1.0.3, ypbind-mt won't be able to retrieve port-secured content anymore. Downgrading to libtirpc-1.0.2-3 fixes the issue for now. Watch [https://github.com/thkukuk/ypbind-mt/issues/1](https://github.com/thkukuk/ypbind-mt/issues/1) and [https://bugs.archlinux.org/index.php?do=details&task_id=58502](https://bugs.archlinux.org/index.php?do=details&task_id=58502) until it got fixed.

### Configuration

#### Set your domain name

```
# ypdomainname EXAMPLE.COM

```

You can apply this permanently by editing /etc/nisdomainname and adding:

```
# NISDOMAINNAME="EXAMPLE.COM"

```

Now edit the /etc/yp.conf file and add your ypserver or nis server.

```
ypserver nis_server

```

#### /etc/hosts

It may be a good idea to add your NIS server to /etc/hosts

```
192.168.1.10   nis_server.domain.com   nis_server

```

#### Start NIS Daemons

**Note:** The daemons MUST be started in this order.

[Start/enable](/index.php/Start/enable "Start/enable") the `rpcbind.service` and `ypbind.service` systemd units.

#### Early testing

To test the setup so far you can run the command yptest:

```
# yptest

```

If it works you will, among other things, see the contents of the NIS user database (which is printed in the same format as /etc/passwd).

#### /etc/nsswitch.conf

To actually use NIS to log in you have to edit /etc/nsswitch.conf. Modify the lines for passwd, group and shadow to read:

```
passwd: files nis
group: files nis
shadow: files nis

```

And then do not forget

```
# systemctl restart ypbind

```

#### /etc/pam.d/passwd

To allow a user on a client machine to change their password on the server, be sure that `yppasswdd.service` is started/enabled on the server.

Edit `/etc/pam.d/passwd` on the client to add the `nis` parameter to `password/pam_unix.so`:

```
password     required     pam_unix.so sha512 shadow nullok nis

```

See [section 7 of The Linux NIS HOWTO](http://www.tldp.org/HOWTO/NIS-HOWTO/settingup_client.html) for further information on configuring NIS clients.

#### Attention on Systemd V235 since 10/2017 (and V239 since 06/2018)

Due a problem with sandboxing on `systemd-logind`, any IP connections from and to the `systemd-logind` service are now denied. This will cause failures to log in, even though `yptest` works as expected, and can also cause `accounts-daemon` to crash outright. The basic problem is that the default `/usr/lib/systemd/system/systemd-logind.service` file that ships with `systemd` specifies `IPAddressDeny=any`, and this prevents it from communicating with the NIS server at login. Moreover, since V239, that file also specifies `RestrictAddressFamilies=AF_UNIX AF_NETLINK`, dropping `AF_INET AF_INET6` from the list.

There are a few possible solutions:

*   **Whitelist the address or address range of your NIS server:**

This can be done by creating a new `.conf` file within the `/etc/systemd/system/systemd-logind.service.d/`, with these lines (the following allows connections `from 10.0.*.*`, edit as appropriate): `/etc/systemd/system/systemd-logind.service.d/open_network_interface.conf` 
```
[Service]
RestrictAddressFamilies=AF_UNIX AF_NETLINK AF_INET AF_INET6
IPAddressAllow=10.0.0.0/16
```
This survives a reboot and updates of the systemd toolchain. It also avoid having to open your system to any IP address.
**Note:** there is no point in using `IPAddressAllow=any`, this is does *not* override the default `IPAddressDeny=any` set in the main unit file.

*   **Override the system's default `systemd-logind.service` with a modified local version:**

```
# cp -a /usr/lib/systemd/system/systemd-logind.service /etc/systemd/system
# nano /etc/systemd/system/systemd-logind.service 

```

and comment out the line `IPAddressDeny=any` to read `# IPAddressDeny=any`. As of V239, you will also need to add `AF_INET AF_INET6` to the `RestrictAddressFamilies=AF_UNIX AF_NETLINK` line.

This solution survives an update of the systemd toolchain and keeps working after a reboot. It does however override *all* settings in the unit file supplied with `systemd`, which may cause issues down the track if other unrelated settings are changed upstream. It also opens up access to *any* IP address, which is not recommended.

*   **Modify the system's default `systemd-logind.service` directly:**

Works, but not a recommended solution since it will not survive an update of the systemd toolchain:

```
# nano /usr/lib/systemd/system/systemd-logind.service 

```

and comment out the line `IPAddressDeny=any` to read `# IPAddressDeny=any`. As of V239, you will also need to add `AF_INET AF_INET6` to the `RestrictAddressFamilies=AF_UNIX AF_NETLINK` line.

Note that this also opens up access to *any* IP address, which is not recommended.

## More resources

*   [The Linux NIS HOWTO](http://www.tldp.org/HOWTO/NIS-HOWTO/),very helpful and generally applicable to Arch Linux.
*   [YoLinux NIS tutorial](http://www.yolinux.com/TUTORIALS/NIS.html)
*   [Quick HOWTO, Configuring NIS](http://www.linuxhomenetworking.com/wiki/index.php/Quick_HOWTO_:_Ch30_:_Configuring_NIS)