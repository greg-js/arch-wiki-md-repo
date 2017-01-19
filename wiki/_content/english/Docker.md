[Docker](https://www.docker.com) is a utility to pack, ship and run any application as a lightweight container.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Storage driver](#Storage_driver)
    *   [2.2 Opening remote API](#Opening_remote_API)
        *   [2.2.1 Remote API with systemd](#Remote_API_with_systemd)
    *   [2.3 Daemon socket configuration](#Daemon_socket_configuration)
    *   [2.4 Proxies](#Proxies)
        *   [2.4.1 Proxy configuration](#Proxy_configuration)
        *   [2.4.2 Container configuration](#Container_configuration)
    *   [2.5 Configuring DNS](#Configuring_DNS)
    *   [2.6 Images location](#Images_location)
*   [3 Docker 0.9.0 -- 1.2.x and LXC](#Docker_0.9.0_--_1.2.x_and_LXC)
*   [4 Images](#Images)
    *   [4.1 Arch Linux](#Arch_Linux)
        *   [4.1.1 x86_64](#x86_64)
        *   [4.1.2 i686](#i686)
        *   [4.1.3 Build Image](#Build_Image)
    *   [4.2 Debian](#Debian)
*   [5 Arch Linux image with snapshot repository](#Arch_Linux_image_with_snapshot_repository)
*   [6 Clean Remove Docker + Images](#Clean_Remove_Docker_.2B_Images)
*   [7 Useful tips](#Useful_tips)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 Cannot start a container with systemd 232](#Cannot_start_a_container_with_systemd_232)
    *   [8.2 Docker info errors out](#Docker_info_errors_out)
    *   [8.3 Deleting Docker Images in a BTRFS Filesystem](#Deleting_Docker_Images_in_a_BTRFS_Filesystem)
    *   [8.4 docker0 Bridge gets no IP / no internet access in containers](#docker0_Bridge_gets_no_IP_.2F_no_internet_access_in_containers)
    *   [8.5 Default number of allowed processes/threads too low](#Default_number_of_allowed_processes.2Fthreads_too_low)
*   [9 See also](#See_also)

## Installation

**Note:**

*   Docker doesn't support i686 [[1]](https://github.com/docker/docker/issues/136).
*   Docker needs the `loop` module on first usage. The following steps may be required before starting docker:

```
# tee /etc/modules-load.d/loop.conf <<< "loop"
# modprobe loop 

```

You may need to reboot before the module is available.

[Install](/index.php/Install "Install") the [docker](https://www.archlinux.org/packages/?name=docker) package or, for the development version, the [docker-git](https://aur.archlinux.org/packages/docker-git/) package. Next [start](/index.php/Start "Start") and enable `docker.service` and verify operation:

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

### Storage driver

Storage driver, a.k.a. graph driver has huge impact on performance. Its job is to store layers of container images efficiently, that is when several images share a layer, only one layer uses disk space. The default, most compatible option, `devicemapper` offers suboptimal performance, which is outright terrible on rotating disks. Additionally, `devicemappper` is not recommended in production.

As Arch linux ships new kernels, there's no point using the compatibility option. A good, modern choice is `overlay2`.

To see current storage driver, run `# docker info | head`.

To set your own choice of storage driver, create a [Drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet") and use `-s` option to `dockerd`:

 `/etc/systemd/system/docker.service.d/override.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd -H fd:// -s overlay2
```

Recall that `ExecStart=` line is needed to drop inherited `ExecStart`.

Further information on options is available on the [user guide](https://docs.docker.com/engine/userguide/storagedriver/selectadriver/).

### Opening remote API

To open the Remote API to port `4243` manually, run:

```
 # docker daemon -H tcp://0.0.0.0:4243 -H unix:///var/run/docker.sock

```

`-H tcp://0.0.0.0:4243` part is for opening the Remote API.

`-H unix:///var/run/docker.sock` part for host machine access via terminal.

##### Remote API with systemd

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
Environment="HTTP_PROXY=192.168.1.1"
```

**Note:** This assumes `192.168.1.1` is your proxy server, do not use `127.0.0.1`.

Verify that the configuration has been loaded:

```
# systemctl show docker --property Environment
Environment=HTTP_PROXY=192.168.1.1

```

#### Container configuration

The settings in the `docker.service` file will not translate into containers. To achieve this you must set `ENV` variables in your `Dockerfile` thus:

```
 FROM base/archlinux
 ENV http_proxy="http://192.168.1.1:3128"
 ENV https_proxy="https://192.168.1.1:3128"

```

[Docker](https://docs.docker.com/reference/builder/#env) provide detailed information on configuration via `ENV` within a Dockerfile.

### Configuring DNS

By default, docker will make `resolv.conf` in the container match `/etc/resolv.conf` on the host machine, filtering out local addresses (e.g. `127.0.0.1`). If this yields an empty file, then [Google DNS servers](https://developers.google.com/speed/public-dns/) are used. If you are using a service like [dnsmasq](/index.php/Dnsmasq "Dnsmasq") to provide name resolution, you may need to add an entry to the `/etc/resolv.conf` for docker's network interface so that it isn't filtered out.

### Images location

By default, docker images are located at `/var/lib/docker`. They can be moved to other partitions. First, [stop](/index.php/Stop "Stop") the `docker.service`.

If you have run the docker images, you need to make sure the images are unmounted totally. Once that is completed, you may move the images from `/var/lib/docker` to the target destination.

Then add a [Drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet") for the `docker.service`, adding the `-g` parameter to the `ExecStart`:

 `/etc/systemd/system/docker.service.d/docker-storage.conf` 
```
[Service]
ExecStart= 
ExecStart=/usr/bin/dockerd -g */path/to/new/location/docker* -H fd://
```

## Docker 0.9.0 -- 1.2.x and LXC

Since version 0.9.0 Docker provides a new way to start containers without relying on a LXC library called *libcontainer*.

The lxc exec driver and the -lxc-conf option may also be removed in the near future [[2]](https://github.com/docker/docker/pull/5797), hence, you will not be able to use `lxc-attach` with containers managed by Docker 0.9.0+ by default. It is required to make docker daemon run with `-e lxc` as an argument.

Create [Drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet") for the `docker.service` with the following content:

 `/etc/systemd/system/docker.service.d/lxc.conf` 
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

**Note:** Don't just copy paste those commands without making sure you know what you are doing!

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
IPForward=kernel
EOF

# cat > /etc/sysctl.d/99-docker.conf <<EOF
net.ipv4.ip_forward = 1
EOF

# sysctl -w net.ipv4.ip_forward=1

```

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

## See also

*   [Arch Linux on docs.docker.com](https://docs.docker.com/engine/installation/linux/archlinux/)
*   [Are Docker containers really secure?](http://opensource.com/business/14/7/docker-security-selinux) — opensource.com