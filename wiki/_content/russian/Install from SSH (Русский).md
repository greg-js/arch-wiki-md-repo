## Contents

*   [1 Введение](#.D0.92.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5)
*   [2 Загрузка с носителя](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_.D1.81_.D0.BD.D0.BE.D1.81.D0.B8.D1.82.D0.B5.D0.BB.D1.8F)
*   [3 Настройка живой среды для использования SSH](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.B6.D0.B8.D0.B2.D0.BE.D0.B9_.D1.81.D1.80.D0.B5.D0.B4.D1.8B_.D0.B4.D0.BB.D1.8F_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_SSH)
*   [4 Подключение к целевому ПК через SSH](#.D0.9F.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA_.D1.86.D0.B5.D0.BB.D0.B5.D0.B2.D0.BE.D0.BC.D1.83_.D0.9F.D0.9A_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_SSH)
    *   [4.1 Замечания](#.D0.97.D0.B0.D0.BC.D0.B5.D1.87.D0.B0.D0.BD.D0.B8.D1.8F)
*   [5 Следующие шаги](#.D0.A1.D0.BB.D0.B5.D0.B4.D1.83.D1.8E.D1.89.D0.B8.D0.B5_.D1.88.D0.B0.D0.B3.D0.B8)

## Введение

Эта статья предназначена для того, чтобы показать пользователям, как установить Arch удалённо через SSH соединение. Рассмотрим данный подход как стандартный в следующих случаях:

Установка Arch на...

*   HTPC без надлежащего монитора (т.е. SDTV).
*   ПК, расположенный в другом городе, области, стране (у друга, родителей и т.д.)
*   ПК, который Вы предпочитаете настраивать удалённо, к примеру, со своей рабочей станции с возможностью копировать/вставлять из Arch Wiki.

**Обратите внимание:** Первые два шага требуют физического доступа к машине. Очевидно, что если она располагается где-то в другом месте, понадобится координировать действия с ещё одним человеком!

## Загрузка с носителя

Загрузитесь в живую стреду Arch с помощью [live CD/USB образа](/index.php/Beginners%27_guide#Obtain_the_latest_installation_media "Beginners' guide") и войдите как **root**.

## Настройка живой среды для использования SSH

**Обратите внимание:** Следующие команды должны быть выполнены от root-пользователя. #-приглашения были намеренно исключены из листингов для обеспечения возможности копировать и вставлять их в целевую область.

Целевая машина должна быть представлена root-приглашением **[root@archiso ~]#** с этого момента.

Во-первых, настройте сеть на целевой машине:

```
 aif -p partial-configure-network

```

Эта строка покажет Вам список известных интерфейсов; введите интерфейс, который хотите использовать (пример: eth0 для проводного Ethernet-интерфейса)

Во-вторых, синхронизируйте живую среду с зеркалом, установите openssh пакет, затем запустите его:

```
pacman -S openssh
rc.d start sshd

```

{
**Обратите внимание:** В зависимости от версии установочного носителя, pacman может попросить обновить сначала **себя**. Так как цель - просто установить openssh, рекомендуется отклонить данный запрос и просто установить пакет.

Наконец, установите пароль администратора (он необходим для ssh-соединения); по умолчанию пароль для root пустой.

```
passwd

```

## Подключение к целевому ПК через SSH

Подключитесь к целевому ПК используя следующую команду:

```
$ ssh root@ip.address.of.target

```

Теперь ПК представлен приветственным сообщение live-среды и позволяет администрировать себя как если бы Вы сидели за его клавиатурой.

```
ssh root@10.1.10.105
root@10.1.10.105's password: 
Last login: Thu Dec 23 08:33:02 2010 from 10.1.10.200
**************************************************************
* To begin installation, run /arch/setup                     *
* You can find documentation at                              *
*  /usr/share/aif/docs/official_installation_guide_en        *
*                                                            *
* i18n: Use the 'km' utility to change your keyboard layout  *
*       and console font.                                    *
*                                                            *
* If you are looking to install Arch on something more       *
* exotic, such as your kerosene-powered cheese grater,       *
* please consult http://wiki.archlinux.org.                  *
*                                                            *
**************************************************************
[root@archiso ~]#
```

### Замечания

*   Если целевой ПК защищён фаерволом/роутером, стандартный 22 порт ssh, очевидно, need to be forward to the target machine's LAN IP address. The use of port forwarding is not covered in this guide.
*   One can edit `/etc/ssh/sshd_config` on the live environment prior to starting the daemon for example to run on a non-standard port if desired.

## Следующие шаги

Предел - небо. Если Вы хотите просто установить Arch, выполните `/arch/setup`. Если Вы намереваетесь исправить уже установленный, но по каким-то причинам сломавшийся Linux, следуйте [Install from Existing Linux](/index.php/Install_from_Existing_Linux "Install from Existing Linux") вики-статье.

Хотите [grub2](/index.php/Grub2 "Grub2") или возможность использовать [GPT](/index.php/GPT "GPT") HDD?

*   Вручную разбейте целевой HDD/SDD используя утилиту **gdisk**, установленную с помощью _pacman -S gdisk_ перед запуском arch-установщика и когда появится опция для установки загрузчика (boot loader), просто ответьте нет и перейдите в live-среду командной строки администратора.
*   Установка grub2 с этого момента тривиальна. Просто используйте chroot в свежеустановленную arch-систему (по умолчанию примонтированную, если Вы только что её устанавливали) затем установите и настройте grub2:

```
cd /mnt
rm console ; mknod -m 600 console c 5 1
rm null ; mknod -m 666 null c 1 3
rm zero ; mknod -m 666 zero c 1 5
mount -t proc proc /mnt/proc
mount -t sysfs sys /mnt/sys
mount -o bind /dev /mnt/dev
chroot /mnt /bin/bash

```

Теперь внутри свежего Arch-chroot'а:

```
pacman -S grub2
grep -v rootfs /proc/mounts > /etc/mtab

```

Edit `/etc/default/grub` to your liking. Install grub and generate a grub.cfg

```
grub-install /dev/sdX --no-floppy
grub-mkconfig -o /boot/grub/grub.cfg

```

**Обратите внимание:** The above assumes that if the user intends to boot from a GPT disk, the user has fully read and understood the aforementioned wiki articles and has made a 1M partition ef02 for grub2.

When ready to reboot into the new Arch install, exit the chroot and unmount the partitions prior to a reboot of the system.

```
exit
umount /mnt/boot   # if mounted this or any other separate partitions
umount /mnt/{proc,sys,dev}
umount /mnt

```