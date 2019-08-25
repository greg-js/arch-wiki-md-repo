هذا المُستند يقوم بشرح كيفية إنشاء ملف يحتوي على صورة قرص لتوزيعة Arch Linux . صورة القرص يمكنها العمل على أحد برامج الآلة الافتراضية [QEMU](/index.php/QEMU "QEMU"), [VirtualBox](/index.php/VirtualBox "VirtualBox"), أو [VMware](/index.php/VMware "VMware"), و يمكنك تخصيصها كيفما تشاء .

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Archiso](#Archiso)
*   [2 تنصيب Arch Linux داخل صورة قرص باستخدام وسيط التنصيب](#تنصيب_Arch_Linux_داخل_صورة_قرص_باستخدام_وسيط_التنصيب)
*   [3 تنصيب Arch Linux داخل صورة قرص دون استخدام وسيط التنصيب](#تنصيب_Arch_Linux_داخل_صورة_قرص_دون_استخدام_وسيط_التنصيب)
    *   [3.1 إنشاء ملف خام لصورة القرص](#إنشاء_ملف_خام_لصورة_القرص)
    *   [3.2 إنشاء أنظمة الملفات في القرص الخام](#إنشاء_أنظمة_الملفات_في_القرص_الخام)
        *   [3.2.1 استخدم القرص بأكمله كنظام ملفات وحيد](#استخدم_القرص_بأكمله_كنظام_ملفات_وحيد)
        *   [3.2.2 استخدام عدة قطاعات](#استخدام_عدة_قطاعات)
    *   [3.3 تنصيب الحزم على النظام الضيف](#تنصيب_الحزم_على_النظام_الضيف)
    *   [3.4 Write a fstab file for the guest](#Write_a_fstab_file_for_the_guest)
    *   [3.5 Generate initramfs for the guest](#Generate_initramfs_for_the_guest)
    *   [3.6 تنصيب مُحمل الإقلاع على النظام الضيف](#تنصيب_مُحمل_الإقلاع_على_النظام_الضيف)
        *   [3.6.1 Extlinux](#Extlinux)
        *   [3.6.2 GRUB2](#GRUB2)
    *   [3.7 إزالة الملفات المؤقتة](#إزالة_الملفات_المؤقتة)
    *   [3.8 إقلاع النظام الضيف](#إقلاع_النظام_الضيف)
    *   [3.9 تلميحات](#تلميحات)

## Archiso

إن [الوسيط الافتراضي للتنصيب](https://archlinux.org/download/) هو ملف ISO , لذا يمكنك الإقلاع منها كقرص عادي أو باستخدام سواقة CD-ROM , لكن بما أنها تستخدم نظام ملفات ISO , فلا يمكنك الكتابة عليها دون إعادة إنشاء قرص التنصيب .

يمكنك أيضا إنشاء قرص الحي من توزيعة Arch Linux الخاص بك عن طريق مجموعة أدوات [Archiso](/index.php/Archiso_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9) "Archiso (العربية)") . , لربما يكون هذا هو غرضك لكن مع ذلك فإن Archiso مُصمم لإنشاء أقراص إقلاعية حيّة لكن نظام ملفاتها يكون أيضاً للقراءة فقط ولا يمكن الكتابة عليه .

## تنصيب Arch Linux داخل صورة قرص باستخدام وسيط التنصيب

باستخدام [QEMU](/index.php/QEMU "QEMU"), [VirtualBox](/index.php/VirtualBox "VirtualBox"), أو أي من برامج الآلة الإفتراضية , يُمكنك تنصيب Arch Linux على صورة القرص عن طريق إقلاعه من [وسيط التنصيب](https://archlinux.org/download/) من داخل برنامج الآلة الإفتراضية الذي تستخدمه مُستخدماً وسيط التثبيت كأحد الأقراص الصلبة داخل الآلة الإفتراضية . هذه هي أفضل طريقة لإنشاء صورة قرص وهمي يحوي على Arch Linux , لأن عملية التنصيب داخل الآلة الإفتراضية مشابهة تماماً لتنصيبها على القرص الصلب .

## تنصيب Arch Linux داخل صورة قرص دون استخدام وسيط التنصيب

يمكن أيضاً إنشاء صورة قرص وهمي يحوي على Arch linux باستخدام البرمجيات و الحزم الموجودة على نظام Arch linux المُستضيف , لهذه الطريقة عدة محاسن :

*   لا يتوجب عليك أن تملك قرص التنصيب الخاص بتوزيعة Arch linux .
*   يمكنك تضمين آخر البرمجيات والحزم في صورة القرص و ذلك عن طريق تنصيبهم باستخدام مدير الحزم على النظام المُستضيف .
*   يمكنك تعديل و تخصيص صورة القرص بشكل يمكن أن لا يدعمه مثبت Arch linux .

على أي حال هذه الطريقة أصعب بكثير من الطريقة السابقة , بالإضافة الى ذلك فهي لن تعمل إذا لم يكن هنالك مدير الحزم [pacman](/index.php/Pacman "Pacman") على النظام المُتسضيف (النظام المُستضيف لا يعمل بنظام Arch linux)

في الفقرات التالية سيتم الإارة الى النظام الذي يعمل بتوزيعة Arch linux والذي تعمل عليه حالياً بـ"النظام المُستضيف" , بينما يتم الإشارة الى النظام الذي ستقوم بإنشاء صورة القرص له باسم "النظام الضيف" .

### إنشاء ملف خام لصورة القرص

*   إنشاء ملف خام للعمل عليه داخل الآلة الإفتراضية , في المثال التالي سيتم إنشاء ملف بحجم تخزيني يساوي 1GiB :

```
$ dd if=/dev/zero of=archlinux.raw bs=4096 count=262144

```

أو بطريقة اخرى , في أنظمة الأقراص التي تدعم دالة النظام `fallocate()` يمكن تنفيذ التعليمة التالية :

```
$ fallocate -l 1G archlinux.raw

```

*   اذا قمت بتنصيب [QEMU](/index.php/QEMU "QEMU"), يمكنك استخدام `qemu-img create` لإنشاء صورة القرص الخام . التعليمة `qemu-img` يمكنها أيضاً إنشاء صورة قرص لكن بإحدى الصيغ الاخرى كصيغة qcow2 . provided that you export the image using `qemu-nbd` to set up a device that appears to contain the actual data of the disk image.

### إنشاء أنظمة الملفات في القرص الخام

#### استخدم القرص بأكمله كنظام ملفات وحيد

إذا لم تكن هناك الحاجة الى إنشاء عدة قطاعات في نظام Arch linux الضيف , فتكون أسهل طريقة بإنشاء نظام ملفات وحيد على القرص الخام , لإنشاء نظام ملفات ext4 قم بتنفيذ التعليمة التالية :

```
$ mkfs.ext4 -F archlinux.raw

```

#### استخدام عدة قطاعات

أو يمكنك استخدام الفطاعات على صورة القرص , في المثال البسيط التالي سنقوم بتقطيع القرص الى قطاع واحد فقط وجعله قطاع رئيسي إقلاعي تمت تهيئته كنظام ملفات [ext4](/index.php/Ext4 "Ext4") يحوي على كامل نظام الملفات الخاص بالنظام الضيف. دون وجود قرص [swap](/index.php/Swap "Swap") .

*   قم بتقطيع القرص

```
$ fdisk archlinux.raw <<< '
$ > o
$ > n
$ > p
$ > 1
$ >
$ >
$ > a
$ > 1
$ > w'

```

*   قم بتقطيع بجعل القطاعات متوفرة كأقراص قابلة للإسترجاع loopback , التعلمات التالية تعتبر أن القرص القابل للإسترجاع للملف `archlinux.raw` هو `/dev/loop0`, لكن الرقم يمكن أن يكون أعلى إذا كان لديك أقراص قابلة للإسترجاع اخرى .

```
# losetup -f --show archlinux.raw
# kpartx -a /dev/loop0

```

**ملاحظة** `kpartx` هو جزء من [multipath-tools-git](https://aur.archlinux.org/packages/multipath-tools-git/) المُقدم من [AUR](/index.php/Arch_User_Repository "Arch User Repository"). يمكنك الرجوع الى[QEMU#Mounting a partition from a raw image](/index.php/QEMU#Mounting_a_partition_from_a_raw_image "QEMU") لمعرفة الطرق الاخرى لكي يتم وصل قطاع داخل صورة قرص وهمي , لكن كن حذراً , حيث لا يتم تنصيب GRUB2 بشكل صحيح الى صورة القرص إذا لم يتم إنشاء القرص القابل للإسترجاع باستخدام (`kpartx`).

*   قم بإنشاء انظمة الأقراص في القطاعات التي قمت بإنشائها.

```
# mkfs.ext4 /dev/mapper/loop0p1

```

### تنصيب الحزم على النظام الضيف

*   قم بوصل المجلد الجذر في نظام ملفات النظام الضيف الى مجلد مؤقت :

```
# TMPDIR=/full/path/to/temporary/directory

```

للقيام بتلك المهمة على قرص تم تقطيعه الى قطاعات :

```
# mount /dev/mapper/loop0p1 $TMPDIR

```

أو على قرص لم يتم تقطيعه:

```
# mount archlinux.raw $TMPDIR

```

قم بتنصيب الحزم التي تريد على النظام :

```
# pacstrap $TMPDIR base

```

### Write a fstab file for the guest

*   Add any mountpoints to the guest's [fstab](/index.php/Fstab "Fstab") file. In this example, we just need a mountpoint for the guest's root filesystem. You do not have to specify it by UUID, but it is a good idea to do so because it guarantees that the root partition will be found regardless of what type of disk is emulated.

```
# UUID=$(blkid -s UUID -o value /dev/mapper/loop0p1)
# echo "UUID=$UUID   /   ext4   defaults   0   1" >> $TMPDIR/etc/fstab 

```

### Generate initramfs for the guest

As noted earlier, [initramfs](/index.php/Initramfs "Initramfs") generation failed when installing [linux](https://www.archlinux.org/packages/?name=linux).

*   You may need to edit `$TMPDIR/etc/mkinitcpio.conf` to remove the `autodetect` hook, to stop your host system's hardware configuration from removing essential modules (e.g. those needed to access the root filesystem) from the [initramfs](/index.php/Initramfs "Initramfs") of the guest, which is going to be running in a different environment in a virtual machine. In addition, it would be a good idea to have the MODULES line read

```
MODULES="virtio_blk virtio_pci"

```

so that it will be possible to boot your Arch Linux guest using a paravirtualized block device.

*   Generate the initramfs for the guest manually by running the following command:

```
# mkinitcpio -g $TMPDIR/boot/initramfs-linux.img -k $TMPDIR/boot/vmlinuz-linux -c $TMPDIR/etc/mkinitcpio.conf

```

### تنصيب مُحمل الإقلاع على النظام الضيف

بخصوص مُحمل الإقلاع, يمكنك الإختيار بين [Extlinux](/index.php/Extlinux "Extlinux"), [GRUB2](/index.php/GRUB2 "GRUB2"), أو غيرها من محملات الإقلاع. وبسبب المشاكل التي تحدث عند تنصيب GRUB2 في هذه الحالة , أنا أقترح تنصيب Extlinux

#### Extlinux

*   تنصيب Extlinux على قطاع الإقلاع في النظام الضيف .

```
# extlinux --install $TMPDIR/boot

```

*   تنصيب MBR الخاص بـ"Syslinux" (فقط للأقراص التي تحوي على قطاعات)

```
# dd if=/usr/lib/syslinux/mbr.bin conv=notrunc bs=440 count=1 of=/dev/loop0

```

*   إنشاء ملف إعدادات لمُحمل الإقلاع Extlinux , قم باستبدال $UUID بقيمة UUID الخاصة بنظام ملفات الذي يستخدمه النظام الضيف.

 `$TMPDIR/boot/extlinux.conf` 
```
DEFAULT archlinux
LABEL   archlinux
SAY     Booting Arch Linux
LINUX   /boot/vmlinuz-linux
APPEND  root=/dev/disk/by-uuid/$UUID ro
INITRD  /boot/initramfs-linux.img

```

**Note:** لكي يتم الإقلاع من القطاع الرئيسي MBR في الإقراص التي تم تقطيعها الى قطاعات باستخدام مُحمل الإقلاع Extlinux ; يجب أن يُحدد القطاع كقطاع إقلاعي .

#### GRUB2

في هذا المثال سنقوم بتنصيب مُحمل الإقلاع [GRUB2](/index.php/GRUB2 "GRUB2") على قرص تم تقطيعه الى قطاعات في النظام الضيف , تأكد من وجود الحزمة [grub2-bios](https://www.archlinux.org/packages/?name=grub2-bios) منصبةً على جهازك المُستضيف .

**ملاحظة:** يمكن أن تقع في عدد من المشاكل عندما تُحاول تنصيب GRUB2 على قرص وهمي . يبدو أنه يعمل فقط على القطاعات المتوفرة كأقراص قابلة للإسترجاع تم إنشاءها يواسطة device mapper , وليس الأقراص التي تم إنشاءها باستخدام `loop` , إضافة الى ذلك فإن GRUB سيفشل في التعرف الى نظام الملفات ext4 الخاص بك , لذلك أنصحك بإستخدام Extlinux إذا لم يكن لديك أسباب خاصة لإستخدام GRUB .

*   قم الآن بتنصيب GRUB2 مُحدداً قيمة الخيار `--boot-directory` الى المجلد `/boot` في نظام ملفات النظام الضيف , لكن إحذر أن تقوم عن طريق الخطأ بإعادة كتابة مُحمل الإقلاع الخاص بجهازك المُستضيف .

```
# grub-install --boot-directory=$TMPDIR/boot /dev/loop0

```

*   الآن قم بكتابة ملف `grub.cfg` مُستبدلاً $UUID, بقيمة UUID الخاصة بنظام ملفات الذي يستخدمه النظام الضيف.

 `$TMPDIR/boot/grub/grub.cfg` 
```
set default="0"
set timeout="3"
insmod msdospart
insmod ext2
set root='(/dev/sda, msdos1)'
search --no-floppy --fs-uuid --set=root $UUID
menuentry "Arch Linux" {
   linux /boot/vmlinuz-linux root=/dev/disk/by-uuid/$UUID ro
   initrd /boot/initramfs-linux.img
}

```

### إزالة الملفات المؤقتة

لا يتوجب عليك إقلاع النظام الضيف بينما نظام ملفاته مايزال موصولاً لأن ذلك قد يُسبب بإتلاف الملفات , لذا قم بفصل نظام ملفات النظام الضيف و إزالة أقراص الإرجاع .

```
# umount $TMPDIR
# kpartx -d /dev/loop0
# losetup -d /dev/loop0

```

### إقلاع النظام الضيف

في النهاية قم بإقلاع النظام الضيف الذي يعمل بتوزيعة Arch Linux بإستخدام أحد برامج الآلة الإفتراضية كبرنامج [QEMU](/index.php/QEMU "QEMU"):

```
# qemu archlinux.raw

```

**تلميحة:** If you have built the virtio block drivers into your guest's initramfs, then you can boot it using a paravirtualized block device. Combine it with [KVM](/index.php/KVM "KVM") and a minimal Arch Linux guest will boot to a login prompt in as little as 3 seconds after starting QEMU.
```
# qemu-system-x86_64 -enable-kvm -drive file=archlinux.raw,media=disk,if=virtio

```

### تلميحات

*   إذا كنت تستخدم QEMU كبرنامج آلة إفتراضية , فيمكنك تحديد النواة المُستخدمة و initramfs للنظام الضيف عن طريق سطر الأوامر . إذا قُمت بذلك فلن تحتاج الى مُحمل إقلاع في صورة القرص الخاص بك ولا الى تنصيب حزمة [linux](https://www.archlinux.org/packages/?name=linux).

*   بما أنك تستطيع التحكم الكامل بالعتاد الذي يعمل عليه النظام الضيف . فليس من الصعب أن تقوم ببناء نواة خاصة بك من المصدر تحوي على جميع الواحدات التي تحتاجها فقط .

*   يمكنك إنشاء عدة نسخ من صورة القرص الذي قُمت بإنشاء و تشغيل أكثر من آلة إفتراضية تعمل على Arch linux في آن واحد .

*   See [Install from existing Linux](/index.php/Install_from_existing_Linux "Install from existing Linux") for some more general tips about installing Arch Linux from an existing Linux installation that doesn't necessarily have to be Arch Linux.