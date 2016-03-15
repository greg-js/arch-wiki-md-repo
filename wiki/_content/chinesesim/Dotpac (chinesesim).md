[dotpac](https://aur.archlinux.org/packages.php?do_Details=1&ID=3017) 帮你去除 /{boot,etc}/*.pac* 文件

贡献者 Jaroslaw Swierczynski <swiergot@juvepoland.com>

* * *

我写这个简单的脚本用于一次性整理我/etc文件夹下的.pacnew 和 .pacsave 文件。我已经厌倦每天做这些重复的动作了(一次又一次地find, diff, vi, mv, rm......) 更糟糕的是每天重复手动做这个工作经常出问题。

此外,这个脚本对于不知道这些文件从何而来的新手来说会很有用（它们都是pacman搞出来的。）

你只需要运行dotpac (抱歉, 我没有什么时间给它起个好名字) 看它过一过运行信息。别担心，没有你的指示dotpac就不会更改系统的任何东西。 也请注意本脚本在工作期间并不会自动一并删除 *.pac* 文件。

对这个脚本有建议、疑问、点子还有想提交bug都可以联系我，随时欢迎。