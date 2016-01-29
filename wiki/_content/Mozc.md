# Mozc

From the project [home page](http://code.google.com/p/mozc/):

NaN

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Unofficial user repository](#Unofficial_user_repository)
    *   [1.2 Using PKGBUILD](#Using_PKGBUILD)
    *   [1.3 Using fcitx](#Using_fcitx)
    *   [1.4 Make available Mozc](#Make_available_Mozc)
    *   [1.5 Variants on AUR](#Variants_on_AUR)
        *   [1.5.1 uim-mozc](#uim-mozc)
        *   [1.5.2 mozc-ut](#mozc-ut)
        *   [1.5.3 mozc-svn](#mozc-svn)
*   [2 Configuration](#Configuration)
    *   [2.1 IBus](#IBus)
    *   [2.2 uim](#uim)
    *   [2.3 Mozc for Emacs](#Mozc_for_Emacs)
        *   [2.3.1 Disabling XIM on Emacs](#Disabling_XIM_on_Emacs)
*   [3 Tips](#Tips)
    *   [3.1 Confirming Mozc version which you are using now](#Confirming_Mozc_version_which_you_are_using_now)
    *   [3.2 Launching Mozc tools from command line](#Launching_Mozc_tools_from_command_line)
    *   [3.3 Use CapsLock as Eisu_toggle key on ASCII layout keyboard](#Use_CapsLock_as_Eisu_toggle_key_on_ASCII_layout_keyboard)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Building Mozc fails (process is killed)](#Building_Mozc_fails_.28process_is_killed.29)
    *   [4.2 New version of Mozc does not appear though I upgraded Mozc and restarted X or IBus (not rebooted)](#New_version_of_Mozc_does_not_appear_though_I_upgraded_Mozc_and_restarted_X_or_IBus_.28not_rebooted.29)

## Installation

You can install [mozc](https://aur.archlinux.org/packages/mozc/)<sup><small>AUR</small></sup> (vanilla) using [unofficial user repository](#Unofficial_user_repository) or build yourself from [AUR](/index.php/AUR "AUR").

**Note:** Mozc works with [ibus](https://www.archlinux.org/packages/?name=ibus). Please see also [IBus](/index.php/IBus "IBus") for installation and configuration.

This package consists as follows:

| Package | mozc | description |
| Group | mozc-im |
| Component | mozc | Server part of the Mozc |
| ibus-mozc | IBus engine module |
| emacs-mozc | Mozc for Emacs (optional) |

**Tip:** [Unofficial plugins for the other IM frameworks are available](#Variants_on_AUR)

### Unofficial user repository

There is an unofficial user repository of Mozc. Add the following into your `/etc/pacman.conf`:

```
[pnsft-pur]
SigLevel = Optional TrustAll
Server = http://downloads.sourceforge.net/project/pnsft-aur/pur/$arch

```

**Note:** This repo provides x86_64 packages only now.

And refresh package database. You can choose to install packages specifying group name as follows:

```
# pacman -S mozc-im

```

Or, specify package names directly. For example:

```
# pacman -S mozc ibus-mozc emacs-mozc

```

### Using PKGBUILD

You can install from AUR as follows.

First, get [mozc](https://aur.archlinux.org/packages/mozc/)<sup><small>AUR</small></sup> tarball from AUR and edit the PKGBUILD if necessary.

```
$ wget [https://aur.archlinux.org/packages/mo/mozc/mozc.tar.gz](https://aur.archlinux.org/packages/mo/mozc/mozc.tar.gz)
$ tar xvf mozc.tar.gz
$ cd mozc

```

If you will be using mozc.el on Emacs, uncomment `_emacs_mozc` line.

```
## If you will be using mozc.el on Emacs, uncomment below.
_emacs_mozc="yes"

```

### Using fcitx

[fcitx-mozc](https://www.archlinux.org/packages/?name=fcitx-mozc) is the all in one Mozc package available in [offical repository](/index.php/Official_repositories "Official repositories"), dedicated to [fcitx](/index.php/Fcitx "Fcitx").

### Make available Mozc

Restart X or IBus to enable use of Mozc.

### Variants on AUR

Each packages consist as follows:

| Package | mozc | mozc-svn | mozc-ut | description |
| Group | mozc-im | mozc-im-svn | mozc-im |
| Component | mozc | mozc-svn | mozc-ut | Server part of the Mozc |
| ibus-mozc | ibus-mozc-svn | ibus-mozc-ut | IBus engine module (optional) |
| (uim-mozc) | uim-mozc-svn | uim-mozc-ut | uim plugin module (optional) |
| <small>_N/A_</small> | fcitx-mozc-svn | <small>_N/A_</small> | Fcitx module (optional) |
| emacs-mozc | emacs-mozc-svn | emacs-mozc-ut | Mozc for Emacs (optional) |

#### uim-mozc

Though [mozc](https://aur.archlinux.org/packages/mozc/)<sup><small>AUR</small></sup> adapts to only IBus input method framework, [macuim](http://code.google.com/p/macuim/) provides _uim-mozc_ plugin. [uim-mozc](https://aur.archlinux.org/packages/uim-mozc/)<sup><small>AUR</small></sup> is for vanilla _mozc_ and [mozc-ut](https://aur.archlinux.org/packages/mozc-ut/)<sup><small>AUR</small></sup>, [mozc-svn](https://aur.archlinux.org/packages/mozc-svn/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/mozc-svn)]</sup> can build _uim-mozc_ itself (see [Input Japanese using uim](/index.php/Input_Japanese_using_uim "Input Japanese using uim")). You can install _uim-mozc_ from [unofficial user repository](#Unofficial_user_repository) as well as vanilla _mozc_.

#### mozc-ut

[mozc-ut](https://aur.archlinux.org/packages/mozc-ut/)<sup><small>AUR</small></sup> comes with [Mozc UT dictionary](http://www.geocities.jp/ep3797/mozc_01.html) and can build _uim-mozc_. The dictionary adds over 350,000 words into original.

**Note:**

*   Building _mozc-ut_ requires long time to generate dictionary seed.
*   _mozc-ut_ can work with _ibus-mozc_, _emacs-mozc_ and _uim-mozc_ of vanilla _mozc_. That is, you don't have to build such as modules of _mozc-ut_ by the use of [unofficial user repository](#Unofficial_user_repository).

To build uim-mozc, edit PKGBUILD like follow, i,e. uncomment `_uim_mozc=` line:

```
## If you will not be using ibus, comment out below.
_ibus_mozc="yes"
## If you will be using uim, uncomment below.
_uim_mozc="yes"
## If applying patch for uim-mozc fails, try to uncomment below.
#_kill_kill_line="yes"
## This will disable the 'kill-line' function of uim-mozc.

```

**Tip:** If you will never be using ibus-mozc, comment out the `_ibus_mozc=` line.

#### mozc-svn

[mozc-svn](https://aur.archlinux.org/packages/mozc-svn/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/mozc-svn)]</sup> builds using the head of published svn repository and can build _uim-mozc_ and _fcitx-mozc_ plugin. You should not use _mozc-svn_ unless you have any reason (e.g. for test).

## Configuration

### IBus

_See also [IBus](/index.php/IBus "IBus") for IBus configuration._

If you use Mozc by default, set it via _ibus-setup_:

```
$ ibus-setup

```

Choose _Input Method_ tab and move _Mozc_ to top of the list.

You can switch input method by `Alt+Shift_L` (by IBus default).

### uim

Configure uim preferences by running :

```
$ uim-pref-gtk (Or, uim-pref-gtk3/uim-pref-qt4)

```

which brings forth a GUI.

Choose your preferring input method as 'Default input method'.

**Note:** Mozc will be not listed in 'Default input method' at first time so you will need to add it into 'Enabled input methods' to use.

**Warning:** You **must** run the following command whenever you upgrade or (re-)install **uim**.
# uim-module-manager --register mozc

### Mozc for Emacs

You can use mozc.el (mozc-mode) to input Japanese via LEIM (Library of Emacs Input Method). To use mozc-mode, write the following into your `.emacs.d/init.el` or some other file for Emacs customizing:

```
(require 'mozc)  ; or (load-file "/path/to/mozc.el")
(setq default-input-method "japanese-mozc")

```

mozc.el provides "overlay" mode in the styles of showing candidates (from mozc r77) which shows a candidate window in box style close to the point. If you want to use it by default, add the following:

```
(setq mozc-candidate-style 'overlay)

```

`C-\` (_toggle-input-method_) enables and disables use of mozc-mode.

#### Disabling XIM on Emacs

When you are using input method on your desktop and assigning activation/deactivation of input method to C-SPC, you will be not able to use C-SPC/C-@ as set-mark-command on Emacs. To avoid this problem, add the following into your `~/.Xresources` or `~/.Xdefaults`. xim will be disabled on Emacs.

```
Emacs*UseXIM: false

```

## Tips

### Confirming Mozc version which you are using now

Type "ばーじょん" ("version") and convert it while activating Mozc. The version number of Mozc will be shown in the candidate list like follows:

```
<u>ばーじょん</u>

```

```
バージョン
ヴァージョン
ばーじょん
Mozc-1.6.1187.102  _⇐ Current version of Mozc_
...
```

### Launching Mozc tools from command line

The followings are commands to launch mozc tools.

*   Mozc property: `$ /usr/lib/mozc/mozc_tool --mode=config_dialog`
*   Mozc Dictionary Tool: `$ /usr/lib/mozc/mozc_tool --mode=dictionary_tool`
*   Mozc Word Register: `$ /usr/lib/mozc/mozc_tool --mode=word_register_dialog`
*   Mozc Hand Writing: `$ /usr/lib/mozc/mozc_tool --mode=hand_writing`
*   Mozc Character Palette: `$ /usr/lib/mozc/mozc_tool --mode=character_palette`

### Use CapsLock as Eisu_toggle key on ASCII layout keyboard

All of the preset keymap styles of Mozc, command _ToggleAlphanumericMode_ on _Composition_ mode is assigned to `Eisu` (Eisu_toggle), `Hiragana/Katakana` or `Muhenkan` key, but the ASCII keyboard has none of them.

One of the solution for it is to use CapsLock key as Eisu_toggle (Mozc does not recognize CapsLock key as of r124). The following is way to assign the Eisu_toggle to `CapsLock` (without any modifier keys) and the Caps_Lock to `Shift+CapsLock`, like OADG keyboard layout.

**Warning:** This way affects to desktop wide.

Edit the `~/.Xmodmap` as follows:

```
keycode 66 = Eisu_toggle Caps_Lock
clear Lock

```

Then, restart X or run xmodmap to apply immediately:

```
$ xmodmap ~/.Xmodmap

```

## Troubleshooting

### Building Mozc fails (process is killed)

If build process is failed with like the following messages:

```
...
/bin/sh: line 1:  xxxx killed
...
make: *** [xxx/xxx...] error 137
...

```

Make sure whether you have run out of memory.

### New version of Mozc does not appear though I upgraded Mozc and restarted X or IBus (not rebooted)

Old version of Mozc may be still on your memory. Try to kill existing _mozc_server_ process:

```
$ killall mozc_server

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Mozc&oldid=392462](https://wiki.archlinux.org/index.php?title=Mozc&oldid=392462)"