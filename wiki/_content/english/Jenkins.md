[Jenkins](https://jenkins-ci.org/) is an open source continuous integration server written in [Java](/index.php/Java "Java"). It is capable of running scheduled automated builds and test suits of managed software projects. The build or tests for example may be triggered on a per commit basis or in a calendar driven manner. Jenkins thereby relies on the code being managed via a version control system (see [git](/index.php/Git "Git")) and an automated build process. Note that Jenkins is not limited to Java applications and is suitable to manage projects in all common languages. Its capabilities can be further expanded by plugins.

## Installation

[Install](/index.php/Install "Install") [jenkins](https://www.archlinux.org/packages/?name=jenkins) for the latest stable release or [jenkins-lts](https://aur.archlinux.org/packages/jenkins-lts/) for the long-term-support version. The package will create a Jenkins user for the daemon using systemd-sysusers.

## Setup

Project configuration can be done using the built-in web interface. To access it [start/enable](/index.php/Start/enable "Start/enable") `jenkins.service`. You can now open `[http://localhost:8090](http://localhost:8090)` with your browser and start setting up Jenkins.

The configuration file of the daemon running Jenkins is located at `/etc/conf.d/jenkins`. It is sourced by the according `.service` file and takes effect immediately after a restart.