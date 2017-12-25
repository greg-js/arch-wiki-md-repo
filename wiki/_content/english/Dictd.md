[dictd](http://sourceforge.net/projects/dict/) is an online dictionary client and server.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Hosting Offline Dictionaries](#Hosting_Offline_Dictionaries)
    *   [2.2 Installing Additional Dictionaries](#Installing_Additional_Dictionaries)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Parse Error](#Parse_Error)
*   [4 Graphical front ends](#Graphical_front_ends)

## Installation

[Install](/index.php/Install "Install") the [dictd](https://www.archlinux.org/packages/?name=dictd) package.

## Configuration

### Hosting Offline Dictionaries

[dictd](https://www.archlinux.org/packages/?name=dictd) can be configured to host offline dictionaries using `localhost` as the server.

[FreeDict](https://github.com/freedict) provides dictionaries compatible with [dictd](https://www.archlinux.org/packages/?name=dictd) and are available through the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

As an example, the [dict-freedict-eng-spa](https://aur.archlinux.org/packages/dict-freedict-eng-spa/) package installs an English-Spanish dictionary.

After installation, in order to access the newly installed dictionary, start the `dictd.service`:

```
# systemctl start dictd.service

```

And now the English-Spanish dictionary can be queried by executing:

```
$ dict 

```

**Note:** After new dictionaries are installed, the `dictd.services` must be restarted in order to refresh the list of available dictionaries. In other words, a

**Tip:** A list of all the available dictionaries can be queried by executing:
```
$ dict -I

```

**Tip:** To query a specific dictionary database, you can use the `-d` flag. To query the English-Spanish database, for example, for the word "free" you can use:
```
$ dict -d eng-spa free

```

### Installing Additional Dictionaries

Additional dictionaries are available in the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") through the search term `dictd`. For example, [dict-wn](https://aur.archlinux.org/packages/dict-wn/) is an English-English dictionary.

After installing the new dictionaries, make sure to restart the `dictd.service` to refresh the available dictionary databases.

```
# systemctl restart dictd.service

```

## Troubleshooting

### Parse Error

The following error:

```
/etc/dict/dictd.conf:25: syntax error, unexpected $end
/etc/dict/dictd.conf:25: #LASTLINE
/etc/dict/dictd.conf:25:          ^
dictd (yyerror): parse error
parse error

```

Means that `dictd` cannot find a dictionary database. These can be added manually to `/etc/dict/dictd.conf`. For example:

```
database eng-spa {
	data /usr/share/dictd/eng-spa.dict.dz
	index /usr/share/dictd/eng-spa.index
}

```

Adds the English-Spanish dicitonary installed by [dict-freedict-eng-spa](https://aur.archlinux.org/packages/dict-freedict-eng-spa/). For other dictionaries, copy and pase the above database declaration but make sure to change the database name, i.e. `eng-spa`, and also change the `data` and `index` paths above to specify the right files.

## Graphical front ends

There are various graphical applications that can access `dictd` through the [DICT protocol](https://en.wikipedia.org/wiki/DICT "wikipedia:DICT"). One of which is: [goldendict](/index.php/Goldendict "Goldendict").