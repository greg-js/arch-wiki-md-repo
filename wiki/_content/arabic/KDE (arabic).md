**ملاحظة:** ما زالت هذه المقالة قيد الترجمة.

من [KDE Software Compilation](http://www.kde.org/community/whatiskde/softwarecompilation.php) و [Getting KDE Software](http://www.kde.org/download/):

	*The KDE Software Compilation is the set of frameworks, workspaces, and applications produced by KDE to create a beautiful, functional and free desktop computing environment for Linux and similar operating systems. It consists of a large number of individual applications and a desktop workspace as a shell to run these applications.*

The KDE upstream has a well maintained [UserBase wiki](http://userbase.kde.org/). Users can get detailed information about most KDE applications there.

## Contents

*   [1 التثبيت](#.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA)
    *   [1.1 التثبيت الكامل](#.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_.D8.A7.D9.84.D9.83.D8.A7.D9.85.D9.84)
    *   [1.2 التثبيت الأدنى](#.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_.D8.A7.D9.84.D8.A3.D8.AF.D9.86.D9.89)
    *   [1.3 حزمة اللغة](#.D8.AD.D8.B2.D9.85.D8.A9_.D8.A7.D9.84.D9.84.D8.BA.D8.A9)
*   [2 الترقية](#.D8.A7.D9.84.D8.AA.D8.B1.D9.82.D9.8A.D8.A9)
*   [3 بدء كدي](#.D8.A8.D8.AF.D8.A1_.D9.83.D8.AF.D9.8A)
    *   [3.1 استخدام مدير عرض](#.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_.D9.85.D8.AF.D9.8A.D8.B1_.D8.B9.D8.B1.D8.B6)
        *   [3.1.1 KDM (مدير عرض كدي)](#KDM_.28.D9.85.D8.AF.D9.8A.D8.B1_.D8.B9.D8.B1.D8.B6_.D9.83.D8.AF.D9.8A.29)
    *   [3.2 استخدام xinitrc](#.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_xinitrc)
*   [4 الضبط](#.D8.A7.D9.84.D8.B6.D8.A8.D8.B7)
    *   [4.1 التخصيص](#.D8.A7.D9.84.D8.AA.D8.AE.D8.B5.D9.8A.D8.B5)
        *   [4.1.1 سطح مكتب بلازما](#.D8.B3.D8.B7.D8.AD_.D9.85.D9.83.D8.AA.D8.A8_.D8.A8.D9.84.D8.A7.D8.B2.D9.85.D8.A7)
            *   [4.1.1.1 السمات](#.D8.A7.D9.84.D8.B3.D9.85.D8.A7.D8.AA)
            *   [4.1.1.2 الودجات](#.D8.A7.D9.84.D9.88.D8.AF.D8.AC.D8.A7.D8.AA)
            *   [4.1.1.3 بريمج الصوت في صينية النظام](#.D8.A8.D8.B1.D9.8A.D9.85.D8.AC_.D8.A7.D9.84.D8.B5.D9.88.D8.AA_.D9.81.D9.8A_.D8.B5.D9.8A.D9.86.D9.8A.D8.A9_.D8.A7.D9.84.D9.86.D8.B8.D8.A7.D9.85)
            *   [4.1.1.4 إضافة قائمة Global إلى سطح المكتب](#.D8.A5.D8.B6.D8.A7.D9.81.D8.A9_.D9.82.D8.A7.D8.A6.D9.85.D8.A9_Global_.D8.A5.D9.84.D9.89_.D8.B3.D8.B7.D8.AD_.D8.A7.D9.84.D9.85.D9.83.D8.AA.D8.A8)
        *   [4.1.2 زخارف النوافذ](#.D8.B2.D8.AE.D8.A7.D8.B1.D9.81_.D8.A7.D9.84.D9.86.D9.88.D8.A7.D9.81.D8.B0)
        *   [4.1.3 سمات الأيقونات](#.D8.B3.D9.85.D8.A7.D8.AA_.D8.A7.D9.84.D8.A3.D9.8A.D9.82.D9.88.D9.86.D8.A7.D8.AA)
        *   [4.1.4 الخطوط](#.D8.A7.D9.84.D8.AE.D8.B7.D9.88.D8.B7)
            *   [4.1.4.1 الخطوط في كدي تبدو رديئة](#.D8.A7.D9.84.D8.AE.D8.B7.D9.88.D8.B7_.D9.81.D9.8A_.D9.83.D8.AF.D9.8A_.D8.AA.D8.A8.D8.AF.D9.88_.D8.B1.D8.AF.D9.8A.D8.A6.D8.A9)
            *   [4.1.4.2 الخطوط ضخمة أو تبدو غير متناسبة](#.D8.A7.D9.84.D8.AE.D8.B7.D9.88.D8.B7_.D8.B6.D8.AE.D9.85.D8.A9_.D8.A3.D9.88_.D8.AA.D8.A8.D8.AF.D9.88_.D8.BA.D9.8A.D8.B1_.D9.85.D8.AA.D9.86.D8.A7.D8.B3.D8.A8.D8.A9)
        *   [4.1.5 كفاءة المساحة](#.D9.83.D9.81.D8.A7.D8.A1.D8.A9_.D8.A7.D9.84.D9.85.D8.B3.D8.A7.D8.AD.D8.A9)
    *   [4.2 الشبكة](#.D8.A7.D9.84.D8.B4.D8.A8.D9.83.D8.A9)
    *   [4.3 الطباعة](#.D8.A7.D9.84.D8.B7.D8.A8.D8.A7.D8.B9.D8.A9)
    *   [4.4 دعم سامبا/ويندوز](#.D8.AF.D8.B9.D9.85_.D8.B3.D8.A7.D9.85.D8.A8.D8.A7.2F.D9.88.D9.8A.D9.86.D8.AF.D9.88.D8.B2)
    *   [4.5 أنشطة سطح مكتب كدي](#.D8.A3.D9.86.D8.B4.D8.B7.D8.A9_.D8.B3.D8.B7.D8.AD_.D9.85.D9.83.D8.AA.D8.A8_.D9.83.D8.AF.D9.8A)
    *   [4.6 حفظ الطاقة](#.D8.AD.D9.81.D8.B8_.D8.A7.D9.84.D8.B7.D8.A7.D9.82.D8.A9)
    *   [4.7 مراقبة التغييرات على الملفات والمجلدات المحلية](#.D9.85.D8.B1.D8.A7.D9.82.D8.A8.D8.A9_.D8.A7.D9.84.D8.AA.D8.BA.D9.8A.D9.8A.D8.B1.D8.A7.D8.AA_.D8.B9.D9.84.D9.89_.D8.A7.D9.84.D9.85.D9.84.D9.81.D8.A7.D8.AA_.D9.88.D8.A7.D9.84.D9.85.D8.AC.D9.84.D8.AF.D8.A7.D8.AA_.D8.A7.D9.84.D9.85.D8.AD.D9.84.D9.8A.D8.A9)
*   [5 إدارة النظام](#.D8.A5.D8.AF.D8.A7.D8.B1.D8.A9_.D8.A7.D9.84.D9.86.D8.B8.D8.A7.D9.85)
    *   [5.1 ضبط لوحة المفاتيح](#.D8.B6.D8.A8.D8.B7_.D9.84.D9.88.D8.AD.D8.A9_.D8.A7.D9.84.D9.85.D9.81.D8.A7.D8.AA.D9.8A.D8.AD)
    *   [5.2 إنهاء خدمة Xorg عبر إعدادات نظام كدي](#.D8.A5.D9.86.D9.87.D8.A7.D8.A1_.D8.AE.D8.AF.D9.85.D8.A9_Xorg_.D8.B9.D8.A8.D8.B1_.D8.A5.D8.B9.D8.AF.D8.A7.D8.AF.D8.A7.D8.AA_.D9.86.D8.B8.D8.A7.D9.85_.D9.83.D8.AF.D9.8A)
    *   [5.3 وحدة الضبط لِكدي](#.D9.88.D8.AD.D8.AF.D8.A9_.D8.A7.D9.84.D8.B6.D8.A8.D8.B7_.D9.84.D9.90.D9.83.D8.AF.D9.8A)
*   [6 بحث سطح المكتب وسطح المكتب الدلالي (Semantic desktop)](#.D8.A8.D8.AD.D8.AB_.D8.B3.D8.B7.D8.AD_.D8.A7.D9.84.D9.85.D9.83.D8.AA.D8.A8_.D9.88.D8.B3.D8.B7.D8.AD_.D8.A7.D9.84.D9.85.D9.83.D8.AA.D8.A8_.D8.A7.D9.84.D8.AF.D9.84.D8.A7.D9.84.D9.8A_.28Semantic_desktop.29)
    *   [6.1 Virtuoso و Soprano](#Virtuoso_.D9.88_Soprano)
    *   [6.2 نبومك](#.D9.86.D8.A8.D9.88.D9.85.D9.83)
        *   [6.2.1 استخدام نبومك وضبطه](#.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_.D9.86.D8.A8.D9.88.D9.85.D9.83_.D9.88.D8.B6.D8.A8.D8.B7.D9.87)
        *   [6.2.2 كدي دون نبومك](#.D9.83.D8.AF.D9.8A_.D8.AF.D9.88.D9.86_.D9.86.D8.A8.D9.88.D9.85.D9.83)
    *   [6.3 أكوندا](#.D8.A3.D9.83.D9.88.D9.86.D8.AF.D8.A7)
        *   [6.3.1 تعطيل أكوندا](#.D8.AA.D8.B9.D8.B7.D9.8A.D9.84_.D8.A3.D9.83.D9.88.D9.86.D8.AF.D8.A7)
        *   [6.3.2 ضبط قاعدة البيانات](#.D8.B6.D8.A8.D8.B7_.D9.82.D8.A7.D8.B9.D8.AF.D8.A9_.D8.A7.D9.84.D8.A8.D9.8A.D8.A7.D9.86.D8.A7.D8.AA)
        *   [6.3.3 تشغيل كدي دون أكوندا](#.D8.AA.D8.B4.D8.BA.D9.8A.D9.84_.D9.83.D8.AF.D9.8A_.D8.AF.D9.88.D9.86_.D8.A3.D9.83.D9.88.D9.86.D8.AF.D8.A7)
*   [7 فونون](#.D9.81.D9.88.D9.86.D9.88.D9.86)
    *   [7.1 ما فونون؟](#.D9.85.D8.A7_.D9.81.D9.88.D9.86.D9.88.D9.86.D8.9F)
    *   [7.2 أيَّ سند ( backend) عليَّ استخدامه؟](#.D8.A3.D9.8A.D9.8E.D9.91_.D8.B3.D9.86.D8.AF_.28_backend.29_.D8.B9.D9.84.D9.8A.D9.8E.D9.91_.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85.D9.87.D8.9F)
*   [8 تطبيقات مفيدة](#.D8.AA.D8.B7.D8.A8.D9.8A.D9.82.D8.A7.D8.AA_.D9.85.D9.81.D9.8A.D8.AF.D8.A9)
    *   [8.1 Yakuake](#Yakuake)
    *   [8.2 كدي تيليباثي](#.D9.83.D8.AF.D9.8A_.D8.AA.D9.8A.D9.84.D9.8A.D8.A8.D8.A7.D8.AB.D9.8A)
*   [9 تلميحات وخُدَع](#.D8.AA.D9.84.D9.85.D9.8A.D8.AD.D8.A7.D8.AA_.D9.88.D8.AE.D9.8F.D8.AF.D9.8E.D8.B9)
    *   [9.1 استخدام أوبن بوكس في كدي](#.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_.D8.A3.D9.88.D8.A8.D9.86_.D8.A8.D9.88.D9.83.D8.B3_.D9.81.D9.8A_.D9.83.D8.AF.D9.8A)
        *   [9.1.1 عند استخدام KDM](#.D8.B9.D9.86.D8.AF_.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_KDM)
        *   [9.1.2 إعادة تمكين تأثيرات التركيب](#.D8.A5.D8.B9.D8.A7.D8.AF.D8.A9_.D8.AA.D9.85.D9.83.D9.8A.D9.86_.D8.AA.D8.A3.D8.AB.D9.8A.D8.B1.D8.A7.D8.AA_.D8.A7.D9.84.D8.AA.D8.B1.D9.83.D9.8A.D8.A8)
    *   [9.2 تكامل أندرويد مع سطح المكتب كدي](#.D8.AA.D9.83.D8.A7.D9.85.D9.84_.D8.A3.D9.86.D8.AF.D8.B1.D9.88.D9.8A.D8.AF_.D9.85.D8.B9_.D8.B3.D8.B7.D8.AD_.D8.A7.D9.84.D9.85.D9.83.D8.AA.D8.A8_.D9.83.D8.AF.D9.8A)
    *   [9.3 الحصول على الإخطارات لتحديثات البرمجيات](#.D8.A7.D9.84.D8.AD.D8.B5.D9.88.D9.84_.D8.B9.D9.84.D9.89_.D8.A7.D9.84.D8.A5.D8.AE.D8.B7.D8.A7.D8.B1.D8.A7.D8.AA_.D9.84.D8.AA.D8.AD.D8.AF.D9.8A.D8.AB.D8.A7.D8.AA_.D8.A7.D9.84.D8.A8.D8.B1.D9.85.D8.AC.D9.8A.D8.A7.D8.AA)
    *   [9.4 ضبط KWin لاستخدام OpenGL ES](#.D8.B6.D8.A8.D8.B7_KWin_.D9.84.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_OpenGL_ES)
    *   [9.5 تمكن مصغّرات الصوت مع مديريّ الملفات كنكر/دولفين](#.D8.AA.D9.85.D9.83.D9.86_.D9.85.D8.B5.D8.BA.D9.91.D8.B1.D8.A7.D8.AA_.D8.A7.D9.84.D8.B5.D9.88.D8.AA_.D9.85.D8.B9_.D9.85.D8.AF.D9.8A.D8.B1.D9.8A.D9.91_.D8.A7.D9.84.D9.85.D9.84.D9.81.D8.A7.D8.AA_.D9.83.D9.86.D9.83.D8.B1.2F.D8.AF.D9.88.D9.84.D9.81.D9.8A.D9.86)
    *   [9.6 تمكن مصغّرات الفيديو مع مديريّ الملفات كنكر/دولفين](#.D8.AA.D9.85.D9.83.D9.86_.D9.85.D8.B5.D8.BA.D9.91.D8.B1.D8.A7.D8.AA_.D8.A7.D9.84.D9.81.D9.8A.D8.AF.D9.8A.D9.88_.D9.85.D8.B9_.D9.85.D8.AF.D9.8A.D8.B1.D9.8A.D9.91_.D8.A7.D9.84.D9.85.D9.84.D9.81.D8.A7.D8.AA_.D9.83.D9.86.D9.83.D8.B1.2F.D8.AF.D9.88.D9.84.D9.81.D9.8A.D9.86)
    *   [9.7 تسريع بدء تشغيل التطبيق](#.D8.AA.D8.B3.D8.B1.D9.8A.D8.B9_.D8.A8.D8.AF.D8.A1_.D8.AA.D8.B4.D8.BA.D9.8A.D9.84_.D8.A7.D9.84.D8.AA.D8.B7.D8.A8.D9.8A.D9.82)
    *   [9.8 إخفاء الأقسام](#.D8.A5.D8.AE.D9.81.D8.A7.D8.A1_.D8.A7.D9.84.D8.A3.D9.82.D8.B3.D8.A7.D9.85)
    *   [9.9 نصائح كنكر](#.D9.86.D8.B5.D8.A7.D8.A6.D8.AD_.D9.83.D9.86.D9.83.D8.B1)
        *   [9.9.1 تعطيل تلميحات المفتاح الذكي (المتصفّح)](#.D8.AA.D8.B9.D8.B7.D9.8A.D9.84_.D8.AA.D9.84.D9.85.D9.8A.D8.AD.D8.A7.D8.AA_.D8.A7.D9.84.D9.85.D9.81.D8.AA.D8.A7.D8.AD_.D8.A7.D9.84.D8.B0.D9.83.D9.8A_.28.D8.A7.D9.84.D9.85.D8.AA.D8.B5.D9.81.D9.91.D8.AD.29)
        *   [9.9.2 استخدام عُدَّة الوِب](#.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_.D8.B9.D9.8F.D8.AF.D9.8E.D9.91.D8.A9_.D8.A7.D9.84.D9.88.D9.90.D8.A8)
    *   [9.10 التكامل مع فَيَرفُكس](#.D8.A7.D9.84.D8.AA.D9.83.D8.A7.D9.85.D9.84_.D9.85.D8.B9_.D9.81.D9.8E.D9.8A.D9.8E.D8.B1.D9.81.D9.8F.D9.83.D8.B3)
    *   [9.11 تعيين خلفية حافظة الشاشة إلى نفس الحالية](#.D8.AA.D8.B9.D9.8A.D9.8A.D9.86_.D8.AE.D9.84.D9.81.D9.8A.D8.A9_.D8.AD.D8.A7.D9.81.D8.B8.D8.A9_.D8.A7.D9.84.D8.B4.D8.A7.D8.B4.D8.A9_.D8.A5.D9.84.D9.89_.D9.86.D9.81.D8.B3_.D8.A7.D9.84.D8.AD.D8.A7.D9.84.D9.8A.D8.A9)
    *   [9.12 تعيين خلفية شاشة القفل إلى صورة arbitrary](#.D8.AA.D8.B9.D9.8A.D9.8A.D9.86_.D8.AE.D9.84.D9.81.D9.8A.D8.A9_.D8.B4.D8.A7.D8.B4.D8.A9_.D8.A7.D9.84.D9.82.D9.81.D9.84_.D8.A5.D9.84.D9.89_.D8.B5.D9.88.D8.B1.D8.A9_arbitrary)

## التثبيت

قبل تثبيت كدي، تأكّد من وجود تثبيت [Xorg](/index.php/Xorg "Xorg") يعمل على نظامك. كدي 4.س "مرنة". يمكنك تثبيت مجموعة كاملة من الحزم أو فقط تطبيقات كدي المفضّلة لديك.

### التثبيت الكامل

[ثبّت](/index.php/Pacman_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9) "Pacman (العربية)") [kde](https://www.archlinux.org/groups/x86_64/kde/) أو [kde-meta](https://www.archlinux.org/groups/x86_64/kde-meta/) المتوفّرتان في [المستودعات الرسمية](/index.php/Official_repositories_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9) "Official repositories (العربية)"). للفروق بين [kde](https://www.archlinux.org/groups/x86_64/kde/) و [kde-meta](https://www.archlinux.org/groups/x86_64/kde-meta/) طالع مقالة [KDE Packages](/index.php/KDE_Packages "KDE Packages").

### التثبيت الأدنى

إن أردت minimal installation of the KDE Software Compilation, ثبّت [kdebase](https://www.archlinux.org/groups/x86_64/kdebase/).

### حزمة اللغة

إن أردت ملفات اللغة، ثبّت `kde-l10n-yourlanguagehere` حيث yourlanguagehere مكان اللغة التي تريدها (مثلًا [kde-l10n-de](https://www.archlinux.org/packages/?name=kde-l10n-de) للغة الألمانية).

لقائمة كاملة من اللغات المتوفّرة طالع [هذا الرابط](https://www.archlinux.org/packages/extra/any/kde-l10n/).

## الترقية

**كدي 4.12** Software Compilation هو [الإصدار الرئيسي](http://kde.org/announcements/) الحالي لِكدي. نصائح مهمة للترقية:

*   تحقّق دائمًا من أن مرآتك **محدّثة**.
*   **لا تُجبِر تحديثًا باستخدام `# pacman --force`**. إن شكا pacman عن تضاربات، فضلًا **أبلغ عن علة**.
*   يمكنك إزالة الحزم الوصفية و sub packages التي لا تحتاجها بعد التحديث.
*   إن لم تعجبك split packages، فقط تابع استخدام حزم kde-meta.

## بدء كدي

بدء كدي يعتمد على تفضيلاتك. توجد طريقتين أساسًا لبدء كدي. استخدام **KDM** أو **xinitrc**.

### استخدام مدير عرض

[مدير العرض](/index.php/Display_manager_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9) "Display manager (العربية)") أو مدير الولوج، يكون عادةً واجهة مستخدم رسومية تُعرض في نهاية تقدّم الإقلاع بدلًا من الصدفة الافتراضية. يَلِج المدير إلى كدي مباشرة بسهولة دائمًا. لِكدي مدير عرض خاص بها، KDM.

#### KDM (مدير عرض كدي)

*طالع صفحة [KDM](/index.php/KDM "KDM") لمعلومات أكثر.*

[مكّن/ابدأ](/index.php/Systemd_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9)#.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_.D8.A7.D9.84.D9.88.D8.AD.D8.AF.D8.A7.D8.AA "Systemd (العربية)") `kdm.service` لبدء مدير العرض.

### استخدام xinitrc

طالع صفحة [xinitrc](/index.php/Xinitrc "Xinitrc") لمعلومات أكثر.

 `~/.xinitrc` 
```
exec startkde

```

نفّذ `startx` أو `xinit` لبدء كدي.

**ملاحظة:** إن أردت بدء Xorg عند الإقلاع، فضلًا اقرأ مقالة [بدء X عند الولوج](/index.php/Start_X_at_login "Start X at login").

## الضبط

ضبط كدي كلّه يُحفظ في المجلد `~/.kde4`. إن كنت تواجه مشاكلًا كثيرة مع كدي أو أردت تثبيت جديد منها، فقط انسخ المجلد احتياطيًّا وأعد تسميته وأعد تشغيل جلسة X. سيعيد كدي إنشاء المجلد بملفات الضبط الافتراضية. إن أردت تحكّم دقيق لبرامج كدي، عليك بتحرير الملفات في هذا المجلد.

على أيِّ حال، ضبط كدي يتمّ في الأصل في **إعدادات النظام**. تتوفّر خيارات أخرى أيضًا في **إعدادات Default Desktop** في قائمة سياق سطح المكتب.

لخيارات تخصيص أخرى لم تُغطّى مثل الأنشطة، أكثر من خلفية لسطح المكتب على المكعب، إلخ، فضلًا ارجع إلى صفحة الويكي [بلازما](/index.php/Plasma "Plasma").

### التخصيص

كيف تضبط سطح مكتب كدي إلى نمطك الخاص: استخدام سمات بلازما المختلفة، وزخارف النوافذ وسمات الأيقونات.

#### سطح مكتب بلازما

[Plasma](/index.php/Plasma "Plasma") تقنية تكامل مع سطح المكتب والتي تُوفّر العديد من الوظائف مثل عرض خلفية سطح المكتب، وإضافة الودجات إلى سطح المكتب و handleing اللوحة(اللوحات)، أو شريط(أشرطة) الأدوات.

##### السمات

يمكن تثبيت [سمات بلازما](http://kde-look.org/index.php?xcontentmode=76) من خلال لوحة تحكّم إعدادات سطح المكتب. سمات بلازما تحدّد مظهر اللوحات و plasmoids. For easy system-wide installation, some such themes are available in both the official repositories and the [AUR](https://aur.archlinux.org/packages.php?O=0&K=plasmatheme&do_Search=Go).

##### الودجات

Plasmoids تطبيقات كدي سكرِبتية (plasmoid scripts) أو ترميزية (plasmoid binaries) مصمّمة لتعزيز وظيفة سطح المكتب.

يمكن تثبيت Plasmoid binaries باستخدام PKGBUILDs من [AUR](https://aur.archlinux.org/packages.php?O=0&K=plasmoid&do_Search=Go&PP=25&SO=d&SB=v)، أو يمكنك كتابة PKGBUILD خاصتك.

أسهل طريقة لتثبيت plasmoid scripts هي بالنقر باليمين على لوحة أو سطح مكتب:

```
أضف ودجات > Get new Widgets > نزّل ودجات بلازما جديدة

```

هذا سيقدّم واجهة جميلة لِـ [kde-look.org](http://www.kde-look.org/) تسمح لك بتثبيت، أو إزالة تثبيت أو تحديث third-party plasmoid scripts بنقرة واحدة فقط.

أغلب plasmoids لم تُنشأ رسميًّا من قِبَل مطوري كدي. يمكنك محاولة تثبيت ودجات ماك أوإس إكس، وودجات مايكروسوفت ويندوز فيستا/7، وودجات جوجل وحتى ودجات SuperKaramba.

##### بريمج الصوت في صينية النظام

ثبّت ك.مكس ([kdemultimedia-kmix](https://www.archlinux.org/packages/?name=kdemultimedia-kmix)) من المستودعات الرسمية وابدأهُ من مُطلِق التطبيقات. بما أنّ كدي -افتراضيًّا- يبدأ تشغيل البرامج من الجلسة السابقة تلقائيًّا، لا حاجة لبدءِ ك.مكس كل مرة تلِج فيها.

**ملاحظة:** لضبط [حجم الزيادة/النقصان للصوت](https://bugs.kde.org/show_bug.cgi?id=313579#c28)، أضف مثلًا `VolumePercentageStep=1` في قسم `[Global]` لِـ `~/.kde4/share/config/kmixrc`

##### إضافة قائمة Global إلى سطح المكتب

**ملاحظة:** ما زالت هذه المقالة قيد الترجمة.

#### زخارف النوافذ

[زخارف النوافذ](http://kde-look.org/index.php?xcontentmode=75) يمكن تغييرها من: إعدادات النظام > مظهر مساحة العمل > زخارف النوافذ يمكنك هناك تنزيل وتثبيت سمات أكثر بنقرة واحدة مباشرةً، وبعضها متوفّر في [AUR](https://aur.archlinux.org/packages.php?O=0&K=kdestyle&do_Search=Go&PP=25&SO=d&SB=v).

#### سمات الأيقونات

لا توجد الكثير من سمات الأيقونات لكل النظام في كدي 4\. يمكن فتح *إعدادات النظام > مظهر التطبيقات > الأيقونات* والتصفّح لسمات جديدة أو تثبيتها يدويًّا. يمكنك العثور على العديد منها من [kde-look.org](http://www.kde-look.org/).

الشعارات الرسمية، والأيقونات، ولصاقات أقراص CD والأعمال الفنية لآرتش لينكس مُزوَّدة في حزمة [archlinux-artwork](https://aur.archlinux.org/packages/archlinux-artwork/). بعد تثبيتها يمكنك العثور على الأعمال الفنية من `/usr/share/archlinux/`.

#### الخطوط

##### الخطوط في كدي تبدو رديئة

جرّب تثبيت الحزمتان [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) و [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation).

بعد التثبيت، اخرج ولِج مرة أخرى. ليس عليك تعديل أيِّ شيءٍ في *إعدادات النظام > الخطوط*.

إن ضبطت تصيير [الخطوط](/index.php?title=Fonts_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9)&action=edit&redlink=1 "Fonts (العربية) (page does not exist)") يدويًّا، اعلم أن النظام قد يغيّر مظهرها. عندما تذهب إلى *إعدادات النظام > المظهر > الخطوط*، سيغيّر إعدادات النظام على الأرجح ملف ضبط الخطوط (`fonts.conf`).

لا توجد طريقة لمنع هذا، لكن إن عيّنت القيم التي تتطابق مع ملف `fonts.conf`، تصيير الخط الافتراضي سيرجع (سيتطلب إعادة تشغيل البرنامج أو -في بعض الحالات- إعادة تشغيل سطح المكتب). اعلم أن تفضيلات خطوط جنوم تفعل هذا أيضًا.

##### الخطوط ضخمة أو تبدو غير متناسبة

جرّب إجبار DPI للخطوط إلى **96** في *إعدادات النظام > مظهر التطبيقات > الخطوط*.

إن لم يعمل هذا، حاول إعداد DPI مباشرةً من ضبط Xorg كما وُثِّقَ [هنا](/index.php/Xorg#Setting_DPI_manually "Xorg").

#### كفاءة المساحة

يمكن للمستخدمين بالشاشات الصغيرة (مثل netbooks) تغيير بعض الإعدادات لجعل كدي بمساحة أكثر كفاءة. طالع [upstream wiki](http://userbase.kde.org/KWin#Using_with_small_screens_(eg_Netbooks)) لمزيد من المعلومات. أيضًا يمكنك استخدام [كتيّب بلازما كدي](http://www.kde.org/workspaces/plasmanetbook/) والتي هي مساحة عمل عُملت خصّيصًا لأجهة netbook الخفيفة والصغيرة.

### الشبكة

يمكنك الاختيار من بين الأدوات التالية:

*   مدير الشبكة. طالع [NetworkManager](/index.php/NetworkManager#KDE4 "NetworkManager") لمعلومات أكثر.
*   Wicd. طالع [Wicd](/index.php/Wicd "Wicd") لمعلومات أكثر.

### الطباعة

**Tip:** استخدم واجهة الوِب [CUPS](/index.php/CUPS "CUPS") لضبط أسرع. الطابعات المُضبَطة بهذه الطريقة يمكن استخدامها في تطبيقات كدي.

يمكنك أيضًا ضبط الطابعات في *إعدادات النظام > Printer Configuration*. لاستخدام هذه الطريقة، عليك أولًا تثبيت [kdeutils-print-manager](https://www.archlinux.org/packages/?name=kdeutils-print-manager) و [cups](https://www.archlinux.org/packages/?name=cups).

عفريتا `avahi-daemon` و `cupsd` يجب أن يبدآ أولًا، وإلّا ستحصل على الخطأ التالي:

```
The service 'Printer Configuration' does not provide an interface 'KCModule'
with keyword 'system-config- printer-kde/system-config-printer-kde.py'
The factory does not support creating components of the specified type.

```

إن واجهك الخطأ التالي، عليك منح المستخدم الصلاحيات الكافية لإدارة الطابعات.

```
There was an error during CUPS operation: 'cups-authorization-canceled'

```

For CUPS, this is set in `/etc/cups/cupsd.conf`.

يسمح إضافة `lp` إلى `SystemGroup` أيَّ شخص يمكنه الطباعة أن يضبط الطابعات. بإمكانك -طبعًا- إضافة مجموعة أخرى بدلًا من `lp`.

 `/etc/cups/cupsd.conf` 
```
# Administrator user group...
SystemGroup sys root lp
```

### دعم سامبا/ويندوز

إن أردت الوصول إلى خدمات ويندوز، ثبّت [Samba](/index.php/Samba "Samba") (الحزمة: [samba](https://www.archlinux.org/packages/?name=samba)).

يمكنك ضبط مشاركات سامبا من خلال:

إعدادات النظام > مشاركة > سامبا

### أنشطة سطح مكتب كدي

أنشطة سطح مكتب كدي هي Plasma-based virtual-desktop-like sets of Plasma Widgets حيث يمكنك ضبط الودحات بشكل مستقل إن كان لديك أكثر من شاشة أو سطح مكتب.

على سطح المكتب، انقر على Cashew Plasmoid وانقر -في النافذة المنبثقة- *الأنشطة*.

سيقدّم شريط بلازما أشنطة سطح مكتب الحالية الموجودة والذي سيظهر أسفل الشاشة. يمكنك التنقّل بينها بنقر الأيقونات المُطابِقة.

### حفظ الطاقة

لِكدي خدمة حفظ طاقة متكاملة اسمها "**Powerdevil Power Management**" حيث يمكنها ضبط profile حفظ الطاقة في نظامك و/أو سطوع الشاشة (إن كان مدعومًا).

منذ كدي 4.6، تحجيم تردّد المعالج لا يمكن لِكدي إدارته. Instead it is assumed to be handled automatically by the the hardware and/or kernel. Arch has used `ondemand` as the default CPU frequency governor since kernel version 3.3, so no additional configuration in needed in most cases. For details on fine-tuning the governor, see [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling").

### مراقبة التغييرات على الملفات والمجلدات المحلية

تستخدم كدي الآن **inotify** مباشرةًا من النواة مع **kdirwatch** (مُضمَّنة في kdelibs)، لذا Gamin أو FAM لم يعودا مطلوبين. قد ترغب في تثبيت [kdirwatch](https://aur.archlinux.org/packages/kdirwatch/) من مستودع مُستخدم آرتش وهو واجهة مستخدم رسومية أمامية لـ kdirwatch.

## إدارة النظام

### ضبط لوحة المفاتيح

انتقل إلى:

```
System Settings > Hardware > Input Devices > Keyboard

```

في أول لسان، يمكنك اختيار طراز لوحة المفاتيح لديك.

في لسان "**Layouts**"، يمكنك اختيار الللغات التي تودُّ استخدامها بنقر زر "Add Layout" واختيار الvariant واللغة بعدها.

في لسان "**Advanced**"، يمكنك اختيار تجميعة لوحة المفاتيح التي تريدها لتغيير التخيططات في قائمة "Key(s) to change layout" الفرعية.

### إنهاء خدمة Xorg عبر إعدادات نظام كدي

انتقل إلى القائمة الفرعية:

```
System Settings > Input Devices > Keyboard > Advanced (tab) > "Key Sequence to kill the X server"

```

وعلّم مربع التعليم.

### وحدة الضبط لِكدي

وحدات الضبط لِكدي (KCM والتي تعني **KC**onfig **M**odule) تساعدك في ضبط نظامك بتوفير واجهات في إعدادات النظام.

**ضبط مظهر وإحساس تطبيقات GTK.**

*   [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config)
*   [kcm-gtk](https://aur.archlinux.org/packages/kcm-gtk/)
*   [kcm-qt-graphicssystem](https://aur.archlinux.org/packages/kcm-qt-graphicssystem/)

**ضبط محمّل الإقلاع GRUB.**

*   [grub2-editor](https://aur.archlinux.org/packages/grub2-editor/)
*   [kcm-grub2](https://aur.archlinux.org/packages/kcm-grub2/)

**ضبط لوحات لمس Synaptics.**

*   [synaptiks](https://aur.archlinux.org/packages/synaptiks/)
*   [kcm_touchpad](https://aur.archlinux.org/packages/kcm_touchpad/)

**ضبط [الجدار الناريّ غيرُ المعقّد](/index.php/Uncomplicated_Firewall "Uncomplicated Firewall") (UFW)**

*   [kcm-ufw](https://aur.archlinux.org/packages/kcm-ufw/)

**ضبط [عُدَّة السياسات](/index.php/PolicyKit "PolicyKit")**

*   [kcm-polkit-kde-git](https://aur.archlinux.org/packages/kcm-polkit-kde-git/)

**ضبط لوحيات Wacom**

*   [kcm-wacomtablet](https://aur.archlinux.org/packages/kcm-wacomtablet/)

يمك العثور على المزيد من وحدات الضبط لِكدي من [kde-apps.org](http://kde-apps.org/index.php?xcontentmode=273).

## بحث سطح المكتب وسطح المكتب الدلالي (Semantic desktop)

وِفقَ [ويكيبيديا](https://ar.wikipedia.org/wiki/%D8%B3%D8%B7%D8%AD_%D9%85%D9%83%D8%AA%D8%A8_%D8%AF%D9%84%D8%A7%D9%84%D9%8A)، *"سطح المكتب الدلالي هو مصطلح يشير إلى عدة أفكار تهدف إلى تغيير واجهة المستخدم للحاسوب، وتغيير قدرات التعامل مع البيانات، بحيث يمكن مشاركة هذه البيانات بسهولة بين التطبيقات، مما يولد علاقات جديدة بين هذه البيانات لم تكن معروفة للحاسوب من قبل."*

إنجاز كدي لهذا المفهوم مرتبط بقطعتين برمجيتين رئيسيتين (من كدي 4.10)، أكوندا ونبومك. هذان البرنامجان يبحثان في بياناتك ويصنعا فهرس سهل البحث فيه عنها. الفكرة وراء قطع البرمجيات هذه هي لجعل نظامك *على علمٍ* ببياناتك وإعطائها سياق باستخدام البيانات الوصفية ووسوم المُستخدم المُورَدة.

Soprano و Virtuoso اعتماديّتان لسطح مكتب نبومك الدلالي. بما أنّ العلاقة بين المكوّنان الرئيسيّان هذان واعتماديّاتهما غير واضحة، الأقسام التالية ستحاول تسليط الضوء على عملهم الداخليّ.

### Virtuoso و Soprano

قاعدة البيانات المُستخدَمة لتخزين البيانات الوصفية التي يستخدمها سطح المكتب الدلالي هي قاعدة بيانات *[إطار توصيف الموارد](https://ar.wikipedia.org/wiki/%D8%A5%D8%B7%D8%A7%D8%B1_%D8%AA%D9%88%D8%B5%D9%8A%D9%81_%D8%A7%D9%84%D9%85%D9%88%D8%A7%D8%B1%D8%AF)* وتُدعى Virtuoso. داخليًّا، , Virtuoso يبدو وكأنه قاعدة بيانات علاقيّة. ( [قاعدة البيانات العلاقيّة](https://en.wikipedia.org/wiki/Relational_model "wikipedia:Relational model") تختلف عن قاعدة البيانات مُفرَدة الجدول التقليدية بمعنى أنها تستخدم عدّة جداول مُرتبِطَة بمفتاح واحد لتخزين البيانات.) تُديرها حاليًّا OpenLink وهي متوفّرة تحت رخصة تجارية وأخرى مفتوحة المصدر.

من [قاعدة بيانات كدي التعليميّة](http://techbase.kde.org/Projects/Nepomuk/ComponentOverview#Soprano)، *Soprano is a Qt abstraction over databases. It provides a friendly Qt-based API for accessing different RDF stores. It currently supports 3 database backends - Sesame, Redland and Virtuoso. The KDE Semantic Stack only works with Virtuoso. Soprano also provides additional features such as serializing, parsing RDF data, and a client server architecture that is heavily used in Nepomuk.*

### نبومك

نبومك (Nepomuk) يعني "البيئة الشبكيّة للإدارة الشخصية والمبنية على علم الوجود للمعرفة المُوَحَدَّة.". It is what allows all the tagging and labeling of files as well to take place and also serves as the way to actually read the Virtuoso databases. يوفّر نبومك واجهة برمجة تطبيقات للمُطوِّرين والتي تسمح لهم بقراءة البيانات التي جمعها.

في السابق، خدمة "Strigi" كانت تُستخدَم لجمع البيانات من الملفات المختلفة الموجودة على النظام. على أيِّ حال، (بسبب الكثير من الأمور، أهمها هو استخدام المعالج والذاكرة) استُبدل Strigi بخدمة فهرسة محليّة تتكامل مع Nepomuk-Core.

لمعلومات أكثر حول نبومك، [هذه الصفحة](http://techbase.kde.org/Projects/Nepomuk/ComponentOverview#Nepomuk_Components) مصدر جيّد. على أيِّ حال، بعض المعلومات في الصفحة السابقة أصبحت قديمة حسبَ [هذه التدوينة](http://vhanda.in/blog/2012/11/nepomuk-without-strigi/).

#### استخدام نبومك وضبطه

للبحث باستخدام نبومك على سطح المكتب كدي، اضغط `ALT+F2` واطبع كلمة البحث. نبومك مُمكَّن افتراضيًّا. يمكن تشغيله وتعطيله من:

```
System Settings > Desktop Search

```

على نبومك تتبّع العديد من الملفات. لهذا السبب يُستحسن زيادة عدد الملفات التي يمكن مشاهدتها بـ inotify. سيكون هذا الأمر جيّد لفعل ذلك:

```
# sysctl fs.inotify.max_user_watches=524288

```

To do it persistently:

```
# echo "fs.inotify.max_user_watches = 524288" >> /etc/sysctl.d/99-inotify.conf

```

أعد تشغيل نبومك لترى التغييرات.

#### كدي دون نبومك

إن أردت تشغيل كدي دون نبومك، توجد الحزمة [nepomuk-core-fake](https://aur.archlinux.org/packages/nepomuk-core-fake/) في مستودع مُستخدم آرتش.

**تحذير:** حاليًّا، يعتمد دولفين على [nepomuk-widgets](https://aur.archlinux.org/packages/nepomuk-widgets/) وبالتالي سيعطب إن استخدمته مع حزمة نبومك الزائفة.

### أكوندا

أكوندا نظام يهدف إلى العمل كخبيئة محليّة لبيانات PIM، بغضّ النظر عن أصله، حيث يمكن استخدامه بواسطة تطبيقات أخرى. وهي تتضمن بُرُد المستخدم الإلكترونية، وجهات الاتصال، والتقويماتن والأحداث، والمجلات، وساعات التوقيت، والملاحظات، إلخ. أكوندا يكون مع واجهة مكتبات نبومك لتوفير إمكانيات البحث.

لا يخزّن أكوندا أية بينات من نفسه: هيئة التخزين تعتمد على طبيعة البيانات (على سبيل المثال، يمكن تخزين جهات الاتصال في هيئة vCard).

لمزيد من المعلومات حول أكوندا وعلاقاته مع نبومك، طالع [[1]](http://blogs.kde.org/node/4503) و [[2]](http://cmollekopf.wordpress.com/2013/02/13/kontact-nepomuk-integration-why-data-from-akonadi-is-indexed-in-nepomuk/).

#### تعطيل أكوندا

طالع [القسم هذا في قاعدة مستخدم كدي](http://userbase.kde.org/Akonadi#Disabling_the_Akonadi_subsystem).

#### ضبط قاعدة البيانات

ابدأ `akonaditray` من الحزمة [kdepim-runtime](https://www.archlinux.org/packages/?name=kdepim-runtime). انقر باليمين عليها واختر **configure**. في لسان Akonadi server configure، يمكنك:

*   ضبط أكوندا لاستخدام خادم MySQL/MariaDB
*   ضبط أكوندا لاستخدام خادم PostgreSQL
*   ضبط أكوندا لاستخدام SQLite

#### تشغيل كدي دون أكوندا

الحزمة [akonadi-fake](https://aur.archlinux.org/packages/akonadi-fake/) خيار جيّد لمن يودُّ تشغيل كدي دون أكوندا.

## فونون

### ما فونون؟

من [ويكيبيديا](https://en.wikipedia.org/wiki/Phonon_(KDE) "wikipedia:Phonon (KDE)"): *Phonon is the multimedia API for KDE 4\. Phonon was created to allow KDE 4 to be independent of any single multimedia framework such as GStreamer or xine and to provide a stable API for KDE 4's lifetime. It was done for various reasons: to create a simple KDE/Qt style multimedia API, to better support native multimedia frameworks on Windows and Mac OS X, and to fix problems of frameworks becoming unmaintained or having API or ABI instability.*

**فونون** استُخدم على نطاق واسع في كدي، للصوت (مثلًا، إخطارات النظام أو تطبيقات كدي للصوت) والفيديو (مثلًا، مصغّرات الفيديو في دولفين) معًا.

### أيَّ سند ( backend) عليَّ استخدامه؟

يمكنك الاختيار من بين مختلف الأسناد مثل GStreamer ([phonon-gstreamer](https://www.archlinux.org/packages/?name=phonon-gstreamer)) أو ڤي‌إل‌سي ([phonon-vlc](https://www.archlinux.org/packages/?name=phonon-vlc))، متوفّر في [official repositories](/index.php/Official_repositories "Official repositories")، و مشغّل إم ([phonon-mplayer-git](https://aur.archlinux.org/packages/phonon-mplayer-git/))، ([phonon-quicktime-git](https://aur.archlinux.org/packages/phonon-quicktime-git/))، و ([phonon-avkode-git](https://aur.archlinux.org/packages/phonon-avkode-git/))، متوفّر في [AUR](/index.php/AUR "AUR"). أغلب المستخدمين يودّون GStreamer أو ڤي‌إل‌سي الذان يمتلكان أفضل upstream support. لاحظ أنه يمكن تثبيت عدّة أسناد مع بعضها البعض والاختيار بينها من *System Settings > Multimedia > Phonon > Backend*.

**ملاحظة:** حسبَ [قاعدة مستخدم كدي](http://userbase.kde.org/Phonon#Backend_libraries)، Phonon-MPlayer لم يعد يُشرَف عليه

حسبَ [هذا البريد في قائمة وسائط كدي المتعدّدة البريدية (KDE-Multimedia)](http://lists.kde.org/?l=kde-multimedia&m=137994906723790&w=2)، على المستخدمين تفضيل ڤي‌إل‌سي على GStreamer.

## تطبيقات مفيدة

المجموعة الرسمية لتطبيقات كدي يمكن العثور عليها [هنا](http://www.kde.org/applications/).

### Yakuake

[Yakuake](http://yakuake.kde.org/) يوفّر محاكي طرفية Quake-like حيث يمكن تبديل شفافيّته بمفتاح F12\. يدعم Yakuake أيضًا تعدّديّة الألسنة. Yakuake متوفّر في الحزمة [yakuake](https://www.archlinux.org/packages/?name=yakuake).

### كدي تيليباثي

[كدي تيليباثي](http://community.kde.org/KTp) مشروع هدفه هو تكامل التراسل الفوري مع سطح المكتب كدي. ينتتفع المشروع بإطار عمل تيليباثي كسند ويُراد استبدال كوبيت به.

لتثبيت كل موافيق تيليباثي، ثبّت مجموعة [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/). لاستخدام عميل كدي تيليباثي، ثبّت حزمة [kde-telepathy-meta](https://www.archlinux.org/packages/?name=kde-telepathy-meta) والتي تحوي على جميع الحزم المُحتواة في مجموعة [kde-telepathy](https://www.archlinux.org/groups/x86_64/kde-telepathy/) .

## تلميحات وخُدَع

### استخدام أوبن بوكس في كدي

**Tip:** مدير النوافذ الأصلي لِكدي هو `kwin`.

مدير النوافذ [أوبن بوكس](/index.php/Openbox "Openbox") يعمل بشكل جيّد جدًا في كدي، combined with a noticable improvement in performance and responsiveness. افتراضيًّا، جلسة `KDE/Openbox` ستكون تلقائيًّا متوفّرة عند تثبيت أوبن بوكس، حتّى ولو كانت بيئة كدي نفسها غير مثبّتة. أغلب مدراء العرض سيسمحون باختيار جلسة كدي مع أوبن بوكس كمدير نوافذ.

لبدأ كدي مع أوبن بوكس كمدير نوافذ يدويًّا -كجلسة افتراضية لـ [SLiM](/index.php/SLiM "SLiM")، أو عندما لا تستخدم مدير عرض بالمرّة- أضف الأمر التالي إلى ملف [Xinitrc](/index.php/Xinitrc "Xinitrc"):

```
exec openbox-kde-session

```

#### عند استخدام KDM

لاستخدام [أوبن بوكس](/index.php/Openbox "Openbox") كمدير نوافذ افتراضيًّا عند الولوج بـ [KDM](/index.php/KDM "KDM")، اذهب فقط إلى Default Applications -> Window Manager -> Use a different windows manager ثمَّ اختر Openbox من صندوق dropdown.

#### إعادة تمكين تأثيرات التركيب

عند استبدال مدير العرض الأصلي `kwin` بِأوبن بوكس، كل تأثيرات التركيب في سطح المكتب -مثل الشفافية- ستُفقَد؛ وهذا يرجع لأن أوبن بوكس لا يوفّر أي وظيفة تركيب. على كلٍّ، استخدام برنامج تركيب منفصل سهل وممكن [لإعادة تمكين التركيب](/index.php/Openbox#Compositing_effects "Openbox").

### تكامل أندرويد مع سطح المكتب كدي

ثبّت [kdeconnect](https://www.archlinux.org/packages/?name=kdeconnect) من مستودع مُستخدم آرتش و [KDE Connect](https://play.google.com/store/apps/details?id=org.kde.kdeconnect_tp&hl=en) من سوق جوجل Play لأفضل تكامل بين كدي وأندرويد.

### الحصول على الإخطارات لتحديثات البرمجيات

ثبّت [apper](https://aur.archlinux.org/packages/apper/) لتحصل على الإخطارات حول تحديثات الحزم في صينية نظام كدي وأيضًا لواجهة رسومية بسيطة لمدير الحزم. طالع [موقع عُدَّة الحزم](http://www.packagekit.org/index.html) لمعلومات أكثر.

### ضبط KWin لاستخدام OpenGL ES

بدءًا بالإصدار 4.8 من KWin أصبح من الممكن استخدام الثنائي **kwin_gles** المبنيّ منفصلًا كبديل عن kwin. It behaves almost the same as the kwin executable in OpenGL2 mode with the slight difference that it uses *egl* instead of *glx* as the native platform interface. لاختبار kwin_gles عليك فقط تنفيذ `kwin_gles --replace` في كونسول. إن أردت إبقاء هذا التغيير دائمًا، عليك إنشاء سكرِبت في `$(kde4-config --localprefix)/env/` والذي يصدّر `KDEWM=kwin_gles`.

### تمكن مصغّرات الصوت مع مديريّ الملفات كنكر/دولفين

لترى مصغّرات ملفات الصوت في كنكر ودولفين، ثبّت [audiothumbs](https://aur.archlinux.org/packages/audiothumbs/) من مستودع مُستخدم آرتش.

### تمكن مصغّرات الفيديو مع مديريّ الملفات كنكر/دولفين

لترى مصغّرات ملفات الصوت في كنكر ودولفين، ثبّت [kdemultimedia-mplayerthumbs](https://www.archlinux.org/packages/?name=kdemultimedia-mplayerthumbs) أو [kdemultimedia-ffmpegthumbs](https://www.archlinux.org/packages/?name=kdemultimedia-ffmpegthumbs).

### تسريع بدء تشغيل التطبيق

المُستخدِم روب (Rob) كتب في مدوّنته هذه "[الخدعة السحرية](http://kdemonkey.blogspot.nl/2008/04/magic-trick.html)" لتحسين بدء تشغيل التطبيق بحوالي 50-150 م‌ث. لتمكينه، أنشئ المجلد هذا في مجلد المنزل:

```
$ mkdir -p ~/.compose-cache/

```

**Note:** لمن لديه حبّ الاستطلاع ويودون معرفة ما الذي يجري هنا، هذا الأمر يمكّن an optimization which Lubos (of general KDE speediness fame) came up with some time ago and was then rewritten and integrated into libx11\. Ordinarily, on startup, applications read input method information from `/usr/share/X11/locale/*your locale*/Compose`. This file is quite long (>5000 lines for the en_US.UTF-8 one) and takes some time to process. libX11 can create a cache of the parsed information which is much quicker to read subsequently, but it will only re-use an existing cache or create a new one in `~/.compose-cache` if the directory already exists.

### إخفاء الأقسام

في دولفين، يكون إخفاء الأقسام بسهولة النقر باليمين على القسم في شريط `الأماكن` الجانبي واختيار `Hide *partition*`. وإلّا...

إن أردت منع الأقسام الداخلية من الظهور في مدير الملفات، يمكنك إنشاء قاعدة udev، مثلًا:

 `/etc/udev/rules.d/10-local.rules`  `KERNEL=="sda[0-9]", ENV{UDISKS_IGNORE}="1"` 

الأمر نفسه لقسم معيّن:

```
KERNEL=="sda1", ENV{UDISKS_IGNORE}="1"
KERNEL=="sda2", ENV{UDISKS_IGNORE}="1"

```

### نصائح كنكر

#### تعطيل تلميحات المفتاح الذكي (المتصفّح)

لتعطيل تلميحات المفتاح الذكي هذه في كنكر (عند ضغط `Ctrl` في صفحة وِب)، استخدم *Settings > Configure Konqueror > Web Browsing* وأزل التأشير عن *Enable Access Key activation with Ctrl key* o

 `~/.kde4/share/config/konquerorrc` 
```
[Access Keys]
Enabled=false
```

#### استخدام عُدَّة الوِب

عُدَّة الوِب محرّك تصفّح مفتوح المصدر طوّرته شركة آبل. وهي اشتقاق من مكتبتيّ KHTML و KJS وتحوي الكثير من التحسينات. عُدَّة الوِب تُستخدم في سفاري، وجوجل كروم وريكونك (rekonq).

يمكن استخدام عُدَّة الوِب بدلًا من KHTML. أولًا ثبّت الحزمة [kwebkitpart](https://www.archlinux.org/packages/?name=kwebkitpart).

بعدها -وبعد تنفيذ كنكر- انتقل إلى *Settings > Configure Konqueror > General > Default web browser engine* وعيّنه إلى `WebKit`.

### التكامل مع فَيَرفُكس

طالع [فَيَرفُكس](/index.php/Firefox_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9)#.D8.A7.D9.84.D8.AA.D9.83.D8.A7.D9.85.D9.84_.D9.85.D8.B9_KDE "Firefox (العربية)").

### تعيين خلفية حافظة الشاشة إلى نفس الحالية

**ملاحظة:** ما زالت هذه المقالة قيد الترجمة.

### تعيين خلفية شاشة القفل إلى صورة arbitrary

انسخ profile الخفية الحالي كقالب:

```
$ cp -r /usr/share/wallpapers/*ExistingWallpaper* ~/.kde4/share/wallpapers/

```

غيّر اسم الدليل، وحرّر `metadata.desktop`:

 `~/.kde4/share/wallpapers/*MyWallpaper*/metadata.desktop` 
```
[Desktop Entry]
Name=MyWallpaper
X-KDE-PluginInfo-Name=MyWallpaper
```

أزل الصور الحالية (`contents/screenshot.png` و `images/*`):

```
$ rm ~/.kde4/share/wallpapers/MyWallpaper/contents/screenshot.png
$ rm ~/.kde4/share/wallpapers/MyWallpaper/contents/images/*

```

انسخ الصورة الجديدة إلى:

```
$ cp *path/to/MyWallpaper.png* MyWallpaper/contents/images/1920x1080.png

```

حرّر بيانات profile الوصفية للسمة الحالية:

 `~/.kde4/share/apps/desktoptheme/MyTheme/metadata.desktop` 
```
[Wallpaper]
defaultWallpaperTheme=NewWallpaper
defaultFileSuffix=.png
defaultWidth=1920
defaultHeight=1080
```

اقفل الشاشة للتحقّق من أنّ كل شيء يعمل.

**ملاحظة:** هذه الطريقة تعيّن خلفية شاشة القفل دون تغيير أية إعدادات على نطاق النظام. للتغيير على نطاق النظام، أنشئ profile خلفية جديد في `/usr/share/wallpapers`.