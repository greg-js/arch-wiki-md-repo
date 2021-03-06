<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Что такое Fsck](#Что_такое_Fsck)
*   [2 Запуск Fsck вручную - легкий способ](#Запуск_Fsck_вручную_-_легкий_способ)
*   [3 Полезные советы](#Полезные_советы)
    *   [3.1 Изменение интервалов проверки](#Изменение_интервалов_проверки)
    *   [3.2 /etc/fstab](#/etc/fstab)

## Что такое Fsck

Fsck расшифровывается как "File System ChecK", то есть "проверка файловой системы" и используется для проверки и исправления файловых систем в Linux. В качестве проверяемой ФС может быть задан раздел (например, `/dev/sda1` или `/dev/sda8`), точка монтирования (`/`, `/home`, `/usr`), или же метка тома или UUID (например, `UUID=8868abf6-88c5-4a83-98b8-bfc24057f7bd` или `LABEL=root`). Обычно fsck пытается параллельно проверять файловые системы на нескольких разделах для уменьшения времени, необходимого для проверки всех файловых систем. (Cм.: [fsck(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fsck.8))

Arch Linux при загрузке автоматически будет запускать fsck для проверки систем, если выполняется одно из требований (например, 180 дней работы системы без проверки разделов или 30 монтирований оных). Обычно нет необходимости переопределять промежуток между проверками.

**Важно:** Не запускайте fsck на примонтированных разделах! Это может привести к потере данных! Fsck будет спрашивать вас о проведении этой операции на примонтированном разделе, однако лучше каждый раз отказываться от этого.

## Запуск Fsck вручную - легкий способ

Если вы хотите запустить проверку всех дисков при следующей загрузке системы, то используйте следующую команду (от root):

```
# shutdown -Fr now

```

Команда **shutdown** выключает систему, **-F** запускает Fsck при загрузке, **-r** указывает на то, что вместо полного выключения питания необходима перезагрузка, и **now** указывает на то, что перезагрузка будет выполнена немедленно.

## Полезные советы

Чтобы узнать все доступные опции Fsck запустите:

```
# fsck -h

```

Для того, чтобы автоматически исправлять ошибки, найденные в процессе проверки, используйте следующую команду:

```
# fsck -a

```

**Важно:** fsck, при обнаружении ошибки, не будет спрашивать вас о том, стоит ли исправлять ошибки.

Если вы хотите просто проверить файловую систему без исправления ошибок:

```
# fsck -n

```

### Изменение интервалов проверки

По-умолчанию fsck выполняется каждые 30 загрузок или 180 дней (считается отдельно для каждого раздела). Для изменения используется утилита **tune2fs**:

```
# tune2fs -c 20 /dev/sda1

```

Эта команда установит промежуток в **20** загрузок. Если указать **1** - то раздел будет проверяться каждую загрузку, а установка значения в **0** вообще отключит проверку.

### /etc/fstab

Включить или выключить проверку файловой системы, помимо tune2fs, можно еще и в `/etc/fstab`. Этот файл может выглядеть так:

```
/dev/sda1 / ext4 defaults 0 **1**
/dev/sda2 /other ext4 defaults 0 **2**
/dev/sda3 /win ntfs defaults 0 **0**

```

6 столбец (выделен жирным) указывает на опции проверки:

*   0 = Не проверять
*   1 = Раздел проверяется в первую очередь; `/` (корневой раздел) должен быть указан с опцией 1.
*   2 = Остальные файловые системы для проверки

Прочитайте [fstab](/index.php/Fstab_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fstab (Русский)") для дополнительной информации.