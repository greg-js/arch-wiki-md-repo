مدير النوافذ (WM) هو عنصر من الواجهة في نظام الرسومي للمستخدم (GUI). قد يفضل المستعمل تنصيب بيئة سطح المكتب كاملة, لأنها توفر واجهة كاملة , كالرموز والنوافذ وأشرطة الأدوات، وخلفيات، و مستلزمات سطح المكتب.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 نظام نوافذ إكس](#نظام_نوافذ_إكس)
*   [2 مدراء النوافذ](#مدراء_النوافذ)
    *   [2.1 الانواع](#الانواع)
*   [3 قائمة من مدراء النوافذ](#قائمة_من_مدراء_النوافذ)
    *   [3.1 مدراء النوافذ المرصوصة](#مدراء_النوافذ_المرصوصة)
    *   [3.2 مدراء النوافذ المبلطة](#مدراء_النوافذ_المبلطة)
    *   [3.3 مدراء النوافذ ديناميكية](#مدراء_النوافذ_ديناميكية)
*   [4 روابط خارجية](#روابط_خارجية)

## نظام نوافذ إكس

[نظام النافذة إكس](https://en.wikipedia.org/wiki/%D9%86%D8%B8%D8%A7%D9%85_%D8%A7%D9%84%D9%86%D8%A7%D9%81%D8%B0%D8%A9_%D8%A5%D9%83%D8%B3 "wikipedia:نظام النافذة إكس") يوفر الأساس لواجهة المستخدم الرسومية. قبل تثبيت مدير النوافذ، عليك اولا تثبيت خادم اكس. شاهد[Xorg](/index.php/Xorg "Xorg") لمعلومات أكثر.

	*يوفر الخادم إكس الإطار الأساسي، أو البدائي، لبناء البيئات و الواجهة الرسومية للمستخدم: رسم وتحريك النوافذ على الشاشة والتفاعل مع الماوس ولوحة المفاتيح. كلها تنجز بواسطة العميل او المعروف باسم مدير النوافذ فهو يقوم بهذه العمليات . إكس لا يفرض واجهة مستخدم معينة و على هذا النحو، فالتصاميم المرئية للبيئات سطح المكتب قائمة على الخادم إكس بشكل كبير، برامج مختلفة قد تقدم واجهات مختلفة جذريا لأنها تتعامل مباشرة مع الخادم .كما أن الخادم إكس تم تصميمه(كبرنامج)لديه طبقة إضافية في نواة نظام التشغيل تعمل بأولوية عالية.*

المستخدم حر في تكوين الواجهة الرسومية و بشتى الطرق.

## مدراء النوافذ

مدراء النوافذ (​WMS) عملاء للخادم إكس يتمثل عملهم في توفر الحدود حول النافذ . مدير النوافذ يسيطر على مظهر التطبيق وكيفية إدارته : كالحدود، شريط العناوين، والحجم، والقدرة على تغيير حجم الإطار . العديد من مديري النوافذ يتوفر على وظائف أخرى مثل أماكن للعصا [dockapps](http://dockapps.windowmaker.org/) مثل [Window Maker](/index.php/Window_Maker "Window Maker")، وقائمة لبدء تشغيل البرامج، والقوائم لتكوين WM وأشياء أخرى مفيدة.[Fluxbox](/index.php/Fluxbox "Fluxbox")، على سبيل المثال، لديه القدرة على تبويب النوافذ.

### الانواع

*   **مرصوص**(الملقب بالعائم)

مدير نوافذ تقليدي مستخدم في أنظمة التشغيل التجارية مثل وينداوز و ماك اواس . النوافذ فيه توضع كالورق فوق الطاولة ويمكن أن تكون مكدسة فوق بعضها البعض.

*   **تبليط**

او مدير نوافذ البلاط . هذا النوع تكون النوافذ فيه غير متداخلة . يستعمل عادة على النظم التي تعتمد على مفاتيح او الاقل استعمال للفأرة .في هذا المدير قد يكون العمل يدوي او يتم تجهيز تخطيط مسبق . او كليهما.

*   **ديناميكي**

هذا النوع من مدراء النوافذ يمكنه التبديل بشكل ديناميكي بين تبليط أو مرصوص .

شاهد [Comparison of tiling window managers](/index.php/Comparison_of_tiling_window_managers "Comparison of tiling window managers") و [Wikipedia:Comparison of X window managers](https://en.wikipedia.org/wiki/Comparison_of_X_window_managers "wikipedia:Comparison of X window managers") للمقارنة بين مدراء النوافذ.

## قائمة من مدراء النوافذ

### مدراء النوافذ المرصوصة

*   **[2bwm](/index.php/2bwm "2bwm")** — 2bwm هو مدير نوافذ مرصوص و سريع, مع خصوصية وجود 2 من الحدود , كتب على مكتبة XCB وهو مستمد من mcwm كتب بواسطة Michael Cardell. في 2bwm كل شيء يمكن الوصول إليه من لوحة المفاتيح لكن المؤشر يمكن إستعماله , تحجيم و اعلى/اسفل. تم تغيير اسمه مؤخرا من mcwm-beast الى 2bwm.

	[https://github.com/venam/2bwm](https://github.com/venam/2bwm) || [2bwm](https://aur.archlinux.org/packages/2bwm/)

*   **aewm** — aewm عصري, حد ادنى من مدير نوافذ صمم للخادم إكس.يتم التحكم فيه كليا بالماوس, ولكن لا يحتوي على واجهة مستخدم مرئية بصرف النظر عن أطر النوافذ. الاوامر فيه تصنف كالمحرر vi : تم تصميمه في بدايات (1997) ليكون سريع على الاجهزة المنخفضة الذاكرة,غير بديهي و غير مرن للمستخدمين الجدد , ولكن سريع وأنيق بطريقته الخاصة.

	[http://www.red-bean.com/decklin/aewm/](http://www.red-bean.com/decklin/aewm/) || [aewm](https://aur.archlinux.org/packages/aewm/) [غير معتمد]

*   **[AfterStep](https://en.wikipedia.org/wiki/AfterStep "wikipedia:AfterStep")** — AfterStep هو مدير نوافذ للخادم إكس على يونكس. في الأصل أساس على شكل ومظهر واجهة NeXTStep , هو متوفر للمستخدمين النهائيين ,سطح المكتب نظيف، وأنيق. الهدف من تطوير AfterStep هو توفير المرونة في تكوين سطح المكتب, تحسين الجماليات, والاستخدام الفعال لموارد النظام.

	[http://www.afterstep.org/](http://www.afterstep.org/) || [afterstep](https://aur.archlinux.org/packages/afterstep/) [غير معتمد]

*   **[Blackbox](https://en.wikipedia.org/wiki/Blackbox "wikipedia:Blackbox")** — Blackbox هو مدير نوافذ ,سريع و خفيف لنظام نوافذ إكس قد يكون ما تبحث عنه,من دون التبعيات المزعجة من المكتبات. Blackbox تم بناءه C++ ويحتوي على التعليمات البرمجية الأصلية لهذه اللغة (على الرغم من أن له اوامر رسومية مشابهة ل WindowMaker).

	[http://blackboxwm.sourceforge.net/](http://blackboxwm.sourceforge.net/) || [blackbox](https://www.archlinux.org/packages/?name=blackbox)

*   **[Compiz](/index.php/Compiz "Compiz")** — Compiz مدير تركيبي بستعمال OpenGL فهو يستعمل GLX_EXT_texture_from_pixmap لتوجيه النوافذ في المقدمة الى جسم نسيج . لديه نظام إضافات مرن وصمم ليعمل جيدا مع العديد من عتاد الغرافيك.

	[http://www.compiz.org/](http://www.compiz.org/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=compiz-core)</small>

*   **[Enlightenment](/index.php/Enlightenment "Enlightenment")** — Enlightenment هو ليس مدير نوافذ فقط للينكس / إكس او اي نظام اخر, ولكن أيضا مجموعة كاملة من المكتبات لمساعدتك في إنشاء واجهات المستخدم جميلة مع عمل أقل و نتائج كبيرة عوض عن الطريقة القديمة و المعانات مع الأدوات التقليدية,ناهيك عن وجود مدير نوافذ تقليدي.

	[http://www.enlightenment.org/](http://www.enlightenment.org/) || [enlightenment](https://www.archlinux.org/packages/?name=enlightenment)

*   **[evilwm](/index.php/Evilwm "Evilwm")** — مدير نوافذ القائمة الدنيا لخادم إكس. 'القائمة الدنيا' هنا لا يعني أنه فقير جدا ليكون صالحا للاستعمال - بل يعني أنه يغفل عن الكثير من الاشياء التي يفعلها مدراء النوافذ أخرى *-تجريبي-*.

	[http://www.6809.org.uk/evilwm/](http://www.6809.org.uk/evilwm/) || [evilwm](https://aur.archlinux.org/packages/evilwm/)

*   **[Fluxbox](/index.php/Fluxbox "Fluxbox")** — Fluxbox ​​هو مدير نافذة للخادم إكس تم بناءه على كود Blackbox 0.61.1 . هو خفيف جدا على الموارد وسهلة في التعامل معه لكن و حتى الآن غير كامل في الميزات لجعله سهل وسريع للغاية في سطح المكتب. صمم بلغة C++ وتحت رخصة MIT License.

	[http://www.fluxbox.org/](http://www.fluxbox.org/) || [fluxbox](https://www.archlinux.org/packages/?name=fluxbox)

*   **[Flwm](https://en.wikipedia.org/wiki/FLWM "wikipedia:FLWM")** — Flwm هو محاولة لجمع أفضل الأفكار التي تتوجد في العديد من مدراء النوافذ. الملامح و الكود الاساسي مستوحى من wm2 الذي صممه Chris Cannam.

	[http://flwm.sourceforge.net/](http://flwm.sourceforge.net/) || [flwm](https://aur.archlinux.org/packages/flwm/) [غير معتمد]

*   **[FVWM](/index.php/FVWM "FVWM")** — FVWM متوافق جدا مع ICCCM-compliantمدير نوافذ محاكي متعدد الأسطح لنظام النوافذ إكس . تطويره ناشط , و دعم ممتاز.

	[http://www.fvwm.org/](http://www.fvwm.org/) || [fvwm](https://www.archlinux.org/packages/?name=fvwm)

*   **[Goomwwm](/index.php?title=Goomwwm&action=edit&redlink=1 "Goomwwm (page does not exist)")** — Goomwwm مدير نوافذ ل إكس كتب بلغة C كمشروع في غرفة الابحاث. يدير النوافذ بأقل تخطيط , يستعمل لوحة المفاتيح لتحكم في الانتقال بين النوافذ كا, تحجيم, تحريك, توسيم, تبليط.و هو سريع, خفيف, غير مشروط, و متوافع كثيرا مع EWMH .

	[http://aerosuidae.net/goomwwm/](http://aerosuidae.net/goomwwm/) || [goomwwm](https://aur.archlinux.org/packages/goomwwm/) [غير معتمد]

*   **[Hackedbox](https://en.wikipedia.org/wiki/Hackedbox "wikipedia:Hackedbox")** — Hackedbox هو مدير نوافذ إكس و نسخة من Blackbox لكن اكثر تجريد . تم إزالة شريط الأدوات والشق. الهدف من Hackedbox ان يكون صغير و مدير نوافذ قابل للتغيير , مع عدم وجود سخامات. لا توجد خطط لإضافة أي وظيفة, فقط إصلاحات الشوائب وتحسينات السرعة كلما كان ذلك ممكنا.

	[http://scrudgeware.org/projects/Hackedbox/](http://scrudgeware.org/projects/Hackedbox/) || [hackedbox](https://aur.archlinux.org/packages/hackedbox/) [غير معتمد]

*   **[IceWM](/index.php/IceWM "IceWM")** — IceWMمدير نوافذ ل إكس .الهدف من IceWM السرعة, البساطة, وعدم المساس بما تعود عليه المستخدم .

	[http://www.icewm.org/](http://www.icewm.org/) || [icewm](https://www.archlinux.org/packages/?name=icewm)

*   **[JWM](/index.php/JWM "JWM")** — JWM مدير نوافذ للخادم إكس . JWM كتب بـ C ويستعمل فقط Xlib في اقل احتياجاته.

	[http://joewing.net/programs/jwm/](http://joewing.net/programs/jwm/) || [jwm](https://www.archlinux.org/packages/?name=jwm)

*   **Karmen** — Karmen مدير نوافذ ل إكس,كتبه Johan Veenhuizen. صمم ليعمل "يعمل فقط." لا يوجد ملف إعداد ولا يعتمد على مكتبة إلا Xlib. نموذج تركيز الإدخال هو نقر-ل-تركيز. Karmen يهدف للإنسجام مع ICCCM و EWMH .

	[http://karmen.sourceforge.net/](http://karmen.sourceforge.net/) || [karmen](https://aur.archlinux.org/packages/karmen/) [غير معتمد]

*   **[KWin](https://en.wikipedia.org/wiki/KWin "wikipedia:KWin")** — KWin, مدير النوافذ المعياري في KDE4, التكوين فيه مدمج من النسخة الاولى ,يجعل منه مدير تكوين كذلك. هذا يسمح لـ KWin بتوفير تأثيرات رسومية متقدمة, مشابها لـ Compiz,بينما يوفر أيضا جميع الميزات السابقة من إصدارات KDE (مثل التكامل الجيد مع بقية إصدارات KDE,قابلية التكوين المتقدم, معالجة قوية من الفاسقة التطبيقات / الأدوات, ألخ.).

	[http://techbase.kde.org/Projects/KWin](http://techbase.kde.org/Projects/KWin) || [kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/)

*   **lwm** — lwm مدير نوافذ لـ إكس قد لا ترغب في إستعماله . ليس هنالك إيقونات, لا شريط الازرار,لا ايقونات الدوكي,لا قوائم اساسية , لا شيئ : إذا كنت تريد هذا , فالبرامج الاخرى يمكن ان توفر لك مما سبق.لا يوجد قابلية للتخصيص: إذا كنت لا تريد هذا استعمل مدير نوافذ اخر.

	[http://www.jfc.org.uk/software/lwm.html](http://www.jfc.org.uk/software/lwm.html) || [lwm](https://www.archlinux.org/packages/?name=lwm)

*   **[Metacity](https://en.wikipedia.org/wiki/Metacity "wikipedia:Metacity")** — ليست هذه هي الصفحة الرئيسية لـ Metacity.لا تتواجد صفحة له. هذا هو نفس السبب عدم وجود شعار له : Metacity صغير و مستقر.

	[http://blogs.gnome.org/metacity/](http://blogs.gnome.org/metacity/) || [metacity](https://www.archlinux.org/packages/?name=metacity)

*   **[Mutter](https://en.wikipedia.org/wiki/Mutter_(window_manager) "wikipedia:Mutter (window manager)")** — مدير و مركب نوافذ لغنوم , مبني على Clutter, يستعمل OpenGL.

	[http://git.gnome.org/browse/mutter/](http://git.gnome.org/browse/mutter/) || [mutter](https://www.archlinux.org/packages/?name=mutter)

*   **[Openbox](/index.php/Openbox "Openbox")** — Openbox عالي التخصيص , الجيل القادم من مدراء النوافذ مع إمكانية التوسيع . النمط *box المرئي معروف جدا كأقل مظهر .يوفير عدد أكبر من الخيارات للمطورين . كما انه يملك توثيق كامل فيما يخص الثيم و المظهر.

	[http://openbox.org/wiki/Main_Page](http://openbox.org/wiki/Main_Page) || [openbox](https://www.archlinux.org/packages/?name=openbox)

*   **[pawm](/index.php/Pawm "Pawm")** — pawm مدير نوافذ للخادم إكس. هو ليس سطح مكتب و لا يقدم لك كومة ضخمة من الخيارات غير مجدية, فقط يقدم التسهيلات اللازمة لتشغيل التطبيقات ، كما انه سهل الاستخدام .

	[http://www.pleyades.net/pawm/](http://www.pleyades.net/pawm/) || [pawm](https://aur.archlinux.org/packages/pawm/)

*   **[PekWM](/index.php/PekWM "PekWM")** — pekwmمدير نوافذ يفتح مرة واحدة مبني على aewm++ , ولكن تطورت بما فيه الكفاية ليختلف عن aewm + + في جميع الاشياء . يحتوي على الكثير من الميزات الموسعة ,كتجميع النوافذ (شبيه لـ Ion, PWM, او Fluxbox), تخصيص اتوماتيكي, Xinerama, خطف المفاتيح مثل keychains, و اشياء اخرى.

	[http://www.pekwm.org/projects/pekwm](http://www.pekwm.org/projects/pekwm) || [pekwm](https://www.archlinux.org/packages/?name=pekwm)

*   **[Sawfish](/index.php/Sawfish "Sawfish")** — مدير نوافذ متوسع مكتوب بسكريبت لغة Lisp. الأمان جد منخفظ بالنسبة لمدراء النوافذ الأخرى .الهدف منه هو البساطة في إدارة النوافذ بطريقة سلسة وجذابة. كل الاوامر العالية المستوى تنادى بـ Lisp هذا لكي يكتسب القدرة على التوسع .

	[http://sawfish.wikia.com/wiki/Main_Page](http://sawfish.wikia.com/wiki/Main_Page) || [sawfish](https://aur.archlinux.org/packages/sawfish/) [غير معتمد]

*   **TinyWM** — TinyWM هو مدير نافذة صغيرة صنع كاتمرين في بساطته.. قد يكون مفيد في تعلم بعض أساسيات إنشاء مدير نوافذ. لأن ملفه المصدري يحتوي على حوالي 50 سطر C. هناك أيضا نسخة بايثون باستخدام python-xlib.

	[http://incise.org/tinywm.html](http://incise.org/tinywm.html) || [tinywm](https://aur.archlinux.org/packages/tinywm/) [غير معتمد]

*   **[twm](/index.php/Twm "Twm")** — twm مدير نوافذ لنظام إكس.يوفر شريط العناوين , تشكيل النوافذ ,عدة أشكال من إدارة الايقونات, وظائف معرفة من قبل المستخدم,إضغط-لـ-نوع و مؤشر يحركها تركيز لوحة المفاتيح, مفاتيح محدد من المستخدم لتحريك المؤشر.

	[http://cgit.freedesktop.org/xorg/app/twm/](http://cgit.freedesktop.org/xorg/app/twm/) || [xorg-twm](https://www.archlinux.org/packages/?name=xorg-twm)

*   **WindowLab** — WindowLab مدير نوافد صغير و بسيط من مصممي novel . يمكنه نقر-تركيز بدون رفع-تركيز, آلية تغيير حجم النافذة تسمح للتغيير واحد أو لعديد من حواف النوافذ في وقت واحد، يحتوي على قوائم مبتكرة تشترك في نفس الجزء من الشاشة مثل شريط المهام. يتم منع إطار أشرطة العناوين من الخروج من حافة الشاشة من خلال تقييد مؤشر الماوس، وعند الاقتضاء يتم تقييد المؤشر أيضا إلى شريط المهام / القوائم من أجل جعل عناصر القائمة سهل الوصول .

	[http://nickgravgaard.com/windowlab/](http://nickgravgaard.com/windowlab/) || [windowlab](https://aur.archlinux.org/packages/windowlab/)

*   **[Window Maker](/index.php/Window_Maker "Window Maker")** — Window Maker مدير نوافذ صمم خصيصا ليتوافق و يندمج مع سطح مكتب GNUstep . يستنسخ خواصه و النظرة الأنيقة من NEXTSTEP . سريع, غني بالمميزات, سهل الاعداد, وسهل الاستخدام. كما انه تطبيق حر, مع المساهمة في صنعه مبرمجين من جميع أنحاء العالم.

	[http://windowmaker.org/](http://windowmaker.org/) || [windowmaker](https://aur.archlinux.org/packages/windowmaker/)

*   **WM2** — wm2 مدير نوافذ للخادم إكس. ويوفر نمط غير عادي من الزخارف للنافذة مع وظائف أقل قدر يشعر مستعمله بالراحة . wm2 غير قابل للتخصيص , إلا إذا عدلت في كوده المصدري و أعدت بنائه,.

	[http://www.all-day-breakfast.com/wm2/](http://www.all-day-breakfast.com/wm2/) || [wm2](https://aur.archlinux.org/packages/wm2/)

*   **Xfwm** — مدير نوافذ Xfce يضع نافذة البرنامج في الشاشة ,يوفر زخارف نافذة جميل،, يدير مساحات العمل أو مكاتب افتراضية و يدعم الشاشات المتعدد اللمس. ويوفر مدير التركيب خاص به (من إضافة التركيب في X.Org ) شفافية وضلال. مدير نوافذ Xfce يوفر محرر لاختصارات لوحة المفاتيح للأوامر المحدد من المستعمل و ;وبرنامج تلاعبي للنوافذ ويوفر علب حوار للتعديل المتقدم.

	[http://www.xfce.org/projects/xfwm4/](http://www.xfce.org/projects/xfwm4/) || [xfwm4](https://www.archlinux.org/packages/?name=xfwm4)

### مدراء النوافذ المبلطة

**dswm** — dswm (مدير نوافذ الفضاء العميق )هو فرع من [Stumpwm](/index.php/Stumpwm "Stumpwm")

	[https://github.com/dss-project/dswm](https://github.com/dss-project/dswm) || [dswm](https://aur.archlinux.org/packages/dswm/) [غير معتمد]

*   **[Herbstluftwm](/index.php/Herbstluftwm "Herbstluftwm")** — herbstluftwm هو كتيب مدراء التبليط في الخادم إكس و مرجع يستعمل Xlib و Glib.ويستند تخطيطه على تقسم الإطار ألى إطار آخر ويمكن ملئ هذا الإطار بنافذة أو إطار اخر (شبيه i3/ musca). قد يحتوي الإطار (مساحة عمل أو سطح مكتب …) يكن التعديل فيه حتى وهو يعمل . كل عروة تحتوي على تخطيط خاصة بها. وتكون عروة لكل شاشة. عروة الشاشة لا تضمّن داخل عروة اخرى أي أنها رأس الشجرة (شبيه xmonad). يمكن تعديله حتى و هو يشتغل عبر نداء ipc من herbstclient. إذن ملف الإعدادات عبارة عن سكريب يشتغل عند بداية التشغيل. (شبيه wmii/ musca)

	[http://wwwcip.cs.fau.de/~re06huxa/herbstluftwm](http://wwwcip.cs.fau.de/~re06huxa/herbstluftwm) || [herbstluftwm-git](https://aur.archlinux.org/packages/herbstluftwm-git/) [unsupported]

*   **[Ion3](/index.php/Ion3 "Ion3")** — Ion مدير نوافذ تبليط صمم لمستعملي لوحة المفاتيح. هو احد مدراء “الموجة الجديدة" في بيئة اسطح المكاتب المبلطة (المدراء الاخرون يجارون LarsWM, مع اتباع نهج مختلف تماما) منذ مدة ولدت فئة كاملة من مدراء النوافذ المبلطة للخادم إكس – ولا احد منهم استطاع مجارات Ion من حيث الوضيفة. هذا الاخير يستعمل Lua لتضمين جميع الاعدادت .

	[http://tuomov.iki.fi/software](http://tuomov.iki.fi/software) || [ion3](https://aur.archlinux.org/packages/ion3/) [غير معتمد]

*   **[Notion](/index.php/Notion "Notion")** — Notion مدير نوافذ تبليط للخادم إكس يستعمل 'التبليط'.'التلسين'
    *   تبليط: تقسيم الشاشة الى مناطق 'تبليط'. كل نافذة تحتل منطقة, كل نافذة مكبرة لحجم المنطقة
    *   لسان: اللسان يمكن أن يحتوي على العديد من النوافذ - هنا تكون في حالة تلسين 'تلسين'
    *   ثابث: معظم النوافذ المبلطة تكون 'ديناميكية', هذا يعني انها تتحرك و تغير حجمها تلقائية حسب حجم البالط في حال فتح نافذة او اغلاق اخرى . . مفهوم، على النقيض من ذلك، التبليط لا يتغير تلقائيا .

	Notion فرع من Ion3.

	[http://notion.sf.net/](http://notion.sf.net/) || [notion](https://www.archlinux.org/packages/?name=notion)

*   **[Ratpoison](/index.php/Ratpoison "Ratpoison")** — Ratpoison هو مدير نوافذ بدون تبعيات للمكتبات الاخرى, لا يحتوي على مؤثرات, و لا تزيين لحدود النافذة. Ratpoison يتم تخصيصه عن طريق ملف نصي. شريط المعلومات في Ratpoison يختلف إلى حد ما، لأنه لا يظهر الا عند الحاجة. الخدمات و البرامج كلاهما يشتغل على شريط الإعلام. . Ratpoison لا يحتوي على شريط المهام.

	[http://www.nongnu.org/ratpoison/](http://www.nongnu.org/ratpoison/) || [ratpoison](https://www.archlinux.org/packages/?name=ratpoison)

*   **[Stumpwm](/index.php/Stumpwm "Stumpwm")** — Stumpwm مدير نوافذ لخادم إكس يستعمل لوحة المفاتيح اكثر كتب كامل بـ Lisp. مدير Stumpwm صمم ليكون قابل للتخصيص و حد أدنى بصريا. لا يملك معالم او متغيرات لتتغيير في خصائصه,لكن يمكن إعادة تخصيصه وإعادة تحميل أثناء تشغيل. ليس هناك تنسيق للنوافذ, لا ايقونات , لا ازرار, لا شريط المهام. شريط معلومات يمكن تعينه لإظهاره باستمرار أو عند الحاجة فقط.

	[http://www.nongnu.org/stumpwm/](http://www.nongnu.org/stumpwm/) || [stumpwm-git](https://aur.archlinux.org/packages/stumpwm-git/) [غير معتمد]

*   **[subtle](/index.php/Subtle "Subtle")** — subtle هو مدير نوافذ تبليط يدوي مع نهج مألوف بدلا من التبليط: افتراضيا ليس هناك تخطيط نموذجي,يتم وضع النوافذ في موقع (جاذبية)في شبكة مخصصة. يمكن للمستخدم تغيير الجاذبية لكل نافذة إما مباشرة أو بتغيير البيانات الموجودة في ملف الاعدادات. السيطرة بالماوس ولوحة المفاتيح فضلا عن شريط الحالة قابل للتمديد.

.

	[http://subforge.org/projects/subtle](http://subforge.org/projects/subtle) || [subtle](https://aur.archlinux.org/packages/subtle/)

*   **[WMFS](/index.php/WMFS "WMFS")** — WMFS (مدير النوافذ من الصفر) هو مدير نوافذ تبليط خفيف وقابل للتخصيص للخادم إكس . يمكن تخصيصه بملف الاعدادات الخاص به , يدعم Xft (FreeType) خطوط كذلك متوافق مع تلمحات مدير النوافذ الموسعة (EWMH) , Xinerama و Xrandr. WMFS يمكن توجيهه من اوامر Vi اي (ViWMFS).

	[https://github.com/xorg62/wmfs](https://github.com/xorg62/wmfs) || [wmfs](https://aur.archlinux.org/packages/wmfs/) [غير معتمد]

### مدراء النوافذ ديناميكية

*   **[awesome](/index.php/Awesome "Awesome")** — awesome عالي التخصيص ,الجيل الجديد من إطار مدراء النوافذ للخادم إكس.سريع جد, قابل للإمتداد ومرخص تحت GNU GPLv2 license. مخصص بـ Lua, لديه شريط المهام, شريط المعلومات, ومطلق تطبيقات. هناك توسعات متاحة له مكتوبة في Lua. يستعمل XCB عوض Xlib, مما قد يؤدي إلى زيادة سرعة. Awesome لديه ميزات أخرى أيضا, مثل البديل المبكر لعفريت المعلومات, نقر على اليمين لإظهار القائمة شبيه لمدير النوافذ *box , وأشياء اخرى كثيرة.

	[http://awesome.naquadah.org/](http://awesome.naquadah.org/) || [awesome](https://www.archlinux.org/packages/?name=awesome)

*   **[catwm](/index.php/Catwm "Catwm")** — catwm هو مدير نافذة صغيرة، حتى أبسط من dwm, كتب بـ C. يمكن تخصيصه عن طريق ملف config.h ثم تقوم إعادة ترجمته او تجميعه.

	[https://github.com/pyknite/catwm](https://github.com/pyknite/catwm) || [catwm-git](https://aur.archlinux.org/packages/catwm-git/) [غير معتمد]

*   **[dwm](/index.php/Dwm "Dwm")** — dwm هو مدير نوافذ ديناميكي للخادم إكس . يتحكم في النوافذ بالتبليط, الأحادية وتخطيطات العائمة.ويمكن تطبيق كافة التخطيطات بشكل ديناميكي, هو بيئة محسنة لإستخدام التطبيقات وتنفيذ المهام. لا يحتوي على شريط مهام و لا على طالق البرامج, مع أن القوائم مدمجة فيه بشكل جيد, و لأنه من نفس المؤلف. لا يحتوي على ملف نصي للتخصيص. التخصيص يكون عن طريق تحرير الكود المصدري المكتوب بـ C, يجب أن يترجم و يعاد تشغيله في كل مرة يتم تغييره.حجم البرنامج هو بالفعل في الحد خط المفروضة ذاتيا, وهو يحتاج الى المزيد من التطوير.

	[http://dwm.suckless.org/](http://dwm.suckless.org/) || [dwm](https://aur.archlinux.org/packages/dwm/)

*   **[echinus](/index.php/Echinus "Echinus")** — مدير نوافذ عائم / تبليط ,بسيط و خفيف يعمل تحت خادم إكس. إنطلق تطويره كفرع من dwm مع تسهيل التخصيص, echinus اصبح بمميزات كاملة مع توافقه مع EWMH . هو متوافق بشكل جيد مع EWMH في ما يخص الادوات/ شريط المهام, [ourico](https://aur.archlinux.org/packages/ourico/)

	[http://plhk.ru/echinus](http://plhk.ru/echinus) || [echinus](https://aur.archlinux.org/packages/echinus/) [غير معتمد]

*   **[euclid-wm](/index.php?title=Euclid-wm&action=edit&redlink=1 "Euclid-wm (page does not exist)")** — euclid-wm دير نوافذ عائم / تبليط ,بسيط و خفيف يعمل تحت خادم إكس,مع دعم تصغير النوافذ. ملف نصي للتحكم في المفاتيح الثابتة و التخصيص . انطلق تطويره كفرع من dwm مع سهولة التخصيص, اصبح بمميزات كاملة مع توافقه مع EWMH . هو متوافق بشكل جيد مع EWMH في ما يخص الادوات/ شريط المهام[ourico](https://aur.archlinux.org/packages/ourico/).

	[http://euclid-wm.sourceforge.net/index.php](http://euclid-wm.sourceforge.net/index.php) || [euclid-wm](https://aur.archlinux.org/packages/euclid-wm/) [غير معتمد]

*   **[i3](/index.php/I3 "I3")** — i3 هو مدير نوافذ تبليطي, كتب بالكامل من الصفر. i3 . تم إنشاء بسبب wmii, مدير النوافذ القديم لأن الاخير ، لا يقدم بعض الميزات الحديثة (تعدد الشاشات مجهز بشكل جيد مثلا)او لديه بعض الشوائب , لم يتم التقدم فيه منذ بعض الوقت، و ليس من السهل التغيير في الكود على الإطلاق(يفتقر لشفرة المصدر التعليقات / والوثائق ). اختلافات ملحوظة في مجالات الدعم متعدد الشاشات هذه الأسباب تركت المطورين يصنعون i3.

	[http://i3wm.org/](http://i3wm.org/) || [i3-wm](https://www.archlinux.org/packages/?name=i3-wm)

*   **[monsterwm](/index.php/Monsterwm "Monsterwm")** — خفيفة الوزن، صغيرة ولكن monsterous مدير نوافد بلاطي ديناميكي. يحاول مطوريه إبقائه صغيرة قدر الإمكان. الاسطر حاليا تحت 700 هذا مع ملف الاعداد . يوفر مجموعة من أربعة أنماط تخطيطة مختلفة (مكدس عمودي، كومة أسفل، وشبكة الأحادية / ملء الشاشة) هذا بشكل افتراضي، ولديه دعم وضع النافذة العائمة. ويتميز أيضا انه متعدد منابع الدعم.يتميز بأن كل سطح مكتب اإفتراضي له خصائص خاصة به. ويتم تعديله عن طريق تعديل ملف البرمجة المصدري و هو مكتوب بـ C، يجب أن يعاد ترجمته وإعادة تشغيله كل مرة يتم تغييره. هناك العديد من الرقع متاحة و مدعومة من المنبع، في شكل فروع مختلفة

.

	[https://github.com/c00kiemon5ter/monsterwm](https://github.com/c00kiemon5ter/monsterwm) || [monsterwm](https://aur.archlinux.org/packages/monsterwm/) [غير معتمد]

*   **[Musca](/index.php/Musca "Musca")** — مدير نوافذ ديناميكي بسيط ل إكس, مع ميزات رصدت من ratpoison و dwm. Musca يعمل كمدير نافذة تبليط افتراضيا.يحدد المستخدم كيفية تقسيم الشاشة إلى إطارات غير متداخلة, مع عدم وجود قيود على تخطيط. نوافذ التطبيق دائما تملء الإطار المسند إليها,مع استثناء من النوافذ الزائلة و علب الحوار التي تطفو فوق التطبيق الأم بالحجم المناسب. فتطبيقات لا تغيير الإطارات إلا إذا طلبت ذلك.

	[http://aerosuidae.net/musca.html](http://aerosuidae.net/musca.html) || [musca](https://aur.archlinux.org/packages/musca/) [غير معتمد]

*   **[snapwm](/index.php/Snapwm "Snapwm")** — هو مدير نوافذ خفيف و ديناميكي مع التركيز على سهولة و القدرة على التخصيص والاختيار. بني في شريط مع مساحات عمل قابلة للنقر و و مساحات للنصوص الخارجية. يوفر خمسة تنسيقات للتبليط:عمودي، ملء الشاشة، الأفقي، شبكة والتراص. لديه ميزات أخرى, مثل دعم التلوين, اسطح مكاتب مستقلة, اختيار استراتيجية وضع النوافذ, ملف التخصيص قابل للتحميل, دعم الشفافية, dmenu مدمج, الشاشات المتعددة و اشياء اخرى.

	[https://github.com/moetunes/Nextwm](https://github.com/moetunes/Nextwm) || [snapwm-git](https://aur.archlinux.org/packages/snapwm-git/) [غير معتمد]

*   **[spectrwm](/index.php/Spectrwm "Spectrwm")** — Spectrwm هو مدير نوافذ تبليطي يشتغل عل إكس, مستوح إلى حد كبير من xmonad و dwm. يحاول الخروج عن المعهود. لديه قيم افتراضية و يمكن كذلك تخصيصه من ملف نصي. كتب من طرف الهاكر ليستعمله الهاكر و يسعى مطوروه لكون صغيرة, مضغوط و سريع. يحتوي على شريط المعلومات يتغذى من ملف نصي معرف من قبل المستخدم

	[https://opensource.conformal.com/wiki/spectrwm](https://opensource.conformal.com/wiki/spectrwm) || [spectrwm](https://www.archlinux.org/packages/?name=spectrwm) [المجتمع]

*   **[Qtile](/index.php/Qtile "Qtile")** — Qtile كامل المواصفات , مدير نوافذ قابل للتعديل كتب بالبايثون تبليطي . Qtile بسيط, صغير, وقابل للتوسع. من السهل كتابة تخطيطات خاصة بك, حاجيات, و اوامر داخلية. تخصيصه يكون بالبايثون, مما يعني أنه يمكنك الاستفادة من القوة الكاملة والمرونة للغة لجعله يناسب احتياجاتك.

	[https://github.com/qtile/qtile](https://github.com/qtile/qtile) || [qtile-git](https://aur.archlinux.org/packages/qtile-git/) [غير معتمد]

*   **[Wingo](/index.php/Wingo "Wingo")** — Wingo مدير نوافذ هجين مع ميزات كاملة يدعم تعدد الشاشات و مساحات العمل, يمزج بين تنسيق العوم و التبليط هذا يعني ان النوافذ تبليط على مساحة عمل واحدة في حين تطفو على الآخر . Wingo يمكن كتابته كسكريب , كما انه قابل لإستعمال الثيم, ويدعم تحديد المستخدم. Wingoكتب بلغة Goوليس لديه تبعيات وقت التشغيل.

	[https://github.com/BurntSushi/wingo](https://github.com/BurntSushi/wingo) || [wingo-git](https://aur.archlinux.org/packages/wingo-git/)[غير معتمد]

*   **[wmii](/index.php/Wmii "Wmii")** — wmii مدير نوافذ ديناميكي للخادم إكس. هو سكريبتي,لديه واجهة 9P و يدعم الطريقة الكلاسيكية و التبليط (Acme-شبيه) . يهد مطوروه إلى الحفاظ عليه صغير ونظيف (قابل للتغيير و جميل) . الاعدادات الافتراضية مصنوعة ب الباش [rc (the Plan 9 shell)](http://rc.cat-v.org), لكنه مكتوب بـ ruby,فأي برنامج يمكنه العمل مع النص يمكن تغييره. لديه شريط المعلومات و مطلق التطبيقات, و كذلك شريط المهام (`witray`).

	[http://wmii.suckless.org/](http://wmii.suckless.org/) || [wmii](https://aur.archlinux.org/packages/wmii/)

*   **[xmonad](/index.php/Xmonad "Xmonad")** — xmonad هو مدير نوافذ تبليطي ديناميكي كتب واعد في Haskell. ,كنت تنفق نصف وقتك في البحث عن النوافذ. xmonad يجعل العمل سهل , و اتوماتكيا . و لكل تغييرات في الاعدادات يجب إعادة ترجمة , xmonad إذان المترجم Haskell (اكثر 100MB) يجب ان يكون منصب . [xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib) يوفر العديد من الميزات الإضافية

	[http://xmonad.org/](http://xmonad.org/) || [xmonad](https://www.archlinux.org/packages/?name=xmonad)

## روابط خارجية

*   [http://www.gilesorr.com/wm/](http://www.gilesorr.com/wm/)