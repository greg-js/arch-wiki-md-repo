**翻译状态：** 本文是英文页面 [OpenStack](/index.php/OpenStack "OpenStack") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-03-22，点击[这里](https://wiki.archlinux.org/index.php?title=OpenStack&diff=0&oldid=425647)可以查看翻译后英文页面的改动。

OpenStack is a global collaboration of developers and cloud computing technologists producing the ubiquitous open source cloud computing platform for public and private clouds. The project aims to deliver solutions for all types of clouds by being simple to implement, massively scalable, and feature rich. The technology consists of a series of interrelated projects delivering various components for a cloud infrastructure solution

## Contents

*   [1 组件](#组件)
    *   [1.1 计算(Nova)](#计算(Nova))
    *   [1.2 网络(Neutron)](#网络(Neutron))
    *   [1.3 镜像服务(Glance)](#镜像服务(Glance))
    *   [1.4 块存储(Cinder)](#块存储(Cinder))
    *   [1.5 对象存储(Swift)](#对象存储(Swift))
    *   [1.6 鉴证(Keystone)](#鉴证(Keystone))
    *   [1.7 监控台(Horizon)](#监控台(Horizon))
    *   [1.8 Telemetry (Ceilometer)](#Telemetry_(Ceilometer))
    *   [1.9 Orchestration (Heat)](#Orchestration_(Heat))
*   [2 部署 OpenStack](#部署_OpenStack)
*   [3 镜像](#镜像)
    *   [3.1 可用的镜像](#可用的镜像)
    *   [3.2 自己创建镜像](#自己创建镜像)
*   [4 参阅](#参阅)

## 组件

### 计算(Nova)

[nova-liberty](https://aur.archlinux.org/packages/nova-liberty/) is available in the [AUR](/index.php/AUR "AUR").

### 网络(Neutron)

[neutron-liberty](https://aur.archlinux.org/packages/neutron-liberty/) is available in the [AUR](/index.php/AUR "AUR").

### 镜像服务(Glance)

[glance-liberty](https://aur.archlinux.org/packages/glance-liberty/) is available in the [AUR](/index.php/AUR "AUR").

### 块存储(Cinder)

[cinder-kilo](https://aur.archlinux.org/packages/cinder-kilo/) is available in the [AUR](/index.php/AUR "AUR").

### 对象存储(Swift)

Swift is not available in Arch, yet.

### 鉴证(Keystone)

[keystone-liberty](https://aur.archlinux.org/packages/keystone-liberty/) is available in the [AUR](/index.php/AUR "AUR").

### 监控台(Horizon)

[horizon-liberty](https://aur.archlinux.org/packages/horizon-liberty/) is available in the [AUR](/index.php/AUR "AUR").

### Telemetry (Ceilometer)

### Orchestration (Heat)

[heat-engine](https://aur.archlinux.org/packages/heat-engine/) is available in the [AUR](/index.php/AUR "AUR").

## 部署 OpenStack

## 镜像

### 可用的镜像

[Official Openstack images](http://docs.openstack.org/image-guide/content/ch_obtaining_images.html) are available from most popular distributions of GNU/Linux.

Images for Arch are *work in progress*. [http://linuximages.de/openstack/arch/](http://linuximages.de/openstack/arch/) has *experimental* images for download.

### 自己创建镜像

OpenStack images need to meet [certain requirements](http://docs.openstack.org/image-guide/content/ch_openstack_images.html). An image can be prepared manually or with help from a tool.

For a tool, [image-bootstrap](https://github.com/hartwork/image-bootstrap) with the `--openstack` parameter may be of help. As of 2015-06-24, resulting images are still in *experimental* stage.

For manual creation, the *essential* steps are:

*   [Partitioning](/index.php/Partitioning "Partitioning") a disk with a single [ext3/4](/index.php/Ext4 "Ext4") partition.
*   Installing a base system (e.g. using `pacstrap` of [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts)) to it
*   Installing a boot loader (e.g. [GRUB](/index.php/GRUB "GRUB") or [extlinux](/index.php/Extlinux "Extlinux"))
*   Installing and configuring [cloud-init](/index.php/Cloud-init "Cloud-init")
*   Adding an unpriviliged user able to run [sudo](/index.php/Sudo "Sudo") without a password
*   Configuring `eth0` for [DHCP](/index.php/DHCP "DHCP")
    *   Configuring [udev](/index.php/Udev "Udev") to name network interfaces `eth*`
    *   Configuring [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") to use [DHCP](/index.php/DHCP "DHCP") on `eth0`
*   Installing [SSH](/index.php/SSH "SSH") server
*   Adjusting [initramfs](/index.php/Initramfs "Initramfs") creation and regenerating initramfs images
    *   Disabling the `autodetect` hook (since autodetection works differently from a chroot)
    *   Either activating hook `growfs` from [mkinitcpio-growrootfs](https://aur.archlinux.org/packages/mkinitcpio-growrootfs/) or installing `growpart` from [cloud-utils](https://aur.archlinux.org/packages/cloud-utils/) and have [cloud-init](/index.php/Cloud-init "Cloud-init") do resizing by itself
*   Making services start automatically (e.g. using `systemctl enable ...`)
*   Deleting generated keys (i.e. those of the SSH server and pacman); optionally generating new ones during first boot
*   Delete machine IDs (`/etc/machine-id` and `/var/lib/dbus/machine-id`) so that two systems are not mistaken for the same thing

## 参阅

*   [Openstack 官方网站](http://www.openstack.org/)