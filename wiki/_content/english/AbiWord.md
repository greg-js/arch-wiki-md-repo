[AbiWord](http://www.abisource.com/) is a word processor that provides a lighter alternative for [LibreOffice](/index.php/LibreOffice "LibreOffice") Writer and [OpenOffice](/index.php/OpenOffice "OpenOffice") Writer, while at the same time providing great functionality. AbiWord supports many standard document types, such as ODF documents, Microsoft Word documents, WordPerfect documents, Rich Text Format documents and HTML web pages.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 User config directory](#User_config_directory)
*   [3 Templates](#Templates)
    *   [3.1 Using templates](#Using_templates)
    *   [3.2 Creating or changing templates](#Creating_or_changing_templates)
    *   [3.3 Mail Merge](#Mail_Merge)
*   [4 Grammar checking](#Grammar_checking)
*   [5 Change keybindings](#Change_keybindings)
*   [6 LaTeX fonts](#LaTeX_fonts)

## Installation

[Install](/index.php/Install "Install") the [abiword](https://www.archlinux.org/packages/?name=abiword) package.

AbiWord can use multiple spell checking dictionaries, see [Language checking](/index.php/Language_checking "Language checking").

To fix tiny cursor and misaligned text issues, install either [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) or [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) and [gnu-free-fonts](https://www.archlinux.org/packages/?name=gnu-free-fonts).

## User config directory

Since version 3.0, AbiWord will use `~/.config/abiword` to store user files.

Previous versions of AbiWord used `~/.config/AbiSuite` and, if it is found upon startup, it will automatically be renamed accordingly. If both `~/.config/AbiSuite` and `~/.config/abiword` do not exist, AbiWord will **not** create it.

## Templates

AbiWord provides a template system that enables to speed up writing common documents. Templates are provided as *.awt* files, for **A**bi**W**ord **T**emplate.

Template files are searched inside of `/usr/share/abiword-3.0/templates` and `~/.config/abiword/templates` folders.

### Using templates

In a new document, choose *File > New using Template...*, then, in the "New Document" dialog, select one of the templates found and listed, or click "Open" to browse your files for an AbiWord file (not necessarily a *.awt* file).

### Creating or changing templates

AbiWord allows to make your own template files, with the desired style, text, tables etc.

In order to create/change a template file, simply open a new/existent document, and make the desired changes to this file. Then, use "Save As" menu option to name it as you want, with *.awt* as extension (e.g. *foobar.awt*) and save it in `~/.config/abiword/templates` folder. Now, your new template can be accessed in *File > New using Template...* by its filename (*foobar.awt* in the given example).

**Note:** If not existent, `templates` folder will be created automatically upon startup inside `~/.config/abiword/`.

### Mail Merge

You can create a CSV file with your data to be used, and run Abiword from the command line against a template to directly render your final files. See [this guide](https://www.abisource.com/help/en-US/howto/howtomailmerge.html) for more details.

## Grammar checking

Enable grammar checking from *Edit > Preferences > Spell Checking > Automatic grammar checking*.

## Change keybindings

**Note:** [This wiki post](http://www.abisource.com/wiki/Keyboard_bindings) has instruction on this, but some are out of date and does not work

You can change the default keyboard bindings in AbiWord using [KeyBindings](https://www.abisource.com/wiki/KeyBindings).

In order to set keybindings, edit `~/.config/abiword/profile` and, inside the `AbiPreferences` tag, add the desired *KeyBindings*. For instance, you can add `KeyBindings="viEdit"` or `KeyBindings="emacs"`

## LaTeX fonts

The package [abiword](https://www.archlinux.org/packages/?name=abiword) comes with a function which allows user to insert LaTeX codes in a document. To display mathematics symbols properly, [install](/index.php/Install "Install") [ttf-latex-xft-fonts](https://aur.archlinux.org/packages/ttf-latex-xft-fonts/).