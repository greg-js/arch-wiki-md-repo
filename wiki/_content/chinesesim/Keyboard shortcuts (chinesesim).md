<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 内核](#内核)
*   [2 终端](#终端)
    *   [2.1 虚拟控制台](#虚拟控制台)
    *   [2.2 Readline](#Readline)
*   [3 X11](#X11)
*   [4 外部链接](#外部链接)

## 内核

以下是系统底层的快捷键，通常被用于调试。遇到系统问题，请尽可能尝试这些快捷键，而不是按住电源开关强制关机。

这些快捷键需要首先使用如下命令激活 `echo "1" > /proc/sys/kernel/sysrq` 如果你希望在系统启动时就开启，请[编辑](/index.php/Sysctl#Configuration "Sysctl") `/etc/sysctl.d/99-sysctl.conf` 并添加配置 `kernel.sysrq = 1`. 如果你希望在挂载分区和启动引导前就开启的话, 请在内核启动参数上添加 `sysrq_always_enabled=1`.

记住这个激活命令的通用口诀是 "**R**eboot **E**ven **I**f **S**ystem **U**tterly **B**roken" (或者"REISUB")。

| 键盘快捷键 | 描述 |
| `Alt`+`SysRq`+`R`+ **Unraw** | 从X收回对键盘的控制 |
| `Alt`+`SysRq`+`E`+ **Terminate** | 向所有进程发送SIGTERM信号，让它们正常终止 |
| `Alt`+`SysRq`+`I`+ **Kill** | 向所有进程发送SIGKILL信号，强制立即终止 |
| `Alt`+`SysRq`+`S`+ **Sync** | 将待写数据写入磁盘 |
| `Alt`+`SysRq`+`U`+ **Unmount** | 卸载所有硬盘然后重新按只读模式挂载 |
| `Alt`+`SysRq`+`B`+ **Reboot** | 重启 |

详情参见 [Magic SysRq key - Wikipedia](https://en.wikipedia.org/wiki/Magic_SysRq_key "wikipedia:Magic SysRq key")。

## 终端

### 虚拟控制台

| 键盘快捷键 | 描述 |
| `Ctrl`+`Alt`+`Del` | 重启计算机（指定在 /etc/inittab） |
| `Alt`+`F1`, `F2`, `F3`, ... | 切换到第 n 个控制台 |
| `Alt`+`←` | 切换到上一个控制台 |
| `Alt`+`→` | 切换到下一个控制台 |
| `Scroll Lock` | 当 Scroll Lock 被激活后，输入/输出将被锁住 |
| `⇑ Shift`+`PgUp`/`PgDown` | 控制台翻页 |
| `Ctrl`+`L` | 清屏 |
| `Ctrl`+`C` | 结束当前进程 |
| `Ctrl`+`D` | 插入一个 EOF（文件结束符） |
| `Ctrl`+`Z` | 暂停当前进程 |

### Readline

GNU readline 是一个用于行编辑的通用库，它被bash、ftp等大量程序使用 (更多示例，请参考 [Arch Package details](https://archlinux.org/packages/core/i686/readline/) 的 "Required By" 章节)。 readline同样可以被定制 (具体细节请查看manpage)。

| 键盘快捷键 | 描述 |
| `Ctrl`+`L` | 清屏 |
| 光标移动 |
| `Ctrl`+`B` | 光标向左移动1个字符宽度 |
| `Ctrl`+`F` | 光标向右移动1个字符宽度 |
| `Alt`+`B` | 光标向左移动1个单词 |
| `Alt`+`F` | 光标向右移动1个单词 |
| `Ctrl`+`A` | 光标移动到行首 |
| `Ctrl`+`E` | 光标移动到行尾 |
| 复制和粘帖 |
| `Ctrl`+`U` | 剪切从行首到光标位置的内容 |
| `Ctrl`+`K` | 剪切从光标到行尾的所有内容 |
| `Alt`+`D` | 剪切紧跟当前光标的1个单词 |
| `Ctrl`+`W` | 剪切当前光标前的1个单词 |
| `Ctrl`+`Y` | 粘帖最近1次剪切的文本 |
| `Alt`+`Y` | 粘帖倒数第2次剪切的文本 |
| `Alt`+`Ctrl`+`Y` | 粘帖前1次命令中的第1个参数 |
| `Alt`+`.`or`_` | 粘帖前1次命令中的最后1个参数 |
| 历史 |
| `Ctrl`+`P` | 移动到前1行 |
| `Altl`+`N` | 移动到后1行 |
| `Ctrl`+`S` | 查找 |
| `Ctrl`+`R` | 反向查找 |
| `Ctrl`+`J` | 结束查找 |
| `Ctrl`+`G` | 中止查找 (恢复原始行) |
| `Alt`+`R` | 取消对当前行的所有修改 |
| 补全 |
| `Tab` | 自动补全一个名称 |
| `Altl`+`?` | 列出所有可能的补全 |
| `Alt`+`*` | 插入所有可能的补全 |

## X11

| 键盘快捷键 | 描述 |
| `Ctrl`+`Alt`+`F1`, `F2`, `F3`, ... | 切换到第 n 个虚拟控制台 |
| `Ctrl`+`Alt`+`+`/`-` | 切换到更高/更低的可用屏幕分辨率 |
| `Ctrl`+`Alt`+`Backspace` | 结束 X-server |
| `Ctrl`+`⇑ Shift`+`Num Lock` | 开启键盘鼠标；使用小键盘控制鼠标，`5`键单击，用`/`、`*`、及`-`将单击模式切换为左键、中键和右键 |

xkeyboard-config 从 2.0.1 开始禁用了键盘鼠标。要启用它，将 `/usr/share/X11/xkb/symbols/pc` 中的下行:

 `key <NMLK> { [ Num_Lock ] }; ` 

修改为:

 `key <NMLK> { [ Num_Lock, Pointer_EnableKeys ] }; ` 

## 外部链接

*   [Linux Newbie Administrator Guide - Shortcuts and Commands](http://linux-newbie.dotsrc.org/html/lnag.html#6.Linux%20Shortcuts%20and%20Commands%7Coutline)
*   [The Linux keyboard and console HOWTO](http://tldp.org/HOWTO/Keyboard-and-Console-HOWTO.html)