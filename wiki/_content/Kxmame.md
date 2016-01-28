# Kxmame

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** please use the first argument of the template to provide more detailed indications. (Discuss in [Talk:Kxmame#](https://wiki.archlinux.org/index.php/Talk:Kxmame))

Kxmame is a KDE port of the GXmame frontend for xmame and sdlmame emulators.

## How to obtain

Download, build and install the [kxmame-svn](https://aur.archlinux.org/packages/kxmame-svn/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/kxmame-svn)]</sup> AUR package.

## Steps to follow after installation

*   Install sdlmame (available in [community]).
*   Start kxmame, click through the first two error messages (regarding xmame) and then add **"/usr/bin/sdlmame"** to the **Xmame/Xmess executables** list.
*   Click OK and then click No when prompted to rebuild the game list. After that, close kxmame.
*   Create a **"roms"** directory inside **"~/.mame"** and move your roms into it.
*   Start kxmame again and select Yes when prompted to rebuild the game list.
*   Close the "Audit done" window.

You should now be able to start your roms from within kxmame.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Kxmame&oldid=392320](https://wiki.archlinux.org/index.php?title=Kxmame&oldid=392320)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Gaming](/index.php/Category:Gaming "Category:Gaming")
*   [Emulators](/index.php/Category:Emulators "Category:Emulators")

Hidden categories:

*   [Pages flagged with Template:Stub](/index.php/Category:Pages_flagged_with_Template:Stub "Category:Pages flagged with Template:Stub")
*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")