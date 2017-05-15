[vpnc](https://www.unix-ag.uni-kl.de/~massar/vpnc/) is a VPN client for Cisco hardware VPNs.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Starting](#Starting)
*   [4 Troubleshooting](#Troubleshooting)

## Installation

[Install](/index.php/Install "Install") the [vpnc](https://www.archlinux.org/packages/?name=vpnc) package.

## Configuration

The vpnc configuration files are in `/etc/vpnc`. It contains a `default.conf` file that you can copy and modify for your setup.

Executing `vpnc --long-help` will provide the names and descriptions of the various configuration options. For instance, in that output you will see

```
 --gateway <ip/hostname>
     IP/name of your IPSec gateway
 conf-variable: IPSec gateway<ip/hostname>

```

which translates into a line like this in your configuration file:

```
IPSec gateway gateway.example.com

```

## Starting

The `vpnc` package comes with a [systemd](/index.php/Systemd#Using_units "Systemd") unit `vpnc@.service`. If you want to use the configuration file `/etc/vpnc/client.conf`, you would start it with `systemctl start vpnc@client`.

## Troubleshooting

In case the vpnc client crashes with:

```
   May 15 09:11:38 ntrp-mimacom systemd-coredump[5858]: Process 5814 (vpnc) of user 0 dumped core.

                                                        Stack trace of thread 5814:
                                                        #0  0x00007f835cba3a10 raise (libc.so.6)
                                                        #1  0x00007f835cba513a abort (libc.so.6)
                                                        #2  0x00007f835cb9c607 __assert_fail_base (libc.so.6)
                                                        #3  0x00007f835cb9c6b2 __assert_fail (libc.so.6)
                                                        #4  0x000000000040e48c n/a (vpnc)
                                                        #5  0x0000000000412348 n/a (vpnc)
                                                        #6  0x0000000000404f72 n/a (vpnc)
                                                        #7  0x00007f835cb90511 __libc_start_main (libc.so.6)
                                                        #8  0x000000000040596a n/a (vpnc)

```

you will need to monkey patch the the software because an assertion is failing with the latest updates..

Download the sources from [http://svn.unix-ag.uni-kl.de/vpnc/trunk/](http://svn.unix-ag.uni-kl.de/vpnc/trunk/) and patch the file vpnc.c with the following:

```
   Index: vpnc.c
   ===================================================================
   --- vpnc.c      (revision 550)
   +++ vpnc.c      (working copy)
   @@ -1206,7 +1206,7 @@
           assert(a->af == isakmp_attr_16);
           assert(a->u.attr_16 == IKE_LIFE_TYPE_SECONDS || a->u.attr_16 == IKE_LIFE_TYPE_K);
           assert(a->next != NULL);
   -       assert(a->next->type == IKE_ATTRIB_LIFE_DURATION);
   +       /* assert(a->next->type == IKE_ATTRIB_LIFE_DURATION); */

           if (a->next->af == isakmp_attr_16)
                   value = a->next->u.attr_16;

```

Temporary workaround found here: [https://bbs.archlinux.org/viewtopic.php?id=225556](https://bbs.archlinux.org/viewtopic.php?id=225556)

Remember to change the PREFIX to /user instead /user/local so you overwrite the broken binary.