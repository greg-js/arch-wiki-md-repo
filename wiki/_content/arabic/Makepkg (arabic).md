يستعمل makepkg لتجميع و بنـاء الحزم لتناسب التثبيت بإستعمال [pacman](/index.php/Pacman "Pacman") , مدير التحزيم على ArchLinux. هو مخطوطة تتولى أتممـة بنـاء الحزم , حيث بإمكانها تولي مهمة تحميل و التحقق من صحة الملفات المصدرية , تفحص الإعتماديات ,تهيئة الإعدادت , تجميع المصدر, التثبيت على بيئة جذر مؤقتة , القيام بالتخصيصات , توليد الـ meta-info , لـتقوم في الأخير بـتحزيم كل شيء معاً.

يتوفر makepkg من خلال حزمة [pacman](https://www.archlinux.org/packages/?name=pacman).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 التهيئة](#التهيئة)
    *   [1.1 المعمارية, خيارات التجميع](#المعمارية,_خيارات_التجميع)
        *   [1.1.1 MAKEFLAGS](#MAKEFLAGS)
    *   [1.2 الحزمة الناتجة](#الحزمة_الناتجة)
    *   [1.3 Signature checking](#Signature_checking)
*   [2 الإستعمال](#الإستعمال)
*   [3 خدع وتلميحات](#خدع_وتلميحات)
    *   [3.1 توليد md5sums جديد](#توليد_md5sums_جديد)
    *   [3.2 Makepkg يطلع على PKGBUILD مرتين](#Makepkg_يطلع_على_PKGBUILD_مرتين)
    *   [3.3 تحذير: حزمة تحتوي على مرجع إلى $srcdir](#تحذير:_حزمة_تحتوي_على_مرجع_إلى_$srcdir)
*   [4 انظر أيضا](#انظر_أيضا)

## التهيئة

`/etc/makepkg.conf` هو ملف الإعدادت الرئيسي لـ makepkg . معضم المستخدمين يودون ضبط خيارات الإعدادت قبل الشروع في بناء اي حزمة.

### المعمارية, خيارات التجميع

الـ `MAKEFLAGS`, `CFLAGS`, و `CXXFLAGS` خيارات تستعمل من قبل [make](https://www.archlinux.org/packages/?name=make) , [gcc](https://www.archlinux.org/packages/?name=gcc) , و `g++` أثنـاء تجميع البرامج بإستعمال makepkg. إفتراضياً , هذه الخيارات تُنشأ بشكل عام حزم يمكن تركيبها على طيف واسع من الأجهزة . يمكن تحسين الآداء من خلال ضبط إعدادت تجميع على الجهاز. Tالجانب السلبي في الامر أنه ما جمع خصيصا لمعالج جهاز قد لا يعمل على جهاز أخر.

**ملاحظة:** ضع في بالك أنه ليس كل أنضمة بناء الحزم ستستعمل هذه المتغيرات. فبعضها قد تتجاوزها من خلال ملفات Makefiles الأصلية أو [PKGBUILD](/index.php/PKGBUILD "PKGBUILD").

 `/etc/makepkg.conf` 
```
[...]

#########################################################################
# ARCHITECTURE, COMPILE FLAGS
#########################################################################
#
CARCH="x86_64"
CHOST="x86_64-unknown-linux-gnu"

#-- Exclusive: will only run on x86_64
# -march (or -mcpu) builds exclusively for an architecture
# -mtune optimizes for an architecture, but builds for whole processor family
CPPFLAGS="-D_FORTIFY_SOURCE=2"
CFLAGS="-march=x86-64 -mtune=generic -O2 -pipe -fstack-protector --param=ssp-buffer-size=4"
CXXFLAGS="-march=x86-64 -mtune=generic -O2 -pipe -fstack-protector --param=ssp-buffer-size=4"
LDFLAGS="-Wl,-O1,--sort-common,--as-needed,-z,relro"
#-- Make Flags: change this for DistCC/SMP systems
#MAKEFLAGS="-j2"

[...]

```

الخياران الإفتراضيان `CFLAGS` و `CXXFLAGS` بملف makepkg.conf متوافقان مع جميع الأجهزة within their respective architectures.

على أجهزة x86_64 , نادراً ما يكون لهما أهمية في الآداء مقابل الوقت المستثمر في بناء الحزم الرسمية.

بالإصدار 4.3.0 , تقدم GCC الخيار `-march=native` الذي يسمح بتغعيل الكشف التلقائي للمعالج و الإختيار التلقائي للتحسينات التي يدعمها الجهاز المحلي في GCC runtime. لإستعمالها, يكفي فقط تعديل الخيارات الإفتراضية بتغير أسطر كل من `CFLAGS` و `CXXFLAGS` كالتالي :

```
# -march=native also sets the correct -mtune=
CFLAGS="-march=native -O2 -pipe -fstack-protector --param=ssp-buffer-size=4 -D_FORTIFY_SOURCE=2"
CXXFLAGS="${CFLAGS}"

```

**تلميحة:** لمعاينة خيارات `march=native` , نفذ:
```
 $ gcc -march=native -E -v - </dev/null 2>&1 | sed -n 's/.* -v - //p'

```

Further optimizing for CPU type can theoretically enhance performance because `-march=native` enables all available instruction sets and improves scheduling for a particular CPU. This is especially noticeable when rebuilding applications (for example: audio/video encoding tools, scientific applications, math-heavy programs, etc.) that can take heavy advantage of newer instructions sets not enabled when using the default options (or packages) provided by Arch Linux.

It is very easy to reduce performance by using "non-standard" CFLAGS because compilers tend to heavily blow up the code size with loop unrolling, bad vectorization, crazy inlining, etc. depending on compiler switches. Unless you can verify/benchmark that something is faster, there is a very good chance it is not!

See the GCC man page for a complete list of available options. The Gentoo [Compilation Optimization Guide](http://www.gentoo.org/doc/en/gcc-optimization.xml) and [Safe CFLAGS](http://wiki.gentoo.org/wiki/Safe_CFLAGS) wiki article provide more in-depth information.

#### MAKEFLAGS

يمكن إستعمال خيار `MAKEFLAGS` لتعين خيارات إضافية لـ make. المستخدمون ذوي الأنضمة متعددة-الأنوية/متعددة-المعالجات بإستطاعتهم تحديد عدد المهام الممكن تشغيلها بالتوازي. ويمكن تحقيق ذلك مع استخدام `nproc` لتحديد عدد المعالجات المتاحة, مثلاً. `-j4` حيث *4 هي خارج `nproc`*. بعض ملفات [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") تتجاوز هذا بإستعمال `-j1`, وذلك بسبب التعارض في بعض الإصدارات أو ببساطة لأنها غير مدعومة أصلاً. الحزم التي تفشل في البناء لمثل هذا السبب ينبغي [التبليغ](/index.php/Reporting_bug_guidelines "Reporting bug guidelines") عنها على متتبع العلل وذلك طبعا بعد التأكد فعلا أن العلة تسببب بها MAKEFLAGS الخاص بك.

راجع [make(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/make.1) للحصول على اللائحة الكاملة للخيارات المتاحة.

### الحزمة الناتجة

بالإمكان تحديد مكان وضع الملفات المصدرية و الحزم أثناء البناء, هذا إختياري, فالحزم ستبق إفتراضياً ضمن دليل العمل حيث نفد الأمر makepkg.

 `/etc/makepkg.conf` 
```
[...]

#########################################################################
# PACKAGE OUTPUT
#########################################################################
#
# Default: put built package and cached source in build directory
#
#-- Destination: specify a fixed directory where all packages will be placed
#PKGDEST=/home/packages
#-- Source cache: specify a fixed directory where source files will be cached
#SRCDEST=/home/sources
#-- Source packages: specify a fixed directory where all src packages will be placed
#SRCPKGDEST=/home/srcpackages
#-- Packager: name/email of the person or organization building packages
#PACKAGER="John Doe <john@doe.com>"

[...]

```

كمثال , أنشئ المجلد :

```
$ mkdir /home/$USER/packages

```

ثم عدل المتغير `PKGDEST` بالملف `/etc/makepkg.conf` وفقاً للمجلد السابق.

المتغير `PACKAGER` سيحدد قيمة المحزم `packager` ضمن ملف .`.PKGINFO` للحزمة المجمعة . إفتراضياً , الحزمة المجمعة ستعرض :

 `pacman -Qi package` 
```
[...]
Packager       : Unknown Packager
[...]

```

بعد القيام بالتعديل :

 `pacman -Qi package` 
```
[...]
Packager       : John Doe <john@doe.com>
[...]

```

هذا عملي خصوصاً إدا تعدد المستخدمون المحزمون على النضام , أو إذا قمت من جهة أخرى بتوزيع حزمك ومشاركتها مع مستخدمين آخرين.

### Signature checking

The following procedure is not necessary for compiling with makepkg, for your initial configuration proceed to [#Usage](#Usage). To temporarily disable signature checking call the makepkg command with the `--skippgpcheck` option. If a signature file in the form of .sig is part of the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") source array, makepkg validates the authenticity of source files. For example, the signature pkgname-pkgver.tar.gz.sig is used to check the integrity of the file pkgname-pkgver.tar.gz with the gpg program. If desired, signatures by other developers can be manually added to the gpg keyring. Look into the [GnuPG](/index.php/GnuPG "GnuPG") article for further information.

**ملاحظة:** The signature checking implemented in makepkg does not use pacman's keyring. Configure gpg as explained below to allow makepkg reading pacman's keyring.

The gpg keys are expected to be stored in the user's `~/.gnupg/pubring.gpg` file. In case it does not contain the given signature, makepkg shows a warning.

 `makepkg` 
```
[...]
==> Verifying source file signatures with gpg...
pkgname-pkgver.tar.gz ... FAILED (unknown public key 1234567890)
==> WARNING: Warnings have occurred while verifying the signatures.
    Please make sure you really trust them.
[...]

```

لإظهار القائمة الحالية لمفاتيح gpg إستعمل أمر gpg.

 `gpg --list-keys` 

إن لم يكن الملف pubring.gpg موجود فسيتم إنشاءه في الحال. يمكنك الآن متابعة إعداد GPG من أجل السماح بتجميع حزم AUR المقدمة من طرف مطوري آرش لينكس مع التحقق من التوقيع بنجاح. أضف السطر التالي إلى نهاية ملف إعداد GPG الخاص بك لضم مفاتيح pacman للمفاتيح الشخصية للمستخدم الخاصة بك.

 `~/.gnupg/gpg.conf` 
```
[...]
keyring /etc/pacman.d/gnupg/pubring.gpg

```

كما في السابق عن الإعداد, خارج `gpg --list-keys` يحتوي على قائمة بالمفاتيح والمطورين. الآن makepkg قادر على تجميع حزم AURالمقدمة من طرف مطوري آرش لينكس مع التحقق من التوقيع بنجاح.

## الإستعمال

قبل المضي قدماً , تأكد من أن مجموعة [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) مثبتة . الحزم التابعة لهذه المجموعة غير ضروري تضمينها للائحة الإعتماديات بملف [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") . تبث مجموعة "base-devel" بتنفيذ (بصلاحية root) الأمر :

```
# pacman -S base-devel

```

**ملاحظة:** قبل البدأ في الشكوى من فقدان إعتماديات (make) , تذكر أن مجموعة [base](https://www.archlinux.org/packages/?name=base) من المفترض أن تكون مثبتة على جميع أنضمة Arch Linux . من المفترض أن المجموعة "base-devel" مثبتة قبل أي عملية بناء بـ **makepkg**.

لبناء حزمة . يجب أولا إنشاء الملف [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"), أو بناء مخطوطة كما هو مشروح في [Creating packages](/index.php/Creating_packages "Creating packages"), أو الحصول على واحد من [ABS tree](/index.php/Arch_Build_System "Arch Build System"), [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"), أو من مصدر آخر.

**تحذير:** إبني أو/و نصب الحزم من المصادر الموثوقة فقط.

عند حصولك على ملف `PKGBUILD` , إنتقل إلى المجلد حيث تم حفض الملف و إتبع التعليمات التالية للبناء الحزمة الموصوفة من قبل `PKGBUILD` :

```
$ makepkg

```

لكي يقوم makepkg بتنضيف المخلفات من ملفات ومجلدات , كالملفات المفكوك الضغط عنها إلى $srcdir , أضف الخيار التالي , هذا عملي للبناء المتعدد لنفس الحزمة أو تحديث إصدار الحزمة ,أثتاء إستعمال نفس المجلد ,فهو يمنع الملفات القديمة والمتبقية من التأثير على عملية البناء الجديدة.

```
$ makepkg -c

```

في حالة عدم توفر الإعتماديات , makepkg سيقوم بإرسال إنذار قبل الفشل , لبناء الحزمة وتثبيت الإعتماديات الازمة بشكل آلي , ببساطة إستعمل الأمر :

```
$ makepkg -s

```

لاحظ أنه هذه الإعتماديات يجب أن تكون متوفرة بالمخازن المعتمدة , راجع [pacman#Repositories](/index.php/Pacman#Repositories "Pacman") للمزيد من التفاصيل . بدلا من ذلك , بمقدورك تنصيب الإعتماديات الضرورية لعملية البناء يدوياً بـ (`pacman -S --asdeps dep1 dep2`).

فور توفر جميع الإعتماديات و بناء الحزمة بنجاح , حزمة بإسم (`pkgname-pkgver.pkg.tar.xz`) سيتم إنشاءها على مسار العمل , للتنصيب , نفذ (كجذر) :

```
# pacman -U pkgname-pkgver.pkg.tar.xz

```

بدلا من ذلك، للتثبيت، إستخدام خيار `-i` هو وسيلة أسهل من تشغيل `pacman -U pkgname-pkgver.pkg.tar.xz`، كما في:

```
$ makepkg -i

```

## خدع وتلميحات

### توليد md5sums جديد

منذ [pacman 4.1](http://allanmcrae.com/2013/04/pacman-4-1-released/), `makepkg -g >> PKGBUILD` لم يعد ضورياً كون pacman-contrib قد تم [دمجه](https://projects.archlinux.org/pacman.git/tree/NEWS) جنبا إلى جنب مع المخطوطة updpkgsums الذي من من شأنه تولد `updpkgsums` جديدة واستبدالها في PKGBUILD:

```
$ updpkgsums

```

### Makepkg يطلع على PKGBUILD مرتين

Makepkg يطلع على PKGBUILD مرتين (المرة الأولى عند مستهل التشغيل, والثانية في بيئة fakroot). لذلك اي وضائف غير قياسية موضوعة بـPKGBUILD سيتم تشغيلها مرتين أيضاً.

### تحذير: حزمة تحتوي على مرجع إلى $srcdir

بطريقة ما, السلاسل الحرفية `$srcdir` أو `$pkgdir`ينتهي بها المطاف للظهور في أحدالملفات المنثيتة في الحزمة الخاصة بك . لتحديد أي الملفات, نفذ التالي من دليل بناء makepkg:

```
$ grep -R "$(pwd)/src" pkg/

```

[Link](http://www.mail-archive.com/arch-general@archlinux.org/msg15561.html) لمناقشة الموضوع.

## انظر أيضا

*   [gcccpuopt](https://github.com/pixelb/scripts/blob/master/scripts/gcccpuopt): مخطوطة لعرض خيارات gcc المصممة خصيصاً لـ CPU الحالي