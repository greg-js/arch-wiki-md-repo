صورة الخلفية والخطوط النقطية

يجب عدم الخلط بين [GRUB](https://www.gnu.org/software/grub/) و [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") وهو الجيل القادم من محمل الإقلاع الموحد . مستمد GRUB من [PUPA](http://www.nongnu.org/pupa/) وهو مشروع بحثي لتطوير الجيل القادم من محمل الإقلاع القديم المسمى الآن GRUB Legacy. تمت كتابة GRUB من الصفر لتنظيف كل شيء وتوفير نمط الوحدات والمحمولية [[1]](https://www.gnu.org/software/grub/grub-faq.html#q1). باختصار ، **محمل الإقلاع** هو البرنامج الأول الذي ينفذ عندم يقلع الحاسوب. وهو المسؤول عن تحميل ونقل التحكم إلى نواة لينكس. النواة، بدورها، تقوم بتهيئة بقية نظام التشغيل.

## Contents

*   [1 مقدمة](#مقدمة)
    *   [1.1 ملاحظات لمستخدمي إصدار GRUB القديم](#ملاحظات_لمستخدمي_إصدار_GRUB_القديم)
        *   [1.1.1 النسخ الاحتياطي للبيانات المهمة](#النسخ_الاحتياطي_للبيانات_المهمة)
    *   [1.2 المتطلبات الأولية](#المتطلبات_الأولية)
        *   [1.2.1 أنظمة BIOS](#أنظمة_BIOS)
            *   [1.2.1.1 إرشادات خاصة بجدول أقسام GUID Partition Table (GPT)](#إرشادات_خاصة_بجدول_أقسام_GUID_Partition_Table_(GPT))
            *   [1.2.1.2 إرشادات بخصوص( Master Boot Record MBR)](#إرشادات_بخصوص(_Master_Boot_Record_MBR))
        *   [1.2.2 أنظمة UEFI](#أنظمة_UEFI)
            *   [1.2.2.1 إنشاء وتوصيل قسم بنظام UEFI](#إنشاء_وتوصيل_قسم_بنظام_UEFI)
*   [2 التثبيت](#التثبيت)
    *   [2.1 أنظمة BIOS](#أنظمة_BIOS_2)
        *   [2.1.1 تثبيت ملفات الإقلاع](#تثبيت_ملفات_الإقلاع)
            *   [2.1.1.1 التثبيت على قسم إقلاع بنظام GPT BIOS](#التثبيت_على_قسم_إقلاع_بنظام_GPT_BIOS)
            *   [2.1.1.2 التثبيت على قطاع إقلاع 440-byte بنظام MBR](#التثبيت_على_قطاع_إقلاع_440-byte_بنظام_MBR)
            *   [2.1.1.3 التثبيت على قرص صلب مقسم أو غير مقسم](#التثبيت_على_قرص_صلب_مقسم_أو_غير_مقسم)
            *   [2.1.1.4 توليد ملف core.img منفردا](#توليد_ملف_core.img_منفردا)
        *   [2.1.2 توليد ملف التكوين](#توليد_ملف_التكوين)
        *   [2.1.3 الإقلاع المزدوج](#الإقلاع_المزدوج)
            *   [2.1.3.1 نظام وندوز مثبت على نمط BIOS-MBR](#نظام_وندوز_مثبت_على_نمط_BIOS-MBR)
    *   [2.2 أنظمة UEFI](#أنظمة_UEFI_2)
        *   [2.2.1 تثبيت ملفات الإقلاع](#تثبيت_ملفات_الإقلاع_2)
            *   [2.2.1.1 التثبيت على قسم بنظام UEFI](#التثبيت_على_قسم_بنظام_UEFI)
        *   [2.2.2 توليد ملف التكوين](#توليد_ملف_التكوين_2)
        *   [2.2.3 إنشاء مدخلة ل GRUB في الجدار الناري لمحمل الإقلاع](#إنشاء_مدخلة_ل_GRUB_في_الجدار_الناري_لمحمل_الإقلاع)
        *   [2.2.4 UEFI إنشاء تطبيق GRUB قابل للتثبيت بنظام](#UEFI_إنشاء_تطبيق_GRUB_قابل_للتثبيت_بنظام)
        *   [2.2.5 الإقلاع المتعدد](#الإقلاع_المتعدد)
            *   [2.2.5.1 UEFI-GPT ميكروسوفت وندوز مثبت على نمط](#UEFI-GPT_ميكروسوفت_وندوز_مثبت_على_نمط)
*   [3 التهيئة](#التهيئة)
    *   [3.1 توليد ملفات الإقلاع آليا باستخدام grub-mkconfig](#توليد_ملفات_الإقلاع_آليا_باستخدام_grub-mkconfig)
        *   [3.1.1 خيارات وأوامر إضافية](#خيارات_وأوامر_إضافية)
    *   [3.2 إنشاء ملف grub.cfg يدويا](#إنشاء_ملف_grub.cfg_يدويا)
    *   [3.3 الإقلاع المزدوج](#الإقلاع_المزدوج_2)
        *   [3.3.1 grub-mkconfig استخدام الأمر](#grub-mkconfig_استخدام_الأمر)
            *   [3.3.1.1 مع نظام GNU/Linux](#مع_نظام_GNU/Linux)
            *   [3.3.1.2 مع نظام FreeBSD](#مع_نظام_FreeBSD)
            *   [3.3.1.3 مع نظام وندوز](#مع_نظام_وندوز)
        *   [3.3.2 مع نظام وندوز باستخدام برنامج EasyBCD و NeoGRUB](#مع_نظام_وندوز_باستخدام_برنامج_EasyBCD_و_NeoGRUB)
    *   [3.4 إعداد المحسنات البصرية](#إعداد_المحسنات_البصرية)
        *   [3.4.1 ضبط دقة شاشة الإقلاع framebuffer](#ضبط_دقة_شاشة_الإقلاع_framebuffer)
        *   [3.4.2 915resolution اﻷداة](#915resolution_اﻷداة)

## مقدمة

*   اسم *GRUB* يشير رسميا إلى الإصدار *2* من البرنامج ، انظر [[2]](https://www.gnu.org/software/grub/).

إذا كنت تبحث عن مقال مخصص للإصدار القديم ، انظر [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy").

*   يدعم GRUB [Btrfs](/index.php/Btrfs "Btrfs") كنظام ملفات جذر بدون قسم من `/boot` منفصل مضغوط إما بنمط zlib أو LZO.

### ملاحظات لمستخدمي إصدار GRUB القديم

*   الترقية من الإصدار القديم [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") إلى GRUB يكون من خلال تثبيت نسخة جديدة من GRUB والذي يتم شرحه [بأسفل](#التثبيت).
*   يوجد اختلافات بين الأوامر لإصدار جروب القديم و جروب الحالي .

قم بالتعود [على أوامر جروب](https://www.gnu.org/software/grub/manual/grub.html#Commands) قبل قبل الشروع في العمل. (مثلا تم وضع "search" بدلا من "find" ).

*   أصبح GRUB *مرنا* ولم يعد يحتاج إلى "stage 1.5". ونتيجة لذلك أصبح محمل الإقلاع نفسه عبارة عن وحدات يتم تحميلها من القرص الصلب كم بقدر الحاجة لتوسيع الوظائف مثل دعم (مثل دعم [LVM](/index.php/LVM "LVM") أو RAID ).
*   تم تغيير طريقة تسمية الأجهزة ما بين الإصدار القديم من GRUB والإصدار الحالي . تم ترقيم أقسام القرص الصلب بدءا من 1 بدلا م0 بينما الأقراص الصلبة ما زال ترقيمها يبدأ من 0 ، مسبوقة بنوع جدولة الأقسام. على سبيل المثال `/dev/sda1` يجب أن يشار إليه ب `(hd0,msdos1)` (لنظام MBR) أو `(hd0,gpt1)` لنظام (GPT).

#### النسخ الاحتياطي للبيانات المهمة

على الرغم من أن تثبيت GRUB ينبغي أن يجري بسلاسة ، إلا أنه يوصى بالاحتفاظ بملفات GRUB Legacy قبل الترقية إلى GRUB2.

```
# mv /boot/grub /boot/grub-legacy

```

قم بعمل نسخة احتياطية من الجدول MBR الذي يحتوي كود الإقلاع وجدول الأقسام ضع مسار القرص الفعلي لديك بدلا من `/dev/sd**X**`

```
# dd if=/dev/sdX of=/path/to/backup/mbr_backup bs=512 count=1

```

446 بايت فقط من MBR تحتوي على كود الإقلاع، و 64 بايت التالية تحتوي على جدول أقسام القرص . إذا كنت ﻻ تريد الكتابة فوق جدول الأقسام لديك عندما تريد استرجاعها فننصحك بشدة أن تقوم بعمل نسخة احتياطية فقط لكود الإقلاع الخاص ب MBR:

```
# dd if=/dev/sdX of=/path/to/backup/bootcode_backup bs=446 count=1

```

إذا لم يمكنك تثبيت GRUB@ بشكل صحيح ، انظر [#استرجاع إصدار GRUB القديم](#استرجاع_إصدار_GRUB_القديم).

### المتطلبات الأولية

#### أنظمة BIOS

##### إرشادات خاصة بجدول أقسام [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table") (GPT)

يحتاج تهيئة جروب إلى [قسم إقلاع بنظام بيوس](http://www.gnu.org/software/grub/manual/html_node/BIOS-installation.html) لتضمين `core.img` الخاصة بجروب في حالة عدم وجود فجوة ما بعد MBR في أنظمة تقسيم GPT (والتي يتم الاستيلاء عليها من قبل رأس الجدول والقسم الأساسي لجدول GPT). *هذا القسم يستخدم من قِبَل* جروب فقط في إعدادات BIOS-GPT. لا يوجد نوع للأقسام في حالة تقسيم MBR (على الأقل ليس ل GRUB) كما أنه لا يتطلب هذا القسم إذا كان النظام يعتمد UEFI ، كما أنه لا يتضمن قطاعات للإقلاع ولا تحجز مكانا في هذه الحالة. لإعداد نظام تقسيم BIOS-GPT ، قم بإنشاء قسم بسعة 1007 كب في بداية القرص الصلب ، باستخدام اﻷداة cgdisk او GNU Parted دون تحديد نظام ملفات له. هذا الحجم 1007 كب سيتيح للقسم التالي أن يقسم صحيحا بقطاعات حجمها 1024 كب . إذا كان من الضروري يمكن لهذا القسم أن يوجد ويمكن أيضا أن يكون موجودا في مكان آخر على القرص، لكن يجب أن يكون داخل مساحة ال 2 تيرا بايت الأولى. اضبط القسم ليكون بنوع `0xEF02` في gdisk ، وبنوع `EF02` في cgdisk أو `set <BOOT_PART_NUM> bios_grub on` في GNU Parted.

**ملاحظة:** يجب إنشاء هذا القسم قبل تنفيذ الأمر `grub-install` أو اﻷمر `grub-setup`

**ملاحظة:** يتيح لك gdisk فقط أن تنشئ هذا القسم على وضعية تتيح لك أن تفقد بها أقل قد قدر ممكن من المساحة (sector 34-2047) إذا قمت بإنشائها في النهاية ، وبعد جميع أقسام القرص اﻷخرى . وذلك ﻷن يعمل بخاصية الضبط التلقائي للأقسام في حدود 2048-sector قدر الإمكان.

##### إرشادات بخصوص( [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record") MBR)

عادة ما تكون فجوة ما بعد MBR المسماة "post-MBR gap" وهي ال 512 التالية لمنطقة MBR وقبل بدية القسم اﻷول ، في العديد من أنظمة تقسيم MBR ( أو أقراص ذات تسمية msdos) تكون 31 كب حيث تتحدد مسائل تخطيط الإسطوانات المتوافقة مع دوس في جدول التقسيم. مع ذلك ما بعد MBR تكون ما بين 1 و 2 ميجابايت مطلوبة لتقديم غرفة مناسبة لتضمين صور جروب GRUB's `core.img` ([FS#24103](https://bugs.archlinux.org/task/24103)). وينصح باستخدام قسم يدعم تخطيط أقسام 1 MiB لتحصل أيضا على هذه المساحة لتلبية حاجة القطاعات من غير نوع 512 بايت (التي لا تتعلق بتضمين صور `core.img`) تقسيم MBR يحصل على دعم أفضل من تقسيم GPT في بعض أنظمة التشغيل ، مثل الإصدارات القديمة من ميكروسوفت وندوز (حتى وندوز 7) و ونظام Haiku. إذا كان لديك إقلاع مزدوج من أنظمة التشغيل يراعى استخدم التقسيم MBR . قرص MBR قد يكون قابلا للتحويل إلى GPT إذا كان هناك قدر قليل من المساحة الإضافية متاحا. انظر [GUID Partition Table#Convert from MBR to GPT](/index.php/GUID_Partition_Table#Convert_from_MBR_to_GPT "GUID Partition Table").

#### أنظمة UEFI

**ملاحظة:** يوصى بقراءة وفهم هذه الصفحات [UEFI](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface"), [GPT](/index.php/GUID_Partition_Table "GUID Partition Table") و [Arch boot process#Boot loader](/index.php/Arch_boot_process#Boot_loader "Arch boot process") .

##### إنشاء وتوصيل قسم بنظام UEFI

فيما يلي [Unified Extensible Firmware Interface#EFI System Partition](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface") إرشادات عن إنشاء نظام تقسيم UEFI . ثم توصيل قسم UEFI على المجلد `/boot/efi/`. إذا قمت بتوصيل قسم بنظام UEFI على نقطة وصل أخرى ، استبدل `/boot/efi` فيما سبق وضع مكانه انقطة التوصيل لديك:

```
# mkdir -p /boot/efi
# mount -t vfat <UEFI_SYSTEM_PARTITION> /boot/efi

```

قم بإنشاء الدليل `/boot/efi/EFI` :

```
# mkdir /boot/efi/EFI

```

## التثبيت

### أنظمة BIOS

يمكن [تثبيت](/index.php/Pacman "Pacman") GRUB مع الحزمة [grub-bios](https://www.archlinux.org/packages/?name=grub-bios) من [المستودعات الرسمية[https://aur.archlinux.org/packages/grub-legacy/ grub-legacy]](/index.php/Official_repositories "Official repositories"). وذلك سيستبدل حزمة أو [grub](https://www.archlinux.org/packages/?name=grub) إذا تم تثبيتها.

**ملاحظة:** ببساطة، لن يسبب تثبيت الحزمة تحديثا للملف `boot/grub/i386-pc/core.img/`

ولا وحدات GRUB في المجلد `/boot/grub/i386-pc`.

أنت تحتاج إلى التحديث يدويا باستخدام اﻷمر `grub-install` كما تم شرحه من قبل.

#### تثبيت ملفات الإقلاع

توجد ثلاثة طرق لتثبيت ملفات إقلاع GRUB في نظام إقلاع BIOS:

*   [#التثبيت على قسم إقلاع بنظام GPT BIOS](#التثبيت_على_قسم_إقلاع_بنظام_GPT_BIOS) (يوصى به مع [GPT](/index.php/GPT "GPT"))
*   [#التثبيت على قطاع إقلاع 440-byte بنظام MBR](#التثبيت_على_قطاع_إقلاع_440-byte_بنظام_MBR) (يوصى به مع [MBR](/index.php/MBR "MBR"))
*   [#التثبيت على قرص صلب مقسم أو غير مقسم](#التثبيت_على_قرص_صلب_مقسم_أو_غير_مقسم) (لا ينصح به)
*   [#توليد ملف core.img منفردا](#توليد_ملف_core.img_منفردا) (أكثر الطرق أمانا إلا أنه تحتاج إلى نوع آخر من محملات إقلاع بيوس مثل القديم [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") or [Syslinux](/index.php/Syslinux "Syslinux") للتثبيت مع chainload `/boot/grub/i386-pc/core.img`)

**ملاحظة:** انظر [http://www.gnu.org/software/grub/manual/html_node/BIOS-installation.html](http://www.gnu.org/software/grub/manual/html_node/BIOS-installation.html) لمزيد من الوثائق.

##### التثبيت على قسم إقلاع بنظام GPT BIOS

أقراص [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table") لا تحتوي على "مسارات إقلاع" محجوزة . لذلك يجب عليك إنشاء قسم إقلاع بيوس (`0xEF02`) لتحمل صورة المحمل GRUB. استخدام GNU Parted يمكنك ضبط هذا باستخدام أمر كما يلي:

```
# parted /dev/disk set <partition-number> bios_grub on

```

إذا كنت تستخدم gdisk ، اضبط نوع القسم على `0xEF02`. عن طريق برامج التقسيم الذي يتطلب إعداد GUID مباشرة يجب أن يكون `‘21686148-6449-6e6f-744e656564454649’` مخزنا على القرص مثل `"!haHdInotNeedEFI"` إذا تم تفسيره على أنه ASCII.

**تحذير:** كن شديد الحذر في تحديدك لقسم إقلاع بيوس . عندما يعثر GRUB على قسم إقلاغ بيوس أثناء التثبيت ، سوف يكتب تلقائيا على جزء منه . كن متأكدا أن هذا القسم لا يحتوي أية بيانات أخرى.

لإعداد `grub-bios` على قرص صلب بنظام GPT قم بتعديل الدليل `/boot/grub` ، وتوليد ملف `/boot/grub/i386-pc/core.img` وتضمينه في قسم إقلاع بيوس ، نفذ الأمر :

```
# modprobe dm-mod
# grub-install --target=i386-pc --recheck --debug /dev/sda
# mkdir -p /boot/grub/locale
# cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo

```

حيث `/dev/sda` هو القرص المستهدف للتثبيت .

##### التثبيت على قطاع إقلاع 440-byte بنظام MBR

لتثبيت `grub-bios` على قطاع الإقلاع الرئيس Master Boot Record ، قم بتعديل المجلد `/boot/grub` ، وتوليد الملف `/boot/grub/i386-pc/core.img`، ووضعه في ال 31 كب ( أصغر مساحة ، وتعتمد على طريقة ترتيب قسم فجوة ما بعد MBR ، وقم بتوليد ملف التكوين بتنفيذ الأمر:

```
# modprobe dm-mod
# grub-install --recheck /dev/sda
# grub-mkconfig -o /boot/grub/grub.cfg

```

حيث `/dev/sda` هو القرص المستهدف للتثبيت ( في هذه الحالة هو قطاع الإقلاع الرئيس MBR الخاص بأول قرص ساتا) إذا كنت تستخدم [LVM](/index.php/LVM "LVM") لعمل قسم `/boot` لديك , يمكنك تثبيت GRUB على أقراص حقيقية متعددة.

**تحذير:** تأكد من فحص المجلد `/boot` إذا كنت تستخدم الأخير . أحيانا ما تنشئ معاملات `boot-directory` مجلد `/boot` آخر بداخل القسم `/boot`. سيكون التثبيت الخطأ يبدو كما يلي `/boot/boot/grub/`.

##### التثبيت على قرص صلب مقسم أو غير مقسم

**ملاحظة:** لا يستحب تثبيت grub-bios على قطاع إقلاع أو قرص غير مقسم مثلما يفعل كل من GRUB Legacy أو Syslinux .هذا النوع من التثبيت عرضة للتحطم ، خاصة أثناء التحديث ، وهو غير مدعوم من قِبل Arch devs.

لتثبيت grub-bios على قطاع إقلاع ، بقرص غير مقسم (يسمى أيضا superfloppy ) أو عل قرص مرن ، استخدم على سبيل المثال `/dev/sdaX/` كقسم إقلاع `boot/` ، نفذ :

```
# modprobe dm-mod 
# grub-install --target=i386-pc --recheck --debug --force /dev/sdaX
# chattr -i /boot/grub/i386-pc/core.img
# mkdir -p /boot/grub/locale
# cp /usr/share/locale/en@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo
# chattr +i /boot/grub/i386-pc/core.img

```

أنت تحتاج إلى الخيار `force--` ليسمح باستخدام قوائم الكتل blocklists ولا يجب استخدام `grub-setup=/bin/true--` (الذي يشبه ببساطة توليد الملف `core.img`). سيعطيك الأمر `grub-install` رسالة خطأ كما يجب أن يعطيك فكرة عن ماهية هذا الخطأ على هذا النهج:

```
/sbin/grub-setup: warn: Attempting to install GRUB to a partitionless disk or to a partition. This is a BAD idea.
/sbin/grub-setup: warn: Embedding is not possible. GRUB can only be installed in this setup by using blocklists. 
                        However, blocklists are UNRELIABLE and their use is discouraged.

```

بدون `force--` ربما تحصل على رسالة الخطأ بأسفل ولن يقوم الأمر `grub-setup` بتثبيت شيفرة الإقلاع على قطاع الإقلاع بالقسم:

```
/sbin/grub-setup: error: will not proceed with blocklists

```

مع الخيار `force--` يجب أن تحصل على رسالة:

```
Installation finished. No error reported.

```

السبب في كون `grub-setup` لا يتيح ذلك افتراضيا لأنه في حالة الأقراص المقسمة أو غير المقسمة أن `grub-bios` يعتمد على قوائم الكتل blocklists المضمنة في قطاع إقلاع القسم لتحديد مكان الملف `boot/grub/i386-pc/core.img/` وبادئة الدليل `/boot/grub/`. مواضع القطاعات الخاصة بملف `core.img`..إلخ ربما تتغير كلما تغير نظام الملفات على القسم ( تم نسخ ملفات أو حذفها) لمزيد من المعلومات انظر [https://bugzilla.redhat.com/show_bug.cgi?id=728742](https://bugzilla.redhat.com/show_bug.cgi?id=728742) and [https://bugzilla.redhat.com/show_bug.cgi?id=730915](https://bugzilla.redhat.com/show_bug.cgi?id=730915). هذه الخلفية من أجل لوضع flag غير قابلة للتغيير على الملف `boot/grub/i386-pc/core.img/` ( باستخدام chattr كما تم شرحه من قبل) حيث إن أماكن القطاعات الخاصة بملف `core.img` على القرص ثابتة . و ال flag الثابت على `boot/grub/i386-pc/core.img/` يحتاج للضبط فقط إذا كانت الحزمة `grub-bios` مثبيتة على قطاع الإقلاع بالقرص المقسم أو غير المقسم ، وليس في حالة التثبيت على قطاع الإقلاع الرئيس MBR أو ببساطة توليد الملف `core.img` بدون تمين أي قطاعات إقلاع (تم شرحه من بأعلى).

##### توليد ملف core.img منفردا

لإنشاء المجلد `/boot/grub/` وتوليد الملف `boot/grub/i386-pc/core.img/` **بدون** تضمين أي شيفرة لقطاعات الإقلاع على مسجل الإقلاع الرئيس ، ومنطقة ما قبل فجوة سجل الإقلاع الرئيس post-MBR ، أو قطاعات الإقلاع بالقسم ، قم بإضافة الخيار `grub-setup=/bin/true--` إلى الأمر `grub-install`: To populate the `/boot/grub` directory and generate a `/boot/grub/i386-pc/core.img` file **without** embedding any

```
# modprobe dm-mod
# grub-install --target=i386-pc --grub-setup=/bin/true --recheck --debug /dev/sda
# mkdir -p /boot/grub/locale
# cp /usr/share/locale/en@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo

```

يمكنك حينئذ تضفير ملف `core.img` GRUB Legacy أو syslinux كصورة أقلاع لنواة واحدة أو متعددة الأنوية.

#### توليد ملف التكوين

في النهاية قم بإعدادGRUB (تم توضيح ذلك بفائض من الشرح في الجزء الخاص بالإعدادات ) :

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

**ملاحظة:** مسار الملف هو `/boot/grub/grub.cfg`, وليس `/boot/grub/i386-pc/grub.cfg`.

إذا كان GRUB يعاني من رسالة "no suitable mode found" أثناء الإقلاع ، اذهب إلى [#تصحيح الخطأ No Suitable Mode Found](#تصحيح_الخطأ_No_Suitable_Mode_Found). إذا فشل الأمر `grub-mkconfig` قم بوضع الملف `/boot/grub/grub.cfg` بدلا من ملف `/boot/grub/menu.lst` باستخدام الأمر:

```
# grub-menulst2cfg /boot/grub/menu.lst /boot/grub/grub.cfg

```

كمثال:

 `/boot/grub/menu.lst` 
```
default=0
timeout=5

title  Arch Linux Stock Kernel
root   (hd0,0)
kernel /vmlinuz-linux root=/dev/sda2 ro
initrd /initramfs-linux.img

title  Arch Linux Stock Kernel Fallback
root   (hd0,0)
kernel /vmlinuz-linux root=/dev/sda2 ro
initrd /initramfs-linux-fallback.img

```
 `/boot/grub/grub.cfg` 
```
set default='0'; if [ x"$default" = xsaved ]; then load_env; set default="$saved_entry"; fi
set timeout=5

menuentry 'Arch Linux Stock Kernel' {
        set root='(hd0,1)'; set legacy_hdbias='0'
        legacy_kernel   '/vmlinuz-linux' '/vmlinuz-linux' 'root=/dev/sda2' 'ro'
        legacy_initrd '/initramfs-linux.img' '/initramfs-linux.img'

}

menuentry 'Arch Linux Stock Kernel Fallback' {
        set root='(hd0,1)'; set legacy_hdbias='0'
        legacy_kernel   '/vmlinuz-linux' '/vmlinuz-linux' 'root=/dev/sda2' 'ro'
        legacy_initrd '/initramfs-linux-fallback.img' '/initramfs-linux-fallback.img'
}

```

إذا نسيت إنشاء ملف `/boot/grub/grub.cfg` قم ببساطة بالإقلاع من داخل صدفة أوامر GRUB واكتب :

```
sh:grub> insmod legacycfg
sh:grub> legacy_configfile ${prefix}/menu.lst

```

أقلع داخل آرتش وأعد إنشاء ملف تهيئة GRUB `/boot/grub/grub.cfg` المناسب .

**ملاحظة:** هذا لخيار يعمل فقط مع أنظمة بيوس ، وليس مع أنظمة UEFI .

#### الإقلاع المزدوج

##### نظام وندوز مثبت على نمط BIOS-MBR

**ملاحظة:** GRUB يدعم إقلاع `bootmgr` مباشرة وجمع قطاعات الإقلاع لم يعد مطلوبا لإقلاع وندوز في إعداد BIOS-MBR.

**تحذير:** إن **قسم النظام** هو الذي يحمل `bootmgr` وليس القسم "الحقيقي" لوندوز (عادة يكون قسم C:) . عند إظهار كل معرفات الأقسام UUIDs بالأمر blkid ، يكون قسم النظام معنون ب `LABEL="SYSTEM RESERVED"` ويكون حجمه في حدود 100 ميجا بايت (يشبه كثيرا حجم قسم الإقلاع في آرتش) . انظر [Wikipedia:System partition and boot partition](https://en.wikipedia.org/wiki/System_partition_and_boot_partition "wikipedia:System partition and boot partition") لمزيد من التفاصيل.

أوجد معرف UUID الخاص بنظام ملفات NTFS لقسم نظام وندوز حيث يقيم `bootmgr` وملفاته. مثلا ؛ إذا كان `bootmgr` الخاص بوندوز يوجد في `/media/SYSTEM_RESERVED/bootmgr`: لوندوز فيستا/7/8:

```
# grub-probe --target=fs_uuid /media/SYSTEM_RESERVED/bootmgr
69B235F6749E84CE

```

```
# grub-probe --target=hints_string /media/SYSTEM_RESERVED/bootmgr
--hint-bios=hd0,msdos1 --hint-efi=hd0,msdos1 --hint-baremetal=ahci0,msdos1

```

**ملاحظة:** لوندوز إكس بي ضع `ntldr` بدلا من `bootmgr` في الأمر بأعلى.

بعد ذلك ، أضف الشيفرة التالية إلى `/etc/grub.d/40_custom` أو `/boot/grub/custom.cfg` ثم قم بإعادة توليد ملف `grub.cfg` بالأمر `grub-mkconfig` كما تم شرحه بأعلى لإقاع وندوز ( إكس بي ، 7 ، أو 8) والمثبت على وضعية BIOS-MBR: لوندوز فيستا/7/8:

```
menuentry "Microsoft Windows Vista/7/8 BIOS-MBR" {
        insmod part_msdos
        insmod ntfs
        insmod search_fs_uuid
        insmod ntldr     
        search --fs-uuid --set=root --hint-bios=hd0,msdos1 --hint-efi=hd0,msdos1 --hint-baremetal=ahci0,msdos1 69B235F6749E84CE
        ntldr /bootmgr
}

```

لوندوز إكس بي:

```
menuentry "Microsoft Windows XP" {
        insmod part_msdos
        insmod ntfs
        insmod search_fs_uuid
        insmod ntldr     
        search --fs-uuid --set=root --hint-bios=hd0,msdos1 --hint-efi=hd0,msdos1 --hint-baremetal=ahci0,msdos1 69B235F6749E84CE
        ntldr /ntldr
}

```

يمكن استخدام `/etc/grub.d/40_custom` كقالب لإنشاء `/etc/grub.d/nn_custom`. حيث إن الحرفين `nn` الأسبقية ، مما يدل على أمر تنفيذ البرنامج النصي. ويتم تنفيذ البرامج النصية محددة المكان في قائمة إقلاع grub .

**ملاحظة:** `nn` يجب أن يكون أكبر من 06 للتأكد من تنفيذ الأوامر النصية الضرورية أولا .

### أنظمة UEFI

**ملاحظة:** يفضل معرفة الاختلافات بين اللوحات الأم في تطبيق UEFI . المستخدمون الخبراء بالمشكلات يجعلون Grub/EFI يعمل بشكل جيد عليهم مشاركة المعلومات والخطوات الخاصة بحالات معين للعتاد عندما لا يعمل إقلاع UEFI كما تم شرحه بأسفل . في محاولة للمحافظة مقال [GRUB](/index.php/GRUB "GRUB") أنيقا ومرتبا ، قم بقراءة صفحة [GRUB EFI Examples](/index.php/GRUB_EFI_Examples "GRUB EFI Examples") لهذه الحالات الخاصة.

أولا [detect which UEFI firmware arch](/index.php/Unified_Extensible_Firmware_Interface#Detecting_UEFI_Firmware_Arch "Unified Extensible Firmware Interface") لديك إما x86_64 أو i386).وبناء على ذلك الناتج ، قم بتثبيت الحزمة المناسبة:

*   لبرنامج التشغيل الأساسي 64 -bit aka x86_64 UEFI ثبت الحزمة [grub-efi-x86_64](https://www.archlinux.org/packages/?name=grub-efi-x86_64)
*   لبرنامج التشغيل الأساسي 32-bit aka i386 UEFI ثبت الحزمة [grub-efi-i386](https://www.archlinux.org/packages/?name=grub-efi-i386)

**ملاحظة:** بساطة تثبيت الحزمة لن يسبب تحديث ملف `core.efi` و وحدات GRUB في قسم نظام UEFI . ستحتاج إلى استخدام الأمر `grub-install` يدويا كما تم شرحه بأسفل .

#### تثبيت ملفات الإقلاع

##### التثبيت على قسم بنظام UEFI

**ملاحظة:** اﻷوامر التالية تفترض أنك تستخدم `grub-efi-x86_64` ل `grub-efi-i386` ضع `i386` بدلا من `x86_64` في اﻷوامر بأسفل.

**ملاحظة:** للقيام بذلك تحتاج إلى الإقلاع باستخدام UEFI وليس BIOS . إذا قمت بالإقلاع فقط عن طريق نسخ ملف أيزو إلى قرص USB ، عليك اتباع [هذا الدليل](/index.php/Unified_Extensible_Firmware_Interface#Create_UEFI_bootable_USB_from_ISO "Unified Extensible Firmware Interface") سيحتاج نظام تقسيم UEFI إلى التوصيل بالدليل `/boot/efi/` في سكربت تثبيت GRUB حتى يستطيع الكشف عنه :

```
# mkdir -p /boot/efi
# mount -t vfat /dev/sdXY /boot/efi

```

قم بتثبيت التطبيق GRUB UEFI في `/boot/efi/EFI/arch_grub/` وتثبيت وحداته على `/boot/grub/x86_64-efi` (يوصى به) بتنفيذ:

```
# modprobe dm-mod
# grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=arch_grub --recheck --debug
# mkdir -p /boot/grub/locale
# cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo

```

**ملاحظة:** بدون الخيار `target--` أو `directory--` لن يستطيع جروب تحديد أي نوع من المشغلات الأساسة لتثبيتها . في مثل هذه الحالة سقوم `grub-install` بعرض `source_dir doesn't exist. Please specify --target or --directory` الرسالة.

إذا أردت تثبيت وحدات GRUB و الملف `grub.cfg` في الدليل `/boot/efi/EFI/grub/` والتطبيق `grubx64.efi` في `/boot/efi/EFI/arch_grub` ( مثلا ، كل ملفات GRUB UEFI بداخل قسم UEFISYS ذاته) استخدم:

```
# modprobe dm-mod 
# grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=arch_grub --boot-directory=/boot/efi/EFI --recheck --debug
# mkdir -p /boot/efi/EFI/grub/locale
# cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/efi/EFI/grub/locale/en.mo

```

الخيار `efi-directory--` يشير إلى نقطة التوصيل لقسم نظام UEFI , و `--bootloader-id` يشير إلى اسم الدليل المستخدم لتخزين الملف `grubx64.efi` و `--boot-directory` يشير إلى الدليل الذي سيتم عليه تثبيت الوحدات الفعلية ( `grub.cfg`ويشير إلى أين يجب يتم تثبيت ) .

المسارات الفعلية هي:

```
<efi-directory>/<EFI or efi>/<bootloader-id>/grubx64.efi

```

```
<boot-directory>/grub/x86_64-efi/<all modules, grub.efi, core.efi, grub.cfg>

```

**ملاحظة:** the `--bootloader-id` option does not change `<boot-directory>/grub`, i.e. you cannot install the modules to `<boot-directory>/<bootloader-id>`, the path is hard-coded to be `<boot-directory>/grub`.

In `--efi-directory=/boot/efi --boot-directory=/boot/efi/EFI --bootloader-id=grub`:

```
<efi-directory>/<EFI or efi>/<bootloader-id> == <boot-directory>/grub == /boot/efi/EFI/grub

```

In `--efi-directory=/boot/efi --boot-directory=/boot/efi/EFI --bootloader-id=arch_grub`:

```
<efi-directory>/<EFI or efi>/<bootloader-id> == /boot/efi/EFI/arch_grub
<boot-directory>/grub == /boot/efi/EFI/grub

```

In `--efi-directory=/boot/efi --boot-directory=/boot --bootloader-id=arch_grub`:

```
<efi-directory>/<EFI or efi>/<bootloader-id> == /boot/efi/EFI/arch_grub
<boot-directory>/grub == /boot/grub

```

In `--efi-directory=/boot/efi --boot-directory=/boot --bootloader-id=grub`:

```
<efi-directory>/<EFI or efi>/<bootloader-id> == /boot/efi/EFI/grub
<boot-directory>/grub == /boot/grub

```

The `<efi-directory>/<EFI or efi>/<bootloader-id>/grubx64.efi` is an exact copy of `<boot-directory>/grub/x86_64-efi/core.efi`.

**ملاحظة:** In GRUB 2.00, the `grub-install` option `--efi-directory` replaces `--root-directory` and the latter is deprecated.

**ملاحظة:** The options `--efi-directory` and `--bootloader-id` are specific to GRUB UEFI.

In all the cases the UEFI SYSTEM PARTITION should be mounted for `grub-install` to install `grubx64.efi` in it, which will be launched by the firmware (using the `efibootmgr` created boot entry in non-Mac systems).

If you notice carefully, there is no <device_path> option (Eg: `/dev/sda`) at the end of the `grub-install` command unlike the case of setting up GRUB for BIOS systems. Any <device_path> provided will be ignored by the install script as UEFI bootloaders do not use MBR or Partition boot sectors at all.

You may now be able to UEFI boot your system by creating a `grub.cfg` file by following [#Generate UEFI Config file](#Generate_UEFI_Config_file) and [#Create GRUB entry in the Firmware Boot Manager](#Create_GRUB_entry_in_the_Firmware_Boot_Manager).

#### توليد ملف التكوين

Finally, generate a configuration for GRUB (this is explained in greater detail in the Configuration section):

```
# grub-mkconfig -o <boot-directory>/grub/grub.cfg

```

**Note:** The file path is `<boot-directory>/grub/grub.cfg`, NOT `<boot-directory>/grub/x86_64-efi/grub.cfg`.

If you used `--boot-directory=/boot`:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

If you used `--boot-directory=/boot/efi/EFI`:

```
# grub-mkconfig -o /boot/efi/EFI/grub/grub.cfg

```

This is independent of the value of `--bootloader-id` option.

If GRUB complains about "no suitable mode found" while booting, try [#Correct No Suitable Mode Found Error](#Correct_No_Suitable_Mode_Found_Error).

#### إنشاء مدخلة ل GRUB في الجدار الناري لمحمل الإقلاع

`grub-install` automatically tries to create a menu entry in the boot manager. If it doesn't, use `efibootmgr` to create a menu entry. However, the problem is likely to be that you haven't booted your CD/USB in UEFI mode, as in [Unified Extensible Firmware Interface#Create UEFI bootable USB from ISO](/index.php/Unified_Extensible_Firmware_Interface#Create_UEFI_bootable_USB_from_ISO "Unified Extensible Firmware Interface").

#### UEFI إنشاء تطبيق GRUB قابل للتثبيت بنظام

It is possible to create a `grubx64_standalone.efi` application which has all the modules embeddded in a memdisk within the UEFI application, thus removing the need for having a separate directory populated with all the GRUB UEFI modules and other related files. This is done using the `grub-mkstandalone` command which is included in [grub-common](https://www.archlinux.org/packages/?name=grub-common).

The easiest way to do this would be with the install command already mentioned before, but specifying the modules to include. For example:

```
# grub-mkstandalone --directory="/usr/lib/grub/x86_64-efi/" --format="x86_64-efi" --compression="xz" \
--output="/boot/efi/EFI/arch_grub/grubx64_standalone.efi" <any extra files you want to include>

```

The `grubx64_standalone.efi` file expects `grub.cfg` to be within its $prefix which is `(memdisk)/boot/grub`. The memdisk is embedded within the efi app. The `grub-mkstandlone` script allow passing files to be included in the memdisk image to be as the arguments to the script (in <any extra files you want to include>).

If you have the `grub.cfg` at `/home/user/Desktop/grub.cfg`, then create a temporary `/home/user/Desktop/boot/grub/` directory, copy the `/home/user/Desktop/grub.cfg` to `/home/user/Desktop/boot/grub/grub.cfg`, cd into `/home/user/Desktop/boot/grub/` and run:

```
# grub-mkstandalone --directory="/usr/lib/grub/x86_64-efi/" --format="x86_64-efi" --compression="xz" \
--output="/boot/efi/EFI/arch_grub/grubx64_standalone.efi" "boot/grub/grub.cfg"

```

The reason to cd into `/home/user/Desktop/boot/grub/` and to pass the file path as `boot/grub/grub.cfg` (notice the lack of a leading slash - boot/ vs /boot/ ) is because `dir1/dir2/file` is included as `(memdisk)/dir1/dir2/file` by the `grub-mkstandalone` script.

If you pass `/home/user/Desktop/grub.cfg` the file will be included as `(memdisk)/home/user/Desktop/grub.cfg`. If you pass `/home/user/Desktop/boot/grub/grub.cfg` the file will be included as `(memdisk)/home/user/Desktop/boot/grub/grub.cfg`. That is the reason for cd'ing into `/home/user/Desktop/boot/grub/` and passing `boot/grub/grub.cfg`, to include the file as `(memdisk)/boot/grub/grub.cfg`, which is what `grub.efi` expects the file to be.

You need to create an UEFI Boot Manager entry for `/boot/efi/EFI/arch_grub/grubx64_standalone.efi` using `efibootmgr`. Follow [#Create GRUB entry in the Firmware Boot Manager](#Create_GRUB_entry_in_the_Firmware_Boot_Manager).

#### الإقلاع المتعدد

##### UEFI-GPT ميكروسوفت وندوز مثبت على نمط

Find the UUID of the FAT32 filesystem in the UEFI SYSTEM PARTITION where the Windows UEFI Bootloader files reside. For example, if Windows `bootmgfw.efi` exists at `/boot/efi/EFI/Microsoft/Boot/bootmgfw.efi` (ignore the upper-lower case differences since that is immaterial in FAT filesystem):

```
# grub-probe --target=fs_uuid /boot/efi/EFI/Microsoft/Boot/bootmgfw.efi
1ce5-7f28

# grub-probe --target=hints_string /boot/efi/EFI/Microsoft/Boot/bootmgfw.efi
--hint-bios=hd0,gpt1 --hint-efi=hd0,gpt1 --hint-baremetal=ahci0,gpt1

```

Then, add this code to `/etc/grub.d/40_custom` to chainload Windows x86_64 (Vista SP1+, 7 or 8) installed in UEFI-GPT mode:

```
menuentry "Microsoft Windows Vista/7/8 x86_64 UEFI-GPT" {
        insmod part_gpt
        insmod fat
        insmod search_fs_uuid
        insmod chain
        search --fs-uuid --set=root --hint-bios=hd0,gpt1 --hint-efi=hd0,gpt1 --hint-baremetal=ahci0,gpt1 1ce5-7f28
        chainloader /efi/Microsoft/Boot/bootmgfw.efi
}

```

Afterwards remake `/boot/grub/grub.cfg`

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

## التهيئة

يمكنك أيضا الاختيار بن توليد الملف `grub.cfg` او يدويا .

**ملاحظة:** بخصوص أنظمة EFI إذا تم تثبيت GRUB بوضع الخيار `--boot-directory` يجب أن يوضع الملف the `grub.cfg` في نفس الدليل ك `grubx64.efi`. خلافا لذلك سيذهب ملف `grub.cfg` إلى الدليل `/boot/grub/` كما يحدث في GRUB BIOS.

**ملاحظة:** هنا ، شرح كامل لكيفية تهيئة [http://members.iinet.net/~herman546/p20/GRUB2%20Configuration%20File%20Commands.html](http://members.iinet.net/~herman546/p20/GRUB2%20Configuration%20File%20Commands.html) GRUB  :

### توليد ملفات الإقلاع آليا باستخدام grub-mkconfig

ملفات الإعداد الخاصة بجروب والمعادلة ل `menu.lst` هي `/etc/default/grub` و `/etc/grub.d/*`. يستخدم الأمر `grub-mkconfig` هذه الملفات لتوليد الملف `grub.cfg`. افتراضيا فإن مخرجات السكربت معيارية. لتوليد الملف `grub.cfg` نفذ الأمر التالي :

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

تم ضبط `/etc/grub.d/10_linux` لإضافة عناصر القائمة الخاصة بنظام آرتش لينكس التي تعمل خارج النظام ، ولتوليد أي نظام تشغيل أن ربما تحتاج إلى إضافتها يدويا إلى الملف `/etc/grub.d/40_custom` أو `/boot/grub/custom.cfg`

#### خيارات وأوامر إضافية

لتمرير مدخلات إضافية إلى صورة لينكس ، يمكنك ضبط متغيرات `GRUB_CMDLINE_LINUX` في الملف `/etc/default/grub`. على سبيل المثال ؛ استخدم `GRUB_CMDLINE_LINUX="resume=/dev/sdaX"` حيث `sda**X**` هو قسم التبديل swap لديك لإتاحة استعادة الجلسة عند عمل إسبات للنظام. يمكنك أيضا استخدام `GRUB_CMDLINE_LINUX="resume=/dev/disk/by-uuid/${swap_uuid}"` حيث `${swap_uuid}` هو التسمية الثابتة للكتلة [UUID](/index.php/Persistent_block_device_naming "Persistent block device naming") الخاصة بقسم السواب لديك. المدخلات المتعددة يمكن الفصل بينها بمسافة داخل علامات الاقتباس المزدوجة . لذا بخصوص المستخدمين الذين يريدون كلا من resume و systemd يمكن أن يكون ذلك شبيها بما يلي: `GRUB_CMDLINE_LINUX="resume=/dev/sdaX init=/usr/lib/systemd/systemd"`

انظر [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") لمزيد من المعلومات.

### إنشاء ملف grub.cfg يدويا

**تحذير:** يوصى بشدة *بعدم تعديل هذا الملف.* يتم توليد هذا الملف بالأمر `grub-mkconfig` ، ومن الأفضل تحرير الملف `/etc/default/grub` أو واحدا من السكربتات في المجلد`/etc/grub.d` .

ملف الإعداد الأساسي لجروب يستخدم الخيارات التالية:

*   `(hdX,Y)` القسم هو `Y` على القرص `X`, ارقام الأقسام تبدأ بـ 1, بينما ترقيم الأقراص يبدأ بـ 0
*   `set default=N` مدخلة الإقلاع الافتراضي يتم إقلاعها بعد مرور زمن يحدده المستخدم.
*   `set timeout=M` هو مقدار الوقت بالثانية قبل بداية إقلاع النظام الافتراضي.
*   `menuentry "title" {entry options}` هو مدخلة العنوان `title`
*   `set root=(hdX,Y)` تحدد قسم الإقلاع ، حيث تم تخزين النواة ووحدات المحمل جروب (الإقلاع لا يحتاج إلى قسم مستقل ، ويمكن أن يكون ببساطة مجلدا منضويا تحت قسم "الجذر" (`/`)

مثال على الإعدادات:

```
/boot/grub/grub.cfg

```

```
# Config file for GRUB - The GNU GRand Unified Bootloader
# /boot/grub/grub.cfg

# DEVICE NAME CONVERSIONS
#
#  Linux           Grub
# -------------------------
#  /dev/fd0        (fd0)
#  /dev/sda        (hd0)
#  /dev/sdb2       (hd1,2)
#  /dev/sda3       (hd0,3)
#

# Timeout for menu
set timeout=5

# Set default boot entry as Entry 0
set default=0

# (0) Arch Linux
menuentry "Arch Linux" {
        set root=(hd0,1)
        linux /vmlinuz-linux root=/dev/sda3 ro
        initrd /initramfs-linux.img
}

## (1) Windows
#menuentry "Windows" {
#        set root=(hd0,3)
#        chainloader +1
#}

```

### الإقلاع المزدوج

**ملاحظة:** If you want GRUB to automatically search for other systems, you may wish to install [os-prober](https://www.archlinux.org/packages/?name=os-prober).

#### grub-mkconfig استخدام الأمر

The best way to add other entries is editing the `/etc/grub.d/40_custom` or `/boot/grub/custom.cfg` . The entries in this file will be automatically added when running `grub-mkconfig`. After adding the new lines, run:

```
# grub-mkconfig -o /boot/grub/grub.cfg 

```

to generate an updated `grub.cfg`.

##### مع نظام GNU/Linux

Assuming that the other distro is on partition `sda2`:

```
menuentry "Other Linux" {
        set root=(hd0,2)
        linux /boot/vmlinuz (add other options here as required)
        initrd /boot/initrd.img (if the other kernel uses/needs one)
}

```

##### مع نظام FreeBSD

Requires that FreeBSD is installed on a single partition with UFS. Assuming it is installed on `sda4`:

```
menuentry "FreeBSD" {
        set root=(hd0,4)
        chainloader +1
}

```

##### مع نظام وندوز

This assumes that your Windows partition is `sda3`. Remember you need to point set root and chainloader to the system reserve partition that windows made when it installed, not the actual partition windows is on. This example works if your system reserve partition is `sda3`.

```
# (2) Windows XP
menuentry "Windows XP" {
        set root=(hd0,3)
        chainloader (hd0,3)+1
}

```

If the Windows bootloader is on an entirely different hard drive than GRUB, it may be necessary to trick Windows into believing that it is the first hard drive. This was possible with `drivemap`. Assuming GRUB is on `hd0` and Windows is on `hd2`, you need to add the following after `set root`:

```
drivemap -s hd0 hd2

```

#### مع نظام وندوز باستخدام برنامج EasyBCD و NeoGRUB

وحيث إن برنامج NeoGRUB في EasyBCD لا يفهم صيغة قائمة GRUB ، قم بوضع محتويات ملف `C:\NST\menu.lst/` لديك بدلا من اﻷسطر التي تشبه ما يلي:

```
default 0
timeout 1

```

```
title       Chainload into GRUB v2
root        (hd0,7)
kernel      /boot/grub/i386-pc/core.img

```

### إعداد المحسنات البصرية

In GRUB it is possible, by default, to change the look of the menu. Make sure to initialize, if not done already, GRUB graphical terminal, gfxterm, with proper video mode, gfxmode, in GRUB. This can be seen in the section [#Correct No Suitable Mode Found Error](#Correct_No_Suitable_Mode_Found_Error). This video mode is passed by GRUB to the linux kernel via 'gfxpayload' so any visual configurations need this mode in order to be in effect.

#### ضبط دقة شاشة الإقلاع framebuffer

يستطيع GRUB ضبط ال framebuffer لكل من GRUB ذاته وللنواة أيضا. والطريقة `vga=` القديمة . الطريقة المفضلة هي تعديل الملف `/etc/default/grub/` كما يلي:

```
GRUB_GFXMODE=1024x768x32
GRUB_GFXPAYLOAD_LINUX=keep

```

لتفعيل هذه التغيرات نفذ:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

الخاصية `gfxpayload` ستتأكد من احتفاظ النواة بالدقة الجديدة .

**ملاحظة:** إذا لم يعمل المثال السابق جرب وضع `vbemode="0x105"` بدلا من `gfxmode="1024x768x32"` لتحديد دقة العرض مع ما يناسب شاشتك.

**ملاحظة:** لإظهار كافة الأنماط التي يمكنك استخدامها نفذ `# hwinfo --framebuffer` ، والحزمة hwinfo متوفرة في المستودع [community]. بينما في محث GRUB استخدم اﻷمر `vbeinfo`.

إن لم تعمل هذه الطريقة معك فإن الطريقة القديمة باستخدام المدخلة `vga=` ما زالت تعمل . قم فقط بإضافة مدخلة بعد السطر التالي `"GRUB_CMDLINE_LINUX_DEFAULT="` الموجود في الملف `/etc/default/grub` ، عل سبيل المثال ، `"GRUB_CMDLINE_LINUX_DEFAULT="quiet splash vga=792"` سيعطيك دقة `1024x768` . يمكنك الاختيار واحدة من هذه الدقات `640×480`, `800×600`, `1024×768`, `1280×1024`, `1600×1200`, `1920×1200`

#### 915resolution اﻷداة

بخصوص بطاقات إنتل الرسوميةأحيانا لا يقوم اﻷمر `# hwinfo --framebuffer` ولا `vbeinfo` بإظهار الدقة المطلوبة ، وفي هذه الحالة يمكنك استخدام اﻷداة `915resolution` . هذه اﻷداة تعدل مؤقتا برنامج تشغيل البطاقة وتضيف دقة الشاشة المطلوبة. انظر [915resolution's home page](http://915resolution.mango-lang.org/).

في البداية عليك أن تجد نمط الفيديو الذي ستقوم بتعديله لاحقا. ولذلك تحتاج إلى أحد أوامر صدفة GRUB :

 `sh:grub> 915resolution -l` 
```
Intel 800/900 Series VBIOS Hack : version 0.5.3
[...]
**Mode 30** : 640x480, 8 bits/pixel
[...]

```

Next, we overwrite the `Mode 30` with `1440x900` resolution:

 `/etc/grub.d/00_header` 
```
[...]
**915resolution 30 1440 900  # Inserted line**
set gfxmode=${GRUB_GFXMODE}
[...]

```

في النهاية سنحتاج إلى ضبط `GRUB_GFXMODE` كما شرحناه سابقا ، ثم نعيد توليد ملف تكوين GRUB وإعادة تشغيل الحاسوب لاختبار ما تم من تغييرات.

```
# grub-mkconfig -o /boot/grub/grub.cfg
# reboot

```