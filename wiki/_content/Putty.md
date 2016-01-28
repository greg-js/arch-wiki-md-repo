# Putty

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** No intro, no see also. (Discuss in [Talk:Putty#](https://wiki.archlinux.org/index.php/Talk:Putty))

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [List of applications](/index.php/List_of_applications "List of applications").**

**Notes:** please use the second argument of the template to provide more detailed indications. (Discuss in [Talk:Putty#](https://wiki.archlinux.org/index.php/Talk:Putty))

## Installation

[Install](/index.php/Install "Install") [putty](https://www.archlinux.org/packages/?name=putty). For a menu item and icon, install [putty-freedesktop](https://aur.archlinux.org/packages/putty-freedesktop/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR").

## 256 color support

_Settings > Connection > Data : Terminal-type string = xterm-256color_

To test color support, execute the following command: [reference](http://www.commandlinefu.com/commands/view/5879/show-numerical-values-for-each-of-the-256-colors-in-bash)

```
for code in {0..255}; do echo -e "\e[38;05;${code}m $code: Test"; done

```

See [256colours](http://www.robmeerman.co.uk/unix/256colours) for details.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Putty&oldid=399113](https://wiki.archlinux.org/index.php?title=Putty&oldid=399113)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Terminal emulators](/index.php/Category:Terminal_emulators "Category:Terminal emulators")

Hidden categories:

*   [Pages flagged with Template:Stub](/index.php/Category:Pages_flagged_with_Template:Stub "Category:Pages flagged with Template:Stub")
*   [Pages or sections flagged with Template:Merge](/index.php/Category:Pages_or_sections_flagged_with_Template:Merge "Category:Pages or sections flagged with Template:Merge")