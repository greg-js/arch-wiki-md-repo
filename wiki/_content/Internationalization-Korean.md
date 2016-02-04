# Internationalization/Korean

This document provides instructions on how to set up a Korean language environment on an Arch linux installation. This document will not cover setting up Korean input on the console.

## Contents

*   [1 Fonts](#Fonts)
*   [2 Locale](#Locale)
*   [3 Input in Xorg](#Input_in_Xorg)
    *   [3.1 Choose a Korean input method](#Choose_a_Korean_input_method)
        *   [3.1.1 Current Issues](#Current_Issues)
    *   [3.2 Configuration](#Configuration)
        *   [3.2.1 ibus-hangul](#ibus-hangul)
        *   [3.2.2 uim-byeoru](#uim-byeoru)
        *   [3.2.3 scim-hangul](#scim-hangul)
        *   [3.2.4 fcitx-hangul](#fcitx-hangul)
        *   [3.2.5 nabi](#nabi)
    *   [3.3 Tips and Tricks](#Tips_and_Tricks)
        *   [3.3.1 Using the Right alt key to switch input methods](#Using_the_Right_alt_key_to_switch_input_methods)
        *   [3.3.2 Libreoffice](#Libreoffice)

## Fonts

To use any korean input method, you need to have Korean fonts installed. Install [ttf-nanum](https://aur.archlinux.org/packages/ttf-nanum/) or the [ttf-unfonts-core](https://aur.archlinux.org/packages/ttf-unfonts-core/) from the [AUR](/index.php/AUR "AUR"). If you also want Korean monospaced fonts, install [ttf-nanumgothic_coding](https://aur.archlinux.org/packages/ttf-nanumgothic_coding/) from the AUR. Alternatively, if you use the [Infinality](/index.php/Infinality "Infinality") patches and have the [Infinality-bundle-fonts repository](/index.php/Unofficial_user_repositories#infinality-bundle-fonts "Unofficial user repositories") enabled, you can install `ttf-nanum-fonts-ibx`, `ttf-nanumgothic-coding-ibx`, and `ttf-unfonts-core-ibx` from the `infinality-bundle-fonts` repository. If you want to view and use Yethangul(옛한글), install the [ttf-unfonts-core](https://aur.archlinux.org/packages/ttf-unfonts-core/) and/or the [ttf-hamchorom-lvt](https://aur.archlinux.org/packages/ttf-hamchorom-lvt/) fonts.

## Locale

You should have `ko_KR.UTF-8` enabled in `/etc/locale.gen`. It is recommended that you always use a `.UTF-8` locale rather than the `ko_KR.EUC-KR` locale. For more information, read [locale](/index.php/Locale "Locale").

## Input in Xorg

### Choose a Korean input method

Input method (IM) frameworks act as frontends to various input methods and libraries, allowing the user to switch between different languages with ease. Frameworks such as [IBus](/index.php/IBus "IBus"), [uim](/index.php/UIM "UIM"), [fcitx](/index.php/Fcitx "Fcitx") and [scim](/index.php/Scim "Scim"), as well as [nabi](https://aur.archlinux.org/packages/nabi/), a stand-alone Korean input method, support Korean input. This section will try to help you choose a suitable IM framework.

**Note:** Check the issues associated with each input method framework before choosing which one to use.

#### Current Issues

	ibus

	[IBus](/index.php/IBus "IBus") is the default input framework of [GNOME](/index.php/GNOME "GNOME") and Ubuntu. It is the most widely supported input method framework. As such, you can use ibus for inputting Korean without issue in most applications. However, there are some issues:

*   As of November 2014, ibus sometimes doesn't recognize user-set hotkeys for IM switching. This means that you may need to click on the ibus systray icon every time to want to switch input methods.

	uim

	[uim](/index.php/UIM "UIM") is a multilingual, cross-platform input method framework. The [uim](https://www.archlinux.org/packages/?name=uim) package in the official repositories includes uim-byeoru, the korean module for uim. uim-byeoru works well on most applications (including Google Chrome and Chromium) without issue. [opera](https://www.archlinux.org/packages/?name=opera) users, however, may want to avoid uim, as trying to use uim-byeoru in Opera may cause it to crash.

	scim

	scim, or the [Smart Common Input Method platform](/index.php/Smart_Common_Input_Method_platform "Smart Common Input Method platform"), is a input method framework for posix-compliant systems. scim-hangul, as of November 2014, has issues with Google Chrome and Chromium web browsers. With the default environment variables, you cannot input Korean in Google Chrome or Chromium. scim also causes problems in Gedit as of November 2014\. When scim-hangul is active, pressing `backspace` does not work properly. A workaround for both these issues will be explained in the scim configuration section. However, even with this workaround applied, Chrome/Chromium users may find that the preedit string disappears when the spacebar or any other modifier key is pressed. _There is currently no known workaround for this issue._

	fcitx

	[Fcitx](/index.php/Fcitx "Fcitx") is another input method framework for posix-compliant systems. Fcitx-hangul has issues with Google Chrome and Chromium. Some users have reported that fcitx only recognizes Google Chrome/Chromium's URL bar as an input window only after their themes have been changed.

	nabi

	[nabi](https://aur.archlinux.org/packages/nabi/) is a standalone Korean input method that is being developed by Choehwanjin. Nabi provides many unique features, such as Yethangul support. If you only need to use Korean and English input, you may want to install nabi. Currently, nabi causes an issue with chromium. When you press the spacebar, the preedit string will be placed after the space, causing your input to look like this: `한 글입력 에문제 가있습니다`

If you have chosen which framework to use, continue with the configuration section.

### Configuration

#### ibus-hangul

See [IBus](/index.php/IBus "IBus") for information about installing and configuring ibus.

#### uim-byeoru

Follow the instructions in [User:Isaac914/uim](/index.php/User:Isaac914/uim "User:Isaac914/uim") to install uim and to get it running. Return to this section after uim is installed and running as the default input method.

Open the uim preferences window by running :

```
$ uim-pref-gtk (Or, uim-pref-gtk3/uim-pref-qt4)

```

Within global settings, check on the _Specify default IM_ checkbox. Then, set _Byeoru_ as default. You may also want to disable input methods that you do not plan on using by clicking on the 'edit' button. If you want to quickly switch between Korean and other languages (other than English), check the _enable IM switching by hotkey_ checkbox, and set a hotkey to switch between enabled IMEs.

When you are done with the global preferences, find _Byeoru_ in the tree menu on the left side of the preferences window. From there, you can set the Korean keyboard layout you want to use (e.g. `3 beol`), specify the korean/Hanja dictionary that Byeoru will use, and other miscellaneous settings. Then, click on _Byeoru Keybinding 1_ in the tree menu. Set the hotkey you want to use to enable/disable Byeoru. Most Korean users use `Ctrl+space` or `shift+space`.

**Note:** If you want to use the right `Alt` key to switch from Korean to English and vice versa, go to the [#Using the Right alt key to switch input methods](#Using_the_Right_alt_key_to_switch_input_methods) section.

If all went properly, you should now be able to use UIM-byeoru to type in Korean.

#### scim-hangul

[Install](/index.php/Install "Install") [scim-hangul](https://www.archlinux.org/packages/?name=scim-hangul).

Now add the following to the user's `.xinitrc`, `.xprofile`, or `.xsession`:

```
export XMODIFIERS=@im=SCIM
export GTK_IM_MODULE="xim"
export QT_IM_MODULE="scim"
scim -d

```

**Note:** The above environment variables differ slightly from the ones recommended in the [scim](/index.php/Scim "Scim") article. We are adding `export GTK_IM_MODULE="xim"` instead of `GTK_IM_MODULE=”scim"`. This allows us to input Korean in apps such as Chrome and Chromium (though with issues discussed above), and to use backspace properly in GTK+3 applications such as gedit.

#### fcitx-hangul

[Install](/index.php/Install "Install") [fcitx-hangul](https://www.archlinux.org/packages/?name=fcitx-hangul) and the gui frontend of your choice. fcitx configuration frontends include: [fcitx-gtk2](https://www.archlinux.org/packages/?name=fcitx-gtk2), [fcitx-gtk3](https://www.archlinux.org/packages/?name=fcitx-gtk3), [fcitx-qt4](https://www.archlinux.org/packages/?name=fcitx-qt4), [fcitx-qt5](https://www.archlinux.org/packages/?name=fcitx-qt5).

If you are using KDE, also install [kcm-fcitx](https://www.archlinux.org/packages/?name=kcm-fcitx), in order to have the fcitx configuration integrated into KDE's system settings.

Once fcitx is installed, edit your `.xinitrc`, `.xprofile`, or `.xsession` file to include:

```
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx

```

#### nabi

[Install](/index.php/Arch_User_Repository#Installing_packages "Arch User Repository") the [nabi](https://aur.archlinux.org/packages/nabi/) package from the AUR.

If you want the latest version of nabi, run `git clone [https://github.com/choehwanjin/nabi.git](https://github.com/choehwanjin/nabi.git)`, `cd` into the cloned git repo, check if you have all the necessary libraries for building nabi by running `./configure`, and then run `make`. When make finishes building the binary, run `make install` as root.

Once you have finished the installation, add the following to `.xprofile`, `.xinitrc`, or `xsession`:

```
export XIM=nabi
export XIM_ARGS=
export XIM_PROGRAM="nabi"
export XMODIFIERS="@im=nabi"
export GTK_IM_MODULE=xim
export QT_IM_MODULE=xim

```

Once you restart the X session, nabi will autostart by default. The default korean keyboard layout is Dubeolsik(두벌식). If you need a different korean keyboard layout (e.g. Sebeolsik or Dubeolsik Yetgul), click on the system tray icon of nabi, and select a input method from the menu that pops up.

### Tips and Tricks

#### Using the Right alt key to switch input methods

You can use the right `Alt` key (e.g. '한/영키') to switch between Input methods if you are using uim, scim, or nabi. To do this, add the following lines **after** the environment variables that start your input method:

 `~/.xprofile` 

```
xmodmap -e 'remove mod1 = Alt_R'
xmodmap -e 'keycode 108 = Hangul'
xmodmap -e 'remove control = Control_R'
xmodmap -e 'keycode 105 = Hangul_Hanja'

```

Then, in the settings of your input method, add the right `Alt` key as a hotkey to switch IMEs. The right `Alt` key has been remapped to a non-modifier key called "Hangul". The script above also allows you to use the right `Ctrl` key (e.g. '한자키') to activate Hanja input. The right `Ctrl` key should also have been remapped to "Hangul_Hanja". Add this key as a Hanja hotkey within the settings of your input method. If adding that to your `.xprofile` or `.xinitrc` file did not work, create a script containing those four lines and set it to auto execute when your desktop environment starts up.

#### Libreoffice

In some cases, Libreoffice will not take Korean input from any input method. To resolve this issue, try adding `export OOO_FORCE_DESKTOP="gnome"` to `.xinitrc`, `.xprofile`, or `.xsession`.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Internationalization/Korean&oldid=407729](https://wiki.archlinux.org/index.php?title=Internationalization/Korean&oldid=407729)"