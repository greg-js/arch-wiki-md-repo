## Contents

*   [1 محمل الإقلاع Bootloader](#.D9.85.D8.AD.D9.85.D9.84_.D8.A7.D9.84.D8.A5.D9.82.D9.84.D8.A7.D8.B9_Bootloader)
*   [2 النواة](#.D8.A7.D9.84.D9.86.D9.88.D8.A7.D8.A9)
*   [3 نظام ملفات الذاكرة الابتدائي initramfs](#.D9.86.D8.B8.D8.A7.D9.85_.D9.85.D9.84.D9.81.D8.A7.D8.AA_.D8.A7.D9.84.D8.B0.D8.A7.D9.83.D8.B1.D8.A9_.D8.A7.D9.84.D8.A7.D8.A8.D8.AA.D8.AF.D8.A7.D8.A6.D9.8A_initramfs)
*   [4 Init process العملية الأم](#Init_process_.D8.A7.D9.84.D8.B9.D9.85.D9.84.D9.8A.D8.A9_.D8.A7.D9.84.D8.A3.D9.85)
*   [5 انظر أيضًا](#.D8.A7.D9.86.D8.B8.D8.B1_.D8.A3.D9.8A.D8.B6.D9.8B.D8.A7)

## محمل الإقلاع Bootloader

بعدما يتم تشغيل الجهاز و يتم إجراء إختبارات ما بعد الإقلاع [POST](https://en.wikipedia.org/wiki/Power-on_self-test "wikipedia:Power-on self-test") , يقوم BIOS يتحديد وسيط التخزين الإقلاعي و يقوم بنقل السلطة الى القطاع الرئيس للإقلاع لهذا الوسيط . في أجهزة GNU/Linux يتم تحميل محمل الإقلاع من سجل الإقلاع الرئيس [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record") لذالك الوسيط ويكون عادةً إما [GRUB](/index.php/GRUB "GRUB") أو [LILO](/index.php/LILO "LILO") , مُحمل الإقلاع يوفر للمستخدم عدد من الخيارات لإتمام عملية الإقلاع . فعلى سبيل المثال عندما يتم تحديد Arch Linux على [محمل إقلاع ثنائي](/index.php/Windows_and_Arch_Dual_Boot "Windows and Arch Dual Boot") يتوفر عليه Arch Linux و نظام windows ; فسيقوم مُحمل الإقلاع بتحميل النواة (`vmlinuz-linux`) وتهيئة صورة نظام الملفات الوهمي (`initramfs-linux.img`) الى الذاكرة ثم يقوم ببدء النواة , ممرراً عنوان الذاكرة الخاص بصورة نظام الملفات الى النواة .

## النواة

النواة هي قلب نظام التشغيل . وتعمل وظائفها في المستوى الأدنى (_kernelspace_) لتقوم بالربط فيما بين عتاد الجهاز والبرامج التي تستخدم ذلك العتاد فتشغله . لاستخدام أمثل للمعالج , تقوم النواة باستخدام الجدولة لكي تُحدد أي من المهام ستأخذ الأولوية في أي لحظة , مما يُعطي الإنطباع أن المهام تُنفذ في آن واحد .

## نظام ملفات الذاكرة الابتدائي initramfs

بعد أن يتم تحميل النواة الى الذاكرة , تقوم النواة بفك ضغط [initramfs](/index.php/Initramfs "Initramfs") (اختصار للعبارة Initial RAM filesystem) الذي يُصبح نظام تشغيل الملفات الإبتدائي للمجلد الجذر , وبعد ذلك تقوم النواة بتنفيذ`/init` كأول عملية . بعد ذلك تبدأ مرحلة فضاءالمستخدم _early userspace_ .

الهدف من initramfs هو هو إقلاع بدائي للنظام لكي يصل الى نقطة تُمكنه من الوصول الى نظام ملفات الجذر . وهذا يعني أن أيّ من ( انظر [FHS](/index.php/FHS "FHS") لمزيد من التفاصيل) .المطلوبة وهذا يعني أن أيّا من الوحدات المتطلبة لتشغيل الأقراص كأقراص IDE, SCSI, SATA, USB/FW (إذا كان الإقلاع من قرص خارجي) يجب أن يتم تحميلها من initramfs إذا لم تكن تلك الواحدات مبنية داخل النواة . بمجرد أن يتم تحميل الواحدات المطلوبة (إما بشكل مقصود عن طريق برنامج أو بشكل تلقائي عن طريق [udev](/index.php/Udev "Udev") لهذا السبب ؛ يحتاج initramfs أن يحتوي فقط على الواحدات المطلوبة للوصول الى نظام الملفات الجذر وليس من الضروري أن تحتوي على جميع الواحدات التي يمكن استخدامها من قبل النظام , لأن الأغلبية من الواحدات سيتم تحميلها الى الذاكرة لاحقاً بواسطة udev خلال عملية init

## Init process العملية الأم

في المرحلة الأخيرة من فضاء المستخدم سيتم وصل قرص نظام ملفات الجذر ويستبدل مكان نظام الملفات الأولي . سيتم تنفيذ العملية `/sbin/init` مُستبدلةً العملية الأم `/init` .

في السابق كانت توزيعة Arch تستخدم SysVinit كعملية init إفتراضية , لكن في الإصدارات الجديدة من Arch أصبحت تستخدم [systemd](/index.php/Systemd "Systemd") إفتراضياً . لذا فينصح جميع مستخدمي [SysVinit](/index.php/SysVinit "SysVinit") الإنتقال الى [systemd](/index.php/Systemd "Systemd") .

## انظر أيضًا

*   [Early Userspace in Arch Linux](http://archlinux.me/brain0/2010/02/13/early-userspace-in-arch-linux/)
*   [Inside the Linux boot process](http://www.ibm.com/developerworks/linux/library/l-linuxboot/)
*   [Boot with GRUB](http://www.linuxjournal.com/article/4622)
*   [Wikipedia:Linux startup process](https://en.wikipedia.org/wiki/Linux_startup_process "wikipedia:Linux startup process")
*   [Wikipedia:initrd](https://en.wikipedia.org/wiki/initrd "wikipedia:initrd")
*   [Boot Linux Grub Into Single User Mode](http://www.cyberciti.biz/faq/grub-boot-into-single-user-mode/)