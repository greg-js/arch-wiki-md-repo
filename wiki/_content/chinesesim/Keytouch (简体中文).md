**翻译状态：** 本文是英文页面 [Keytouch](/index.php/Keytouch "Keytouch") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-06-06，点击[这里](https://wiki.archlinux.org/index.php?title=Keytouch&diff=0&oldid=261523)可以查看翻译后英文页面的改动。

KeyTouch是一个可以自由配置键盘额外功能按键的软件,你可以通过它来轻松自定义键盘的额外功能按键.

这篇文章将介绍Keytouch如何工作于Arch Linux下. 更多信息参见[Keytouch的官方文档](http://keytouch.sourceforge.net/doc.html).

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 键盘模型文件](#.E9.94.AE.E7.9B.98.E6.A8.A1.E5.9E.8B.E6.96.87.E4.BB.B6)
    *   [2.1 创建一个键盘模型文件](#.E5.88.9B.E5.BB.BA.E4.B8.80.E4.B8.AA.E9.94.AE.E7.9B.98.E6.A8.A1.E5.9E.8B.E6.96.87.E4.BB.B6)
    *   [2.2 公布这个键盘模型文件](#.E5.85.AC.E5.B8.83.E8.BF.99.E4.B8.AA.E9.94.AE.E7.9B.98.E6.A8.A1.E5.9E.8B.E6.96.87.E4.BB.B6)
*   [3 配置Keytouch](#.E9.85.8D.E7.BD.AEKeytouch)
*   [4 启动keytouch守护进程](#.E5.90.AF.E5.8A.A8keytouch.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B)
*   [5 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)

## 安装

安装[keytouch](https://aur.archlinux.org/packages/keytouch/)软件包 ,它位于[Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

## 键盘模型文件

你需要一个适用于你的键盘的键盘模型文件. 软件包自身包含了一些键盘模型文件. 你也可以在[官方的键盘模型文件列表](http://keytouch.sourceforge.net/dl-keyboards.html)中寻找更多键盘模型文件.

如果没有找到的话,你需要自己创建一个键盘模型文件.

### 创建一个键盘模型文件

安装 [keytouch-editor](https://aur.archlinux.org/packages/keytouch-editor/) ,位于 [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). 确保evdev已经装载. (如果你使用的是官方库的内核则不必顾虑于此)

```
# lsmod | grep evdev

```

如果evdev没有装载，装载evdev

```
# modprobe evdev

```

创建一个键盘模型文件前，我们还需要知道哪个输入设备是键盘:

```
# ls /dev/input/

```

每一个 event device (比如键盘鼠标) 都与这些文件中的一个相对应 要找出键盘对应哪一个文件, 运行:

```
# keytouch-editor /dev/input/eventX mykeyboardconfig

```

如果之前的命令由于kdesu依赖关系缺失而失败(原文:If the previous command fails due to a missing kdesu dependency), 试着运行:

```
# keytouch-editor-bin /dev/input/eventX mykeyboardconfig

```

X换成一个数字. KeyTouch editor将显示一些设备相关信息, 其中包含设备名字 (”Input device name”)，你可以据此判断是否选择了正确的设备. KeyTouch editor将请求你输入一个额外功能按键 . 如果输入额外功能按键后程序继续运行的话，则表示你选择了正确的设备. 如果不是，按下 Ctrl+C 终止程序，重选择另一个 event device. 注意，如果你的键盘通过USB口连接到电脑，这儿将会有两个event devices: /dev/input/eventA (A是一个数字) ，普通按键， 和 /dev/input/eventB (B = A+1) ，额外功能按键.

*   找到正确设备后继续以下步骤. keytouch-editor将询问你的名字和你键盘的型号与制造商.

*   现在该告诉keytouch-editor额外功能按键. 你会收到这样的信息:

```
Press an extra function key or press enter to finish...(按下一个额外功能按键或者按下回车键结束)

```

如果你的键盘通过USB口连接到电脑,或者你启动keyTouch editor时使用了”–acpi”选项,则你将收到如下信息(而不是上一条信息):

```
Press return to a new key or enter F followed by return to finish...(按回车键来定义新的按键或者在回车键后按下F键结束)

```

*   你应该先按下额外功能按键.注意,不要按其他的按键.按键之后你将被询问按键名字,按键代码和默认操作.
*   按键名字

为按键选择一个合适的名字. 如果按键上有文字标签的话,用此标签作名字即可.

*   按键代码

使用如下的按键代码. 其实选择哪一个按键代码都没关系,但推荐选择和按键的实际意义相同或相似的按键代码.(在同一个键盘模型文件里)每个按键代码只能使用一次

```
AGAIN               EJECTCLOSECD        MAIL              REFRESH
ALTERASE            EMAIL               MEDIA             REWIND
BACK                EXIT                MENU              RIGHTMETA
BASSBOOST           FASTFORWARD         MOVE              SCROLLDOWN
BOOKMARKS           FILE                MSDOS             SCROLLUP
BRIGHTNESSDOWN      FINANCE             MUTE              SEARCH
BRIGHTNESSUP        FIND                NEXTSONG          SENDFILE
CALC                FORWARD             OPEN              SETUP
CAMERA              FRONT               PASTE             SHOP
CANCEL              HANGUEL             PAUSE             SLEEP
CHAT                HANJA               PAUSECD           SOUND
CLOSE               HELP                PHONE             SPORT
CLOSECD             HOMEPAGE            PLAY              STOP
COFFEE              HP                  PLAYCD            STOPCD
COMPOSE             ISO                 PLAYPAUSE         SUSPEND
COMPUTER            KBDILLUMDOWN        POWER             SWITCHVIDEOMODE
CONFIG              KBDILLUMTOGGLE      PREVIOUSSONG      UNDO
CONNECT             KBDILLUMUP          PRINT             VOLUMEDOWN
COPY                KPCOMMA             PROG1             VOLUMEUP
CUT                 KPEQUAL             PROG2             WAKEUP
CYCLEWINDOWS        KPLEFTPAREN         PROG3             WWW
DELETEFILE          KPPLUSMINUS         PROG4             XFER
DIRECTION           KPRIGHTPAREN        PROPS             YEN
EDIT                LEFTMETA            QUESTION
EJECTCD             MACRO               RECORD
```

你可以在[官方按键代码列表](http://keytouch.sourceforge.net/keytouch_editor/node7.html)中找到正确的按键代码.

*   默认操作

注意,"默认操作"不是你想为这个按键定义的操作, 而是这个键本来的操作 (It is important to realize that the default action for a key, is not the action you want to use for this key, but one that corresponds to the function of the key.) 默认操作可能是一个程序或者一个插件. 如果是程序, 填入程序名. 如果是插件,填入”plugin” (没有引号),之后填入插件名称. 在这里查看有效的插件名:打开keyTouch->”Preferences”(选项),选择plugin,点击”Information...” 按钮,在这里可以得到选定插件的函数列表.在keytouch-editor中选定了插件名后,填入函数名.注意这里区分大小写.

*   这些信息输入完成后,程序将引导你定义下一个额外功能按键.如果这时已经完成了所有额外功能按键的定义,按回车键,输入生成的文件名,退出程序.

### 公布这个键盘模型文件

完成键盘模型文件的制作和测试后,你可以把它发送给Keytouch的作者,以便作者把它添加到下一个发行版本中.以后如果有人键盘和你的一样的话就不用自己写键盘模型文件啦.

```
marvinr users.sourceforge.net

```

(缺个@符号 ;))

## 配置Keytouch

*   运行Keytouch

```
$ keytouch

```

*   接下来...

1.  Keytouch将给出一个键盘列表,点击import,选择你创建的键盘模型文件
2.  找到你的键盘,选择它
3.  然后是配置界面.应该可以自己解决了

## 启动keytouch守护进程

*   在启动时运行keytouch守护进程:将`keytouch`添加到`/etc/rc.conf`中的daemons队列
*   在会话开始时加载keytouchd. 脚本`/etc/X11/Xsession`将运行所有位于`/etc/X11/Xsession.d/`的守护进程,包括keytouchd.
    *   如果你在命令行下登录,将`/etc/X11/Xsession`添加到`~/.xinitrc`
    *   如果你使用显示管理器(例如KDM), `~/.xinitrc`将不被执行. 你可以在你的桌面环境(Gnome, Kde, Xfce-svn等等)中设置在你登录时运行`/etc/X11/Xsession`.

## 故障排除

*   **我用额外功能按键改变音量时, OSD看起来很丑. 为什么?:**

也许是因为你用root去运行`/etc/X11/Xsession` .你将"`/etc/X11/Xsession`"写到像`/opt/kde/share/config/kdm/Xstartup`这样的脚本里的话就会出现这种情况. `/etc/X11/Xsession`所做的是搜寻并执行位于`/etc/X11/Xsession.d/`中的脚本. 安装keytouch将在这里创建两个脚本:

```
$ pwd
/etc/X11/Xsession.d
$ ls
91keytouch-acpid_launch  92keytouchd_launch

```

如果它们没有运行, 则keytouchd不工作. 如果root去运行它们(比如在KDM的自启动脚本里)的话就会看起来很丑,这不适合大多数人.以自己身份运行它们即可(比如在`~/.kde/Autostart`中创建一个软链接到`/etc/X11/Xsession`).

*   **我的多媒体键(播放/暂停/前一个/后一个...)根本不工作:**

和上面的同理. 如果root运行keytouchd,程序将认为是root在动作, 当然看起来像是这些键不工作.

*   **我刚刚(用keytouch-editor)创建了键盘模型文件,但是我在keytouch里选择它时, keytouch说键盘模型文件不存在. 我确定它存在! :**

它当然在——只是文件名不对罢了 创建键盘模型文件时,文件名的格式必须与此*完全*一致:

```
Model.Manufacturer

```

比如:

```
Satellite-L25-SP141.Toshiba

```

这样应该就好了.