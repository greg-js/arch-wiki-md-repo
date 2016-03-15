يجب عدم الخلط بين [GRUB](https://www.gnu.org/software/grub/) و [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") وهو الجيل القادم من محمل الإقلاع الموحد . مستمد GRUB من [PUPA](http://www.nongnu.org/pupa/) وهو مشروع بحثي لتطوير الجيل القادم من محمل الإقلاع القديم المسمى الآن GRUB Legacy. تمت كتابة GRUB من الصفر لتنظيف كل شيء وتوفير نمط الوحدات والمحمولية [[1]](https://www.gnu.org/software/grub/grub-faq.html#q1). باختصار ، **محمل الإقلاع** هو البرنامج الأول الذي ينفذ عندم يقلع الحاسوب. وهو المسؤول عن تحميل ونقل التحكم إلى نواة لينكس. النواة، بدورها، تقوم بتهيئة بقية نظام التشغيل.

## Contents

*   [1 مقدمة](#.D9.85.D9.82.D8.AF.D9.85.D8.A9)
    *   [1.1 ملاحظات لمستخدمي إصدار GRUB القديم](#.D9.85.D9.84.D8.A7.D8.AD.D8.B8.D8.A7.D8.AA_.D9.84.D9.85.D8.B3.D8.AA.D8.AE.D8.AF.D9.85.D9.8A_.D8.A5.D8.B5.D8.AF.D8.A7.D8.B1_GRUB_.D8.A7.D9.84.D9.82.D8.AF.D9.8A.D9.85)
        *   [1.1.1 النسخ الاحتياطي للبيانات المهمة](#.D8.A7.D9.84.D9.86.D8.B3.D8.AE_.D8.A7.D9.84.D8.A7.D8.AD.D8.AA.D9.8A.D8.A7.D8.B7.D9.8A_.D9.84.D9.84.D8.A8.D9.8A.D8.A7.D9.86.D8.A7.D8.AA_.D8.A7.D9.84.D9.85.D9.87.D9.85.D8.A9)
    *   [1.2 المتطلبات الأولية](#.D8.A7.D9.84.D9.85.D8.AA.D8.B7.D9.84.D8.A8.D8.A7.D8.AA_.D8.A7.D9.84.D8.A3.D9.88.D9.84.D9.8A.D8.A9)
        *   [1.2.1 أنظمة BIOS](#.D8.A3.D9.86.D8.B8.D9.85.D8.A9_BIOS)
            *   [1.2.1.1 إرشادات خاصة بجدول أقسام GUID Partition Table (GPT)](#.D8.A5.D8.B1.D8.B4.D8.A7.D8.AF.D8.A7.D8.AA_.D8.AE.D8.A7.D8.B5.D8.A9_.D8.A8.D8.AC.D8.AF.D9.88.D9.84_.D8.A3.D9.82.D8.B3.D8.A7.D9.85_GUID_Partition_Table_.28GPT.29)
            *   [1.2.1.2 إرشادات بخصوص( Master Boot Record MBR)](#.D8.A5.D8.B1.D8.B4.D8.A7.D8.AF.D8.A7.D8.AA_.D8.A8.D8.AE.D8.B5.D9.88.D8.B5.28_Master_Boot_Record_MBR.29)
        *   [1.2.2 أنظمة UEFI](#.D8.A3.D9.86.D8.B8.D9.85.D8.A9_UEFI)
            *   [1.2.2.1 إنشاء وتوصيل قسم بنظام UEFI](#.D8.A5.D9.86.D8.B4.D8.A7.D8.A1_.D9.88.D8.AA.D9.88.D8.B5.D9.8A.D9.84_.D9.82.D8.B3.D9.85_.D8.A8.D9.86.D8.B8.D8.A7.D9.85_UEFI)
*   [2 التثبيت](#.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA)
    *   [2.1 أنظمة BIOS](#.D8.A3.D9.86.D8.B8.D9.85.D8.A9_BIOS_2)
        *   [2.1.1 تثبيت ملفات الإقلاع](#.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_.D9.85.D9.84.D9.81.D8.A7.D8.AA_.D8.A7.D9.84.D8.A5.D9.82.D9.84.D8.A7.D8.B9)
            *   [2.1.1.1 التثبيت على قسم إقلاع بنظام GPT BIOS](#.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_.D8.B9.D9.84.D9.89_.D9.82.D8.B3.D9.85_.D8.A5.D9.82.D9.84.D8.A7.D8.B9_.D8.A8.D9.86.D8.B8.D8.A7.D9.85_GPT_BIOS)
            *   [2.1.1.2 التثبيت على قطاع إقلاع 440-byte بنظام MBR](#.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_.D8.B9.D9.84.D9.89_.D9.82.D8.B7.D8.A7.D8.B9_.D8.A5.D9.82.D9.84.D8.A7.D8.B9_440-byte_.D8.A8.D9.86.D8.B8.D8.A7.D9.85_MBR)
            *   [2.1.1.3 التثبيت على قرص صلب مقسم أو غير مقسم](#.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_.D8.B9.D9.84.D9.89_.D9.82.D8.B1.D8.B5_.D8.B5.D9.84.D8.A8_.D9.85.D9.82.D8.B3.D9.85_.D8.A3.D9.88_.D8.BA.D9.8A.D8.B1_.D9.85.D9.82.D8.B3.D9.85)
            *   [2.1.1.4 توليد ملف core.img منفردا](#.D8.AA.D9.88.D9.84.D9.8A.D8.AF_.D9.85.D9.84.D9.81_core.img_.D9.85.D9.86.D9.81.D8.B1.D8.AF.D8.A7)
        *   [2.1.2 توليد ملف التكوين](#.D8.AA.D9.88.D9.84.D9.8A.D8.AF_.D9.85.D9.84.D9.81_.D8.A7.D9.84.D8.AA.D9.83.D9.88.D9.8A.D9.86)
        *   [2.1.3 الإقلاع المزدوج](#.D8.A7.D9.84.D8.A5.D9.82.D9.84.D8.A7.D8.B9_.D8.A7.D9.84.D9.85.D8.B2.D8.AF.D9.88.D8.AC)
            *   [2.1.3.1 نظام وندوز مثبت على نمط BIOS-MBR](#.D9.86.D8.B8.D8.A7.D9.85_.D9.88.D9.86.D8.AF.D9.88.D8.B2_.D9.85.D8.AB.D8.A8.D8.AA_.D8.B9.D9.84.D9.89_.D9.86.D9.85.D8.B7_BIOS-MBR)
    *   [2.2 أنظمة UEFI](#.D8.A3.D9.86.D8.B8.D9.85.D8.A9_UEFI_2)
        *   [2.2.1 تثبيت ملفات الإقلاع](#.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_.D9.85.D9.84.D9.81.D8.A7.D8.AA_.D8.A7.D9.84.D8.A5.D9.82.D9.84.D8.A7.D8.B9_2)
            *   [2.2.1.1 التثبيت على قسم بنظام UEFI](#.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_.D8.B9.D9.84.D9.89_.D9.82.D8.B3.D9.85_.D8.A8.D9.86.D8.B8.D8.A7.D9.85_UEFI)
        *   [2.2.2 توليد ملف التكوين](#.D8.AA.D9.88.D9.84.D9.8A.D8.AF_.D9.85.D9.84.D9.81_.D8.A7.D9.84.D8.AA.D9.83.D9.88.D9.8A.D9.86_2)
        *   [2.2.3 إنشاء مدخلة ل GRUB في الجدار الناري لمحمل الإقلاع](#.D8.A5.D9.86.D8.B4.D8.A7.D8.A1_.D9.85.D8.AF.D8.AE.D9.84.D8.A9_.D9.84_GRUB_.D9.81.D9.8A_.D8.A7.D9.84.D8.AC.D8.AF.D8.A7.D8.B1_.D8.A7.D9.84.D9.86.D8.A7.D8.B1.D9.8A_.D9.84.D9.85.D8.AD.D9.85.D9.84_.D8.A7.D9.84.D8.A5.D9.82.D9.84.D8.A7.D8.B9)
        *   [2.2.4 UEFI إنشاء تطبيق GRUB قابل للتثبيت بنظام](#UEFI_.D8.A5.D9.86.D8.B4.D8.A7.D8.A1_.D8.AA.D8.B7.D8.A8.D9.8A.D9.82_GRUB_.D9.82.D8.A7.D8.A8.D9.84_.D9.84.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_.D8.A8.D9.86.D8.B8.D8.A7.D9.85)
        *   [2.2.5 الإقلاع المتعدد](#.D8.A7.D9.84.D8.A5.D9.82.D9.84.D8.A7.D8.B9_.D8.A7.D9.84.D9.85.D8.AA.D8.B9.D8.AF.D8.AF)
            *   [2.2.5.1 UEFI-GPT ميكروسوفت وندوز مثبت على نمط](#UEFI-GPT_.D9.85.D9.8A.D9.83.D8.B1.D9.88.D8.B3.D9.88.D9.81.D8.AA_.D9.88.D9.86.D8.AF.D9.88.D8.B2_.D9.85.D8.AB.D8.A8.D8.AA_.D8.B9.D9.84.D9.89_.D9.86.D9.85.D8.B7)
*   [3 التهيئة](#.D8.A7.D9.84.D8.AA.D9.87.D9.8A.D8.A6.D8.A9)
    *   [3.1 توليد ملفات الإقلاع آليا باستخدام grub-mkconfig](#.D8.AA.D9.88.D9.84.D9.8A.D8.AF_.D9.85.D9.84.D9.81.D8.A7.D8.AA_.D8.A7.D9.84.D8.A5.D9.82.D9.84.D8.A7.D8.B9_.D8.A2.D9.84.D9.8A.D8.A7_.D8.A8.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_grub-mkconfig)
        *   [3.1.1 خيارات وأوامر إضافية](#.D8.AE.D9.8A.D8.A7.D8.B1.D8.A7.D8.AA_.D9.88.D8.A3.D9.88.D8.A7.D9.85.D8.B1_.D8.A5.D8.B6.D8.A7.D9.81.D9.8A.D8.A9)
    *   [3.2 إنشاء ملف grub.cfg يدويا](#.D8.A5.D9.86.D8.B4.D8.A7.D8.A1_.D9.85.D9.84.D9.81_grub.cfg_.D9.8A.D8.AF.D9.88.D9.8A.D8.A7)
    *   [3.3 الإقلاع المزدوج](#.D8.A7.D9.84.D8.A5.D9.82.D9.84.D8.A7.D8.B9_.D8.A7.D9.84.D9.85.D8.B2.D8.AF.D9.88.D8.AC_2)
        *   [3.3.1 grub-mkconfig استخدام الأمر](#grub-mkconfig_.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_.D8.A7.D9.84.D8.A3.D9.85.D8.B1)
            *   [3.3.1.1 مع نظام GNU/Linux](#.D9.85.D8.B9_.D9.86.D8.B8.D8.A7.D9.85_GNU.2FLinux)
            *   [3.3.1.2 مع نظام FreeBSD](#.D9.85.D8.B9_.D9.86.D8.B8.D8.A7.D9.85_FreeBSD)
            *   [3.3.1.3 مع نظام وندوز](#.D9.85.D8.B9_.D9.86.D8.B8.D8.A7.D9.85_.D9.88.D9.86.D8.AF.D9.88.D8.B2)
        *   [3.3.2 مع نظام وندوز باستخدام برنامج EasyBCD و NeoGRUB](#.D9.85.D8.B9_.D9.86.D8.B8.D8.A7.D9.85_.D9.88.D9.86.D8.AF.D9.88.D8.B2_.D8.A8.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_.D8.A8.D8.B1.D9.86.D8.A7.D9.85.D8.AC_EasyBCD_.D9.88_NeoGRUB)
    *   [3.4 إعداد المحسنات البصرية](#.D8.A5.D8.B9.D8.AF.D8.A7.D8.AF_.D8.A7.D9.84.D9.85.D8.AD.D8.B3.D9.86.D8.A7.D8.AA_.D8.A7.D9.84.D8.A8.D8.B5.D8.B1.D9.8A.D8.A9)
        *   [3.4.1 ضبط دقة شاشة الإقلاع framebuffer](#.D8.B6.D8.A8.D8.B7_.D8.AF.D9.82.D8.A9_.D8.B4.D8.A7.D8.B4.D8.A9_.D8.A7.D9.84.D8.A5.D9.82.D9.84.D8.A7.D8.B9_framebuffer)
        *   [3.4.2 915resolution اﻷداة](#915resolution_.D8.A7.EF.BB.B7.D8.AF.D8.A7.D8.A9)
        *   [3.4.3 صورة الخلفية والخطوط النقطية](#.D8.B5.D9.88.D8.B1.D8.A9_.D8.A7.D9.84.D8.AE.D9.84.D9.81.D9.8A.D8.A9_.D9.88.D8.A7.D9.84.D8.AE.D8.B7.D9.88.D8.B7_.D8.A7.D9.84.D9.86.D9.82.D8.B7.D9.8A.D8.A9)
        *   [3.4.4 المظهر Theme](#.D8.A7.D9.84.D9.85.D8.B8.D9.87.D8.B1_Theme)
        *   [3.4.5 ألوان القائمة](#.D8.A3.D9.84.D9.88.D8.A7.D9.86_.D8.A7.D9.84.D9.82.D8.A7.D8.A6.D9.85.D8.A9)
        *   [3.4.6 القائمة المخفية](#.D8.A7.D9.84.D9.82.D8.A7.D8.A6.D9.85.D8.A9_.D8.A7.D9.84.D9.85.D8.AE.D9.81.D9.8A.D8.A9)
        *   [3.4.7 إيقاف framebuffer](#.D8.A5.D9.8A.D9.82.D8.A7.D9.81_framebuffer)
    *   [3.5 خيارات أخرى](#.D8.AE.D9.8A.D8.A7.D8.B1.D8.A7.D8.AA_.D8.A3.D8.AE.D8.B1.D9.89)
        *   [3.5.1 مدير القرص المنطقي LVM](#.D9.85.D8.AF.D9.8A.D8.B1_.D8.A7.D9.84.D9.82.D8.B1.D8.B5_.D8.A7.D9.84.D9.85.D9.86.D8.B7.D9.82.D9.8A_LVM)
        *   [3.5.2 أقراص RAID](#.D8.A3.D9.82.D8.B1.D8.A7.D8.B5_RAID)
        *   [3.5.3 Persistent block device naming](#Persistent_block_device_naming)
        *   [3.5.4 استخدام العناوين](#.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_.D8.A7.D9.84.D8.B9.D9.86.D8.A7.D9.88.D9.8A.D9.86)
        *   [3.5.5 استدعاء المدخلة الأخيرة](#.D8.A7.D8.B3.D8.AA.D8.AF.D8.B9.D8.A7.D8.A1_.D8.A7.D9.84.D9.85.D8.AF.D8.AE.D9.84.D8.A9_.D8.A7.D9.84.D8.A3.D8.AE.D9.8A.D8.B1.D8.A9)
        *   [3.5.6 الأمن](#.D8.A7.D9.84.D8.A3.D9.85.D9.86)
        *   [3.5.7 تشفير الجذر](#.D8.AA.D8.B4.D9.81.D9.8A.D8.B1_.D8.A7.D9.84.D8.AC.D8.B0.D8.B1)
        *   [3.5.8 الإقلاع للنظام غير الافتراضي لمرة واحدة](#.D8.A7.D9.84.D8.A5.D9.82.D9.84.D8.A7.D8.B9_.D9.84.D9.84.D9.86.D8.B8.D8.A7.D9.85_.D8.BA.D9.8A.D8.B1_.D8.A7.D9.84.D8.A7.D9.81.D8.AA.D8.B1.D8.A7.D8.B6.D9.8A_.D9.84.D9.85.D8.B1.D8.A9_.D9.88.D8.A7.D8.AD.D8.AF.D8.A9)
    *   [3.6 إقلاع ملف أيزو مباشرة من GRUB](#.D8.A5.D9.82.D9.84.D8.A7.D8.B9_.D9.85.D9.84.D9.81_.D8.A3.D9.8A.D8.B2.D9.88_.D9.85.D8.A8.D8.A7.D8.B4.D8.B1.D8.A9_.D9.85.D9.86_GRUB)
        *   [3.6.1 صورة Arch ISO](#.D8.B5.D9.88.D8.B1.D8.A9_Arch_ISO)
            *   [3.6.1.1 معمارية x86_64](#.D9.85.D8.B9.D9.85.D8.A7.D8.B1.D9.8A.D8.A9_x86_64)
            *   [3.6.1.2 معمارية i686](#.D9.85.D8.B9.D9.85.D8.A7.D8.B1.D9.8A.D8.A9_i686)
        *   [3.6.2 Ubuntu ISO](#Ubuntu_ISO)
        *   [3.6.3 صور أيزو أخرى](#.D8.B5.D9.88.D8.B1_.D8.A3.D9.8A.D8.B2.D9.88_.D8.A3.D8.AE.D8.B1.D9.89)
*   [4 استخدام صدفة الأوامر](#.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_.D8.B5.D8.AF.D9.81.D8.A9_.D8.A7.D9.84.D8.A3.D9.88.D8.A7.D9.85.D8.B1)
    *   [4.1 دعم التصفح](#.D8.AF.D8.B9.D9.85_.D8.A7.D9.84.D8.AA.D8.B5.D9.81.D8.AD)
*   [5 أدوات إعداد الواجهة الرسومية](#.D8.A3.D8.AF.D9.88.D8.A7.D8.AA_.D8.A5.D8.B9.D8.AF.D8.A7.D8.AF_.D8.A7.D9.84.D9.88.D8.A7.D8.AC.D9.87.D8.A9_.D8.A7.D9.84.D8.B1.D8.B3.D9.88.D9.85.D9.8A.D8.A9)
*   [6 parttool for hide/unhide](#parttool_for_hide.2Funhide)
*   [7 استخدام الشاشة النصية للإنقاذ](#.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_.D8.A7.D9.84.D8.B4.D8.A7.D8.B4.D8.A9_.D8.A7.D9.84.D9.86.D8.B5.D9.8A.D8.A9_.D9.84.D9.84.D8.A5.D9.86.D9.82.D8.A7.D8.B0)
*   [8 الجمع بين استخدام UUIDs والبرمجة النصية الأساسية](#.D8.A7.D9.84.D8.AC.D9.85.D8.B9_.D8.A8.D9.8A.D9.86_.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_UUIDs_.D9.88.D8.A7.D9.84.D8.A8.D8.B1.D9.85.D8.AC.D8.A9_.D8.A7.D9.84.D9.86.D8.B5.D9.8A.D8.A9_.D8.A7.D9.84.D8.A3.D8.B3.D8.A7.D8.B3.D9.8A.D8.A9)
*   [9 استكشاف الأخطاء وإصلاحها](#.D8.A7.D8.B3.D8.AA.D9.83.D8.B4.D8.A7.D9.81_.D8.A7.D9.84.D8.A3.D8.AE.D8.B7.D8.A7.D8.A1_.D9.88.D8.A5.D8.B5.D9.84.D8.A7.D8.AD.D9.87.D8.A7)
    *   [9.1 بيوس إنتل لا يقلع مع GPT](#.D8.A8.D9.8A.D9.88.D8.B3_.D8.A5.D9.86.D8.AA.D9.84_.D9.84.D8.A7_.D9.8A.D9.82.D9.84.D8.B9_.D9.85.D8.B9_GPT)
    *   [9.2 تفعيل رسائل إصلاح العلل](#.D8.AA.D9.81.D8.B9.D9.8A.D9.84_.D8.B1.D8.B3.D8.A7.D8.A6.D9.84_.D8.A5.D8.B5.D9.84.D8.A7.D8.AD_.D8.A7.D9.84.D8.B9.D9.84.D9.84)
    *   [9.3 تصحيح الخطأ No Suitable Mode Found](#.D8.AA.D8.B5.D8.AD.D9.8A.D8.AD_.D8.A7.D9.84.D8.AE.D8.B7.D8.A3_No_Suitable_Mode_Found)
    *   [9.4 رسالة خطأ msdos-style](#.D8.B1.D8.B3.D8.A7.D9.84.D8.A9_.D8.AE.D8.B7.D8.A3_msdos-style)
    *   [9.5 GRUB UEFI يدخل على نمط صدفةالإنقاذ](#GRUB_UEFI_.D9.8A.D8.AF.D8.AE.D9.84_.D8.B9.D9.84.D9.89_.D9.86.D9.85.D8.B7_.D8.B5.D8.AF.D9.81.D8.A9.D8.A7.D9.84.D8.A5.D9.86.D9.82.D8.A7.D8.B0)
    *   [9.6 GRUB UEFI لا يقلع](#GRUB_UEFI_.D9.84.D8.A7_.D9.8A.D9.82.D9.84.D8.B9)
    *   [9.7 توقيع غير صالح](#.D8.AA.D9.88.D9.82.D9.8A.D8.B9_.D8.BA.D9.8A.D8.B1_.D8.B5.D8.A7.D9.84.D8.AD)
    *   [9.8 تجمد عملية الإقلاع](#.D8.AA.D8.AC.D9.85.D8.AF_.D8.B9.D9.85.D9.84.D9.8A.D8.A9_.D8.A7.D9.84.D8.A5.D9.82.D9.84.D8.A7.D8.B9)
    *   [9.9 استرجاع إصدار GRUB القديم](#.D8.A7.D8.B3.D8.AA.D8.B1.D8.AC.D8.A7.D8.B9_.D8.A5.D8.B5.D8.AF.D8.A7.D8.B1_GRUB_.D8.A7.D9.84.D9.82.D8.AF.D9.8A.D9.85)
*   [10 المراجع](#.D8.A7.D9.84.D9.85.D8.B1.D8.A7.D8.AC.D8.B9)
*   [11 روابط خارجية](#.D8.B1.D9.88.D8.A7.D8.A8.D8.B7_.D8.AE.D8.A7.D8.B1.D8.AC.D9.8A.D8.A9)

## مقدمة

*   اسم *GRUB* يشير رسميا إلى الإصدار *2* من البرنامج ، انظر [[2]](https://www.gnu.org/software/grub/).

إذا كنت تبحث عن مقال مخصص للإصدار القديم ، انظر [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy").

*   يدعم GRUB [Btrfs](/index.php/Btrfs "Btrfs") كنظام ملفات جذر بدون قسم من `/boot` منفصل مضغوط إما بنمط zlib أو LZO.

### ملاحظات لمستخدمي إصدار GRUB القديم

*   الترقية من الإصدار القديم [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") إلى GRUB يكون من خلال تثبيت نسخة جديدة من GRUB والذي يتم شرحه [بأسفل](#.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA).
*   يوجد اختلافات بين الأوامر لإصدار جروب القديم و جروب الحالي .

قم بالتعود [على أوامر جروب](https://www.gnu.org/software/grub/manual/grub.html#Commands) قبل قبل الشروع في العمل. (مثلا تم وضع "search" بدلا من "find" ).

*   أصبح GRUB *مرنا* ولم يعد يحتاج إلى "stage 1.5". ونتيجة لذلك أصبح محمل الإقلاع نفسه عبارة عن وحدات يتم تحميلها من القرص الصلب كم بقدر الحاجة لتوسيع الوظائف مثل دعم (مثل دعم [LVM](/index.php/LVM "LVM") أو RAID ).
*   تم تغيير طريقة تسمية الأجهزة ما بين الإصدار القديم من GRUB والإصدار الحالي . تم ترقيم أقسام القرص الصلب بدءا من 1 بدلا م0 بينما الأقراص الصلبة ما زال ترقيمها يبدأ من 0 ، مسبوقة بنوع جدولة الأقسام. على سبيل المثال `/dev/sda1` يجب أن يشار إليه ب `(hd0,msdos1)` (لنظام MBR) أو `(hd0,gpt1)` لنظام (GPT).

#### النسخ الاحتياطي للبيانات المهمة

على الرغم من أن تثبيت GRUB ينبغي أن يجري بسلاسة ، إلا أنه يوصى بالاحتفاظ بملفات GRUB Legacy قبل الترقية إلى GRUB2.

```
# mv /boot/grub /boot/grub-legacy

```

قم بعمل نسخة احتياطية من الجدول MBR الذي يحتوي كود الإقلاع وجدول الأقسام ضع مسار القرص الفعلي لديك بدلا من `/dev/sd**X**`

```
# dd if=/dev/sdX of=/path/to/backup/mbr_backup bs=512 count=1

```

446 بايت فقط من MBR تحتوي على كود الإقلاع، و 64 بايت التالية تحتوي على جدول أقسام القرص . إذا كنت ﻻ تريد الكتابة فوق جدول الأقسام لديك عندما تريد استرجاعها فننصحك بشدة أن تقوم بعمل نسخة احتياطية فقط لكود الإقلاع الخاص ب MBR:

```
# dd if=/dev/sdX of=/path/to/backup/bootcode_backup bs=446 count=1

```

إذا لم يمكنك تثبيت GRUB@ بشكل صحيح ، انظر [#استرجاع إصدار GRUB القديم](#.D8.A7.D8.B3.D8.AA.D8.B1.D8.AC.D8.A7.D8.B9_.D8.A5.D8.B5.D8.AF.D8.A7.D8.B1_GRUB_.D8.A7.D9.84.D9.82.D8.AF.D9.8A.D9.85).

### المتطلبات الأولية

#### أنظمة BIOS

##### إرشادات خاصة بجدول أقسام [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table") (GPT)

يحتاج تهيئة جروب إلى [قسم إقلاع بنظام بيوس](http://www.gnu.org/software/grub/manual/html_node/BIOS-installation.html) لتضمين `core.img` الخاصة بجروب في حالة عدم وجود فجوة ما بعد MBR في أنظمة تقسيم GPT (والتي يتم الاستيلاء عليها من قبل رأس الجدول والقسم الأساسي لجدول GPT). *هذا القسم يستخدم من قِبَل* جروب فقط في إعدادات BIOS-GPT. لا يوجد نوع للأقسام في حالة تقسيم MBR (على الأقل ليس ل GRUB) كما أنه لا يتطلب هذا القسم إذا كان النظام يعتمد UEFI ، كما أنه لا يتضمن قطاعات للإقلاع ولا تحجز مكانا في هذه الحالة. لإعداد نظام تقسيم BIOS-GPT ، قم بإنشاء قسم بسعة 1007 كب في بداية القرص الصلب ، باستخدام اﻷداة cgdisk او GNU Parted دون تحديد نظام ملفات له. هذا الحجم 1007 كب سيتيح للقسم التالي أن يقسم صحيحا بقطاعات حجمها 1024 كب . إذا كان من الضروري يمكن لهذا القسم أن يوجد ويمكن أيضا أن يكون موجودا في مكان آخر على القرص، لكن يجب أن يكون داخل مساحة ال 2 تيرا بايت الأولى. اضبط القسم ليكون بنوع `0xEF02` في gdisk ، وبنوع `EF02` في cgdisk أو `set <BOOT_PART_NUM> bios_grub on` في GNU Parted.

**ملاحظة:** يجب إنشاء هذا القسم قبل تنفيذ الأمر `grub-install` أو اﻷمر `grub-setup`

**ملاحظة:** يتيح لك gdisk فقط أن تنشئ هذا القسم على وضعية تتيح لك أن تفقد بها أقل قد قدر ممكن من المساحة (sector 34-2047) إذا قمت بإنشائها في النهاية ، وبعد جميع أقسام القرص اﻷخرى . وذلك ﻷن يعمل بخاصية الضبط التلقائي للأقسام في حدود 2048-sector قدر الإمكان.

##### إرشادات بخصوص( [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record") MBR)

عادة ما تكون فجوة ما بعد MBR المسماة "post-MBR gap" وهي ال 512 التالية لمنطقة MBR وقبل بدية القسم اﻷول ، في العديد من أنظمة تقسيم MBR ( أو أقراص ذات تسمية msdos) تكون 31 كب حيث تتحدد مسائل تخطيط الإسطوانات المتوافقة مع دوس في جدول التقسيم. مع ذلك ما بعد MBR تكون ما بين 1 و 2 ميجابايت مطلوبة لتقديم غرفة مناسبة لتضمين صور جروب GRUB's `core.img` ([FS#24103](https://bugs.archlinux.org/task/24103)). وينصح باستخدام قسم يدعم تخطيط أقسام 1 MiB لتحصل أيضا على هذه المساحة لتلبية حاجة القطاعات من غير نوع 512 بايت (التي لا تتعلق بتضمين صور `core.img`) تقسيم MBR يحصل على دعم أفضل من تقسيم GPT في بعض أنظمة التشغيل ، مثل الإصدارات القديمة من ميكروسوفت وندوز (حتى وندوز 7) و ونظام Haiku. إذا كان لديك إقلاع مزدوج من أنظمة التشغيل يراعى استخدم التقسيم MBR . قرص MBR قد يكون قابلا للتحويل إلى GPT إذا كان هناك قدر قليل من المساحة الإضافية متاحا. انظر [GUID Partition Table#Convert from MBR to GPT](/index.php/GUID_Partition_Table#Convert_from_MBR_to_GPT "GUID Partition Table").

#### أنظمة UEFI

**ملاحظة:** يوصى بقراءة وفهم هذه الصفحات [UEFI](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface"), [GPT](/index.php/GUID_Partition_Table "GUID Partition Table") و [UEFI Bootloaders](/index.php/UEFI_Bootloaders "UEFI Bootloaders") .

##### إنشاء وتوصيل قسم بنظام UEFI

فيما يلي [Unified Extensible Firmware Interface#EFI System Partition](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface") إرشادات عن إنشاء نظام تقسيم UEFI . ثم توصيل قسم UEFI على المجلد `/boot/efi/`. إذا قمت بتوصيل قسم بنظام UEFI على نقطة وصل أخرى ، استبدل `/boot/efi` فيما سبق وضع مكانه انقطة التوصيل لديك:

```
# mkdir -p /boot/efi
# mount -t vfat <UEFI_SYSTEM_PARTITION> /boot/efi

```

قم بإنشاء الدليل `/boot/efi/EFI` :

```
# mkdir /boot/efi/EFI

```

## التثبيت

### أنظمة BIOS

يمكن [تثبيت](/index.php/Pacman "Pacman") GRUB مع الحزمة [grub-bios](https://www.archlinux.org/packages/?name=grub-bios) من [المستودعات الرسمية[https://aur.archlinux.org/packages/grub-legacy/ grub-legacy]](/index.php/Official_repositories "Official repositories"). وذلك سيستبدل حزمة أو [grub](https://www.archlinux.org/packages/?name=grub) إذا تم تثبيتها.

**ملاحظة:** ببساطة، لن يسبب تثبيت الحزمة تحديثا للملف `boot/grub/i386-pc/core.img/`

ولا وحدات GRUB في المجلد `/boot/grub/i386-pc`.

أنت تحتاج إلى التحديث يدويا باستخدام اﻷمر `grub-install` كما تم شرحه من قبل.

#### تثبيت ملفات الإقلاع

توجد ثلاثة طرق لتثبيت ملفات إقلاع GRUB في نظام إقلاع BIOS:

*   [#التثبيت على قسم إقلاع بنظام GPT BIOS](#.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_.D8.B9.D9.84.D9.89_.D9.82.D8.B3.D9.85_.D8.A5.D9.82.D9.84.D8.A7.D8.B9_.D8.A8.D9.86.D8.B8.D8.A7.D9.85_GPT_BIOS) (يوصى به مع [GPT](/index.php/GPT "GPT"))
*   [#التثبيت على قطاع إقلاع 440-byte بنظام MBR](#.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_.D8.B9.D9.84.D9.89_.D9.82.D8.B7.D8.A7.D8.B9_.D8.A5.D9.82.D9.84.D8.A7.D8.B9_440-byte_.D8.A8.D9.86.D8.B8.D8.A7.D9.85_MBR) (يوصى به مع [MBR](/index.php/MBR "MBR"))
*   [#التثبيت على قرص صلب مقسم أو غير مقسم](#.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_.D8.B9.D9.84.D9.89_.D9.82.D8.B1.D8.B5_.D8.B5.D9.84.D8.A8_.D9.85.D9.82.D8.B3.D9.85_.D8.A3.D9.88_.D8.BA.D9.8A.D8.B1_.D9.85.D9.82.D8.B3.D9.85) (لا ينصح به)
*   [#توليد ملف core.img منفردا](#.D8.AA.D9.88.D9.84.D9.8A.D8.AF_.D9.85.D9.84.D9.81_core.img_.D9.85.D9.86.D9.81.D8.B1.D8.AF.D8.A7) (أكثر الطرق أمانا إلا أنه تحتاج إلى نوع آخر من محملات إقلاع بيوس مثل القديم [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") or [Syslinux](/index.php/Syslinux "Syslinux") للتثبيت مع chainload `/boot/grub/i386-pc/core.img`)

**ملاحظة:** انظر [http://www.gnu.org/software/grub/manual/html_node/BIOS-installation.html](http://www.gnu.org/software/grub/manual/html_node/BIOS-installation.html) لمزيد من الوثائق.

##### التثبيت على قسم إقلاع بنظام GPT BIOS

أقراص [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table") لا تحتوي على "مسارات إقلاع" محجوزة . لذلك يجب عليك إنشاء قسم إقلاع بيوس (`0xEF02`) لتحمل صورة المحمل GRUB. استخدام GNU Parted يمكنك ضبط هذا باستخدام أمر كما يلي:

```
# parted /dev/disk set <partition-number> bios_grub on

```

إذا كنت تستخدم gdisk ، اضبط نوع القسم على `0xEF02`. عن طريق برامج التقسيم الذي يتطلب إعداد GUID مباشرة يجب أن يكون `‘21686148-6449-6e6f-744e656564454649’` مخزنا على القرص مثل `"!haHdInotNeedEFI"` إذا تم تفسيره على أنه ASCII.

**تحذير:** كن شديد الحذر في تحديدك لقسم إقلاع بيوس . عندما يعثر GRUB على قسم إقلاغ بيوس أثناء التثبيت ، سوف يكتب تلقائيا على جزء منه . كن متأكدا أن هذا القسم لا يحتوي أية بيانات أخرى.

لإعداد `grub-bios` على قرص صلب بنظام GPT قم بتعديل الدليل `/boot/grub` ، وتوليد ملف `/boot/grub/i386-pc/core.img` وتضمينه في قسم إقلاع بيوس ، نفذ الأمر :

```
# modprobe dm-mod
# grub-install --target=i386-pc --recheck --debug /dev/sda
# mkdir -p /boot/grub/locale
# cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo

```

حيث `/dev/sda` هو القرص المستهدف للتثبيت .

##### التثبيت على قطاع إقلاع 440-byte بنظام MBR

لتثبيت `grub-bios` على قطاع الإقلاع الرئيس Master Boot Record ، قم بتعديل المجلد `/boot/grub` ، وتوليد الملف `/boot/grub/i386-pc/core.img`، ووضعه في ال 31 كب ( أصغر مساحة ، وتعتمد على طريقة ترتيب قسم فجوة ما بعد MBR ، وقم بتوليد ملف التكوين بتنفيذ الأمر:

```
# modprobe dm-mod
# grub-install --recheck /dev/sda
# grub-mkconfig -o /boot/grub/grub.cfg

```

حيث `/dev/sda` هو القرص المستهدف للتثبيت ( في هذه الحالة هو قطاع الإقلاع الرئيس MBR الخاص بأول قرص ساتا) إذا كنت تستخدم [LVM](/index.php/LVM "LVM") لعمل قسم `/boot` لديك , يمكنك تثبيت GRUB على أقراص حقيقية متعددة.

**تحذير:** تأكد من فحص المجلد `/boot` إذا كنت تستخدم الأخير . أحيانا ما تنشئ معاملات `boot-directory` مجلد `/boot` آخر بداخل القسم `/boot`. سيكون التثبيت الخطأ يبدو كما يلي `/boot/boot/grub/`.

##### التثبيت على قرص صلب مقسم أو غير مقسم

**ملاحظة:** لا يستحب تثبيت grub-bios على قطاع إقلاع أو قرص غير مقسم مثلما يفعل كل من GRUB Legacy أو Syslinux .هذا النوع من التثبيت عرضة للتحطم ، خاصة أثناء التحديث ، وهو غير مدعوم من قِبل Arch devs.

لتثبيت grub-bios على قطاع إقلاع ، بقرص غير مقسم (يسمى أيضا superfloppy ) أو عل قرص مرن ، استخدم على سبيل المثال `/dev/sdaX/` كقسم إقلاع `boot/` ، نفذ :

```
# modprobe dm-mod 
# grub-install --target=i386-pc --recheck --debug --force /dev/sdaX
# chattr -i /boot/grub/i386-pc/core.img
# mkdir -p /boot/grub/locale
# cp /usr/share/locale/en@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo
# chattr +i /boot/grub/i386-pc/core.img

```

أنت تحتاج إلى الخيار `force--` ليسمح باستخدام قوائم الكتل blocklists ولا يجب استخدام `grub-setup=/bin/true--` (الذي يشبه ببساطة توليد الملف `core.img`). سيعطيك الأمر `grub-install` رسالة خطأ كما يجب أن يعطيك فكرة عن ماهية هذا الخطأ على هذا النهج:

```
/sbin/grub-setup: warn: Attempting to install GRUB to a partitionless disk or to a partition. This is a BAD idea.
/sbin/grub-setup: warn: Embedding is not possible. GRUB can only be installed in this setup by using blocklists. 
                        However, blocklists are UNRELIABLE and their use is discouraged.

```

بدون `force--` ربما تحصل على رسالة الخطأ بأسفل ولن يقوم الأمر `grub-setup` بتثبيت شيفرة الإقلاع على قطاع الإقلاع بالقسم:

```
/sbin/grub-setup: error: will not proceed with blocklists

```

مع الخيار `force--` يجب أن تحصل على رسالة:

```
Installation finished. No error reported.

```

السبب في كون `grub-setup` لا يتيح ذلك افتراضيا لأنه في حالة الأقراص المقسمة أو غير المقسمة أن `grub-bios` يعتمد على قوائم الكتل blocklists المضمنة في قطاع إقلاع القسم لتحديد مكان الملف `boot/grub/i386-pc/core.img/` وبادئة الدليل `/boot/grub/`. مواضع القطاعات الخاصة بملف `core.img`..إلخ ربما تتغير كلما تغير نظام الملفات على القسم ( تم نسخ ملفات أو حذفها) لمزيد من المعلومات انظر [https://bugzilla.redhat.com/show_bug.cgi?id=728742](https://bugzilla.redhat.com/show_bug.cgi?id=728742) and [https://bugzilla.redhat.com/show_bug.cgi?id=730915](https://bugzilla.redhat.com/show_bug.cgi?id=730915). هذه الخلفية من أجل لوضع flag غير قابلة للتغيير على الملف `boot/grub/i386-pc/core.img/` ( باستخدام chattr كما تم شرحه من قبل) حيث إن أماكن القطاعات الخاصة بملف `core.img` على القرص ثابتة . و ال flag الثابت على `boot/grub/i386-pc/core.img/` يحتاج للضبط فقط إذا كانت الحزمة `grub-bios` مثبيتة على قطاع الإقلاع بالقرص المقسم أو غير المقسم ، وليس في حالة التثبيت على قطاع الإقلاع الرئيس MBR أو ببساطة توليد الملف `core.img` بدون تمين أي قطاعات إقلاع (تم شرحه من بأعلى).

##### توليد ملف core.img منفردا

لإنشاء المجلد `/boot/grub/` وتوليد الملف `boot/grub/i386-pc/core.img/` **بدون** تضمين أي شيفرة لقطاعات الإقلاع على مسجل الإقلاع الرئيس ، ومنطقة ما قبل فجوة سجل الإقلاع الرئيس post-MBR ، أو قطاعات الإقلاع بالقسم ، قم بإضافة الخيار `grub-setup=/bin/true--` إلى الأمر `grub-install`: To populate the `/boot/grub` directory and generate a `/boot/grub/i386-pc/core.img` file **without** embedding any

```
# modprobe dm-mod
# grub-install --target=i386-pc --grub-setup=/bin/true --recheck --debug /dev/sda
# mkdir -p /boot/grub/locale
# cp /usr/share/locale/en@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo

```

يمكنك حينئذ تضفير ملف `core.img` GRUB Legacy أو syslinux كصورة أقلاع لنواة واحدة أو متعددة الأنوية.

#### توليد ملف التكوين

في النهاية قم بإعدادGRUB (تم توضيح ذلك بفائض من الشرح في الجزء الخاص بالإعدادات ) :

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

**ملاحظة:** مسار الملف هو `/boot/grub/grub.cfg`, وليس `/boot/grub/i386-pc/grub.cfg`.

إذا كان GRUB يعاني من رسالة "no suitable mode found" أثناء الإقلاع ، اذهب إلى [#تصحيح الخطأ No Suitable Mode Found](#.D8.AA.D8.B5.D8.AD.D9.8A.D8.AD_.D8.A7.D9.84.D8.AE.D8.B7.D8.A3_No_Suitable_Mode_Found) . إذا فشل الأمر `grub-mkconfig` قم بوضع الملف `/boot/grub/grub.cfg` بدلا من ملف `/boot/grub/menu.lst` باستخدام الأمر:

```
# grub-menulst2cfg /boot/grub/menu.lst /boot/grub/grub.cfg

```

كمثال:

 `/boot/grub/menu.lst` 
```
default=0
timeout=5

title  Arch Linux Stock Kernel
root   (hd0,0)
kernel /vmlinuz-linux root=/dev/sda2 ro
initrd /initramfs-linux.img

title  Arch Linux Stock Kernel Fallback
root   (hd0,0)
kernel /vmlinuz-linux root=/dev/sda2 ro
initrd /initramfs-linux-fallback.img

```
 `/boot/grub/grub.cfg` 
```
set default='0'; if [ x"$default" = xsaved ]; then load_env; set default="$saved_entry"; fi
set timeout=5

menuentry 'Arch Linux Stock Kernel' {
        set root='(hd0,1)'; set legacy_hdbias='0'
        legacy_kernel   '/vmlinuz-linux' '/vmlinuz-linux' 'root=/dev/sda2' 'ro'
        legacy_initrd '/initramfs-linux.img' '/initramfs-linux.img'

}

menuentry 'Arch Linux Stock Kernel Fallback' {
        set root='(hd0,1)'; set legacy_hdbias='0'
        legacy_kernel   '/vmlinuz-linux' '/vmlinuz-linux' 'root=/dev/sda2' 'ro'
        legacy_initrd '/initramfs-linux-fallback.img' '/initramfs-linux-fallback.img'
}

```

إذا نسيت إنشاء ملف `/boot/grub/grub.cfg` قم ببساطة بالإقلاع من داخل صدفة أوامر GRUB واكتب :

```
sh:grub> insmod legacycfg
sh:grub> legacy_configfile ${prefix}/menu.lst

```

أقلع داخل آرتش وأعد إنشاء ملف تهيئة GRUB `/boot/grub/grub.cfg` المناسب .

**ملاحظة:** هذا لخيار يعمل فقط مع أنظمة بيوس ، وليس مع أنظمة UEFI .

#### الإقلاع المزدوج

##### نظام وندوز مثبت على نمط BIOS-MBR

**ملاحظة:** GRUB يدعم إقلاع `bootmgr` مباشرة وجمع قطاعات الإقلاع لم يعد مطلوبا لإقلاع وندوز في إعداد BIOS-MBR.

**تحذير:** إن **قسم النظام** هو الذي يحمل `bootmgr` وليس القسم "الحقيقي" لوندوز (عادة يكون قسم C:) . عند إظهار كل معرفات الأقسام UUIDs بالأمر blkid ، يكون قسم النظام معنون ب `LABEL="SYSTEM RESERVED"` ويكون حجمه في حدود 100 ميجا بايت (يشبه كثيرا حجم قسم الإقلاع في آرتش) . انظر [Wikipedia:System partition and boot partition](https://en.wikipedia.org/wiki/System_partition_and_boot_partition "wikipedia:System partition and boot partition") لمزيد من التفاصيل.

أوجد معرف UUID الخاص بنظام ملفات NTFS لقسم نظام وندوز حيث يقيم `bootmgr` وملفاته. مثلا ؛ إذا كان `bootmgr` الخاص بوندوز يوجد في `/media/SYSTEM_RESERVED/bootmgr`: لوندوز فيستا/7/8:

```
# grub-probe --target=fs_uuid /media/SYSTEM_RESERVED/bootmgr
69B235F6749E84CE

```

```
# grub-probe --target=hints_string /media/SYSTEM_RESERVED/bootmgr
--hint-bios=hd0,msdos1 --hint-efi=hd0,msdos1 --hint-baremetal=ahci0,msdos1

```

**ملاحظة:** لوندوز إكس بي ضع `ntldr` بدلا من `bootmgr` في الأمر بأعلى.

بعد ذلك ، أضف الشيفرة التالية إلى `/etc/grub.d/40_custom` أو `/boot/grub/custom.cfg` ثم قم بإعادة توليد ملف `grub.cfg` بالأمر `grub-mkconfig` كما تم شرحه بأعلى لإقاع وندوز ( إكس بي ، 7 ، أو 8) والمثبت على وضعية BIOS-MBR: لوندوز فيستا/7/8:

```
menuentry "Microsoft Windows Vista/7/8 BIOS-MBR" {
        insmod part_msdos
        insmod ntfs
        insmod search_fs_uuid
        insmod ntldr     
        search --fs-uuid --set=root --hint-bios=hd0,msdos1 --hint-efi=hd0,msdos1 --hint-baremetal=ahci0,msdos1 69B235F6749E84CE
        ntldr /bootmgr
}

```

لوندوز إكس بي:

```
menuentry "Microsoft Windows XP" {
        insmod part_msdos
        insmod ntfs
        insmod search_fs_uuid
        insmod ntldr     
        search --fs-uuid --set=root --hint-bios=hd0,msdos1 --hint-efi=hd0,msdos1 --hint-baremetal=ahci0,msdos1 69B235F6749E84CE
        ntldr /ntldr
}

```

يمكن استخدام `/etc/grub.d/40_custom` كقالب لإنشاء `/etc/grub.d/nn_custom`. حيث إن الحرفين `nn` الأسبقية ، مما يدل على أمر تنفيذ البرنامج النصي. ويتم تنفيذ البرامج النصية محددة المكان في قائمة إقلاع grub .

**ملاحظة:** `nn` يجب أن يكون أكبر من 06 للتأكد من تنفيذ الأوامر النصية الضرورية أولا .

### أنظمة UEFI

**ملاحظة:** يفضل معرفة الاختلافات بين اللوحات الأم في تطبيق UEFI . المستخدمون الخبراء بالمشكلات يجعلون Grub/EFI يعمل بشكل جيد عليهم مشاركة المعلومات والخطوات الخاصة بحالات معين للعتاد عندما لا يعمل إقلاع UEFI كما تم شرحه بأسفل . في محاولة للمحافظة مقال [GRUB](/index.php/GRUB "GRUB") أنيقا ومرتبا ، قم بقراءة صفحة [GRUB EFI Examples](/index.php/GRUB_EFI_Examples "GRUB EFI Examples") لهذه الحالات الخاصة.

أولا [detect which UEFI firmware arch](/index.php/Unified_Extensible_Firmware_Interface#Detecting_UEFI_Firmware_Arch "Unified Extensible Firmware Interface") لديك إما x86_64 أو i386).وبناء على ذلك الناتج ، قم بتثبيت الحزمة المناسبة:

*   لبرنامج التشغيل الأساسي 64 -bit aka x86_64 UEFI ثبت الحزمة [grub-efi-x86_64](https://www.archlinux.org/packages/?name=grub-efi-x86_64)
*   لبرنامج التشغيل الأساسي 32-bit aka i386 UEFI ثبت الحزمة [grub-efi-i386](https://www.archlinux.org/packages/?name=grub-efi-i386)

**ملاحظة:** بساطة تثبيت الحزمة لن يسبب تحديث ملف `core.efi` و وحدات GRUB في قسم نظام UEFI . ستحتاج إلى استخدام الأمر `grub-install` يدويا كما تم شرحه بأسفل .

#### تثبيت ملفات الإقلاع

##### التثبيت على قسم بنظام UEFI

**ملاحظة:** اﻷوامر التالية تفترض أنك تستخدم `grub-efi-x86_64` ل `grub-efi-i386` ضع `i386` بدلا من `x86_64` في اﻷوامر بأسفل.

**ملاحظة:** للقيام بذلك تحتاج إلى الإقلاع باستخدام UEFI وليس BIOS . إذا قمت بالإقلاع فقط عن طريق نسخ ملف أيزو إلى قرص USB ، عليك اتباع [هذا الدليل](/index.php/Unified_Extensible_Firmware_Interface#Create_UEFI_bootable_USB_from_ISO "Unified Extensible Firmware Interface") سيحتاج نظام تقسيم UEFI إلى التوصيل بالدليل `/boot/efi/` في سكربت تثبيت GRUB حتى يستطيع الكشف عنه :

```
# mkdir -p /boot/efi
# mount -t vfat /dev/sdXY /boot/efi

```

قم بتثبيت التطبيق GRUB UEFI في `/boot/efi/EFI/arch_grub/` وتثبيت وحداته على `/boot/grub/x86_64-efi` (يوصى به) بتنفيذ:

```
# modprobe dm-mod
# grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=arch_grub --recheck --debug
# mkdir -p /boot/grub/locale
# cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo

```

**ملاحظة:** بدون الخيار `target--` أو `directory--` لن يستطيع جروب تحديد أي نوع من المشغلات الأساسة لتثبيتها . في مثل هذه الحالة سقوم `grub-install` بعرض `source_dir doesn't exist. Please specify --target or --directory` الرسالة.

إذا أردت تثبيت وحدات GRUB و الملف `grub.cfg` في الدليل `/boot/efi/EFI/grub/` والتطبيق `grubx64.efi` في `/boot/efi/EFI/arch_grub` ( مثلا ، كل ملفات GRUB UEFI بداخل قسم UEFISYS ذاته) استخدم:

```
# modprobe dm-mod 
# grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=arch_grub --boot-directory=/boot/efi/EFI --recheck --debug
# mkdir -p /boot/efi/EFI/grub/locale
# cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/efi/EFI/grub/locale/en.mo

```

الخيار `efi-directory--` يشير إلى نقطة التوصيل لقسم نظام UEFI , و `--bootloader-id` يشير إلى اسم الدليل المستخدم لتخزين الملف `grubx64.efi` و `--boot-directory` يشير إلى الدليل الذي سيتم عليه تثبيت الوحدات الفعلية ( `grub.cfg`ويشير إلى أين يجب يتم تثبيت ) .

المسارات الفعلية هي:

```
<efi-directory>/<EFI or efi>/<bootloader-id>/grubx64.efi

```

```
<boot-directory>/grub/x86_64-efi/<all modules, grub.efi, core.efi, grub.cfg>

```

**ملاحظة:** the `--bootloader-id` option does not change `<boot-directory>/grub`, i.e. you cannot install the modules to `<boot-directory>/<bootloader-id>`, the path is hard-coded to be `<boot-directory>/grub`.

In `--efi-directory=/boot/efi --boot-directory=/boot/efi/EFI --bootloader-id=grub`:

```
<efi-directory>/<EFI or efi>/<bootloader-id> == <boot-directory>/grub == /boot/efi/EFI/grub

```

In `--efi-directory=/boot/efi --boot-directory=/boot/efi/EFI --bootloader-id=arch_grub`:

```
<efi-directory>/<EFI or efi>/<bootloader-id> == /boot/efi/EFI/arch_grub
<boot-directory>/grub == /boot/efi/EFI/grub

```

In `--efi-directory=/boot/efi --boot-directory=/boot --bootloader-id=arch_grub`:

```
<efi-directory>/<EFI or efi>/<bootloader-id> == /boot/efi/EFI/arch_grub
<boot-directory>/grub == /boot/grub

```

In `--efi-directory=/boot/efi --boot-directory=/boot --bootloader-id=grub`:

```
<efi-directory>/<EFI or efi>/<bootloader-id> == /boot/efi/EFI/grub
<boot-directory>/grub == /boot/grub

```

The `<efi-directory>/<EFI or efi>/<bootloader-id>/grubx64.efi` is an exact copy of `<boot-directory>/grub/x86_64-efi/core.efi`.

**ملاحظة:** In GRUB 2.00, the `grub-install` option `--efi-directory` replaces `--root-directory` and the latter is deprecated.

**ملاحظة:** The options `--efi-directory` and `--bootloader-id` are specific to GRUB UEFI.

In all the cases the UEFI SYSTEM PARTITION should be mounted for `grub-install` to install `grubx64.efi` in it, which will be launched by the firmware (using the `efibootmgr` created boot entry in non-Mac systems).

If you notice carefully, there is no <device_path> option (Eg: `/dev/sda`) at the end of the `grub-install` command unlike the case of setting up GRUB for BIOS systems. Any <device_path> provided will be ignored by the install script as UEFI bootloaders do not use MBR or Partition boot sectors at all.

You may now be able to UEFI boot your system by creating a `grub.cfg` file by following [#Generate UEFI Config file](#Generate_UEFI_Config_file) and [#Create GRUB entry in the Firmware Boot Manager](#Create_GRUB_entry_in_the_Firmware_Boot_Manager).

#### توليد ملف التكوين

Finally, generate a configuration for GRUB (this is explained in greater detail in the Configuration section):

```
# grub-mkconfig -o <boot-directory>/grub/grub.cfg

```

**Note:** The file path is `<boot-directory>/grub/grub.cfg`, NOT `<boot-directory>/grub/x86_64-efi/grub.cfg`.

If you used `--boot-directory=/boot`:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

If you used `--boot-directory=/boot/efi/EFI`:

```
# grub-mkconfig -o /boot/efi/EFI/grub/grub.cfg

```

This is independent of the value of `--bootloader-id` option.

If GRUB complains about "no suitable mode found" while booting, try [#Correct No Suitable Mode Found Error](#Correct_No_Suitable_Mode_Found_Error).

#### إنشاء مدخلة ل GRUB في الجدار الناري لمحمل الإقلاع

`grub-install` automatically tries to create a menu entry in the boot manager. If it doesn't, then see [Beginners' guide#GRUB](/index.php/Beginners%27_guide#GRUB "Beginners' guide") for instructions to use `efibootmgr` to create a menu entry. However, the problem is likely to be that you haven't booted your CD/USB in UEFI mode, as in [Unified Extensible Firmware Interface#Create UEFI bootable USB from ISO](/index.php/Unified_Extensible_Firmware_Interface#Create_UEFI_bootable_USB_from_ISO "Unified Extensible Firmware Interface").

#### UEFI إنشاء تطبيق GRUB قابل للتثبيت بنظام

It is possible to create a `grubx64_standalone.efi` application which has all the modules embeddded in a memdisk within the UEFI application, thus removing the need for having a separate directory populated with all the GRUB UEFI modules and other related files. This is done using the `grub-mkstandalone` command which is included in [grub-common](https://www.archlinux.org/packages/?name=grub-common).

The easiest way to do this would be with the install command already mentioned before, but specifying the modules to include. For example:

```
# grub-mkstandalone --directory="/usr/lib/grub/x86_64-efi/" --format="x86_64-efi" --compression="xz" \
--output="/boot/efi/EFI/arch_grub/grubx64_standalone.efi" <any extra files you want to include>

```

The `grubx64_standalone.efi` file expects `grub.cfg` to be within its $prefix which is `(memdisk)/boot/grub`. The memdisk is embedded within the efi app. The `grub-mkstandlone` script allow passing files to be included in the memdisk image to be as the arguments to the script (in <any extra files you want to include>).

If you have the `grub.cfg` at `/home/user/Desktop/grub.cfg`, then create a temporary `/home/user/Desktop/boot/grub/` directory, copy the `/home/user/Desktop/grub.cfg` to `/home/user/Desktop/boot/grub/grub.cfg`, cd into `/home/user/Desktop/boot/grub/` and run:

```
# grub-mkstandalone --directory="/usr/lib/grub/x86_64-efi/" --format="x86_64-efi" --compression="xz" \
--output="/boot/efi/EFI/arch_grub/grubx64_standalone.efi" "boot/grub/grub.cfg"

```

The reason to cd into `/home/user/Desktop/boot/grub/` and to pass the file path as `boot/grub/grub.cfg` (notice the lack of a leading slash - boot/ vs /boot/ ) is because `dir1/dir2/file` is included as `(memdisk)/dir1/dir2/file` by the `grub-mkstandalone` script.

If you pass `/home/user/Desktop/grub.cfg` the file will be included as `(memdisk)/home/user/Desktop/grub.cfg`. If you pass `/home/user/Desktop/boot/grub/grub.cfg` the file will be included as `(memdisk)/home/user/Desktop/boot/grub/grub.cfg`. That is the reason for cd'ing into `/home/user/Desktop/boot/grub/` and passing `boot/grub/grub.cfg`, to include the file as `(memdisk)/boot/grub/grub.cfg`, which is what `grub.efi` expects the file to be.

You need to create an UEFI Boot Manager entry for `/boot/efi/EFI/arch_grub/grubx64_standalone.efi` using `efibootmgr`. Follow [#Create GRUB entry in the Firmware Boot Manager](#Create_GRUB_entry_in_the_Firmware_Boot_Manager).

#### الإقلاع المتعدد

##### UEFI-GPT ميكروسوفت وندوز مثبت على نمط

Find the UUID of the FAT32 filesystem in the UEFI SYSTEM PARTITION where the Windows UEFI Bootloader files reside. For example, if Windows `bootmgfw.efi` exists at `/boot/efi/EFI/Microsoft/Boot/bootmgfw.efi` (ignore the upper-lower case differences since that is immaterial in FAT filesystem):

```
# grub-probe --target=fs_uuid /boot/efi/EFI/Microsoft/Boot/bootmgfw.efi
1ce5-7f28

# grub-probe --target=hints_string /boot/efi/EFI/Microsoft/Boot/bootmgfw.efi
--hint-bios=hd0,gpt1 --hint-efi=hd0,gpt1 --hint-baremetal=ahci0,gpt1

```

Then, add this code to `/etc/grub.d/40_custom` to chainload Windows x86_64 (Vista SP1+, 7 or 8) installed in UEFI-GPT mode:

```
menuentry "Microsoft Windows Vista/7/8 x86_64 UEFI-GPT" {
        insmod part_gpt
        insmod fat
        insmod search_fs_uuid
        insmod chain
        search --fs-uuid --set=root --hint-bios=hd0,gpt1 --hint-efi=hd0,gpt1 --hint-baremetal=ahci0,gpt1 1ce5-7f28
        chainloader /efi/Microsoft/Boot/bootmgfw.efi
}

```

Afterwards remake `/boot/grub/grub.cfg`

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

## التهيئة

يمكنك أيضا الاختيار بن توليد الملف `grub.cfg` او يدويا .

**ملاحظة:** بخصوص أنظمة EFI إذا تم تثبيت GRUB بوضع الخيار `--boot-directory` يجب أن يوضع الملف the `grub.cfg` في نفس الدليل ك `grubx64.efi`. خلافا لذلك سيذهب ملف `grub.cfg` إلى الدليل `/boot/grub/` كما يحدث في GRUB BIOS.

**ملاحظة:** هنا ، شرح كامل لكيفية تهيئة [http://members.iinet.net/~herman546/p20/GRUB2%20Configuration%20File%20Commands.html](http://members.iinet.net/~herman546/p20/GRUB2%20Configuration%20File%20Commands.html) GRUB  :

### توليد ملفات الإقلاع آليا باستخدام grub-mkconfig

ملفات الإعداد الخاصة بجروب والمعادلة ل `menu.lst` هي `/etc/default/grub` و `/etc/grub.d/*`. يستخدم الأمر `grub-mkconfig` هذه الملفات لتوليد الملف `grub.cfg`. افتراضيا فإن مخرجات السكربت معيارية. لتوليد الملف `grub.cfg` نفذ الأمر التالي :

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

تم ضبط `/etc/grub.d/10_linux` لإضافة عناصر القائمة الخاصة بنظام آرتش لينكس التي تعمل خارج النظام ، ولتوليد أي نظام تشغيل أن ربما تحتاج إلى إضافتها يدويا إلى الملف `/etc/grub.d/40_custom` أو `/boot/grub/custom.cfg`

#### خيارات وأوامر إضافية

لتمرير مدخلات إضافية إلى صورة لينكس ، يمكنك ضبط متغيرات `GRUB_CMDLINE_LINUX` في الملف `/etc/default/grub`. على سبيل المثال ؛ استخدم `GRUB_CMDLINE_LINUX="resume=/dev/sdaX"` حيث `sda**X**` هو قسم التبديل swap لديك لإتاحة استعادة الجلسة عند عمل إسبات للنظام. يمكنك أيضا استخدام `GRUB_CMDLINE_LINUX="resume=/dev/disk/by-uuid/${swap_uuid}"` حيث `${swap_uuid}` هو التسمية الثابتة للكتلة [UUID](/index.php/Persistent_block_device_naming "Persistent block device naming") الخاصة بقسم السواب لديك. المدخلات المتعددة يمكن الفصل بينها بمسافة داخل علامات الاقتباس المزدوجة . لذا بخصوص المستخدمين الذين يريدون كلا من resume و systemd يمكن أن يكون ذلك شبيها بما يلي: `GRUB_CMDLINE_LINUX="resume=/dev/sdaX init=/usr/lib/systemd/systemd"`

انظر [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") لمزيد من المعلومات.

### إنشاء ملف grub.cfg يدويا

**تحذير:** يوصى بشدة *بعدم تعديل هذا الملف.* يتم توليد هذا الملف بالأمر `grub-mkconfig` ، ومن الأفضل تحرير الملف `/etc/default/grub` أو واحدا من السكربتات في المجلد`/etc/grub.d` .

ملف الإعداد الأساسي لجروب يستخدم الخيارات التالية:

*   `(hdX,Y)` القسم هو `Y` على القرص `X`, ارقام الأقسام تبدأ بـ 1, بينما ترقيم الأقراص يبدأ بـ 0
*   `set default=N` مدخلة الإقلاع الافتراضي يتم إقلاعها بعد مرور زمن يحدده المستخدم.
*   `set timeout=M` هو مقدار الوقت بالثانية قبل بداية إقلاع النظام الافتراضي.
*   `menuentry "title" {entry options}` هو مدخلة العنوان `title`
*   `set root=(hdX,Y)` تحدد قسم الإقلاع ، حيث تم تخزين النواة ووحدات المحمل جروب (الإقلاع لا يحتاج إلى قسم مستقل ، ويمكن أن يكون ببساطة مجلدا منضويا تحت قسم "الجذر" (`/`)

مثال على الإعدادات:

```
/boot/grub/grub.cfg

```

```
# Config file for GRUB - The GNU GRand Unified Bootloader
# /boot/grub/grub.cfg

# DEVICE NAME CONVERSIONS
#
#  Linux           Grub
# -------------------------
#  /dev/fd0        (fd0)
#  /dev/sda        (hd0)
#  /dev/sdb2       (hd1,2)
#  /dev/sda3       (hd0,3)
#

# Timeout for menu
set timeout=5

# Set default boot entry as Entry 0
set default=0

# (0) Arch Linux
menuentry "Arch Linux" {
        set root=(hd0,1)
        linux /vmlinuz-linux root=/dev/sda3 ro
        initrd /initramfs-linux.img
}

## (1) Windows
#menuentry "Windows" {
#        set root=(hd0,3)
#        chainloader +1
#}

```

### الإقلاع المزدوج

**ملاحظة:** If you want GRUB to automatically search for other systems, you may wish to install [os-prober](https://www.archlinux.org/packages/?name=os-prober).

#### grub-mkconfig استخدام الأمر

The best way to add other entries is editing the `/etc/grub.d/40_custom` or `/boot/grub/custom.cfg` . The entries in this file will be automatically added when running `grub-mkconfig`. After adding the new lines, run:

```
# grub-mkconfig -o /boot/grub/grub.cfg 

```

to generate an updated `grub.cfg`.

##### مع نظام GNU/Linux

Assuming that the other distro is on partition `sda2`:

```
menuentry "Other Linux" {
        set root=(hd0,2)
        linux /boot/vmlinuz (add other options here as required)
        initrd /boot/initrd.img (if the other kernel uses/needs one)
}

```

##### مع نظام FreeBSD

Requires that FreeBSD is installed on a single partition with UFS. Assuming it is installed on `sda4`:

```
menuentry "FreeBSD" {
        set root=(hd0,4)
        chainloader +1
}

```

##### مع نظام وندوز

This assumes that your Windows partition is `sda3`. Remember you need to point set root and chainloader to the system reserve partition that windows made when it installed, not the actual partition windows is on. This example works if your system reserve partition is `sda3`.

```
# (2) Windows XP
menuentry "Windows XP" {
        set root=(hd0,3)
        chainloader (hd0,3)+1
}

```

If the Windows bootloader is on an entirely different hard drive than GRUB, it may be necessary to trick Windows into believing that it is the first hard drive. This was possible with `drivemap`. Assuming GRUB is on `hd0` and Windows is on `hd2`, you need to add the following after `set root`:

```
drivemap -s hd0 hd2

```

#### مع نظام وندوز باستخدام برنامج EasyBCD و NeoGRUB

وحيث إن برنامج NeoGRUB في EasyBCD لا يفهم صيغة قائمة GRUB ، قم بوضع محتويات ملف `C:\NST\menu.lst/` لديك بدلا من اﻷسطر التي تشبه ما يلي:

```
default 0
timeout 1

```

```
title       Chainload into GRUB v2
root        (hd0,7)
kernel      /boot/grub/i386-pc/core.img

```

### إعداد المحسنات البصرية

In GRUB it is possible, by default, to change the look of the menu. Make sure to initialize, if not done already, GRUB graphical terminal, gfxterm, with proper video mode, gfxmode, in GRUB. This can be seen in the section [#Correct No Suitable Mode Found Error](#Correct_No_Suitable_Mode_Found_Error). This video mode is passed by GRUB to the linux kernel via 'gfxpayload' so any visual configurations need this mode in order to be in effect.

#### ضبط دقة شاشة الإقلاع framebuffer

يستطيع GRUB ضبط ال framebuffer لكل من GRUB ذاته وللنواة أيضا. والطريقة `vga=` القديمة . الطريقة المفضلة هي تعديل الملف `/etc/default/grub/` كما يلي:

```
GRUB_GFXMODE=1024x768x32
GRUB_GFXPAYLOAD_LINUX=keep

```

لتفعيل هذه التغيرات نفذ:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

الخاصية `gfxpayload` ستتأكد من احتفاظ النواة بالدقة الجديدة .

**ملاحظة:** إذا لم يعمل المثال السابق جرب وضع `vbemode="0x105"` بدلا من `gfxmode="1024x768x32"` لتحديد دقة العرض مع ما يناسب شاشتك.

**ملاحظة:** لإظهار كافة الأنماط التي يمكنك استخدامها نفذ `# hwinfo --framebuffer` ، والحزمة hwinfo متوفرة في المستودع [community]. بينما في محث GRUB استخدم اﻷمر `vbeinfo`.

إن لم تعمل هذه الطريقة معك فإن الطريقة القديمة باستخدام المدخلة `vga=` ما زالت تعمل . قم فقط بإضافة مدخلة بعد السطر التالي `"GRUB_CMDLINE_LINUX_DEFAULT="` الموجود في الملف `/etc/default/grub` ، عل سبيل المثال ، `"GRUB_CMDLINE_LINUX_DEFAULT="quiet splash vga=792"` سيعطيك دقة `1024x768` . يمكنك الاختيار واحدة من هذه الدقات `640×480`, `800×600`, `1024×768`, `1280×1024`, `1600×1200`, `1920×1200`

#### 915resolution اﻷداة

بخصوص بطاقات إنتل الرسوميةأحيانا لا يقوم اﻷمر `# hwinfo --framebuffer` ولا `vbeinfo` بإظهار الدقة المطلوبة ، وفي هذه الحالة يمكنك استخدام اﻷداة `915resolution` . هذه اﻷداة تعدل مؤقتا برنامج تشغيل البطاقة وتضيف دقة الشاشة المطلوبة. انظر [915resolution's home page](http://915resolution.mango-lang.org/).

في البداية عليك أن تجد نمط الفيديو الذي ستقوم بتعديله لاحقا. ولذلك تحتاج إلى أحد أوامر صدفة GRUB :

 `sh:grub> 915resolution -l` 
```
Intel 800/900 Series VBIOS Hack : version 0.5.3
[...]
**Mode 30** : 640x480, 8 bits/pixel
[...]

```

Next, we overwrite the `Mode 30` with `1440x900` resolution:

 `/etc/grub.d/00_header` 
```
[...]
**915resolution 30 1440 900  # Inserted line**
set gfxmode=${GRUB_GFXMODE}
[...]

```

في النهاية سنحتاج إلى ضبط `GRUB_GFXMODE` كما شرحناه سابقا ، ثم نعيد توليد ملف تكوين GRUB وإعادة تشغيل الحاسوب لاختبار ما تم من تغييرات.

```
# grub-mkconfig -o /boot/grub/grub.cfg
# reboot

```

#### صورة الخلفية والخطوط النقطية

GRUB comes with support for background images and bitmap fonts in `pf2` format. The unifont font is included in the [grub-common](https://www.archlinux.org/packages/?name=grub-common) package under the filename `unicode.pf2`, or, as only ASCII characters under the name `ascii.pf2`.

Image formats supported include tga, png and jpeg, providing the correct modules are loaded. The maximum supported resolution depends on your hardware.

Make sure you have set up the proper [framebuffer resolution](#Setting_the_framebuffer_resolution).

Edit `/etc/default/grub` like this:

```
GRUB_BACKGROUND="/boot/grub/myimage"
#GRUB_THEME="/path/to/gfxtheme"
GRUB_FONT="/path/to/font.pf2"

```

**Note:** If you have installed GRUB on a separate partition, `/boot/grub/myimage` becomes `/grub/myimage`.

To generate the changes and add the information into `grub.cfg`, run:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

If adding the splash image was successful, the user will see `"Found background image..."` in the terminal as the command is executed. If this phrase is not seen, the image information was probably not incorporated into the `grub.cfg` file.

If the image is not displayed, check:

*   The path and the filename in `/etc/default/grub` are correct.
*   The image is of the proper size and format (tga, png, 8-bit jpg).
*   The image was saved in the RGB mode, and is not indexed.
*   The console mode is not enabled in `/etc/default/grub`.
*   The command `grub-mkconfig` must be executed to place the background image information into the `/boot/grub/grub.cfg` file.

#### المظهر Theme

Here is an example for configuring Starfield theme which was included in GRUB package.

Edit `/etc/default/grub`

```
GRUB_THEME="/usr/share/grub/themes/starfield/theme.txt"

```

Generate the changes:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

If configuring the theme was successful, you'll see `Found theme: /usr/share/grub/themes/starfield/theme.txt` in the terminal. Your splash image will usually not be displayed when using a theme.

#### ألوان القائمة

You can set the menu colors in GRUB. The available colors for GRUB can be found in [the GRUB Manual](https://www.gnu.org/software/grub/manual/html_node/Theme-file-format.html). Here is an example:

Edit `/etc/default/grub`:

```
GRUB_COLOR_NORMAL="light-blue/black"
GRUB_COLOR_HIGHLIGHT="light-cyan/blue"

```

Generate the changes:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

#### القائمة المخفية

One of the unique features of GRUB is hiding/skipping the menu and showing it by holding `Esc` when needed. You can also adjust whether you want to see the timeout counter.

Edit `/etc/default/grub` as you wish. Here is an example where the comments from the beginning of the two lines have been removed to enable the feature, the timeout has been set to five seconds and to be shown to the user:

```
GRUB_HIDDEN_TIMEOUT=5
GRUB_HIDDEN_TIMEOUT_QUIET=false

```

and run:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

#### إيقاف framebuffer

Users who use NVIDIA proprietary driver might wish to disable GRUB's framebuffer as it can cause problems with the binary driver.

To disable framebuffer, edit `/etc/default/grub` and uncomment the following line:

```
GRUB_TERMINAL_OUTPUT=console

```

and run:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

Another option if you want to keep the framebuffer in GRUB is to revert to text mode just before starting the kernel. To do that modify the variable in `/etc/default/grub`:

```
GRUB_GFXPAYLOAD_LINUX=text

```

and rebuild the configuration as before.

### خيارات أخرى

#### مدير القرص المنطقي LVM

If you use [LVM](/index.php/LVM "LVM") for your `/boot`, add the following before menuentry lines:

```
insmod lvm

```

and specify your root in the menuentry as:

```
set root=lvm/*lvm_group_name*-*lvm_logical_boot_partition_name*

```

Example:

```
# (0) Arch Linux
menuentry "Arch Linux" {
        insmod lvm
        set root=lvm/VolumeGroup-lv_boot
        # you can only set following two lines
        linux /vmlinuz-linux root=/dev/mapper/VolumeGroup-root ro
        initrd /initramfs-linux.img
}

```

#### أقراص RAID

GRUB provides convenient handling of RAID volumes. You need to add `insmod mdraid` which allows you to address the volume natively. For example, `/dev/md0` becomes:

```
set root=(md0)

```

whereas a partitioned RAID volume (e.g. `/dev/md0p1`) becomes:

```
set root=(md0,1)

```

#### Persistent block device naming

One naming scheme for [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") is the use of globally unique UUIDs to detect partitions instead of the "old" `/dev/sd*`. Advantages are covered up in the above linked article.

Persistent naming via filesystem UUIDs are used by default in GRUB.

**Note:** The `/boot/grub.cfg` file needs regeneration with the new UUID in `/etc/default/grub` every time a relevant filesystem is resized or recreated. Remember this when modifying partitions & filesystems with a Live-CD.

Whether to use UUIDs is controlled by an option in `/etc/default/grub`:

 `# GRUB_DISABLE_LINUX_UUID=true` 

Either way, do not forget to generate the changes:

 `# grub-mkconfig -o /boot/grub/grub.cfg` 

#### استخدام العناوين

It is possible to use labels, human-readable strings attached to filesystems, by using the `--label` option to `search`. First of all, label your existing partition:

```
# tune2fs -L <LABEL> <PARTITION>

```

Then, add an entry using labels. An example of this:

```
menuentry "Arch Linux, session texte" {
        search --label --set=root archroot
        linux /boot/vmlinuz-linux root=/dev/disk/by-label/archroot ro
        initrd /boot/initramfs-linux.img
}

```

#### استدعاء المدخلة الأخيرة

GRUB can remember the last entry you booted from and use this as the default entry to boot from next time. This is useful if you have multiple kernels (i.e., the current Arch one and the LTS kernel as a fallback option) or operating systems. To do this, edit `/etc/default/grub` and change the setting of `GRUB_DEFAULT`:

```
GRUB_DEFAULT=saved

```

This ensures that GRUB will default to the saved entry. To enable saving the selected entry, add the following line to `/etc/default/grub`:

```
GRUB_SAVEDEFAULT=true

```

**Note:** Manually added menu items, e.g. Windows in `/etc/grub.d/40_custom` or `/boot/grub/custom.cfg`, will need `savedefault` added. Remember to regenerate your configuration file.

#### الأمن

If you want to secure GRUB so it is not possible for anyone to change boot parameters or use the command line, you can add a user/password combination to GRUB's configuration files. To do this, run the command `grub-mkpasswd-pbkdf2`. Enter a password and confirm it:

 `grub-mkpasswd-pbkdf2` 
```
[...]
Your PBKDF2 is grub.pbkdf2.sha512.10000.C8ABD3E93C4DFC83138B0C7A3D719BC650E6234310DA069E6FDB0DD4156313DA3D0D9BFFC2846C21D5A2DDA515114CF6378F8A064C94198D0618E70D23717E82.509BFA8A4217EAD0B33C87432524C0B6B64B34FBAD22D3E6E6874D9B101996C5F98AB1746FE7C7199147ECF4ABD8661C222EEEDB7D14A843261FFF2C07B1269A

```

Then, add the following to `/etc/grub.d/00_header`:

 `/etc/grub.d/00_header` 
```
cat << EOF

set superusers="**username**"
password_pbkdf2 **username** **<password>**

EOF

```

where `<password>` is the string generated by `grub-mkpasswd_pbkdf2`.

Regenerate your configuration file. Your GRUB command line, boot parameters and all boot entries are now protected.

This can be relaxed and further customized with more users as described in the "Security" part of [the GRUB manual](https://www.gnu.org/software/grub/manual/grub.html#Security).

#### تشفير الجذر

To let GRUB automatically add the kernel parameters for root encryption, add `cryptdevice=/dev/yourdevice:label` to `GRUB_CMDLINE_LINUX` in `/etc/default/grub`.

Example with root mapped to `/dev/mapper/root`:

```
GRUB_CMDLINE_LINUX="cryptdevice=/dev/sda2:root"

```

Also, disable the usage of UUIDs for the rootfs:

```
GRUB_DISABLE_LINUX_UUID=true

```

Regenerate the configuration.

#### الإقلاع للنظام غير الافتراضي لمرة واحدة

The command `grub-reboot` is very helpful to boot another entry than the default only once. GRUB loads the entry passed in the first command line argument, when the system is rebooted the next time. Most importantly GRUB returns to loading the default entry for all future booting. Changing the configuration file or selecting an entry in the GRUB menu is not necessary.

**Note:** This requires `GRUB_DEFAULT=saved` in `/etc/default/grub` (and then regenerating `grub.cfg`) or, in case of hand-made `grub.cfg`, the line `set default="${saved_entry}"`.

### إقلاع ملف أيزو مباشرة من GRUB

Edit `/etc/grub.d/40_custom` or `/boot/grub/custom.cfg` to add an entry for the target ISO. When finished, update the GRUB menu as with the usual `grub-mkconfig -o /boot/grub/grub.cfg` (as root).

#### صورة Arch ISO

**Note:** The following examples assume the ISO is in `/archives` on `hd0,6`.

**Tip:** For thumbdrives, use something like `(hd1,$partition)` and either `/dev/sdb**Y**` for the `img_dev` parameter or [a persistent name](/index.php/Persistent_block_device_naming "Persistent block device naming"), e.g. `img_dev=/dev/disk/by-label/CORSAIR`.

##### معمارية x86_64

```
menuentry "Archlinux-2013.05.01-dual.iso" --class iso {
        set isofile="/archives/archlinux-2013.05.01-dual.iso"
        set partition="6"
        loopback loop (hd0,$partition)/$isofile
        linux (loop)/arch/boot/x86_64/vmlinuz archisolabel=ARCH_201305 img_dev=/dev/sda$partition img_loop=$isofile earlymodules=loop
        initrd (loop)/arch/boot/x86_64/archiso.img
}

```

##### معمارية i686

```
menuentry "Archlinux-2013.05.01-dual.iso" --class iso {
        set isofile="/archives/archlinux-2013.05.01-dual.iso"
        set partition="6"
        loopback loop (hd0,$partition)/$isofile
        linux (loop)/arch/boot/i686/vmlinuz archisolabel=ARCH_201305 img_dev=/dev/sda$partition img_loop=$isofile earlymodules=loop
        initrd (loop)/arch/boot/i686/archiso.img
}

```

#### Ubuntu ISO

**Note:** The example assumes that the iso is in `/archives` on `hd0,6`. Users must adjust the location and hdd/partition in the lines below to match their systems.

```
menuentry "ubuntu-13.04-desktop-amd64.iso" {
        set isofile="/archives/ubuntu-13.04-desktop-amd64.iso"
        loopback loop (hd0,6)/$isofile
        linux (loop)/casper/vmlinuz.efi boot=casper iso-scan/filename=$isofile quiet noeject noprompt splash --
        initrd (loop)/casper/initrd.lz
}

```

```
menuentry "ubuntu-12.04-desktop-amd64.iso" {
        set isofile="/archives/ubuntu-12.04-desktop-amd64.iso"
        loopback loop (hd0,6)/$isofile
        linux (loop)/casper/vmlinuz boot=casper iso-scan/filename=$isofile quiet noeject noprompt splash --
        initrd (loop)/casper/initrd.lz
}

```

#### صور أيزو أخرى

Other working configurations from [link Source](http://askubuntu.com/questions/141940/how-to-boot-live-iso-images).

## استخدام صدفة الأوامر

Since the MBR is too small to store all GRUB modules, only the menu and a few basic commands reside there. The majority of GRUB functionality remains in modules in `/boot/grub`, which are inserted as needed. In error conditions (e.g. if the partition layout changes) GRUB may fail to boot. When this happens, a command shell may appear.

GRUB offers multiple shells/prompts. If there is a problem reading the menu but the bootloader is able to find the disk, you will likely be dropped to the "normal" shell:

```
sh:grub>

```

If there is a more serious problem (e.g. GRUB cannot find required files), you may instead be dropped to the "rescue" shell:

```
grub rescue>

```

The rescue shell is a restricted subset of the normal shell, offering much less functionality. If dumped to the rescue shell, first try inserting the "normal" module, then starting the "normal" shell:

```
grub rescue> set prefix=(hdX,Y)/boot/grub
grub rescue> insmod (hdX,Y)/boot/grub/i386-pc/normal.mod
rescue:grub> normal

```

### دعم التصفح

GRUB supports pager for reading commands that provide long output (like the `help` command). This works only in normal shell mode and not in rescue mode. To enable pager, in GRUB command shell type:

```
sh:grub> set pager=1

```

## أدوات إعداد الواجهة الرسومية

Following package may be installed from [AUR](/index.php/AUR "AUR")

*   [grub-customizer](https://aur.archlinux.org/packages/grub-customizer/) (requires gettext gksu gtkmm hicolor-icon-theme openssl)

    	Customize the bootloader (GRUB or BURG)

*   [grub2-editor](https://aur.archlinux.org/packages/grub2-editor/) (requires kdelibs)

    	A KDE4 control module for configuring the GRUB bootloader

*   [kcm-grub2](https://aur.archlinux.org/packages/kcm-grub2/) (requires kdelibs python2-qt kdebindings-python)

    	This Kcm module manages the most common settings of GRUB.

*   [startupmanager](https://aur.archlinux.org/packages/startupmanager/) (requires gnome-python imagemagick yelp python2 xorg-xrandr)

    	GUI app for changing the settings of GRUB Legacy, GRUB, Usplash and Splashy

## parttool for hide/unhide

If you have a Windows 9x paradigm with hidden C:\ disks GRUB can hide/unhide it using `parttool`. For example, to boot the third C:\ disk of three Windows 9x installations on the CLI enter the CLI and:

```
parttool hd0,1 hidden+ boot-
parttool hd0,2 hidden+ boot-
parttool hd0,3 hidden- boot+
set root=hd0,3
chainloader +1
boot

```

## استخدام الشاشة النصية للإنقاذ

See [#Using the command shell](#Using_the_command_shell) first. If unable to activate the standard shell, one possible solution is to boot using a live CD or some other rescue disk to correct configuration errors and reinstall GRUB. However, such a boot disk is not always available (nor necessary); the rescue console is surprisingly robust.

The available commands in GRUB rescue include `insmod`, `ls`, `set`, and `unset`. This example uses `set` and `insmod`. `set` modifies variables and `insmod` inserts new modules to add functionality.

Before starting, the user must know the location of their `/boot` partition (be it a separate partition, or a subdirectory under their root):

```
grub rescue> set prefix=(hdX,Y)/boot/grub

```

where X is the physical drive number and Y is the partition number.

To expand console capabilities, insert the `linux` module:

```
grub rescue> insmod (hdX,Y)/boot/grub/linux.mod

```

**Note:** With a separate boot partition, omit `/boot` from the path, (i.e. type `set prefix=(hdX,Y)/grub` and `insmod (hdX,Y)/grub/linux.mod`).

This introduces the `linux` and `initrd` commands, which should be familiar (see [#Configuration](#Configuration)).

An example, booting Arch Linux:

```
set root=(hd0,5)
linux /boot/vmlinuz-linux root=/dev/sda5
initrd /boot/initramfs-linux.img
boot

```

With a separate boot partition, again change the lines accordingly:

```
set root=(hd0,5)
linux /vmlinuz-linux root=/dev/sda6
initrd /initramfs-linux.img
boot

```

After successfully booting the Arch Linux installation, users can correct `grub.cfg` as needed and then reinstall GRUB.

To reinstall GRUB and fix the problem completely, changing `/dev/sda` if needed. See [#Bootloader installation](#Bootloader_installation) for details.

## الجمع بين استخدام UUIDs والبرمجة النصية الأساسية

If you like the idea of using UUIDs to avoid unreliable BIOS mappings or are struggling with GRUB's syntax, here is an example boot menu item that uses UUIDs and a small script to direct GRUB to the proper disk partitions for your system. All you need to do is replace the UUIDs in the sample with the correct UUIDs for your system. The example applies to a system with a boot and root partition. You will obviously need to modify the GRUB configuration if you have additional partitions:

```
 menuentry "Arch Linux 64" {
         # Set the UUIDs for your boot and root partition respectively
         set the_boot_uuid=ece0448f-bb08-486d-9864-ac3271bd8d07
         set the_root_uuid=c55da16f-e2af-4603-9e0b-03f5f565ec4a

         # (Note: This may be the same as your boot partition)

         # Get the boot/root devices and set them in the root and grub_boot variables
         search --fs-uuid --set=root $the_root_uuid
         search --fs-uuid --set=grub_boot $the_boot_uuid

         # Check to see if boot and root are equal.
         # If they are, then append /boot to $grub_boot (Since $grub_boot is actually the root partition)
         if [ $the_boot_uuid == $the_root_uuid] ; then
             set grub_boot=$grub_boot/boot
         fi

         # $grub_boot now points to the correct location, so the following will properly find the kernel and initrd
         linux ($grub_boot)/vmlinuz-linux root=/dev/disk/by-uuid/$uuid_os_root ro
         initrd ($grub_boot)/initramfs-linux.img
 }

```

## استكشاف الأخطاء وإصلاحها

### بيوس إنتل لا يقلع مع GPT

Some Intel BIOS's require at least one bootable MBR partition to be present at boot, causing GPT-partitioned boot setups to be unbootable.

This can be circumvented by using (for instance) fdisk to mark one of the GPT partitions (preferably the 1007 KiB partition you've created for GRUB already) bootable in the MBR. This can be achieved, using fdisk, by the following commands: Start fdisk against the disk you're installing, for instance `fdisk /dev/sda`, then press `a` and select the partition you wish to mark as bootable (probably #1) by pressing the corresponding number, finally press `w` to write the changes to the MBR.

**Note:** The bootable-marking must be done in `fdisk` or similar, not in GParted or others, as they will not set the bootable flag in the MBR.

More information is available [here](http://www.rodsbooks.com/gdisk/bios.html)

### تفعيل رسائل إصلاح العلل

Add:

```
set pager=1
set debug=all

```

to `grub.cfg`.

### تصحيح الخطأ No Suitable Mode Found

If you get this error when booting any menuentry:

```
error: no suitable mode found
Booting however

```

Then you need to initialize GRUB graphical terminal (`gfxterm`) with proper video mode (`gfxmode`) in GRUB. This video mode is passed by GRUB to the linux kernel via 'gfxpayload'. In case of UEFI systems, if the GRUB video mode is not initialized, no kernel boot messages will be shown in the terminal (atleast until KMS kicks in).

Copy `/usr/share/grub/unicode.pf2` to ${GRUB_PREFIX_DIR} (`/boot/grub/` in case of BIOS and UEFI systems). If GRUB UEFI was installed with `--boot-directory=/boot/efi/EFI` set, then the directory is `/boot/efi/EFI/grub/`:

```
# cp /usr/share/grub/unicode.pf2 ${GRUB_PREFIX_DIR}

```

If `/usr/share/grub/unicode.pf2` does not exist, install [bdf-unifont](https://www.archlinux.org/packages/?name=bdf-unifont), create the `unifont.pf2` file and then copy it to `${GRUB_PREFIX_DIR}`:

```
# grub-mkfont -o unicode.pf2 /usr/share/fonts/misc/unifont.bdf

```

Then, in the `grub.cfg` file, add the following lines to enable GRUB to pass the video mode correctly to the kernel, without of which you will only get a black screen (no output) but booting (actually) proceeds successfully without any system hang.

BIOS systems:

```
insmod vbe

```

UEFI systems:

```
insmod efi_gop
insmod efi_uga

```

After that add the following code (common to both BIOS and UEFI):

```
insmod font

```

```
if loadfont ${prefix}/fonts/unicode.pf2
then
    insmod gfxterm
    set gfxmode=auto
    set gfxpayload=keep
    terminal_output gfxterm
fi

```

As you can see for gfxterm (graphical terminal) to function properly, `unicode.pf2` font file should exist in `${GRUB_PREFIX_DIR}`.

### رسالة خطأ msdos-style

```
grub-setup: warn: This msdos-style partition label has no post-MBR gap; embedding won't be possible!
grub-setup: warn: Embedding is not possible. GRUB can only be installed in this setup by using blocklists.
            However, blocklists are UNRELIABLE and its use is discouraged.
grub-setup: error: If you really want blocklists, use --force.

```

This error may occur when you try installing GRUB in a VMware container. Read more about it [here](https://bbs.archlinux.org/viewtopic.php?pid=581760#p581760). It happens when the first partition starts just after the MBR (block 63), without the usual space of 1 MiB (2048 blocks) before the first partition. Read [#Master Boot Record (MBR) specific instructions](#Master_Boot_Record_.28MBR.29_specific_instructions)

### GRUB UEFI يدخل على نمط صدفةالإنقاذ

If GRUB loads but drops you into the rescue shell with no errors, it may be because of a missing or misplaced `grub.cfg`. This will happen if GRUB UEFI was installed with `--boot-directory` and `grub.cfg` is missing OR if the partition number of the boot partition changed (which is hard-coded into the `grubx64.efi` file).

### GRUB UEFI لا يقلع

An example of a working EFI:

 `# efibootmgr -v` 
```
BootCurrent: 0000
Timeout: 3 seconds
BootOrder: 0000,0001,0002
Boot0000* Grub	HD(1,800,32000,23532fbb-1bfa-4e46-851a-b494bfe9478c)File(\efi\grub\grub.efi)
Boot0001* Shell	HD(1,800,32000,23532fbb-1bfa-4e46-851a-b494bfe9478c)File(\EfiShell.efi)
Boot0002* Festplatte	BIOS(2,0,00)P0: SAMSUNG HD204UI

```

If the screen only goes black for a second and the next boot option is tried afterwards, according to [this post](https://bbs.archlinux.org/viewtopic.php?pid=981560#p981560), moving GRUB to the partition root can help. The boot option has to be deleted and recreated afterwards. The entry for GRUB should look like this then:

```
Boot0000* Grub	HD(1,800,32000,23532fbb-1bfa-4e46-851a-b494bfe9478c)File(\grub.efi)

```

### توقيع غير صالح

If trying to boot Windows results in an "invalid signature" error, e.g. after reconfiguring partitions or adding additional hard drives, (re)move GRUB's device configuration and let it reconfigure:

```
# mv /boot/grub/device.map /boot/grub/device.map-old
# grub-mkconfig -o /boot/grub/grub.cfg

```

`grub-mkconfig` should now mention all found boot options, including Windows. If it works, remove `/boot/grub/device.map-old`.

### تجمد عملية الإقلاع

If booting gets stuck without any error message after GRUB loading the kernel and the initial ramdisk, try removing the `add_efi_memmap` kernel parameter.

### استرجاع إصدار GRUB القديم

*   Move GRUB2 files out of the way:

```
# mv /boot/grub /boot/grub.nonfunctional

```

*   Copy GRUB Legacy back to `/boot`:

```
# cp -af /boot/grub-legacy /boot/grub

```

*   Replace MBR and next 62 sectors of sda with backed up copy

**Warning:** This command also restores the partition table, so be careful of overwriting a modified partition table with the old one. It **will** mess up your system.

```
# dd if=/path/to/backup/first-sectors of=/dev/sdX bs=512 count=1

```

A safer way is to restore only the MBR boot code use:

```
# dd if=/path/to/backup/mbr-boot-code of=/dev/sdX bs=446 count=1

```

## المراجع

1.  Official GRUB Manual - [https://www.gnu.org/software/grub/manual/grub.html](https://www.gnu.org/software/grub/manual/grub.html)
2.  Ubuntu wiki page for GRUB - [https://help.ubuntu.com/community/Grub2](https://help.ubuntu.com/community/Grub2)
3.  GRUB wiki page describing steps to compile for UEFI systems - [https://help.ubuntu.com/community/UEFIBooting](https://help.ubuntu.com/community/UEFIBooting)
4.  Wikipedia's page on [BIOS Boot partition](https://en.wikipedia.org/wiki/BIOS_Boot_partition "wikipedia:BIOS Boot partition")

## روابط خارجية

1.  [A Linux Bash Shell script to compile and install GRUB for BIOS from BZR Source](https://github.com/the-ridikulus-rat/My_Shell_Scripts/blob/master/grub/grub_bios.sh)
2.  [A Linux Bash Shell script to compile and install GRUB for UEFI from BZR Source](https://github.com/the-ridikulus-rat/My_Shell_Scripts/blob/master/grub/grub_uefi.sh)