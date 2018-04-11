From the [official website](http://aspell.net/): "GNU Aspell is a Free and Open Source spell checker designed to eventually replace [Ispell](https://en.wikipedia.org/wiki/Ispell "wikipedia:Ispell"). It can either be used as a library or as an independent spell checker."

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 All text is marked as misspelled](#All_text_is_marked_as_misspelled)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [aspell dictionary](https://www.archlinux.org/packages/?sort=&q=aspell-) for the language you require. Doing so will also pull in the [aspell](https://www.archlinux.org/packages/?name=aspell) package as a dependency.

## Usage

Many programs use *aspell* automatically and need no further configuration. Additionally one can use *aspell* manually. Here are some basic usages. See [aspell(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/aspell.1) for more.

To spell check a single file:

```
$ aspell check *somefile*

```

You will then be dropped into a prompt with the file text displayed. From there you can select for *aspell* to make corrections to each misspelled word it detects, or you can choose to ignore its suggestions. Corrections you make will be saved to the file.

To list mispelled words from standard input:

```
$ cat *somefile* | aspell list

```

## Troubleshooting

### All text is marked as misspelled

Ensure you have the correct dictionary installed. If installing the dictionary files does not resolve the problem, it is most likely a problem with `enchant`. Check for known dictionary files:

 `$ aspell dicts` 
```
en
en_GB
...etc
```

If your respective language dictionary is listed, add it to `/usr/share/enchant/enchant.ordering`. From the above example, it would be:

```
en_GB:aspell

```

## See also

*   [aspell info document](http://aspell.net/man-html/index.html)
*   [Wikipedia:GNU Aspell](https://en.wikipedia.org/wiki/GNU_Aspell "wikipedia:GNU Aspell")