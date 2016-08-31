[tmsu](http://tmsu.org) is a tool for tagging your files. It provides a simple command-line tool for applying tags and a virtual file-system so that you can get a tagged based view of your files from within any other program.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Obstacles](#Obstacles)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [tmsu](https://aur.archlinux.org/packages/tmsu/) package.

## Usage

The tmsu [website](http://tmsu.org) provides an excellent short quick tour on the basic usage.

## Obstacles

tmsu creates symlinks between files, folders and the related tags. That is, it cannot handle file deletions and moves very well although there is a 'repair' command that will detect file moves and renames. It also updates fingerprints for modified files. There is no automatic directory watcher and it is not planned to add this facility as it would not work across all file system types.

## See also

*   [Reddit discussion](http://en.reddit.com/r/linux/comments/woear/tmsu_is_a_program_that_allows_you_to_organise/)
*   [tmsu extensions](https://github.com/Dieterbe/tmsu-helpers)
*   [tagsistant](https://aur.archlinux.org/packages/tagsistant/) (alternative semantic filesystem)