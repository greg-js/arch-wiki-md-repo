[Docker](http://www.docker.io) 提供使用者包裝、搬移、執行任意程式作為一個輕量級容器。

## Contents

*   [1 安裝](#.E5.AE.89.E8.A3.9D)
*   [2 設定](#.E8.A8.AD.E5.AE.9A)
    *   [2.1 代理伺服器](#.E4.BB.A3.E7.90.86.E4.BC.BA.E6.9C.8D.E5.99.A8)
        *   [2.1.1 Docker Daemon 設定](#Docker_Daemon_.E8.A8.AD.E5.AE.9A)
        *   [2.1.2 Container 設定](#Container_.E8.A8.AD.E5.AE.9A)
    *   [2.2 Daemon Socket 設定](#Daemon_Socket_.E8.A8.AD.E5.AE.9A)
*   [3 Docker與LXC](#Docker.E8.88.87LXC)
*   [4 映像檔](#.E6.98.A0.E5.83.8F.E6.AA.94)
    *   [4.1 Arch Linux](#Arch_Linux)
        *   [4.1.1 x86_64](#x86_64)
        *   [4.1.2 i686](#i686)
        *   [4.1.3 建置映像檔](#.E5.BB.BA.E7.BD.AE.E6.98.A0.E5.83.8F.E6.AA.94)
    *   [4.2 Debian](#Debian)
*   [5 快照倉庫](#.E5.BF.AB.E7.85.A7.E5.80.89.E5.BA.AB)
*   [6 提示](#.E6.8F.90.E7.A4.BA)
*   [7 常見問題](#.E5.B8.B8.E8.A6.8B.E5.95.8F.E9.A1.8C)
    *   [7.1 Docker Info顯示錯誤訊息](#Docker_Info.E9.A1.AF.E7.A4.BA.E9.8C.AF.E8.AA.A4.E8.A8.8A.E6.81.AF)
    *   [7.2 在BTRFS檔案系統中刪除 Docker 映像檔](#.E5.9C.A8BTRFS.E6.AA.94.E6.A1.88.E7.B3.BB.E7.B5.B1.E4.B8.AD.E5.88.AA.E9.99.A4_Docker_.E6.98.A0.E5.83.8F.E6.AA.94)
    *   [7.3 Container中的docker0 Bridge無法取得IP/無法存取網路](#Container.E4.B8.AD.E7.9A.84docker0_Bridge.E7.84.A1.E6.B3.95.E5.8F.96.E5.BE.97IP.2F.E7.84.A1.E6.B3.95.E5.AD.98.E5.8F.96.E7.B6.B2.E8.B7.AF)
*   [8 參考資料](#.E5.8F.83.E8.80.83.E8.B3.87.E6.96.99)

## 安裝

你可以透過官方套件庫安裝 [docker](https://www.archlinux.org/packages/?name=docker) 套件：

```
# pacman -S docker

```

或是從[AUR](/index.php/AUR "AUR")安裝 [docker-git](https://aur.archlinux.org/packages/docker-git/) 套件：

```
# git clone [https://aur.archlinux.org/docker-git.git](https://aur.archlinux.org/docker-git.git)
# cd docker-git
# makepkg -sri

```

接著，你可以[啟動](/index.php/Start "Start") `docker.service` 並驗證安裝是否成功：

```
# systemctl start docker.service
# docker info

```

如果你想用你的使用者帳戶(非root帳戶)來使用Docker，把你的帳戶加到Docker的群組中：

```
# gpasswd -a _user_ docker

```

記得重新登入來套用新權限，或者你可以用這個指令讓現在的使用者階段套用新群組：

```
$ newgrp docker

```

## 設定

### 代理伺服器

Proxy設定有兩個地方：一個是主機端的Docker Daemon設定，另一個是套用在Container上的Proxy設定。

#### Docker Daemon 設定

將 `/usr/lib/systemd/system/docker.service` 複製到 `/etc/systemd/system/docker.service`。

接著編輯 `/etc/systemd/system/docker.service`, 將 `http_proxy` 替換成你的 Proxy伺服器。

```
[Service]
Environment="http_proxy=192.168.1.1:3128"

```

**注意:** 這裡的 `192.168.1.1` 是你的Proxy伺服器位址，千萬不要設定成 `127.0.0.1`.

#### Container 設定

在 `docker.service` 中的設定並不會套用到Container中，你必須在Container中的 `Dockerfile` 設定 `ENV` ，如：

```
 FROM base/archlinux
 ENV http_proxy="http://192.168.1.1:3128"
 ENV https_proxy="https://192.168.1.1:3128"

```

你可以在 [Docker#env](https://docs.docker.com/reference/builder/#env) 找到更詳細的資料。

### Daemon Socket 設定

_Docker Daemon_ 預設會監聽 [Unix socket](https://en.wikipedia.org/wiki/Unix_domain_socket "wikipedia:Unix domain socket")。如果要讓他監聽特定的通訊埠號，可以修改 `/etc/systemd/system/docker.socket` 中的 `ListenStream` 為想要的通訊埠號：

```
[Socket]
ListenStream=0.0.0.0:2375

```

## Docker與LXC

0.9.0 版以後的 Docker 提供了一個不依賴LXC的函式庫的新Container啟動方式，稱為_libcontainer_。

LXC的驅動及設定有可能也在近期移除，因此，使用者將無法在0.9.0版以上的Docker使用 `lxc-attach` 管理Container，它需要 `-e lxc` 作為 Docker daemon 執行時的參數。

你可以在 `/etc/systemd/system/docker.service.d/` 建立 `lxc.conf`，並新增以下內容：

```
[Service]
ExecStart=
ExecStart=/usr/bin/docker -d -e lxc

```

**註記:** 你可以參照[Remove lxc exec driver #5797](https://github.com/docker/docker/pull/5797)來了解這一段的內容。

## 映像檔

### Arch Linux

#### x86_64

用這個個指令來下載 x86_64 的映像檔。

```
# docker pull base/archlinux

```

#### i686

在 Docker Registry 中的 Arch Linux 映像檔只提供 x86_64 版本，i686版本請參考下面章節自行編譯。

#### 建置映像檔

首先，到 [docker base/archlinux registry](https://registry.hub.docker.com/u/base/archlinux/) 點擊 `mkimage-arch.sh` 下載 `mkimage-arch.sh` 和 `mkimage-arch-pacman.conf` 到相同目錄。

接著，賦予它執行權限並執行它。

```
$ chmod +x mkimage-arch.sh
$ cp /etc/pacman.conf ./mkimage-arch-pacman.conf
$ LC_ALL=C ./mkimage-arch.sh
# docker run -t -i --rm archlinux /bin/bash

```

在電腦或網路速度較慢的環境下，你可以延長timeout時間：

```
$ sed -i 's/timeout 60/timeout 120/' mkimage-arch.sh

```

### Debian

從 [AUR](/index.php/AUR "AUR") 下載 [debootstrap](https://aur.archlinux.org/packages/debootstrap/) 以建置 Debain 的映像檔。

```
# mkdir wheezy-chroot
# debootstrap wheezy ./wheezy-chroot [http://http.debian.net/debian/](http://http.debian.net/debian/)
# cd wheezy-chroot
# tar cpf - . | docker import - debian
# docker run -t -i --rm debian /bin/bash

```

## 快照倉庫

當多個映像檔建立或更新，他們可能各自有不同的套件版本，為了讓這些Containers能夠有一致的套件版本，使用者可以使用[Docker image with a snapshot repository](https://registry.hub.docker.com/u/pritunl/archlinux/)，他允許使用者在建立之後從官方套件庫安裝套件。

```
$ docker pull pritunl/archlinux:latest
$ docker run --rm -t -i pritunl/archlinux:latest /bin/bash

```

## 提示

你可以透過這個指令擷取執行中Container的IP位址：

 `$ docker inspect --format '{{ .NetworkSettings.IPAddress }}' <container-name OR id> `  `172.17.0.37` 

## 常見問題

### Docker Info顯示錯誤訊息

如果執行 `docker info` 後收到下面的錯誤訊息：

```
 FATA[0000] Get [http:///var/run/docker.sock/v1.17/info](http:///var/run/docker.sock/v1.17/info): read unix /var/run/docker.sock: connection reset by peer. Are you trying to connect to a TLS-enabled daemon without TLS? 

```

這表示你可能沒有載入 `bridge` 模組，你可以透過執行 `lsmod` 來檢查是否載入。 如果沒有，你可以使用 `modprobe bridge` 來載入或者是重新開機(當近期有更新核心(kernel)後而沒有重新開機，請務必進行重新開機，因為Bridge模組有可能是建置在最新的核心上)。

**註記:** 您可以參考 [Docker daemon fails to start on Arch Linux with "package not installed" #6853](https://github.com/docker/docker/issues/6853) 來獲得更多資訊。

### 在BTRFS檔案系統中刪除 Docker 映像檔

當使用者在[btrfs](/index.php/Btrfs "Btrfs")檔案系統中刪除Docker映像檔時，在 `/var/lib/docker/btrfs/subvolumes/` 會殘留一個檔案大小為0的映像檔。當你嘗試刪除它時，可能會收到權限上的錯誤。

```
 # docker rm bab4ff309870
 # rm -Rf /var/lib/docker/btrfs/subvolumes/*
 rm: cannot remove '/var/lib/docker/btrfs/subvolumes/85122f1472a76b7519ed0095637d8501f1d456787be1a87f2e9e02792c4200ab': Operation not permitted

```

這是[btrfs](/index.php/Btrfs "Btrfs")建立subvolumes導致的問題，正確的刪除指令為：

```
 # btrfs subvolume delete /var/lib/docker/btrfs/subvolumes/85122f1472a76b7519ed0095637d8501f1d456787be1a87f2e9e02792c4200ab

```

### Container中的docker0 Bridge無法取得IP/無法存取網路

Docker預設是有啟用IP forwarding的，但是systemd的預設值會覆蓋掉它，你可以按照下列步驟來取消覆蓋(對所有介面有效)：

```
# cat >/etc/systemd/network/ipforward.network <<EOF
[Network]
IPForward=kernel
EOF

```

最後 [重新啟動](/index.php/Restart "Restart") `systemd-networkd` 和 `docker` 兩個服務。

```
# systemctl restart systemd-networkd.service
# systemctl restart docker.service

```

## 參考資料

*   [Arch Linux on docs.docker.com](https://docs.docker.com/installation/archlinux/)
*   [《Docker —— 從入門到實踐­》正體中文版](https://www.gitbook.com/book/philipzheng/docker_practice/details) (非官方文件)