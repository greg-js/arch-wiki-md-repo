# Tp-battery-mode

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [[]].**

**Notes:** Duplicates [tp_smapi](/index.php/Tp_smapi "Tp smapi"), and the script itself arguably offers little over following the instructions in that article. Perhaps it is best to redirect this to [tp_smapi](/index.php/Tp_smapi "Tp smapi"). (Discuss in [Talk:Tp-battery-mode#](https://wiki.archlinux.org/index.php/Talk:Tp-battery-mode))

tp-battery-mode is a module to easily switch your Thinkpad's battery charging mode to prolong battery lifetime using [tpacpi-bat](https://aur.archlinux.org/packages/tpacpi-bat/) from the [AUR](/index.php/AUR "AUR").

## Contents

*   [1 Installation](#Installation)
*   [2 Features](#Features)
    *   [2.1 Prolong Battery Lifetime](#Prolong_Battery_Lifetime)
    *   [2.2 Reverting to default charging behavior](#Reverting_to_default_charging_behavior)

## Installation

Install the [tp-battery-mode](https://aur.archlinux.org/packages/tp-battery-mode/)<sup><small>AUR</small></sup> package available from the [AUR](/index.php/AUR "AUR").

## Features

Your Thinkpad's default behavior is to start charging its battery as soon as it drops below 100% capacity and stop charging once it is at 100% capacity. Switching your battery charging mode changes these start & stop threshold. tp-battery-mode's default values can be found in `/etc/tp-battery-mode.conf`

```
STARTTHRESHOLD=85
STOPTHRESHOLD=90

```

These values mean that your battery will start charging once the capacity drops below 85% and stop charging once it has reached 90% capacity. This should prolong your battery's lifespan while still giving you ample charge for portable needs.

### Prolong Battery Lifetime

Switching to these new charging thresholds is as simple as:

```
systemctl start tp-battery-mode

```

To make sure that the change is persistent, enable the service. This will ensure that your charging mode is correct on boot:

```
systemctl enable tp-battery-mode

```

You can tailor the start/stop thresholds to fit your needs by modifying `/etc/tp-battery-mode.conf`. If you modify these values, you will need to restart the tp-battery-mode service otherwise the changes will not be reflected until you reboot.

**Note:** tp-battery-mode supports the T440's dual batteries however their charging thresholds cannot be changed independently.

### Reverting to default charging behavior

Sometimes you might want to charge your battery all the way to 100% If you wish to revert to the default Thinkpad charging behavior, you just need to stop the service:

```
systemctl stop tp-battery-mode

```

If you wish to revert to the default Thinkpad charging behavior completely, you will also need to disable the service:

```
systemctl disable tp-battery-mode

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Tp-battery-mode&oldid=410948](https://wiki.archlinux.org/index.php?title=Tp-battery-mode&oldid=410948)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Laptops](/index.php/Category:Laptops "Category:Laptops")