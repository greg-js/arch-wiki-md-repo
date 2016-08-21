**翻译状态：** 本文是英文页面 [Dvorak](/index.php/Dvorak "Dvorak") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-08-19，点击[这里](https://wiki.archlinux.org/index.php?title=Dvorak&diff=0&oldid=435865)可以查看翻译后英文页面的改动。

本文是一个快速参考手册，可以设置你的键盘映射从qwerty转换到Dvorak.

## Contents

*   [1 设置 Dvorak 键盘布局](#.E8.AE.BE.E7.BD.AE_Dvorak_.E9.94.AE.E7.9B.98.E5.B8.83.E5.B1.80)
*   [2 国际用户](#.E5.9B.BD.E9.99.85.E7.94.A8.E6.88.B7)
    *   [2.1 Swedish](#Swedish)
    *   [2.2 Spanish](#Spanish)
*   [3 打字练习软件](#.E6.89.93.E5.AD.97.E7.BB.83.E4.B9.A0.E8.BD.AF.E4.BB.B6)

## 设置 Dvorak 键盘布局

设置方法请阅读 [终端设置](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") 和 [Xorg 设置](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg") 。

下面布局可以同时在终端和 Xorg 中使用：

*   `dvorak`, 标准 Dvorak
*   `dvorak-l`, 左手布局
*   `dvorak-r`, 右手布局

**Note:** 终端有单独的键盘映射，但是 Xorg 有 `us` 布局变体，需要传递给 `XkbVariant` 变量，参考 [Keyboard configuration in Xorg#Setting keyboard layout](/index.php/Keyboard_configuration_in_Xorg#Setting_keyboard_layout "Keyboard configuration in Xorg")。

下面的国际 Dvorak 仅能在 Xorg 中使用:

*   `dvorak-intl`, international layout with dead keys

## 国际用户

### Swedish

Swedish 用户可以选择使用 swedish "dvorak 版本"，被称为 svorak，要将 X 切换到 svorak，并不需要从 www.aoeu.info 下载额外文件。

### Spanish

要使用西班牙 dvorak 变体，使用 `dvorak-es` 替换 `dvorak`。

在 Xorg 中将 `XkbLayout` 设置为 `es`， `XkbVariant` 设置为 `dvorak`.

## 打字练习软件

*   终端: [DvorakNG](https://aur.archlinux.org/packages/DvorakNG/)
*   GUI: [KTouch](https://www.archlinux.org/packages/extra/x86_64/kdeedu-ktouch/) (包含了英语、法语、德语和西班牙语的 Dvorak 课程)
*   GUI: [klavaro](https://www.archlinux.org/packages/?name=klavaro) Dvorak 课程: (BG; BR; DE_neo2; EO; FR; FR_bépo; TR; UK; US; US_BR; US_ES; US_SE)