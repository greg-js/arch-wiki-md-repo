Ссылки по теме

*   [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn")
*   [Linux Containers](/index.php/Linux_Containers "Linux Containers")
*   [Lxc-systemd](/index.php/Lxc-systemd "Lxc-systemd")
*   [Vagrant](/index.php/Vagrant "Vagrant")

[Docker](http://www.docker.io) — это утилита для упаковки, загрузки и запуска любых приложений через легковесный контейнер.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

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
    *   [2.8 Небезопасные реестры](#Небезопасные_реестры)
*   [3 Образы](#Образы)
    *   [3.1 Arch Linux](#Arch_Linux)
    *   [3.2 Debian](#Debian)
        *   [3.2.1 Создание образа вручную](#Создание_образа_вручную)
*   [4 Удаление Docker и образов](#Удаление_Docker_и_образов)
*   [5 Полезные советы](#Полезные_советы)
*   [6 Устранение неполадок](#Устранение_неполадок)
    *   [6.1 docker0 Bridge не получает IP адреса/нет доступа к Интернету в контейнерах](#docker0_Bridge_не_получает_IP_адреса/нет_доступа_к_Интернету_в_контейнерах)
    *   [6.2 Слишком низкое значение количества процессов/потоков по умолчанию](#Слишком_низкое_значение_количества_процессов/потоков_по_умолчанию)
    *   [6.3 Error initializing graphdriver: devmapper](#Error_initializing_graphdriver:_devmapper)
    *   [6.4 Failed to create some/path/to/file: No space left on device](#Failed_to_create_some/path/to/file:_No_space_left_on_device)
    *   [6.5 Invalid cross-device link in kernel 4.19.1](#Invalid_cross-device_link_in_kernel_4.19.1)
    *   [6.6 CPUACCT missing in docker with Linux-ck](#CPUACCT_missing_in_docker_with_Linux-ck)
*   [7 Docker 0.9.0 — 1.2.x и LXC](#Docker_0.9.0_—_1.2.x_и_LXC)
*   [8 Сборка образа i686](#Сборка_образа_i686)
    *   [8.1 Образ ArchLinux](#Образ_ArchLinux)
    *   [8.2 Образ Debian](#Образ_Debian)
*   [9 Смотрите также](#Смотрите_также)

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

### Небезопасные реестры

Если вы решите использовать самозаверенный сертификат для своего личного реестра, Docker откажется использовать его, пока вы не заявите, что доверяете ему. Добавьте [Drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet") для `docker.service`, добавив `--insecure-registry` параметр в `dockerd`:

 `/etc/systemd/system/docker.service.d/override.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd -H fd:// --insecure-registry my.registry.name:5000
```

## Образы

### Arch Linux

Следующая команда выгружает [archlinux/base](https://hub.docker.com/r/archlinux/base/) x86_64 образ. Это урезанная версия ядра Arch без сети и т.д.

```
# docker pull archlinux/base

```

Смотрите также [README.md](https://github.com/archlinux/archlinux-docker/blob/master/README.md).

Для полноценного образа Arch, клонируйте репозиторий и создайте свой собственный образ.

```
$ git clone [https://github.com/archlinux/archlinux-docker.git](https://github.com/archlinux/archlinux-docker.git)

```

Отредактируйте файл `packages` так, чтобы он содержал только «base». Затем запустите:

```
# make docker-image

```

### Debian

Следующая команда выгружает [debian](https://hub.docker.com/r/_/debian/) x86_64 образ.

```
# docker pull debian

```

#### Создание образа вручную

Создайте образ Debian с [debootstrap](https://www.archlinux.org/packages/?name=debootstrap):

```
# mkdir jessie-chroot
# debootstrap jessie ./jessie-chroot [http://http.debian.net/debian/](http://http.debian.net/debian/)
# cd jessie-chroot
# tar cpf - . | docker import - debian
# docker run -t -i --rm debian /bin/bash

```

## Удаление Docker и образов

Если вы хотите полностью удалить Docker, вам следует выполнить следующие шаги:

**Примечание:** Не копируйте бездумно эти команды, не убедившись, что вы знаете, что делаете.

Выдать список работающих контейнеров:

```
# docker ps

```

Выдать список всех контейнеров, запущенных на хосте для удаления:

```
# docker ps -a

```

Остановить работающий контейнер:

```
# docker stop <CONTAINER ID>

```

Выполнить команду kill для всё ещё работающих контейнеров:

```
# docker kill <CONTAINER ID>

```

Удалить все контейнеры, перечисленные по ID:

```
# docker rm <CONTAINER ID>

```

Выдать список всех образов Docker:

```
# docker images

```

Удалить все образы Docker по ID:

```
# docker rmi <IMAGE ID>

```

Удалить все данные Docker (очистить каталог):

```
# rm -R /var/lib/docker

```

## Полезные советы

Чтобы получить IP адрес контейнера, выполните:

 `$ docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' <container-name OR id> `  `172.17.0.37` 

Для каждого работающего контейнера имя и соответствующий IP-адрес могут быть перечислены для использования в `/etc/hosts`:

```
#!/usr/bin/env sh
for ID in $(docker ps -q | awk '{print $1}'); do
    IP=$(docker inspect --format="{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}" "$ID")
    NAME=$(docker ps | grep "$ID" | awk '{print $NF}')
    printf "%s %s
" "$IP" "$NAME"
done
```

## Устранение неполадок

### docker0 Bridge не получает IP адреса/нет доступа к Интернету в контейнерах

Docker сам включает переадресацию IP, но по умолчанию [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") переопределяет соответствующую настройку sysctl. Установите `IPForward=yes` в настройках сети. Подробнее читайте в [Internet sharing#Enable packet forwarding](/index.php/Internet_sharing#Enable_packet_forwarding "Internet sharing").

**Примечание:** Вам может понадобится выполнить [restart](/index.php/Restart "Restart") `docker.service` каждый раз, когда Вы выполняете [restart](/index.php/Restart "Restart") `systemd-networkd.service` или `iptables.service`

### Слишком низкое значение количества процессов/потоков по умолчанию

Если вы столкнетесь с сообщениями об ошибках, похожими на следующие:

```
# e.g. Java
java.lang.OutOfMemoryError: unable to create new native thread
# e.g. C, bash, ...
fork failed: Resource temporarily unavailable

```

тогда вам может потребоваться настроить количество процессов, разрешенных systemd. Значени по умолчанию 500 (смотрите `system.conf`), что довольно мало для запуска нескольких Docker контейнеров. [Edit](/index.php/Edit "Edit") `docker.service` со следующим фрагментом:

 `# systemctl edit docker.service` 
```
[Service]
TasksMax=infinity
```

### Error initializing graphdriver: devmapper

If *systemctl* fails to start docker and provides an error:

```
Error starting daemon: error initializing graphdriver: devmapper: Device docker-8:2-915035-pool is not a thin pool

```

Then, try the following steps to resolve the error. Stop the service, back up `/var/lib/docker/` (if desired), remove the contents of `/var/lib/docker/`, and try to start the service. See the open [GitHub issue](https://github.com/docker/docker/issues/21304) for details.

### Failed to create some/path/to/file: No space left on device

If you are getting an error message like this:

```
ERROR: Failed to create some/path/to/file: No space left on device

```

when building or running a Docker image, even though you do have enough disk space available, make sure:

*   [Tmpfs](/index.php/Tmpfs "Tmpfs") is disabled or has enough memory allocation. Docker might be trying to write files into `/tmp` but fails due to restrictions in memory usage and not disk space.
*   If you are using [XFS](/index.php/XFS "XFS"), you might want to remove the `noquota` mount option from the relevant entries in `/etc/fstab` (usually where `/tmp` and/or `/var/lib/docker` reside). Refer to [Disk quota](/index.php/Disk_quota "Disk quota") for more information, especially if you plan on using and resizing `overlay2` Docker storage driver.
*   XFS quota mount options (`uquota`, `gquota`, `prjquota`, etc.) fail during re-mount of the file system. To enable quota for root file system, the mount option must be passed to initramfs as a [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `rootflags=`. Subsequently, it should not be listed among mount options in `/etc/fstab` for the root (`/`) filesystem.

**Note:** There are some differences of XFS Quota compared to standard Linux [Disk quota](/index.php/Disk_quota "Disk quota"), [[1]](http://inai.de/linux/adm_quota) may be worth reading.

### Invalid cross-device link in kernel 4.19.1

If commands like *dpkg* fail to run in docker, e.g:

```
dpkg: error: error creating new backup file '/var/lib/dpkg/status-old': Invalid cross-device link

```

Either add a `overlay.metacopy=N` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") or downgrade to 4.18.x until [this issue](https://github.com/docker/for-linux/issues/480) is resolved. More info in the [Arch forum](https://bbs.archlinux.org/viewtopic.php?id=241866).

### CPUACCT missing in docker with Linux-ck

In newer versions of [Linux-ck](/index.php/Linux-ck "Linux-ck") ([some experienced](https://aur.archlinux.org/packages/linux-ck#comment-677316) with 4.19, 4.20 seems general), a change to the MuQSS was made that disables the `CONFIG_CGROUP_CPUACCT` option from the kernel, which makes *some* usage of docker (`run` or `build`) to produce the following error:

 `$ docker run --rm hello-world`  `docker: Error response from daemon: unable to find "cpuacct" in controller set: unknown.` 

This error does not seems to affect the docker daemon, just containers. Read more on [Linux-ck#CPUACCT missing in docker](/index.php/Linux-ck#CPUACCT_missing_in_docker "Linux-ck").

## Docker 0.9.0 — 1.2.x и LXC

Начиная с версии 0.9.0, Docker предоставляет новый способ запуска контейнеров без необходимости в LXC, называемый *libcontainer*.

LXC может быть удален в ближайшем будущем, однако таким образом вы не сможете использовать `lxc-attach` с контейнерами, управляемыми Docker 0.9.0+ по умолчанию ([запрос 5797](https://github.com/docker/docker/pull/5797)). Для этого потребуется запускать службу Docker с параметром `-e lxc`.

Вы можете создать файл с именем `lxc.conf` в `/etc/systemd/system/docker.service.d/` со следующим содержимым:

```
[Service]
ExecStart=
ExecStart=/usr/bin/docker -d -e lxc

```

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