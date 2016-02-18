## Contents

*   [1 简介](#.E7.AE.80.E4.BB.8B)
*   [2 安装](#.E5.AE.89.E8.A3.85)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 cfg_ion.lua](#cfg_ion.lua)
    *   [3.2 cfg_bindings.lua](#cfg_bindings.lua)
    *   [3.3 cfg_menus.lua](#cfg_menus.lua)
    *   [3.4 cfg_ionws.lua](#cfg_ionws.lua)
    *   [3.5 look.lua](#look.lua)

# 简介

[Ion](http://iki.fi/tuomov/ion/) 是一个有着标签(tab)框架的风格的，平铺的窗体管理器。它的配置文件以Lua语言作为内嵌的释译器。它的功能主要使用键盘来控制，同时也支持鼠标。

# 安装

Ion3现已被移出官方软件仓库，详细信息可以看[Arch Linux新闻页面](https://www.archlinux.org/news/374/)。所以现在只能通过[AUR](https://aur.archlinux.org/packages.php?ID=16754)来安装。

安装好之后，把配置文件拷贝到您的主目录下：

```
cp /etc/ion3/* ~/.ion3

```

要启用Ion3，需把下面这一行加到 **`~/.xinitrc`** 中来 :

```
exec ion3

```

现在您可以按下面配置文件所述，来配置Ion。

# 配置

***注意:** 相比原有的配置文件，我已经对这些文件基于我自己喜好进行了很大的改动。/xerxes2*

## cfg_ion.lua

Ion3的主配置文件。

```
-- Ion main configuration file
-- 
-- Ion主配置文件
--

--
-- Some basic setup
--
-- 一些基本的设置
--

-- Set default modifiers. Alt should usually be mapped to Mod1 on
-- XFree86-based systems. The flying window keys are probably Mod3
-- or Mod4; see the output of 'xmodmap'.
--
-- 设置默认功能键(modifiers)。在基于XFree86的X系统中，Alt键通常被映射为Mod1，
-- Win键常被映射为Mod3或是Mod4，详见 'xmodmap' 命令的输出。
--
MOD1="Mod4+"
MOD2="Mod1+"

ioncore.set{
    -- Maximum delay between clicks in milliseconds to be considered a
    -- double click.
    dblclick_delay=250,

    -- For keyboard resize, time (in milliseconds) to wait after latest
    -- key press before automatically leaving resize mode (and doing
    -- the resize in case of non-opaque move).
    kbresize_delay=1500,

    -- Opaque resize?
    opaque_resize=false,

    -- Movement commands warp the pointer to frames instead of just
    -- changing focus. Enabled by default.
    warp=true,

    -- Default workspace type.
    default_ws_type="WIonWS",
}

--
-- Load some modules, extensions and other configuration files
--
-- 加载一些模块，扩展功能，以及其它配置文件

-- Load some modules.
dopath("mod_query")
dopath("mod_menu")
dopath("mod_ionws")
dopath("mod_floatws")
dopath("mod_panews")
--dopath("mod_statusbar")
--dopath("mod_dock")
dopath("mod_sp")

-- Load some kludges to make apps behave better.
-- 加载一些补充程序(kludges)，以使程序有更好的外观。
dopath("cfg_kludges")

-- Make some bindings.
-- 完成热键绑定
dopath("cfg_bindings")

-- Define some menus (mod_menu required)
-- 定义一些菜单（需要用到mod_menu）
dopath("cfg_menus")

-- Load additional user configuration. 'true' as second parameter asks
-- Ion not to complain if the file is not found.
-- 加载用户自定义的配置。第二个参数 'ture' 告诉Ion被抱怨找不到该文件。
dopath("cfg_user", true)

```

要使用热键，按住功能键的同时按下热键（Modkey + hotkey）。 **`dopath`** 命令能配置Ion启动时加载的模块。如果您不想启动某个模块，把它所在的那一行注释即可。

## cfg_bindings.lua

这个文件配置键盘上的控制热键。

```
-- 
-- Ion bindings configuration file. Global bindings and bindings common 
-- to screens and all types of frames only. See modules' configuration 
-- files for other bindings.
--
--
-- 此配置文件只用于Ion全局、screan，以及各种frame的热键绑定。
-- 想了解配置的细节，参见各模块的配置文件。
--

-- WScreen context bindings
--
-- WScreen 事件的热键绑定
--
-- The bindings in this context are available all the time.
--
-- 此文中的各种热键绑定将一直生效。
--
-- The variable MOD1 should contain a string of the form 'Mod1+'
-- where Mod1 maybe replaced with the modifier you want to use for most
-- of the bindings. Similarly MOD2 may be redefined to add a 
-- modifier to some of the F-key bindings.
--
-- MOD1变量将赋于一个字符串，该字符串以 'Mod1+'的形式表征。
-- 此Mod1可以为任何一个您想使用的modifier，用于绝大多数的热键绑定。
-- 和MOD1相似地，MOD2也可以被重新定义。由此添加一个用于F-key绑定的modifier。
--
defbindings("WScreen", {
    bdoc("Switch to n:th object (workspace, full screen client window) "..
         "within current screen."),
    kpress(MOD1.."1", "WScreen.switch_nth(_, 0)"),
    kpress(MOD1.."2", "WScreen.switch_nth(_, 1)"),
    kpress(MOD1.."3", "WScreen.switch_nth(_, 2)"),
    kpress(MOD1.."4", "WScreen.switch_nth(_, 3)"),
    kpress(MOD1.."5", "WScreen.switch_nth(_, 4)"),
    kpress(MOD1.."6", "WScreen.switch_nth(_, 5)"),
    kpress(MOD1.."7", "WScreen.switch_nth(_, 6)"),
    kpress(MOD1.."8", "WScreen.switch_nth(_, 7)"),
    kpress(MOD1.."9", "WScreen.switch_nth(_, 8)"),
    kpress(MOD1.."0", "WScreen.switch_nth(_, 9)"),

--    bdoc("Switch to next/previous object within current screen."),
--    kpress(MOD2.."comma", "ioncore.goto_previous()"),
--    kpress(MOD2.."period", "ioncore.goto_next()"),

    kpress(MOD1.."Left", "WScreen.switch_prev(_)"),
    kpress(MOD1.."Right", "WScreen.switch_next(_)"),

    submap(MOD1.."K", {
        bdoc("Go to previous active object."),
        kpress("K", "ioncore.goto_previous()"),

        bdoc("Clear all tags."),
        kpress("T", "ioncore.clear_tags()"),
    }),

    bdoc("Go to n:th screen on multihead setup."),
    kpress(MOD1.."Shift+1", "ioncore.goto_nth_screen(0)"),
    kpress(MOD1.."Shift+2", "ioncore.goto_nth_screen(1)"),

    bdoc("Go to next/previous screen on multihead setup."),
    kpress(MOD1.."Shift+Left", "ioncore.goto_next_screen()"),
    kpress(MOD1.."Shift+Right", "ioncore.goto_prev_screen()"),

    bdoc("Create a new workspace of chosen default type."),
    kpress(MOD1.."F9", "ioncore.create_ws(_)"),

    bdoc("Display the main menu."),
    kpress(MOD1.."F12", "mod_menu.bigmenu(_, _sub, 'mainmenu')"),
    mpress("Button3", "mod_menu.pmenu(_, _sub, 'mainmenu')"),

    bdoc("Display the window list menu."),
    mpress("Button2", "mod_menu.pmenu(_, _sub, 'windowlist')"),
})

-- WMPlex context bindings
--
-- WMPlex 事件的热键绑定
--
-- These bindings work in frames and on screens. The innermost of such
-- contexts/objects always gets to handle the key press. Most of these 
-- bindings define actions on client windows. (Remember that client windows 
-- can be put in fullscreen mode and therefore may not have a frame.)
-- 
-- 这些热键绑定在各个frame和screan中生效。这些事件/实体会一直在您按下按键时生效。
-- 它们所定义的，大多是控制窗体的动作。
-- （记得当窗体(client window)处于全屏模式时，它们不会表现为一个个的框(frame)。）
--
-- The "_sub:WClientWin" guards are used to ensure that _sub is a client
-- window in order to stop Ion from executing the callback with an invalid
-- parameter if it is not and then complaining.
-- 守卫进程 "_sub:WClientWin" 用于保证 _sub 为一个窗体(client window)，以便于当Ion
-- 在执行收回函数时接收到一个非法参数而抱怨。（此处可能有翻译不当）

defbindings("WMPlex", {
    bdoc("Close current object."),
    kpress_wait(MOD1.."C", "WRegion.rqclose_propagate(_, _sub)"),

    bdoc("Nudge current client window. This might help with some "..
         "programs' resizing problems."),
    kpress_wait(MOD1.."L", 
                "WClientWin.nudge(_sub)", "_sub:WClientWin"),

    bdoc("Toggle fullscreen mode of current client window."),
    kpress_wait(MOD1.."Return", 
                "WClientWin.set_fullscreen(_sub, 'toggle')", 
                "_sub:WClientWin"),

    submap(MOD1.."K", {
       bdoc("Kill client owning current client window."),
       kpress("C", "WClientWin.kill(_sub)", "_sub:WClientWin"),

       bdoc("Send next key press to current client window. "..
            "Some programs may not allow this by default."),
       kpress("Q", "WClientWin.quote_next(_sub)", "_sub:WClientWin"),
    }),

    bdoc("Query for manual page to be displayed."),
    kpress(MOD2.."F1", "mod_query.query_man(_, ':man')"),

    bdoc("Show the Ion manual page."),
    kpress(MOD1.."F1", "ioncore.exec_on(_, ':man ion3')"),

    bdoc("Run a terminal emulator."),
    kpress(MOD1.."F2", "ioncore.exec_on(_, 'urxvt')"),

    bdoc("Query for command line to execute."),
    kpress(MOD2.."F3", "mod_query.query_exec(_)"),

    bdoc("Query for Lua code to execute."),
    kpress(MOD1.."F3", "mod_query.query_lua(_)"),

    bdoc("Query for host to connect to with SSH."),
    kpress(MOD2.."F4", "mod_query.query_ssh(_, ':ssh')"),

    bdoc("Query for file to edit."),
    kpress(MOD2.."F5", 
           "mod_query.query_editfile(_, 'run-mailcap --action=edit')"),

    bdoc("Query for file to view."),
    kpress(MOD2.."F6", 
           "mod_query.query_runfile(_, 'run-mailcap --action=view')"),

    bdoc("Query for workspace to go to or create a new one."),
    kpress(MOD2.."F9", "mod_query.query_workspace(_)"),

    bdoc("Query for a client window to go to."),
    kpress(MOD1.."G", "mod_query.query_gotoclient(_)"),
})

-- WFrame context bindings
--
-- WFrame 事件的热键绑定
--
-- These bindings are common to all types of frames. The rest of frame
-- bindings that differ between frame types are defined in the modules' 
-- configuration files.
--
-- 这些热键绑定用于各种框体(frame)。其它框体的配置在模块配置文件中定义。
--

defbindings("WFrame", {
    bdoc("Tag current object within the frame."),
    kpress(MOD1.."T", "WRegion.set_tagged(_sub, 'toggle')", "_sub:non-nil"),

    submap(MOD1.."K", {
        bdoc("Switch to n:th object within the frame."),
        kpress("1", "WFrame.switch_nth(_, 0)"),
        kpress("2", "WFrame.switch_nth(_, 1)"),
        kpress("3", "WFrame.switch_nth(_, 2)"),
        kpress("4", "WFrame.switch_nth(_, 3)"),
        kpress("5", "WFrame.switch_nth(_, 4)"),
        kpress("6", "WFrame.switch_nth(_, 5)"),
        kpress("7", "WFrame.switch_nth(_, 6)"),
        kpress("8", "WFrame.switch_nth(_, 7)"),
        kpress("9", "WFrame.switch_nth(_, 8)"),
        kpress("0", "WFrame.switch_nth(_, 9)"),

        bdoc("Switch to next/previous object within the frame."),
        kpress("N", "WFrame.switch_next(_)"),
        kpress("P", "WFrame.switch_prev(_)"),

        bdoc("Move current object within the frame left/right."),
        kpress("comma", "WFrame.dec_index(_, _sub)", "_sub:non-nil"),
        kpress("period", "WFrame.inc_index(_, _sub)", "_sub:non-nil"),

        bdoc("Maximize the frame horizontally/vertically."),
        kpress("H", "WFrame.maximize_horiz(_)"),
        kpress("V", "WFrame.maximize_vert(_)"),

        bdoc("Attach tagged objects to this frame."),
        kpress("A", "WFrame.attach_tagged(_)"),
    }),

    kpress(MOD1.."comma", "WFrame.switch_prev(_)"),
    kpress(MOD1.."period", "WFrame.switch_next(_)"),

    bdoc("Query for a client window to attach to active frame."),
    kpress(MOD1.."A", "mod_query.query_attachclient(_)"),

    bdoc("Display frame context menu."),
    kpress(MOD1.."M", "mod_menu.menu(_, _sub, 'ctxmenu')"),
    mpress("Button3", "mod_menu.pmenu(_, _sub, 'ctxmenu')"),

    bdoc("Begin move/resize mode."),
    kpress(MOD1.."R", "WFrame.begin_kbresize(_)"),

    bdoc("Switch the frame to display the object indicated by the tab."),
    mclick("Button1@tab", "WFrame.p_switch_tab(_)"),
    mclick("Button2@tab", "WFrame.p_switch_tab(_)"),

    bdoc("Resize the frame."),
    mdrag("Button1@border", "WFrame.p_resize(_)"),
    mdrag(MOD1.."Button3", "WFrame.p_resize(_)"),

    bdoc("Move the frame."),
    mdrag(MOD1.."Button1", "WFrame.p_move(_)"),

    bdoc("Move objects between frames by dragging and dropping the tab."),
    mdrag("Button1@tab", "WFrame.p_tabdrag(_)"),
    mdrag("Button2@tab", "WFrame.p_tabdrag(_)"),

})

-- WMoveresMode context bindings
--
-- WMoveresMode 事件的绑定
-- 
-- These bindings are available keyboard move/resize mode. The mode
-- is activated on frames with the command begin_kbresize (bound to
-- MOD1.."R" above by default).
--
-- 这些绑定让您可以使用键盘来移动和改变框体的大小(move/resize mode)。
-- 您可以用begin_kbresize命令来进入这个移动和改变框体大小的状态。
-- （默认是绑定于上面的MOD1.."R"）

defbindings("WMoveresMode", {
    bdoc("Cancel the resize mode."),
    kpress("AnyModifier+Escape","WMoveresMode.cancel(_)"),

    bdoc("End the resize mode."),
    kpress("AnyModifier+Return","WMoveresMode.finish(_)"),

    bdoc("Grow in specified direction."),
    kpress("Left",  "WMoveresMode.resize(_, 1, 0, 0, 0)"),
    kpress("Right", "WMoveresMode.resize(_, 0, 1, 0, 0)"),
    kpress("Up",    "WMoveresMode.resize(_, 0, 0, 1, 0)"),
    kpress("Down",  "WMoveresMode.resize(_, 0, 0, 0, 1)"),
    kpress("F",     "WMoveresMode.resize(_, 1, 0, 0, 0)"),
    kpress("B",     "WMoveresMode.resize(_, 0, 1, 0, 0)"),
    kpress("P",     "WMoveresMode.resize(_, 0, 0, 1, 0)"),
    kpress("N",     "WMoveresMode.resize(_, 0, 0, 0, 1)"),

    bdoc("Shrink in specified direction."),
    kpress("Shift+Left",  "WMoveresMode.resize(_,-1, 0, 0, 0)"),
    kpress("Shift+Right", "WMoveresMode.resize(_, 0,-1, 0, 0)"),
    kpress("Shift+Up",    "WMoveresMode.resize(_, 0, 0,-1, 0)"),
    kpress("Shift+Down",  "WMoveresMode.resize(_, 0, 0, 0,-1)"),
    kpress("Shift+F",     "WMoveresMode.resize(_,-1, 0, 0, 0)"),
    kpress("Shift+B",     "WMoveresMode.resize(_, 0,-1, 0, 0)"),
    kpress("Shift+P",     "WMoveresMode.resize(_, 0, 0,-1, 0)"),
    kpress("Shift+N",     "WMoveresMode.resize(_, 0, 0, 0,-1)"),

    bdoc("Move in specified direction."),
    kpress(MOD1.."Left",  "WMoveresMode.move(_,-1, 0)"),
    kpress(MOD1.."Right", "WMoveresMode.move(_, 1, 0)"),
    kpress(MOD1.."Up",    "WMoveresMode.move(_, 0,-1)"),
    kpress(MOD1.."Down",  "WMoveresMode.move(_, 0, 1)"),
    kpress(MOD1.."F",     "WMoveresMode.move(_,-1, 0)"),
    kpress(MOD1.."B",     "WMoveresMode.move(_, 1, 0)"),
    kpress(MOD1.."P",     "WMoveresMode.move(_, 0,-1)"),
    kpress(MOD1.."N",     "WMoveresMode.move(_, 0, 1)"),
})

```

## cfg_menus.lua

cfg_menus.lua配置您的主菜单。

```
--
-- Ion menu definitions
--
-- Ion 菜单定义
--

-- Main menu
-- 主菜单
defmenu("mainmenu", {
    submenu("Programs",         "appmenu"),
    menuentry("Lock screen",    "ioncore.exec_on(_, 'xlock')"),
    menuentry("Help",           "mod_query.query_man(_)"),
    menuentry("About Ion",      "mod_query.show_about_ion(_)"),
    submenu("Styles",           "stylemenu"),
    submenu("Session",          "sessionmenu"),
})

-- Application menu
-- 程序菜单
defmenu("appmenu", {
    menuentry("Firefox","ioncore.exec_on(_, 'firefox')"),
    menuentry("Thunderbird","ioncore.exec_on(_, 'thunderbird')"),
    menuentry("Editor","ioncore.exec_on(_, 'lazy-edit')"),
    menuentry("Player","ioncore.exec_on(_, 'lazy-player')"),
    menuentry("FTP","ioncore.exec_on(_, 'lazy-ftp')"),
    menuentry("GVim","ioncore.exec_on(_, 'gvim')"),
    menuentry("Run...", "mod_query.query_exec(_)"),
})

-- Session control menu
-- Session 控制菜单
defmenu("sessionmenu", {
    menuentry("Save",           "ioncore.snapshot()"),
    menuentry("Restart",        "ioncore.restart()"),
    menuentry("Restart PWM",    "ioncore.restart_other('pwm')"),
    menuentry("Restart TWM",    "ioncore.restart_other('twm')"),
    menuentry("Exit",           "ioncore.shutdown()"),
})

-- Context menu (frame/client window actions)
-- 事件菜单 （作用于框体/窗体）
defctxmenu("WFrame", {
    menuentry("Close",          "WRegion.rqclose_propagate(_, _sub)"),
    menuentry("Kill",           "WClientWin.kill(_sub)",
                                "_sub:WClientWin"),
    menuentry("(Un)tag",        "WRegion.set_tagged(_sub, 'toggle')",
                                "_sub:non-nil"),
    menuentry("Attach tagged",  "WFrame.attach_tagged(_)"),
    menuentry("Clear tags",     "ioncore.clear_tags()"),
    menuentry("Window info",    "mod_query.show_clientwin(_, _sub)",
                                "_sub:WClientWin"),
})

```

## cfg_ionws.lua

cfg_ionws.lua配置工作区。

```
--
-- Ion ionws module configuration file
--
-- Ion的ionws模块配置文件
--

-- Bindings for the tiled workspaces (ionws). These should work on any 
-- object on the workspace.
-- 用于叠覆的工作区(ionws)的热键绑定。将用于工作区中的所有实体。

defbindings("WIonWS", {
    bdoc("Split current frame vertically."),
    kpress(MOD1.."V", "WIonWS.split_at(_, _sub, 'bottom', true)"),

    bdoc("Split current frame horizontally."),
    kpress(MOD1.."H", "WIonWS.split_at(_, _sub, 'right', true)"),

    bdoc("Destroy current frame."),
    kpress(MOD1.."Tab", "WIonWS.unsplit_at(_, _sub)"),

    bdoc("Go to frame above/below/right/left of current frame."),
    kpress(MOD2.."Up", "WIonWS.goto_dir(_, 'above')"),
    kpress(MOD2.."Down", "WIonWS.goto_dir(_, 'below')"),
    kpress(MOD2.."Right", "WIonWS.goto_dir(_, 'right')"),
    kpress(MOD2.."Left", "WIonWS.goto_dir(_, 'left')"),
    submap(MOD1.."K", {
        bdoc("Split current frame horizontally."),
        kpress("S", "WIonWS.split_at(_, _sub, 'right', true)"),

        bdoc("Destroy current frame."),
        kpress("X", "WIonWS.unsplit_at(_, _sub)"),
    }),
})

-- Frame bindings. These work in (Ion/tiled-style) frames. Some bindings
-- that are common to all frame types and multiplexes are defined in
-- ion-bindings.lua.
--
-- 框体的热键绑定。用于（Ion/叠覆风格的）框体。
-- 一些对所有框体皆用的绑定，定义于ion-bindings.lua。
--

--defbindings("WFrame-on-WIonWS", {
--})

-- WFloatFrame context menu extras
-- 额外的 WFloatFrame 事件菜单

if mod_menu then
    defctxmenu("WIonWS", {
        menuentry("Destroy frame", 
                  "WIonWS.unsplit_at(_, _sub)"),
        menuentry("Split vertically", 
                  "WIonWS.split_at(_, _sub, 'bottom', true)"),
        menuentry("Split horizontally", 
                  "WIonWS.split_at(_, _sub, 'right', true)"),
        menuentry("Flip", "WIonWS.flip_at(_, _sub)"),
        menuentry("Transpose", "WIonWS.transpose_at(_, _sub)"),
        submenu("Float split", {
            menuentry("At left", 
                      "WIonWS.set_floating_at(_, _sub, 'toggle', 'left')"),
            menuentry("At right", 
                      "WIonWS.set_floating_at(_, _sub, 'toggle', 'right')"),
            menuentry("Above",
                      "WIonWS.set_floating_at(_, _sub, 'toggle', 'up')"),
            menuentry("Below",
                      "WIonWS.set_floating_at(_, _sub, 'toggle', 'down')"),
        }),
        submenu("At root", {
            menuentry("Split vertically", 
                      "WIonWS.split_top(_, 'bottom')"),
            menuentry("Split horizontally", 
                      "WIonWS.split_top(_, 'right')"),
            menuentry("Flip", "WIonWS.flip_at(_)"),
            menuentry("Transpose", "WIonWS.transpose_at(_)"),
        }),
    })
end

```

## look.lua

look.lua设置窗体的主题。在文件末端，默认的主题被设置为：

```
dopath("look_xerxes") 

```

主题的命名规则为： **`look_<主题名>.lua`** 。修改主题名，即可得到相应的主题。