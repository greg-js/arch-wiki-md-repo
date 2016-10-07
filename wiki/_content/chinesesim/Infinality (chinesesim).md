**翻译状态：** 本文是英文页面 [Infinality](/index.php/Infinality "Infinality") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-09-22，点击[这里](https://wiki.archlinux.org/index.php?title=Infinality&diff=0&oldid=451547)可以查看翻译后英文页面的改动。

[infinality](http://www.infinality.net/)补丁集可以显著改善 freetype2 字体渲染。另外也新增了一些新功能。

Infinality 可以通过修改环境变量来启用一些功能：

*   **加粗增强 (Emboldening Enhancement)**：禁用Y加粗可以（使用原生 TrueType 微调器或者自动微调器）使得没有加粗版本的字体的显示得以改善。
*   **自动微调 (Auto-Autohint)**：强制那些不含 TrueType 信息的字体使用自动微调。
*   **自动微调增强 (Autohint Enhancement)**：自动微调使得水平字符主干微移 (snap horizontal stems) 对齐像素。看起来就像精心微调 TrueType 的字体一样。
*   **自定义有限冲激响应滤波器 (Customized FIR Filter)**：运行时（使用原生 TrueType 微调器或者自动微调器）选择[过滤器的值](http://www.infinality.net/forum/viewtopic.php?f=2&t=19) 。
*   **字符主干对齐 (Stem Alignment)**：根据字符的像素边界优化调整。适用于原生 TrueType 微调器或者自动微调器。
*   **伪伽玛校正 (Pseudo Gamma Correction)**：（使用原生 TrueType 微调器或者自动微调器）亮化和暗化给定大小的字形达到规定的值。
*   **加粗细体字体 (Embolden Thin Fonts)**：加粗细体字体，使得他们更加好看（自动微调）。
*   **强制微少微调 (Force Slight Hinting)**：强制微少微调甚至程序希望饱和微调。
*   **ChromeOS 锐化 (ChromeOS Style Sharpening)**: ChromeOS 所使用的锐化字体渲染的补丁现在包含在当infinality补丁集里。

具体详见 [README](http://www.infinality.net/forum/viewtopic.php?f=2&t=18)。

Infinality 内置了一些预设置，可以通过在 `/etc/X11/xinit/xinitrc.d/xft-settings.sh` 设置 USE_STYLE 环境变量来使用。

Infinality 的环境变量应该在 `/etc/profile.d/infinality-settings.sh` 里进行设置。模板详见 [infinality-settings.sh](https://github.com/bohoomil/fontconfig-ultimate/blob/master/freetype/infinality-settings.sh)。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 Infinality-bundle](#Infinality-bundle)
        *   [1.1.1 附加字体](#.E9.99.84.E5.8A.A0.E5.AD.97.E4.BD.93)
    *   [1.2 AUR](#AUR)
*   [2 设置](#.E8.AE.BE.E7.BD.AE)
    *   [2.1 许可限制字体](#.E8.AE.B8.E5.8F.AF.E9.99.90.E5.88.B6.E5.AD.97.E4.BD.93)
    *   [2.2 Xft 和 FreeType 设置](#Xft_.E5.92.8C_FreeType_.E8.AE.BE.E7.BD.AE)
    *   [2.3 Fontconfig 设置](#Fontconfig_.E8.AE.BE.E7.BD.AE)
        *   [2.3.1 字体替换](#.E5.AD.97.E4.BD.93.E6.9B.BF.E6.8D.A2)
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

**Warning:** 上游 infinality 补丁为早于 2.4x 的 freetype2 使用的。建议用户使用*Bohoomil*的[infinality-bundle](#Infinality-bundle)。

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

*   不要忘记向pacman密钥环导入密钥 **962DDE58**。详细介绍详见 [导入非官方密钥](/index.php/Pacman-key_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.AF.BC.E5.85.A5.E9.9D.9E.E5.AE.98.E6.96.B9.E5.AF.86.E9.92.A5 "Pacman-key (简体中文)")。
*   当pacman解决软件包依赖和冲突时，例如：
    ```
    resolving dependencies...
    looking for inter-conflicts...
    :: freetype2-infinality-ultimate and freetype2 are in conflict. Remove freetype2? [y/N]

    ```
    回答 `y`.

#### 附加字体

如果想要安装更多字体，还有一个额外字体集合 *infinality-bundle-fonts-extra* 可供安装。运行

```
$ pacman -Ss infinality-bundle-fonts-extra

```

可以列出所有可用的字体包。

**Warning:** **不要**尝试安装 *infinality-bundle-fonts* 组或者 *infinality-bundle-fonts-extra* 组的全部包。除非你确信你需要有可用的字体在其中，否则你只会无缘无故地塞满你的硬盘以及降低字体缓存性能。*ibfonts-meta-extended* 大多数情况下甚至复杂的应用场景应该是够用的。此外，一些字体家族有多种字体格式（T1、TTF、OTF）可供选择。尝试安装所有的字体包可能会导致无法解决安装包的冲突。如果是这种情况，你应该坚持每个字体家族只使用一种字体格式。

**Tip:** 从 [官方源](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)") 或 [AUR](/index.php/AUR "AUR") 安装第三方字体之前，应该检查该字体是否包含在 *infinality-bundle-fonts* 里。

**Note:** 当**报告错误**时，所有与代码相关的问题（如不正确渲染、fontconfig 的问题等）请在GitHub [Issues * bohoomil/fontconfig-ultimate](https://github.com/bohoomil/fontconfig-ultimate/issues) 上提交，其他具体问题（包括有关维护、打包和一般性问题）请在Arch论坛反应。提交报告之前，请确保正确安装或定制 [infinality-bundle]。

### AUR

截至 2016年04月，以下是可用的包含 （大部分是 Bohoomil 的）Infinality 补丁的 AUR 包：

*   [freetype2-infinality](https://aur.archlinux.org/packages/freetype2-infinality/)
*   [fontconfig-infinality](https://aur.archlinux.org/packages/fontconfig-infinality/)
*   [cairo-infinality](https://aur.archlinux.org/packages/cairo-infinality/)
*   [jdk8-openjdk-infinality](https://aur.archlinux.org/packages/jdk8-openjdk-infinality/)
    *   [jdk7-openjdk-infinality](https://aur.archlinux.org/packages/jdk7-openjdk-infinality/) (IcedTea JDK7) 已经包含 Infinality 补丁，所以维护者只要设置 <tt>--enable-infinality=yes</tt> 即可。

虽然这些软件包是使用和 Bohoomil 库相同的补丁源码，但是他们通常以 Bohoomil 库中的一个具体的提交，所以可能有些延迟。打包者对于打什么补丁可能有自己的想法。

除了 [freetype2-infinality](https://aur.archlinux.org/packages/freetype2-infinality/) 以外，建议同时安装 [fontconfig-infinality](https://aur.archlinux.org/packages/fontconfig-infinality/)，使得除了系统渲染引擎的设置以外的预定义字体替换样式和抗锯齿的设置能够启用。

## 设置

### 许可限制字体

你会发现下列字体是不能自由分发的，所以这些字体并不在 *infinality-bundle-fonts* 的字体包里。但是，它们仍然可以在指定的条件下免费安装和使用。源包可以在[AUR](/index.php/AUR "AUR")中找到。在使用的这些字体之前，请认真阅读**最终用户许可协议**！

*   [ttf-brill](https://aur.archlinux.org/packages/ttf-brill/)
*   [otf-neris](https://aur.archlinux.org/packages/otf-neris/)
*   [ttf-aller](https://aur.archlinux.org/packages/ttf-aller/)
*   [ttf-envy-code-r](https://aur.archlinux.org/packages/ttf-envy-code-r/)

### Xft 和 FreeType 设置

[Xft](/index.php/Font_configuration#Applications_without_fontconfig_support "Font configuration") 的配置文件 (`/etc/X11/xinit/xinitrc.d/xft-settings.sh`) 不应该重复设置：

```
Xft.antialias: 1
Xft.autohint: 0
Xft.dpi: 96
Xft.hinting: 1
Xft.hintstyle: hintfull
Xft.lcdfilter: lcddefault
Xft.rgba: rgb

```

除了上述这些值以外，你可以修改 `INFINALITY_FT` [环境变量](/index.php/Environment_variables_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Environment variables (简体中文)")。 例如：

```
# 使字体更粗或者更细
export INFINALITY_FT_BRIGHTNESS="-10"

# 不要太锐利，也不要太平滑
export INFINALITY_FT_FILTER_PARAMS="16 20 28 20 16"

```

**Note:** 在升级 infinality 包过后，自定义设置 将被保存在 `.pacsave` 文件中。

### Fontconfig 设置

Infinality 补丁 [fontconfig](/index.php/Fontconfig "Fontconfig") 提供一组不同的示例配置和一个默认配置。 [fontconfig](/index.php/Fontconfig "Fontconfig") 提供多种预设配置，运行 `fc-presets help` 以获取更多信息。

譬如，如果你想使用微软专有字体集，可以不安装 *infinality-bundle-fonts* ，但是必须选择 fontconfig 的 ms 预设配置保证正确的字体集被选中，执行

 `# fc-presets set` 
```
1) combi
2) free
3) ms
4) reset
5) quit
Enter your choice...

```

然后选择 `3`。

如果你希望使用自定义字体集合，`combi` 预设配置可让你调整相应的 fontconfig 参数。当选择 `combi` 预设配置时，combi 配置文件(`/etc/fonts/conf.avail.infinality/combi`) 的内容可以随意修改。当完成修改之后，不要忘记创建 combi 目录的备份。

**Note:**

*   Install [grip-git](https://aur.archlinux.org/packages/grip-git/) from the AUR to have a realtime font preview.
*   The `README` for [fontconfig-infinality](https://aur.archlinux.org/packages/fontconfig-infinality/) says that `/etc/fonts/local.conf` should either not exist, or have no infinality-related configurations in it. The `local.conf` is now obsolete and completely replaced by this configuration.

#### 字体替换

想要覆盖在 `/etc/fonts/conf.d/37-repl-global-*preset*.conf` 中设置的默认字体替换，或者想要添加新的字体替换，请使用 `/etc/fonts/conf.d/35-repl-custom.conf` 。你需要复制每个字体家族模板（16行代码），在此基础上进行更换为适当的字体名称。

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