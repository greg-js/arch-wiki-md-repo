Related articles

*   [FAQ](/index.php/FAQ "FAQ")
*   [Installation guide](/index.php/Installation_guide "Installation guide")
*   [List of applications](/index.php/List_of_applications "List of applications")

This document is an annotated index of popular articles and important information for improving and adding functionalities to the installed Arch system. Readers are assumed to have read and followed the [Installation guide](/index.php/Installation_guide "Installation guide") to obtain a basic Arch Linux installation. Having read and understood the concepts explained in [#System administration](#System_administration) and [#Package management](#Package_management) is *required* for following the other sections of this page and the other articles in the wiki.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 إدارة النظام](#إدارة_النظام)
    *   [1.1 المستخدمون والمجموعات](#المستخدمون_والمجموعات)
    *   [1.2 تصعيد الامتيازات](#تصعيد_الامتيازات)
    *   [1.3 إدارة الخدمات](#إدارة_الخدمات)
    *   [1.4 صيانة النظام](#صيانة_النظام)
*   [2 إدارة الحزم](#إدارة_الحزم)
    *   [2.1 باكمان](#باكمان)
    *   [2.2 المستودعات](#المستودعات)
    *   [2.3 المرايا](#المرايا)
    *   [2.4 نظام بناء آرتش](#نظام_بناء_آرتش)
    *   [2.5 مخزن مستخدمي آرتش](#مخزن_مستخدمي_آرتش)
*   [3 الإقلاع](#الإقلاع)
    *   [3.1 التمييز الآلي للعتاد](#التمييز_الآلي_للعتاد)
    *   [3.2 Microcode](#Microcode)
    *   [3.3 الاحتفاظ برسائل الإقلاع](#الاحتفاظ_برسائل_الإقلاع)
    *   [3.4 Num Lock activation](#Num_Lock_activation)
*   [4 واجهة المستخدم الرسومية](#واجهة_المستخدم_الرسومية)
    *   [4.1 خادوم العرض](#خادوم_العرض)
    *   [4.2 تعريفات العرض](#تعريفات_العرض)
    *   [4.3 بيئات سطح المكتب](#بيئات_سطح_المكتب)
    *   [4.4 مديرو النوافذ](#مديرو_النوافذ)
    *   [4.5 مدير العرض](#مدير_العرض)
*   [5 إدارة الطاقة](#إدارة_الطاقة)
    *   [5.1 أحداث ACPI](#أحداث_ACPI)
    *   [5.2 CPU frequency scaling](#CPU_frequency_scaling)
    *   [5.3 الحواسيب المحمولة](#الحواسيب_المحمولة)
    *   [5.4 التعليق والإسبات](#التعليق_والإسبات)
*   [6 الوسائط المتعددة](#الوسائط_المتعددة)
    *   [6.1 الصوت](#الصوت)
    *   [6.2 ملحقات المتصفحات](#ملحقات_المتصفحات)
    *   [6.3 المرامز](#المرامز)
*   [7 ربط الشبكات](#ربط_الشبكات)
    *   [7.1 مزامنة الساعة](#مزامنة_الساعة)
    *   [7.2 أمان DNS](#أمان_DNS)
    *   [7.3 إعداد جدار ناري](#إعداد_جدار_ناري)
    *   [7.4 مشاركة الموارد](#مشاركة_الموارد)
*   [8 أجهزة الدخل](#أجهزة_الدخل)
    *   [8.1 تخطيطات لوحة المفاتيح](#تخطيطات_لوحة_المفاتيح)
    *   [8.2 أزرار الفأرة](#أزرار_الفأرة)
    *   [8.3 لوحات اللمس في الحواسيب المحملة](#لوحات_اللمس_في_الحواسيب_المحملة)
    *   [8.4 TrackPoints](#TrackPoints)
*   [9 Optimization](#Optimization)
    *   [9.1 Benchmarking](#Benchmarking)
    *   [9.2 تحسين الآداء](#تحسين_الآداء)
    *   [9.3 Solid state drives](#Solid_state_drives)
*   [10 حدمات النظام](#حدمات_النظام)
    *   [10.1 فهرسة الملفات والبحث](#فهرسة_الملفات_والبحث)
    *   [10.2 نوصيل البريد المحلي](#نوصيل_البريد_المحلي)
    *   [10.3 الطباعة](#الطباعة)
*   [11 المظهر](#المظهر)
    *   [11.1 الخطوط](#الخطوط)
    *   [11.2 GTK+ and Qt themes](#GTK+_and_Qt_themes)
*   [12 تحسينات الكونسول](#تحسينات_الكونسول)
    *   [12.1 Tab-completion enhancements](#Tab-completion_enhancements)
    *   [12.2 Aliases](#Aliases)
    *   [12.3 الصدفات البديلة](#الصدفات_البديلة)
    *   [12.4 إضافات باش](#إضافات_باش)
    *   [12.5 الخرج الملون](#الخرج_الملون)
    *   [12.6 الملفات المضغوطة](#الملفات_المضغوطة)
    *   [12.7 محثّ الكونسول](#محثّ_الكونسول)
    *   [12.8 Emacs shell](#Emacs_shell)
    *   [12.9 دعم الفأرة](#دعم_الفأرة)
    *   [12.10 Scrollback buffer](#Scrollback_buffer)
    *   [12.11 إدارة الجلسة](#إدارة_الجلسة)

## إدارة النظام

يتعامل هذا الجزء مع المهام الإدارية وإدارة النظام. للمزيد، فضلًا طالع [Core utilities](/index.php/Core_utilities "Core utilities") و [Category:System administration](/index.php/Category:System_administration "Category:System administration").

### المستخدمون والمجموعات

يتركك التثبيت الجديد مع حساب [ذو امتيازات كاملة](https://en.wikipedia.org/wiki/Superuser "wikipedia:Superuser") فقط، يسمى حساب «الجذر». Logging in as root for prolonged periods of time, possibly even exposing it via [SSH](/index.php/SSH "SSH") on a server, [is insecure](https://apple.stackexchange.com/questions/192365/is-it-ok-to-use-the-root-user-as-a-normal-user/192422#192422). بدلًا من ذلك، يجب عليك إنشاء حسابات محدودة الامتيازات واستعمالها لمعظم المهام, only using the root account for system administration. See [Users and groups#User management](/index.php/Users_and_groups#User_management "Users and groups") for details.

Users and groups are a mechanism for *access control*; administrators may fine-tune group membership and ownership to grant or deny users and services access to system resources. Read the [Users and groups](/index.php/Users_and_groups "Users and groups") article for details and potential security risks.

### تصعيد الامتيازات

كلا الأمرين [su](/index.php/Su_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9) "Su (العربية)") و [sudo](/index.php/Sudo "Sudo") يسمحان لك بتنفيذ أوامر باسم مستخدم آخر. يدخلك *su* مبدئيا إلى صدفة ولوج باسم المستخدم الجذر، و *sudo* مبدئيا يمنجك مؤقتا امتيازات الجذر لأمر واحد. طالع مقالتيهما الخاصتين لمعرفة الفروق.

### إدارة الخدمات

Arch Linux uses [systemd](/index.php/Systemd "Systemd") as the [init](/index.php/Init "Init") process, which is a system and service manager for Linux. For maintaining your Arch Linux installation, it is a good idea to learn the basics about it. Interaction with *systemd* is done through the *systemctl* command. Read [systemd#Basic systemctl usage](/index.php/Systemd#Basic_systemctl_usage "Systemd") for more information.

### صيانة النظام

Arch is a rolling release system and has rapid package turnover, so users have to take some time to do [system maintenance](/index.php/System_maintenance "System maintenance"). Read [Security](/index.php/Security "Security") for recommendations and best practices on hardening the system.

## إدارة الحزم

This section contains helpful information related to package management. For more, please see [FAQ#Package management](/index.php/FAQ#Package_management "FAQ") and [Category:Package management](/index.php/Category:Package_management "Category:Package management").

**Note:** It is imperative to keep up to date with changes in Arch Linux that require manual intervention **before** upgrading your system. Subscribe to the [arch-announce mailing list](https://mailman.archlinux.org/mailman/listinfo/arch-announce/) or check the front page [Arch news](https://www.archlinux.org/) every time before you update. Alternatively, you may find it useful to subscribe to [this RSS feed](https://www.archlinux.org/feeds/news/).

### باكمان

[باكمان](/index.php/Pacman_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9) "Pacman (العربية)") هو مدير حزم آرتش لينكس: يجب على كل المستخدمين أن يألفوه قبل قراءة مقال آخر.

طالع [pacman/Tips and tricks](/index.php/Pacman/Tips_and_tricks "Pacman/Tips and tricks") لاقتراحات حول كيفية تحسن تفاعلك مع *باكمان* وإدارة الحزم عموما.

### المستودعات

طالع مقالة [Official repositories](/index.php/Official_repositories "Official repositories") لتفاصيل عن الغرض من كل مستودع مُصان رسميا.

إن كنت عازمًا على استعمال تطبيقات ذات 32 بتة، فستحتاج إلى تفعيل المستودع [multilib](/index.php/Multilib "Multilib").

تسرد المقالة [Unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories") مستودعات أخرى عديدة غير مدعومة.

You may consider installing the [pkgstats](/index.php/Pkgstats "Pkgstats") service.

### المرايا

Visit the [Mirrors](/index.php/Mirrors "Mirrors") article for steps on taking full advantage of using the fastest and most up to date mirrors of the official repositories. As explained in the article, a particularly good advice is to routinely check the [Mirror Status](https://www.archlinux.org/mirrors/status/) page for a list of mirrors that have been recently synced.

### نظام بناء آرتش

*Ports* is a system initially used by BSD distributions consisting of build scripts that reside in a directory tree on the local system. Simply put, each port contains a script within a directory intuitively named after the installable third-party application.

The [Arch Build System](/index.php/Arch_Build_System "Arch Build System") offers the same functionality by providing build scripts called [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD"), which are populated with information for a given piece of software; integrity hashes, project URL, version, license and build instructions. These PKGBUILDs are parsed by [makepkg](/index.php/Makepkg "Makepkg"), the actual program that generates packages that are cleanly manageable by *pacman*.

Every package in the repositories along with those present in the AUR are subject to recompilation with *makepkg*.

### مخزن مستخدمي آرتش

While the Arch Build System allows the ability of building software available in the official repositories, the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") (AUR) is the equivalent for user submitted packages. It is an unsupported repository of build scripts accessible through the [web interface](https://aur.archlinux.org/) or through the [Aurweb RPC interface](/index.php/Aurweb_RPC_interface "Aurweb RPC interface").

## الإقلاع

This section contains information pertaining to the boot process. An overview of the Arch boot process can be found at [Arch boot process](/index.php/Arch_boot_process "Arch boot process"). For more, please see [Category:Boot process](/index.php/Category:Boot_process "Category:Boot process").

### التمييز الآلي للعتاد

Hardware should be auto-detected by [udev](/index.php/Udev "Udev") during the boot process by default. A potential improvement in boot time can be achieved by disabling module auto-loading and specifying required modules manually, as described in [Kernel modules](/index.php/Kernel_modules "Kernel modules"). Additionally, [Xorg](/index.php/Xorg "Xorg") should be able to auto-detect required drivers using `udev`, but users have the option to configure the X server manually too.

### Microcode

Processors may have [faulty behaviour](http://www.anandtech.com/show/8376/intel-disables-tsx-instructions-erratum-found-in-haswell-haswelleep-broadwelly), which the kernel can correct by updating the *microcode* on startup. See [Microcode](/index.php/Microcode "Microcode") for details.

### الاحتفاظ برسائل الإقلاع

Once it concludes, the screen is cleared and the login prompt appears, leaving users unable to gather feedback from the boot process. [Disable clearing of boot messages](/index.php/Disable_clearing_of_boot_messages "Disable clearing of boot messages") to overcome this limitation.

### Num Lock activation

Num Lock is a toggle key found in most keyboards. For activating Num Lock's number key-assignment during startup, see [Activating Numlock on Bootup](/index.php/Activating_Numlock_on_Bootup "Activating Numlock on Bootup").

## واجهة المستخدم الرسومية

This section provides orientation for users wishing to run graphical applications on their system. See [Category:Graphical user interfaces](/index.php/Category:Graphical_user_interfaces "Category:Graphical user interfaces") for additional resources.

### خادوم العرض

[Xorg](/index.php/Xorg "Xorg") هو تنفيذ عام ومفتوح المصدر لنظام النوافذ إكس ([X Window System](https://en.wikipedia.org/wiki/X_Window_System "wikipedia:X Window System")) (معروف باسم X11 أو X)، وهو مطلوب لتشغيل التطبيقات التي لها واجهات مستخدم رسومية (GUIs). معظم المستخدمين سيحتاجون إلى تثبيته.

[Wayland](/index.php/Wayland "Wayland") هو ميفاق بديل وأحدث لخادوم العرض، وتنفيذه المرجعي Weston متاح.

### تعريفات العرض

نعريف العرض المبدئي *vesa* سيعمل مع معظم بطاقات المرئيات، لكن يمكن تحسين الأداء بفرق واضح واستغلال الميزات الإضافية بتثبيت التعريف المناسب لمنتجات [ATI](/index.php/ATI "ATI") و [Intel](/index.php/Intel "Intel") و [NVIDIA](/index.php/NVIDIA "NVIDIA").

### بيئات سطح المكتب

رغم أن Xorg يوفر هيكلًا بسيطًا لبناء بيئات رسومية، فإن بعض المكونات الإضافية قد تعتبر ضرورية لإكمال تجربة المستخدم. [بيئات سطح المكتب](/index.php/Desktop_environment "Desktop environment") مثل [غنوم](/index.php/GNOME "GNOME") و[كدي](/index.php/KDE "KDE") و [LXDE](/index.php/LXDE "LXDE") و [Xfce](/index.php/Xfce "Xfce") تحزم طيفًا عريضًا من *عملاء X*، مثل مديري النوافذ، والألواح، ومديري الملفات، ومحاكيات الطرفية، ومحررات النص، والأيقونات، وبرامج نافعة أخرى. قد يريد المستخدمون الذين لديهم تجربة أقل أن يثبتوا بيئة سطح مكتب مألوفة أكثر. طالع [Category:Desktop environments](/index.php/Category:Desktop_environments "Category:Desktop environments") لموارد إضافية.

### مديرو النوافذ

A full-fledged desktop environment provides a complete and consistent graphical user interface, but tends to consume a considerable amount of system resources. Users seeking to maximize performance or otherwise simplify their environment may opt to install a [window manager](/index.php/Window_manager "Window manager") alone and hand-pick desired extras. Most desktop environments allow use of an alternative window manager as well. [Dynamic](/index.php/Category:Dynamic_WMs "Category:Dynamic WMs"), [stacking](/index.php/Category:Stacking_WMs "Category:Stacking WMs"), and [tiling](/index.php/Category:Tiling_WMs "Category:Tiling WMs") window managers differ in their handling of window placement.

### مدير العرض

Most desktop environments include a [display manager](/index.php/Display_manager "Display manager") for automatically starting the graphical environment and managing user logins. Users without a desktop environment can install one separately. Alternatively you may [start X at login](/index.php/Start_X_at_login "Start X at login") as a simple alternative to a display manager.

## إدارة الطاقة

هذا القسم لأصحاب الحواسيب المحمولة أو المستخدمين الذين يبحثون عن التحكم بإدارة الطاقة. رجاء طالع [Category:Power management](/index.php/Category:Power_management "Category:Power management") للمزيد.

طالع [إدارة الطاقة](/index.php/Power_management "Power management") لمقدمة أكثر عمومًا.

### أحداث ACPI

Users can configure how the system reacts to ACPI events such as pressing the power button or closing a laptop's lid. For the new (recommended) method using [systemd](/index.php/Systemd "Systemd"), see [Power management with systemd](/index.php/Power_management#Power_management_with_systemd "Power management"). For the old method, see [acpid](/index.php/Acpid "Acpid").

### CPU frequency scaling

Modern processors can decrease their frequency and voltage to reduce heat and power consumption. Less heat leads to more quiet system and prolongs the life of hardware. See [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling") for details.

### الحواسيب المحمولة

For articles related to portable computing along with model-specific installation guides, please see [Category:Laptops](/index.php/Category:Laptops "Category:Laptops"). For a general overview of laptop-related articles and recommendations, see [Laptop](/index.php/Laptop "Laptop").

### التعليق والإسبات

طالع المقالة الرئيسة: [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate").

## الوسائط المتعددة

[Category:Multimedia](/index.php/Category:Multimedia "Category:Multimedia") يحوي موارد إضافية.

### الصوت

[الصوت](/index.php/Sound "Sound") توفره تعاريف النواة للصوت:

*   [ALSA](/index.php/ALSA "ALSA") مضمن مع النواة ومنصوح به because usually it works out of the box (it just needs to be [unmuted](/index.php/Advanced_Linux_Sound_Architecture#Unmuting_the_channels "Advanced Linux Sound Architecture")).

*   [OSS](/index.php/OSS "OSS") is a viable alternative in case ALSA does not work.

Users may additionally wish to install and configure a [sound server](/index.php/Sound_system#Sound_servers "Sound system") such as [PulseAudio](/index.php/PulseAudio "PulseAudio"). For advanced audio requirements, see [professional audio](/index.php/Professional_audio "Professional audio").

### ملحقات المتصفحات

يمكن تثبيت [ملحقات متصفحات](/index.php/Browser_plugins "Browser plugins") مثل Adobe Acrobat Reader ومشغل الفلاش Adobe Flash Player والجافا للنفاذ إلى محتوى وب معين.

### المرامز

[Codecs](/index.php/Codecs "Codecs") are utilized by multimedia applications to encode or decode audio or video streams. In order to play encoded streams, users must ensure an appropriate codec is installed.

## ربط الشبكات

This section is confined to small networking procedures. Head over to [Network configuration](/index.php/Network_configuration "Network configuration") for a full guide. For more, please see [Category:Networking](/index.php/Category:Networking "Category:Networking").

### مزامنة الساعة

[Wikipedia:Network Time Protocol|Network Time Protocol]] (NTP) is a protocol for synchronizing the clocks of computer systems over packet-switched, variable-latency data networks. See [Time synchronization](/index.php/Time_synchronization "Time synchronization") for implementations of such protocol.

### أمان DNS

For better security while browsing web, paying online, connecting to [SSH](/index.php/SSH "SSH") services and similar tasks consider using [DNSSEC](/index.php/DNSSEC "DNSSEC")-enabled [DNS resolver](/index.php/DNS_resolver "DNS resolver") that can validate signed [DNS](https://en.wikipedia.org/wiki/Domain_Name_System "wikipedia:Domain Name System") records, and [DNSCrypt](/index.php/DNSCrypt "DNSCrypt") to encrypt DNS traffic.

### إعداد جدار ناري

A firewall can provide an extra layer of protection on top of the Linux networking stack. While the stock Arch kernel is capable of using [Netfilter](https://en.wikipedia.org/wiki/Netfilter "wikipedia:Netfilter")'s [iptables](/index.php/Iptables "Iptables") and [nftables](/index.php/Nftables "Nftables"), neither are enabled by default. It is highly recommended to set up some form of firewall. See [Category:Firewalls](/index.php/Category:Firewalls "Category:Firewalls") for available guides.

### مشاركة الموارد

To share files among the machines in a network, follow the [NFS](/index.php/NFS "NFS") or the [SSHFS](/index.php/SSHFS "SSHFS") article.

Use [Samba](/index.php/Samba "Samba") to join a Windows network. To configure the machine to use Active Directory for authentication, read [Active Directory integration](/index.php/Active_Directory_integration "Active Directory integration").

See also [Category:Network sharing](/index.php/Category:Network_sharing "Category:Network sharing").

## أجهزة الدخل

This section contains popular input device configuration tips. For more, please see [Category:Input devices](/index.php/Category:Input_devices "Category:Input devices").

### تخطيطات لوحة المفاتيح

Non-English or otherwise non-standard keyboards may not function as expected by default. The necessary steps to configure the keymap are different for virtual console and [Xorg](/index.php/Xorg "Xorg"), they are described in [Keyboard configuration in console](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") and [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg") respectively.

### أزرار الفأرة

Owners of advanced or unusual mice may find that not all mouse buttons are recognized by default, or may wish to assign different actions for extra buttons. Instructions can be found in [Mouse buttons](/index.php/Mouse_buttons "Mouse buttons").

### لوحات اللمس في الحواسيب المحملة

Many laptops use [Synaptics](https://www.synaptics.com/) or [ALPS](http://www.alps.com/) "touchpad" pointing devices. For these, and several other touchpad models, you can use either the Synaptics input driver or libinput; see [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") and [libinput](/index.php/Libinput "Libinput") for installation and configuration details.

### TrackPoints

See the [TrackPoint](/index.php/TrackPoint "TrackPoint") article to configure your TrackPoint device.

## Optimization

This section aims to summarize tweaks, tools and available options useful to improve system and application performance.

### Benchmarking

[Benchmarking](/index.php/Benchmarking "Benchmarking") is the act of measuring performance and comparing the results to another system's results or a widely accepted standard through a unified procedure.

### تحسين الآداء

The [Improving performance](/index.php/Improving_performance "Improving performance") article gathers information and is a basic rundown about gaining performance in Arch Linux.

### Solid state drives

The [Solid State Drives](/index.php/Solid_State_Drives "Solid State Drives") article covers many aspects of solid state drives, including configuring them to maximize their lifetimes.

## حدمات النظام

This section relates to [daemons](/index.php/Daemons "Daemons"). For more, please see [Category:Daemons](/index.php/Category:Daemons "Category:Daemons").

### فهرسة الملفات والبحث

Most distributions have a *locate* command available to be able to quickly search for files. To get this functionality in Arch Linux, [mlocate](https://www.archlinux.org/packages/?name=mlocate) is the recommended install. After the install you should run *updatedb* to index the filesystems.

[Desktop search engines](/index.php/List_of_applications/Utilities#File_searching "List of applications/Utilities") provide a similar service, while better integrated into [desktop environments](/index.php/Desktop_environment "Desktop environment").

### نوصيل البريد المحلي

A default setup does not provide a way to sync mail. To configure *Postfix* for simple local mailbox delivery, see [Postfix](/index.php/Postfix "Postfix"). Other options are [SSMTP](/index.php/SSMTP "SSMTP"), [msmtp](/index.php/Msmtp "Msmtp") and [fdm](/index.php/Fdm "Fdm").

### الطباعة

[CUPS](/index.php/CUPS "CUPS") is a standards-based, open source printing system developed by Apple. See [Category:Printers](/index.php/Category:Printers "Category:Printers") for printer-specific articles.

## المظهر

This section contains frequently-sought "eye candy" tweaks for an aesthetically pleasing Arch experience. For more, please see [Category:Eye candy](/index.php/Category:Eye_candy "Category:Eye candy").

### الخطوط

You may wish to install a set of TrueType fonts, as only unscalable bitmap fonts are included in a basic Arch system. There are several general-purpose [font families](/index.php/Fonts#Families "Fonts") providing large [Unicode](https://en.wikipedia.org/wiki/Unicode "wikipedia:Unicode") coverage and even [metric compatibility](/index.php/Metric-compatible_fonts "Metric-compatible fonts") with fonts from other operating systems.

A plethora of information on the subject can be found in the [Fonts](/index.php/Fonts "Fonts") and [Font configuration](/index.php/Font_configuration "Font configuration") articles.

If spending a significant amount of time working from the virtual console (i.e. outside an X server), users may wish to change the console font to improve readability; see [Linux console#Fonts](/index.php/Linux_console#Fonts "Linux console").

### GTK+ and Qt themes

A big part of the applications with a graphical interface for Linux systems are based on the [GTK+](/index.php/GTK%2B "GTK+") or the [Qt](/index.php/Qt "Qt") toolkits. See those articles and [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications") for ideas to improve the appearance of your installed programs and adapt it to your liking.

## تحسينات الكونسول

This section applies to small modifications that improve console programs' practicality. For more, please see [Category:Command shells](/index.php/Category:Command_shells "Category:Command shells").

### Tab-completion enhancements

It is recommended to properly set up extended [tab completion](https://en.wikipedia.org/wiki/Command-line_completion "wikipedia:Command-line completion") right away, as instructed in the article of your chosen shell.

### Aliases

Aliasing a command, or a group thereof, is a way of saving time when using the console. This is specially helpful for repetitive tasks that do not need significant alteration to their parameters between executions. Common time-saving aliases can be found in [Bash#Aliases](/index.php/Bash#Aliases "Bash"), which are easily portable to [zsh](/index.php/Zsh "Zsh") as well.

### الصدفات البديلة

[Bash](/index.php/Bash "Bash") is the shell that is installed by default in an Arch system. The live installation media, however, uses [zsh](/index.php/Zsh "Zsh") with the [grml-zsh-config](https://www.archlinux.org/packages/?name=grml-zsh-config) addon package. See [Command-line shell#List of shells](/index.php/Command-line_shell#List_of_shells "Command-line shell") for more alternatives.

### إضافات باش

A list of miscellaneous Bash settings, history search and [Readline](/index.php/Readline "Readline") macros is available in [Bash#Tips and tricks](/index.php/Bash#Tips_and_tricks "Bash").

### الخرج الملون

This section is covered in [Color output in console](/index.php/Color_output_in_console "Color output in console").

### الملفات المضغوطة

Compressed files, or archives, are frequently encountered on a GNU/Linux system. [Tar](/index.php/Tar "Tar") is one of the most commonly used archiving tools, and users should be familiar with its syntax (Arch Linux packages, for example, are simply xzipped tarballs). See [Archiving and compression](/index.php/Archiving_and_compression "Archiving and compression").

### محثّ الكونسول

The console prompt (PS1) can be customized to a great extent. See [Bash/Prompt customization](/index.php/Bash/Prompt_customization "Bash/Prompt customization") or [Zsh#Prompts](/index.php/Zsh#Prompts "Zsh") if using Bash or Zsh, respectively.

### Emacs shell

Emacs is known for featuring options beyond the duties of regular text editing, one of these being a full shell replacement. Consult [Emacs#Colored output issues](/index.php/Emacs#Colored_output_issues "Emacs") for a fix regarding garbled characters that may result from enabling colored output.

### دعم الفأرة

Using a mouse with the console for copy-paste operations can be preferred over [GNU Screen](/index.php/GNU_Screen "GNU Screen")'s traditional copy mode. Refer to [General purpose mouse](/index.php/General_purpose_mouse "General purpose mouse") for comprehensive directions. Note that you can already do this in [terminal emulators](/index.php/Terminal_emulator "Terminal emulator") with the [clipboard](/index.php/Clipboard "Clipboard").

### Scrollback buffer

To be able to save and view text which has scrolled off the screen, refer to [General troubleshooting#Scrollback](/index.php/General_troubleshooting#Scrollback "General troubleshooting").

### إدارة الجلسة

Using terminal multiplexers like [tmux](/index.php/Tmux "Tmux") or [GNU Screen](/index.php/GNU_Screen "GNU Screen"), programs may be run under sessions composed of tabs and panes that can be detached at will, so when the user either kills the terminal emulator, terminates [X](/index.php/X "X"), or logs off, the programs associated with the session will continue to run in the background as long as the terminal multiplexer server is active. Interacting with the programs requires reattaching to the session.