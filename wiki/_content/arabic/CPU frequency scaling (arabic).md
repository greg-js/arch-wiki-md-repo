Related articles

*   [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools")
*   [pm-utils](/index.php/Pm-utils "Pm-utils")
*   [PHC](/index.php/PHC "PHC")

cpufreq تعني بنية النواة التحتية التي تقوم بتغيير تردد وحدة المعالجة المركزية، تسمح هذه التقنية لنظام التشغيل من أن يقوم بتغيير تردد المعالج زيادةً أو نقصاناً من أجل توفير استهلاك الطاقة، من الممكن أن يتم تغيير التردد تلقائياً automatically بحسب احتياجات النظام واستجابةً لأحداث ACPI (واجهة التهيئة المتقدمة للطاقة Advanced Configuration Power Interface) أو يدوياً عن طريق البرامج.

منذ إصدار النواة رقم 3.4 فإن الوحدات modules الضرورية يتم تحميلها تلقائياً بالإضافة إلى تفعيل مخطط الطاقة [ondemand governor](/index.php/CPU_frequency_scaling#Scaling_governors "CPU frequency scaling") (العمل عند الطلب) الذي ينصح بالعمل عليه بشكل افتراضي. غير أن برامج مثل [cpupower](#cpupower), [acpid](/index.php/Acpid "Acpid"), [laptop-mode-tools](/index.php/Laptop-mode-tools "Laptop-mode-tools") أو بعض الأدوات ذات الواجهة الرسومية GUI ما زالت تُستخدم للتهيئة المتقدمة.

## Contents

*   [1 أدوات(cpupower)](#.D8.A3.D8.AF.D9.88.D8.A7.D8.AA.28cpupower.29)
    *   [1.1 تعاريف المعالج الخاصة بالتردد](#.D8.AA.D8.B9.D8.A7.D8.B1.D9.8A.D9.81_.D8.A7.D9.84.D9.85.D8.B9.D8.A7.D9.84.D8.AC_.D8.A7.D9.84.D8.AE.D8.A7.D8.B5.D8.A9_.D8.A8.D8.A7.D9.84.D8.AA.D8.B1.D8.AF.D8.AF)
    *   [1.2 Scaling governors](#Scaling_governors)
        *   [1.2.1 عند استخدام cpupower](#.D8.B9.D9.86.D8.AF_.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_cpupower)
        *   [1.2.2 عند عدم استخدام cpupower](#.D8.B9.D9.86.D8.AF_.D8.B9.D8.AF.D9.85_.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_cpupower)
    *   [1.3 ضبط مخططات الطاقة (باستخدام cpupower)](#.D8.B6.D8.A8.D8.B7_.D9.85.D8.AE.D8.B7.D8.B7.D8.A7.D8.AA_.D8.A7.D9.84.D8.B7.D8.A7.D9.82.D8.A9_.28.D8.A8.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_cpupower.29)
        *   [1.3.1 معدل أخد العينات](#.D9.85.D8.B9.D8.AF.D9.84_.D8.A3.D8.AE.D8.AF_.D8.A7.D9.84.D8.B9.D9.8A.D9.86.D8.A7.D8.AA)
    *   [1.4 تعيين الحد الأعلى والحد الأدنى للتردد](#.D8.AA.D8.B9.D9.8A.D9.8A.D9.86_.D8.A7.D9.84.D8.AD.D8.AF_.D8.A7.D9.84.D8.A3.D8.B9.D9.84.D9.89_.D9.88.D8.A7.D9.84.D8.AD.D8.AF_.D8.A7.D9.84.D8.A3.D8.AF.D9.86.D9.89_.D9.84.D9.84.D8.AA.D8.B1.D8.AF.D8.AF)
*   [2 التفاعل مع حالات ACPI](#.D8.A7.D9.84.D8.AA.D9.81.D8.A7.D8.B9.D9.84_.D9.85.D8.B9_.D8.AD.D8.A7.D9.84.D8.A7.D8.AA_ACPI)
*   [3 Privilege Granting Under GNOME](#Privilege_Granting_Under_GNOME)
*   [4 أدوات وضعية الحاسب المحمول](#.D8.A3.D8.AF.D9.88.D8.A7.D8.AA_.D9.88.D8.B6.D8.B9.D9.8A.D8.A9_.D8.A7.D9.84.D8.AD.D8.A7.D8.B3.D8.A8_.D8.A7.D9.84.D9.85.D8.AD.D9.85.D9.88.D9.84)
*   [5 استكشاف الأخطاء وإصلاحها](#.D8.A7.D8.B3.D8.AA.D9.83.D8.B4.D8.A7.D9.81_.D8.A7.D9.84.D8.A3.D8.AE.D8.B7.D8.A7.D8.A1_.D9.88.D8.A5.D8.B5.D9.84.D8.A7.D8.AD.D9.87.D8.A7)
    *   [5.1 تقييد التردد من قبل BIOS](#.D8.AA.D9.82.D9.8A.D9.8A.D8.AF_.D8.A7.D9.84.D8.AA.D8.B1.D8.AF.D8.AF_.D9.85.D9.86_.D9.82.D8.A8.D9.84_BIOS)

## أدوات(cpupower)

حزمة [cpupower](https://www.archlinux.org/packages/?name=cpupower) هي عبارة عن أدوات صممت لتساعد في *تغيير تردد المعالج*، مع العلم أنك تستطيع تغيير التردد من دون وجود هذه الحزمة ولكن من المستحسن وجودها لأنها تحتوي على أدوات مفيدة تعمل في سطر الأوامر وخدمة لتغيير مخطط الطاقة governor عند الإقلاع، يتواجد ملف تهيئة الحزمة [cpupower](https://www.archlinux.org/packages/?name=cpupower) في المسار `/etc/default/cpupower`، يتم قراءة هذا الملف من قبل سكربت bash في `/usr/lib/systemd/scripts/cpupower` والذي يتم تفعيله من قبل مدير النظام `systemd` مع `cpupower.service`، لتفعيل [cpupower](https://www.archlinux.org/packages/?name=cpupower) عند الإقلاع باستعمال [systemd](https://www.archlinux.org/packages/?name=systemd) قم بتنفيذ:

```
# systemctl enable cpupower.service

```

تستطيع الحصول على واجهة لـ gnome-shell من [CPU Freq](https://extensions.gnome.org/extension/444/cpu-freq/).

### تعاريف المعالج الخاصة بالتردد

**ملاحظة:** اعتباراً من النواة 3.4 فإن وحدة المعالج المحلية يتم تحميلها تلقائياً

**ملاحظة:** بدءاً من النواة 3.9 سيتم وبشكل تلقائي استخدام تعريف `pstate` الخاص بإدارة الطاقة في معالجات إنتل الحديثة والاستغناء عن التعاريف الظاهرة في الأسفل، هذا التعريف له الأفضلية على التعاريف الأخرى كما أنه بُني بحيث لا يكون كوحدة module، يتم استخدام هذا التعريف حالياً بشكل تلقائي في المعالجات من النوع Sandy Bridge و Ivy Bridge، إذا كنت تواجه مشكلة أثناء استخدام هذا التعريف قم بإضافة `intel_pstate=disable` إلى سطر النواة، يمكنك استعمال نفس أدوات المُستخدِم مع هذا التعريف لكن لا تستطيع أن تتحكم فيه.

أداة [cpupower](https://www.archlinux.org/packages/?name=cpupower) تحتاج إلى وحدات لمعرفة حدود المعالج المحلي (انظر إلى الجدول في الأسفل)، للاطلاع على قائمة بكل الوحدات المتوفرة قم بتنفيذ:

```
$ ls /lib/modules/$(uname -r)/kernel/drivers/cpufreq/

```

**Tip:** لتحميل الوحدة أثناء إقلاع النظام نفذ التالي:
```
# echo <module> >/etc/modules-load.d/<module>.conf

```

**ملاحظة:** تحميل وحدة خاطئة سينتج عنه الخطأ "No such device"

قم بتحميل الوحدة المناسبة عن طريق:

```
# modprobe <module>

```

| الوحدة | الوصف |
| acpi-cpufreq | تعريف CPUFreq الذي يستخدم ACPI Processor Performance States، هذا التعريف يدعم تقنية Intel Enhanced SpeedStep (سابقاً كانت هذه التقنية مدعومة من وحدة speedstep-centrino التي تم إهمالها) |
| speedstep-lib | تعريف CPUFreq لمعالجات Intel speedstep enabled (خاصة المعالجات من فئة atoms و معالجات pentium القديمة (أقدم من 3)) |
| powernow-k8 | تعريف CPUFreq لمعالجات K8/K10 Athlon64/Opteron/Phenom. **تم إهمال هذا التعريف منذ إصدار النواة رقم 3.7، استعمل acpi_cpufreq** |
| pcc-cpufreq | هذا التعريف يدعم واجهة Processor Clocking Control المصممة من قبل شركتا Hewlett-Packard و Microsoft التي تفيد في بعض مُخدمات Proliant |
| p4_clockmod | تعريف CPUFreq لمعالجات Intel Pentium 4 / Xeon / Celeron ، عند تفعيل التعريف سيقوم بتخفيض حرارة المعالج عن طريق تخطي دورات الساعة skipping clocks، من الأرجح أنك ستقوم باستخدام تعريف Speedstep بدلاً من هذا |

عند تحميل التعريف المناسب فإنك تستطيع عرض معلومات مفصلة عن المعالج (أو المعالجات) بتنفيذ:

```
$ cpupower frequency-info

```

### Scaling governors

الـ governors هي مخططات الطاقة للمعالج (انظر إلى الجدول في الأسفل)، ولا يمكن تفعيل أكثر من مخطط واحد في نفس اللحظة، لتفاصيل أكثر قم بالاطلاع على الوثائق الرسمية [official documentation](https://www.kernel.org/doc/Documentation/cpu-freq/governors.txt) في مصادر النواة.

**ملاحظة:** النواة تقوم بتحميل المخطط `on_demand` بشكل افتراضي

| الوحدة | الوصف |
| cpufreq_ondemand | تقوم بالتبديل بين الترددات ديناميكياً عند وصول نسبة الحِمل على المعالج إلى 95% |
| cpufreq_performance | تجعل المعالج يعمل بأعلى تردد |
| cpufreq_conservative | تقوم بالتبديل بين الترددات ديناميكياً عند وصول نسبة الحِمل على المعالج إلى 75% |
| cpufreq_powersave | تجعل المعالج يعمل بأدنى تردد |
| cpufreq_userspace | تجعل المعالج يعمل بالترددات التي يحددها المستخدم |

**Tip:** لمراقبة سرعة المعالج لحظياً قم بتنفيذ:
```
$ watch grep \"cpu MHz\" /proc/cpuinfo

```

#### عند استخدام cpupower

لتحميل وتفعيل مخطط معين يجب عليك تنفيذ:

```
# cpupower frequency-set -g <governor_without cpufreq_>

```

#### عند عدم استخدام cpupower

**Tip:** لتحميل مخطط أثناء إقلاع النظام نفذ التالي:
```
# echo <module> > /etc/modules-load.d/<module>

```

لتحميل مخطط معين نفذ:

```
# modprobe <governor>

```

### ضبط مخططات الطاقة (باستخدام cpupower)

**Tip:** قم بإضافة الأوامر التالية إلى `/etc/default/cpupower`، <percent> هي النسبة المئوية للحِمل على المعالج cpu load، <governor> هي مخطط cpupower.

لوضع عتبة (نقطة بداية) للصعود إلى تردد آخر:

```
# echo -n <percent> > /sys/devices/system/cpu/cpufreq/<governor>/up_threshold

```

لوضع عتبة (نقطة بداية) للنزول إلى تردد آخر:

```
# echo -n <percent> > /sys/devices/system/cpu/cpufreq/<governor>/down_threshold

```

#### معدل أخد العينات

يقوم مخطط الطاقة بتفحص إعدادات المعالج لضبطها من فترة لأخرى، والذي يقوم بتحديد تكرار هذه العملية هو معدل أخد العينات sampling rate، عامل `sampling_down_factor` الأكبر من 1 يحسن من الأداء وذلك بتخفيض السقف الأعلى للحِمل على المعالج وتركه يعمل بأعلى تردد ساعة نظراً للحِمل الكبير عليه، هذه العملية ليس لها تأثير على الأداء في حالة الترددات المنخفضة أو الحمولة المنخفضة. لقراءة قيمة معدل أخذ العينات (افتراضياً =1) قم بتنفيذ:

```
$ cat /sys/devices/system/cpu/cpufreq/ondemand/sampling_down_factor

```

لتغيير القيمة نفذ:

```
# echo -n <value> > /sys/devices/system/cpu/cpufreq/ondemand/sampling_down_factor

```

### تعيين الحد الأعلى والحد الأدنى للتردد

**ملاحظة:** يمكن تعيين مخطط الطاقة والحد الأعلى والأدنى للتردد من `/etc/default/cpupower`، للتعيين لنواة معالج واحدة فقط: `-c <core #>` حيث <clock_freq> هو تردد ساعة المعالج بالواحدات GHz أو MHz.

لضبط الحد الأعلى لتردد المعالج:

```
# cpupower frequency-set -u <clock_freq>

```

لضبط الحد الأدنى:

```
# cpupower frequency-set -d <clock_freq>

```

لتحديد تردد معين للمعالج:

```
# cpupower frequency-set -f <clock_freq>

```

## التفاعل مع حالات ACPI

قد يُعِد بعض المستخدمين مخططات تتبدل تلقائياً بحسب حالات ACPI المختلفة مثل توصيل شاحن الكهرباء أو غلق شاشة الحاسب المحمول laptop lid، سنعطي مثالاً سريعاً في الأسفل لكن من الجيد قراءة مقال كامل عن [acpid](/index.php/Acpid "Acpid").

إذا كانت حزمة [acpid](https://www.archlinux.org/packages/?name=acpid) مثبتة لديك فإنك ستجد قائمة بالحالات أو الوضعيات مسجلة في الملف `/etc/acpi/handler.sh`، على سبيل المثال لتبديل مخطط أداء المعالج من `performance` إلى `conservative` عند فصل شاحن الكهرباء وإعادة تبديل المخطط عند إعادة وصل الشاحن:

```
/etc/acpi/handler.sh

```

```
[...]

 ac_adapter)
     case "$2" in
         AC*)
             case "$4" in
                 00000000)
                     echo "conservative" >/sys/devices/system/cpu/cpu0/cpufreq/scaling_governor    
                     echo -n $minspeed >$setspeed
                     #/etc/laptop-mode/laptop-mode start
                 ;;
                 00000001)
                     echo "performance" >/sys/devices/system/cpu/cpu0/cpufreq/scaling_governor
                     echo -n $maxspeed >$setspeed
                     #/etc/laptop-mode/laptop-mode stop
                 ;;
             esac
         ;;
         *) logger "ACPI action undefined: $2" ;;
     esac
 ;;

[...]

```

## Privilege Granting Under GNOME

**ملاحظة:** قام مدير النظام systemd بتقديم الأداة logind التي تتعامل مع إجرائيات consolekit و policykit، الكود التالي في الأسفل لا يعمل، قم بتعديل العنصر <defaults> باستخدام logind في الملف /usr/share/polkit-1/actions/org.gnome.cpufreqselector.policy بما يتناسب مع احتياجاتك ومع كتيب polkit الإرشادي [[1]](http://www.freedesktop.org/software/polkit/docs/latest/polkit.8.html)

واجهة [GNOME](/index.php/GNOME "GNOME") لديها أداة جميلة لتبديل مخطط الطاقة governor بشكل سريع، لاستخدامها دون الحاجة لإدخال كلمة مرور الجذر root قم بإنشاء `/var/lib/polkit-1/localauthority/50-local.d/org.gnome.cpufreqselector.pkla` ومن ثم قم بإضافة الأسطر التالية فيه:

```
[org.gnome.cpufreqselector]
Identity=unix-user:USER
Action=org.gnome.cpufreqselector
ResultAny=no
ResultInactive=no
ResultActive=yes
```

قم بتغيير كلمة `USER` إلى اسم المستخدم لديك.

تشتمل حزمة [desktop-privileges](https://aur.archlinux.org/packages/desktop-privileges/) المتوفرة في مستودعات [AUR](/index.php/Arch_User_Repository "Arch User Repository") على ملف `.pkla` مشابه للملف السابق ولكن وظيفة هذا الملف هي السماح لكل المستخدمين في [المجموعة](/index.php/Users_and_groups "Users and groups") `power` بتبديل المخططات.

## أدوات وضعية الحاسب المحمول

إذا كنت تستخدم [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools") لحلول توفير الطاقة الأخرى فبإمكانك تركها لتُدير لك تردد المعالج، لعمل هذا الأمر يجب عليك إضافة التعريف المناسب إلى المجلد `/etc/modules.d/` (انظر إلى [#CPU frequency driver](#CPU_frequency_driver) في الأعلى) ومن ثم قم بالذهاب إلى الملف `/etc/laptop-mode/conf.d/cpufreq.conf` لتعيين مخططات الطاقة والتردد والسياسات أو الخطط، لن تحتاج إلى تحميل وحدات أو خدمات أخرى لضبط مخططات الطاقة أو لكيفية التعامل مع حالات ACPI، يرجى الاطلاع على [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools") لمزيد من التفاصيل.

## استكشاف الأخطاء وإصلاحها

الدقة الفعلية لهذه المقالة أو هذا القسم ما زالت قيد النقاش. السبب: الرجاء الاطلاع على أول مناقشة في القالب لرؤية شرح مختصر.

*   بعض التطبيقات مثل [ntop](/index.php/Ntop "Ntop") لا تستجيب بشكل جيد لتغيير التردد التلقائي، وفي هذه الحالة يمكن لـ ntop أن يسبب مشاكل في التجزئة وضياع الكثير من المعلومات والبيانات، كما أن مخطط `on-demand` لا يستطيع أن يرفع من تردد المعالج بسرعة عندما يكون التردد الحالي غير كافي لمعالجة حزم البيانات الواردة إلى واجهة مراقبة الشبكة monitored network interface.

*   في بعض المعالجات قد يكون الأداء ضعيفاً مع إعدادات مخطط `on-demand` الافتراضية (على سبيل المثال: ملفات الفيديو بصيغة فلاش لا تعمل بسلاسة أو تأثيرات النوافذ تكون مهتزة وغير ثابتة)، في هذه الحالة وبدلاً من تعطيل المخطط نهائياً لحل هذه المشكلة، يمكنك الزيادة من اندفاع التردد وذلك بتخفيض عتبة (نقطة بدء) الزيادة *up_threshold* لمتغير [sysctl](/index.php/Sysctl "Sysctl") لكل معالج على حدى.

قم بالاطلاع على [#Changing the on-demand governor's threshold](#Changing_the_on-demand_governor.27s_threshold).

*   في بعض الأحيان لا يعمل مخطط on-demand بأقصى تردد مُعين له ولكن بتردد أقل منه بقليل، تُحل هذه المشكلة بوضع قيمة أقصى تردد max_freq أعلى قليلاً من القيمة الحقيقية، على سبيل المثال: إذا كان مدى تردد المعالج بين 2.00 GHz و 3.00 GHz فإن وضع max_freq على 3.01 GHz سيكون جيداً.

*   بعض مجموعات تعاريف [ALSA](/index.php/ALSA "ALSA") وبعض كروت الصوت قد تواجه مشكلة تخطي المقاطع الصوتية عند التبديل بين ترددات المعالج، لحل هذه المشكلة يتوجب عليك أن تختار مخطط طاقة ثابت لا يغير من تردد المعالج.

### تقييد التردد من قبل BIOS

هناك بعض تكوينات CPU/BIOS تواجه صعوبة في رفع التردد إلى الحد الأقصى أو رفع التردد بشكل عام، هذه الصعوبة يكون سببها على الأرجح إجراءات BIOS التي تطلب من نظام التشغيل تقييد أقصى تردد يصل إليه المعالج مما يجعل الملف `/sys/devices/system/cpu/cpu0/cpufreq/bios_limit` يضبط قيمة أقصى تردد على قيمة أقل مما هي عليه.

أو قد يكون سبب هذه الصعوبة أنك قمت بضبط معين في أداة إعداد BIOS (التردد، إدارة الحرارة ... إلخ)، أو أن الـ BIOS قديمة أو بها أعطال، أو أن BIOS لديها أسباب خطيرة تجعلها تتحكم بتردد المعالج على طريقتها.

أسباب مثل هذه يمكن أن تحدث عند إزالة البطارية (على افتراض أن حاسوبك من النوع المحمول) أو أنها شبه فارغة أو متعطلة، وبالتالي سيعمل الحاسوب على شاحن الكهرباء فقط، في هذه الحالة فإن مقابس الكهرباء الضعيفة قد لا تتمكن من تزويد الكمية الكافية من الكهرباء لتلبية المتطلبات الكبيرة للنظام بأكمله (خاصة مع عدم وجود بطارية لكي تقوم بالمساعدة) مما يؤدي إلى ضياع في البيانات data أو تلفها أو في أسوأ الأحوال ضرر في العتاد الصلب hardware.

ليس كل أنواع BIOS تُقيد أو تحد من تردد المعالج، لكن على سبيل المثال أغلب IBM/Lenove Thinkpads تفعل ذلك، راجع [thinkpad related info on this topic](http://www.thinkwiki.org/wiki/Problem_with_CPU_frequency_scaling) لمزيد من المعلومات المتعلقة بـ Thinkpads.

إذا قمت بالمراجعة ولم تجد أي ضبط غريب أو مريب لـ BIOS وإذا كنت تعلم ما الذي تفعله فإنك تستطيع أن تجعل النواة kernel تتجاهل (ترفض) هذه الحدود التي وضعتها BIOS.

**تحذير:** تأكد من أنك قرأت وفهمت الجزء السابق، تقييد تردد المعالج CPU frequency limitation هي خاصية أمان لـ BIOS ويجب عدم التلاعب بها

لجعل النواة تتجاهل هذه الحدود يجب تمرير متغير خاص إلى وحدة المعالج، لتجربة هذا الأمر مؤقتاً قم بتغيير القيمة في الملف `/sys/module/processor/parameters/ignore_ppc` من `0` إلى `1`.

أما لجعل هذا التجاهل بشكل دائم قم بالاطلاع على [Kernel modules](/index.php/Kernel_modules#Configuration "Kernel modules") أو قم بإضافة `processor.ignore_ppc=1` إلى سطر إقلاع النواة أو قم بإنشاء:

 `/etc/modprobe.d/ignore_ppc.conf` 
```
# If the frequency of your machine gets wrongly limited by BIOS, this should help
options processor ignore_ppc=1
```