相关文章

*   [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg")
*   [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys")

**翻译状态：** 本文是英文页面 [Keyboard_Configuration_in_Console](/index.php/Keyboard_Configuration_in_Console "Keyboard Configuration in Console") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-02-07，点击[这里](https://wiki.archlinux.org/index.php?title=Keyboard_Configuration_in_Console&diff=0&oldid=359908)可以查看翻译后英文页面的改动。

**Note:** 此文仅介绍简单设置，修改布局、按键映射等高级功能请查看 [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys")。

[虚拟控制台](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console")键盘映射(keymaps), 控制台字体和控制台映射由软件包 [kbd](https://www.archlinux.org/packages/?name=kbd) 提供([systemd](/index.php/Systemd "Systemd")依赖此软件包)。这个包还提供了很多管理虚拟控制台的底层工具。此外，*systemd* 还提供了 *localectl* 工具，可以同时控制系统 [locale](/index.php/Locale "Locale") 和控制台、Xorg 的键盘布局设置.

## Contents

*   [1 查看键盘设置](#查看键盘设置)
*   [2 设置键盘映射](#设置键盘映射)
    *   [2.1 键盘映射码](#键盘映射码)
    *   [2.2 永久设置](#永久设置)
    *   [2.3 临时设置](#临时设置)
*   [3 修改按键延时和频率](#修改按键延时和频率)
    *   [3.1 Systemd service](#Systemd_service)

## 查看键盘设置

用下面命令查看键盘和本地化设置:

 `$ localectl status` 
```
   System Locale: LANG=en_GB.utf8
                  LC_COLLATE=C
       VC Keymap: cz-qwertz
      X11 Layout: cz

```

## 设置键盘映射

### 键盘映射码

通常一个键盘映射文件对应一个键盘布局，可以通过`include`语句共享通用的部分。一个映射文件可以包含多个布局，通过快捷键切换。键盘映射文件位于目录`/usr/share/kbd/keymaps/`。

映射名并没有统一的规则，但是通常基于下面标准：

*   [语言代码](https://en.wikipedia.org/wiki/ISO_639-1 "wikipedia:ISO 639-1"): 语言代码和国家代码一样的时候(例如：德国用`de`，法国用 `fr`).
*   [国家代码](https://en.wikipedia.org/wiki/Country_code "wikipedia:Country code"): 有些国家语言相同，但是在不同的国家使用的不一样。例如英国用`uk`，美国用 `us`，[次链接可以查看国家代码](https://en.wikipedia.org/wiki/ISO_3166-1#Officially_assigned_code_elements "wikipedia:ISO 3166-1").
*   [键盘布局](https://en.wikipedia.org/wiki/Keyboard_layout "wikipedia:Keyboard layout"): 布局和国家或语言不相关，例如 [Dvorak 键盘布局](https://en.wikipedia.org/wiki/Dvorak_Simplified_Keyboard "wikipedia:Dvorak Simplified Keyboard") 使用 `dvorak`。

下面命令可以查看所有键盘映射

```
$ localectl list-keymaps

```

查找键盘布局：

```
$ localectl list-keymaps | grep -i *search_term*

```

### 永久设置

可以把键盘设置到 `/etc/vconsole.conf`，[systemd](/index.php/Systemd "Systemd") 在启动时会读取此文件. `KEYMAP` 变量指定键盘映射，如果未设置或为空，则使用默认的 `us` 键盘映射，选项信息可以参考 [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5)。

 `/etc/vconsole.conf` 
```
KEYMAP=uk
...

```

以用 *localectl* 修改键盘映射，例如下面命令同时修改了`/etc/vconsole.conf` 和当前会话中的 `KEYMAP`:

```
$ localectl set-keymap --no-convert *keymap*

```

`--no-convert` 选项会阻止 `localectl` 自动将 [Xorg keymap](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg") 修改为最接近的匹配。详情参阅 [localectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/localectl.1)。

### 临时设置

也可以使用 *loadkeys* 工具临时修改键盘布局，参阅 [loadkeys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1)

```
# loadkeys *keymap*

```

## 修改按键延时和频率

**按键延时**是只长按一个按键多少时间才会开始重复这个按键。开始重复过程后，字符会以一定频率出现(Hz)，也就是**重复频率**. 终端中，这些值可以通过 *kbdrate* 设置。X 中的设置参考[这里](/index.php/Keyboard_configuration_in_Xorg#Adjusting_typematic_delay_and_rate "Keyboard configuration in Xorg").

```
# kbdrate [-d *delay*] [-r *rate*]

```

延迟 200ms 重复频率是 30Hz：:

```
# kbdrate -d 200 -r 30

```

不加任何参数会还原到默认值 250ms 和 11Hz:

```
# kbdrate

```

### Systemd service

可以用下面 systemd service 修改按键频率：

 `/etc/systemd/system/kbdrate.service` 
```

[Unit]
Description=Keyboard repeat rate in tty.

[Service]
Type=simple
RemainAfterExit=yes
StandardInput=tty
StandardOutput=tty
ExecStart=/usr/bin/kbdrate -s -d 450 -r 60

[Install]
WantedBy=multi-user.target

```

```
$ systemctl enable kbdrate.service
$ systemctl start kbdrate.service

```