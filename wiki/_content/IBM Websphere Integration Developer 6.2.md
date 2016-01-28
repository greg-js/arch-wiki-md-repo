# IBM Websphere Integration Developer 6.2

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Article needs some more details. (Discuss in [Talk:IBM Websphere Integration Developer 6.2#](https://wiki.archlinux.org/index.php/Talk:IBM_Websphere_Integration_Developer_6.2))

Launching IBM WID in modern Arch environment is not a trivial task, here is a detailed guide on how to do it.

## Installation

To intsall IBM WID 6.2 on Arch Linux you need:

*   Delete IBM Installation Manager if you have it installed
*   Comment out the following line in installer_dir/IM_linux/install.xml
*   Launch silent installation

```
# ./userinst --launcher.ini ./silent-install.ini

```

## Usage

To make IBM WID 6.2 run successfully you will need to install [swt](https://www.archlinux.org/packages/?name=swt), [lib32-gtk2](https://www.archlinux.org/packages/?name=lib32-gtk2), [lib32-libstdc++5](https://www.archlinux.org/packages/?name=lib32-libstdc%2B%2B5) and [lib32-libxtst](https://www.archlinux.org/packages/?name=lib32-libxtst). You can run WID with the following command

```
$ /opt/IBM/WID62/eclipse -product com.ibm.wbit.feature.ide -showlocation

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=IBM_Websphere_Integration_Developer_6.2&oldid=381763](https://wiki.archlinux.org/index.php?title=IBM_Websphere_Integration_Developer_6.2&oldid=381763)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Development](/index.php/Category:Development "Category:Development")

Hidden category:

*   [Pages or sections flagged with Template:Expansion](/index.php/Category:Pages_or_sections_flagged_with_Template:Expansion "Category:Pages or sections flagged with Template:Expansion")