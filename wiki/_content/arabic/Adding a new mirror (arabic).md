## Contents

*   [1 Adding a new mirror](#Adding_a_new_mirror)
*   [2 2 مخطط -tier mirroring](#2_.D9.85.D8.AE.D8.B7.D8.B7_-tier_mirroring)
*   [3 ل مدرين المرايا](#.D9.84_.D9.85.D8.AF.D8.B1.D9.8A.D9.86_.D8.A7.D9.84.D9.85.D8.B1.D8.A7.D9.8A.D8.A7)
    *   [3.1 متطلبات Tier 2](#.D9.85.D8.AA.D8.B7.D9.84.D8.A8.D8.A7.D8.AA_Tier_2)
    *   [3.2 Tier 1 requirements](#Tier_1_requirements)
    *   [3.3 طلب مزية جديدة او طلب اخر](#.D8.B7.D9.84.D8.A8_.D9.85.D8.B2.D9.8A.D8.A9_.D8.AC.D8.AF.D9.8A.D8.AF.D8.A9_.D8.A7.D9.88_.D8.B7.D9.84.D8.A8_.D8.A7.D8.AE.D8.B1)
*   [4 The Arch Linux side](#The_Arch_Linux_side)
*   [5 حجم المرايا](#.D8.AD.D8.AC.D9.85_.D8.A7.D9.84.D9.85.D8.B1.D8.A7.D9.8A.D8.A7)

### Adding a new mirror

هاذ النص يشرح كيفية اضافة مرايا جديدة ل حزم ارتش

## 2 مخطط -tier mirroring

بسبب الحمل الثقيل علا السيرفرات و الباندوذ المحدود تستخدم ارتش لينكس مخطط 2-tier mirroring. هناك بعض المرايا من هاذ النوع تتزامن مع سيرفرات ارتش لينكس كل ساعة

و كل المرايا المتبقية يجب ان تتزامن من احد الاقسام من سيرفرات ارتش

## ل مدرين المرايا

#### متطلبات Tier 2

*   مساحة القرص الصلب >= 60 GB
*   Sync off a tier 1 mirror (see [https://archlinux.org/mirrors](https://archlinux.org/mirrors))

*   زامن جميع محتويات الفرع الرءيسي لا تزامن بعض المستودعات فقط

*   لا تزامن كل ساعة بل عليك ان تزامن مرة واحدة في اليوم

*   زامن ب وقت عشواءي
*   استخدم الخيارات التالية ل [rsync](/index.php/Rsync "Rsync"): **-rtlvH --delete-after --delay-updates --safe-links --max-delete=1000**
*   اشترك في [arch-mirrors](https://mailman.archlinux.org/mailman/listinfo/arch-mirrors)
*   http support

#### Tier 1 requirements

*   Tier 2 requirements
*   الباندويذ >= 100Mbit/s
*   [rsync](/index.php/Rsync "Rsync") يجب ان يكون مدعوم

*   يجب ان يكون مستقر

يمكنك استخدام rsync مباشرة او [this script](https://git.server-speed.net/users/flo/bin/tree/syncrepo.sh) as a starting point. Please note that the script tries to minimize load and bandwidth used (about 5MiB as of 2014-01-21) in case there are no changes. Feel free to remove this check if you don't sync very often or your upstream mirror does not provide the lastupdate file.

### طلب مزية جديدة او طلب اخر

**Note:** لا نستقبل مرايا ftp

اذهب الا [https://bugs.archlinux.org](https://bugs.archlinux.org) و اطلب ميزة جديدة (category: mirrors) يحتوي علا المعلومات التالية:

*   ناسم نطاق المرايا
*   الموقع الجغرافي ل المرايا
*   URLs لدعم طرق الوصول (http(s), [rsync](/index.php/Rsync "Rsync")) (no ftp)
*   الباندويذ المتوفر ل المرايا

بريد الالكتروني ب مدير المرايا* An alternative administrative contact email (optional)

*   (tier 1 mirrors) Rsync IPs so your server(s) can be allowed to sync off tier 0 (rsync.archlinux.org)
*   (tier 2 mirrors) The name of tier 1 mirror you are syncing from. You can find available tier 1 mirrors [here](https://www.archlinux.org/mirrors/) (sort using the tier column)

Please also join the [arch-mirrors mailing list](https://mailman.archlinux.org/mailman/listinfo/arch-mirrors).

## The Arch Linux side

*   اضف المرايا ل موقع ادارة جانغو
*   اعد انتاج ال rsync whitelist مع the gen_rsyncd.conf.pl script - only for tier 1 mirrors, or when disabling access to a previously untiered mirror (also done by an hourly cronjob)
*   Regenerate the pacman-mirrorlist package

## حجم المرايا

ل تعرف الحجم هاذه المستعملت في هاذه السنة Mandatory:

*   pool (all packages) - 41GB
*   repositories (core, community, extra, testing, gnome-unstable, kde-unstable, multilib) - total ~200MB

Optional:

*   iso - 7GB (encouraged)
*   archive - 15GB (permanently frozen)
*   other - 9GB
*   sources - 28GB

بعض المرايا لا تزامن الارشيف بل المصدر فقط ف كل عادة تحتاج تقريبً 50 غيغا.