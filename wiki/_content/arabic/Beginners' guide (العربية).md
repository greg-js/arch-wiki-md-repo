****تلميح** :** هذا المستند يوجد أيضا في شكل مقال متعدد الصفحات بدلا من صفحة واحدة ممتدة، فإن كنت ترغب في قراءته بهذه الطريقة [اضغط هنا](/index.php/Beginners%27_Guide/Preparation_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9) "Beginners' Guide/Preparation (العربية)")

هذا المستند سيرشدك خلال عملية تثبيت [Arch Linux](/index.php/Arch_Linux "Arch Linux") باستخدام [Arch Install Scripts](https://github.com/falconindy/arch-install-scripts). وقبل البدء في التثبيت، ننصحك بعمل جولة عبر [FAQ](/index.php/FAQ "FAQ") .

الصفحة الرئيسية للمجتمع على [ArchWiki](/index.php/Main_page "Main page") هو المورد الأساسي الذي ينبغي استشارته إذا نشأت أي مشاكل.

قناة المجتمع [IRC](https://en.wikipedia.org/wiki/IRC "wikipedia:IRC") ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)) وأيضا المنتديات [forums](https://bbs.archlinux.org/) تعتبر مصدرا ممتازا إن لم تجد إجابة عن اﻷسئلة في مكان آخر. وفقا ل [Arch Way](/index.php/The_Arch_Way "The Arch Way") ، مطلوب منك أن تكتب `man _command_` لقراءة صفحة الإراشادات ﻷي أمر `man` لست معتادا عليه .

## Contents

*   [1 التجهيز](#.D8.A7.D9.84.D8.AA.D8.AC.D9.87.D9.8A.D8.B2)
    *   [1.1 حرق أحدث صورة لإسطوانة التثبيت](#.D8.AD.D8.B1.D9.82_.D8.A3.D8.AD.D8.AF.D8.AB_.D8.B5.D9.88.D8.B1.D8.A9_.D9.84.D8.A5.D8.B3.D8.B7.D9.88.D8.A7.D9.86.D8.A9_.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA)
        *   [1.1.1 التثبيت عبر الشبكة](#.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_.D8.B9.D8.A8.D8.B1_.D8.A7.D9.84.D8.B4.D8.A8.D9.83.D8.A9)
        *   [1.1.2 التثبيت على اﻵلة الافتراضية](#.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_.D8.B9.D9.84.D9.89_.D8.A7.EF.BB.B5.D9.84.D8.A9_.D8.A7.D9.84.D8.A7.D9.81.D8.AA.D8.B1.D8.A7.D8.B6.D9.8A.D8.A9)
    *   [1.2 الإقلاع من قرص التثبيت](#.D8.A7.D9.84.D8.A5.D9.82.D9.84.D8.A7.D8.B9_.D9.85.D9.86_.D9.82.D8.B1.D8.B5_.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA)
        *   [1.2.1 اختبار الإقلاع عبر نمط UEFI](#.D8.A7.D8.AE.D8.AA.D8.A8.D8.A7.D8.B1_.D8.A7.D9.84.D8.A5.D9.82.D9.84.D8.A7.D8.B9_.D8.B9.D8.A8.D8.B1_.D9.86.D9.85.D8.B7_UEFI)
        *   [1.2.2 إصلاح مشكلات الإقلاع](#.D8.A5.D8.B5.D9.84.D8.A7.D8.AD_.D9.85.D8.B4.D9.83.D9.84.D8.A7.D8.AA_.D8.A7.D9.84.D8.A5.D9.82.D9.84.D8.A7.D8.B9)
*   [2 تثبيت النظام](#.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_.D8.A7.D9.84.D9.86.D8.B8.D8.A7.D9.85)
    *   [2.1 تغيير اللغة](#.D8.AA.D8.BA.D9.8A.D9.8A.D8.B1_.D8.A7.D9.84.D9.84.D8.BA.D8.A9)
    *   [2.2 إعدادات الاتصال بالإنترنت](#.D8.A5.D8.B9.D8.AF.D8.A7.D8.AF.D8.A7.D8.AA_.D8.A7.D9.84.D8.A7.D8.AA.D8.B5.D8.A7.D9.84_.D8.A8.D8.A7.D9.84.D8.A5.D9.86.D8.AA.D8.B1.D9.86.D8.AA)
        *   [2.2.1 Wired الاتصال السلكي](#Wired_.D8.A7.D9.84.D8.A7.D8.AA.D8.B5.D8.A7.D9.84_.D8.A7.D9.84.D8.B3.D9.84.D9.83.D9.8A)
        *   [2.2.2 Wireless الاتصال اللاسلكي](#Wireless_.D8.A7.D9.84.D8.A7.D8.AA.D8.B5.D8.A7.D9.84_.D8.A7.D9.84.D9.84.D8.A7.D8.B3.D9.84.D9.83.D9.8A)
        *   [2.2.3 المودم الثنائي و ISDN أوPPoE DSL](#.D8.A7.D9.84.D9.85.D9.88.D8.AF.D9.85_.D8.A7.D9.84.D8.AB.D9.86.D8.A7.D8.A6.D9.8A_.D9.88_ISDN_.D8.A3.D9.88PPoE_DSL)
        *   [2.2.4 العمل عبر سيرفر بروكسي](#.D8.A7.D9.84.D8.B9.D9.85.D9.84_.D8.B9.D8.A8.D8.B1_.D8.B3.D9.8A.D8.B1.D9.81.D8.B1_.D8.A8.D8.B1.D9.88.D9.83.D8.B3.D9.8A)
    *   [2.3 إعدادات القرص الصلب](#.D8.A5.D8.B9.D8.AF.D8.A7.D8.AF.D8.A7.D8.AA_.D8.A7.D9.84.D9.82.D8.B1.D8.B5_.D8.A7.D9.84.D8.B5.D9.84.D8.A8)
        *   [2.3.1 مثال](#.D9.85.D8.AB.D8.A7.D9.84)
    *   [2.4 ربط أقسام القرص الصلب](#.D8.B1.D8.A8.D8.B7_.D8.A3.D9.82.D8.B3.D8.A7.D9.85_.D8.A7.D9.84.D9.82.D8.B1.D8.B5_.D8.A7.D9.84.D8.B5.D9.84.D8.A8)
    *   [2.5 mirror اختيار خادم بديل](#mirror_.D8.A7.D8.AE.D8.AA.D9.8A.D8.A7.D8.B1_.D8.AE.D8.A7.D8.AF.D9.85_.D8.A8.D8.AF.D9.8A.D9.84)
    *   [2.6 تثبيت النظام الأساسي](#.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_.D8.A7.D9.84.D9.86.D8.B8.D8.A7.D9.85_.D8.A7.D9.84.D8.A3.D8.B3.D8.A7.D8.B3.D9.8A)
    *   [2.7 توليد ملف fstab](#.D8.AA.D9.88.D9.84.D9.8A.D8.AF_.D9.85.D9.84.D9.81_fstab)
    *   [2.8 تغيير الجذر chroot وإعداد النظام اﻷساسي](#.D8.AA.D8.BA.D9.8A.D9.8A.D8.B1_.D8.A7.D9.84.D8.AC.D8.B0.D8.B1_chroot_.D9.88.D8.A5.D8.B9.D8.AF.D8.A7.D8.AF_.D8.A7.D9.84.D9.86.D8.B8.D8.A7.D9.85_.D8.A7.EF.BB.B7.D8.B3.D8.A7.D8.B3.D9.8A)
        *   [2.8.1 Locale ضبط الإعدادات المحلية](#Locale_.D8.B6.D8.A8.D8.B7_.D8.A7.D9.84.D8.A5.D8.B9.D8.AF.D8.A7.D8.AF.D8.A7.D8.AA_.D8.A7.D9.84.D9.85.D8.AD.D9.84.D9.8A.D8.A9)
        *   [2.8.2 خط الكونسول ومخطط لوحة المفاتيح](#.D8.AE.D8.B7_.D8.A7.D9.84.D9.83.D9.88.D9.86.D8.B3.D9.88.D9.84_.D9.88.D9.85.D8.AE.D8.B7.D8.B7_.D9.84.D9.88.D8.AD.D8.A9_.D8.A7.D9.84.D9.85.D9.81.D8.A7.D8.AA.D9.8A.D8.AD)
        *   [2.8.3 ضبط منطقة التوقيت Time zone](#.D8.B6.D8.A8.D8.B7_.D9.85.D9.86.D8.B7.D9.82.D8.A9_.D8.A7.D9.84.D8.AA.D9.88.D9.82.D9.8A.D8.AA_Time_zone)
        *   [2.8.4 ساعة العتاد Hardware clock](#.D8.B3.D8.A7.D8.B9.D8.A9_.D8.A7.D9.84.D8.B9.D8.AA.D8.A7.D8.AF_Hardware_clock)
        *   [2.8.5 وحدات النواة Kernel modules](#.D9.88.D8.AD.D8.AF.D8.A7.D8.AA_.D8.A7.D9.84.D9.86.D9.88.D8.A7.D8.A9_Kernel_modules)
        *   [2.8.6 اسم الجهاز المضيف Hostname](#.D8.A7.D8.B3.D9.85_.D8.A7.D9.84.D8.AC.D9.87.D8.A7.D8.B2_.D8.A7.D9.84.D9.85.D8.B6.D9.8A.D9.81_Hostname)
    *   [2.9 إعدادات الشبكة](#.D8.A5.D8.B9.D8.AF.D8.A7.D8.AF.D8.A7.D8.AA_.D8.A7.D9.84.D8.B4.D8.A8.D9.83.D8.A9)
        *   [2.9.1 الاتصال السلكي](#.D8.A7.D9.84.D8.A7.D8.AA.D8.B5.D8.A7.D9.84_.D8.A7.D9.84.D8.B3.D9.84.D9.83.D9.8A)
            *   [2.9.1.1 رقم IP متغير](#.D8.B1.D9.82.D9.85_IP_.D9.85.D8.AA.D8.BA.D9.8A.D8.B1)
            *   [2.9.1.2 رقم IP ثابت](#.D8.B1.D9.82.D9.85_IP_.D8.AB.D8.A7.D8.A8.D8.AA)
        *   [2.9.2 الاتصال اللاسلكي Wireless](#.D8.A7.D9.84.D8.A7.D8.AA.D8.B5.D8.A7.D9.84_.D8.A7.D9.84.D9.84.D8.A7.D8.B3.D9.84.D9.83.D9.8A_Wireless)
        *   [2.9.3 ISDN أو المودم الثنائي، PPoE DSLISDN](#ISDN_.D8.A3.D9.88_.D8.A7.D9.84.D9.85.D9.88.D8.AF.D9.85_.D8.A7.D9.84.D8.AB.D9.86.D8.A7.D8.A6.D9.8A.D8.8C_PPoE_DSLISDN)
    *   [2.10 إنشاء بيئة قرص الذاكرة الأولي initial ramdisk environment](#.D8.A5.D9.86.D8.B4.D8.A7.D8.A1_.D8.A8.D9.8A.D8.A6.D8.A9_.D9.82.D8.B1.D8.B5_.D8.A7.D9.84.D8.B0.D8.A7.D9.83.D8.B1.D8.A9_.D8.A7.D9.84.D8.A3.D9.88.D9.84.D9.8A_initial_ramdisk_environment)
    *   [2.11 تحديد كلمة مرور المستخدم الجذر](#.D8.AA.D8.AD.D8.AF.D9.8A.D8.AF_.D9.83.D9.84.D9.85.D8.A9_.D9.85.D8.B1.D9.88.D8.B1_.D8.A7.D9.84.D9.85.D8.B3.D8.AA.D8.AE.D8.AF.D9.85_.D8.A7.D9.84.D8.AC.D8.B0.D8.B1)
    *   [2.12 تثبيت وإعداد محمل الإقلاع](#.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_.D9.88.D8.A5.D8.B9.D8.AF.D8.A7.D8.AF_.D9.85.D8.AD.D9.85.D9.84_.D8.A7.D9.84.D8.A5.D9.82.D9.84.D8.A7.D8.B9)
        *   [2.12.1 خاص بلوحات أم بنظام BIOS](#.D8.AE.D8.A7.D8.B5_.D8.A8.D9.84.D9.88.D8.AD.D8.A7.D8.AA_.D8.A3.D9.85_.D8.A8.D9.86.D8.B8.D8.A7.D9.85_BIOS)
            *   [2.12.1.1 محمل الإقلاع Syslinux](#.D9.85.D8.AD.D9.85.D9.84_.D8.A7.D9.84.D8.A5.D9.82.D9.84.D8.A7.D8.B9_Syslinux)
            *   [2.12.1.2 GRUB محمل الإقلاع](#GRUB_.D9.85.D8.AD.D9.85.D9.84_.D8.A7.D9.84.D8.A5.D9.82.D9.84.D8.A7.D8.B9)
        *   [2.12.2 خاص باللوحات اﻷم بنظام UEFI](#.D8.AE.D8.A7.D8.B5_.D8.A8.D8.A7.D9.84.D9.84.D9.88.D8.AD.D8.A7.D8.AA_.D8.A7.EF.BB.B7.D9.85_.D8.A8.D9.86.D8.B8.D8.A7.D9.85_UEFI)
            *   [2.12.2.1 EFISTUB](#EFISTUB)
            *   [2.12.2.2 محمل الإقلاع GRUB](#.D9.85.D8.AD.D9.85.D9.84_.D8.A7.D9.84.D8.A5.D9.82.D9.84.D8.A7.D8.B9_GRUB)
    *   [2.13 إلغاء ربط أقسام القرص الصلب وإعادة التشغيل](#.D8.A5.D9.84.D8.BA.D8.A7.D8.A1_.D8.B1.D8.A8.D8.B7_.D8.A3.D9.82.D8.B3.D8.A7.D9.85_.D8.A7.D9.84.D9.82.D8.B1.D8.B5_.D8.A7.D9.84.D8.B5.D9.84.D8.A8_.D9.88.D8.A5.D8.B9.D8.A7.D8.AF.D8.A9_.D8.A7.D9.84.D8.AA.D8.B4.D8.BA.D9.8A.D9.84)
*   [3 ما بعد التثبيت](#.D9.85.D8.A7_.D8.A8.D8.B9.D8.AF_.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA)
    *   [3.1 إدارة المستخدمين](#.D8.A5.D8.AF.D8.A7.D8.B1.D8.A9_.D8.A7.D9.84.D9.85.D8.B3.D8.AA.D8.AE.D8.AF.D9.85.D9.8A.D9.86)
    *   [3.2 مدير الحزم](#.D9.85.D8.AF.D9.8A.D8.B1_.D8.A7.D9.84.D8.AD.D8.B2.D9.85)
    *   [3.3 إدارة الخدمات](#.D8.A5.D8.AF.D8.A7.D8.B1.D8.A9_.D8.A7.D9.84.D8.AE.D8.AF.D9.85.D8.A7.D8.AA)
    *   [3.4 الصوت](#.D8.A7.D9.84.D8.B5.D9.88.D8.AA)
    *   [3.5 واجهة المستخدم الرسومية **G U I**](#.D9.88.D8.A7.D8.AC.D9.87.D8.A9_.D8.A7.D9.84.D9.85.D8.B3.D8.AA.D8.AE.D8.AF.D9.85_.D8.A7.D9.84.D8.B1.D8.B3.D9.88.D9.85.D9.8A.D8.A9_G_U_I)
        *   [3.5.1 تثبيت الخادم X](#.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_.D8.A7.D9.84.D8.AE.D8.A7.D8.AF.D9.85_X)
        *   [3.5.2 تثبيت مشغل الفيديو](#.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_.D9.85.D8.B4.D8.BA.D9.84_.D8.A7.D9.84.D9.81.D9.8A.D8.AF.D9.8A.D9.88)
        *   [3.5.3 تثبيت مشغلات الإدخال](#.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_.D9.85.D8.B4.D8.BA.D9.84.D8.A7.D8.AA_.D8.A7.D9.84.D8.A5.D8.AF.D8.AE.D8.A7.D9.84)
        *   [3.5.4 إعداد الخادم الرسومي X](#.D8.A5.D8.B9.D8.AF.D8.A7.D8.AF_.D8.A7.D9.84.D8.AE.D8.A7.D8.AF.D9.85_.D8.A7.D9.84.D8.B1.D8.B3.D9.88.D9.85.D9.8A_X)
        *   [3.5.5 اختبار الخادم الرسومي X](#.D8.A7.D8.AE.D8.AA.D8.A8.D8.A7.D8.B1_.D8.A7.D9.84.D8.AE.D8.A7.D8.AF.D9.85_.D8.A7.D9.84.D8.B1.D8.B3.D9.88.D9.85.D9.8A_X)
            *   [3.5.5.1 إصلاح المشكلات](#.D8.A5.D8.B5.D9.84.D8.A7.D8.AD_.D8.A7.D9.84.D9.85.D8.B4.D9.83.D9.84.D8.A7.D8.AA)
        *   [3.5.6 الخطوط](#.D8.A7.D9.84.D8.AE.D8.B7.D9.88.D8.B7)
        *   [3.5.7 اختيار وتثبيت الوجهة الرسومية](#.D8.A7.D8.AE.D8.AA.D9.8A.D8.A7.D8.B1_.D9.88.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_.D8.A7.D9.84.D9.88.D8.AC.D9.87.D8.A9_.D8.A7.D9.84.D8.B1.D8.B3.D9.88.D9.85.D9.8A.D8.A9)
*   [4 ملحق](#.D9.85.D9.84.D8.AD.D9.82)

## التجهيز

يفترض أن يعمل Arch linux على أي معالج بمعمارية [i686](https://en.wikipedia.org/wiki/P6_(microarchitecture) "wikipedia:P6 (microarchitecture)") مع 256MB ذاكرة RAM كحد أدنى. التثبيت الأساسي مع كل الحزم من المجموعة [base](https://www.archlinux.org/groups/x86_64/base/) سيأخذ أقل من 800MB من مساحة القرص.

ألقي نظرة على [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch") لمعلومات عن تنزيل وسيط التثبيت, وطرق إقلاعها على الجهاز المطلوب. هذا الدليل يفترض أنك تستخدم آخر إصدار.

### حرق أحدث صورة لإسطوانة التثبيت

أحدث نسخة من إسطوانة التثبيت متاحة من خلال صفحةالتحميل [Download](https://archlinux.org/) .لاحظ أن صورةالإسطوانةاﻷيزو تد عم كلا من معمارية 32-بت، وكذلك 64-بت .ISO تصدر صورة اﻷيزو مرة كل شهر ويوصى دائما بتنزيل أحدث نسخة من ملفات

*   .قم بحرق أو كتابة صورة القرص (اﻷيزو) ﻷحدث نسخة تثبيت

**ملاحظة :** تأكد أن محرك اﻷقراص المدمحة واﻷقراص نفسها عالية الجودة. عموما يوصى باستخدام سرعة بطيئة لحرق القرص ، فإذا كنت تعاني من سلوك غير متوقع من القرص، عليك بمحاولة حرقه بأقل سرعة يدعمها من محرك الأقراص الخاص بك.

*   ويمكنك أيضا كتابة صورة قرص أيزو إلى قرص USB،انظر : [USB Installation Media](/index.php/USB_Installation_Media "USB Installation Media").

#### التثبيت عبر الشبكة

بدلا من حرق قرص الإقلاع و التثبيت على قرص مدمج أو قرص usb يمكنك الإقلاع من صورة قرص مدمج عبر الشبكة. وذلك يعمل ايضا عندما يكون لديك خادم مُعَد بالفعل. من فضلك انظر إلى [هذا المقال](https://wiki.archlinux.org/index.php/Install_Arch_from_network_(via_PXE)/) ثم واصل مع [Boot the installation medium](#Boot_the_installation_medium).

#### التثبيت على اﻵلة الافتراضية

التثبيت على اﻵلة الافتراضية [Virtual_machine](http://en.wikipedia.org/wiki/Virtual_machine/) طريقة جيدة للتعود على توزيعة Arch Linux وإجراءات تثبيتها بدون أن تغادر نظام التشغيل الخاص بك ودون أن تعيد تقسيم القرص الصلب الخاص بك. وذلك ايضا سيجعل هذا الدليل الخاص بالمبتدئين مفتوحا أمامك في متصفح الإنترنت أثناء عملية التنصيب. ربما يجد بعض المستخدمين أنه من المفيد أن يكون هناك نظام تشغيل مستقل لArch Linux على محرك الأقراص ، بغرض الاختبار. ومن أمثلة برامج النظم الافتراضية هناك [VirtualBox](/index.php/VirtualBox "VirtualBox"), [VMware](/index.php/VMware "VMware"), [QEMU](/index.php/QEMU "QEMU"), [Xen](/index.php/Xen "Xen"), [Parallels](/index.php/Parallels "Parallels") الإجراء الفعلي لإعداد النظام الافتراضي يعتمد على نوع البرنامج، ولكنك ستتبع في الأعم الأغلب ذهه الخطوات:

1.  إنشاء صورة قرص وهمي يستخدمه النظام المضيف.
2.  إعدادات الآلة الافتراضية.
3.  الإقلاع من صورة أيزو من خلال سواقة أقراص الأﻻة الافتراضية.
4.  استكمال تثبيت النظام الوهمي من وسيط التثبيت [Boot the installation medium](#Boot_the_installation_medium).

المقالات التالية ربما تفيدك:

*   [Arch Linux as VirtualBox guest](/index.php/VirtualBox#Arch_Linux_guests "VirtualBox")
*   [Arch Linux as VirtualBox guest on a physical drive](/index.php/VirtualBox_Arch_Linux_Guest_On_Physical_Drive "VirtualBox Arch Linux Guest On Physical Drive")
*   [Arch Linux as VMware guest](/index.php/Installing_Arch_Linux_in_VMware "Installing Arch Linux in VMware")
*   [Moving an existing install into (or out of) a virtual machine](/index.php/Moving_an_existing_install_into_(or_out_of)_a_virtual_machine "Moving an existing install into (or out of) a virtual machine")

### الإقلاع من قرص التثبيت

في البداية ربما تحتاج إلى تغيير إعدادات الإقلاع من بيوس الحاسوب الخاص بك، عليك أن تضغط زر ما (عادة ما يكون `Delete`, `F1`, `F2`, `F11` أو `F12`). أثناء مرحلة إقلاع الحاسوب. بعدها تختار "Boot Arch Linux" من القائمة ثم اضغط مفتاح `Enter` من أجل بدء عملية التثبيت.

****ملاحظة :** ****الذاكرة العشوائية** رام المطلوبة للتثبيت هي 64 ميجا

**ملاحظة :** المستخدمون الذين يبحثون عن تثبيت Arch Linux عن بعد بواسطة اتصال [SSH](/index.php/SSH "SSH") عليهم القيام ببعض الإعدادات لتفعيل خدمة SSH مباشرة عبر بيئة القرص الحي، انظر هذا المقال [Install from SSH](/index.php/Install_from_SSH "Install from SSH").

بمجرد إتمام الإقلاع في بيئة القرص الحي ، ستكون الصدفة من نوع [Zsh](/index.php/Zsh "Zsh") ، وهذا يتيح لك بابا من الخيارات المتقدمة وبعض المزايا اﻷخرى من [grml config](http://grml.org/zsh/).

#### اختبار الإقلاع عبر نمط UEFI

في حالة اقتائك لوحة أم نظامها الاساسي من نوع [UEFI](/index.php/UEFI "UEFI") التي تحتوي على نظام إقلاع من نوع UEFI مفعلا ومفضل على مود BIOS/Legacy ، سيتم تشغيل نواة نظام Arch Linux من خلال محمل إقلاع Gummiboot. ولاختبار ما إذا كنت أقلعت في مود UEFI قم التأكد من إنشاء الدليل `/sys/firmware/efi` .

```
 ls -1 /sys/firmware/efi

```

**ملاحظة** في العديد من النواة تم اﻵن ترجمة الوحدة CONFIG_EFI_VARS داخل النواة. وبالتالي: لم تعد الوحدة النمطية efivars . تحتاج إلى التحميل يدويا.

#### إصلاح مشكلات الإقلاع

*   إذا كنت تستخدم إحدى شرائح إنتل الرسومية VGA وينتقل وصارت الشاشة بيضاء أثناء عملية الإقلاع، فهي على الأرجح مشكلة مع خيارت إعداد النواة [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting")

. ويمكن الالتفاف حول المشكلة من خلال إعادة التشغيل والضغط على مفتاح `e` اثناء التوقف على الخانة التي ستقلع من خلالها (i686 أو x86_64) وفي نهاية السطر اكتب nomodeset ثم اضغط مفتاح `Enter` . بدلا من ذلك حاول كتابة اﻷمر `video=SVIDEO-1:d` والذي إن عمل فلن يوقف عمل إعدادات النواة. انظر هذا المقال [Intel](/index.php/Intel "Intel") للمزيد من المعلومات.

*   إذا كانت الشاشة لم تعد بيضاء ولكن تجمدت عملية الإقلاع اثناء محاولة تحميل النواة اضغط مفتاح `Tab` اثناء الوقوف على خانة بالقائمة ، ثم اكتب `acpi=off` في نهاية السطر ثم اضغط المفتاح `Enter`.

## تثبيت النظام

أنت الآن أمام مؤشر أوامر الصدفة ، وتعمل تلقائيا كمستخدم جذر.

### تغيير اللغة

****تلميح** :** هذه الأمر اختياري بالنسبة لغالبية المستخدمين. وهو مفيد فقط إذا كنت تخطط للكتابة باللغة الخاصة بك في أي من ملفات التكوين، إذا كنت تستخدم علامات التشكيل في كلمة مرور الواي فاي، أو إذا كنت ترغب في الحصول على رسائل النظام (على سبيل المثال الأخطاء المحتملة) باللغة الخاصة بك

تأتي لوحة المفاتيح معدة افتراضيا لـ `us` . فإن كان لديك لوحة مفاتيح غير إنجليزية [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg") قم بإجراء الأمر :

```
# loadkeys _layout_

```

حيث ... _layout_ يمكن أن يكون `fr`, `uk`, `be-latin1`, إلخ . انظر [هنـا](/index.php/KEYMAP#Keyboard_layouts "KEYMAP") من أجل القائمة الشاملة.

يجب أيضا تغيير الخط، حيث إن أغلب اللغات تستخدم أكثر من 26 حرفا [English alphabet](https://en.wikipedia.org/wiki/English_alphabet "wikipedia:English alphabet") . وإلا فإن بعض المحارف ربما تظهر بصورة مربعاتبيضاء أو رمز آخر. لاحظ أن الأسماء حساسة لحالة الأحرف ، لذلك يرجى كتابتها _بالضبط_ كما تراها :

```
# setfont Lat2-Terminus16

```

افتراضيا ، اللغة معدة سلفا للإنجليزية (US). _( إن كنت ترغب في تغيير اللغة من أجل عملية التثبيت_ ( وهي الألمانية, في هذا المثال `#` من مقدمة جنبا إلى جنب قم بإزالة بجوار اللغة الإنجليزية من فضلك اختر الخانة `UTF-8`.(US) [locale](http://www.greendesktiny.com/support/knowledgebase_detail.php?ref=EUH-483) للغة التي تريدها `/etc/locale.gen` . استخدم المفاتيح `Ctrl+X` للخروج، وعندما يتغير مؤشر الصدفة اضغط المفتاح `Y` ثم المفتاح `Enter` لاستخدام نفس اسم الملف.

 `# nano /etc/locale.gen` 

```
en_US.UTF-8 UTF-8
de_DE.UTF-8 UTF-8
```

```
# locale-gen
# export LANG=de_DE.UTF-8

```

تذكر أن المفتاحين `LAlt+LShift` ينشطان ويمنعان تنشيط keymap .

### إعدادات الاتصال بالإنترنت

**تحذير** udev لم يعد يقوم بتعيين أسماء واجهة الشبكة وفقا ل wlanX ولا نظام التسمية ethX . إذا كنت قادما من توزيعة مختلفة أو قمت بإعادة تثبيت آارتش لينكس لا تنزعج من طريقة التسمسة الجديدة ، من فضلك لا تفترض أن واجهة الشبكة اللاسلكية تدعى wlan0 أو أن واجهة الشبكة السلكسة تسمىeth0 . يمكنك استخدام الأمر `ip addr show` لاستكشاف أسماء الواجهات الشبكية لديك

منذ الإصدار systemd-197 يقوم udev بتعيين أسماء لواجهات الشبكة يمكن التنبؤ بها بعيدا عن إرث التسميات القديمة مثل `wlan0`, `wlan1`). ويضمن هذا أن أسماء واجهة الشبكة لتكون مستقرة بعدإعادة التشغيل، ويحل مشكلة عدم القدرة على التنبؤ وتعيين اسم واجهة الشبكة ، (انظر [Predictable Network Interface Names](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames)):

يتم تفعيل الخدمة الشبكية تلقائيا أثناء الإقلاع وسوف تعمل على تشغيل الاتصال السلكي. حاول عمل بنج للخادم لترى ما إذا كان الاتصال يعمل أم لا . على سبيل المثال جرب سيرفرات Google's DNS . `dhcpcd`

 `# ping -c 3 www.google.com` 

```
PING www.l.google.com (74.125.132.105) 56(84) bytes of data.
64 bytes from wb-in-f105.1e100.net (74.125.132.105): icmp_req=1 ttl=50 time=17.0 ms
64 bytes from wb-in-f105.1e100.net (74.125.132.105): icmp_req=2 ttl=50 time=18.2 ms
64 bytes from wb-in-f105.1e100.net (74.125.132.105): icmp_req=3 ttl=50 time=16.6 ms

--- www.l.google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 16.660/17.320/18.254/0.678 ms
```

إذا حصلت على خطأ `ping: unknown host` , قم في االبداية بفحص المشكلة مع كابل الشبكة او قوة إشارة الاتصال اللاسلكي . فإن لم يكن ستحتاج حينئذ إلى إعداد الشبكة قم بالانتقال إلى يدويا، كما تم شرحه مسبقا. وبمجرد عمل الاتصال [Prepare the storage drive](#Prepare_the_storage_drive).

#### Wired الاتصال السلكي

اتبع هذا الإحراء إذا كنت ترغب في إعداد اتصال سلكي عن طريق IP ثابت.

أولا، قم بإيقاف خدمة dhcpcd التي تعمل تلقائيا عند الإقلاع :

```
# systemctl stop dhcpcd.service

```

قم بتعريف اسم واجهة الشبكة الخاص بك

 `# ip link` 

```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: enp2s0f0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN mode DEFAULT qlen 1000
    link/ether 00:11:25:31:69:20 brd ff:ff:ff:ff:ff:ff
3: wlp3s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP mode DORMANT qlen 1000
    link/ether 01:02:03:04:05:06 brd ff:ff:ff:ff:ff:ff
```

في هذا المثال ، واجهة الشبكة هي `enp2s0f0`. فإن لم تكن متأكدا ، فإن واجهة شبكتك يبدو أنها تبدأ بالحرف "e" ويستبعد أن تكون بادئة بالحرف "lo" أو تبدأ بالحرف "w" يمكنك أيضا استخدام االأمر `iwconfig` وترى اي نوع من واجهات الشبكة غير اللاسلكية لديك

 `# iwconfig` 

```
enp2s0f0  no wireless extensions.
wlp3s0    IEEE 802.11bgn  ESSID:"NETGEAR97"
          Mode:Managed  Frequency:2.427 GHz  Access Point: 2C:B0:5D:9C:72:BF
          Bit Rate=65 Mb/s   Tx-Power=16 dBm
          Retry  long limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          Link Quality=61/70  Signal level=-49 dBm
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:430   Missed beacon:0
lo        no wireless extensions.
```

في هذا المثال ليس الجهاز `enp2s0f0` ليس loopback ولا به ملحقات لاسلكية ومعنى `enp2s0f0` أنه واجهة الشبكة الخاصة بنا.

أنت أيضا تحتاج إلى معرفة هذه الاإعدادات:

*   عنوان ip ثابت.
*   Subnet mask قناع الشبكة.
*   عنوان IP بوابة الشبكة .
*   عنوان IP خادم أسماء النطاقات DNS.
*   Domain name (unless you are on a local LAN, in which case you can make it up).

قم بتفعيل اتصال واجهة الشبكة مثلا `enp2s0f0` :

```
# ip link set enp2s0f0 up

```

وعنوان ال IP:

```
# ip addr add _ip_address_/_subnetmask_ dev _interface_name_

```

على سبيل المثال:

```
# ip addr add 192.168.1.2/24 dev enp2s0f0

```

لمزيد من الخيارات شغل الأمر `man ip`. أضف بوابة الشبكة الخاصة بك واستبدل أرقام البوابة الخاصة بعنوان IP خاصتك.

```
# ip route add default via _ip_address_

```

على سبيل المثال:

```
# ip route add default via 192.168.1.1

```

قم بتحرير `resolv.conf`, واستبدل مكانها أسماء الخوادم وعناوين ال IP الخاصة بك واسم الدومين المحلي الخاص بك:

 `# nano /etc/resolv.conf` 

```
nameserver 61.23.173.5
nameserver 61.95.849.8
search example.com
```

**ملاحظة  :** ربما يجب إضافة أسطر ثلاثة `nameserver` كحد أقصى.

والأن يجب أن يعمل الاتصال الشبكي . فإن لم يحدث ذلك قم بفحص تفاصيل صفحة [Network configuration](/index.php/Network_configuration "Network configuration") .

#### Wireless الاتصال اللاسلكي

اتبع هذا الإجراء إن كنت تريد عمل اتصال لاسلكي (Wi-Fi) أثناء عملية التثبيت.

أولا ، حدد اسم واجهة شبكتك اللاسلكية.

 `# iwconfig` 

```
enp2s0f0  no wireless extensions.
wlp3s0    IEEE 802.11bgn  ESSID:"NETGEAR97"
          Mode:Managed  Frequency:2.427 GHz  Access Point: 2C:B0:5D:9C:72:BF
          Bit Rate=65 Mb/s   Tx-Power=16 dBm
          Retry  long limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          Link Quality=61/70  Signal level=-49 dBm
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:430   Missed beacon:0
lo        no wireless extensions.
```

في هذا المثال ، `wlp3s0` هي واجهة شبكة متاحة . فإن كنت غير متأكد فمن المرجح أن تكون واجهة شبكتك اللاسلكية تبدأ بالحرف "w" ومن غير المرجح أن تبدأ بالحرف "lo" ولا بالحرف "e" .

**ملاحظة  :** إن لم تر خرج الأمر يشبه ذلك، فمعنى ذلك أن مشغل االواجهة اللاسلكية لم يتم تحميله ، وفي هذه الحالة يجب عليك تحميل مشغل الواجهة بنفسك . يرجى قراءة [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") لمزيد من التفاصيل

تشغيل واجهة الشبكة عبر الأمر :

```
# ip link set wlp3s0 up

```

وهناك نسبة قليلة من رقائق الأجهزة اللاسلكية تتطلب أيضا البرامج الثابتة firmware ، بالإضافة إلى مشغل مقابل لها . إذا كانت شريحة الواجهةاللاسلكية تتطلب برامج ثابتةfirmware ، فمن المحتمل أن تتلقى هذا الخطأ عند تشغيل الواجهة :

 `# ip link set wlp3s0 up`  `SIOCSIFFLAGS: No such file or directory` 

إن لم تكن متأكدا جرب `dmesg` للاستعلام عن سجل ال نواة لطلب البرامج الثابتة firmware من للشرائح اللاسلكية. على سبيل المثال، الخرج الخاص بشريحة إنتل المطلوبة تتطلب برامج تشغيل فيرويمر من النواة عند الإقلاع:

 `# dmesg | grep firmware`  `firmware: requesting iwlwifi-5000-1.ucode` 

"إن لم يظهر مثل هذا الخرج ربما نستنج أن شريحة الواجهة اللاسلكية لا تتطلب برامج تشغيل أساسية "فيرموير.

**’’’ تحذيـر’’’ :** البرنامج الأساسي لشريحة الواجهة اللاسلكية (للبطاقات التي لا تحتاجها ) هي سابقة التثبيت في المسار `/usr/lib/firmware` في بيئة القرص الحي(على CD/USB فلاشة) ’’’ لكن يجب تثبيتها على النظام الحقيقي لإمداد واجهة الشبكة بعد الإقلاع من خلاله’’’ الحزم الخاصة بالتثبيت سيتم تغطيتها لاحقا في هذا الدليل. تأكد من تثبيت كل من وحدة الواجهة اللاسلكية وكذلك البرنامج الأساسي للواجهة قبل إعادة تشغيل النظام! انظر[Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") إن لم تكن متأكدا من متطلبات التثبيت الخاصة بالبرنامج الأساسي للشريحة الخاصةبك.

بعد ذلك، استخدم [netctl](https://www.archlinux.org/packages/?name=netctl)'s {{ic|wifi-menu}للاتصال بالشبكة :

```
# wifi-menu wlp3s0

```

الآن يجب أن يعمل الاتصال الشبكة. فإن لم يحدث ، قم بمراجعة التفاصيل في صفحة [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration").

#### المودم الثنائي و ISDN أوPPoE DSL

```
من أجل اتصالات xDSL ،  dial-up و ISDN , انظر [Direct Modem Connection](/index.php/Direct_Modem_Connection "Direct Modem Connection").

```

#### العمل عبر سيرفر بروكسي

If you are behind a proxy server, you will need to export the `http_proxy` and `ftp_proxy` environment variables. See [Proxy settings](/index.php/Proxy_settings "Proxy settings") for more information.

### إعدادات القرص الصلب

**تحذير** تقسيم القرص الصلب قد يدمر البيانات . فانتبه **بشدة** وننصحك بعمل نسخة احتياطية لي بيانات مهمة قبل هذا الإحراء

قطعا، يستحب للمبتدئين أن يستخدموا أداة ذات واجهة رسومية . يعتبر [GParted](http://gparted.sourceforge.net/download.php) مثالا جيدا ، وهو متاح كقرص حي [متاح كقرص "حي"](http://gparted.sourceforge.net/livecd.php) . وهو أيضا مضاف إلى القرص الحي لأغلب توزيعات لينكس مثل [Ubuntu](https://en.wikipedia.org/wiki/Ubuntu_(operating_system) "wikipedia:Ubuntu (operating system)") و [Linux Mint](https://en.wikipedia.org/wiki/Linux_Mint "wikipedia:Linux Mint") يجب أن يكون القرص الصلب أولا مقسما [partitioned](/index.php/Partitioning "Partitioning") وتكون الأقسام مهيئة بنظام ملفات [file system](/index.php/File_systems "File systems") قبل إعادة الإقلاع.

النصيجة لمن يعمل على جهاز يقلع بواسطة UEFI بدلا من النظام القديم للإقلاع MBR هو عمل تهيئة للقرص الصلب باستخدام جدول تقسيم من نوع GPT . ذلك يعني أن القرص الصلب الذي تهيئته مسبقا بنظام جداول سيكون عليه نظام جداول جديد وسيتم تدمير البيانات الأخرى على القرص . بمجرد إنشاء جدول التقسيم الجديد على القرص يمكن عمل أقسام مستقلة مع اي نوع من أنواع نظم الملفات المختارة. MBR (MSDOS) . عند استخدام الأداة Gparted اختيار إنشاء جدول جديد للأقسام يكون افتراضيا من نوع دوس "msdos" . إذا كنت تنوي اتباع النصيحة بإنشاء جدول تقسيم من نوع GPT حينئذ تحتاج لاختيار الخيار _متقدم_ "Advanced" ثم اختر "gpt" من القائمة المنسدلة. لا يمكن تحقيق ذلك إن كنت قمت مكسبقا بتثبيت نظام وندوز على القرص الصلب الذي لا ترغب بتدمير بياناته. إذا كنت تنوي وجود نظام تشغيل مزدوج الإقلاع فلا تقم بتغيير نظام جدول الأقسام إلى نوع GPT . اترك نظام وندوز كما هو وحاول تثبيت عليه نظام لينكس يعمل مع UEFI على قرص يحتوي على جدول تقسيم MBR القديم . إضافة إلى ذلك، يوجد بعض الحواسب الحديثة تأتي بنظام وندوز 8 سابق التثبيت وهو يعمل بنظام الإقلاع اﻵمن . وتوزيعة آرتش لينكس لا تدعم حاليا الإقلاع اﻵمن ، ولكن يعض نسخ وندوز 8 لوحظ أنها لا تقلع إذا تم تعطيل خاصية الإقلاع اﻵمن Secure Boot من البيوس. في بعض الحالات يكون من الضروري تعطيل كل من اﻹقلاع اﻵمن Secure Boot وكذلك الإقلاع السريع Fastboot من خيارات البيوس في سبيل السماح بإقلاع وندوز 8 بدون Secure Boot. على أية حال توجد بعض المخاطر اﻷمنية عند تعطيل Secure Boot من أجل إقلاع وندوز 8 . لذلك ربما يكون من المفضل الاحتفاظ بوندوز 8 دون مساس والحصول على قرص صلب مستقل من أجل تثبيت لينكس . والذي يمكن تقسيمه لاحقا من الصفر باستخدام جدول GPT . وبمجرد حصول ذلك قم بغنشاء عدة أقسام بنظم ملفات ext4/FAT32/swap على القرص الثاني هو أفضل السبل إذا كان الحاسب يحتوي على قرصين . وغالبا ما يكون ذلك متعذرا خاصة على الحواسب المحمولة الصغيرة . حاليا Secure Boot ما زال غير مستقر تماما حتى مع توزيعات لينكس التي تدعمه. إذا كنت ترغب في عمل قسم تبديل SWAP أو ملف Swap . يعتبر ملف Swap أيسر من حيث تغيير المساحة من قسم Sawp ، ويمكن إنشاؤه وربطه مع أي نقطة ربط بعد انتهاء التثبيت, ولكن لا يمكن استخدامه مع نظام ملفات من نوعBtrfs إن قمت بعمل ذلك بالفعل اذهب إلى [Mount the partitions](#Mount_the_partitions). ولمزيد من التفاصيل انظر [Swap](/index.php/Swap "Swap")

بخلاف ذلك انظر إلى المثال التالي :

#### مثال

يحتوي قرص تثبيت آرتش لينكس على أدوات تقسيم القرص الصلب التالية : `fdisk`, `gdisk`, `cfdisk`, `cgdisk`, `parted`.

**تلميحة** استخدم اﻷمر `lsblk` لعرض قائمة اﻷقراص الصلبة المتصلة بالنظام إضافة إلى أحجام الأقسام. وذلك سيساعدك على التحقق من أنك تقسم القرص الصلب الصحيح.

**ملاحظات بخصوص إقلاع [UEFI](/index.php/UEFI "UEFI")**

*   إذا كان لديك لوحة أم [UEFI](/index.php/UEFI "UEFI") ستحتاج إلى إنشاء قسم إضافي للنظام [UEFI System Partition](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface").
*   ينصح دائما باستخدام جدول تقسيم GPT لإقلاع UEFI، حيث إن بعض مشغلات UEFI لا تسمح بإقلاع UEFI-MBR .

**ملاحظات بخصوص تقسيم [GPT](/index.php/GPT "GPT") :**

*   إن لم يكن لديك نظام إقلاع مزدوج مع وندوز ، حينئذ ينصح باستخدام جدول تقسيم GPT بدلا من mbr . اقرأ [GPT](/index.php/GPT "GPT") لمعرفة قائمة المزايا.
*   إذا كان لديك لوحة أم مع BIOS ( أو كنت تخطط للإقلاع بنمط BIOS ) وقد قمت بتثبيت محمل إقلاع GRUB على قسم من نوع GPT ستحتاج لإنشاء قسم إضافي على القرص [قسم إقلاع BIOS](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB")

Syslinux لا يحتاج إلى ذلك .

*   بعض أنظمة بيوس ربما تتعرض لمشكلات مع GPT. انظر لمزيد من المعلومات [http://mjg59.dreamwidth.org/8035.html](http://mjg59.dreamwidth.org/8035.html) و [http://rodsbooks.com/gdisk/bios.html](http://rodsbooks.com/gdisk/bios.html) والحلول المتاحة .

**ملاحظة** إذا كنت تقوم بالتثبيت على قرص USB انظر [Installing Arch Linux on a USB key](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key").

هذا المثال سيحتوي على 15 جيجا كقسم جذر ، [home](/index.php/Partitioning#.2Fhome "Partitioning") و قسم للمنزل على المساحة المتبقية. اختر إما [MBR](/index.php/MBR "MBR") or [GPT](/index.php/GPT "GPT") ﻻ تختر كليهما معا! .

وينبغي التأكيد على أن مسألة التقسيم هي اختيار شخصي وأن هذا المثال هو فقط لأغراض التوضيح. انظر [Partitioning](/index.php/Partitioning "Partitioning").

| **MBR** | `cfdisk /dev/sda` | **Root:**

*   Choose New (or press `N`) – `Enter` for Primary – type in "15360" – `Enter` for Beginning – `Enter` for Bootable.

 |
| 

**Home:**

*   Press the down arrow to move to the free space area.
*   Choose New (or press `N`) – `Enter` for Primary – `Enter` to use the rest of the drive (or you could type in the desired size).

 |
| **GPT** | `cgdisk /dev/sda` | **Root:**

*   Choose New (or press `N`) – `Enter` for the first sector (2048) – type in "15G" – `Enter` for the default hex code (8300) – `Enter` for a blank partition name.

 |
| **Home:**

*   Press the down arrow a couple of times to move to the larger free space area.
*   Choose New (or press `N`) – `Enter` for the first sector – `Enter` to use the rest of the drive (or you could type in the desired size; for example "30G") – `Enter` for the default hex code (8300) – `Enter` for a blank partition name.

 |

إذا قمت باختيار MBR ينبغي أن يظهر بالشكل التالي

```
Name    Flags     Part Type    FS Type          [Label]       Size (MB)
-----------------------------------------------------------------------
sda1    Boot       Primary     Linux                             15360
sda2               Primary     Linux                             133000*

```

إذا قمت باختيار GPT ينبغي أن يظهر بالشكل التالي :

```
Part. #     Size        Partition Type            Partition Name
----------------------------------------------------------------
            1007.0 KiB  free space
   1        15.0 GiB    Linux filesystem
   2        123.45 GiB  Linux filesystem

```

قم بالتحقق مرة أخرى وتأكد أنك راضٍ بهذا التقسيم وأيضا بالجدول هذا قبل المواصلة. إذا كنت ترغب في البدء من جديد يمكنك ببساطة اختيار Quit (أو اضغط `Q`) للخروج دون حفظ أي تغييرات ثم أعد تشغيل cfdisk (أو cgdisk). إذا كنت راضيا ، اختر Write (او اضغط `Shift+W`) للإنهاء وكتابة جدول التقسيم على القرص الصلب. اضغط "yes" واختر Quit (أو اضغط `Q`) للخروج دون عمل أية تغييرات أخرى.

التقسيم البسيط ليس كافيا ، يجب أيضا ان تحتوي الأقسام على نظم ملفات بنظام ملفات ext4 [نظام ملفات](/index.php/File_systems "File systems")  :

**تحذيـر** تأكد مرتين وثلاثة أن القسم `/dev/sda2` و `/dev/sda1` هو بالفعل ما تريد تهيئته. يمكنك استخدام اﻷمر`lsblk` ليساعدك في ذلك .

```
# mkfs.ext4 /dev/sda1
# mkfs.ext4 /dev/sda2

```

إذا كنت قد قمت بعمل قسم سواب (code 82) ، لا تنسَ تهيئته وتنشيطه باﻷمرين:

```
# mkswap /dev/sda_X_
# swapon /dev/sda_X_ 

```

### ربط أقسام القرص الصلب

كل قسم يكون معرفا ومذيلا برقم . كمثال `sda1` يعرف بأنه القسم اﻷول للقرص الصلب اﻷول، بينما `sda` يعرف بأنه القرص الصلب بأكمله. لعرض جدول بأقسام القرص الحالي اكتب اﻷمر :

```
# lsblk /dev/sda

```

**ملاحظة :** لا تقم بربط أكثر من قسم واحد على نفس المجلد. وكن منتبها ﻷن مسألة الربط أمر مهم.

بدايةً، اربط قسم الجذر مع المجلد `/mnt` . اتباع المثال السابق عند استخدام اﻷمر `cfdisk` (قد يكون اﻷمر مختلفا بالنسبة لك) سيكون اﻷمر هكذا:

```
# mount /dev/sda1 /mnt

```

ربط قسم المنزل وأي قسم منفصل مثل `/boot`, `/var` إلخ ، إن كان لديك أي منها :

```
# mkdir /mnt/home
# mount /dev/sda2 /mnt/home

```

في حال كان لديك لوحة أم بنظام UEFI اربط قسم UEFI : In case you have a UEFI motherboard, mount the UEFI partition:

```
# mkdir -p /mnt/boot/efi
# mount /dev/sda_X_ /mnt/boot/efi

```

### mirror اختيار خادم بديل

قبل التثبيت لعلك ترغب في تحرير الملف `mirrorlist` ووضع ما تفضله من خوادم أولا. سيتم تثبيت نسخة من هذا الملف على نظامك الجديد باﻷمر `pacstrap` ، لذا فإن الأمر يستحق الحصول علىه حقا .

 `# nano /etc/pacman.d/mirrorlist` 

```

##
## Arch Linux repository mirrorlist
## Sorted by mirror score from mirror status page
## Generated on 2012-MM-DD
##

Server = http://mirror.example.xyz/archlinux/$repo/os/$arch
...
```

*   `Alt+6` لنسخ سطر `Server`.
*   `PageUp` مفتاح لتحريك شريط التمرير ﻷعلى.
*   `Ctrl+U` للصق في أعلى القائمة .
*   `Ctrl+X` للخروج، وعند ظهور المؤشر لحفظ التغييرات, اضغط مفتاح `Y` `Enter` لاستخدام نفس اسم الملف .

إذا أردت يمكنك جعله **هو فقط** الخادم المتاح مع التخلص من أي شيء آخر ( باستخدام المفتاحين `Ctrl+K`) ، لكن ذلك فكرة جيدة للحصول على عدد أقل، في حال ما أصبح الخادم اﻷول غير متاح.

{{Box GREEN|تلميحة:| * استخدم مولد قائمة الخوادم للحصول على أحدث قائمة [Mirrorlist Generator](https://www.archlinux.org/mirrorlist/) خوادم خاصة بببلدك. تعد خوادم HTTP أسرع من خوادم FTP بسبب شيء يدعى [keepalive](https://en.wikipedia.org/wiki/Keepalive "wikipedia:Keepalive") مع خوادم FTP يقوم باكمان pacman بإرسال إشارة كل مرة لتنزيل حزمة ما مسببا بعض التأخير القصير ولمعرفة طرق أخرى لتوليد قائمة الخوادم انظر [[Mirrors#Sorting mirrors| ترتيب الخوادم و [Reflector](/index.php/Reflector "Reflector"). * يقدم تقارير متنوعة مثل مشاكل الشبكة مع الخوادم ومجموعة مشاكل البياانات وآخر مرة تم فيها مزامنة الخوادم [Arch Linux MirrorStatus](https://archlinux.org/mirrors/status/).}}

**تلميحة:** * استخدم مولد قائمة الخوادم [Mirrorlist Generator](https://www.archlinux.org/mirrorlist/) للحصول على أحدث قائمة خوادم خاصة بببلدك.

تعد HTTP أسرع من خوادم FTP بسبب شيء يدعى [keepalive](https://en.wikipedia.org/wiki/Keepalive "wikipedia:Keepalive") مع خوادم FTP.

يقوم باكمان pacman بإرسال إشارة كل مرة لتنزيل حزمة ما مسببا بعض التأخير القصير ولمعرفة طرق أخرى لتوليد قائمة الخوادم انظر [Sorting mirrors](/index.php/Mirrors#Sorting_mirrors "Mirrors") و [Reflector](/index.php/Reflector "Reflector") . *يقدم [Arch Linux MirrorStatus](https://archlinux.org/mirrors/status/) تقارير متنوعة مثل مشاكل الشبكة مع الخوادم ومجموعة مشاكل البياانات وآخر مرة تم فيها مزامنة الخوادم .

**ملاحظة**

*   كلما قمت في المستقبل بتغيير القائمة الخاصة بك من الخوادم، تذكر دائما أن تجبر بكمان لتحديث جميع قوائم الحزم بالأمر `pacman -Syy` وتعتبر هذه الممارسة جيدة وسوف تجنبك الصداع قدر الإمكان. انظر [Mirrors](/index.php/Mirrors "Mirrors")

لمزيد من المعلومات.

*   إذا كنت تستخدم إسطوانة تثبيت قديمة ربما تكون قائمة الخوادم غير محدثة ما قد يؤدي إلى عند تحديث آرتش لينكس ، انظر [FS#22510](https://bugs.archlinux.org/task/22510) . لذلك ننصح بالحصول على بيانات أحدث خادم كما تم شرحه سابقا.
*   بعض المشكلات تم الإبلاغ عنها في منتديات [Arch Linux forums](https://bbs.archlinux.org/).

فيما يخص مشكلات الشبكة التي تمنع باكمن من التحديث او مزامنة المتطلبات انظر [[1]](https://bbs.archlinux.org/viewtopic.php?id=68944) و [[2]](https://bbs.archlinux.org/viewtopic.php?id=65728) . عند تثبيت آرتش لينكس محليا يتم حل هذه المشكلة عن طريق إحلال ملف بكمان الافتراضي بملف تحميل بديل، انظر [Improve pacman performance](/index.php/Improve_pacman_performance "Improve pacman performance") للمزيد من التفاصيل.

عند تثبيت آرتش لينكس كنظام ضيف على اﻵلة الافتراضية [VirtualBox](/index.php/VirtualBox "VirtualBox") ، تم معالجة هذه المشكلة أيضا باستخدام واجهة الشبكة "Host interface" بدلا من "NAT" في خصائص الآلة.

### تثبيت النظام الأساسي

تم تثبيت النظام اﻷساسي باستخدام السكربت[pacstrap](https://github.com/falconindy/arch-install-scripts/blob/master/pacstrap.in) . الخيار `-i` يمكن إهماله غذا كنت ترغب في تثبيت كل حزمة من المجموعة _base_ بدون تنبيه .

```
# pacstrap -i /mnt base

```

**ملاحظة**

إذا فشل بكمان في الحصول على الحزم ، قم بفحص توقيت النظام بالأمر `cal` . إذا كان توقيت النظام غير صالح ) كأن يظهر التاريخ في سنة 2010 مثلا ) ، وسوف تظهر مفاتيح توقيع منتهية الصلاحية (أو غير صالحة) ، التوقيع الذي يفحص في الحزم سيفشل وسوف تتوقف عملية التثبيت . تأكد من التوقيت الصحيح للنظام ، إما بعمل ذلك يدويا او بالعميل[ntp](https://www.archlinux.org/packages/?name=ntp) ، وأعد محاولة تشغيل اﻷمر pacstrap.

اذهب إلى صفحة [Time](/index.php/Time "Time") للمزيد من المعلومات عن تصحيح توقيت النظام.

**ملاحظة** إذا كان بكمان يشكو من خطأ

```
`error: failed to commit transaction (invalid or corrupted package)`,

```

شغل الأمر التالي :

```
# pacman-key --init && pacman-key --populate archlinux. 

```

ذلك سيمنحك النظام اﻷساسي ل آرتش لينكس. وسيتم تثبيت الحزم اﻷخرى لاحقا باستخدام [pacman](/index.php/Pacman "Pacman").

### توليد ملف fstab

اوليد ملف [fstab](/index.php/Fstab "Fstab") من خلال اﻷمر التالي, سوف نستخدم UUIDs ﻷنها تحتوي على مزايا معينة انظر [fstab#Identifying filesystems](/index.php/Fstab#Identifying_filesystems "Fstab")). إذا كنت تفضل استخدام اسماء للاقسام بدلا من ذلك ضع الخيار `-L` بدلا من `-U` .

```
# genfstab -U -p /mnt >> /mnt/etc/fstab
# nano /mnt/etc/fstab 

```

**تحذير** يجب دوما فحص ملف fstab بعد إنشائه . إن واجهتك أخطاء عند تشغيل genfstab أو لاحقا أثناء عملية التثبيت **فلا** تشغل اﻷمر genfstab ثانية ، فقط قم بتحرير الملف fstab .

بعض الاعتبارات :

*   فقط القسم الجذر (`/`) يحتاج لكتابة الرقم `1` في آخر حقل. وسوى ذلك يحتاج لكتابة رقم إما `2` أو `0` انظر تعاريف هذه الحقول في [fstab#Field definitions](/index.php/Fstab#Field_definitions "Fstab").

### تغيير الجذر `chroot` وإعداد النظام اﻷساسي

فيما يلي قمنا بتبديل الجذر [chroot](/index.php/Chroot "Chroot") إلى النظام الجديد المثبت : Next, we [chroot](/index.php/Chroot "Chroot") into our newly installed system:

```
# arch-chroot /mnt 

```

**تحذير** استخدم اﻷمر `arch-chroot /mnt /bin/bash` لتبديل الجذر chroot في صدفة باش .

عند هذه المرحلة من التثبيت ستقوم بإعداد ملفات ال التهيئة الأولية للنظام اﻷساسي لآرتش لينكس . وذلك يكون إما بإنشائها إن لم تكن موجودة أو بتحريريها إن أردت تغيير إعداداتها الافتراضية. اتباع وفهم هذه الخطوات عن كثب هو مفتاح ذو أهمية لضمان صحة إعدادات وتكوين النظام.

#### Locale ضبط الإعدادات المحلية

تستخدم الإعدادات المحلية Locales بواسطة **glibc** والبرامج والمكتبيات اﻷخرى في تصيير الكتابة ، عرض قيم الإعدات المحلية بشكل صحيح، ، التوقيت وشكل التاريخ ، الألفبائية ، العملة ، الخصوصيات ، والإعدادات المحلية القياسية اﻷخرى. يوجد ملفان يحتاجان للتعديل : `locale.gen` و `locale.conf`.

*   الملف `locale.gen`) ( يكون افتراضيا فارغا ( كل شيء بالملف عليه تعليق .

وتحتاج لإزالة علامة `#` من أمام اﻷسطر التي تريدها. ويجوز ان تزيل التعليق لأسطر أخرى بجانب الإنجليزية (US) بجانب اختيارك التكويد `UTF-8` :

 `# nano /etc/locale.gen` 

```
en_US.UTF-8 UTF-8
de_DE.UTF-8 UTF-8
```

```
# locale-gen

```

ذلك سيعمل عند كل تحديث لـ **glibc**، وتوليد كل الإعدادات المحلية في الملف `/etc/locale.gen`.

*   الملف `locale.conf` ليس موجودا افتراضيا. فقط إعداد Setting only `LANG` يجب أن يكون كافيا . ذلك سيفعل القيمة الافتراضية لجميع المتغيرات اﻷخرى .

```
# echo LANG=en_US.UTF-8 > /etc/locale.conf
# export LANG=en_US.UTF-8

```

**تنبيه** إذا قمت بإعداد لغة ما غير الإنجليزية (US) في مقدمة عملية التثبيت ، الأمر السابق سيكون شبيها بما يلي :

```
# echo LANG=de_DE.UTF-8 > /etc/locale.conf

```

# export LANG=de_DE.UTF-8

لاستخدام إعدات محلية أخرى لمتغيرات `LC_*` اﻷخرى ، شغل اﻷمر `locale` لترى الخيارات المتاحة وإضافتها للملف `locale.conf`. ولا ينصح بوضع متغير `LC_ALL` . المثال المتقدم يمكن رؤيته [هنـــا](/index.php/Locale#Setting_system-wide_locale "Locale").

#### خط الكونسول ومخطط لوحة المفاتيح

إذا قمت بتغيير لوحة المفاتيح عند بداية عملية التثبيت [the beginning](#Change_the_language) قم بتحميل ذلك أيضا ﻷن البيئة قد تغيرت ، على سبيل المثال:

```
# loadkeys _de-latin1_
# setfont Lat2-Terminus16

```

ولتجعلها متاحة بعد إعادة التشغيل قم بتعديل الملف `vconsole.conf` :

```
{{hc|# nano /etc/vconsole.conf|2=
KEYMAP=de-latin1
FONT=Lat2-Terminus16 

```

*   `KEYMAP` – الطرفيات يرجى ملاحظة ان هذه الإعدادات خاصة خاصة بواجهاتTTYs الخاصة بك وليس باي مدير للنوافذ الرسومية أو خادم Xorg.

*   `FONT` – خطوط الكونسول البديلة توجد في المجلد `/usr/share/kbd/consolefonts/` .

الفراغ الافتراضي يعد آمنا، بينما بعض الحروف قد تبدو كمربعات بيضاء أو كرموز أخرى. يوصى بتغيير ذلك إلى `Lat2-Terminus16` ، وفقا ل `/usr/share/kbd/consolefonts/README.Lat2-Terminus16` والتي تدعي أنها تدعم حوالي ( 110 لغة ) .

*   الخيار المتاح `FONT_MAP` ـ يحدد مخطط الكونسول لتحميله أثناء الإقلاع. اقرأ `man setfont`. قم بإزالته أو تركه فارغا في أمان. انظر [Console fonts](/index.php/Fonts#Console_fonts "Fonts") و `man vconsole.conf` لمزيد من المعلومات .

#### ضبط منطقة التوقيت Time zone

المناطق الزمنية المتاحة والمناطق الفرعية يمكن إيجادها في المسارات `/usr/share/zoneinfo/<Zone>/<SubZone>` . لرؤية المناطق المتاحة ، افحص المجلد `/usr/share/zoneinfo/`:

```
# ls /usr/share/zoneinfo/

```

كذلك، يمكنك فحص مكونات المجلدات المنتمية إلى <SubZone>:

```
# ls /usr/share/zoneinfo/Europe

```

قم بإنشاء اختصار symbolic link `/etc/localtime` لملف المنطقة الزمنية الخاصة بك `/usr/share/zoneinfo/<Zone>/<SubZone>` باستخدام هذا اﻷمر:

```
# ln -s /usr/share/zoneinfo/<Zone>/<SubZone> /etc/localtime

```

**مثال:**

```
# ln -s /usr/share/zoneinfo/Europe/Minsk /etc/localtime

```

#### ساعة العتاد Hardware clock

اضبط وضع ساعة الجهاز بشكل موحد بين أنظمة التشغيل لديك. وإلا، فإنها قد تكتب فوق ساعة الجهاز وتسبب التحولات الزمنية يمكنك توليد الملف `/etc/adjtime` تلقائيا باستخدام أحد هذه اﻷوامر

*   **UTC** (يوصى به)

**ملاحظة** استخدام [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time "wikipedia:Coordinated Universal Time") لساعة العتاد لا يعني أن البرامج ستظهر التوقيت بنظام UTC.

	 `# hwclock --systohc --utc` 

لعمل مزامنة لتوقيت "UTC" عبر الإنترنت ، انظر [NTPd](/index.php/Network_Time_Protocol_daemon "Network Time Protocol daemon").

*   **localtime** (للأسف يستخدم افتراضيا في نظام تشغيل وندوز)

**تحذيـر** استخدام _localtime_ بما يؤدي إلى أضرار وأخطاء برمجية غير قابلة للإصلاح، ومع ذلك، لا توجد خطط لإسقاط دعم _localtime_.

	 `# hwclock --systohc --localtime` 

إن كان لديك ( او تخطط لعمل ) إقلاع مزدوج مع وندوز :

*   يوصى بـ : ضبط كل من آرتش لينكس و وندوز على UTC. تحتاج إلى [في وندوز مصلح للسجلات](/index.php/Time#UTC_in_Windows "Time") .

كذلك تأكد من منع وندوز من مزامنة وندوز للتوقيت عبر الإنترنت ، لن ساعة العتاد ستعود افتراضيا إلى _localtime_.

*   لا يوصى بـ: ضبط آرتش لينكس على _localtime_ وتعطيل أي خدمات متعلقة بالتوقيت ، مثل [NTPd](/index.php/Network_Time_Protocol_daemon "Network Time Protocol daemon")

ذلك سيجعل وندوز ينتبه لتصحيح ساعة العتاد وسوف تحتاج إلى تذكر الإقلاع عبر وندوز على اﻷقل مرتين كل عام ( في الربيع وفي الخريف). حيث [DST](https://en.wikipedia.org/wiki/Daylight_saving_time "wikipedia:Daylight saving time") حيث التوقيت الصيفي.

#### وحدات النواة Kernel modules

**تلميحة** كافة الوحدات يتم تحميلها آليا عن طريق udev ، يعد هذا مثالا فحسب ، أنت لا تحتاج لعمله . كل لذلك نادرا ما ستحتاج إلى إضافة شيء هنا. فقط أضف الوحدات التي تعلم أنها مفقودة.

لكي يتم تحميل وحدات النواة أثناء الإقلاع، ضع ملف `*.conf` في `/etc/modules-load.d/` ، مع اسم يستندإلى البرنامج الذي يستخدمه

 `# nano /etc/modules-load.d/virtio-net.conf` 

```
 # Load 'virtio-net.ko' at boot.
 virtio-net
```

إذا كان هناك وحدات أخرى ينبغي تحميلها بـ `*.conf`، يمكنك الفصل بين أسماء الملفات بسطر جديد يعتبر كمثال جيد[VirtualBox Guest Additions](/index.php/VirtualBox#Arch_Linux_guests "VirtualBox") . الأسطر الفارغة تبدأ بـ `#` أو مهملة.

#### اسم الجهاز المضيف Hostname

ضع اسم المضيف [hostname](https://en.wikipedia.org/wiki/hostname "wikipedia:hostname") حسبما ترغب مثلا _arch_ .

```
# echo _myhostname_ > /etc/hostname

```

**ملاحظة** لا حاجة لتعديل الملف `/etc/hosts`.

### إعدادات الشبكة

ستحتاج لضبط إعدادات الشبكة مرة ثانية ، ولكن هذه المرة لبيئة نظامك الجديد المثبت . الإجرائات والمتطلبات الأساسية مشابهة جدا لتلك التي سبق وصفها أعلاه [above](#Establish_an_internet_connection). ما عدا اننا سنجعلها مستمرة وتعمل تلقائيا أثناء الإقلاع .

**ملاحظة** لمعلومات عميقة عن إعدادات الشبكة يمكنك زيارة [Network configuration](/index.php/Network_configuration "Network configuration") و [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration").

#### الاتصال السلكي

**تحذير** ظهرت إحدى العلل البرمجية في أيزو التثبيت، في اختلاف تعيين اسم واجهة الشبكة أثناء التثبيت عنه بعد إعادة التشغيل . انظر [FS#33923](https://bugs.archlinux.org/task/33923) لمزيد من التفاصيل .
استخدم اﻷمر `ip link` ( الذي يظهر اسماء واجهات الشبكة ) بعد إعادة التشغيل في النظام المثبت لاكتشاف ما إذا تأثر سلبا بسبب ذلك . إذا كان ذلك عليك أن تعيد الإعدادات التي تم شرحها آنفا من خلال تصحيح اسم الواجهة.

##### رقم IP متغير

	باستخدام dhcpcd

إذا كنت تستخدم اتصال شبكي وحيد، فلست بحاجة لخدمة إدارة الشبكة ، ويمكنك ببساطة تشغيل خدمة `dhcpcd` . حيث `_interface_name_` هنا ، هي اسم واجهة الاتصال الشبكي السلكي لديك :

```
# systemctl enable dhcpcd@_interface_name_.service

```

	باستخدام netctl

قم بنسخ نموذج الملف الشخصي من `/etc/netctl/examples` إلى `/etc/netctl/`:

```
# cd /etc/netctl
# cp examples/ethernet-dhcp .

```

قم بتعديل البروفايل كما هو مطلوب ( تعديل `Interface`):

```
# nano ethernet-dhcp

```

قم بتفعيل خدمة `ethernet-dhcp` :

```
# netctl enable ethernet-dhcp

```

	باستخدام netctl-ifplugd

بدلا من ذلك يمكنك استخدام [netctl](https://www.archlinux.org/packages/?name=netctl)'s `netctl-ifplugd` ، الذي يعالج برشاقة الاتصالات الديناميكية للشبكات الجديدة قم بتثبيت [ifplugd](https://www.archlinux.org/packages/?name=ifplugd) وهو مطلوب من أجل عمل `netctl-ifplugd`:

```
# pacman -S ifplugd

```

بعدها ، قم بتفعيل واجهة الشبكة التي تريد :

```
# systemctl enable netctl-ifplugd@<interface>.service

```

##### رقم IP ثابت

	باستخدام netctl

قم بنسخ نموذج الملف الشخصي من `/etc/netctl/examples` إلى `/etc/netctl/`:

```
# cd /etc/netctl
# cp examples/ethernet-static .

```

قم بتعديل الملف الشخصي كما هو مطلوب : تعديل `Interface` ، `Address` ، `Gateway` و `DNS`):

```
# nano ethernet-static

```

بعدها قم بتفعيل البروفايل الذي أنشئ مسبقا :

```
# netctl enable ethernet-static

```

#### الاتصال اللاسلكي Wireless

ستحتاج إلى تثبيت برامج إضافية لتمكنك من تهيئة و تشغيل الشبكة اللاسلكية ل [netcfg](/index.php/Netcfg "Netcfg"). تعتبر [NetworkManager](/index.php/NetworkManager "NetworkManager") و [Wicd](/index.php/Wicd "Wicd") بدائل شهيرة :

*   تثبيت الحزم المطلوبة:

```
# pacman -S wireless_tools wpa_supplicant wpa_actiond dialog

```

إذا كان محول الوايرلس يحتاج لبرنامج تشغيلي ( كما تم شرحه مسبقا) في قسم [Establish an internet connection](#Wireless) وكذلك قسم [here](/index.php/Wireless_network_configuration#Drivers_and_firmware "Wireless network configuration")) قم بتثبيت الحزمة التي تتضمن الفيرموير الخاص بك. مثلا :

```
# pacman -S zd1211-firmware

```

انظر [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") و [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") لمزيد من المعلومات.

*   بعد الانتهاء من بقية خطوات التثبيت هذه ثم إعادة التشغيل، يمكنك الاتصال بالشبكة عن طريق `wifi-menu _interface_name_` ، حيث `_interface_name_` هو اسم شريحة بطاقة الوايرلس ، والتي تنشئ ملفا شخصيا في `/etc/network.d` مسماة بعد SSID.

يوجد أيضا قوالب متاحة في `/etc/network.d/examples/` لدليل الإعدادات.

```
# wifi-menu _interface_name_

```

**تحذير** `wifi-menu` فيجب أن يكون ذلك *بعد* إعادة التشغيل بعد أن لم تعد مبدلا للجذر chroot . هذه العملية نتجت بهذا اﻷمر ستتعارض إذا كنت مستخدما مع مع ما قمت به خارج مبدل الجذر chroot . بدلا من ذلك يمكن فقط أن تقوم بتعديل ملف الشبكة يدويا باستخدام القوالب التي سبق ذكرها آنفا ، لذا ليس عليك أن تقلق بشأن استخدام اﻷمر `wifi-menu` مطلقا .

*   قم بتفعيل خدمة `net-auto-wireless` التي ستتصل بكل الشبكات المعروفة وتتعامل برشاقة التجوال وقطع الاتصالات :

```
# systemctl enable net-auto-wireless.service

```

**ملاحظة** من [Netcfg#Net-Auto-Wireless](/index.php/Netcfg#Net-Auto-Wireless "Netcfg") ملفات البروفايل `wireless-wpa-config` لا تعمل مع `net-auto-wireless` . قم بتحويلها إلى `wireless-wpa-configsection` أو `wireless-wpa` بدلا من ذلك.

**ملاحظة** توفر [Netcfg](/index.php/Netcfg "Netcfg") أيضا `net-auto-wired` والتي يمكن استخدامها بالتعاون مع `net-auto-wireless` .

**ملاحظة**

يمكن فشل Wpasupplicant مع رسالة "WPA Authentication/Association Failed".

في هذه الحالة انظر هذا [الرابط](https://bbs.archlinux.org/viewtopic.php?id=155273) لمعرفة الحل .

*   تأكد من وضع اسم واجهة الشبكة اللاسلكية الصحيح مثلا `wlp3s0` في `/etc/conf.d/netcfg`:

 `# nano /etc/conf.d/netcfg`  `WIRELESS_INTERFACE="wlp3s0"` 

ومن الممكن أيضا تحديد قائمة من بروفايلات الشبكة والتي يجب أن تتصل تلقائيا، باستخدام المتغير `AUTO_PROFILES` في الملف `/etc/conf.d/netcfg`. إذا لم يتم وضع `AUTO_PROFILES` كل الشبكات اللاسلكية ستيتم تجربتها

#### ISDN أو المودم الثنائي، PPoE DSLISDN

```
من أجل اتصالات من نوع xDSL ، dial-up و  ISDN  انظر  [Direct Modem Connection](/index.php/Direct_Modem_Connection "Direct Modem Connection").

```

### إنشاء بيئة قرص الذاكرة الأولي initial ramdisk environment

**تلميحة واستخدام** أغلب المستخدمين يمكنهم تجاوز هذه الخطوة ، واستخدام ال المتاحة في `mkinitcpio.conf`. initramfs تم توليد وإنشا ء صور قرص الذاكرة بالفعل في الدليل `/boot` على أساس هذا الملف حيث إن الحزمة [linux](https://www.archlinux.org/packages/?name=linux) ( نواة لينكس ) تم تثبيتها مسبقا من خلال اﻷمر `pacstrap`.

وهنا أنت تحتاج لوضع الخيارات الصحيحة للخطاطيف [hooks](/index.php/Mkinitcpio#HOOKS "Mkinitcpio") إذا كان قسم الجذر على قرص USB . إذا كنت تستخدم مصفوفة RAID ، LVM , أو كان الدليل `/usr` على قسم منفصل من القرص الصلب.

قم بتعديل الملف `/etc/mkinitcpio.conf` كما هو مطلوب ، وأعد توليد قرص الذاكرة اﻷولي initramfs بالأمر:

```
# mkinitcpio -p linux

```

**ملاحظة** تثبيت الخادم الافتراضي لآرتش لينكس

VPS على المحاكي QEMU حين نستخدم `virt-manager` ربما يحتاج إلى وحدات `virtio` في `mkinitcpio.conf` ليكون قابلا للإقلاع.

 `# nano /etc/mkinitcpio.conf`  `MODULES="virtio virtio_blk virtio_pci virtio_net"` 

### تحديد كلمة مرور المستخدم الجذر

ضع كلمة مرور المستخدم الجذر باﻷمر :

```
# passwd

```

### تثبيت وإعداد محمل الإقلاع

#### خاص بلوحات أم بنظام BIOS

بخصوص أنظمة بيوس ، يوجد ثلاث محملات إقلاع ـ Syslinux ، GRUB و [LILO](/index.php/LILO "LILO"). وفقا لراحتك اختر من محملات الإقلاع . وفيما يلي سيتم شرح Syslinux و GRUB فقط.

*   Syslinux مقتصر حاليا على تحميل الملفات من على القسم الذي تم تثبيتها عليه فقط. ويعتبر مل التكوين الخاص به أكثر يسرا في فهمه. يمكن الحصول على مثال للإعداد [هنا](https://bbs.archlinux.org/viewtopic.php?pid=1109328#p1109328).
*   GRUB يعد أكثر ثراءًا في مزاياه ويدعم السيناريوهات اﻷكثر تعقيدا . إعداد ملفات جروب يشبه كثيرا لغة البرمجة النصية، وهي ربما تكون صعبة على المبتدئين ليكتبوها يدويا. ينصح هؤلاء بتوليد هذا الملف آلياً.

**ملاحظة** بعض أنظمة BIOS قد يعاني مشكلات مع جداول GPT. انظر [http://mjg59.dreamwidth.org/8035.html](http://mjg59.dreamwidth.org/8035.html) and [http://rodsbooks.com/gdisk/bios.html](http://rodsbooks.com/gdisk/bios.html) لمعرفة الحيل والحلول الممكنة.

##### محمل الإقلاع Syslinux

قم بتثبيت الحزمة [syslinux](https://www.archlinux.org/packages/?name=syslinux) ثم استخدم السكربت `syslinux-install_update` _لتثبيت_ الملفات (`-i`) الإقلاع ولجعل البارتشن _نشطا_ بإعداد فلاج (`-a`) و تثبيت كود الإقلاع الخاص ب _MBR_ (`-m`):

**ملاحظة** إذا قمت بتقسيم القرص الصلب بجداول GPT ، ثبت الحزمة [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk) ، وكذلك (`pacman -S gptfdisk`) ﻷنها تحتوي على `sgdisk` التي ستستخدم في ضبط GPT-specific boot flag.

```
# pacman -S syslinux
# syslinux-install_update -i -a -m

```

قم بإعداد الملف `syslinux.cfg` لتحديد القسم الصحيح لبارتشن الجذر. هذه الخطوات أساسية. إذا قمت بتحديد قسم جذر خطأ فلن يقلع نظام آرتش لينكس . قم بتغيير `/dev/sda3` ليعكس اسم قسم الجذر الخاص بك _( إن كنت قد قسمت القرص الصلب خاصتك كما هو موضح سابقا في [هذا المثال](#.D8.A5.D8.B9.D8.AF.D8.A7.D8.AF.D8.A7.D8.AA_.D8.A7.D9.84.D9.82.D8.B1.D8.B5_.D8.A7.D9.84.D8.B5.D9.84.D8.A8) سيكون قسم الجذر لديك هو sda1)_. افعل نفس الشيء لخانة fallback

 `# nano /boot/syslinux/syslinux.cfg` 

```
...
LABEL arch
        ...
        APPEND root=/dev/sda3 ro
        ...
```

لمزيد من المعلومات عن تكوين واستخدام Syslinux انظر [Syslinux](/index.php/Syslinux "Syslinux").

##### GRUB محمل الإقلاع

ثبت الحزمة [grub-bios](https://www.archlinux.org/packages/?name=grub-bios) ثم شغل اﻷمر `grub-install /dev/sda`:

**ملاحظة** `/dev/sda` ذلك يعكس اسم القرص الصلب الذي قمت بتثبيت آرتش لينكس فوقه . لا تضف رقم قسم ( لا تستخدم `sda_X_`).

**ملاحظة** بخصوص اﻷقراص المقسمة بجداول GPT على لوحات أم BIOS تحتاج إلى "[BIOS Boot Partition](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB")".

```
# pacman -S grub-bios
# grub-install --recheck /dev/sda
# cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo

```

في حين أن استخدام ملف `grub.cfg` منشأ يدويا هو قطعا امر جيد . ينصح المبتدئون بتوليد أحد هذه الملفات آليا.

**ملاحظة** للبحث آليا عن نظم التشغيل اﻷخرى الموجودة على حاسوبك ، قم بتثبيت الحزمة [os-prober](https://www.archlinux.org/packages/?name=os-prober) (`pacman -S os-prober`) قبل إجراء اﻷمر التالي :

```
# grub-mkconfig -o /boot/grub/grub.cfg 

```

لمزيد من المعلومات عن إعداد واستخدام جروب انظر [GRUB](/index.php/GRUB "GRUB").

#### خاص باللوحات اﻷم بنظام UEFI

بخصوص إقلاع UEFI ، يحتاج القرص الصلب للتقسيم بجداول GPT ، وقسم لنظام UEFI يكون مهيئا بنظام ملفات FAT32 ( حجمه 512 ميجا أو أكثر ، نوعه `EF00` ) ويجب أن يوجد ويربط على المجلد `/boot/efi`. إذا قمت باتباع هذه الإرشادات منذ البداية تكون بالفعل قد قمت بكل هذا. في حين أن محملات إقلاع [UEFI bootloaders](/index.php/UEFI_Bootloaders "UEFI Bootloaders") اخرى متاحة ، يوصي المطورون باستخدام EFISTUB ، وفيما يلي بعض التعليمات لإعداد EFISTUB و GRUB ( أنت بالطبع قد اخترت أحدهما ).

**ملاحظة** Syslinux لم يدعم بعد UEFI.

##### EFISTUB

تستطيع نواة لينكس أن تعمل بمثابة محمل الإقلاع خاصتها باستخدام EFISTUB . وتلك هي طريقة إقلاع UEFI التي يوصي بها المطورون وهي أسهل بالمقارنة مع `grub-efi-x86_64`. الخطوات التالية تقوم بإعداد rEFInd لتقديم قائمة من أنوية EFISTUB ، وأيضا لمحملات إقلاع UEFI اﻷخرى. يوجد بدائل لمديري إقلاع EFISTUB على الصفحة [UEFI Bootloaders#Booting EFISTUB](/index.php/UEFI_Bootloaders#Booting_EFISTUB "UEFI Bootloaders") . كل من rEFInd و [gummiboot](/index.php/Gummiboot "Gummiboot") يمكن اكتشافهما من قِبَل محمل إقلاع UEFI الخاص بوندوز في حالة الإقلاع المزدوج اﻷنظمة.

1\. قم بربط قسم نظام UEFI على الدليل `/mnt/boot/efi` و بدل الجذر chroot إلى `/mnt`. 2\. [انسخ ملفات kernel و initramfs](/index.php/UEFI_Bootloaders#Setting_up_EFISTUB "UEFI Bootloaders") إلى الدليل `/mnt/boot/efi`:

```
# mkdir -p /boot/efi/EFI/arch/
# cp /boot/vmlinu**z**-linux /boot/efi/EFI/arch/vmlinuz-arch**.efi**
# cp /boot/initramfs-linux.img /boot/efi/EFI/arch/initramfs-arch.img
# cp /boot/initramfs-linux-fallback.img /boot/efi/EFI/arch/initramfs-arch-fallback.img

```

في كل مرة يتم تحديث النواة أو قرص الذاكرة initramfs في الدليل `/boot` ، يحتاجان إلى التحديث في الدليل `/boot/efi/EFI/arch`. ويمكن عمل ذلك آليا [using systemd](/index.php/UEFI_Bootloaders#Systemd "UEFI Bootloaders"). 3\. بحصوص مدير إقلاع rEFInd ، ثبت الحزمتين [refind-efi](https://www.archlinux.org/packages/?name=refind-efi) و [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr):

```
# pacman -S refind-efi efibootmgr

```

4\. ثبت rEFInd على قسم النظام الخاص ب UEFI (ملخص من [UEFI Bootloaders#Using rEFInd](/index.php/UEFI_Bootloaders#Using_rEFInd "UEFI Bootloaders")):

```
# mkdir -p /boot/efi/EFI/refind
# cp /usr/lib/refind/refind_x64.efi /boot/efi/EFI/refind/refind_x64.efi
# cp /usr/lib/refind/config/refind.conf /boot/efi/EFI/refind/refind.conf
# cp -r /usr/share/refind/icons /boot/efi/EFI/refind/icons

```

5\. أنشئ الملف `refind_linux.conf` مع بارمترات النواة لتستخدم من قِبَل rEFInd:

 `# nano /boot/efi/EFI/arch/refind_linux.conf` 

```
"Boot to X"          "root=/dev/sdaX ro rootfstype=ext4 systemd.unit=graphical.target"
"Boot to console"    "root=/dev/sdaX ro rootfstype=ext4 systemd.unit=multi-user.target"
```

**ملاحظة** يتم نسخ `refind_linux.conf` في الدليل `/boot/efi/EFI/arch/` حيث يتم نسخ قرص الذاكرة initramfs والنواة kernel كما في الخطوة رقم 2.

**ملاحظة** في `refind_linux.conf` يشير sdaX إلى نظام ملفات الجذر لديك ، وليس إلى بارتشن الإقلاع، إذا قمت بإنشاءهم منفصلين.

6\. أضف rEFInd إلى قائمة إقلاع UEFI باستخدام [efibootmgr](/index.php/UEFI#efibootmgr "UEFI"). استبدل X و Y وضع مكانهم القرص والقسم الخاص بنظام UEFI . مثلا؛ في `/dev/sdc5` تعتببر X هي "C" و Y هي "5" .

**تحذير :** استخدام `efibootmgr` في أجهزة أبل ماك ربما يحطم المشغل اﻷساسي فيرموير وقد يحتاج إلى إعادة تحميل ال ROM الخاص باللوحة اﻷم، استخدم [mactel-boot](https://aur.archlinux.org/packages/mactel-boot/) أو " خذه حلالا " ضمن نظام أبل OS X.

```
# efibootmgr -c -d /dev/sdX -p Y -w -L "rEFInd" -l '\EFI\refind\refind_x64.efi'

```

**ملاحظة** في بعض اﻷنظمة ربما لا يعمل اﻷمر السابق بشكل صحيح. سينفذ دون ظهور أي خطأ ، ولكن قائمة إقلاع UEFI لن يتم تحديثه بالمدخلة الجديدة . لتحديد لتحديد ما إذا كان الأمر ينفذ على الوجه الصحيح ، شغل اﻷمر `efibootmgr` بدون أي خيارات وانظر إن ظهرت أي مدخلة جديدة في القائمة المعروضة. إذا لم يكن هناك أي مدخلة جديدة حينئذ لن يكون ممكنا دخول rEFInd عند إعادة التشغيل. حيث إن قائمة إقلاع UEFI لم تتغير . في هذه الحال ، بدلا من ذلك عليك أن تدخل صدفة UEFI وتضيف يدويا المدخلة إلى قائمة إقلاع UEFI مع اﻷمر `bcfg` . كما تم شرحه [هنا](/index.php/Unified_Extensible_Firmware_Interface#bcfg "Unified Extensible Firmware Interface").

##### محمل الإقلاع GRUB

**ملاحظة** في حال كان لديك نظام EFI ذي 32-bit ، مثل أبل ماك pre-2008 ، قم بتثبيت `grub-efi-i386` بدلا من `grub-efi-x86_64`.

```
# pacman -S grub-efi-x86_64 efibootmgr
# grub-install --efi-directory=/boot/efi --bootloader-id=arch_grub --recheck
# cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo

```

بعد ذلك، في حين أن استخدام ملف `grub.cfg` منشأ يدويا هو بالقطع أمر جيد ، إلا أنه يوصى المستخدمون الميتدئون بتوليد هذا الملف آليا.

**ملاحظة** للبحث آليا عن نظم التشغيل اﻷخرى الموجودة على حاسوبك ، قم بتثبيت الحزمة [os-prober](https://www.archlinux.org/packages/?name=os-prober) (`pacman -S os-prober`) قبل إجراء اﻷمر التالي :

```
# grub-mkconfig -o /boot/grub/grub.cfg 

```

**ملاحظة :** `grub-install` ينبغي أن ينشئ مدخلة جديدة في قائمة إقلاع UEFI فإن لم يحدث ذلك؛ ، بدلا من ذلك عليك أن تدخل صدفة UEFI وتضيف يدويا المدخلة إلى قائمة إقلاع UEFI مع اﻷمر `bcfg` كما تم شرحه [هنا](/index.php/Unified_Extensible_Firmware_Interface#bcfg "Unified Extensible Firmware Interface").

لمزيد من المعلومات عن إعداد GRUB جروب واستخدامه انظر [GRUB](/index.php/GRUB "GRUB").

### إلغاء ربط أقسام القرص الصلب وإعادة التشغيل

اخرج من بيئة مبدل الجذر chroot :

```
# exit

```

وحيث إن أقسام القرص الصلب مربوطة تحت على الدليل ، `/mnt` سنستخدم اﻷمر التالي لفك الربط :

```
# umount /mnt/{boot,home,}

```

إعادة تشغيل الحاسب:

```
# reboot

```

**تلميحة:** تأكد من فصل إسطوانة التثبيت وإلا فإنك ستقلع من خلالها مجددا.

## ما بعد التثبيت

نظام ارتش لينكس الأساسي خاصتك هو الأن بيئة وظيفية من جنو/لينكس جاهزة للبناء في كل ما ترغبه أو تحتاجه لأغراضك.

### إدارة المستخدمين

أضف أي حسابات للمستخدمين تحتاجه بجانب المستخدم الجذر ، كما تم شرحه في [User management](/index.php/Users_and_groups#User_management "Users and groups"). ليس من الممارسة الجيدة استخدام حساب الجذر للاستخدامات العادية، أو كشفه عن طريق الخادم [SSH](/index.php/SSH "SSH") . وينبغي أن تستخدم حساب الجذر فقط للمهام الإدارية.

### مدير الحزم

بكمان هو مدير حزم آرتش لينكس اختصارا ل **pac**kage **man**ager ، انظر [pacman](/index.php/Pacman "Pacman") و [FAQ#Package Management](/index.php/FAQ#Package_Management "FAQ") للحصول على إجابات بشأن تركيب وتحديث وإدارة الحزم . إن كنت قمت بتثبيت نسخة آرتش لينكس x86_64 ، ربما ترغب في تفعيل مستودع المكتبات المتعددة [enable the [multilib] repository](/index.php/Multilib "Multilib") إن كنت تخطط لاستخدام تطبيقات 32-bit . انظر [Official repositories](/index.php/Official_repositories "Official repositories") لمعرفة تفاصيل عن غرض كل مستودع.

### إدارة الخدمات

تستخدم توزيعة آرتش لينكس [systemd](/index.php/Systemd "Systemd") مثل init ، وهو بمثابة مدير خدمات لنظام لينكس. من أجل الحفاظ على توزيعة آرتش لينكس خاصتك ، تعد فكرة جيدة أن تتعلم ا أساسيات عن ذلك . ويتم التفاعل مع systemd عن طريق الأمر `systemctl` . اقرأ [systemd#استخدامات systemctl الأساسية](/index.php/Systemd#.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85.D8.A7.D8.AA_systemctl_.D8.A7.D9.84.D8.A3.D8.B3.D8.A7.D8.B3.D9.8A.D8.A9 "Systemd") . لمزيد من المعلومات

### الصوت

[ALSA](/index.php/ALSA "ALSA") يعمل عادة خارج الإطار . هو فقط يحتاج إلى إلغاء كتم الصوت . قم بتثبيت الحزمة [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) ( التي تحتوي على `alsamixer`) واتبع [هذه](/index.php/Advanced_Linux_Sound_Architecture#Unmuting_the_channels "Advanced Linux Sound Architecture") التعليمات. ALSA يأتي مضمنا مع النواة وينصح به . فإن لم يعمل ، يعتبر [OSS](/index.php/OSS "OSS") بديلا مجديا عنه . إذا كن لديك احتياجات متقدمة ألق نظرة على [Sound system](/index.php/Sound_system "Sound system") لإلقاء نظرة عامة عن الموضوعات المتنوعة .

### واجهة المستخدم الرسومية **G U I**

#### تثبيت الخادم X

[X Window System](https://en.wikipedia.org/wiki/X_Window_System "wikipedia:X Window System") (الشائع **X11** أو **X**) هو بروتوكول رسومي وشبكي يوفر النوافذ على شاشات العرض النقطية . وهو يوفر مجموعة من الأدوات القياسية وبروتوكول لبناء الواجهات الرسومية للمستخدم (GUIs). لتثبيت الحزم الأساسية لخادم [Xorg](/index.php/Xorg "Xorg") :

```
# pacman -S xorg-server xorg-server-utils xorg-xinit

```

قم بتثبيت [mesa](https://en.wikipedia.org/wiki/Mesa_(computer_graphics) "wikipedia:Mesa (computer graphics)") لدعم 3D :

```
# pacman -S mesa

```

#### تثبيت مشغل الفيديو

**Note:** If you installed Arch as a VirtualBox guest, you don't need to install a video driver. See [Arch Linux guests](/index.php/VirtualBox#Arch_Linux_guests "VirtualBox") for installing and setting up Guest Additions, and jump to the [configuration](#Configure_X) part below.

The Linux kernel includes open-source video drivers and support for hardware accelerated framebuffers. However, userland support is required for OpenGL and 2D acceleration in X11\.

If you don't know which video chipset is available on your machine, run:

```
$ lspci | grep VGA

```

For a complete list of open-source video drivers, search the package database:

```
$ pacman -Ss xf86-video | less

```

The `vesa` driver is a generic mode-setting driver that will work with almost every GPU, but will not provide any 2D or 3D acceleration. If a better driver cannot be found or fails to load, Xorg will fall back to vesa. To install it:

```
# pacman -S xf86-video-vesa

```

In order for video acceleration to work, and often to expose all the modes that the GPU can set, a proper video driver is required:

| Brand | Type | Driver | [Multilib](/index.php/Multilib "Multilib") Package
(for 32-bit applications on Arch x86_64) |  Documentation  |
| ** AMD/ATI ** |  Open source  | [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) | [lib32-ati-dri](https://www.archlinux.org/packages/?name=lib32-ati-dri) | [ATI](/index.php/ATI "ATI") |
| Proprietary | [catalyst-dkms](https://aur.archlinux.org/packages/catalyst-dkms/) | [lib32-catalyst-utils](https://aur.archlinux.org/packages/lib32-catalyst-utils/) | [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst") |
| **Intel** | Open source | [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) | [lib32-intel-dri](https://www.archlinux.org/packages/?name=lib32-intel-dri) | [Intel graphics](/index.php/Intel_graphics "Intel graphics") |
| **Nvidia** | Open source | [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) | [lib32-nouveau-dri](https://www.archlinux.org/packages/?name=lib32-nouveau-dri) | [Nouveau](/index.php/Nouveau "Nouveau") |
| [xf86-video-nv](https://www.archlinux.org/packages/?name=xf86-video-nv) | – | (legacy driver) |
| Proprietary | [nvidia](https://www.archlinux.org/packages/?name=nvidia) | [lib32-nvidia-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-libgl) | [NVIDIA](/index.php/NVIDIA "NVIDIA") |
| [nvidia-304xx](https://www.archlinux.org/packages/?name=nvidia-304xx) | [lib32-nvidia-304xx-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-304xx-utils) |

#### تثبيت مشغلات الإدخال

Udev should be capable of detecting your hardware without problems. The `evdev` driver ([xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev)) is the modern hot-plugging input driver for almost all devices, so in most cases, installing input drivers is not needed. At this point, `evdev` has already been installed as a dependency of the [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) package.

Laptop users (or users with a tactile screen) will need the [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) package for the touchpad/touchscreen to work:

```
# pacman -S xf86-input-synaptics

```

For instructions on fine tuning or troubleshooting touchpad issues, see the [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") article.

#### إعداد الخادم الرسومي X

**Warning:** Proprietary drivers usually require a reboot after installation. See [NVIDIA](/index.php/NVIDIA "NVIDIA") or [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst") for details.

Xorg features auto-detection and therefore can function without an `xorg.conf`. If you still wish to manually configure X Server, please see the [Xorg](/index.php/Xorg "Xorg") wiki page.

Here you may set a [keyboard layout](/index.php/Xorg#Setting_keyboard_layout_with_hot-plugging "Xorg") if you do not use a standard [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg") keyboard.

**Note:** The `XkbLayout` key may differ from the keymap code you used with the `loadkeys` command. A list of many keyboard layouts and variants can be found in `/usr/share/X11/xkb/rules/base.lst` (after the line beginning with `! layout`). For instance, the layout `gb` corresponds to "English (UK)", whereas for the console it was `loadkeys uk`.

#### اختبار الخادم الرسومي X

**Tip:** These steps are optional. Test only if you're installing Arch Linux for the first time, or if you're installing on new and unfamiliar hardware.

**Note:** If your input devices are not working during this test, install the needed driver from the [xorg-drivers](https://www.archlinux.org/groups/x86_64/xorg-drivers/) group, and try again. For a complete list of available input drivers, invoke a pacman search (press `Q` to exit):

```
$ pacman -Ss xf86-input | less

```

You only need [xf86-input-keyboard](https://www.archlinux.org/packages/?name=xf86-input-keyboard) or [xf86-input-mouse](https://www.archlinux.org/packages/?name=xf86-input-mouse) if you plan on disabling [hot-plugging](https://en.wikipedia.org/wiki/Hot-plugging "wikipedia:Hot-plugging"), otherwise, `evdev` will act as the input driver (recommended).

Install the default environment:

```
# pacman -S xorg-twm xorg-xclock xterm

```

If Xorg was installed before creating the non-root user, there will be a template `.xinitrc` file in your home directory that needs to be either deleted or commented out. Simply deleting it will cause **X** to run with the default environment installed above.

```
$ rm ~/.xinitrc

```

**Note:** X must always be run on the same tty where the login occurred, to preserve the logind session. This is handled by the default `/etc/X11/xinit/xserverrc`.

To start the (test) Xorg session, run:

```
$ startx

```

A few movable windows should show up, and your mouse should work. Once you are satisfied that **X** installation was a success, you may exit out of **X** by issuing the `exit` command into the prompts until you return to the console.

```
$ exit

```

If the screen goes black, you may still attempt to switch to a different virtual console (e.g. `Ctrl+Alt+F2`), and blindly log in as root. You can do this by typing "root" (press `Enter` after typing it) and entering the root password (again, press `Enter` after typing it).

You may also attempt to kill the **X** server with:

```
# pkill X

```

If this does not work, reboot blindly with:

```
# reboot

```

##### إصلاح المشكلات

If a problem occurs, look for errors in `Xorg.0.log`. Be on the lookout for any lines beginning with `(EE)` which represent errors, and also `(WW)` which are warnings that could indicate other issues.

```
$ grep EE /var/log/Xorg.0.log

```

If you are still having trouble after consulting the [Xorg](/index.php/Xorg "Xorg") article and need assistance via the Arch Linux forums or the IRC channel, be sure to install and use [wgetpaste](https://www.archlinux.org/packages/?name=wgetpaste) by providing the links from:

```
# pacman -S wgetpaste
$ wgetpaste ~/.xinitrc
$ wgetpaste /etc/X11/xorg.conf
$ wgetpaste /var/log/Xorg.0.log

```

**Note:** Please provide all pertinent information (hardware, driver information, etc) when asking for assistance.

#### الخطوط

You may wish to install a set of TrueType fonts, as only unscalable bitmap fonts are included by default. DejaVu is a set of high quality, general-purpose fonts with good [Unicode](https://en.wikipedia.org/wiki/Unicode "wikipedia:Unicode") coverage:

```
# pacman -S ttf-dejavu

```

Refer to [Font configuration](/index.php/Font_configuration "Font configuration") for how to configure font rendering and [Fonts](/index.php/Fonts "Fonts") for font suggestions and installation instructions.

#### اختيار وتثبيت الوجهة الرسومية

The X Window System provides the basic framework for building a graphical user interface (GUI).

**Note:** Choosing your DE or WM is a very subjective and personal decision. Choose the best environment for _your_ needs. You can also build your own DE with just a WM and the applications of your choice.

*   [Window Managers](/index.php/Window_manager "Window manager") (WM) control the placement and appearance of application windows in conjunction with the X Window System.

*   [Desktop Environments](/index.php/Desktop_environment "Desktop environment") (DE) work atop and in conjunction with X, to provide a completely functional and dynamic GUI. A DE typically provides a window manager, icons, applets, windows, toolbars, folders, wallpapers, a suite of applications and abilities like drag and drop.

Instead of starting X manually with `startx` from [xorg-xinit](https://www.archlinux.org/packages/?name=xorg-xinit), see [Display manager](/index.php/Display_manager "Display manager") for instructions on using a display manager, or see [Start X at login](/index.php/Start_X_at_login "Start X at login") for using an existing virtual terminal as an equivalent to a display manager.

## ملحق

للحصول على قائمة من التطبيقات التي قد تكون ذات فائدة، انظر [List of applications](/index.php/List_of_applications "List of applications").

انظر [General recommendations](/index.php/General_recommendations "General recommendations") للدروس التعليمية عما بعد التثبيت مثل إعداد لوحة اللمس touchpad أو تصيير الخطوط.