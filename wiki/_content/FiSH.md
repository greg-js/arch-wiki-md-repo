# FiSH

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:FiSH#](https://wiki.archlinux.org/index.php/Talk:FiSH))

FiSH is a plugin/module that facilitates encrypted chatting over IRC. It's available for mIRC, xChat and Irssi.

## Contents

*   [1 Adding FiSH to mIRC](#Adding_FiSH_to_mIRC)
*   [2 Adding FiSH to xChat](#Adding_FiSH_to_xChat)
*   [3 Adding FiSH to Irssi](#Adding_FiSH_to_Irssi)
*   [4 See also](#See_also)

## Adding FiSH to mIRC

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** TODO (Discuss in [Talk:FiSH#](https://wiki.archlinux.org/index.php/Talk:FiSH))

## Adding FiSH to xChat

There is a package in the AUR called [xchat-fish](https://aur.archlinux.org/packages/xchat-fish/)<sup><small>AUR</small></sup>. Note that the package builds and installs only the plugin—you’ll need to create and install the `~/.xchat2/blow.ini` file yourself.

## Adding FiSH to Irssi

This requires light editing of a Makefile and compiling from source, nothing too difficult if you RTFM.

Proceedure Outline Download, unpack and build the MIRACL library for handling large numbers. Download and unpack the FiSH source. Copy the MIRACL.so library (built in step 1) to the FiSH source directory. Edit the makefile to point to paths for glib and irssi Compile FiSH Move the compiled plugin to irssi's folder.

Needed Packages: MIRACL FiSH opt: Irssi (If you did not compile Irssi from source, you will need to get the irssi headers from the irssi source for compiling FiSH)

## See also

*   [FiSH -- Secure communications with Internet Relay Chat](http://ultrx.net/doc/fish/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=FiSH&oldid=374474](https://wiki.archlinux.org/index.php?title=FiSH&oldid=374474)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Internet Relay Chat](/index.php/Category:Internet_Relay_Chat "Category:Internet Relay Chat")
*   [Encryption](/index.php/Category:Encryption "Category:Encryption")

Hidden categories:

*   [Pages or sections flagged with Template:Style](/index.php/Category:Pages_or_sections_flagged_with_Template:Style "Category:Pages or sections flagged with Template:Style")
*   [Pages or sections flagged with Template:Expansion](/index.php/Category:Pages_or_sections_flagged_with_Template:Expansion "Category:Pages or sections flagged with Template:Expansion")