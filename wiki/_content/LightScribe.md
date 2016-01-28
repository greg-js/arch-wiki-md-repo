# LightScribe

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** please use the first argument of the template to provide more detailed indications. (Discuss in [Talk:LightScribe#](https://wiki.archlinux.org/index.php/Talk:LightScribe))

From [lightscribe.com](http://www.lightscribe.com/):

_LightScribe is an innovative technology that uses a special disc drive, special media, and label-making software to burn labels directly onto CDs and DVDs._

Labels burnt using LightScribe are monochromatic, as it works by making a chemical in the media react with the laser beam and change color.

## Installation

To use LightScribe, regardless of which operating system you're using, you need two pieces of software: the LightScribe System Software and another LightScribe label making software.

On Arch, the LightScribe System Software is available from the [AUR](/index.php/AUR "AUR"):

*   **i686**: [lightscribe](https://aur.archlinux.org/packages/lightscribe/)<sup><small>AUR</small></sup>
*   **x86_64**: [bin32-lightscribe](https://aur.archlinux.org/packages/bin32-lightscribe/)<sup><small>AUR</small></sup>

## Labelers

In the [AUR](/index.php/AUR "AUR") you can find:

*   **LightScribe Simple Labeler**: official tool to make simple thin labels. You can only type text and use the provided templates as separators. Useful to make good looking labels quickly (it takes only 3 minutes, as opposed to a full-disk label which takes around 30 minutes)
    *   **i686**: [lightscribe-labeler](https://aur.archlinux.org/packages/lightscribe-labeler/)<sup><small>AUR</small></sup>
    *   **x86_64**: [bin32-lightscribe-labeler](https://aur.archlinux.org/packages/bin32-lightscribe-labeler/)<sup><small>AUR</small></sup>
*   **LaCie 4L LightScribe Labeler for Linux**: tool from LaCie that allows to create a full-disk label using a picture.
    *   **i686**: [4l](https://aur.archlinux.org/packages/4l/)<sup><small>AUR</small></sup>
    *   **x86_64**: [bin32-4l](https://aur.archlinux.org/packages/bin32-4l/)<sup><small>AUR</small></sup>

Additionally, [searching for lightscribe in the AUR](https://aur.archlinux.org/packages.php?K=lightscribe) will create a list of related software.

## Enhanced Label Contrast Utility

To adjust the contrast which is often too light, run:

```
# /usr/lib/lightscribe/elcu.sh

```

then hit 1 to use the enhanced contrast setting or 2 to reset it. Note that some programs (like LaCie 4L) have this option built-in and it can be changed at runtime.

Retrieved from "[https://wiki.archlinux.org/index.php?title=LightScribe&oldid=411647](https://wiki.archlinux.org/index.php?title=LightScribe&oldid=411647)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Optical](/index.php/Category:Optical "Category:Optical")

Hidden category:

*   [Pages flagged with Template:Stub](/index.php/Category:Pages_flagged_with_Template:Stub "Category:Pages flagged with Template:Stub")