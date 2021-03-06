"*OpenNebula is the industry standard for on-premise IaaS cloud computing, offering the most feature-rich, flexible solution for the comprehensive management of virtualized data centers to enable private, public and hybrid (cloudbursting) clouds. OpenNebula interoperability makes cloud an evolution by leveraging existing IT infrastructure, protecting your investments, and avoiding vendor lock-in.*"

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Configuration specific to QEMU-KVM](#Configuration_specific_to_QEMU-KVM)
    *   [2.2 Configuration specific to Xen](#Configuration_specific_to_Xen)
    *   [2.3 Configuration specific to VMware](#Configuration_specific_to_VMware)
*   [3 Troubleshooting](#Troubleshooting)
*   [4 Resources](#Resources)

## Installation

[Install](/index.php/Install "Install") the [opennebula](https://aur.archlinux.org/packages/opennebula/) package from the [AUR](/index.php/AUR "AUR"). For those interested in running the latest bleeding edge version of OpenNebula, install the [opennebula-unstable](https://aur.archlinux.org/packages/opennebula-unstable/) package, also in the AUR.

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