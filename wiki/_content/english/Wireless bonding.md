Here is a way to provide Automatic Wireless Network Configuration while also "[bonding](https://en.wikipedia.org/wiki/Bonding_protocol)" a wireless interface to a wired interface, using only the kernel "[bonding](https://www.kernel.org/doc/Documentation/networking/bonding.txt)" module in "active-backup" mode, the sysfs and [iproute2](https://www.archlinux.org/packages/core/x86_64/iproute2/) commands, and [systemd](https://www.archlinux.org/packages/?name=systemd) "template" Unit files **without** systemd-networkd. This will run wpa_supplicant on the wireless interface and DHCP and DHCPv6 daemons on a virtual "bond0" interface. This is useful, for instance, with a portable computer when you want to use the wired interface for speed and/or security when available, and the wireless interface when the wired interface is not available. The basic idea is to have two "always active" wired and wireless interfaces, then "bond" or "enslave" them to a virtual interface "master", and then let the kernel bonding module handle switching between the interfaces. Of course, this scheme can be extended to two wireless interfaces or to more than two physical network interfaces. Note that no other "connection manager" is used here, for those who prefer a more basic approach. But then also, note that wpa_supplicant itself can be managed directly using `wpa_gui` from [wpa_supplicant_gui](https://www.archlinux.org/packages/?name=wpa_supplicant_gui) or [wpa_supplicant_gui-qt5](https://aur.archlinux.org/packages/wpa_supplicant_gui-qt5/), to scan for, select, and connect to new access points/base stations.

In this example, there are three [systemd](/index.php/Systemd "Systemd") unit files needed, along with three corresponding configuration files for [wpa_supplicant](https://wiki.archlinux.org/index.php/WPA_supplicant), [dhclient](https://www.archlinux.org/packages/?name=dhclient), and [dhcp6c](https://aur.archlinux.org/packages/wide-dhcpv6/). Additionally, there will be a module configuration file for the kernel "bonding" module and a systemd Timer Unit File.

Note also that systemd "template" Unit File names allow exactly one variable to be specified, the "Instance name". Here, the Instance name will specify the wireless device. And, since there are at least three network interfaces to address - wireless, wired, and virtual - then the wired and virtual interfaces must be specified either as "hard coded" names, or using systemd's "Environment" or EnvironmentFile" directives. In this example, the virtual interface will be hard coded as "bond0", and the Environment directive will be edited manually to specify the wired interface name.

**Note:** **All** of the required systemd service files and configuration files from a working example are shown here because they are **not** the same as the standard files provided with the Arch Linux packages. Edit as required.

## Contents

*   [1 DHCP configuration](#DHCP_configuration)
*   [2 wpa_supplicant](#wpa_supplicant)
*   [3 Bonding configuration](#Bonding_configuration)
*   [4 Testing the result](#Testing_the_result)

## DHCP configuration

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

Make sure that the DHCP Client Identifier and the DHCPv6 Client Identifier are the same DUID. See `xxd -g1 -s2 /var/lib/dhcpv6/dhcp6c_duid`. The DHCP Server, [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) for instance, can be configured to give fixed IP addresses based upon multiple MAC addresses, or provided hostname, or provided Client Identifier.

 `/etc/systemd/system/dhclient@.service` 

```
[Unit]
Description=ISC dhclient on interface %I
Documentation=man:dhclient(8) man:dhclient.conf(5)
Wants=network.target
After=network.target
BindsTo=sys-subsystem-net-devices-%i.device
After=sys-subsystem-net-devices-%i.device

[Service]
ExecStart=/usr/bin/dhclient -d -pf /run/dhclient-%i -i %I
ExecStop=/usr/bin/dhclient -r -pf /run/dhclient-%i
Restart=on-abnormal

[Install]
WantedBy=sys-subsystem-net-devices-%i.device
```

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

# keyinfo kame-key {                    # Required to use the dhcp6ctl tool.
#     realm "kame.net";
#     keyid 1;
#     secret "ErEJ0GEz7HS3uBU03/hKZA=="; # Generate with "openssl rand -base64 16 > /etc/wide-dhcpv6/dhcp6cctlkey"
# };
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
After=sys-subsystem-net-devices-%i.device

[Service]
ExecStart=/usr/bin/dhcp6c -f -p /run/dhcp6c-%i -P default -c /etc/wide-dhcpv6/dhcp6c.conf %I
ExecReload=/usr/bin/kill -s SIGHUP $MAINPID
Restart=on-abnormal

[Install]
WantedBy=sys-subsystem-net-devices-%i.device
```

## wpa_supplicant

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

Be careful with the actual protocol configuration in the [wpa_supplicant](/index.php/Wpa_supplicant "Wpa supplicant") configuration file. Using protocols incompatible with the base station can result in unstable and otherwise difficult to troubleshoot wireless connections.

## Bonding configuration

 `/etc/modprobe.d/bonding.conf` 

```
# The primary slave will be configured in the systemd unit file.
# Currently, the kernel bonding module supports link detection methods only one at a time, and
# there is no IPv6 Neighbor Solicitation/Advertisement link detection method available.

options bonding max_bonds=0 miimon=100 mode=active-backup fail_over_mac=active
```

There is one more issue to address. When _starting_ bond0-supplicant@.service, where the only working interface is the _non_-primary slave - for instance, starting with only a wireless interface available when the wired interface is the primary - then dhclient will quickly start and adopt the MAC address of the initial primary slave, and use that MAC address when attempting to communicate with the DHCP server. When the wireless interface, some short time later, authenticates and associates with the access point/base station, establishing a connection to the network, the bonding driver will make the wireless interface the new active interface, and change the active MAC address on the bond0 interface, to match the wireless MAC address. Because dhclient will continue to use the MAC address from the wired interface, and that MAC address is no longer accepted by the bond0 interface, all DHCP communication will fail. If there is no saved lease file in /var/lib/dhclient/dhclient.leases, then no IPv4 address will be configured, and no IPv4 traffic will be possible. It can also be seen that when dhclient starts quickly, it can read the primary slave's firmware MAC address, rather than any MAC address assigned to the device interface. If the firmware MAC address is "null", then dhclient assigns a random MAC address. BOOTP/DHCP packets using these firmware or random MAC addresses may "succeed" in gaining a reply on the primary slave device and fail on the non-primary slave device. That can be confusing and annoying.

These are only issues with dhclient and IPv4\. Fortunately, on a dhclient DHCP request, after the lease expires, dhclient "does the right thing". dhclient will function properly no matter on which slave interface it was started.

This problem **cannot** be solved by configuring the bonding driver with the default `fail_over_mac=none`. Almost all network interface devices will not pass traffic with a MAC address which is not their own. An example of this kind of warning can be seen [here](http://www.ibm.com/developerworks/linux/linux390/development_restrictions.html#net). Strange network behavior will be the result, where broadcast packets will pass, but ping/icmp packets will only pass in some circumstances and not others.

Ideally, dhclient would re-determine the bond0 MAC address each time it initially retried contacting the DHCP server. Without that, a different approach is to simply delay the start of dhclient until after the kernel bonding driver has configured an active slave. If the active slave is to be the wireless interface, then wpa_supplicant will first have authenticated and associated with the access point/base station, and dhclient will adopt the correct MAC address. If the active slave is the primary slave, again dhclient will adopt the correct MAC address. This delay is imposed with a systemd Timer Unit File.

 `/etc/systemd/system/dhclient@.timer` 

```
[Unit]
Description=service-start-delay

[Timer]
OnActiveSec=5s
AccuracySec=100ms
RemainAfterElapse=no

[Install]
WantedBy=sys-subsystem-net-devices-%i.device
```

With those preliminaries, here is the systemd Unit File which configures the virtual interface, bond0, and applies wpa_supplicant to the wireless interface, specified as a systemd template instance. Remember to set the "ETH" variable to the correct wired interface name.

 `/etc/systemd/system/bond0-supplicant@.service` 

```
[Unit]
Description=bond0-%I-wpa_supplicant-nl80211
Documentation=[https://www.kernel.org/doc/Documentation/networking/bonding.txt](https://www.kernel.org/doc/Documentation/networking/bonding.txt)
Documentation=man:wpa_supplicant(8) man:wpa_cli(8) man:wpa_supplicant.conf(5) man:wpa_passphrase(8)

Wants=network.target
Before=network.target

BindsTo=sys-subsystem-net-devices-%i.device
After=sys-subsystem-net-devices-%i.device

Before=dhclient@bond0.timer
Before=dhcp6c@bond0.service

[Service]
# NOTE - Set this ETH variable to the desired wired ethernet interface name.
Environment= ETH=enp0s10
Type=simple

# Invoking the bond device will automatically load the bonding module if not already loaded.
# NOTE - Be sure to leave a space before the semicolon.
ExecStartPre=\
-/usr/bin/ip link add bond0 type bond ;\
 /usr/bin/sh -c 'echo -n $ETH > /sys/devices/virtual/net/bond0/bonding/primary' ;\
 /usr/bin/ip link set bond0 up ;\
 /usr/bin/ip link set $ETH down ;\
 /usr/bin/ip address flush dev $ETH ;\
 /usr/bin/ip link set $ETH master bond0 ;\
 /usr/bin/ip link set $ETH up ;\
 /usr/bin/ip link set %I down ;\
 /usr/bin/ip address flush dev %I ;\
-/usr/bin/ip link set %I master bond0 ;\
-/usr/bin/ip link set %I up ;\

# Disable legacy 802.11b bitrates.
ExecStartPre=-/usr/bin/iw %I set bitrates legacy-2.4  6 9 12 18 24 36 48 54

# NOTE- ./wpa_supplicant/wpa_supplicant_i.h
#        /**
#         * bridge_ifname - Optional bridge interface name
#         *
#         * If the driver interface (ifname) is included in a Linux bridge
#         * device, the bridge interface may need to be used for receiving EAPOL
#         * frames. This can be enabled by setting this variable to enable
#         * receiving of EAPOL frames from an additional interface.
#         */
#        const char *bridge_ifname;
#
# NOTE - man 8 wpa_supplicant - if you are bonding more than one wireless interface:
#   -i ifname - Interface to listen on. Multiple instances of this option can be present,
#   one per interface, separated by -N option.
# Environment variables will be needed to specify each additional interface.
ExecStart=/usr/bin/wpa_supplicant -c/etc/wpa_supplicant/wpa_supplicant.conf -Dnl80211 -i %I -b bond0

# Reset bitrates.
ExecStop=-/usr/bin/iw %I set bitrates

# Stop the DHCP clients before tearing-down the link.
ExecStop=\
 /usr/bin/systemctl stop dhcp6c@bond0.service ;\
 /usr/bin/systemctl stop dhclient@bond0.service ;\
 /usr/bin/wpa_cli -i %I terminate ;\

ExecStopPost=\
 /usr/bin/ip link set %I nomaster ;\
 /usr/bin/ip link set $ETH nomaster ;\
 /usr/bin/ip link set bond0 down ;\
 /usr/bin/ip address flush bond0 ;\
 /usr/bin/ip link delete bond0 type bond ;\

ExecReload=/usr/bin/wpa_cli -i %I reconfigure
Restart=on-abnormal

[Install]
WantedBy=default.target
# Possible alternative when using a removable wireless device, this reverse dependency
# would start this Unit File immediately whenever the wireless device is inserted.
# Use a "Conflicts=" directive in the [Unit] section above to automatically Stop any other
# Unit File being used to configure IP addresses on, say, the un-bonded wired interface.
# And then use an "OnFailure=" directive in the [Unit] section above to automatically Start
# that same Unit File - or Files - when the wireless device is removed.
# WantedBy=sys-subsystem-net-devices-%i.device
```

## Testing the result

Whenever a unit file is edited, run:

```
# systemctl daemon-reload

```

The "activation" of the DHCP servers is to be conditioned upon the "appearance" of the bond0 Device Unit File, sys-subsystem-net-devices-bond0.device, where the bond0-supplicant@.service Unit File operates otherwise independently. This condition, though, is itself manually "enabled" and "disabled" through systemd and its control tool, systemctl. Enable one or both of the DHCP servers for the bond0 device.

```
# systemctl enable dhclient@bond0.timer dhcp6c@bond0.service

```

Then, [Enable](/index.php/Enable "Enable") and start `bond0-supplicant@_wlp3s0_.service`, replacing _wlp3s0_ with the desired wireless interface.

```
# systemctl enable bond0-supplicant@_wlp3s0_.service
# systemctl start bond0-supplicant@_wlp3s0_.service

```

Check the results:

```
# journalctl -afn100
$ ip a
$ ps wax

```

 `$ systemctl list-units '*bond0*'` 

```
UNIT                                   LOAD   ACTIVE   SUB     DESCRIPTION
sys-devices-virtual-net-bond0.device   loaded active   plugged /sys/devices/virtual/net/bond0
sys-subsystem-net-devices-bond0.device loaded active   plugged /sys/subsystem/net/devices/bond0
bond0-supplicant@wlp3s0.service        loaded active   running bond0-wlp3s0-wpa_supplicant-nl80211
dhclient@bond0.service                 loaded active   running ISC dhclient on interface bond0
dhcp6c@bond0.service                   loaded active   running WIDE-DHCPv6 dhcp6c on interface bond0
system-bond0\x2dsupplicant.slice       loaded active   active  system-bond0\x2dsupplicant.slice
dhclient@bond0.timer                   loaded active   running dhclient-start-delay

LOAD   = Reflects whether the unit definition was properly loaded.
ACTIVE = The high-level unit activation state, i.e. generalization of SUB.
SUB    = The low-level unit activation state, values depend on unit type.

7 loaded units listed.
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

This approach to bonded wireless networking leaves wpa_supplicant running continuously for any built-in wireless device. Running [htop](https://www.archlinux.org/packages/?name=htop), wpa_supplicant, and the DHCP and DHCPv6 Client daemons, seem to behave well, and do not use any noticeable CPU time.

Still, a hardware switch or [rfkill](/index.php/Rfkill "Rfkill") can be used to actually disable the radio when desired.

Notice that the DHCP servers are managed by systemd and will "Stop", "Start", and "Restart" if they are properly stopped, started, or restarted using systemctl. The DHCP servers are quite independent of the bonding driver and wpa_supplicant except for any dependency that has been explicitly enabled. So, for instance, a dhclient configured IPv4 address may be removed without disturbing any other network configuration or functionality with

```
# systemctl stop dhclient@bond0.service

```

Similarly, an address may be released and a new address acquired with

```
# systemctl restart dhclient@bond0.service

```

Check that the Ethernet cable is actually plugged-in when wired networking is preferred.