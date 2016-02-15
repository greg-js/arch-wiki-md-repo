**Vifm** هو مدير ملفات يتبع أسلوب المحرر vi لاختصارات المفاتيح، إذا كنت من مستخدمي vi فإن vifm سيمكنك من التحكم بملفاتك من دون أن تضطر لتعلم أوامر جديدة. المصدر: [Vifm on sourceforge](http://vifm.sourceforge.net/).

## Contents

*   [1 التثبيت](#.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA)
*   [2 ملف المساعدة](#.D9.85.D9.84.D9.81_.D8.A7.D9.84.D9.85.D8.B3.D8.A7.D8.B9.D8.AF.D8.A9)
*   [3 تخصيص Vifm](#.D8.AA.D8.AE.D8.B5.D9.8A.D8.B5_Vifm)
    *   [3.1 أنظمة الألوان](#.D8.A3.D9.86.D8.B8.D9.85.D8.A9_.D8.A7.D9.84.D8.A3.D9.84.D9.88.D8.A7.D9.86)
    *   [3.2 عمل خرائط للمفاتيح](#.D8.B9.D9.85.D9.84_.D8.AE.D8.B1.D8.A7.D8.A6.D8.B7_.D9.84.D9.84.D9.85.D9.81.D8.A7.D8.AA.D9.8A.D8.AD)
    *   [3.3 فتح الملفات في Vifm](#.D9.81.D8.AA.D8.AD_.D8.A7.D9.84.D9.85.D9.84.D9.81.D8.A7.D8.AA_.D9.81.D9.8A_Vifm)
    *   [3.4 استعراض الصور في المجلد الحالي باستخدام Feh](#.D8.A7.D8.B3.D8.AA.D8.B9.D8.B1.D8.A7.D8.B6_.D8.A7.D9.84.D8.B5.D9.88.D8.B1_.D9.81.D9.8A_.D8.A7.D9.84.D9.85.D8.AC.D9.84.D8.AF_.D8.A7.D9.84.D8.AD.D8.A7.D9.84.D9.8A_.D8.A8.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_Feh)
    *   [3.5 أوامر المستخدم](#.D8.A3.D9.88.D8.A7.D9.85.D8.B1_.D8.A7.D9.84.D9.85.D8.B3.D8.AA.D8.AE.D8.AF.D9.85)
    *   [3.6 إنشاء روابط](#.D8.A5.D9.86.D8.B4.D8.A7.D8.A1_.D8.B1.D9.88.D8.A7.D8.A8.D8.B7)
    *   [3.7 إنشاء ملف تورنت](#.D8.A5.D9.86.D8.B4.D8.A7.D8.A1_.D9.85.D9.84.D9.81_.D8.AA.D9.88.D8.B1.D9.86.D8.AA)
    *   [3.8 الإشارات](#.D8.A7.D9.84.D8.A5.D8.B4.D8.A7.D8.B1.D8.A7.D8.AA)
*   [4 بدائل](#.D8.A8.D8.AF.D8.A7.D8.A6.D9.84)

## التثبيت

يتوفر Vifm في المجتمع:

```
# pacman -S vifm

```

تستطيع تثبيت هذه الإضافات الاختيارية لمعاينة الملفات:

*   [tree](https://www.archlinux.org/packages/?name=tree) لمعاينة المجلدات
*   [mp3info](https://www.archlinux.org/packages/?name=mp3info) لمعاينة معلومات ملفات mp3
*   [poppler](https://www.archlinux.org/packages/?name=poppler) لمعاينة ملفات PDF

## ملف المساعدة

المعلومات الأساسية حول Vifm تجدها في ملف المساعدة، يمكنك الاطلاع على الملف عند تشغيل vifm وكتابة:

```
:h

```

تستطيع الاطلاع على الكتيب الإرشادي man page فهو مصدر جيد آخر للمعلومات.

## تخصيص Vifm

بعد تثبيت vifm على الجهاز فإنه يُنشأ مجلداً باسم .vifm في مجلد المنزل يحتوي على:

*   vifmrc - عبارة عن ملف تهيئة يمكنك تعديله بما يتناسب مع أسلوب عملك
*   vifm-help.txt ملف المساعدة
*   vifminfo - محتويات المحذوفات والإشارات المرجعية، يُنصح بعدم تعديل هذا الملف يدوياً
*   Trash/ directory - مجلد المحذوفات
*   colors/ directory - أنظمة الألوان
    *   Default - نظام الألوان الافتراضي، يمكن نسخه من أجل عمل أنظمة أخرى

لبدء التخصيص قم بقراءة المعلومات المتواجدة في:

*   /usr/share/vifm/vifm.txt
*   /usr/share/vifm/vifm-help.txt

### أنظمة الألوان

يحوي مجلد ~/.vifm/colors ملفات أنظمة الألوان، التصميم مُبين في الملف ويتبع تصميم المحرر vi/vim في قواعد التلوين، وهي كالتالي:

```
highlight <group> cterm=<attribute> ctermfg=<color> ctermbg=<color>

```

مثال: نظام الألوان يكون على الشكل التالي:

```
highlight Win cterm=none ctermfg=white ctermbg=black
highlight Directory cterm=bold ctermfg=cyan ctermbg=none
highlight Link cterm=bold ctermfg=yellow ctermbg=none
highlight BrokenLink cterm=bold ctermfg=red ctermbg=none
highlight Socket cterm=bold ctermfg=magenta ctermbg=none
highlight Device cterm=bold ctermfg=red ctermbg=none
highlight Fifo cterm=bold ctermfg=cyan ctermbg=none
highlight Executable cterm=bold ctermfg=green ctermbg=none
highlight Selected cterm=bold ctermfg=magenta ctermbg=none
highlight CurrLine cterm=bold ctermfg=none ctermbg=blue
highlight TopLine cterm=none ctermfg=black ctermbg=white
highlight TopLineSel cterm=bold ctermfg=black ctermbg=none
highlight StatusLine cterm=bold ctermfg=black ctermbg=white
highlight WildMenu cterm=underline,reverse ctermfg=white ctermbg=black
highlight CmdLine cterm=none ctermfg=white ctermbg=black
highlight ErrorMsg cterm=none ctermfg=red ctermbg=black
highlight Border cterm=none ctermfg=black ctermbg=white

```

### عمل خرائط للمفاتيح

منذ الإصدار 0.6.2 أصبح من الممكن تخصيص أزرار لوحة المفاتيح، وذلك في وضع الأوامر وباستعمال الأمر map بالشكل التالي:

```
 :map ] :s

```

هذه العملية لن يتم حفظها بشكل دائم، لحفظ التخصيص بشكل دائم قم بوضع ملف التخصيص في ~/vifm/vifmrc ، توجد بعض الأمثلة عن خرائط المفاتيح في نهاية الملف.

### فتح الملفات في Vifm

يمكنك تحديد تطبيقات معينة لفتح صيغ ملفات محددة في vifm، على سبيل المثال:

```
filetype *.jpg,*.jpeg,*.png,*.gif feh %f 2>/dev/null &
filetype *.md5 md5sum -c %f

```

ستجد قائمة بالكثير من التطبيقات الافتراضية في ملف vifmrc التي يمكنك تعديلها.

### استعراض الصور في المجلد الحالي باستخدام Feh

```
filextype *.jpg,*.jpeg,*.png,*.gif
       \ {View in feh}
       \ feh -FZ %d --start-at %d/%c,

```

سيتم عرض الصورة المحددة باستخدام تطبيق feh لكن ستعرض الصور الأخرى في المجلد باستخدام تطبيق عرض الصور الافتراضي الخاص بها.

### أوامر المستخدم

تستطيع إنشاء أوامر مخصصة في vifm، مثال على ذلك:

```
command df df -h %m 2> /dev/null
command diff vim -d %f %F

```

### إنشاء روابط

```
command link ln -s %d/%f %D

```

عندما تكتب:

```
:link

```

سيتم إنشاء رابط للملف المحدد في المجلد الآخر (إذا كنت في وضع split view)، هذه العملية تعمل أيضاً بتحديد عدة ملفات سواءً بتحديدها بالنظر(v) أو بتحديد الوسم(t).

### إنشاء ملف تورنت

لإنشاء ملف .torrent للملف الحالي ووضعه في مجلد على التبويب الآخر:

```
command mkt mktorrent -p -a [your announce url here] -o %D/%f.torrent %d/%f

```

### الإشارات

يمكن وضع إشارات بشكل مماثل لطريقة المحرر vi، لوضع إشارة للملف الحالي:

```
m[a-z][A-Z][0-9]

```

اذهب إلى ملف تم وضع إشارة له:

```
'[a-z][A-Z][0-9]

```

vifm سيتذكر الإشارات حتى بعد تغيير الجلسات

## بدائل

يوجد مدير ملفات أخر يستخدم الطرفية ويتبع أسلوب vi لاختصارات المفاتيح وهو مدير الملفات [ranger](/index.php/Ranger "Ranger").