# netctl

[netctl](https://projects.archlinux.org/netctl.git/) is a CLI-based tool used to configure and manage network connections via profiles.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
    *   [3.1 Profile configuration](#Profile_configuration)
    *   [3.2 Automatic operation](#Automatic_operation)
        *   [3.2.1 Basic method](#Basic_method)
        *   [3.2.2 Automatic switching of profiles](#Automatic_switching_of_profiles)
    *   [3.3 Example profiles](#Example_profiles)
        *   [3.3.1 Wired](#Wired)
        *   [3.3.2 Wireless (WPA-PSK)](#Wireless_.28WPA-PSK.29)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Using an Experimental GUI](#Using_an_Experimental_GUI)
    *   [4.2 Eduroam](#Eduroam)
    *   [4.3 Bonding](#Bonding)
        *   [4.3.1 Load balancing](#Load_balancing)
        *   [4.3.2 Wired to wireless failover](#Wired_to_wireless_failover)
    *   [4.4 Using any interface](#Using_any_interface)
    *   [4.5 Using hooks](#Using_hooks)
        *   [4.5.1 Examples](#Examples)
            *   [4.5.1.1 Execute commands on established connection](#Execute_commands_on_established_connection)
            *   [4.5.1.2 Activate network-online.target](#Activate_network-online.target)
            *   [4.5.1.3 Set default DHCP client](#Set_default_DHCP_client)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Job for netctl@wlan(...).service failed](#Job_for_netctl.40wlan.28....29.service_failed)
    *   [5.2 dhcpcd: ipv4_addroute: File exists](#dhcpcd:_ipv4_addroute:_File_exists)
    *   [5.3 DHCP timeout issues](#DHCP_timeout_issues)
    *   [5.4 Connection timeout issues](#Connection_timeout_issues)
    *   [5.5 Problems with netctl-auto on resume](#Problems_with_netctl-auto_on_resume)
    *   [5.6 netctl-auto suddenly stopped working for WiFi adapters](#netctl-auto_suddenly_stopped_working_for_WiFi_adapters)
    *   [5.7 netctl-auto does not automatically unblock a wireless card to use an interface](#netctl-auto_does_not_automatically_unblock_a_wireless_card_to_use_an_interface)
    *   [5.8 RTNETLINK answers: File exists (with multiple NICs)](#RTNETLINK_answers:_File_exists_.28with_multiple_NICs.29)
*   [6 See also](#See_also)

## Installation

[netctl](https://www.archlinux.org/packages/?name=netctl) is part of the [base](https://www.archlinux.org/groups/x86_64/base/) group, so it should already be installed on your system. Otherwise [install](/index.php/Install "Install") it as usual.

Optional dependencies are shown in the table below.

| Feature | Dependency | netctl program
(if relevant) |
| Automatic wireless connections | [wpa_actiond](https://www.archlinux.org/packages/?name=wpa_actiond) | `netctl-auto` |
| Automatic wired connections | [ifplugd](https://www.archlinux.org/packages/?name=ifplugd) | `netctl-ifplugd` |
| WPA | [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) |
| DHCP | [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) or [dhclient](https://www.archlinux.org/packages/?name=dhclient) |
| Wifi menus | [dialog](https://www.archlinux.org/packages/?name=dialog) |
| PPPoE | [ppp](https://www.archlinux.org/packages/?name=ppp) |

**Warning:** Do not enable concurrent, conflicting network service. Use `systemctl --type=service` to ensure that no other network service is running before enabling a _netctl_ profile/service.

## Usage

It is advisable to read the following man pages before using netctl:

*   [netctl](https://github.com/joukewitteveen/netctl/blob/master/docs/netctl.1.txt)
*   [netctl.profile](https://github.com/joukewitteveen/netctl/blob/master/docs/netctl.profile.5.txt)
*   [netctl.special](https://github.com/joukewitteveen/netctl/blob/master/docs/netctl.special.7.txt)

## Configuration

_netctl_ uses profiles to manage network connections and different modes of operation to start profiles automatically or manually on demand.

### Profile configuration

The _netctl_ profile files are stored in `/etc/netctl/` and example configuration files are available in `/etc/netctl/examples/`. Common configurations include:

*   ethernet-dhcp
*   ethernet-static
*   wireless-wpa
*   wireless-wpa-static

To use an example profile, simply copy it from `/etc/netctl/examples/` to `/etc/netctl/` and configure it to your needs; see basic [#Example profiles](#Example_profiles) below. The first parameter you need to create a profile is the network `Interface`, see [Network configuration#Device names](/index.php/Network_configuration#Device_names "Network configuration") for details.

**Tip:**

*   For wireless settings, you can use `wifi-menu -o` as root to generate the profile file in `/etc/netctl/`.
*   To enable a static IP profile on wired interface no matter if the cable is connected or not, use `SkipNoCarrier=yes` in your profile.

Once you have created your profile, attempt to establish a connection (use only the profile name, not the full path):

```
# netctl start _profile_

```

If the above command results in a failure, then use `journalctl -xn` and `netctl status _profile_` to obtain a more in depth explanation of the failure.

### Automatic operation

If you use only one profile (per interface) or want to switch profiles manually, the [Basic method](#Basic_method) will do. Most common examples are servers, workstations, routers etc.

If you need to switch multiple profiles frequently, use [Automatic switching of profiles](#Automatic_switching_of_profiles). Most common examples are laptops.

#### Basic method

With this method, you can statically start only one profile per interface. First manually check that the profile can be started successfully with:

```
# netctl start _profile_ 

```

then it can be enabled using:

```
# netctl enable _profile_

```

This will create and enable a [systemd](/index.php/Systemd "Systemd") service that will start when the computer boots. Changes to the profile file will not propagate to the service file automatically. After such changes, it is necessary to reenable the profile:

```
# netctl reenable _profile_

```

After enabling a profile, it will be started at next boot. Obviously this can only be successful, if the network cable for a wired connection is plugged in, or the wireless access point used in a profile is in range respectively.

#### Automatic switching of profiles

_netctl_ provides two special [systemd](/index.php/Systemd "Systemd") services for automatic switching of profiles:

*   Package [ifplugd](https://www.archlinux.org/packages/?name=ifplugd) for wired interfaces: After [starting and enabling](/index.php/Start "Start") `netctl-ifplugd@_interface_.service` DHCP profiles are started/stopped when the network cable is plugged in and out. To include a static IP profile the option `ExcludeAuto=no` needs to be set in it.
*   Package [wpa_actiond](https://www.archlinux.org/packages/?name=wpa_actiond) for wireless interfaces: After [starting and enabling](/index.php/Start "Start") `netctl-auto@_interface_.service` profiles are started/stopped automatically as you move from the range of one network into the range of another network (roaming).

Note that _interface_ is not literal, but to be substituted by the name of your device's interface, e.g. `netctl-auto@wlp4s0.service`.

The following options can be used:

*   If you want some wireless profile **not** to be started automatically by `netctl-auto@_interface_.service`, you have to explicitly add `ExcludeAuto=yes` to that profile.
*   The `netctl-ifplugd@_interface_.service` will prefer profiles which use [DHCP](https://en.wikipedia.org/wiki/DHCP "wikipedia:DHCP"). To prefer a profile with a static IP, you can set `Priority=2`, which is higher than the default priority given to DHCP profiles of `Priority=1`. Do not forget to also set `ExcludeAuto=no` as mentioned above. See `netctl.profile(5)` for details.
*   You can use `priority=` in the _WPAConfigSection_ (see `/etc/netctl/examples/wireless-wpa-configsection`) to set priority of a profile when multiple wireless access points are available. Note that automatic selection of a WPA profile by _netctl-auto_ is not possible with option `Security=wpa-config`, use `Security=wpa-configsection` instead.

**Warning:**

*   If any of the profiles contain errors, such as an empty or misquoted `Key=` variable, the unit will fail to load with the message `"Failed to read or parse configuration '/run/network/wpa_supplicant_wlan0.conf'`, even when that profile is not being used.
*   This method conflicts with the [Basic method](#Basic_method). If you have previously enabled a profile through _netctl_, run `netctl disable _profile_` to prevent the profile from starting twice at boot.

Since netctl 1.3 it is possible to manually control an interface otherwise managed by _netctl-auto_ without having to stop `netctl-auto.service`. This is done using the _netctl-auto_ command. For a list of available actions run:

```
 # netctl-auto --help

```

### Example profiles

#### Wired

For a DHCP connection, only the `Interface` has to be configured after copying the `/etc/netctl/examples/ethernet-dhcp` example profile to `/etc/netctl`.

For example:

 `/etc/netctl/_my_dhcp_profile_` 

```
Interface=enp1s0
Connection=ethernet
IP=dhcp

```

For a static IP configuration copy the `/etc/netctl/examples/ethernet-static` example profile to `/etc/netctl` and modify `Interface`, `Address`, `Gateway` and `DNS`) as needed.

For example:

 `/etc/netctl/_my_static_profile_` 

```
Interface=enp1s0
Connection=ethernet
IP=static
Address=('10.1.10.2/24')
Gateway='10.1.10.1'
DNS=('10.1.10.1')

```

Take care to include the subnet notation of `/24`. It equates to a netmask of `255.255.255.0`) and without out it the profile will fail to start. See also [CIDR notation](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing#CIDR_notation "wikipedia:Classless Inter-Domain Routing"). To alias more than one IP address per a NIC set `Address=('10.1.10.2/24' '192.168.1.2/24')`.

#### Wireless (WPA-PSK)

The following applies for the standard wireless connections using a pre-shared key (WPA-PSK). See [WPA2 Enterprise#netctl](/index.php/WPA2_Enterprise#netctl "WPA2 Enterprise") for example profiles with other authentication methods.

The standard _netctl_ tool to connect to a wireless network (WPA-PSK, WEP) interactively is _wifi-menu_; used with the `-o` option:

```
wifi-menu -o 

```

it generates the configuration file in `/etc/netctl/` for the network to use for [#Automatic operation](#Automatic_operation) at the same time.

Alternatively, the profile may also be configured manually, as follows:

Copy the example file `wireless-wpa` from `/etc/netctl/examples` to `/etc/netctl` (name of your choice):

```
# cp /etc/netctl/examples/wireless-wpa /etc/netctl/.

```

Edit the profile as needed (modifying `Interface`, `ESSID` and `Key`) and it is done.

At this step you may want to re-confirm the new profile you created is `chmod 600` and confirm it works by starting it:

```
netctl start wireless-wpa

```

before configuring any [#Automatic operation](#Automatic_operation).

Optionally you can also follow the following step to obfuscate the wireless passphrase (_wifi-menu_ does it automatically):

Users **not** wishing to have the passphrase to their wireless network stored in _plain text_ have the option of storing the corresponding 256-bit pre-shared key instead, which is calculated from the passphrase and the SSID using standard algorithms.

Calculate your 256-bit PSK using [wpa_passphrase](/index.php/WPA_supplicant#Connecting_with_wpa_passphrase "WPA supplicant"):

 `$ wpa_passphrase _your_essid_ _passphrase_` 

```
network={
  ssid="_your_essid_"
  #psk="_passphrase_"
  psk=64cf3ced850ecef39197bb7b7b301fc39437a6aa6c6a599d0534b16af578e04a
}
```

The _pre-shared key_ (psk) now needs to replace the plain text passphrase of the `Key` variable in the profile. Once completed your network profile `wireless-wpa` containing a 256-bit PSK should resemble:

 `/etc/netctl/wireless-wpa` 

```
Description='A simple WPA encrypted wireless connection using 256-bit PSK'
Interface=wlp2s2
Connection=wireless
Security=wpa
IP=dhcp
ESSID=_your_essid_
Key=\"64cf3ced850ecef39197bb7b7b301fc39437a6aa6c6a599d0534b16af578e04a
```

**Note:**

*   Make sure to use the **special quoting rules** for the `Key` variable as explained at the end of [netctl.profile(5)](https://github.com/joukewitteveen/netctl/blob/master/docs/netctl.profile.5.txt).
*   If the passphrase fails, try removing the `\"` in the `Key` variable.
*   Although "encrypted", the key that you put in the profile configuration is enough to connect to a WPA-PSK network. Therefore this process is only useful for hiding the human-readable version of the passphrase. This will not prevent anyone with read access to this file from connecting to the network.

## Tips and tricks

### Using an Experimental GUI

If you want a graphical user interface to manage _netctl_ and your connections and you are not afraid of highly experimental unofficial packages you can install [netgui](https://aur.archlinux.org/packages/netgui/) from [AUR](/index.php/AUR "AUR"). Note, however, that _netgui_ is still in beta status and you should be familiar with the general _netctl_ syntax to debug possible issues. Another GUI alternative is [netctl-gui](https://aur.archlinux.org/packages/netctl-gui/) which provides a Qt-based graphical interface, DBus daemon and KDE widget. A third alternative is [netmenu](https://aur.archlinux.org/packages/netmenu/), which uses [dmenu](https://www.archlinux.org/packages/?name=dmenu) as its graphical interface.

### Eduroam

See [WPA2 Enterprise#netctl](/index.php/WPA2_Enterprise#netctl "WPA2 Enterprise").

### Bonding

From [kernel documentation](https://www.kernel.org/doc/Documentation/networking/bonding.txt):

	_The Linux bonding driver provides a method for aggregating multiple network interfaces into a single logical "bonded" interface. The behavior of the bonded interfaces depends on the mode. Generally speaking, modes provide either hot standby or load balancing services. Additionally, link integrity monitoring may be performed._

#### Load balancing

To use bonding with netctl, additional package from official repositories is required: [ifenslave](https://www.archlinux.org/packages/?name=ifenslave).

Copy `/etc/netctl/examples/bonding` to `/etc/netctl/bonding` and edit it, for example:

 `/etc/netctl/bonding` 

```
Description='Bond Interface'
Interface='bond0'
Connection=bond
BindsToInterfaces=('eth0' 'eth1')
IP=dhcp
IP6=stateless
```

Now you can disable your old configuration and set _bonding_ to be started automatically. Switch to the new profile, for example:

```
# netctl switch-to bonding

```

**Note:** This uses the round-robin policy, which is the default for the `bonding` driver. See [official documentation](https://www.kernel.org/doc/Documentation/networking/bonding.txt) for details.

**Tip:** To check the status and bonding mode: `$ cat /proc/net/bonding/bond0` 

#### Wired to wireless failover

This example describes how to use _bonding_ to fallback to wireless when the wired ethernet goes down. This is most useful when both the wired and wireless interface will be connected to the same network. Your wireless router/access point must be configured in _bridge_ mode.

You will need additional packages from the official repositories: [ifenslave](https://www.archlinux.org/packages/?name=ifenslave) and [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant).

First enable the bonding module to be loaded upon boot time, as instructed on [Kernel modules#Automatic module handling](/index.php/Kernel_modules#Automatic_module_handling "Kernel modules"):

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

Now you need to configure _wpa_supplicant_ to connect to any know network you wish. You should create a file for each interface and enable it on systemd. Create the following file with this content:

 `/etc/wpa_supplicant/wpa_supplicant-wlan0.conf` 

```
ctrl_interface=/run/wpa_supplicant
update_config=1
```

And append to the end of this file any networks you want to connect:

```
network={
    ssid="SSID"
    psk=PSK
}

```

To generate the obfuscated PSK you can run _wpa_passphrase_ as on the [WPA supplicant#Connecting with wpa_passphrase](/index.php/WPA_supplicant#Connecting_with_wpa_passphrase "WPA supplicant") page.

Now, [enable](/index.php/Enable "Enable") the `wpa_supplicant@` template service on the network interface, for example `wpa_supplicant@wlan0`.

You can try now to reboot your machine and see if your configuration worked.

**Note:** If you get this error on boot bonding:

```
wlan0 is up - this may be due to an out of date ifenslave

```

Then this is happening because the _wpa_supplicant_ is being run before the `failover` netctl profile. This happens because [systemd](/index.php/Systemd "Systemd") runs everything in parallel, unless told otherwise. _ifenslave_ need all the interfaces to be down before bonding them to the `bond0` interface. And, since the _wpa_supplicant_ need to put the interface up to be able to scan for networks, this might cause the interface to not be enslaved and your bonding to only have the wired interface.

If this is your case, then you will need to setup a custom dependency on the `wpa_supplicant@wlan0` service in relation with the `netctl@failover` profile. More specifically, the _wpa_supplicant_ must be started **after** the netctl profile. To accomplish this, create a custom dependency file based on the instructions provided here: [systemd#Handling dependencies](/index.php/Systemd#Handling_dependencies "Systemd")

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

netctl supports hooks in `/etc/netctl/hooks/` and per interface hooks in `/etc/netctl/interfaces/`. You can set any option in a hook/interface that you can in a profile. They are read the same way! Most importantly this includes `ExecUpPost` and `ExecDownPre`.

When a profile is read, netctl sources **all executable** scripts in `hooks`, then it reads the profile file for the connection and finally it sources an executable script with the name of the interface used in the profile from the `interfaces` directory. Therefore, declarations in an interface script override declarations in the profile, which override declarations in hooks.

The variables `$INTERFACE`, `$SSID`, `$ACTION` and `$Profile` are available in hooks/interfaces **only** when using `netctl-auto`

#### Examples

##### Execute commands on established connection

 `/etc/netctl/hooks/myservices` 

```
#!/bin/sh
ExecUpPost="systemctl start crashplan.service; systemctl start dropbox@<username>.service"
ExecDownPre="systemctl stop crashplan.service; systemctl stop dropbox@<username>.service"

```

##### Activate network-online.target

 `/etc/netctl/hooks/status` 

```
#!/bin/sh
ExecUpPost="systemctl start network-online.target"
ExecDownPre="systemctl stop network-online.target"

```

Using this, systemd services requiring an active network connection can be [ordered](/index.php/Systemd#Handling_dependencies "Systemd") to start only after the `network-online.target` is reached, and can be stopped before the connection is brought down.

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

## Troubleshooting

### Job for netctl@wlan(...).service failed

Some people have an issue when they connect to a network with _netctl_, for example:

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

2\. If it is down:

```
dhcpcd[261]: wlan0: ipv4_sendrawpacket: Network is down

```

One way to solve this is to use a different DHCP client, for example [dhclient](https://www.archlinux.org/packages/?name=dhclient). After installing the package configure _netctl_ to use it:

 `/etc/netctl/wlan0-ssid` 

```
...
DHCPClient='dhclient'

```

Adding the `ForceConnect` option may also be helpful:

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

### Connection timeout issues

If you are having timeout issues that are unrelated to DHCP (on a static ethernet connection for example), and are experiencing errors similar to the following when starting your profile:

 `# journalctl _SYSTEMD_UNIT=netctl@_profile_.service` 

```
Starting network profile '_profile_'...
No connection found on interface 'eth0' (timeout)
Failed to bring the network up for profile '_profile_'

```

Then you should increase carrier and up timeouts by adding `TimeoutUp=` and `TimeoutCarrier=` to your profile file:

 `/etc/netctl/_profile_` 

```
...
TimeoutUp=300
TimeoutCarrier=300

```

Do not forget to reenable your profile:

```
# netctl reenable _profile_

```

### Problems with netctl-auto on resume

Sometimes _netctl-auto_ fails to reconnect when the system resumes from suspend. An easy solution is to restart the service for _netctl-auto_. This can be automated with an additional service like the following:

 `/etc/systemd/system/netctl-auto-resume@.service` 

```
[Unit]
Description=restart netctl-auto on resume.
Requisite=netctl-auto@%i.service
After=suspend.target

[Service]
Type=oneshot
ExecStart=/usr/bin/systemctl restart netctl-auto@%i.service

[Install]
WantedBy=suspend.target

```

To [enable](/index.php/Enable "Enable") this service for your wireless card, for example, enable `netctl-auto-resume@wlan0.service` as root. Change `wlan0` to the required network interface.

If the device is not yet running on resume when the unit is started, this will fail. It can be fixed by adding the following dependency in the _After_ line:

 `/etc/systemd/system/netctl-auto-resume@.service` 

```
...
After=suspend.target sys-subsystem-net-devices-%i.device
...

```

### netctl-auto suddenly stopped working for WiFi adapters

This problem seems to be related to a recent wpa_supplicant update (see [FS#44731](https://bugs.archlinux.org/task/44731)), but a work-around is quite trivial. Just create a file for your interface (e.g. wlp3s0) in /etc/netctl/interfaces with the following content and make it executable:

 `/etc/netctl/interfaces/wlp3s0` 

```
WPAOptions="-m ''"

```

After that, try to restart your netctl-auto service and WiFi auto detection should work well again.

### netctl-auto does not automatically unblock a wireless card to use an interface

Many laptops have a hardware button (or switch) to turn off wireless card, however, the card can also be blocked by the kernel. This can be handled by [rfkill](/index.php/Wireless_network_configuration#Rfkill_caveat "Wireless network configuration").

If you want _netctl-auto_ to automatically unblock your wireless card to connect to a particular network, set `RFKill=++auto++` option for the wireless connection of your choice, as specified in the [netctl.profile(5)](https://github.com/joukewitteveen/netctl/blob/master/docs/netctl.profile.5.txt) man page.

### RTNETLINK answers: File exists (with multiple NICs)

This is a very misleading response, it really means that you have assigned a default gateway in an earlier netctl control file. When netctl starts up the n-th NIC and goes to set its local route, it fails because there is already a default route from n-1.

Remove it and everything works, except you no longer have a default route and so cannot access things such as the internet. `ExecUpPost` does not work as it gets executed for each network card.

A possible solution is creating a new service:

 `/etc/system/system/defaultrouter.service` 

```
[Unit]
Description
Requires=netctl.service
After=netctl.service
Before=ntpd.service,dnsmasq.service

[Service]
Type=oneshot
ExecStart=/usr/bin/ip route add default via 192.168.xxx.yyy
```

## See also

*   [Initial mailing list announcement](https://lists.archlinux.org/pipermail/arch-projects/2012-December/003473.html)
*   [Official announcement thread](https://bbs.archlinux.org/viewtopic.php?id=157670)
*   [Official news announcement](https://www.archlinux.org/news/netctl-is-now-in-core/)
*   There is a cinnamon applet available in the AUR: [cinnamon-applet-netctl-systray-menu](https://aur.archlinux.org/packages/cinnamon-applet-netctl-systray-menu/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Netctl&oldid=418919](https://wiki.archlinux.org/index.php?title=Netctl&oldid=418919)"