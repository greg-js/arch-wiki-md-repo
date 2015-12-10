# PhpMetrics

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [PHP](/index.php/PHP "PHP").**

**Notes:** The main article already lists tools and extensions, the [#Example](#Example) could be just kept upstream. (Discuss in [Talk:PhpMetrics#](https://wiki.archlinux.org/index.php/Talk:PhpMetrics))

[PhpMetrics](http://www.phpmetrics.org/) (phpmetrics) is a static analysis tool for PHP

## Installing

[Install](/index.php/Install "Install") the [phpmetrics](https://aur.archlinux.org/packages/phpmetrics/)<sup><small>AUR</small></sup> package.

**Note:** You have to enable `extension=phar.so` in your php.ini for PHP to be able to run the PHP Archive/PHAR file.

## Example

To display the version number execute:

```
 > phpmetrics --version
 PhpMetrics, by Jean-François Lépine ([https://twitter.com/Halleck45](https://twitter.com/Halleck45)) version 1.0.0

```

To analyze some code execute a command like this:

```
 > phpmetrics -q --report-xml=php://stdout src

 Maintenability................ 36.77 / 100
 Accessibility for new developers 17.83 / 100
 Simplicity of algorithms...... 80 / 100
 Volume........................ 48.37 / 100
 Reducing bug's probability.... 60.66 / 100

 <?xml version="1.0" encoding="UTF-8"?>
 <project loc="379" lloc="126" cyclomaticComplexity="2.4" maintenabilityIndex="77.65" volume="1001.07" vocabulary="48" difficulty="13.65" bugs="0.33" time="1004" intelligentContent="77.39" lcom="2.2" instability="1" efferentCoupling="4" afferentCoupling="0">
   <modules>
     <module loc="379" lloc="126" cyclomaticComplexity="2.4" maintenabilityIndex="77.65" volume="1001.07" vocabulary="48" difficulty="13.65" bugs="0.33" time="1004" intelligentContent="77.39" lcom="2.2" instability="1" efferentCoupling="4" afferentCoupling="0" namespace="mir"/>
     <module loc="379" lloc="126" cyclomaticComplexity="2.4" maintenabilityIndex="77.65" volume="1001.07" vocabulary="48" difficulty="13.65" bugs="0.33" time="1004" intelligentContent="77.39" lcom="2.2" instability="1" efferentCoupling="4" afferentCoupling="0" namespace="mir/src"/>
     <module loc="379" lloc="126" cyclomaticComplexity="2.4" maintenabilityIndex="77.65" volume="1001.07" vocabulary="48" difficulty="13.65" bugs="0.33" time="1004" intelligentContent="77.39" lcom="2.2" instability="1" efferentCoupling="4" afferentCoupling="0" namespace="mir/src/mir"/>
     <module loc="379" lloc="126" cyclomaticComplexity="2.4" maintenabilityIndex="77.65" volume="1001.07" vocabulary="48" difficulty="13.65" bugs="0.33" time="1004" intelligentContent="77.39" lcom="2.2" instability="1" efferentCoupling="4" afferentCoupling="0" namespace="mir/src/mir/Console"/>
     <module loc="379" lloc="126" cyclomaticComplexity="2.4" maintenabilityIndex="77.65" volume="1001.07" vocabulary="48" difficulty="13.65" bugs="0.33" time="1004" intelligentContent="77.39" lcom="2.2" instability="1" efferentCoupling="4" afferentCoupling="0" namespace="mir/src/mir/Console/Command"/>
   </modules>
 </project>

```

## References

*   [PhpMetrics project page](http://www.phpmetrics.org/)
*   [PhpMetrics github page](https://github.com/Halleck45/PhpMetrics)

Retrieved from "[https://wiki.archlinux.org/index.php?title=PhpMetrics&oldid=391626](https://wiki.archlinux.org/index.php?title=PhpMetrics&oldid=391626)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Development](/index.php/Category:Development "Category:Development")