From the [WireGuard](https://www.wireguard.io/) project homepage:

	Wireguard is an extremely simple yet fast and modern VPN that utilizes state-of-the-art cryptography. It aims to be faster, simpler, leaner, and more useful than IPSec, while avoiding the massive headache. It intends to be considerably more performant than OpenVPN. WireGuard is designed as a general purpose VPN for running on embedded interfaces and super computers alike, fit for many different circumstances. Initially released for the Linux kernel, it plans to be cross-platform and widely deployable. It is currently under heavy development, but already it might be regarded as the most secure, easiest to use, and simplest VPN solution in the industry.

## Installation

Install the [wireguard-dkms](https://www.archlinux.org/packages/?name=wireguard-dkms) and [wireguard-tools](https://www.archlinux.org/packages/?name=wireguard-tools) packages.

## Troubleshooting

### DKMS module not available

If the following command does not list any module after you installed [wireguard-dkms](https://www.archlinux.org/packages/?name=wireguard-dkms),

```
$ modprobe wireguard && lsmod | grep wireguard

```

or if creating a new link returns

```
# ip link add dev wg0 type wireguard
RTNETLINK answers: Operation not supported

```

you probably miss the linux headers.

These headers are available in [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) or [linux-lts-headers](https://www.archlinux.org/packages/?name=linux-lts-headers) depending of the kernel installed on your system.