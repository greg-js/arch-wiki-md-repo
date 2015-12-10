# Zim

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

From the project [home page](http://zim-wiki.org/):

_Zim is a graphical text editor used to maintain a collection of wiki pages. Each page can contain links to other pages, simple formatting and images. Pages are stored in a folder structure, like in an outliner, and can have attachments. Creating a new page is as easy as linking to a nonexistent page. All data is stored in plain text files with wiki formatting. Various plugins provide additional functionality, like a task list manager, an equation editor, a tray icon, and support for version control._

_Zim can be used to:_

*   _Keep an archive of notes_
*   _Take notes during meetings or lectures_
*   _Organize task lists_
*   _Draft blog entries and emails_
*   _Do brainstorming_

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
*   [4 Tips](#Tips)
    *   [4.1 Plugins](#Plugins)
        *   [4.1.1 Spell checker](#Spell_checker)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Problems at launch](#Problems_at_launch)
    *   [5.2 Error: Unable to find or create trash directory](#Error:_Unable_to_find_or_create_trash_directory)
*   [6 See also](#See_also)

## Installation

You can install [zim](https://www.archlinux.org/packages/?name=zim) from the [official repositories](/index.php/Official_repositories "Official repositories"). There is also an AUR package called [zim-bzr](https://aur.archlinux.org/packages/zim-bzr/)<sup><small>AUR</small></sup> which provides the latest developer snapshot.

## Usage

The usage of Zim is very self-explanatory. This [screencast](http://www.youtube.com/watch?v=yBZpWgzO9Ps) provides a good overview about the basic functionality.

## Configuration

The main configuration file is located in Zim's config directory: `~/.config/zim/preferences.conf`. Another important file is located in the same directory: `~/.config/zim/notebooks.list`. This file contains a list of all wikis and there file path.

Besides the configuration there exist the wiki directories which are set up when a new wikis are created. Those folders store all wiki pages in plain txt format.

## Tips

Specific user tricks to accomplish tasks.

### Plugins

Zim provides a lot of useful plugins where many of them are not enabled by default. They can be found at _Edit > Preferences > Plugins_. That is, there is a plugin which provides a tray icon.

#### Spell checker

The requirements for the Spell Checker plugin are as follows: [gtkspell](https://www.archlinux.org/packages/?name=gtkspell), [python2-gtkspell](https://www.archlinux.org/packages/?name=python2-gtkspell) and [aspell-en](https://www.archlinux.org/packages/?name=aspell-en).

Change `aspell-en` to your desired language support. Now you can configure the Spell Checker and define the default language, in my case `en_GB`.

## Troubleshooting

### Problems at launch

A common error is at start up resulting in a error message like the following [this thread](https://bbs.archlinux.org/viewtopic.php?id=120139):

```
UnboundLocalError: local variable 'i' referenced before assignment

```

It is often related to a problem with the file path of the wikis stored in `~/.config/zim/notebooks.list`. Try to delete or move this file and restart Zim.

### Error: Unable to find or create trash directory

This error message indicates that Zim is not able to find the trash directory as in [this thread](https://bbs.archlinux.org/viewtopic.php?id=126413). This occurs when the wiki is stored on a partition that does not have any trash directory under `/partition/.local/share/Trash`. Due to that one is not able to delete pages as Zim tries to move them to the trash. Solutions are either the creation of a trash directory or the installation of the developer snapshot instead of the stable version which permanently deletes a page if no trash directory can be found. Thus, the user does not receive this error message anymore.

## See also

*   [Zim homepage](http://www.zim-wiki.org/)
*   [Zim official manual](http://zim-wiki.org/manual/Start.html)
*   [A short screencast](http://www.youtube.com/watch?v=yBZpWgzO9Ps)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Zim&oldid=307451](https://wiki.archlinux.org/index.php?title=Zim&oldid=307451)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Text editors](/index.php/Category:Text_editors "Category:Text editors")