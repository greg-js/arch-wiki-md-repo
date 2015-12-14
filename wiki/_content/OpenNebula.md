# OpenNebula

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** please use the first argument of the template to provide more detailed indications. (Discuss in [Talk:OpenNebula#](https://wiki.archlinux.org/index.php/Talk:OpenNebula))

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:OpenNebula#](https://wiki.archlinux.org/index.php/Talk:OpenNebula))

"_OpenNebula is the industry standard for on-premise IaaS cloud computing, offering the most feature-rich, flexible solution for the comprehensive management of virtualized data centers to enable private, public and hybrid (cloudbursting) clouds. OpenNebula interoperability makes cloud an evolution by leveraging existing IT infrastructure, protecting your investments, and avoiding vendor lock-in._"

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Configuration specific to QEMU-KVM](#Configuration_specific_to_QEMU-KVM)
    *   [2.2 Configuration specific to Xen](#Configuration_specific_to_Xen)
    *   [2.3 Configuration specific to VMware](#Configuration_specific_to_VMware)
*   [3 Troubleshooting](#Troubleshooting)
*   [4 Resources](#Resources)

## Installation

[Install](/index.php/Install "Install") the [opennebula](https://aur.archlinux.org/packages/opennebula/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/opennebula)]</sup> package from the [AUR](/index.php/AUR "AUR"). For those interested in running the latest bleeding edge version of OpenNebula, install the [opennebula-unstable](https://aur.archlinux.org/packages/opennebula-unstable/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/opennebula-unstable)]</sup> package, also in the AUR.

## Configuration

OpenNebula supports multiple hypervisors (QEMU-KVM, Xen, VMware) which means that the configuration of your OpenNebula deployment is dependent on which hypervisor technology you plan on using, but because OpenNebula uses [libvirt](/index.php/Libvirt "Libvirt") for managing virtual machines (VMs) some of the OpenNebula configuration is hypervisor agnostic. The hypervisor agnostic configuration will be in this section and the hypervisor dependent configuration will be in the appropriate sub-sections.

See also: [libvirt](/index.php/Libvirt "Libvirt")

### Configuration specific to QEMU-KVM

To be added later

See also: [QEMU](/index.php/QEMU "QEMU") and [KVM](/index.php/KVM "KVM")

### Configuration specific to Xen

TODO

See also: [Xen](/index.php/Xen "Xen")

### Configuration specific to VMware

TODO

See also: [VMware](/index.php/VMware "VMware")

## Troubleshooting

TODO

## Resources

*   [OpenNebula's Official Website](http://www.opennebula.org/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=OpenNebula&oldid=412144](https://wiki.archlinux.org/index.php?title=OpenNebula&oldid=412144)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Virtualization](/index.php/Category:Virtualization "Category:Virtualization")