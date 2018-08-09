[Wireshark](https://www.wireshark.org/) is a free and open-source packet analyzer. It is used for network troubleshooting, analysis, software and communications protocol development, and education.

## Contents

*   [1 Installation](#Installation)
*   [2 Capturing as normal user](#Capturing_as_normal_user)
*   [3 A few capturing techniques](#A_few_capturing_techniques)
    *   [3.1 Filtering TCP packets](#Filtering_TCP_packets)
    *   [3.2 Filtering UDP packets](#Filtering_UDP_packets)
    *   [3.3 Filter packets to a specific IP Address](#Filter_packets_to_a_specific_IP_Address)

## Installation

[Install](/index.php/Install "Install") the [wireshark-qt](https://www.archlinux.org/packages/?name=wireshark-qt) package for the Wireshark GUI or [wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli) for just the `tshark` CLI.

For the deprecated GTK+ interface, install the [wireshark-gtk](https://www.archlinux.org/packages/?name=wireshark-gtk) package. Note that this package will be removed in the future (Wireshark 3.0).

## Capturing as normal user

Do not run Wireshark as root, it is insecure. Wireshark has implemented privilege separation. [[1]](https://wiki.wireshark.org/CaptureSetup/CapturePrivileges#Most_UNIXes)

The [wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli) [install script](/index.php/PKGBUILD#install "PKGBUILD") sets packet capturing [capabilities](/index.php/Capabilities "Capabilities") on the `/usr/bin/dumpcap` executable.

`/usr/bin/dumpcap` can only be executed by root and members of the `wireshark` group.

Therefore to use Wireshark as a normal user you just have to add your user to the `wireshark` [group](/index.php/Group "Group"):

```
# gpasswd -a *username* wireshark

```

Re-login to apply the change.

## A few capturing techniques

There are a number of different ways to capture exactly what you are looking for in Wireshark, by applying [capture filters](https://wiki.wireshark.org/CaptureFilters) or [display filters](https://wiki.wireshark.org/DisplayFilters).

**Note:** To learn the capture filter syntax, see [pcap-filter(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pcap-filter.7). For display filters, see [wireshark-filter(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wireshark-filter.4).

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