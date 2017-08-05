From [Wikipedia:Virtual private server](https://en.wikipedia.org/wiki/Virtual_private_server "wikipedia:Virtual private server"):

	Virtual private server (VPS) is a term used by Internet hosting services to refer to a virtual machine. The term is used for emphasizing that the virtual machine, although running in software on the same physical computer as other customers' virtual machines, is in many respects functionally equivalent to a separate physical computer, is dedicated to the individual customer's needs, has the privacy of a separate physical computer, and can be configured to run server software.

This article discusses the use of Arch Linux on Virtual Private Servers, and includes some fixes and installation instructions specific to VPSes.

**Warning:**

*   Linux 2.6.32 is not supported by systemd since version 205 (and will not work with systemd-212 or higher). Since many container-based virtualization environments rely on older kernels, it may be impossible to keep an Arch Linux install up-to-date in such an environment. However, OpenVZ, as of [kernel build 042stab094.7](http://openvz.org/Download/kernel/rhel6/042stab094.7), has backported the CLOCK_BOOTTIME feature, making it work with later versions of systemd.
*   Systemd since version 220 doesn't work on OpenVZ containers. [[1]](https://github.com/systemd/systemd/issues/421) This issue has been fixed in OpenVZ kernel 042stab111.1 [[2]](https://bugzilla.openvz.org/show_bug.cgi?id=3280#c11)

## Contents

*   [1 Providers that offer Arch Linux](#Providers_that_offer_Arch_Linux)
*   [2 Installation](#Installation)
    *   [2.1 KVM](#KVM)
    *   [2.2 OpenVZ](#OpenVZ)
        *   [2.2.1 Installing the latest Arch Linux on any OpenVZ provider](#Installing_the_latest_Arch_Linux_on_any_OpenVZ_provider)
            *   [2.2.1.1 Prerequisites](#Prerequisites)
            *   [2.2.1.2 Building a clean Arch Linux installation](#Building_a_clean_Arch_Linux_installation)
            *   [2.2.1.3 Replacing everything on the VPS with the Arch build](#Replacing_everything_on_the_VPS_with_the_Arch_build)
            *   [2.2.1.4 Configuration](#Configuration)
    *   [2.3 Xen](#Xen)

## Providers that offer Arch Linux

**Warning:** We cannot vouch for the honesty or quality of any provider. Please conduct due diligence before ordering.

**Note:** This list is for providers with a convenient Arch Linux template. Using Arch on other providers is possible but requires more work. Example methods include:

*   Loading custom disc images (requires hardware virtualization such as in Xen or KVM),
*   [Installing under chroot](/index.php/Installation_guide "Installation guide"), for example with the help of the [vps2arch](https://github.com/drizzt/vps2arch) script (it will download the latest iso; be particularly aware of the systemd 220/221 [bug](https://github.com/systemd/systemd/issues/421)), or
*   Following [#Installing the latest Arch Linux on any OpenVZ provider](#Installing_the_latest_Arch_Linux_on_any_OpenVZ_provider) instructions, using rsync to synchronize Arch over the top of another distribution.

| Provider | Arch Release | Virtualization | Locations | Notes |
| [4smart.cz](http://4smart.cz/) | 2013.08 | OpenVZ | Prague, CZ | (Czech language site only) when updating system make sure you use [tredaelli-systemd] in pacman.conf (see [Unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories") |
| [affinity.net.nz](https://www.affinity.net.nz/) | 2013.08.01 | KVM | Auckland, New Zealand (NZ) | IRC channel is #affinity on ircs.kiwicon.org |
| [Atlantic.Net](https://www.atlantic.net/) | 2015.05.01 | KVM | NYC/SF/Toronto/Dallas/Orlando, US & Canada | 100% SSD 1-click Arch Linux, ready in 30 seconds |
| [BuyVM](https://buyvm.net/) | 2013.07.01 | KVM | LA, Buffalo NY | Must chose a different OS at sign up. Once accessible, choose to mount the latest Arch ISO and reboot to install manually. |
| [Coinshost](https://coinshost.com/en/vps) | 2015.04 | Xen | Zurich, Switzerland | Bitcoin and other cryptocurrencies accepted. |
| [Cherry Host](https://cherry.host) | Latest | KVM | Santee, US-CA | Must submit a support ticket to get Arch installed. |
| [DirectVPS](https://www.directvps.nl/) | 2014.01.xx | OpenVZ | Amsterdam, NL; Rotterdam, NL | (Dutch language site only) |
| [Edis](http://www.edis.at/en/) | [2013.03.01](http://www.edis.at/en/support-and-service/faq/server-faq/which-distributions-are-available-with-edis-kvm-vps-plans/) | vServer, KVM, OpenVZ | [Multiple international locations](http://www.edis.at/en/server/kvm-vps/austria/). | Also offer dedicated server options as well as an "off-shore" location at the Isle of Man (IM). |
| [GigaTux](https://www.gigatux.com/virtual.php) | [2013.06.01](https://www.gigatux.com/distro/) | Xen | Chicago, US-IL; Frankfurt, DE; London, GB; San Jose, US-CA |
| [Host Virtual](https://www.hostvirtual.com/) | [2014.06.01](https://www.hostvirtual.com/os/linux-vps/archlinux-vps) | KVM | [Multiple International Locations](http://www.vr.org/cloud-locations/) | Appears to use KVM virtualization. Site lists "Xen based virtualization" and [features](http://www.vr.org/features/) lists ability to install from ISO. |
| [Hostigation](https://hostigation.com/) | [Latest](https://hostigation.com/?page=KVM) | OpenVZ, KVM | Charlotte, US-NC; Los Angeles, US-CA |
| [Kloud51](https://www.kloud51.com) | Latest | OpenVZ | US-CA, Canada | SSD, 2 images available: A bare-bones system or a pre-configured Desktop with OpenBox, XRDP, Firefox, Fail2ban, Geany, and Yaourt. |
| [Leapswitch Networks](https://leapswitch.com) | 2013.10.xx | OpenVZ/KVM | USA, India, Portugal, Spain, Ukraine, Germany | Arch Linux currently available in Control Panel for reinstall, not on order form. |
| [Linevast.de](https://linevast.de) | Latest | OpenVZ, KVM | Germany | Arch Linux is possible on openvz and on KVM with the one click os installer. |
| [Linode.com](https://www.linode.com) | [2016.06.01](https://blog.linode.com/2016/06/13/arch-linux-network-configuration-update/) | Xen, KVM | [Tokyo, JP; Multiple US; London, GB](https://www.linode.com/speedtest/) | To run a custom kernel, install [linux-linode](https://aur.archlinux.org/packages/linux-linode/) ([linux](https://www.archlinux.org/packages/?name=linux) will break on a 32-bit Linode). When shipped, the NIC enp4s0 is renamed to eth0 and reverts back to enp4s0 on reboot --- on reboot, this may cause sshd load to fail. |
| [LYLIX](http://lylix.net/) | [2014.01.xx](http://lylix.net/archlinux) | OpenVZ | Multiple US; Europe | 32-bit and 64-bit available |
| [Netcup](https://www.netcup.de/) | 2012.11.xx | KVM | Germany (DE) | (German language site only) |
| [OnePoundWebHosting](https://www.onepoundwebhosting.co.uk/) | 2014.01 | Xen PV, Xen HVM | United Kingdom (UK) | They are a registrar too. Unable to verify server locations. |
| [OVH](https://www.ovh.com/us/vps/) | Latest | KVM | France, Canada |
| [PacmanVPS](https://pacmanvps.com/) | [Latest](https://panel.pacmanvps.com/machines/new) | KVM | Canada (CA), Poland (PL) | Support for any kernel. Ready to use template or install manually from ISO in VNC console. |
| [Proplay](https://www.proplay.de/) | Latest | OpenVZ, KVM | Germany (DE) | (German language site only) |
| [Rackspace Cloud](https://www.rackspace.com/cloud/servers) | 2013.6 | Xen | [Multiple international locations](https://www.rackspace.com/whyrackspace/network/datacenters/) | Billed per hour. Use their "next gen" VPSes (using the mycloud.rackspace.com panel); the Arch image on the first gen Rackspace VPSes is out of date. |
| [RamHost.us](http://www.ramhost.us/) | [2013.05.01](http://www.ramhost.us/?page=news) | OpenVZ, KVM | Los Angeles, US-CA; Great Britain (GB); Atlanta, US-GA; Germany (DE) | You can request a newer ISO on RamHost's IRC network. |
| [RamNode](http://www.ramnode.com/) | [2016.01.01](https://clientarea.ramnode.com/knowledgebase.php?action=displayarticle&id=48) | [SSD and SSD Cached:](https://clientarea.ramnode.com/knowledgebase.php?action=displayarticle&id=39) [KVM](https://clientarea.ramnode.com/knowledgebase.php?action=displayarticle&id=52) | [Alblasserdam, NL; Atlanta, GA-US; Los Angeles, CA-US; New York, NY-US; Seattle, WA-US](https://clientarea.ramnode.com/knowledgebase.php?action=displayarticle&id=50) | You can request Host/CPU passthrough with KVM service.[[3]](https://clientarea.ramnode.com/knowledgebase.php?action=displayarticle&id=66) Frequent use of discount promotions.[[4]](https://twitter.com/search?q=ramnode%20code&src=typd), Must install Arch manually from an ISO using VNC viewer. |
| [RoseHosting](https://www.rosehosting.com/) | Latest | OpenVZ, KVM | St. Louis, Missouri, USA | SSD powered hosting plans with free fully-managed 24/7 support |
| [SeedVPS](https://www.seedvps.com.com/) | Latest | OpenVZ, KVM | Amsterdam, Netherlands | Linux VPS and Windows VPS Hosting in The Netherlands (NL). Newer ISO can be requested by opening a support ticket. |
| [Tilaa](https://www.tilaa.com/) | 2016.03.01 | [KVM](https://www.tilaa.com/pages/vps/technology) | Amsterdam, NL |
| [TransIP](https://www.transip.eu/) | [2017.01.01](https://www.transip.eu/vps/vps-os/) | [KVM](https://www.transip.eu/vps/vps-technology/) | Amsterdam, NL | Also registrar. |
| [upCUBE](https://upcube.io) | Latest | Docker | Germany | Different prepared arch linux templates available |
| [Virpus](http://virpus.com/) | [2014.11.07](http://virpus.com/linux-vps.php) | Xen | Kansas City, US-KS; Los Angeles, US-CA | A subcompany of Wow Technologies, Inc. 24/7 support via Live Chat, Email, Phone, and Ticket System. |
| [Virtual Master](https://www.virtualmaster.com/) | 2012-08 |  ?? | Prague, CZ |
| [VPS6.NET](https://vps6.net/) | 2013.01.xx | OpenVZ, Xen, HVM-ISO | [Multiple US](http://vps6.net/network/); Frankfurt, DE; Bucharest, RO; Istanbul, TR | Registrar. |
| [VPSBG.eu](https://www.vpsbg.eu/) | 2013.10 | OpenVZ | [Sofia, Bulgaria](https://vpsbg.eu/en/index.php?page=vps-datacenter) | Offshore VPS in Bulgaria - anonymous registrations and Bitcoin are accepted. |
| [VPSSERVER](https://www.vpsserver.com/) | 2015.07 | KVM | Chicago, US-IL; Dallas, US-TX; Miami, US-FL; New York, US-NY; Silicon Valley, US-CA; Amsterdam, NL; Frankfurt, DE; London, UK |
| [World4You](https://www.world4you.com/) | 2015.10.28 | OpenVZ | Austria (AT) | Internet hosting provider; quick setup; 24/7 support; shared web hosting; also CentOS, Debian, Ubuntu, Fedora and Arch OpenVZ servers; supports newest systemd (227 atm) |
| [XenVZ](http://www.xenvz.co.uk/) | 2009.12.07 | OpenVZ, Xen | United Kingdom (UK), United States (US) | [Hardware](http://www.xenvz.co.uk/faq.php#use2) |
| [1984hosting.com](https://www.1984hosting.com/) | 2016.x | Xen | Iceland (IS) | [Hardware](https://www.1984hosting.com/product/vps/) will provide any image you request, has Arch in default image list. |

## Installation

### KVM

See [QEMU#Preparing an (Arch) Linux guest](/index.php/QEMU#Preparing_an_.28Arch.29_Linux_guest "QEMU").

### OpenVZ

#### Installing the latest Arch Linux on any OpenVZ provider

**Warning:** See the [above warning](#top) about older kernel builds and systemd.

It is possible to directly copy an installation of Arch Linux over the top of a working OpenVZ VPS. This tutorial explains how to create a basic installation of Arch Linux with `pacstrap` (as used in a standard install) and then replace the contents of a target VPS with it using [rsync](/index.php/Rsync "Rsync").

This process (with minor modification) also works to migrate existing Arch installations between various environments and has been confirmed to work in migrating from OpenVZ to Xen and from Xen to OpenVZ. For an install to Xen, other hardware-virtualized platforms, or probably even to physical hardware (unconfirmed), extra steps (basically running `mkinitcpio` and [installing a bootloader](/index.php/Boot_loaders "Boot loaders")) are needed.

##### Prerequisites

*   A working Arch Linux installation
    *   To keep things simple, it should match the architecture you want to install on your VPS (x86_64 or i686).
    *   To build from other distributions, [arch-bootstrap.sh](/index.php/Archbootstrap "Archbootstrap") can be used in place of `pacstrap`.
*   The [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts), [rsync](https://www.archlinux.org/packages/?name=rsync), and [openssh](https://www.archlinux.org/packages/?name=openssh) packages from the [official repositories](/index.php/Official_repositories "Official repositories")
    *   SSH is not strictly required, but rsync over SSH is the method used here.
*   A VPS running any distribution, with `rsync` and a working SSH server
    *   Its architecture (x86_64 or i686) does not matter as long as the OpenVZ installation can support your target architecture.
*   OpenVZ's serial console feature (usually accessible via your provider's control panel)
    *   Without this, any network configuration for the target VPS will have to be done immediately after the "Build" step below.

##### Building a clean Arch Linux installation

As root, build the installation (optionally replacing `build` with your preferred target directory):

```
# mkdir build
# pacstrap -cd build

```

Other tweaks for the `pacstrap` command:

*   `-C custom-pacman-config.conf` - Use a custom pacman configuration file. By default, `pacstrap` builds according to your local pacman.conf. This determines the architecture (i686 or x86_64) of the build, the mirror list, etc.
*   `-G` - Prevent `pacstrap` from copying your system's pacman keyring to the new build. If you use this option, you will need to run `pacman-key --init` and `pacman-key --populate archlinux` in the [Configuration](#Configuration) step to set up the keyring.
*   `-M` - Prevent `pacstrap` from copying your system's pacman mirror list to the new build.
*   You can pass a list of packages to `pacstrap` to add them to your install, instead of the default `base` group. For example: `pacstrap -cd build base openssh dnsutils gnu-netcat traceroute vim`

##### Replacing everything on the VPS with the Arch build

Replace all files, directories, etc. on your target VPS with the contents of your `build` directory (replacing "YOUR.VPS.IP.ADDRESS" below):

**Warning:** Be careful with the following command. By design, `rsync` is very destructive, especially with any of the `--delete` options.

```
# rsync -axH --delete-delay -e ssh --stats -P build/ YOUR.VPS.IP.ADDRESS:/

```

Explanation of options:

*   `-a` - Required. Preserves timestamps, permissions, etc.
*   `--delete` - Required. Deletes anything in the target that does not exist in the source
*   `-x` - Important. Prevents the crossing of filesystem boundaries (other partitions, /dev, etc.) during the copy
*   `-H` - Important. Preserves hardlinks
*   `--delete-delay` - Recommended. Enables alternate deletion mode which waits to delete anything until the synchronization is otherwise complete, which may reduce the risk of a slow transfer causing the target VPS to lock-up
*   `-e ssh` - Recommended. Uses `rsync` over SSH (recommended for simplicity compared to setting up an `rsync` server)
*   `-P` - Recommended. Shows partial progress information during transfer
*   `--stats` - Recommended. Shows transfer statistics at the end

##### Configuration

1.  Reboot the VPS externally (using your provider's control panel, for example).
2.  Using OpenVZ's serial console feature, configure the [network](/index.php/Network "Network") and [basic system settings](/index.php/Installation_guide#Configure_the_system "Installation guide") (ignoring fstab generation and arch-chroot steps).
    *   If you do not have access to the serial console feature, you will need to preconfigure your network settings before synchronizing Arch to the VPS.
    *   On some VPS configuration you won't have a gateway to connect to, here is an example [netctl](/index.php/Netctl "Netctl") configuration for this setup. It configures static IP addresses and default routes on venet0 and uses Google Public DNS.

 `/etc/netctl/venet` 
```
Description='VPS venet connection'
Interface=venet0
Connection=ethernet

IP=static
Address=('192.0.2.42/32')
Routes=('default')

IP6=static
Address6=('2001:db8::1234:5678/128')
Routes6=('default')

DNS=('2001:4860:4860::8888' '2001:4860:4860::8844' '8.8.8.8' '8.8.4.4')
```

### Xen

See [Xen](/index.php/Xen "Xen").