| **ملخص**  |
| Article covers configuration of NFSv4 which is an open standard network file sharing protocol. |
| **مواضيع ذات صلة** |
| [NFS Troubleshooting](/index.php/NFS_Troubleshooting "NFS Troubleshooting") - Dedicated article for common problems and solutions. |

نقلا عن: [Wikipedia](https://en.wikipedia.org/wiki/Network_File_System "wikipedia:Network File System"): نظام ملفات الشبكة:_(Network File System NFS) هو بروتوكول نظام الملفات الموزع وقد تم تطويره من شركة صن ميكروسيستمز عام 1984 ، حيث يتيح للمستخدم على الحاسب العميل أن يصل للملفات عبر الشبكة بطريقة مشابهة لكيفية الوصول إلى أقراص التخزين المحلية._

## Contents

*   [1 التثبيت](#.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA)
*   [2 التهيئة](#.D8.A7.D9.84.D8.AA.D9.87.D9.8A.D8.A6.D8.A9)
    *   [2.1 الخادم](#.D8.A7.D9.84.D8.AE.D8.A7.D8.AF.D9.85)
        *   [2.1.1 مخطط المعرفات ID mapping](#.D9.85.D8.AE.D8.B7.D8.B7_.D8.A7.D9.84.D9.85.D8.B9.D8.B1.D9.81.D8.A7.D8.AA_ID_mapping)
        *   [2.1.2 نظام الملفات](#.D9.86.D8.B8.D8.A7.D9.85_.D8.A7.D9.84.D9.85.D9.84.D9.81.D8.A7.D8.AA)
        *   [2.1.3 ملف Exports](#.D9.85.D9.84.D9.81_Exports)
        *   [2.1.4 بدء عمل الخادم](#.D8.A8.D8.AF.D8.A1_.D8.B9.D9.85.D9.84_.D8.A7.D9.84.D8.AE.D8.A7.D8.AF.D9.85)
    *   [2.2 العميل Client](#.D8.A7.D9.84.D8.B9.D9.85.D9.8A.D9.84_Client)
        *   [2.2.1 التوصيل من نظام لينكس](#.D8.A7.D9.84.D8.AA.D9.88.D8.B5.D9.8A.D9.84_.D9.85.D9.86_.D9.86.D8.B8.D8.A7.D9.85_.D9.84.D9.8A.D9.86.D9.83.D8.B3)
            *   [2.2.1.1 إعدادات الملف etc/fstab/](#.D8.A5.D8.B9.D8.AF.D8.A7.D8.AF.D8.A7.D8.AA_.D8.A7.D9.84.D9.85.D9.84.D9.81_etc.2Ffstab.2F)
        *   [2.2.2 استخدام autofs](#.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_autofs)
        *   [2.2.3 التوصيل من وندوز](#.D8.A7.D9.84.D8.AA.D9.88.D8.B5.D9.8A.D9.84_.D9.85.D9.86_.D9.88.D9.86.D8.AF.D9.88.D8.B2)
        *   [2.2.4 التوصيل من نظام ماك OS X](#.D8.A7.D9.84.D8.AA.D9.88.D8.B5.D9.8A.D9.84_.D9.85.D9.86_.D9.86.D8.B8.D8.A7.D9.85_.D9.85.D8.A7.D9.83_OS_X)
*   [3 استكشاف الأخطاء وإصلاحها](#.D8.A7.D8.B3.D8.AA.D9.83.D8.B4.D8.A7.D9.81_.D8.A7.D9.84.D8.A3.D8.AE.D8.B7.D8.A7.D8.A1_.D9.88.D8.A5.D8.B5.D9.84.D8.A7.D8.AD.D9.87.D8.A7)

## التثبيت

كل من الخادم والعميل يتطلبان فقط إلى [تثبيت](/index.php/Pacman "Pacman") الحزمة [nfs-utils](https://www.archlinux.org/packages/?name=nfs-utils).

**ملاحظة:** ينصح **بشدة** باستخدام خدمة المزامنة على جميع النقاط في شبكتك للاحتفاظ بتزامن التوقيت على الخادم/العميل.وبدون الضبط الدقيق للتوقيت على كافة العقد ، يمكن ل NFS ان يسبب تأخيرات غير مرغوب فيها! يوصى باستخدام نظام بروتوكول توقيت الشبكة [NTP](/index.php/NTP "NTP") لمزامنة كل من الخادم والعملاء لوجود خوادم عالية الدقة لتوقيت الشبكة المتاحة على الإنترنت.

## التهيئة

### الخادم

#### مخطط المعرفات ID mapping

عدل الملف `/etc/idmapd.conf` واضبط حقل `Domain` حسب اسم النطاق لديك.

 `/etc/idmapd.conf` 

```
[General]

Verbosity = 1
Pipefs-Directory = /var/lib/nfs/rpc_pipefs
Domain = atomic

[Mapping]

Nobody-User = nobody
Nobody-Group = nobody

```

#### نظام الملفات

**ملاحظة:** لأسباب تتعلق بالأمن ، يوصى باستخدام قسم جذر export للتصدير في NFS والذي سيحدد عمل المستخدمين على هذه النقطة فحسب هذا الثمال سيوضح هذا المفهوم.

تحديد اي مشاركات ل NFS في `/etc/exports` والتي ترتبط ب NFS root. في هذا المثال سيكون قسم الجذر ل NFS هو `/srv/nfs4` وسوف يتشارك ب `/mnt/music`.

 `# mkdir -p /srv/nfs4/music` 

تصاريح الكتابة والقراءة Read/Write يجب ضبطها على المجلد music لذا يمكن للعملاء أن يكتبوا عليه. اﻵن وصل مجلد التشارك الفعلي، `/mnt/music` مع NFS عن طريق أمر الوصل:

 `# mount --bind /mnt/music /srv/nfs4/music` 

لجعل ذلك ثابتا عند إعادة تشغيل الخادم ، أضف خيار الربط الإلزامي bind لملف `fstab`:

 `/etc/fstab` 

```
/mnt/music /srv/nfs4/music  none   bind   0   0

```

#### ملف Exports

أضف المجلدات التي تريد مشاركتها وأحد عناوين ip أو اسم المضيف hostname(s) لحاسب العميل ، الذي سيتاح له توصيل هذه المجلدات في `exports`:

 `/etc/exports` 

```
/srv/nfs4/ 192.168.0.1/24(rw,fsid=root,no_subtree_check)
/srv/nfs4/music 192.168.0.1/24(rw,no_subtree_check,nohide) # note the nohide option which is applied to mounted directories on the file system.

```

لا يحتاج المستخدمون لفتح المشاركة بداخل الشبكة الفرعية، أحدهم يمكنه تحديد عنوان IP مفرد أو hostname أيضا. لمزيد من المعلومات عن كل الخيارات المتاحة انظر `man 5 exports`. إذا قمت بتعديل الملف `/etc/exports` أثناء عمل الخادم ، يجب عليك إعادة التصدير لها لتفعيل ما قمت به من تغييرات:

 `# exportfs -ra` 

#### بدء عمل الخادم

[بدء/تفعيل](/index.php/Daemons "Daemons") `rpc-idmapd.service` و `rpc-mountd.service`. لاحظ أن هذه الوحدات تتطلب غيرها من الخدمات، والتي يتم تشغيلها تلقائيا من قِبل [systemd](/index.php/Systemd "Systemd").

### العميل Client

يحتاج العملاء إلى الحزمة [nfs-utils](https://www.archlinux.org/packages/?name=nfs-utils) للاتصال، لكن لا يتطلب إعدادا خاصا عندما يتصل بخوادم NFS4 .

#### التوصيل من نظام لينكس

إظهار أنظمة الملفات الخوادم المصدرة:

 `$ showmount -e servername` 

ثم توصيل جذر خادم NFS :

 `# mount -t nfs4 servername:/music /mountpoint/on/client` 

##### إعدادات الملف etc/fstab/

استخدام الملف [fstab](/index.php/Fstab "Fstab") مفيد للخادم الذي يعمل دوما، وتكون مشاركات NFS متاحة حالما يشتغل العميل.قم بتحرير الملف `/etc/fstab` ، وأضف السطر المناسب الذي يعكس هذا الإعداد. مرة ثانية، جذر خادم NFS مهمل.

 `/etc/fstab` 

```
servername:/music   /mountpoint/on/client   nfs4   rsize=8192,wsize=8192,timeo=14,intr,_netdev	0 0

```

**ملاحظة:** خيارات التوصيل الإضافية يمكن تحديدها هنا. قم بالرجوع إلى صفحة مساعدة NFS لمزيد من المعلومات.

بعض خيارات التوصيل الإضافية للنظر هي ما يلي:

*   `rsize=8192` and `wsize=8192`
*   `timeo=14`
*   `intr`
*   `_netdev`

قيمة `rsize` هي عدد البايتات المستخدمة حين القراءة من الخادم. القيمة `wsize` هي عدد البايتات المستخدمة عند الكتابة على الخادم. يوصى بتجربة ذلك بعد عمل هذه التغييرات. قيمة `timeo` هي مقدار الوقت، محسوبا بمعشار الثانية، التي يتم انتظارها قبل إعادة الإرسال بعد نفاذ مهلة نداء الإجراء البعيد RPC timeout. بعد نفاذ المهلة اﻷولى، تضاعف قيمة المهلة لكل إعادة محاولة لمدة أقصاها 60 ثانية أو حتى تنفذ المهلة الكبرى. إذا كان الاتصال بالخادم بطيئا أو خلال انشغال بالشبكة ، يمكن تحقيق أفضل أداء بزيادة قيمة هذه المهلة. الخيار `intr` يسمح للإشارات بمقاطعة العملية إذا كانت المهلة اﻷكبر تحدث في اتصال دائم hard-mounted.. الخيار `_netdev` يبلغ النظام بالانتظار طالما كانت تعمل الشبكة قبل محاولة توصيل المشاركة. يفترض systemd ذلك بالنسبة ل NFS لكن على أية حال من اﻷفضل تطبيقه لجميع أنواع نظم ملفات الشبكة.

#### استخدام autofs

استخدام [autofs](/index.php/Autofs "Autofs") مفيد للحواسب التي تريد الاتصال عن طريق NFS; ويمكن أن تكون خوادم أو عملاء أيضا. السبب في هذه الطريقة هو أفضلية بعضها على بعض أنه عند إطفاء الخادم ، فلن يحصل العميل على أخطاء عن عدم قدرته الوصول إلى مشاركات NFS. انظر [autofs#NFS Network mounts](/index.php/Autofs#NFS_Network_mounts "Autofs") لمزيد من التفاصيل.

#### التوصيل من وندوز

**ملاحظة:** إصدارات وندوز 7 من نوع Ultimate و Enterprise وإصدارة Enterprise من ندوز 8 تحتوي على "عميل NFS".

ملفات مشاركة NFS يمكن توصيلها من وندوز غذا كان خدمة "عمسل NFS" مفعلة )حيث إنها غير مفعلة افتراضيا) ولتثبيت هذه الخدمة اذهب إلى "Programs and features" في لوحة التحكم واضغط على "Turn Windows features on or off". حدد مكان "خدمات NFS" وقم بتفعيلها أيضا وكذلك كل من الخدمات الفرعية("Administrative tools" و "عميل NFS").

بعض الخيارات العامة يمكن ضبطها عن طريق فتح "Services for Network File System" (حدد مكانها عنة طريق صندوق البحث) ثم اضغط بالزر اﻷيمن على client->properties.

**تحذير:** قد تحدث بعض المشاكل المتعلقة باﻷداء (حيث تأخذ ما بين 30-60 ثانية لإظهار المجلد ، وسرعة نقل الملفات 2 MB/s على شرائح شبكات جيجابايت، حيث لم تتوصل ميكروسوفت إلى حل لذلك حتى اﻵن . [[1]](https://social.technet.microsoft.com/Forums/en-CA/w7itpronetworking/thread/40cc01e3-65e4-4bb6-855e-cef1364a60ac)

لتوصيل مجلدات الماركة باستخدام المتصفح Explorer:

`Computer` > `Map network drive` > `servername:/srv/nfs4/music`

#### التوصيل من نظام ماك OS X

**ملاحظة:** نظام OS X يستخدم افتراضيا المنفذ غير الآمن (>1024) لتوصيل مجلدات المشاركة

ويستوي كل من استيراد ملفات المشاركة ب `insecure` flag, والتوصيل باستخدام Finder:

`Go` > `Connect to Server` > `nfs://servername/` أو توصيل ملفات المشاركة عن طريق استخدام المنفذ غير اﻵمن عن طريق الطرفية:

 `# sudo mount -t nfs -o resvport servername:/srv/nfs4 /Volumes/servername` 

## استكشاف الأخطاء وإصلاحها

_اقرأ هذا المقال المخصص [NFS Troubleshooting](/index.php/NFS_Troubleshooting "NFS Troubleshooting")._