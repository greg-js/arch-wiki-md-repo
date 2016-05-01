| **ملخص**  |
| هذه المقالة تناقش مدير الملفات ثونَر [Thunar](http://thunar.xfce.org/index.html) من جميع الجوانب. |
| **مواضيع متصلة** |
| [Xfce](/index.php/Xfce "Xfce"): يتم تثبيت ثونَر مع تثبيت [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/). |
| [Nautilus](/index.php/GNOME#Nautilus "GNOME"): ثونَر ليس مدير الملفات الوحيد فهناك الكثير منهم، على سبيل المثال هناك نُوتيلُس وهو مدير الملفات في [gnome](https://www.archlinux.org/groups/x86_64/gnome/). |

**ثونَر** [Thunar](http://thunar.xfce.org/index.html) عبارة عن مدير ملفات صمم ليكون سريعاً خفيفاً وسهل الاستخدام، يمكن تثبيته منفصلاً أو ضمن حزمة [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/).

## Contents

*   [1 التثبيت](#.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA)
*   [2 الربط التلقائي لوسائط التخزين](#.D8.A7.D9.84.D8.B1.D8.A8.D8.B7_.D8.A7.D9.84.D8.AA.D9.84.D9.82.D8.A7.D8.A6.D9.8A_.D9.84.D9.88.D8.B3.D8.A7.D8.A6.D8.B7_.D8.A7.D9.84.D8.AA.D8.AE.D8.B2.D9.8A.D9.86)
*   [3 مدير أقراص التخزين في ثونَر](#.D9.85.D8.AF.D9.8A.D8.B1_.D8.A3.D9.82.D8.B1.D8.A7.D8.B5_.D8.A7.D9.84.D8.AA.D8.AE.D8.B2.D9.8A.D9.86_.D9.81.D9.8A_.D8.AB.D9.88.D9.86.D9.8E.D8.B1)
    *   [3.1 التثبيت](#.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_2)
    *   [3.2 التهيئة](#.D8.A7.D9.84.D8.AA.D9.87.D9.8A.D8.A6.D8.A9)
*   [4 تلميحات وحِيَل](#.D8.AA.D9.84.D9.85.D9.8A.D8.AD.D8.A7.D8.AA_.D9.88.D8.AD.D9.90.D9.8A.D9.8E.D9.84)
    *   [4.1 استخدام ثونَر لاستعراض الأماكن البعيدة](#.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_.D8.AB.D9.88.D9.86.D9.8E.D8.B1_.D9.84.D8.A7.D8.B3.D8.AA.D8.B9.D8.B1.D8.A7.D8.B6_.D8.A7.D9.84.D8.A3.D9.85.D8.A7.D9.83.D9.86_.D8.A7.D9.84.D8.A8.D8.B9.D9.8A.D8.AF.D8.A9)
        *   [4.1.1 التشغيل في الوضع المخفي](#.D8.A7.D9.84.D8.AA.D8.B4.D8.BA.D9.8A.D9.84_.D9.81.D9.8A_.D8.A7.D9.84.D9.88.D8.B6.D8.B9_.D8.A7.D9.84.D9.85.D8.AE.D9.81.D9.8A)
    *   [4.2 ضبط سمة الأيقونات](#.D8.B6.D8.A8.D8.B7_.D8.B3.D9.85.D8.A9_.D8.A7.D9.84.D8.A3.D9.8A.D9.82.D9.88.D9.86.D8.A7.D8.AA)
    *   [4.3 حل مشكلة البطء والجمود أثناء التشغيل](#.D8.AD.D9.84_.D9.85.D8.B4.D9.83.D9.84.D8.A9_.D8.A7.D9.84.D8.A8.D8.B7.D8.A1_.D9.88.D8.A7.D9.84.D8.AC.D9.85.D9.88.D8.AF_.D8.A3.D8.AB.D9.86.D8.A7.D8.A1_.D8.A7.D9.84.D8.AA.D8.B4.D8.BA.D9.8A.D9.84)
*   [5 إضافات وملحقات أخرى](#.D8.A5.D8.B6.D8.A7.D9.81.D8.A7.D8.AA_.D9.88.D9.85.D9.84.D8.AD.D9.82.D8.A7.D8.AA_.D8.A3.D8.AE.D8.B1.D9.89)
    *   [5.1 Thunar Archive Plugin](#Thunar_Archive_Plugin)
    *   [5.2 Thunar Media Tags Plugin](#Thunar_Media_Tags_Plugin)
    *   [5.3 Thunar thumbnails](#Thunar_thumbnails)
    *   [5.4 Thunar Shares](#Thunar_Shares)
*   [6 إجراءات مخصصة](#.D8.A5.D8.AC.D8.B1.D8.A7.D8.A1.D8.A7.D8.AA_.D9.85.D8.AE.D8.B5.D8.B5.D8.A9)
    *   [6.1 البحث عن الفيروسات](#.D8.A7.D9.84.D8.A8.D8.AD.D8.AB_.D8.B9.D9.86_.D8.A7.D9.84.D9.81.D9.8A.D8.B1.D9.88.D8.B3.D8.A7.D8.AA)
    *   [6.2 الربط مع Dropbox](#.D8.A7.D9.84.D8.B1.D8.A8.D8.B7_.D9.85.D8.B9_Dropbox)
*   [7 روابط ومراجع](#.D8.B1.D9.88.D8.A7.D8.A8.D8.B7_.D9.88.D9.85.D8.B1.D8.A7.D8.AC.D8.B9)

## التثبيت

قم بتثبيت حزمة [thunar](https://www.archlinux.org/packages/?name=thunar) من [المستودعات الرسمية](/index.php/Official_repositories "Official repositories") أما إذا كنت تعمل على واجهة [Xfce4](/index.php/Xfce "Xfce") فعلى الأرجح سيكون ثونَر مثبتاً لديك.

## الربط التلقائي لوسائط التخزين

يقوم ثونَر باستخدام [gvfs](/index.php/Gvfs "Gvfs") من أجل ربط وسائط التخزين بمجرد وصلها بالحاسب، اطلع على [GVFS](/index.php/GVFS "GVFS") لمعرفة تفاصيل حول كيفية عملها.

## مدير أقراص التخزين في ثونَر

على الرغم من أن ثونَر يدعم الربط والفصل التلقائيَّين لوسائط التخزين إلا أن مدير أقراص التخزين في ثونَر يقدم وظائف موسعة أكثر مثل تنفيذ أمر بشكل تلقائي أو فتح ثونَر تلقائياً بمجرد وصل أي وسيط تخزين إلى الحاسب.

#### التثبيت

يمكنك تثبيت مدير أقراص ثونَر من الحزمة [thunar-volman](https://www.archlinux.org/packages/?name=thunar-volman) من [المستودعات الرسمية](/index.php/Official_repositories "Official repositories").

#### التهيئة

يمكنك أيضاً تهيئة المدير لتنفيذ أمور معينة عند وصل كاميرا أو مشغل صوتيات إلى الحاسب، بعد تثبيت المدير قم بالتالي:

1.  قم بفتح ثونَر ثم اذهب إلى قائمة تحرير Edit ثم تفضيلات Preferences.
2.  تحت تبويب 'خيارات متقدمة' Advanced قم بتفعيل خيار 'تمكين إدارة الأقراص' Enable Volume Management.
3.  اضغط على تهيئة configure وقم بتفعيل العناصر التالية:
    *   ربط الأقراص القابلة للإزالة بمجرد وصلها بالجهاز Mount removable drives when hot-plugged.
    *   ربط الوسائط القابلة للإزالة عند إدخالها Mount removable media when inserted.
4.  قم بعمل التغييرات التي تريدها.

مثال لجعل برنامج أماروك Amarok يشغل الملفات الصوتية على القرص المدمج audio CD:

```
 Multimedia - Audio CDs: `amarok --cdplay %d`

```

## تلميحات وحِيَل

### استخدام ثونَر لاستعراض الأماكن البعيدة

منذ إصدار واجهة Xfce رقم 4.8 (ثونَر إصدار رقم 1.2) أصبح من الممكن أن تستعرض أماكن بعيدة Remote Locations (مثل مخدمات FTP أو Samba shares) مباشرة في ثونَر بشكل مشابه لما هو موجود في Gnome و KDE، لتفعيل استعراض الأماكن البعيدة يجب تواجد الحزمتين [gvfs](https://www.archlinux.org/packages/?name=gvfs) و [gvfs-smb](https://www.archlinux.org/packages/?name=gvfs-smb) المتوفرتين في [المستودعات الرسمية](/index.php/Official_repositories "Official repositories"). بعد أن تقوم بإعادة تشغيل الواجهة Xfce ستجد عنصر جديد يدعى الشبكة "Network" في الشريط الجانبي لثونَر، ولفتح مكان بعيد قم بإظهار نافذة الأماكن عن طريق `Ctrl+L` ومن ثم استخدم أحد أنواع URI التالية: smb:// , ftp:// , ssh://

#### التشغيل في الوضع المخفي

يستطيع ثونَر العمل في الوضع المخفي daemon mode (في الخلفية) لما لهذه الخاصية من فوائد عديدة من بينها فتح أسرع لنافذة ثونَر، حيث يبقى ثونَر يعمل في الخلفية ويقوم بفتح نافذته عند الضرورة (على سبيل المثال: عند توصيل ذاكرة فلاش).

لتفعيل هذه الخاصية هناك عدة طرق من بينها أن تقوم بتشغيل ثونَر بنفسك مباشرة بعد إقلاع النظام عن طريق الأمر `.xinitrc` أو باستخدام سكربت ليشغل ثونَر بشكل تلقائي مباشرة بعد إقلاع النظام (مثل [Openbox](/index.php/Openbox "Openbox")'s `autostart`)، الخيار يعود لك في اختيار الطريقة المناسبة.

لتشغيل ثونَر في الوضع الخلفي daemon mode قم بإضافة الكود التالي إلى سكربت التشغيل التلقائي الذي ستُنشئه أو قم بكتابة الكود في الطرفية مباشرة:

 `$ thunar --daemon &` 

### ضبط سمة الأيقونات

عند تثبيت ثونَر على واجهات غير Gnome أو Xfce فإن بعض الحزم والإعدادات التي تُعنى بتحديد سمة الأيقونات الواجب إظهارها قد تكون مفقودة، كما أن بعض مديري النوافذ مثل Awesome و Xmonad لا يشتملون على مدير XSettings وهو المكان الأول الذي يقوم ثونَر بالبحث فيه على إعدادات أيقوناته.

إذا كانت تطبيقات Xfce4 و Gnome التي سيتم تشغيلها كثيرة فمن الممكن تثبيت حزمة xfce-mcs-manager ومن ثم تشغيلها من سكربت بدء تشغيل مثلاً، ولكي تضبط اسم gtk-icon-theme-name لواجهة gtk2 عليك بإضافة التالي للملف `~/.gtkrc-2.0` (مع استبدال "tango" بالاسم الذي تريده):

```
 gtk-icon-theme-name = "Tango"

```

بمجرد تثبيت حزمة gnome-icon-theme ستضاف إلى ثونَر سمة أيقونات جديدة:

 `# pacman -S gnome-icon-theme` 

### حل مشكلة البطء والجمود أثناء التشغيل

يعاني بعض الأشخاص من أن ثونَر يستغرق وقتاً طويلاً للإقلاع أول مرة، هذه المشكلة يسببها gvfs حيث أنه يمنع ثونَر من الإقلاع حتى ينتهي gvfs من التحقق من الشبكة، لتغيير هذا الأمر قم بتعديل الملف `/usr/share/gvfs/mounts/network.mount` وذلك بتغيير **AutoMount=true** إلى **AutoMount=false**.

## إضافات وملحقات أخرى

الكثير من هذه الإضافات تنتمي إلى مجموعة [xfce4-goodies](https://www.archlinux.org/groups/x86_64/xfce4-goodies/) ، وبالتالي فإذا كانت هذه المجموعة مثبتة على نظامك فغالباً ستكون هذه الإضافات متوفرة لديك.

### Thunar Archive Plugin

هذه الإضافة [Thunar Archive Plugin](http://goodies.xfce.org/projects/thunar-plugins/thunar-archive-plugin) تسمح لك بإنشاء واستخراج المجلدات المؤرشفة من قائمة الخيارات، هذه الإضافة لا تقوم بالإنشاء أو الاستخراج مباشرةً ولكنها تعمل كواجهة لبرامج أخرى مثل File Roller, Ark أو Xarchiver، تتوفر هذه الإضافة [thunar-archive-plugin](https://www.archlinux.org/packages/?name=thunar-archive-plugin) في [المستودعات الرسمية](/index.php/Official_repositories "Official repositories").

### Thunar Media Tags Plugin

تُمكنك هذه الإضافة [Thunar Media Tags Plugin](http://goodies.xfce.org/projects/thunar-plugins/thunar-media-tags-plugin) من مشاهدة معلومات مفصلة عن ملفات الوسائط، كما أنها تشمل على أداة bulk لإعادة تسمية الملفات ووسوم ملفات الوسائط tags، بالإضافة إلى أنها تدعم ID3 ووسوم Ogg/Vorbis، تتوفر هذه الإضافة في حزمة [thunar-media-tags-plugin](https://www.archlinux.org/packages/?name=thunar-media-tags-plugin).

### Thunar thumbnails

يعتمد مدير الملفات ثونَر على برنامج خارجي يدعي [tumbler](http://git.xfce.org/xfce/tumbler/tree/README) لتكوين الصور المصغرة، ويتوفر هذا البرنامج من خلال حزمة [tumbler](https://www.archlinux.org/packages/?name=tumbler).

لتكوين صور مصغرة عن ملفات الفيديو فإنك تحتاج أيضاً إلى تثبيت [ffmpegthumbnailer](https://www.archlinux.org/packages/?name=ffmpegthumbnailer).

### Thunar Shares

تُمكنك هذه الإضافة [Thunar Shares Plugin](http://goodies.xfce.org/projects/thunar-plugins/thunar-shares-plugin) من مشاركة المجلدات بسهولة باستخدام Samba ضمن ثونَر ومن دون أن تكون مستخدماً جذراً root، تتوفر هذه الإضافة في حزمة [thunar-shares-plugin](https://aur.archlinux.org/packages/thunar-shares-plugin/) في مستودعات [AUR](/index.php/AUR "AUR").

اطلع على [Samba#Creating usershare path](/index.php/Samba#Creating_usershare_path "Samba") لمعلومات حول هذا الموضوع.

## إجراءات مخصصة

هذا القسم يتضمن إجراءات مخصصة مفيدة والتي يمكن الوصول إليها من قائمة تحرير Edit ثم تهيئة الإجراءات المخصصة Configure custom actions، المزيد من الأمثلة موضحة في [thunar wiki](http://docs.xfce.org/xfce/thunar/custom-actions).

### البحث عن الفيروسات

لاستعمال هذا الإجراء يجب أن تتأكد من تثبيت clamav و clamtk.

| الاسم | الأمر | أنماط الملف | الظهور عند وجود |
| Scan for virus | clamtk %F | * | Select all |

### الربط مع Dropbox

| الاسم | الأمر | أنماط الملف | الظهور عند وجود |
| Link to Dropbox | ln -s %f /path/to/DropboxFolder | * | Directories, other files |

يرجى ملاحظة أنه في حال استعمال إجراءات مخصصة كثيرة لربط ملفات ومجلدات بأماكن معينة فمن الأفضل أن يتم وضعهم جميعاً في قائمة `Send To` ضمن قائمة الخيارات لتجنب امتلاء القائمة الرئيسية لخيارات الملف أو المجلد، يمكنك تنفيذ هذه العملية بسهولة، كل ما يتطلبه الأمر هو إنشاء ملف بامتداد .desktop لكل إجراء مخصص ويتم وضع هذا الملف في المسار `~/.local/share/Thunar/sendto` لنفترض أننا نريد وضع رابط dropbox السابق في قائمة Send To، نقوم بإنشاء `dropbox_folder.desktop` ونضع داخله الأسطر التالية (يجب إعادة تشغيل ثونَر لتفعيل الإجراءات الجديدة):

```
[Desktop Entry]
Type=Application
Version=1.0
Encoding=UTF-8
Exec=ln -s %f /path/to/DropboxFolder
Icon=/usr/share/icons/dropbox.png
Name=Dropbox

```

## روابط ومراجع

*   [Thunar](http://thunar.xfce.org/index.html) صفحة مشروع ثونًر
*   [Thunar Volume Manager](http://goodies.xfce.org/projects/thunar-plugins/thunar-volman) صفحة مشروع
*   [Thunar Archive Plugin](http://goodies.xfce.org/projects/thunar-plugins/thunar-archive-plugin) صفحة مشروع
*   [Thunar Media Tags Plugin](http://goodies.xfce.org/projects/thunar-plugins/thunar-media-tags-plugin) صفحة مشروع
*   [Thunar Shares Plugin](http://goodies.xfce.org/projects/thunar-plugins/thunar-shares-plugin/) صفحة مشروع
*   [list](http://goodies.xfce.org/projects/thunar-plugins/start) قائمة بإضافات وملحقات ثونًر