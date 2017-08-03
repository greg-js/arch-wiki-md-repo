**Состояние перевода:** На этой странице представлен перевод статьи [Overlay filesystem](/index.php/Overlay_filesystem "Overlay filesystem"). Дата последней синхронизации: 29 июля 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Overlay_filesystem&diff=0&oldid=483209).

Из [the initial kernel commit](https://github.com/torvalds/linux/commit/e9be9d5e76e34872f0c37d72e25bc27fe9e2c54c)

	Overlayfs позволяет накладывать одно, обычно чтение и запись, дерево каталогов на другое дерево только для чтения. Все изменения переходят на верхний слой с возможностью записи. Этот тип механизма чаще всего используется для live компакт-дисков, но существует множество других применений.

	Реализация отличается от других реализаций "объединенных файловых систем" тем, что после открытия файла все операции идут непосредственно в базовую, нижнюю или верхнюю файловую систему. Это упрощает реализацию и позволяет использовать в этих случаях собственную производительность.

Overlayfs находится в ядре linux с версии 3.18.[[1]](https://github.com/torvalds/linux/commit/e9be9d5e76e34872f0c37d72e25bc27fe9e2c54c)

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [2.1 Overlay только для чтения](#Overlay_.D1.82.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_.D0.B4.D0.BB.D1.8F_.D1.87.D1.82.D0.B5.D0.BD.D0.B8.D1.8F)
*   [3 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

Overlayfs включен в ядре по умолчанию, а модуль `overlay` автоматически загружается после ввода команды монтирования.

## Использование

Для монтирования overlay используйте следующие опции `mount`:

```
# mount -t overlay overlay -o lowerdir=*/lower*,upperdir=*/upper*,workdir=*/work* */merged*

```

**Примечание:** Рабочий каталог (*workdir*) должен быть на той же файловой системе монтирования в качестве верхнего каталога. Нет никакого требования (*lowerdir*).

Нижняя директория может фактически быть списком каталогов, разделенных `:`, все изменения в каталоге `merged` по-прежнему отражаются в `upper`.

Пример:

```
# mount -t overlay overlay -o lowerdir=*/lower1:/lower2:/lower3*,upperdir=*/upper*,workdir=*/work* */merged*

```

Чтобы добавить запись overlayfs в `/etc/fstab`, используйте следующий формат:

 `/etc/fstab`  `overlay */merged* overlay noauto,x-systemd.automount,lowerdir=*/lower*,upperdir=*/upper*,workdir=*/work* 0 0` 

Параметры монтирования `noauto` и `x-systemd.automount` необходимы для предотвращения зависания systemd при загрузке, поскольку он не смонтировал overlay. Overlay теперь монтируется всякий раз, когда он получает первый доступ, и запросы буферизуются до тех пор, пока они не будут готовы. Для получения дополнительной информации смотрите [Fstab#Автоматическое монтирование с systemd](/index.php/Fstab_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B5_.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81_systemd "Fstab (Русский)").

### Overlay только для чтения

Иногда желательно только создать представление только для чтения о комбинации двух или более каталогов. В этом случае его можно создать более простым способом, так как каталоги `upper` и `work` **не** обязательны:

```
# mount -t overlay overlay -o lowerdir=*/lower1:/lower2* */merged*

```

Когда `upperdir` не указан, overlay [монтируется автоматически как только для чтения](https://github.com/torvalds/linux/blob/352526f45387cb96671f13b003bdd5b249e509bd/fs/overlayfs/super.c#L897).

## Смотрите также

*   [Документация файловой системы Overlay](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/Documentation/filesystems/overlayfs.txt)