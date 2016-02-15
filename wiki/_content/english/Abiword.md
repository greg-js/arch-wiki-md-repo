[Abiword](http://www.abisource.com/) is a word processor that provides a lighter alternative for [LibreOffice](/index.php/LibreOffice "LibreOffice") Writer and [OpenOffice](/index.php/OpenOffice "OpenOffice") Writer, while at the same time providing great functionality. Abiword supports many standard document types, such as ODF documents, Microsoft Word documents, WordPerfect documents, Rich Text Format documents and HTML web pages.

## Contents

*   [1 Installation](#Installation)
*   [2 Templates](#Templates)
*   [3 Grammar Checking](#Grammar_Checking)
*   [4 Change keybindings](#Change_keybindings)
*   [5 LaTeX fonts](#LaTeX_fonts)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Fix for print dialog crash](#Fix_for_print_dialog_crash)

## Installation

[Install](/index.php/Install "Install") the [abiword](https://www.archlinux.org/packages/?name=abiword) package. You may want to install dictionaries if you want spell check, which can be provided by the [aspell-en](https://www.archlinux.org/packages/?name=aspell-en) package for English.

To fix tiny cursor and misaligned text issues, install either [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) from the official repositories or [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) from the [AUR](/index.php/AUR "AUR") and [ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont) from the official repositories.

## Templates

If you want to change the default styles in Abiword, you should open a new document, change it to your own needs, and save it as the template name _normal.awt_ in the `$HOME/.AbiSuite/templates` directory. After that, your new documents will follow the template.

The instructions above don't work for Abiword 3.0\. The following does work:

In a new document, choose Format -> Create and Modify Styles... from the menu, adjust the Normal style to what you'd prefer, and save it as ~/normal.awt then:

sudo mv ~/normal.awt /usr/share/abiword-3.0/templates/

Other styles in /usr/share/abiword-3.0/templates/ can be modified as well.

## Grammar Checking

Install the [abiword-plugins](https://www.archlinux.org/packages/?name=abiword-plugins) package and enable grammar checking from _Edit>Preferences>Spell Checking>Automatic grammar checking_.

## Change keybindings

See [this wiki post](http://www.abisource.com/wiki/Keyboard_bindings) on how to change the default key bindings in Abiword.

If such method does not work, add `KeyBindings="viEdit"` to `/usr/share/abiword-3.0/system.profile` inside of the `SystemDefaults` tag.

## LaTeX fonts

The package [abiword-plugins](https://www.archlinux.org/packages/?name=abiword-plugins) comes with a function which allows user to insert LaTeX codes in a document. To display mathematics symbols properly, one needs to download [latex-xft-fonts](http://movementarian.org/latex-xft-fonts-0.1.tar.gz) and save it to the directory `/usr/share/fonts`. To install the font, extract the tarball and then run the following:

```
# fc-cache -fv

```

## Troubleshooting

### Fix for print dialog crash

**Note:** This bug has been reported as non-existent for version 2.8.1 or higher. However, this section will remain for legacy versions or if it crops up again,

For some reason, the current versions of Abiword and libgnomeprint are not playing nice together. The `.abw` default template causes the program to crash when the user attempts to print. The solution is to force abiword to work with the `.rtf` format instead. By following the steps below, you will set the default save format to .rtf and trick Abiword into using a `.rtf` file as its default template.

Open `~/.AbiSuite/AbiWord.Profile` and insert the following line into the second <scheme> section.

```
DefaultSaveFormat=".rtf"

```

It should look similar to the following:

```
<Scheme
   name="_custom_"
   ZoomPercentage="64"
   DefaultSaveFormat=".rtf"
/>

```

It is then neccessary to change the default template. You must follow these steps exactly.

1.  Open Abiword and save a blank document titled `normal.rtf` in `~/.AbiSuite/templates/`. If the directory does not exist, create it.
2.  Rename the file to _normal.awt_.

Do **not** just save a blank `.awt` file! You must trick Abiword into using a `.rtf` template in order for this to work.

As soon as the conflict between Abiword and libgnomeprint is resovled, these instructions will no longer be neccessary and should be removed.