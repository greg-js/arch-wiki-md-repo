# PhpDox

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [PHP](/index.php/PHP "PHP").**

**Notes:** The main article already lists tools and extensions, the [#Example](#Example) could be just kept upstream. (Discuss in [Talk:PhpDox#](https://wiki.archlinux.org/index.php/Talk:PhpDox))

[phpDox](http://phpdox.de//) (phpdox) is the documentation generator for PHP projects.

## Installing

[Install](/index.php/Install "Install") the [phpdox](https://aur.archlinux.org/packages/phpdox/)<sup><small>AUR</small></sup> package.

## Example

To display the version number execute:

```
 > phpdox --version
 phpDox 0.8.0 - Copyright (C) 2010 - 2015 by Arne Blankerts

```

To analyze some code execute a command like this:

```
 > phpdox
 phpDox 0.8.0 - Copyright (C) 2010 - 2015 by Arne Blankerts

 [06.04.2015 - 10:00:02] Using config file './phpdox.xml.dist'
 [06.04.2015 - 10:00:02] Registered collector backend 'parser'
 [06.04.2015 - 10:00:02] Registered enricher 'build'
 [06.04.2015 - 10:00:02] Registered enricher 'git'
 [06.04.2015 - 10:00:02] Registered enricher 'checkstyle'
 [06.04.2015 - 10:00:02] Registered enricher 'phpcs'
 [06.04.2015 - 10:00:02] Registered enricher 'pmd'
 [06.04.2015 - 10:00:02] Registered enricher 'phpunit'
 [06.04.2015 - 10:00:02] Registered enricher 'phploc'
 [06.04.2015 - 10:00:02] Registered output engine 'xml'
 [06.04.2015 - 10:00:02] Registered output engine 'html'
 [06.04.2015 - 10:00:02] Starting to process project 'phpDox'
 [06.04.2015 - 10:00:02] Starting collector
 [06.04.2015 - 10:00:02] Scanning directory '/usr/local/src/example/src' for files to process

 {....}

 [06.04.2015 - 10:00:03] Saving results to directory '/usr/local/src/example/build/api/xml'
 [06.04.2015 - 10:00:04] Resolving inheritance

 {....}

 [06.04.2015 - 10:00:04] The following unit(s) had missing dependencies during inheritance resolution:
 [06.04.2015 - 10:00:04] Collector process completed

 [06.04.2015 - 10:00:04] Starting generator
 [06.04.2015 - 10:00:04] Loading enrichers
 [06.04.2015 - 10:00:04] Enricher Build Information initialized successfully
 [06.04.2015 - 10:00:04] Enricher GIT information initialized successfully
 [06.04.2015 - 10:00:04] Enricher CheckStyle XML initialized successfully
 [06.04.2015 - 10:00:04] Enricher PHPMessDetector XML initialized successfully
 [06.04.2015 - 10:00:04] Enricher PHPLoc xml initialized successfully
 [06.04.2015 - 10:00:04] Enricher PHPUnit Coverage XML initialized successfully
 [06.04.2015 - 10:00:04] Starting event loop.

 {....}

 [06.04.2015 - 10:00:12] Generator process completed
 [06.04.2015 - 10:00:12] Processing project 'phpDox' completed.

 Time: 10.8 seconds, Memory: 11.25Mb

```

## References

*   [phpDox project page](http://phpdox.de/)
*   [phpDox github page](https://github.com/theseer/phpdox)

Retrieved from "[https://wiki.archlinux.org/index.php?title=PhpDox&oldid=414211](https://wiki.archlinux.org/index.php?title=PhpDox&oldid=414211)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Development](/index.php/Category:Development "Category:Development")