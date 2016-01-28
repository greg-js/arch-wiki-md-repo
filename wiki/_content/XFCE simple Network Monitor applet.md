# XFCE simple Network Monitor applet

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Xfce](/index.php/Xfce "Xfce").**

**Notes:** A PKGBUILD for the AUR should also be made and only linked from the section. (Discuss in [Talk:XFCE simple Network Monitor applet#](https://wiki.archlinux.org/index.php/Talk:XFCE_simple_Network_Monitor_applet))

The latest and fairly improved version (now not only reports the network activity) has been moved.

Full information and screenshots in [github](https://github.com/lightful/xfce-hkmon).

The original version is also available in git history, but the new one it is as simple and easy to install:

## Installation instructions

Download [xfce-hkmon.cpp](https://raw.githubusercontent.com/lightful/xfce-hkmon/master/xfce-hkmon.cpp) and compile it:

```
g++ -std=c++0x -O3 -lrt xfce-hkmon.cpp -o xfce-hkmon

```

Place the executable somewhere (e.g. /usr/local/bin) and add a **XFCE Generic Monitor Applet** with these settings: no label, 1 second period, _Bitstream Vera Sans Mono font_ (recommended) and the following command:

```
/usr/local/bin/xfce-hkmon NET CPU TEMP IO RAM

```

You may also add an interface name (eth0, ppp0,...) to override the automatic selection by traffic.

Retrieved from "[https://wiki.archlinux.org/index.php?title=XFCE_simple_Network_Monitor_applet&oldid=355994](https://wiki.archlinux.org/index.php?title=XFCE_simple_Network_Monitor_applet&oldid=355994)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Internet applications](/index.php/Category:Internet_applications "Category:Internet applications")

Hidden category:

*   [Pages or sections flagged with Template:Merge](/index.php/Category:Pages_or_sections_flagged_with_Template:Merge "Category:Pages or sections flagged with Template:Merge")