[Document viewer](https://en.wikipedia.org/wiki/Evince "w:Evince") is specifically designed to support the following file formats: [PDF, PostScript, DjVu](/index.php/PDF,_PS_and_DjVu "PDF, PS and DjVu"), tiff, dvi, XPS, SyncTex support with gedit, comics books (cbr,cbz,cb7 and cbt). For a comprehensive list of formats supported, see [Supported Document Formats](https://wiki.gnome.org/Apps/Evince/SupportedDocumentFormats).

Document viewer uses the poppler library as a backend.

**Note:** Document viewer was previously known as [Evince](https://wiki.gnome.org/Apps/Evince) until the application was given new descriptive names, one for each supported language. The name *Evince* is still used in numerous places such as the executable name, some package names, some desktop entries, and some GSettings schemas.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Printer does not show up](#Printer_does_not_show_up)
    *   [2.2 Zoom-in is limited](#Zoom-in_is_limited)
    *   [2.3 PDF texts is not show correctly](#PDF_texts_is_not_show_correctly)
    *   [2.4 Inverse search with SyncTeX doesn't work](#Inverse_search_with_SyncTeX_doesn't_work)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [evince](https://www.archlinux.org/packages/?name=evince) package, or [evince-git](https://aur.archlinux.org/packages/evince-git/) for the development version. Evince installs the gnome-desktop as a dependency.

For a standalone version install [evince-no-gnome](https://aur.archlinux.org/packages/evince-no-gnome/) or the light version [evince-light](https://aur.archlinux.org/packages/evince-light/) for PDF support only.

## Troubleshooting

### Printer does not show up

Upgrade [gtk3](https://www.archlinux.org/packages/?name=gtk3) to version `3.22.26+47+g3a1a7135a2-1` or higher. In previous GTK+ 3 versions, the GTK+ printer backends were included in a separate package. [[1]](https://git.archlinux.org/svntogit/packages.git/commit/trunk?h=packages/gtk3&id=54e7af64837e18355122e62ff565970620db3537)

### Zoom-in is limited

Increasing Evince's page cache size allows you to zoom in further, which is handy for large documents. By default the setting is set to 50MiB. Increasing the page cache size obviously increases Evince's memory consumption when zoomed-in.

The following command increases the page cache size to one gigabyte:

```
$ gsettings set org.gnome.Evince page-cache-size 'uint32 1000'

```

### PDF texts is not show correctly

Try setting `override-restrictions` parameter to false:

```
$ gsettings set org.gnome.Evince override-restrictions false

```

### Inverse search with SyncTeX doesn't work

Check that [python-dbus](https://www.archlinux.org/packages/?name=python-dbus) is [installed](/index.php/Install "Install"). After that `Ctrl+click` should work.

## See also

*   [Evince website](https://wiki.gnome.org/Apps/Evince)
*   [Poppler website](http://poppler.freedesktop.org/)
*   [Page "PDF reference" from Adobe](http://www.adobe.com/devnet/pdf/pdf_reference.html)