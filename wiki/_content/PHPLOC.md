# PHPLOC

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [PHP](/index.php/PHP "PHP").**

**Notes:** The main article already lists tools and extensions, the [#Example](#Example) could be just kept upstream. (Discuss in [Talk:PHPLOC#](https://wiki.archlinux.org/index.php/Talk:PHPLOC))

[PHPLOC](https://github.com/sebastianbergmann/phploc) (phploc) is a tool for quickly measuring the size and analyzing the structure of a PHP project.

## Installing

[Install](/index.php/Install "Install") the [phploc](https://aur.archlinux.org/packages/phploc/)<sup><small>AUR</small></sup> package.

**Note:** You have to enable `extension=phar.so` in your php.ini for PHP to be able to run the PHP Archive/PHAR file.

## Example

To display the version number execute:

```
 > phploc --version
 phploc 2.1.4 by Sebastian Bergmann.

```

To analyze some code execute a command like this:

```
 > phploc src
 phploc 2.1.4 by Sebastian Bergmann.

 Directories                                          3
 Files                                                8

 Size
   Lines of Code (LOC)                             1858
   Comment Lines of Code (CLOC)                     560 (30.14%)
   Non-Comment Lines of Code (NCLOC)               1298 (69.86%)
   Logical Lines of Code (LLOC)                     289 (15.55%)
     Classes                                        260 (89.97%)
       Average Class Length                          37
       Average Method Length                          9
     Functions                                        5 (1.73%)
       Average Function Length                        5
     Not in classes or functions                     24 (8.30%)

 Complexity
   Cyclomatic Complexity / LLOC                    0.67
   Cyclomatic Complexity / Number of Methods       7.86

 Dependencies
   Global Accesses                                    2
     Global Constants                                 2 (100.00%)
     Global Variables                                 0 (0.00%)
     Super-Global Variables                           0 (0.00%)
   Attribute Accesses                                48
     Non-Static                                      48 (100.00%)
     Static                                           0 (0.00%)
   Method Calls                                      96
     Non-Static                                      91 (94.79%)
     Static                                           5 (5.21%)

 Structure
   Namespaces                                         4
   Interfaces                                         0
   Traits                                             0
   Classes                                            7
     Abstract Classes                                 0 (0.00%)
     Concrete Classes                                 7 (100.00%)
   Methods                                           28
     Scope
       Non-Static Methods                            28 (100.00%)
       Static Methods                                 0 (0.00%)
     Visibility
       Public Method                                 10 (35.71%)
       Non-Public Methods                            18 (64.29%)
   Functions                                          1
     Named Functions                                  0 (0.00%)
     Anonymous Functions                              1 (100.00%)
   Constants                                          1
     Global Constants                                 1 (100.00%)
     Class Constants                                  0 (0.00%)

```

## References

*   [PHPLOC project page](https://github.com/sebastianbergmann/phploc)

Retrieved from "[https://wiki.archlinux.org/index.php?title=PHPLOC&oldid=391627](https://wiki.archlinux.org/index.php?title=PHPLOC&oldid=391627)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Development](/index.php/Category:Development "Category:Development")