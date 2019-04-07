Related articles

*   [Internationalization](/index.php/Internationalization "Internationalization")

This article describes how to set up a Korean language environment. It does not cover setting up Korean input on the console.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Fonts](#Fonts)
*   [2 Locale](#Locale)
*   [3 Input methods](#Input_methods)
    *   [3.1 Configuration](#Configuration)
        *   [3.1.1 Nabi](#Nabi)
        *   [3.1.2 scim-hangul](#scim-hangul)
        *   [3.1.3 uim-byeoru](#uim-byeoru)
    *   [3.2 Troubleshooting](#Troubleshooting)
        *   [3.2.1 Libreoffice](#Libreoffice)
    *   [3.3 Tips and Tricks](#Tips_and_Tricks)
        *   [3.3.1 Using the Right alt key to switch input methods](#Using_the_Right_alt_key_to_switch_input_methods)

## Fonts

To use any Korean input method, you need to have Korean fonts installed. Install [ttf-nanum](https://aur.archlinux.org/packages/ttf-nanum/) from the [AUR](/index.php/AUR "AUR"). If you also want Korean monospaced fonts, install [ttf-nanumgothic_coding](https://aur.archlinux.org/packages/ttf-nanumgothic_coding/) from the AUR. If you want to view and use Yethangul(옛한글), install [ttf-unfonts-core-ibx](https://aur.archlinux.org/packages/ttf-unfonts-core-ibx/) or [ttf-kopubworld](https://aur.archlinux.org/packages/ttf-kopubworld/)/[otf-kopubworld](https://aur.archlinux.org/packages/otf-kopubworld/) font.

See also [Fonts#Korean](/index.php/Fonts#Korean "Fonts").

## Locale

You should have `ko_KR.UTF-8` enabled in `/etc/locale.gen`. It is recommended that you always use a `.UTF-8` locale rather than the `ko_KR.EUC-KR` locale. For more information, read [locale](/index.php/Locale "Locale").

## Input methods

The following [input methods](/index.php/Input_method "Input method") are available for Korean:

*   [fcitx-hangul](https://www.archlinux.org/packages/?name=fcitx-hangul) for [Fcitx](/index.php/Fcitx "Fcitx")
*   [ibus-hangul](https://www.archlinux.org/packages/?name=ibus-hangul) for [IBus](/index.php/IBus "IBus")
*   [scim-hangul](https://aur.archlinux.org/packages/scim-hangul/) for [SCIM](/index.php/SCIM "SCIM")
*   *uim-byeoru* of [uim](/index.php/Uim "Uim")
*   [Nimf](/index.php/Nimf "Nimf")
*   [#Nabi](#Nabi)

### Configuration

#### Nabi

[Nabi](https://github.com/libhangul/nabi) is a standalone Korean input method, developed by Choe Hwanjin, offering many unique features, such as Yethangul support.

[Install](/index.php/Install "Install") the [nabi-git](https://aur.archlinux.org/packages/nabi-git/) package.

Once you have finished the installation, add the following to [xprofile](/index.php/Xprofile "Xprofile"), [xinitrc](/index.php/Xinitrc "Xinitrc"), or `xsession`:

```
export XIM=nabi
export XIM_ARGS=
export XIM_PROGRAM="nabi"
export XMODIFIERS="@im=nabi"
export GTK_IM_MODULE=xim
export QT_IM_MODULE=xim

```

Once you restart the X session, nabi will autostart by default. The default Korean keyboard layout is Dubeolsik(두벌식). If you need a different Korean keyboard layout (e.g. Sebeolsik or Dubeolsik Yetgul), click on the system tray icon of nabi, and select a input method from the menu that pops up.

#### scim-hangul

[Install](/index.php/Install "Install") [scim-hangul](https://aur.archlinux.org/packages/scim-hangul/).

Now add the following to the user's `.xinitrc`, `.xprofile`, or `.xsession`:

```
export XMODIFIERS=@im=SCIM
export GTK_IM_MODULE="xim"
export QT_IM_MODULE="scim"
scim -d

```

**Note:** The above environment variables differ slightly from the ones recommended in the [scim](/index.php/Scim "Scim") article. We are adding `export GTK_IM_MODULE="xim"` instead of `GTK_IM_MODULE=”scim"`. This allows us to input Korean in apps such as Chrome and Chromium (though with issues discussed above), and to use backspace properly in GTK+3 applications such as gedit.

#### uim-byeoru

Follow the instructions in [User:Isaac914/uim](/index.php/User:Isaac914/uim "User:Isaac914/uim") to install uim and to get it running. Return to this section after uim is installed and running as the default input method.

Open the uim preferences window by running :

```
$ uim-pref-gtk (Or, uim-pref-gtk3/uim-pref-qt4)

```

Within global settings, check on the *Specify default IM* checkbox. Then, set *Byeoru* as default. You may also want to disable input methods that you do not plan on using by clicking on the 'edit' button. If you want to quickly switch between Korean and other languages (other than English), check the *enable IM switching by hotkey* checkbox, and set a hotkey to switch between enabled IMEs.

When you are done with the global preferences, find *Byeoru* in the tree menu on the left side of the preferences window. From there, you can set the Korean keyboard layout you want to use (e.g. `3 beol`), specify the korean/Hanja dictionary that Byeoru will use, and other miscellaneous settings. Then, click on *Byeoru Keybinding 1* in the tree menu. Set the hotkey you want to use to enable/disable Byeoru. Most Korean users use `Ctrl+space` or `shift+space`.

**Note:** If you want to use the right `Alt` key to switch from Korean to English and vice versa, go to the [#Using the Right alt key to switch input methods](#Using_the_Right_alt_key_to_switch_input_methods) section.

If all went properly, you should now be able to use UIM-byeoru to type in Korean.

### Troubleshooting

	[IBus](/index.php/IBus "IBus")

	As of November 2014, IBus sometimes doesn't recognize user-set hotkeys for IM switching. This means that you may need to click on the IBus systray icon every time to want to switch input methods.

	[uim](/index.php/Uim "Uim")

	*uim-byeoru* may cause [Opera](/index.php/Opera "Opera") to crash.

	scim

	scim-hangul, as of November 2014, has issues with Google Chrome and [Chromium](/index.php/Chromium "Chromium") web browsers. With the default environment variables, you cannot input Korean in Google Chrome or Chromium. scim also causes problems in Gedit as of November 2014\. When scim-hangul is active, pressing `backspace` does not work properly. A workaround for both these issues will be explained in [#scim-hangul](#scim-hangul). However, even with this workaround applied, Chrome/Chromium users may find that the preedit string disappears when the spacebar or any other modifier key is pressed. *There is currently no known workaround for this issue.*

	fcitx

	Fcitx-hangul has issues with Google Chrome and Chromium. Some users have reported that fcitx only recognizes Google Chrome/Chromium's URL bar as an input window only after their themes have been changed.

	nabi

	[nabi-git](https://aur.archlinux.org/packages/nabi-git/) is a standalone Korean input method that is being developed by Choehwanjin. Nabi provides many unique features, such as Yethangul support. If you only need to use Korean and English input, you may want to install nabi. Currently, nabi causes an issue with chromium. When you press the spacebar, the preedit string will be placed after the space, causing your input to look like this: `한 글입력 에문제 가있습니다`

#### Libreoffice

In some cases, Libreoffice will not take Korean input from any input method. To resolve this issue, try adding `export OOO_FORCE_DESKTOP="gnome"` to `.xinitrc`, `.xprofile`, or `.xsession`.

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