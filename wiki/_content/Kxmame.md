# Kxmame

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