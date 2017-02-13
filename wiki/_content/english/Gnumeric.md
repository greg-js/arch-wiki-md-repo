[Gnumeric](https://en.wikipedia.org/wiki/Gnumeric "wikipedia:Gnumeric") is a powerful spreadsheet application which can import and export in various formats including .csv, HTML, LaTeX, Lotus 1-2-3, OpenDocument Spreadsheet and Microsoft Excel.

## Installing

[Install](/index.php/Install "Install") [gnumeric](https://www.archlinux.org/packages/?name=gnumeric).

Optional dependencies are [psiconv](https://www.archlinux.org/packages/?name=psiconv) (for Psion 5 file support), [python2-gobject2](https://www.archlinux.org/packages/?name=python2-gobject2) (for python plugin support) and [yelp](https://www.archlinux.org/packages/?name=yelp) (for viewing the help manual).

## Tips and tricks

Gnumeric respects your [locale](/index.php/Locale "Locale") for the numeric decimal separator and uses it for exporting, e.g. to .csv files, as well. For example

*   with a german locale `de`, a number shows as `0,5` *(comma)*,
*   with an english locale `en`, a number shows as `0.5` *(dot)*.

To start Gnumeric with a different locale, run

```
 LC_NUMERIC="en" gnumeric

```

## See also

*   [Gnumeric Official Website](http://projects.gnome.org/gnumeric/)