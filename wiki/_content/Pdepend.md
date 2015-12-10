# Pdepend

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [PHP](/index.php/PHP "PHP").**

**Notes:** The main article already lists tools and extensions, the [#Example](#Example) could be just kept upstream. (Discuss in [Talk:Pdepend#](https://wiki.archlinux.org/index.php/Talk:Pdepend))

[PHP Depend](http://pdepend.org/) (pdepend) is software metrics tool for php.

## Installing

[Install](/index.php/Install "Install") the [pdepend](https://aur.archlinux.org/packages/pdepend/)<sup><small>AUR</small></sup> package.

**Note:** You have to enable `extension=phar.so` and `extension=bz2.so` in your php.ini for PHP to be able to run the PHP Archive/PHAR file.

## Example

To display the version number execute:

```
 > pdepend --version

 PHP_Depend 0.9.4 by Manuel Pichler

```

To analyze some code execute a command like this:

```
 > pdepend --summary-xml=/tmp/summary.xml \
                      --jdepend-chart=/tmp/jdepend.svg \
                      --overview-pyramid=/tmp/pyramid.svg \
                      /usr/local/share/pear/PDepend

 PHP_Depend 0.9.4 by Manuel Pichler

 Parsing source files:
 ............................................................    60
 ............................                                    88

 Executing NPathComplexity-Analyzer:
 ...........................................                    869

 Executing Coupling-Analyzer:
 ...........................................................   1193

 Executing NodeCount-Analyzer:
 .................................                              677

 Executing Dependency-Analyzer:
 ...................................                            703

 Executing Hierarchy-Analyzer:
 ...........................................                    880

 Executing Inheritance-Analyzer:
 .....................                                          421

 Executing CodeRank-Analyzer:
 ......                                                         126

 Executing CyclomaticComplexity-Analyzer:
 ...........................................                    869

 Executing ClassLevel-Analyzer:
 .......................................                        783

 Executing NodeLoc-Analyzer:
 ...............................................                951

 Generating pdepend log files, this may take a moment.

 Time: 00:13; Memory: 15.00Mb

```

## References

*   [Official PHPDepend Page](http://pdepend.org/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Pdepend&oldid=391624](https://wiki.archlinux.org/index.php?title=Pdepend&oldid=391624)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Development](/index.php/Category:Development "Category:Development")