**翻译状态：** 本文是英文页面 [Wine](/index.php/Wine "Wine") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-08-5，点击[这里](https://wiki.archlinux.org/index.php?title=Wine&diff=0&oldid=389504)可以查看翻译后英文页面的改动。

相关文章

*   [Steam](/index.php/Steam "Steam")
*   [CrossOver](/index.php/CrossOver "CrossOver")

[Wine](https://en.wikipedia.org/wiki/Wine_(software) 是类UNIX系统下运行微软Windows程序的"兼容层"。在Wine中运行的Windows程序，就如同运行原生Linux程序一样，不会有模拟器那样的性能问题。

获取更详细的介绍请浏览[项目官方网站](http://www.winehq.org/)和[wiki](http://wiki.winehq.org/)页面。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 配置](#配置)
    *   [2.1 WINEPREFIX](#WINEPREFIX)
    *   [2.2 WINEARCH](#WINEARCH)
    *   [2.3 显卡驱动](#显卡驱动)
    *   [2.4 声音](#声音)
        *   [2.4.1 MIDI 支持](#MIDI_支持)
    *   [2.5 其他函数库](#其他函数库)
    *   [2.6 字体](#字体)
    *   [2.7 启动器和菜单](#启动器和菜单)
        *   [2.7.1 创建菜单项](#创建菜单项)
        *   [2.7.2 Gnome3 中清理 Wine 菜单启动项](#Gnome3_中清理_Wine_菜单启动项)
        *   [2.7.3 修复 KDE 4 菜单问题](#修复_KDE_4_菜单问题)
*   [3 运行 Windows 程序](#运行_Windows_程序)
*   [4 技巧和技巧](#技巧和技巧)
    *   [4.1 取消注册Wine文件关联](#取消注册Wine文件关联)
    *   [4.2 Dual Head with different resolutions](#Dual_Head_with_different_resolutions)
    *   [4.3 exe-thumbnailer](#exe-thumbnailer)
    *   [4.4 CSMT patch](#CSMT_patch)
    *   [4.5 CSMT via wine-staging](#CSMT_via_wine-staging)
        *   [4.5.1 Further Information](#Further_Information)
    *   [4.6 Changing the language](#Changing_the_language)
    *   [4.7 Proper mounting of optical media images](#Proper_mounting_of_optical_media_images)
    *   [4.8 Burning optical media](#Burning_optical_media)
    *   [4.9 OpenGL 模式](#OpenGL_模式)
    *   [4.10 将 Wine 作为 Win16/Win32 程序的解释器](#将_Wine_作为_Win16/Win32_程序的解释器)
    *   [4.11 Wine 控制台](#Wine_控制台)
    *   [4.12 Winetricks](#Winetricks)
    *   [4.13 Installing .NET framework 4.0](#Installing_.NET_framework_4.0)
    *   [4.14 Crackling sound when using PulseAudio](#Crackling_sound_when_using_PulseAudio)
    *   [4.15 16 Bit Programs](#16_Bit_Programs)
    *   [4.16 解决中文乱码](#解决中文乱码)
*   [5 第三方工具](#第三方工具)
    *   [5.1 CrossOver](#CrossOver)
    *   [5.2 PlayOnLinux/PlayOnMac](#PlayOnLinux/PlayOnMac)
    *   [5.3 PyWinery](#PyWinery)
    *   [5.4 Q4wine](#Q4wine)
*   [6 相关链接](#相关链接)

## 安装

**警告:** 如果您的账户能浏览某些文件或资源，Wine运行的程序也可以。Wine不是[沙箱](https://en.wikipedia.org/wiki/Sandbox_(computer_security) "wikipedia:Sandbox (computer security)")。如果很重视安全，请考虑使用[虚拟化](https://en.wikipedia.org/wiki/Virtualization "wikipedia:Virtualization")。

Wine可通过开启[Multilib](/index.php/Multilib "Multilib")仓库来安装[wine](https://www.archlinux.org/packages/?name=wine)(稳定版本)or[wine-staging](https://www.archlinux.org/packages/?name=wine-staging)(测试版本)。[Wine-Staging](http://www.wine-staging.com/)包括目前上游未采纳的补丁，专门为wine开发者在向上游打补丁前测试。

另外，您可能需要安装 [wine_gecko](https://www.archlinux.org/packages/?name=wine_gecko) 和 [wine-mono](https://www.archlinux.org/packages/?name=wine-mono) 软件包。它们分别用于运行依赖于 Internet Explorer 和 .NET 的程序。不过，也可以随后通过 Wine 在需要时下载安装这些组件。但如果提前下载安装，您就可以离线使用它们，而且 Wine 不必为了每一个 WINEPREFIX 都单独下载。

**平台差异**

默认的Wine是32位的程序，也是i686的Arch软件包。所以它不能运行64位的Windows程序（反正是罕见的）。

然而，x86_64的Wine软件包目前以 `--enable-win64`方式编译。这个参数激活了[WoW64](https://en.wikipedia.org/wiki/WoW64 "wikipedia:WoW64")的Wine版本。

*   在Windows中，这个复杂的子系统允许用户同时使用32位和64位的Windows程序，甚至是在同一目录。

*   在Wine中，用户将必须建立单独分开的目录/前缀。这项Wine功能仍是试验阶段，并建议用户使用一个win32`WINEPREFIX`。浏览[Wine64](http://wiki.winehq.org/Wine64)以获取有关这个的详细信息。

总结一下，配置`WINEARCH=win32`后，x86_64平台的Arch和i686平台的Arch完全相同。

**注意:** 如果在64位环境中执行`winetricks`或其它程序出现问题，请试试创建一个新的32位`WINEPREFIX`. 参见下面的[#使用 WINEARCH](#使用_WINEARCH)

## 配置

配置Wine的方式通常有：

*   [winecfg](http://wiki.winehq.org/winecfg)是Wine的图形界面配置程序。控制台下调用`$ winecfg`（或指定系统目录：`$ WINEPREFIX=~/.系统目录 winecfg`）即可启动
*   [control.exe](http://wiki.winehq.org/control)是Windows控制面板的Wine实现，通过`$ wine control`命令启动
*   [regedit](http://wiki.winehq.org/regedit)是Wine的注册表编辑器，比较前两者，该工具能配置更多东西。部分常用键值参见：[WineHQ's article on Useful Registry Keys](http://wiki.winehq.org/UsefulRegistryKeys)

### WINEPREFIX

Wine默认将配置文件和安装的Windows程序保存在`~/.wine`。这样的目录称为一个"Wine prefix"或"Wine bottle"（保留原文，下文称“系统目录”）。每次运行Windows程序（包括内置程序，如`winecfg`）时，系统目录会自动创建（如果缺失）或更新。系统目录中存放有相当于Windows下 `C:\`C盘（更确切的说应是系统盘）的文件夹。

通过设置`WINEPREFIX`环境变量，可以更改Wine系统目录的位置。如果希望让不同的Windows程序使用不同的系统环境或配置，这一变量会非常有用。

例如，如果您使用 `$ env WINEPREFIX=~/.win-a wine-A程序.exe`参数来运行一个程序。另一个使用 `$ env WINEPREFIX=~/.win-b wine-B程序.exe`参数，这两个程序将使用独立的C盘和注册表配置。

以下命令会建立一个默认的系统目录，且不启动任何Windows程序：

```
$ env WINEPREFIX=~/.customprefix wineboot -u

```

### WINEARCH

对于64位用户，如果使用[multilib]仓库里的Wine，默认创建的系统目录是64位环境的。若想使用纯32位环境，修改`WINEARCH` 变量win32为即可： `$ WINEARCH=win32 winecfg`这样就会生成32位Wine环境。若不设置`WINEARCH`得到的就是64位环境。

通过`WINEPREFIX`变量，在不同的系统目录分别创建32位和64位环境：

```
$ WINEARCH=win32 WINEPREFIX=~/win32 winecfg 
$ WINEPREFIX=~/win64 winecfg

```

**注意:** 系统目录创建过程中，64位版本的wine将视全部目录如同64位系统目录，也将不会在已存在的目录中创建任何32位的.创建32位系统目录，您必须让Wine创建指定的`WINEPREFIX`目录。

winetricks也接受`WINEPREFIX`变量，以安装Steam为例：

```
env WINEARCH=win32 WINEPREFIX=~/.local/share/wineprefixes/steam winetricks steam

```

To have them permanently defined for [bash configuration ~/.bashrc](/index.php/Bash#Shell_and_environment_variables "Bash") do:

```
export WINEPREFIX=$HOME/.config/wine/
export WINEARCH=win32

```

**提示：** 编辑 [~/.bashrc](/index.php/Bash_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#外壳和环境变量 "Bash (简体中文)")，使得 WINEPREFIX 和 WINEARCH 永久生效。

**注意:** 不必手动在 `wineprefixes` 文件夹下建立 steam 文件夹，Wine会自动创建不存在的系统目录。

### 显卡驱动

使用Wine运行Windows游戏时，可能需要高性能的显卡驱动。[Nvidia](/index.php/NVIDIA_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "NVIDIA (简体中文)")、[Amd/ATI](/index.php/ATI_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ATI (简体中文)")用户最好使用闭源驱动。[Intel](/index.php/Intel_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Intel (简体中文)")显卡用户也可以选择开源驱动，它已经非常成熟。

要是显卡驱动有问题或者相关配置有误，控制台用Wine运行某些程序时会输出：

```
Direct rendering is disabled, most likely your OpenGL drivers have not been installed correctly

```

x86-64用户需要从[multilib](/index.php/Multilib "Multilib")或[AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)")安装额外的32位库：

*   **NVIDIA**：[lib32-nvidia-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-libgl) 至于老显卡，请到 AUR 搜索 **lib32-nvidia-utils** （如-173xx）。
*   **NVIDIA （开源驱动）**：[lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa)。
*   **Intel**: [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa)。运行Wine时需要手动添加`LIBGL_DRIVERS_PATH=/usr/lib32/xorg/modules/dri`
*   **AMD/ATI**：[lib32-catalyst-utils](https://aur.archlinux.org/packages/lib32-catalyst-utils/)。
*   **AMD/ATI （开源驱动）**: [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa)。

**注意:** 安装上述软件包后，可能需要重启X才能生效！

### 声音

Wine程序有可能遇到某些声音问题。首先，确保`winecfg`中只启用了一种声卡驱动。目前，Wine对[Alsa](/index.php/Alsa_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Alsa (简体中文)")的支持最好。

x86_64平台下使用[Alsa](/index.php/Alsa_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Alsa (简体中文)")的话，需要安装[lib32-alsa-lib](https://www.archlinux.org/packages/?name=lib32-alsa-lib)。如果还要使用PulseAudio，则需安装[lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse)。

若使用[OSS](/index.php/OSS_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "OSS (简体中文)")，需要安装[lib32-alsa-oss](https://www.archlinux.org/packages/?name=lib32-alsa-oss)。仅靠内核驱动是不行的。

安装上述软件包后，若`winecfg`**仍**无法识别声卡（Selected driver: (none)），请尝试[registry 通过注册表配置](http://wiki.jswindle.com/index.php/Wine_Registry#Configuring_Sound)。

运行使用某些高级声音系统的游戏，可能还需要安装[lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal)。

#### MIDI 支持

[MIDI](/index.php/MIDI "MIDI") was a quite popular system for video games music in the 90's. If you are trying out old games, it is not uncommon that the music will not play out of the box. Wine has excellent MIDI support. However you first need to make it work on your host system. See the wiki page for more details. Last but not least you need to make sure Wine will use the correct MIDI output. See the [Wine Wiki](http://wiki.winehq.org/MIDI) for a detailed setup.

### 其他函数库

*   某些程序（如 Office 2003）需要解析HTML、XML（使用MSXML库），需要安装[lib32-libxml2](https://www.archlinux.org/packages/?name=lib32-libxml2)。

*   播放音频的程序可能依赖[lib32-mpg123](https://www.archlinux.org/packages/?name=lib32-mpg123)。

*   使用色彩管理引擎的一些应用 (例如： PDF查看器, 图片查看器, etc) may require [lib32-lcms2](https://www.archlinux.org/packages/?name=lib32-lcms2).

*   对于使用图像处理库的程序，可能依赖[lib32-giflib](https://www.archlinux.org/packages/?name=lib32-giflib)和[lib32-libpng](https://www.archlinux.org/packages/?name=lib32-libpng)，

*   x86_64的加密支持需要[lib32-gnutls](https://www.archlinux.org/packages/?name=lib32-gnutls)软件包。

### 字体

如果没有安装微软Truetype字体，Wine程序的字体显示可能会一团糟，参见[MS Fonts (简体中文)](/index.php/MS_Fonts_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "MS Fonts (简体中文)")。如果还是不行，试试`winetricks allfonts`。

上述操作后，杀死wine相关进程再运行`winecfg`，字体应该变好看了。

如果字体看起来很毛糙，试试用[regedit](http://wiki.winehq.org/regedit)导入下列文本文件：

```
[HKEY_CURRENT_USER\Software\Wine\X11 Driver]
"ClientSideWithRender"="N"

```

**提示：** 高分辨率显示器，可在winecfg的显示选项卡中适当dpi的值，例如缩放150%，将dpi设置为144。

参阅 [Font configuration#Applications without fontconfig support](/index.php/Font_configuration#Applications_without_fontconfig_support "Font configuration").

### 启动器和菜单

Wine不会为内置程序（如`winecfg`、`winebrowser`）创建桌面启动器和菜单项。但手动安装的Windows程序通常会自动创建启动器和菜单项。在Windows下，安装程序（如`setup.exe`）通常会在桌面和开始菜单建立快捷方式，而Wine下会创建遵循freedesktop.org规范的.desktop文件（即启动器，相当于快捷方式）。

**提示：** 如果启动器*没有*自动创建，或者这些文件丢失了，可以尝试使用[winemenubuilder](http://wiki.winehq.org/winemenubuilder)修复。

Ubuntu下，Wine项目以子菜单形式出现在系统菜单。以下步骤将实现这个效果：

#### 创建菜单项

首先，用Wine安装一个Windows程序，以建立基本的菜单。完成后，向其中添加菜单项。桌面右键选择`"创建启动器..."`（不同桌面环境操作有所差异），设置如下：

```
**类型（Type）**: 应用程序（Application）
**名称（Name）**: 配置
**命令（Command）**: winecfg
**备注（Comment）**: Wine配置工具

```

```
**类型**: 应用程序
**名称**: 卸载程序
**命令**: wine uninstaller
**备注**: 卸载Wine下的Windows程序

```

```
**类型**: 应用程序
**名称**: 浏览 C:\
**命令**: wine winebrowser c:\\
**备注**: 浏览Wine中虚拟的C盘

```

现在，桌面上出现了三个启动器，下面将把它们移入菜单。不过首先，我们给这些启动器加上动态图标（由图标主题提供）。方法是，用文本编辑器打开启动器，编辑Icon项目：

`配置` 启动器：

```
Icon=wine-winecfg

```

`卸载程序` 启动器:

```
Icon=wine-uninstaller

```

`浏览 C:\` 启动器:

```
Icon=wine-winefile

```

**提示：** 多数桌面环境在上述“创建启动器”步骤即可设置图标。以第一个启动器为例，在选择图标窗口中搜索wine-winecfg，选择即可，无需手动编辑。 ——译者注

如果图标无法显示或者你觉得很丑陋，换成其他图标也可以。右键设置启动器，应该有更改图标的地方。很多图标主题，例如[GNOME-colors](http://www.gnome-look.org/content/show.php/GNOME-colors?content=82562)，都提供这些图标。

现在，将启动器移入菜单。把启动器复制到 `~/.local/share/applications/wine/` 目录即可。

诶？图标还没出现在菜单中！还剩下最后一步，创建下列文本文件：

 `~/.config/menus/applications-merged/wine-utilities.menu` 
```
 <!DOCTYPE Menu PUBLIC "-//freedesktop//DTD Menu 1.0//EN"
 "http://www.freedesktop.org/standards/menu-spec/menu-1.0.dtd">
 <Menu>
   <Name>Applications</Name>
   <Menu>
     <Name>wine-wine</Name>
     <Directory>wine-wine.directory</Directory>
     <Include>
 	<Filename>wine-Configuration.desktop</Filename>
     </Include>
     <Include>
 	<Filename>wine-Browse C:\.desktop</Filename>
     </Include>
     <Include>
 	<Filename>wine-Uninstall Programs.desktop</Filename>
     </Include>
   </Menu>
 </Menu>

```

再看看菜单，应该万事大吉了。

#### Gnome3 中清理 Wine 菜单启动项

系统全局的菜单启动器安装在 `/usr/share/applications/`，清除相应程序的“.desktop”文件即可从整个系统删除该启动器。

如果这样还是无法解决问题，那么很可能 Wine 的启动器存放在用户级别的 `~/.local/share/applications/wine/Programs/` 目录中。删除相应的“.desktop”文件即可清理对应启动项。删除整个 Programs 文件夹将清理所有 Wine 程序的启动项。

#### 修复 KDE 4 菜单问题

Wine菜单项有可能[错误地出现](https://bugs.launchpad.net/ubuntu/+source/wine/+bug/263041)在`"Lost & Found（其他）"` ，而非Wine子菜单。原因是kde-applications.menu文件缺失`MergeDir`配置。

编辑`/etc/xdg/menus/kde-applications.menu`。

在文件末尾处，`<DefaultMergeDirs/>`后添加`<MergeDir>applications-merged</MergeDir>`。修改后内容大致如下：

```
<Menu>
        <Include>
                <And>
                        <Category>KDE</Category>
                        <Category>Core</Category>
                </And>
        </Include>
        <DefaultMergeDirs/>
        **<MergeDir>applications-merged</MergeDir>**
        <MergeFile>applications-kmenuedit.menu</MergeFile>
</Menu>

```

另一个方法是：

```
ln -s ~/.config/menus/applications-merged ~/.config/menus/kde-applications-merged

```

这样的好处是，不会因为KDE升级而重置配置。但该方法只对一个用户有效。

## 运行 Windows 程序

**警告:** 千万不要以root身份运行Wine！详情参见[本文](http://wiki.winehq.org/FAQ#run_as_root)。

运行Windows程序：

```
$ wine <exe文件>

```

内置的msiexec程序可以运行MSI安装包：

```
$ msiexec /i *path_to_msi*

```

## 技巧和技巧

**提示：** 此外您可能会感兴趣以下文章的开始所提供的链接

*   [Wine程序数据库 (Wine Application Database, AppDB)](http://appdb.winehq.org/) —— 特定Windows程序的Wine兼容情况（运行时的已知问题、用户评分、指南等等）
*   [WineHQ论坛](http://forum.winehq.org/) —— 要是看完上述网页还有问题，可以到这里咨询

这里介绍一些安装Windows组件的工具。由于这些工具可能严重破坏Wine配置，没有需要时最好不要使用。

### 取消注册Wine文件关联

在默认情况下,Wine接管了许多扩展名. 一些扩展名 {例如 `.vbs` 或者 `.chm`) 是Windows专用, 用Wine打开这些程序是很方便的. 但是, 有一些其他格式 (例如 `gif`, `jpeg`, `txt`, `js`) 在Wine中用 `Internet Explorer` 和 `Windows记事本` 打开会出错 .

Wine的文件关联设置在 `~/.local/share/applications/` 像 {{ic|wine-extension-{extension}.desktop}} 这样的文件中. 删除与要取消注册的扩展名相对应的文件. 或者像这样删除所有的扩展名:

```
$ rm -f ~/.local/share/applications/wine-extension*.desktop
$ rm -f ~/.local/share/icons/hicolor/*/*/application-x-wine-extension*

```

Next, remove the old cache:

```
$ rm -f ~/.local/share/applications/mimeinfo.cache
$ rm -f ~/.local/share/mime/packages/x-wine*
$ rm -f ~/.local/share/mime/application/x-wine-extension*

```

And, update the cache:

```
$ update-desktop-database ~/.local/share/applications

```

Please note Wine will still create new file associations and even recreate the file associations if the application sets the file associations again.

### Dual Head with different resolutions

If you have issues with dual-head setups and different display resolutions you are probably missing [lib32-libxrandr](https://www.archlinux.org/packages/?name=lib32-libxrandr).

### exe-thumbnailer

This is a small piece of UI code meant to be installed with (or even before) Wine. It provides thumbnails for executable files that show the embedded icons when available, and also gives the user a hint that Wine will be used to open it. Details can be found at [Wine wiki](http://wiki.winehq.org/exe-thumbnailer). Install it with the [gnome-exe-thumbnailer](https://aur.archlinux.org/packages/gnome-exe-thumbnailer/) package.

### CSMT patch

Currently [wine developers](http://www.winehq.org/pipermail/wine-devel/2013-September/101106.html) experiment with stream/worker thread optimizations for Wine. You may experience an enormous performance improvement by using this experimental patched Wine versions. Many games may run as fast as on Windows or even faster. This Wine patch is is known as CSMT patch and works with NVidia and AMD graphics cards.

**Note:** This is *still experimental code*, therefore, it may not work as expected. Please, report your experiences to the developers for helping with development of those patches.

The easy way is to install [playonlinux](https://www.archlinux.org/packages/?name=playonlinux). Then install your game and activate the Wine version *1.7.4-CSMT* from the `Tools` → `Manage Wine Versions` menu in PlayOnLinux. For now it is recommended to use the patched Wine version *1.7.4-CSMT*.

Open your game's configuration settings and copy the following settings to the `Miscellaneous`/`Command to exec before running the program` section of your game configuration settings:

```
export WINEDEBUG=-all
export LD_PRELOAD="libpthread.so.0 libGL.so.1"
export __GL_THREADED_OPTIMIZATIONS=0
export __GL_SYNC_TO_VBLANK=1
export __GL_YIELD="NOTHING"
export CSMT=enabled

```

Make sure you have disabled `StrictDrawOrdering` from `Tools` → `General`.

### CSMT via wine-staging

[Wine-staging](http://www.wine-staging.com/) includes CSMT support, and can be installed with the [wine-staging](https://www.archlinux.org/packages/?name=wine-staging) package, or directly via the wine-staging [Arch Linux repo](https://github.com/wine-compholio/wine-staging/wiki/Installation#-arch-linux).

CSMT support needs to be enabled before it can be used, instructions can be found [here](https://github.com/wine-compholio/wine-staging/wiki/CSMT#enabledisable-csmt), no further configuration is needed.

#### Further Information

[Phoronix Forum discussion](http://www.phoronix.com/forums/showthread.php?93967-Wine-s-Big-Command-Stream-D3D-Patch-Set-Updated/page3&s=7775d7c3d4fa698089d5492bb7b1a435) with the CSMT developer Stefan Dösinger

[FOSDEM2014 CSMT presentation](http://wiki.winehq.org/FOSDEM2014?action=AttachFile&do=get&target=d3d-drivers.odp) of CSMT with benchmarks

[Here](https://www.youtube.com/playlist?list=PL0P2a_sII2eTd8uq-azTNpQjiFLqBhDjg) you find some game videos running with CSMT enabled

### Changing the language

Some programs may not offer a language selection, they will guess the desired language upon the sytem locales. Wine will transfer the current environment (including the locales) to the application, so it should work out of the box. If you want to force a program to run in a specific locale (which is fully [generated](/index.php/Locale "Locale") on your system), you can call Wine with the following setting:

```
LC_ALL=*xx_XX.encoding* wine */path/to/program*

```

For instance

```
LC_ALL=it_IT.UTF-8 wine */path/to/program*

```

=== 安装 Microsoft Office ===/

更新（2013年4月9日）：对于 Wine 1.5.27，下面所述的步骤已经不必要了。先安装 winbind（包含在 [samba](https://www.archlinux.org/packages/?name=samba) 中），然后执行：

```
$ export WINEPREFIX="<用户家目录中的某一可写目录>"	
$ export WINEARCH="win32"
$ wine /到/office安装盘/的路径/setup.exe

```

可以把上述 export 语句加入 bashrc 文件。

安装结束后，打开 Word 或 Excel，联网激活。完成后，关闭程序，执行 **winecfg**，在“函数库”选项卡中把 riched20 设置为“Native (Windows)”。这样 PowerPoint 就可以正常工作。 （使用 Office Home/Student 2010 和 wine 1.5.27 测试。在线激活有效）

安装Office套装前，需要先安装某些Windows组件：

```
$ WINEARCH=win32 WINEPREFIX=/path/to/wineprefix winecfg
# pacman -S winetricks
$ winetricks msxml3 # For MS Office 2007
$ winetricks msxml3 msxml6 # For MS Office 2010
$ wine /path/to/office_cd/setup.exe

```

更多信息，参见[WineHQ上的文章](http://appdb.winehq.org/appview.php?iVersionId=4992)。

**注意:** [playonlinux](https://www.archlinux.org/packages/?name=playonlinux) 提供了一个自定义安装脚本，简化了 Office 2003、2007 和 2010 的安装。您只需提供 setup.exe 或 ISO 文件，这个脚本就可以指导您完成安装，完全不需要自己设置 Wine。

### Proper mounting of optical media images

Some applications will check for the optical media to be in drive. They may check for data only, in which case it might be enough to configure the corresponding path as being a CD-ROM drive in *winecfg*. However, other applications will look for a media name and/or a serial number, in which case the image has to be mounted with these special properties.

Some virtual drive tools do not handle these metadata, like fuse-based virtual drives (Acetoneiso for instance). CDEmu will handle it correctly.

### Burning optical media

To burn CDs or DVDs, you will need to load the `sg` [kernel module](/index.php/Kernel_module "Kernel module").

### OpenGL 模式

很多游戏（比如魔兽争霸啦）都支持OpenGL模式，在Wine下*可能*比默认DirectX模式性能更好。一般添加`-opengl`启动程序即可，但*不同程序可能有所不同*：

```
$ wine /path/to/3d_game.exe -opengl

```

请参考[AppDB](http://appdb.winehq.org)，了解特定程序的相关信息。

### 将 Wine 作为 Win16/Win32 程序的解释器

通知内核识别和执行 Win16/Win32 程序的方式：

```
echo ':DOSWin:M::MZ::/usr/bin/wine:' > /proc/sys/fs/binfmt_misc/register

```

To make the setting permanent, create a configuration file in `/etc/binfmt.d` with the following contents: 测试效果，若一切正常，可以使该设置永久生效。在 `/etc/binfmt.d` 目录创建新的配置文件，内容为：

 `/etc/tmpfiles.d/wine.conf`  `:DOSWin:M::MZ::/usr/bin/wine:` 

说明一下，和 initscripts 不同，systemd 会自动挂载 `/proc/sys/fs/binfmt_misc`，所以只需要通过临时文件机制向内核写入配置即可。

更多信息，参见 [Systemd (简体中文)#临时文件](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#临时文件 "Systemd (简体中文)")。

现在，直接运行Windows程序试试：

```
chmod 755 exefile.exe
./exefile.exe

```

### Wine 控制台

有些时候，可能需要运行`.exe`给游戏打补丁，比如给古董游戏添加宽屏支持。这时直接通过Wine运行可能没有用。那么，打开终端，运行一下命令：

```
$ wineconsole cmd

```

将进入一个和Windows下cmd一样的命令行环境。在该环境下试试也许就可以了。

### Winetricks

使用[Winetricks](http://wiki.winehq.org/winetricks)快速脚本，能够方便地安装许多Windows组件，包括DirectX、msxml（被Office 2007、IE浏览器依赖）visual运行库还有其他更多的。

您可以使用[pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")或者从[AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)")上获取[winetricks-git](https://aur.archlinux.org/packages/winetricks-git/)软件包来安装该工具：

运行：

```
$ winetricks

```

### Installing .NET framework 4.0

First create a new 32-bit Wine prefix if you are on a 64-bit system.

```
$ WINEARCH=win32 WINEPREFIX=~/win32 winecfg

```

Then install the following packages using winetricks

```
$ WINEARCH=win32 WINEPREFIX=~/win32 winetricks -q msxml3 dotnet40 corefonts

```

### Crackling sound when using PulseAudio

If you experience crackling sound in Wine applications when PulseAudio is in use, edit the file `/etc/pulse/daemon.conf` by uncommenting the line `; default-fragment-size-msec = 25` and setting the value to `5` such that it looks like this:

```
default-fragment-size-msec = 5

```

See [here](http://wiki.winehq.org/FAQ#head-58290651b9f85c059a8bfc98118a0262e2cca84b) for further information.

### 16 Bit Programs

Upon running older Windows 9x programs, the following error may be encountered:

```
modify_ldt: Invalid argument
err:winediag:build_module Failed to create module for "krnl386.exe",
16-bit LDT support may be missing.
err:module:attach_process_dlls "krnl386.exe16" failed to initialize,
aborting

```

In this case, running the following may fix it:

```
echo 1 > /proc/sys/abi/ldt16

```

Source: [Fedora Mailing List](http://www.spinics.net/linux/fedora/fedora-users/msg450821.html)

### 解决中文乱码

中文乱码解决，新建一个reg文件（例如 zh.reg）添加如下内容：

```
REGEDIT4
[HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\FontLink\SystemLink]
"Lucida Sans Unicode"="wqy-microhei.ttc"
"Microsoft Sans Serif"="wqy-microhei.ttc"
"Microsoft YaHei"="wqy-microhei.ttc"
"微软雅黑"="wqy-microhei.ttc"
"MS Sans Serif"="wqy-microhei.ttc"
"Tahoma"="wqy-microhei.ttc" 
"Tahoma Bold"="wqy-microhei.ttc"
"SimSun"="wqy-microhei.ttc"
"Arial"="wqy-microhei.ttc"
"Arial Black"="wqy-microhei.ttc"
"宋体"="wqy-microhei.ttc"
"新細明體"="wqy-microhei.ttc"

```

**提示：** 这里以文泉驿微米黑为例，如果使用其他字体，请到/usr/share/fonts目录下找到该字体的完整名称，例如使用adobe source hans 中号字体，将上面的wqy-microhei.ttc改为SourceHanSansCN-Medium.otf。

然后打开注册表编辑器:

```
 wine regedit

```

在注册表编辑器界面选择“注册表”--“导入”，导入该wine-fonts.reg文件即可。 或者直接运行:

```
 $regedit zh.reg

```

更多信息参考[Wine的中文显示与字体设置](http://linux-wiki.cn/wiki/Wine%E7%9A%84%E4%B8%AD%E6%96%87%E6%98%BE%E7%A4%BA%E4%B8%8E%E5%AD%97%E4%BD%93%E8%AE%BE%E7%BD%AE)

## 第三方工具

这些程序有其自己的主页和支持论坛。

### CrossOver

[CrossOver](http://www.codeweavers.com/about/) 有单独的[wiki 页面](/index.php/CrossOver "CrossOver").

### PlayOnLinux/PlayOnMac

[PlayOnLinux](http://www.playonlinux.com/)是一个图形界面的Windows/DOS程序管理器。它提供了一些帮助配置/运行程序的脚本，能够管理多个不同版本的Wine，甚至能对不同程序使用不同Wine版本。参考[AppDB](http://appdb.winehq.org)，看看哪个Wine版本对你要运行的程序兼容最好。从[AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)")安装[playonlinux](https://www.archlinux.org/packages/?name=playonlinux)。

### PyWinery

[PyWinery](http://code.google.com/p/pywinery/)是一个简单的、图形界面的Wine系统目录管理器，用它可以方便地管理不同系统目录，并从不同系统目录运行程序。同时可以开启winetricks在同一系统目录，打开系统目录所在文件夹, `winecfg`, 软件卸载程序和wineDOS。[AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)")中提供了软件包[pywinery](https://aur.archlinux.org/packages/pywinery/)。当你使用很多系统目录（一个打游戏用、一个编程用……）时，这个程序会非常有用。

它在默认情况下使用winetricks打开`.exe`文件，所以你可以选择你有的任何Wine的配置。

### Q4wine

[Q4Wine](http://q4wine.brezblock.org.ua/) 是一个图形界面的系统目录（wine-prefix）管理器。它的特色是可以把 QT 主题导入 Wine 配置，使两者完美整合。[q4wine](https://aur.archlinux.org/packages/q4wine/) 软件包在 [[multilib](/index.php/Multilib "Multilib")] 仓库中提供。

## 相关链接

*   [Wine官方网站](http://www.winehq.com/)
*   [Wine程序数据库](http://appdb.winehq.org/)
*   [加速Wine，显卡及OpenGL高级配置](http://linuxgamingtoday.wordpress.com/2008/02/16/quick-tips-to-speed-up-your-gaming-in-wine/)
*   [FileInfo](http://wiki.gotux.net/code:perl:fileinfo) —— Find Win32 PE/COFF headers in EXE/DLL/OCX files under linux/unix environment