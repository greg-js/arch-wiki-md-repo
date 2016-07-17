هذا المستند سيرشدك خلال عملية تثبيت [Arch Linux](/index.php/Arch_Linux "Arch Linux") باستخدام [Arch Install Scripts](https://projects.archlinux.org/arch-install-scripts.git/). قبل التثبيت, ننصحك بإلقاء نظرة على [FAQ](/index.php/FAQ "FAQ").

الصفحة الرئيسية للمجتمع على [ArchWiki](https://wiki.archlinux.org/index.php/Main_page_%28%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9%29) هي المورد الأساسي الذي ينبغي استشارته إذا نشأت أي مشاكل.

تعتبر قناة المجتمع (IRC ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux) وأيضا المنتديات [forums](https://bbs.archlinux.org/) مصدرا ممتازا إن لم تجد إجابة عن اﻷسئلة في مكان آخر. وفقا لـ[منهج آرتش](https://wiki.archlinux.org/index.php/The_Arch_Way), نشجعك على أن تكتب man command لقراءة [دليل إرشادات](https://wiki.archlinux.org/index.php/Man_page) أي أمر غير مألوف لك.

**ملاحظة:** يمكن الوصول لهذا الدليل من وسيط التثبيت الحي باستخدام متصفح [ELinks](/index.php/ELinks "ELinks")، وذلك بعد تنفيذ خطوة [#Connect to the Internet](#Connect_to_the_Internet). يمكنك فعل ذلك بالدخول إلى طرفية وهمية جديدة [virtual console](https://en.wikipedia.org/wiki/Virtual_console "w:Virtual console")، والتبديل بين الطرفية التي تستخدمها للتثبيت والطرفية التي تشغل منها المتصفح بـ (`Alt+arrow`). وبشكل مشابه يمكن الدخول ل[غرفة المحادثة الفوريّة](/index.php/IRC "IRC") `#archlinux` باستخدام [irssi](/index.php/Irssi "Irssi").

## Contents

*   [1 التجهيز](#.D8.A7.D9.84.D8.AA.D8.AC.D9.87.D9.8A.D8.B2)
    *   [1.1 وضع UEFI](#.D9.88.D8.B6.D8.B9_UEFI)
    *   [1.2 ضبط تنسيق لوحة المفاتيح keyboard layout](#.D8.B6.D8.A8.D8.B7_.D8.AA.D9.86.D8.B3.D9.8A.D9.82_.D9.84.D9.88.D8.AD.D8.A9_.D8.A7.D9.84.D9.85.D9.81.D8.A7.D8.AA.D9.8A.D8.AD_keyboard_layout)
    *   [1.3 الإتصال بالإنترنت](#.D8.A7.D9.84.D8.A5.D8.AA.D8.B5.D8.A7.D9.84_.D8.A8.D8.A7.D9.84.D8.A5.D9.86.D8.AA.D8.B1.D9.86.D8.AA)
    *   [1.4 تحديث وقت النظام](#.D8.AA.D8.AD.D8.AF.D9.8A.D8.AB_.D9.88.D9.82.D8.AA_.D8.A7.D9.84.D9.86.D8.B8.D8.A7.D9.85)
*   [2 تجهيز وسائط التخزين](#.D8.AA.D8.AC.D9.87.D9.8A.D8.B2_.D9.88.D8.B3.D8.A7.D8.A6.D8.B7_.D8.A7.D9.84.D8.AA.D8.AE.D8.B2.D9.8A.D9.86)
    *   [2.1 تحديد الأجهزة](#.D8.AA.D8.AD.D8.AF.D9.8A.D8.AF_.D8.A7.D9.84.D8.A3.D8.AC.D9.87.D8.B2.D8.A9)
    *   [2.2 أنماط جدولة التقسيم Partition table types](#.D8.A3.D9.86.D9.85.D8.A7.D8.B7_.D8.AC.D8.AF.D9.88.D9.84.D8.A9_.D8.A7.D9.84.D8.AA.D9.82.D8.B3.D9.8A.D9.85_Partition_table_types)
    *   [2.3 أدوات التقسيم](#.D8.A3.D8.AF.D9.88.D8.A7.D8.AA_.D8.A7.D9.84.D8.AA.D9.82.D8.B3.D9.8A.D9.85)
        *   [2.3.1 استخدام parted بالوضع التفاعلي](#.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_parted_.D8.A8.D8.A7.D9.84.D9.88.D8.B6.D8.B9_.D8.A7.D9.84.D8.AA.D9.81.D8.A7.D8.B9.D9.84.D9.8A)
    *   [2.4 إنشاء جدول تقسيم جديد](#.D8.A5.D9.86.D8.B4.D8.A7.D8.A1_.D8.AC.D8.AF.D9.88.D9.84_.D8.AA.D9.82.D8.B3.D9.8A.D9.85_.D8.AC.D8.AF.D9.8A.D8.AF)
    *   [2.5 مخطط التقسيم](#.D9.85.D8.AE.D8.B7.D8.B7_.D8.A7.D9.84.D8.AA.D9.82.D8.B3.D9.8A.D9.85)
        *   [2.5.1 أمثلة UEFI/GPT](#.D8.A3.D9.85.D8.AB.D9.84.D8.A9_UEFI.2FGPT)
        *   [2.5.2 أمثلة BIOS/MBR](#.D8.A3.D9.85.D8.AB.D9.84.D8.A9_BIOS.2FMBR)
    *   [2.6 تهيئة أنظمة الملفات وتفعيل مساحة التبديل swap](#.D8.AA.D9.87.D9.8A.D8.A6.D8.A9_.D8.A3.D9.86.D8.B8.D9.85.D8.A9_.D8.A7.D9.84.D9.85.D9.84.D9.81.D8.A7.D8.AA_.D9.88.D8.AA.D9.81.D8.B9.D9.8A.D9.84_.D9.85.D8.B3.D8.A7.D8.AD.D8.A9_.D8.A7.D9.84.D8.AA.D8.A8.D8.AF.D9.8A.D9.84_swap)
*   [3 التثبيت](#.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA)
    *   [3.1 اختيار المرايا](#.D8.A7.D8.AE.D8.AA.D9.8A.D8.A7.D8.B1_.D8.A7.D9.84.D9.85.D8.B1.D8.A7.D9.8A.D8.A7)
    *   [3.2 تثبيت الحزم الأساسيّة](#.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_.D8.A7.D9.84.D8.AD.D8.B2.D9.85_.D8.A7.D9.84.D8.A3.D8.B3.D8.A7.D8.B3.D9.8A.D9.91.D8.A9)
*   [4 التكوين Configuration](#.D8.A7.D9.84.D8.AA.D9.83.D9.88.D9.8A.D9.86_Configuration)
    *   [4.1 fstab](#fstab)
    *   [4.2 تغيير الجذر Change root](#.D8.AA.D8.BA.D9.8A.D9.8A.D8.B1_.D8.A7.D9.84.D8.AC.D8.B0.D8.B1_Change_root)
    *   [4.3 الإعدادات المحليّة Locale](#.D8.A7.D9.84.D8.A5.D8.B9.D8.AF.D8.A7.D8.AF.D8.A7.D8.AA_.D8.A7.D9.84.D9.85.D8.AD.D9.84.D9.8A.D9.91.D8.A9_Locale)
    *   [4.4 الوقت](#.D8.A7.D9.84.D9.88.D9.82.D8.AA)
    *   [4.5 Initramfs](#Initramfs)
    *   [4.6 تثبيت محمّل الإقلاع](#.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_.D9.85.D8.AD.D9.85.D9.91.D9.84_.D8.A7.D9.84.D8.A5.D9.82.D9.84.D8.A7.D8.B9)
        *   [4.6.1 UEFI/GPT](#UEFI.2FGPT)
        *   [4.6.2 BIOS/MBR](#BIOS.2FMBR)
    *   [4.7 ضبط الشبكة](#.D8.B6.D8.A8.D8.B7_.D8.A7.D9.84.D8.B4.D8.A8.D9.83.D8.A9)
        *   [4.7.1 Hostname](#Hostname)
        *   [4.7.2 سلكي](#.D8.B3.D9.84.D9.83.D9.8A)
        *   [4.7.3 لاسلكي](#.D9.84.D8.A7.D8.B3.D9.84.D9.83.D9.8A)
*   [5 إلغاء توسيع الأقسام وإعادة التشغيل](#.D8.A5.D9.84.D8.BA.D8.A7.D8.A1_.D8.AA.D9.88.D8.B3.D9.8A.D8.B9_.D8.A7.D9.84.D8.A3.D9.82.D8.B3.D8.A7.D9.85_.D9.88.D8.A5.D8.B9.D8.A7.D8.AF.D8.A9_.D8.A7.D9.84.D8.AA.D8.B4.D8.BA.D9.8A.D9.84)
*   [6 ما بعد التثبيت](#.D9.85.D8.A7_.D8.A8.D8.B9.D8.AF_.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA)

## التجهيز

يفترض أن يعمل آرتش لينكس على أي معالج بمعمارية [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) مع 256MB ذاكرة RAM كحد أدنى. يحتاج التثبيت الأساسي لكل الحزم من المجموعة [base](https://www.archlinux.org/groups/x86_64/base/) أقل من 800MB تقريبا من مساحة القرص.

ألق نظرة على [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch") لمعلومات عن تنزيل وسيط التثبيت, وطرق إقلاعها على الجهاز المطلوب. هذا يفترض الدليل أنك تستخدم آخر إصدار.

سيتم تسجيل الدخول تلقائيا بحساب الجذر إلى صدفة [Zsh](/index.php/Zsh "Zsh"). ينصح باستخدام محرر مثل [nano](/index.php/Nano#Usage "Nano") أو [vim](/index.php/Vim#Usage "Vim") للتعديل على ملفات الضبط الموجودة عادة في `/etc`

### وضع UEFI

في حال كان لديك لوحة أم بوضع [UEFI](/index.php/UEFI "UEFI") مفعّل, سيقوم المثبت بتشغيل Arch تلقائيا عبر [systemd-boot](http://www.freedesktop.org/wiki/Software/systemd/systemd-boot/).

للتحقق من أنك أقلعت بوضع UEFI, تحقق أن المجلد التالي موجود:

```
# ls /sys/firmware/efi/efivars

```

انظر إلى [UEFI#UEFI Variables](/index.php/UEFI#UEFI_Variables "UEFI") لمزيد من التفاصيل.

### ضبط تنسيق لوحة المفاتيح keyboard layout

الإعداد الإفتراضي [console keymap](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") مضبوط ليكون [us](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg"). يمكن عرض الخيارات المتاحة بالأمر `localectl list-keymaps`.

على سبيل المثال, لتغيير التنسيق إلى `de-latin1`, نفذ الأمر

```
# loadkeys *de-latin1*

```

إذا ظهرت المحارف بشكل مربعات بيضاء أو رموز آخرى, قم بتغيير [console font](/index.php/Console_fonts "Console fonts"). مثال:

```
# setfont *lat9w-16*

```

### الإتصال بالإنترنت

يتم تفعيل [dhcpcd](/index.php/Dhcpcd "Dhcpcd") daemon عند الإقلاع للأجهزة السلكية, ويحاول إنشاء إتصال. للوصول إلى صفحة تسجيل الدخول, استخدم متصفح [ELinks](/index.php/ELinks "ELinks").

تتحقق من إنشاء الإتصال, بالأمر `ping archlinux.org` مثلا. إذا لم يكن الإتصال متوفرا, انتقل إلى الفقرة [ضبط الشبكة](https://wiki.archlinux.org/index.php/Beginners%27_guide_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9)#.D8.B6.D8.A8.D8.B7_.D8.A7.D9.84.D8.B4.D8.A8.D9.83.D8.A9) أو اتبع أمثلة [netctl](/index.php/Netctl "Netctl") أدناه. في حال نجح الإتصال انتقل إلى [تحديث وقت النظام](https://wiki.archlinux.org/index.php/Beginners%27_guide_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9)#.D8.AA.D8.AD.D8.AF.D9.8A.D8.AB_.D9.88.D9.82.D8.AA_.D8.A7.D9.84.D9.86.D8.B8.D8.A7.D9.85).

	تجهيز Netctl

لمنع التعارض, اوقف الخدمة *dhcpcd* (مستبدلا `enp0s25` بواجهة بطاقة الشبكة السلكية لديك):

```
# systemctl stop dhcpcd@*enp0s25*.service

```

يمكن عرض [واجهات بطاقات الشبكة](/index.php/Network_configuration#Device_names "Network configuration") بالأمر `ip link`, أو `iw dev` للأجهزة اللاسلكية. تكون واجهة الشبكة مسبوقة بـ `en` (سلكي ethernet) , `wl` (لاسلكي WLAN), أو `ww` (WWAN).

	إتصال لاسلكي

لعرض [الشبكات المتاحة](/index.php/Wireless_network_configuration#Getting_some_useful_information "Wireless network configuration"), وإنشاء اتصال من خلال واجهة محددة:

```
# wifi-menu -o *wlp2s0*

```

ملف التكوين الناتج يتم تخزينه في `/etc/netctl`. للأجهزة التي تتطلب اسم مستخدم وكلمة مرور, انظر إلى [WPA2 Enterprise#netctl](/index.php/WPA2_Enterprise#netctl "WPA2 Enterprise").

	غير ذلك

تتوفر العديد من الأمثلة, مثل تكوين [static IP address](/index.php/Network_configuration#Static_IP_address "Network configuration"). انسخ الملف المطلوب إلى `/etc/netctl`, مثلا `ethernet-static`:

```
# cp /etc/netctl/examples/*ethernet-static* /etc/netctl

```

اضبط الملف بحسب الحاجة, وفعّله:

```
# netctl start *ethernet-static*

```

### تحديث وقت النظام

استخدم [systemd-timesyncd](/index.php/Systemd-timesyncd "Systemd-timesyncd") للتأكد من صحّة وقت النظام. لبدأ الخدمة:

```
# timedatectl set-ntp true

```

للتحقق من حالة الخدمة, استخدم `timedatectl status`.

## تجهيز وسائط التخزين

**تحذير:**

*   يؤدي التقسيم أو التهيئة عادة إلى جعل البيانات الموجودة غير قابلة للإستخدام ويتم الكتابة فوقها خلال عمليّات لاحقة مما يؤدي لتدميرها, لهذا السبب, يجب أن تنسخ كل البيانات التي تريد أن تحافظ عليها إحتياطيا قبل البدأ.
*   إذا أردت عمل إقلاع ثنائي dual-booting مع نظام Windows مثبت مسبقا على نظام UEFI/GPT, لا تقم بتهيئة قسم UEFI, على اعتباره يحوي ملف *.efi* المطلوب لإقلاع Windows. بالإضافة لذلك, Arch يجب أن تتبع نفس نظام الإقلاع والتقسيم المستخدم في Windows. انظر إلى [Dual boot with Windows#Important information](/index.php/Dual_boot_with_Windows#Important_information "Dual boot with Windows").

في هذه الخطوة, سيتم تجهيز جهاز التخزين الذي سيستخدمه النظام الجديد. اقرأ [Partitioning](/index.php/Partitioning "Partitioning") لنظرة عامّة موسّعة.

المستخدمين العازمين على إنشاء [LVM](/index.php/LVM "LVM"), [أقراص مشفّرة](/index.php/Disk_encryption "Disk encryption") أو [RAID](/index.php/RAID "RAID"), عليهم أن يضعوا هذه التعليمات بالحسبان عند تجهيز الأقسام. إذا كنت تعتزم التثبيت على USB flash key, انظر إلى [Installing Arch Linux on a USB key](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key").

### تحديد الأجهزة

أول خطوة هي معرفة الأجهزة التي سيتم تثبيت النظام عليها. الأمر التالي سيعرض كل الأجهزة المتاحة:

```
# lsblk

```

سيعرض كل الأجهزة المتّصلة بنظامك بالإضافة لأنماط تقسيمها, متضمنا الجهاز المضيف والمستخدم لإقلاع قرص تثبيت Arch (مثل قرص USB). ليست كل الأجهزة المعروضة ستكون وسائط مناسبة للتثبيت. النتائج المنتهية بـ `rom`, `loop` or `airoot` يمكن تجاهلها.

الأجهزة (مثلا القرص الصلب hard disks) يتم عرضها بالشكل `sd*x*`, حيث `*x*` هو حرف صغير يبدأ من `a` للإشارة إلى الجهاز الأول (`sda`), `b` للإشارة إلى الجهاز الثاني (`sdb`), وهكذا. الأقسام الموجود على هذه الأجهزة تعرض بالشكل `sd*xY*`, حيث `*Y*` هو رقم يبدأ من `1` للإشارة إلى القسم الأول, `2` للإشارة إلى القسم الثاني, وهكذا. في المثال التالي, جهاز واحد فقط متاح (`sda`), وذلك الجهاز يحوي قسم واحد فقط (`sda1`):

```
NAME            MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda               8:0    0    80G  0 disk
└─sda1            8:1    0    80G  0 part

```

سيتم استخدام اصطلاح `sd*xY*` في الأمثلة اللاحقة لتخطيط التقسيم, الأقسام, وأنظمة الملفات. باعتبارها مجرد أمثلة, من المهم أن تتأكد من أسماء الأجهزة, أرقام الأقسام, و/أو مساحات الأقسام (إلخ.) عند القيام بأي تغييرات هامّة. لا تقم بنسخ الأوامر ولصقها بصورة عمياء.

في حال كان مخطط التقسيم الموجود لا يحتاج لتعديل, انتقل إلى [#File systems and swap](#File_systems_and_swap), وإلا تابع قراءة الفقرة التالية.

### أنماط جدولة التقسيم Partition table types

في حال كنت تقوم بتثبيت النظام إلى جانب نظام آخر (dual-booting), جدولة التقسيم ستكون موجودة مسبقا. في حال الأجهزة لم تكن مقسمة مسبقا, أو جدولة التقسيم الحالي أو مخطط التقسيم بحاجة لتغيير, سيكون عليك أولا أن تحدد جدولة التقسيم لكل جهاز مستخدم أو تنوي استخدامه.

يوجد نمطين لجدولة التقسيم:

*   [GPT](/index.php/GPT "GPT")
*   [MBR](/index.php/MBR "MBR")

يمكن معرفة جدولة التقسيم الموجودة بتنفيذ الأمر التالي لكل جهاز:

```
# parted /dev/sd*x* print

```

### أدوات التقسيم

**تحذير:** استخدام أداة تقسيم غير متوافقة مع نمط جدول التقسيم لديك سيؤدي على الأرجح إلى تخريب الجدول, بالإضافة إلى الأقسام والبيانات الموجودة.

يجب إختيار الأداة المناسبة لكل جهاز وفقا لجدول التقسيم المستخدم. وسيط تثبيت Arch يزود عدة أدوات تقسيم, تتضمن:

*   [parted](/index.php/Parted "Parted"): GPT and MBR
*   [fdisk](/index.php/Fdisk#Fdisk_usage_summary "Fdisk"), **cfdisk**, **sfdisk**: GPT and MBR
*   [gdisk](/index.php/Gdisk#Gdisk_usage_summary "Gdisk"), **cgdisk**, **sgdisk**: GPT

يمكن أيضا تقسيم الأجهزة قبل إقلاع وسيط التخزين, مثلا من خلال أدوات مثل [GParted](/index.php/GParted "GParted") (أيضا تتوفر كـ [قرص CD حي](http://gparted.sourceforge.net/livecd.php)).

#### استخدام parted بالوضع التفاعلي

كل الأمثلة المقدمة أدناه تستخدم *parted*, على اعتبار أنه يمكن استخدامها للنوعين UEFI/GPT و BIOS/MBR. سيتم تشغيلها بالوضع التفاعلي *interactive mode*, الذي يسهل عملية التقسيم ويقلل التكرار غير اللازم بتطبيق كل أوامر التقسيم للجهاز المحدد تلقائيا.

للبدأ على جهاز, نفذ الأمر:

```
# parted /dev/sd*x*

```

ستلاحظ أن محث سطر الأوامر تغير من (`#`) إلى `(parted)`: هذا يعني أن الأوامر في الأمثلة هي أوامر خاصة بالمحث الجديد ولا يمكن إدخالها يدويا مع محث الصدفة.

لمشاهدة قائمة بالأوامر المتاحة, أدخل:

```
(parted) help

```

عند الإنتهاء, أو إذا رغبت بتطبيق جدول تقسيم أو تخطيط لجهاز آخر, اخرج من parted بإدخال:

```
(parted) quit

```

بعد الإغلاق, محث سطر الأوامر سيعود إلى `#`.

### إنشاء جدول تقسيم جديد

تحتاج إلى (إعادة)إنشاء جدول التقسيم عندما يكون الجهاز بلا جدول تقسيم مسبق, أو عندما تكون بحاجة لتغيير نوع جدولته. إعادة إنشاء جدول التقسيم مفيدة أيضا عندما يكون مخطط التقسيم بحاجة لإعادة هيكلة من الصفر.

افتح كل جهاز بحاجة لـ(إعادة)إنشاء جدول التقسيم بالأمر:

```
# parted /dev/sd*x*

```

ثم لإنشاء جدول تقسيم GPT لأنظمة UEFI, استخدم الأمر:

```
(parted) mklabel gpt

```

لإنشاء جدول تقسيم MBR/msdos جديد لأنظمة BIOS, استخدم الأمر:

```
(parted) mklabel msdos

```

### مخطط التقسيم

يمكنك تحديد عدد وأحجام الأقسام التي ستقسم الأقراص إليها, والمجلدات التي ستوسع الأقسام إليها في النظام المثبّت (وتعرف باسم *نقاط التوسيع mount points*). الربط بين الأقسام والمجلّدات يسمّى [تخطيط التقسيم partition scheme](/index.php/Partitioning#Partition_scheme "Partitioning"), والذي يجب أن يفي بهذه المتطلّبات:

*   قسم على الأقل لمجلّد `/` (*الجذر root*) **يجب** أن يتّم إنشاؤه.
*   عند استخدام لوحة أم بنمط UEFI, **يجب** إنشاء [قسم نظام EFI](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface")

في الأمثلة التالية يفترض أن مخطّط التقسيم يتم على قرص واحد. سيتم إنشاء بعض المجلّدات الإختيارية للمجلّدات `/boot` و `/home`: لشرح عن هذه المجلّدات انظر إلى [Arch filesystem hierarchy](/index.php/Arch_filesystem_hierarchy "Arch filesystem hierarchy"); في حال لم يتم إنشاء قسم مستقل لمجلّدات مثل `/boot` أو `/home`, سيتم إحتوائهم في القسم `/`. سيتم شرح إنشاء قسم اختياري لمساحة التبديل [swap space](/index.php/Swap_space "Swap space")

إن لم تكن فتحت *parted* بالوضع التفاعلي مسبقا, استخدم الأمر لتقسيم كل جهاز:

```
# parted /dev/sd*x*

```

الأمر التالي سيستخدم لإنشاء الأقسام:

```
(parted) mkpart *part-type* *fs-type* *start* *end*

```

*   `*part-type*` هو إمّا `primary`, `extended` أو `logical`, وهو فعّال فقط لمخططات تقسيم MBR.
*   `*fs-type*` هو معرّف يستخدم إحدى الإدخالات التي يمكنك عرض قائمة بها بالأمر `help mkpart` اختار نظام الملفات الأنسب لما ستستخدمه في [#File systems and swap](#File_systems_and_swap). الأمر *mkpart* لا ينشأ فعليا نظام ملفات: المعامل `*fs-type*` سيستخدم ببساطة من قبل 'parted *لتعيين 1-byte code تستخدمها محملات الإقلاع ل"معاينة" أي نوع بيانات موجودة في القسم, ويتصرف وفقا لذلك عند الحاجة. ألق نظرة على [Wikipedia:Disk partitioning#PC partition types](https://en.wikipedia.org/wiki/Disk_partitioning#PC_partition_types "wikipedia:Disk partitioning").*

****تلميح:**** معظم [أنظمة الملفات الخاصة بلينكس](https://en.wikipedia.org/wiki/File_system#Linux "wikipedia:File system") تستخدم نفس معرف القسم ([0x83](https://en.wikipedia.org/wiki/Partition_type#PID_83h "wikipedia:Partition type")), لذلك يفضل إستخدام `ext2` لقسم مهيأ بنظام ملفات `ext4`

*   بداية القسم من أول الجهاز `*start*`. تتكون من عدد متبوع بـ [وحدة](http://www.gnu.org/software/parted/manual/parted.html#unit), مثلا `1M` تعني البداية من 1MiB
*   نهاية القسم `*end*`. بنفس صياغة `*start*`, مثلا `100%` تعني النهاية عند نهاية الجهاز (كامل المساحة المتبقية).

**تحذير:** من المهم ألا تتخطى الأقسام بعضها البعض: إذا كنت لا ترغب بترك أي مساحة غير مستخدمة على الجهاز, تأكد من أن كل قسم يبدأ حيث انتهى سابقه.

قد يعرض *parted* رسالة التحذير التالية:

```
Warning: The resulting partition is not properly aligned for best performance.
Ignore/Cancel?

```

في هذه الحالة, اقرأ [Partitioning#Partition alignment](/index.php/Partitioning#Partition_alignment "Partitioning") و [GNU Parted#Alignment](/index.php/GNU_Parted#Alignment "GNU Parted") لحل المشكلة.

الأمر التالي سيستخدم ليضع علم الإقلاع على القسم الذي يحوي مجلد الإقلاع `/boot`:

```
(parted) set *partition* boot on

```

*   حيث `*partition*` هو رقم القسم الذي يجب تعليمه (يمكنك استخدام الأمر `print` لعرض الأقسام).

#### أمثلة UEFI/GPT

مع UEFI/GPT ,قسم الإقلاع [EFI System Partition](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface") مطلوب.

لإنشاء قسم نظام EFI جديد, أدخل الأوامر التالية:

```
(parted) mkpart ESP fat32 1MiB 513MiB
(parted) set 1 boot on

```

أكمل تخطيط التقسيم كما ترغب. مثلا لإنشاء قسم آخر وحيد يملأ كل المساحة المتبقية:

```
(parted) mkpart primary ext4 513MiB 100%

```

لإنشاء قسمين واحد `/` (20GiB) والآخر `/home` (يملأ المساحة المتبقية):

```
(parted) mkpart primary ext4 513MiB 20.5GiB
(parted) mkpart primary ext4 20.5GiB 100%

```

ولإنشاء قسم `/` (20GiB), وقسم لمساحة التبديل swap (4GiB), وقسم للمجلد المنزل `/home` (يملأ المساحة المتبقية):

```
(parted) mkpart primary ext4 513MiB 20.5GiB
(parted) mkpart primary linux-swap 20.5GiB 24.5GiB
(parted) mkpart primary ext4 24.5GiB 100%

```

#### أمثلة BIOS/MBR

إذا كنت ترغب بقسم واحد استخدم كل المساحة المتوفرة لإنشاء قسم رئيسي, بتنفيذ الأمر التالي:

```
(parted) mkpart primary ext4 1MiB 100%
(parted) set 1 boot on

```

في المثال التالي, سيتم إنشاء قسم `/` بحجم 20GiB, متبوعا بقسم المنزل `/home` ليحجز كل المساحة المتبقيّة:

```
(parted) mkpart primary ext4 1MiB 20GiB
(parted) set 1 boot on
(parted) mkpart primary ext4 20GiB 100%

```

في المثال الأخير أدناه, سيتم إنشاء قسم منفصل `/boot` بحجم (100MiB), قسم تبديل swap (4GiB), وقسم المنزل `/home` (كل المساحة المتبقية):

```
(parted) mkpart primary ext4 1MiB 100MiB
(parted) set 1 boot on
(parted) mkpart primary ext4 100MiB 20GiB
(parted) mkpart primary linux-swap 20GiB 24GiB
(parted) mkpart primary ext4 24GiB 100%

```

### تهيئة أنظمة الملفات وتفعيل مساحة التبديل swap

بعد إنشاء الأقسام, كل قسم تم إنشاؤه **يجب** أن تتم تهيئته ب [نظام ملفات](/index.php/File_system "File system") مناسب, *ما عدا* أقسام swap. كل الأقسام على الجهاز المحدد يمكن عرضها بالأمر التالي:

```
# lsblk /dev/sd*x*

```

ماعدا الإستثناءات المذكورة أدناه, من المستحسن أن يتم استخدام نظام الملفات `ext4`:

```
# mkfs.ext4 /dev/sd*xY*

```

*إذا* قمت بإنشاء قسم UEFI جديد على نظام UEFI/GPT, **يجب** أن يتم تهيئته بنظام ملفات `fat32`

```
# mkfs.fat -F32 /dev/sd*xY*

```

*إذا* قمت بإنشاء قسم swap, يجب أن يتم ضبطه وتفعيله:

```
# mkswap /dev/sd*xY*
# swapon /dev/sd*xY*

```

قم بتوسيع القسم الجذر root partition إلى المجلد `/mnt` على النظام الحي:

```
# mount /dev/sd*xY* /mnt

```

يمكنك توسيع [الأقسام](/index.php/Partitioning#Partition_scheme "Partitioning") المتبقية بأي ترتيب (ماعدا *swap*), بعد إنشاء نقاط توسيع لكل قسم منها. مثلا عند استخدام القسم `/boot`:

```
# mkdir -p /mnt/boot
# mount /dev/sd*xZ* /mnt/boot

```

قسم `/boot` مستحسن أيضا عند توسيع القسم EFI System Partition على نظام UEFI/GPT. لبدائل عنها انظر إلى [EFISTUB](/index.php/EFISTUB "EFISTUB") والمقالات ذات الصلة.

## التثبيت

### اختيار المرايا

يجب تنزيل الحزم من الخوادم لتثبيتها, تجد قائمة بخوادم المرايا في `/etc/pacman.d/mirrorlist`. على النظام الحي, كلا المرايا مفعّلة افتراضيّا, مخزنة ومرتبة بحسب حالة المزامنة والسرعة عند إنشاء قرص التثبيت.

المرآة الموجودة في أعلى القائمة تعطى أولويّة عند تنزيل الحزمة. يمكنك تعديل الملف, ونقل المرايا الأقرب جغرافيّا إلى موقعك إلى أعلى القائمة, كما أن معايير أخرى يجب أن تؤخذ بعين الإعتبار. انظر إلى [Mirrors](/index.php/Mirrors "Mirrors") لمزيد من التفاصيل.

سيقوم *pacstrap* بتثبيت نسخة من ذاك الملف على النظام الجديد, لذلك فإن ترتيب المرايا يستحق العناء.

### تثبيت الحزم الأساسيّة

السكربت *pacstrap* يثبّت أساس النظام. لبناء حزم من [AUR](/index.php/AUR "AUR") أو باستخدام [ABS](/index.php/ABS "ABS"), مجموعة الحزم [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) مطلوبة أيضا.

ليس كل الأدوات من التثبيت الحي live installation (انظر [packages.both](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.both)) هي جزء من مجموعة الحزم الأساسيّة base. الحزم يمكن [تثبيت](https://wiki.archlinux.org/index.php/Install)ها لاحقا باستخدام *pacman*, أو بإلحاق أسمائهم إلى الأمر *pacstrap*

```
# pacstrap -i /mnt base base-devel

```

الخيار `-i` يضمن عرض رسالة تأكيد قبل تثبيت الحزم.

## التكوين Configuration

### fstab

أنشأ ملف [fstab](/index.php/Fstab "Fstab"). الخيار `-U` يشير إلى UUIDs انظر [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming"). يمكن تعيين تسميات للأقسام Labels بالخيار `-L`

```
# genfstab -U /mnt > /mnt/etc/fstab

```

تحقق من الملف الناتج `/mnt/etc/fstab`, وعدله في حالة وجود أخطاء.

### تغيير الجذر Change root

انسخ أي ملفات تكوين أخرى إلى النظام الجديد في `/mnt` مثل ملفات `/etc/netctl`, ثم انتقل إلى إلى النظام الجديد([chroot](/index.php/Chroot "Chroot")):

```
# arch-chroot /mnt /bin/bash

```

### الإعدادات المحليّة Locale

الإعدادات المحلية تحدد اللغات التي يستخدمها النظام, والإعتبارات الإقليمية الأخرى مثل العملة, الأعداد, مجموعات الأحرف.

القيم المتاحة مدرجة في `/etc/locale.gen`. أزل التعليق عن `en_US.UTF-8 UTF-8`, بالإضافة للسطور الأخرى اللازمة. احفظ الملف, وولد الإعدادات الجديدة:

```
# locale-gen

```

أنشأ `/etc/locale.conf`, حيث `LANG` يشير إلى *أول عمود* من الإدخال الموجود في `/etc/locale.gen`:

 `/etc/locale.conf`  `LANG=*en_US.UTF-8*` 

إذا كنت [حددت تخطط لوحة مفاتيح](#Set_the_keyboard_layout), اجعل التغييرات دائمة في `/etc/vconsole.conf`. مثلا, إذا تم تعيين `de-latin1` بالأمر *loadkeys*, و `lat9w-16` بالأمر *setfont*, عيّن المتغيرات `KEYMAP` و `FONT` وفقا لذلك:

 `/etc/vconsole.conf` 
```
KEYMAP=*de-latin1*
FONT=*lat9w-16*
```

### الوقت

اختر [المنطقة الزمنية](https://wiki.archlinux.org/index.php/Time_zone):

```
# tzselect

```

أنشأ وصلة رمزية `/etc/localtime`, حيث `Zone/Subzone` هي قيمة `TZ` من الأمر *tzselect*:

```
# ln -s /usr/share/zoneinfo/*Zone*/*SubZone* /etc/localtime

```

من المستحسن ضبط انحراف الوقت, وتعيين معيار الوقت إلى UTC:

```
# hwclock --systohc --utc

```

إذا وجد أنظمة تشغيل أخرى مثبتة على الجهاز, يجب أن تضبط وفقا لذلك. انظر إلى [Time](/index.php/Time "Time") لمزيد من التفاصيل.

### Initramfs

يتم تشغيل [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") مع تثبيت الحزمة [linux](https://www.archlinux.org/packages/?name=linux) بالأمر *pacstrap*, معظم المستخدمين يمكنهم استخدام الإفتراضيات المتوفرة ضمن `mkinitcpio.conf`.

إذا كنت ترغب بتكوين إعدادات خاصة, اضبط ملفات [hooks](/index.php/Mkinitcpio#HOOKS "Mkinitcpio") المناسبة في `/etc/mkinitcpio.conf` و [أعد توليد](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio") صورة initramfs:

```
# mkinitcpio -p linux

```

### تثبيت محمّل الإقلاع

اطّلع على [Boot loaders](/index.php/Boot_loaders "Boot loaders") لمعرفة الخيارات والتكوينات المتاحة. إذا كنت تملك معالج Intel, ثبت الحزمة [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) و [فعّل تحديثات microcode](/index.php/Microcode#Enabling_Intel_microcode_updates "Microcode").

#### UEFI/GPT

هذا المثال يفترض أن قرص التثبيت من النوع GPT, ويحوي [قسم نظام EFI](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface") (gdisk type `EF00`,مهيئ بنظام الملفات FAT32 وتم توسيعه إلى `/boot`.

ثبت [systemd-boot](/index.php/Systemd-boot "Systemd-boot") بالأمر:

```
# bootctl install

```

عند نجاح التثبيت, أنشئ سجل إقلاع كما هو مشروح في [systemd-boot#Configuration](/index.php/Systemd-boot#Configuration "Systemd-boot") (استبدل `$esp` with `/boot`), أو قم باستخدام الأمثلة الموجودة ضمن `/usr/share/systemd/bootctl/`.

#### BIOS/MBR

ثبت الحزمة [grub](https://www.archlinux.org/packages/?name=grub). للبحث عن أنظمة التشغيل الأخرى, ثبّت الحزمة [os-prober](https://www.archlinux.org/packages/?name=os-prober) أيضا:

```
# pacman -S grub os-prober

```

ثبت محمّل الإقلاع على *محرك الأقراص* الذي ثبتّ Arch عليه:

```
# grub-install --target=i386-pc --recheck */dev/sda*

```

ولّد `grub.cfg`:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

لمزيد من المعلومات: [GRUB](/index.php/GRUB "GRUB").

### ضبط الشبكة

الإجراء مشابه لما ورد في [#Connect to the Internet](#Connect_to_the_Internet), ماعدا جعله مستمر للإقلاعات اللاحقة. اختر daemon **واحد** للتعامل مع الشبكة.

#### Hostname

اضبط اسم المضيف [hostname](/index.php/Hostname "Hostname") لما يناسبك:

 `/etc/hostname`  `*myhostname*` 

من المستحسن إلحاق نفس اسم المضيف إلى إدخالات `localhost` في `/etc/hosts`. الق نظرة على [Network configuration#Local network hostname resolution](/index.php/Network_configuration#Local_network_hostname_resolution "Network configuration").

#### سلكي

في حال طلب اتصال سلكي وحيد, فعّل الخدمة [dhcpcd](/index.php/Dhcpcd "Dhcpcd"):

```
# systemctl enable dhcpcd@*interface*.service

```

حيث `*interface*` هو اسم جهاز الشبكة [device name](/index.php/Network_configuration#Device_names "Network configuration").

انظر إلى [Network configuration#Configure the IP address](/index.php/Network_configuration#Configure_the_IP_address "Network configuration") لمعرفة الطرق المتاحة.

#### لاسلكي

ثبت الحزم [iw](https://www.archlinux.org/packages/?name=iw), [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant), و(من أجل *wifi-menu*) [dialog](https://www.archlinux.org/packages/?name=dialog):

```
# pacman -S iw wpa_supplicant dialog

```

قد تحتاج تثبيت حزم إضافية [firmware packages](/index.php/Wireless#Installing_driver.2Ffirmware "Wireless").

في حال كنت قد استخدمت *wifi-menu* مسبقا, اعد تنفيذ الخطوات **بعد** إنهاء هذا التثبيت وإعادة التشغيل, لمنع التعارض مع العمليات قيد التشغيل.

انظر إلى [Netctl](/index.php/Netctl "Netctl") و [إدارة الإتصال اللاسلكي](/index.php/Wireless#Wireless_management "Wireless") لمزيد من المعلومات.

## إلغاء توسيع الأقسام وإعادة التشغيل

اضبط [كلمة سر](/index.php/Password "Password") المستخدم root بالأمر:

```
# passwd

```

اخرج من بيئة chroot بالأمر `exit` أو بضغط المفاتيح `Ctrl+D`.

سيقوم *systemd* بإلغاء توسيع الأقسام تلقائيا عند إيقاف التشغيل. رغم ذلك يمكنك إلغاء توسيعها يدويّا بالأمر:

```
# umount -R /mnt

```

إذا وجدت القسم مشغول "busy", يمكنك معرفة السبب بالأمر [fuser](/index.php/Fuser "Fuser"). أعد تشغيل الحاسب.

```
# reboot

```

أزل وسيط التثبيت, وإلا قد يتم الإقلاع إليه مرة أخرى. يمكنك الدخول إلى نظامك الجديد باسم المستخدم *root*, باستخدام كلمة المرور التي حددتها مسبقا بالأمر *passwd*.

## ما بعد التثبيت

يعتبر نظام Arch linux الذي ثبتّه الآن بيئة GNU/Linux جاهزة ليتم توظيفها فوق حاجتك للغرض الذي تريده. ننصحك الآن *بشّدة* لقراءة مقال [توصيات عامّة](/index.php/General_recommendations "General recommendations"), خاصة أوّل فقرتين منه. الفقرات الأخرى تقدم روابط إلى تعليمات ما بعد التثبيت مثل ضبط الواجهة الرسوميّة, الصوت و لوحة اللمس.

لقائمة بالبرامج التي قد تهمّك, انظر إلى [List of applications](/index.php/List_of_applications "List of applications").