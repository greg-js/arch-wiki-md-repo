أدناه قائمة بالأسئلة المتكررة عن توزيعة آرتش لينوكس بمعمارية 64 بت.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 كيف يمكنني أن أحدد ما إذا كان معالجي متوافقاً مع معمارية 64 بت أم لا؟](#كيف_يمكنني_أن_أحدد_ما_إذا_كان_معالجي_متوافقاً_مع_معمارية_64_بت_أم_لا؟)
    *   [1.1 لمستخدمي لينوكس](#لمستخدمي_لينوكس)
    *   [1.2 لمستخدمي نظام التشغيل ويندوز](#لمستخدمي_نظام_التشغيل_ويندوز)
*   [2 هل يجب أن أستخدم نسخة آرتش 32 بت أم 64 بت؟](#هل_يجب_أن_أستخدم_نسخة_آرتش_32_بت_أم_64_بت؟)
*   [3 كيف يمكنني تثبيت آرتش 64؟](#كيف_يمكنني_تثبيت_آرتش_64؟)
*   [4 ما مدى اكتمال المستودعات؟](#ما_مدى_اكتمال_المستودعات؟)
*   [5 هل سأتمكن من الحصول على كل الحزم التي اعتدت على استخدامها في آرتش 32 بت؟](#هل_سأتمكن_من_الحصول_على_كل_الحزم_التي_اعتدت_على_استخدامها_في_آرتش_32_بت؟)
*   [6 لماذا أختار 64 بت؟](#لماذا_أختار_64_بت؟)
*   [7 كيف يمكنني التبليغ عن العلل bugs؟](#كيف_يمكنني_التبليغ_عن_العلل_bugs؟)
*   [8 ما هي المستودعات التي يستخدمها مدير الحزم pacman حتى أقوم بتثبيتها؟](#ما_هي_المستودعات_التي_يستخدمها_مدير_الحزم_pacman_حتى_أقوم_بتثبيتها؟)
*   [9 كيف يمكنني ترميم حزم PKGBUILDs الحالية لكي تعمل على آرتش 64؟](#كيف_يمكنني_ترميم_حزم_PKGBUILDs_الحالية_لكي_تعمل_على_آرتش_64؟)
*   [10 ما الذي سأفتقده في آرتش 64؟](#ما_الذي_سأفتقده_في_آرتش_64؟)
*   [11 هل أستطيع تشغيل تطبيقات بنسخة 32 بت داخل آرتش 64 بت؟](#هل_أستطيع_تشغيل_تطبيقات_بنسخة_32_بت_داخل_آرتش_64_بت؟)
*   [12 هل يمكنني أن أبني حزمة 32 بت ﻷجهزة i686 داخل آرتش 64؟](#هل_يمكنني_أن_أبني_حزمة_32_بت_ﻷجهزة_i686_داخل_آرتش_64؟)
    *   [12.1 مستودع Multilib](#مستودع_Multilib)
*   [13 هل أستطيع الترقية أو الانتقال من نظام i686 إلى x86_64 بدون إعادة تثبيت؟](#هل_أستطيع_الترقية_أو_الانتقال_من_نظام_i686_إلى_x86_64_بدون_إعادة_تثبيت؟)

## كيف يمكنني أن أحدد ما إذا كان معالجي متوافقاً مع معمارية 64 بت أم لا؟

### لمستخدمي لينوكس

قم بتنفيذ الأمر التالي في الطرفية:

```
$ less /proc/cpuinfo

```

ابحث عن المدخل `flags` إذا وجدت كلمة `lm` فإن معالجك متوافق مع معمارية 64 بت. أو يمكنك تنفيذ الأمر التالي:

```
$ grep -q "^flags.*\blm\b" /proc/cpuinfo && echo "x86_64" || echo "not x86_64"

```

### لمستخدمي نظام التشغيل ويندوز

تستطيع تحديد توافق معالجك مع معمارية 64 بت باستخدام التطبيق المجاني [CPU-Z](http://www.cpuid.com/cpuz.php)، ينبغي على معالجات شركة AMD ذات مجموعة التعليمات "AMD64" أو معالجات Intel "EM64T" أن تكون متوافقة مع إصدارات 64 بت والحزم الثنائية binary packages.

## هل يجب أن أستخدم نسخة آرتش 32 بت أم 64 بت؟

إذا كان معالجك يدعم [x86_64](https://en.wikipedia.org/wiki/X86-64 "wikipedia:X86-64") ينبغي أن تستخدم آرتش 64.

## كيف يمكنني تثبيت آرتش 64؟

قم بالاطلاع على [official installation ISO CD](https://www.archlinux.org/download/)

## ما مدى اكتمال المستودعات؟

المستودعات جاهزة للاستخدام اليومي للحواسيب والمُخدمات.

## هل سأتمكن من الحصول على كل الحزم التي اعتدت على استخدامها في آرتش 32 بت؟

مستودعات التطبيقات للمعماريتين متصلة ببعضها وكل الأمور وإلى حد كبير ستسير على ما يرام كما هو متوقع لها. في حالات نادرة تكون الحزم القديمة في مستودعات [AUR](/index.php/AUR "AUR") تدعم فقط أنظمة `'i686'` أي 32 بت، ولكن عادة ما تعمل هذه الحزم على 64 بت أيضاً، فقط قم بإضافة `'x86_64'`

## لماذا أختار 64 بت؟

معمارية 64 بت أسرع في أغلب ظروف التشغيل، كما أنها بطبيعتها تكون آمنة أكثر بفضل [Address space layout randomization (ASLR)](https://en.wikipedia.org/wiki/Address_space_layout_randomization "wikipedia:Address space layout randomization") (وهو عبارة عن نظام حماية) بالاشتراك مع [Position-independent code (PIC)](https://en.wikipedia.org/wiki/Position-independent_code "wikipedia:Position-independent code") و [NX Bit](https://en.wikipedia.org/wiki/NX_Bit "wikipedia:NX Bit") (تقنيات خاصة بالحماية أيضاً) والتي لا تكون متوفرة في أنوية i686 بسبب تعطيل ميزة PAE.

إذا كان حاسوبك يحوي على 4 غيغابايت أو أكثر من ذاكرة RAM فيجب عليك أن تضع باعتبارك أن أنظمة 32 بت لا تستطيع التعامل مع ذواكر أكبر من 4 غيغابايت، وبالتالي عليك بـ 64 بت.

وبما أن معالجات x86 الجديدة تدعم معمارية 64 بت فإن المبرمجين بدأو وبنحو متزايد تقليل اهتمامهم بأنظمة 32 بت ("legacy").

لمعلومات إضافية قم بمشاهدة [differences reports](https://www.archlinux.org/packages/differences/)، ستجد مقارنة بين حزم وتطبيقات أنظمة 32 بت و64بت.

## كيف يمكنني التبليغ عن العلل bugs؟

ببساطة قم بالدخول إلى صفحة [Flyspray](https://bugs.archlinux.org/)، قم باختيار x86_64 في حقل تحديد المعمارية إذا كنت تعتقد أنها مشكلة port-related.

## ما هي المستودعات التي يستخدمها مدير الحزم pacman حتى أقوم بتثبيتها؟

كل المستودعات مدعومة.

## كيف يمكنني ترميم حزم PKGBUILDs الحالية لكي تعمل على آرتش 64؟

قم بإضافة هذا المتغير إلى جميع الحزم المشتركة بين المعماريتين:

```
arch=('i686' 'x86_64') 

```

أضف بعض الترقيعات الصغيرة مباشرة إلى الحزم المصدرية وإلى md5sums أما الحزم المختلفة تماماً فلا ينفع معها الإضافة:

```
[ "$CARCH" = "x86_64" ] && source=(${source[@]} 'other source')
[ "$CARCH" = "x86_64" ] && md5sums=(${md5sums[@]} 'other md5sum')

```

لأي إصلاح صغير قم بالتالي في منطقة البناء build area:

```
[ "$CARCH" = "x86_64" ] && (patch -Np0 -i ../foo_x86_64.patch)

```

أو عندما تريد المزيد من التعديلات:

```
if [ "$CARCH" = "x86_64" ]; then
    configure/patch/sed      # for x86_64
  else configure/patch/sed   # for i686
fi

```

## ما الذي سأفتقده في آرتش 64؟

تقريباً كل التطبيقات أصبحت تدعم 64 بت أو أنها في مرحلة الانتقال إلى دعم 64 بت، وبالتالي فإنك لن تفتقد أي شيء على الإطلاق. المشكلة الكبيرة تقع في بعض التطبيقات التي إما أن تكون **مغلقة المصدر** **closed source** أو أنها تحوي على تكوينات مخصصة لـ x86 والتي من الصعب تشغيلها على 64 بت (النموذجي لمحاكي الطرفية).

هذه التطبيقات كانت تسبب إشكالية سابقاً ولكنها الآن أصبحت متوفرة في مستودعات [AUR](/index.php/AUR "AUR") وتعمل بشكل جيد.

*   تطبيق Acrobat Reader غير متوفر بنسخة 64 بت، لكن يمكنك تشغيل نسخة 32 بت في وضع التوافق compatibility mode، مع العلم أنه تتوفر بدائل كثيرة لقراءة ملفات PDF.

كل شيء آخر ينبغي أن يعمل بشكل ممتاز، إذا افتقدت أي حزمة بنسخة 32 بت في مستودعاتنا وتعلم أنها ستعمل (أو سيتم ترجمتها compile) على x86_64 (أو لعلك وجدت نفس الحزمة التي تريدها متوفرة بشكل رسمي على توزيعة 64 بت أخرى) قم بمراسلة المطور أو قم بطلب حزمة جديدة في منتديات آرتش.

## هل أستطيع تشغيل تطبيقات بنسخة 32 بت داخل آرتش 64 بت؟

نعم تستطيع.

*   يمكنك تثبيت مكتبات `lib32-*` من مستودع [multilib]، لاستخدام هذا المستودع يجب عليك أن تضيف الأسطر التالية إلى ملف `/etc/pacman.conf`:

```
[multilib]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

```

حالياً (ديسمبر 2011) يحوي مستودع [multilib] على تطبيقي wine و Skype كما أن multilib compiler متوفر أيضاً.

*   أو يمكنك إنشاء جذر root جديد بنظام 32 بت (قم بالرجوع إلى [Arch64 Install bundled 32bit system](/index.php/Arch64_Install_bundled_32bit_system "Arch64 Install bundled 32bit system")):

أقلع نظام آرتش64 ثم startx ثم افتح الطرفية:

```
$ xhost +local:
$ su
# mount /dev/sda1 /mnt/arch32
# mount --bind /proc /mnt/arch32/proc
# chroot /mnt/arch32
# su your32bitusername
$ /usr/bin/command-you want # or eg: /opt/mozilla/bin/firefox

```

بعض تطبيقات 32 بت (مثل OpenOffice) قد تتطلب روابط إضافية، الأسطر التالية يمكن وضعها في الملف `/etc/rc.local` لضمان أنك استوفيت كل المتطلبات لتشغيل تطبيقات 32 بت (على افتراض أن `/mnt/arch32` تم ربطه في `/etc/fstab`):

```
mount --bind /dev /mnt/arch32/dev
mount --bind /dev/pts /mnt/arch32/dev/pts
mount --bind /dev/shm /mnt/arch32/dev/shm
mount --bind /proc /mnt/arch32/proc
mount --bind /proc/bus/usb /mnt/arch32/proc/bus/usb
mount --bind /sys /mnt/arch32/sys
mount --bind /tmp /mnt/arch32/tmp
#comment the following line if you do not use the same home folder
mount --bind /home /mnt/arch32/home

```

يمكنك بعدها أن تكتب في الطرفية:

```
$ xhost +localhost
$ sudo chroot /mnt/arch32 su your32bitusername /opt/openoffice/program/soffice

```

## هل يمكنني أن أبني حزمة 32 بت ﻷجهزة i686 داخل آرتش 64؟

نعم يمكنك ذلك بأحد طريقتين:

*   باستخدام نسخة [multilib] من الحزم ذات الصلة في مستودع [multilib].
*   أو عن طريق جذر i686

### مستودع Multilib

لكي تستطيع استخدام مستودع [multilib] قم بإزالة تعليق الأسطر التالية في ملف `/etc/pacman.conf` :

```
[multilib]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

```

قم بترقية النظام عن طريق `pacman -Syu` وثبت حزمة [gcc-multilib](https://www.archlinux.org/packages/?name=gcc-multilib)

**ملاحظة:**

*   إذا كانت مجموعة حزم `base-devel` مثبة على الجهاز فيجب استبدال نسخة [extra] بنسخة [mutlilib] كما هو موضح أدناه.
*   حزمة [gcc-multilib](https://www.archlinux.org/packages/?name=gcc-multilib) قادرة على بناء أكواد 32 بت و64 بت، يمكنك تثبيت `multilib-devel` لاستبدال الحزم الموضوحة أدناه، لكنك ما زلت تحتاج إلى حزمة `base-devel` بسبب الحزم الأخرى التي تضمها، اطلع على https://bbs.archlinux.org/viewtopic.php?id=102828 لمزيد من المعلومات.

 `# pacman -S gcc-multilib` 
```
resolving dependencies...
warning: dependency cycle detected:
warning: lib32-gcc-libs will be installed before its gcc-libs-multilib dependency
looking for inter-conflicts...
:: gcc-libs-multilib and gcc-libs are in conflict. Remove gcc-libs? [y/N] y
:: binutils-multilib and binutils are in conflict. Remove binutils? [y/N] y
:: gcc-multilib and gcc are in conflict. Remove gcc? [y/N] y
:: libtool-multilib and libtool are in conflict. Remove libtool? [y/N] y

Remove (4): gcc-libs-4.6.1-1  binutils-2.21.1-1  gcc-4.6.1-1  libtool-2.4-4

Total Removed Size:   87.65 MB

Targets (7): lib32-glibc-2.14-4  lib32-gcc-libs-4.6.1-1  gcc-libs-multilib-4.6.1-1  binutils-multilib-2.21.1-1
             gcc-multilib-4.6.1-1  lib32-libtool-2.4-2  libtool-multilib-2.4-2

Total Download Size:    25.04 MB
Total Installed Size:   108.27 MB

Proceed with installation? [Y/n]
```

ترجمة Compiling حزم i686 على x86_64 سهل جداً ويحتاج فقط إلى إضافة الأسطر التالية إلى ملف تكوين بديل (على سبيل المثال: `~/.makepkg.i686.conf`):

```
CARCH="i686"
CHOST="i686-pc-linux-gnu"
CFLAGS="-m32 -march=i686 -mtune=generic -O2 -pipe -fstack-protector --param=ssp-buffer-size=4 -D_FORTIFY_SOURCE=2"
CXXFLAGS="${CFLAGS}"

```

ومن ثم باستدعاء makepkg عن طريق:

```
$ linux32 makepkg -src --config ~/.makepkg.i686.conf

```

## هل أستطيع الترقية أو الانتقال من نظام i686 إلى x86_64 بدون إعادة تثبيت؟

لا تستطيع ذلك، لكن يمكنك الاطلاع على [هذا](https://bbs.archlinux.org/viewtopic.php?id=64485) الموضوع في منتديات آرتش الذي يخبرك كيف تنتقل من 32 إلى 64 دون أن تفقد أي إعدادات أو بيانات (تحتاج إلى قرص صلب خارجي لعملية النقل).

يمكنك أن تقلع من قرص تثبيت آرتش64 ثم تربط mount القرص الصلب الذي توجد عليه ملفاتك ومن ثم قم بعمل نسخة احتياطية عنهم ومن ثم قم بتثبيت آرتش64.

قد تود الاطلاع أيضاً على [Migrating Between Architectures Without Reinstalling](/index.php/Migrating_Between_Architectures_Without_Reinstalling "Migrating Between Architectures Without Reinstalling").