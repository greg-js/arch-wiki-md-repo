Sawfish is a highly customizable [window manager](/index.php/Window_manager "Window manager"). Formerly it has been the standard Window manager of the GNOME desktop, but because of a change of maintainership this is no longer true. This article will show you how to install and configure it for standalone use (without GNOME).

## Contents

*   [1 Installation](#Installation)
*   [2 Starting Sawfish](#Starting_Sawfish)
*   [3 Customization](#Customization)
    *   [3.1 Themes](#Themes)
        *   [3.1.1 Adding new](#Adding_new)
    *   [3.2 Menus](#Menus)
        *   [3.2.1 Menu example](#Menu_example)
*   [4 Additional resources](#Additional_resources)

## Installation

Sawfish can be [installed](/index.php/Installed "Installed") with the [sawfish](https://aur.archlinux.org/packages/sawfish/) package.

## Starting Sawfish

If you use **startx**, just put

```
 exec sawfish

```

at the end of your `~/.xinitrc`. For other cases, see ... ?

## Customization

Out-of-the box Sawfish provides a menu accessible by clicking Mouse-2 (middle button) on the root window. From there, you can launch the customization app.

If you change any settings, they are stored in `~/.sawfish/custom`.

### Themes

You can select a window theme from the customization app. There is a small bug: if the theme is parametrizable, its configuration window will only appear after you restart the customization app.

#### Adding new

Create the directory `~/.sawfish/themes/` and drop there any theme files. You do not need to uncompress them. There are 500+ themes to choose from in the [Sawfish site](http://sawfish.wikia.com/wiki/Themes).

### Menus

Arch doesn't provide an automatic menu generator for Sawfish, but you can generate the menus using the XFCE4 ones. Here are the necessary steps:

Create the directory `~/.sawfish/lisp/`. This is where custom Sawfish scripts are stored; the menu will be one of them. Install [libxslt](https://www.archlinux.org/packages/?name=libxslt), copy the [xslt stylesheet example](#Menu_example), paste it into a file named `xfce4-menu-to-sawfish.xslt`. Now you need a XFCE4 menu. You may have one already or you can generate one with menumaker or xdg_menu.

*   If want to use [menumaker](https://www.archlinux.org/packages/?name=menumaker):

```
$ mmaker -c xfce4 | xsltproc xfce4-menu-to-sawfish.xslt - > ~/.sawfish/lisp/arch-menu.jl

```

*   If you want to use [archlinux-xdg-menu](https://www.archlinux.org/packages/?name=archlinux-xdg-menu):

```
$  xdg_menu --format xfce4 --root-menu /etc/xdg/menus/arch-applications.menu | xsltproc xfce4-menu-to-sawfish.xslt - > ~/.sawfish/lisp/arch-menu.jl

```

Now you have a script `~/.sawfish/lisp/arch-menu.jl` that defines a variable *arch-menu* with a list of your applications. You need to link to it from the root menu. You need to write the code for that to happen in `~/.sawfishrc`. So, start your favorite editor, create `~/.sawfishrc`, and type:

```
;;; sawfish configuration file
; 1\. Load defaults
(require 'sawfish-defaults)
; 2\. Load autogenerated arch-menu
(require 'arch-menu)
; 3\. Replace Sawfish's apps-menu with ours
(setq apps-menu arch-menu)

```

Restart Sawfish to effect the changes.

#### Menu example

 `xfce4-menu-to-sawfish.xslt` 
```
<?xml version="1.0" encoding="UTF-8" ?>
<xsl:stylesheet version="1.0"
                xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
  <xsl:output method="text"/>
  <xsl:strip-space elements="*"/>
  <xsl:param name="terminal">urxvt</xsl:param>
  <xsl:template name="indent">
    <xsl:text>
</xsl:text>
    <xsl:for-each select="ancestor-or-self::*">
      <xsl:text>  </xsl:text>
    </xsl:for-each>
  </xsl:template>
  <xsl:template match="/">
    <xsl:text>;;; Arch applications menu for Sawfish, generated from xfce4 menu
(defvar arch-menu nil)
(setq arch-menu '(</xsl:text>
    <xsl:apply-templates/>
    <xsl:text>))
</xsl:text>
  </xsl:template>
  <xsl:template match="menu[.//app]">
    <xsl:call-template name="indent"/>
    <xsl:text>("</xsl:text>
    <xsl:value-of select="@name"/>
    <xsl:text>"</xsl:text>
    <xsl:apply-templates/>
    <xsl:text>)</xsl:text>
  </xsl:template>
  <xsl:template match="app">
    <xsl:call-template name="indent"/>
    <xsl:text>("</xsl:text>
    <xsl:value-of select="@name"/>
    <xsl:text>" (system "</xsl:text>
    <xsl:if test="@term='true'">
      <xsl:copy-of select="$terminal"/>
      <xsl:text> -e </xsl:text>
    </xsl:if>
    <xsl:value-of select="@cmd"/>    
    <xsl:text> &"))</xsl:text>
  </xsl:template>
</xsl:stylesheet>

```

## Additional resources

*   [Sawfish wiki](http://sawfish.wikia.com/wiki/Main_Page) - Official website