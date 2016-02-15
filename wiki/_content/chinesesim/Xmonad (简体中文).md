[xmonad](http://xmonad.org/) 是一个平铺式窗口管理器。窗口会自动填满屏幕，因此能最大化利用屏幕空间。窗口管理器的所有功能都可通过键盘控制，鼠标不是必须的。

xmonad是用[Haskell](http://haskell.org/)语言写的，对xmonad的配置和扩展也需要使用Haskell语言。名字中的[monad](http://en.wikibooks.org/wiki/Haskell/Understanding_monads)是Haskell语言的一个重要特性。窗口布局算法、键盘快捷键和其它扩展都可以通过配置文件(~/.xmonad/xmonad.hs)重新定义。

窗口布局会自适应，不同的工作空间可以使用不同的窗口布局。xmonad完全支持[Xinerama](/index.php?title=Xinerama&action=edit&redlink=1 "Xinerama (page does not exist)")，允许窗口平铺至多个物理显示器。

更多信息，请访问xmonad官网: [http://xmonad.org/](http://xmonad.org/)

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 Configuration](#Configuration)
    *   [2.1 启动xmonad](#.E5.90.AF.E5.8A.A8xmonad)
    *   [2.2 配置xmonad](#.E9.85.8D.E7.BD.AExmonad)
    *   [2.3 退出xmonad](#.E9.80.80.E5.87.BAxmonad)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Complementary applications](#Complementary_applications)
    *   [3.2 Making room for Conky or tray apps](#Making_room_for_Conky_or_tray_apps)
    *   [3.3 Using xmobar with xmonad](#Using_xmobar_with_xmonad)
        *   [3.3.1 Option 1: Quick, less flexible](#Option_1:_Quick.2C_less_flexible)
        *   [3.3.2 Option 2: More Configurable](#Option_2:_More_Configurable)
        *   [3.3.3 Verify XMobar Config](#Verify_XMobar_Config)
    *   [3.4 Controlling xmonad with external scripts](#Controlling_xmonad_with_external_scripts)
    *   [3.5 Launching another window manager within xmonad](#Launching_another_window_manager_within_xmonad)
    *   [3.6 Example configurations](#Example_configurations)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 GNOME 3 and xmonad](#GNOME_3_and_xmonad)
        *   [4.1.1 Compositing in Gnome and Xmonad](#Compositing_in_Gnome_and_Xmonad)
    *   [4.2 GDM 2.x/KDM cannot find xmonad](#GDM_2.x.2FKDM_cannot_find_xmonad)
    *   [4.3 Missing xmonad-i386-linux or xmonad-x86_64-linux](#Missing_xmonad-i386-linux_or_xmonad-x86_64-linux)
    *   [4.4 Problems with Java applications](#Problems_with_Java_applications)
    *   [4.5 Empty space at the bottom of gvim or terminals](#Empty_space_at_the_bottom_of_gvim_or_terminals)
    *   [4.6 Chromium/Chrome will not go fullscreen](#Chromium.2FChrome_will_not_go_fullscreen)
    *   [4.7 Multitouch / touchegg](#Multitouch_.2F_touchegg)
*   [5 Other Resources](#Other_Resources)

## 安装

[官方软件库](/index.php/Official_repositories "Official repositories")里的[xmonad](https://www.archlinux.org/packages/?name=xmonad)和[xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib)是xmonad正式版。[AUR](/index.php/Arch_User_Repository "Arch User Repository")里的[xmonad-darcs](https://aur.archlinux.org/packages/xmonad-darcs/)和[xmonad-contrib-darcs](https://aur.archlinux.org/packages/xmonad-contrib-darcs/)是开发版。

安装顺序：

*   [xmonad](https://www.archlinux.org/packages/?name=xmonad) 或 [xmonad-darcs](https://aur.archlinux.org/packages/xmonad-darcs/) -- 窗口管理器核心功能
*   [xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib) 或 [xmonad-contrib-darcs](https://aur.archlinux.org/packages/xmonad-contrib-darcs/) -- 提供自定义布局、配置等功能的一些扩展 (可选安装)

## Configuration

### 启动xmonad

只要添加`xmonad`命令到启动脚本(如果使用startx则添加到`~/.xinitrc`文件，如果使用xdm则添加到`~/.xsession`文件)，就能自动运行xmonad。在添加到启动脚本时，`exec`是可选的，既可以写`exec xmonad`，也可以写`xmonad`。GDM和KDM用户可以创建一个新的会话文件，然后从相应的会话菜单选择进入xmonad。

**注意:** 如果xmonad无法启动，请检查home目录下是否有`.xmonad`文件夹，没有的话，创建一个:
 `mkdir ~/.xmonad` 

**注意:** xmonad默认不设定鼠标光标，因此光标一直呈“X”形可能会让新用户误以为xmonad还没启动完毕或启动出错。将下面的命令添加到启动脚本，就可以将光标设置成常见的左键头形状:
 `xsetroot -cursor_name left_ptr` 

另外，xmonad默认使用US键盘布局，如果想修改为其它键盘布局，比如说德语键盘布局，将以下命令添加到启动脚本，也可以参阅[这里](/index.php/Xorg#Keyboard_settings "Xorg")。

```
 setxkbmap -layout de

```

`~/.xinitrc`文件示例:

```
 # 设置鼠标光标
 xsetroot -cursor_name left_ptr
 # 设置为德语键盘布局
 setxkbmap -layout de
 # 启动xmonad
 exec xmonad

```

### 配置xmonad

xmonad的默认配置文件是`~/.xmonad/xmonad.hs`，如果`~/.xmonad/`路径下没有`xmonad.hs`文件，可以从`/usr/share/xmonad-VERSION/man/xmonad.hs`拷贝一份。可以通过编辑`~/.xmonad/xmonad.hs`文件对xmonad进行自定义和扩展。

要使配置生效需要重新编译xmonad，重编译不需要退出xmonad。可以在终端中输入`xmonad --recompile`，也可以使用快捷键`Mod+q`进行重编译。Mod默认是Alt键。

因为xmonad配置文件是用Haskell语言写的，非程序员可能会在配置时遇到困难。更多帮助和一些配置文件示例可以从以下链接找到：

*   [xmonad wiki](http://haskell.org/haskellwiki/Xmonad)
*   [xmonad config archive](http://haskell.org/haskellwiki/Xmonad/Config_archive)
*   [xmonad FAQ](http://haskell.org/haskellwiki/Xmonad/Frequently_asked_questions)
*   Arch Linux [forum thread](https://bbs.archlinux.org/viewtopic.php?id=40636)

自定义配置最好都写在`~/.xmonad/xmonad.hs`文件里，并且应该把未设置的参数交给内置的defaultConfig处理。

如下面这个示例文件：

```
 import XMonad

 main = do
   xmonad $ defaultConfig
     { terminal    = "urxvt"
     , modMask     = mod4Mask
     , borderWidth = 3
     }

```

它仅仅将默认终端设置为"urxvt“，Mod键设置为“Windows键”，边框宽度设置为3，其它参数的设置都采用默认值(从defaultConfig函数继承)。

当配置项变多以后，在主函数里将函数名配给参数的做法会更方便。不同的函数置于`~/.xmonad/xmonad.hs`文件的不同部分。这样的话，大范围的自定义配置会更易于维护。

按照这个思路，上面那个简单的`xmonad.hs`示例文件，可以写成下面这样：

```
 import XMonad

 main = do
   xmonad $ defaultConfig
     { terminal    = myTerminal
     , modMask     = myModMask
     , borderWidth = myBorderWidth
     }

 -- 是的，这些也都是函数，只不过是简单函数
 -- 它们不接受输入变量，返回静态值
 myTerminal    = "urxvt"
 myModMask     = mod4Mask -- Windows键或Super_L键
 myBorderWidth = 3

```

函数(如main, myTerminal, myModMask)的定义顺序或在{}中的顺序是不重要的，只要import语句是在文件起始位置就可以。

下面的例子摘自xmonad 0.9的配置文件模板，完整模板在[这里](http://haskell.org/haskellwiki/Xmonad/Config_archive/Template_xmonad.hs_(0.9))。这个例子包含了经常会在main函数里自定义的项。

```
 {
   terminal           = myTerminal,
   focusFollowsMouse  = myFocusFollowsMouse,
   borderWidth        = myBorderWidth,
   modMask            = myModMask,
   -- 0.9.1之后已经弃用了numlockMask 
   -- numlockMask        = myNumlockMask,
   workspaces         = myWorkspaces,
   normalBorderColor  = myNormalBorderColor,
   focusedBorderColor = myFocusedBorderColor,

   -- 快捷键
   keys               = myKeys,
   mouseBindings      = myMouseBindings,

   -- 事件钩子、窗口布局
   layoutHook         = myLayout,
   manageHook         = myManageHook,
   handleEventHook    = myEventHook,
   logHook            = myLogHook,
   startupHook        = myStartupHook
 }

```

推荐参考`/usr/share/xmonad-VERSION/man/xmonad.hs`文件，它是官方最新的xmonad.hs示例文件，在安装xmonad时自带。

### 退出xmonad

按下组合键 `Mod+Shift+Q` 来结束当前的xmonad会话。默认设置下， `Mod` 是 `Alt` key.

## Tips and tricks

### Complementary applications

There are number of complementary utilities that work well with xmonad. The most common of these include:

*   [dmenu](/index.php/Dmenu "Dmenu")
*   [xmobar](/index.php/Xmobar "Xmobar")
*   [dzen](/index.php/Dzen "Dzen")
*   [Conky](/index.php/Conky "Conky") and [conky-cli](https://aur.archlinux.org/packages/conky-cli/)
*   [gmrun](/index.php/Gmrun "Gmrun")
*   [Unclutter](/index.php/Unclutter "Unclutter") - a small utility to hide the mouse pointer
*   [XMonad-log-applet](http://uhsure.com/xmonad-log-applet.html) - a GNOME applet for the gnome-panel (the package is in the [Official repositories](/index.php/Official_repositories "Official repositories"))

### Making room for Conky or tray apps

Wrap your layouts with avoidStruts from XMonad.Hooks.ManageDocks for automatic dock/panel/trayer spacing:

```
 import XMonad
 import XMonad.Hooks.ManageDocks

 main=do
   xmonad $ defaultConfig
     { ...
     , layoutHook=avoidStruts $ layoutHook defaultConfig
     , manageHook=manageHook defaultConfig <+> manageDocks
     , ...
     }

```

If you ever want to toggle the gaps, this action can be added to your key bindings:

```
,((modMask x, xK_b     ), sendMessage ToggleStruts)

```

### Using xmobar with xmonad

**[xmobar](/index.php/Xmobar "Xmobar")** is a light and minimalistic text-based bar, designed to work with xmonad. To use xmobar with xmonad, you will need two packages in addition to the [xmonad](https://www.archlinux.org/packages/?name=xmonad) package. These packages are [xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib) and [xmobar](https://www.archlinux.org/packages/?name=xmobar) from the [official repositories](/index.php/Official_repositories "Official repositories"), or you can use [xmobar-git](https://aur.archlinux.org/packages/xmobar-git/) from the [AUR](/index.php/Arch_User_Repository "Arch User Repository") instead of the official [xmobar](https://www.archlinux.org/packages/?name=xmobar) package.

Here we will start xmobar from within xmonad, which reloads xmobar whenever you reload xmonad.

Open `~/.xmonad/xmonad.hs` in your favorite editor, and choose one of the two following options:

#### Option 1: Quick, less flexible

**Note:** There is also [dzen2](https://www.archlinux.org/packages/?name=dzen2) which you can substitute for [xmobar](https://www.archlinux.org/packages/?name=xmobar) in either case.

Common imports:

```
import XMonad
import XMonad.Hooks.DynamicLog

```

The xmobar action starts xmobar and returns a modified configuration that includes all of the options described in the [xmonad:Option2: More configurable](/index.php/Xmonad#Option_2:_More_configurable "Xmonad") choice.

```
main = xmonad =<< xmobar defaultConfig { modMask = mod4Mask {- or any other configurations here ... -}}

```

#### Option 2: More Configurable

As of xmonad(-contrib) 0.9, there is a new [statusBar](http://xmonad.org/xmonad-docs/xmonad-contrib/XMonad-Hooks-DynamicLog.html#v%3AstatusBar) function in [XMonad.Hooks.DynamicLog](http://xmonad.org/xmonad-docs/xmonad-contrib/XMonad-Hooks-DynamicLog.html). It allows you to use your own configuration for:

*   The command used to execute the bar
*   The PP that determines what is being written to the bar
*   The key binding to toggle the gap for the bar

The following is an example of how to use it:

 `~/.xmonad/xmonad.hs` 

```
-- Imports.
import XMonad
import XMonad.Hooks.DynamicLog

-- The main function.
main = xmonad =<< statusBar myBar myPP toggleStrutsKey myConfig

-- Command to launch the bar.
myBar = "xmobar"

-- Custom PP, configure it as you like. It determines what is being written to the bar.
myPP = xmobarPP { ppCurrent = xmobarColor "#429942" "" . wrap "<" ">" }

-- Key binding to toggle the gap for the bar.
toggleStrutsKey XConfig {XMonad.modMask = modMask} = (modMask, xK_b)

-- Main configuration, override the defaults to your liking.
myConfig = defaultConfig { modMask = mod4Mask }

```

#### Verify XMobar Config

The template and default xmobarrc contains this.

At last, open up `~/.xmobarrc` and make sure you have `StdinReader` in the template and run the plugin. E.g.

 `~/.xmobarrc` 

```
Config { ...
       , commands = [ Run StdinReader .... ]
         ...
       , template = " %StdinReader% ... "
       }

```

Now, all you should have to do is either to start, or restart, xmonad.

### Controlling xmonad with external scripts

There are at least two ways to do this.

Firstly, you can use the following xmonad extension, [XMonad.Hooks.ServerMode](http://xmonad.org/xmonad-docs/xmonad-contrib/XMonad-Hooks-ServerMode.html).

Secondly, you can simulate keypress events using [xdotool](https://www.archlinux.org/packages/?name=xdotool) or similar programs. See this [Ubuntu forums thread](http://ubuntuforums.org/archive/index.php/t-658040.html). The following command would simulate the keypress `Super+n`:

```
xdotool key Super+n

```

### Launching another window manager within xmonad

If you are using [xmonad-darcs](https://aur.archlinux.org/packages/xmonad-darcs/), as of January of 2011, you can restart to another window manager from within xmonad. You just need to write a small script, and add stuff to your `~/.xmonad/xmonad.hs`. Here is the script.

 `~/bin/obtoxmd` 

```
#!/bin/sh
openbox
xmonad

```

And here are the modifications you need to add to your `~/.xmonad/xmonad.hs`:

 `~/.xmonad/xmonad.hs` 

```
import XMonad
--You need to add this import
import XMonad.Util.Replace

main do
    -- And this "replace"
    replace
    xmonad $ defaultConfig
    {
    --Add the usual here
    }

```

You also need to add the following key binding:

 `~/xmonad/xmonad.hs` 

```
--Add a keybinding as follows:
((modm .|. shiftMask, xK_o     ), restart "/home/abijr/bin/obtoxmd" True)

```

Just remember to add a comma before or after and change the path to your actual script path. Now just `Mod+q` (restart xmonad to refresh the config), and then hit `Mod+Shift+o` and you should have Openbox running with the same windows open as in xmonad. To return to xmonad you should just exit Openbox. Here is a link to adamvo's `~/.xmonad/xmonad.hs` which uses this setup [Adamvo's xmonad.hs](http://www.haskell.org/haskellwiki/Xmonad/Config_archive/adamvo%27s_xmonad.hs)

### Example configurations

Below are some example configurations from fellow xmonad users. Feel free to add links to your own.

*   brisbin33 :: complex and simpler branches, importable dzen and scratchpad modules, very readable :: [config](https://github.com/pbrisbin/xmonad-config) [screenshot](http://pbrisbin.com/static/screenshots/current_desktop.png)
*   jelly :: Configuration with prompt, different layouts, twinview with xmobar :: [xmonad.hs](http://github.com/jelly/dotfiles/tree/master/.xmonad/xmonad.hs)
*   MrElendig :: Simple configuration, with xmobar :: [xmonad.hs](http://github.com/MrElendig/dotfiles-alice/blob/master/.xmonad/xmonad.hs), [.xmobarrc](http://github.com/MrElendig/dotfiles-alice/blob/master/.xmobarrc), [screenshot](http://arch.har-ikkje.net/gfx/ss/2010-09-05-163305_2960x1050_scrot.png).
*   thayer :: A minimal mouse-friendly config ideal for netbooks :: [configs](http://haskell.org/haskellwiki/Xmonad/Config_archive/Thayer_Williams%27_xmonad.hs) [screenshot](http://haskell.org/haskellwiki/Image:Thayer-xmonad-20110511.png)
*   vicfryzel :: Beautiful and usable xmonad configuration, along with xmobar configuration, xinitrc, dmenu, and other scripts that make xmonad more usable. :: [git repository](https://github.com/vicfryzel/xmonad-config), [screenshot](https://github.com/vicfryzel/xmonad-config/raw/master/screenshot.png).
*   vogt :: Check out adamvo's config and many others in the official [Xmonad/Config archive](http://haskell.org/haskellwiki/Xmonad/Config_archive)

## Troubleshooting

### GNOME 3 and xmonad

With the release of [GNOME](/index.php/GNOME "GNOME") 3, some additional steps are necessary to make GNOME play nicely with xmonad.

First, add an xmonad session file for use by gnome-session (`/usr/share/gnome-session/sessions/xmonad.session`):

```
[GNOME Session]
Name=Xmonad session
RequiredComponents=gnome-panel;gnome-settings-daemon;
RequiredProviders=windowmanager;notifications;
DefaultProvider-windowmanager=xmonad
DefaultProvider-notifications=notification-daemon
```

Now create a desktop file for GDM (`/usr/share/xsessions/xmonad-gnome-session.desktop`):

```
[Desktop Entry]
Name=Xmonad GNOME
Comment=Tiling window manager
TryExec=/usr/bin/gnome-session
Exec=gnome-session --session=xmonad
Type=XSession
```

Add / edit this file (`/usr/share/applications/xmonad.desktop`):

```
[Desktop Entry]
Type=Application
Encoding=UTF-8
Name=Xmonad
Exec=xmonad
NoDisplay=true
X-GNOME-WMName=Xmonad
X-GNOME-Autostart-Phase=WindowManager
X-GNOME-Provides=windowmanager
X-GNOME-Autostart-Notify=false
```

Then install [xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib) and create or edit `~/.xmonad/xmonad.hs` to have the following

```
import XMonad
import XMonad.Config.Gnome

main = xmonad gnomeConfig
```

Xmonad should now appear in the list of GDM sessions and also play nicely with gnome-session itself.

#### Compositing in Gnome and Xmonad

Some applications look better (e.g. GNOME Do) when composition is enabled. This is, however not, the case in the default Xmonad window manager. To enable it add an additional .desktop file `/usr/share/xsessions/xmonad-gnome-session-composite.desktop`:

```
[Desktop Entry]
Name=Xmonad GNOME (Composite)
Comment=Tiling window manager
TryExec=/usr/bin/gnome-session
Exec=/usr/sbin/gnome-xmonad-composite
Type=XSession
```

And create `/usr/sbin/gnome-xmonad-composite` and `chmod +x /usr/sbin/gnome-xmonad-composite`:

```
xcompmgr &
gnome-session --session=xmonad
```

Now choose "Xmonad GNOME (Composite)" in the list of sessions during log in. Checkout `man xcompmgr` for additional "eye candy".

### GDM 2.x/KDM cannot find xmonad

You can force GDM to launch xmonad by creating the file `xmonad.desktop` in the `/usr/share/xsessions` directory and add the contents:

```
[Desktop Entry]
Encoding=UTF-8
Name=xmonad
Comment=This session starts xmonad
Exec=/usr/bin/xmonad
Type=Application

```

Now xmonad will show in your GDM session menu. Thanks to [Santanu Chatterjee](http://santanuchatterjee.blogspot.com/2009/03/making-xmonad-to-show-up-in-gdm-session.html) for the hint.

For KDM, you will need to create the file here as `/usr/share/apps/kdm/sessions/xmonad.desktop`

Official documentation can be found here: [Haskell Documentation Page](http://www.haskell.org/haskellwiki/Xmonad/Frequently_asked_questions#How_can_I_use_xmonad_with_a_display_manager.3F_.28xdm.2C_kdm.2C_gdm.29)

### Missing xmonad-i386-linux or xmonad-x86_64-linux

Xmonad should automatically create the `xmonad-i386-linux` file (in `~/.xmonad/`). If this it not the case you can grab a cool looking config file from the [xmonad wiki](http://haskell.org/haskellwiki/Xmonad/Config_archive) or create your [own](http://haskell.org/haskellwiki/Xmonad/Config_archive/John_Goerzen's_Configuration). Put the `.hs` and all others files in `~/.xmonad/` and run this command from the folder:

```
xmonad --recompile

```

Now you should see the file.

**Note:** A reason you may get an error message saying that xmonad-x86_64-linux is missing is that [xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib) is not installed.

### Problems with Java applications

The standard Java GUI toolkit has a hard-coded list of "non-reparenting" window managers. Since xmonad is not in that list, there can be some problems with running some Java applications. One of the most common problems is "gray blobs", when the Java application renders as a plain gray box instead of rendering the GUI.

There are several things that may help:

*   If you are using [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk), uncomment the line `export _JAVA_AWT_WM_NONREPARENTING=1` in `/etc/profile.d/jre.sh`. Then, source the file `/etc/profile.d/jre.sh` or log out and log back in.
*   If you are using Oracle's JRE/JDK, the best solution is usually to use [SetWMName.](http://xmonad.org/xmonad-docs/xmonad-contrib/XMonad-Hooks-SetWMName.html) However, its effect may be nullified if one also uses XMonad.Hooks.EwmhDesktops, in which case

```
 >> setWMName "LG3D"

```

added to the LogHook may help.

For more details about the problem, refer to the [xmonad FAQ.](http://haskell.org/haskellwiki/Xmonad/Frequently_asked_questions#Problems_with_Java_applications.2C_Applet_java_console)

### Empty space at the bottom of gvim or terminals

See [Vim#Empty space at the bottom of gvim windows](/index.php/Vim#Empty_space_at_the_bottom_of_gvim_windows "Vim") for a solution which makes the area match the background color.

For [rxvt-unicode](/index.php/Rxvt-unicode "Rxvt-unicode"), you can use [rxvt-unicode-patched](https://aur.archlinux.org/packages/rxvt-unicode-patched/).

You can also configure xmonad to respect size hints, but this will leave a gap instead. See [the documentation on Xmonad.Layout.LayoutHints](http://www.eng.uwaterloo.ca/~aavogt/xmonad/docs/xmonad-contrib/XMonad-Layout-LayoutHints.html).

### Chromium/Chrome will not go fullscreen

If Chrome fails to go fullscreen when `F11` is pressed, you can use the [XMonad.Hooks.EwmhDesktops](http://xmonad.org/xmonad-docs/xmonad-contrib/XMonad-Hooks-EwmhDesktops.html) extension found in the [xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib) package. Simply add the `import` statement to your `~/.xmonad/xmonad.hs`:

```
import XMonad.Hooks.EwmhDesktops

```

and then add `handleEventHook = fullscreenEventHook` to the appropriate place; for example:

```
...
        xmonad $ defaultConfig
            { modMask            = mod4Mask
            , handleEventHook    = fullscreenEventHook
            }
...

```

After a recompile/restart of xmonad, Chromium should now respond to `F11` (fullscreen) as expected.

### Multitouch / touchegg

Touchégg polls the window manager for the _NET_CLIENT_LIST (in order to fetch a list of windows it should listen for mouse events on.) By default, xmonad does not supply this property. To enable this, use the [XMonad.Hooks.EwmhDesktops](http://xmonad.org/xmonad-docs/xmonad-contrib/XMonad-Hooks-EwmhDesktops.html) extension found in the [xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib) package.

## Other Resources

*   [xmonad](http://xmonad.org/) - The official xmonad website
*   [xmonad.hs](http://haskell.org/haskellwiki/Xmonad/Config_archive/Template_xmonad.hs_(0.9)) - Template xmonad.hs
*   [xmonad: a guided tour](http://xmonad.org/tour.html)
*   [dzen](/index.php/Dzen "Dzen") - General purpose messaging and notification program
*   [dmenu](/index.php/Dmenu "Dmenu") - Dynamic X menu for the quick launching of programs
*   [Comparison of tiling window managers](/index.php/Comparison_of_tiling_window_managers "Comparison of tiling window managers") - Arch wiki article providing an overview of mainstream tiling window managers
*   [Share your xmonad desktop!](https://bbs.archlinux.org/viewtopic.php?id=94969)
*   [xmonad hacking thread](https://bbs.archlinux.org/viewtopic.php?id=40636)