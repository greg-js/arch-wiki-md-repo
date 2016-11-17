**Warning:** surf is based on a WebKit port that is today considered insecure and outdated. It's recommended to use [another browser](/index.php/List_of_applications/Internet#Web_browsers "List of applications/Internet") instead. More info [here](https://blogs.gnome.org/mcatanzaro/2016/02/01/on-webkit-security-updates/).

[surf](http://surf.suckless.org/) is a simple web browser based on WebKit/GTK+. It is able to display websites and follow links. It supports the XEmbed protocol which makes it possible to embed it in another application. Furthermore, one can point surf to another URI by setting its XProperties.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Extended usage](#Extended_usage)
    *   [3.1 Patches & additional features](#Patches_.26_additional_features)
    *   [3.2 Tabbed browsing](#Tabbed_browsing)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Fuzzy font in Github](#Fuzzy_font_in_Github)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [surf](https://www.archlinux.org/packages/?name=surf) package. Alternatively, there is the [surf-git](https://aur.archlinux.org/packages/surf-git/) package for the development version.

Optionally also install the [dmenu](https://www.archlinux.org/packages/?name=dmenu) package for URL-bar

## Configuration

surf is configured through its `config.h` file. A sample `config.def.h` file is included with the source and should be instructive.

As with other packages such as [dwm](/index.php/Dwm "Dwm"), consider using the Arch Build System ([ABS](/index.php/ABS "ABS")) and maintaining your own [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") with sources and md5sums for your own configuration and source files.

## Extended usage

### Patches & additional features

There are many user-created [patches](http://surf.suckless.org/patches/) available from the offical site that greatly extend the functionality of surf. Patches can be applied to both the source `surf.c` file and the `config.h` file:

```
$ cd src/surf-[version]/
$ patch -p1 < path/to/patch.diff

```

### Tabbed browsing

The [tabbed](https://www.archlinux.org/packages/?name=tabbed) program can be used with surf to create a simple tabbed browsing experience.

A basic set-up:

```
$ tabbed surf -e

```

Note that to achieve a similar effect to Firefox or Chromium where upon closing the last tab, the browser exits, use instead:

```
$ tabbed -c surf -e

```

See the man page for tabbed for more details and possibilities.

## Troubleshooting

### Fuzzy font in Github

Install [ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont) or add this in your `~/.config/fontconfig/fonts.conf` inside the fontconfig-tags:

```
 <selectfont>
   <rejectfont>
     <pattern>
       <patelt name="family">
         <string>Clean</string>
       </patelt>
     </pattern>
   </rejectfont>
 </selectfont>

```

## See also

*   [surf's official website](http://surf.suckless.org/)
*   [dmenu](/index.php/Dmenu "Dmenu") - Simple application launcher from the developers of dwm
*   [Hacking surf thread](https://bbs.archlinux.org/viewtopic.php?id=167804/)