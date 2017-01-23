سيرشدك هذا المستند خلال عملية تثبيت [آرتش لينكس](/index.php/Arch_Linux_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9) "Arch Linux (العربية)") باستخدام [سكرِبتات تثبيت آرتش](https://projects.archlinux.org/arch-install-scripts.git/). قبل التثبيت، نَنصحُك بزيارة [الأسئلة الأكثر تكرارًا](/index.php/FAQ_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9) "FAQ (العربية)"). طالع [دليل المبتدئين](/index.php/Beginners%27_guide_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9) "Beginners' guide (العربية)") لدليل تثبيت مفصّل ومفسّر أكثر.

[ويكي آرتش](/index.php/Main_page_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9) "Main page (العربية)") الذي يشرف عليه المجتمع هو مورد ممتاز ويجب مراجعته للمشاكل أولًا. قناة [آي‌آر‌سي](https://en.wikipedia.org/wiki/IRC "wikipedia:IRC") ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux) )، و[المنتديات](https://bbs.archlinux.org/) متوفّران أيضًا للإجابة إن لم تحصل عليها من أي مكان آخر. أيضًا، تأكّد من مراجعة صفحات `man` لأي أمر تجده غريب، يمكن تنفيذ ذلك بسهولة عبر `man *الأمر*`.

## Contents

*   [1 التنزيل](#.D8.A7.D9.84.D8.AA.D9.86.D8.B2.D9.8A.D9.84)
*   [2 التثبيت](#.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA)
    *   [2.1 تخطيط لوحة المفاتيح](#.D8.AA.D8.AE.D8.B7.D9.8A.D8.B7_.D9.84.D9.88.D8.AD.D8.A9_.D8.A7.D9.84.D9.85.D9.81.D8.A7.D8.AA.D9.8A.D8.AD)
    *   [2.2 تقسيم الأقراص](#.D8.AA.D9.82.D8.B3.D9.8A.D9.85_.D8.A7.D9.84.D8.A3.D9.82.D8.B1.D8.A7.D8.B5)
    *   [2.3 تهيئة الأقسام](#.D8.AA.D9.87.D9.8A.D8.A6.D8.A9_.D8.A7.D9.84.D8.A3.D9.82.D8.B3.D8.A7.D9.85)
    *   [2.4 ضمّ الأقراص](#.D8.B6.D9.85.D9.91_.D8.A7.D9.84.D8.A3.D9.82.D8.B1.D8.A7.D8.B5)
    *   [2.5 الاتصال بالإنترنت](#.D8.A7.D9.84.D8.A7.D8.AA.D8.B5.D8.A7.D9.84_.D8.A8.D8.A7.D9.84.D8.A5.D9.86.D8.AA.D8.B1.D9.86.D8.AA)
        *   [2.5.1 الشبكة اللاسلكية](#.D8.A7.D9.84.D8.B4.D8.A8.D9.83.D8.A9_.D8.A7.D9.84.D9.84.D8.A7.D8.B3.D9.84.D9.83.D9.8A.D8.A9)
    *   [2.6 تثبيت أساس النظام](#.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_.D8.A3.D8.B3.D8.A7.D8.B3_.D8.A7.D9.84.D9.86.D8.B8.D8.A7.D9.85)
    *   [2.7 ضبط النظام](#.D8.B6.D8.A8.D8.B7_.D8.A7.D9.84.D9.86.D8.B8.D8.A7.D9.85)
    *   [2.8 تثبيت وضبط محمّل الإقلاع](#.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA_.D9.88.D8.B6.D8.A8.D8.B7_.D9.85.D8.AD.D9.85.D9.91.D9.84_.D8.A7.D9.84.D8.A5.D9.82.D9.84.D8.A7.D8.B9)
    *   [2.9 إزالة الضمّ وإعادة التشغيل](#.D8.A5.D8.B2.D8.A7.D9.84.D8.A9_.D8.A7.D9.84.D8.B6.D9.85.D9.91_.D9.88.D8.A5.D8.B9.D8.A7.D8.AF.D8.A9_.D8.A7.D9.84.D8.AA.D8.B4.D8.BA.D9.8A.D9.84)
*   [3 ما بعدَ التثبيت](#.D9.85.D8.A7_.D8.A8.D8.B9.D8.AF.D9.8E_.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA)
    *   [3.1 إدارة المستخدمين](#.D8.A5.D8.AF.D8.A7.D8.B1.D8.A9_.D8.A7.D9.84.D9.85.D8.B3.D8.AA.D8.AE.D8.AF.D9.85.D9.8A.D9.86)
    *   [3.2 إدارة الحزم](#.D8.A5.D8.AF.D8.A7.D8.B1.D8.A9_.D8.A7.D9.84.D8.AD.D8.B2.D9.85)
    *   [3.3 إدارة الخدمات](#.D8.A5.D8.AF.D8.A7.D8.B1.D8.A9_.D8.A7.D9.84.D8.AE.D8.AF.D9.85.D8.A7.D8.AA)
    *   [3.4 الصوت](#.D8.A7.D9.84.D8.B5.D9.88.D8.AA)
    *   [3.5 تعريف الفيديو](#.D8.AA.D8.B9.D8.B1.D9.8A.D9.81_.D8.A7.D9.84.D9.81.D9.8A.D8.AF.D9.8A.D9.88)
    *   [3.6 خادم العرض](#.D8.AE.D8.A7.D8.AF.D9.85_.D8.A7.D9.84.D8.B9.D8.B1.D8.B6)
    *   [3.7 الخطوط](#.D8.A7.D9.84.D8.AE.D8.B7.D9.88.D8.B7)
*   [4 ملحق](#.D9.85.D9.84.D8.AD.D9.82)

## التنزيل

نزّل صورة ISO الجديدة لآرتش لينكس من [صفحة تنزيل آرتش لينكس](https://www.archlinux.org/download/).

*   الصورة الموفّرة يمكن إقلاعها من نظامي الإقلاع i686 و x86_64 لتثبيت آرتش لينكس عبر الشبكة. الوسيط الذي يحوي مستودع [core] لم يعد متوفّرًا الآن.
*   الصور موقّع عليها، لذا ينصح بشِدّة التحقق من التوقيع قبل استخدامها: يمكن فعل ذلك بتنزيل ملف ".sig" من صفحة التنزيل (أو واحد من المرايا المُسردة هناك) إلى نفس الدليل كملف ".iso" واستخدام `pacman-key -v *iso-file*.sig`.
*   يمكن حرق الصورة على اسطوانة CD، ضَمّ ملف ISO، أو [كتابته إلى عصا USB](/index.php/USB_Installation_Media_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9) "USB Installation Media (العربية)") مباشرةً. تحتاج إلى الصورة فقط للتثبيتات الجديدة، في حال وجود نظام آرتش لينكس مسبقًا، يمكنك تحديثه عبر `pacman -Syu`.

## التثبيت

### تخطيط لوحة المفاتيح

هناك خرائط مناسبة للمفاتيح للعديد من الدول وأنواع لوحة المفاتيح، ويمكن لأمر مثل `loadkeys uk` فعل ما تريد. يمكن العثور على خرائط مفاتيح أخرى في `/usr/share/kbd/keymaps/` (يمكنك تجاهل مسار خريطة مفاتيح وامتداد الملف عندما تستعمل `loadkeys`).

### تقسيم الأقراص

طالع [التقسيم](/index.php/Partitioning_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9) "Partitioning (العربية)") للتفاصيل.

إن أردت إنشاء أي أجهزة كتلية مكدّسة لـ [LVM](/index.php/LVM "LVM")، [disk encryption](/index.php/Disk_encryption "Disk encryption") أو [RAID](/index.php/RAID "RAID")، قم بذلك الآن.

### تهيئة الأقسام

طالع [أنظمة الملفات](/index.php/File_systems#Step_2:_create_the_new_file_system "File systems") للتفاصيل.

إن كنت تستعمل ‎(U)EFI، ستحتاج غالبًا إلى قسم آخر لاستضافة قسم نظام UEFI. اقرأ [إنشاء قسم نظام UEFI في لينكس](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface").

### ضمّ الأقراص

علينا الآن ضمّ قسم الجذر على `/mnt`. عليك أيضًا إنشاء أدلة لضمّ بقيّة الأقسام (في حال أردتها) (`/mnt/boot`، `/mnt/home`، ...) وضُمّ قسم [التبديل](/index.php/Swap "Swap") لديك إن أردت أن يكتشفهم `genfstab`.

### الاتصال بالإنترنت

خدمة DHCP ممكّنة افتراضيًّا لكل الأجهزة المتوفّرة. إن احتجت إلى إعداد عنوان IP ثابت أو استخدام أدوات إدارة مثل [Netctl](/index.php/Netctl "Netctl")، عليك إيقاف هذه الخدمة أولًا: `systemctl stop dhcpcd.service`. لمعلوماتٍ أكثر، قم بقراءة [configuring network](/index.php/Configuring_network "Configuring network").

#### الشبكة اللاسلكية

شغّل `wifi-menu` لإعداد الشبكة اللاسلكية لديك. للتفاصيل، طالع [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") و [Netctl](/index.php/Netctl "Netctl").

### تثبيت أساس النظام

قبل التثبيت، قد ترغب في تحرير `/etc/pacman.d/mirrorlist` لوضع [المرآة](/index.php/Mirrors "Mirrors") المفضّلة لديك في الأعلى. ستُنسخ نسخة من قائمة المرايا هذه على نظامك الجديد عبر `pacstrap` كذلك، لذلك عليك القيام بذلك لأنه يستحقّ.

باستخدام السكرِبت [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) سنثبّت أساس النظام.

```
# pacstrap /mnt base

```

يمكن تثبيت حزم أخرى بإضافة أسمائها إلى الأمر أعلاه (مفصولة بفواصل)، متضمّنة محمّل الإقلاع إن أردته.

### ضبط النظام

*   ولّد [fstab](/index.php/Fstab_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9) "Fstab (العربية)") بالأمر التالي (إن كنت تفضّل استخدام UUIDs أو الملصقات، أضف الخيار `-U` أو `-L`، بالترتيب):

	 `# genfstab -p /mnt >> /mnt/etc/fstab` 

*   [غيّر الجذر](/index.php/Chroot "Chroot") إلى نظامنا المثبّت الجديد:

	 `# arch-chroot /mnt` 

*   اكتب اسمَ مضيفكَ إلى `/etc/hostname`.

*   أوصِل `/etc/localtime` رمزيًّا إلى `/usr/share/zoneinfo/Zone/SubZone`. استبدل `Zone` و `Subzone` إلى your liking. مثلًا:

	 `# ln -s /usr/share/zoneinfo/Europe/Athens /etc/localtime` 

*   أزل التعليق عن المحليّة المحدّدة في `/etc/locale.gen` وولّدها عبر `locale-gen`.
*   عيّن تفضيلات [المحليّة](/index.php/Locale#Setting_the_system_locale "Locale") في `/etc/locale.conf`.
*   أضف [خريطة مفاتيح الطرفية](/index.php/KEYMAP "KEYMAP") وتفضيلات [الخط](/index.php/Fonts#Console_fonts "Fonts") في `/etc/vconsole.conf`
*   اضبط `/etc/mkinitcpio.conf` كما تحتاجه (طالع [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")) وأنشئ قرص الذاكرة العشوائية الأولي عبر:

	 `# mkinitcpio -p linux` 

*   عيّن كلمة سر للجذر عبر `passwd`.
*   اضبط الشبكة مرةً أخرى للبيئة المثبّتة الجديدة. طالع [Network configuration](/index.php/Network_configuration "Network configuration") و [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration").

### تثبيت وضبط محمّل الإقلاع

يمكنك الاختيار بين [GRUB](/index.php/GRUB_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9) "GRUB (العربية)") أو [Syslinux](/index.php/Syslinux "Syslinux").

### إزالة الضمّ وإعادة التشغيل

إذا كنتَ لا تزال في بيئة chroot اطبع `exit` أو اضغط `Ctrl+D` للخروج منها. لقد ضممنا الأقسام سابقًا تحت `/mnt`. في هذه الخطوة سنزيل الضمّ عنهم:

```
# umount /mnt/{boot,home,}

```

أعد التشغيل الآن ولِج داخل نظامك الجديد بحساب الجذر.

## ما بعدَ التثبيت

### إدارة المستخدمين

أضف أيّ حسابات للمستخدمين التي تحتاجها إلى جانب الجذر، كما هو مشروح في [إدارة المستخدمين](/index.php/Users_and_groups#User_management "Users and groups"). ليست عادةً جيّدة لاستخدام حساب الجذر للاستخدام العادي، أو كشفهِ خلال [SSH](/index.php/SSH "SSH") على خادم. يجب استخدام حساب الجذر فقط للمهام الإدارية.

### إدارة الحزم

طالع [pacman](/index.php/Pacman_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9) "Pacman (العربية)") و [إدارة الحزم](/index.php/FAQ_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9)#.D8.A5.D8.AF.D8.A7.D8.B1.D8.A9_.D8.A7.D9.84.D8.AD.D8.B2.D9.85 "FAQ (العربية)") للإجابات حول تثبيت، تحديث وإدارة الحزم.

### إدارة الخدمات

تستخدم آرتش لينكس [systemd](/index.php/Systemd "Systemd") كمُمهِّد (init)، الذي يكون مدير نظام وخدمات لِلينكس. لصيانة تثبيت آرتش لينكس لديك، ستكون فكرة جيّدة أن تتعلّم الأساسيات حولها. يتمّ التفاعل مع systemd بالأمر `systemctl`. اقرأ [الاستخدام الأوّلي لأداة systemctl](/index.php/Systemd_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9)#.D8.A7.D9.84.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_.D8.A7.D9.84.D8.A3.D9.88.D9.91.D9.84.D9.8A_.D9.84.D8.A3.D8.AF.D8.A7.D8.A9_systemctl "Systemd (العربية)") لمزيدٍ من المعلومات.

### الصوت

يعمل [ALSA](/index.php/ALSA "ALSA") غالبًا خارج نطاق الصندوق (out-of-the-box). تحتاج فقط إلى كتمه. ثبّت [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) (والذي يحتوي `alsamixer`) واتبع التعليمات [هذه](/index.php/Advanced_Linux_Sound_Architecture#Unmuting_the_channels "Advanced Linux Sound Architecture").

ALSA مضمّن أيضًا مع النواة وهو مستحسن. إن لم يعمل، فـ [OSS](/index.php/OSS "OSS") بديل موجود. إن احتجت متطلّبات صوت متقدّمة، ألقِ نظرةً على [Sound system](/index.php/Sound_system "Sound system") لنظرةٍ عامة على المقالات المختلفة.

### تعريف الفيديو

نواة لينكس تتضمّن تعريفات مفتوحة المصدر للفيديو وتدعم hardware accelerated framebuffers. على أية حال، دعم userland مطلوب لتسريع OpenGL و 2D في X11.

إن لم تكن تعرف أي chipset للفيديو موجودة على حاسوبك، نفّذ:

```
$ lspci | grep VGA

```

لتحصل على قائمة كاملة من التعريفات مفتوحة المصدر للفيديو، ابحث في قاعدة بيانات الحزم.

```
$ pacman -Ss xf86-video | less

```

التعريف `vesa` هو تعريف generic mode-setting يعمل مع أغلب وحدات معالجة الرسوميات (GPU)، ولكن لا يوفّر أي تسريع ثنائي أو ثلاثي الأبعاد. إن لم تعثر على تعريف أفضل أو فشل تحميله، , Xorg سيرجع إلى vesa. لتثبيته:

```
# pacman -S xf86-video-vesa

```

لكي يعمل تسريع الفيديو، وأحيانًا لكشف كل الأوضاع التي يمكن لوحدة معالجة الرسوميات تعيينها، ستحتاج إلى تعريف فيديو مناسب:

| الصنف | النوع | التعريف | حزمة [Multilib](/index.php/Multilib "Multilib")
(for 32-bit applications on Arch x86_64) | التوثيق |
| **AMD/ATI** | مفتوح المصدر | [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) | [lib32-ati-dri](https://www.archlinux.org/packages/?name=lib32-ati-dri) | [ATI](/index.php/ATI "ATI") |
| مملوك | [catalyst-dkms](https://aur.archlinux.org/packages/catalyst-dkms/) | [lib32-catalyst-utils](https://aur.archlinux.org/packages/lib32-catalyst-utils/) | [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst") |
| **Intel** | مفتوح المصدر | [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) | [lib32-intel-dri](https://www.archlinux.org/packages/?name=lib32-intel-dri) | [Intel graphics](/index.php/Intel_graphics "Intel graphics") |
| **Nvidia** | مفتوح المصدر | [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) | [lib32-nouveau-dri](https://www.archlinux.org/packages/?name=lib32-nouveau-dri) | [Nouveau](/index.php/Nouveau "Nouveau") |
| [xf86-video-nv](https://aur.archlinux.org/packages/xf86-video-nv/) | – | (تعريف أثري (قديم)) |
| مملوك | [nvidia](https://www.archlinux.org/packages/?name=nvidia) | [lib32-nvidia-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-utils) | [NVIDIA](/index.php/NVIDIA "NVIDIA") |
| [nvidia-304xx](https://www.archlinux.org/packages/?name=nvidia-304xx) | [lib32-nvidia-304xx-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-304xx-utils) |

### خادم العرض

خادم العرض إكس (معروفٌ بـ X11 أو X) هو ميفاق (protocol) الشبكات والعرض، والذي يوفّر إنشاء النوافذ على عروض نقطية. إنّه المعيار الواقعيّ لإنجاز واجهات المستخدم الرسومية. طالع المقالة [Xorg](/index.php/Xorg "Xorg") للتفاصيل.

[Wayland](/index.php/Wayland "Wayland") ميفاق خادم عرض جديد ومرجع إنجاز ويستون متوفّر. هناك القليل من الدعم للتطبيقات لهذه المرحلة المبكّرة من التطوير.

### الخطوط

قد ترغب في تثبيت مجموعة خطوط TrueType؛ بسبب تضمين الخطوط النقطية غير القابلة للتحجيم افتراضيًّا. DejaVu مجموعة من الجودة العالية، بخطوط للأغراض العامة بتغطية [يونيكود](https://en.wikipedia.org/wiki/Unicode "wikipedia:Unicode") جيّدة:

```
# pacman -S ttf-dejavu

```

ارجع إلى [Font configuration](/index.php/Font_configuration "Font configuration") لكيفية ضبط تصيير (rendering) الخطوط و [Fonts](/index.php/Fonts "Fonts") لاقترحات للخطوط وتعليمات التثبيت.

## ملحق

لقائمةٍ من التطبيقات المفيدة، طالع [قائمة التطبيقات](/index.php/List_of_applications "List of applications").

طالع [التوصيات العامة](/index.php/General_recommendations "General recommendations") لدروس ما بعد التثبيت مثل إعداد لوحة اللمس أو تصيير الخطوط.