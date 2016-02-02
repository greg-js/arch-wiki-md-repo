# Gnumeric

[Gnumeric](https://en.wikipedia.org/wiki/Gnumeric "wikipedia:Gnumeric") is a powerful spreadsheet application which can import and export in various formats including csv, HTML, LaTeX, Lotus 1-2-3, OpenDocument Spreadsheet and Microsoft Excel.

## Installing

[Install](/index.php/Install "Install") [gnumeric](https://www.archlinux.org/packages/?name=gnumeric) from the [Official repositories](/index.php/Official_repositories "Official repositories").

Optional dependencies are [psiconv](https://www.archlinux.org/packages/?name=psiconv) (for Psion 5 file support), [python2-gobject2](https://www.archlinux.org/packages/?name=python2-gobject2) (for python plugin support) and [yelp](https://www.archlinux.org/packages/?name=yelp) (for viewing the help manual).

### decimal separator

Gnumeric is depending on your locale and use it for exporting as csv file too. For example, octave use dot decimal seperator.

Display 1/2:

With german locale "de", Gnumeric shows 0,5 _(comma)_

With englisch locale "en", Gnumeric shows 0.5 _(dot)_

To start Gnumeric with a different locale, just run

```
 LC_NUMERIC="en" gnumeric

```

## External Resources

*   [Gnumeric Official Website](http://projects.gnome.org/gnumeric/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Gnumeric&oldid=412091](https://wiki.archlinux.org/index.php?title=Gnumeric&oldid=412091)"