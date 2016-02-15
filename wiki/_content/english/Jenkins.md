[Jenkins](https://jenkins-ci.org/) is a continuous integration server: basically it is a Java application that compiles your software and runs tests on it. Note that applications do not have to contain any Java themselves, so you can benefit from it for PHP applications, Node.js, etc.

## Installation and usage

[Install](/index.php/Install "Install") the [jenkins](https://www.archlinux.org/packages/?name=jenkins) package.

The configuration file is located in `/etc/conf.d/jenkins`.

[Start](/index.php/Start "Start") and possibly [enable](/index.php/Enable "Enable") `jenkins.service`.

You can now log into your jenkins at `http://localhost:8090`.