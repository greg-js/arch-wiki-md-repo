# Tmsu

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[tmsu](http://tmsu.org) is a tool for tagging your files. It provides a simple command-line tool for applying tags and a virtual file-system so that you can get a tagged based view of your files from within any other program.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Obstacles](#Obstacles)
*   [4 See also](#See_also)

## Installation

tmsu can be installed with the [tmsu](https://aur.archlinux.org/packages/tmsu/)<sup><small>AUR</small></sup> or [tmsu-bin](https://aur.archlinux.org/packages/tmsu-bin/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/tmsu-bin)]</sup> packages.

## Usage

The tmsu [website](http://tmsu.org) provides an excellent short quick tour on the basic usage.

## Obstacles

tmsu creates symlinks between files, folders and the related tags. That is, it cannot handle file deletions and moves very well although there is a 'repair' command that will detect file moves and renames. It also updates fingerprints for modified files. There is no automatic directory watcher and it is not planned to add this facility as it would not work across all file system types.

## See also

*   [Reddit discussion](http://en.reddit.com/r/linux/comments/woear/tmsu_is_a_program_that_allows_you_to_organise/)
*   [tmsu extensions](https://github.com/Dieterbe/tmsu-helpers)
*   [tagsistant](https://aur.archlinux.org/packages/tagsistant/)<sup><small>AUR</small></sup> (alternative semantic filesystem)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Tmsu&oldid=399131](https://wiki.archlinux.org/index.php?title=Tmsu&oldid=399131)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Search](/index.php/Category:Search "Category:Search")
*   [File systems](/index.php/Category:File_systems "Category:File systems")

Hidden category:

*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")