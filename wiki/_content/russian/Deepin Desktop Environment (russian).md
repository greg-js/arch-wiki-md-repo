**Состояние перевода:** На этой странице представлен перевод статьи [Deepin Desktop Environment](/index.php/Deepin_Desktop_Environment "Deepin Desktop Environment"). Дата последней синхронизации: 26 февраля 2018\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Deepin_Desktop_Environment&diff=0&oldid=512143).

Ссылки по теме

*   [Среда рабочего стола](/index.php/%D0%A1%D1%80%D0%B5%D0%B4%D0%B0_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE_%D1%81%D1%82%D0%BE%D0%BB%D0%B0 "Среда рабочего стола")
*   [GNOME (Русский)](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)")
*   [LightDM (Русский)](/index.php/LightDM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "LightDM (Русский)")

[DDE](https://www.deepin.org/?language=ru) (Deepin Desktop Environment) является средой рабочего стола по-умолчанию для дистрибутива Linux Deepin.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Запуск Deepin Desktop Environment](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_Deepin_Desktop_Environment)
*   [3 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [3.1 Отсутствие изображение на рабочем столе после пробуждения](#.D0.9E.D1.82.D1.81.D1.83.D1.82.D1.81.D1.82.D0.B2.D0.B8.D0.B5_.D0.B8.D0.B7.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B0_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.BC_.D1.81.D1.82.D0.BE.D0.BB.D0.B5_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D1.83.D0.B6.D0.B4.D0.B5.D0.BD.D0.B8.D1.8F)
*   [4 Сообщение об ошибках](#.D0.A1.D0.BE.D0.BE.D0.B1.D1.89.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BE.D0.B1_.D0.BE.D1.88.D0.B8.D0.B1.D0.BA.D0.B0.D1.85)
*   [5 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

Чтобы получить минимальный интерфейс рабочего стола, [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") группу пакетов [deepin](https://www.archlinux.org/groups/x86_64/deepin/). Она включает в себя все основные компоненты.

Группа пакетов [deepin-extra](https://www.archlinux.org/groups/x86_64/deepin-extra/) содержит некоторые дополнительные приложения, необходимые для более удобной работы.

Чтобы иметь возможность использовать встроенную поддержку управления сетью, необходимо установить пакет [networkmanager](https://www.archlinux.org/packages/?name=networkmanager), и [запустить, включить](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.8E.D0.BD.D0.B8.D1.82.D0.BE.D0.B2 "Systemd (Русский)") службу `NetworkManager.service`.

## Запуск Deepin Desktop Environment

По-умолчанию Deepin рассчитан на работу с экранным менеджером [lightdm](https://www.archlinux.org/packages/?name=lightdm).

Чтобы использовать оригинальный экран приветствия для Deepin в lightdm, вам необходимо изменить конфигурационный файл следующим образом:

 `/etc/lightdm/lightdm.conf` 
```
[Seat:*]
...
greeter-session=lightdm-deepin-greeter
```

Для корректной работы экрана приветствия должна существовать хотя бы одна домашняя папка.

## Решение проблем

### Отсутствие изображение на рабочем столе после пробуждения

Из-за особенностей хранения FBO (Framebuffer Object) драйверами NVIDIA [[1]](https://devtalk.nvidia.com/default/topic/787748/linux/-nvidia340xx-archlinux64-gnome3-14-the-background-of-desktop-and-lockscreen-mess-after-resume-from-/post/4367179/#4367179), иногда после пробуждения отображается только белый экран и, возможно, небольшой цветовой шум. Баг исправлен в репозитории GNOME, но в Deepin он всё ещё наблюдается.

Возможным решением проблемы может быть перезапуск оконного менеджера каждый раз после пробуждения компьютера из приостановленного состояния. Этого можно достигнуть, создав следующую службу systemd:

 `/etc/systemd/system/resume@.service` 
```
[Unit]
Description=User resume actions
After=suspend.target

[Service]
User=%I
Type=simple
ExecStart=/usr/bin/deepin-wm-restart.sh

[Install]
WantedBy=suspend.target

```

Данная служба должна выполнять следующий скрипт:

 `/usr/bin/deepin-wm-restart.sh` 
```
#!/bin/bash
export DISPLAY=:0
deepin-wm --replace

```

Когда вы поместите описанные файлы в нужные каталоги, запустите сценарий следующими командами:

```
# chmod +x /usr/bin/deepin-wm-restart.sh
# systemctl enable resume@*user*
# systemctl start resume@*user* 

```

Первая команда делает скрипт, созданный тобой, исполняемым, вторая помещает службу в автозапуск при загрузке системы, а последняя сразу запускает эту службу, таким образом, ты можешь обойтись без перезагрузки системы.

## Сообщение об ошибках

При возникновении каких-либо ошибок в работе, их подробное описание и шаги по вопспроизведению можно оставить [тут](https://github.com/linuxdeepin/developer-center/issues).

## Смотрите также

*   [Официальный сайт дистрибутива Deepin](https://www.deepin.org/ru/)
*   [Сайт русского сообщества Deepin](https://mydeepin.ru/)
*   [Telegram-канал официального сообщества Deepin](https://t.me/deepin)
*   [Telegram-канал русского сообщества Deepin](https://t.me/DeepinRussia)