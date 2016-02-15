**RetroShare** — свободный клиент одноимённой [Friend-to-Friend](https://en.wikipedia.org/wiki/ru:Friend-to-friend "wikipedia:ru:Friend-to-friend") сети для приватного обмена файлами и сообщениями.

## Contents

*   [1 Установка из репозитория RetroShare](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B8.D0.B7_.D1.80.D0.B5.D0.BF.D0.BE.D0.B7.D0.B8.D1.82.D0.BE.D1.80.D0.B8.D1.8F_RetroShare)
*   [2 Установка из AUR](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B8.D0.B7_AUR)
*   [3 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
*   [4 Ссылки](#.D0.A1.D1.81.D1.8B.D0.BB.D0.BA.D0.B8)

## Установка из репозитория RetroShare

1\. Добавьте репозиторий пакетов, отредактировав файл _/etc/pacman.conf_:

```
[home_AsamK_RetroShare_Arch_Extra]
SigLevel = Never
Server = [http://download.opensuse.org/repositories/home:/AsamK:/RetroShare/Arch_Extra/$arch](http://download.opensuse.org/repositories/home:/AsamK:/RetroShare/Arch_Extra/$arch)

```

2\. Установите RetroShare.

```
# pacman -Syu
# pacman -S home_AsamK_RetroShare_Arch_Extra/retroshare06

```

Желательно удалить все другие сборки RetroShare с вашего компьютера.

## Установка из AUR

Текущая версия RetroShare доступна в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"). Воспользуетесь пакетом [retroshare](https://aur.archlinux.org/packages/retroshare/) для сборки последней _стабильной_ версии исходных текстов. Для этого, под root-пользователем выполните:

```
# yaourt -Sa retroshare

```

## Использование

После установки программа генерирует личный сертификат RetroShare, используя сведения, предоставленные пользователем. После этого происходит запуск программы. Так как соединения в F2F-сети устанавливаются только с доверенными участниками (пирами), то дальше пользователю необходимо обменяться сертификатом с действующим участником сети. Чтобы найти доверенных пиров, предлагается произвести обмен сертификатами с [одним из публичных чат-серверов](https://retroshare.rocks/). После успешного обмена пользователю становятся доступны чат-комнаты сети RetroShare, в том числе чат "Key Exchange", предназначенный для обмена сертификатами с участниками сети.

## Ссылки

*   [Русскоязычный сайт](http://ru.retroshare.net/)
*   [Группа ВКонтакте](https://vk.com/retroshare)