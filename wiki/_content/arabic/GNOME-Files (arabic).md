Related articles

*   [بيئة سطح المكتب لجنوم تشمل ناتوليس](/index.php/Desktop_environment "Desktop environment")
*   [Xfce4's مدير ملفات افتراضي.](/index.php/Xfce4 "Xfce4")

[نوتيلس](http://live.gnome.org/Nautilus) هو مدير الملفات الافتراضي لواجهة [غنوم](https://live.gnome.org/)، [من موقع غنوم على الإنترنت](http://library.gnome.org/users/user-guide/stable/gosnautilus-22.html.en): *مدير الملفات "نوتيلس" يقدم طريقة بسيطة ومتكاملة لإدارة ملفاتك وتطبيقاتك، يمكنك استخدام "نوتيلس" للقيام بالأمور التالية:*

*   إنشاء مجلدات ومستندات
*   عرض ملفاتك ومجلداتك
*   البحث عن ملفاتك وإدارتها
*   تشغيل السكربتات أو التطبيقات
*   تخصيص مظهر الملفات والمجلدات
*   الوصول إلى مواقع خاصة داخل حاسوبك
*   كتابة البيانات على CD أو DVD
*   تثبيت أو إزالة الخطوط

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 التثبيت](#التثبيت)
*   [2 الإعداد](#الإعداد)
*   [3 إدارة سطح المكتب](#إدارة_سطح_المكتب)
    *   [3.1 إزالة المجلدات من الشريط الجانبي](#إزالة_المجلدات_من_الشريط_الجانبي)
    *   [3.2 دائماً اعرض وضع الإدخال النصي في شريط الأماكن](#دائماً_اعرض_وضع_الإدخال_النصي_في_شريط_الأماكن)
    *   [3.3 الإضافات](#الإضافات)
    *   [3.4 إنشاء مستند فارغ في نوتيلس 3.6](#إنشاء_مستند_فارغ_في_نوتيلس_3.6)
    *   [3.5 نقل الملفات إلى المحذوفات باستخدام زر delete في نوتيلس 3.6](#نقل_الملفات_إلى_المحذوفات_باستخدام_زر_delete_في_نوتيلس_3.6)
*   [4 استكشاف الأخطاء وإصلاحها](#استكشاف_الأخطاء_وإصلاحها)
    *   [4.1 نوتيلس لا يستطيع تصفح الملفات المُشاركة على شبكة ويندوز](#نوتيلس_لا_يستطيع_تصفح_الملفات_المُشاركة_على_شبكة_ويندوز)
    *   [4.2 نوتيلس لا يستطيع تصفح الملفات المُشاركة على شبكة آبل](#نوتيلس_لا_يستطيع_تصفح_الملفات_المُشاركة_على_شبكة_آبل)
    *   [4.3 لم يعُد نوتيلس مدير الملفات الافتراضي](#لم_يعُد_نوتيلس_مدير_الملفات_الافتراضي)

## التثبيت

قم [بتثبيت](/index.php/Pacman "Pacman") [nautilus](https://www.archlinux.org/packages/?name=nautilus) من [المستودعات الرسمية](/index.php/Official_repositories "Official repositories").

**ملاحظة:** نوتيلس لا يحتاج إلى كل محتويات حزمة [gnome-desktop](https://www.archlinux.org/packages/?name=gnome-desktop)، البعض سيجد هذا جيداً لأن حزمة [gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell) أعقد قليلاً من أن تكون عملية تثبيت.

"نوتيلس" جزء من مجموعة [gnome](https://www.archlinux.org/groups/x86_64/gnome/).

## الإعداد

إعداد مدير الملفات "نوتيلس" عبر الواجهة الرسومية سهل، ولكن لا يمكن أن تتحكم بكل الخيارات المتوفرة من قائمة التفضيلات في "نوتيلس" فقط، المزيد من الخيارات موجودة في *dconf-editor* تحت `org.gnome.nautilus`

## إدارة سطح المكتب

لم يعد "نوتيلس" بشكل افتراضي قادراً على التحكم بسطح المكتب في واجهة غنوم كما كان في السابق، فإذا كنت من محبي وضع الأيقونات على سطح المكتب أو كنت تستمتع بمستطيل التحديد الأنيق الذي يظهر بالنقر والسحب على سطح المكتب في أوقات الملل فيمكنك بسهولة أن تُعِد "نوتيلس" للقيام بهذه الأمور.

قم بتثبيت حزمة [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool) ومن ثم قم بتشغيلها، اذهب إلى قائمة "سطح المكتب" وقم بتفعيل خيار "تمكين مدير الملفات من التعامل مع سطح المكتب"، قد تحتاج إلى إعادة تشغيل "نوتيلس" عن طريق كتابة الأمر `killall nautilus; nautilus` في الطرفية أو إذا كنت تعمل على [GNOME](/index.php/GNOME "GNOME") فقم بالضغط على `ALT+F2` ومن ثم اكتب `r` واضغط على `Enter`

### إزالة المجلدات من الشريط الجانبي

المجلدات المعروضة في الشريط الجانبي تجدها محددة في المسار `~/.config/user-dirs.dirs` ويمكن تغييرها باستخدام أي محرر نصوص، تنفيذ `xdg-user-dirs-update` في الطرفية سيُحدث المجلدات التي سيتم عرضها في الشريط الجانبي، وبالتالي قد يكون من المستحسن أن يتم إعطاء صلاحيات القراءة فقط للملف.

### دائماً اعرض وضع الإدخال النصي في شريط الأماكن

في الحالة المعيارية فإن شريط أدوات "نوتيلس" ولعرض المسار أو الدليل للمجلدات فإنه يكون على وضع "شريط الأزرار"، للتنقل بين المجلدات والمسارات باستخدام الإدخال النصي عن طريق *لوحة المفاتيح* عوضاً عن شريط الأزرار قم بالضغط على `Ctrl+l`

لجعل وضع الإدخال النصي يُعرض بشكل دائم قم باستخدام gsettings كما هو موضح:

```
$ gsettings set org.gnome.nautilus.preferences always-use-location-entry true

```

**ملاحظة:** لن تستطيع عرض شريط الأزرار بعد أن تقوم بالتغيير السابق، لجعل وضعي العرض (شريط الأزرار أو الإدخال النصي) مفعلين يجب وضع قيمة التغيير السابق على **false**.

### الإضافات

بعض البرامج تستطيع أن تُثري "نوتيلس" بمزيد من الإضافات، هذه بعض الحزم المتواجدة في المستودعات الرسمية التي تفعل ذلك:

*   **Nautilus Actions** — تقوم بإعداد البرامج التي يجب أن تعمل عند تحديد الملفات في نوتيلس

	[http://gnome.org](http://gnome.org) || [nautilus-actions](https://www.archlinux.org/packages/?name=nautilus-actions)

*   **Open in Terminal** — إضافة لنوتيلس تقوم بفتح الطرفية في نفس مسار المجلد الحالي

	[http://ftp.gnome.org/pub/GNOME/sources/nautilus-open-terminal](http://ftp.gnome.org/pub/GNOME/sources/nautilus-open-terminal) || [nautilus-open-terminal](https://www.archlinux.org/packages/?name=nautilus-open-terminal)

*   **Send to Menu** — قائمة نوتيلس لإرسال الملفات

	[http://download.gnome.org/sources/nautilus-sendto/](http://download.gnome.org/sources/nautilus-sendto/) || [nautilus-sendto](https://www.archlinux.org/packages/?name=nautilus-sendto)

*   **Sound Converter** — إضافة لتحويل صيغ الملفات الصوتية

	[http://code.google.com/p/nautilus-sound-converter/](http://code.google.com/p/nautilus-sound-converter/) || [nautilus-sound-converter](https://aur.archlinux.org/packages/nautilus-sound-converter/)

*   **seahorse-nautilus** — تشفير وتوقيع PGP لنوتيلس

	[http://git.gnome.org/browse/seahorse-nautilus/](http://git.gnome.org/browse/seahorse-nautilus/) || [seahorse-nautilus](https://www.archlinux.org/packages/?name=seahorse-nautilus)

### إنشاء مستند فارغ في نوتيلس 3.6

واجهة "غنوم" 3.6 أتت بتغيرات على "نوتيلس"، بعض الميزات قللت من سهولة صيانة "نوتيلس"، فخيار إنشاء مستند فارغ تمت إزالته من القائمة الافتراضية في "نوتيلس"، يجب على المستخدم أن يُنشأ مجلداً اسمه `~/Templates/` في المجلد المحلي home ومن ثم إنشاء ملف فارغ في نفس المجلد باستخدام الطرفية عن طريق الأمر `touch ~/Templates/new` أو إنشاء الملف الفارغ باستخدام مدير ملفات آخر، قم بإعادة تشغيل "نوتيلس" لاستعادة خيار إنشاء مستند فارغ من القائمة الافتراضية.

### نقل الملفات إلى المحذوفات باستخدام زر delete في نوتيلس 3.6

لم يعد "نوتيلس" ينقل الملفات إلى سلة المحذوفات عند الضغط على زر delete بعد الآن، إذا كنت ترغب باستعادة هذه الميزة فقم ببعض التعديلات على `~/.config/nautilus/accels` :

```
- ; (gtk_accel_path "<Actions>/DirViewActions/Trash" "<Primary>Delete")
+ (gtk_accel_path "<Actions>/DirViewActions/Trash" "Delete")

```

## استكشاف الأخطاء وإصلاحها

### نوتيلس لا يستطيع تصفح الملفات المُشاركة على شبكة ويندوز

"نوتيلس" يعتمد على حزمة [gvfs-smb](https://www.archlinux.org/packages/?name=gvfs-smb) للقيام بهذا العمل، يمكن [تثبيت](/index.php/Pacman "Pacman") الحزمة من [المستودعات الرسمية](/index.php/Official_repositories "Official repositories")

### نوتيلس لا يستطيع تصفح الملفات المُشاركة على شبكة آبل

"نوتيلس" يعتمد على حزمة [gvfs-afp](https://www.archlinux.org/packages/?name=gvfs-afp) وحزمة [avahi](https://www.archlinux.org/packages/?name=avahi) للقيام بهذا العمل، يمكن [تثبيت](/index.php/Pacman "Pacman") الحزمتان من [المستودعات الرسمية](/index.php/Official_repositories "Official repositories")،لاحظ أنه بالإضافة إلى [Avahi](/index.php/Avahi "Avahi") يجب تشغيل الحزم أيضاً باستخدام التالي:

 `systemctl start avahi-daemon` 

و\أو

 `systemctl enable avahi-daemon` 

### لم يعُد نوتيلس مدير الملفات الافتراضي

إذا رفضت بعض البرامج مثل firefox أن تعتبر "نوتيلس" مديراً افتراضياً للملفات، فيمكن حل هذه المشكلة بإضافة السطر التالي تحت قسم [البرامج الافتراضية] في `~/.local/share/applications/mimeapps.list` :

```
inode/directory=nautilus.desktop

```