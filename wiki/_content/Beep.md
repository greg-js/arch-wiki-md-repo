# Beep

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Disable PC speaker beep](/index.php/Disable_PC_speaker_beep "Disable PC speaker beep").**

**Notes:** ...and rename to [PC speaker](/index.php?title=PC_speaker&action=edit&redlink=1 "PC speaker (page does not exist)")? (Discuss in [Talk:Beep#](https://wiki.archlinux.org/index.php/Talk:Beep))

Beep is an advanced PC speaker beeping program. It is useful for situations where no sound card and/or speakers are available, and simple audio notification is desired.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Access for non-root users](#Access_for_non-root_users)
    *   [2.2 Unmuting in alsamixer](#Unmuting_in_alsamixer)
*   [3 Tips and Tricks](#Tips_and_Tricks)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [beep](https://www.archlinux.org/packages/?name=beep) package.

## Configuration

### Access for non-root users

By default `beep` will fail if not run by the root. Other users may call it using [sudo](/index.php/Sudo "Sudo"). To let group `users` call `sudo beep` without a password (for example to use it in scripts), `/etc/sudoers` [should be edited](https://wiki.archlinux.org/index.php/Sudo#Using_visudo):

```
%users ALL=(ALL) NOPASSWD: /usr/bin/beep

```

or, to let only a single user do that:

```
username ALL=(ALL) NOPASSWD: /usr/bin/beep

```

Another way is setting the sticky bit on `/usr/bin/beep`:

```
# chmod 4755 /usr/bin/beep

```

Note however that this way **anyone** can execute `/usr/bin/beep` with root permissions. The change also creates a difference between local copy and the package, which will be reported by `pacman -Qkk`.

### Unmuting in alsamixer

You should also unmute the Beep channel using `alsamixer`.

```
$ alsamixer

```

You may need to press `F6` and select your card. scroll to the Beep channel using the arrow keys and press `M` to unmute the channel. notice that the "MM" label below the channel will change to "00". you can also use `↑` to increase the volume of the channel.

Press `Esc` to close alsamixer.

You can also save your settings to ALSA Mixer to make it permanent:

```
# alsactl -f /var/lib/alsa/asound.state store

```

## Tips and Tricks

While many people are happy with the traditional beep sound, some may like to change its properties a bit. The following example plays slighly higher and shorter sound and repeats it two times.

```
# beep -f 5000 -l 50 -r 2

```

## See also

*   [Advanced Linux Sound Architecture](/index.php/Advanced_Linux_Sound_Architecture "Advanced Linux Sound Architecture")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Beep&oldid=411977](https://wiki.archlinux.org/index.php?title=Beep&oldid=411977)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Sound](/index.php/Category:Sound "Category:Sound")

Hidden category:

*   [Pages or sections flagged with Template:Merge](/index.php/Category:Pages_or_sections_flagged_with_Template:Merge "Category:Pages or sections flagged with Template:Merge")