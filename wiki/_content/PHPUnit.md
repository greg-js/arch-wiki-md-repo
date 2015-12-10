# PHPUnit

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

## Installing

By far the easiest way to install is using the PHP Archive ([PHAR](http://php.net/phar)) package provided by the project. The PHAR package contains all dependencies as well as some of the optional dependencies for PHPUnit. The latest version can be retrieved from the project's site:

```
wget [https://phar.phpunit.de/phpunit.phar](https://phar.phpunit.de/phpunit.phar)

```

**Note:** PHPUnit is also avalible from the [AUR](/index.php/AUR "AUR") as [phpunit](https://aur.archlinux.org/packages/phpunit/)<sup><small>AUR</small></sup>.

You can then run PHPUnit using `php phpunit.phar`. You can also make the PHP Archive executable (`chmod +x phpunit.phar`) and move it to /usr/local/bin or ~/bin or somewhere else you have in your `$PATH`.

**Note:** You have to enable `extension=phar.so` in your php.ini for PHP to be able to run PHP Archive/PHAR files.

## Example

This section gives beginners a very brief introduction to how to use PHPUnit to run test cases. It won't explain how to write them but if you want to get more information about this have a look at the references.

As the application to be tested we use in this example a [JSON schema validator](https://github.com/hasbridge/php-json-schema%7C). In the directory _tests_ you'll see the directory _mock_ and three files.

*   mock
*   JsonValidatorTest.php
*   bootstrap.php
*   phpunit.xml

_mock_ contains JSON schemas which have nothing to do with PHPUnit itself, it's application-specific here, you won't find it in other applications.

_phpunit.xml is a [configuration file](http://www.phpunit.de/manual/current/en/appendixes.configuration.html) where you_

*   configure PHPUnit's core functionality,
*   compose a test suite out of test suites and test cases,
*   select groups of tests from a suite of tests that should (not) be run,
*   configure the blacklist and whitelist for the code coverage reporting,
*   configure the logging of the test execution,
*   attach additional test listeners to the test execution,
*   configure PHP settings, constants, and global variables or
*   configure a list of Selenium RC servers.

In _bootstrap.php_ you put code to be run before tests are executed. Here you could register your autoloading functions or include other php scripts. Though there's one limitation, only one bootstrap can be defined per PHPUnit configuration file.

_JsonValidatorTest.php_ is the PHP file with the test cases. It's beyond the scope to explain the content of this file in depth. As a beginner you are most likely interested in how to run the test cases so what you need to execute is simply

 `phpunit JsonValidatorTest JsonValidatorTest.php` 

You pass it the class with the test cases and the file where they're defined. That's it.

## References

*   [Official PHPUnit Manual](http://www.phpunit.de/manual/current/en/index.html)
*   [Introduction to Unit Testing with PHPUnit](http://www.slideshare.net/DragonBe/introduction-to-unit-testing-with-phpunit-presentation-705447)

Retrieved from "[https://wiki.archlinux.org/index.php?title=PHPUnit&oldid=401666](https://wiki.archlinux.org/index.php?title=PHPUnit&oldid=401666)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Development](/index.php/Category:Development "Category:Development")