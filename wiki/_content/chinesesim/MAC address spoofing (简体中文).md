This article gives several methods to spoof a Media Access Control (MAC) address.

**Note:** In the examples below is assumed the ethernet device is `eth0`. Use `ip link` to check your actual device name, and adjust the examples as necessary

## Contents

*   [1 Manually](#Manually)
    *   [1.1 Method 1: iproute2](#Method_1:_iproute2)
    *   [1.2 Method 2: macchanger](#Method_2:_macchanger)
*   [2 Automatically](#Automatically)
    *   [2.1 netcfg](#netcfg)
    *   [2.2 Systemd Unit](#Systemd_Unit)
*   [3 See also](#See_also)

## Manually

There are two methods for spoofing a MAC address using either [iproute2](https://www.archlinux.org/packages/?name=iproute2) (installed by default) or [macchanger](https://www.archlinux.org/packages/?name=macchanger) (available on the [Official repositories](/index.php/Official_repositories "Official repositories")).

Both of them are outlined below.

### Method 1: iproute2

First, you can check your current MAC address with the command:

 `# ip link show eth0` 

The section that interests us at the moment is the one that has "link/ether" followed by a 6-byte number. It will probably look something like this:

 `link/ether 00:1d:98:5a:d1:3a` 

The first step to spoofing the MAC address is to bring the network interface down. You must be logged in as root to do this. It can be accomplished with the command:

 `# ip link set dev eth0 down` 

Next, we actually spoof our MAC. Any hexadecimal value will do, but some networks may be configured to refuse to assign IP addresses to a client whose MAC does not match up with a vendor. Therefore, unless you control the network(s) you are connecting to, it is a good idea to test this out with a known good MAC rather than randomizing it right away.

To change the MAC, we need to run the command:

 `# ip link set dev eth0 address XX:XX:XX:XX:XX:XX` 

Where any 6-byte value will suffice for 'XX:XX:XX:XX:XX:XX'.

The final step is to bring the network interface back up. This can be accomplished by running the command:

 `# ip link set dev eth0 up` 

If you want to verify that your MAC has been spoofed, simply run `ip link show eth0` again and check the value for 'link/ether'. If it worked, 'link/ether' should be whatever address you decided to change it to.

### Method 2: macchanger

Another method uses [macchanger](https://www.archlinux.org/packages/?name=macchanger) (a.k.a., the GNU MAC Changer). It provides a variety of features such as changing the address to match a certain vendor or completely randomizing it.

[Install](/index.php/Pacman "Pacman") the package [macchanger](https://www.archlinux.org/packages/?name=macchanger) from the [Official repositories](/index.php/Official_repositories "Official repositories").

After this, the MAC can be spoofed with a random address. The syntax is `macchanger -r *<device>*`.

Here is an example command for spoofing the MAC address of a device named eth0.

 `# macchanger -r eth0` 

To randomize all of the address except for the vendor bytes (that is, so that if the MAC address was checked it would still register as being from the same vendor), you would run the command:

 `# macchanger -e eth0` 

Finally, to change the MAC address to a specific value, you would run:

 `# macchanger --mac=XX:XX:XX:XX:XX:XX` 

Where `XX:XX:XX:XX:XX:XX` is the MAC you wish to change to.

**Note:** A device cannot be in use (connected in any way or with its interface up) while the MAC address is being changed.

## Automatically

### netcfg

[Install](/index.php/Pacman "Pacman") the package [macchanger](https://www.archlinux.org/packages/?name=macchanger) from the [Official repositories](/index.php/Official_repositories "Official repositories"). Read the [#Method 2: macchanger](#Method_2:_macchanger) method for more information.

Put the following line in your [netcfg](/index.php/Netcfg "Netcfg") profile to have it spoof your MAC address when it's started:

 `PRE_UP='macchanger -e wlan0'` 

You may have to replace `wlan0` with your interface name.

### Systemd Unit

 `/etc/systemd/system/macspoof@.service` 
```
[Unit]
Description=MAC address change %I
Before=dhcpcd@%i.service

[Service]
Type=oneshot
ExecStart=/usr/sbin/ip link set dev %i address 36:aa:88:c8:75:3a
ExecStart=/usr/sbin/ip link set dev %i up

[Install]
WantedBy=network.target
```

You may have to edit this file if you do not use dhcpcd. Note: This works without netcfg. If you are using netcfg, see above.

## See also

*   [macchanger project page](http://www.alobbs.com/macchanger)
*   [Article on DebianAdmin](http://www.debianadmin.com/change-your-network-card-mac-media-access-control-address.html) with more macchanger options.
*   [SMAC](http://wiki.gotux.net/downloads/smac) Arch Linux MAC Address Spoofer