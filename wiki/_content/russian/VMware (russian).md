[VMware](http://www.vmware.com/) устанавливается на [Arch Linux](/index.php/Arch_Linux "Arch Linux") довольно легко, однако установка не всегда предельно ясна.

## Contents

*   [1 Установка VMware Workstation](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_VMware_Workstation)
*   [2 Установка VMware Server](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_VMware_Server)
    *   [2.1 Требования:](#.D0.A2.D1.80.D0.B5.D0.B1.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F:)
    *   [2.2 Инструкция:](#.D0.98.D0.BD.D1.81.D1.82.D1.80.D1.83.D0.BA.D1.86.D0.B8.D1.8F:)
*   [3 Запуск](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA)
*   [4 Ядро 2.6 и udev](#.D0.AF.D0.B4.D1.80.D0.BE_2.6_.D0.B8_udev)
*   [5 VMware и ядро 2.6.16 - проблема сборки модулей](#VMware_.D0.B8_.D1.8F.D0.B4.D1.80.D0.BE_2.6.16_-_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D0.B0_.D1.81.D0.B1.D0.BE.D1.80.D0.BA.D0.B8_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D0.B5.D0.B9)
*   [6 VMware и ядро 2.6.20 - проблема сборки модулей](#VMware_.D0.B8_.D1.8F.D0.B4.D1.80.D0.BE_2.6.20_-_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D0.B0_.D1.81.D0.B1.D0.BE.D1.80.D0.BA.D0.B8_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D0.B5.D0.B9)
*   [7 VMware и ядро 2.6.22 - проблема сборки модулей](#VMware_.D0.B8_.D1.8F.D0.B4.D1.80.D0.BE_2.6.22_-_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D0.B0_.D1.81.D0.B1.D0.BE.D1.80.D0.BA.D0.B8_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D0.B5.D0.B9)
*   [8 VMware и ядро 2.6.24 - проблема сборки модулей](#VMware_.D0.B8_.D1.8F.D0.B4.D1.80.D0.BE_2.6.24_-_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D0.B0_.D1.81.D0.B1.D0.BE.D1.80.D0.BA.D0.B8_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D0.B5.D0.B9)
*   [9 VMware и ядро 2.6.25 - проблема сборки модулей](#VMware_.D0.B8_.D1.8F.D0.B4.D1.80.D0.BE_2.6.25_-_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D0.B0_.D1.81.D0.B1.D0.BE.D1.80.D0.BA.D0.B8_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D0.B5.D0.B9)
*   [10 VMware и ядро 2.6.26 - проблема сборки модулей](#VMware_.D0.B8_.D1.8F.D0.B4.D1.80.D0.BE_2.6.26_-_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D0.B0_.D1.81.D0.B1.D0.BE.D1.80.D0.BA.D0.B8_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D0.B5.D0.B9)
*   [11 VMware и ядра 2.6.27 и 2.6.28 - проблема сборки модулей](#VMware_.D0.B8_.D1.8F.D0.B4.D1.80.D0.B0_2.6.27_.D0.B8_2.6.28_-_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D0.B0_.D1.81.D0.B1.D0.BE.D1.80.D0.BA.D0.B8_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D0.B5.D0.B9)
*   [12 Медленная работа сети между хостом и гостевой ОС](#.D0.9C.D0.B5.D0.B4.D0.BB.D0.B5.D0.BD.D0.BD.D0.B0.D1.8F_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0_.D1.81.D0.B5.D1.82.D0.B8_.D0.BC.D0.B5.D0.B6.D0.B4.D1.83_.D1.85.D0.BE.D1.81.D1.82.D0.BE.D0.BC_.D0.B8_.D0.B3.D0.BE.D1.81.D1.82.D0.B5.D0.B2.D0.BE.D0.B9_.D0.9E.D0.A1)
*   [13 Проблема в Samba](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D0.B0_.D0.B2_Samba)
*   [14 Удаленное соединение](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.BD.D0.BE.D0.B5_.D1.81.D0.BE.D0.B5.D0.B4.D0.B8.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5)
*   [15 Проблема с клавиатурой](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D0.B0_.D1.81_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D0.BE.D0.B9)
*   [16 VMware 6.5 не удается запустить vmware-modconfig](#VMware_6.5_.D0.BD.D0.B5_.D1.83.D0.B4.D0.B0.D0.B5.D1.82.D1.81.D1.8F_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D1.82.D0.B8.D1.82.D1.8C_vmware-modconfig)
*   [17 Обзор установки VMware 6.5.3 с ядром 2.6.32](#.D0.9E.D0.B1.D0.B7.D0.BE.D1.80_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8_VMware_6.5.3_.D1.81_.D1.8F.D0.B4.D1.80.D0.BE.D0.BC_2.6.32)
*   [18 Обновление ядра и пересборка модулей](#.D0.9E.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.8F.D0.B4.D1.80.D0.B0_.D0.B8_.D0.BF.D0.B5.D1.80.D0.B5.D1.81.D0.B1.D0.BE.D1.80.D0.BA.D0.B0_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D0.B5.D0.B9)
*   [19 Удаление](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5)

## Установка VMware Workstation

Следующая информация взята из пользовательких комментариев в AUR по VMWare Workstation пользователем whompus. Она описывает как установить VMWare Workstation 6.5.x на одну из архитектур.

В качестве временной меры можно воспользоваться представленным способом установки 6.5\. Заметьте, что pacman **не** будет использован в данном случае, так что установку **нельзя** будет отследить\удалить, используя pacman.

Для установки Workstation на Linux действуйте следующим образом:

1\. Скачайте VMware-Workstation-6.5.xxxxxx.bundle. Где xxxxx минорная (с незначительными изменениями) версия программы и архитектура.

2\. В терминале смените текущую дерикторию на ту, в которую загрузили файл.

3\. С правами root выполните начальные шаги установки:

```
# mkdir -p /etc/rc.d/vmware.d/{rc{0,1,2,3,4,5,6},init}.d
# sh VMware-Workstation-6.5.xxxxxx.bundle --custom

```

4\. Прочитайте и примите EULA для продолжения.

5\. Принимайте стандартные настройки до тех пор, пока не появится запрос "System service runlevels", установите тогда следующее:

```
/etc/rc.d/vmware.d/

```

6\. Для System service scripts выставьте:

```
/etc/rc.d 

```

7\. (Опционально) Введите путь к директории с Integrated Virtual Debugger для Eclipse, если Eclipse установлен.

8\. Жмите "ввод" для установки.

9\. Добавьте `vmmon vmci vmnet` к модулям в свой `/etc/rc.conf`:

```
MODULES=(...vmnet vmmon vmci...)

```

10\. Откройте Workstation (наберите `vmware` в консоли) для настройки и использования!

## Установка VMware Server

**Примечание:** **Настоятельно рекомендуется использовать VMWare Server 2 на ядре 2.6.27, так как это актуальные сборки. Также они не требуют наложения патча.**

Вы можете использовать [AUR](https://aur.archlinux.org/packages.php?do_Details=1&ID=6182&O=0&L=0&C=0&K=vmware&SB=n&SO=a&PP=25&do_MyPackages=0&do_Orphans=0&SeB=nd) или ручную установку [VMware Server](http://www.vmware.com/download/server/) скачанного с [VMware.com](http://www.vmware.com/). Это руководство покажет как в ручную установить скачанный тарбол с VMware server, предполагается, что вы используете Voodoo или более свежий Arch Linux с версией ядра 2.6.20+ **32-bit**.

### Требования:

*   Root доступ. Одно из двух, 'sudo' или 'su'. В этом руководстве я буду использовать 'sudo'.
*   [Xinetd](https://archlinux.org/packages/search/?repo=all&category=all&q=xinetd&lastupdate=&limit=50) установлен и запущен.
*   Библиотеки X - libxtst, libxt и libxrender установлены.
*   [VMware server tarball](http://www.vmware.com/download/server/); последний 1.0.4 build 56528 во время написания этих строк.
*   ~~VMware server [any-to-any](http://www.vmware.com/community/thread.jspa?messageID=76957&tstart=0)" patch: [mirror 1](http://platan.vc.cvut.cz/ftp/pub/vmware) and [mirror 2](ftp://ftp.cvut.cz/vmware). Note: For server 1.0.4 build 56528 you need patch vmware-any-any-update113.tar.bz2, which is on mirror 1 only.~~
*   UPDATE: Для ядра 2.6.24 вам понадобится этот [patch](http://rtr.ca/vmware-2.6.24/) (vmware-any-any-update115a.tgz)
*   UPDATE: Для ядра 2.6.25 вам также понадобится также этот [patch](http://blog.creonfx.com/temp/vmware-any-any-update-117-very-ALPHA.tgz) (vmware-any-any-update-117-very-ALPHA)
*   Совместимость с VMware Workstation >= 6.0.2 Build 59824 on Linux 2.6.25
*   UPDATE: Для ядра 2.6.26 вам понадобится этот [patch](http://vmkernelnewbies.googlegroups.com/web/vmware-any-any-update117d.tar.gz) (vmware-any-any-update117d.tar.gz), VMware версии 6.0.5 этот патч не нуже, версия vmmon нужна не младше 169.
*   UPDATE: Для ядра 2.6.26 и VMWare 6.5 патчи больше _не_ нужны (6.5.0 build-118166). Графический инсталлятор работает хорошо, а все модули работают "из коробки". Следуйте дальнейшим инструкциям до определения директории, содержащей init-скрипты.

### Инструкция:

*   Выполните ***sudo mkdir -p /etc/rc.d/vmware.d/rc{0,1,2,3,4,5,6}.d*** для создания runlevel-директорий для VMware.
*   Выполните ***sudo ln -s /bin/lsmod /sbin/*** для создания символической ссылки на lsmod.
*   Извлеките тарбол с VMware Server куда угодно, например в /tmp/.
*   Выполните ***cd /tmp/vmware-server-distrib;sudo ./vmware-install.pl***. Я использовал для установки ***/home/vmware/bin***.
*   При запросе расположения директорий от *rc0.d* до *rc6.d*, используйте ***/etc/rc.d/vmware.d***.
*   При запросе директории с init скриптами укажите ***/etc/rc.d***.
*   ***Выйдите***, когда появится запрос о запуске первоначальной конфигурации VMware.
*   Извлеките куда-нибудь VMware Server any-to-any patch... например /tmp/.
*   Выполните ***cd /tmp/vmware-any-any-update*REV*;sudo ./runme.pl***. Это наложит заплатку на модули VMware Server, чтобы позволить ядру Linux 2.6.20 скомпилироваться.
*   Для ядра 2.6.25 дополнительно к предыдущей заплатке patch115a или 116 вам понадобится вручную установить 117_Alpha.
*   Для 2.6.25 Извлеките 117 в каталог ***tar xzf vmware-any-any-update-117-very-ALPHA.tgz -C /usr/lib/vmware/modules/source/***
*   Для наложения заплатки на 2.6.25 ***cd /usr/lib/vmware/modules/source/*** и запустите ***./vmware-2.6.25.sh*** и продолжите выполнять следующие шаги.
*   Выполните ***cd /home/vmware/bin;sudo ./vmware-config.pl*** для компиляции модулей VMware.

## Запуск

Возможно, что при первом запуске VMware Server вы получите ошибку, которая начинается примерно так "Unable to power virtual machine". Остановите VMware Server и перезапустите xinetd ***/etc/rc.d/vmware stop;wait;/etc/rc.d/xinetd restart***.

Выполните ***sudo /home/vmware/bin/vmware-config.pl*** снова. Если ошибка не исчезла, перезапустите свой компьютер и повторите последнее действие снова. Все должно исправиться.

Теперь `vmware` init-скрипт в `/etc/rc.d`. Вы можете добавить его в лист демонов, если захотите. Лично я так не сделал, но если вы намереваетесь использовать сеть vmware, не используя сам vmware, вам это понадобится. Вам нужно запустить этот init-скрипт перед запуском VMware.

Есть проблема, когда vmware не может корректно запуститься после перезагрузки. Для того, чтобы исправить это, отредактируйте `/etc/rc.d/vmware`, найдите следующий текст

```
case "$1" in
  start)

```

и вставьте

```
rm /etc/vmware/not_configured

```

сразу же после последней строки.

Чтобы запустить vmware, просто выполните `vmware` в терминале, или создайте ярлык или строку меню, как пожелаете.

**Некоторые замечания:**

Оставьте директорию `/etc/rc.d/vmware.d` там где она есть, потому что она необходима, когда вы выполните `vmware-config.pl`.

Помните, если ваше ядро изменилось или обновилось, вам нужно запустить `vmware-config.pl` снова.

## Ядро 2.6 и udev

Проделайте шаги, описанные выше, а затем:

**1\. Отредактируйте файл конфигурации udev**

Отредактируйте `/etc/udev/rules.d/00-myrules.rules` добавив 2 строки:

```
# терминальные (tty) устройства
KERNEL="tty[[0-9]]*", NAME="vc/%n", SYMLINK="%k"

# дисковод (floppy)
KERNEL="fd[[0-9]]*", NAME="floppy/%n" , SYMLINK="fd%n"

```

**2\. Скрипт Запуска/остановки**

Он (скрипт) позаботится об устройствах и запуске vmware, а также об его остановке и удалении созданных dev устройствах. Назовите его, для примера `mkvmdev`, используйте chmod `755` для этого файла и переместите в каталог `/etc/rc.d`:

```
#!/bin/sh

. /etc/rc.conf
. /etc/rc.d/functions

case "$1" in
    start)
    stat_busy "Creating /dev entries and starting VMware"
    for i in `seq 0 9`; do
        mknod /dev/vmnet$i c 119 $i
        chmod 0600 /dev/vmnet$i
    done
    for i in `seq 0 3`; do
        mknod /dev/parport$i c 99 $i
        chmod 0600 /dev/parport$i
    done
    mknod /dev/vmmon c 10 165
    chmod 0660 /dev/vmmon
    /etc/rc.d/vmware start
    ;;

    stop)
    stat_busy "Stopping VMware and removing /dev entries"
    /etc/rc.d/vmware stop
    rm /dev/vmmon
    for i in `seq 0 3`; do
        rm /dev/parport$i
    done
    for i in `seq 0 9`; do
        rm /dev/vmnet$i
    done
    ;;

    restart)
    $0 stop
    $0 start
    ;;

    *)
    echo "usage: $0 {start|stop|restart}"
esac
exit 0

```

**3\. Отрекдактируйте `/etc/rc.conf`.** (*Заметка - это дополнительный шаг! Смотрите также заметки под секцией "Запуск" выше.)

Добавьте `mkvmdev` к демонам (daemons) в свой `rc.conf`, и не забудьте удалить `vmware` из `rc.conf`. Или, если так будет угодней, вы можете удалить эти строки запуска vmware из `mkvmdev` и оставить оригинальный `vmware` в `rc.conf` - на ваше усмотрение.

* * *

**Комментарии:**

hi guys, a couple of quick questions:
- why is /dev/vmmon chmod 0660, as opposed to the rest (0600)?
- i suppose /dev/vmmon should be "rm"-ed as well in the "stop" section for the script above? (that line is missing) - FIXED

## VMware и ядро 2.6.16 - проблема сборки модулей

**Проблема**: ядро 2.6.16-x - vmware или vmwareplayer выдает ошибку, что заголовки неверны.
**Решение**: Вам понадобится заплатка [vmware-any-any-update](http://knihovny.cvut.cz/ftp/pub/vmware/vmware-any-any-update101.tar.gz),[зеркало здесь](ftp://ftp.cvut.cz/vmware/vmware-any-any-update101.tar.gz) [или здесь](http://www.inarad.ro/soft/vmware/vmware-any-any-update101.tar.gz).
Просто извлеките данные из tar и запустите ./runme.pl с правами суперпользователя - и вы снова счастливы!

## VMware и ядро 2.6.20 - проблема сборки модулей

Ниже представлено решение для сборки модулей vmware на ядре 2.6.20.

```
cd /usr/lib/vmware/modules/source/
sudo tar -xvf vmmon.tar
cd vmmon-only
sudo vi include/compat_kernel.h

Найдите это:

#define __NR_compat_exit __NR_exit
static inline _syscall1(int, compat_exit, int, exit_code);

и замените "static inline" строку на эту:

int compat_exit(int exit_code);

Затем снова упакуйте в tar директорию vmmon-only.

cd .. #go back to the source directory
tar -cf vmmon.tar vmmon-only

И наконец, выполните vmware-config.pl

```

## VMware и ядро 2.6.22 - проблема сборки модулей

Может и не сработать. Наложите заплатку отсюда [http://knihovny.cvut.cz/ftp/pub/vmware/vmware-any-any-update112.tar.gz](http://knihovny.cvut.cz/ftp/pub/vmware/vmware-any-any-update112.tar.gz), замените vmnet.tar на этот [http://npw.net/~phbaer/vmnet.tar](http://npw.net/~phbaer/vmnet.tar) и переустановите. Заметка: это "костыль", пожалуйста, не используйте его на производственных системах. Некоторые гостевые ОС могут обрушиться с ошибками, а также наблюдаются некоторые проблемы с сетью. **Не говорите, что вас не предупреждали**

## VMware и ядро 2.6.24 - проблема сборки модулей

Может и не сработать. Примените эту заплатку [http://bio.artcradle.com/temp/vault/vmware-any-any-update-116.tgz](http://bio.artcradle.com/temp/vault/vmware-any-any-update-116.tgz) (извлеките из tar, запустите скрипт runme.pl) Заметка: это "костыль", пожалуйста, не используйте его на производственных системах. Некоторые гостевые ОС могут обрушиться с ошибками, а также наблюдаются некоторые проблемы с сетью. **Не говорите, что вас не предупреждали**

## VMware и ядро 2.6.25 - проблема сборки модулей

Здесь представлены дополнительные шаги, необходимые для Vmware Workstation 6.0.3 build 80004, следовательно то же самое необходимо для VMware Server

1.  Установите VMware и заплаку, как это уже описано (используйте vmware-any-any-update-116.tgz)
2.  Загрузите [patch117](http://blog.creonfx.com/temp/vmware-any-any-update-117-very-ALPHA.tgz)vmware-any-any-update-117-very-ALPHA.tgz
3.  Извлеките архив в /usr/lib/vmware/modules/source
4.  Выполните vmware-2.6.25.sh и затем vmware-config.pl

## VMware и ядро 2.6.26 - проблема сборки модулей

Если после сборки модулей согласно методу для ядра 2.6.25 вы получите "Version mismatch with vmmon module:" ошибку, тогда для включения виртуальной машины вам понадобится выполнить дополнительный шаг.

```

cd /usr/lib/vmware/moduels/source/;
sudo tar -xvf vmmon.tar;
sudo vi vmmon-only/include/iocontrols.h;

Найдите строку 48:

#define VMMON_VERSION           (161 << 16 | 0)

и замените на: 

#define VMMON_VERSION           (167 << 16 | 0)

Сохраните и выйдите.

sudo tar -cf vmmon.tar vmmon-only;

И наконец, выполните vmware-config.pl.

```

## VMware и ядра 2.6.27 и 2.6.28 - проблема сборки модулей

Проверенное решение - это [скачать](http://www.insecure.ws/warehouse/vmware-update-2.6.27-5.5.7-2.tar.gz) [исправленные модули](http://www.insecure.ws/2008/10/20/vmware-specific-specific-55x-and-kernel-2627) и заменить ими. Чтобы сделать это, вам понадобится извлечть скачанный архив, и заменить оба файла: vmmon.tar и vmnet.tar в /usr/lib/vmware/modules/source. После чего выполните /usr/bin/vmware-config.pl для пересборки модулей.

## Медленная работа сети между хостом и гостевой ОС

"Those oversized improperly checksummed packets are TCP Segmentation Offload packets. Use '**ethtool -k eth0 tso off'** to disable TSO on eth0 (or any other interface which you want to get bridged). At this moment vmnet does not understand TSO, and in addition to that it is silly to use TSO together with bridged networking as vmnet will have to split such packet anyway to pass it to the guest, so splitting will be done anyway, and in addition to it kernel will have to prepare metadata about TCP stream for hardware, so you'll probably get worse performance with TSO enabled than with disabled when you'll have some guest running."

**Примечание:** ethtool is on extra packages

## Проблема в Samba

Гостевая ОС в VMware не может увидеть общие директории Samba, запущенные на хост-машине под управлением Linux. Для решения этой проблемы отрекдактируйте /etc/samba/smb.conf, добавив некоторые изменения в секцию [global]. Изменения ниже:
workgroup = YOUR_WORKGROUP
netbios name = YOUR_SERVER_NAME
encrypt passwords = yes
socket options = TCP_NODELAY IPTOS_LOWDELAY SO_KEEPALIVE SO_RCVBUF=8192 SO_SNDBUF=8192
interfaces = eth0 vmnet1 vmnet8
sysv shm key=/dev/vmnet1
bind interfaces only = true

## Удаленное соединение

Если вы установили в VMware сервер, к которому хотите подключаться удаленно, пожалуйста добавьте следующее в файл **/etc/hosts.allow**:

 `vmware-authd: ALL` 

Это позволит **xinetd** разрешить соединения от удаленных клиентов vmware.

Если это условие не удовлетворено, вы можете посмотреть ваш файл лога **/var/log/everything.log**:

 `Feb  4 03:34:12 jeffc xinetd[7232]: libwrap refused connection to vmware-authd (libwrap=vmware-authd) from 192.168.1.1` 

## Проблема с клавиатурой

Если у вас есть гостевая машина Windows (или другая), некоторые\большинство клавиш на клавиатуре могут не работать (особенно клавиши со стрелками, ctrl, alt, клавиша windows и другие).

Одним из решений может послужить редактирование или создание файла `~/.vmware/config` и добавление туда следующих строк:

```
xkeymap.keycode.108 = 0x138 # Alt_R
xkeymap.keycode.106 = 0x135 # KP_Divide
xkeymap.keycode.104 = 0x11c # KP_Enter
xkeymap.keycode.111 = 0x148 # Up
xkeymap.keycode.116 = 0x150 # Down
xkeymap.keycode.113 = 0x14b # Left
xkeymap.keycode.114 = 0x14d # Right
xkeymap.keycode.105 = 0x11d # Control_R
xkeymap.keycode.118 = 0x152 # Insert
xkeymap.keycode.119 = 0x153 # Delete
xkeymap.keycode.110 = 0x147 # Home
xkeymap.keycode.115 = 0x14f # End
xkeymap.keycode.112 = 0x149 # Prior
xkeymap.keycode.117 = 0x151 # Next
xkeymap.keycode.78 = 0x46 # Scroll_Lock
xkeymap.keycode.127 = 0x100 # Pause
xkeymap.keycode.133 = 0x15b # Meta_L
xkeymap.keycode.134 = 0x15c # Meta_R
xkeymap.keycode.135 = 0x15d # Menu

```

## VMware 6.5 не удается запустить vmware-modconfig

Если vmware-modconfig "падает" на первом старте, скачайте и выполните это [http://communities.vmware.com/servlet/JiveServlet/download/1088282-15379/vmware-build-modules](http://communities.vmware.com/servlet/JiveServlet/download/1088282-15379/vmware-build-modules) Больше информации здесь [http://communities.vmware.com/thread/172023](http://communities.vmware.com/thread/172023)

## Обзор установки VMware 6.5.3 с ядром 2.6.32

Итак, рассматриваемые компоненты:

```
- VMware-Workstation-6.5.3-185404.i386.bundle
- kernel26-2.6.32.1-1

```

1\. Перемещаем VMware-Workstation в корневой каталог и выполняем от имени суперпользователя следующие шаги:

```
[root@hp]# mkdir -p /etc/rc.d/vmware.d/{rc{0,1,2,3,4,5,6}.d,init.d}
[root@hp]# export VMWARE_SKIP_MODULES=true
[root@hp]# sh VMware-Workstation-6.5.3-185404.i386.bundle --console --custom

```

2\. Читаем и принимаем лицензионное соглашение.

3\. Дальше отвечаем на все пункты положительно, кроме "**System service runlevels**", где нужно ввести путь **/etc/rc.d/vmware/**, как это показано в примере ниже:

```
    Do you agree? [yes/no]: yes

    System path prefix.  Please note that choosing a path other than /usr
    may result in missing icons, application launchers, and other desktop
    integrations [/usr]:

    System lib directory [/usr/lib]:

    Architecture-independent files [/usr/share]:

    User level binaries [/usr/bin]:

    Super user level binaries [/usr/sbin]:

    Documentation [/usr/share/doc]:

    Manual pages [/usr/share/man]:

    Header files [/usr/include]:

    System configuration files [/etc]:

    System service runlevels: /etc/rc.d/vmware.d/       <<--------------------------------

    System service scripts [/etc/rc.d/vmware.d/init.d]:

    Path to Eclipse directory for use with Integrated Virtual Debugger
    (optional):

    The product is ready to be installed.  Press enter to begin
    installation or Ctrl-C to cancel.

```

4\. Переключаем учетную запись с суперпользователя на нормального пользователя. Запускаем VMware:

```
[user@hp]$ vmware

```

Программа попросит скомпилировать модули и вы должны нажать кнопку "_Install". После нескольких сообщений об ошибках она спросит у вас пароль суперпользователя и начнет компилировать модули. По окончании запустится VMware.

5\. Вы должны закрыть программу и выполнить следующую команду от имени суперпользователя:

```
[root@hp]# ln -s /etc/rc.d/vmware.d/init.d/vmware /etc/rc.d/vmware

```

6\. Дальше добавляем пункт "vmware" в секцию DAEMONS в файле /etc/rc.conf

```
#
# /etc/rc.conf - Main Configuration for Arch Linux
#
...
DAEMONS=(syslog-ng ... ... vmware)

```

7\. Вы должны заменить **/sbin/lsmod** на **/bin/lsmod** в файле **/etc/rc.d/vmware/init.d/vmware**, набрав следующую команду:

```
[root@hp]# sed -i 's/\/sbin\/lsmod/\/bin\/lsmod/g' /etc/rc.d/vmware.d/init.d/vmware

```

8\. Перезапускаем службы и модули VMware следующей командой:

```
[root@hp]# /etc/rc.d/vmware restart

```

9\. Возможны некоторые проблемы с работой мыши (теряется фокус за пределами VGA-области 640x480) из-за новых версий GTK+. Чтобы решить эту проблему, добавьте в файл **/etc/vmware/bootstrap** следующую строку:

```
# /etc/vmware/bootstrap
export VMWARE_USE_SHIPPED_GTK=yes

```

10\. Теперь можно запустить программу от имени простого пользователя:

```
[user@hp]$ vmware

```

## Обновление ядра и пересборка модулей

Пожалуйста, запомните, что каждый раз при обновлении ядра, вам необходимо пересобрать модули VMware. Сделать это можно следующей командой:

```
# vmware-modconfig --console --install-all

```

Иначе это может привести к сбою системы при запуске виртуальной машины.

## Удаление

Проверьте имя программы:

```
# vmware-installer -l

```

Удалите программу:

```
# vmware-installer -u <vmware-product>

```

Некоторые (вручную измененные или созданные) файлы программы в **/etc/rc.d** необходимо будет удалить вручную. Не забудьте удалить пункт **vmware** из секции DAEMONS в файле **/etc/rc.conf**.