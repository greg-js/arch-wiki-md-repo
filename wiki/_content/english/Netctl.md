Related articles

*   [Bridge with netctl](/index.php/Bridge_with_netctl "Bridge with netctl")
*   [Network configuration](/index.php/Network_configuration "Network configuration")
*   [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration")

[netctl](https://projects.archlinux.org/netctl.git/) is a CLI and profile-based network manager and an Arch project.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
    *   [3.1 Starting a profile](#Starting_a_profile)
    *   [3.2 Enabling a profile](#Enabling_a_profile)
    *   [3.3 Special systemd units](#Special_systemd_units)
        *   [3.3.1 Wired](#Wired)
        *   [3.3.2 Wireless](#Wireless)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Example profiles](#Example_profiles)
        *   [4.1.1 Wired](#Wired_2)
        *   [4.1.2 Wireless (WPA-PSK)](#Wireless_(WPA-PSK))
    *   [4.2 Obfuscate wireless passphrase](#Obfuscate_wireless_passphrase)
    *   [4.3 Using an experimental GUI](#Using_an_experimental_GUI)
    *   [4.4 Bonding](#Bonding)
        *   [4.4.1 Load balancing](#Load_balancing)
        *   [4.4.2 Wired to wireless failover](#Wired_to_wireless_failover)
    *   [4.5 Using any interface](#Using_any_interface)
    *   [4.6 Using hooks](#Using_hooks)
        *   [4.6.1 Examples](#Examples)
            *   [4.6.1.1 Execute commands on established connection](#Execute_commands_on_established_connection)
            *   [4.6.1.2 Set default DHCP client](#Set_default_DHCP_client)
    *   [4.7 Minimal WPAConfigSection](#Minimal_WPAConfigSection)
    *   [4.8 resolv.conf](#resolv.conf)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Job for netctl@wlan(...).service failed](#Job_for_netctl@wlan(...).service_failed)
    *   [5.2 dhcpcd: ipv4_addroute: File exists](#dhcpcd:_ipv4_addroute:_File_exists)
    *   [5.3 DHCP timeout issues](#DHCP_timeout_issues)
    *   [5.4 dhcpcd debugging](#dhcpcd_debugging)
    *   [5.5 Connection timeout issues](#Connection_timeout_issues)
    *   [5.6 Problems with netctl-auto on resume](#Problems_with_netctl-auto_on_resume)
    *   [5.7 netctl-auto does not automatically unblock a wireless card to use an interface](#netctl-auto_does_not_automatically_unblock_a_wireless_card_to_use_an_interface)
    *   [5.8 RTNETLINK answers: File exists (with multiple NICs)](#RTNETLINK_answers:_File_exists_(with_multiple_NICs))
    *   [5.9 Problems with eduroam and other MSCHAPv2 connections](#Problems_with_eduroam_and_other_MSCHAPv2_connections)
    *   [5.10 Journal warnings for profiles using .include directives](#Journal_warnings_for_profiles_using_.include_directives)
    *   [5.11 Hooks don't work](#Hooks_don't_work)
*   [6 See also](#See_also)

## Installation

[netctl](https://www.archlinux.org/packages/?name=netctl) is part of the [base](https://www.archlinux.org/groups/x86_64/base/) group, so it should already be installed on your system. Otherwise [install](/index.php/Install "Install") it as usual.

*netctl's* [#Special systemd units](#Special_systemd_units) used in automating connections require some additional dependencies; see that section for more information.

Other optional dependencies are shown in the table below.

| Feature | Dependency |
| WPA | [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) |
| DHCP | [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) or [dhclient](https://www.archlinux.org/packages/?name=dhclient) |
| *wifi-menu* | [dialog](https://www.archlinux.org/packages/?name=dialog) |
| PPPoE | [ppp](https://www.archlinux.org/packages/?name=ppp) |

**Warning:** Do not enable concurrent, conflicting network services. Use `systemctl --type=service` to ensure that no other network service is running before enabling a *netctl* profile/service.

## Configuration

*netctl* uses profiles to manage network connections and different modes of operation to start profiles automatically or manually on demand.

The *netctl* profile files are stored in `/etc/netctl/` and example configuration files are available in `/etc/netctl/examples/`.

To use an example profile, simply copy it from `/etc/netctl/examples/` to `/etc/netctl/` and configure it to your needs; see basic [#Example profiles](#Example_profiles) below. The first parameter you need to create a profile is the network `Interface`, see [Network configuration#Network interfaces](/index.php/Network_configuration#Network_interfaces "Network configuration") for details.

**Tip:**

*   For wireless settings, you can use `wifi-menu -o` as root to generate the profile file in `/etc/netctl/`. The [dialog](https://www.archlinux.org/packages/?name=dialog) package is required to use *wifi-menu*.
*   Use `SkipNoCarrier=yes` in your profile to enable a static IP profile on a wired interface no matter if the cable is connected or not.

See [netctl.profile(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/netctl.profile.5) for a complete list of profile options.

## Usage

See [netctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/netctl.1) for a complete list of *netctl* commands.

### Starting a profile

Once you have created your profile, attempt to establish a connection, where *profile* is only the profile name, not the full path:

```
# netctl start *profile*

```

If the above command results in a failure, then use `journalctl -xn` and `netctl status *profile*` to obtain a more in-depth explanation of the failure.

### Enabling a profile

A profile can be enabled to start at boot by using:

```
# netctl enable *profile*

```

This will create and enable a [systemd](/index.php/Systemd "Systemd") service that will start when the computer boots. Changes to the profile file will not propagate to the service file automatically. After such changes, it is necessary to reenable the profile:

```
# netctl reenable *profile*

```

After enabling a profile, it will be started at next boot. Obviously this can only be successful, if the network cable for a wired connection is plugged in, or the wireless access point used in a profile is in range respectively.

If you need to switch multiple profiles frequently (i.e., traveling with a laptop), use [#Special systemd units](#Special_systemd_units) instead of enabling a profile.

### Special systemd units

*netctl* provides special [systemd](/index.php/Systemd "Systemd") services for automatically switching of profiles for wired and wireless connections. See [netctl.special(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/netctl.special.7) for a complete list of special systemd units.

#### Wired

[Install](/index.php/Install "Install") the [ifplugd](https://www.archlinux.org/packages/?name=ifplugd) package and [start/enable](/index.php/Start/enable "Start/enable") the `netctl-ifplugd@*interface*.service` systemd unit. DHCP profiles will be started/stopped when the network cable is plugged in/unplugged.

*   The `netctl-ifplugd@*interface*.service` will prefer profiles that use [DHCP](https://en.wikipedia.org/wiki/DHCP "wikipedia:DHCP").
*   To automatically start a static IP profile the option `ExcludeAuto=no` needs to be set in it.
*   To prioritize a profile with a static IP over DHCP profiles, you can set `Priority=2`, which is higher than the default priority given to DHCP profiles of `Priority=1`.

#### Wireless

[Start/enable](/index.php/Start/enable "Start/enable") `netctl-auto@*interface*.service` systemd unit. *netctl* profiles will be started/stopped automatically as you move from the range of one network into the range of another network (roaming).

*   Profiles must use `Security=wpa-configsection` or `Security=wpa` to work with *netctl-auto* rather than `Security=wpa-config`.
*   If you want some wireless profile **not** to be started automatically by `netctl-auto@*interface*.service`, you have to explicitly add `ExcludeAuto=yes` to that profile.
*   You can use `priority=` in the *WPAConfigSection* (see `/etc/netctl/examples/wireless-wpa-configsection`) to set priority of a profile when multiple wireless access points are available.

Note that *interface* is not literal, but to be substituted by the name of your device's interface, e.g. `netctl-auto@wlp4s0.service`. See `netctl.profile(5)` for details.

**Note:**

*   If any of the profiles contain errors, such as an empty or misquoted `Key=` variable, the unit will fail to load with the message `"Failed to read or parse configuration '/run/network/wpa_supplicant_wlan0.conf'`, even when that profile is not being used.
*   If you have previously [enabled a profile](#Enabling_a_profile) through *netctl*, run `netctl disable *profile*` to prevent the profile from starting twice at boot.

It is possible to manually control an interface otherwise managed by *netctl-auto* without having to stop `netctl-auto.service`. This is done using the *netctl-auto* command. For a complete list of available actions see [netctl-auto(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/netctl-auto.1).

## Tips and tricks

### Example profiles

#### Wired

For a DHCP connection, only the `Interface` has to be configured after copying the `/etc/netctl/examples/ethernet-dhcp` example profile to `/etc/netctl`.

For example:

 `/etc/netctl/*my_dhcp_profile*` 
```
Interface=enp1s0
Connection=ethernet
IP=dhcp

```

For a static IP configuration copy the `/etc/netctl/examples/ethernet-static` example profile to `/etc/netctl` and modify `Interface`, `Address`, `Gateway` and `DNS`) as needed.

For example:

 `/etc/netctl/*my_static_profile*` 
```
Interface=enp1s0
Connection=ethernet
IP=static
Address=('10.1.10.2/24')
Gateway='10.1.10.1'
DNS=('10.1.10.1')

```

Take care to include the subnet notation of `/24`. It equates to a netmask of `255.255.255.0`) and without it the profile will fail to start. See also [CIDR notation](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing#CIDR_notation "wikipedia:Classless Inter-Domain Routing"). To alias more than one IP address per a NIC set `Address=('10.1.10.2/24' '192.168.1.2/24')`.

#### Wireless (WPA-PSK)

The following applies for the standard wireless connections using a pre-shared key (WPA-PSK).

 `/etc/netctl/wireless-wpa` 
```
Description='A simple WPA encrypted wireless connection using 256-bit PSK'
Interface=wlp2s2
Connection=wireless
Security=wpa
IP=dhcp
ESSID=*your_essid*
Key=\"64cf3ced850ecef39197bb7b7b301fc39437a6aa6c6a599d0534b16af578e04a
```

**Note:**

*   Make sure to use the **special quoting rules** for the `Key` variable as explained at the end of [netctl.profile(5)](https://github.com/joukewitteveen/netctl/blob/master/docs/netctl.profile.5.txt).
*   If the passphrase fails, try removing the `\"` in the `Key` variable.
*   Although "encrypted", the key that you put in the profile configuration is enough to connect to a WPA-PSK network. Therefore this process is only useful for hiding the human-readable version of the passphrase. This will not prevent anyone with read access to this file from connecting to the network.

### Obfuscate wireless passphrase

You can also follow the following step to obfuscate the wireless passphrase (*wifi-menu* does it automatically when using the `-o` flag):

Users **not** wishing to have the passphrase to their wireless network stored in *plain text* have the option of storing the corresponding 256-bit pre-shared key instead, which is calculated from the passphrase and the SSID using standard algorithms.

Calculate your 256-bit PSK using [wpa_passphrase](/index.php/WPA_supplicant#Connecting_with_wpa_passphrase "WPA supplicant"):

 `$ wpa_passphrase *your_essid*` 
```
network={
  ssid="*your_essid*"
  #psk="*passphrase*"
  psk=64cf3ced850ecef39197bb7b7b301fc39437a6aa6c6a599d0534b16af578e04a
}
```

The *pre-shared key* (psk) now needs to replace the plain text passphrase of the `Key` variable in the profile.

### Using an experimental GUI

If you want a graphical user interface to manage *netctl* and your connections and you are not afraid of highly experimental unofficial packages, there are some options available. [netctl-gui](https://aur.archlinux.org/packages/netctl-gui/) provides a Qt-based graphical interface, DBus daemon and KDE widget. An alternative is [netmenu](https://aur.archlinux.org/packages/netmenu/), which uses [dmenu](https://www.archlinux.org/packages/?name=dmenu) as its graphical interface.

### Bonding

From [kernel documentation](https://www.kernel.org/doc/Documentation/networking/bonding.txt):

	The Linux bonding driver provides a method for aggregating multiple network interfaces into a single logical "bonded" interface. The behavior of the bonded interfaces depends on the mode. Generally speaking, modes provide either hot standby or load balancing services. Additionally, link integrity monitoring may be performed.

#### Load balancing

To use bonding with netctl, additional package from official repositories is required: [ifenslave](https://www.archlinux.org/packages/?name=ifenslave).

Copy `/etc/netctl/examples/bonding` to `/etc/netctl/bond0` and edit it, for example:

 `/etc/netctl/bond0` 
```
Description='Bond Interface'
Interface='bond0'
Connection=bond
BindsToInterfaces=('eth0' 'eth1')
IP=dhcp
IP6=stateless
```

Now you can disable your old configuration and set *bond0* to be started automatically. Switch to the new profile, for example:

```
# netctl switch-to bond0

```

**Note:** This uses the round-robin policy, which is the default for the `bonding` driver. See [official documentation](https://www.kernel.org/doc/Documentation/networking/bonding.txt) for details.

Setting the MODE in the netctl configuration is not always successful and it may be necessary to pass options directly to the bonding module on load as noted [here](https://bbs.archlinux.org/viewtopic.php?id=203255). This may be needed to use LACP / mode 4.

**Tip:** To check the status and bonding mode: `$ cat /proc/net/bonding/bond0` 

#### Wired to wireless failover

This example describes how to use *bonding* to fallback to wireless when the wired ethernet goes down. This is most useful when both the wired and wireless interface will be connected to the same network. Your wireless router/access point must be configured in [bridge](/index.php/Bridge "Bridge") mode.

You will need additional packages from the official repositories: [ifenslave](https://www.archlinux.org/packages/?name=ifenslave) and [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant).

First enable the bonding module to be loaded upon boot time, as instructed on [Kernel modules#Automatic module loading with systemd](/index.php/Kernel_modules#Automatic_module_loading_with_systemd "Kernel modules"):

 `/etc/modules-load.d/bonding.conf`  `bonding` 

Then, configure the options of the `bonding` driver to use `active-backup` and configure the `primary` parameter to the device you want to be the active one (normally the wired interface). Also, be sure to use the same device name as returned when running `ip link`:

 `/etc/modprobe.d/bonding.conf`  `options bonding mode=active-backup miimon=100 primary=eth0 max_bonds=0` 

The `miimon` option is needed, for the link failure detection. The `max_bonds` option avoids the `Interface bond0 already exists` error. More information can be obtained on the [kernel documentation](https://www.kernel.org/doc/Documentation/networking/bonding.txt).

Next, configure a netctl profile to enslave the two hardware interfaces. Use the name of all the devices you want to enslave. If you have more than two wired or wireless interfaces, you can enslave all of them on a bond interface. But, for most cases you will have only two devices, a wired and a wireless one:

 `/etc/netctl/failover` 
```
Description='A wired connection with failover to wireless'
Interface='bond0'
Connection=bond
BindsToInterfaces=('eth0' 'wlan0')
IP='dhcp'
```

Disable any other profiles (specially a wired or wireless) you had enabled before and then enable the failover profile on startup:

```
# netctl enable failover

```

Now you need to configure *wpa_supplicant* to connect to any known network you wish. You should create a file for each interface and enable it on systemd. Create the following file with this content:

 `/etc/wpa_supplicant/wpa_supplicant-wlan0.conf` 
```
ctrl_interface=/run/wpa_supplicant
update_config=1
```

And append to the end of this file any network you want to connect to:

```
network={
    ssid="SSID"
    psk=PSK
}

```

To generate the obfuscated PSK you can run *wpa_passphrase* as on the [WPA supplicant#Connecting with wpa_passphrase](/index.php/WPA_supplicant#Connecting_with_wpa_passphrase "WPA supplicant") page.

Now, [enable](/index.php/Enable "Enable") the `wpa_supplicant@` template service on the network interface, for example `wpa_supplicant@wlan0`.

You can try now to reboot your machine and see if your configuration worked.

**Note:** If you get this error on boot bonding:
```
wlan0 is up - this may be due to an out of date ifenslave

```

Then this is happening because the *wpa_supplicant* is being run before the `failover` netctl profile. This happens because [systemd](/index.php/Systemd "Systemd") runs everything in parallel, unless told otherwise. *ifenslave* need all the interfaces to be down before bonding them to the `bond0` interface. And, since the *wpa_supplicant* need to put the interface up to be able to scan for networks, this might cause the interface to not be enslaved and your bonding to only have the wired interface.

If this is your case, then you will need to setup a custom dependency on the `wpa_supplicant@wlan0` service in relation with the `netctl@failover` profile. More specifically, the *wpa_supplicant* must be started **after** the netctl profile. To accomplish this, create a custom dependency file based on the instructions provided here: [systemd#Handling dependencies](/index.php/Systemd#Handling_dependencies "Systemd")

 `/etc/systemd/system/wpa_supplicant@wlan0.service.d/customdependency.conf` 
```
[Unit]
After=netctl@failover.service
```

After that you can try to reboot your system again and see if it works. You can check the status of your bonding by checking [journalctl](/index.php/Journalctl "Journalctl") for the `netctl@failover.service` unit.

And by checking:

```
# ip link

```

You should see something like this:

```
1: eth0: <BROADCAST,MULTICAST,SLAVE,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast master bond0 state UP mode DEFAULT group default qlen 1000
    link/ether xx:xx:xx:xx:xx:xx brd ff:ff:ff:ff:ff:ff
2: wlan0: <BROADCAST,MULTICAST,SLAVE,UP,LOWER_UP> mtu 1500 qdisc mq master bond0 state UP mode DORMANT group default qlen 1000
    link/ether xx:xx:xx:xx:xx:xx brd ff:ff:ff:ff:ff:ff
3: bond0: <BROADCAST,MULTICAST,MASTER,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP mode DEFAULT group default 
    link/ether xx:xx:xx:xx:xx:xx brd ff:ff:ff:ff:ff:ff

```

Now, you can test your failover setup, by initiating a big download. Unplug your wired interface. Your download should keep going over the wireless interface. Then, plug your wired interface again and it should keep working. You can debug by checking [journalctl](/index.php/Journalctl "Journalctl") for the `netctl@failover.service` and `wpa_supplicant@wlan0.service` units.

### Using any interface

In some cases it may be desirable to allow a profile to use any interface on the system. A common example use case is using a common disk image across many machines with differing hardware (this is especially useful if they are headless). If you use the kernel's naming scheme, and your machine has only one ethernet interface, you can probably guess that eth0 is the right interface. If you use udev's [Predictable Network Interface Names](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames/), however, names will be assigned based on the specific hardware itself (e.g. enp1s0), rather than simply the order that the hardware was detected (e.g. eth0, eth1). This means that a netctl profile may work on one machine and not another, because they each have different interface names.

A quick and dirty solution is to make use of the `/etc/netctl/interfaces/` directory. Choose a name for your interface alias (`en-any` in this example), and write the following to a file with that name (making sure it is executable).

 `/etc/netctl/interfaces/en-any` 
```
#!/bin/bash
for interface in /sys/class/net/en*; do
        break;
done
Interface=$(basename $interface)
echo "en-any: using interface $Interface";

```

Then create a profile that uses the interface. Pay special attention to the `Interface` directive. The rest are only provided as examples.

 `/etc/netctl/wired` 
```
Description='Wired'
Interface=en-any
Connection=ethernet
IP=static
Address=('192.168.1.15/24')
Gateway='192.168.1.1'
DNS=('192.168.1.1')

```

When the `wired` profile is started, any machine using the two files above will automatically bring up and configure the first ethernet interface found on the system, regardless of what name udev assigned to it. Note that this is not the most robust way to go about configuring interfaces. If you use multiple interfaces, netctl may try to assign the same interface to them, and will likely cause a disruption in connectivity. If you do not mind a more complicated solution, `netctl-auto` is likely to be more reliable.

### Using hooks

netctl supports hooks in `/etc/netctl/hooks/` and per interface hooks in `/etc/netctl/interfaces/`. You can set any option in a hook/interface that you can in a profile. Most importantly this includes `ExecUpPost` and `ExecDownPre`.

When a profile is read, netctl sources **all executable** scripts in `hooks`, then it reads the profile file for the connection and finally it sources an executable script with the name of the interface used in the profile from the `interfaces` directory. Therefore, declarations in an interface script override declarations in the profile, which override declarations in hooks.

The variables `$INTERFACE` and `$ACTION` are available in hooks/interfaces **only** when using `netctl-auto`

#### Examples

##### Execute commands on established connection

 `/etc/netctl/hooks/myservices` 
```
#!/bin/sh
ExecUpPost="systemctl start crashplan.service; systemctl start dropbox@<username>.service"
ExecDownPre="systemctl stop crashplan.service; systemctl stop dropbox@<username>.service"

```

##### Set default DHCP client

To set or change the DHCP client used for all profiles:

 `/etc/netctl/hooks/dhcp` 
```
#!/bin/sh
DHCPClient='dhclient'

```

Alternatively, it may also be specified for a specific network interface by creating an executable file `/etc/netctl/interfaces/<interface>` with the following line:

```
DHCPClient='dhclient'

```

### Minimal WPAConfigSection

As stated in the [netctl.profile(5)](https://projects.archlinux.org/netctl.git/tree/docs/netctl.profile.5.txt#n281) man page, the `WPAConfigSection` variable is an array of config lines passed to [wpa_supplicant](/index.php/Wpa_supplicant "Wpa supplicant"). So, a minimal WPAConfigSection would contain:

```
Description='A wireless connection using a custom network block configuration'
Interface=wlan0
Connection=wireless
Security=wpa-configsection
IP=dhcp
WPAConfigSection=(
    'ssid="University"'
    'psk="very secret passphrase"'
)

```

**Note:** If trying to connect to an SSID with non-ASCII characters (unicode, emoji, etc), you can specify the SSID as hex instead of as a string, e.g. `ssid=F09F90BA` for "🐺". When unsure on the hex encoding, run *wifi-menu* (be sure to remove the \ and x characters).

### resolv.conf

If you use `DNS*` options in your profile, *netctl* calls [resolvconf](/index.php/Resolvconf "Resolvconf") to overwrite [resolv.conf](/index.php/Resolv.conf "Resolv.conf").

## Troubleshooting

### Job for netctl@wlan(...).service failed

**Warning:** This section assumes that there is no other network service running before starting a *netctl* profile/service. See [#Installation](#Installation) for details.

Some people have an issue when they connect to a network with *netctl*, for example:

 `# netctl start wlan0-ssid` 
```
Job for netctl@wlan0\x2ssid.service failed. See 'systemctl status netctl@wlan0\x2ssid.service' and 'journalctl -xn' for details.

```

When then looking at `journalctl -xn`, either of the following are shown:

1\. If your device (`wlan0` in this case) is up:

```
network[2322]: The interface of network profile 'wlan0-ssid' is already up

```

Setting the interface down should resolve the problem:

```
# ip link set wlan0 down

```

Then retry:

```
# netctl start wlan0-ssid

```

2\. If the error continues, try again after adding the `ForceConnect` option:

 `/etc/netctl/wlan0-ssid` 
```
...
ForceConnect=yes

```

Save it and try to connect with the profile:

```
# netctl start wlan0-ssid

```

### dhcpcd: ipv4_addroute: File exists

On some systems dhcpcd in combination with netctl causes timeout issues on resume, particularly when having switched networks in the meantime. netctl will report that you are successfully connected but you still receive timeout issues. In this case, the old default route still exists and is not being renewed. A workaround to avoid this misbehaviour is to switch to [dhclient](#Set_default_DHCP_client) as the default dhcp client. More information on the issue can be found [here](https://bbs.archlinux.org/viewtopic.php?pid=1399842#p1399842).

### DHCP timeout issues

If you are having timeout issues when requesting leases via DHCP you can set the timeout value higher than netctl's 30 seconds by default. Create a file in `/etc/netctl/hooks/` or `/etc/netctl/interfaces/`, add `TimeoutDHCP=40` to it for a timeout of 40 seconds and make the file executable.

### dhcpcd debugging

If dhcpcd fails to obtain an address, add the `-d` option to `/usr/lib/netctl/dhcp` and then use `journalctl -xe` to view the debugging messages which may indicate, for example, that the IP address offered by the server is rejected by the client after detecting that the IP address is already in use.

### Connection timeout issues

If you are having timeout issues that are unrelated to DHCP (on a static ethernet connection for example), and are experiencing errors similar to the following when starting your profile:

 `# journalctl _SYSTEMD_UNIT=netctl@*profile*.service` 
```
Starting network profile '*profile*'...
No connection found on interface 'eth0' (timeout)
Failed to bring the network up for profile '*profile*'

```

Then you should increase carrier and up timeouts by adding `TimeoutUp=` and `TimeoutCarrier=` to your profile file:

 `/etc/netctl/*profile*` 
```
...
TimeoutUp=300
TimeoutCarrier=300

```

Do not forget to reenable your profile:

```
# netctl reenable *profile*

```

### Problems with netctl-auto on resume

Sometimes *netctl-auto* fails to reconnect when the system resumes from suspend, hibernate or hybrid-sleep. An easy solution is to restart the service for *netctl-auto*. This can be automated with an additional service like the following ([netctl-auto-resume](https://aur.archlinux.org/packages/netctl-auto-resume/)):

 `/etc/systemd/system/netctl-auto-resume@.service` 
```
[Unit]
Description=restart netctl-auto on resume.
Requisite=netctl-auto@%i.service
After=sleep.target

[Service]
Type=oneshot
ExecStart=/usr/bin/systemctl restart netctl-auto@%i.service

[Install]
WantedBy=sleep.target

```

To [enable](/index.php/Enable "Enable") this service for your wireless card, for example, enable `netctl-auto-resume@wlan0.service` as root. Change `wlan0` to the required network interface.

If the device is not yet running on resume when the unit is started, this will fail. It can be fixed by adding the following dependency in the *After* line:

 `/etc/systemd/system/netctl-auto-resume@.service` 
```
...
After=sleep.target sys-subsystem-net-devices-%i.device
...

```

### netctl-auto does not automatically unblock a wireless card to use an interface

Many laptops have a hardware button (or switch) to turn off wireless card, however, the card can also be blocked by the kernel. This can be handled by [rfkill](/index.php/Rfkill "Rfkill").

If you want *netctl-auto* to automatically unblock your wireless card to connect to a particular network, set `RFKill=++auto++` option for the wireless connection of your choice, as specified in the [netctl.profile(5)](https://github.com/joukewitteveen/netctl/blob/master/docs/netctl.profile.5.txt) man page.

### RTNETLINK answers: File exists (with multiple NICs)

This is a very misleading response, it really means that you have assigned a default gateway in an earlier netctl control file. When netctl starts up the n-th NIC and goes to set its local route, it fails because there is already a default route from n-1.

Remove it and everything works, except you no longer have a default route and so cannot access things such as the internet. `ExecUpPost` does not work as it gets executed for each network card.

A possible solution is creating a new service. Replace "FIRST_INTERFACE" and "SECOND_INTERFACE" with your interface names, and replace "192.168.xxx.yyy" with your default gateway.

 `/etc/systemd/system/defaultrouter.service` 
```
[Unit]
Description="Configure default gateway"
Requires=netctl@FIRST_INTERFACE.service netctl@SECOND_INTERFACE.service
After=netctl@FIRST_INTERFACE.service netctl@SECOND_INTERFACE.service

[Service]
Type=oneshot
ExecStart=/usr/bin/ip route add default via 192.168.xxx.yyy

[Install]
WantedBy=network-online.target

```

### Problems with eduroam and other MSCHAPv2 connections

See [WPA supplicant#Problems with eduroam and other MSCHAPv2 connections](/index.php/WPA_supplicant#Problems_with_eduroam_and_other_MSCHAPv2_connections "WPA supplicant").

### Journal warnings for profiles using .include directives

Profiles still using systemd's old `.include` directives will produce journal warnings, for example:

```
systemd[1]: /etc/systemd/system/netctl@<profile>.service:1: .include directives are deprecated, and support for them will be removed in a future version of systemd. Please use drop-in files instead.

```

See [FS#59494](https://bugs.archlinux.org/task/59494) for details.

Executing

```
netctl reenable *profile*

```

will update the profile to the new [drop-in unit file](/index.php/Drop-in_unit_file "Drop-in unit file") format.

### Hooks don't work

If you have multiple hooks in `/etc/netctl/hooks/`, variables like `ExecUpPost` and `ExecDownPre` will be executed only from one file. To fix this, define the variables like this:

 `/etc/netctl/hooks/test` 
```
ExecUpPost="some command ; "$ExecUpPost
ExecDownPre="some command ; "$ExecDownPre

```

This will append your commands to be executed with already defined ones.

## See also

*   [Initial mailing list announcement](https://lists.archlinux.org/pipermail/arch-projects/2012-December/003473.html)
*   [Official announcement thread](https://bbs.archlinux.org/viewtopic.php?id=157670)
*   [Official news announcement](https://www.archlinux.org/news/netctl-is-now-in-core/)