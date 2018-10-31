[WPS Office for Linux](https://www.wps.com/linux) is an efficient,stable and compatible alternative for microsoft office with modern UI which supports cross-device file transfer,cloud backup.The suite contains writer,presentation and spreadsheet

## Contents

*   [1 installation](#installation)
*   [2 Language aids](#Language_aids)
    *   [2.1 interface language](#interface_language)
    *   [2.2 Spell checking](#Spell_checking)
*   [3 Theme](#Theme)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 What is the command to start WPS Office](#What_is_the_command_to_start_WPS_Office)
    *   [4.2 formula can not display normally](#formula_can_not_display_normally)
    *   [4.3 Microsoft Office file in KDE is recognized as Zip](#Microsoft_Office_file_in_KDE_is_recognized_as_Zip)
    *   [4.4 Fcitx imput method framework can't input on WPS](#Fcitx_imput_method_framework_can.27t_input_on_WPS)
*   [5 See also](#See_also)

## installation

install [wps-office](https://aur.archlinux.org/packages/wps-office/) from [AUR](/index.php/AUR "AUR")

**Note:**

*   you can optionally install the font wps need:[ttf-wps-fonts](https://aur.archlinux.org/packages/ttf-wps-fonts/)

## Language aids

### interface language

To change interface lannguage of WPS you can install [wps-office-mui-fr-fr](https://aur.archlinux.org/packages/wps-office-mui-fr-fr/) for French,[wps-office-mui-ja-jp](https://aur.archlinux.org/packages/wps-office-mui-ja-jp/) for Japanese,etc.Then set your language by selecting *Review->Spell Check->Set Language* to choose your language and restart WPS.

### Spell checking

For spell checking,you need to install [wps-office-extension-german-dictionary](https://aur.archlinux.org/packages/wps-office-extension-german-dictionary/)for German,[wps-office-extension-french-dictionary](https://aur.archlinux.org/packages/wps-office-extension-french-dictionary/)for French,etc.Then,customize spell check by selecting *Tool -> Options -> Language -> choose* to choose your language and restart WPS.

## Theme

## Troubleshooting

### What is the command to start WPS Office

wps,et,wpp is the command to start WPS Writer,WPS Spreadsheet and WPS Presentation

### formula can not display normally

the display of most Mathematical formula need fonts show below:

```
symbol.ttf webdings.ttf wingding.ttf wingdng2.ttf wingdng3.ttf monotypesorts.ttf MTExtra.ttf

```

[ttf-wps-fonts](https://aur.archlinux.org/packages/ttf-wps-fonts/) in [AUR](/index.php/AUR "AUR") contain all of these fonts except *monotypesorts.ttf*,you can install it directly.

### Microsoft Office file in KDE is recognized as Zip

after install WPS Office,Microsoft Office file will be recognized as zip,and can't open with WPS,you can change this kind of recognition by delete mime file in */usr/share/packages/*:

```
sudo rm /usr/share/mime/packages/wps-office-*.xml
sudo update-mime-database /usr/share/mime

```

### Fcitx imput method framework can't input on WPS

add following lines to /usr/bin/wps /usr/bin/et /usr/bin/wpp seperately to add fcitx to writer,spreadsheet and presentation:

```
export XMODIFIERS="@im=fcitx"
export QT_IM_MODULE="fcitx"

```

## See also

*   [WPS Office Community](http://wps-community.org/)
*   [WPS For Linux(Chinese)](http://www.wps.cn/product/wpslinux/)