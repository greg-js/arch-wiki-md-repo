Wireshark is a free and open-source packet analyzer. It is used for network troubleshooting, analysis, software and communications protocol development, and education. Originally named Ethereal, in May 2006 the project was renamed Wireshark due to trademark issues.

## Contents

*   [1 Installation](#Installation)
*   [2 Capturing as normal user](#Capturing_as_normal_user)
    *   [2.1 Add the user to the wireshark group](#Add_the_user_to_the_wireshark_group)
    *   [2.2 Use sudo](#Use_sudo)
*   [3 A few capturing techniques](#A_few_capturing_techniques)
    *   [3.1 Filtering TCP packets](#Filtering_TCP_packets)
    *   [3.2 Filtering UDP packets](#Filtering_UDP_packets)
    *   [3.3 Filter packets to a specific IP Address](#Filter_packets_to_a_specific_IP_Address)

## Installation

The wireshark package has been split into the CLI version as well as GTK and Qt frontends, which depend on the CLI.

*   CLI version - [Install](/index.php/Pacman "Pacman") package [wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli).
*   GTK frontend - [Install](/index.php/Pacman "Pacman") package [wireshark-gtk](https://www.archlinux.org/packages/?name=wireshark-gtk).
*   Qt frontend - [Install](/index.php/Pacman "Pacman") package [wireshark-qt](https://www.archlinux.org/packages/?name=wireshark-qt).

## Capturing as normal user

Running Wireshark as root is insecure.

Arch Linux uses [method from Wireshark wiki](http://wiki.wireshark.org/CaptureSetup/CapturePrivileges#Other_Linux_based_systems_or_other_installation_methods) to separate privileges. When [wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli) is installed, [install script](/index.php/PKGBUILD#install "PKGBUILD") sets `/usr/bin/dumpcap` capabilities.

 `$ getcap /usr/bin/dumpcap`  `/usr/bin/dumpcap = cap_net_admin,cap_net_raw+eip` 

`/usr/bin/dumpcap` is the only process that has privileges to capture packets. `/usr/bin/dumpcap` can only be run by root and members of the `wireshark` group.

There are two methods to capture as a normal user :

### Add the user to the wireshark group

To use wireshark as a normal user, add user to the `wireshark` [group](/index.php/Group "Group").

### Use sudo

You can use [sudo](/index.php/Sudo "Sudo") to temporarily change group to `wireshark`. The following line allows all users in the wheel group to run programs with GID set to wireshark GID:

 `%wheel ALL=(:wireshark) /usr/bin/wireshark, /usr/bin/tshark` 

Then run wireshark with

 `$ sudo -g wireshark wireshark` 

## A few capturing techniques

There are a number of different ways to capture exactly what you are looking for in Wireshark, by applying filters.

**Note:** To learn the filter syntax, see man pcap-filter(7).

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

*   If you would like to see all the traffic going to a specific address, enter `ip.dst == 1.2.3.4`, replacing `1.2.3.4` with the IP address the outgoing traffic is being sent to.

*   If you would like to see all the incoming traffic for a specific address, enter `ip.src == 1.2.3.4`, replacing `1.2.3.4` with the IP address the incoming traffic is being sent to.

*   If you would like to see all the incoming and outgoing traffic for a specific address, enter `ip.addr == 1.2.3.4`, replacing `1.2.3.4` with the relevant IP address.