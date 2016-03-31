From [Wikipedia:Virtual private server](https://en.wikipedia.org/wiki/Virtual_private_server "wikipedia:Virtual private server"):

	*Virtual private server (VPS) is a term used by Internet hosting services to refer to a virtual machine. The term is used for emphasizing that the virtual machine, although running in software on the same physical computer as other customers' virtual machines, is in many respects functionally equivalent to a separate physical computer, is dedicated to the individual customer's needs, has the privacy of a separate physical computer, and can be configured to run server software.*

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
| [A MilesWeb VPS](http://www.milesweb.com/vps-hosting.php) | 2013.10.14 | OpenVZ | Europe, India, US | Latest Arch Linux available on OpenVZ platform. Quick setup, 24/7 support via Live Chat, Email and Phone. VPS starts from $20 / mo |
| [123 Systems](http://123systems.net) | 2010.05.xx | OpenVZ | Dallas, US-TX | Arch available as a selection upon reinstall. Very old (2.6.18-308) kernel - See [OpenVZ troubleshooting](#OpenVZ:_kernel_too_old_for_glibc). Limited information available before purchase. Cannot verify Arch Linux version without purchase. |
| [4smart.cz](http://www.4smart.cz) | 2013.08 (x86_64) | OpenVZ | Europe, Prague | when updating system make sure you use [tredaelli-systemd] in pacman.conf (see [Unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories") |
| [AUSWEB](http://ausweb.com.au) | Latest Only (clarify?) | VMware ESXi | Sydney, AU | Latest ISO (clarify?) of Arch Available. Enterprise Service. |
| [affinity.net.nz](https://www.affinity.net.nz) | 2013.08.01 | KVM | Auckland, New Zealand (NZ) | IRC channel is #affinity on ircs.kiwicon.org |
| [Atlantic.Net](http://www.atlantic.net/) | 2015.05.01 | KVM | NYC/SF/Toronto/Dallas/Orlando, US & Canada | 100% SSD 1-click ArchLinux from $5/mo for 512M/20GB SSD, ready in 30 seconds |
| [BuyVM](http://www.buyvm.net/) | 2013.07.01 | KVM | LA, Buffalo NY | Must chose a different OS at sign up. Once accessible, choose to mount the latest Arch ISO and reboot to install manually. |
| [Coinshost](https://coinshost.com/en/vps) | 2015.04 | Xen | Zurich, Switzerland | $3/mo for 512M/20GB. Bitcoin and other cryptocurrencies accepted. |
| [DirectVPS](https://www.directvps.nl/) | 2014.01.xx | OpenVZ | Amsterdam, NL; Rotterdam, NL | Dutch language site. Version verifyable by clicking through [https://www.directvps.nl/try-1.plp?p=31](https://www.directvps.nl/try-1.plp?p=31) |
| [Edis](http://en.edis.at/) | [2013.03.01](http://www.edis.at/en/support-and-service/faq/server-faq/which-distributions-are-available-with-edis-kvm-vps-plans/) | vServer, KVM, OpenVZ | [Multiple international locations](http://www.edis.at/en/server/kvm-vps/austria/). | Also offer dedicated server options as well as an "off-shore" location at the Isle of Man (IM). |
| [Gandi](https://www.gandi.net/hosting/) | 2013.10.27 | Xen | Paris, FR; Baltimore, MD, US; Bissen, LU | Very granular scaling of system resources (e.g. RAM, disk space); IPv6-only option available; you can supply your own install image, version based on keyring package version |
| [GigaTux](https://www.gigatux.com/virtual.php) | [2013.06.01](https://www.gigatux.com/distro/) | Xen | Chicago, US-IL; Frankfurt, DE; London, GB; San Jose, US-CA |
| [Host Virtual](http://www.vr.org/) | [2011.08.19](http://www.vr.org/os/linux-vps/archlinux-vps) | KVM | [Multiple International Locations](http://www.vr.org/cloud-locations/) | Appears to use KVM virtualization. Site lists "Xen based virtualization" and [features](http://www.vr.org/features/) lists ability to install from ISO. |
| [Hostigation](https://hostigation.com/) | [2010.05 i686](https://hostigation.com/wiki/index.php?title=KVM:Install) | OpenVZ, KVM | Charlotte, US-NC; Los Angeles, US-CA | You can [migrate to x86_64](/index.php/Migrating_Between_Architectures_Without_Reinstalling "Migrating Between Architectures Without Reinstalling"). |
| [IntoVPS](http://www.intovps.com) | 2012.09.xx | OpenVZ | Amsterdam, NL; Bucharest, RO; Dallas, US-TX; Fremont, US-CA; London, GB | Blog has not been updated since September, 2012 which included the Arch Linux update. |
| [Kloud51](https://www.kloud51.com) | 2014.7.7 | OpenVZ | US-CA, Canada | SSD, 2 images available: A bare-bones system or a pre-configured Desktop with OpenBox, XRDP, Firefox, SSH Brute Force, Geany, and Yaourt. |
| [Leapswitch Networks](https://leapswitch.com) | [2013.10.xx] | OpenVZ/KVM | USA, India, Portugal, Spain, Ukraine, Germany | ArchLinux currently available in Control Panel for reinstall, not on order form. |
| [Linode.com](https://www.linode.com) | [2015.02.xx](https://www.linode.com/faq.cfm) | Xen, KVM | [Tokyo, JP; Multiple US; London, GB](https://www.linode.com/speedtest/) | To run a custom kernel, install [linux-linode](https://aur.archlinux.org/packages/linux-linode/). ([linux](https://www.archlinux.org/packages/?name=linux) will break on a 32-bit Linode.) |
| [LYLIX](http://lylix.net/) | [2014.01.xx](http://lylix.net/archlinux) | OpenVZ | Multiple US; Europe | 32-bit and 64-bit available |
| [Node Deploy](http://www.nodedeploy.com) | 2014.10.01 | OpenVZ, KVM | Germany (DE); Los Angeles, US-CA; Atlanta, US-GA; Phoenix, US-AZ | "At NodeDeploy we support virtually every linux distribution." Arch Linux is listed under their Operating Systems. No version information. |
| [Netcup](http://netcup.de) | 2012.11.xx | KVM | Germany (DE) | German language site. |
| [OnePoundWebHosting](http://onepoundwebhosting.co.uk) | 2013.05.xx | Xen PV, Xen HVM | United Kingdom (UK) | They are a registrar too. Unable to verify server locations. |
| [OVH](https://www.ovh.com/us/vps/) | Latest | KVM | France, Canada | $3.5 for 2GB RAM and 10GB SSD, $7 for 4GB RAM and 20GB SSD. |
| [proPlay.de](https://www.proplay.biz/) | 2012.12.xx | OpenVZ, KVM | Germany (DE) | German language site. |
| [QuickVZ](https://www.quickvz.com) | 2013.10 | OpenVZ, Xen | Amsterdam, Netherlands (NL); Stockholm, Sweden (SE) | Provide hardened Arch Linux images along with Enterprise services (e,g. VPN, Virtual Private LAN Service (VPLS) and Virtual Routers. |
| [Rackspace Cloud](http://www.rackspace.com/cloud/cloud_hosting_products/servers/) | 2013.6 | Xen | [Multiple international locations](https://www.rackspace.com/whyrackspace/network/datacenters/) | Billed per hour. Use their "next gen" VPSes (using the mycloud.rackspace.com panel); the Arch image on the first gen Rackspace VPSes is out of date. |
| [RamHost.us](http://www.ramhost.us) | [2013.05.01](http://www.ramhost.us/?page=news) | OpenVZ, KVM | Los Angeles, US-CA; Great Britain (GB); Atlanta, US-GA; Germany (DE) | You can request a newer ISO on RamHost's IRC network. |
| [RamNode](http://www.ramnode.com) | [2016.01.01](https://clientarea.ramnode.com/knowledgebase.php?action=displayarticle&id=48) | [SSD and SSD Cached:](https://clientarea.ramnode.com/knowledgebase.php?action=displayarticle&id=39) [KVM](https://clientarea.ramnode.com/knowledgebase.php?action=displayarticle&id=52) | [Alblasserdam, NL; Atlanta, GA-US; Los Angeles, CA-US; New York, NY-US; Seattle, WA-US](https://clientarea.ramnode.com/knowledgebase.php?action=displayarticle&id=50) | You can request Host/CPU passthrough with KVM service.[[3]](https://clientarea.ramnode.com/knowledgebase.php?action=displayarticle&id=66) Frequent use of discount promotions.[[4]](https://twitter.com/search?q=ramnode%20code&src=typd), Must install Arch manually from an ISO using VNC viewer. |
| [Tilaa](http://www.tilaa.nl/) | 2014.10.01 | [KVM](https://www.tilaa.com/pages/vps/technology) | Amsterdam, NL | English or Dutch language site. |
| [TransIP](https://www.transip.eu/) | [2016.02.01](https://www.transip.eu/vps/vps-os/) | [KVM](https://www.transip.eu/vps/vps-technology/) | Amsterdam, NL | English language site. Registrar. |
| [XenVZ](http://www.xenvz.co.uk/) | 2009.12.07 | OpenVZ, Xen | United Kingdom (UK), United States (US) | [Hardware](http://www.xenvz.co.uk/faq.php#use2) |
| [Virpus](http://www.virpus.com/) | [2014.11.07](http://virpus.com/linux-vps.php) | Xen | Kansas City, US-KS; Los Angeles, US-CA | A subcompany of Wow Technologies, Inc. 24/7 support via Live Chat, Email, Phone, and Ticket System. Service starts at $5/month. |
| [Virtual Master](http://www.virtualmaster.com/) | 2012-08 |  ?? | Europe, Prague |
| [Vmline](http://www.vmline.pl/) | 2013.09.01 | KVM, OpenVZ | Kraków, PL | [S-Net](http://www.s-net.pl/en/) reseller. Full virtualization. Polish language site. |
| [VPSBG.eu](https://vpsbg.eu/) | 2013.10 | OpenVZ | [Sofia, Bulgaria](https://vpsbg.eu/en/index.php?page=vps-datacenter) | Offshore VPS in Bulgaria - anonymous registrations and Bitcoin are accepted. |
| [VPS6.NET](https://vps6.net/) | 2013.01.xx  | OpenVZ, Xen, HVM-ISO | [Multiple US](http://vps6.net/network/); Frankfurt, DE; Bucharest, RO; Istanbul, TR | Registrar. |
| [VPS.NET](http://www.vps.net/) | 2014.01.xx  | OpenVZ, Xen, HVM-ISO | [US, Canada, UK, Brazil, Netherlands, France, Germany, Japan, Singapore, India, Austrlia](http://vps.net/cloud-datacenter-locations); Multiple | Managed & Un managed VPS service provider, multiple OS and configurations.. |
| [World4You](http://www.world4you.com/) | 2015.10.28 | OpenVZ | Austria (AT) | Internet hosting provider; quick setup; 24/7 support; shared web hosting; also CentOS, Debian, Ubuntu, Fedora and Arch OpenVZ servers; supports newest systemd (227 atm) |

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

*   `-C custom-pacman-config.conf` - Use a custom pacman configuration file. By default, pacstrap builds according to your local pacman.conf. This determines the architecture (i686 or x86_64) of the build, the mirror list, etc.
*   `-B` - Prevent pacstrap from copying your system's pacman keyring to the new build. If you use this option, you will need to run `pacman-key --init` and `pacman-key --populate archlinux` in the [Configuration](#Configuration) step to set up the keyring.
*   `-M` - Prevent pacstrap from copying your system's pacman mirror list to the new build.

##### Replacing everything on the VPS with the Arch build

Replace all files, directories, etc. on your target VPS with the contents of your `build` directory (replacing "YOUR.VPS.IP.ADDRESS" below):

**Warning:** Be careful with the following command. By design, `rsync` is very destructive, especially with any of the `--delete` options.

```
# rsync -axH --delete-delay -e ssh --stats -P build/ YOUR.VPS.IP.ADDRESS:/

```

Explanation of options:

At minimum, only the `-a` (preserve timestamps, permissions, etc.), `-x` (do not cross filesystem boundaries), and `--delete` (delete anything in the target that does not exist in the source) options are required. The `--delete-delay` option is an alternate deletion mode which waits to delete anything until the synchronization is otherwise complete; this is not necessary but may reduce the risk of a slow transfer causing the target VPS to lock-up. The `-H` causes hardlinks to be preserved. The `-e ssh` (use rsync over SSH) option is recommended and makes things simple. The `--stats` and `-P` options are just to show more information.

##### Configuration

1.  Reboot the VPS externally (using your provider's control panel, for example).
2.  Using OpenVZ's serial console feature, configure the [network](/index.php/Network "Network") and [basic system settings](/index.php/Installation_guide#Configure_the_system "Installation guide") (ignoring fstab generation and arch-chroot steps).
    *   If you do not have access to the serial console feature, you will need to preconfigure your network settings before synchronizing Arch to the VPS.

### Xen

See [Xen#Arch as Xen guest (PVHVM mode)](/index.php/Xen#Arch_as_Xen_guest_.28PVHVM_mode.29 "Xen") and/or [Xen#Arch as Xen guest (PV mode)](/index.php/Xen#Arch_as_Xen_guest_.28PV_mode.29 "Xen").