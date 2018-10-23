Related articles

*   [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn")
*   [Linux Containers](/index.php/Linux_Containers "Linux Containers")
*   [Lxc-systemd](/index.php/Lxc-systemd "Lxc-systemd")
*   [Vagrant](/index.php/Vagrant "Vagrant")

**翻译状态：** 本文是英文页面 [Docker](/index.php/Docker "Docker") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-10-22，点击[这里](https://wiki.archlinux.org/index.php?title=Docker&diff=0&oldid=549067)可以查看翻译后英文页面的改动。

[Docker](https://en.wikipedia.org/wiki/Docker_(software) 是一种打包、传输和运行任何程序作为轻量级容器的实用工具.

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 存储驱动程序](#.E5.AD.98.E5.82.A8.E9.A9.B1.E5.8A.A8.E7.A8.8B.E5.BA.8F)
    *   [2.2 远程 API](#.E8.BF.9C.E7.A8.8B_API)
        *   [2.2.1 用systemd打开远程API](#.E7.94.A8systemd.E6.89.93.E5.BC.80.E8.BF.9C.E7.A8.8BAPI)
    *   [2.3 守护进程socket配置](#.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8Bsocket.E9.85.8D.E7.BD.AE)
    *   [2.4 代理](#.E4.BB.A3.E7.90.86)
        *   [2.4.1 代理配置](#.E4.BB.A3.E7.90.86.E9.85.8D.E7.BD.AE)
        *   [2.4.2 容器配置](#.E5.AE.B9.E5.99.A8.E9.85.8D.E7.BD.AE)
    *   [2.5 配置 DNS](#.E9.85.8D.E7.BD.AE_DNS)
    *   [2.6 在systemd-networkd用手动定义的网络运行Docker](#.E5.9C.A8systemd-networkd.E7.94.A8.E6.89.8B.E5.8A.A8.E5.AE.9A.E4.B9.89.E7.9A.84.E7.BD.91.E7.BB.9C.E8.BF.90.E8.A1.8CDocker)
    *   [2.7 镜像位置](#.E9.95.9C.E5.83.8F.E4.BD.8D.E7.BD.AE)
    *   [2.8 不安全的注册](#.E4.B8.8D.E5.AE.89.E5.85.A8.E7.9A.84.E6.B3.A8.E5.86.8C)
*   [3 镜像](#.E9.95.9C.E5.83.8F)
    *   [3.1 Arch Linux](#Arch_Linux)
    *   [3.2 Debian](#Debian)
        *   [3.2.1 手动](#.E6.89.8B.E5.8A.A8)
*   [4 移除docker和镜像](#.E7.A7.BB.E9.99.A4docker.E5.92.8C.E9.95.9C.E5.83.8F)
*   [5 有用的建议](#.E6.9C.89.E7.94.A8.E7.9A.84.E5.BB.BA.E8.AE.AE)
*   [6 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [6.1 docker0 网桥无法获取 IP / internet 到容器](#docker0_.E7.BD.91.E6.A1.A5.E6.97.A0.E6.B3.95.E8.8E.B7.E5.8F.96_IP_.2F_internet_.E5.88.B0.E5.AE.B9.E5.99.A8)
    *   [6.2 默认的允许的进程/线程数太少](#.E9.BB.98.E8.AE.A4.E7.9A.84.E5.85.81.E8.AE.B8.E7.9A.84.E8.BF.9B.E7.A8.8B.2F.E7.BA.BF.E7.A8.8B.E6.95.B0.E5.A4.AA.E5.B0.91)
    *   [6.3 初始化显卡驱动错误: devmapper](#.E5.88.9D.E5.A7.8B.E5.8C.96.E6.98.BE.E5.8D.A1.E9.A9.B1.E5.8A.A8.E9.94.99.E8.AF.AF:_devmapper)
    *   [6.4 无法创建到某文件的路径: 设备没有多余的空间了](#.E6.97.A0.E6.B3.95.E5.88.9B.E5.BB.BA.E5.88.B0.E6.9F.90.E6.96.87.E4.BB.B6.E7.9A.84.E8.B7.AF.E5.BE.84:_.E8.AE.BE.E5.A4.87.E6.B2.A1.E6.9C.89.E5.A4.9A.E4.BD.99.E7.9A.84.E7.A9.BA.E9.97.B4.E4.BA.86)
*   [7 查阅更多](#.E6.9F.A5.E9.98.85.E6.9B.B4.E5.A4.9A)

## 安装

[Install](/index.php/Install "Install") [docker](https://www.archlinux.org/packages/?name=docker) 包 或者，对于开发版本，选择[docker-git](https://aur.archlinux.org/packages/docker-git/) 包. 下一步 [start](/index.php/Start "Start") 并启用 `docker.service` 然后验证操作:

```
# docker info

```

注意到如果你有启用的vpn连接的话开启docker服务可能会失败。这样的话，试下开启docker服务前断开vpn连接。之后你可以自行重连vpn。

如果你想以普通用户身份运行docker的话，添加你自己到 `docker` [user group](/index.php/User_group "User group").

**警告:** 任何加入到 `docker` 组的用户都和root用户等价. 查阅更多信息可访问 [这里](https://github.com/docker/docker/issues/9976) 和 [这里](https://docs.docker.com/engine/security/security/).

**注意:** 因为 [linux](https://www.archlinux.org/packages/?name=linux) 4.15.0-1 的*vsyscalls*, 这被容器里的特定程序需要 (比如 *apt-get*), 被内核配置默认关闭了. 要重新启用的话, 添加 `vsyscall=emulate`到 [Kernel parameters (简体中文)](/index.php/Kernel_parameters_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernel parameters (简体中文)"). 查阅更多信息到 [FS#57336](https://bugs.archlinux.org/task/57336).

## 配置

### 存储驱动程序

docker存储驱动 (或者是显卡驱动) 对性能有巨大影响. 它的工作是高效存储容器图像层，也就是许多图像共享一个层时只有一个层使用磁盘空间。兼容选项, `devicemapper` 提供了次优性能, 这在旋转磁盘上是非常糟糕的. 例外, `devicemappper` 不建议在生产中使用.

随着arch Linux发布新的内核，没有必要使用兼容选项了。一个好的现代的选择是 `overlay2`.

想看现在的存储驱动, 运行 `# docker info | head`, 现代docker安装应该已经默认使用 `overlay2` 了.

想设置你自己的存储驱动选项, 编辑 `/etc/docker/daemon.json` (如果不存在就自己创建):

 `/etc/docker/daemon.json` 
```
{
  "storage-driver": "overlay2"
}
```

然后, [restart](/index.php/Restart "Restart") docker.

更多的选项信息能在 [用户指导](https://docs.docker.com/engine/userguide/storagedriver/selectadriver/)查阅. 更多的 `daemon.json` 选项查阅 [dockerd文献](https://docs.docker.com/engine/reference/commandline/dockerd/#daemon-configuration-file).

### 远程 API

手动打开远程 API 端口 `4243` , 运行:

```
# /usr/bin/dockerd -H tcp://0.0.0.0:4243 -H unix:///var/run/docker.sock

```

`-H tcp://0.0.0.0:4243` 部分是用来打开远程 API的.

`-H unix:///var/run/docker.sock` 部分是通过终端连接主机的.

#### 用systemd打开远程API

如果要用docker守护进程开启远程API, 创建一个 [Drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet") ，内容如下:

 `/etc/systemd/system/docker.service.d/override.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd -H tcp://0.0.0.0:4243 -H unix:///var/run/docker.sock
```

### 守护进程socket配置

*docker* 守护进场默认监听 [Unix socket](https://en.wikipedia.org/wiki/Unix_domain_socket "wikipedia:Unix domain socket") .如果要监听特定端口的话, 创建一个 [Drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet") ，内容如下:

 `/etc/systemd/system/docker.socket.d/socket.conf` 
```
[Socket]
ListenStream=0.0.0.0:2375
```

### 代理

代理配置分为两部分。一部分是主机docker守护进程的配置，另一部分是让容器检测到代理的配置

#### 代理配置

创建一个 [Drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet") 内容如下:

 `/etc/systemd/system/docker.service.d/proxy.conf` 
```
[Service]
Environment="HTTP_PROXY=192.168.1.1:8080"
Environment="HTTPS_PROXY=192.168.1.1:8080"
```

**注意:** 这假定 `192.168.1.1` 是你的代理服务器，不要使用 `127.0.0.1`.

确定配置被加载了:

 `# systemctl show docker --property Environment`  `Environment=HTTP_PROXY=192.168.1.1:8080 HTTPS_PROXY=192.168.1.1:8080` 

#### 容器配置

在 `docker.service` 文件里的设置并不会进入到容器里. 要实现这样的话必须设置 `ENV` 变量在你的 `Dockerfile` 里:

```
FROM base/archlinux
ENV http_proxy="http://192.168.1.1:3128"
ENV https_proxy="https://192.168.1.1:3128"

```

[Docker](https://docs.docker.com/engine/reference/builder/#env) 提供了配置的细节信息，通过Dockerfile的 `ENV` .

### 配置 DNS

默认的，docker会让容器里的 `resolv.conf` 和主机里的 `/etc/resolv.conf` 匹配, 并过滤掉本地地址 (e.g. `127.0.0.1`). 如果这产生了一个空文件, 那么 [Google DNS servers](https://developers.google.com/speed/public-dns/) 就会被使用. 如果你用的是 [dnsmasq (简体中文)](/index.php/Dnsmasq_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Dnsmasq (简体中文)") 一样的服务来提供域名解析的话, 你可能需要在 `/etc/resolv.conf` 添加入口给docker网络借口让它不被过滤掉.

### 在systemd-networkd用手动定义的网络运行Docker

如果你是手动配置的网络，用的是 [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") 版本 **220 或者更高**, 你运行的容器可能无法连接网络. 从版本 220开始, 对于给定网络 (`net.ipv4.conf.<interface>.forwarding`) 的转发设置默认是 `off`. 这个设置阻止了IP转发. 它会与在容器里启用了 `net.ipv4.conf.all.forwarding` 设置的docker冲突

一个解决办法是编辑 在`/etc/systemd/network/`里的`<interface>.network`文件 , 添加 `IPForward=kernel` 到docker主机:

 `/etc/systemd/network/<interface>.network` 
```
[Network]
...
IPForward=kernel
...
```

这项设置像预期一样允许来自容器的IP转发.

### 镜像位置

默认，docker镜像放置在 `/var/lib/docker`. 他们可以被移动到其他分区. 首先, [stop](/index.php/Stop "Stop") the `docker.service`.

如果你正在运行docker镜像，你必须确定镜像被完全解除挂载。一旦这个完成后，你就可以把镜像从 `/var/lib/docker` 移动到你的目标地点.

然后为`docker.service`添加 [Drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet")，加入 `--data-root` 参数到 `ExecStart`:

 `/etc/systemd/system/docker.service.d/docker-storage.conf` 
```
[Service]
ExecStart= 
ExecStart=/usr/bin/dockerd --data-root=*/path/to/new/location/docker* -H fd://
```

### 不安全的注册

如果你想用自签名的证书, docker会拒绝它直到你定义你相信它. 为`docker.service`添加 [Drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet"), 添加 `--insecure-registry`参数到 `dockerd`:

 `/etc/systemd/system/docker.service.d/override.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd -H fd:// --insecure-registry my.registry.name:5000
```

## 镜像

### Arch Linux

下面的命令会拉取 [archlinux/base](https://hub.docker.com/r/archlinux/base/) x86_64 image.这是一个arch内核的剥离版本，没有网络等等.

```
# docker pull archlinux/base

```

也可查阅 [README.md](https://github.com/archlinux/archlinux-docker/blob/master/README.md).

对于完整的arch基础，可以从下面克隆镜像并且建立你自己的镜像.

```
$ git clone [https://github.com/archlinux/archlinux-docker.git](https://github.com/archlinux/archlinux-docker.git)

```

编辑包文件让它只含有 '基础'. 运行:

```
# make docker-image

```

### Debian

下面的命令会拉取Debian镜像 [debian](https://hub.docker.com/r/_/debian/) x86_64 image.

```
# docker pull debian

```

#### 手动

用 [debootstrap](https://www.archlinux.org/packages/?name=debootstrap)建立Debian镜像:

```
# mkdir jessie-chroot
# debootstrap jessie ./jessie-chroot [http://http.debian.net/debian/](http://http.debian.net/debian/)
# cd jessie-chroot
# tar cpf - . | docker import - debian
# docker run -t -i --rm debian /bin/bash

```

## 移除docker和镜像

如果你想完全移除Docker，你可以通过下面的步骤完成:

**注意:** 不要仅仅只是复制粘贴下面的命令而不知道你在干什么.

检查正在运行的容器:

```
# docker ps

```

列出在主机运行的所有容器，为删除做准备:

```
# docker ps -a

```

停止一个运行的容器:

```
# docker stop <CONTAINER ID>

```

杀死还在运行的容器:

```
# docker kill <CONTAINER ID>

```

通过ID删除列出的所有容器:

```
# docker rm <CONTAINER ID>

```

列出所有的docker镜像:

```
# docker images

```

通过ID删除所有镜像:

```
# docker rmi <IMAGE ID>

```

删除所有docker数据 (清除目录):

```
# rm -R /var/lib/docker

```

## 有用的建议

抓取运行容器的IP地址:

 `$ docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' <container-name OR id> `  `172.17.0.37` 

每个正在运行的容器，它们的名字和相关IP地址都能被列出来在 `/etc/hosts`里用:

```
#!/usr/bin/env sh
for ID in $(docker ps -q | awk '{print $1}'); do
    IP=$(docker inspect --format="{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}" "$ID")
    NAME=$(docker ps | grep "$ID" | awk '{print $NF}')
    printf "%s %s
" "$IP" "$NAME"
done
```

## 故障排除

### docker0 网桥无法获取 IP / internet 到容器

Docker会自己启用IP转发，但是默认 [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") 会覆盖对应的sysctl设置. 在网络配置文件里设置 `IPForward=yes` . 查阅 [Internet sharing#Enable packet forwarding](/index.php/Internet_sharing#Enable_packet_forwarding "Internet sharing") 获取细节.

### 默认的允许的进程/线程数太少

如果你允许时得到下面的错误信息

```
# e.g. Java
java.lang.OutOfMemoryError: unable to create new native thread
# e.g. C, bash, ...
fork failed: Resource temporarily unavailable

```

那么你可能需要调整被systemd允许的进程数. 默认的是 500 (see `system.conf`), 这对需要允许几个容器的话太少了. [Edit](/index.php/Edit "Edit") 并添加下面片段 `docker.service` :

 `# systemctl edit docker.service` 
```
[Service]
TasksMax=infinity
```

### 初始化显卡驱动错误: devmapper

如果 *systemctl* 不能开启docker并提供了以下信息:

```
Error starting daemon: error initializing graphdriver: devmapper: Device docker-8:2-915035-pool is not a thin pool

```

那么尝试以下步骤来解决错误。停止docker服务，备份 `/var/lib/docker/` (如果需要的话), 移除`/var/lib/docker/`的内容, 尝试重启docker服务. 查阅 [GitHub issue](https://github.com/docker/docker/issues/21304) 获取更多细节.

### 无法创建到某文件的路径: 设备没有多余的空间了

如果你获取到的错误信息是像这样的话:

```
ERROR: Failed to create some/path/to/file: No space left on device

```

当创建或者运行Docker镜像时，尽管磁盘还有多余的空间。所以请确保:

*   [Tmpfs](/index.php/Tmpfs "Tmpfs") 被禁用了并且有足够的内存分配. Docker可能会尝试写入文件到 `/tmp` 但是失败了因为内存使用的限制和磁盘空间不足.
*   如果你在使用 [XFS (简体中文)](/index.php/XFS_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "XFS (简体中文)"), 你可能得从相关入口移除 `noquota` 挂载选项在 `/etc/fstab`里 (通常是 `/tmp` 和/或 `/var/lib/docker` 在的地方). 查阅 [Disk quota](/index.php/Disk_quota "Disk quota") 获取更多信息, 特别是你计划使用和调整 `overlay2` Docker 存储驱动.
*   XFS 的配额挂载选项在文件系统重新挂载时 (`uquota`, `gquota`, `prjquota`, 等等.) 失败了. 为了为root文件系统启用配额挂载选项必须作为 [Kernel parameters (简体中文)](/index.php/Kernel_parameters_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernel parameters (简体中文)") `rootflags=`传递到initramfs. 之后, 它就不应该在 `/etc/fstab`中的挂载选项中列出root (`/`) 文件系统.

**注意:** XFS配额和标准Linux[Disk quota](/index.php/Disk_quota "Disk quota"), [[1]](http://inai.de/linux/adm_quota) 是有区别的。这里值得一读.

## 查阅更多

*   [Official website](https://www.docker.com)
*   [Arch Linux on docs.docker.com](https://docs.docker.com/engine/installation/linux/archlinux/)
*   [Are Docker containers really secure?](http://opensource.com/business/14/7/docker-security-selinux) — opensource.com