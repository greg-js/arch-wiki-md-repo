# Jenkins

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[Jenkins](https://jenkins-ci.org/) is a continuous integration server: basically it is a Java application that compiles your software and runs tests on it. Note that applications do not have to contain any Java themselves, so you can benefit from it for PHP applications, Node.js, etc.

## Installation and usage

[Install](/index.php/Install "Install") the [jenkins](https://www.archlinux.org/packages/?name=jenkins) package.

The configuration file is located in `/etc/conf.d/jenkins`.

[Start](/index.php/Start "Start") and possibly [enable](/index.php/Enable "Enable") `jenkins.service`.

You can now log into your jenkins at `http://localhost:8090`.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Jenkins&oldid=391153](https://wiki.archlinux.org/index.php?title=Jenkins&oldid=391153)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Package development](/index.php/Category:Package_development "Category:Package development")
*   [Web server](/index.php/Category:Web_server "Category:Web server")