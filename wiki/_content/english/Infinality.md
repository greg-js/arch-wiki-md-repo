The [infinality](http://www.infinality.net/) patchset aims to greatly improve font rendering in freetype2 and friends. It adds multiple new capabilities.

Infinality's settings are configurable at runtime via environment variables and include the following:

*   **Emboldening Enhancement**: Disables Y emboldening, which may improve results on fonts without bold versions (native TT hinter, autohinter).
*   **Auto-Autohint**: Automatically forces autohint on fonts that contain no TT instructions.
*   **Autohint Enhancement**: Makes autohint snap horizontal stems to pixels. Gives a result that appears like a well-hinted truetype font.
*   **Customized FIR Filter**: Select [filter values](http://www.infinality.net/forum/viewtopic.php?f=2&t=19) at run-time (native TT hinter, auto-hinter).
*   **Stem Alignment**: Aligns bitmap glyphs to pixel boundaries. Works on native TT hinter and autohinter.
*   **Pseudo Gamma Correction**: Lighten and darken glyphs at a given value, below a given size (native TT hinter, autohinter).
*   **Embolden Thin Fonts**: Embolden thin or light fonts so that they are more visible (autohinter).
*   **Force Slight Hinting**: Force slight hinting even when programs want full hinting.
*   **ChromeOS Style Sharpening**: ChromeOS uses a patch to sharpen the look of fonts. This is now included in the infinality patchset.

See the [README](http://www.infinality.net/forum/viewtopic.php?f=2&t=18) for details.

A number of presets are included and can be used by setting the USE_STYLE variable in `/etc/X11/xinit/xinitrc.d/xft-settings.sh`.

Variables should be set in `/etc/profile.d/infinality-settings.sh`. See [infinality-settings.sh](https://github.com/bohoomil/fontconfig-ultimate/blob/master/freetype/infinality-settings.sh) for a template.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Infinality-bundle](#Infinality-bundle)
        *   [1.1.1 Additional fonts](#Additional_fonts)
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

## Installation

**Warning:** Upstream infinality patches are intended for the older 2.4x freetype2 branch. Users are advised to use the [infinality-bundle](#Infinality-bundle) by *bohoomil*.

### Infinality-bundle

**Infinality-bundle** is a collection of software aiming to improve text rendering in Arch Linux by bohoomil.

Currently, the bundle comprises:

*   *freetype2-infinality-ultimate* – [freetype2](https://www.archlinux.org/packages/?name=freetype2) built with [Infinality](http://www.infinality.net/blog/) and additional patches.
*   *fontconfig-infinality-ultimate* – [fontconfig](https://www.archlinux.org/packages/?name=fontconfig) optimized for use with *freetype2-infinality-ultimate*, including separate configuration presets for free (default), MS and custom font collections. See [CHANGELOG](https://github.com/bohoomil/fontconfig-ultimate/blob/master/fontconfig_patches/CHANGELOG) for a list of changes.
*   *cairo-infinality-ultimate* – [cairo](https://www.archlinux.org/packages/?name=cairo) built with Ubuntu and additional patches.
*   *jdk8-openjdk-infinality* – [jdk8-openjdk](https://www.archlinux.org/packages/?name=jdk8-openjdk) with infinality patch applied.

A complementary repository *infinality-bundle-fonts* is available, offering a selection of typefaces needed to create and reproduce hypertext documents. All fonts are fully freely available and licensed under GPL, OFL, Apache or compatible, non-restrictive licenses.

By default, no additional configuration is required. To customize bundle settings, see [#Configuration](#Configuration).

The installation consists of adding the selected repositories to `pacman.conf` and [installing](/index.php/Installing "Installing") the packages from the relevant groups or meta packages. Remember to restart the X server after the installation to see the changes.

*   The [infinality-bundle](/index.php/Unofficial_user_repositories#infinality-bundle "Unofficial user repositories") repository contains core packages gathered into the *infinality-bundle* group.
*   The [infinality-bundle-multilib](/index.php/Unofficial_user_repositories#infinality-bundle-multilib "Unofficial user repositories") repository contains optional multilib libraries for the x86_64 architecture gathered in the *infinality-bundle-multilib* group.
*   The [infinality-bundle-fonts](/index.php/Unofficial_user_repositories#infinality-bundle-fonts "Unofficial user repositories") repository contains a comprehensive collection of free fonts gathered in the *ibfonts-meta-base*, *ibfonts-meta-extended* and *ibfonts-meta-extended-lt* meta packages.

**Note:**

*   Do not forget to add key ID 962DDE58 to your pacman keyring. See [Pacman-key#Adding unofficial keys](/index.php/Pacman-key#Adding_unofficial_keys "Pacman-key") to detailed instructions.
*   When pacman resolves dependencies and encounters a conflicting package, e.g.:
    ```
    resolving dependencies...
    looking for inter-conflicts...
    :: freetype2-infinality-ultimate and freetype2 are in conflict. Remove freetype2? [y/N]

    ```
    answer `yes`.

#### Additional fonts

If you want to install even more fonts, there is an additional *infinality-bundle-fonts-extra* collection. Run

```
$ pacman -Ss infinality-bundle-fonts-extra

```

to list available packages.

**Warning:** **Do not** attempt to install the entire *infinality-bundle-fonts* or *infinality-bundle-fonts-extra* group. Unless you know for sure you need any of the fonts available there, you will only unnecessarily clutter your hard drive and decrease performance of the font cache. *ibfonts-meta-extended* should suffice in most, even very complex, use scenarios. Besides, several font families are available in multiple formats (T1, TTF, OTF): trying to install all font packages will lead to unresolvable package conflicts. If this is the case, you should always use only **one** format per family.

**Tip:** Before you install any third party font from either [official repositories](/index.php/Official_repositories "Official repositories") or the [AUR](/index.php/AUR "AUR"), always check if it is available in the *infinality-bundle-fonts* collection.

**Note:** When **reporting bugs**, please report all code-related issues (incorrect rendering, fontconfig problems, etc.) at GitHub [Issues * bohoomil/fontconfig-ultimate](https://github.com/bohoomil/fontconfig-ultimate/issues) and Arch specific, including problems regarding maintenance, packaging and general questions, in dedicated threads at Arch Forums. Before filing a report, make sure that [infinality-bundle] packages were correctly installed and customized.

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

When experiencing font rendering issues with Spotify [[3]](http://i.imgur.com/E51vt2b.jpg), try the following font settings:

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

To solve rendering issues in Google Chrome [[4]](https://bbs.archlinux.org/viewtopic.php?pid=1344172#p1344172), edit `/etc/fonts/fonts.conf` file and uncomment the following entry:

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

Some CJK characters like "的" "照" "吧" are likely to deform under certain sizes[[5]](https://github.com/bohoomil/fontconfig-ultimate/issues/182). Disabling certain aspects of the autohinter can help:

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