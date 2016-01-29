# Gnome Color Chooser

[![Tango-emblem-symbolic-link.png](/images/f/f9/Tango-emblem-symbolic-link.png)](/index.php/File:Tango-emblem-symbolic-link.png)

[![Tango-emblem-symbolic-link.png](/images/f/f9/Tango-emblem-symbolic-link.png)](/index.php/File:Tango-emblem-symbolic-link.png)

**This article is being considered for redirection to [Gtk](/index.php/Gtk "Gtk").**

**Notes:** Most text are general gtk configure. Redirect to [Gtk](/index.php/Gtk "Gtk")? (Discuss in [Talk:Gnome Color Chooser#](https://wiki.archlinux.org/index.php/Talk:Gnome_Color_Chooser))

GNOME's color schemes are editable easily via the ~/.gtkrc-2.0 file, but the GNOME color chooser makes this process easier and graphical.

## Contents

*   [1 Installation](#Installation)
*   [2 Tips and Tricks](#Tips_and_Tricks)
    *   [2.1 Global](#Global)
        *   [2.1.1 Default Normal](#Default_Normal)
        *   [2.1.2 Default Entry Fields](#Default_Entry_Fields)
    *   [2.2 Buttons](#Buttons)
        *   [2.2.1 Buttons](#Buttons_2)
        *   [2.2.2 Comboboxes](#Comboboxes)
    *   [2.3 Panel](#Panel)
        *   [2.3.1 Panel](#Panel_2)
        *   [2.3.2 Start Menu](#Start_Menu)
    *   [2.4 Desktop](#Desktop)
    *   [2.5 Specific](#Specific)
        *   [2.5.1 Window Decoration](#Window_Decoration)
        *   [2.5.2 Scrollbars](#Scrollbars)
        *   [2.5.3 Progress Bars](#Progress_Bars)
        *   [2.5.4 Tooltips](#Tooltips)
        *   [2.5.5 Links](#Links)
    *   [2.6 Icons](#Icons)
    *   [2.7 Engines](#Engines)

## Installation

Install [gnome-color-chooser](https://aur.archlinux.org/packages/gnome-color-chooser/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gnome-color-chooser)]</sup> from the [AUR](/index.php/AUR "AUR").

## Tips and Tricks

This should be an outline of what each of the fields affect, determined by trial-and-error. Know that this affects the local user's setup and thus this will likely override the related default configurations set by files earlier in the preference list (i.e. /usr/share/ or /etc/).

### Global

```
 These affect all programs (hence global) that use the current coloring scheme via the GTK interface.

```

#### Default Normal

These affect standard items that are click and choose or are entirely static.

**normal**: _foreground_ = standard text; i.e. font color of "Default Configuration"

**normal**: _background_ = area surrounding standard text; i.e. background color surrounding all the buttons and standard text

**hover**: _foreground_ = text of selectable items when hovering; i.e. font color of visible drop down menu item, date and time font color during hover

**hover**: _background_ = background of selectable items when hovering; i.e. drop down menus prior to clicking

**selected**: _foreground_ = Unknown

**selected**: _background_ = color of items indicating currently active area; i.e. scrollbars, tab covers

**active**: _forground_ = text of selectable items that are available (as opposed to the selected item); i.e. not currently selected tabs

**active**: _background_ = background of selectable items that are available (as opposed to the selected item); i.e. not currently selected tabs

**disabled**: _foreground_ = text of not selectable items; i.e. typically grayed out selectable items

**disabled**: _background_ = background of not selectable items; i.e. typically grayed out selectable items

#### Default Entry Fields

These affect areas that require user input.

**normal**: _foreground_ = fonts/items placed in user input fields; i.e. color of checks in checkboxes, text color in drop-down menu widgets

**normal**: _background_ = area of the entry field; i.e. background color contained in text boxes, check boxes, etc.

**hover**: _foreground_ = text of selectable input items when hovering; i.e. drop down menu font items during selection

**hover**: _background_ = Unknown

**selected**: _foreground_ = text of currently user-selected item(s); i.e. font of currently selected file in a browser window

**selected**: _background_ = background of currently user-selected item(s); i.e. highlight of currently selected file in a browser window

**active**: _forground_ = text of selectable items that are available (as opposed to the selected item); i.e. not currently items in a browser window

**active**: _background_ = background of selectable items that are available (as opposed to the selected item); i.e. not currently selected items in a browser window

**disabled**: _foreground_ = text of unavailable user input fields; i.e. unchangeable text box font

**disabled**: _background_ = background of unavailable user input fields; i.e. unchangeable text box background

### Buttons

These affect the button widgets that are used, such as the standard "Close" and "Apply" buttons as well drop down lists.

#### Buttons

The buttons akin to "Close" and "Apply", the "Go" and "Search" buttons on the left of this page

#### Comboboxes

The visible drop-down menu item.

### Panel

These affect the items in panels that are used by the system (note, not just gnome-panel, but any panels that use the .gtkrc-2.0 file)

#### Panel

These affect standard panel, such as the gnome-panel

#### Start Menu

These affect the Main GNOME Menu, and imaginably other primary menus

### Desktop

These affect the items on the desktop (i.e. the "Computer" icon)

### Specific

#### Window Decoration

These affect the coloring of the window title bars when using the GTK window decorator

#### Scrollbars

These affect the scrollbars used in the GTK applications, such as to the right of this text.

#### Progress Bars

Purportedly, these affect the progress bars used in GTK applications, though none come to mind. Likely requires the GTK window decorator.

#### Tooltips

Likely requires the GTK window decorator, changes the tooltop colors.

#### Links

Likely requires the GTK window decorator, imaginably changes link colors.

### Icons

Allow you to change icon sizes, as of the time of this writing.

### Engines

Advanced: (presumably) Allows you to select "engines" for each subset.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Gnome_Color_Chooser&oldid=417045](https://wiki.archlinux.org/index.php?title=Gnome_Color_Chooser&oldid=417045)"