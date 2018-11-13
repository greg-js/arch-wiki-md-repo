**ppp** (Paul's PPP Package) is an open source package which implements the [point-to-point protocol](https://en.wikipedia.org/wiki/point-to-point_protocol "wikipedia:point-to-point protocol") (PPP) on Linux and Solaris systems. It is implemented as single *pppd* daemon and acts as backend for [xl2tpd](https://www.archlinux.org/packages/?name=xl2tpd), [pptpd](https://www.archlinux.org/packages/?name=pptpd) and [netctl](/index.php/Netctl "Netctl"). [3G](https://en.wikipedia.org/wiki/3G "wikipedia:3G"), [L2TP](https://en.wikipedia.org/wiki/L2TP "wikipedia:L2TP") and [PPPoE](https://en.wikipedia.org/wiki/PPPoE "wikipedia:PPPoE") connections are internally based on PPP protocol and therefore can be managed by ppp.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 PPPoE](#PPPoE)
    *   [2.2 Easy wizard configuration](#Easy_wizard_configuration)
    *   [2.3 Starting pppd on boot](#Starting_pppd_on_boot)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Do an auto redial](#Do_an_auto_redial)
    *   [3.2 ISP auto-disconnect after 24h](#ISP_auto-disconnect_after_24h)
        *   [3.2.1 Using cron](#Using_cron)
        *   [3.2.2 Using a systemd timer](#Using_a_systemd_timer)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Default route](#Default_route)
    *   [4.2 Masquerading seems to be working fine but some sites do not work](#Masquerading_seems_to_be_working_fine_but_some_sites_do_not_work)
    *   [4.3 pppd cannot load kernel module ppp_generic](#pppd_cannot_load_kernel_module_ppp_generic)

## Installation

[Install](/index.php/Install "Install") the [ppp](https://www.archlinux.org/packages/?name=ppp) package.

Make sure that your kernel is compiled with PPPoE support (present in default kernel):

 `$ zgrep CONFIG_PPPOE /proc/config.gz`  `CONFIG_PPPOE=m` 

## Configuration

### PPPoE

Create the connection configuration file:

 `/etc/ppp/peers/*your_provider*` 
```
plugin rp-pppoe.so
# rp_pppoe_ac 'your ac name'
# rp_pppoe_service 'your service name'

# network interface
eth0
# login name
name "*someloginname*"
usepeerdns
persist
# Uncomment this if you want to enable dial on demand
#demand
#idle 180
defaultroute
hide-password
noauth
```

If `usepeerdns` option is used, *pppd* will create the `/etc/ppp/resolv.conf` file with obtained DNS addresses while establishing a connection. By default, the `/etc/ppp/ip-up.d/00_dns` hook script moves this file to `/etc/resolv.conf`, allowing the system to use these name servers. If this is undesirable (e.g. you are using a local caching DNS), edit the `/etc/ppp/ip-up.d/00_dns.sh` as you need.

Put a line like this in `/etc/ppp/pap-secrets` or `/etc/ppp/chap-secrets` as required by the authentication method used by your ISP.

Chap should always be preferred, when possible, if aiming at security (to understand how chap works see [this](http://www.tldp.org/LDP/nag/node120.html)), however it is OK to write these two files at the same time, *pppd* will automatically use the appropriate one:

```
*someloginname* * *yourpassword*

```

You can now start the link using the command:

```
# pppd call *your_provider*

```

Alternatively, you can use this

```
# pon *your_provider*

```

where *your_provider* is the exact name of your options file in `/etc/ppp/peers`.

To see whether your PPPoE connection is started correctly, check the *pppd* output in system logs:

```
# journalctl -b --no-pager | grep pppd

```

On a successful connection, you will see something like the following:

```
Jul 09 22:42:33 localhost pppd[239]: Plugin rp-pppoe.so loaded.
Jul 09 22:42:33 localhost pppd[239]: RP-PPPoE plugin version 3.8p compiled against pppd 2.4.6
Jul 09 22:42:33 localhost network[184]: RP-PPPoE plugin version 3.8p compiled against pppd 2.4.6
Jul 09 22:42:33 localhost pppd[239]: pppd 2.4.6 started by root, uid 0
Jul 09 22:42:39 localhost pppd[239]: PPP session is 292
Jul 09 22:42:39 localhost pppd[239]: Connected to a0:f3:e4:4f:e3:b0 via interface enp4s0
Jul 09 22:42:39 localhost pppd[239]: Using interface ppp0
Jul 09 22:42:39 localhost pppd[239]: Connect: ppp0 <--> enp4s0
Jul 09 22:42:39 localhost pppd[239]: CHAP authentication succeeded: CHAP authentication success
Jul 09 22:42:39 localhost pppd[239]: CHAP authentication succeeded
Jul 09 22:42:39 localhost pppd[239]: peer from calling number A0:F3:E4:4F:E3:B0 authorized
Jul 09 22:42:39 localhost pppd[239]: Cannot determine ethernet address for proxy ARP
Jul 09 22:42:39 localhost pppd[239]: local  IP address 10.6.2.137
Jul 09 22:42:39 localhost pppd[239]: remote IP address 10.6.1.1
Jul 09 22:42:39 localhost pppd[239]: primary   DNS address 10.6.1.1
Jul 09 22:42:39 localhost pppd[239]: secondary DNS address 210.21.196.6

```

By default the configuration in `/etc/ppp/peers/provider` is treated as the default, so if you want to make "your_provider" the default, you can create a link like this

```
# ln -s /etc/ppp/peers/*your_provider* /etc/ppp/peers/provider

```

Now you can start the link by simply running:

```
# pon

```

To close a connection, use this

```
# poff *your_provider*

```

### Easy wizard configuration

[pppconfig](https://aur.archlinux.org/packages/pppconfig/) provides a dialog interface to create pppd configuration easily. The usage is as simple as running `pppconfig` as root and it will guide the configuration creation.

```
# pppconfig --dialog

```

The resulting configuration can be called using `pon` and discarded using `poff` as mentioned before.

### Starting pppd on boot

*   Configure the `ppp_generic` module to load on boot. See [Kernel modules#Automatic module loading with systemd](/index.php/Kernel_modules#Automatic_module_loading_with_systemd "Kernel modules") for more information.
*   [Enable](/index.php/Enable "Enable") the systemd service `ppp@*your_provider*.service`.

## Tips and tricks

### Do an auto redial

If *pppd* is running, you can force a connection reset by sending the `SIGHUP` signal to the process:

```
# export PPPD_PID=$(pidof pppd)
# kill -s HUP $PPPD_PID

```

And you have redialed the connection.

**Note:** Make sure you have `persist` option enabled in your `/etc/ppp/peers/provider` tab. Additionally you might want to set `holdoff 0` to reconnect without waiting.

### ISP auto-disconnect after 24h

**Note:** If you are not running your computer always on (running 24/7) then you can skip this step.

If you use a flat-rate always-on connection on a computer, some providers restart your connection after 24h. That makes sure that the IP is rotated every 24h. To compensate, you can use an dynamic DNS service in combination with [inadyn](https://aur.archlinux.org/packages/inadyn/) to compensate for the rotating IP address. But to avoid disconnects when you do not need it, you might try to restart the connection using a cron job or [systemd](/index.php/Systemd#Timers "Systemd") timer at a time of day you know no one will be using the connection (e.g. at 4 AM).

#### Using cron

**Note:** There are many [cron](/index.php/Cron "Cron") implementations, but none of them are installed by default as the base system uses [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers") instead.

As root, do the following:

Create a bash script similar to this and give it a name (e.g. `pppd_redial.sh`):

```
#!/bin/bash

message="Restarting the PPP connection @:" $(date)
pppd_id=$(pidof pppd)

kill -s HUP $pppd_id
echo $message

```

Give it execute permissions and put it on a path visible to root.

Then create a cron job using `crontab -e`. Check that your `EDITOR` env variable is set if the command fails. So add anywhere in the file,

```
0 4 * * * /bin/bash /root/pppd_redial.sh

```

Confirm that `cronie` service is up and running. If this is not the case, just [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") it.

Save and exit. Your PPPoE connection will now restart every day at 4AM.

#### Using a systemd timer

An alternative way to force a reconnect is using a [systemd](/index.php/Systemd "Systemd") timer and the *poff* script (in particular its `-r` option). Simply create a *.service* and *.timer* files with the same name:

 `ppp-redial.timer` 
```
[Unit]
Description=Reconnect PPP connections daily

[Timer]
OnCalendar=*-*-* 05:00:00

[Install]
WantedBy=multi-user.target

```
 `ppp-redial.service` 
```
[Unit]
Description=Reconnect PPP connections

[Service]
Type=simple
ExecStart=/usr/bin/poff -r

```

Now just [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the timer and systemd will cause a restart at the specified time.

## Troubleshooting

### Default route

If you have a preconfigured default route before the *pppd* is started, the default route is kept, so take a look in `/var/log/errors.log` and if you have something like:

```
pppd[nnnn]: not replacing existing default route via *xxx.xxx.xxx.xxx*

```

and `xxx.xxx.xxx.xxx` is not the correct route for you

*   Create a new script in `/etc/ppp/ip-pre-up.d` with this content:

 `/etc/ppp/ip-pre-up.d/10-route-del-default.sh` 
```
#!/bin/sh
/usr/bin/route del default

```

Note: Make sure you have a script named 'ip-pre-up' which launches *.sh in 'ip-pre-up.d' like other launch scripts do.

*   [Restart](/index.php/Restart "Restart") the `pppd` service.

### Masquerading seems to be working fine but some sites do not work

The MTU under pppoe is 1492 bytes. Most sites use an MTU of 1500\. So your connection sends an ICMP 3:4 (fragmentation needed) packet, asking for a smaller MTU, but some sites have their firewall blocking that.

Enabling the PMTU clamping in [iptables](/index.php/Iptables "Iptables") can solve that:

```
iptables -I FORWARD -p tcp --tcp-flags SYN,RST SYN -j TCPMSS --clamp-mss-to-pmtu

```

Now, for some reason, just trying to save the resulting iptables configuration with *iptables-save* and restoring it later, does not work. It has to be executed after the other iptables configuration had been loaded. So, here is a systemd unit to solve it:

 `pmtu-clamping.service` 
```
[Unit]
Description=PMTU clamping for pppoe
Requires=iptables.service
After=iptables.service

[Service]
Type=oneshot
ExecStart=/usr/bin/iptables -I FORWARD -p tcp --tcp-flags SYN,RST SYN -j TCPMSS --clamp-mss-to-pmtu

[Install]
WantedBy=multi-user.target

```

And [enable](/index.php/Enable "Enable") it.

### pppd cannot load kernel module ppp_generic

When starting PPTP client, the *pppd* process cannot locate the appropriate module:

```
Couldn't open the /dev/ppp device: No such device or address
Please load the ppp_generic kernel module.

```

The solution is to edit the `/etc/modprobe.d/modules.conf` file and change

```
alias char-major-108 ppp

```

to

```
alias char-major-108 ppp_generic

```

or just add such alias if it does not exist.

The correct module will be loaded after reboot.