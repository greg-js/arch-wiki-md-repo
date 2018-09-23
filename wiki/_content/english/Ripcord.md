[Ripcord](https://cancel.fm/ripcord/) is a lightweight desktop chat client for group-centric services like [Slack](/index.php/Slack "Slack") and [Discord](/index.php/Discord "Discord") built upon the [Qt](/index.php/Qt "Qt") toolkit. It is proprietary software and currently distributed as freeware, with the intention of eventually reaching a commercial release while maintaining at least the Discord portion usable free of charge.

## Installation

Install the [ripcord](https://aur.archlinux.org/packages/ripcord/) package.

## Custom themes

See the following [guide](https://gist.github.com/randrew/81d4fed3ef72e56bb3d24bf2a564225c). The directory containing `settings.ini` is `$HOME/.local/share/Ripcord`.

## Emoji glitch

There is a bug with some emoji fonts (known: [ttf-emojione-color](https://aur.archlinux.org/packages/ttf-emojione-color/), [noto-fonts-emoji](https://aur.archlinux.org/packages/noto-fonts-emoji/)) which generates rendering glitches, currently not fixed. Emoji fonts known to behave well include [ttf-twemoji-color](https://aur.archlinux.org/packages/ttf-twemoji-color/) and [ttf-symbola](https://aur.archlinux.org/packages/ttf-symbola/), so it is recommended to use one of them. Please note that some dialogs in the application always use system fonts, so it is sufficient to rely on the mentioned font in one's fontconfig to experience the bug.

For further updates and information, see the relevant [ticket](https://dev.cancel.fm/tktview?name=d2dc78360c) on the issue tracker.