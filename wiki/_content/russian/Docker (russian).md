Ссылки по теме

*   [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn")
*   [Linux Containers](/index.php/Linux_Containers "Linux Containers")
*   [Lxc-systemd](/index.php/Lxc-systemd "Lxc-systemd")
*   [Vagrant](/index.php/Vagrant "Vagrant")

[Docker](http://www.docker.io) — это утилита для упаковки, загрузки и запуска любых приложений через легковесный контейнер.

## Contents

*   [1 Установка](#Установка)
*   [2 Настройка](#Настройка)
    *   [2.1 Storage driver](#Storage_driver)
    *   [2.2 Remote API](#Remote_API)
        *   [2.2.1 Remote API с systemd](#Remote_API_с_systemd)
    *   [2.3 Конфигурация сокета демона](#Конфигурация_сокета_демона)
    *   [2.4 Proxies](#Proxies)
        *   [2.4.1 Конфигурация Proxy](#Конфигурация_Proxy)
        *   [2.4.2 Конфигурация контейнера](#Конфигурация_контейнера)
    *   [2.5 Конфигурация DNS](#Конфигурация_DNS)
    *   [2.6 Запуск Docker с сетью, заданной вручную, в systemd-networkd](#Запуск_Docker_с_сетью,_заданной_вручную,_в_systemd-networkd)
    *   [2.7 Расположение образов](#Расположение_образов)
    *   [2.8 Insecure registries](#Insecure_registries)
*   [3 Docker 0.9.0 — 1.2.x и LXC](#Docker_0.9.0_—_1.2.x_и_LXC)
*   [4 Skype](#Skype)
*   [5 Сборка образа i686](#Сборка_образа_i686)
    *   [5.1 Образ ArchLinux](#Образ_ArchLinux)
    *   [5.2 Образ Debian](#Образ_Debian)
*   [6 Смотрите также](#Смотрите_также)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [docker](https://www.archlinux.org/packages/?name=docker), доступный в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"). Для i686 установите [docker-git](https://aur.archlinux.org/packages/docker-git/) из [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)"). Затем [включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") и [запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") службу `docker.service` и проверьте ее работу:

```
 # docker info

```

Обратите внимание, что запуск службы Docker может завершиться сбоем, если у вас есть активное VPN-соединение из-за конфликтов IP между VPN и сетевым мостом и оверлейной сетью Docker. Если это так, попробуйте отключить VPN перед запуском службы Docker. Вы можете переподключить VPN сразу после этого. [Вы также можете попытаться разрешить конфликт сетей.](https://stackoverflow.com/questions/45692255/how-make-openvpn-work-with-docker)

Если вы хотите иметь возможность запускать docker как обычный пользователь, добавьте его в `docker` [user group](/index.php/User_group "User group") и перелогиньтесь:

```
# gpasswd -a *user* docker

```

**Важно:** Любой, кто добавлен в группу `docker`, имеет права, эквивалентные правам суперпользователя. Больше информации [здесь](https://github.com/docker/docker/issues/9976) и [здесь](https://docs.docker.com/engine/security/security/).

**Примечание:** По состоянию на [linux](https://www.archlinux.org/packages/?name=linux) 4.15.0-1 *vsyscalls*, которые требуются определенными программами в контейнерах (такими как *apt-get*), по умолчанию отключены в конфигурации ядра. Чтобы включить их снова, добавьте`vsyscall=emulate` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"). Больше информации в [FS#57336](https://bugs.archlinux.org/task/57336).

## Настройка

### Storage driver

Docker storage driver (или graph driver) оказывает огромное влияние на производительность. Его задача - эффективно хранить слои изображений контейнеров, то есть, когда несколько изображений совместно используют слой, только один слой использует дисковое пространство. Совместимая опция `devicemapper` предлагает неоптимальную производительность, которая просто ужасна на вращающихся дисках. Кроме того, `devicemapper` не рекомендуется в производстве.

Поскольку Arch linux поставляется с новым ядром Linux, нет смысла использовать опцию совместимости. Хороший, современный выбор - `overlay2`.

Чтобы увидеть текущий драйвер хранилища, запустите `# docker info | head`, современная установка Docker уже должна использовать `overlay2` по умолчанию.

Чтобы установить свой собственный драйвер хранилища, отредактируйте `/etc/docker/daemon.json` (создайте его, если он не существует):

 `/etc/docker/daemon.json` 
```
{
  "storage-driver": "overlay2"
}
```

После этого [restart](/index.php/Restart "Restart") докер.

Дополнительную информацию о вариантах можно найти в [руководстве пользователя](https://docs.docker.com/engine/userguide/storagedriver/selectadriver/). Для получения дополнительной информации о параметрах в `daemon.json` см. [dockerd документацию](https://docs.docker.com/engine/reference/commandline/dockerd/#daemon-configuration-file).

### Remote API

Чтобы открыть Remote API для порта `4243`, используйте:

```
# /usr/bin/dockerd -H tcp://0.0.0.0:4243 -H unix:///var/run/docker.sock

```

`-H tcp://0.0.0.0:4243` часть для открытия Remote API.

`-H unix:///var/run/docker.sock` часть для доступа к хост-машине через терминал.

#### Remote API с systemd

Чтобы запустить удаленный API с помощью docker демона, создайте [Drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet") со следующим содержимым:

 `/etc/systemd/system/docker.service.d/override.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd -H tcp://0.0.0.0:4243 -H unix:///var/run/docker.sock
```

### Конфигурация сокета демона

Демон docker по умолчанию прослушивает [Сокет домена Unix](https://en.wikipedia.org/wiki/Unix_domain_socket_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "wikipedia:Unix domain socket (Русский)"). Чтобы прослушивать определённый порт, создайте [Drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet") со следующим содержимым:

 `/etc/systemd/system/docker.socket.d/socket.conf` 
```
[Socket]
ListenStream=0.0.0.0:2375
```

### Proxies

#### Конфигурация Proxy

Создайте [Drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet") со следующим содержанием:

 `/etc/systemd/system/docker.service.d/proxy.conf` 
```
[Service]
Environment="HTTP_PROXY=192.168.1.1:8080"
Environment="HTTPS_PROXY=192.168.1.1:8080"
```

**Примечание:** Это предполагает что `192.168.1.1` ваш прокси-сервер, не используйте `127.0.0.1`.

Убедитесь, что конфигурация была загружена:

 `# systemctl show docker --property Environment`  `Environment=HTTP_PROXY=192.168.1.1:8080 HTTPS_PROXY=192.168.1.1:8080` 

#### Конфигурация контейнера

Настройки в файле `docker.service` не будут применены к контейнерам. Чтобы достичь этого, вы должны установить `ENV` переменные в `Dockerfile` так:

```
FROM base/archlinux
ENV http_proxy="http://192.168.1.1:3128"
ENV https_proxy="https://192.168.1.1:3128"

```

[Docker](https://docs.docker.com/engine/reference/builder/#env) предоставляет подробную информацию о конфигурации через `ENV` в Dockerfile.

### Конфигурация DNS

По умолчанию docker создаёт `resolv.conf` в контейнере с `/etc/resolv.conf` на хост-машине, отфильтровывая локальные адреса (например, `127.0.0.1`). Если это приводит к пустому файлу, тогда используются [Google DNS серверы](https://developers.google.com/speed/public-dns/). Если вы используете службу типа [dnsmasq](/index.php/Dnsmasq "Dnsmasq") для предоставления разрешения имен, вам может потребоваться добавить запись в `/etc/resolv.conf` для сетевого интерфейса докера, чтобы она не отфильтровывалась.

### Запуск Docker с сетью, заданной вручную, в systemd-networkd

Если вы вручную конфигурируете свою сеть, используя [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") версии **220 или выше**, контейнеры, которые вы запускаете с помощью Docker, могут не иметь доступа к вашей сети. Начиная с версии 220, параметр переадресации для данной сети (`net.ipv4.conf.<Interface>.forwarding`) по умолчанию равен `off`. Этот параметр запрещает переадресацию IP. Он также конфликтует с Docker, который включает параметр `net.ipv4.conf.all.forwarding` внутри контейнера.

Обходной путь - отредактировать файл `<interface>.network` в `/etc/systemd/network/`, добавив `IPForward=kernel` на хосте Docker:

 `/etc/systemd/network/<interface>.network` 
```
[Network]
...
IPForward=kernel
...
```

Эта конфигурация разрешает переадресацию IP из контейнера, как и ожидалось.

### Расположение образов

По умолчанию Docker образы расположены в `/var/lib/docker`. Они могут быть перемещены в другие разделы. Во-первых, [остановите](/index.php/%D0%9E%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Остановите") `docker.service`.

Если вы запустили Docker образы, вам необходимо убедиться, что они полностью размонтированы. После этого вы можете переместить изображения из `/var/lib/docker` в целевой путь.

Затем добавьте [Drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet") для `docker.service`, добавив параметр `--data-root` в `ExecStart`:

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

## Docker 0.9.0 — 1.2.x и LXC

Начиная с версии 0.9.0, Docker предоставляет новый способ запуска контейнеров без необходимости в LXC, называемый *libcontainer*.

LXC может быть удален в ближайшем будущем, однако таким образом вы не сможете использовать `lxc-attach` с контейнерами, управляемыми Docker 0.9.0+ по умолчанию ([запрос 5797](https://github.com/docker/docker/pull/5797)). Для этого потребуется запускать службу Docker с параметром `-e lxc`.

Вы можете создать файл с именем `lxc.conf` в `/etc/systemd/system/docker.service.d/` со следующим содержимым:

```
[Service]
ExecStart=
ExecStart=/usr/bin/docker -d -e lxc

```

## Skype

Смотрите [Skype#Docker](/index.php/Skype#Docker "Skype").

## Сборка образа i686

Для архитектуры i686, мы **не** можем использовать образ x86_64, полученный с помощью следующей команды:

```
# docker pull base/archlinux

```

### Образ ArchLinux

Вместо этого, посетите [реестр base/archlinux](https://registry.hub.docker.com/u/base/archlinux/) и перейдите по ссылке `mkimage-arch.sh` для скачивания `mkimage-arch.sh` и `mkimage-arch-pacman.conf`. Затем сделайте скрипт исполняемым:

```
$ chmod +x mkimage-arch.sh

```

и выполните следущее:

```
# LC_ALL=C ./mkimage-arch.sh # LC_ALL=C потому что скрипт парсит вывод консоли

```

Скрипт проверит наличие необходимых утилит. В случае их отсутствия будет предложено их установить.

```
$ docker run -t -i --rm archlinux /bin/bash # для запуска

```

Для медленных сетевых подключений и/или на слабых машинах можно увеличить тайм-аут сборки:

```
$ sed -i 's/timeout 60/timeout 120/' mkimage-arch.sh

```

### Образ Debian

Собрать образ Debian можно с помощью [debootstrap](https://www.archlinux.org/packages/?name=debootstrap) из [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)"):

```
$ mkdir wheezy-chroot
# debootstrap wheezy ./wheezy-chroot [http://http.debian.net/debian/](http://http.debian.net/debian/)
$ cd wheezy-chroot
# tar cpf - . | docker import - debian
$ docker run -t -i --rm debian /bin/bash

```

## Смотрите также

*   [Official website](https://www.docker.com)
*   [Arch Linux на docs.docker.com](https://docs.docker.com/engine/installation/linux/archlinux/)
*   [Are Docker containers really secure?](http://opensource.com/business/14/7/docker-security-selinux) — opensource.com
*   [Arch Linux Docker Tutorial на linuxhint.com](https://linuxhint.com/arch-linux-docker-tutorial/)