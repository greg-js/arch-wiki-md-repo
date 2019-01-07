Related articles

*   [List of applications/Documents#Vi text editors](/index.php/List_of_applications/Documents#Vi_text_editors "List of applications/Documents")

*   [Vim](/index.php/Vim "Vim")

[Kakoune](http://kakoune.org/) is a modal text editor. It is inspired by Vim and similar alternatives, but tries to improve the text editing workflow as well as fit better to the Unix philosophy. Besides modal editing, two other main concepts are selection based editing, and multi-cursor editing. It has an interactive help system, and supports many languages.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [kakoune](https://www.archlinux.org/packages/?name=kakoune) package.

## Usage

`:doc <topic>` opens the documentation of <topic>.

It has an interactive help system, which means e.g. pressing `g` `(goto mode)` shows a dialog with possible keys and destinations, or it displays a help dialog with the description of the highlighted completion candidate in `prompt` mode.

## Configuration

Kakoune reads configuration from `$XDG_CONFIG_HOME/kak`.

The main configuration file is `kakrc`, and custom colorschemes can be stored in the `colors` directory.

Every `*.kak` file is loaded from `autoload` at startup. If this directory exists in `$XDG_CONFIG_HOME`, Kakoune doesn't load the system wide `autoload` dir (located at `/usr/share/kak/autoload`), so it has to be linked there. For example:

```
 ln -s /usr/share/kak/autoload $XDG_CONFIG_HOME/kak/autoload/default

```

## See also

*   [GitHub repository](https://github.com/mawww/kakoune)
*   [GitHub wiki](https://github.com/mawww/kakoune/wiki)