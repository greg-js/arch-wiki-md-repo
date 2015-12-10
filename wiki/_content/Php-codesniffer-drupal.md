# Php-codesniffer-drupal

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [PHP](/index.php/PHP "PHP").**

**Notes:** The main article already lists tools and extensions, the [#Example](#Example) could be just kept upstream. (Discuss in [Talk:Php-codesniffer-drupal#](https://wiki.archlinux.org/index.php/Talk:Php-codesniffer-drupal))

Related articles

*   [Drupal](/index.php/Drupal "Drupal")

[PHP_Codesniffer Drupal](https://www.drupal.org/project/coder) (coder) is a coding standards checker for Drupal .

## Installing

[Install](/index.php/Install "Install") the [php-codesniffer-drupal](https://aur.archlinux.org/packages/php-codesniffer-drupal/)<sup><small>AUR</small></sup> package.

## Example

To display the version number execute:

```
 > phpcs --version

 PHP_CodeSniffer version 2.3.2 (stable) by Squiz ([http://www.squiz.net](http://www.squiz.net))

```

To analyze some code execute a command like this:

```
 > phpcs --standard=Drupal example.module

 FILE: /home/user/workspace/coder/example.module
 --------------------------------------------------------------------------------
 FOUND 5 ERRORS AFFECTING 5 LINES
 --------------------------------------------------------------------------------
  1 | ERROR | [ ] Missing file doc comment
  3 | ERROR | [ ] Missing function doc comment
  4 | ERROR | [ ] Opening brace should be on the same line as the declaration
  5 | ERROR | [x] Line indented incorrectly; expected 2 spaces, found 1
  6 | ERROR | [x] Line indented incorrectly; expected 2 spaces, found 3
 --------------------------------------------------------------------------------
 PHPCBF CAN FIX THE 2 MARKED SNIFF VIOLATIONS AUTOMATICALLY
 --------------------------------------------------------------------------------

```

## References

*   [Drupal Coder page](https://www.drupal.org/project/coder)
*   [PHP_CodeSniffer page](https://github.com/squizlabs/PHP_CodeSniffer)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Php-codesniffer-drupal&oldid=391625](https://wiki.archlinux.org/index.php?title=Php-codesniffer-drupal&oldid=391625)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Development](/index.php/Category:Development "Category:Development")