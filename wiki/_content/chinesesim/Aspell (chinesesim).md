**翻译状态：** 本文是英文页面 [Aspell](/index.php/Aspell "Aspell") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-09-11，点击[这里](https://wiki.archlinux.org/index.php?title=Aspell&diff=0&oldid=489440)可以查看翻译后英文页面的改动。

[官方网站](http://aspell.net/): "GNU Aspell 是一个自由、开源的拼写检查工具，目的是取代 Ispell. 可以单独使用，也可以作为库文件使用."

## Contents

*   [1 安装](#安装)
*   [2 使用](#使用)
*   [3 问题处理](#问题处理)
    *   [3.1 拼写检查说所有文本都是错误的](#拼写检查说所有文本都是错误的)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 需要的 [aspell 字典](https://www.archlinux.org/packages/?sort=&q=aspell-)，安装时会同时安装 [aspell](https://www.archlinux.org/packages/?name=aspell) 依赖包。

## 使用

很多程序会自动使用 *aspell*，无需额外配置。用户也可以手动执行 *aspell*，参考 [aspell(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/aspell.1).

对单个文件执行拼写检查:

```
$ aspell check *somefile*

```

执行后会出现文本提示，可以选择让 *aspell* 修正扫描到的错误或忽略建议，进行的修正会保存到文件中。

显示拼写错误的单词:

```
$ cat *somefile* | aspell list

```

## 问题处理

### 拼写检查说所有文本都是错误的

如果安装字典也没用，可能是`enchant`出问题了。查看aspell识别到的词典文件：

 `$ aspell dicts` 
```
en
en_GB
...etc
```

如果你需要的语言不在其中，添加下面的内容到`/usr/share/enchant/enchant.ordering`：

```
en_GB:aspell # 以en_GB为例

```