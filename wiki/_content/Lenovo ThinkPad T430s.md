# Lenovo ThinkPad T430s

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Laptop/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo").**

**Notes:** Too little unique content to warrant a separate page (Discuss in [Talk:Lenovo ThinkPad T430s#](https://wiki.archlinux.org/index.php/Talk:Lenovo_ThinkPad_T430s))

## Contents

*   [1 Known issues](#Known_issues)
    *   [1.1 Open issues](#Open_issues)
    *   [1.2 Fixed](#Fixed)
    *   [1.3 Laptop Settings](#Laptop_Settings)

## Known issues

The following are known problems and workarounds for the Lenovo Thinkpad T430s, and likely also for the related models (X230, T430, T530).

### Open issues

*   The usual issue with laptop hard drives and disk head parking: [see here](/index.php/Hdparm#Parking_your_hard_drive "Hdparm")
*   At least on one T430s, using QCad with [SNA](/index.php/Intel_graphics "Intel graphics") would reliably crash Xorg. A workaround is using UXA instead of SNA. ([FS#31617](https://bugs.archlinux.org/task/31617))
*   The accelerometer for [HDAPS](/index.php/HDAPS "HDAPS") isn't supported.

### Fixed

*   Fixed accurately setting the brightness levels with the Fn + brightness up/down shortcut keys. The problem comes from Intel graphics, and the solution can be found from [here](https://wiki.archlinux.org/index.php/Intel#Backlight_not_fully_adjusting.2C_or_adjusting_at_all.2C_after_resume.).

### Laptop Settings

[Xbindkeys](/index.php/Xbindkeys "Xbindkeys") or [sxhkd](/index.php/Sxhkd "Sxhkd") can be used to create and modify keyboard bindings. The following example requires the [xorg-xset](https://www.archlinux.org/packages/?name=xorg-xset) package, and turns the display off when the rectangular button to the right of the microphone mute button is pressed.

 `~/.xinbkeysrc` 

```
# Close display
"xset dpms force off"
    m:0x0 + c:156
    XF86Launch1

```

Other options can be found from [Lenovo ThinkPad T420#Volume up/down not changing volume](/index.php/Lenovo_ThinkPad_T420#Volume_up.2Fdown_not_changing_volume "Lenovo ThinkPad T420")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_T430s&oldid=412567](https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_T430s&oldid=412567)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Lenovo](/index.php/Category:Lenovo "Category:Lenovo")

Hidden category:

*   [Pages or sections flagged with Template:Merge](/index.php/Category:Pages_or_sections_flagged_with_Template:Merge "Category:Pages or sections flagged with Template:Merge")