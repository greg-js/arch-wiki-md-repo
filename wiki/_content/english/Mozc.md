From the project [home page](https://github.com/google/mozc):

	Mozc is a Japanese Input Method Editor (IME) designed for multi-platform such as Android OS, Apple OS X, Chromium OS, GNU/Linux and Microsoft Windows. This OpenSource project originates from [Google Japanese Input](http://www.google.com/intl/ja/ime/). […] Detailed differences between Google Japanese Input and Mozc are described in [About Branding](https://github.com/google/mozc/blob/master/docs/about_branding.md).

(In short, Mozc does not have equivalent conversion quality to Google Japanese Input).

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 IBus](#IBus)
    *   [2.2 uim](#uim)
    *   [2.3 Fcitx](#Fcitx)
    *   [2.4 Mozc for Emacs](#Mozc_for_Emacs)
        *   [2.4.1 Disabling XIM on Emacs](#Disabling_XIM_on_Emacs)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Confirming Mozc version which you are using now](#Confirming_Mozc_version_which_you_are_using_now)
    *   [3.2 Launching Mozc tools from command line](#Launching_Mozc_tools_from_command_line)
    *   [3.3 Use CapsLock as Eisu_toggle key on ASCII layout keyboard](#Use_CapsLock_as_Eisu_toggle_key_on_ASCII_layout_keyboard)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Building Mozc fails (process is killed)](#Building_Mozc_fails_.28process_is_killed.29)
    *   [4.2 New version of Mozc does not appear though I upgraded Mozc and restarted X or Input Method Framework (not rebooted)](#New_version_of_Mozc_does_not_appear_though_I_upgraded_Mozc_and_restarted_X_or_Input_Method_Framework_.28not_rebooted.29)
    *   [4.3 mozc_server becomes defunct](#mozc_server_becomes_defunct)

## Installation

Depending on your target setup, there are several available Mozc packages to choose from. Firstly, you will likely need to install both the Mozc core package and an integration for the Input Method Framework of your choice (such as [Fcitx](/index.php/Fcitx "Fcitx"), [IBus](/index.php/IBus "IBus"), or [uim](/index.php/UIM "UIM")), though some Fcitx packages come bundled with the core. Secondly, there exist some unofficial dictionaries: The UT (discontinued) and UT2 dictionaries, which are combined from several sources with hit numbers coming from Google/Yahoo and Wikipedia, respectively, and the NEologd UT dictionary based on the mecab-ipadic-NEologd Neologism dictionary.

The following table shows the packages corresponding to certain combinations of the components and dictionaries; merged cells with multiple package names indicate split packages. Some of the packages are also available from the [pnsft-pur](/index.php/Unofficial_user_repository#pnsft-pur "Unofficial user repository") repository.

 Vanilla | UT | UT2 | NEologd UT |
| Fcitx integration | [fcitx-mozc](https://www.archlinux.org/packages/?name=fcitx-mozc) | [fcitx-mozc-ut](https://aur.archlinux.org/packages/fcitx-mozc-ut/) | [fcitx-mozc-ut2](https://aur.archlinux.org/packages/fcitx-mozc-ut2/) | [fcitx-mozc-neologd-ut](https://aur.archlinux.org/packages/fcitx-mozc-neologd-ut/)
[mozc-neologd-ut](https://aur.archlinux.org/packages/mozc-neologd-ut/) |
| Mozc core |
| [mozc](https://aur.archlinux.org/packages/mozc/)
[ibus-mozc](https://aur.archlinux.org/packages/ibus-mozc/)
[emacs-mozc](https://aur.archlinux.org/packages/emacs-mozc/) | [mozc-ut2](https://aur.archlinux.org/packages/mozc-ut2/)
[ibus-mozc-ut2](https://aur.archlinux.org/packages/ibus-mozc-ut2/)
[emacs-mozc-ut2](https://aur.archlinux.org/packages/emacs-mozc-ut2/)
[uim-mozc-ut2](https://aur.archlinux.org/packages/uim-mozc-ut2/) |
| IBus integration |
| Emacs integration |
| uim integration | [uim-mozc](https://aur.archlinux.org/packages/uim-mozc/) |

Some of the above packages also contain definitions at the top of their respective PKGBUILDs that can be altered to (de)activate certain features. Most notably, to build the emacs packages you need to uncomment the `_emacs_mozc` line:

```
## If you will be using mozc.el on Emacs, uncomment below.
_emacs_mozc="yes"

```

Likewise, you must also enable uim-mozc-ut2 manually to build it.

Once Mozc is installed, you might need to restart X or your Input Method Framework before you can use it.

## Configuration

### IBus

*See also [IBus](/index.php/IBus "IBus") for IBus configuration.*

If you use Mozc by default, set it via *ibus-setup*:

```
$ ibus-setup

```

Choose *Input Method* tab and move *Mozc* to top of the list.

You can switch input method by `Alt+Shift_L` (by IBus default).

### uim

*See also [UIM](/index.php/UIM "UIM") for uim configuration.*

Configure uim preferences by running:

```
$ uim-pref-gtk (Or, uim-pref-gtk3/uim-pref-qt4)

```

which brings forth a GUI.

Choose your preferring input method as *Default input method*.

**Note:** Mozc will be not listed in *Default input method* at first time so you will need to add it into *Enabled input methods* to use.

**Warning:** You **must** run the following command whenever you upgrade or (re-)install **uim**.
# uim-module-manager --register mozc

### Fcitx

*See also [Fcitx](/index.php/Fcitx "Fcitx") for Fcitx configuration.*

Open the configuration dialog of Fcitx by running:

```
$ fcitx-configtool

```

In the *Input Method* tab, click on the plus sign and choose Mozc from the list in the dialog. Depending on your configuration, you might need to disable the *Only Show Current Language* option for Mozc to be available. After confirming the dialog, you can activate Mozc as input method using the usual keyboard shortcuts.

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

`C-\` (*toggle-input-method*) enables and disables use of mozc-mode.

#### Disabling XIM on Emacs

When you are using input method on your desktop and assigning activation/deactivation of input method to C-SPC, you will be not able to use C-SPC/C-@ as set-mark-command on Emacs. To avoid this problem, add the following into your `~/.Xresources` or `~/.Xdefaults`. xim will be disabled on Emacs.

```
Emacs*UseXIM: false

```

## Tips and tricks

### Confirming Mozc version which you are using now

Type "ばーじょん" ("version") and convert it while activating Mozc. The version number of Mozc will be shown in the candidate list like follows:

```
<u>ばーじょん</u>

```

```
バージョン
ヴァージョン
ばーじょん
Mozc-1.6.1187.102  *⇐ Current version of Mozc*
...
```

### Launching Mozc tools from command line

The followings are commands to launch Mozc tools.

*   Mozc Settings: `$ /usr/lib/mozc/mozc_tool --mode=config_dialog`
*   Mozc Dictionary Tool: `$ /usr/lib/mozc/mozc_tool --mode=dictionary_tool`
*   Mozc Word Register: `$ /usr/lib/mozc/mozc_tool --mode=word_register_dialog`
*   Mozc Hand Writing: `$ /usr/lib/mozc/mozc_tool --mode=hand_writing`
*   Mozc Character Palette: `$ /usr/lib/mozc/mozc_tool --mode=character_palette`

### Use CapsLock as Eisu_toggle key on ASCII layout keyboard

In all of the preset keymap styles of Mozc, the command *Toggle alphanumeric mode* on *Composition* mode is assigned to the `Eisu` (Eisu_toggle), `Hiragana/Katakana` or `Muhenkan` key, but the ASCII keyboard has none of them.

One solution for it is to use Caps Lock key as Eisu_toggle (Mozc does not recognize the Caps Lock key as of r124). The following is a way to assign Eisu_toggle to `Caps Lock` (without any modifier keys) and Caps_Lock to `Shift+CapsLock`, as on the OADG keyboard layout.

**Warning:** This will affect all applications.

Edit `~/.Xmodmap` as follows:

```
keycode 66 = Eisu_toggle Caps_Lock
clear Lock

```

Then, restart X or run *xmodmap* to apply the changes immediately:

```
$ xmodmap ~/.Xmodmap

```

## Troubleshooting

### Building Mozc fails (process is killed)

If the build process fails with an error message like the following:

```
...
/bin/sh: line 1:  xxxx killed
...
make: *** [xxx/xxx...] error 137
...

```

Make sure you have not run out of memory.

### New version of Mozc does not appear though I upgraded Mozc and restarted X or Input Method Framework (not rebooted)

The old version of Mozc may be still on your memory. Try to kill the existing *mozc_server* process:

```
$ killall mozc_server

```

### mozc_server becomes defunct

Mozc cannot run in root. Start X in normal user.