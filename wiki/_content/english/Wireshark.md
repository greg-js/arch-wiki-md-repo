Wireshark is a free and open-source packet analyzer. It is used for network troubleshooting, analysis, software and communications protocol development, and education. Originally named Ethereal, in May 2006 the project was renamed Wireshark due to trademark issues.

## Contents

*   [1 Installation](#Installation)
*   [2 Capturing as normal user](#Capturing_as_normal_user)
*   [3 A few capturing techniques](#A_few_capturing_techniques)
    *   [3.1 Filtering TCP packets](#Filtering_TCP_packets)
    *   [3.2 Filtering UDP packets](#Filtering_UDP_packets)
    *   [3.3 Filter packets to a specific IP Address](#Filter_packets_to_a_specific_IP_Address)

## Installation

The wireshark package has been split into the CLI version as well as GTK+ and Qt frontends, which depend on the CLI.

**Warning:** The Qt frontend, along with missing some features, is also not as stable as the GTK+ frontend. If you have issues with listing network interfaces, enabling monitor mode, and/or permissions, even after setting everything up correctly, try using the GTK version and see if your issues persist.

*   CLI version (tshark) - [Install](/index.php/Pacman "Pacman") package [wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli).
*   GTK+ frontend (wireshark-gtk) - [Install](/index.php/Pacman "Pacman") package [wireshark-gtk](https://www.archlinux.org/packages/?name=wireshark-gtk) (deprecated).
*   Qt frontend (wireshark) - [Install](/index.php/Pacman "Pacman") package [wireshark-qt](https://www.archlinux.org/packages/?name=wireshark-qt) (recommended).

## Capturing as normal user

Running Wireshark as root is insecure.

Arch Linux uses [method from Wireshark wiki](https://wiki.wireshark.org/CaptureSetup/CapturePrivileges#Other_Linux_based_systems_or_other_installation_methods) to separate privileges. When [wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli) is installed, [install script](/index.php/PKGBUILD#install "PKGBUILD") sets additional [capabilities](/index.php/Capabilities "Capabilities") on the `/usr/bin/dumpcap` executable, these capabilities can be listed as follows:

 `$ getcap /usr/bin/dumpcap`  `/usr/bin/dumpcap = cap_dac_override,cap_net_admin,cap_net_raw+eip` 

`/usr/bin/dumpcap` is the only process that has privileges to capture packets. `/usr/bin/dumpcap` can only be run by root and members of the `wireshark` group. Other users will see the *Couldn't run /usr/bin/dumpcap in child process: Permission denied* error in Wireshark.

To use wireshark as a normal user, add the user to the `wireshark` [group](/index.php/Group "Group") (`sudo gpasswd -a $USER wireshark`). Re-login to apply the changes or use `newgrp wireshark` to open a shell with the new group and start Wireshark from there.

## A few capturing techniques

There are a number of different ways to capture exactly what you are looking for in Wireshark, by applying [capture filters](https://wiki.wireshark.org/CaptureFilters) or [display filters](https://wiki.wireshark.org/DisplayFilters).

**Note:** To learn the capture filter syntax, see man pcap-filter(7). For display filters, see man wireshark-filter(4).

### Filtering TCP packets

If you want to see all the current TCP packets, type `tcp` into the "Filter" bar or in the CLI, enter:

```
$ tshark -f "tcp"

```

### Filtering UDP packets

If you want to see all the current UDP packets, type `udp` into the "Filter" bar or in the CLI, enter:

```
$ tshark -f "udp"

```

### Filter packets to a specific IP Address

*   If you would like to see all the traffic going to a specific address, enter display filter `ip.dst == 1.2.3.4`, replacing `1.2.3.4` with the IP address the outgoing traffic is being sent to.

*   If you would like to see all the incoming traffic for a specific address, enter display filter `ip.src == 1.2.3.4`, replacing `1.2.3.4` with the IP address the incoming traffic is being sent to.

*   If you would like to see all the incoming and outgoing traffic for a specific address, enter display filter `ip.addr == 1.2.3.4`, replacing `1.2.3.4` with the relevant IP address.