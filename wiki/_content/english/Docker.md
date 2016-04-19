[Docker](http://www.docker.io) is a utility to pack, ship and run any application as a lightweight container.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Opening Remote API](#Opening_Remote_API)
    *   [2.2 Proxies](#Proxies)
        *   [2.2.1 Daemon Proxy Configuration](#Daemon_Proxy_Configuration)
        *   [2.2.2 Container Configuration](#Container_Configuration)
    *   [2.3 Daemon Socket Configuration](#Daemon_Socket_Configuration)
    *   [2.4 Configuring DNS](#Configuring_DNS)
    *   [2.5 Images location](#Images_location)
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
    *   [7.4 docker complains about no loopback devices](#docker_complains_about_no_loopback_devices)
    *   [7.5 Default number of allowed processes/threads too low](#Default_number_of_allowed_processes.2Fthreads_too_low)
*   [8 See also](#See_also)

## Installation

**Note:** Docker doesn't support i686\. [[1]](https://github.com/docker/docker/issues/136)

[Install](/index.php/Install "Install") the [docker](https://www.archlinux.org/packages/?name=docker) package or, for the development version, the [docker-git](https://aur.archlinux.org/packages/docker-git/) package. You may need to reboot. Next [start](/index.php/Start "Start") and enable `docker.service` and verify operation:

```
# docker info

```

If you want to be able to run docker as a regular user, add yourself to the docker group:

**Warning:** Anyone added to the 'docker' group is root equivalent. More information [here](https://github.com/docker/docker/issues/9976) and [here](http://docs.docker.com/engine/articles/security/).

```
# gpasswd -a *user* docker

```

Then re-login or to make your current user session aware of this new group, you can use:

```
$ newgrp docker

```

## Configuration

### Opening Remote API

To opening the Remote API to port `4243` manually.

```
 # docker daemon -H tcp://0.0.0.0:4243 -H unix:///var/run/docker.sock

```

`-H tcp://0.0.0.0:4243` part is for opening the Remote API.

`-H unix:///var/run/docker.sock` part for host machine access via terminal.

### Proxies

Proxy configuration is broken down into two. First is the host configuration of the Docker daemon, second is the configuration required for your container to see your proxy.

#### Daemon Proxy Configuration

Copy `/usr/lib/systemd/system/docker.service` to `/etc/systemd/system/docker.service`. Then edit `/etc/systemd/system/docker.service`, where `http_proxy` is your proxy server and `-g <path>` is your docker home. The path defaults to `/var/lib/docker`.

First, create a systemd drop-in directory for the docker service: `mkdir /etc/systemd/system/docker.service.d`

Now create a file called `/etc/systemd/system/docker.service.d/http-proxy.conf` that adds the `HTTP_PROXY` environment variable:

```
[Service]
Environment="HTTP_PROXY=192.168.1.1"

```

**Note:** This assumes `192.168.1.1` is your proxy server, do not use `127.0.0.1`.

Flush changes: `sudo systemctl daemon-reload`

Verify that the configuration has been loaded:

```
sudo systemctl show docker --property Environment
Environment=HTTP_PROXY=192.168.1.1

```

Restart Docker: `sudo systemctl restart docker`

#### Container Configuration

The settings in the `docker.service` file will not translate into containers. To achieve this you must set `ENV` variables in your `Dockerfile` thus:

```
 FROM base/archlinux
 ENV http_proxy="http://192.168.1.1:3128"
 ENV https_proxy="https://192.168.1.1:3128"

```

[Docker](https://docs.docker.com/reference/builder/#env) provide detailed information on configuration via `ENV` within a Dockerfile.

### Daemon Socket Configuration

The *docker* daemon listens to a [Unix socket](https://en.wikipedia.org/wiki/Unix_domain_socket "wikipedia:Unix domain socket") by default. To listen on a specified port instead, edit `/etc/systemd/system/docker.socket`, where `ListenStream` is the used port:

```
[Socket]
ListenStream=0.0.0.0:2375

```

### Configuring DNS

By default, docker will make resolv.conf in the container match resolv.conf on the host machine, filtering out local addresses (e.g. `127.0.0.1`). If this yields and empty file, than googles DNS servers are defaulted. If you are using a service like dnsmasq to provide name resolution, you will need to add an entry to your resolv.conf for docker's network interface so that it isn't filtered out.

### Images location

By default, docker images are located at `/var/lib/docker`. They can be moved to other partitions. First, [stop](/index.php/Stop "Stop") the `docker.service`.

If you have run the docker images, you need to make sure the images are unmounted totally. Once that is completed, you may move the images from `/var/lib/docker` to the target destination.

Then add a [Drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet") for the `docker.service`, adding the `-g` parameter to the `ExecStart`:

 `/etc/systemd/system/docker.service.d/imagelocation.conf` 
```
ExecStart= 
ExecStart=/usr/bin/docker daemon -g */path/to/new/location/docker* -H fd://
```

Finally, [reload](/index.php/Reload "Reload") configuration and [start](/index.php/Start "Start") `docker.service` again.

## Docker 0.9.0 -- 1.2.x and LXC

Since version 0.9.0 Docker provides a new way to start containers without relying on a LXC library called *libcontainer*.

The lxc exec driver and the -lxc-conf option may also be removed in the near future, [[2]](https://github.com/docker/docker/pull/5797)

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
$ ./mkimage-arch.sh
# docker run -t -i --rm archlinux /bin/bash  # try it

```

For slow network connections or CPU, the build timeout can be extended:

```
$ sed -i 's/timeout 60/timeout 120/' mkimage-arch.sh

```

### Debian

Build Debian image with [debootstrap](https://www.archlinux.org/packages/?name=debootstrap):

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

### docker complains about no loopback devices

If starting the docker service fails and `journalctl` says that no loopback device can be found, try following the steps outlined in [TrueCrypt's troubleshooting section](/index.php/TrueCrypt#Failed_to_set_up_a_loop_device "TrueCrypt"). In particular, if you've upgraded the kernel since last rebooting, you just need to reboot.

### Default number of allowed processes/threads too low

If you run into error messages like

```
# e.g. Java
java.lang.OutOfMemoryError: unable to create new native thread
# e.g. C, bash, ...
fork failed: Resource temporarily unavailable

```

then you might need to adjust the number of processes allowed by systemd. Default (see system.conf) is 500, which is pretty small for running several docker containers. You need to create a drop-in service file for this:

```
# mkdir /etc/systemd/system/docker.service.d
# cat > /etc/systemd/system/docker.service.d/tasks.conf <<EOF
[Service]
TasksMax=infinity
EOF
# systemctl daemon-reload
# systemctl restart docker.service

```

## See also

*   [Arch Linux on docs.docker.com](https://docs.docker.com/installation/archlinux/)
*   [Are Docker containers really secure?](http://opensource.com/business/14/7/docker-security-selinux) — opensource.com