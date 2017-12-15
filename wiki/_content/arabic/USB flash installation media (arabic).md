Related articles

*   [CD Burning](/index.php/CD_Burning "CD Burning")

هذه الصفحة تناقش الطرق المتعددة في كتابة نسخة آرتش لينوكس على قرص USB (كما تسمى أيضاً *قرص فلاش، ذاكرة USB، مفتاح USB* ... إلخ)، والنتيجة ستكون نظام مشابه لـ LiveCD (يمكنك تسميته *"LiveUSB"* إن أردت) والذي وبطبيعة [SquashFS](https://en.wikipedia.org/wiki/SquashFS "wikipedia:SquashFS") فإنه سيقوم بنبذ كل التغييرات بمجرد إيقاف تشغيل الحاسوب.

إن كنت ترغب بالقيام بعملية تثبيت كاملة لآرتش لينوكس من قرص USB (أي مع الإعدادات المستمرة) قم بالاطلاع على [Installing Arch Linux on a USB key](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key").

**ملاحظة:** للإقلاع عبر [UEFI](/index.php/UEFI "UEFI") قم بالاطلاع على [هذه الإرشادات](/index.php/UEFI#Create_UEFI_bootable_USB_from_ISO "UEFI").

## Contents

*   [1 في أنظمة جنو/لينوكس](#.D9.81.D9.8A_.D8.A3.D9.86.D8.B8.D9.85.D8.A9_.D8.AC.D9.86.D9.88.2F.D9.84.D9.8A.D9.86.D9.88.D9.83.D8.B3)
    *   [1.1 إعادة الكتابة على ذاكرة USB](#.D8.A5.D8.B9.D8.A7.D8.AF.D8.A9_.D8.A7.D9.84.D9.83.D8.AA.D8.A7.D8.A8.D8.A9_.D8.B9.D9.84.D9.89_.D8.B0.D8.A7.D9.83.D8.B1.D8.A9_USB)
        *   [1.1.1 كيفية استرجاع قرص USB](#.D9.83.D9.8A.D9.81.D9.8A.D8.A9_.D8.A7.D8.B3.D8.AA.D8.B1.D8.AC.D8.A7.D8.B9_.D9.82.D8.B1.D8.B5_USB)
    *   [1.2 بدون إعادة الكتابة على ذاكرة USB](#.D8.A8.D8.AF.D9.88.D9.86_.D8.A5.D8.B9.D8.A7.D8.AF.D8.A9_.D8.A7.D9.84.D9.83.D8.AA.D8.A7.D8.A8.D8.A9_.D8.B9.D9.84.D9.89_.D8.B0.D8.A7.D9.83.D8.B1.D8.A9_USB)
        *   [1.2.1 باستخدام UNetbootin](#.D8.A8.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_UNetbootin)
*   [2 في نظام Mac OS X](#.D9.81.D9.8A_.D9.86.D8.B8.D8.A7.D9.85_Mac_OS_X)
*   [3 في Windows](#.D9.81.D9.8A_Windows)
    *   [3.1 برنامج Image Writer](#.D8.A8.D8.B1.D9.86.D8.A7.D9.85.D8.AC_Image_Writer)
    *   [3.2 برنامج USBWriter](#.D8.A8.D8.B1.D9.86.D8.A7.D9.85.D8.AC_USBWriter)
    *   [3.3 طريقة Flashnul](#.D8.B7.D8.B1.D9.8A.D9.82.D8.A9_Flashnul)
    *   [3.4 طريقة Cygwin](#.D8.B7.D8.B1.D9.8A.D9.82.D8.A9_Cygwin)
    *   [3.5 أداة dd في Windows](#.D8.A3.D8.AF.D8.A7.D8.A9_dd_.D9.81.D9.8A_Windows)
    *   [3.6 إقلاع ملف ISO من الذاكرة العشوائية RAM](#.D8.A5.D9.82.D9.84.D8.A7.D8.B9_.D9.85.D9.84.D9.81_ISO_.D9.85.D9.86_.D8.A7.D9.84.D8.B0.D8.A7.D9.83.D8.B1.D8.A9_.D8.A7.D9.84.D8.B9.D8.B4.D9.88.D8.A7.D8.A6.D9.8A.D8.A9_RAM)
*   [4 استكشاف الأخطاء وإصلاحها](#.D8.A7.D8.B3.D8.AA.D9.83.D8.B4.D8.A7.D9.81_.D8.A7.D9.84.D8.A3.D8.AE.D8.B7.D8.A7.D8.A1_.D9.88.D8.A5.D8.B5.D9.84.D8.A7.D8.AD.D9.87.D8.A7)
*   [5 انظر أيضاً](#.D8.A7.D9.86.D8.B8.D8.B1_.D8.A3.D9.8A.D8.B6.D8.A7.D9.8B)

## في أنظمة جنو/لينوكس

### إعادة الكتابة على ذاكرة USB

**تحذير:** هذه العملية ستتلف جميع البيانات على القرص `/dev/sd**x**` بدون القدرة على استرجاعها.

**ملاحظة:** هذه الطريقة لا تعمل مع UEFI.

**ملاحظة:** بواسطة الأمر `lsblk` قم بالتأكد من أن جهاز USB **غير** مربوط بالنظام unmounted، ولا تنسى اختيار `/dev/sd**x**` بدلاً من `/dev/sd**x1**` **فهذه أخطاء شائعة كثيراً!**

```
# dd bs=4M if=/path/to/archlinux.iso of=/dev/sd**x**

```

**ملاحظة:** بعض البرامج الثابتة firmware لا تستطيع فهم الـ isohybrid hack حيث تكون بداية انزياح القسم المزيف هي 0، اطلع على الرابط [https://bugs.archlinux.org/task/32189](https://bugs.archlinux.org/task/32189) للمزيد.

#### كيفية استرجاع قرص USB

صورة ISO هجينة أي أنه يمكن حرقها على قرص مضغوط أو كتابتها مباشرة إلى ذاكرة USB، ولهذا السبب فإنها لا تتضمن جدول تقسيم معياري.

بعد الانتهاء من تثبيت آرتش لينوكس بوساطة ذاكرة USB يجب عليك أن تُصَفِّر أول 512 بايت فيها لكي تسترجع كامل المساحة المتوفرة عليها *(هذه الـ 512 بايت تمثل كود الإقلاع في MBR وجدول التقسيم الغير معياري)*، وذلك عن طريق الأمر:

```
# dd count=1 bs=512 if=/dev/zero of=/dev/sd**x**

```

ثم قم بإنشاء جدول تقسيم جديد (على سبيل المثال: "msdos") ونظام ملفات (على سبيل المثال: EXT4 أو FAT32) بواسطة برنامج [gparted](https://www.archlinux.org/packages/?name=gparted) أو باستخدام الطرفية:

*   من أجل EXT2/3/4 (عَدِّل mkfs.ext4 وفقاً لاختيارك) قم بالتالي:

```
# cfdisk /dev/sd**x**
# mkfs.ext4 /dev/sd**x1**
# e2label /dev/sd**x1** USB_STICK

```

*   من أجل FAT32 قم بتثبيت حزمة [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) ومن ثم نفذ:

```
# cfdisk /dev/sd**x**
# mkfs.vfat -F32 /dev/sd**x1**
# dosfslabel /dev/sd**x1** USB_STICK

```

### بدون إعادة الكتابة على ذاكرة USB

هذه الطريقة أكثر تعقيداً من طريقة كتابة صورة ISO مباشرة بواسطة الأمر `dd` لكنها تُبقي ذاكرة USB قابلة للاستخدام ولتخزين البيانات، قبل البدء تأكد من أن ذاكرة USB مُهيئة وفقاً لنظام الملفات FAT32 أو EXT2/3/4 أو Btrfs، من أجل الإقلاع عبر [UEFI](/index.php/UEFI "UEFI") أو للتشغيل على أنظمة التشغيل الأخرى يتوجب عليك اختيار FAT32، كما تأكد من أن حزمة *syslinux* مثبتة لديك (نسخة 4.04 أو أحدث).

**1.** قم باستخراج مجلد `arch` من ملف ISO وضعه في ذاكرة USB، ومن أجل لوحات الأم الداعمة لـ UEFI قم بالاطلاع على [هذا](/index.php/UEFI#Create_UEFI_bootable_USB_from_ISO "UEFI").

**2.** قم بتثبيت مُحَمِّل الإقلاع Syslinux:

**تحذير:** انتبه جيداً للمسارات التي تختارها أثناء تنفيذك للأمر `dd` والرجاء تحديد القرص **نفسه** أثناء استعمال الأمر السابق و**ليس** القسم الأول منه فهذا خطأ شائع جداً.

**ملاحظة:** في بعض التوزيعات فإن ملف `mbr.bin` من الممكن أن يتواجد في `/usr/**share**/syslinux/mbr.bin`.

```
$ cd /*path/to/folder*/arch/boot/syslinux #حيث أن *path/to/folder* هو المجلد الذي تم ربط قرص USB فيه
# extlinux --install .                       #اكتب هذا السطر كما تراه تماماً ولا تنسى النقطة (.)
# dd bs=440 conv=notrunc count=1 if=/usr/lib/syslinux/mbr.bin of=/dev/sd**x**
# parted /dev/sd**x** toggle 1 boot

```

**3.** اضبط ملفات التكوين:

**تحذير:** الفشل في تسمية القرص "`ARCH_2013XX`" (حيث XX تتغير بحسب الشهر الصادرة فيه النسخة) أو الفشل في استخدام [UUID](/index.php/UUID "UUID") (لإعادة تعيين عنوان له وفقاً لما تريد) **سيجلب** لك الخطأ "30 seconds".

لاستبدال جزء `archisolabel=ARCH_2013XX` بالمناسب له `archiso**device**=/dev/disk/by-uuid/47FA-4071` ومن أجل ملفي التكوين في نفس الوقت وعن طريق أمر واحد نَفِّذ السطر التالي:

**ملاحظة:** عَدِّل `/dev/sd**x1**` قبل تنفيذ الأمر وإلا سيصبح فارغاً (لأن قرص `sd**x**` غير موجود).

```
$ sed -i "s|label=ARCH_.*|device=/dev/disk/by-uuid/$(blkid -o value -s UUID /dev/sd**x1**)|" archiso_sys{32,64}.cfg

```

إذا كانت حزمة *syslinux* على توزيعتك أقدم من النسخة 4.06 يجب استبدال السطر `APPEND` في ملف `syslinux.cfg`وذلك كحل لأنظمة FAT32 (غير ضروري لأنظمة EXT4):

```
$ sed -i "s|../../|/arch|" syslinux.cfg

```

#### باستخدام UNetbootin

يمكن استخدام برنامج UNetbootin على أي توزيعة لينوكس أو على ويندوز من أجل نسخ ملف ISO إلى قرص USB، غير أن UNetbootin يعيد الكتابة فوق ملف syslinux.cfg وبالتالي يُنشئ قرص USB لا يُقلع بشكل جيد، لهذا السبب **فإن استخدام Unetbootin لا ينصح به** - الرجاء استخدم `dd` أو أحد الطرق الأخرى المشروحة في هذه الصفحة.

**تحذير:** يقوم UNetbootin بالكتابة فوق ملف `syslinux.cfg` الافتراضي، يجب استرجاع الملف قبل أن يقلع قرص USB بشكل صحيح.

قم بتعديل ملف `syslinux.cfg`:

 `sysconfig.cfg` 
```
default menu.c32
prompt 0
menu title Archlinux Installer
timeout 100

label unetbootindefault
menu label Archlinux_x86_64
kernel /arch/boot/x86_64/vmlinuz
append initrd=/arch/boot/x86_64/archiso.img archisodevice=/dev/sd**x1** ../../

label ubnentry0
menu label Archlinux_i686
kernel /arch/boot/i686/vmlinuz
append initrd=/arch/boot/i686/archiso.img archisodevice=/dev/sd**x1** ../../
```

في الجزء `/dev/sd**x1**` يجب عليك استبدال **x** بأول حرف غير مستخدم من قبل النظام الذي ستُثبِّت آرتش لينوكس عليه (على سبيل المثال: إذا كنت تملك قرصين صلبين فاختر الحرف `c`.)، يمكنك القيام بهذا الأمر أثناء المرحلة الأولى من عملية الإقلاع عن طريق الضغط على مفتاح `Tab` عند ظهور القائمة.

## في نظام Mac OS X

لكي تتمكن من استخدام الأداة `dd` في نظام التشغيل Mac يجب القيام بعدة خطوات، في البداية قم بوصل قرص USB بالحاسوب، سيقوم نظام OS X بربطه تلقائياً ومن ثم قم بتنفيذ التالي داخل `Terminal.app`:

```
$ diskutil list

```

قم بمعرفة ما هو اسم قرص USB الخاص بك عن طريق `mount` أو `sudo dmesg | tail` (مثلاً سيكون اسمه `/dev/disk1`)، ثم قم بفصل unmount الأقسام من على القرص (أي القسم /dev/disk1s1):

```
$ diskutil unmountDisk /dev/disk1

```

الآن نكمل وفقاً للإرشادات أعلاه (لكن حدد القيمة `bs=8192` إذا كنت تستخدم OS X `dd`، الرقم السابق أتى من `1024*8`).

 `dd if=image.iso of=/dev/disk1 bs=8192` 
```
20480+0 records in
20480+0 records out
167772160 bytes transferred in 220.016918 secs (762542 bytes/sec)

```

من الجيد أن تقوم بفصل القرص eject قبل إزالته من الحاسوب في هذه المرحلة:

```
$ diskutil eject /dev/disk1

```

## في Windows

### برنامج Image Writer

حَمِّل البرنامج من الموقع [http://sourceforge.net/projects/usbwriter/](http://sourceforge.net/projects/usbwriter/) وقم بتشغيله ثم حدد ملف آرتش المراد نسخه وذاكرة USB التي سيُنسخ عليها، متصفح الملفات Win32 Disk Imager's يفترض أن ملفات الصور تنتهي باللاحقة `.img` فإذا كانت الصورة لديك لاحقتها `.iso` فيجب عليك كتابة اسمها بنفسك، هذا الاختلاف في اللواحق هو اختلاف شكلي فقط فالصورة ستكتب على الذاكرة بشكل سليم بغض النظر عن اللاحقة، انقر على زر `write`، الآن من المفروض أن تكون قادراً على الإقلاع من ذاكرة USB وتثبيت آرتش لينوكس منها.

### برنامج USBWriter

حَمِّل البرنامج من [http://sourceforge.net/projects/usbwriter/](http://sourceforge.net/projects/usbwriter/) وقم بتشغيله، ثم حدد ملف آرتش المطلوب وذاكرة USB المطلوبة وانقر على زر `write`، الآن من المفروض أن تكون قادراً على الإقلاع من ذاكرة USB وتثبيت آرتش لينوكس منها.

### طريقة Flashnul

[flashnul](http://shounen.ru/soft/flashnul/) عبارة عن أداة للتحقق من تشغيل وصيانة ذواكر الفلاش (USB-Flash, IDE-Flash, SecureDigital, MMC, MemoryStick, SmartMedia, XD, CompactFlash ... إلخ).

من سطر الأوامر قم باستدعاء flashnul مع الخيار `-p` واعرف ما هو الرقم التسلسلي لقرص USB الخاص بك، على سبيل المثال:

 `C:\>flashnul -p` 
```
Avaible physical drives:
Avaible logical disks:
C:\
D:\
E:\

```

بعد تحديدك للقرص الصحيح يمكنك كتابة الصورة على القرص عن طريق استدعاء flashnul مع الرقم التسلسلي (أي الحرف) للقرص إضافة إلى الخيار `-L` والمسار المتواجدة فيه الصورة المطلوب كتابتها، على سبيل المثال:

```
C:\>flashnul **E:** -L *path\to\arch.iso*

```

اكتب yes ثم انتظر قليلاً حتى يتم الانتهاء من الكتابة، إذا حصلت على الخطأ "غير مسموح بالوصول access denied" قم بإغلاق كل نوافذ المتصفح المفتوحة.

في نسختي Vista أو Win7 يجب عليك تشغيل سطر الأوامر console كمدير نظام administrator وإلا فإن flashnul سيفشل في فتح قرص USB كجهاز تخزين وسوف يكون قادراً فقط على الكتابة بواسطة الأدوات المقدمة من windows.

**ملاحظة:** يجب عليك استعمال حرف القرص الصلب بدلاً من رقمه، flashnul 1rc1, Windows 7 x64.

### طريقة Cygwin

قم بالتأكد من أن عملية تثبيت [Cygwin](http://www.cygwin.com/) تتضمن حزمة `dd`، أما إذا كنت لا ترغب في تثبيت Cygwin فتستطيع أن تحمل حزمة `dd` لنظام التشغيل Windows من الموقع [http://www.chrysocome.net/dd](http://www.chrysocome.net/dd).

قم بوضع ملف الصورة في مجلد المنزل:

```
C:\cygwin\home\John\

```

قم بتشغيل Cygwin كمدير نظام (لكي يتمكن Cygwin من الوصول إلى العتاد hardware)، للكتابة على قرص USB نفذ الأمر التالي:

```
dd if=image.iso of=\\.\[x]:

```

حيث أن image.iso هو المسار المتواجد فيه ملف ISO ضمن المجلد cygwin، أما `\\.\[**x**]`: فهو قرص USB الخاص بك حيث أن **x** هو حرف القرص الصلب على سبيل المثال `\\.\d:`.

في حال النسخة 6.0 من Cygwin استعمل الأمر التالي لكي تعرف القسم الصحيح:

```
cat /proc/partitions

```

ثم اكتب ملف ISO على ذاكرة USB وفقاً للمعلومات الصادرة من الأمر السابق، على سبيل المثال:

**تحذير:** هذا الأمر سيحذف نهائياً كل الملفات المتواجدة على ذاكرة USB، الرجاء التأكد من عدم وجود أي ملفات مهمة على الذاكرة قبل القيام بتنفيذ الأمر.

```
dd if=image.iso of=/dev/sdb

```

### أداة dd في Windows

تتوفر نسخة من أداة dd مرخصة برخصة GPL لنظام التشغيل Windows على الموقع [http://www.chrysocome.net/dd،](http://www.chrysocome.net/dd،) ميزة تحميل أداة dd هذه أن الكمية المطلوب تحميلها من الإنترنت أقل بكثير من تحميل Cygwin، استعمل نفس إرشادات Cygwin السابقة للتعامل مع dd.

### إقلاع ملف ISO من الذاكرة العشوائية RAM

هذه الطريقة تتطلب [Syslinux](/index.php/Syslinux "Syslinux") و **[MEMDISK](http://www.syslinux.org/wiki/index.php/MEMDISK)** لتحميل ملف ISO كاملاً إلى ذاكرة RAM لذا تأكد من توفر ذاكرة RAM كافية لديك، حالما ينتهي التحميل وترى القائمة الرسومية يمكنك إزالة قرص USB أو حتى أن تضعه في حاسوب آخر وتعيد نفس العملية عليه، كما تسمح هذه الطريقة بإقلاع وتثبيت آرتش من (أو إلى) نفس قرص USB.

**1.** قم بتهيئة Format قرص USB إلى نظام الملفات FAT32 ومن ثم أنشئ هذه المجلدات:

```
X:\Boot
X:\Boot\ISOs
X:\Boot\Settings

```

**2.**انسخ ملف ISO المراد الإقلاع منه إلى المجلد `ISOs` (على سبيل المثال: ملف `archlinux-2013.04.01-dual.iso`)، ثم استخرج الملفات التالية من **[النسخة الأخيرة](http://www.kernel.org/pub/linux/utils/boot/syslinux/)** (على سبيل المثال: `syslinux-4.05.zip`):

*   استخرج `./win32/syslinux.exe` إلى سطح المكتب أو أي مكان تريده.
*   استخرج `./memdisk/memdisk` إلى مجلد `Settings`.

وبينما أنت في هذا المجلد قم بإنشاء ملف `syslinux.cfg`:

 `X:\Boot\Settings\syslinux.cfg` 
```
DEFAULT arch_iso

LABEL arch_iso
        MENU LABEL Arch Setup
        LINUX memdisk
        INITRD /Boot/ISOs/archlinux-2013.04.01-dual.iso
        APPEND iso
```

**تلميحة:** إذا كنت ترغب بإضافة المزيد من التوزيعات فيمكنك تعديل هذا الملف (تم تجربة توزيعة Debian و Parted Magic)، وأيضاً يمكنك إضافة قائمة جميلة له وصورة للخلفية بدلاً من الإعدادات الافتراضية، اطلع على ويكي [Syslinux](/index.php/Syslinux "Syslinux").

**3.** وأخيراً قم بإنشاء ملف `*.bat` في المجلد الموجود فيه ملف `syslinux.exe` ثم قم بتشغيله (كمدير نظام "Run as administrator" في حال استعمال Vista أو Windows 7):

 `C:\Documents and Settings\username\Desktop\install.bat` 
```
@echo off
syslinux.exe -m -a -d /Boot/Settings X:
```

انتهى.

## استكشاف الأخطاء وإصلاحها

**ملاحظة:** في طريقة [MEMDISK Method](#Boot_the_entire_ISO_from_RAM) إذا صادفك الخطأ الشائع "30 seconds" في حال قيامك بالإقلاع من نسخة i686 فقم بالضغط على المفتاح `Tab`بعد الوقوف على الخيار `Boot Arch Linux (i686)` وأضف `vmalloc=448M` في النهاية، مرجع: *إذا كانت صورة ISO أكبر من 128 ميغابايت وكنت تملك نظام تشغيل 32 بت يتوجب عليك زيادة الحد الأقصى لاستعمال الذاكرة الخاص بـ vmalloc* [(*)](http://www.syslinux.org/wiki/index.php/MEMDISK#-_memdiskfind_in_combination_with_phram_and_mtdblock)

**ملاحظة:** إذا ظهر لك خطأ "30 seconds" بسبب أن المجلد `/dev/disk/by-label/ARCH_XXXXXX` لا يمكن ربطه، قم بإعادة تسمية قرص USB إلى `ARCH_XXXXXX` (على سبيل المثال: `ARCH_201302`).

## انظر أيضاً

*   [Gentoo liveusb document](http://www.gentoo.org/doc/en/liveusb.xml)