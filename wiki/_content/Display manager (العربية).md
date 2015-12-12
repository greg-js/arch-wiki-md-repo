# Display manager (العربية)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[مدير العرض](https://en.wikipedia.org/wiki/X_display_manager_(program_type) "wikipedia:X display manager (program type)"), أو مدير الدخول, هو شاشة واجهة رسومية يتم عرضها في نهاية عملية الإقلاع في مكان ما من لصدفة الافتراضية. يوجد العديد من أنواع مديري الدخول ، تماما كما أن هناك أنواع مختلفة من مديري النوافذ وأسطح المكتب . عادة ما يكون هناك قدر معين من التخصيص المتاح مع هؤلاء المديرين.

## Contents

*   [1 قائمة مديري الدخول](#.D9.82.D8.A7.D8.A6.D9.85.D8.A9_.D9.85.D8.AF.D9.8A.D8.B1.D9.8A_.D8.A7.D9.84.D8.AF.D8.AE.D9.88.D9.84)
    *   [1.1 كونسول](#.D9.83.D9.88.D9.86.D8.B3.D9.88.D9.84)
    *   [1.2 رسومي](#.D8.B1.D8.B3.D9.88.D9.85.D9.8A)
*   [2 تحميل مدير الدخول](#.D8.AA.D8.AD.D9.85.D9.8A.D9.84_.D9.85.D8.AF.D9.8A.D8.B1_.D8.A7.D9.84.D8.AF.D8.AE.D9.88.D9.84)

## قائمة مديري الدخول

**تلميحة:** إن كنت مستخدما لبيئة سطح المكتب [desktop environment](/index.php/Desktop_environment "Desktop environment") ، عليك أن تراعي مدير الدخول الذي يتطابق معها .

**تلميحة:** مدخلات مدراءالدخول الآتية تقدم قائمة آلية لمديري النوافذ المثبتة لديك (تقوم بقراءة `/usr/share/xsessions` ) : GDM, KDM, LXDM, LightDM

### كونسول

*   **[CDM](/index.php/CDM "CDM") (Console Display Manager)** — ultra-minimalistic, yet full-featured login manager written in bash

[https://github.com/ghost1227/cdm](https://github.com/ghost1227/cdm) || [cdm-git](https://aur.archlinux.org/packages/cdm-git/)<sup><small>AUR</small></sup>

### رسومي

*   **[SLiM](/index.php/SLiM "SLiM") (Simple Login Manager)** — lightweight and elegant graphical login solution

[http://slim.berlios.de/](http://slim.berlios.de/) || [slim](https://www.archlinux.org/packages/?name=slim)

*   **[Qingy](/index.php/Qingy "Qingy")** — ultralight and very configurable graphical login independent on X Windows (uses DirectFB)

[http://qingy.sourceforge.net/](http://qingy.sourceforge.net/) || [qingy](https://aur.archlinux.org/packages/qingy/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/qingy)]</sup>

*   **[XDM](/index.php/XDM "XDM")** — X Display Manager with support for XDMCP, host chooser.

[http://www.x.org/archive/X11R7.5/doc/man/man1/xdm.1.html](http://www.x.org/archive/X11R7.5/doc/man/man1/xdm.1.html) || [xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm)

*   **[GDM](/index.php/GDM "GDM")** — [GNOME](/index.php/GNOME "GNOME") Display Manager

[http://projects.gnome.org/gdm/](http://projects.gnome.org/gdm/) || [gdm](https://www.archlinux.org/packages/?name=gdm)

*   **[KDM](/index.php/KDM "KDM")** — [KDE](/index.php/KDE "KDE") Display Manager

[http://www.kde.org/](http://www.kde.org/) || [kdebase-workspace](https://www.archlinux.org/packages/?name=kdebase-workspace)

*   **[LXDM](/index.php/LXDM "LXDM")** — [LXDE](/index.php/LXDE "LXDE") Display Manager. Can be used independent of the LXDE desktop environment.

[http://sourceforge.net/projects/lxdm/](http://sourceforge.net/projects/lxdm/) || [lxdm](https://www.archlinux.org/packages/?name=lxdm)

*   **[wdm](/index.php/Wdm "Wdm")** — WINGs Display Manager

[http://voins.program.ru/wdm/](http://voins.program.ru/wdm/) || [wdm](https://aur.archlinux.org/packages/wdm/)<sup><small>AUR</small></sup>

*   **[LightDM](/index.php/LightDM "LightDM")** — Ubuntu replacement for GDM using WebKit

[http://www.freedesktop.org/wiki/Software/LightDM](http://www.freedesktop.org/wiki/Software/LightDM) || [lightdm](https://www.archlinux.org/packages/?name=lightdm), [lightdm-bzr](https://aur.archlinux.org/packages/lightdm-bzr/)<sup><small>AUR</small></sup>

*   **[SDDM](/index.php/SDDM "SDDM")** — QML-based display manager

[https://github.com/sddm/sddm](https://github.com/sddm/sddm) || [sddm-git](https://aur.archlinux.org/packages/sddm-git/)<sup><small>AUR</small></sup>, [sddm-qt5-git](https://aur.archlinux.org/packages/sddm-qt5-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/sddm-qt5-git)]</sup>

## تحميل مدير الدخول

تأتي العديد من مديري الدخول محزمة مع ملف لمدير الخدمات [systemd](/index.php/Systemd "Systemd") . قم ببساطة بتنفيذ الأمر التالي وفقا لمدير الدخول الذي تختاره:

*   **GDM**:

```
# systemctl enable gdm.service

```

*   **KDM**:

```
# systemctl enable kdm.service

```

*   **SLiM**

```
# systemctl enable slim.service

```

*   **LXDM**:

```
# systemctl enable lxdm.service

```

*   **LightDM**:

```
# systemctl enable lightdm.service

```

*   **SDDM**:

```
# systemctl enable sddm.service

```

في المرة التالية التي تعيد بها التشغيل ، يجب أن يعمل مدير الدخول. سيتم تحميل مدير الدخول تلقائيا بعد الإقلاع وسوف يعاود الظهور إذا حدث أي عطل.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Display_manager_(العربية)&oldid=411578](https://wiki.archlinux.org/index.php?title=Display_manager_(العربية)&oldid=411578)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [العربية](/index.php/Category:%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9 "Category:العربية")
*   [Display managers (العربية)](/index.php/Category:Display_managers_(%D8%A7%D9%84%D8%B9%D8%B1%D8%A8%D9%8A%D8%A9) "Category:Display managers (العربية)")