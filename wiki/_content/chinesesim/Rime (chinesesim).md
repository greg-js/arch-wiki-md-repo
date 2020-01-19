**翻译状态：** 本文是英文页面 [Rime](/index.php/Rime "Rime") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2020-01-16，点击[这里](https://wiki.archlinux.org/index.php?title=Rime&diff=0&oldid=594862)可以查看翻译后英文页面的改动。

**[Rime](https://rime.github.io/)**是一款支持多种输入方案的输入法引擎，可用于[Fcitx](/index.php/Fcitx_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fcitx (简体中文)")和[IBus](/index.php/IBus_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "IBus (简体中文)")等输入法框架。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 配置](#配置)
*   [3 使用](#使用)
    *   [3.1 选择输入方案](#选择输入方案)
    *   [3.2 中文标点](#中文标点)
    *   [3.3 高级](#高级)
*   [4 参见](#参见)

## 安装

先安装[librime](https://www.archlinux.org/packages/?name=librime)，再根据所使用的输入法框架安装[ibus-rime](https://www.archlinux.org/packages/?name=ibus-rime)或[fcitx-rime](https://www.archlinux.org/packages/?name=fcitx-rime)。

## 配置

**Note:** Rime与[ibus](https://www.archlinux.org/packages/?name=ibus)或[fcitx](https://www.archlinux.org/packages/?name=fcitx)一同使用。参见[IBus (简体中文)](/index.php/IBus_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "IBus (简体中文)")和[Fcitx (简体中文)](/index.php/Fcitx_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fcitx (简体中文)")了解更多有关安装和配置的信息。

在使用Rime之前，需要安装输入方案。输入方案可由用户定制。[默认输入方案](https://github.com/rime/brise#packages)如下：

*   现代标准汉语：
    *   朙月拼音
    *   地球拼音（带声调）
    *   注音符号
*   拼音变体：
    *   双拼（自然码、微软拼音）
*   方言：
    *   粤拼
    *   吴语
*   字形输入法：
    *   仓颉
    *   五笔

你可以在任何时间通过按下 `F4` 调出菜单来切换输入法。参见[选择输入方案](#选择输入方案)。

要自定义 Rime，首先需要创建 rime 的配置文件夹。 如果你在使用 [ibus-rime](https://www.archlinux.org/packages/?name=ibus-rime)：

```
$ mkdir ~/.config/ibus/rime

```

或者你在使用 [fcitx-rime](https://www.archlinux.org/packages/?name=fcitx-rime)：

```
$ mkdir ~/.config/fcitx/rime/

```

在文件夹中创建 `default.custom.yaml` 文件，以便于指定可选的输入法。例如，如果你想要按照声调来输入拼音，你可以通过添加下列内容来使用地球拼音：

 `default.custom.yaml` 
```
patch:
  schema_list:
    - schema: terra_pinyin

```

注意：缩进级别是很重要的。这个文件会覆盖默认的配置文件，因此如果只添加了地球拼音，那么将只有这一个选择。

要使得自定义生效，需要进行重新部署。如果你在使用 ibus 或 fcitx 的 图形界面，你可以找到 ⟲ (部署) 按钮。 或者使用以下的命令：

如果你在使用 [ibus-rime](https://www.archlinux.org/packages/?name=ibus-rime)：

```
$ rm ~/.config/ibus/rime/default.yaml && ibus-daemon -drx

```

或者你在使用 [fcitx-rime](https://www.archlinux.org/packages/?name=fcitx-rime)：

```
$ rm ~/.config/fcitx/rime/default.yaml && fcitx-remote -r

```

注意：声调是可选的，你可以使用它来很好地过滤列表。以下是如何使用：

```
第一声： -
第二声： /
第三声： <
第四声： \

```

例如，如果想要打出发音为 `hǎo` 的字，需要输入 `hao<` ，输入法会自动将其转换为 hǎo 。

默认情况下，Rime 只会列出5个候选项，可以通过修改 `"menu/page_size"` 的值来手动更改列出候选项的个数

 `default.custom.yaml` 
```
patch:
     "menu/page_size": 9

```

## 使用

Rime 有一些十分优秀的特质，使之能够很好地输入中文字符和标点

### 选择输入方案

不论何时，在使用 Rime 的时候，你都可以通过 `F4` 来进行基础设置。显示的设置项如下：

```
1.　输入法名称
2\. 中文　－›　西文
3\. 全角　－›　半角
4\. 漢字　－›　汉字
...

```

第一项显示的是输入方案的名称，如果你开启了多个输入方案，那将能够在其中进行切换

第二项选择输入中文或英语

第三项选择输入全角或半角标点

最后一项选择输入简体中文或繁体中文

### 中文标点

按下列各键输入不同的符号：

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

### 高级

更多示例和个性化设置方法参见 [https://github.com/rime/home/wiki/CustomizationGuide](https://github.com/rime/home/wiki/CustomizationGuide) 。

## 参见

*   [官网](https://rime.github.io/)
*   [GitHub wiki](https://github.com/rime/home/wiki)