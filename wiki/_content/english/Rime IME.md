**[Rime IME](https://rime.github.io/)** is an input method engine for entering Chinese characters supporting a wide range of input methods. Rime IME can be used with the [IBus](/index.php/IBus "IBus") and [Fcitx](/index.php/Fcitx "Fcitx") input method frameworks.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
    *   [3.1 Selecting Input Method](#Selecting_Input_Method)
    *   [3.2 Chinese punctuation](#Chinese_punctuation)
    *   [3.3 Advanced](#Advanced)
*   [4 See also](#See_also)

## Installation

Rime IME is provided by [librime](https://www.archlinux.org/packages/?name=librime) and can be used with [ibus-rime](https://www.archlinux.org/packages/?name=ibus-rime) or [fcitx-rime](https://www.archlinux.org/packages/?name=fcitx-rime).

## Configuration

**Note:** Rime works with [ibus](https://www.archlinux.org/packages/?name=ibus) or [fcitx](https://www.archlinux.org/packages/?name=fcitx). Please see also [IBus](/index.php/IBus "IBus") and [Fcitx](/index.php/Fcitx "Fcitx") for installation and configuration.

In order for Rime to work, input schemas are needed. Schemas are text files that can be created and customized by users. Alternatively, there are several [default input schemas](https://github.com/rime/brise#packages) you can choose from:

*   Luna Pinyin (Standard Mandarin)
*   Terra Pinyin (with tones)
*   Zhuyin (Mandarin Phonetic Symbol)
*   Double Pinyin (Ziranma, MSPY)
*   Jyutping (Cantonese)
*   Wugniu (Wuu)
*   Cangjie5
*   Wubi86

You can switch input schema at any time by pressing `F4` to trigger the program menu. See [Selecting Input Method](#Selecting_Input_Method).

To customize Rime, you should first create the rime config directory. Assuming you are using [ibus-rime](https://www.archlinux.org/packages/?name=ibus-rime):

```
$ mkdir ~/.config/ibus/rime

```

Or if you are using [fcitx-rime](https://www.archlinux.org/packages/?name=fcitx-rime):

```
$ mkdir ~/.config/fcitx/rime/

```

In this directory, create a file named `default.custom.yaml`, where you can specify your input schema of choice. For example, if you want to be able to type pinyin with tones, you can use the Terra Pinyin input method by adding it to the list of enabled schemas:

 `default.custom.yaml` 
```
patch:
  schema_list:
    - schema: terra_pinyin

```

Note that the indentation level is important. This file overrides the default configuration. So if you only add Terra Pinyin, it will be the only schema enabled.

To make the customizations effective, you need to redeploy. If you have working ibus or fcitx GUI, you may find a ⟲ (Deploy) button and click it. Alternatively, use the following command, assuming you are using [ibus-rime](https://www.archlinux.org/packages/?name=ibus-rime):

```
$ rm ~/.config/ibus/rime/default.yaml && ibus-daemon -drx

```

Or if you are using [fcitx-rime](https://www.archlinux.org/packages/?name=fcitx-rime):

```
$ rm ~/.config/fcitx/rime/default.yaml && fcitx-remote -r

```

Note: Tones are optionals but you can type them to filter the list very well. Here is how to type them:

```
1st tone: -
2nd tone: /
3rd tone: <
4th tone: \

```

Example: if one wants to type `hǎo` to display only Chinese characters that are pronounced this way, one must type `hao<` and it will be automatically converted to hǎo.

By default, RIME only displays five candidates for input whilst typing. You can change this by setting the `"menu/page_size"` value manually.

 `default.custom.yaml` 
```
patch:
     "menu/page_size": 9

```

## Usage

Rime provides some great features that allow you to write Chinese characters and its punctuation well.

### Selecting Input Method

At any time, while running Rime, you can access some basic options with `F4`. The displayed options look like this:

```
1.　Method name
2\. 中文　－›　西文
3\. 全角　－›　半角
4\. 漢字　－›　汉字
etc.

```

The first one indicates the name of the method you have selected (Ex: 地球拼音 for Terra Pinyin). If you have enabled multiple input methods, you can switch between them.

The second one lets you switch between Chinese and western languages.

The third one lets you select if you want to type the punctuation in full width (全角) or in half width (半角).

The last one allows you to switch between traditional Chinese (漢字) and simplified Chinese (汉字).

### Chinese punctuation

You have access to all the Chinese punctuation thanks to Rime. Here is a little table showing you how to type some of them:

```
[ -> 「　【　〔　［
] ->　」　】　〕　］
{ ->　『　〖　｛
} ->　』　〗　｝
< ->　《　〈　«　‹
> ->　》　〉　»　›
@ ->　＠　@　☯
/ ->　／　/　÷
* ->　＊　*　・　×　※
% ->　％　%　°　℃
$ ->　￥　$　€　£　¥
| ->　・　｜　|　§　¦
_ -> ——
\ ->　、　＼　\
^ ->　……
~ ->　〜　~　～　〰

```

### Advanced

Rime allows you to change everything you can imagine and more examples are provided on the website of the project (in Chinese): [https://github.com/rime/home/wiki/CustomizationGuide](https://github.com/rime/home/wiki/CustomizationGuide)

## See also

*   [Rime IME official site](https://rime.github.io/)
*   [Rime IME Wiki at Github](https://github.com/rime/home/wiki)