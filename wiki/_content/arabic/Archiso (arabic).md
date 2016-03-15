**Archiso** هي مجموعة صغيرة من البرامج النصية الخاصة بالصدفة bash قادرة على بناء صورة لقرص إقلاعي سواءً أكان CD أو USB لتوزيعة Arch Linux , هذه الأداة عامة جداً , لذا فهي تُتيح لك إمكانية توليد العديد من أنواع الأقراص : بدءًا من أنظمة الإستعادة وحتى أقراص التنصيب و الأقراص الحية CD/DVD/USB . ببساطة إن كانت تتضمن Arch على إسطوانة براقة فهي قادرة على فعل ذلك. تعد الأداة mkarchiso بمثابة القلب والروح بالنسبة ل Archiso .جميع خيارات هذه الأداة تم توثيقها في مخرجات الاستخدام , لذا استخدامها المباشر لن يتم التطرق إليه هنا . يساعدك مقال الويكي التالي على إنشاء قرصك الحي في وقت بالغ القصر .

## Contents

*   [1 الإعداد](#.D8.A7.D9.84.D8.A5.D8.B9.D8.AF.D8.A7.D8.AF)
*   [2 إعداد القرص الحي](#.D8.A5.D8.B9.D8.AF.D8.A7.D8.AF_.D8.A7.D9.84.D9.82.D8.B1.D8.B5_.D8.A7.D9.84.D8.AD.D9.8A)
    *   [2.1 تنصيب الحزم](#.D8.AA.D9.86.D8.B5.D9.8A.D8.A8_.D8.A7.D9.84.D8.AD.D8.B2.D9.85)
    *   [2.2 إضافة مستخدم](#.D8.A5.D8.B6.D8.A7.D9.81.D8.A9_.D9.85.D8.B3.D8.AA.D8.AE.D8.AF.D9.85)
    *   [2.3 إضافة ملفات إلى صورة القرص الحي](#.D8.A5.D8.B6.D8.A7.D9.81.D8.A9_.D9.85.D9.84.D9.81.D8.A7.D8.AA_.D8.A5.D9.84.D9.89_.D8.B5.D9.88.D8.B1.D8.A9_.D8.A7.D9.84.D9.82.D8.B1.D8.B5_.D8.A7.D9.84.D8.AD.D9.8A)
    *   [2.4 aitab](#aitab)
    *   [2.5 محمل الإقلاع](#.D9.85.D8.AD.D9.85.D9.84_.D8.A7.D9.84.D8.A5.D9.82.D9.84.D8.A7.D8.B9)
    *   [2.6 مدير تسجيل الدخول](#.D9.85.D8.AF.D9.8A.D8.B1_.D8.AA.D8.B3.D8.AC.D9.8A.D9.84_.D8.A7.D9.84.D8.AF.D8.AE.D9.88.D9.84)
*   [3 بناء ملف ISO](#.D8.A8.D9.86.D8.A7.D8.A1_.D9.85.D9.84.D9.81_ISO)
*   [4 استخدام ملف ISO](#.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_.D9.85.D9.84.D9.81_ISO)
    *   [4.1 CD](#CD)
    *   [4.2 USB](#USB)
    *   [4.3 grub4dos](#grub4dos)
    *   [4.4 التنصيب](#.D8.A7.D9.84.D8.AA.D9.86.D8.B5.D9.8A.D8.A8)
*   [5 See also](#See_also)

## الإعداد

**ملاحظة** البرنامج النصي التالي يجب استخدامه على جهاز يعمل بمعمارية x86_64
. قبل البدء يجب عليك [تنصيب](/index.php/Pacman "Pacman")[archiso](https://www.archlinux.org/packages/?name=archiso) من [المستودعات الرسمية](/index.php/Official_repositories "Official repositories") بشكل آخر يمكنك الحصول عليه من [AUR](/index.php/AUR "AUR").

قم بإنشاء مجلد جديد لكي تعمل داخله , هذا المجلد يحتوي على جميع التعديلات الي ستجري على القرص الحي : `~/archlive` سيكون مناسباً .

```
$ mkdir ~/archlive

```

البرامج النصية الخاصة بالحزمة Archiso التي تم تنصيبها على الجهاز المُضيف host مسبقا يجب نقلها الى المجلد الجديد الذي تم إنشاؤه , Archiso يأتي "profiles" بنمطين : *releng* و *baseline*. , إذا اردت إنشاء قرص حي مُخصص بشكل كبير من Arch Linux يكون منصباً عليها جميع البرامج التي تريدها بالإضافة الى الإعددات قم باستخدم *releng*. وأما إذا أردت فقط إنشاء قرص إقلاعي بسيط لا يحتوي على برامج مسبقة التثبيت و يحوي الحد الأدنى من الإعدادات استخدم *baseline*. لذا حسب احتياجاتك قم بتنفيذ التعليمة التالية مستبدلاً كلمة 'PROFILE' وضع إحدى الكلمتين : **releng** أو **baseline**.

```
# cp -r /usr/share/archiso/configs/**PROFILE**/ ~USER/archlive

```

إذا كنت تستخدم نمط *releng* لإنشاء قرص كامل التخصيص يجب عليك الانتقال الى الخطوة [#إعداد القرص الحي](#.D8.A5.D8.B9.D8.AF.D8.A7.D8.AF_.D8.A7.D9.84.D9.82.D8.B1.D8.B5_.D8.A7.D9.84.D8.AD.D9.8A). أما إذا كنت تستخدم نمط *baseline* لإنشاء قرص حي بسيط , لذا فإنك لا تحتاج الى أي تعديلات او تخصيصات و يمكنك مباشرة الإنتقال الى الخطوة [#بناء ملف ISO](#.D8.A8.D9.86.D8.A7.D8.A1_.D9.85.D9.84.D9.81_ISO).

## إعداد القرص الحي

هذا القسم يُفصل كيفية تهيئة إعدادت صورة القرص الحي الذي ستقوم بإنشائه سامحاً لك بتحديد الحزم و الإعدادات التي ترغب في تضمينها الى صورة القرص . الآن إنتقل الى المجلد الذي قمت بإنشائه مسبقاً (~/archlive/releng/ اذا كنت تتبع خطوات هذا الدليل) ستشاهد عدداً من الملفات والمجلدات :

	داخله , نحن مهتمون بعدد منها فحسب , بشكل رئيسي

packages.* هنا نقوم سطرًا بسطر بإنشاء قائمة للحزم التي تريد تنصيبها , هذا المجلد root-image وهو المجلد الجذر لصورة القرص الذي يعمل كطبقة فوقية حيث يحتوي على جميع التغيرات التي سنقوم بها .

### تنصيب الحزم

عليك إنشاء قائمة بالحزم التي تريد تنصيبها على القرص الحي ; بإنشاء ملف يحوي على أسماء الحزم كاملةً حيث يجب أن يكون هنالك اسم حزمة واحدة في كل سطر , هذه الجزئية ***عظيمة القدر'** حيث تسمح لك بإنشاء أقراص حية ذات توجه مُعين , فقط عليك تحديد الحزم التي تُريد ومن م القيام بإنشاء ملف iso الخاص بالقرص .* الملفان packages.i686 و packages.x86_64 يسمحان لك بتحديد الحزم التي التي سيتم تنصيبها على معماريات 32 bit أو 64 bit على و الترتيب .

**تلميحة :** يمكنك أيضا إنشاء مستودع محلي خاص بك **[custom local repository](/index.php/Custom_local_repository "Custom local repository")** أو باستخدام الحزم من [AUR](/index.php/AUR "AUR")/[ABS](/index.php/ABS "ABS"). , عليك فقط إضافة مستودعك المحلي في أعلى الملف **pacman.conf** للحصول على أولوية عن باقي المستودعات، ثم انطلق .

يُفضل تنصيب "rsync" إذا أردت تنصيب النظام الذي تُريد إنشاؤه في وقت لاحق دون الحاجة الى وجود اتصال بالإنترنت أو لتجاوز خطوة إعادة تحميل الحزم مرة اخرى .([#التنصيب](#.D8.A7.D9.84.D8.AA.D9.86.D8.B5.D9.8A.D8.A8))

### إضافة مستخدم

توجد طريقتان لإنشاء المستخدمين ; أما بإضافة تعليمة useradd المناسبة الى ملف rc.local أو عن طريق نسخ و تعديل الملفات التالية /etc/shadow, /etc/passwd, و /etc/group الطريقة الأخيرة سيتم اعتمادها بالشرح هنا . في البداية انسخ ملفات /etc/shadow, /etc/passwd, و /etc/group من النظام المُضيف **host** الذي تستخدمه في بناء القرص الحي إلى المجلد /etc/ **الخاص بالنظام الجديد على القرص الحي** : والذي ينبغي أن يكون /archlive/releng/root-image/etc/~.

```
# cp /etc/{shadow,passwd,group} ~/archlive/releng/root-image/etc/

```

**تحذير:**  : ملف shadow الذي قمت بنسخه يحتوي على كلمة المرور الخاصة بك و التي سيستخدمها مُستخدم القرص الحي , لذا يُفضل تغيير كلمة المرور الخاصة بك قبل نسخ ملف shadow على القرص الحي ، قم بتغيير كلمة مرور النظام المضيف التي تريد أن يستخدمها مستخدم القرص الحي، ثم بعدها قم بالعودة إلى كلمة السر خاصتك.

### إضافة ملفات إلى صورة القرص الحي

**ملاحظة :** يجب أن تكون مستخدماً مديراً للنظام (مستخدم جذر root) للقيام بهذه **المهمة , لا تقم بتغيير ملكية أي ملف تقوم بنسخه .** **جميع الملفات** الموجودة داخل المجلد الجذر / يجب أن تكون مملوكة للمستخدم root سيتم فرز الملكيات في وقت قصير.

إن مجلد root-image يُمثل صندوقاً يحتوي على الملفات الموجودة في اعتبره كالمجلد الجذر '/' في نظامك الحالي، لذا كل الملفات التي تضعها في هذا المجلد سيتم نسخها على القرص الحي لذا في حال كان لديك نسخة من برامج النصية iptables على نظامك الحالي الخاصة ببرنامج و أردت إستخدامها في القرص الحي يمكنك نسخها باستخدام التعليمة التالية :

```
# cp -r /etc/iptables ~/archlive/releng/root-image/etc

```

لكن وضع الملفات داخل مجلد المنزل للمستخدمين مختلف قليلاً حيث لا يمكن وضعهم مباشرة ضمن المجلد root-image/home , وإنما ستقوم بإنشاء مجلد skel داخل root-image وتقوم بوضع الملفات هناك وبعد ذلك تقوم بإضافة التعليمات المناسبة لملف rc.local التي تقوم بنسخ هذه الملفات الى مجلد المنزل الخاص بالمستخدم عند الإقلاع و تقوم بإعطاء الصلاحيات المناسبة لها . في البداية أنشئ مجلد skel ويجب عليك التأكد من أنك داخل المجلد : /archlive/releng/root-image/etc/~ (إذا كنت تعمل من خلاله):

1.  cd ~/archlive/releng/root-image/etc && mkdir skel

الآن قم بنسخ الملفات الموجودة داخل مجلد المنزل 'home' في النظام المُضيف الى داخل مجلد skel , تذكر بأنه يجب عليك تطبيق جميع التعليمات كمستخدم جذر root فمثلا بخصوص ملف bashrc :

```
# cp ~/.bashrc ~/archlive/releng/root-image/etc/skel/

```

لآن داخل مجلد root-image/etc/ قم بإنشاء ملف rc.local **وتأكد** من أنك أعطيت الملف صلاحيات التنفيذ

```
# cd ~/archlive/releng/root-image/etc && touch rc.local && chmod +x rc.local

```

الآن قم بإضافة السطور التالية الى ملف rc.local مُستبدلاً كلمة 'youruser' باسم المستخدم الذي قُمت بتحديده

1.  قم بإنشاء مجلد المستخدم للجلسة الحية

```
if [ ! -d /home/**youruser** ]; then
    mkdir /home/**youruser** && chown **youruser** /home/**youruser**
fi

```

1.  انسخ الملفات إلى مجلد المنزل.

```
su -c "cp -r /etc/skel/.* /home/**youruser**/" **youruser**

```

### aitab

الملف الافتراضي يجب أن يعمل بشكل جيد , لذا لا تقم بتعديله . ملف aitab يحتوي معلومات حول حول انظمة الملفات الخاصة بالصور التي يتم إنشاءها بواسطة mkarchiso ويتم وصلها -mount- في مرحلة initramfs من خلال خطاف archiso hook. وهي تتألف من بعض الحقول التي تُحدد سلوك الصور

```
# <img>         <mnt>                 <arch>   <sfs_comp>  <fs_type>  <fs_size>

```

	<img>

	اسم الصورة بدون لاحقة (.fs .fs.sfs .sfs).

	<mnt>

	نقظة الوصل.

	<arch>

	المعماريات{ i686 | x86_64 | any }.

	<sfs_comp>

	نوع ضغط نظام الملفات SquashFS { gzip | lzo | xz }.

	<fs_type>

	ضع نوع نظام الملفات الخاص بالصورة { ext4 | ext3 | ext2 | xfs }.قيمة خاصة من "none" يدل على عدم استخدام أي نظام الملفات

توضع الملفات مباشرة إلى نظام ملفات في هذه الحالة SquashFS.

	<fs_size>

	بايت الصورة قيمة محددة لحجم نظام ملفات بالميجا (مثال : 100, 1000, 4096, إلخ)

قيمة بديلة للمساحة الخالية على نظام الملفات [بالنسبة المئوية] {1%..99%} (مثال 50%, 10%, 7%).هذه قيمة تقديرية وتحسب بطريقة بسيطة المساحة المستخدمة + 10% (مقدرة للحمل الزائد) + المطلوب %

**Note:** Some combinations are invalid. Example both sfs_comp and fs_type are set to none

### محمل الإقلاع

الملف الإفتراضي يجب أن يعمل بشكل جيد , لا تقم بتعديله .

بسبب الطبيعة الواحدية لـ isolinux , فيمكنك استخدام العديد من الإضافات لطالما جميع ملفات *.c32 تم نسخها و هي متوفرة لديك و يمكنك إلقاء نظرة سريعة على [الرسمي syslinux موقع](http://syslinux.zytor.com/wiki/index.php/SYSLINUX) بالإضافة الى [archiso git repo](https://projects.archlinux.org/archiso.git/tree/configs/syslinux-iso/boot-files). باستخدام الإضافات يمكنك إنشاء قوائم ذات مظهر جميل و معقد بآن واحد , شاهد المثال [هنا](http://syslinux.zytor.com/wiki/index.php/Comboot/menu.c32).

### مدير تسجيل الدخول

تشغيل X في زمن الإقلاع كان يتم عن طريق تعديل inittab في الأنظمة التي تعتمد على sysvinit , في انظمة systemd يتم تفعيل ذلك عن طريق تفعيل خدمة تسجيل الدخول الخاصة بك . إذا كنت تعرف أي ملف .service يحتاج الى رابط softlink فهذا شيئ جيد , أما إذا لم تكن تعرف ذلك فيمكنك ببساطة إيجاده إذا كنت الخدمة ذاتها في النظام المُضيف الذي تقوم بإنشاء القرص الحي عليه فقط قم بتنفيذ التعليمة التالية

```
# systemctl disable **nameofyourloginmanager**

```

لكي توقف عمله مؤقتاً . الآن قم بإعادة كتابة التعليمة السابقة مع إستبدال كلمة disable بكلمة enable لإعادة تفعيلها مرة اخرى , Systemctl يقوم بإظهار معلومات عن الروابط التي يقوم بإنشاءها . الآن إنتقل الى المجلد ~/archiso/releng/root-image/etc/systemd/system وقم بإنشاء الرابط softlink ذاته

```
# ln -s /usr/lib/systemd/system/lxdm.service display-manager.service

```

التعليمة السابقة ستقوم بتفعيل واجهة LXDE كواجهة إفتراضية للنظام الحي .

## بناء ملف ISO

الآن انت جاهز لتحويل ملفاتك الى صورة قرص من صيغة ISO و من ثم حرقها على إسطوانة CD أو على USB , داخل المجلد الذي تعمل فيه سواءً كان ~/archlive/releng, أو ~/archlive/baseline قم بتنفيذ التعليمة التالية :

```
# ./build.sh -v

```

البرنامج النصي سيقوم الآن بتحميل و تنصيب الحزم التي قُمت بتحديدها , يقوم بإنشاء صور للنواة و init , و تطبيق تعديلاتك ومن ثم يقوم ببناء ملف ISO في مجلد out/

## استخدام ملف ISO

### CD

يمكنك حرق ملف ISO الى قرص cd , يمكنك إتباع دليل [CD Burning](/index.php/CD_Burning "CD Burning") كما تريد .

### USB

يمكنك نسخ ملف ISO الى قرص USB عن طريق تعليمة dd :

```
# dd if=~/archlive/releng/out/*.iso of=/dev/sdx

```

عليك تعديل التعليمة السابقة لكي توافق إحتياجاتك , لكن يجب التنبيه أن خطأ صغير في القسم الثاني من التعليمة يمكن أن يؤدي الى فقدان المعلومات في القرص الصلب

### grub4dos

الأداة grub4dos تسمح لك بإنشاء USB مُتعددة الإقلاع يمكنها الإقلاع من أكثرمن توزيعة linux على USB ذاتها .

لإقلاع القرص الحي الذي قمت بإنشاءه من USB تحوي على grub4dos مُنصب مسبقاً عليك وصل ملف iso الذي قمت بإنشاءه loop mount و من ثم تقوم بنسخ المجلد `/arch` بكافة محتوياته الى المجلد الرئيسي للـ USB . ثم تقوم بتعديل ملف `menu.lst` الخاص ببرنامج grub4dos و إضافة الأسطر التالية :

```
title Archlinux x86_64
kernel /arch/boot/x86_64/vmlinuz archisolabel=<your usb label>
initrd /arch/boot/x86_64/archiso.img

```

قم بتعديل x86_64 حسب المعمارية التي تستخدمها و قم بوضع اسم قرص USB الخاص بك عوضاً عن <your usb label> .

### التنصيب

Boot the created CD/DVD/USB. If you wish to install the Archiso you created **-as it is-**, there are several ways to do this, but either way we're following the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide") mostly.

If you don't have an internet connection on that PC, or if you don't want to download every packages you want again, follow the guide, and when you get to [Beginners' guide#Install_the_base_system](/index.php/Beginners%27_guide#Install_the_base_system "Beginners' guide"), instead of downloading, use this: [Full system backup with rsync](/index.php/Full_system_backup_with_rsync "Full system backup with rsync"). (more info here: [Talk:Archiso](/index.php/Talk:Archiso "Talk:Archiso"))

You can also try: [Archboot](/index.php/Archboot "Archboot"), GUI installer.

## See also

*   [Archiso project page](https://projects.archlinux.org/?p=archiso.git;a=summary)
*   [Archiso as pxe server](/index.php/Archiso_as_pxe_server "Archiso as pxe server")
*   [Step-by-step tutorial on using ArchISO](https://kroweer.wordpress.com/2011/09/07/creating-a-custom-arch-linux-live-usb)
*   [A live DJ distribution powered by ArchLinux and built with Archiso](http://didjix.blogspot.com/)