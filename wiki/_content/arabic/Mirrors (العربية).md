| **ملخص**  |
| تحديث وإدارة مرايا الحزم. |
| **مواضيع متصلة** |
| [Mirroring](/index.php/Mirroring "Mirroring") |
| [pacman](/index.php/Pacman "Pacman") |
| [reflector](/index.php/Reflector "Reflector") |

هذه الصفحة دليل لاختيار وإعداد المرايا Mirrors (المرآة mirror هي نفسها المُخدم server، لكن يستخدم هذا الاسم مرآة mirror مع بعض المخدمات من بينها مخازن الحزم Package Repositories) ،بالإضافة إلى قائمة بالمرايا المتوفرة.

## Contents

*   [1 تفعيل مرآة معينة](#.D8.AA.D9.81.D8.B9.D9.8A.D9.84_.D9.85.D8.B1.D8.A2.D8.A9_.D9.85.D8.B9.D9.8A.D9.86.D8.A9)
    *   [1.1 إجبار مدير الحزم pacman على تحديث قوائم الحزم](#.D8.A5.D8.AC.D8.A8.D8.A7.D8.B1_.D9.85.D8.AF.D9.8A.D8.B1_.D8.A7.D9.84.D8.AD.D8.B2.D9.85_pacman_.D8.B9.D9.84.D9.89_.D8.AA.D8.AD.D8.AF.D9.8A.D8.AB_.D9.82.D9.88.D8.A7.D8.A6.D9.85_.D8.A7.D9.84.D8.AD.D8.B2.D9.85)
*   [2 حالة المرايا](#.D8.AD.D8.A7.D9.84.D8.A9_.D8.A7.D9.84.D9.85.D8.B1.D8.A7.D9.8A.D8.A7)
*   [3 ترتيب المرايا](#.D8.AA.D8.B1.D8.AA.D9.8A.D8.A8_.D8.A7.D9.84.D9.85.D8.B1.D8.A7.D9.8A.D8.A7)
    *   [3.1 الترتيب حسب السرعة](#.D8.A7.D9.84.D8.AA.D8.B1.D8.AA.D9.8A.D8.A8_.D8.AD.D8.B3.D8.A8_.D8.A7.D9.84.D8.B3.D8.B1.D8.B9.D8.A9)
    *   [3.2 الترتيب حسب السرعة والحالة](#.D8.A7.D9.84.D8.AA.D8.B1.D8.AA.D9.8A.D8.A8_.D8.AD.D8.B3.D8.A8_.D8.A7.D9.84.D8.B3.D8.B1.D8.B9.D8.A9_.D9.88.D8.A7.D9.84.D8.AD.D8.A7.D9.84.D8.A9)
    *   [3.3 سكربت لإدارة استخدام Pacman Mirrorlist Generator](#.D8.B3.D9.83.D8.B1.D8.A8.D8.AA_.D9.84.D8.A5.D8.AF.D8.A7.D8.B1.D8.A9_.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_Pacman_Mirrorlist_Generator)
    *   [3.4 استخدام سكربت Reflector](#.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_.D8.B3.D9.83.D8.B1.D8.A8.D8.AA_Reflector)
    *   [3.5 اختيار مرآة محلية](#.D8.A7.D8.AE.D8.AA.D9.8A.D8.A7.D8.B1_.D9.85.D8.B1.D8.A2.D8.A9_.D9.85.D8.AD.D9.84.D9.8A.D8.A9)
*   [4 المرايا الرسمية](#.D8.A7.D9.84.D9.85.D8.B1.D8.A7.D9.8A.D8.A7_.D8.A7.D9.84.D8.B1.D8.B3.D9.85.D9.8A.D8.A9)
    *   [4.1 المرايا المعدة لـ IPv6](#.D8.A7.D9.84.D9.85.D8.B1.D8.A7.D9.8A.D8.A7_.D8.A7.D9.84.D9.85.D8.B9.D8.AF.D8.A9_.D9.84.D9.80_IPv6)
*   [5 المرايا غير الرسمية](#.D8.A7.D9.84.D9.85.D8.B1.D8.A7.D9.8A.D8.A7_.D8.BA.D9.8A.D8.B1_.D8.A7.D9.84.D8.B1.D8.B3.D9.85.D9.8A.D8.A9)
    *   [5.1 Global](#Global)
    *   [5.2 TOR Network](#TOR_Network)
    *   [5.3 Singapore](#Singapore)
    *   [5.4 Bulgaria](#Bulgaria)
    *   [5.5 Viet Nam](#Viet_Nam)
    *   [5.6 China](#China)
    *   [5.7 France](#France)
    *   [5.8 Germany](#Germany)
    *   [5.9 Indonesia](#Indonesia)
    *   [5.10 Kazakhstan](#Kazakhstan)
    *   [5.11 Malaysia](#Malaysia)
    *   [5.12 New Zealand](#New_Zealand)
    *   [5.13 Poland](#Poland)
    *   [5.14 Russia](#Russia)
    *   [5.15 South Africa](#South_Africa)
    *   [5.16 United States](#United_States)
    *   [5.17 Hyperboria](#Hyperboria)
*   [6 استكشاف الأخطاء وإصلاحها](#.D8.A7.D8.B3.D8.AA.D9.83.D8.B4.D8.A7.D9.81_.D8.A7.D9.84.D8.A3.D8.AE.D8.B7.D8.A7.D8.A1_.D9.88.D8.A5.D8.B5.D9.84.D8.A7.D8.AD.D9.87.D8.A7)
    *   [6.1 مرايا لم يتم مزامنتها out-of-sync: حزم تالفة أو لم يتم إيجاد الملف](#.D9.85.D8.B1.D8.A7.D9.8A.D8.A7_.D9.84.D9.85_.D9.8A.D8.AA.D9.85_.D9.85.D8.B2.D8.A7.D9.85.D9.86.D8.AA.D9.87.D8.A7_out-of-sync:_.D8.AD.D8.B2.D9.85_.D8.AA.D8.A7.D9.84.D9.81.D8.A9_.D8.A3.D9.88_.D9.84.D9.85_.D9.8A.D8.AA.D9.85_.D8.A5.D9.8A.D8.AC.D8.A7.D8.AF_.D8.A7.D9.84.D9.85.D9.84.D9.81)
        *   [6.1.1 استخدام كل المرايا](#.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_.D9.83.D9.84_.D8.A7.D9.84.D9.85.D8.B1.D8.A7.D9.8A.D8.A7)
*   [7 انظر أيضاً](#.D8.A7.D9.86.D8.B8.D8.B1_.D8.A3.D9.8A.D8.B6.D8.A7.D9.8B)

## تفعيل مرآة معينة

لتفعيل المرايا افتح الملف `/etc/pacman.d/mirrorlist`، ثم قم بتفعيل المرايا التي تريدها (إزالة علامة # قبل المرآة المطلوبة) حسب موقعك الجغرافي.

**ملاحظة:** تم تحديد سرعة مُخدّم ftp.archlinux.org القصوى بـ 50 كيلوبايت في الثانية [throttled at 50KB/s](https://www.archlinux.org/news/throttling-ftparchlinuxorg-rsyncarchlinuxorg/).

مثال:

```
# Any
# Server = ftp://mirrors.kernel.org/archlinux/$repo/os/$arch
**Server = http://mirrors.kernel.org/archlinux/$repo/os/$arch**

```

انظر إلى [#Mirror status](#Mirror_status) و [#List by speed](#List_by_speed) للاطلاع على أدوات مساعدة في اختيار المرايا.

**تلميحة:** قم بتفعيل 5 مرايا مفضلة لديك ثم ضعهم في أعلى ملف قائمة المرايا، بهذه الطريقة يسهل إيجادهم وتغيير ترتيبهم في حال حصلت أي مشكلة للمرآة الأولى، كما أنها تسهل عملية دمج تحديثات قائمة المرايا.

من الممكن أيضاً تعيين مرايا محددة ضمن الملف `/etc/pacman.conf`، لكي تحدد مرآة لمستودع _[core]_ فإن الطريقة الافتراضية هي:

```
[core]
Include = /etc/pacman.d/mirrorlist

```

لكي تجعل المرآة _HostEurope_ مرآة افتراضية قم بإضافتها قبل سطر `Include`:

```
[core]
**Server = ftp://ftp.hosteurope.de/mirror/ftp.archlinux.org/core/os/$arch**
Include = /etc/pacman.d/mirrorlist

```

سيقوم مدير الحزم pacman بالاتصال بهذه المرآة قبل أي مرآة أخرى، يمكنك فعل السابق للمستودعات الأخرى مثل _[testing]_ و _[extra]_ و _[community]_.

**ملاحظة:** إذا قمت بتعيين مرايا في الملف `pacman.conf` بشكل مباشر فتذكر أن تستخدم مرآة واحدة لكل المستودعات، وإلا فقد يتم تثبيت حزم غير متوافقة مع بعضها، مثل linux من مستودع _[core]_ ووحدة نواة قديمة من_[extra]_.

### إجبار مدير الحزم pacman على تحديث قوائم الحزم

بعد إنشاء أو تعديل ملف `/etc/pacman.d/mirrorlist` (يدوياً أو باستخدام `rankmirrors`) نفذ الأمر التالي:

```
# pacman -Syy

```

**تلميحة:** تمرير خيار `--refresh` أو `-y` مرتين يجبر pacman على تحديث كل قوائم الحزم حتى تلك التي تم اعتبارها أنها على آخر تحديث up to date، تنفيذ `pacman -Syy` _كلما انتقلت إلى مرايا جديدة_ هو عمل جيد يساعد في تجنب المشاكل المحتملة.

## حالة المرايا

قم بتفحص حالة مرايا آرتش ومدى حداثتها بزيارة [http://www.archlinux.de/?page=MirrorStatus](http://www.archlinux.de/?page=MirrorStatus) و [https://www.archlinux.org/mirrors/status/](https://www.archlinux.org/mirrors/status/).

يمكنك توليد قائمة بأحدث المرايا من [هنا](https://www.archlinux.org/mirrorlist/)، ولإدارة العملية استخدم [script](#Script_to_automate_use_of_Pacman_Mirrorlist_Generator)، أو ثبّت [Reflector](/index.php/Reflector "Reflector") وهي أداة تولد قوائم مرايا mirrorlist باستخدام قائمة Mirrorcheck، كما يمكنك معرفة مدى حداثة مرآة يدوياً عن طريق:

1.  اختيار مُخدم (مرآة) والذهاب إلى المسار "extra/os/" ضمنه.
2.  الذهاب إلى [https://www.archlinux.org/](https://www.archlinux.org/) في نافذة جديدة أو لسان جديد داخل المتصفح.
3.  مقارنة تاريخ آخر تعديل last-modified لمجلد `i686` على المرآة وتاريخ آخر تعديل لمستودع _[extra]_ على الصفحة الرئيسية للموقع، في صندوق _مستودعات الحزم Package Repositories_ على الجانب الأيمن.

## ترتيب المرايا

عند تحميل الحزم من المستودعات فإن pacman يقوم باستخدام المرايا حسب ترتيبها في الملف `/etc/pacman.d/mirrorlist`، في حال أنك لا تستخدم أداة reflector التي تقوم بترتيب المرايا بطريقتين إما حسب حداثتها أو حسب سرعتها، فقم باتباع هذا الشرح حول ترتيب المرايا يدوياً.

**ملاحظة:** هذا لا ينطبق على سكربت [powerpill-light](/index.php/Improve_pacman_performance#Using_powerpill-light "Improve pacman performance") الذي يقوم بالاتصال بعدة مُخدمات معاً لزيادة سرعة التحميل الكلية وبالتالي سرعة الاتصالات الفردية تصبح أقل أهمية، ويمكن إعداد powerpill-light لكي يطلب السرعات الدنيا لكل اتصال.

### الترتيب حسب السرعة

يمكنك استخدام أسرع مرآة محلية عند التحميل، وذلك بتحديدها عن طريق السكربت`/usr/bin/rankmirrors` وهو عبارة عن سكربت Bash مضمّن مع توزيعة آرتش.

قم بأخذ نسخة احتياطية من الملف ملف عن طريق:

```
# cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.backup

```

قم بتفعيل المرايا داخل الملف `/etc/pacman.d/mirrorlist.backup` لكي يتم اختبارها عن طريق `rankmirrors`.

أو تستطيع تنفيذ الأمر `sed` لتفعيل جميع المرايا دون تدخل منك:

```
# sed '/^#\S/ s|#||' -i /etc/pacman.d/mirrorlist.backup

```

أخيراً قم بترتيب المرايا، المعامل `-n 6` يعني أظهر فقط أسرع 6 مرايا:

```
# rankmirrors -n 6 /etc/pacman.d/mirrorlist.backup > /etc/pacman.d/mirrorlist

```

نفذ `rankmirrors -h` لإظهار قائمة بكل الخيارات المتاحة.

### الترتيب حسب السرعة والحالة

التحميل من المرايا السريعة فقط ليست فكرة جيدة فقد لا تكون هذه المرايا محتوية على أحدث نسخ من الحزم، الطريقة المفضلة هي الترتيب حسب السرعة [#List by speed](#List_by_speed) ومن ثم ترتيب هذه المرايا الستة وفقاً لحالتها [#Mirror status](#Mirror_status).

قم بزيارة الرابط أو الرابطان في [#Mirror status](#Mirror_status) وقم بترتيبهم الأحدث تحديثاً ثم الأقدم، ضع المرايا الأحدث في أعلى ملف `/etc/pacman.d/mirrorlist` وإذا كانت المرايا قديمة التحديث فلا تضفها، إعادة هذه العملية ستزيل المرايا القديمة التحديث، وفي النهاية ستحصل على قائمة من ستة مرايا مرتبة حسب السرعة والحالة.

عندما تواجه مشاكل في المرايا قم بإعادة تكرار العملية السابقة، أو قم بإعادة تكرارها كل فترة حتى لو لم تواجه مشاكل كي تُبقي ملف `/etc/pacman.d/mirrorlist` محدثاً up to date.

### سكربت لإدارة استخدام Pacman Mirrorlist Generator

يمكن استخدام سكربت shell التالي لكي تُحدّث المرايا بناءً على الترتيب الذي يقوم به [Pacman Mirrorlist Generator](https://www.archlinux.org/mirrorlist/)، إذا لم تكن تعيش في الولايات المتحدة تستطيع تعديل متغير `country`.

 `updatemirrors.sh` 

```
#!/bin/sh

[ "$UID" != 0 ] && su=sudo

country='US'
url="https://www.archlinux.org/mirrorlist/?country=$country&protocol=https&protocol=http&ip_version=4&use_mirror_status=on"

tmpfile=$(mktemp --suffix=-mirrorlist)

# Get latest mirror list and save to tmpfile
wget -qO- "$url" | sed 's/^#Server/Server/g' > "$tmpfile"

# Backup and replace current mirrorlist file (if new file is non-zero)
if [ -s "$tmpfile" ]
then
  { echo " Backing up the original mirrorlist..."
    $su mv -i /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.orig; } &&
  { echo " Rotating the new list into place..."
    $su mv -i "$tmpfile" /etc/pacman.d/mirrorlist; }
else
  echo " Unable to update, could not download list."
fi

# allow global read access (required for non-root yaourt execution)
chmod +r /etc/pacman.d/mirrorlist
```

**ملاحظة:** يتوجب عليك نسخ النص السابق ووضعه في ملف ثم تنفيذ الأمر `chmod +x` على الملف، إذا لم تكن مسجلاً دخولك كمستخدم جذر سيقوم السكربت باستدعاء sudo بدلاً عنك عندما يحتاج إلى تغيير الترتيب في قائمة المرايا.

### استخدام سكربت Reflector

بدلاً من السابق يمكنك استخدام سكربت [Reflector](/index.php/Reflector "Reflector") حيث أنه يقوم بجلب أحدث قائمة مرايا من صفحة [MirrorStatus](https://www.archlinux.org/mirrors/status/) تلقائياً، ثم يقوم بتحديد المرايا الأحدث تحديثاً، ثم يرتبهم حسب السرعة ويكتب هذه التعديلات في الملف `/etc/pacman.d/mirrorlist`.

### اختيار مرآة محلية

أبسط طريقة هي وضع مرآة محلية في أعلى القائمة داخل ملف قائمة المرايا، وسيجعل pacman لهذه المرآة الأولوية عن باقي المرايا.

بدلاً من ذلك يمكن تعديل ملف pacman.conf بوضع مرآة محلية قبل السطر الذي يحدد ملف قائمة المرايا المستخدم في التحميل، أي في المكان المكتوب فيه "أضف المُخدمات المفضلة هنا add your preferred servers here"، يُفضل (وهو أكثر أماناً) بأن تقوم باختيار نفس المُخدم لكل المستودعات.

## المرايا الرسمية

قائمة مرايا آرتش لينوكس الرسمية تتوفر في حزمة [pacman-mirrorlist](https://www.archlinux.org/packages/?name=pacman-mirrorlist)، ولكي تحصل على قوائم أحدث من الموجودة في الحزمة السابقة اذهب إلى صفحة [Pacman Mirror List Generator](https://www.archlinux.org/mirrorlist/).

في حال أنك لم تقم بإعداد أية مرايا وأن حزمة `pacman-mirrorlist` غير مثبتة لديك، قم بتفيذ الأوامر التالية:

```
# wget -O /etc/pacman.d/mirrorlist https://www.archlinux.org/mirrorlist/all/

```

تأكد من أنك قمت بتفعيل المرايا المفضلة كما هو مشروح في الأعلى، ومن ثم نفذ:

```
# pacman -Syy
# pacman -S --force pacman-mirrorlist

```

إذا كنت ترغب بأن تضيف مرآتك إلى القائمة الرسمية قدم طلباً بذلك، في غضون ذلك أضفها إلى قائمة [#Unofficial mirrors](#Unofficial_mirrors) في نهاية هذه الصفحة.

إذا حصلت على خطأ يعلمك بأن متغير `$arch` تم استخدامه لكن لم يتم تعريفه، قم بإضافة التالي إلى ملف `/etc/pacman.conf`:

```
Architecture = x86_64

```

**ملاحظة:** يمكنك أيضاً استعمال `auto` و `i686` لمتغير `Architecture`.

### المرايا المعدة لـ IPv6

يمكن استعمال [pacman mirror list generator](https://www.archlinux.org/mirrorlist/?country=all&protocol=http&ip_version=6) لإيجاد قائمة بمرايا IPv6 المتوفرة.

## المرايا غير الرسمية

هذه المرايا _غير_ مكتوبة في `/etc/pacman.d/mirrorlist`.

### Global

*   [http://sourceforge.net/projects/archlinux/files/](http://sourceforge.net/projects/archlinux/files/) - _ISO files only; Does not have any releases since 2006\. Use it only if for getting older ISOs._

### TOR Network

*   [http://cz2jqg7pj2hqanw7.onion/archlinux](http://cz2jqg7pj2hqanw7.onion/archlinux)
*   [ftp://mirror:mirror@cz2jqg7pj2hqanw7.onion/archlinux](ftp://mirror:mirror@cz2jqg7pj2hqanw7.onion/archlinux)

### Singapore

*   [http://mirror.nus.edu.sg/archlinux/](http://mirror.nus.edu.sg/archlinux/)

### Bulgaria

*   [http://mirror.telepoint.bg/archlinux/](http://mirror.telepoint.bg/archlinux/)
*   [ftp://mirror.telepoint.bg/archlinux/](ftp://mirror.telepoint.bg/archlinux/)

### Viet Nam

**FPT TELECOM**

*   [http://mirror-fpt-telecom.fpt.net/archlinux/](http://mirror-fpt-telecom.fpt.net/archlinux/)

### China

**CHINA TELECOM**

*   [http://mirror.lupaworld.com/archlinux/](http://mirror.lupaworld.com/archlinux/)

**CHINA UNICOM**

*   [http://mirrors.sohu.com/archlinux/](http://mirrors.sohu.com/archlinux/)

**Cernet**

*   [http://mirrors.zju.edu.cn/archlinux/](http://mirrors.zju.edu.cn/archlinux/) - "Zhejian University"
*   [http://ftp.sjtu.edu.cn/archlinux/](http://ftp.sjtu.edu.cn/archlinux/) - _Shanghai Jiaotong University_
*   [ftp://ftp.sjtu.edu.cn/archlinux/](ftp://ftp.sjtu.edu.cn/archlinux/)
*   [http://mirrors.ustc.edu.cn/archlinux/](http://mirrors.ustc.edu.cn/archlinux/) - _University of Science and Technology of China_
*   [ftp://mirrors.ustc.edu.cn/archlinux/](ftp://mirrors.ustc.edu.cn/archlinux/)
*   [http://mirrors.tuna.tsinghua.edu.cn/archlinux/](http://mirrors.tuna.tsinghua.edu.cn/archlinux/) - _Tsinghua University_
*   [http://mirrors.4.tuna.tsinghua.edu.cn/archlinux/](http://mirrors.4.tuna.tsinghua.edu.cn/archlinux/) _(ipv4 only)_
*   [http://mirrors.6.tuna.tsinghua.edu.cn/archlinux/](http://mirrors.6.tuna.tsinghua.edu.cn/archlinux/) _(ipv6 only)_
*   [http://mirror.lzu.edu.cn/archlinux/](http://mirror.lzu.edu.cn/archlinux/) - _Lanzhou University_

### France

*   [http://delta.archlinux.fr/](http://delta.archlinux.fr/) - _With Delta package support. Needs xdelta3 package from extra to run._
*   [http://mirror.soa1.org/archlinux](http://mirror.soa1.org/archlinux)
*   [ftp://mirror:mirror@mirror.soa1.org/archlinux](ftp://mirror:mirror@mirror.soa1.org/archlinux)

### Germany

*   [http://ftp.uni-erlangen.de/mirrors/archlinux/](http://ftp.uni-erlangen.de/mirrors/archlinux/)
*   [ftp://ftp.uni-erlangen.de/mirrors/archlinux/](ftp://ftp.uni-erlangen.de/mirrors/archlinux/)
*   [http://ftp.u-tx.net/archlinux/](http://ftp.u-tx.net/archlinux/)
*   [ftp://ftp.u-tx.net/archlinux/](ftp://ftp.u-tx.net/archlinux/)
*   [http://mirror.michael-eckert.net/archlinux/](http://mirror.michael-eckert.net/archlinux/)
*   [http://linux.rz.rub.de/archlinux/](http://linux.rz.rub.de/archlinux/)

### Indonesia

*   [http://mirror.kavalinux.com/archlinux/](http://mirror.kavalinux.com/archlinux/) - _only from Indonesia_
*   [http://kambing.ui.ac.id/archlinux/](http://kambing.ui.ac.id/archlinux/)
*   [http://repo.ukdw.ac.id/archlinux/](http://repo.ukdw.ac.id/archlinux/)

### Kazakhstan

*   [http://archlinux.kz/](http://archlinux.kz/)
*   [http://mirror.neolabs.kz/archlinux/](http://mirror.neolabs.kz/archlinux/)
*   [http://mirror-kt.neolabs.kz/archlinux/](http://mirror-kt.neolabs.kz/archlinux/)

### Malaysia

*   [http://mirror.oscc.org.my/archlinux/](http://mirror.oscc.org.my/archlinux/)
*   [http://mirrors.inetutils.net/archlinux/](http://mirrors.inetutils.net/archlinux/) - _ISO and Core_

### New Zealand

*   [http://mirror.ihug.co.nz/archlinux/](http://mirror.ihug.co.nz/archlinux/)
*   [http://mirror.ece.auckland.ac.nz/archlinux/](http://mirror.ece.auckland.ac.nz/archlinux/) _NZ only_

### Poland

*   [ftp://ftp.icm.edu.pl/pub/Linux/dist/archlinux/](ftp://ftp.icm.edu.pl/pub/Linux/dist/archlinux/) - ICM UW
*   [http://ftp.icm.edu.pl/pub/Linux/dist/archlinux/](http://ftp.icm.edu.pl/pub/Linux/dist/archlinux/) - ICM UW
*   rsync://ftp.icm.edu.pl/pub/Linux/dist/archlinux/ - ICM UW

### Russia

*   [http://hatred.homelinux.net/archlinux/](http://hatred.homelinux.net/archlinux/) - _Vladivostok, without iso, with <sub>[3SPY](http://hatred.homelinux.net/wiki/proekty:3spy:start)</sub> project repos and [**mingw32**](http://hatred.homelinux.net/archlinux/mingw32/os/i686) repo_
*   [http://mirrors.krasinfo.ru/archlinux/](http://mirrors.krasinfo.ru/archlinux/) - _Krasnoyarsk, Classica-Service Ltd_

### South Africa

*   [http://ftp.sun.ac.za/ftp/pub/mirrors/archlinux/](http://ftp.sun.ac.za/ftp/pub/mirrors/archlinux/) - _Stellenbosch University_
*   [ftp://ftp.sun.ac.za/pub/mirrors/archlinux/](ftp://ftp.sun.ac.za/pub/mirrors/archlinux/)
*   [http://ftp.leg.uct.ac.za/pub/linux/arch/](http://ftp.leg.uct.ac.za/pub/linux/arch/) - _University of Cape Town_
*   [ftp://ftp.leg.uct.ac.za/pub/linux/arch/](ftp://ftp.leg.uct.ac.za/pub/linux/arch/)
*   [http://mirror.ufs.ac.za/archlinux/](http://mirror.ufs.ac.za/archlinux/) - _University of the Free State_
*   [ftp://mirror.ufs.ac.za/os/linux/distros/archlinux/](ftp://mirror.ufs.ac.za/os/linux/distros/archlinux/)
*   [http://ftp.wa.co.za/pub/archlinux/](http://ftp.wa.co.za/pub/archlinux/) - _Web Africa Networks_
*   [ftp://ftp.wa.co.za/pub/archlinux/](ftp://ftp.wa.co.za/pub/archlinux/)
*   [http://archlinux.mirror.ac.za](http://archlinux.mirror.ac.za) - _TENET - Tertiary Education and Research Network of South Africa_
*   [ftp://archlinux.mirror.ac.za](ftp://archlinux.mirror.ac.za)

### United States

*   [http://archlinux.linuxfreedom.com](http://archlinux.linuxfreedom.com) - _Contains numerous ISO images but does not contain the ISO dated 2011.08.19_
*   [http://mirror.pointysoftware.net/archlinux/](http://mirror.pointysoftware.net/archlinux/)

### Hyperboria

*   [http://[fc7b:5f90:01f8:2b33:7c3e:f94b:00f3:0bed]/archlinux/](http://[fc7b:5f90:01f8:2b33:7c3e:f94b:00f3:0bed]/archlinux/)

## استكشاف الأخطاء وإصلاحها

### مرايا لم يتم مزامنتها out-of-sync: حزم تالفة أو لم يتم إيجاد الملف

المشاكل الناتجة عن المرايا التي لم يتم مزامنتها out-of-sync المُشار لها في هذا الرابط [this news post](https://www.archlinux.org/news/482/) قد تم بالفعل حلها بالنسبة لمعظم المستخدمين، لكن في حال أن هذه المشاكل ظهرت مرة أخرى قم بالتأكد من أن الحزم موجودة في مستودع [testing].

بعد قيامك بالمزامنة عن طريق `pacman -Sy` نفذ هذا الأمر:

```
# pacman -Ud $(pacman -Sup | tail -n +2 | sed -e 's,/\(core\|extra\)/,/testing/,' \
                                              -e 's,/\(community\)/,/\1-testing/,')

```

قيامك بالأمر السابق سيساعد في حال أن الحزم الموجودة في المرايا بقيت في مستودع [testing] ولم تتم مزامنتها مع مستودع [core] أو [extra]، ومن الآمن جداً أن تثبت الحزم من مستودع [testing] حيث أن الحزم تتم مطابقتها بالنسخة ورقم الإصدار.

عموماً فمن الأفضل تبديل المرايا ومزامنتها عن طريق `pacman -Syy` من أن تلجأ إلى مستودع بديل، ومع ذلك فإن بعض أو كل المرايا مع مرور الوقت قد تصبح بحالة out-of-sync.

#### استخدام كل المرايا

لمحاكاة سلوك `pacman -Su` في التنقل في قائمة المرايا كاملة استخدم هذا السكربت:

 `~/bin/pacup` 

```
#!/bin/bash

# Pacman will not exit on the first error. Comment the line below to
# try from [testing] directly.
pacman -Su "$@" && exit

while read -r pkg; do
  if pacman -Ud "$pkg"; then
    continue
  else
    while read -r mirror; do
      pacman -Ud $(sed "s,.*\(/\(community-\)*testing/os/\(i686\|x86_64\)/\),$mirror\1," <<<"$pkg") &&
      break
    done < <(sed -ne 's,^ *Server *= *\|/$repo/os/\(i686\|x86_64\).*,,gp' \
           </etc/pacman.d/mirrorlist | tail -n +2 )
  fi
done < <(pacman -Sup | tail -n +2 | sed -e 's,/\(core\|extra\)/,/testing/,' \
                                        -e 's,/\(community\)/,/\1-testing/,')

```

## انظر أيضاً

[MirUp](http://wiki.gotux.net/code/bash/mirup) - مُحمّل وفاحص لقائمة مرايا pacman