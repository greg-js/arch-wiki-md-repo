جاء تعريفًا من [صفحة المشروع](http://freedesktop.org/wiki/Software/systemd):

***النظام الرابع Systemd** هو مدير للنظام و الخدمات في لينكس ، متوافق مع المخطوطات الابتدائية بنوعيها SysV و LSB . يعمل **systemd** مقدّمًا قدرات الرد المتوازي ، مستعملًا نشاطي socket و [D-Bus](/index.php/D-Bus "D-Bus") في تشغيل الخدمات ، عارضًا مقدّمات التشغيل مسبقة الطلب من المخدّمات ، محافظًا على قطاع العمليات من خلال [مجموعات التحكم](/index.php/Cgroups "Cgroups") في لينكس ، داعمًا التوقف الفوري لحالة النظام و الاستمرارية فيما بعد ، مديرًا لنقاط الوصل و الوصل التلقائي ، منفّذًا معاملات المنطق الخدمي التحكمي القائمة على التّبعية . Systemd يشكل بديلًا متكاملًا لبرنامج [sysvinit](/index.php/SysVinit "SysVinit") .*

**ملاحظة: لمعرفة مزيد من التفاصيل عن أسباب انتقال Arch إلى systemd ، انظر [منشور المنتدى](https://bbs.archlinux.org/viewtopic.php?pid=1149530#p1149530).** :

انظر أيضًا مقالة systemd [في ويكيبيديا](https://en.wikipedia.org/wiki/Systemd "wikipedia:Systemd").

## Contents

*   [1 تحضيرات قبل التحوّل](#.D8.AA.D8.AD.D8.B6.D9.8A.D8.B1.D8.A7.D8.AA_.D9.82.D8.A8.D9.84_.D8.A7.D9.84.D8.AA.D8.AD.D9.88.D9.91.D9.84)
*   [2 التثبيت](#.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA)
    *   [2.1 معلومات إضافية](#.D9.85.D8.B9.D9.84.D9.88.D9.85.D8.A7.D8.AA_.D8.A5.D8.B6.D8.A7.D9.81.D9.8A.D8.A9)
*   [3 الإعدادات الأصلية](#.D8.A7.D9.84.D8.A5.D8.B9.D8.AF.D8.A7.D8.AF.D8.A7.D8.AA_.D8.A7.D9.84.D8.A3.D8.B5.D9.84.D9.8A.D8.A9)
    *   [3.1 الطرفية الافتراضية](#.D8.A7.D9.84.D8.B7.D8.B1.D9.81.D9.8A.D8.A9_.D8.A7.D9.84.D8.A7.D9.81.D8.AA.D8.B1.D8.A7.D8.B6.D9.8A.D8.A9)
    *   [3.2 ساعة العتاد](#.D8.B3.D8.A7.D8.B9.D8.A9_.D8.A7.D9.84.D8.B9.D8.AA.D8.A7.D8.AF)
        *   [3.2.1 ساعة العتاد بالتوقيت المحلّي](#.D8.B3.D8.A7.D8.B9.D8.A9_.D8.A7.D9.84.D8.B9.D8.AA.D8.A7.D8.AF_.D8.A8.D8.A7.D9.84.D8.AA.D9.88.D9.82.D9.8A.D8.AA_.D8.A7.D9.84.D9.85.D8.AD.D9.84.D9.91.D9.8A)
    *   [3.3 وحدات النّواة](#.D9.88.D8.AD.D8.AF.D8.A7.D8.AA_.D8.A7.D9.84.D9.86.D9.91.D9.88.D8.A7.D8.A9)
        *   [3.3.1 الوحدات الإضافية المعدّة للتحميل مع الإقلاع](#.D8.A7.D9.84.D9.88.D8.AD.D8.AF.D8.A7.D8.AA_.D8.A7.D9.84.D8.A5.D8.B6.D8.A7.D9.81.D9.8A.D8.A9_.D8.A7.D9.84.D9.85.D8.B9.D8.AF.D9.91.D8.A9_.D9.84.D9.84.D8.AA.D8.AD.D9.85.D9.8A.D9.84_.D9.85.D8.B9_.D8.A7.D9.84.D8.A5.D9.82.D9.84.D8.A7.D8.B9)
        *   [3.3.2 إعداد خيارات الوحدات](#.D8.A5.D8.B9.D8.AF.D8.A7.D8.AF_.D8.AE.D9.8A.D8.A7.D8.B1.D8.A7.D8.AA_.D8.A7.D9.84.D9.88.D8.AD.D8.AF.D8.A7.D8.AA)
        *   [3.3.3 الحظر](#.D8.A7.D9.84.D8.AD.D8.B8.D8.B1)
    *   [3.4 وصل نظام الملفات](#.D9.88.D8.B5.D9.84_.D9.86.D8.B8.D8.A7.D9.85_.D8.A7.D9.84.D9.85.D9.84.D9.81.D8.A7.D8.AA)
        *   [3.4.1 الوصل التلقائي](#.D8.A7.D9.84.D9.88.D8.B5.D9.84_.D8.A7.D9.84.D8.AA.D9.84.D9.82.D8.A7.D8.A6.D9.8A)
        *   [3.4.2 إدارة الأقسام المنطقية ( LVM )](#.D8.A5.D8.AF.D8.A7.D8.B1.D8.A9_.D8.A7.D9.84.D8.A3.D9.82.D8.B3.D8.A7.D9.85_.D8.A7.D9.84.D9.85.D9.86.D8.B7.D9.82.D9.8A.D8.A9_.28_LVM_.29)
    *   [3.5 إدارة الطاقة ( من خلال البوابة المتقدمة ACPI )](#.D8.A5.D8.AF.D8.A7.D8.B1.D8.A9_.D8.A7.D9.84.D8.B7.D8.A7.D9.82.D8.A9_.28_.D9.85.D9.86_.D8.AE.D9.84.D8.A7.D9.84_.D8.A7.D9.84.D8.A8.D9.88.D8.A7.D8.A8.D8.A9_.D8.A7.D9.84.D9.85.D8.AA.D9.82.D8.AF.D9.85.D8.A9_ACPI_.29)
        *   [3.5.1 المُعَلِّقات](#.D8.A7.D9.84.D9.85.D9.8F.D8.B9.D9.8E.D9.84.D9.90.D9.91.D9.82.D8.A7.D8.AA)
            *   [3.5.1.1 ملفات خدمات التّعليق و الاستكمال](#.D9.85.D9.84.D9.81.D8.A7.D8.AA_.D8.AE.D8.AF.D9.85.D8.A7.D8.AA_.D8.A7.D9.84.D8.AA.D9.91.D8.B9.D9.84.D9.8A.D9.82_.D9.88_.D8.A7.D9.84.D8.A7.D8.B3.D8.AA.D9.83.D9.85.D8.A7.D9.84)
            *   [3.5.1.2 الملف المُجَمَّع لخدمات التعليق و الاستكمال](#.D8.A7.D9.84.D9.85.D9.84.D9.81_.D8.A7.D9.84.D9.85.D9.8F.D8.AC.D9.8E.D9.85.D9.8E.D9.91.D8.B9_.D9.84.D8.AE.D8.AF.D9.85.D8.A7.D8.AA_.D8.A7.D9.84.D8.AA.D8.B9.D9.84.D9.8A.D9.82_.D9.88_.D8.A7.D9.84.D8.A7.D8.B3.D8.AA.D9.83.D9.85.D8.A7.D9.84)
            *   [3.5.1.3 المُعَلِّقات في /usr/lib/systemd/system-sleep](#.D8.A7.D9.84.D9.85.D9.8F.D8.B9.D9.8E.D9.84.D9.90.D9.91.D9.82.D8.A7.D8.AA_.D9.81.D9.8A_.2Fusr.2Flib.2Fsystemd.2Fsystem-sleep)
    *   [3.6 الملفات المؤقّتة](#.D8.A7.D9.84.D9.85.D9.84.D9.81.D8.A7.D8.AA_.D8.A7.D9.84.D9.85.D8.A4.D9.82.D9.91.D8.AA.D8.A9)
    *   [3.7 الوحدات](#.D8.A7.D9.84.D9.88.D8.AD.D8.AF.D8.A7.D8.AA)
*   [4 الاستخدام الأوّلي لأداة systemctl](#.D8.A7.D9.84.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_.D8.A7.D9.84.D8.A3.D9.88.D9.91.D9.84.D9.8A_.D9.84.D8.A3.D8.AF.D8.A7.D8.A9_systemctl)
    *   [4.1 تحليل حالة النظام](#.D8.AA.D8.AD.D9.84.D9.8A.D9.84_.D8.AD.D8.A7.D9.84.D8.A9_.D8.A7.D9.84.D9.86.D8.B8.D8.A7.D9.85)
    *   [4.2 استخدام الوحدات](#.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_.D8.A7.D9.84.D9.88.D8.AD.D8.AF.D8.A7.D8.AA)
    *   [4.3 إدارة الطّاقة](#.D8.A5.D8.AF.D8.A7.D8.B1.D8.A9_.D8.A7.D9.84.D8.B7.D9.91.D8.A7.D9.82.D8.A9)
*   [5 تشغيل المُخدّمات الرسومية في systemd](#.D8.AA.D8.B4.D8.BA.D9.8A.D9.84_.D8.A7.D9.84.D9.85.D9.8F.D8.AE.D8.AF.D9.91.D9.85.D8.A7.D8.AA_.D8.A7.D9.84.D8.B1.D8.B3.D9.88.D9.85.D9.8A.D8.A9_.D9.81.D9.8A_systemd)
    *   [5.1 استخدام مدير الولوج systemd-logind](#.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_.D9.85.D8.AF.D9.8A.D8.B1_.D8.A7.D9.84.D9.88.D9.84.D9.88.D8.AC_systemd-logind)
*   [6 كتابة ملفات تخصصية بتنسيق .service](#.D9.83.D8.AA.D8.A7.D8.A8.D8.A9_.D9.85.D9.84.D9.81.D8.A7.D8.AA_.D8.AA.D8.AE.D8.B5.D8.B5.D9.8A.D8.A9_.D8.A8.D8.AA.D9.86.D8.B3.D9.8A.D9.82_.service)
    *   [6.1 استنباط الاعتماديّات](#.D8.A7.D8.B3.D8.AA.D9.86.D8.A8.D8.A7.D8.B7_.D8.A7.D9.84.D8.A7.D8.B9.D8.AA.D9.85.D8.A7.D8.AF.D9.8A.D9.91.D8.A7.D8.AA)
    *   [6.2 النوع](#.D8.A7.D9.84.D9.86.D9.88.D8.B9)
    *   [6.3 تحرير ملفات الوحدات المضافة](#.D8.AA.D8.AD.D8.B1.D9.8A.D8.B1_.D9.85.D9.84.D9.81.D8.A7.D8.AA_.D8.A7.D9.84.D9.88.D8.AD.D8.AF.D8.A7.D8.AA_.D8.A7.D9.84.D9.85.D8.B6.D8.A7.D9.81.D8.A9)
    *   [6.4 تسليط الضوء على بناء الوحدات بواسطة Vim](#.D8.AA.D8.B3.D9.84.D9.8A.D8.B7_.D8.A7.D9.84.D8.B6.D9.88.D8.A1_.D8.B9.D9.84.D9.89_.D8.A8.D9.86.D8.A7.D8.A1_.D8.A7.D9.84.D9.88.D8.AD.D8.AF.D8.A7.D8.AA_.D8.A8.D9.88.D8.A7.D8.B3.D8.B7.D8.A9_Vim)
*   [7 الأهداف](#.D8.A7.D9.84.D8.A3.D9.87.D8.AF.D8.A7.D9.81)
    *   [7.1 الأهداف الحالية](#.D8.A7.D9.84.D8.A3.D9.87.D8.AF.D8.A7.D9.81_.D8.A7.D9.84.D8.AD.D8.A7.D9.84.D9.8A.D8.A9)
    *   [7.2 إنشاء هدف معيّن](#.D8.A5.D9.86.D8.B4.D8.A7.D8.A1_.D9.87.D8.AF.D9.81_.D9.85.D8.B9.D9.8A.D9.91.D9.86)
    *   [7.3 جدولة الاهداف](#.D8.AC.D8.AF.D9.88.D9.84.D8.A9_.D8.A7.D9.84.D8.A7.D9.87.D8.AF.D8.A7.D9.81)
    *   [7.4 تغيير الهدف الحالي](#.D8.AA.D8.BA.D9.8A.D9.8A.D8.B1_.D8.A7.D9.84.D9.87.D8.AF.D9.81_.D8.A7.D9.84.D8.AD.D8.A7.D9.84.D9.8A)
    *   [7.5 تغيير الهدف الافتراضي للإقلاع من خلاله](#.D8.AA.D8.BA.D9.8A.D9.8A.D8.B1_.D8.A7.D9.84.D9.87.D8.AF.D9.81_.D8.A7.D9.84.D8.A7.D9.81.D8.AA.D8.B1.D8.A7.D8.B6.D9.8A_.D9.84.D9.84.D8.A5.D9.82.D9.84.D8.A7.D8.B9_.D9.85.D9.86_.D8.AE.D9.84.D8.A7.D9.84.D9.87)
*   [8 الدّوريّات](#.D8.A7.D9.84.D8.AF.D9.91.D9.88.D8.B1.D9.8A.D9.91.D8.A7.D8.AA)
    *   [8.1 تنقيح المُخرجات](#.D8.AA.D9.86.D9.82.D9.8A.D8.AD_.D8.A7.D9.84.D9.85.D9.8F.D8.AE.D8.B1.D8.AC.D8.A7.D8.AA)
    *   [8.2 الحجم الأقصى للدّورية](#.D8.A7.D9.84.D8.AD.D8.AC.D9.85_.D8.A7.D9.84.D8.A3.D9.82.D8.B5.D9.89_.D9.84.D9.84.D8.AF.D9.91.D9.88.D8.B1.D9.8A.D8.A9)
    *   [8.3 الترابط بين مدير الدّوريات journald و سجل النظام syslog](#.D8.A7.D9.84.D8.AA.D8.B1.D8.A7.D8.A8.D8.B7_.D8.A8.D9.8A.D9.86_.D9.85.D8.AF.D9.8A.D8.B1_.D8.A7.D9.84.D8.AF.D9.91.D9.88.D8.B1.D9.8A.D8.A7.D8.AA_journald_.D9.88_.D8.B3.D8.AC.D9.84_.D8.A7.D9.84.D9.86.D8.B8.D8.A7.D9.85_syslog)
*   [9 التّحسين](#.D8.A7.D9.84.D8.AA.D9.91.D8.AD.D8.B3.D9.8A.D9.86)
    *   [9.1 تحليل عملية الإقلاع](#.D8.AA.D8.AD.D9.84.D9.8A.D9.84_.D8.B9.D9.85.D9.84.D9.8A.D8.A9_.D8.A7.D9.84.D8.A5.D9.82.D9.84.D8.A7.D8.B9)
        *   [9.1.1 استخدام أداة التحليل systemd-analyze](#.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_.D8.A3.D8.AF.D8.A7.D8.A9_.D8.A7.D9.84.D8.AA.D8.AD.D9.84.D9.8A.D9.84_systemd-analyze)
        *   [9.1.2 استخدام راسم خريطة الإقلاع systemd-bootchart](#.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_.D8.B1.D8.A7.D8.B3.D9.85_.D8.AE.D8.B1.D9.8A.D8.B7.D8.A9_.D8.A7.D9.84.D8.A5.D9.82.D9.84.D8.A7.D8.B9_systemd-bootchart)
        *   [9.1.3 المرحلة الثانية من رسم خريطة الإقلاع](#.D8.A7.D9.84.D9.85.D8.B1.D8.AD.D9.84.D8.A9_.D8.A7.D9.84.D8.AB.D8.A7.D9.86.D9.8A.D8.A9_.D9.85.D9.86_.D8.B1.D8.B3.D9.85_.D8.AE.D8.B1.D9.8A.D8.B7.D8.A9_.D8.A7.D9.84.D8.A5.D9.82.D9.84.D8.A7.D8.B9)
*   [10 استكشاف الاخطاء و إصلاحها](#.D8.A7.D8.B3.D8.AA.D9.83.D8.B4.D8.A7.D9.81_.D8.A7.D9.84.D8.A7.D8.AE.D8.B7.D8.A7.D8.A1_.D9.88_.D8.A5.D8.B5.D9.84.D8.A7.D8.AD.D9.87.D8.A7)
    *   [10.1 الوقت الطّويل لإيقاف أو إعادة التّشغيل](#.D8.A7.D9.84.D9.88.D9.82.D8.AA_.D8.A7.D9.84.D8.B7.D9.91.D9.88.D9.8A.D9.84_.D9.84.D8.A5.D9.8A.D9.82.D8.A7.D9.81_.D8.A3.D9.88_.D8.A5.D8.B9.D8.A7.D8.AF.D8.A9_.D8.A7.D9.84.D8.AA.D9.91.D8.B4.D8.BA.D9.8A.D9.84)
    *   [10.2 عدم وجود مُخرجات للتطبيقات قصيرة العُمر](#.D8.B9.D8.AF.D9.85_.D9.88.D8.AC.D9.88.D8.AF_.D9.85.D9.8F.D8.AE.D8.B1.D8.AC.D8.A7.D8.AA_.D9.84.D9.84.D8.AA.D8.B7.D8.A8.D9.8A.D9.82.D8.A7.D8.AA_.D9.82.D8.B5.D9.8A.D8.B1.D8.A9_.D8.A7.D9.84.D8.B9.D9.8F.D9.85.D8.B1)
    *   [10.3 تشخيص مشاكل الإقلاع](#.D8.AA.D8.B4.D8.AE.D9.8A.D8.B5_.D9.85.D8.B4.D8.A7.D9.83.D9.84_.D8.A7.D9.84.D8.A5.D9.82.D9.84.D8.A7.D8.B9)
    *   [10.4 تعطيل التطبيقات مسببة الانهيار](#.D8.AA.D8.B9.D8.B7.D9.8A.D9.84_.D8.A7.D9.84.D8.AA.D8.B7.D8.A8.D9.8A.D9.82.D8.A7.D8.AA_.D9.85.D8.B3.D8.A8.D8.A8.D8.A9_.D8.A7.D9.84.D8.A7.D9.86.D9.87.D9.8A.D8.A7.D8.B1)
*   [11 انظر أيضًا](#.D8.A7.D9.86.D8.B8.D8.B1_.D8.A3.D9.8A.D8.B6.D9.8B.D8.A7)

## تحضيرات قبل التحوّل

*   اقرأ [بعض المعلومات](http://freedesktop.org/wiki/Software/systemd/) عن systemd.
*   لاحظ أن حقيقة systemd أنه نظام **دوريّ** التسجيل يقوم مقام أداة **syslog** ، ومع ذلك يمكن لهما أن يتعايشا معًا . راجع [الدّوريّات](#.D8.A7.D9.84.D8.AF.D9.91.D9.88.D8.B1.D9.8A.D9.91.D8.A7.D8.AA) أدناه .
*   على الرّغم من إمكانية systemd على استبدال بعض وظائف **cron** و **acoid** و **xinetd** ، إلا أنه لا داعِ للتحول الكامل من المُخدّمات التقليدية ما لم ترغب في ذلك .
*   المخطوطات الابتدائية التفاعلية لا تعمل من خلال systemd . خصوصًا مخطوطة قائمة إعداد الشبكة netcfg-menu [لا يمكن](https://bugs.archlinux.org/task/31377) أن تعمل أثناء الإقلاع .

## التثبيت

**ملاحظة:** كلًّا من الأداتين [systemd](https://www.archlinux.org/packages/?name=systemd) و [systemd-sysvcompat](https://www.archlinux.org/packages/?name=systemd-sysvcompat) مثبّتتان افتراضيًّا في وسيط التثبيت منذ [2012-10-13](https://www.archlinux.org/news/systemd-is-now-the-default-on-new-installations/).

**ملاحظة:** إذا هممت بتشغيل أرتش لينُكس داخل VPS ، راجِع [الخيارات الملاءمة](/index.php/Virtual_Private_Server#Moving_your_VPS_from_initscripts_to_systemd "Virtual Private Server").

The following section is aimed at Arch Linux installations that still rely on [sysvinit](https://aur.archlinux.org/packages/sysvinit/) and initscripts which have not migrated to [systemd](https://www.archlinux.org/packages/?name=systemd).

1.  Install [systemd](https://www.archlinux.org/packages/?name=systemd) and append the following to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"): `init=/usr/lib/systemd/systemd`
2.  Once completed you may enable any desired services via the use of `systemctl enable <service_name>` (this roughly equates to what you included in the `DAEMONS` array. New names can be found [here](/index.php/Daemons_List "Daemons List")).
3.  Reboot your system and verify that `systemd` is currently active by issuing the following command: `cat /proc/1/comm`. This should return the string `systemd`.
4.  Make sure your hostname is set correctly under systemd: `hostnamectl set-hostname myhostname`.
5.  Proceed to remove initscripts and sysvinit from your system and install [systemd-sysvcompat](https://www.archlinux.org/packages/?name=systemd-sysvcompat).
6.  Optionally, remove the `init=/usr/lib/systemd/systemd` parameter as it is no longer needed. [systemd-sysvcompat](https://www.archlinux.org/packages/?name=systemd-sysvcompat) provides the default init.

### معلومات إضافية

*   If you have `quiet` in your kernel parameters, you might want to remove it for your first couple of systemd boots, to assist with identifying any issues during boot.

*   Adding your user to [groups](/index.php/Users_and_groups "Users and groups") (`sys`, `disk`, `lp`, `network`, `video`, `audio`, `optical`, `storage`, `scanner`, `power`, etc.) is **not** necessary for most use cases with systemd. The groups can even cause some functionality to break. For example, the `audio` group will break fast user switching and allows applications to block software mixing. Every PAM login provides a logind session, which for a local session will give you permissions via [POSIX ACLs](https://en.wikipedia.org/wiki/Access_control_list "wikipedia:Access control list") on audio/video devices, and allow certain operations like mounting removable storage via [udisks](/index.php/Udisks "Udisks").

*   See the [Network configuration](/index.php/Network_configuration "Network configuration") article for how to set up networking targets.

## الإعدادات الأصلية

**Note:** قد تحتاج إنشاء هذه الملفات. جميعها يجب أن تخضع للترخيص `644` و لملكية الجذر `root:root`.

### الطرفية الافتراضية

The virtual console (keyboard mapping, console font and console map) is configured in `/etc/vconsole.conf`:

 `/etc/vconsole.conf` 
```
KEYMAP=us
FONT=lat9w-16
FONT_MAP=8859-1_to_uni
```

**Note:** As of [systemd](https://www.archlinux.org/packages/?name=systemd)-194, the built-in *kernel* font and the *us* keymap are used if `KEYMAP=` and `FONT=` are empty or not set.

Another way to set the keyboard mapping (keymap) is doing:

```
# localectl set-keymap de

```

`localectl` can also be used to set the X11 keymap:

```
# localectl set-x11-keymap de

```

See [localectl(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/localectl.1) and [vconsole.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5) for details.

*   For more information, see [console fonts](/index.php/Fonts#Console_fonts "Fonts") and [keymaps](/index.php/KEYMAP "KEYMAP").

### ساعة العتاد

Systemd will use **UTC** for the hardware clock by default.

**Tip:** It is advised to have a [Network Time Protocol daemon](/index.php/NTP "NTP") running to keep the system time synchronized with Internet time and the hardware clock.

#### ساعة العتاد بالتوقيت المحلّي

If you want to change the hardware clock to use local time (**STRONGLY DISCOURAGED**) do:

```
# timedatectl set-local-rtc true

```

If you want to revert to the hardware clock being in UTC, do:

```
# timedatectl set-local-rtc false

```

Be warned that, if the hardware clock is set to localtime, dealing with daylight saving time is messy. If the DST changes when your computer is off, your clock will be wrong on next boot ([there is a lot more to it](http://www.cl.cam.ac.uk/~mgk25/mswish/ut-rtc.html)). Recent kernels set the system time from the RTC directly on boot, assuming that the RTC is in UTC. This means that if the RTC is in local time, then the system time will first be set up wrongly and then corrected shortly afterwards on every boot. This is the root of certain weird bugs (time going backwards is rarely a good thing).

One reason for allowing the RTC to be in local time is to allow dual boot with Windows ([which uses localtime](http://blogs.msdn.com/b/oldnewthing/archive/2004/09/02/224672.aspx)). However, Windows is able to deal with the RTC being in UTC with a simple [registry fix](/index.php/Time#UTC_in_Windows "Time"). It is recommended to configure Windows to use UTC, rather than Linux to use localtime. If you make Windows use UTC, also remember to disable the "Internet Time Update" Windows feature, so that Windows don't mess with the hardware clock, trying to sync it with internet time. You should instead leave touching the RTC and syncing it to internet time to Linux, by enabling an [NTP](/index.php/NTP "NTP") daemon, as suggested previously.

*   For more information, see [Time](/index.php/Time "Time").

### وحدات النّواة

Today, all necessary module loading is handled automatically by [udev](/index.php/Udev "Udev"), so that, if you don't want/need to use any out-of-tree kernel modules, there is no need to put modules that should be loaded at boot in any config file. However, there are cases where you might want to load an extra module during the boot process, or blacklist another one for your computer to function properly.

#### الوحدات الإضافية المعدّة للتحميل مع الإقلاع

Extra kernel modules to be loaded during boot are configured as a static list in files under `/etc/modules-load.d/`. Each configuration file is named in the style of `/etc/modules-load.d/<program>.conf`. Configuration files simply contain a list of kernel module names to load, separated by newlines. Empty lines and lines whose first non-whitespace character is `#` or `;` are ignored.

 `/etc/modules-load.d/virtio-net.conf` 
```
# Load virtio-net.ko at boot
virtio-net
```

See [modules-load.d(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/modules-load.d.5) for more details.

#### إعداد خيارات الوحدات

Additional module options must be set in the `/etc/modprobe.d/modprobe.conf`.

Example:

*   we have `/etc/modules-load.d/loop.conf` with module `loop` inside to load during the boot.

*   in the `/etc/modprobe.d/modprobe.conf` specify the additional options, e.g. `options loop max_loop=64`

Afterwards, the newly set option might be verified via `cat /sys/module/loop/parameters/max_loop`

#### الحظر

Module blacklisting works the same way as with [initscripts](https://www.archlinux.org/packages/?name=initscripts) since it is actually handled by [kmod](https://www.archlinux.org/packages/?name=kmod). See [Module Blacklisting](/index.php/Kernel_modules#Blacklisting "Kernel modules") for details.

### وصل نظام الملفات

The default setup will automatically fsck and mount filesystems before starting services that need them to be mounted. For example, systemd automatically makes sure that remote filesystem mounts like [NFS](/index.php/NFS "NFS") or [Samba](/index.php/Samba "Samba") are only started after the network has been set up. Therefore, local and remote filesystem mounts specified in `/etc/fstab` should work out of the box.

See [systemd.mount(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.mount.5) for details.

#### الوصل التلقائي

*   If you have a large `/home` partition, it might be better to allow services that do not depend on `/home` to start while `/home` is checked by fsck. This can be achieved by adding the following options to the `/etc/fstab` entry of your `/home` partition:

```
noauto,x-systemd.automount

```

This will fsck and mount `/home` when it is first accessed, and the kernel will buffer all file access to `/home` until it is ready.

Note: this will make your `/home` filesystem type `autofs`, which is ignored by [mlocate](/index.php/Mlocate "Mlocate") by default. The speedup of automounting `/home` may not be more than a second or two, depending on your system, so this trick may not be worth it.

*   The same applies to remote filesystem mounts. If you want them to be mounted only upon access, you will need to use the `noauto,x-systemd.automount` parameters. In addition, you can use the `x-systemd.device-timeout=#` option to specify a timeout in case the network resource is not available.

*   If you have encrypted filesystems with keyfiles, you can also add the `noauto` parameter to the corresponding entries in `/etc/crypttab`. Systemd will then not open the encrypted device on boot, but instead wait until it is actually accessed and then automatically open it with the specified keyfile before mounting it. This might save a few seconds on boot if you are using an encrypted RAID device for example, because systemd doesn't have to wait for the device to become available. For example:

 `/etc/crypttab`  `data /dev/md0 /root/key noauto` 

#### إدارة الأقسام المنطقية ( LVM )

If you have [LVM](/index.php/LVM "LVM") volumes not activated via the [initramfs](/index.php/Mkinitcpio "Mkinitcpio"), enable the `lvm-monitoring` service, which is provided by the [lvm2](https://www.archlinux.org/packages/?name=lvm2) package:

```
# systemctl enable lvm-monitoring

```

### إدارة الطاقة ( من خلال البوابة المتقدمة ACPI )

Systemd handles some power-related [ACPI](https://en.wikipedia.org/wiki/Advanced_Configuration_and_Power_Interface "wikipedia:Advanced Configuration and Power Interface") events. They can be configured via the following options from `/etc/systemd/logind.conf`:

*   `HandlePowerKey`: specifies which action is invoked when the power key is pressed.
*   `HandleSuspendKey`: specifies which action is invoked when the suspend key is pressed.
*   `HandleHibernateKey`: specifies which action is invoked when the hibernate key is pressed.
*   `HandleLidSwitch`: specifies which action is invoked when the lid is closed.

The specified action can be one of `ignore`, `poweroff`, `reboot`, `halt`, `suspend`, `hibernate`, `hybrid-sleep`, `lock` or `kexec`.

If these options are not configured, systemd will use its defaults: `HandlePowerKey=poweroff`, `HandleSuspendKey=suspend`, `HandleHibernateKey=hibernate`, and `HandleLidSwitch=suspend`.

On systems which run no graphical setup or only a simple window manager like [i3](/index.php/I3 "I3") or [awesome](/index.php/Awesome "Awesome"), this may replace the [acpid](/index.php/Acpid "Acpid") daemon which is usually used to react to these ACPI events.

**Note:** Run `systemctl restart systemd-logind` for your changes to take effect.

**Note:** Systemd cannot handle AC and Battery ACPI events, so if you use [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools") or other similar tools [acpid](/index.php/Acpid "Acpid") is still required.

In the current version of systemd, the `Handle*` options will apply throughout the system unless they are "inhibited" (temporarily turned off) by a program, such as a power manager inside a desktop environment. If these inhibits are not taken, you can end up with a situation where systemd suspends your system, then when it wakes up the other power manager suspends it again.

**Warning:** Currently, the power managers in the newest versions of [KDE](/index.php/KDE "KDE") and [GNOME](/index.php/GNOME "GNOME") are the only ones that issue the necessary "inhibited" commands. Until the others do, you will need to set the `Handle` options to `ignore` if you want your ACPI events to be handled by [Xfce](/index.php/Xfce "Xfce"), [acpid](/index.php/Acpid "Acpid") or other programs.

**Note:** Systemd can also use other suspend backends (such as [Uswsusp](/index.php/Uswsusp "Uswsusp") or [TuxOnIce](/index.php/TuxOnIce "TuxOnIce")), in addition to the default *kernel* backend, in order to put the computer to sleep or hibernate.

For `systemctl hibernate` to work on your system you need to follow instructions at [Hibernation](/index.php/Pm-utils#Hibernation_.28suspend2disk.29 "Pm-utils") and possibly at [Mkinitcpio Resume Hook](/index.php/Pm-utils#Mkinitcpio_Resume_Hook "Pm-utils") (`pm-utils` does not need to be installed).

#### المُعَلِّقات

Systemd does not use [pm-utils](/index.php/Pm-utils "Pm-utils") to put the machine to sleep when using `systemctl suspend`, `systemctl hibernate` or `systemctl hybrid-sleep`; [pm-utils](/index.php/Pm-utils "Pm-utils") hooks, including any [custom hooks](/index.php/Pm-utils#Creating_your_own_hooks "Pm-utils"), will not be run. However, systemd provides two similar mechanisms to run custom scripts on these events.

##### ملفات خدمات التّعليق و الاستكمال

Service files can be hooked into suspend.target, hibernate.target and sleep.target to execute actions before or after suspend/hibernate. Separate files should be created for user actions and root/system actions. To activate the user service files, `# systemctl enable suspend@<user> && systemctl enable resume@<user>`. Examples:

 `/etc/systemd/system/suspend@.service` 
```
[Unit]
Description=User suspend actions
Before=sleep.target

[Service]
User=%I
Type=forking
Environment=DISPLAY=:0
ExecStartPre= -/usr/bin/pkill -u %u unison ; /usr/local/bin/music.sh stop ; /usr/bin/mysql -e 'slave stop'
ExecStart=/usr/bin/sflock

[Install]
WantedBy=sleep.target
```
 `/etc/systemd/system/resume@.service` 
```
[Unit]
Description=User resume actions
After=suspend.target

[Service]
User=%I
Type=simple
ExecStartPre=/usr/local/bin/ssh-connect.sh
ExecStart=/usr/bin/mysql -e 'slave start'

[Install]
WantedBy=suspend.target
```

For root/system actions (activate with `# systemctl enable root-suspend`):

 `/etc/systemd/system/root-resume.service` 
```
[Unit]
Description=Local system resume actions
After=suspend.target

[Service]
Type=simple
ExecStart=/usr/bin/systemctl restart mnt-media.automount

[Install]
WantedBy=suspend.target
```
 `/etc/systemd/system/root-suspend.service` 
```
[Unit]
Description=Local system suspend actions
Before=sleep.target

[Service]
Type=simple
ExecStart=-/usr/bin/pkill sshfs

[Install]
WantedBy=sleep.target
```

A couple of handy hints about these service files (more in [systemd.service(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.service.5)):

*   If `Type=OneShot` then you can use multiple `ExecStart=` lines. Otherwise only one ExecStart line is allowed. You can add more commands with either `ExecStartPre` or by separating commands with a semicolon (see the first example above -- note the spaces before and after the semicolon...these are required!).
*   A command prefixed with '-' will cause a non-zero exit status to be ignored and treated as a successful command.
*   The best place to find errors when troubleshooting these service files is of course with `journalctl`.

##### الملف المُجَمَّع لخدمات التعليق و الاستكمال

With the combined suspend/resume service file, a single hook does all the work for different phases (sleep/resume) and for different targets (suspend/hibernate/hybrid-sleep).

Example and explanation:

 `/etc/systemd/system/wicd-sleep.service` 
```
[Unit]
Description=Wicd sleep hook
Before=sleep.target
StopWhenUnneeded=yes

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=-/usr/share/wicd/daemon/suspend.py
ExecStop=-/usr/share/wicd/daemon/autoconnect.py

[Install]
WantedBy=sleep.target
```

*   `RemainAfterExit=yes`: After started, the service is considered active until it is explicitly stopped.
*   `StopWhenUnneeded=yes`: When active, the service will be stopped if no other active service requires it. In this specific example, it will be stopped after sleep.target is stopped.
*   Because sleep.target is pulled in by suspend.target, hibernate.target and hybrid-sleep.target and sleep.target itself is a StopWhenUnneeded service, the hook is guaranteed to start/stop properly for different tasks.

##### المُعَلِّقات في /usr/lib/systemd/system-sleep

Systemd runs all executables in `/usr/lib/systemd/system-sleep/`, passing two arguments to each of them:

*   Argument 1: either `pre` or `post`, depending on whether the machine is going to sleep or waking up
*   Argument 2: `suspend`, `hibernate` or `hybrid-sleep`, depending on which is being invoked

In contrast to [pm-utils](/index.php/Pm-utils "Pm-utils"), systemd will run these scripts concurrently and not one after another.

The output of any custom script will be logged by `systemd-suspend.service`, `systemd-hibernate.service` or `systemd-hybrid-sleep.service`. You can see its output in systemd's [journal](/index.php/Systemd#Journal "Systemd"):

```
# journalctl -b -u systemd-suspend

```

Note that you can also use `sleep.target`, `suspend.target`, `hibernate.target` or `hybrid-sleep.target` to hook units into the sleep state logic instead of using custom scripts.

An example of a custom sleep script:

 `/usr/lib/systemd/system-sleep/example.sh` 
```
#!/bin/sh
case $1/$2 in
  pre/*)
    echo "Going to $2..."
    ;;
  post/*)
    echo "Waking up from $2..."
    ;;
esac
```

Don't forget to make your script executable:

```
# chmod a+x /usr/lib/systemd/system-sleep/example.sh

```

See [systemd.special(7)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.special.7) and [systemd-sleep(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-sleep.8) for more details.

### الملفات المؤقّتة

Systemd-tmpfiles uses configuration files in `/usr/lib/tmpfiles.d/` and `/etc/tmpfiles.d/` to describe the creation, cleaning and removal of volatile and temporary files and directories which usually reside in directories such as `/run` or `/tmp`. Each configuration file is named in the style of `/etc/tmpfiles.d/<program>.conf`. This will also override any files in `/usr/lib/tmpfiles.d/` with the same name.

tmpfiles are usually provided together with service files to create directories which are expected to exist by certain daemons. For example the [Samba](/index.php/Samba "Samba") daemon expects the directory `/run/samba` to exist and to have the correct permissions. The corresponding tmpfile looks like this:

 `/usr/lib/tmpfiles.d/samba.conf`  `D /run/samba 0755 root root` 

tmpfiles may also be used to write values into certain files on boot. For example, if you use `/etc/rc.local` to disable wakeup from USB devices with `echo USBE > /proc/acpi/wakeup`, you may use the following tmpfile instead:

 `/etc/tmpfiles.d/disable-usb-wake.conf`  `w /proc/acpi/wakeup - - - - USBE` 

See [tmpfiles.d(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/tmpfiles.d.5) for details.

**Note:** This method may not work to set options in `/sys` since the `systemd-tmpfiles-setup` service may run before the appropriate device modules is loaded. In this case you could check whether the module has a parameter for the option you want to set with `modinfo <module>` and set this option with a [config file in `/etc/modprobe.d`](/index.php/Modprobe.d#Configuration "Modprobe.d"). Otherwise you will have to write a [udev rule](/index.php/Udev#About_udev_rules "Udev") to set the appropriate attribute as soon as the device appears.

### الوحدات

A unit configuration file encodes information about a service, a socket, a device, a mount point, an automount point, a swap file or partition, a start-up target, a file system path or a timer controlled and supervised by systemd. The syntax is inspired by XDG Desktop Entry Specification .desktop files, which are in turn inspired by Microsoft Windows .ini files.

See [systemd.unit(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.unit.5) for details.

## الاستخدام الأوّلي لأداة systemctl

تمثّل الأداة `systemctl` الأمر الرّئيسي للتّبحّر و التّحكم بـ systemd . بعض من استخداماته فحص حالة النظام وإدارته بالإضافة لإدارة الخدمات. انظر [systemctl(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1) لمزيد من التّفاصيل.

**Tip:** يمكنك استخدام جميع أوامر `systemctl` التّالية بصورة متغيّرة لكل `-H <user>@<host>` وذلك للتّحكم بنموذج systemd في الجهاز البعيد. لاتّباع هذه الطريقة نستخدم الأداة [SSH](/index.php/SSH "SSH") وذلك للاتصال بنموذج systemd البعيد.

**Note:** الواجهة الرسوميّة الرّسمية للأداة `systemctl` تتمثل بالأداة `systemadm`. تُؤمّن هذه الأداة الحزمةُ[systemd-ui-git](https://aur.archlinux.org/packages/systemd-ui-git/) المتوفّرة ضمن مستودع [AUR](/index.php/AUR "AUR").

### تحليل حالة النظام

List running units:

```
$ systemctl

```

or:

```
$ systemctl list-units

```

List failed units:

```
$ systemctl --failed

```

The available unit files can be seen in `/usr/lib/systemd/system/` and `/etc/systemd/system/` (the latter takes precedence). You can see list installed unit files by:

```
$ systemctl list-unit-files

```

### استخدام الوحدات

Units can be, for example, services (`.service`), mount points (`.mount`), devices (`.device`) or sockets (`.socket`).

When using `systemctl`, you generally have to specify the complete name of the unit file, including its suffix, for example `sshd.socket`. There are however a few shortforms when specifying the unit in the following `systemctl` commands:

*   If you don't specify the suffix, systemctl will assume `.service`. For example, `netcfg` and `netcfg.service` are treated equivalent.
*   Mount points will automatically be translated into the appropriate `.mount` unit. For example, specifying `/home` is equivalent to `home.mount`.
*   Similiar to mount points, devices are automatically translated into the appropriate `.device` unit, therefore specifying `/dev/sda2` is equivalent to `dev-sda2.device`.

See [systemd.unit(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.unit.5) for details.

Activate a unit immediately:

```
# systemctl start <unit>

```

Deactivate a unit immediately:

```
# systemctl stop <unit>

```

Restart a unit:

```
# systemctl restart <unit>

```

Ask a unit to reload its configuration:

```
# systemctl reload <unit>

```

Show the status of a unit, including whether it is running or not:

```
$ systemctl status <unit>

```

Check whether a unit is already enabled or not:

```
$ systemctl is-enabled <unit>

```

Enable a unit to be started on bootup:

```
# systemctl enable <unit>

```

**Note:** Services without an `[Install]` section are usually called automatically by other services. If you need to install them manually, use the following command, replacing `foo` with the name of the service.
```
# ln -s /usr/lib/systemd/system/*foo*.service /etc/systemd/system/graphical.target.wants/

```

Disable a unit to not start during bootup:

```
# systemctl disable <unit>

```

Show the manual page associated with a unit (this has to be supported by the unit file):

```
$ systemctl help <unit>

```

Reload systemd, scanning for new or changed units:

```
# systemctl daemon-reload

```

### إدارة الطّاقة

`polkit` is necessary for power management. If you are in a local `systemd-logind` user session and no other session is active, the following commands will work without root privileges. If not (for example, because another user is logged into a tty), systemd will automatically ask you for the root password.

Shut down and reboot the system:

```
$ systemctl reboot

```

Shut down and power-off the system:

```
$ systemctl poweroff

```

Suspend the system:

```
$ systemctl suspend

```

Put the system into hibernation:

```
$ systemctl hibernate

```

Put the system into hybrid-sleep state (or suspend-to-both):

```
$ systemctl hybrid-sleep

```

## تشغيل المُخدّمات الرسومية في systemd

To enable graphical login, run your preferred [Display manager](/index.php/Display_manager "Display manager") daemon (e.g. [KDM](/index.php/KDM "KDM")). At the moment, service files exist for [GDM](/index.php/GDM "GDM"), [KDM](/index.php/KDM "KDM"), [SLiM](/index.php/SLiM "SLiM"), [XDM](/index.php/XDM "XDM"), [LXDM](/index.php/LXDM "LXDM") and [LightDM](/index.php/LightDM "LightDM").

```
# systemctl enable kdm

```

This should work out of the box. If not, you might have a `default.target` set manually or from a older install:

 `# ls -l /etc/systemd/system/default.target`  `/etc/systemd/system/default.target -> /usr/lib/systemd/system/graphical.target` 

Simply delete the symlink and systemd will use its stock `default.target` (i.e. `graphical.target`).

```
# rm /etc/systemd/system/default.target

```

### استخدام مدير الولوج systemd-logind

In order to check the status of your user session, you can use `loginctl`. All [PolicyKit](/index.php/PolicyKit "PolicyKit") actions like suspending the system or mounting external drives will work out of the box.

```
$ loginctl show-session $XDG_SESSION_ID

```

## كتابة ملفات تخصصية بتنسيق .service

*انظر*

### استنباط الاعتماديّات

With systemd, dependencies can be resolved by designing the unit files correctly. The most typical case is that the unit `A` requires the unit `B` to be running before `A` is started. In that case add `Requires=B` and `After=B` to the `[Unit]` section of `A`. If the dependency is optional, add `Wants=B` and `After=B` instead. Note that `Wants=` and `Requires=` do not imply `After=`, meaning that if `After=` is not specified, the two units will be started in parallel.

Dependencies are typically placed on services and not on targets. For example, `network.target` is pulled in by whatever service configures your network interfaces, therefore ordering your custom unit after it is sufficient since `network.target` is started anyway.

### النوع

There are several different start-up types to consider when writing a custom service file. This is set with the `Type=` parameter in the `[Service]` section. See [systemd.service(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.service.5) for a more detailed explanation.

*   `Type=simple` (default): systemd considers the service to be started up immediately. The process must not fork. Do not use this type if other services need to be ordered on this service, unless it is socket activated.
*   `Type=forking`: systemd considers the service started up once the process forks and the parent has exited. For classic daemons use this type unless you know that it is not necessary. You should specify `PIDFile=` as well so systemd can keep track of the main process.
*   `Type=oneshot`: This is useful for scripts that do a single job and then exit. You may want to set `RemainAfterExit=yes` as well so that systemd still considers the service as active after the process has exited.
*   `Type=notify`: Identical to `Type=simple`, but with the stipulation that the daemon will send a signal to systemd when it is ready. The reference implementation for this notification is provided by `libsystemd-daemon.so`.
*   `Type=dbus`: The service is considered ready when the specified `BusName` appears on DBus's system bus.

### تحرير ملفات الوحدات المضافة

To edit a unit file provided by a package, you can create a directory called `/etc/systemd/system/<unit>.d/` for example `/etc/systemd/system/httpd.service.d/` and place `*.conf` files in there to override or add new options. Systemd will parse these `*.conf` files and apply them on top of the original unit. For example, if you simply want to add an additional dependency to a unit, you may create the following file:

 `/etc/systemd/system/<unit>.d/customdependency.conf` 
```
[Unit]
Requires=<new dependency>
After=<new dependency>
```

Then run the following for your changes to take effect:

```
# systemctl daemon-reload
# systemctl restart <unit>

```

Alternatively you can copy the old unit file from `/usr/lib/systemd/system/` to `/etc/systemd/system/` and make your changes there. A unit file in `/etc/systemd/system/` always overrides the same unit in `/usr/lib/systemd/system/`. Note that when the original unit in `/usr/lib/` is changed due to a package upgrade, these changes will not automatically apply to your custom unit file in `/etc/`. Additionally you will have to manually reenable the unit with `systemctl reenable <unit>`. It is therefore recommended to use the `*.conf` method described before instead.

**Tip:** You can use `systemd-delta` to see which unit files have been overridden and what exactly has been changed.
As the provided unit files will be updated from time to time, use systemd-delta for system maintenance.

### تسليط الضوء على بناء الوحدات بواسطة Vim

Syntax highlighting for systemd unit files within [Vim](/index.php/Vim "Vim") can be enabled by installing [vim-systemd](https://www.archlinux.org/packages/?name=vim-systemd) from the [official repositories](/index.php/Official_repositories "Official repositories").

## الأهداف

Systemd uses *targets* which serve a similar purpose as runlevels but act a little different. Each *target* is named instead of numbered and is intended to serve a specific purpose with the possibility of having multiple ones active at the same time. Some *targets* are implemented by inheriting all of the services of another *target* and adding additional services to it. There are systemd *target*s that mimic the common SystemVinit runlevels so you can still switch *target*s using the familiar `telinit RUNLEVEL` command.

### الأهداف الحالية

The following should be used under systemd instead of `runlevel`:

```
$ systemctl list-units --type=target

```

### إنشاء هدف معيّن

The runlevels that are assigned a specific purpose on vanilla Fedora installs; 0, 1, 3, 5, and 6; have a 1:1 mapping with a specific systemd *target*. Unfortunately, there is no good way to do the same for the user-defined runlevels like 2 and 4\. If you make use of those it is suggested that you make a new named systemd *target* as `/etc/systemd/system/<your target>` that takes one of the existing runlevels as a base (you can look at `/usr/lib/systemd/system/graphical.target` as an example), make a directory `/etc/systemd/system/<your target>.wants`, and then symlink the additional services from `/usr/lib/systemd/system/` that you wish to enable.

### جدولة الاهداف

| SysV Runlevel | systemd Target | Notes |
| 0 | runlevel0.target, poweroff.target | Halt the system. |
| 1, s, single | runlevel1.target, rescue.target | Single user mode. |
| 2, 4 | runlevel2.target, runlevel4.target, multi-user.target | User-defined/Site-specific runlevels. By default, identical to 3. |
| 3 | runlevel3.target, multi-user.target | Multi-user, non-graphical. Users can usually login via multiple consoles or via the network. |
| 5 | runlevel5.target, graphical.target | Multi-user, graphical. Usually has all the services of runlevel 3 plus a graphical login. |
| 6 | runlevel6.target, reboot.target | Reboot |
| emergency | emergency.target | Emergency shell |

### تغيير الهدف الحالي

In systemd targets are exposed via "target units". You can change them like this:

```
# systemctl isolate graphical.target

```

This will only change the current target, and has no effect on the next boot. This is equivalent to commands such as `telinit 3` or `telinit 5` in Sysvinit.

### تغيير الهدف الافتراضي للإقلاع من خلاله

The standard target is `default.target`, which is aliased by default to `graphical.target` (which roughly corresponds to the old runlevel 5). To change the default target at boot-time, append one of the following [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") to your bootloader:

**Tip:** The `.target` extension can be left out.

*   `systemd.unit=multi-user.target` (which roughly corresponds to the old runlevel 3),
*   `systemd.unit=rescue.target` (which roughly corresponds to the old runlevel 1).

Alternatively, you may leave the bootloader alone and change `default.target`. This can be done using `systemctl`:

```
# systemctl enable multi-user.target

```

The effect of this command is outputted by `systemctl`; a symlink to the new default target is made at `/etc/systemd/system/default.target`. This works if, and only if:

```
[Install]
Alias=default.target

```

is in the target's configuration file. Currently, `multi-user.target` and `graphical.target` both have it.

## الدّوريّات

Since version 38, systemd has its own logging system, the journal. Therefore, running a syslog daemon is no longer required. To read the log, use:

```
# journalctl

```

By default (when `Storage=` is set to `auto` in `/etc/systemd/journald.conf`), the journal writes to `/var/log/journal/`. The directory `/var/log/journal/` is part of core/systemd. If you or some program delete it, systemd will **not** recreate it automatically, however it will be recreated during the next update of systemd. Till then, logs will be written to `/run/systemd/journal`. This means that logs will be lost on reboot.

### تنقيح المُخرجات

`journalctl` allows you to filter the output by specific fields.

Examples:

Show all messages from this boot:

```
# journalctl -b

```

However, often one is interested in messages not from the current, but from the previous boot (e.g. if an unrecoverable system crash happened). Currently, this feature is not implemented, though there was a discussion at [systemd-devel@lists.freedesktop.org](http://comments.gmane.org/gmane.comp.sysutils.systemd.devel/6608) (September/October 2012).

As a workaround you can use at the moment:

```
# journalctl --since=today | tac | sed -n '/-- Reboot --/{n;:r;/-- Reboot --/q;p;n;b r}' | tac

```

provided, that the previous boot happened today. Be aware that, if there are many messages for the current day, the output of this command can be delayed for quite some time.

Follow new messages:

```
# journalctl -f

```

Show all messages by a specific executable:

```
# journalctl /usr/lib/systemd/systemd

```

Show all messages by a specific process:

```
# journalctl _PID=1

```

Show all messages by a specific unit:

```
# journalctl -u netcfg

```

See [journalctl(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/journalctl.1), `systemd.journal-fields` or Lennert's [blog post](http://0pointer.de/blog/projects/journalctl.html) for details.

### الحجم الأقصى للدّورية

If the journal is persistent (non-volatile), its size limit is set to a default value of 10% of the size of the respective file system. For example, with `/var/log/journal` located on a 50 GiB root partition this would lead to 5 GiB of journal data. The maximum size of the persistent journal can be controlled by `SystemMaxUse` in `/etc/systemd/journald.conf`, so to limit it for example to 50 MiB uncomment and edit the corresponding line to:

```
SystemMaxUse=50M

```

Refer to [journald.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/journald.conf.5) for more info.

### الترابط بين مدير الدّوريات journald و سجل النظام syslog

Compatibility with classic syslog implementations is provided via a socket `/run/systemd/journal/syslog`, to which all messages are forwarded. To make the syslog daemon work with the journal, it has to bind to this socket instead of `/dev/log` ([official announcement](http://lwn.net/Articles/474968/)). The [syslog-ng](https://www.archlinux.org/packages/?name=syslog-ng) package in the repositories automatically provides the necessary configuration.

```
# systemctl enable syslog-ng

```

A good `journalctl` tutorial is [here](http://0pointer.de/blog/projects/journalctl.html).

## التّحسين

See [Improve boot performance](/index.php/Improve_boot_performance "Improve boot performance").

### تحليل عملية الإقلاع

#### استخدام أداة التحليل systemd-analyze

Systemd provides a tool called `systemd-analyze` that allows you to analyze your boot process so you can see which unit files are causing your boot process to slow down. You can then optimize your system accordingly.

To see how much time was spent in kernelspace and userspace on boot, simply use:

```
$ systemd-analyze

```

**Tip:**

*   If you append the `timestamp` hook to your `HOOKS` array in `/etc/[mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio").conf` and rebuild your initramfs with `mkinitcpio -p linux`, systemd-analyze is also able to show you how much time was spent in the initramfs.
*   If you boot via [UEFI](/index.php/UEFI "UEFI") and use a boot loader which implements systemds' [Boot Loader Interface](http://www.freedesktop.org/wiki/Software/systemd/BootLoaderInterface) (which currently only [Gummiboot](/index.php/Gummiboot "Gummiboot") does), systemd-analyze can additionally show you how much time was spent in the EFI firmware and the boot loader itself.

To list the started unit files, sorted by the time each of them took to start up:

```
$ systemd-analyze blame

```

You can also create a SVG file which describes your boot process graphically, similiar to [Bootchart](/index.php/Bootchart "Bootchart"):

```
$ systemd-analyze plot > plot.svg

```

#### استخدام راسم خريطة الإقلاع systemd-bootchart

Bootchart has been merged into systemd since Oct. 17, and you can use it to boot just as you would with the original bootchart. Add this to your kernel line:

```
initcall_debug printk.time=y init=/usr/lib/systemd/systemd-bootchart

```

#### المرحلة الثانية من رسم خريطة الإقلاع

You could also use a version of bootchart to visualize the boot sequence. Since you are not able to put a second init into the kernel command line you won't be able to use any of the standard bootchart setups. However the [bootchart2-git](https://aur.archlinux.org/packages/bootchart2-git/) package from [AUR](/index.php/AUR "AUR") comes with an undocumented systemd service. After you've installed bootchart2 do:

```
# systemctl enable bootchart

```

Read the [bootchart documentation](https://github.com/mmeeks/bootchart) for further details on using this version of bootchart.

## استكشاف الاخطاء و إصلاحها

### الوقت الطّويل لإيقاف أو إعادة التّشغيل

If the shutdown process takes a very long time (or seems to freeze) most likely a service not exiting is to blame. Systemd waits some time for each service to exit before trying to kill it. To find out if you are affected, see [this article](http://freedesktop.org/wiki/Software/systemd/Debugging#Shutdown_Completes_Eventually).

### عدم وجود مُخرجات للتطبيقات قصيرة العُمر

If `journalctl -u foounit` doesn't show any output for a short lived service, look at the PID instead. For example, if `systemd-modules-load.service` fails, and `systemctl status systemd-modules-load` shows that it ran as PID 123, then you might be able to see output in the journal for that PID, i.e. `journalctl -b _PID=123`. Metadata fields for the journal such as _SYSTEMD_UNIT and _COMM are collected asynchronously and rely on the `/proc` directory for the process existing. Fixing this requires fixing the kernel to provide this data via a socket connection, similar to SCM_CREDENTIALS.

### تشخيص مشاكل الإقلاع

أضف هذه المُعامِلات لسطر النّواة أثناء الإقلاع :

`systemd.log_level=debug systemd.log_target=kmsg log_buf_len=1M`

[معلومات أكثر عن الإصلاح](http://freedesktop.org/wiki/Software/systemd/Debugging)

### تعطيل التطبيقات مسببة الانهيار

فقط قم بإنشاء اختصار في العادم /dev/null للملف coredump.conf ، ثم طبق أداة التحكم بالنظام sysctl ([المصدر](https://bbs.archlinux.org/viewtopic.php?id=154511)) :

```
ln -s /dev/null /etc/sysctl.d/coredump.conf
/lib/systemd/systemd-sysctl
ulimit -c unlimited

```

## انظر أيضًا

*   [الموقع الرّسمي](http://www.freedesktop.org/wiki/Software/systemd)
*   [دليل الاستخدام](http://0pointer.de/public/systemd-man/)
*   [تحسين systemd](http://freedesktop.org/wiki/Software/systemd/Optimizations)
*   [الأسئلة الشّائِعة](http://www.freedesktop.org/wiki/Software/systemd/FrequentlyAskedQuestions)
*   [تلميحات و خُدَع](http://www.freedesktop.org/wiki/Software/systemd/TipsAndTricks)
*   [systemd للمُدراء (PDF)](http://0pointer.de/public/systemd-ebook-psankar.pdf)
*   [مشروع فيدورا و systemd](http://fedoraproject.org/wiki/Systemd)
*   [كيف تُصلح مشاكل systemd](http://fedoraproject.org/wiki/How_to_debug_Systemd_problems)
*   [جزء 2](http://www.h-online.com/open/features/Control-Centre-The-systemd-Linux-init-system-1565543.html) [جزء 1](http://www.h-online.com/open/features/Booting-up-Tools-and-tips-for-systemd-1570630.html) المقالات التمهيدية في مجلة *The H Open*.
*   [Lennart's blog story](http://0pointer.de/blog/projects/systemd.html)
*   [حالة التحديث](http://0pointer.de/blog/projects/systemd-update.html)
*   [حالة التحديث 2](http://0pointer.de/blog/projects/systemd-update-2.html)
*   [حالة التحديث 3](http://0pointer.de/blog/projects/systemd-update-3.html)
*   [الخُلاصة الحديثة](http://0pointer.de/blog/projects/why.html)
*   [ورقة عمل تحوُّل فيدورا من SysVinint إلى Systemd](http://fedoraproject.org/wiki/SysVinit_to_Systemd_Cheatsheet)