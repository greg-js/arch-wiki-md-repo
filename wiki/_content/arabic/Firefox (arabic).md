[Firefox](http://www.firefox.com) هو متصفح رسومي شهير مفتوح المصدر من شركة [Mozilla](http://www.mozilla.com).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 التنصيب](#التنصيب)
*   [2 الملحقات add-ons](#الملحقات_add-ons)
*   [3 الإضافات plugins](#الإضافات_plugins)
    *   [3.1 التكامل مع حافظة مفاتيح GNOME](#التكامل_مع_حافظة_مفاتيح_GNOME)
    *   [3.2 التكامل مع KDE](#التكامل_مع_KDE)
    *   [3.3 القواميس لتصحيح مدخلات المستخدم](#القواميس_لتصحيح_مدخلات_المستخدم)
    *   [3.4 إضافة مُحركات بحث الى متصفح firefox](#إضافة_مُحركات_بحث_الى_متصفح_firefox)
        *   [3.4.1 حزمة arch-firefox-search](#حزمة_arch-firefox-search)
*   [4 مشتقات المتصفح فايرفوكس](#مشتقات_المتصفح_فايرفوكس)
*   [5 إسكتشاف الأخطاء و إصلاحها](#إسكتشاف_الأخطاء_و_إصلاحها)
    *   [5.1 تحديد عميل البريد الإلكتروني الخاص بك](#تحديد_عميل_البريد_الإلكتروني_الخاص_بك)
    *   [5.2 مشاكل Open containing folder في واجهة GNOME3](#مشاكل_Open_containing_folder_في_واجهة_GNOME3)
    *   [5.3 مشاكل Open containing folder في واجهة KDE](#مشاكل_Open_containing_folder_في_واجهة_KDE)
    *   [5.4 استمرار فايرفوكس في إنشاء الدليل Desktop/~ حتى ولو لم يكن مطلوبا](#استمرار_فايرفوكس_في_إنشاء_الدليل_Desktop/~_حتى_ولو_لم_يكن_مطلوبا)
    *   [5.5 إلزام الإضافات بمنع النوافذ المنبثقة](#إلزام_الإضافات_بمنع_النوافذ_المنبثقة)
    *   [5.6 رسائل خطأ زر الفأرة اﻷوسط](#رسائل_خطأ_زر_الفأرة_اﻷوسط)
    *   [5.7 مفتاح Backspace لا يعمل كزر عودة](#مفتاح_Backspace_لا_يعمل_كزر_عودة)
    *   [5.8 فايرفوكس لا يتذكر بيانات تسجيل الدخول](#فايرفوكس_لا_يتذكر_بيانات_تسجيل_الدخول)
    *   [5.9 حقول الإدخال غير مقروءة مع ثيمات dark GTK+](#حقول_الإدخال_غير_مقروءة_مع_ثيمات_dark_GTK+)
    *   [5.10 مشاكل الملفات ذات الصلة](#مشاكل_الملفات_ذات_الصلة)
    *   [5.11 "هل تريد من فايرفوكس أن يحتفظ بألسنة التصفح عند بدئه المرة القادمة؟" المربع الحواري لا يظهر](#"هل_تريد_من_فايرفوكس_أن_يحتفظ_بألسنة_التصفح_عند_بدئه_المرة_القادمة؟"_المربع_الحواري_لا_يظهر)
    *   [5.12 فايرفوكس يستخدم خطوطا قبيحة في واجهته](#فايرفوكس_يستخدم_خطوطا_قبيحة_في_واجهته)
    *   [5.13 فايرفوكس يستخدم خطوطا قبيحة في صفحات معينة](#فايرفوكس_يستخدم_خطوطا_قبيحة_في_صفحات_معينة)
    *   [5.14 حل بعض مشكلات خطوط فايرفوكس بخطوط جوجل](#حل_بعض_مشكلات_خطوط_فايرفوكس_بخطوط_جوجل)
    *   [5.15 لا يمكن انسدال القائمة بعد الترقية لفايرفوكس 13](#لا_يمكن_انسدال_القائمة_بعد_الترقية_لفايرفوكس_13)
*   [6 انظر أيضا](#انظر_أيضا)

## التنصيب

متصفح firefox يُمكن تنصيبه من الحزمة [firefox](https://www.archlinux.org/packages/?name=firefox) المتوفرة من المستودعات الرسمية. هنالك عدد من الحزم اللغات متوفرة لمتصفح firefox، غير اللغة الإنكليزية الإفتراضية. حزم اللغات تُسمى عادة `firefox-i18n-languagecode`. حيث `languagecode` يمكن أن يكون الكود الخاص بالغة ar,fr أو ja ...الخ . للحصول على قائمة كاملة باسماء الحزم يمكنك الرجوع الى الرابط [التالي](https://www.archlinux.org/packages/?sort=&q=firefox-i18n&maintainer=&last_update=&flagged=&limit=100).

إذا لم يقم firefox بإظهار حواف ناعمة للخطوط، قم بمحاولة تنصيب حزمة الخطوط [ttf-win7-fonts](https://aur.archlinux.org/packages/ttf-win7-fonts/) أو [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) ومن ثم قم بإلقاء نظرة على إعدادت الخطوط.

## الملحقات add-ons

إن متصفح firefox مشهور بعدد الملحقات الكبير الذي يمكن تنصيبها عليه والتي تجلب مزايا جديدة أو تُعدل سلوك مزايا موجودة مُسبقًا في firefox. يمكنك الحصول على محلقات جديدة أو التحكم في المحلقات المُنصبة مُستخدمًا "مدير المحلقات" الخاص بمتصفح firefox. للحصول على قائمة بإشهر المحلقات راجع الصفحة التالية [Mozilla's add-on list sorted by popularity](https://addons.mozilla.org/en-US/firefox/extensions/?sort=popular).

## الإضافات plugins

لكي تعرف ما هي الإضافات المُنصبة على متصفح firefox قم بإدخال :

```
about:plugins

```

في شريط العنوان، أو بالذهاب الى قيد *Add-ons* في القوائم ومن ثم قم بتحديد لسان *Plugins*

### التكامل مع حافظة مفاتيح GNOME

قم بتثبيت [firefox-gnome-keyring](https://aur.archlinux.org/packages/firefox-gnome-keyring/) من مستودع [AUR](/index.php/AUR "AUR") لعمل تكامل فايرفوكس مع حافظة مفاتيح [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring"). لجعل firefox-gnome-keyring يستخدم سلسلة مفاتيحك الخاصة بتسجيل الدخول ، قم بتعديل قيمة extensions.gnome-keyring.keyringName إلى "login" (بدون علامات اقتباس) في صفحة about:config. لاحظ الحرف الصغير 'l' رغم أن الاسم في keychain يحتوي على حرف كبير 'L' في الحافظة Seahorse.

### التكامل مع KDE

*   لإستخدام تكنولوجيا الخاصة بـ KPart مع متصفح firefox، عن طريق دمج عدة عوارض للملفات في المتصفح، يمكنك تنصيب حزمة [kpartsplugin](https://www.archlinux.org/packages/?name=kpartsplugin).
*   للحصول على تكامل أكثر مع ثيمة Oxygen يمكنك تنصيب [Oxygen KDE](http://kde-look.org/content/show.php/?content=117962) التي تدعم عددًا كبيرًا من الثيمات الخاصة بمتصفح firefrox بالإضافة الى الأيقونات وغيرها.
*   لمزيد من التكامل مع mime type الخاص بمربعات الحوار في KDE، يمكنك استخدام [version of firefox](https://aur.archlinux.org/packages/firefox-kde-opensuse) الذي يأتي مع رقع OpenSUSE.

### القواميس لتصحيح مدخلات المستخدم

لكي تقوم بتفعيل التدقيق اللغوي للغة مُحددة، قم بالنقر بالزر الأيمن للفأرة على مربع النص وقم بتفعيل خيار *Check Spelling*. لكي تُحدد اللغة التي سيتم التدقيق اللغوي فيها قم بالضغط مرة اخرى بالزر الأيمن وقم بتحديد لغتك من القائمة الفرعية المُعنونة *Languages*. للحصول على لغات غضافية قم بالضغط على *Add Dictionaries...* و من ثم قم بتحديد اللغة التي تريد تنصيبها من الخيارات.

بشكل بديل، يمكنك تنصيب حزمة [hunspell](https://www.archlinux.org/packages/?name=hunspell) المتوفرة في المستودعات الرسمية، ويتوجب عليك بعدها تنصيب القواميس الخاصة بلغتك كحزمة [hunspell-ar](https://aur.archlinux.org/packages/hunspell-ar/) للغة العربية و حزمة [hunspell-fr](https://www.archlinux.org/packages/?name=hunspell-fr) للغة الفرنسية. بشكل إفتراضي، fireofx يقوم بإنشاء روابط الى جميع قواميس hunspell الموجودة في `/usr/lib/firefox/dictionaries`. إذا اردت الحصول على قواميس أقل في القائمة المتوفرة في المتصفح، يُمكنك حذف بعض من هذه الروابط. لكن كن مدركًا أن تحديث المتصفح سيقوم بإعادة الروابط التي تم حذفها.

### إضافة مُحركات بحث الى متصفح firefox

مُحركات البحث يُمكن إضافتها كملحقات عادية، راجع المقال التالي [this page](https://addons.mozilla.org/en-US/firefox/search-tools/) for a list of available search engines. قائمة كبيرة جدًا بمجركات البحث يمكن أيجادها [هنا](http://mycroft.mozdev.org/). أيضًا يُمكنك إستخدام المحلق [add-to-searchbar](https://firefox.maltekraus.de/extensions/add-to-search-bar) لإضافة محركات البحث الموجودة في أي موقع الى شريط البحث الخاص بك عن طريق الضغط عليه بالزر الأيمن للفأرة وتحديد الخيار *Add to Search Bar...*. إذا أردت إضافة مُحركات البحث يدويًا يمكنك إلقاء نظرة على الملف `~/.mozilla/firefox/profile-id.default/searchplugins/` (حيث profile-id هو profile ID الخاص بك).

#### حزمة arch-firefox-search

يُمكنك تنصيب حزمة [arch-firefox-search](https://aur.archlinux.org/packages/arch-firefox-search/) المتوفرة في المستودعات الرسمية، لإضافة حقل بحث خاص بأرتش لينكس (AUR، الوكي، المنتدى...الخ) في متصفح firefox.

## مشتقات المتصفح فايرفوكس

*   **[Iceweasel](https://en.wikipedia.org/wiki/Mozilla_Corporation_software_rebranded_by_the_Debian_project#IceWeasel "wikipedia:Mozilla Corporation software rebranded by the Debian project")** — نسخة متفرعة من firefox تم تطويرها من قبل فريق عمل debian، لا تحوي على أي علامات تجارية أو شعارات خاصة بشركة Mozilla.

	[http://wiki.debian.org/Iceweasel](http://wiki.debian.org/Iceweasel) || [iceweasel](https://aur.archlinux.org/packages/iceweasel/)

**Note:** gl.d] لمزيد من المعلومات حول Iceweasel راجع [التدوينة التالية](http://web.glandium.org/blog/?p=97).

*   **[GNU IceCat](https://en.wikipedia.org/wiki/Gnu_IceCat "wikipedia:Gnu IceCat")** — متصفح ويب تم تطويره من قبل مشروع GNU، يحوي فقط على برمجيات حرة ومتوافق تمامًا مع انظمة GNU/Linux و الإضافات الخاصة بمتصفح firfox.

	[http://www.gnu.org/software/gnuzilla/](http://www.gnu.org/software/gnuzilla/) || [icecat](https://aur.archlinux.org/packages/icecat/)

*   **Firefox KDE** — نسخة من متصفح firefox يحوي على رقعة من OpenSUSE لتحقيق أكبر قد من التكامل مع واجهة KDE.

	[http://gitorious.org/firefox-kde-opensuse](http://gitorious.org/firefox-kde-opensuse) || [firefox-kde-opensuse](https://aur.archlinux.org/packages/firefox-kde-opensuse/)

## إسكتشاف الأخطاء و إصلاحها

### تحديد عميل البريد الإلكتروني الخاص بك

يقوم firefox عادةً بفتح روابط `mailto` بإستخدام تطبيقات الويب كتطبيق Gmail أو Yahoo. لتحديد عميل البريد الإلكتروني المُفضل لديك في firefox الذي ستم فتحه عند الضغط على روابط `mailto`، قم بالذهاب الى *Preferences > Applications* وقم بتعديل حقل *action* الخاص بنوع المحتوى `mailto`. بالطبع يتوجب عليك تحديد المسار الكامل لعميل البريد الإلكتروني (على سبيل المثال `/usr/bin/kmail` لبرنامج Kmail).

### مشاكل Open containing folder في واجهة GNOME3

إذا كنت تتوقع تشغيل متصفح الملفات [GNOME Files](/index.php/GNOME_Files "GNOME Files") عندما تقوم بالضغط على خيار "Open Containing Folder" في مدير التنزيلات، لكن متصفح ملفات [Thunar](/index.php/Thunar "Thunar") أو [Wine](/index.php/Wine "Wine") يتم تشغيله عوضًا عنه، يمكنك التحقق من السطرين التاليين في ملف `~/.local/share/applications/defaults.list`:

```
 inode/directory=<someprogram>.desktop
 x-directory/normal=<someprogram>.desktop

```

إذا كانت قيمة `<someprogram>` ليست `nautilus`، فقم بتغييرها الى ذلك.

### مشاكل Open containing folder في واجهة KDE

اذا كنت تتوقع تشغيل متصفح الملفات المُفضل لديك عندما تقوم بالضغط على خيار "Open Containing Folder" في مدير التنزيلات، لكن متصفح ملفات آخر تم تشغيله عوضًا عنه، يمكنك إستخدام متصفح الملفات المفضل لديك وليكن Dolphin في لوحة التحكم الخاصة بكدي تحت *Workspace Appearance and Behavior > Default Applications > File Manager*. إذا كان firefox ما يزال لا يفتح المجلدات بمتصفح الملفات الذي تُفضل قم بتعديل الملف التالي مُضمنًا السطرين التاليين :

```
x-directory/normal=kde4-dolphin.desktop;kde4-kfmclient_dir.desktop;
inode/directory=kde4-dolphin.desktop;kde4-kfmclient_dir.desktop;kde4-gwenview.desktop;kde4-filelight.desktop;kde4-cervisia.desktop;

```

### استمرار فايرفوكس في إنشاء الدليل Desktop/~ حتى ولو لم يكن مطلوبا

متصفح firefox يستخدم `~/Desktop` كمكان افتراضي للملفات المحملة والمرفوعة. يمكنك وضعها الى مجلد آخر عن طريق إنشاء ملف `~/.config/user-dirs.dirs` وإضافة الأسطر التالية إليه :

```
XDG_DESKTOP_DIR="/home/<user>/"
XDG_DOWNLOAD_DIR="/home/<user>/<dir>"
XDG_TEMPLATES_DIR="/home/<user>/<dir>"
XDG_PUBLICSHARE_DIR="/home/<user>/<dir>"
XDG_DOCUMENTS_DIR="/home/<user>/<dir>"
XDG_MUSIC_DIR="/home/<user>/<dir>"
XDG_PICTURES_DIR="/home/<user>/<dir>"
XDG_VIDEOS_DIR="/home/<user>/<dir>"

```

قم بتغيير `<user>` و `<dir>` إلى المجلد الفعلي لديك.

### إلزام الإضافات بمنع النوافذ المنبثقة

بعض الإضافات تقوم بتجاوز الإعدادات الإفتراضية، كإضافة Flash. لذا يمكنك منع ذلك عن طريق التالي :

1.  قم بكتابة `about:config` في شريط العنوان.
2.  قم بالضغط بالزر الأيمن للفأرة وقم بالنقر على `New` ومن ثم النقر على `Integer`.
3.  قم بتسمة الخاصية الجديدة `privacy.popups.disable_from_plugins`.
4.  قم بتحديد قيمتها الى 2.

القيم المُمكنة هي :

*   **0**: قم بالسماح بالنوافذ المنبثقة من جميع الإضافات.
*   **1**: قم بالسماح بالنوافذ المنبثقة لكن قم بتحديدهم بقيمة الخيار dom.popup_maximum.
*   **2**: قم بمنع النوافذ المنبثقة من الإضافات.
*   **3**: قم بمنع النوافذ المنبثقة من الإضافاتن حتى في المواقع المسموح بها.

### رسائل خطأ زر الفأرة اﻷوسط

رسالة خطأ شهيرة تنتج عن الضغط على زر الفأرة الأوسط هي :

```
The URL is not valid and cannot be loaded.

```

أيضًا قد يحدث سلوك غير متوقع عند الضغط على الزر الأوسط، كفتح صفحة عشوائية.

السبب وراء هذه المشكلة هو طريقة إستخدام زر الفأرة الأوسط في الانظمة الشبيهة باليونكس. الزر الأوسط يقوم بلصق النص الذي تم تحديده أو نسخه الى الحافظة. لربما يحدث إلتباس في firefox الذي يكون السلوك الإفتراضي هو فتح الرابط الذي تم الضغط عليه في لسان جديد. يمكن تعطيل هذه الميزة عن طريق الذهاب الى `about:config` وتحديد قيمة الخيار `middlemouse.contentLoadURL` الى القيمة**false**.

بشكل آخر، إذا أردت إستعادة التمرير بإستخدام الزر الأوسط (السلوك الإفتراضي في نظام windows). يمكن تفعيل ذلك بالبحث عن الخيار `general.autoScroll` وتحديد قيمةته الى القيمة **true**.

### مفتاح Backspace لا يعمل كزر عودة

حسب [هذا المقال](http://ubuntu.wordpress.com/2006/12/21/fix-firefox-backspace-to-take-you-to-the-previous-page/)، فإن هذه الميزة تمت إزالتها لحل علّة في المتصفح. لكي تُعيد سلوكها الى ما كانت عليه قم بالذهاب الى `about:config` وتحديد قيمة الخيار `browser.backspace_action` الى القيمة صفر **0**

### فايرفوكس لا يتذكر بيانات تسجيل الدخول

بسبب حدوث عطب في ملف `cookies.sqlite` الموجود في مجلد [Firefox's profile](http://support.mozilla.com/en-US/kb/Profiles#How_to_find_your_profile). لكي تحل هذه المشكلة قم بإعادة تسمية أو حذف ملف `cookie.sqlite` عندما يكون متصفح firefxo مغلقًا.

قم بفتح الطرفية وكتالبة هذه الأوامر فيها :

```
$ cd ~/.mozilla/firefox/xxxxxxxx.default/
$ rm -f cookies.sqlite

```

**Note:** xxxxxxxx تعني ثمانية محارف عشوائية.

قم الآن بإعادة تشغيل firefox وانظر هل تم حل المشكلة أم لا.

### حقول الإدخال غير مقروءة مع ثيمات dark GTK+

عندما تقوم بإستخدام ثيمات [GTK+](/index.php/GTK%2B "GTK+") داكنة للون، ربما تظهر بعض الحقول في صفحات الويب بشكل غير مقروء (على سبيل المثال الخط ابيض على خلفية بيضاء في موقع Amazon). هذا يحدث عندما يقوم الموقع بتحديد لون الخلفية أو النص فقط، ويقوم firefox بإخد القيمة الاخرى من الثيمة.

لحل هذه المشكلة يجب عليك تحديد قيمة معيارية للألوان في جميع الصفحات في ملف `~/.mozilla/firefox/xxxxxxxx.default/chrome/userContent.css`.

التالي يقوم بتحديد لون أسود على خلفية بيضاء لجميع حقول النص في نماذج HTML، كلا اللونين يمكن تحديد قيمته من قبل الموقع الذي تتم زيارته، لذا فإن الالوان تظهر كما يجب:

```
input {
    -moz-appearance: none !important;
    background-color: white;
    color: black;
}

textarea {
    -moz-appearance: none !important;
    background-color: white;
    color: black;
}

select {
    -moz-appearance: none !important;
    background-color: white;
    color: black;
}

```

الكود التالي سيجبر إستخدام الألوان من قبل جميع الصفحات :

```
input {
    -moz-appearance: none !important;
    background-color: pink !important;
    color: green !important;
}

textarea {
    -moz-appearance: none !important;
    background-color: pink !important;
    color: green !important;
}

select {
    -moz-appearance: none !important;
    background-color: pink !important;
    color: green !important;
}

```

قم بتغيير قيم الألوان الى أن تلائم إحتياجاتك، أو بإمكانك إستخدام إضافة [Stylish](https://addons.mozilla.org/en-US/firefox/addon/2108)

### مشاكل الملفات ذات الصلة

للمستخدمين الذين لا يستخدمون واجهة [GNOME](/index.php/GNOME "GNOME")، متصفح firefox قد لا يقوم بربط البرامج بشكل صحيح، لحل المشكلة قم بتنصيب حزمة [libgnome](https://aur.archlinux.org/packages/libgnome/) من المستودعات الرسمية.

إذا كنت تستخدم واجهة KDE يمكنك أيضًا القيام بالتالي :

```
ln -s ~/.local/share/applications/mimeapps.list ~/.local/share/applications/mimeinfo.cache

```

الآن متصفح firefox يجب أن يقوم بتشغيل البرمجيات الصحيحة.

### "هل تريد من فايرفوكس أن يحتفظ بألسنة التصفح عند بدئه المرة القادمة؟" المربع الحواري لا يظهر

من موقع [Mozilla Support](http://support.mozilla.com/en-US/questions/767751) :

1.  اكتب `about:config` in the address bar.
2.  اضبط `browser.warnOnQuit` على **true**.
3.  اضبط `browser.showQuitWarning` على **true**.

### فايرفوكس يستخدم خطوطا قبيحة في واجهته

إذا شعرت بأن الخطوط التي يستخدمها متصفح firefox قبيحة. هنالك إحتمال بأنه ينقصك خطوط أجمل في firefox. ببساطة قم بتنصيب خطوط "Type 1" من حزمة [xorg-fonts-type1](https://www.archlinux.org/packages/?name=xorg-fonts-type1) المتوفرة في المستودعات الرسمية.

### فايرفوكس يستخدم خطوطا قبيحة في صفحات معينة

عندما يستخدم متصفح firefox خطوط نقطية، ينتج عن ذلك خطوط قبيحة جدًا في عدد من الصفحات مقارنةً مع متصفح Google Chrome على سبيل المثال :

[http://i.imgur.com/SMVdi.png](http://i.imgur.com/SMVdi.png) vs [http://i.imgur.com/jNmxU.png](http://i.imgur.com/jNmxU.png)

لحل هذه المشكلة ، قم بإلغاء تفعيل الخطوط النقطية لمخدم العرض X :

```
# ln -s /etc/fonts/conf.avail/70-no-bitmaps.conf /etc/fonts/conf.d/

```

### حل بعض مشكلات خطوط فايرفوكس بخطوط جوجل

بعض مشكلات الخطوط في متصفح firefox يُمكن حلها عن طريق تنصيب خطوط Google من حزم AUR [ttf-google-fonts-hg](https://aur.archlinux.org/packages/ttf-google-fonts-hg/) أو [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/). هذه الخطوط ستقوم بتحسين عرض تطبيقات Google Drive بشكل كبير.

### لا يمكن انسدال القائمة بعد الترقية لفايرفوكس 13

هذه المشكلة متعلقة [بهذه العلة](https://bugzilla.mozilla.org/show_bug.cgi?id=787943)، هذه العلة قد تؤثر على أي مستخدم يقوم بهذا الضبط :

```
GTK_IM_MODULE=xim

```

عندما يقوم بتهيئة إعدادات الإدخال.

## انظر أيضا

*   [Official Website](http://www.mozilla.org/firefox/)
*   [Mozilla Foundation](http://www.mozilla.org/)
*   [Firefox Wiki](https://wiki.mozilla.org/Firefox)
*   [Firefox Add-ons](https://addons.mozilla.org/)
*   [Firefox Persona Themes](http://www.getpersonas.com/)