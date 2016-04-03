[DOSBox](http://www.dosbox.com/) 是一个x86 PC平台DOS模拟器，用于运行DOS游戏和DOS程序。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
*   [3 使用](#.E4.BD.BF.E7.94.A8)
*   [4 提示](#.E6.8F.90.E7.A4.BA)
*   [5 更多请看](#.E6.9B.B4.E5.A4.9A.E8.AF.B7.E7.9C.8B)

## 安装

从[官方仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)") [安装](/index.php/Pacman "Pacman") [dosbox](https://www.archlinux.org/packages/?name=dosbox)

## 配置

无需初始化配置, 尽管DOSBox官方手册提供一个名为“dosbox.conf”的配置文件以供参阅。那个文件默认在你的`~/.dosbox`目录.

你可以通过从`~/.dosbox`复制“dosbox.conf”来创建一个新的配置文件，放在每个DOS程序所在目录并单独修改。你也可以自动生成一个配置文件: 只需在你希望的程序目录里不带任何参数运行`dosbox`:

```
$ dosbox

```

然后在DOS提示符后，手打：

```
Z:\> config -wc dosbox.conf

```

然后配置文件“dosbox.conf”会被保存到正确目录。然后怎样配置随你便了。

配置选项在官方DosBox维基有描述: [http://www.dosbox.com/wiki/Dosbox.conf](http://www.dosbox.com/wiki/Dosbox.conf).

## 使用

把你的DOS游戏（或者其安装文件）放在一个目录里，然后运行dosbox，后面要加上那个目录。举个栗子:

```
$ dosbox ./game-folder/

```

你现在应该看到一个DOS提示符，你上面设定的那个目录已变成它的工作目录。然后你就可以运行你想运行的程序啦。

```
C:\> SETUP.EXE

```

## 提示

如果dosbox获取了你的焦点（鼠标的？），你可以按`CTRL+F10`来释放。

## 更多请看

*   [http://www.dosbox.com/](http://www.dosbox.com/) - DOSBox官网。
*   [http://www.abandonia.com/](http://www.abandonia.com/) - Abandonia: 最大的旧dos游戏仓库。
*   [http://www.dosgames.com/](http://www.dosgames.com/) - DosGames.com: 最大的dos游戏仓库。