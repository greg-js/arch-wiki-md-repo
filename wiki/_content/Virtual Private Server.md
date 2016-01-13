# Virtual Private Server

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Server](/index.php/Server "Server")

From [Wikipedia:Virtual private server](https://en.wikipedia.org/wiki/Virtual_private_server "wikipedia:Virtual private server"):

_Virtual private server (VPS) is a term used by Internet hosting services to refer to a virtual machine. The term is used for emphasizing that the virtual machine, although running in software on the same physical computer as other customers' virtual machines, is in many respects functionally equivalent to a separate physical computer, is dedicated to the individual customer's needs, has the privacy of a separate physical computer, and can be configured to run server software._

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

<table class="wikitable">

<tbody>

<tr>

<th>Provider</th>

<th>Arch Release</th>

<th>Virtualization</th>

<th>Locations</th>

<th>Notes</th>

</tr>

<tr>

<td>[A MilesWeb VPS](http://www.milesweb.com/vps-hosting.php)</td>

<td>2013.10.14</td>

<td>OpenVZ</td>

<td>Europe, India, US</td>

<td>Latest Arch Linux available on OpenVZ platform. Quick setup, 24/7 support via Live Chat, Email and Phone. VPS starts from $20 / mo</td>

</tr>

<tr>

<td>[123 Systems](http://123systems.net)</td>

<td>2010.05.xx</td>

<td>OpenVZ</td>

<td>Dallas, US-TX</td>

<td>Arch available as a selection upon reinstall. Very old (2.6.18-308) kernel - See [OpenVZ troubleshooting](#OpenVZ:_kernel_too_old_for_glibc). Limited information available before purchase. Cannot verify Arch Linux version without purchase.</td>

</tr>

<tr>

<td>[4smart.cz](http://www.4smart.cz)</td>

<td>2013.08 (x86_64)</td>

<td>OpenVZ</td>

<td>Europe, Prague</td>

<td>when updating system make sure you use [tredaelli-systemd] in pacman.conf (see [Unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories")</td>

</tr>

<tr>

<td>[AUSWEB](http://ausweb.com.au)</td>

<td>Latest Only (clarify?)</td>

<td>VMware ESXi</td>

<td>Sydney, AU</td>

<td>Latest ISO (clarify?) of Arch Available. Enterprise Service.</td>

</tr>

<tr>

<td>[affinity.net.nz](https://www.affinity.net.nz)</td>

<td>2013.08.01</td>

<td>KVM</td>

<td>Auckland, New Zealand (NZ)</td>

<td>IRC channel is #affinity on ircs.kiwicon.org</td>

</tr>

<tr>

<td>[Atlantic.Net](http://www.atlantic.net/)</td>

<td>2015.05.01</td>

<td>KVM</td>

<td>NYC/SF/Toronto/Dallas/Orlando, US & Canada</td>

<td>100% SSD 1-click ArchLinux from $5/mo for 512M/20GB SSD, ready in 30 seconds</td>

</tr>

<tr>

<td>[BuyVM](http://www.buyvm.net/)</td>

<td>2013.07.01</td>

<td>KVM</td>

<td>LA, Buffalo NY</td>

<td>Must chose a different OS at sign up. Once accessible, choose to mount the latest Arch ISO and reboot to install manually.</td>

</tr>

<tr>

<td>[Coinshost](https://coinshost.com/en/vps)</td>

<td>2015.04</td>

<td>Xen</td>

<td>Zurich, Switzerland</td>

<td>$3/mo for 512M/20GB. Bitcoin and other cryptocurrencies accepted.</td>

</tr>

<tr>

<td>[DirectVPS](https://www.directvps.nl/)</td>

<td>2014.01.xx</td>

<td>OpenVZ</td>

<td>Amsterdam, NL; Rotterdam, NL</td>

<td>Dutch language site. Version verifyable by clicking through [https://www.directvps.nl/try-1.plp?p=31](https://www.directvps.nl/try-1.plp?p=31)</td>

</tr>

<tr>

<td>[Edis](http://en.edis.at/)</td>

<td>[2013.03.01](http://www.edis.at/en/support-and-service/faq/server-faq/which-distributions-are-available-with-edis-kvm-vps-plans/)</td>

<td>vServer, KVM, OpenVZ</td>

<td>[Multiple international locations](http://www.edis.at/en/server/kvm-vps/austria/).</td>

<td>Also offer dedicated server options as well as an "off-shore" location at the Isle of Man (IM).</td>

</tr>

<tr>

<td>[Gandi](https://www.gandi.net/hosting/)</td>

<td>2013.10.27</td>

<td>Xen</td>

<td>Paris, FR; Baltimore, MD, US; Bissen, LU</td>

<td>Very granular scaling of system resources (e.g. RAM, disk space); IPv6-only option available; you can supply your own install image, version based on keyring package version</td>

</tr>

<tr>

<td>[GigaTux](https://www.gigatux.com/virtual.php)</td>

<td>[2013.06.01](https://www.gigatux.com/distro/)</td>

<td>Xen</td>

<td>Chicago, US-IL; Frankfurt, DE; London, GB; San Jose, US-CA</td>

</tr>

<tr>

<td>[Host Virtual](http://www.vr.org/)</td>

<td>[2011.08.19](http://www.vr.org/os/linux-vps/archlinux-vps)</td>

<td>KVM</td>

<td>[Multiple International Locations](http://www.vr.org/cloud-locations/)</td>

<td>Appears to use KVM virtualization. Site lists "Xen based virtualization" and [features](http://www.vr.org/features/) lists ability to install from ISO.</td>

</tr>

<tr>

<td>[Hostigation](https://hostigation.com/)</td>

<td>[2010.05 i686](https://hostigation.com/wiki/index.php?title=KVM:Install)</td>

<td>OpenVZ, KVM</td>

<td>Charlotte, US-NC; Los Angeles, US-CA</td>

<td>You can [migrate to x86_64](/index.php/Migrating_Between_Architectures_Without_Reinstalling "Migrating Between Architectures Without Reinstalling").</td>

</tr>

<tr>

<td>[IntoVPS](http://www.intovps.com)</td>

<td>2012.09.xx</td>

<td>OpenVZ</td>

<td>Amsterdam, NL; Bucharest, RO; Dallas, US-TX; Fremont, US-CA; London, GB</td>

<td>Blog has not been updated since September, 2012 which included the Arch Linux update.</td>

</tr>

<tr>

<td>[Kloud51](https://www.kloud51.com)</td>

<td>2014.7.7</td>

<td>OpenVZ</td>

<td>US-CA, Canada</td>

<td>Choose from 2 images. A bare-bones system or a pre-configured Desktop with OpenBox, XRDP, Firefox, SSH Brute Force, Geany, and Yaourt.</td>

</tr>

<tr>

<td>[Leapswitch Networks](https://leapswitch.com)</td>

<td>[2013.10.xx]</td>

<td>OpenVZ/KVM</td>

<td>USA, India, Portugal, Spain, Ukraine, Germany</td>

<td>ArchLinux currently available in Control Panel for reinstall, not on order form.</td>

</tr>

<tr>

<td>[Linode.com](https://www.linode.com)</td>

<td>[2015.02.xx](https://www.linode.com/faq.cfm)</td>

<td>Xen, KVM</td>

<td>[Tokyo, JP; Multiple US; London, GB](https://www.linode.com/speedtest/)</td>

<td>To run a custom kernel, install [linux-linode](https://aur.archlinux.org/packages/linux-linode/)<sup><small>AUR</small></sup>. ([linux](https://www.archlinux.org/packages/?name=linux) will break on a 32-bit Linode.)</td>

</tr>

<tr>

<td>[LYLIX](http://lylix.net/)</td>

<td>[2014.01.xx](http://lylix.net/archlinux)</td>

<td>OpenVZ</td>

<td>Multiple US; Europe</td>

<td>32-bit and 64-bit available</td>

</tr>

<tr>

<td>[Node Deploy](http://www.nodedeploy.com)</td>

<td>2014.10.01</td>

<td>OpenVZ, KVM</td>

<td>Germany (DE); Los Angeles, US-CA; Atlanta, US-GA; Phoenix, US-AZ</td>

<td>"At NodeDeploy we support virtually every linux distribution." Arch Linux is listed under their Operating Systems. No version information.</td>

</tr>

<tr>

<td>[Netcup](http://netcup.de)</td>

<td>2012.11.xx</td>

<td>KVM</td>

<td>Germany (DE)</td>

<td>German language site.</td>

</tr>

<tr>

<td>[OnePoundWebHosting](http://onepoundwebhosting.co.uk)</td>

<td>2013.05.xx</td>

<td>Xen PV, Xen HVM</td>

<td>United Kingdom (UK)</td>

<td>They are a registrar too. Unable to verify server locations.</td>

</tr>

<tr>

<td>[proPlay.de](https://www.proplay.biz/)</td>

<td>2012.12.xx</td>

<td>OpenVZ, KVM</td>

<td>Germany (DE)</td>

<td>German language site.</td>

</tr>

<tr>

<td>[QuickVZ](https://www.quickvz.com)</td>

<td>2013.10</td>

<td>OpenVZ, Xen</td>

<td>Amsterdam, Netherlands (NL); Stockholm, Sweden (SE)</td>

<td>Provide hardened Arch Linux images along with Enterprise services (e,g. VPN, Virtual Private LAN Service (VPLS) and Virtual Routers.</td>

</tr>

<tr>

<td>[Rackspace Cloud](http://www.rackspace.com/cloud/cloud_hosting_products/servers/)</td>

<td>2013.6</td>

<td>Xen</td>

<td>[Multiple international locations](https://www.rackspace.com/whyrackspace/network/datacenters/)</td>

<td>Billed per hour. Use their "next gen" VPSes (using the mycloud.rackspace.com panel); the Arch image on the first gen Rackspace VPSes is out of date.</td>

</tr>

<tr>

<td>[RamHost.us](http://www.ramhost.us)</td>

<td>[2013.05.01](http://www.ramhost.us/?page=news)</td>

<td>OpenVZ, KVM</td>

<td>Los Angeles, US-CA; Great Britain (GB); Atlanta, US-GA; Germany (DE)</td>

<td>You can request a newer ISO on RamHost's IRC network.</td>

</tr>

<tr>

<td>[RamNode](http://www.ramnode.com)</td>

<td>[2013.07.01](https://clientarea.ramnode.com/knowledgebase.php?action=displayarticle&id=48)</td>

<td>[SSD and SSD Cached:](https://clientarea.ramnode.com/knowledgebase.php?action=displayarticle&id=39) [OpenVZ, KVM](https://clientarea.ramnode.com/knowledgebase.php?action=displayarticle&id=52)</td>

<td>[Seattle, WA USA, Atlanta, GA USA](https://clientarea.ramnode.com/knowledgebase.php?action=displayarticle&id=18)</td>

<td>You can request Host/CPU passthrough with KVM service.[[3]](https://clientarea.ramnode.com/knowledgebase.php?action=displayarticle&id=66) Frequent use of discount promotions.[[4]](https://twitter.com/search?q=ramnode%20code&src=typd)</td>

</tr>

<tr>

<td>[Tilaa](http://www.tilaa.nl/)</td>

<td>2014.10.01</td>

<td>[KVM](https://www.tilaa.com/pages/vps/technology)</td>

<td>Amsterdam, NL</td>

<td>English or Dutch language site.</td>

</tr>

<tr>

<td>[TransIP](https://www.transip.eu/)</td>

<td>[2013.05.01](https://www.transip.eu/vps/vps-os/)</td>

<td>[KVM](https://www.transip.eu/vps/vps-technology/)</td>

<td>Amsterdam, NL</td>

<td>English language site. Registrar.</td>

</tr>

<tr>

<td>[XenVZ](http://www.xenvz.co.uk/)</td>

<td>2009.12.07</td>

<td>OpenVZ, Xen</td>

<td>United Kingdom (UK), United States (US)</td>

<td>[Hardware](http://www.xenvz.co.uk/faq.php#use2)</td>

</tr>

<tr>

<td>[Virpus](http://www.virpus.com/)</td>

<td>[2014.11.07](http://virpus.com/linux-vps.php)</td>

<td>Xen</td>

<td>Kansas City, US-KS; Los Angeles, US-CA</td>

<td>A subcompany of Wow Technologies, Inc. 24/7 support via Live Chat, Email, Phone, and Ticket System. Service starts at $5/month.</td>

</tr>

<tr>

<td>[Virtual Master](http://www.virtualmaster.com/)</td>

<td>2012-08</td>

<td> ??</td>

<td>Europe, Prague</td>

</tr>

<tr>

<td>[Vmline](http://www.vmline.pl/)</td>

<td>2013.09.01</td>

<td>KVM, OpenVZ</td>

<td>Kraków, PL</td>

<td>[S-Net](http://www.s-net.pl/en/) reseller. Full virtualization. Polish language site.</td>

</tr>

<tr>

<td>[VPSBG.eu](https://vpsbg.eu/)</td>

<td>2013.10</td>

<td>OpenVZ</td>

<td>[Sofia, Bulgaria](https://vpsbg.eu/en/index.php?page=vps-datacenter)</td>

<td>Offshore VPS in Bulgaria - anonymous registrations and Bitcoin are accepted.</td>

</tr>

<tr>

<td>[VPS6.NET](https://vps6.net/)</td>

<td>2013.01.xx </td>

<td>OpenVZ, Xen, HVM-ISO</td>

<td>[Multiple US](http://vps6.net/network/); Frankfurt, DE; Bucharest, RO; Istanbul, TR</td>

<td>Registrar.</td>

</tr>

<tr>

<td>[VPS.NET](http://www.vps.net/)</td>

<td>2014.01.xx </td>

<td>OpenVZ, Xen, HVM-ISO</td>

<td>[US, Canada, UK, Brazil, Netherlands, France, Germany, Japan, Singapore, India, Austrlia](http://vps.net/cloud-datacenter-locations); Multiple</td>

<td>Managed & Un managed VPS service provider, multiple OS and configurations..</td>

</tr>

<tr>

<td>[World4You](http://www.world4you.com/)</td>

<td>2015.10.28</td>

<td>OpenVZ</td>

<td>Austria (AT)</td>

<td>Internet hosting provider; quick setup; 24/7 support; shared web hosting; also CentOS, Debian, Ubuntu, Fedora and Arch OpenVZ servers; supports newest systemd (227 atm)</td>

</tr>

</tbody>

</table>

## Installation

### KVM

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Are there instructions specific to VPSes? (Discuss in [Talk:Virtual Private Server#](https://wiki.archlinux.org/index.php/Talk:Virtual_Private_Server))

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

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Are there instructions specific to VPSes? (Discuss in [Talk:Virtual Private Server#](https://wiki.archlinux.org/index.php/Talk:Virtual_Private_Server))

See [Xen#Arch as Xen guest (PVHVM mode)](/index.php/Xen#Arch_as_Xen_guest_.28PVHVM_mode.29 "Xen") and/or [Xen#Arch as Xen guest (PV mode)](/index.php/Xen#Arch_as_Xen_guest_.28PV_mode.29 "Xen").

Retrieved from "[https://wiki.archlinux.org/index.php?title=Virtual_Private_Server&oldid=415074](https://wiki.archlinux.org/index.php?title=Virtual_Private_Server&oldid=415074)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch")
*   [Virtualization](/index.php/Category:Virtualization "Category:Virtualization")