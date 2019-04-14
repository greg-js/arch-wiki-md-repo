Ссылки по теме

*   [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn")
*   [Linux Containers](/index.php/Linux_Containers "Linux Containers")
*   [Vagrant](/index.php/Vagrant "Vagrant")

[Docker](https://en.wikipedia.org/wiki/ru:Docker "wikipedia:ru:Docker") — утилита для упаковки, загрузки и запуска любых приложений в легковесных контейнерах.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Настройка](#Настройка)
    *   [2.1 Драйвер хранения](#Драйвер_хранения)
    *   [2.2 Remote API](#Remote_API)
        *   [2.2.1 Remote API с systemd](#Remote_API_с_systemd)
    *   [2.3 Конфигурация сокета демона](#Конфигурация_сокета_демона)
    *   [2.4 Прокси](#Прокси)
        *   [2.4.1 Конфигурация прокси](#Конфигурация_прокси)
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
    *   [6.3 Ошибка инициализации графического драйвера: devmapper](#Ошибка_инициализации_графического_драйвера:_devmapper)
    *   [6.4 Failed to create some/path/to/file: No space left on device](#Failed_to_create_some/path/to/file:_No_space_left_on_device)
    *   [6.5 Неверная ссылка между устройствами в ядре 4.19.1](#Неверная_ссылка_между_устройствами_в_ядре_4.19.1)
    *   [6.6 Отсутствие CPUACCT в docker с Linux-ck](#Отсутствие_CPUACCT_в_docker_с_Linux-ck)
*   [7 Docker 0.9.0 — 1.2.x и LXC](#Docker_0.9.0_—_1.2.x_и_LXC)
*   [8 Смотрите также](#Смотрите_также)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [docker](https://www.archlinux.org/packages/?name=docker) или [docker-git](https://aur.archlinux.org/packages/docker-git/), версию для разработки. Затем [включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") и [запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") службу `docker.service` и проверьте ее работу:

```
 # docker info

```

Обратите внимание, что запуск службы Docker может завершиться сбоем, если имеется активное VPN-соединение. Это происходит из-за IP-конфликтов между сетевыми мостами и оверлейными сетями VPN и Docker. Если это так, попробуйте отключить VPN перед запуском службы Docker. Вы можете переподключить VPN сразу после этого. [Вы также можете попытаться разрешить конфликт сетей.](https://stackoverflow.com/questions/45692255/how-make-openvpn-work-with-docker)

Если требуется запуск Docker от имени обычного пользователя, добавьте его в [группу пользователей](/index.php/Users_and_groups_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Управление_группами "Users and groups (Русский)") `docker`:

```
# gpasswd -a *user* docker

```

**Важно:** Каждый пользователь в группе `docker` имеет права, равноценные правам суперпользователя. Больше информации [здесь](https://github.com/docker/docker/issues/9976) и [здесь](https://docs.docker.com/engine/security/security/).

## Настройка

### Драйвер хранения

Драйвер хранения Docker (storage driver или graph driver) значительно влияет на производительность. Его задача — эффективно хранить слои образов контейнеров, то есть когда несколько образов совместно используют слой, только один слой использует дисковое пространство. Совместимая опция `devicemapper` предлагает неоптимальную производительность, которая просто ужасна на вращающихся дисках. Кроме того, `devicemapper` не рекомендуется использовать в промышленной среде.

Поскольку Arch Linux поставляется с новыми ядрами Linux, нет смысла использовать опцию совместимости. Хороший, современный выбор — `overlay2`.

Выполните `# docker info | head`, чтобы увидеть текущий драйвер хранилища. Новые установки Docker уже должны использовать `overlay2` по умолчанию.

Отредактируйте файл `/etc/docker/daemon.json` (создайте его, если он не существует), чтобы изменить драйвер хранения:

 `/etc/docker/daemon.json` 
```
{
  "storage-driver": "overlay2"
}
```

После чего [перезапустите](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Перезапустите") Docker.

Дополнительную информацию о доступных опциях можно найти в [руководстве пользователя](https://docs.docker.com/engine/userguide/storagedriver/selectadriver/). Также см. [документацию dockerd](https://docs.docker.com/engine/reference/commandline/dockerd/#daemon-configuration-file) для получения информации о параметрах `daemon.json`.

### Remote API

Используйте следующую команду, чтобы вручную открыть порт `4243` для Remote API:

```
# /usr/bin/dockerd -H tcp://0.0.0.0:4243 -H unix:///var/run/docker.sock

```

`-H tcp://0.0.0.0:4243` — часть для открытия Remote API.

`-H unix:///var/run/docker.sock` — часть для доступа к хост-машине через терминал.

#### Remote API с systemd

Чтобы запустить Remote API с помощью демона Docker, создайте [Drop-in сниппет](/index.php/Drop-in_%D1%81%D0%BD%D0%B8%D0%BF%D0%BF%D0%B5%D1%82 "Drop-in сниппет") со следующим содержимым:

 `/etc/systemd/system/docker.service.d/override.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd -H tcp://0.0.0.0:4243 -H unix:///var/run/docker.sock
```

### Конфигурация сокета демона

Демон *docker* по умолчанию прослушивает [Unix-сокет](https://en.wikipedia.org/wiki/ru:%D0%A1%D0%BE%D0%BA%D0%B5%D1%82_%D0%B4%D0%BE%D0%BC%D0%B5%D0%BD%D0%B0_Unix "wikipedia:ru:Сокет домена Unix"). Чтобы прослушивать определённый порт, создайте [Drop-in сниппет](/index.php/Drop-in_%D1%81%D0%BD%D0%B8%D0%BF%D0%BF%D0%B5%D1%82 "Drop-in сниппет") со следующим содержимым:

 `/etc/systemd/system/docker.socket.d/socket.conf` 
```
[Socket]
ListenStream=0.0.0.0:2375
```

### Прокси

#### Конфигурация прокси

Создайте [Drop-in сниппет](/index.php/Drop-in_%D1%81%D0%BD%D0%B8%D0%BF%D0%BF%D0%B5%D1%82 "Drop-in сниппет") со следующим содержанием:

 `/etc/systemd/system/docker.service.d/proxy.conf` 
```
[Service]
Environment="HTTP_PROXY=192.168.1.1:8080"
Environment="HTTPS_PROXY=192.168.1.1:8080"
```

**Примечание:** Предполагается, что прокси-сервер имеет адрес `192.168.1.1`, не используйте `127.0.0.1`.

Убедитесь, что конфигурация была загружена:

 `# systemctl show docker --property Environment`  `Environment=HTTP_PROXY=192.168.1.1:8080 HTTPS_PROXY=192.168.1.1:8080` 

#### Конфигурация контейнера

Настройки в файле `docker.service` не применяются к контейнерам. Для этого необходимо задать переменные `ENV` в `Dockerfile` следующим образом:

```
FROM base/archlinux
ENV http_proxy="http://192.168.1.1:3128"
ENV https_proxy="https://192.168.1.1:3128"

```

[Docker](https://docs.docker.com/engine/reference/builder/#env) предоставляет подробную информацию о конфигурации с помощью `ENV` в Dockerfile.

### Конфигурация DNS

По умолчанию docker создаёт `resolv.conf` в контейнере с `/etc/resolv.conf` на хост-машине, отфильтровывая локальные адреса (например, `127.0.0.1`). Если это приводит к пустому файлу, тогда используются [Google DNS серверы](https://developers.google.com/speed/public-dns/). Если вы используете службу типа [dnsmasq](/index.php/Dnsmasq "Dnsmasq") для предоставления разрешения имен, вам может потребоваться добавить запись в `/etc/resolv.conf` для сетевого интерфейса докера, чтобы она не отфильтровывалась.

### Запуск Docker с сетью, заданной вручную, в systemd-networkd

Если вы вручную конфигурируете свою сеть, используя [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") версии **220 или выше**, контейнеры, которые вы запускаете с помощью Docker, могут не иметь доступа к вашей сети. Начиная с версии 220, параметр переадресации для данной сети (`net.ipv4.conf.<Interface>.forwarding`) по умолчанию равен `off`. Этот параметр запрещает переадресацию IP. Он также конфликтует с Docker, который включает параметр `net.ipv4.conf.all.forwarding` внутри контейнера.

Обходной путь — отредактировать файл `<interface>.network` в `/etc/systemd/network/`, добавив `IPForward=kernel` на хосте Docker:

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

Затем добавьте [Drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet") для `docker.service`, добавив параметр `-g` в `ExecStart`:

 `/etc/systemd/system/docker.service.d/docker-storage.conf` 
```
[Service]
ExecStart= 
ExecStart=/usr/bin/dockerd -g=*/path/to/new/location/docker* -H fd://
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

### Ошибка инициализации графического драйвера: devmapper

Если *systemctl* не запускает Docker и выдает ошибку::

```
Error starting daemon: error initializing graphdriver: devmapper: Device docker-8:2-915035-pool is not a thin pool

```

Попробуйте выполнить следующие действия, чтобы устранить ошибку. Остановите службу, сделайте резервную копию `/var/lib/docker/` (если это необходимо), удалите содержимое `/var/lib/docker/`, и попробуйте запустить службу. Смотрите [описание проблемы на GitHub](https://github.com/docker/docker/issues/21304) для более детальной информации.

### Failed to create some/path/to/file: No space left on device

Если вы получаете сообщение об ошибке, подобное этому:

```
ERROR: Failed to create some/path/to/file: No space left on device

```

При создании или исполнении Docker образа, даже если у вас достаточно свободного места на диске, убедитесь, что:

*   [Tmpfs](/index.php/Tmpfs "Tmpfs") отключен или имеет достаточно памяти. Docker может пытаться записать файлы в `/tmp` но терпит неудачу из-за ограничений в использовании памяти, а не дискового пространства.
*   Если вы используете [XFS](/index.php/XFS "XFS"), Вы можете удалить опцию монтирования `noquota` из соответствующих записей в `/etc/fstab` (обычно, где находятся `/tmp` и/или `/var/lib/docker`). Для получения дополнительной информации обратитесь к [Disk quota](/index.php/Disk_quota "Disk quota"), особенно, если вы планируете использовать и изменить размер `overlay2` Docker хранилища.
*   Варианты установки монтирования квоты XFS (`uquota`, `gquota`, `prjquota`, и т.д.) выдают ошибку при перемонтировании файловой системы.

Чтобы включить квоту для корневой файловой системы, параметр монтирования должен быть передан как [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `rootflags=`. Впоследствии его не следует указывать среди параметров монтирования в `/etc/fstab` для корневой файловой системы (`/`).

**Примечание:** Есть некоторые отличия XFS Quota по сравнению со стандартом Linux [Disk quota](/index.php/Disk_quota "Disk quota"), [[1]](http://inai.de/linux/adm_quota) рекомендуется к прочтению.

### Неверная ссылка между устройствами в ядре 4.19.1

Если команды типа *dpkg* не запускаются в Docker, например:

```
dpkg: error: error creating new backup file '/var/lib/dpkg/status-old': Invalid cross-device link

```

Либо добавьте `overlay.metacopy=N` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") или поставьте версию 4.18.x, в которой [эта проблема](https://github.com/docker/for-linux/issues/480) решена. Больше информации в [Arch forum](https://bbs.archlinux.org/viewtopic.php?id=241866).

### Отсутствие CPUACCT в docker с Linux-ck

В новых версиях [Linux-ck](/index.php/Linux-ck "Linux-ck") ([some experienced](https://aur.archlinux.org/packages/linux-ck#comment-677316) кажется общей проблемой в версиях 4.19, 4.20), было сделано изменение в MuQSS, которое отключает опцию в ядре `CONFIG_CGROUP_CPUACCT`, что делает «некоторое» использование docker (`run` или `build`) вызывающим следующую ошибку:

 `$ docker run --rm hello-world`  `docker: Error response from daemon: unable to find "cpuacct" in controller set: unknown.` 

Эта ошибка, похоже, не влияет на демон docker, только на контейнеры. Читайте больше в [Linux-ck#CPUACCT отсутствует в docker](/index.php/Linux-ck#CPUACCT_отсутствует_в_docker "Linux-ck").

## Docker 0.9.0 — 1.2.x и LXC

Начиная с версии 0.9.0, Docker предоставляет новый способ запуска контейнеров без необходимости в LXC, называемый *libcontainer*.

LXC может быть удален в ближайшем будущем, однако таким образом вы не сможете использовать `lxc-attach` с контейнерами, управляемыми Docker 0.9.0+ по умолчанию ([запрос 5797](https://github.com/docker/docker/pull/5797)). Для этого потребуется запускать службу Docker с параметром `-e lxc`.

Вы можете создать файл с именем `lxc.conf` в `/etc/systemd/system/docker.service.d/` со следующим содержимым:

```
[Service]
ExecStart=
ExecStart=/usr/bin/docker -d -e lxc

```

## Смотрите также

*   [Официальный сайт](https://www.docker.com)
*   [Arch Linux на docs.docker.com](https://docs.docker.com/engine/installation/linux/archlinux/)
*   [Are Docker containers really secure?](http://opensource.com/business/14/7/docker-security-selinux) — opensource.com