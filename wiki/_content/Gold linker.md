# Gold linker

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** Still very short to stay as a separate page. (Discuss in [Talk:Gold linker#](https://wiki.archlinux.org/index.php/Talk:Gold_linker))

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [GNU Project#Development Tools](/index.php/GNU_Project#Development_Tools "GNU Project").**

**Notes:** please use the second argument of the template to provide more detailed indications. (Discuss in [Talk:Gold linker#](https://wiki.archlinux.org/index.php/Talk:Gold_linker))

The Gold linker is a newer and reportedly faster linker than the standard GNU ld linker. It is included in the [binutils](https://www.archlinux.org/packages/?name=binutils) package.

To use the GOLD linker, simply

```
export LD=ld.gold

```

Alternatively, if your $PATH has /usr/local/bin before /usr/bin, you can do

```
ln -s /usr/bin/ld.gold /usr/local/bin/ld

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Gold_linker&oldid=342455](https://wiki.archlinux.org/index.php?title=Gold_linker&oldid=342455)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Development](/index.php/Category:Development "Category:Development")