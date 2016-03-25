[Docker](http://www.docker.io) — это утилита для упаковки, загрузки и запуска любых приложений через легковесный контейнер.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
*   [3 Docker 0.9.0 — 1.2.x и LXC](#Docker_0.9.0_.E2.80.94_1.2.x_.D0.B8_LXC)
*   [4 Skype](#Skype)
*   [5 Сборка образа i686](#.D0.A1.D0.B1.D0.BE.D1.80.D0.BA.D0.B0_.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D0.B0_i686)
    *   [5.1 Образ ArchLinux](#.D0.9E.D0.B1.D1.80.D0.B0.D0.B7_ArchLinux)
    *   [5.2 Образ Debian](#.D0.9E.D0.B1.D1.80.D0.B0.D0.B7_Debian)
*   [6 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [docker](https://www.archlinux.org/packages/?name=docker), доступный в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"). Для i686 установите [docker-git](https://aur.archlinux.org/packages/docker-git/) из [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)"). Затем [включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") и [запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") службу `docker.service` и проверьте ее работу:

```
# docker info

```

Если необходимо запускать *docker* от обычного пользователя, добавьте его в группу `docker` и перелогиньтесь:

```
# gpasswd -a *user* docker

```

## Настройка

Отредактируйте `/etc/systemd/system/docker.service`, где `http_proxy` — ваш прокси сервер, `-g <path>` — директория docker (по умолчанию `/var/cache/docker`).

```
[Service]
Environment="http_proxy=192.168.1.1:3128"
ExecStart=
ExecStart=/usr/bin/docker -d -g /var/yourDockerDir

```

**Примечание:** Предполагается, что адрес используемого прокси-сервера `192.168.1.1`; не используйте `127.0.0.1`.

По умолчанию, демон docker принимает запросы на [доменном сокете Unix](https://en.wikipedia.org/wiki/ru:Unix_domain_socket "wikipedia:ru:Unix domain socket"). Если вы хотите, чтобы запросы принимались на сетевом порту, отредактируйте `/etc/systemd/system/docker.socket`, где `ListenStream` — сетевой адрес сокета:

```
[Socket]
ListenStream=0.0.0.0:2375

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

*   [Arch Linux на docs.docker.com](https://docs.docker.com/installation/archlinux/)