Related articles

*   [List of applications/Documents#Vi text editors](/index.php/List_of_applications/Documents#Vi_text_editors "List of applications/Documents")
*   [Vim](/index.php/Vim "Vim")

Kakoune is a modal text editor. It is inspired by Vim and similar alternatives, but tries to improve the text editing workflow as well as fit better to the Unix philosophy. Besides modal editing, two other main concepts are selection based editing, and multi-cursor editing. It has an interactive help system, and supports many languages.

## Installation

[Install](/index.php/Install "Install") the [kakoune-git](https://aur.archlinux.org/packages/kakoune-git/) package.

## Usage

`:doc <topic>` opens the documentation of <topic>.

It has an interactive help system, which means e.g. pressing `g` `(goto mode)` shows a dialog with possible keys and destinations, or it displays a help dialog with the description of the highlighted completion candidate in `prompt` mode.

## Configuration

Kakoune reads configuration from `$XDG_CONFIG_HOME/kak`.

The main configuration file is `kakrc`, and custom colorschemes can be stored in the `colors` directory.

Every `*.kak` file is loaded from `autoload` at startup. If this directory exists in `$XDG_CONFIG_HOME`, Kakoune don't loads the system wide `autoload` dir (/usr/share/kak/autoload), so it have to be linked there. For example:

```
 ln -s /usr/share/kak/autoload $XDG_CONFIG_HOME/kak/autoload/default

```