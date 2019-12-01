[arch-boxes](https://github.com/archlinux/arch-boxes) builds vagrant and cloud images via Hashicorp packer. The vagrant images are going to be uploaded to vagrantcloud.com, the cloud-images need to get signed manually and uploaded into a web directory.

## Requirements

We have the following requirements for building vagrant images and cloud-images via the [arch-boxes](https://github.com/archlinux/arch-boxes) project.

*   Virtualization support: `egrep (vmx|svm) -o /proc/cpuinfo`
*   Hypervisors installed: virtualbox, qemu
*   Hashicorp packer installed

**Note:** Use the `arch-boxes` Ansible role for deploying the project on a host. The role makes sure, that kernel modules are loaded, hypervisors and packer are installed and more

## Components

 `arch-boxes` 
```
├── cloud.json (1)
├── controller.py (2)
├── generic-ci.sh (3)
├── http (4)
│  ├── install-chroot.sh (5)
│  ├── install-cloud.sh (6)
│  └── install.sh (7)
├── LICENSE
├── local.json (8)
├── packer_cache (9)
├── provision (10)
│  ├── cleanup.sh (11)
│  ├── cloud-init.sh (12)
│  ├── postinstall.sh (13)
│  ├── qemu.sh (14)
│  ├── virtualbox.sh (15)
│  ├── vmware.sh (16)
│  └── write_zeroes.sh (17)
├── README.md
├── STYLEGUIDE.md
└── vagrant.json (18)
```

1.  The `cloud.json` file is the packer configuration for `qcow2` cloud-images.
2.  `controller.py` is triggered via a systemd-timer unit every day and checks if a build needs to get triggered.
3.  `generic-ci.sh` is an abstraction layer for the testing environment and can be therefore ignored in production.
4.  The `http` directory contains all scripts for a basic installation.
5.  `install-chroot.sh` is all code that needs to get executed for vagrant images in the arch-mount during installation.
6.  `install-cloud.sh` is the installation script for the qcow2 cloud-images. It get's executed during arch-mount and replaces `install-chroot.sh` for cloud-images.
7.  `install.sh` is the code for partitioning the VM, making the filesystem and executing arch-mount.
8.  `local.json` is for third-party users only. You can ignore it in production.
9.  `packer_cache` is the cache directory of packer for saving ISOs etc (When a local mirror is used this directory should be empty)
10.  `provision` is a directory with additional provisioning scripts, these scripts get executed after the installation process.
11.  `cleanup.sh` makes sure to remove man pages, pacman cache etc.
12.  `cloud-init.sh` installs cloud-init and enables all cloud-init services
13.  `postinstall.sh` sets a hostname, timezone, locales and enables systemd-resolved.
14.  `qemu.sh` installs the qemu guest-agent.
15.  `virtualbox.sh` installs the virtualbox guest-agent.
16.  `vmware.sh` installs the vmware guest-agent.
17.  `write_zeroes.sh` shrinks the VM image size via writing zeroes into a tmpfile. This is maybe harmful to your SSD.
18.  `vagrant.json` this is the packer configuration for building vagrant images and uploading them to the vagrantcloud.

## Troubleshooting

If you need to run an image build manually, you can do so via:

`packer build -parallel=false -var 'headless=true' -var 'write_zeroes=yes' -except=vmware-iso vagrant.json`

This line will start a build process for virtualbox and qemu. If you need debugging output you need to add the following environment variable in front of the command: `PACKER_LOG=1`