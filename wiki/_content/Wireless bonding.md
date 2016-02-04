# Wireless bonding

Here is a way to configure a wireless interface "[bonded](https://en.wikipedia.org/wiki/Bonding_protocol)" to a wired interface using only the kernel "[bonding](https://www.kernel.org/doc/Documentation/networking/bonding.txt)" module in "active-backup" mode, the sysfs and [iproute2](https://www.archlinux.org/packages/core/x86_64/iproute2/) commands, and systemd "template" Unit files **without** systemd-networkd. This will run wpa_supplicant on the wireless interface and DHCP and DHCPv6 daemons on a virtual "bond0" interface. This is useful, for instance, with a portable computer when you want to use the wired interface for speed and/or security when available, and the wireless interface when the wired interface is not available. The basic idea is to have two "always active" wired and wireless interfaces, then "bond" or "enslave" them to a virtual interface "master", and then let the kernel bonding module handle switching between the interfaces. Of course, this scheme can be extended to more than two physical network interfaces. Note that no other "connection manager" is used here, for those who prefer a more basic approach.

"systemd Unit Files" can be viewed as a kind of Declarative Program in the "systemd" [Declarative Programming](https://en.wikipedia.org/wiki/Declarative_programming) language, which describes various dependencies between programs and enables the systemd "Declarative [Interpreter](https://en.wikipedia.org/wiki/Interpreter_%28computing%29)" to execute and manage these dependencies. In this example, there are three Unit Files needed, along with the three corresponding configuration files for [wpa_supplicant](https://wiki.archlinux.org/index.php/WPA_supplicant), [dhclient](https://www.archlinux.org/packages/?name=dhclient), and [dhcp6c](https://aur.archlinux.org/packages/wide-dhcpv6/). Additionally, there will be a module configuration file for the kernel "bonding" module.

Something you might find unusual in these Unit Files is the use of "BindsTo" and "WantedBy" to "bind" a "Service Unit File" and its associated program to a systemd "Device Unit File", which is a kind of systemd "special file" corresponding to a linux "[sysfs](https://en.wikipedia.org/wiki/Sysfs)" special file. systemd uses directives in the "Unit" section to describe "forward" dependencies, which "trigger" other Unit Files, and uses directives in the "Install" section to describe "reverse" dependencies, which - "enabled" manually or automatically - cause other Unit Files to "trigger" the defining Unit File. Here, the defining Service Unit File will Start and Stop the associated program whenever the sysfs device "Appears" or "Disappears", as, for instance, with a hot-pluggable wireless or wired device, or with the virtual interface device, "bond0".

Note also that systemd "template" Unit File names allow exactly one variable to be specified, the "Instance name". Here, the Instance name will specify the wireless device. And, since there are at least three network interfaces to address - wireless, wired, and virtual - then the wired and virtual interfaces must be specified either as "hard coded" names, or using systemd's "Environment" or EnvironmentFile" directives. In this example, the virtual interface will be hard coded as "bond0", and the Environment directive will be edited manually to specify the wired interface name.

**Note:** **All** of the required systemd service files and configuration files from a working example are shown here because they are **not** the same as the standard files provided with the Arch packages. Copy, paste, and edit.

 `/etc/dhclient.conf` 

```
# These time-outs are aggressively short, supposing a sparsely populated network.
initial-interval 2;
timeout 5;
retry 10;

send host-name "laptop";
# [RFC 4361](//tools.ietf.org/html/rfc4361)          Node-specific Identifiers for DHCPv4     February 2006
send dhcp-client-identifier 00:02:00:02:2e:2d:01:bd:c3:92:9a:44:2a:c4 ;
```

For instance, dnsmasq can be configured to give fixed IP addresses based upon multiple MAC addresses, or provided hostname, or provided Client Identifier.

 `/etc/systemd/system/dhclient@.service` 

```
[Unit]
Description=ISC dhclient on interface %I
Documentation=man:dhclient(8) man:dhclient.conf(5)
Wants=network.target
After=network.target
BindsTo=sys-subsystem-net-devices-%i.device
StopWhenUnneeded=true

[Service]
ExecStart=/usr/bin/dhclient -d -i %I
Restart=on-abnormal

[Install]
WantedBy=sys-subsystem-net-devices-%i.device
```

Make sure that the DHCP Client Identifier and the DHCPv6 Client Identifier are the same DUID.

 `/etc/wide-dhcpv6/dhcp6c.conf` 

```
profile default {                       # generic interface using a profile named "default"
        send ia-na 1;                   # a corresponding identity association statement must exist with the same ID.
#       send ia-pd 2;
        send rapid-commit;
#       send authentication auth-protocol;
        request domain-name-servers, domain-name, ntp-servers;
#       script "/etc/wide-dhcpv6/dhcp6c-script";
};

id-assoc na 1 {                         # Identity Association for Non-temporary Addresses request
#       address <ipv6-address> <pltime> [<vltime>];   # Request a specific address.
                                        # pltime and vltime are preferred and valid lifetimes of the prefix.
                                        # When pltime reaches zero the address becomes deprecated and should not be used for new connections.
                                        # When the vltime reaches zero the address becomes invalid.
                                        # A decimal number provides the lifetime in seconds, while infinity means the lifetime never expires.
};
```

A simple example configuration file, with no Prefix Delegation being requested. Here, the "Profile" statement is used instead of the "Interface" statement, since the same configuration is to be applied to whatever interface is provided on the dhcp6c command line.

 `/etc/systemd/system/dhcp6c@.service` 

```
[Unit]
Description=WIDE-DHCPv6 dhcp6c on interface %I
Documentation=man:dhcp6c(8) man:dhcp6c.conf(5)
Wants=network.target
After=network.target
BindsTo=sys-subsystem-net-devices-%i.device
StopWhenUnneeded=true

[Service]
ExecStart=/usr/bin/dhcp6c -f -P default -c /etc/wide-dhcpv6/dhcp6c.conf %I
Restart=on-abnormal

[Install]
WantedBy=sys-subsystem-net-devices-%i.device
```

 `/etc/modprobe.d/bonding.conf` 

```
# The primary slave will be configured in the systemd unit file.
# Currently, the kernel bonding module supports link detection methods only one at a time, and
# there is no IPv6 Neighbor Solicitation/Advertisement link detection method available.

options bonding max_bonds=0 miimon=100 mode=active-backup fail_over_mac=active
```

 `/etc/wpa_supplicant/wpa_supplicant.conf` 

```
update_config=1
ctrl_interface=/var/run/wpa_supplicant
ctrl_interface_group=wheel
eapol_version=2
ap_scan=1
# fast_reauth=1
country=US

network={
        ssid="MyHome"
        priority=2
        proto=RSN
        group=CCMP
        pairwise=CCMP
        key_mgmt=WPA-PSK
        #psk="SuperSecret"
        psk=404fe69d94ef522ba8e7a0c456a67a583c8f39ba0b29a3ac22ebe9494cf9992b
}
```

Be careful with the actual protocol configuration in the wpa_supplicant configuration file. Using protocols incompatible with the base station can result in unstable and otherwise difficult to troubleshoot wireless connections.

With those preliminaries, here is the systemd Unit File which configures the virtual interface, bond0, and applies wpa_supplicant to the wireless interface, specified as a systemd template instance.

 `/etc/systemd/system/bond0-supplicant@.service` 

```
[Unit]
# bond0-supplicant@.service
Description=bond0 interface bonding wpa_supplicant-nl80211
Documentation=[https://www.kernel.org/doc/Documentation/networking/bonding.txt](https://www.kernel.org/doc/Documentation/networking/bonding.txt)
Documentation=man:wpa_supplicant(8) man:wpa_cli(8) man:wpa_supplicant.conf(5) man:wpa_passphrase(8)
After=sys-subsystem-net-devices-%i.device
BindsTo=sys-subsystem-net-devices-%i.device
BindsTo=sys-subsystem-net-devices-bond0.device
Before=network.target
Wants=network.target
Before=dhclient@bond0.service
Wants=dhclient@bond0.service
Before=dhcp6c@bond0.service
Wants=dhcp6c@bond0.service

[Service]
# NOTE - Set this ETH variable to the desired wired ethernet interface name.
Environment= ETH=enp0s10
Type=simple

# Invoking the bond device will automatically load the bonding module if not already loaded.
# The bonding module may be configured through a modprobe options file.
# options bonding max_bonds=0 miimon=100 mode=active-backup fail_over_mac=active
# NOTE - Using "/usr/bin/echo" does not seem to work for setting the Primary Slave.
# NOTE - Be sure to leave a space before the semicolon.
ExecStartPre=\
-/usr/bin/ip link add bond0 type bond ;\
 /usr/bin/sh -c 'echo -n $ETH > /sys/devices/virtual/net/bond0/bonding/primary' ;\
 /usr/bin/ip link set $ETH down ;\
 /usr/bin/ip address flush dev $ETH ;\
 /usr/bin/ip link set $ETH master bond0 ;\
 /usr/bin/ip link set $ETH up ;\
 /usr/bin/ip link set %I down ;\
 /usr/bin/ip address flush dev %I ;\
-/usr/bin/ip link set %I master bond0 ;\

ExecStart=/usr/bin/wpa_supplicant -c/etc/wpa_supplicant/wpa_supplicant.conf -Dnl80211 -i %I -b bond0
ExecStop=/usr/bin/wpa_cli -i %I terminate

# NOTE - do NOT "BindTo" a device that will also be deleted in this Unit File!
# This would make a "systemctl restart" act instead as a "systemctl stop".
# To remove bond0 manually: sudo ip link delete bond0 type bond
ExecStopPost=\
 /usr/bin/ip link set %I nomaster ;\
 /usr/bin/ip link set $ETH nomaster ;\
 /usr/bin/ip link set bond0 down ;\
 /usr/bin/ip address flush bond0 ;\

ExecReload=/usr/bin/wpa_cli -i %I reconfigure

[Install]
WantedBy=default.target
# Possible alternative when using a removable wireless device.
# This would start this Unit File immediately whenever the wireless device is inserted.
# Use a "Conflicts=" directive in the [Unit] section above to automatically Stop any other
# Unit File being used to configure IP addresses on, say, the un-bonded wired interface.
# And then use an "OnFailure=" directive in the [Unit] section above to automatically Start
# that same Unit File - or Files - when the wireless device is removed.

# WantedBy=sys-subsystem-net-devices-%i.device
```

 `$ sudo systemctl daemon-reload` 

NOTE - Set the desired wireless interface instance name here.

 `$ sudo systemctl enable bond0-supplicant@wlp3s0.service` 

```
Created symlink from /etc/systemd/system/default.target.wants/bond0-supplicant@wlp3s0.service to /etc/systemd/system/bond0-supplicant@.service.

```

And then, finally, start the service, and check the results.

 `$ sudo systemctl start bond0-supplicant@wlp3s0.service`  `$ sudo journalctl -afn100`  `$ ip a`  `$ systemctl list-units '*bond0*'` 

```
UNIT                                   LOAD   ACTIVE   SUB     DESCRIPTION
sys-devices-virtual-net-bond0.device   loaded active   plugged /sys/devices/virtual/net/bond0
sys-subsystem-net-devices-bond0.device loaded active   plugged /sys/subsystem/net/devices/bond0
bond0-supplicant@wlp3s0.service        loaded active   running bond0 interface bonding wpa_supplicant-nl80211
dhclient@bond0.service                 loaded active   running ISC dhclient on interface bond0
dhcp6c@bond0.service                   loaded active   running WIDE-DHCPv6 dhcp6c on interface bond0
system-bond0\x2dsupplicant.slice       loaded active   active  system-bond0\x2dsupplicant.slice

LOAD   = Reflects whether the unit definition was properly loaded.
ACTIVE = The high-level unit activation state, i.e. generalization of SUB.
SUB    = The low-level unit activation state, values depend on unit type.

6 loaded units listed.
To show all installed unit files use 'systemctl list-unit-files'.
```

Using the wired ethernet interface,

 `$ cat /proc/net/bonding/bond0` 

```
Ethernet Channel Bonding Driver: v3.7.1 (April 27, 2011)

Bonding Mode: fault-tolerance (active-backup) (fail_over_mac active)
Primary Slave: enp0s10 (primary_reselect always)
Currently Active Slave: enp0s10
MII Status: up
MII Polling Interval (ms): 100
Up Delay (ms): 0
Down Delay (ms): 0

Slave Interface: enp0s10
MII Status: up
Speed: 100 Mbps
Duplex: full
Link Failure Count: 0
Permanent HW addr: c2:91:8b:44:3b:d5
Slave queue ID: 0

Slave Interface: wlp3s0
MII Status: up
Speed: Unknown
Duplex: Unknown
Link Failure Count: 34
Permanent HW addr: 00:1e:4c:33:a2:44
Slave queue ID: 0

```

Using the wireless interface,

 `$ cat /proc/net/bonding/bond0` 

```
Ethernet Channel Bonding Driver: v3.7.1 (April 27, 2011)

Bonding Mode: fault-tolerance (active-backup) (fail_over_mac active)
Primary Slave: enp0s10 (primary_reselect always)
Currently Active Slave: wlp3s0
MII Status: up
MII Polling Interval (ms): 100
Up Delay (ms): 0
Down Delay (ms): 0

Slave Interface: enp0s10
MII Status: down
Speed: Unknown
Duplex: Unknown
Link Failure Count: 1
Permanent HW addr: c2:91:8b:44:3b:d5
Slave queue ID: 0

Slave Interface: wlp3s0
MII Status: up
Speed: Unknown
Duplex: Unknown
Link Failure Count: 36
Permanent HW addr: 00:1e:4c:33:a2:44
Slave queue ID: 0

```

This approach to bonded wireless networking leaves wpa_supplicant running continuously for any built-in wireless device. Still, rfkill can be used to actually disable the radio when desired, either using an external switch to turn-off the radio, or using rfkill on the command line. But then also note, some wireless drivers will fail to respond when this external radio switch or rfkill sets the radio back, from "off" to "on". For instance, the ath5k driver has this bug. You might see something like `... wpa_supplicant[5808]: Could not set interface wlp3s0 flags (UP): Operation not possible due to RF-kill`

A possible work-around, to recover, is to

```
$ sudo modprobe -r ath5k
$ sudo rfkill unblock all
$ sudo modprobe ath5k

```

Note that that will Stop the bond0-wpa_supplicant@.service Unit when the wireless device disappears, but this will not necessarily disable the bond0 interface running on the wired device, especially if the DHCP Client daemon did not remove a configured IP address, as the DHCP client will also be Stopped.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Wireless_bonding&oldid=419006](https://wiki.archlinux.org/index.php?title=Wireless_bonding&oldid=419006)"