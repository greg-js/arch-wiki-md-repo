# Docbook

## Contents

*   [1 Installation](#Installation)
*   [2 Validating XML file](#Validating_XML_file)
*   [3 Converting into XHTML](#Converting_into_XHTML)
    *   [3.1 Single file](#Single_file)
    *   [3.2 Segmented](#Segmented)
*   [4 Automating](#Automating)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Compilation errors](#Compilation_errors)

## Installation

[Install](/index.php/Install "Install") [docbook-xml](https://www.archlinux.org/packages/?name=docbook-xml) and [docbook-xsl](https://www.archlinux.org/packages/?name=docbook-xsl).

## Validating XML file

To validate the XML file use:

```
$ xmllint --valid --noout _/path/to/file.xml_

```

This will generate no output if the file is proper XML.

## Converting into XHTML

### Single file

To convert into a XHTML file (single file) use:

```
$ xsltproc /usr/share/xml/docbook/$(pacman -Q docbook-xsl | cut -d ' ' -f 2 | cut -d '-' -f 1)/xhtml/docbook.xsl _/path/to/file.xml_ > _output.html_

```

### Segmented

To convert into a a segmented XHTML file (each section in its own file) use:

```
$ xsltproc /usr/share/xml/docbook/$(pacman -Q docbook-xsl | cut -d ' ' -f 2 | cut -d '-' -f 1)/xhtml/chunk.xsl _/path/to/file.xml_

```

## Automating

You can add these to `~/.bashrc` (or similar shell startup file):

```
alias doc2html1="xsltproc /usr/share/xml/docbook/xhtml/docbook.xsl"
alias doc2multihtml="xsltproc /usr/share/xml/docbook/xhtml/chunk.xsl"
alias docvalidate="xmllint --valid --noout"
```

## Troubleshooting

### Compilation errors

If you have already installed the packages above, but begin to see compilation errors such as:

```
GEN    appdata-validate.1
I/O error : Attempt to load network entity [http://docbook.sourceforge.net/release/xsl/current/manpages/docbook.xsl](http://docbook.sourceforge.net/release/xsl/current/manpages/docbook.xsl)
warning: failed to load external entity "[http://docbook.sourceforge.net/release/xsl/current/manpages/docbook.xsl](http://docbook.sourceforge.net/release/xsl/current/manpages/docbook.xsl)"
cannot parse [http://docbook.sourceforge.net/release/xsl/current/manpages/docbook.xsl](http://docbook.sourceforge.net/release/xsl/current/manpages/docbook.xsl)

```

Then reinstall [docbook-xml](https://www.archlinux.org/packages/?name=docbook-xml) and [docbook-xsl](https://www.archlinux.org/packages/?name=docbook-xsl). If something has corrupted the catalog file, this will run `xmlcatalog` and rebuild `/etc/xml/catalog`, which may resolve these compile errors.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Docbook&oldid=374374](https://wiki.archlinux.org/index.php?title=Docbook&oldid=374374)"