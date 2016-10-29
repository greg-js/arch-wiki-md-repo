From [w:LightScribe](https://en.wikipedia.org/wiki/LightScribe "w:LightScribe"):

	LightScribe is an optical disc recording technology, created by the Hewlett-Packard Company, that uses specially coated recordable CD and DVD media to produce laser-etched labels with text or graphics, as opposed to stick-on labels and printable discs.

Labels burnt using LightScribe are monochromatic, as it works by making a chemical in the media react with the laser beam and change color.

**Note:**

*   The official home of LightScribe [www.lightscribe.com](http://www.lightscribe.com) is discontinued since 2013\. The lightscribe system software is only available from third parties like [pawtec](http://www.pawtec.com/lightscribe/).
*   x86_64 is only partially supported with [Multilib](/index.php/Multilib "Multilib").

## Contents

*   [1 Installation](#Installation)
*   [2 Labelers](#Labelers)
*   [3 Enhanced Label Contrast Utility](#Enhanced_Label_Contrast_Utility)
*   [4 See also](#See_also)

## Installation

To use LightScribe, regardless of which operating system you are using, you need two pieces of software: the LightScribe System Software and another LightScribe label making software.

On Arch, the LightScribe System Software is available from the [AUR](/index.php/AUR "AUR"):

*   **i686**: [lightscribe](https://aur.archlinux.org/packages/lightscribe/)
*   [Multilib](/index.php/Multilib "Multilib") **x86_64**: [bin32-lightscribe](https://aur.archlinux.org/packages/bin32-lightscribe/)

## Labelers

In the [AUR](/index.php/AUR "AUR") you can find:

*   **LightScribe Simple Labeler**: official tool to make simple thin labels. You can only type text and use the provided templates as separators. Useful to make good looking labels quickly (it takes only 3 minutes, as opposed to a full-disk label which takes around 30 minutes)
    *   **i686**: [lightscribe-labeler](https://aur.archlinux.org/packages/lightscribe-labeler/)
    *   **x86_64**: [bin32-lightscribe-labeler](https://aur.archlinux.org/packages/bin32-lightscribe-labeler/)
*   **LaCie 4L LightScribe Labeler for Linux**: tool from LaCie that allows to create a full-disk label using a picture.
    *   **i686**: [4l](https://aur.archlinux.org/packages/4l/)
    *   **x86_64**: [bin32-4l](https://aur.archlinux.org/packages/bin32-4l/)

Additionally, [searching for lightscribe in the AUR](https://aur.archlinux.org/packages.php?K=lightscribe) will create a list of related software.

## Enhanced Label Contrast Utility

To adjust the contrast which is often too light, run:

```
# /usr/lib/lightscribe/elcu.sh

```

then hit `1` to use the enhanced contrast setting or `2` to reset it. Note that some programs (e.g. LaCie 4L) have this option built-in and it can be changed at runtime.

## See also

*   [http://www.pawtec.com/lightscribe/](http://www.pawtec.com/lightscribe/)
*   (GER) [https://wiki.ubuntuusers.de/LightScribe/](https://wiki.ubuntuusers.de/LightScribe/)