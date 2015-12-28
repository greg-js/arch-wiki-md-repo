# Docker

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn")
*   [Linux Containers](/index.php/Linux_Containers "Linux Containers")
*   [Lxc-systemd](/index.php/Lxc-systemd "Lxc-systemd")
*   [Vagrant](/index.php/Vagrant "Vagrant")

[Docker](http://www.docker.io) is a utility to pack, ship and run any application as a lightweight container.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Proxies](#Proxies)
        *   [2.1.1 Daemon Proxy Configuration](#Daemon_Proxy_Configuration)
        *   [2.1.2 Container Configuration](#Container_Configuration)
    *   [2.2 Daemon Socket Configuration](#Daemon_Socket_Configuration)
*   [3 Docker 0.9.0 -- 1.2.x and LXC](#Docker_0.9.0_--_1.2.x_and_LXC)
*   [4 Images](#Images)
    *   [4.1 Arch Linux](#Arch_Linux)
        *   [4.1.1 x86_64](#x86_64)
        *   [4.1.2 i686](#i686)
        *   [4.1.3 Build Image](#Build_Image)
    *   [4.2 Debian](#Debian)
*   [5 Arch Linux image with snapshot repository](#Arch_Linux_image_with_snapshot_repository)
*   [6 Useful tips](#Useful_tips)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Docker info errors out](#Docker_info_errors_out)
    *   [7.2 Deleting Docker Images in a BTRFS Filesystem](#Deleting_Docker_Images_in_a_BTRFS_Filesystem)
    *   [7.3 docker0 Bridge gets no IP / no internet access in containers](#docker0_Bridge_gets_no_IP_.2F_no_internet_access_in_containers)
*   [8 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [docker](https://www.archlinux.org/packages/?name=docker) package or, for the i686 architecture, the [docker-git](https://aur.archlinux.org/packages/docker-git/)<sup><small>AUR</small></sup> package. Next [start](/index.php/Start "Start") `docker.service` and verify operation:

```
# docker info

```

If you want to be able to run docker as a regular user, add yourself to the docker group:

**Warning:** Anyone added to the 'docker' group is root equivalent. More information [here](https://github.com/docker/docker/issues/9976) and [here](http://docs.docker.com/engine/articles/security/).

```
# gpasswd -a _user_ docker

```

Then re-login or to make your current user session aware of this new group, you can use:

```
$ newgrp docker

```

## Configuration

### Proxies

Proxy configuration is broken down into two. First is the host configuration of the Docker daemon, second is the configuration required for your container to see your proxy.

#### Daemon Proxy Configuration

Copy `/usr/lib/systemd/system/docker.service` to `/etc/systemd/system/docker.service`. Then edit `/etc/systemd/system/docker.service`, where `http_proxy` is your proxy server and `-g <path>` is your docker home. The path defaults to `/var/lib/docker`.

```
[Service]
Environment="http_proxy=192.168.1.1:3128"

```

**Note:** This assumes `192.168.1.1` is your proxy server, do not use `127.0.0.1`.

#### Container Configuration

The settings in the `docker.service` file will not translate into containers. To achieve this you must set `ENV` variables in your `Dockerfile` thus:

```
 FROM base/archlinux
 ENV http_proxy="http://192.168.1.1:3128"
 ENV https_proxy="https://192.168.1.1:3128"

```

[Docker](https://docs.docker.com/reference/builder/#env) provide detailed information on configuration via `ENV` within a Dockerfile.

### Daemon Socket Configuration

The _docker_ daemon listens to a [Unix socket](https://en.wikipedia.org/wiki/Unix_domain_socket "wikipedia:Unix domain socket") by default. To listen on a specified port instead, edit `/etc/systemd/system/docker.socket`, where `ListenStream` is the used port:

```
[Socket]
ListenStream=0.0.0.0:2375

```

## Docker 0.9.0 -- 1.2.x and LXC

Since version 0.9.0 Docker provides a new way to start containers without relying on a LXC library called _libcontainer_.

The lxc exec driver and the -lxc-conf option may also be removed in the near future, [[1]](https://github.com/docker/docker/pull/5797)

Hence, you will not be able to use `lxc-attach` with containers managed by Docker 0.9.0+ by default. It is required to make Docker daemon run with `-e lxc` as an argument.

You can create a file named `lxc.conf` under `/etc/systemd/system/docker.service.d/` with the following contents:

```
[Service]
ExecStart=
ExecStart=/usr/bin/docker -d -e lxc

```

## Images

### Arch Linux

#### x86_64

The following command pulls the [base/archlinux](https://hub.docker.com/r/base/archlinux/) x86_64 image.

```
# docker pull base/archlinux

```

#### i686

The default Arch Linux image in Docker Registry is for x86_64 only. i686 image must be built manually.

#### Build Image

Instead, check [docker base/archlinux registry](https://registry.hub.docker.com/u/base/archlinux/) and click the `mkimage-arch.sh` link to download `mkimage-arch.sh` and `mkimage-arch-pacman.conf` to the same directory as raw files. Next, make the script executable and run it:

```
$ chmod +x mkimage-arch.sh
$ cp /etc/pacman.conf ./mkimage-arch-pacman.conf # or get a pacman.conf from somewhere else
$ LC_ALL=C ./mkimage-arch.sh # LC_ALL=C because the script parses the console output
# docker run -t -i --rm base/archlinux /bin/bash # try it

```

For slow network connections or CPU, the build timeout can be extended:

```
$ sed -i 's/timeout 60/timeout 120/' mkimage-arch.sh

```

### Debian

Build Debian image with [debootstrap](https://aur.archlinux.org/packages/debootstrap/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR"):

```
# mkdir wheezy-chroot
# debootstrap wheezy ./wheezy-chroot [http://http.debian.net/debian/](http://http.debian.net/debian/)
# cd wheezy-chroot
# tar cpf - . | docker import - debian
# docker run -t -i --rm debian /bin/bash

```

## Arch Linux image with snapshot repository

Archlinux on Docker can become problematic when multiple images are created and updated each having different package versions. To keep Docker containers with consistent package versions a [Docker image with a snapshot repository](https://registry.hub.docker.com/u/pritunl/archlinux/) is available. This allows installing new packages from the official repository as it was on the day that the snapshot was created.

```
$ docker pull pritunl/archlinux:latest
$ docker run --rm -t -i pritunl/archlinux:latest /bin/bash

```

## Useful tips

To grab the IP address of a running container:

 `$ docker inspect --format '{{ .NetworkSettings.IPAddress }}' <container-name OR id> `  `172.17.0.37` 

## Troubleshooting

### Docker info errors out

If running `docker info` gives an error that looks like this:

```
 FATA[0000] Get [http:///var/run/docker.sock/v1.17/info](http:///var/run/docker.sock/v1.17/info): read unix /var/run/docker.sock: connection reset by peer. Are you trying to connect to a TLS-enabled daemon without TLS? 

```

then you might not have the `bridge` module loaded. You can check for it by running `lsmod` . If it is not loaded, you can try to load it with `modprobe` or simply reboot (a reboot might be required if you have upgraded your kernel recently without rebooting and the bridge module was built for the more recent kernel.)

See [this issue on GitHub for more information](https://github.com/docker/docker/issues/6853).

### Deleting Docker Images in a BTRFS Filesystem

Deleting docker images in a [btrfs](/index.php/Btrfs "Btrfs") filesystem leaves the images in `/var/lib/docker/btrfs/subvolumes/` with a size of 0\. When you try to delete this you get a permission error.

```
 # docker rm bab4ff309870
 # rm -Rf /var/lib/docker/btrfs/subvolumes/*
 rm: cannot remove '/var/lib/docker/btrfs/subvolumes/85122f1472a76b7519ed0095637d8501f1d456787be1a87f2e9e02792c4200ab': Operation not permitted

```

This is caused by btrfs which created subvolumes for the docker images. So the correct command to delete them is:

```
 # btrfs subvolume delete /var/lib/docker/btrfs/subvolumes/85122f1472a76b7519ed0095637d8501f1d456787be1a87f2e9e02792c4200ab

```

### docker0 Bridge gets no IP / no internet access in containers

Docker enables IP forwarding by itself, but by default systemd overrides the respective sysctl setting. The following disables this override (for all interfaces):

```
# cat > /etc/systemd/network/ipforward.network <<EOF
[Network]
IPForward=ipv4
EOF

# cat > /etc/systemd/network/99-docker.conf <<EOF
net.ipv4.ip_forward = 1
EOF

# sysctl -w net.ipv4.ip_forward=1

```

Finally [restart](/index.php/Restart "Restart") the `systemd-networkd` and `docker` services.

## See also

*   [Arch Linux on docs.docker.com](https://docs.docker.com/installation/archlinux/)
*   [Are Docker containers really secure?](http://opensource.com/business/14/7/docker-security-selinux) — opensource.com

Retrieved from "[https://wiki.archlinux.org/index.php?title=Docker&oldid=413627](https://wiki.archlinux.org/index.php?title=Docker&oldid=413627)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Virtualization](/index.php/Category:Virtualization "Category:Virtualization")