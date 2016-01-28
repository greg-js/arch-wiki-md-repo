# EVE Online

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Written in first person. (Discuss in [Talk:EVE Online#](https://wiki.archlinux.org/index.php/Talk:EVE_Online))

Successful install of EVE Online: Rhea.

## Contents

*   [1 Packages](#Packages)
*   [2 Installing EVE Online](#Installing_EVE_Online)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Performance](#Performance)
    *   [3.2 Wine errors and font incompatibilities](#Wine_errors_and_font_incompatibilities)

## Packages

Per [https://bugs.winehq.org/show_bug.cgi?id=36139#c13](https://bugs.winehq.org/show_bug.cgi?id=36139#c13), from multilib, you will need to install/have lib32-libxml2 before you will be able to install EVE. My system had several other multilib libraries already, so if there are any dependencies I already had, please edit them in.

*   multilib/lib32-libxml2

## Installing EVE Online

In a fresh WINEPREFIX, follow the directions at [https://appdb.winehq.org/objectManager.php?sClass=version&iId=25823](https://appdb.winehq.org/objectManager.php?sClass=version&iId=25823) under "HOWTO - Eve Online install on Linux". You should be able to run the normal launcher with wine > 1.7 as noted, instead of running ExeFile.exe directly.

## Troubleshooting

### Performance

If you are on a multi-core processer and are experiencing occasional multi-second freezes, instead of running wine directly, add "taskset -c 0 wine ...". This forces the EVE process to stay on one of your cores, preventing very slow context switches (every 20-30 seconds). If you are not experiencing freezes, this will probably decrease performance, and is not recommended.

### Wine errors and font incompatibilities

Running the installer (several post-Rubicon versions tried) on wine-1.7.36 with the "ttf-ms-fonts" AUR package installed results in wine throwing "fixme:uniscribe:GSUB_apply_lookup We do not handle SubType 7" in a loop when trying to render the actual MS fonts on the installer, since the second installer page features an RTF/HTML-formatter EULA. This freezes the install process right after the first "Next >" button press. Uninstalling the "ttf-ms-fonts" package then re-running the installer works fine as a workaround.

Retrieved from "[https://wiki.archlinux.org/index.php?title=EVE_Online&oldid=362174](https://wiki.archlinux.org/index.php?title=EVE_Online&oldid=362174)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Gaming](/index.php/Category:Gaming "Category:Gaming")
*   [Wine](/index.php/Category:Wine "Category:Wine")

Hidden category:

*   [Pages or sections flagged with Template:Style](/index.php/Category:Pages_or_sections_flagged_with_Template:Style "Category:Pages or sections flagged with Template:Style")