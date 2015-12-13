# pacman (العربية)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

يعد [مدير الحزم](https://en.wikipedia.org/wiki/Package_management_system "wikipedia:Package management system") **[pacman](https://www.archlinux.org/pacman/)** واحد من الخصائص المميزة لـ Arch Linux. فهو يجمع بين حزم ذات بنية (binary) بسيطة و [نضام بناء](/index.php/Arch_Build_System "Arch Build System") سهل الإستعمال . الهدف من إستعمال pacman هو إدارة الحزم وبكل سهولة ممكنة , سواء أكان مصدر هذه الحزم [المخازن الرسمية لآرش](/index.php/Official_repositories "Official repositories") أو بناء خاص بالمستخدمين .

يبقي pacman النضام محدثاً و ذلك بمزامنة لائحة الحزم مع الخادم الرئيسي , هذا النمودج خادم/عميل يسمح لك ايضاً بـ تحميل/تثبيت الحزم بأمر بسيط , مع إستكمال جميع الإعتماديات المطلوبة.

كتب pacman بلغة البرمجة C ويستعمل حزم ذات تنسيق `.pkg.tar.xz`.

**تلميحة :** الحزمة الرسمية من [pacman](https://www.archlinux.org/packages/?name=pacman) تضم أيضاً مجموعة أدوات مساعدة , من قبيل **makepkg**, **pactree**, **vercmp** والمزيد . نفذ `pacman -Ql pacman | grep bin` للحصول على الائحة كاملة.

## Contents

*   [1 التهيئة](#.D8.A7.D9.84.D8.AA.D9.87.D9.8A.D8.A6.D8.A9)
    *   [1.1 الخيارات العامة](#.D8.A7.D9.84.D8.AE.D9.8A.D8.A7.D8.B1.D8.A7.D8.AA_.D8.A7.D9.84.D8.B9.D8.A7.D9.85.D8.A9)
        *   [1.1.1 إستثناء حزمة من التحديث](#.D8.A5.D8.B3.D8.AA.D8.AB.D9.86.D8.A7.D8.A1_.D8.AD.D8.B2.D9.85.D8.A9_.D9.85.D9.86_.D8.A7.D9.84.D8.AA.D8.AD.D8.AF.D9.8A.D8.AB)
        *   [1.1.2 إستثناء مجموعة حزمية من التحديث](#.D8.A5.D8.B3.D8.AA.D8.AB.D9.86.D8.A7.D8.A1_.D9.85.D8.AC.D9.85.D9.88.D8.B9.D8.A9_.D8.AD.D8.B2.D9.85.D9.8A.D8.A9_.D9.85.D9.86_.D8.A7.D9.84.D8.AA.D8.AD.D8.AF.D9.8A.D8.AB)
        *   [1.1.3 إستثناء ملفات من أن تثبت على النضام](#.D8.A5.D8.B3.D8.AA.D8.AB.D9.86.D8.A7.D8.A1_.D9.85.D9.84.D9.81.D8.A7.D8.AA_.D9.85.D9.86_.D8.A3.D9.86_.D8.AA.D8.AB.D8.A8.D8.AA_.D8.B9.D9.84.D9.89_.D8.A7.D9.84.D9.86.D8.B6.D8.A7.D9.85)
    *   [1.2 المخازن](#.D8.A7.D9.84.D9.85.D8.AE.D8.A7.D8.B2.D9.86)
    *   [1.3 أمان الحزمة](#.D8.A3.D9.85.D8.A7.D9.86_.D8.A7.D9.84.D8.AD.D8.B2.D9.85.D8.A9)
*   [2 الإستعمال](#.D8.A7.D9.84.D8.A5.D8.B3.D8.AA.D8.B9.D9.85.D8.A7.D9.84)
    *   [2.1 تثبيت الحزم](#.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_.D8.A7.D9.84.D8.AD.D8.B2.D9.85)
        *   [2.1.1 تثبيت حزمة محددة](#.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_.D8.AD.D8.B2.D9.85.D8.A9_.D9.85.D8.AD.D8.AF.D8.AF.D8.A9)
        *   [2.1.2 تثبيت مجموعة حزمية](#.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_.D9.85.D8.AC.D9.85.D9.88.D8.B9.D8.A9_.D8.AD.D8.B2.D9.85.D9.8A.D8.A9)
    *   [2.2 حذف الحزم](#.D8.AD.D8.B0.D9.81_.D8.A7.D9.84.D8.AD.D8.B2.D9.85)
    *   [2.3 تحديث الحزم](#.D8.AA.D8.AD.D8.AF.D9.8A.D8.AB_.D8.A7.D9.84.D8.AD.D8.B2.D9.85)
    *   [2.4 Querying package databases](#Querying_package_databases)
    *   [2.5 أوامر إضافية](#.D8.A3.D9.88.D8.A7.D9.85.D8.B1_.D8.A5.D8.B6.D8.A7.D9.81.D9.8A.D8.A9)
    *   [2.6 الترقيات الجزئية غير معتمدة](#.D8.A7.D9.84.D8.AA.D8.B1.D9.82.D9.8A.D8.A7.D8.AA_.D8.A7.D9.84.D8.AC.D8.B2.D8.A6.D9.8A.D8.A9_.D8.BA.D9.8A.D8.B1_.D9.85.D8.B9.D8.AA.D9.85.D8.AF.D8.A9)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 An update to package XYZ broke my system!](#An_update_to_package_XYZ_broke_my_system.21)
    *   [3.2 I know an update to package ABC was released, but pacman says my system is up to date!](#I_know_an_update_to_package_ABC_was_released.2C_but_pacman_says_my_system_is_up_to_date.21)
    *   [3.3 I get an error when updating: "file exists in filesystem"!](#I_get_an_error_when_updating:_.22file_exists_in_filesystem.22.21)
    *   [3.4 I get an error when installing a package: "not found in sync db"](#I_get_an_error_when_installing_a_package:_.22not_found_in_sync_db.22)
    *   [3.5 Pacman is repeatedly upgrading the same package!](#Pacman_is_repeatedly_upgrading_the_same_package.21)
    *   [3.6 Pacman crashes during an upgrade!](#Pacman_crashes_during_an_upgrade.21)
    *   [3.7 I installed software using "make install"; these files do not belong to any package!](#I_installed_software_using_.22make_install.22.3B_these_files_do_not_belong_to_any_package.21)
    *   [3.8 I need a package with a specific file. How do I know what provides it?](#I_need_a_package_with_a_specific_file._How_do_I_know_what_provides_it.3F)
    *   [3.9 Pacman is completely broken! How do I reinstall it?](#Pacman_is_completely_broken.21_How_do_I_reinstall_it.3F)
    *   [3.10 After updating my system, I get a "unable to find root device" error after rebooting and my system will no longer boot](#After_updating_my_system.2C_I_get_a_.22unable_to_find_root_device.22_error_after_rebooting_and_my_system_will_no_longer_boot)
    *   [3.11 Signature from "User <email@gmail.com>" is unknown trust, installation failed](#Signature_from_.22User_.3Cemail.40gmail.com.3E.22_is_unknown_trust.2C_installation_failed)
    *   [3.12 I keep getting](#I_keep_getting)
    *   [3.13 I keep getting a "failed to commit transaction (invalid or corrupted package)" error](#I_keep_getting_a_.22failed_to_commit_transaction_.28invalid_or_corrupted_package.29.22_error)
    *   [3.14 I get an error every time I use pacman saying 'warning: current locale is invalid; using default "C" locale'. What do I do?](#I_get_an_error_every_time_I_use_pacman_saying_.27warning:_current_locale_is_invalid.3B_using_default_.22C.22_locale.27._What_do_I_do.3F)
    *   [3.15 How can I get Pacman to honor my proxy settings?](#How_can_I_get_Pacman_to_honor_my_proxy_settings.3F)
*   [4 See also](#See_also)

## التهيئة

إعدادات pacman تقع بالملف `/etc/pacman.conf`. هذا الملف حيث يقوم المستخدم بإعداد البرنامج لليشتغل على النحو المطلوب , للحصول على معلومات تفصيلية عن ملف الإعدادات يمكنك الإطلاع على [man pacman.conf](https://www.archlinux.org/pacman/pacman.conf.5.html).

### الخيارات العامة

الخيارات العامة ستجدها بقسم `[options]`, إقرأ صفحة man أو أنظر لملف `pacman.conf` الإفتراضي لمزيد من المعلومات عن ما يمكن القيام به.

#### إستثناء حزمة من التحديث

لإستثناء حزمة من التحديث , بإمكانك تحديدها كالتالي :

```
IgnorePkg=linux

```

للحزم المتعددة إستعمل مسافة للفصل بين أسماء الحزم , أو أضف أسطر IgnorePkg إضافية.

#### إستثناء مجموعة حزمية من التحديث

كما في حالة الحزم , إستثناء المجموعة بأكملها شيء ممكن :

```
IgnoreGroup=gnome

```

#### إستثناء ملفات من أن تثبت على النضام

لتخطي دائما تثبيت دلائل معينة يتم بإدراجها تحت قائمة `NoExtract`. كمثال , للتجاهل تثبيت وحدة [systemd](/index.php/Systemd "Systemd") إستعمل التالي :

```
NoExtract=usr/lib/systemd/system/*

```

### المخازن

هذا القسم يحدد [المخازن](/index.php/Official_repositories "Official repositories") التي يتم إستعمالها , حسب ما هو مشار إليه في `/etc/pacman.conf`. يمكن إدراجها بشكل مباشر هنا أو ضمها من ملف أخر (مثلاً `/etc/pacman.d/mirrorlist`), مما يجعل من الضروري الحفاظ على لائحة واحدة فقط. انظر [هنا](/index.php/Mirrors "Mirrors") للإطلاع على طريقة إعداد المرايا.

 `/etc/pacman.conf` 

```
#[testing]
#SigLevel = PackageRequired
#Include = /etc/pacman.d/mirrorlist

[core]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

[extra]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

#[community-testing]
#SigLevel = PackageRequired
#Include = /etc/pacman.d/mirrorlist

[community]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

# If you want to run 32 bit applications on your x86_64 system,
# enable the multilib repositories as required here.

#[multilib-testing]
#SigLevel = PackageRequired
#Include = /etc/pacman.d/mirrorlist

#[multilib]
#SigLevel = PackageRequired
#Include = /etc/pacman.d/mirrorlist

# An example of a custom package repository.  See the pacman manpage for
# tips on creating your own repositories.
#[custom]
#SigLevel = Optional TrustAll
#Server = file:///home/custompkgs
```

**تحذير:** يجب توخي الحذر عند إستعمال مخزن [testing]. فهو في طور التحديث والتطوير مما قد يتسبب في عطب بعض الحزم. الأشخاص المستعملون للمخازن التجريبية مدعون للتسجيل في [arch-dev-public mailing list](https://mailman.archlinux.org/mailman/listinfo/arch-dev-public) للتزويد بالمعلومات.

### أمان الحزمة

الإصدرا 4 من pacman يدعم الحزم الموقعة , والتي تضيف طبقة إضافية من الحماية على الحزم , الإعدادت الإفتراضية, `SigLevel = Required DatabaseOptional`, تفعل التحقق من التوقيع لجميع الحزم على المستوى العالي, يمكن تجاوز ذلك بالنسبة لكل مستودع من خلال أسطر `SigLevel`كما هو موضح أعلاه. للحصول على المزيد من التفاصيل حول توقيع حزمة والتحقق من صحة التوقيع، ألقي نظرة على [pacman-key](/index.php/Pacman-key "Pacman-key").

## الإستعمال

ما يلي هو مجرد عينة صغيرة من العمليات التي يمكن أن يقوم بها pacman. للمزيد من الأمثلة ، راجع [man pacman](https://www.archlinux.org/pacman/pacman.8.html).

### تثبيت الحزم

#### تثبيت حزمة محددة

للتثبيت حزمة أو عدة حزم (بما في ذلك الإعتماديات) نفذ الإمر التالي :

```
# pacman -S _package_name1_ _package_name2_ ...

```

أحياناً هناك إصدارات مختلفة لحزمة على مخازن مختلفة , على سبيل المثال , [extra] و [testing]. للتثبيت الإصدار السابق , يجب ذكر المخزن أولاً :

```
# pacman -S extra/_package_name_

```

#### تثبيت مجموعة حزمية

بعض الحزم تنتمي لمجموعة والتي بالإمكان تثبيتها في نفس الوقت . مثالا نفذ الأمر :

```
# pacman -S gnome

```

سيتم توجيهك إلى اختيار بعض حزم المجموعة [gnome](https://www.archlinux.org/groups/x86_64/gnome/) التي ترغب في تثبيتها. احيانا ما تحتوى إحدى المجموعات عل عدد كبير من الحزم ، ويوجد القليل من الحزم التي ،تريد تثبيتها أو لا تريد فبدلا من إدخال كل الأرقام ما عدا تلك التي لا تريدها من الملائم أن تحدد أو تستبعد الحزم أو نطاقا من الحزم بصيغة الأمر التالي:

```
Enter a selection (default=all): 1-10 15

```

والذي سيحدد الحزم من 1 إلى 10 و 15 لتثبيتها، أو :

```
Enter a selection (default=all): ^5-8 ^2

```

وذلك سيحدد جميع الحزم ما عدا من 5 إلى 8 و 2 لتثبيتها. لرؤية الحزم التي تنتمي للمجموعة gnome نفذ الأمر التالي:

```
# pacman -Sg gnome

```

أيضا، قم بزيارة [https://www.archlinux.org/groups/](https://www.archlinux.org/groups/) لرؤية ما هي مجموعات الحزم المتاحة.

**ملاحظة :** إذا كانت حزمة في القائمة مثبتة بالفعل على النظام فسيعاد تنصيبها حتى ولو كانت أحدث نسخة . هذا السلوك يمكن تجاوزه بالخيار `needed--`.

**تحذير :** عند تنصيب الحزم **لا تقم** بعمل تحديث لقائمة الحزم بدون [تحديث](#.D8.AA.D8.AD.D8.AF.D9.8A.D8.AB_.D8.A7.D9.84.D8.AD.D8.B2.D9.85) النظام مثلا استخدم الأمر

```
pacman -Sy _package_name_

```

وذلك قد يؤدي إلى مشكلة في التبعيات . انظر [#الترقيات الجزئية غير معتمدة](#.D8.A7.D9.84.D8.AA.D8.B1.D9.82.D9.8A.D8.A7.D8.AA_.D8.A7.D9.84.D8.AC.D8.B2.D8.A6.D9.8A.D8.A9_.D8.BA.D9.8A.D8.B1_.D9.85.D8.B9.D8.AA.D9.85.D8.AF.D8.A9) و [https://bbs.archlinux.org/viewtopic.php](https://bbs.archlinux.org/viewtopic.php)? id=89328.

### حذف الحزم

لحذف حزمة مفردة، مع إبقاء جميع تبعياتها المثبتة:

```
# pacman -R _package_name_

```

لحذف حزمة وجميع تبعياتها غير المطلوبة لتثبيت أية حزمة أخرى :

```
# pacman -Rs _package_name_

```

**تحذير:** هذه العملية تكرارية ويجب استخدامها بحرص بالغ حيث إنها قد تحذف العديد من الحزم المحتمل الاحتياج إليها. من المحتمل

```
# pacman -Rsc _package_name_

```

لحذف حزمة مطلوبة لحزمة أخرى دون حذف للحزمة التابعة:

```
# pacman -Rdd _package_name_

```

يقوم بكمان بحفظ ملفات الإعداد المهمة عند حذف تطبيقات معينة ويقوم إعطائهاتسمية مذيلة بالامتداد `.pacsave`. لتجنب إنشاء نسخة احتياطية لهذه الملفات استخدم الخيار `-n`:

```
# pacman -Rn _package_name_

```

**ملاحظة :** بكمان لن يحذف الإعدادات التي تنشؤها البرامج بنفسها ( مثلا "dotfiles" في مجلد المنزل ) .

### تحديث الحزم

بأمر واحد فقط pacman قادر على تحديث كل الحزم بالنضام . عملية تستغرق بعض الوقت حسب حالة تحديث النضام (up-to date). يقوم هذا الأمر بمزامنة قواعد بيانات المخازن و تحديث حزم النضام (ما عدا الحزم 'المحلية' الغير متوفرة بالخازن):

```
# pacman -Syu

```

**تحذير:** بدلا من التحديث المباشر فور توفر التحديثات , على المستخدم أن يعي ويتعرف على طبيعة Arch و الإصدار المتدحرج الذي تنهجه , فهذا التحديث قد تكون له تبعات غير متوقعة .على سبيل المثال , ليس من الحكمة تحديث النضام إذا كان الشخص على وشك تقديم عرض مهم , فمن الأحسن التحديث في وقت الفراغ حتى يسهل التعامل مع أي مشكلة قد تحدث.

مدير الحزم pacman أداة قوية , لكن لا تنتظر منه أن يتعامل مه جل الحالات , إذا كان الأمر مربكاً بالنسبة لك راجع [The Arch Way](/index.php/The_Arch_Way "The Arch Way"), على المستخدم أن يكون يقضاً وأن يتحمل مسؤولية صيانة نضامه الخاص. **عند عملية التحديث على المستخدم أن يقرأ وينتبه لكل الرسائل الصادرة من pacman وأن يتحلى بحس سليم.** إذا إستلزم تحديث ملف إعدادت معدل لحزمة ذات إصدار جديد , فملف `.pacnew` يتم إتشاؤه لتجنب الكتابة فوق الإعدادات المعدلة من طرف المستخدم. سيقوم pacman يتنبيه المستخدم لدمجهم, هذه الملفات تتطلب التدخل اليدوي من قبل المستخدم من الجيد التعود على مراجعتها بعد كل عملية ترقية أو حذف للحزمة. للمزيد راجع [Pacnew و Pacsave ملفات](/index.php?title=Pacnew_%D9%88_Pacsave_%D9%85%D9%84%D9%81%D8%A7%D8%AA&action=edit&redlink=1 "Pacnew و Pacsave ملفات (page does not exist)").

**Tip:** تذكر أن مخرجات pacman تسجل بالملف `/var/log/pacman.log`.

من المحبب زيارة [Arch Linux home page](https://www.archlinux.org/) قبل التحديث, للتحقق من أخر الأخبار (أو سجل في خدمة Rss), عندما يتطلب التحديث تدخلاً من المستخدم خارج عن المألوف (أكثر من ما يمكن تدبره بإتباع إرشادات pacmac), فسوف يتم إنزال خبر حول الموضوع.

إذا إستعصى حل المشكل المصادف بإتباع هذه التعليمات , تاند من البحث بالمنتدى , فمن الشائع أن يصادف آخرون نفس المشكل وأن يكون قد فتحوا بالفعل موضوع حوله وحول طريقة حله .

### Querying package databases

يستعلم pacman من قاعدة بيانات الحزم المحلية بإستعمال `-Q` flag; أنظر:

```
$ pacman -Q --help

```

و الإستعلام من قواعد بيانات المزامنة `-S` flag; أنظر:

```
$ pacman -S --help

```

بمقدور pacman البحث عن الحزم بقاعدة البيانات , بحثاً عن الإسم ووصف الحزمة:

```
$ pacman -Ss _string1_ _string2_ ...

```

للبحث عن الحزم التي سبق تثبيتها:

```
$ pacman -Qs _string1_ _string2_ ...

```

لعرض معلومات حول حزمة ما:

```
$ pacman -Si _package_name_

```

بالنسبة للحزم المثبتة محلياً:

```
$ pacman -Qi _package_name_

```

تمرير إثنان من `-i` flags سيظهر قائمة بإسماء ملفات النسخ الإحتياطية وحالة التعديل خاصتها:

```
$ pacman -Qii _package_name_

```

لسرد قائمة الملفات المثبة من قبل الحزمة:

```
$ pacman -Ql _package_name_

```

بالنسبة للحزم الغير مثبتة, إستعمل [pkgfile](/index.php/Pkgfile "Pkgfile").

One can also query the database to know which package a file in the file system belongs to:

```
$ pacman -Qo _/path/to/file_name_

```

لسرد الحزم الغير مطلوبة كإعتمادية (يثيمة):

```
$ pacman -Qdt

```

لسرد شجرة إعتمادبات الحزمة:

```
$ pactree _package_name_

```

لسرد كل الحزم التي تعتمد على حزمة _متبثة_, إستعمل `whoneeds` من [pkgtools](/index.php/Pkgtools "Pkgtools"):

```
$ whoneeds _package_name_

```

### أوامر إضافية

لتحديث النضام وتثبيت قائمة الحزم (سطر واحد):

```
# pacman -Syu _package_name1_ _package_name2_ ...

```

تحميل الحزمة بدون تنصيبها:

```
# pacman -Sw _package_name_

```

تثبيت حزمة 'محلية' غير موجودة بالمخزن (مثلاً. مصدر الحزمة من [AUR](/index.php/Arch_User_Repository "Arch User Repository")):

```
# pacman -U /path/to/package/package_name-version.pkg.tar.xz

```

**تلميحة:** لإبقاء نسخة من الحزم المحلية في cache الخاص بـ pacman, إستعمل:

```
# pacman -U file://path/to/package/package_name-version.pkg.tar.xz

```

تثبيت حزمة 'عن بعد' (ليس من المخزن المصرح به في ملف إعادات pacman):

```
# pacman -U http://www.example.com/repo/example.pkg.tar.xz

```

تنظيف cache الحزم من الحزم الغير مثبتة حالياً (`/var/cache/pacman/pkg`):

**تحذير:** Only do this if certain that the installed packages are stable and that a [downgrade](/index.php/Downgrading_packages "Downgrading packages") will not be necessary, since it will remove all of the old versions from the cache folder, leaving behind only the versions of the packages that are currently installed. Having older versions of packages comes in handy in case a future upgrade causes breakage.

```
# pacman -Sc

```

Clean the entire package cache:

**تحذير:** This clears out the entire package cache. Doing this is considered a bad practice; it prevents the ability to downgrade something directly from the cache folder. Users will be forced to have to use an alternative source of deprecated packages such as the [Arch Rollback Machine](/index.php/Downgrading_packages#ARM "Downgrading packages").

```
# pacman -Scc

```

**تلميحة:** As an alternative to both the `-Sc` and `-Scc` switches, consider using `paccache` from [pacman](https://www.archlinux.org/packages/?name=pacman). This offers more control over what and how many packages are deleted. Run `paccache -h` for instructions.

### الترقيات الجزئية غير معتمدة

Arch Linux is a rolling release, and new [library](https://en.wikipedia.org/wiki/Library_(computing) "wikipedia:Library (computing)") versions will be pushed to the repositories. The developers and Trusted Users will rebuild all the packages in the repositories that need to be rebuilt against the libraries. If the system has locally installed packages (such as [AUR](/index.php/Arch_User_Repository "Arch User Repository") packages), users will need to rebuild them when their dependencies receive a [soname](https://en.wikipedia.org/wiki/soname "wikipedia:soname") bump.

This means that partial upgrades are **not supported**. Do not use `pacman -Sy package` or any equivalent such as `pacman -Sy` and then `pacman -S package`. Always upgrade before installing a package -- particularly if pacman has refreshed the sync repositories. Be very careful when using `IgnorePkg` and `IgnoreGroup` for the same reason.

If a partial upgrade scenario has been created, and binaries are broken because they cannot find the libraries they are linked against, **do not "fix" the problem simply by symlinking**. Libraries receive [soname](https://en.wikipedia.org/wiki/soname "wikipedia:soname") bumps when they are **not backwards compatible**. A simple `pacman -Syu` to a properly synced mirror will fix the problem as long as pacman is not broken.

## Troubleshooting

### An update to package XYZ broke my system!

Arch Linux is a rolling-release cutting-edge distribution. Package updates are available as soon as they are deemed stable enough for general use. However, updates sometimes require user intervention: configuration files may need to be updated, optional dependencies may change, etc.

The most important tip to remember is to not "blindly" update Arch systems. Always read the list of packages to be updated. Note whether "critical" packages are going to be updated ([linux](https://www.archlinux.org/packages/?name=linux), [xorg-server](https://www.archlinux.org/packages/?name=xorg-server), and so on). If so, it is usually a good idea to check for any news at [https://www.archlinux.org/](https://www.archlinux.org/) and scan recent forum posts to see if people are experiencing problems as a result of an update.

If a package update is expected/known to cause problems, packagers will ensure that pacman displays an appropriate message when the package is updated. If experiencing trouble after an update, double-check pacman's output by looking at the log (`/var/log/pacman.log`).

At this point, **only after ensuring there is no information available through pacman, there is no relative news on [https://www.archlinux.org/](https://www.archlinux.org/), and there are no forum posts regarding the update**, consider seeking help on the forum, over [IRC](/index.php/IRC_Channel "IRC Channel"), or [downgrading the offending package](/index.php/Downgrading_packages "Downgrading packages").

### I know an update to package ABC was released, but pacman says my system is up to date!

Pacman mirrors are not synced immediately. It may take over 24 hours before an update is available to you. The only options are be patient or use another mirror. [MirrorStatus](https://www.archlinux.org/mirrors/status/) can help you identify an up-to-date mirror.

### I get an error when updating: "file exists in filesystem"!

ASIDE: _Taken from [https://bbs.archlinux.org/viewtopic.php?id=56373](https://bbs.archlinux.org/viewtopic.php?id=56373) by Misfit138._

```
error: could not prepare transaction
error: failed to commit transaction (conflicting files)
package: /path/to/file exists in filesystem
Errors occurred, no packages were upgraded.

```

Why this is happening: pacman has detected a file conflict, and by design, will not overwrite files for you. This is a design feature, not a flaw.

The problem is usually trivial to solve. A safe way is to first check if another package owns the file (`pacman -Qo /path/to/file`). If the file is owned by another package, [file a bug report](/index.php/Reporting_bug_guidelines "Reporting bug guidelines"). If the file is not owned by another package, rename the file which 'exists in filesystem' and re-issue the update command. If all goes well, the file may then be removed.

If you had installed a program manually without using pacman or a frontend, you have to remove it and all its files and reinstall properly using pacman.

Every installed package provides `/var/lib/pacman/local/$package-$version/files` file that contains metadata about this package. If this file gets corrupted - is empty or missing - it results in "file exists in filesystem" errors when trying to update the package. Such an error usually concerns only one package and instead of manually renaming and later removing all the files that belong to the package in question, you can run `pacman -S --force $package` to force pacman to overwrite these files.

Do **not** run `pacman -Syu --force`.

### I get an error when installing a package: "not found in sync db"

Firstly, ensure the package actually exists (and watch out for typos!). If certain the package exists, your package list may be out-of-date or your repositories may be incorrectly configured. Try running `pacman -Syy` to force a refresh of all package lists.

### Pacman is repeatedly upgrading the same package!

This is due to duplicate entries in `/var/lib/pacman/local/`, such as two `linux` instances. `pacman -Qi` outputs the correct version, but `pacman -Qu` recognizes the old version and therefore will attempt to upgrade.

Solution: delete the offending entry in `/var/lib/pacman/local/`.

**ملاحظة:** Pacman version 3.4 should display an error in case of duplicate entries, which should make this note obsolete.

### Pacman crashes during an upgrade!

In the case that pacman crashes with a "database write" error whilst removing packages, and reinstalling or upgrading packages fails:

1.  Boot using the Arch install media.
2.  Mount your root filesystem.
3.  Update the pacman database via `pacman -Syy`.
4.  Reinstall the broken package via `pacman -r /path/to/root -S package`.

### I installed software using "make install"; these files do not belong to any package!

If receiving a "conflicting files" error, note that pacman will overwrite manually-installed software if supplied with the `--force` switch (`pacman -S --force`). See [Pacman tips#Identify files not owned by any package](/index.php/Pacman_tips#Identify_files_not_owned_by_any_package "Pacman tips") for a script that searches the file system for _disowned_ files.

**تحذير:** Take care when using the `--force` switch because it can cause major problems if used improperly.

### I need a package with a specific file. How do I know what provides it?

Install [pkgfile](/index.php/Pkgfile "Pkgfile") which uses a separate database with all files and their associated packages.

### Pacman is completely broken! How do I reinstall it?

In the case that pacman is broken beyond repair, manually download the necessary packages ([openssl](https://www.archlinux.org/packages/?name=openssl), [libarchive](https://www.archlinux.org/packages/?name=libarchive), and [pacman](https://www.archlinux.org/packages/?name=pacman)) and extract them to root. The pacman binary will be restored along with its default configuration file. Afterwards, reinstall these packages with pacman to maintain package database integrity. Additional information and an example (outdated) script that automates the process is available in [this](https://bbs.archlinux.org/viewtopic.php?id=95007) forum post.

### After updating my system, I get a "unable to find root device" error after rebooting and my system will no longer boot

Most likely your initramfs got broken during a kernel update (improper use of pacman's `--force` option can be a cause). You have two options:

**1.** Try the _Fallback_ entry.

**Tip:** In case you removed this entry for whatever reason, you can always press the `Tab` key when the bootloader menu shows up (for Syslinux) or `e` (for GRUB), rename it `initramfs-linux-fallback.img` and press `Enter` or `b` (depending on your bootloader) to boot with the new parameters.

Once the system starts, run this command (for the stock [linux](https://www.archlinux.org/packages/?name=linux) kernel) either from the console or from a terminal to rebuild the initramfs image:

 `# mkinitcpio -p linux` 

**2.** If that does not work, from a 2012 Arch release (CD/DVD or USB stick), run:

**ملاحظة:** If you do not have a 2012 release or if you only have some other "live" Linux distribution laying around, you can [chroot](/index.php/Chroot "Chroot") using the old fashion way. Obviously, there will be more typing than simply running the `arch-chroot` script.

```
# mount /dev/sdxY /mnt         #Your root partition.
# mount /dev/sdxZ /mnt/boot    #If you use a separate /boot partition.
# arch-chroot /mnt
# pacman -Syu mkinitcpio systemd linux
```

Reinstalling the kernel (the [linux](https://www.archlinux.org/packages/?name=linux) package) will automatically re-generate the initramfs image with `mkinitcpio -p linux`. There is no need to do this separately.

Afterwards, it is recommended that you run `exit`, `umount /mnt/{boot,}` and `reboot`.

**ملاحظة:** If you cannot enter the arch-chroot or chroot environment but need to re-install packages you can use the command `pacman -r /mnt -Syu foo bar` to use pacman on your root partition.

### Signature from "User <email@gmail.com>" is unknown trust, installation failed

Follow [pacman-key#Resetting all the keys](/index.php/Pacman-key#Resetting_all_the_keys "Pacman-key"). Or you can try to manually upgrade [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) package first, i.e. `pacman -S archlinux-keyring`.

### I keep getting

```
error: PackageName: signature from "User <email@archlinux.org>" is invalid
error: failed to commit transaction (invalid or corrupted package (PGP signature))
Errors occured, no packages were upgraded. 

```

It happens when the system clock is wrong. Set the [time](/index.php/Time "Time") and run: `# hwclock -w` before to try to install/upgrade a package again.

### I keep getting a "failed to commit transaction (invalid or corrupted package)" error

Look for `*.part` files (partially downloaded packages) in `/var/cache/pacman/pkg` and remove them (often caused by usage of custom `XferCommand` in `pacman.conf`).

### I get an error every time I use pacman saying 'warning: current locale is invalid; using default "C" locale'. What do I do?

As the error message says, your locale is not correctly configured. See [Locale](/index.php/Locale "Locale").

### How can I get Pacman to honor my proxy settings?

Make sure that the relevant environment variables (`$http_proxy`, `$ftp_proxy` etc.) are set up. If you use Pacman with [sudo](/index.php/Sudo "Sudo"), you need to configure sudo to [pass these environment variables to Pacman](/index.php/Sudo#Environment_variables_.28Outdated.3F.29 "Sudo").

## See also

*   [Common Applications/Utilities#Package management](/index.php/Common_Applications/Utilities#Package_management "Common Applications/Utilities")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Pacman_(العربية)&oldid=411899](https://wiki.archlinux.org/index.php?title=Pacman_(العربية)&oldid=411899)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Package management (العربية)](/index.php/Category:Package_management_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9) "Category:Package management (العربية)")
*   [العربية](/index.php/Category:%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9 "Category:العربية")