# NIS

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Network Information Service (NIS) is a protocol developed by Sun to allow one to defer user authentication to a server. The server software is in the [ypserv](https://www.archlinux.org/packages/?name=ypserv) package, and the client software is in the [yp-tools](https://www.archlinux.org/packages/?name=yp-tools) package. [ypbind-mt](https://www.archlinux.org/packages/?name=ypbind-mt) is also available, which is a multi threaded version of the client daemon.

**Note:** This article somewhat unfinished. In the future that will change, but in the meantime check the [More resources section](#More_resources).

## Contents

*   [1 NIS Server](#NIS_Server)
    *   [1.1 Install Packages](#Install_Packages)
    *   [1.2 Configuration](#Configuration)
        *   [1.2.1 /etc/hosts](#.2Fetc.2Fhosts)
        *   [1.2.2 /etc/nisdomainname](#.2Fetc.2Fnisdomainname)
        *   [1.2.3 /etc/ypserv.conf](#.2Fetc.2Fypserv.conf)
        *   [1.2.4 /var/yp/Makefile](#.2Fvar.2Fyp.2FMakefile)
        *   [1.2.5 /var/yp/securenets](#.2Fvar.2Fyp.2Fsecurenets)
        *   [1.2.6 /var/yp/ypservers](#.2Fvar.2Fyp.2Fypservers)
        *   [1.2.7 Set your domain name](#Set_your_domain_name)
    *   [1.3 Start NIS Daemons](#Start_NIS_Daemons)
*   [2 NIS Client](#NIS_Client)
    *   [2.1 Install Packages](#Install_Packages_2)
    *   [2.2 Configuration](#Configuration_2)
        *   [2.2.1 Set your domain name](#Set_your_domain_name_2)
        *   [2.2.2 /etc/hosts](#.2Fetc.2Fhosts_2)
        *   [2.2.3 Start NIS Daemons](#Start_NIS_Daemons_2)
        *   [2.2.4 Early testing](#Early_testing)
        *   [2.2.5 /etc/nsswitch.conf](#.2Fetc.2Fnsswitch.conf)
*   [3 More resources](#More_resources)

## NIS Server

### Install Packages

Make sure packages ypbind-mt, ypserv, yp-tools and make are installed:

```
# pacman -S ypbind-mt yp-tools ypserv make

```

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

Start rpcbind if it isn't already started:

```
# systemctl start rpcbind

```

Start ypbind:

```
# systemctl start ypbind

```

Start ypserv:

```
# systemctl start ypserv

```

Use systemctl enable instead of start to make the daemons load at every boot.

## NIS Client

### Install Packages

The first step is to install the tools that you need. This provides the configuration files and general tools needed to use NIS.

```
# pacman -S yp-tools ypbind-mt

```

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

Start the rpcbind and ypbind daemons.

```
# systemctl start rpcbind
# systemctl start ypbind

```

Use systemctl enable instead of start to make the daemons load at every boot.

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

See [section 7 of The Linux NIS HOWTO](http://www.tldp.org/HOWTO/NIS-HOWTO/settingup_client.html) for further information on configuring NIS clients.

## More resources

*   [The Linux NIS HOWTO](http://www.tldp.org/HOWTO/NIS-HOWTO/),very helpful and generally applicable to Arch Linux.
*   [YoLinux NIS tutorial](http://www.yolinux.com/TUTORIALS/NIS.html)
*   [Quick HOWTO, Configuring NIS](http://www.linuxhomenetworking.com/wiki/index.php/Quick_HOWTO_:_Ch30_:_Configuring_NIS)

Retrieved from "[https://wiki.archlinux.org/index.php?title=NIS&oldid=416064](https://wiki.archlinux.org/index.php?title=NIS&oldid=416064)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Security](/index.php/Category:Security "Category:Security")