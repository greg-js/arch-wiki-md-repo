**mikutter**是由toshi_a桑开发的一个开源的Twitter客户端. mikutter 的开发使用了 [Arch Linux (简体中文)](/index.php/Arch_Linux_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Linux (简体中文)") 和 [ruby](/index.php/Ruby "Ruby") (其中GUI使用了 [GTK](/index.php/GTK "GTK")).(我爱miku)

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 插件](#.E6.8F.92.E4.BB.B6)
*   [3 参阅](#.E5.8F.82.E9.98.85)

## 安装

mikutter 可以通过[AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)")来安装。同时你应该安装[ruby](https://www.archlinux.org/packages/?name=ruby).

```
$ yaourt -S mikutter

```

## 配置

### 插件

mikutter可以通过安装插件来扩展机能(比如煮咖啡←雾)。 要安装插件的话, 请放置`~/.mikutter/plugin`下的`.rb`文件, 创建插件名的目录, 并且在那个目录中对名为`插件名.rb`的文件进行设置.

	[miku商店](https://github.com/toshia/mikustore)

	插件管理。

## 参阅

*   [mikutter 公式サイト](http://mikutter.hachune.net/)
*   [mikutter news](http://mikutter.tumblr.com/)
*   [Writing mikutter plugin](http://toshia.github.com/writing-mikutter-plugin/)
*   [mikutter開発日記](http://mikutter.blogspot.jp/)