**翻译状态：** 本文是英文页面 [Infinality](/index.php/Infinality "Infinality") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-09-22，点击[这里](https://wiki.archlinux.org/index.php?title=Infinality&diff=0&oldid=451547)可以查看翻译后英文页面的改动。

[infinality](http://www.infinality.net/)补丁集可以显著改善 freetype2 字体渲染。另外也新增了一些新功能。

Infinality可以通过动态设置环境变量来启用功能。设置如下：

*   **加粗增强 (Emboldening Enhancement)**：禁用Y加粗可以（使用原生 TrueType 微调器或者自动微调器）使得没有加粗版本的字体的显示得以改善。
*   **自动微调 (Auto-Autohint)**：强制那些不含 TrueType 信息的字体使用自动微调。
*   **自动微调增强 (Autohint Enhancement)**：自动微调使得水平字符主干微移 (snap horizontal stems) 对齐像素。看起来就像精心微调 TrueType 的字体一样。
*   **自定义有限冲激响应滤波器 (Customized FIR Filter)**：运行时（使用原生 TrueType 微调器或者自动微调器）选择[过滤器的值](http://www.infinality.net/forum/viewtopic.php?f=2&t=19) 。
*   **字符主干对齐 (Stem Alignment)**：根据字符的像素边界优化调整。适用于原生 TrueType 微调器或者自动微调器。
*   **伪伽玛校正 (Pseudo Gamma Correction)**：（使用原生 TrueType 微调器或者自动微调器）亮化和暗化给定大小的字形达到规定的值。
*   **加粗细体字体 (Embolden Thin Fonts)**：加粗细体字体，使得他们更加好看（自动微调）。
*   **强制微少微调 (Force Slight Hinting)**：强制微少微调甚至程序希望饱和微调。
*   **ChromeOS 风格锐化 (ChromeOS Style Sharpening)**: ChromeOS 所使用的锐化字体渲染的补丁现在包含在当infinality补丁集里。

具体详见 [README](http://www.infinality.net/forum/viewtopic.php?f=2&t=18)。

内置了一些预设置，可以通过设置那些在 `/etc/X11/xinit/xinitrc.d/xft-settings.sh` 中的 USE_STYLE 变量在来使用。

变量应该在 `/etc/profile.d/infinality-settings.sh` 里进行设置。模板详见 [infinality-settings.sh](https://github.com/bohoomil/fontconfig-ultimate/blob/master/freetype/infinality-settings.sh)。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 Infinality-bundle](#Infinality-bundle)
        *   [1.1.1 附加字体](#.E9.99.84.E5.8A.A0.E5.AD.97.E4.BD.93)
    *   [1.2 AUR](#AUR)
*   [2 Configuration](#Configuration)
    *   [2.1 Fonts with restricted licenses](#Fonts_with_restricted_licenses)
    *   [2.2 Xft and FreeType settings](#Xft_and_FreeType_settings)
    *   [2.3 Fontconfig settings](#Fontconfig_settings)
        *   [2.3.1 Font substitutions](#Font_substitutions)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Spotify](#Spotify)
    *   [3.2 Google Chrome](#Google_Chrome)
    *   [3.3 Emacs](#Emacs)
    *   [3.4 GIMP](#GIMP)
    *   [3.5 Language specifics diacritics / glyphs](#Language_specifics_diacritics_.2F_glyphs)
    *   [3.6 Firefox/Chrome browsers rendering monospaced with proportional font](#Firefox.2FChrome_browsers_rendering_monospaced_with_proportional_font)
    *   [3.7 CJK character distortion](#CJK_character_distortion)
    *   [3.8 General problems with fonts](#General_problems_with_fonts)
*   [4 See also](#See_also)

## 安装

**Warning:** 上游 infinality 补丁为早于2.4x的freetype2使用的。建议用户使用*Bohoomil*的[infinality-bundle](#Infinality-bundle)。

### Infinality-bundle

**Infinality-bundle** 是一个在Arch Linux 下由 Bohoomil 打包的旨在改善文字显示的软件合集。

目前，**Infinality-bundle** 包括：

*   *freetype2-infinality-ultimate* – 使用 [freetype2](https://www.archlinux.org/packages/?name=freetype2) 的构建的含额外补丁的 [Infinality](http://www.infinality.net/blog/)。
*   *fontconfig-infinality-ultimate* – [fontconfig](https://www.archlinux.org/packages/?name=fontconfig) 使用 *freetype2-infinality-ultimate* 优化显示，其中包括独立预设配置：自由（默认）、微软和自定义字体集合。更改列表详见 [更改日志](https://github.com/bohoomil/fontconfig-ultimate/blob/master/fontconfig_patches/CHANGELOG)。
*   *cairo-infinality-ultimate* – 使用Ubuntu来构建的含额外补丁的[cairo](https://www.archlinux.org/packages/?name=cairo)
*   *jdk8-openjdk-infinality* – 使用 infinality 补丁的[jdk8-openjdk](https://www.archlinux.org/packages/?name=jdk8-openjdk)。

附加源 *infinality-bundle-fonts* 提供一个用于创建和再现超文本文件所需的字体的可供选择的仓库。所有字体根据GPL、OFL、兼容 Apache 和非限制性许可证授权完全免费提供。

默认情况下不需要额外的配置。要自定义设置，请参阅[#Configuration](#Configuration)。

安装包括向 `pacman.conf` 添加所选源和 [安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 相关组或安装包两步。在安装后，记得重新启动 X server 以便看生效。

*   The [infinality-bundle](/index.php/Unofficial_user_repositories#infinality-bundle "Unofficial user repositories") 源包含的核心包，构成 *infinality-bundle* 组。
*   The [infinality-bundle-multilib](/index.php/Unofficial_user_repositories#infinality-bundle-multilib "Unofficial user repositories") 源包含x86_64架构可选 multilib 库，构成 *infinality-bundle-multilib* 组。
*   The [infinality-bundle-fonts](/index.php/Unofficial_user_repositories#infinality-bundle-fonts "Unofficial user repositories") 源包含广泛收集的免费字体，构成*ibfonts-meta-base*, *ibfonts-meta-extended* and *ibfonts-meta-extended-lt* 安装包。

**Note:**

*   不要忘记向pacman密钥环导入密钥 **962DDE58**。详细介绍详见 [Pacman-key (简体中文)#.E5.AF.BC.E5.85.A5.E9.9D.9E.E5.AE.98.E6.96.B9.E5.AF.86.E9.92.A5](/index.php/Pacman-key_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.AF.BC.E5.85.A5.E9.9D.9E.E5.AE.98.E6.96.B9.E5.AF.86.E9.92.A5 "Pacman-key (简体中文)")。
*   当pacman解决软件包依赖和冲突时，例如：
    ```
    resolving dependencies...
    looking for inter-conflicts...
    :: freetype2-infinality-ultimate and freetype2 are in conflict. Remove freetype2? [y/N]

    ```
    回答 `y`.

#### 附加字体

如果想要安装更多字体，还有一个额外字体集合 *infinality-bundle-fonts-extra* 。运行

```
$ pacman -Ss infinality-bundle-fonts-extra

```

列出可用的安装包。

**Warning:** **不要**尝试安装 *infinality-bundle-fonts* 组或者 *infinality-bundle-fonts-extra* 组的全部包。除非你确信你需要有可用的字体在其中，否则你只会无缘无故地塞满你的硬盘以及降低字体缓存性能。*ibfonts-meta-extended* 大多数情况下甚至复杂的应用场景应该是够用的。此外，一些字体家族有多种字体格式（T1、TTF、OTF）可供选择。尝试安装所有的字体包可能会导致无法解决安装包的冲突。如果是这种情况，你应该坚持每个字体家族只使用一种字体格式。

**Tip:** 从 [official repositories (简体中文)](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)") 或 [AUR](/index.php/AUR "AUR") 安装第三方字体之前，应该检查该字体是否包含在 *infinality-bundle-fonts* 里。

**Note:** 当**报告错误**时，所有与代码相关的问题（如不正确渲染、fontconfig 的问题等）请在GitHub [Issues * bohoomil/fontconfig-ultimate](https://github.com/bohoomil/fontconfig-ultimate/issues) 上提交，其他具体问题（包括有关维护、打包和一般性问题）请在Arch论坛反应。提交报告之前，请确保正确安装或定制 [infinality-bundle]。

### AUR

As of 2016-04, the following AUR packages containing (mainly Bohoomil's) Infinality patches are available:

*   [freetype2-infinality](https://aur.archlinux.org/packages/freetype2-infinality/)
*   [fontconfig-infinality](https://aur.archlinux.org/packages/fontconfig-infinality/)
*   [cairo-infinality](https://aur.archlinux.org/packages/cairo-infinality/)
*   [jdk8-openjdk-infinality](https://aur.archlinux.org/packages/jdk8-openjdk-infinality/)
    *   In [jdk7-openjdk-infinality](https://aur.archlinux.org/packages/jdk7-openjdk-infinality/) (IcedTea JDK7), the Infinality patch is already included, so all the maintainer did was setting <tt>--enable-infinality=yes</tt>.

Although these packages are using the same source of patches as Bohoomil's repo does, they often target a specific commit in Bohoomil's repo and can be lagging behind. The packagers may also have their own ideas on what patches to apply.

Besides [freetype2-infinality](https://aur.archlinux.org/packages/freetype2-infinality/), it is recommended to also install [fontconfig-infinality](https://aur.archlinux.org/packages/fontconfig-infinality/) to enable selection of predefined font substitution styles and antialiasing settings, apart from the rendering settings of the engine itself.

## Configuration

### Fonts with restricted licenses

Below you will find a list of fonts that cannot be freely redistributed and thus could not be included in the *infinality-bundle-fonts* collection as binary packages. However, they can still be installed and used free of charge under specified conditions. Source packages can be found in the [AUR](/index.php/AUR "AUR"). Please, read the EULAs for details before you use the fonts!

*   [ttf-brill](https://aur.archlinux.org/packages/ttf-brill/)
*   [otf-neris](https://aur.archlinux.org/packages/otf-neris/)
*   [ttf-aller](https://aur.archlinux.org/packages/ttf-aller/)
*   [ttf-envy-code-r](https://aur.archlinux.org/packages/ttf-envy-code-r/)

### Xft and FreeType settings

Settings should duplicate those found in the [Xft](/index.php/Font_configuration#Applications_without_fontconfig_support "Font configuration") configuration file (`/etc/X11/xinit/xinitrc.d/xft-settings.sh`):

```
Xft.antialias: 1
Xft.autohint: 0
Xft.dpi: 96
Xft.hinting: 1
Xft.hintstyle: hintfull
Xft.lcdfilter: lcddefault
Xft.rgba: rgb

```

Aside from these values you can modify `INFINALITY_FT` [environment variables](/index.php/Environment_variable "Environment variable"). For example:

```
# Makes fonts darker and thicker
export INFINALITY_FT_BRIGHTNESS="-10"

# Not too sharp, not too smooth
export INFINALITY_FT_FILTER_PARAMS="16 20 28 20 16"

```

**Note:** Customisations will be saved in a `.pacsave` file on an update of the infinality package.

### Fontconfig settings

Infinality-patched [fontconfig](/index.php/Fontconfig "Fontconfig") provides a different set of example/avail and default configurations. There are also multiple presets available. Run `fc-presets help` for more information.

For example, it is possible to skip installation of *infinality-bundle-fonts* if you want to use Microsoft proprietary font collection instead. If this is the case, you have to activate fontconfig MS preset to ensure the correct set of fonts is selected. To do so, issue

 `# fc-presets set` 
```
1) combi
2) free
3) ms
4) reset
5) quit
Enter your choice...

```

and select `3`.

If you would rather use a custom font collection, there is a `combi` preset available that should let you adjust fontconfig parameters accordingly. When you activate the `combi` preset, the content of 'custom' configuration files (`/etc/fonts/conf.avail.infinality/combi`) can be freely modified. When you are done, do not forget to create a backup copy of the 'combi' directory.

**Note:**

*   Install [grip-git](https://aur.archlinux.org/packages/grip-git/) from the AUR to have a realtime font preview.
*   The `README` for [fontconfig-infinality](https://aur.archlinux.org/packages/fontconfig-infinality/) says that `/etc/fonts/local.conf` should either not exist, or have no infinality-related configurations in it. The `local.conf` is now obsolete and completely replaced by this configuration.

#### Font substitutions

To override default font substitutions set in `/etc/fonts/conf.d/37-repl-global-*preset*.conf` or add new ones, use `/etc/fonts/conf.d/35-repl-custom.conf` to do so. You will need to duplicate the template (16 lines of code) for each font family to be replaced and provide appropriate font names.

## Troubleshooting

See also [Font configuration#Troubleshooting](/index.php/Font_configuration#Troubleshooting "Font configuration").

### Spotify

When experiencing font rendering issues with Spotify [[1]](http://i.imgur.com/E51vt2b.jpg), try the following font settings:

```
USE_STYLE="2"
export INFINALITY_FT_FRINGE_FILTER_STRENGTH="50"
export INFINALITY_FT_USE_VARIOUS_TWEAKS="true"
export INFINALITY_FT_CHROMEOS_STYLE_SHARPENING_STRENGTH="20"
export INFINALITY_FT_GAMMA_CORRECTION="30 80"
export INFINALITY_FT_STEM_ALIGNMENT_STRENGTH="25"
export INFINALITY_FT_STEM_FITTING_STRENGTH="25"

```

### Google Chrome

To solve rendering issues in Google Chrome [[2]](https://bbs.archlinux.org/viewtopic.php?pid=1344172#p1344172), edit `/etc/fonts/fonts.conf` file and uncomment the following entry:

```
<!--match target="pattern">
<edit name="dpi" mode="assign">
<double>72</double>
</edit>
</match-->
```

### Emacs

Emacs users have reported issues with Noto Sans as the default sans-serif font. This will affect any font face that specifies "Sans Serif" as the font family including the variable-pitch face that is used in Emacs Info mode.

Noto Sans is a collection of many individual language specific font files. Emacs does not find the correct version when it tries to render the font and displays glyphs instead.

To get around the issue you need to either specify a different default Sans Serif font for all applications or modify the font family for any faces that specify "Sans Serif" within Emacs.

To change the default font for all applications place the following:

```
  <alias>
    <family>sans-serif</family>
    <prefer>
      <family>Liberation Sans</family>
    </prefer>
  </alias>

```

in either `/etc/fonts/conf.avail.infinality/35-repl-custom.conf` for global effect or `$XDG_CONFIG_HOME/fontconfig/fonts.conf` or `$XDG_CONFIG_HOME/fontconfig/conf.d/60-latin.conf` for a single user. For `combi` users, `60-latin-combi.conf` should be modified accordingly.

The default font can be any but Noto Sans.

To change the font in Emacs only:

If you prefer Noto Sans for other applications and just want to fix Emacs specifically then you can specify a new Font Family for the variable pitch face. This could be done via customize (M-x customize-face RET variable-pitch RET) or by placing the following code in `$HOME/.emacs` or `$HOME/emacs.d/init.el`.

```
(custom-set-faces
  '(variable-pitch ((t (:family "Liberation Sans")))))

```

Note that there may be other faces either in default Emacs or specified by themes that also use the default Sans Serif font and would have to be modified in the same way. Changing the system wide default to something like Liberation Sans is therefore a more universal fix.

### GIMP

GIMP users have reported issues with the subpixel rendering of text in images (see for example [this topic](http://www.infinality.net/forum/viewtopic.php?f=2&t=229)). The best course of action is to disable subpixel rendering completely for GIMP. Add a file `/etc/gimp/2.0/fonts.conf` (or `~/.gimp-2.8/fonts.conf` for a single user) with the following content:

 `/etc/gimp/2.0/fonts.conf` 
```
<fontconfig>
  <match target="font">
    <edit name="rgba" mode="assign">
      <const>none</const>
    </edit>
  </match>
</fontconfig>

```

### Language specifics diacritics / glyphs

Some language specifics diacritics / glyphs are displayed inconsistently using default font.

This is usually the case with websites (notably blogs) utilizing predefined CSS templates that make use of web fonts missing support for extended Latin scripts (most often A and B). Even though this is not a problem with any of the infinality-bundle components and thus should be fixed by the author / maintainer of the problematic site, it can still be got round by creating a relevant font replacement rule in fontconfig. If you want to use this option, activate `36-repl-missing-glyphs.conf` first:

```
$ cd /etc/fonts/conf.d
$ ln -s ../conf.avail.infinality/36-repl-missing-glyphs.conf .

```

and then edit the file accordingly following the provided example.

**Note:** Default fonts for non-Latin scripts are set in `65-non-latin-*preset*.conf` (default settings).

Overriding default replacement rules and adding custom ones is possible with `35-repl-custom.conf`. The file is activated by default, so all you need to do is edit if you want to use it.

### Firefox/Chrome browsers rendering monospaced with proportional font

You can check which font the browser is using with the `fc-match` tool. If for `"monospace"` you get a proportional font like Arial

```
# fc-match "monospace"
monospace: arial.ttf: "Arial" "Normal"

```

you probably should run

```
 # fc-presets set

```

### CJK character distortion

Some CJK characters like "的" "照" "吧" are likely to deform under certain sizes[[3]](https://github.com/bohoomil/fontconfig-ultimate/issues/182). Disabling certain aspects of the autohinter can help:

```
export INFINALITY_FT_STEM_ALIGNMENT_STRENGTH=0
export INFINALITY_FT_STEM_FITTING_STRENGTH=0
export INFINALITY_FT_STEM_SNAPPING_SLIDING_SCALE=0
export INFINALITY_FT_AUTOHINT_SNAP_STEM_HEIGHT=0
export INFINALITY_FT_AUTOHINT_HORIZONTAL_STEM_DARKEN_STRENGTH=0
export INFINALITY_FT_AUTOHINT_INCREASE_GLYPH_HEIGHTS=false

```

### General problems with fonts

If you experience general problems with fonts (e.g. certain glyphs are not loaded in PDF documents, while a font family providing them has been correctly installed), start troubleshooting by issuing

```
# fc-cache -fr

```

This will remove the entire font cache and recreate it from scratch.

## See also

*   [Short article about infinality (contains screenshots)](http://www.webupd8.org/2013/06/better-font-rendering-in-linux-with.html)
*   [Infinality bundle and fonts](http://bohoomil.com) - Home page of the infinality bundle
*   [fontconfig-ultimate](https://github.com/bohoomil/fontconfig-ultimate) - git repository providing all patches, configuration files and build scripts for the entire *infinality-bundle+fonts* collection in separate branches
*   [infinality-bundle: good looking fonts made (even) easier](https://bbs.archlinux.org/viewtopic.php?id=162098) - *infinality-bundle* support thread in the Arch Linux Forums
*   [infinality-bundle-fonts: a free multilingual font collection for Arch](https://bbs.archlinux.org/viewtopic.php?id=170976) - *infinality-bundle-fonts* support thread in the Arch Linux Forums