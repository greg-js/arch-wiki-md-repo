**حالة الترجمة：** هذه المقالة هي إصدار مُترجَم من [LibreOffice](/index.php/LibreOffice "LibreOffice"). آخر تاريخ ترجمة: 2014-11-06\. انقر [هذه الوصلة](https://wiki.archlinux.org/index.php?title=LibreOffice&diff=0&oldid=333741) للتحقّق من تغييرات الصفحة الإنجليزية بعد الترجمة.

من [Home - LibreOffice](http://www.libreoffice.org/):

	*LibreOffice is the free power-packed Open Source personal productivity suite for Windows, Macintosh and Linux, that gives you six feature-rich applications for all your document production and data processing needs: Writer, Calc, Impress, Draw, Math and Base. [Support](http://www.libreoffice.org/get-help/) and [documentation](http://www.libreoffice.org/get-help/documentation/) is free from our large, dedicated community of users, contributors and developers. [You, too, can also get involved!](http://www.libreoffice.org/get-involved/)*

## Contents

*   [1 ليبر أوفيس في آرتش لينكس](#.D9.84.D9.8A.D8.A8.D8.B1_.D8.A3.D9.88.D9.81.D9.8A.D8.B3_.D9.81.D9.8A_.D8.A2.D8.B1.D8.AA.D8.B4_.D9.84.D9.8A.D9.86.D9.83.D8.B3)
*   [2 التثبيت](#.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA)
*   [3 السمة](#.D8.A7.D9.84.D8.B3.D9.85.D8.A9)
    *   [3.1 سمات فَيَرفُكس](#.D8.B3.D9.85.D8.A7.D8.AA_.D9.81.D9.8E.D9.8A.D9.8E.D8.B1.D9.81.D9.8F.D9.83.D8.B3)
    *   [3.2 تعطيل شعار البدء](#.D8.AA.D8.B9.D8.B7.D9.8A.D9.84_.D8.B4.D8.B9.D8.A7.D8.B1_.D8.A7.D9.84.D8.A8.D8.AF.D8.A1)
*   [4 إدارة الامتدادات](#.D8.A5.D8.AF.D8.A7.D8.B1.D8.A9_.D8.A7.D9.84.D8.A7.D9.85.D8.AA.D8.AF.D8.A7.D8.AF.D8.A7.D8.AA)
*   [5 مساعدات اللغة](#.D9.85.D8.B3.D8.A7.D8.B9.D8.AF.D8.A7.D8.AA_.D8.A7.D9.84.D9.84.D8.BA.D8.A9)
    *   [5.1 المدقّق الإملائي](#.D8.A7.D9.84.D9.85.D8.AF.D9.82.D9.91.D9.82_.D8.A7.D9.84.D8.A5.D9.85.D9.84.D8.A7.D8.A6.D9.8A)
    *   [5.2 قواعد الواصلة](#.D9.82.D9.88.D8.A7.D8.B9.D8.AF_.D8.A7.D9.84.D9.88.D8.A7.D8.B5.D9.84.D8.A9)
    *   [5.3 المترادفات](#.D8.A7.D9.84.D9.85.D8.AA.D8.B1.D8.A7.D8.AF.D9.81.D8.A7.D8.AA)
    *   [5.4 المدقّق النحوي](#.D8.A7.D9.84.D9.85.D8.AF.D9.82.D9.91.D9.82_.D8.A7.D9.84.D9.86.D8.AD.D9.88.D9.8A)
    *   [5.5 مساعدة الإنجليزية الأمريكية (en-US) دون الإنترنت](#.D9.85.D8.B3.D8.A7.D8.B9.D8.AF.D8.A9_.D8.A7.D9.84.D8.A5.D9.86.D8.AC.D9.84.D9.8A.D8.B2.D9.8A.D8.A9_.D8.A7.D9.84.D8.A3.D9.85.D8.B1.D9.8A.D9.83.D9.8A.D8.A9_.28en-US.29_.D8.AF.D9.88.D9.86_.D8.A7.D9.84.D8.A5.D9.86.D8.AA.D8.B1.D9.86.D8.AA)
*   [6 تثبيت وحدات الماكرو](#.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_.D9.88.D8.AD.D8.AF.D8.A7.D8.AA_.D8.A7.D9.84.D9.85.D8.A7.D9.83.D8.B1.D9.88)
*   [7 تسريع ليبر أوفيس](#.D8.AA.D8.B3.D8.B1.D9.8A.D8.B9_.D9.84.D9.8A.D8.A8.D8.B1_.D8.A3.D9.88.D9.81.D9.8A.D8.B3)
*   [8 إصلاح المشاكل](#.D8.A5.D8.B5.D9.84.D8.A7.D8.AD_.D8.A7.D9.84.D9.85.D8.B4.D8.A7.D9.83.D9.84)
    *   [8.1 إنابة (استبدال) الخطوط](#.D8.A5.D9.86.D8.A7.D8.A8.D8.A9_.28.D8.A7.D8.B3.D8.AA.D8.A8.D8.AF.D8.A7.D9.84.29_.D8.A7.D9.84.D8.AE.D8.B7.D9.88.D8.B7)
    *   [8.2 إزالة التسنّن (التنعيم)](#.D8.A5.D8.B2.D8.A7.D9.84.D8.A9_.D8.A7.D9.84.D8.AA.D8.B3.D9.86.D9.91.D9.86_.28.D8.A7.D9.84.D8.AA.D9.86.D8.B9.D9.8A.D9.85.29)
    *   [8.3 التجمّد عند استخدام مشاركات NFSv3](#.D8.A7.D9.84.D8.AA.D8.AC.D9.85.D9.91.D8.AF_.D8.B9.D9.86.D8.AF_.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_.D9.85.D8.B4.D8.A7.D8.B1.D9.83.D8.A7.D8.AA_NFSv3)
    *   [8.4 إصلاح خطأ هيكل جاڤا](#.D8.A5.D8.B5.D9.84.D8.A7.D8.AD_.D8.AE.D8.B7.D8.A3_.D9.87.D9.8A.D9.83.D9.84_.D8.AC.D8.A7.DA.A4.D8.A7)
    *   [8.5 لا يكتشف ليبر أوفيس الشهادات](#.D9.84.D8.A7_.D9.8A.D9.83.D8.AA.D8.B4.D9.81_.D9.84.D9.8A.D8.A8.D8.B1_.D8.A3.D9.88.D9.81.D9.8A.D8.B3_.D8.A7.D9.84.D8.B4.D9.87.D8.A7.D8.AF.D8.A7.D8.AA)
    *   [8.6 تشغيل ملفات .pps في وضع التحرير (دون العرض التقديمي)](#.D8.AA.D8.B4.D8.BA.D9.8A.D9.84_.D9.85.D9.84.D9.81.D8.A7.D8.AA_.pps_.D9.81.D9.8A_.D9.88.D8.B6.D8.B9_.D8.A7.D9.84.D8.AA.D8.AD.D8.B1.D9.8A.D8.B1_.28.D8.AF.D9.88.D9.86_.D8.A7.D9.84.D8.B9.D8.B1.D8.B6_.D8.A7.D9.84.D8.AA.D9.82.D8.AF.D9.8A.D9.85.D9.8A.29)
    *   [8.7 مشاكل المَصَادر](#.D9.85.D8.B4.D8.A7.D9.83.D9.84_.D8.A7.D9.84.D9.85.D9.8E.D8.B5.D9.8E.D8.A7.D8.AF.D8.B1)
    *   [8.8 دعم الوسائط](#.D8.AF.D8.B9.D9.85_.D8.A7.D9.84.D9.88.D8.B3.D8.A7.D8.A6.D8.B7)
    *   [8.9 لا يتغيّر حجم المحتوى في النوافذ مع Xfwm4](#.D9.84.D8.A7_.D9.8A.D8.AA.D8.BA.D9.8A.D9.91.D8.B1_.D8.AD.D8.AC.D9.85_.D8.A7.D9.84.D9.85.D8.AD.D8.AA.D9.88.D9.89_.D9.81.D9.8A_.D8.A7.D9.84.D9.86.D9.88.D8.A7.D9.81.D8.B0_.D9.85.D8.B9_Xfwm4)
    *   [8.10 gvfs mounts](#gvfs_mounts)

## ليبر أوفيس في آرتش لينكس

أُسقِط الدعم الرسمي لـ [OpenOffice.org](/index.php/OpenOffice.org "OpenOffice.org") لأجل ليبر أوفيس، the "Document Foundation" fork of the project, والذي يتضمّن أيضًا تعزيزات ومزايا إضافية. طالع [Dropping Oracle OpenOffice (arch-general)](https://mailman.archlinux.org/pipermail/arch-general/2011-March/018819.html).

## التثبيت

[ثبّت](/index.php/Pacman "Pacman") إحدى المجموعات التالية من [المستودعات الرسمية](/index.php/Official_repositories_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9) "Official repositories (العربية)"):

*   [libreoffice-fresh](https://www.archlinux.org/packages/?name=libreoffice-fresh) هي الفرع المميّز بتحسينات البرنامج الجديدة.
*   [libreoffice-still](https://www.archlinux.org/packages/?name=libreoffice-still) هي الفرع المُصان.

**ملاحظة:**

*   تثبيت حزمة لغة واحدة مطلوب. اللغة الافتراضية هي الأفريكانية (لأنّها (أبجديًّا المُوفِّر الأولّ لِـ libreoffice-langpack). إن أردتَ حزمة الأمريكية الإنجليزية (en-US)، ثبّت [libreoffice-en-GB](https://www.archlinux.org/packages/?name=libreoffice-en-GB)، وليس [libreoffice-uk](https://www.archlinux.org/packages/?name=libreoffice-uk) (الأوكرانية) أو [libreoffice-br](https://www.archlinux.org/packages/?name=libreoffice-br) (البريتونية)!
*   حزمتي [libreoffice-still-kde4](https://www.archlinux.org/packages/?name=libreoffice-still-kde4) و [libreoffice-still-gnome](https://www.archlinux.org/packages/?name=libreoffice-still-gnome) مطلوبتان للتكامل البصري مع كيوت وجتك+ بالترتيب. طالع قسم [السمة](#Theme).
*   لعدّة تطوير البرمجيات، استخدم [libreoffice-fresh-sdk](https://www.archlinux.org/packages/?name=libreoffice-fresh-sdk) أو [libreoffice-still-sdk](https://www.archlinux.org/packages/?name=libreoffice-still-sdk) وفقًا لما لديك.

Check the optional dependencies pacman displays. A Java Runtime Environment is not required unless you want to use Libreoffice Base: see [Java](/index.php/Java "Java"). You may need [hsqldb2-java](https://aur.archlinux.org/packages/hsqldb2-java/) to use [some modules](https://wiki.documentfoundation.org/Base#Java_and_HSQLDB) in LibreOffice Base.

## السمة

لتكامل [Qt](/index.php/Qt "Qt")، ثبّت الحزمة [libreoffice-still-kde4](https://www.archlinux.org/packages/?name=libreoffice-still-kde4). لتكامل [GTK+](/index.php/GTK%2B "GTK+")، ثبّت الحزمة [libreoffice-still-gnome](https://www.archlinux.org/packages/?name=libreoffice-still-gnome).

**ملاحظة:**

*   يمكن لتكامل QT محاكاة سمة GTK+. الأمر `qtconfig-qt4` يفتح نافذة حيث تستطيع الاختيار بينها.
*   حتّى لو لم تكن تشغّل أيًّا من بيئات سطح المكتب هذه ولا تريد "التكامل" معها، قد تحتاج تثبيت هذه الحزم ليستخدم ليبر أوفيس سمات GTK+ أو Qt غير الافتراضية. كمثال، يستخدم ليبر أوفيس على e17 السمة الافتراضية "القبيحة"" (aka "win95"/"win98"). تثبيت libreoffice-still-gnome يسمح لك باختيار سمة GTK+ جذّابة أكثر.

As of LibreOffice version 3.5.x it tries to magically autodetect your desktop UI using the following magic if proper libs will be found:

```
gtk > kde4 > generic

```

To force the use of a certain VCL UI interface use one of this:

```
SAL_USE_VCLPLUGIN=gen lowriter
SAL_USE_VCLPLUGIN=kde4 lowriter
SAL_USE_VCLPLUGIN=gtk lowriter
SAL_USE_VCLPLUGIN=gtk3 lowriter

```

It is convenient to save `SAL_USE_VCLPLUGIN` variable in your shell configuration file, e.g.`/etc/bash.bashrc` or `~/.bashrc` if using Bash.

**ملاحظة:** واجهة مستخدم GTK3 الجديدة معلّمة كأوّلية وتجربيبة، وستكون متوفرة فقط إن مكّنت "المزايا التجريبية" في حواري ضبط ليبر أوفيس العام.

في كلّ الأحوال، إن بدا وكأنّه يستخدم أيقونات ويندوز 95/98، اذهب إلى "أدوات > خيارات..." في القوائم (التي توفّر حواري الخيارات)، وثمّ اختر "LibreOffice > الموصليّة" وأزل تعليم "الكشف تلقائيًا عن وضع التباين العالي في نظام التشغيل"

إن لم يعمل ذلك مباشرةً، عليك تغيير طقم الأيقونات المُستخدمة، توجد هي الأخرى في حواري الخيارات، تحت "LibreOffice > عرض" بصندوقين منبثقين "حجم الأيقونة ونمطها" (الصندوق المنبثق الثاني يجب أن يتغيّر إلى شيء غير "تباين عالٍ".

### سمات فَيَرفُكس

سلسلة ليبر أوفيس 4.x يمكنها استخدام سمات فَيَرفُكس. أُدخل إلى خيارات ليبر أوفيس واختر "Personalization > Select Theme"، ثمّ ألصِق عنوان URL لسمتكَ المفضّلة. سيظهر زر في المربع الحواري يسمح لك بفتح المتصفّح. يمكن العثور على السمات من [مستودع سمات موزيلا](https://addons.mozilla.org/en-US/firefox/themes/).

### تعطيل شعار البدء

إن فضّلت تعطيل شعار البدء، افتح `/etc/libreoffice/sofficerc`، ابحث عن السطر `Logo=` وعيّن `Logo=0`.

**ملاحظة:** هذا المتغيّر غير متربط مع دعم برمجة لوجو.

## إدارة الامتدادات

الامتدادات الإضافية التالية متوفّرة من [المستودعات الرسمية](/index.php/Official_repositories_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9) "Official repositories (العربية)"):

*   [libreoffice-still-extension-nlpsolver](https://www.archlinux.org/packages/?name=libreoffice-still-extension-nlpsolver)
*   [libreoffice-still-extension-wiki-publisher](https://www.archlinux.org/packages/?name=libreoffice-still-extension-wiki-publisher)

تفحّص [| مستودع مستخدم آرتش](/index.php?title=AUR_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9)&action=edit&redlink=1 "AUR (العربية) (page does not exist)") لمزيد من الامتدادات، أو مدير امتدادات ليبر أوفيس، أو [كوكب ليبر](http://libreplanet.org/wiki/Group:OpenOfficeExtensions/List).

## مساعدات اللغة

### المدقّق الإملائي

لتدقيق الإملاء، ستحتاج إلى [hunspell](https://www.archlinux.org/packages/?name=hunspell) وقاموس لغة لِـ hunspell (مثل [hunspell-en](https://www.archlinux.org/packages/?name=hunspell-en) للإنجليزية, [hunspell-de](https://www.archlinux.org/packages/?name=hunspell-de) للألمانية، إلخ).

### قواعد الواصلة

لقواعد الواصلة، ستحتاج إلى [hyphen](https://www.archlinux.org/packages/?name=hyphen) ومجموعة لغة لقواعد الواصلة ([hyphen-en](https://www.archlinux.org/packages/?name=hyphen-en) للإنجليزية، [hyphen-de](https://www.archlinux.org/packages/?name=hyphen-de) للألمانية، إلخ).

### المترادفات

لخيار المترادفات، ستحتاج إلى [libmythes](https://www.archlinux.org/packages/?name=libmythes) و a mythes language thesaurus (like [mythes-en](https://www.archlinux.org/packages/?name=mythes-en) للإنجليزية، [mythes-de](https://www.archlinux.org/packages/?name=mythes-de) للألمانية، إلخ).

### المدقّق النحوي

للتدقيق النحوي، ستحتاج إلى تثبيت امتداد مثل LanguageTool، حيث تجدها في [AUR](/index.php/AUR "AUR"): [libreoffice-extension-languagetool](https://aur.archlinux.org/packages/libreoffice-extension-languagetool/) أو [موقع وِب LanguageTool](http://www.languagetool.org/).

يمكن العثور على أدوات نحوية أخرى من [صفحة امتدادات ليبر أوفيس](http://libreplanet.org/wiki/Group:OpenOfficeExtensions/List) أو [موقع وِب أوبن أوفيس](http://lingucomponent.openoffice.org/grammar.html) . لا يُضمن عمل كل امتدادات أوبن أوفيس مع ليبر أوفيس.

**ملاحظة:** يستخدم Languagetool جاڤا وقد يُبطئ أو يعلّق ليبر أوفيس لفترة بسيطة، خاصّةً عند فتح المستندات. لحسن الحظ هذا يحدث غالبًا عند فتح مستند لأول مرة أو غير ظاهر.

للمستخدمين الفنلديين، هناك أربع حزم لتثبيتها. ثبّتها بهذا الترتيب: [malaga](https://aur.archlinux.org/packages/malaga/)، و[suomi-malaga-voikko](https://aur.archlinux.org/packages/suomi-malaga-voikko/)، و[libvoikko](https://www.archlinux.org/packages/?name=libvoikko) و [voikko-libreoffice](https://aur.archlinux.org/packages/voikko-libreoffice/).

### مساعدة الإنجليزية الأمريكية (en-US) دون الإنترنت

حزم الإنجليزية الأمريكية في المستودعات الرسمية لا تحوي ملفات المساعدة التي تعمل دون الإنترنت. للمستخديم الراغبين بهذه المساعدة عليه تثبيت حزمة [libreoffice-still-en-us-help](https://aur.archlinux.org/packages/libreoffice-still-en-us-help/) أو [libreoffice-fresh-en-us-help](https://aur.archlinux.org/packages/libreoffice-fresh-en-us-help/) من [مستودع مستخدم آرتش](/index.php?title=AUR_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9)&action=edit&redlink=1 "AUR (العربية) (page does not exist)").

## تثبيت وحدات الماكرو

إن اعتزمت استخدام وحدات الماكرو، يجب أن تكون لديك بيئة تشغيل جاڤا ممكّنة. هناك بيئة تشغيل جاڤا ممكّنة افتراضيًّا، لكن تعطيلها [يسرّع البرنامج](#.D8.AA.D8.B3.D8.B1.D9.8A.D8.B9_.D9.84.D9.8A.D8.A8.D8.B1_.D8.A3.D9.88.D9.81.D9.8A.D8.B3).

المسار الافتراضي لوحدات الماكرو في آرتش لينكس يختلف من أغلب توزيعات لينكس. المسار هو:

```
~/.config/libreoffice/4/user/Scripts/

```

## تسريع ليبر أوفيس

قد تحسّن بعض الإعدادات وقت تحميل ليبر أوفيس واستجابته كذلك، بعضها أيضًا يزيد استخدام الذاكرة العشوائية، لذا استخدمها بحذر. يمكن الوصول إليها تحت "أدوات > خيارات".

*   تحت "الذاكرة":
    *   قلّل عدد خطوات التراجع لأقل من 100، شيءٌ كـ 20 أو 30 خطوة.
    *   تحت *ذاكرة تخزين الرسومات المؤقّتة*، عيّن استخدام ليبر أوفيس إلى 128 م.بايت (أعلى من الأصلية، 20 م.بايت).
    *   عيّن "ذاكرة لكل كائن" إلى 20 م.بايت (أعلى من الأصلية، 5 م.بايت).
    *   إن كان ليبر أوفيس يُستخدَم مرارًا، علّم "تمكين صينية التشغيل السريع".

**ملاحظة:** يجب أن تكون الحزمة [libreoffice-still-gnome](https://www.archlinux.org/packages/?name=libreoffice-still-gnome) مثبّتة ليتوفّر خيار التشغيل السريع.

*   تحت "متقدّم"، أزل تعليم "استخدم البيئة التشغيلية لجافا".

**ملاحظة:** لقائمة من الوظائف المكتوبة بجاڤا فقط، طالع: [https://wiki.documentfoundation.org/Development/Java](https://wiki.documentfoundation.org/Development/Java).

## إصلاح المشاكل

### إنابة (استبدال) الخطوط

يمكن تغيير هذه الإعدادات في قوائم ليبر أوفيس. من القائمة المنسدلة، اختر "أدوات > خيارات > LibreOffice > الخطوط". علّم المربع الذي يقول "تطبيق الجدول البديل". اطبع `Andale Sans UI` في صندوق الخط واختر الخط المطلوب في خيار "استبدال بـ". عندما تنتهي، انقر "علامة التحقّق". ثمّ اختر الخياران "دائمًا" و "الشاشة فقط" في الصندوق بالأسفل. انقر حسنًا. عليك فيما بعد الذهاب إلى "أدوات > خيارات > LibreOffice > عرض"، وأزل تعليم "استخدام خط النظام لواجهة المستخدم". إن كنت تستخدم خط non-antialised، كـ Arial، عليك أيضًا إزالة تعليم " تحسين حواف خط الشاشة" قبل تصيير خطوط القوائم بشكل جيّد.

### إزالة التسنّن (التنعيم)

نفّذ:

```
$ echo "Xft.lcdfilter: lcddefault" | xrdb -merge

```

لجعل التغيير مستمرًّا، أضف `Xft.lcdfilter: lcddefault` إلى الملف `~/.Xresources`، وتأكّد من تشغيل `$ xrdb -merge ~/.Xresources` ([المصدر](https://bugs.launchpad.net/ubuntu/+source/openoffice.org/+bug/271283/comments/19)). طالع [X resources](/index.php/X_resources "X resources") لتفاصيل أكثر.

إن لم تعمل هذه، حاول أيضًا إضافة `Xft.lcdfilter: lcddefault` إلى الملف `~/.Xdefaults`. إن لم يكن لديك هذا الملف، عليك إنشاءه.

### التجمّد عند استخدام مشاركات NFSv3

إن تجمّد ليبر أوفيس أثناء فتح أو حفظ مستند موجود على مشاركة NFSv3، حاول تعليق الأسطر التالية مؤقّتًا بـ `#` في `/usr/lib/libreoffice/program/soffice`:

```
# file locking now enabled by default
SAL_ENABLE_FILE_LOCKING=1
export SAL_ENABLE_FILE_LOCKING

```

لتجنّب الكتابة فوقه عند التحديث، انسخ `/usr/lib/libreoffice/program/soffice` في `/usr/local/bin`. المنشور الأصلي [هنا](http://www.crazysquirrel.com/computing/debian/bugs/openoffice-over-nfs.jspx).

### إصلاح خطأ هيكل جاڤا

قد يواجهك الخطأ التالي وأنت تحاول تشغيل ليبر أوفيس.

```
[Java framework] Error in function createSettingsDocument (elements.cxx).
javaldx failed!

```

إن حصل ذلك، اعطِ لنفسك ملكية `~/.config/` مثل:

```
# chown -vR username:users ~/.config

```

[أُنشُر في منتديات آرتش لينكس](https://bbs.archlinux.org/viewtopic.php?id=93168).

### لا يكتشف ليبر أوفيس الشهادات

إن لم ترَ أيًّا من الشهادات عندما تحاول توقيع مستند، عليك امتلاك الشهادات المُضبطة في موزيلا فَيَرفُكس (أو ثَندِربيرد). إن لم يُرِ ليبر أوفيس أيًّا منها، طالع متغيّر البيئة `MOZILLA_CERTIFICATE_FOLDER` للإشارة إلى مجلد موزيلا فَيَرفُكس (أو ثَندِربيرد):

```
export MOZILLA_CERTIFICATE_FOLDER=$HOME/.mozilla/firefox/XXXXXX.default/

```

[اكتشاف الشهادة](http://wiki.openoffice.org/wiki/Certificate_Detection).

### تشغيل ملفات .pps في وضع التحرير (دون العرض التقديمي)

الحل الوحيد هو بإعادة تسمية الملف `.pps` إلى `.ppt`.

أضف السكرِبت التالي إلى دليل المنزل واستخدمهُ لفتح أي ملف `.pps`. مفيدٌ جدًّا لفتح ملفات `.pps` المُستقبَلة من بريد إلكتروني دون الحاجة لحفظها.

```
#!/bin/bash

f=$(mktemp)
cp "$1" "${f}.ppt" && libreoffice "${f}.ppt" && rm -f "${f}.ppt"

```

### مشاكل المَصَادر

إن انهار رايتر في محاولة الوصول إلى "أدوات > قاعدة بيانات المراجع"، بالخطأ التالي:

```
com::sun::star::loader::CannotActivateFactoryException

```

ثبّت [libreoffice-base](https://www.archlinux.org/packages/?name=libreoffice-base) للالتفاف حول علّة معروفة، يظهر أنها [أُصلِحت](http://cgit.freedesktop.org/libreoffice/core/commit/?id=1889c1af41650576a29c587a0b2cdeaf0d297587).

### دعم الوسائط

إن كانت الفيديوهات المضمّنة صناديق رمادية فقط، تأكد من تثبيت [ملحقات GStreamer](/index.php/GStreamer#Current_version_plugins "GStreamer") المطلوبة.

### لا يتغيّر حجم المحتوى في النوافذ مع Xfwm4

إن لم يتغيّر حجم محتوى نافذة ليبر أوفيس معه تحت Xfce (أو باستخدام Xfwm4 فقط)، مثل هذا المنشور: [[1]](https://bbs.archlinux.org/viewtopic.php?id=133137). ثبّت [libreoffice-still-gnome](https://www.archlinux.org/packages/?name=libreoffice-still-gnome) لحلّ هذه المشكلة.

### gvfs mounts

إن احتجت إلى فتح/حفظ المستندات على gvfs mounts، سيكون عليك تثبيت الحزمة [libreoffice-still-gnome](https://www.archlinux.org/packages/?name=libreoffice-still-gnome).