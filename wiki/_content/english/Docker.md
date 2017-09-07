Related articles

*   [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn")
*   [Linux Containers](/index.php/Linux_Containers "Linux Containers")
*   [Lxc-systemd](/index.php/Lxc-systemd "Lxc-systemd")
*   [Vagrant](/index.php/Vagrant "Vagrant")

[Docker](https://www.docker.com) is a utility to pack, ship and run any application as a lightweight container.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Storage driver](#Storage_driver)
    *   [2.2 Remote API](#Remote_API)
        *   [2.2.1 Remote API with systemd](#Remote_API_with_systemd)
    *   [2.3 Daemon socket configuration](#Daemon_socket_configuration)
    *   [2.4 Proxies](#Proxies)
        *   [2.4.1 Proxy configuration](#Proxy_configuration)
        *   [2.4.2 Container configuration](#Container_configuration)
    *   [2.5 Configuring DNS](#Configuring_DNS)
    *   [2.6 Running Docker with a manually-defined network](#Running_Docker_with_a_manually-defined_network)
    *   [2.7 Images location](#Images_location)
    *   [2.8 Insecure registries](#Insecure_registries)
*   [3 Images](#Images)
    *   [3.1 Arch Linux](#Arch_Linux)
        *   [3.1.1 Manually](#Manually)
    *   [3.2 Debian](#Debian)
        *   [3.2.1 Manually](#Manually_2)
*   [4 Arch Linux image with snapshot repository](#Arch_Linux_image_with_snapshot_repository)
*   [5 Clean Remove Docker + Images](#Clean_Remove_Docker_.2B_Images)
*   [6 Useful tips](#Useful_tips)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Cannot start a container with systemd 232](#Cannot_start_a_container_with_systemd_232)
    *   [7.2 Deleting Docker Images in a BTRFS Filesystem](#Deleting_Docker_Images_in_a_BTRFS_Filesystem)
    *   [7.3 docker0 Bridge gets no IP / no internet access in containers](#docker0_Bridge_gets_no_IP_.2F_no_internet_access_in_containers)
    *   [7.4 Default number of allowed processes/threads too low](#Default_number_of_allowed_processes.2Fthreads_too_low)
    *   [7.5 Error initializing graphdriver: devmapper](#Error_initializing_graphdriver:_devmapper)
*   [8 See also](#See_also)

## Installation

**Note:**

*   Docker does not support i686 [[1]](https://github.com/docker/docker/issues/136).
*   Docker needs the `loop` module on first usage. The following steps may be required before starting docker:

```
# tee /etc/modules-load.d/loop.conf <<< "loop"
# modprobe loop 

```

You may need to reboot before the module is available.

The error message from not enabling the loop module may look like this:

```
'overlay' not found as a supported filesystem on this host. Please ensure kernel is new enough and has overlay

```

[Install](/index.php/Install "Install") the [docker](https://www.archlinux.org/packages/?name=docker) package or, for the development version, the [docker-git](https://aur.archlinux.org/packages/docker-git/) package. Next [start](/index.php/Start "Start") and enable `docker.service` and verify operation:

```
# docker info

```

If you want to be able to run docker as a regular user, add yourself to the `docker` [group](/index.php/Group "Group").

**Warning:** Anyone added to the `docker` group is root equivalent. More information [here](https://github.com/docker/docker/issues/9976) and [here](http://docs.docker.com/engine/articles/security/).

Then re-login or to make your current user session aware of this new group, you can use:

```
$ newgrp docker

```

## Configuration

### Storage driver

The docker storage driver (or graph driver) has huge impact on performance. Its job is to store layers of container images efficiently, that is when several images share a layer, only one layer uses disk space. The compatible option, `devicemapper` offers suboptimal performance, which is outright terrible on rotating disks. Additionally, `devicemappper` is not recommended in production.

As Arch linux ships new kernels, there is no point using the compatibility option. A good, modern choice is `overlay2`.

To see current storage driver, run `# docker info | head`, modern docker installation should already use `overlay2` by default.

To set your own choice of storage driver, create a [Drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet") and use `-s` option to `dockerd`:

 `/etc/systemd/system/docker.service.d/override.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd -H fd:// -s overlay2
```

Recall that `ExecStart=` line is needed to drop inherited `ExecStart`.

Further information on options is available on the [user guide](https://docs.docker.com/engine/userguide/storagedriver/selectadriver/).

### Remote API

To open the Remote API to port `4243` manually, run:

```
# /usr/bin/dockerd -H tcp://0.0.0.0:4243 -H unix:///var/run/docker.sock

```

`-H tcp://0.0.0.0:4243` part is for opening the Remote API.

`-H unix:///var/run/docker.sock` part for host machine access via terminal.

#### Remote API with systemd

To start the remote API with the docker daemon, create a [Drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet") with the following content:

 `/etc/systemd/system/docker.service.d/override.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd -H tcp://0.0.0.0:4243 -H unix:///var/run/docker.sock
```

### Daemon socket configuration

The *docker* daemon listens to a [Unix socket](https://en.wikipedia.org/wiki/Unix_domain_socket "wikipedia:Unix domain socket") by default. To listen on a specified port instead, create a [Drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet") with the following content:

 `/etc/systemd/system/docker.socket.d/socket.conf` 
```
[Socket]
ListenStream=0.0.0.0:2375
```

### Proxies

Proxy configuration is broken down into two. First is the host configuration of the Docker daemon, second is the configuration required for your container to see your proxy.

#### Proxy configuration

Create a [Drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet") with the following content:

 `/etc/systemd/system/docker.service.d/proxy.conf` 
```
[Service]
Environment="HTTP_PROXY=192.168.1.1:8080"
Environment="HTTPS_PROXY=192.168.1.1:8080"
```

**Note:** This assumes `192.168.1.1` is your proxy server, do not use `127.0.0.1`.

Verify that the configuration has been loaded:

```
# systemctl show docker --property Environment
Environment=HTTP_PROXY=192.168.1.1:8080 HTTPS_PROXY=192.168.1.1:8080

```

#### Container configuration

The settings in the `docker.service` file will not translate into containers. To achieve this you must set `ENV` variables in your `Dockerfile` thus:

```
 FROM base/archlinux
 ENV http_proxy="http://192.168.1.1:3128"
 ENV https_proxy="https://192.168.1.1:3128"

```

[Docker](https://docs.docker.com/engine/reference/builder/#env) provide detailed information on configuration via `ENV` within a Dockerfile.

### Configuring DNS

By default, docker will make `resolv.conf` in the container match `/etc/resolv.conf` on the host machine, filtering out local addresses (e.g. `127.0.0.1`). If this yields an empty file, then [Google DNS servers](https://developers.google.com/speed/public-dns/) are used. If you are using a service like [dnsmasq](/index.php/Dnsmasq "Dnsmasq") to provide name resolution, you may need to add an entry to the `/etc/resolv.conf` for docker's network interface so that it is not filtered out.

### Running Docker with a manually-defined network

If you manually configure your network using systemd-network version **220 or higher**, containers you start with Docker may be unable to access your network. Beginning with version 220, the forwarding setting for a given network (`net.ipv4.conf.<interface>.forwarding`) defaults to `off`. This setting prevents IP forwarding. It also conflicts with Docker which enables the `net.ipv4.conf.all.forwarding` setting within a container.

To work around this, edit the `<interface>.network` file in `/etc/systemd/network/` on your Docker host add the following block:

 `/etc/systemd/network/<interface>.network` 
```
[Network]
...
IPForward=kernel
...
```

This configuration allows IP forwarding from the container as expected.

### Images location

By default, docker images are located at `/var/lib/docker`. They can be moved to other partitions. First, [stop](/index.php/Stop "Stop") the `docker.service`.

If you have run the docker images, you need to make sure the images are unmounted totally. Once that is completed, you may move the images from `/var/lib/docker` to the target destination.

Then add a [Drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet") for the `docker.service`, adding the `--data-root` parameter to the `ExecStart`:

 `/etc/systemd/system/docker.service.d/docker-storage.conf` 
```
[Service]
ExecStart= 
ExecStart=/usr/bin/dockerd --data-root=*/path/to/new/location/docker* -H fd://
```

### Insecure registries

If you decide to use a self signed certificate for your private registry, Docker will refuse to use it until you declare that you trust it. Add a [Drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet") for the `docker.service`, adding the `--insecure-registry` parameter to the `dockerd`:

 `/etc/systemd/system/docker.service.d/override.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd -H fd:// --insecure-registry my.registry.name:5000
```

## Images

### Arch Linux

The following command pulls the [base/archlinux](https://hub.docker.com/r/base/archlinux/) x86_64 image.

```
# docker pull base/archlinux

```

#### Manually

Check [moby/contrib repo](https://github.com/moby/moby/tree/master/contrib) and download `mkimage-arch.sh` and `mkimage-arch-pacman.conf` to the same directory as raw files. Next, make the script executable and run it:

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

The following command pulls the [debian](https://hub.docker.com/r/_/debian/) x86_64 image.

```
# docker pull debian

```

#### Manually

Build Debian image with [debootstrap](https://www.archlinux.org/packages/?name=debootstrap):

```
# mkdir jessie-chroot
# debootstrap jessie ./jessie-chroot [http://http.debian.net/debian/](http://http.debian.net/debian/)
# cd jessie-chroot
# tar cpf - . | docker import - debian
# docker run -t -i --rm debian /bin/bash

```

## Arch Linux image with snapshot repository

Arch Linux on Docker can become problematic when multiple images are created and updated each having different package versions. To keep Docker containers with consistent package versions, a [Docker image with a snapshot repository](https://registry.hub.docker.com/u/pritunl/archlinux/) is available. This allows installing new packages from the official repository as it was on the day that the snapshot was created.

```
$ docker pull pritunl/archlinux:latest
$ docker run --rm -t -i pritunl/archlinux:latest /bin/bash

```

Alternatively, you could use [Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive") by freezing `/etc/pacman.d/mirrorlist`

```
 Server=[https://archive.archlinux.org/repos/2020/01/02/$repo/os/$arch](https://archive.archlinux.org/repos/2020/01/02/$repo/os/$arch)

```

## Clean Remove Docker + Images

In case you want to remove Docker entirely you can do this by following the steps below:

**Note:** Do not just copy paste those commands without making sure you know what you are doing.

Check for running containers:

```
# docker ps

```

List all containers running on the host for deletion:

```
# docker ps -a

```

Stop a running container:

```
# docker stop <CONTAINER ID>

```

Killing still running containers:

```
# docker kill <CONTAINER ID>

```

Delete all containers listed by ID:

```
# docker rm <CONTAINER ID>

```

List all Docker images:

```
# docker images

```

Delete all images by ID:

```
# docker rmi <IMAGE ID>

```

Delete all Docker data (purge directory):

```
# rm -R /var/lib/docker

```

## Useful tips

To grab the IP address of a running container:

 `$ docker inspect --format '{{ .NetworkSettings.IPAddress }}' <container-name OR id> `  `172.17.0.37` 

## Troubleshooting

### Cannot start a container with systemd 232

Append `systemd.legacy_systemd_cgroup_controller=yes` as [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"), see [bug report](https://github.com/opencontainers/runc/issues/1175) for details.

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
IPForward=kernel
EOF

# cat > /etc/sysctl.d/99-docker.conf <<EOF
net.ipv4.ip_forward = 1
EOF

# sysctl -w net.ipv4.ip_forward=1

```

**Note:** It has been observed that with systemd version 220 creating this file causes bridges used by Docker to lose their IP addresses. Running Docker with a manually-defined network, as described above, is known to work.

Finally [restart](/index.php/Restart "Restart") the `systemd-networkd` and `docker` services.

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

### Error initializing graphdriver: devmapper

If `systemctl` fails to start docker and provides an error:

```
 Error starting daemon: error initializing graphdriver: devmapper: Device docker-8:2-915035-pool is not a thin pool

```

Then, try the following steps to resolve the error. Stop the service, back up `/var/lib/docker/` (if desired), remove the contents of `/var/lib/docker/`, and try to start the service. See the open [GitHub issue](https://github.com/docker/docker/issues/21304) for details.

## See also

*   [Arch Linux on docs.docker.com](https://docs.docker.com/engine/installation/linux/archlinux/)
*   [Are Docker containers really secure?](http://opensource.com/business/14/7/docker-security-selinux) — opensource.com