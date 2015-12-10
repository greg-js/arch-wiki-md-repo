# DeveloperWiki:Repo Cleanup

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

## Contents

*   [1 Extra package cleanup](#Extra_package_cleanup)
    *   [1.1 Goals and ideas](#Goals_and_ideas)
    *   [1.2 Packages list](#Packages_list)
    *   [1.3 Candidate to [community]](#Candidate_to_.5Bcommunity.5D)
*   [2 Issues](#Issues)

# Extra package cleanup

## Goals and ideas

*   A cleanup of the extra repository
*   Currently we have 441 orphans packages in [extra] (any, i686, x86_64)
*   Reduce the packaging work load of the developers
*   Minimise the number of apps per task
*   TUs are easier to appoint and find, it makes sense to move some of the workload to the community repo
*   Games should all go to community (except those that come with KDE and Gnome)

## Packages list

This packages will be moved to Unsupported, if you want to keep it in [extra] simply cross it out. Adoption is not required (but would be nice). If you are a TU and you want to maintain a package in [community] DO NOT cross it out, but add it to [#Candidate to .5Bcommunity.5D](#Candidate_to_.5Bcommunity.5D)

*   abcde
*   <s>archlinux-artwork</s> - artwork
*   <s>archlinux-themes-slim</s> - artwork
*   <s>archlinux-wallpaper</s> - artwork
*   aria2
*   <s>artwiz-fonts</s>
*   <s>aspell-*</s> - languages support
*   <s>atkmm-docs</s> - part of the atkmm package
*   <s>aufs2</s> - needed by aufs2-util
*   <s>banshee</s>
*   bladeenc
*   bs
*   <s>chkrootkit</s>
*   <s>chromium</s> - adopted by me (foutrelis)
*   <s>clang-analyzer</s> - part of the llvm package
*   <s>cscope</s> - keep this, Dan
*   dosbox
*   <s>eog-plugins</s> - recently updated, ioni/heftig should adopt it
*   <s>eric4-plugins</s> - should be adopted by the eric4 maintainer.
*   ettercap-gtk
*   <s>festival-english</s> - voices for festival
*   <s>festival-us</s> - voices for festival
*   <s>gcdmaster</s>- part of the cdrdao package
*   <s>gnome-alsamixer</s>
*   gnupod
*   <s>gperf</s> - makedependence of various packages
*   <s>gptfdisk</s> - keep this, Ionut
*   gqmpeg
*   gtk-theme-switch2
*   <s>gtkmm3-docs</s> - parf ot the gtkmm3 package
*   <s>haskell-platform</s> - up to Vesa
*   <s>haskell-tar</s> - up to Vesa
*   <s>hunspell-hu</s> - languages support
*   <s>hunspell-ln</s> - languages support
*   <s>hyphen-hu</s> - languages support
*   <s>hyphen-nl</s> - languages support
*   icecast
*   <s>imap</s> - needed by php
*   <s>ipod-sharp</s>
*   <s>iptraf-ng</s>
*   <s>ispell</s> - needed by hunspell-de
*   <s>kernel26-manpages</s> - part of the kernel26 package
*   kmldonkey
*   kmplayer
*   <s>krusader</s> - keep this, Andrea
*   <s>laptop-mode-tools</s> - keep this, Andrea
*   libbtctl
*   <s>llvm-ocaml</s> - part of the llvm package
*   <s>ltrace</s> - adopted by me (foutrelis)
*   <s>mailman</s> - keep this, Andrea
*   mc
*   <s>meld</s>
*   <s>mm-common</s> - needed by gtkmm3
*   monotone
*   <s>mythes-hu</s> - languages support
*   <s>mythes-nl</s> - languages support
*   nbsmtp
*   nickle
*   nppangband
*   numlockx
*   <s>obconf</s> - keep this for OpenBox users, Andrea
*   perl-text-csv
*   <s>perl-text-patch</s> - needed by perl-alien-sdl
*   <s>proftpd</s> - keep this, Andrea
*   python-gtkglext
*   <s>qt3-doc</s> - part of the qt3 package
*   <s>ruby-docs</s> - part of the ruby package
*   <s>slim-themes</s> - themes for slim
*   speedcrunch
*   tango-icon-theme-extras
*   <s>texi2html</s> - needed by qemu
*   <s>ttf-cheapskate</s>
*   <s>ttf-fireflysung</s> - keep this for i18n support, Eric
*   <s>ttf-tibetan-machine</s> - keep this for i18n support, Eric
*   <s>ttf-ubraille</s> - keep this for blind users, Andrea
*   vbetool
*   vim-a
*   vim-bufexplorer
*   vim-colorsamplerpack
*   vim-doxygentoolkit
*   vim-guicolorscheme
*   vim-minibufexpl
*   vim-omnicppcomplete
*   vim-project
*   vim-taglist
*   vim-vcscommand
*   vim-workspace
*   xchat-gnome
*   <s>xf86-input-wacom</s> - up to Jan
*   <s>xorg-xfontsel</s> - up to Jan
*   <s>xorg-xlsfonts</s> - up to Jan
*   <s>xorg-xvidtune</s> - up to Jan

## Candidate to [community]

*   abcde - (schuay)
*   aria2 - I have used this occasionally in the past for torrents, so I would be willing to maintain this fine utility (td123)
*   dosbox - Good stuff (svenstaro)
*   gtk-theme-switch2 - (cryptocrack)
*   icecast - (cryptocrack)
*   mc - (schuay)
*   nickle - (cryptocrack)
*   numlockx - (cryptocrack)
*   tango-icon-theme-extras - (cryptocrack)
*   vbetool - (cryptocrack)
*   vim-a - (svenstaro)
*   vim-bufexplorer - (svenstaro)
*   vim-colorsamplerpack - (svenstaro)
*   vim-doxygentoolkit - (svenstaro)
*   vim-guicolorscheme - (svenstaro)
*   vim-minibufexpl - (svenstaro)
*   vim-omnicppcomplete - (svenstaro)
*   vim-project - (svenstaro)
*   vim-taglist - (svenstaro)
*   vim-vcscommand - (svenstaro)
*   vim-workspace - (svenstaro)

# Issues

Retrieved from "[https://wiki.archlinux.org/index.php?title=DeveloperWiki:Repo_Cleanup&oldid=383808](https://wiki.archlinux.org/index.php?title=DeveloperWiki:Repo_Cleanup&oldid=383808)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Package development](/index.php/Category:Package_development "Category:Package development")