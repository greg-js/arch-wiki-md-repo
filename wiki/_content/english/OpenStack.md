OpenStack is a global collaboration of developers and cloud computing technologists producing the ubiquitous open source cloud computing platform for public and private clouds. The project aims to deliver solutions for all types of clouds by being simple to implement, massively scalable, and feature rich. The technology consists of a series of interrelated projects delivering various components for a cloud infrastructure solution

## Contents

*   [1 Components](#Components)
    *   [1.1 Compute (Nova)](#Compute_.28Nova.29)
    *   [1.2 Networking (Neutron)](#Networking_.28Neutron.29)
    *   [1.3 Image Service (Glance)](#Image_Service_.28Glance.29)
    *   [1.4 Block Storage (Cinder)](#Block_Storage_.28Cinder.29)
    *   [1.5 Object Storage (Swift)](#Object_Storage_.28Swift.29)
    *   [1.6 Identity (Keystone)](#Identity_.28Keystone.29)
    *   [1.7 Dashboard (Horizon)](#Dashboard_.28Horizon.29)
    *   [1.8 Telemetry (Ceilometer)](#Telemetry_.28Ceilometer.29)
    *   [1.9 Orchestration (Heat)](#Orchestration_.28Heat.29)
*   [2 Deploy OpenStack](#Deploy_OpenStack)
*   [3 Images](#Images)
    *   [3.1 Available images](#Available_images)
    *   [3.2 Creating images yourself](#Creating_images_yourself)
*   [4 See also](#See_also)

## Components

### Compute (Nova)

[nova](https://aur.archlinux.org/packages/nova/) is available in the [AUR](/index.php/AUR "AUR").

### Networking (Neutron)

[neutron-server](https://aur.archlinux.org/packages/neutron-server/) is available in the [AUR](/index.php/AUR "AUR").

### Image Service (Glance)

[glance](https://aur.archlinux.org/packages/glance/) is available in the [AUR](/index.php/AUR "AUR").

### Block Storage (Cinder)

[cinder-icehouse](https://aur.archlinux.org/packages/cinder-icehouse/) is available in the [AUR](/index.php/AUR "AUR").

### Object Storage (Swift)

Swift is not available in Arch, yet.

### Identity (Keystone)

[keystone](https://aur.archlinux.org/packages/keystone/) is available in the [AUR](/index.php/AUR "AUR").

### Dashboard (Horizon)

[horizon-deb](https://aur.archlinux.org/packages/horizon-deb/) is available in the [AUR](/index.php/AUR "AUR").

### Telemetry (Ceilometer)

### Orchestration (Heat)

[heat-engine](https://aur.archlinux.org/packages/heat-engine/) is available in the [AUR](/index.php/AUR "AUR").

## Deploy OpenStack

## Images

### Available images

[Official Openstack images](http://docs.openstack.org/image-guide/content/ch_obtaining_images.html) are available from most popular distributions of GNU/Linux.

Images for Arch are _work in progress_. [http://linuximages.de/openstack/arch/](http://linuximages.de/openstack/arch/) has _experimental_ images for download.

### Creating images yourself

OpenStack images need to meet [certain requirements](http://docs.openstack.org/image-guide/content/ch_openstack_images.html). An image can be prepared manually or with help from a tool.

For a tool, [image-bootstrap](https://github.com/hartwork/image-bootstrap) with the `--openstack` parameter may be of help. As of 2015-06-24, resulting images are still in _experimental_ stage.

For manual creation, the _essential_ steps are:

*   [Partitioning](/index.php/Partitioning "Partitioning") a disk with a single [ext3/4](/index.php/Ext4 "Ext4") partition.
*   Installing a base system (e.g. using `pacstrap` of [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts)) to it
*   Installing a boot loader (e.g. [GRUB](/index.php/GRUB "GRUB") or [extlinux](/index.php/Extlinux "Extlinux"))
*   Installing and configuring [cloud-init](/index.php/Cloud-init "Cloud-init")
*   Adding an unpriviliged user able to run [sudo](/index.php/Sudo "Sudo") without a password
*   Configuring `eth0` for [DHCP](/index.php?title=DHCP&action=edit&redlink=1 "DHCP (page does not exist)")
    *   Configuring [udev](/index.php/Udev "Udev") to name network interfaces `eth*`
    *   Configuring [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") to use [DHCP](/index.php?title=DHCP&action=edit&redlink=1 "DHCP (page does not exist)") on `eth0`
*   Installing [SSH](/index.php/SSH "SSH") server
*   Adjusting [initramfs](/index.php/Initramfs "Initramfs") creation and regenerating initramfs images
    *   Disabling the `autodetect` hook (since autodetection works differently from a chroot)
    *   Either activating hook `growfs` from [mkinitcpio-growrootfs](https://aur.archlinux.org/packages/mkinitcpio-growrootfs/) or installing `growpart` from [cloud-utils](https://aur.archlinux.org/packages/cloud-utils/) and have [cloud-init](/index.php/Cloud-init "Cloud-init") do resizing by itself
*   Making services start automatically (e.g. using `systemctl enable ...`)
*   Deleting generated keys (i.e. those of the SSH server and pacman); optionally generating new ones during first boot
*   Delete machine IDs (`/etc/machine-id` and `/var/lib/dbus/machine-id`) so that two systems are not mistaken for the same thing

## See also

*   [Openstack web site](http://www.openstack.org/)