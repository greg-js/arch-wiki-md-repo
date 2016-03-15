**翻译状态：** 本文是英文页面 [Configure_virtual_console_colors](/index.php/Configure_virtual_console_colors "Configure virtual console colors") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-02-04，点击[这里](https://wiki.archlinux.org/index.php?title=Configure_virtual_console_colors&diff=0&oldid=359136)可以查看翻译后英文页面的改动。

改变Linux虚拟控制台中的颜色样式.可以通过编写转义字符`\\e]PXRRGGBB`来实现，`X`处为0-F的十六进制颜色索引字符，`RRGGBB`处为传统的十六进制调色板代码。

## 重新利用 ~/.Xdefaults 中的配置

重新利用~/.Xdefaults中的颜色配置, 请把下面的代码片段加入到shell脚本中，如(`.bashrc`/`.zshrc`/...)。

```
if [ "$TERM" = "linux" ]; then
    _SEDCMD='s/.*\*color\([0-9]\{1,\}\).*#\([0-9a-fA-F]\{6\}\).*/\1 \2/p'
    for i in $(sed -n "$_SEDCMD" $HOME/.Xdefaults | \
               awk '$1 < 16 {printf "\\e]P%X%s", $1, $2}'); do
        echo -en "$i"
    done
    clear
fi

```

## 更改虚拟控制台启动界面

修改默认的登陆界面。 请先备份原先的`/etc/issue`文件，比如加上后缀：`mv /etc/issue /etc/issue.bak`. 在`/etc/`目录中新建一个名为`issue`的文件，并输入以下文字：

```
echo -e '\e[H\e[2J' > issue
echo -e '                                                            \e[1;30m| \e[34m\\s \\r' >> issue
echo -e '       \e[36;1m/\\\\                      \e[37m||     \e[36m| |                   \e[30m|' >> issue
echo -e '      \e[36m/  \\\\                     \e[37m||     \e[36m|     _               \e[30m| \e[32m\\t' >> issue
echo -e '     \e[1;36m/ \e[0;36m.. \e[1m\\\\   \e[37m//==\\\\\\\\ ||/= /==\\\\ ||/=\\\\  \e[36m| | |/ \\\\ |  | \\\\ /     \e[30m| \e[32m\\d' >> issue
echo -e '    \e[0;36m/ .  . \\\\  \e[37m||  || ||   |    ||  || \e[36m| | |  | |  |  X      \e[1;30m|' >> issue
echo -e '   \e[0;36m/  .  .  \\\\ \e[37m\\\\\\\\==/| ||   \\\\==/ ||  || \e[36m| | |  | \\\\_/| / \\\\     \e[1;30m| \e[31m\\U' >> issue
echo -e '  \e[0;36m/ ..    .. \\\\   \e[0;37mA simple, lightweight linux distribution.  \e[1;30m|' >> issue
echo -e ' \e[0;36m/_\x27        `_\\\\                                             \e[1;30m| \e[35m\\l \e[0mon \e[1;33m\
' >> issue
echo -e ' \e[0m' >> issue
echo -e * >> issue*

```

保存文件,然后执行命令 `chmod +x issue`完成更改。

如想恢复原先的`issue`文件，只需键入以下命令:

```
`mv /etc/issue /etc/issue.old && mv /etc/issue.bak /etc/issue`.

```

原文与原作者链接: [https://bbs.archlinux.org/viewtopic.php?pid=386429#p386429](https://bbs.archlinux.org/viewtopic.php?pid=386429#p386429)