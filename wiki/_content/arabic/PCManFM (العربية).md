**PCManFM** "هو مدير ملفات سريع وخفيف ومليء بالميزات مع إمكانية فتح عدة تبويبات أثناء التصفح"، المصدر من [PCManFM on sourceforge](http://pcmanfm.sourceforge.net/)، وهو أيضاً مدير الملفات الافتراضي في [LXDE](/index.php/LXDE "LXDE") (بيئة سطح مكتب X11 خفيفة)

## Contents

*   [1 التثبيت](#.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA)
*   [2 التعامل مع المساحات التخزينية](#.D8.A7.D9.84.D8.AA.D8.B9.D8.A7.D9.85.D9.84_.D9.85.D8.B9_.D8.A7.D9.84.D9.85.D8.B3.D8.A7.D8.AD.D8.A7.D8.AA_.D8.A7.D9.84.D8.AA.D8.AE.D8.B2.D9.8A.D9.86.D9.8A.D8.A9)
    *   [2.1 الربط التلقائي لأجهزة تخزين USB الخارجية](#.D8.A7.D9.84.D8.B1.D8.A8.D8.B7_.D8.A7.D9.84.D8.AA.D9.84.D9.82.D8.A7.D8.A6.D9.8A_.D9.84.D8.A3.D8.AC.D9.87.D8.B2.D8.A9_.D8.AA.D8.AE.D8.B2.D9.8A.D9.86_USB_.D8.A7.D9.84.D8.AE.D8.A7.D8.B1.D8.AC.D9.8A.D8.A9)
    *   [2.2 الربط مع udisks](#.D8.A7.D9.84.D8.B1.D8.A8.D8.B7_.D9.85.D8.B9_udisks)
    *   [2.3 دعم القراءة والكتابة في أنظمة ملفات NTFS](#.D8.AF.D8.B9.D9.85_.D8.A7.D9.84.D9.82.D8.B1.D8.A7.D8.A1.D8.A9_.D9.88.D8.A7.D9.84.D9.83.D8.AA.D8.A7.D8.A8.D8.A9_.D9.81.D9.8A_.D8.A3.D9.86.D8.B8.D9.85.D8.A9_.D9.85.D9.84.D9.81.D8.A7.D8.AA_NTFS)
    *   [2.4 دعم الوصول إلى المحذوفات وتصفح الملفات التي تم مشاركتها على الشبكة والربط التلقائي مع gvfs](#.D8.AF.D8.B9.D9.85_.D8.A7.D9.84.D9.88.D8.B5.D9.88.D9.84_.D8.A5.D9.84.D9.89_.D8.A7.D9.84.D9.85.D8.AD.D8.B0.D9.88.D9.81.D8.A7.D8.AA_.D9.88.D8.AA.D8.B5.D9.81.D8.AD_.D8.A7.D9.84.D9.85.D9.84.D9.81.D8.A7.D8.AA_.D8.A7.D9.84.D8.AA.D9.8A_.D8.AA.D9.85_.D9.85.D8.B4.D8.A7.D8.B1.D9.83.D8.AA.D9.87.D8.A7_.D8.B9.D9.84.D9.89_.D8.A7.D9.84.D8.B4.D8.A8.D9.83.D8.A9_.D9.88.D8.A7.D9.84.D8.B1.D8.A8.D8.B7_.D8.A7.D9.84.D8.AA.D9.84.D9.82.D8.A7.D8.A6.D9.8A_.D9.85.D8.B9_gvfs)
*   [3 تلميحات](#.D8.AA.D9.84.D9.85.D9.8A.D8.AD.D8.A7.D8.AA)
    *   [3.1 نقرة واحدة لفتح الملفات و المجلدات](#.D9.86.D9.82.D8.B1.D8.A9_.D9.88.D8.A7.D8.AD.D8.AF.D8.A9_.D9.84.D9.81.D8.AA.D8.AD_.D8.A7.D9.84.D9.85.D9.84.D9.81.D8.A7.D8.AA_.D9.88_.D8.A7.D9.84.D9.85.D8.AC.D9.84.D8.AF.D8.A7.D8.AA)
*   [4 استكشاف الأخطاء وإصلاحها](#.D8.A7.D8.B3.D8.AA.D9.83.D8.B4.D8.A7.D9.81_.D8.A7.D9.84.D8.A3.D8.AE.D8.B7.D8.A7.D8.A1_.D9.88.D8.A5.D8.B5.D9.84.D8.A7.D8.AD.D9.87.D8.A7)
    *   [4.1 لا توجد "تطبيقات"](#.D9.84.D8.A7_.D8.AA.D9.88.D8.AC.D8.AF_.22.D8.AA.D8.B7.D8.A8.D9.8A.D9.82.D8.A7.D8.AA.22)
    *   [4.2 لا تظهر الأيقونات؟](#.D9.84.D8.A7_.D8.AA.D8.B8.D9.87.D8.B1_.D8.A7.D9.84.D8.A3.D9.8A.D9.82.D9.88.D9.86.D8.A7.D8.AA.D8.9F)
    *   [4.3 نافذة "البحث" تظهر بدلاً من فتح المجلد](#.D9.86.D8.A7.D9.81.D8.B0.D8.A9_.22.D8.A7.D9.84.D8.A8.D8.AD.D8.AB.22_.D8.AA.D8.B8.D9.87.D8.B1_.D8.A8.D8.AF.D9.84.D8.A7.D9.8B_.D9.85.D9.86_.D9.81.D8.AA.D8.AD_.D8.A7.D9.84.D9.85.D8.AC.D9.84.D8.AF)
    *   [4.4 الرجوع إلى الخلف أو الأمام لا يعمل باسخدام أزرار الفأرة](#.D8.A7.D9.84.D8.B1.D8.AC.D9.88.D8.B9_.D8.A5.D9.84.D9.89_.D8.A7.D9.84.D8.AE.D9.84.D9.81_.D8.A3.D9.88_.D8.A7.D9.84.D8.A3.D9.85.D8.A7.D9.85_.D9.84.D8.A7_.D9.8A.D8.B9.D9.85.D9.84_.D8.A8.D8.A7.D8.B3.D8.AE.D8.AF.D8.A7.D9.85_.D8.A3.D8.B2.D8.B1.D8.A7.D8.B1_.D8.A7.D9.84.D9.81.D8.A3.D8.B1.D8.A9)
    *   [4.5 معاملات --desktop لا تعمل أو تُعطِل X-server](#.D9.85.D8.B9.D8.A7.D9.85.D9.84.D8.A7.D8.AA_--desktop_.D9.84.D8.A7_.D8.AA.D8.B9.D9.85.D9.84_.D8.A3.D9.88_.D8.AA.D9.8F.D8.B9.D8.B7.D9.90.D9.84_X-server)
    *   [4.6 إعدادات التهيئة المتقدمة لمحاكي الطرفية لا يمكن حفظها](#.D8.A5.D8.B9.D8.AF.D8.A7.D8.AF.D8.A7.D8.AA_.D8.A7.D9.84.D8.AA.D9.87.D9.8A.D8.A6.D8.A9_.D8.A7.D9.84.D9.85.D8.AA.D9.82.D8.AF.D9.85.D8.A9_.D9.84.D9.85.D8.AD.D8.A7.D9.83.D9.8A_.D8.A7.D9.84.D8.B7.D8.B1.D9.81.D9.8A.D8.A9_.D9.84.D8.A7_.D9.8A.D9.85.D9.83.D9.86_.D8.AD.D9.81.D8.B8.D9.87.D8.A7)
    *   [4.7 جعل PCManFM يتذكر إعدادك المفضل لفرز الملفات](#.D8.AC.D8.B9.D9.84_PCManFM_.D9.8A.D8.AA.D8.B0.D9.83.D8.B1_.D8.A5.D8.B9.D8.AF.D8.A7.D8.AF.D9.83_.D8.A7.D9.84.D9.85.D9.81.D8.B6.D9.84_.D9.84.D9.81.D8.B1.D8.B2_.D8.A7.D9.84.D9.85.D9.84.D9.81.D8.A7.D8.AA)
    *   [4.8 أخطاء "لا تملك تصريح" عند الدخول أو تحميل أقراص تخزين USB](#.D8.A3.D8.AE.D8.B7.D8.A7.D8.A1_.22.D9.84.D8.A7_.D8.AA.D9.85.D9.84.D9.83_.D8.AA.D8.B5.D8.B1.D9.8A.D8.AD.22_.D8.B9.D9.86.D8.AF_.D8.A7.D9.84.D8.AF.D8.AE.D9.88.D9.84_.D8.A3.D9.88_.D8.AA.D8.AD.D9.85.D9.8A.D9.84_.D8.A3.D9.82.D8.B1.D8.A7.D8.B5_.D8.AA.D8.AE.D8.B2.D9.8A.D9.86_USB)

## التثبيت

مدير الملفات [pcmanfm](https://www.archlinux.org/packages/?name=pcmanfm) متوفر في [المستودعات الرسمية](/index.php/Official_repositories "Official repositories").

ستحتاج إلى [gamin](/index.php/Gamin "Gamin") (بديل عن [FAM](/index.php/FAM "FAM") والذي يحتاج إلى daemon) لاختيار أحداث مثل تغيير المجلدات أو الملفات.

## التعامل مع المساحات التخزينية

يستطيع PCManFM ربط أو إلغاء ربط أقراص التخزين بشكل تلقائي أو حين الطلب منه، هذه الميزة تعتبر بديل عن أدوات CLI مثل الأداة [pmount](https://aur.archlinux.org/packages/pmount/).

### الربط التلقائي لأجهزة تخزين USB الخارجية

لجعل أجهزة تخزين USB الخارجية تُربط تلقائياً قم بتثبيت [gvfs](https://www.archlinux.org/packages/?name=gvfs).

إذا لم يتم ربطها تلقائياً قم بإعادة تشغيل النظام.

### الربط مع udisks

الإصدار الحالي من PCManFM قادر على التعامل مع المساحات التخزينية من خلال udisks، إذا كنت ترغب باستعمال هذه الميزة تأكد من أن D-Bus daemon مثبت وقيد التشغيل أولاً، قم بالاطلاع على صفحة [D-Bus](/index.php/D-Bus "D-Bus") للمزيد من التفاصيل.

### دعم القراءة والكتابة في أنظمة ملفات NTFS

قم بتثبيت [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) (اطلع على [NTFS-3G](/index.php/NTFS-3G "NTFS-3G")).

### دعم الوصول إلى المحذوفات وتصفح الملفات التي تم مشاركتها على الشبكة والربط التلقائي مع gvfs

لحل مشكلة "العملية غير مدعومة" Operation not supporte عند الضغط على أيقونة المحذوفات يجب عليك القيام بالخطوات التالية:

1\. قم بتثبيت حزمة gvfs 2\. قم بتشغيل PCManFM باسخدام الأمر التالي حصراً: pcmanfm

لتصفح الملفات التي تم مشاركتها على الشبكة:

1\. قم بتثبيت الحزم gvfs gvfs-smb gvfs-afp 2\. قم بتشغيل PCManFM عن طريق الأمر التالي حصراً: pcmanfm 3\. قم بكتابة smb://<اسم المُخدم>/<الاسم التشاركي> للدخول إلى الملفات المُشاركة من قبل Windows أو CIFS أو Samba 4\. قم بكتابة afp://<اسم المُخدم>/<الاسم التشاركي> للملفات المشاركة من قبل AFP

## تلميحات

### نقرة واحدة لفتح الملفات و المجلدات

شغل PCManFM بوضع مستكشف الملفات ثم اذهب إلى *قائمة تحريرEdit* ثم *تفضيلاتPreferences* ثم من *قائمة عامGeneral* اختر *المظهرBehavior* ثم قم بتحديد خيار *افتح الملفات* بنقرة بسيطةOpen files with a simple click

**ملاحظة:** هذا الخيار يعمل أيضاً في pcmanfm --desktop

## استكشاف الأخطاء وإصلاحها

### لا توجد "تطبيقات"

في البداية قم بتثبيت [gnome-menus](https://www.archlinux.org/packages/?name=gnome-menus). ثم يمكنك تجريب هذه الطريقة: امسح كل الملفات في المسار $HOME/.cache/menus ثم قم بإعادة تشغيل PCManFM مجددا.

PCManFM يحتاج لإعداد متغيرات البيئة "XDG_MENU_PREFIX"، قيمة المتغير يجب أن تتطابق مع بداية الملف الموجود في "/etc/xdg/menus/" في حال أنك قمت بتثبيت حزمة "gnome-menus" تستطيع تعيين القيمة في الملف .xinitrc بالسطر التالي:

```
$ export XDG_MENU_PREFIX=gnome-

```

اطلع على هذه المواضيع لمزيد من المعلومات: [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1110903) وخاصة هذا المقال في منتديات Linux Mint [[2]](http://forums.linuxmint.com/viewtopic.php?f=175&t=53986#p501920)

### لا تظهر الأيقونات؟

إذا كنت تستعمل مدير نوافذ [WM](/index.php/WM "WM") بدلاً من بيئة سطح مكتب [DE](/index.php/DE "DE") ولا تظهر أيقونات الملفات أو المجلدات فقم بتحديد أحد سمات أيقونات gtk.

قم بتحرير `~/.gtkrc-2.0` أو **`/etc/gtk-2.0/gtkrc` بإضافة السطر التالي**:

```
gtk-icon-theme-name = "oxygen"

```

**ملاحظة:** لكي يتم تطبيق التغييرات يجب إعادة تشغيل PCManFM وجميع تبويباته المفتوحة
.

إذا لم تكن حزمة [oxygen-icons](https://www.archlinux.org/packages/?name=oxygen-icons) مثبتة لديك، فاستخدم أي حزمة أخرى (**gnome**, **hicolor** أما **locolor** فإنها لا تعمل)، لعرض قائمة بجميع حزم الأيقونات المثبتة نفذ:

```
ls ~/.icons /usr/share/icons/

```

إذا لم تناسبك الحزم المثبتة لديك قم بتثبيت واحدة، لعرض قائمة بجميع حزم الأيقونات القابلة للتثبيت نفذ التالي:

```
$ pacman -Ss icon-theme

```

**Tip:** إذا كنت ترغب باستعمال واجهة رسومية لاختيار سمات الأيقونات بدلاً من الطرفية قم بتثبيت [lxappearance](https://www.archlinux.org/packages/?name=lxappearance).

### نافذة "البحث" تظهر بدلاً من فتح المجلد

قم بحذف أو إعادة تسمية الملف `/usr/share/applications/pcmanfm-find.desktop` ، إذا كنت تشغل pcmanfm-mod من مستودعات AUR قم بحذف أو إعادة تسمية الملف `/usr/share/applications/pcmanfm-mod-find.desktop`.

### الرجوع إلى الخلف أو الأمام لا يعمل باسخدام أزرار الفأرة

إحدى الطرق لإصلاح هذه المشكلة هي [Xbindkeys](/index.php/Xbindkeys "Xbindkeys")

قم بتثبيت [xbindkeys](https://www.archlinux.org/packages/?name=xbindkeys) ثم حرر ~/.xbindkeysrc ليصبح متضمناً على:

```
# Sample .xbindkeysrc for a G9x mouse.
"/usr/bin/xvkbd -text '\[Alt_L]\[Left]'"
 b:8
"/usr/bin/xvkbd -text '\[Alt_L]\[Right]'"
 b:9

```

يمكن الحصول على الكودات الخاصة بالزر الفعلي من الحزمة [xorg-xev](https://www.archlinux.org/packages/?name=xorg-xev)

قم بإضافة الكود التالي للملف `~/.xinitrc` لكي يتم تشغيل xbindkeys عند تسجيل الدخول مباشرة:

```
xbindkeys &

```

### معاملات --desktop لا تعمل أو تُعطِل X-server

قم بالتأكد من أن لديك ملكية وصلاحية الكتابة في الملف `~/.config/pcmanfm`، وضع خلفية للشاشة باستعمال المُعامل *--desktop-pref* أو بتعديل `~/.config/pcmanfm/default/pcmanfm.config` سيحل المشكلة.

### إعدادات التهيئة المتقدمة لمحاكي الطرفية لا يمكن حفظها

قم بالتأكد من أنك تملك صلاحيات لاستخدام ملف التهيئة libfm:

```
$ chmod -R 755 ~/.config/libfm
$ chmod 777 ~/.config/libfm/libfm.conf

```

### جعل PCManFM يتذكر إعدادك المفضل لفرز الملفات

يمكنك الذهاب إلى *قائمة عرض* View ثم *فرز الملفات* Sort Files للتغيير من طريقة ترتيب الملفات، لكن PCManFM لن يتذكر هذا التغيير في المرة المقبلة التي تقوم بالدخول فيها إليه، ولجعله يتذكر اذهب إلى *قائمة تحرير* Edit ثم *تفضيلات* Preferences ومن ثم إغلاق، هذه العملية ستقوم بكتابة طريقة الفرز sort_type الحالية وقيم الفرز تبعاً sort_by إلى الملف `~/.config/pcmanfm/LXDE/pcmanfm.conf`.

### أخطاء "لا تملك تصريح" عند الدخول أو تحميل أقراص تخزين USB

في كثير من مديري النوافذ WM (وعند استخدام [PolicyKit](/index.php/PolicyKit#Mounting_USB_drives "PolicyKit")) ستواجهك مشكلة "لا تملك تصريح" Not authorized عند محاولة فتح قرص تخزين USB على سبيل المثال. قم بإنشاء الملف (بالإضافة إلى مؤثرات الدليل أو المجلد والتي لا تكون موجودة بشكل افتراضي هنا) `/etc/polkit-1/actions/org.freedesktop.udisks2.pkla` إذا لم يكن موجوداً واجعله يحتوي على التالي:

```
[Storage Permissions]
Identity=unix-group:storage
Action=org.freedesktop.udisks2.filesystem-mount;org.freedesktop.udisks2.modify-device
ResultAny=yes
ResultInactive=yes
ResultActive=yes

```