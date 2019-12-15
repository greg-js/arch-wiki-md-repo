[Jenkins](https://jenkins-ci.org/) is an open source [continuous integration](https://en.wikipedia.org/wiki/Continuous_integration "wikipedia:Continuous integration") server written in [Java](/index.php/Java "Java"). It is capable of running scheduled automated builds and test suites of managed software projects. The build or tests for example may be triggered on a per commit basis or in a calendar driven manner. Jenkins thereby relies on the code being managed via a version control system (see [git](/index.php/Git "Git")) and an automated build process. Note that Jenkins is not limited to Java applications and is suitable to manage projects in all common languages. Its capabilities can be further expanded by plugins.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Setup](#Setup)
*   [3 Log in as the Jenkins user](#Log_in_as_the_Jenkins_user)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [jenkins](https://www.archlinux.org/packages/?name=jenkins) for the latest stable release or [jenkins-lts](https://aur.archlinux.org/packages/jenkins-lts/) for the long-term-support version. The package will create a Jenkins user for the daemon using systemd-sysusers.

## Setup

Project configuration can be done using the built-in web interface. To access it [start/enable](/index.php/Start/enable "Start/enable") `jenkins.service`. You can now open `[http://localhost:8090](http://localhost:8090)` with your browser and start setting up Jenkins.

The configuration file of the daemon running Jenkins is located at `/etc/conf.d/jenkins`. It is sourced by the according `.service` file and takes effect immediately after a restart.

## Log in as the Jenkins user

The home folder of the `jenkins` user is located at `/var/lib/jenkins`. The Jenkins user does not have a default shell, so if you need to log in this user (for example to manage SSH keys) you need to specify which shell you want to use:

```
# su -s /bin/bash jenkins

```

## See also

*   [Wikipedia:Jenkins_(software)](https://en.wikipedia.org/wiki/Jenkins_(software) "wikipedia:Jenkins (software)")