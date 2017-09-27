Ссылки по теме

*   [udev (Русский)](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)")
*   [mount (Русский)](/index.php/Mount_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Mount (Русский)")
*   [Polkit](/index.php/Polkit "Polkit")
*   [Функциональность файлового менеджера](/index.php/%D0%A4%D1%83%D0%BD%D0%BA%D1%86%D0%B8%D0%BE%D0%BD%D0%B0%D0%BB%D1%8C%D0%BD%D0%BE%D1%81%D1%82%D1%8C_%D1%84%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2%D0%BE%D0%B3%D0%BE_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80%D0%B0 "Функциональность файлового менеджера")

**Состояние перевода:** На этой странице представлен перевод статьи [Udisks](/index.php/Udisks "Udisks"). Дата последней синхронизации: 7 октября 2015\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Udisks&diff=0&oldid=403685).

[udisks](http://www.freedesktop.org/wiki/Software/udisks/) предоставляет демон *udisksd*, который реализует интерфейс [D-Bus](/index.php/D-Bus "D-Bus"), используемый для запроса и управления устройств хранения данных и инструмента командной строки *udisksctl*, используемый для запросов и использования в качестве демона.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
*   [3 Помощники монтирования](#.D0.9F.D0.BE.D0.BC.D0.BE.D1.89.D0.BD.D0.B8.D0.BA.D0.B8_.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
    *   [3.1 Devmon](#Devmon)
    *   [3.2 inotify](#inotify)
*   [4 Советы и хитрости](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.85.D0.B8.D1.82.D1.80.D0.BE.D1.81.D1.82.D0.B8)
    *   [4.1 Отключить скрытие устройств (udisks2)](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B8.D1.82.D1.8C_.D1.81.D0.BA.D1.80.D1.8B.D1.82.D0.B8.D0.B5_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2_.28udisks2.29)
    *   [4.2 Монтировать в /media (udisks2)](#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D1.82.D1.8C_.D0.B2_.2Fmedia_.28udisks2.29)
    *   [4.3 Монтирование ISO-образа](#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_ISO-.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D0.B0)
    *   [4.4 Скрыть выбранные разделы](#.D0.A1.D0.BA.D1.80.D1.8B.D1.82.D1.8C_.D0.B2.D1.8B.D0.B1.D1.80.D0.B0.D0.BD.D0.BD.D1.8B.D0.B5_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D1.8B)
*   [5 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [5.1 udisks: Устройства не остаются размонтированными](#udisks:_.D0.A3.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.B0_.D0.BD.D0.B5_.D0.BE.D1.81.D1.82.D0.B0.D1.8E.D1.82.D1.81.D1.8F_.D1.80.D0.B0.D0.B7.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.BD.D1.8B.D0.BC.D0.B8)
*   [6 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

Существует две версии *udisks* по имени [udisks](https://aur.archlinux.org/packages/udisks/) и [udisks2](https://www.archlinux.org/packages/?name=udisks2). Разработка *udisks* прекратилась в пользу *udisks2*. [[1]](http://davidz25.blogspot.be/2012/03/simpler-faster-better.html)

*udisksd* ([udisks2](https://www.archlinux.org/packages/?name=udisks2)) и *udisks-демон* ([udisks](https://aur.archlinux.org/packages/udisks/)) запускаются по требованию [D-Bus](/index.php/D-Bus "D-Bus") и не должны быть включены явно (см. [udisksd(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/udisksd.8) и [udisks-daemon()](http://jlk.fjfi.cvut.cz/arch/manpages/man/udisks-daemon.)). Ими можно управлять через командную строку с помощью *udisksctl* и *udisks*, соответственно. Для получения дополнительной информации смотрите [udisksctl(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/udisksctl.1) и [udisks(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/udisks.8).

## Настройка

Действия пользователя, на выполнение и использование udisks, ограничиваются [Policykit](/index.php/Policykit "Policykit"). Если Вашей [сессии](/index.php/%D0%A3%D1%81%D1%82%D1%80%D0%B0%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5_%D1%87%D0%B0%D1%81%D1%82%D0%BE_%D0%B2%D1%81%D1%82%D1%80%D0%B5%D1%87%D0%B0%D1%8E%D1%89%D0%B8%D1%85%D1%81%D1%8F_%D0%BD%D0%B5%D0%BF%D0%BE%D0%BB%D0%B0%D0%B4%D0%BE%D0%BA#.D0.A0.D0.B0.D0.B7.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D1.8F_.D1.81.D0.B5.D1.81.D1.81.D0.B8.D0.B8 "Устранение часто встречающихся неполадок") нет или она не активируется, настройте policykit вручную. Следующий файл устанавливает общие полномочия udisks для группы `storage`. [[2]](https://github.com/coldfix/udiskie#permissions)

 `/etc/polkit-1/rules.d/50-udisks.rules` 
```
polkit.addRule(function(action, subject) {
  var YES = polkit.Result.YES;
  var permission = {
    //Требуется только для udisks1:
    "org.freedesktop.udisks.filesystem-mount": YES,
    "org.freedesktop.udisks.filesystem-mount-system-internal": YES,
    "org.freedesktop.udisks.luks-unlock": YES,
    "org.freedesktop.udisks.drive-eject": YES,
    "org.freedesktop.udisks.drive-detach": YES,
    //Требуется только для udisks2:
    "org.freedesktop.udisks2.filesystem-mount": YES,
    "org.freedesktop.udisks2.filesystem-mount-system": YES,
    "org.freedesktop.udisks2.encrypted-unlock": YES,
    "org.freedesktop.udisks2.eject-media": YES,
    "org.freedesktop.udisks2.power-off-drive": YES,
    //Требуется только для udisks2, при использовании udiskie с другого места (например, systemd):
    "org.freedesktop.udisks2.filesystem-mount-other-seat": YES,
    "org.freedesktop.udisks2.encrypted-unlock-other-seat": YES,
    "org.freedesktop.udisks2.eject-media-other-seat": YES,
    "org.freedesktop.udisks2.power-off-drive-other-seat": YES
  };
  if (subject.isInGroup("storage")) {
    return permission[action.id];
  }
});
```

Более строгие примеры смотрите [тут](https://gist.github.com/grawity/3886114#file-udisks2-allow-mount-internal-js). Обратите внимание на настройки `org.freedesktop.udisks2.filesystem -*`, необходимые чтобы запустить udiskie со службой [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)").

## Помощники монтирования

Автоматическое монтирование устройств легко достигается с [оболочками udisks](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9#Udisks "Список приложений"). См. также [Список приложений#Монтирование](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5 "Список приложений")и [File manager functionality#Mounting](/index.php/File_manager_functionality#Mounting "File manager functionality").

### Devmon

[udevil](https://www.archlinux.org/packages/?name=udevil) включает [devmon](http://igurublog.wordpress.com/downloads/script-devmon), который совместим с *udisks* и *udisks2*.Он использует помощников монтирования со следующим приоритетом:

1.  [udevil](http://ignorantguru.github.io/udevil/) (SUID)
2.  pmount (SUID)
3.  udisks
4.  udisks2

Для монтирования устройств с *udisks* или *udisks2* удалите разрешение SUID из *udevil*:

```
# chmod-s/usr/bin/udevil

```

**Примечание:** После запуска этой команды от имени суперпользователя *devmon* для слежения за устройствами будет использовать *udisks*

**Совет:** Чтобы для автоматического монтирования устройств запустить *devmon* в фоновом режиме, [включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") службу `devmon@.service`, используя имя пользователя в качестве аргумента: `devmon@*пользователь*.service`. Следует иметь в виду службы, выполняемые вне [сессии](/index.php/General_troubleshooting_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A0.D0.B0.D0.B7.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D1.8F_.D1.81.D0.B5.D1.81.D1.81.D0.B8.D0.B8 "General troubleshooting (Русский)"). Скорректируйте правила [Polkit](/index.php/Polkit "Polkit"), где это необходимо, или запускайте *devmon* из сеанса пользователя (смотрите статью [Автозапуск](/index.php/%D0%90%D0%B2%D1%82%D0%BE%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA "Автозапуск"))

### inotify

Вы можете использовать [inotify-tools](https://www.archlinux.org/packages/?name=inotify-tools), чтобы контролировать `/dev` и монтировать диски, когда создается новое блочное устройство. Устаревшие точки монтирования автоматически удаляются *udisksd*, так, что никаких специальных действий не требуется для удаления.

```
#!/bin/bash
pattern='sd[b-z][1-9]$'
coproc inotifywait --monitor --event create,delete --format '%e %w%f' /dev

while read -r -u "${COPROC[0]}" event file; do
    if [[ $file =~ $pattern ]]; then
	case $event in
	    CREATE)
		echo "Settling..."; sleep 1
		udisksctl mount --block-device $file --no-user-interaction
		;;
	    DELETE)
		;;
	esac
    fi
done

```

## Советы и хитрости

### Отключить скрытие устройств (udisks2)

По умолчанию Udisks2 скрывает определенные устройства от пользователя. Если это поведение нежелательно или создаёт неудобства, скопируйте `/usr/lib/udev/rules.d/80-udisks2.rules` в `/etc/udev/rules.d/80-udisks2.rules`, и удалите следующий раздел в копии:

```
# ------------------------------------------------------------------------
# ------------------------------------------------------------------------
# ------------------------------------------------------------------------
# Devices which should not be display in the user interface
[...]

```

### Монтировать в /media (udisks2)

По умолчанию, udisks2 монтирует съемные диски в контролируемом каталоге ACL `/run/media/$USER/`. Если Вы хотите вместо этого монтировать в `/media`, используйте это правило:

 `/etc/udev/rules.d/99-udisks2.rules ` 
```

# UDISKS_FILESYSTEM_SHARED
# == 1: монтировать файловую систему в общий каталог (/media/VolumeName)
# == 0: монтировать файловую систему в частный каталог (/run/media/$USER/VolumeName)
# Смотрите udisks (8)
ENV {ID_FS_USAGE} == «filesystem|other|crypto», ENV {UDISKS_FILESYSTEM_SHARED} = «1»

```

### Монтирование ISO-образа

Для простого монтирования ISO-образов, используйте следующую команду:

$ udisksctl loop-setup -r -f *image.iso*

Это создаст циклическое устройство и покажет готовый к монтированию ISO-образ. После размонтирования, циклическое устройство будет завершено [udev](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)").

### Скрыть выбранные разделы

Если Вы хотите скрыть определенные разделы или диски, появляющиеся на рабочем столе, Вы можете создать правило udev, например `/etc/udev/rules.d/10-local.rules`:

```
KERNEL == «sda1», ENV {UDISKS_PRESENTATION_HIDE} = «1»
KERNEL == «sda2», ENV {UDISKS_PRESENTATION_HIDE} = «1»

```

- показать все разделы за исключением `sda1` и `sda2` на Вашем рабочем столе. Заметьте, если вы используете [udisks2](https://www.archlinux.org/packages/?name=udisks2), вышеупомянутое правило не будет работать, поскольку `UDISKS_PRESENTATION_HIDE` больше не поддерживается. Вместо этого используйте `UDISKS_IGNORE` следующим образом:

```
KERNEL == «sda1», ENV {UDISKS_IGNORE} = «1»
KERNEL == «sda2», ENV {UDISKS_IGNORE} = «1»

```

## Решение проблем

### udisks: Устройства не остаются размонтированными

*udisks* повторно монтирует устройства или *опрашивает* их после установленного времени. Это может вызвать неожиданное поведение, например при форматировании дисков, совместном использовании их в [виртуальной машине](/index.php/Virtual_machine "Virtual machine"), экономия электроэнергии, или удалении дисков не отсоединенных с помощью `--detach`.

Отключить опрос относительно данного устройства, например устройства CD/DVD:

```
# udisks --inhibit-polling /dev/sr*0*

```

или для всех устройств:

```
# udisks --inhibit-all-polling

```

Для получения дополнительной информации смотрите [udisks(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/udisks.8).

## Смотрите также

*   [Gentoo wiki udisks (Англ.)](http://wiki.gentoo.org/wiki/Udisksi)
*   [Введение в udisks (Англ.)](http://blog.fpmurphy.com/2011/08/introduction-to-udisks.html?output=pdf)