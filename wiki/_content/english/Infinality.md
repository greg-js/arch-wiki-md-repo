The [infinality](http://www.infinality.net/) patchset aims to greatly improve freetype2 font rendering. It adds multiple new capabilities.

## Contents

*   [1 Features](#Features)
*   [2 Installation](#Installation)
    *   [2.1 Infinality-bundle](#Infinality-bundle)
        *   [2.1.1 Installation](#Installation_2)
        *   [2.1.2 Recommended fonts with restricted licenses](#Recommended_fonts_with_restricted_licenses)
        *   [2.1.3 Usage](#Usage)
        *   [2.1.4 More fonts](#More_fonts)
        *   [2.1.5 Font substitutions](#Font_substitutions)
        *   [2.1.6 Package signatures](#Package_signatures)
        *   [2.1.7 Updating](#Updating)
    *   [2.2 Upstream infinality](#Upstream_infinality)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Spotify font issue](#Spotify_font_issue)
    *   [3.2 Google Chrome issues](#Google_Chrome_issues)
    *   [3.3 Emacs issues](#Emacs_issues)
    *   [3.4 GIMP issues](#GIMP_issues)
    *   [3.5 Language specifics diacritics / glyphs](#Language_specifics_diacritics_.2F_glyphs)
    *   [3.6 Firefox/Chrome browsers rendering monospaced with proportional font](#Firefox.2FChrome_browsers_rendering_monospaced_with_proportional_font)
    *   [3.7 General problems with fonts](#General_problems_with_fonts)
*   [4 See also](#See_also)

## Features

Infinality's settings are all configurable at runtime via environment variables in `/etc/X11/xinit/xinitrc.d/xft-settings.sh`, and include the following:

*   **Emboldening Enhancement**: Disables Y emboldening, producing a much nicer result on fonts without bold versions. Works on native TT hinter and autohinter.
*   **Auto-Autohint**: Automatically forces autohint on fonts that contain no TT instructions.
*   **Autohint Enhancement**: Makes autohint snap horizontal stems to pixels. Gives a result that appears like a well-hinted truetype font, but is 100% patent-free (as far as I know).
*   **Customized FIR Filter**: Select your own [filter values](http://www.infinality.net/forum/viewtopic.php?f=2&t=19) at run-time. Works on native TT hinter and autohinter.
*   **Stem Alignment**: Aligns bitmap glyphs to optimized pixel boundaries. Works on native TT hinter and autohinter.
*   **Pseudo Gamma Correction**: Lighten and darken glyphs at a given value, below a given size. Works on native TT hinter and autohinter.
*   **Embolden Thin Fonts**: Embolden thin or light fonts so that they are more visible. Works on autohinter.
*   **Force Slight Hinting**: Force slight hinting even when programs want full hinting. If you use the local.conf I provide (included in infinality-settings fedora package) you will notice nice improvements on @font-face fonts.
*   **ChromeOS Style Sharpening**: ChromeOS uses a patch to sharpen the look of fonts. This is now included in the infinality patchset.

See the [README](http://www.infinality.net/forum/viewtopic.php?f=2&t=18) for details.

A number of presets are included and can be used by setting the USE_STYLE variable in `/etc/X11/xinit/xinitrc.d/xft-settings.sh`.

## Installation

### Infinality-bundle

**Infinality-bundle** is a collection of software aiming to improve text rendering in Arch Linux.

Currently, the bundle comprises:

*   *freetype2-infinality-ultimate* - [freetype2](https://www.archlinux.org/packages/?name=freetype2) built with [Infinality](http://www.infinality.net/blog/) and additional patches.
*   *fontconfig-infinality-ultimate* - [fontconfig](https://www.archlinux.org/packages/?name=fontconfig) optimized for use with *freetype2-infinality-ultimate*, including separate configuration presets for free (default), MS and custom font collections.
*   *cairo-infinality-ultimate* - [cairo](https://www.archlinux.org/packages/?name=cairo) built with Ubuntu and additional patches.

All libraries are built in a clean chroot environment and are available for both i686 and x86_64 architectures, including multilib support.

For best results and users' convenience, a complementary repository *infinality-bundle-fonts* is available, offering a wide selection of all necessary typefaces needed to create and reproduce hypertext documents. All fonts were manually selected, ensuring high quality text rendering as well as compatibility with proprietary equivalents used for the Web and the office. All fonts are 100% freely available and are licensed under GPL, OFL, Apache or compatible, non-restrictive licenses.

By default, no post installation configuration is required. However, for maximum flexibility users can easily customize the bundle depending on their needs.

#### Installation

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

#### Recommended fonts with restricted licenses

Below you will find a list of fonts that cannot be freely redistributed and thus could not be included in the *infinality-bundle-fonts* collection as binary packages. However, they can still be installed and used free of charge under specified conditions. Source packages can be found in the [AUR](/index.php/AUR "AUR"). Please, read the EULAs for details before you use the fonts!

*   [ttf-brill](https://aur.archlinux.org/packages/ttf-brill/)
*   [otf-neris](https://aur.archlinux.org/packages/otf-neris/)
*   [ttf-aller](https://aur.archlinux.org/packages/ttf-aller/)
*   [ttf-envy-code-r](https://aur.archlinux.org/packages/ttf-envy-code-r/)

#### Usage

Users of popular Desktop Environments (GNOME, KDE, Xfce4, Cinnamon, LXDE) should adjust font settings via their DE's control panel. Basically, the settings should duplicate those found in the freetype2 configuration file (`/etc/X11/xinit/xinitrc.d/xft-settings.sh`):

```
Xft.antialias: 1
Xft.autohint: 0
Xft.dpi: 96
Xft.hinting: 1
Xft.hintstyle: hintfull
Xft.lcdfilter: lcddefault
Xft.rgba: rgb

```

If your DE's control panel does not let you set any of the above, adjust only those available. Aside these values you can customise all `INFINALITY_FT` variables. Example:

```
# Makes fonts darker and thicker
export INFINALITY_FT_BRIGHTNESS="-10"

# Not too sharp, not too smooth
export INFINALITY_FT_FILTER_PARAMS="16 20 28 20 16"

```

**Note:** Your customisations will be saved in a `.pacsave` file on an update of the infinality package.

*   It is possible to skip installation of *infinality-bundle-fonts* if you want to use Microsoft proprietary font collection instead. If this is the case, you have to activate fontconfig MS preset to ensure the correct set of fonts is selected. To do so, issue

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

Run `fc-presets help` for more information.

*   If you would rather use a custom font collection, there is a `combi` preset available that should let you adjust fontconfig parameters accordingly. When you activate the `combi` preset, the content of 'custom' configuration files (`/etc/fonts/conf.avail.infinality/combi`) can be freely modified. When you are done, do not forget to create a backup copy of the 'combi' directory.

#### More fonts

If you want to install even more fonts, there is an additional *infinality-bundle-fonts-extra* collection. Run

```
$ pacman -Ss infinality-bundle-fonts-extra

```

to list available packages.

**Warning:** **Do not** attempt to install the entire *infinality-bundle-fonts* or *infinality-bundle-fonts-extra* group. Unless you know for sure you need any of the fonts available there, you will only unnecessarily clutter your hard drive and decrease performance of the font cache. *ibfonts-meta-extended* should suffice in most, even very complex, use scenarios. Besides, several font families are available in multiple formats (T1, TTF, OTF): trying to install all font packages will lead to unresolvable package conflicts. If this is the case, you should always use only **one** format per family.

**Tip:** Before you install any third party font from either [official repositories](/index.php/Official_repositories "Official repositories") or the [AUR](/index.php/AUR "AUR"), always check if it is available in the *infinality-bundle-fonts* collection.

#### Font substitutions

If you want to override default font substitutions set in `/etc/fonts/conf.d/37-repl-global-*preset*.conf` or add new ones, use `/etc/fonts/conf.d/35-repl-custom.conf` to do so. You will need to duplicate the template (16 lines of code) for each font family to be replaced and provide appropriate font names.

#### Package signatures

One frequent issue users may face with this repositories is that the package database or signatures do not correspond. Often a simple force refresh of the package lists (`pacman -Syy`) will fix the issue. If that fails, try removing the infinality-bundle files from `/var/lib/pacman/sync` and then resyncing again.

#### Updating

*fontconfig-infinality-ultimate* is updated frequently, usually every 3-4 weeks, after a number of recently reported minor bugs has been fixed. As every fix is immediately committed to the GitHub repository, users who chose [fontconfig-infinality-ultimate-git](https://aur.archlinux.org/packages/fontconfig-infinality-ultimate-git/) from the AUR will get them sooner, i.e. when they rebuild the package.

**Note:**

*   *fontconfig-infinality-ultimate-git* is a development branch of the package available in the [infinality-bundle] repository. Keep in mind that it is not a stable release and can break at times.
*   When **reporting bugs**, please report all code-related issues (incorrect rendering, fontconfig problems, etc.) at GitHub [Issues * bohoomil/fontconfig-ultimate](https://github.com/bohoomil/fontconfig-ultimate/issues) and Arch specific, including problems regarding maintenance, packaging and general questions, in dedicated threads at Arch Forums. Before filing a report, make sure that [infinality-bundle] packages were correctly installed and customized.

### Upstream infinality

**Warning:** Upstream infinality patches are intended for the older 2.4x freetype2 branch. Users are advised to use the [infinality-bundle](#Infinality-bundle) by *bohoomil*.

[freetype2-infinality](https://aur.archlinux.org/packages/freetype2-infinality/) can be installed from the [AUR](/index.php/AUR "AUR"). If you are a multilib user, also install [lib32-freetype2-infinality](https://aur.archlinux.org/packages/lib32-freetype2-infinality/) from the AUR. The AUR also contains the latest development snapshot of freetype2 with the Infinality patchset: [freetype2-infinality-git](https://aur.archlinux.org/packages/freetype2-infinality-git/) and [lib32-freetype2-infinality-git](https://aur.archlinux.org/packages/lib32-freetype2-infinality-git/).

It is recommended to also install [fontconfig-infinality](https://aur.archlinux.org/packages/fontconfig-infinality/) to enable selection of predefined font substitution styles and antialiasing settings, apart from the rendering settings of the engine itself. After doing so, you can select the font style (win7, winxp, osx, linux, ...) with:

```
# fc-presets set

```

The corresponding fonts need to be installed.

**Note:**

*   Install [grip-git](https://aur.archlinux.org/packages/grip-git/) from the AUR to have a realtime font preview.
*   The `README` for [fontconfig-infinality](https://aur.archlinux.org/packages/fontconfig-infinality/) says that `/etc/fonts/local.conf` should either not exist, or have no infinality-related configurations in it. The `local.conf` is now obsolete and completely replaced by this configuration.

For more information see this forum post: [http://www.infinality.net/forum/viewtopic.php?f=2&t=77#p794](http://www.infinality.net/forum/viewtopic.php?f=2&t=77#p794)

## Troubleshooting

See also [Font configuration#Troubleshooting](/index.php/Font_configuration#Troubleshooting "Font configuration").

### Spotify font issue

If you experience font rendering issues with Spotify [[1](http://i.imgur.com/E51vt2b.jpg)], you might want to try the following font settings:

```
USE_STYLE="2"
export INFINALITY_FT_FRINGE_FILTER_STRENGTH="50"
export INFINALITY_FT_USE_VARIOUS_TWEAKS="true"
export INFINALITY_FT_CHROMEOS_STYLE_SHARPENING_STRENGTH="20"
export INFINALITY_FT_GAMMA_CORRECTION="30 80"
export INFINALITY_FT_STEM_ALIGNMENT_STRENGTH="25"
export INFINALITY_FT_STEM_FITTING_STRENGTH="25"

```

### Google Chrome issues

To solve rendering issues in Google Chrome browser described [in this post](https://bbs.archlinux.org/viewtopic.php?pid=1344172#p1344172), edit `/etc/fonts/fonts.conf` file and uncomment the following entry:

```
<!--match target="pattern">
<edit name="dpi" mode="assign">
<double>72</double>
</edit>
</match-->
```

### Emacs issues

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

### GIMP issues

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