# Trac

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

From the [project web page](http://trac.edgewall.org):

Trac is an enhanced wiki and issue tracking system for software development projects. Trac uses a minimalistic approach to web-based software project management. Our mission is to help developers write great software while staying out of the way. Trac should impose as little as possible on a team's established development process and policies.

## Contents

*   [1 Installation](#Installation)
*   [2 Getting Started Quickly](#Getting_Started_Quickly)
    *   [2.1 Create and Initialize an Environment](#Create_and_Initialize_an_Environment)
    *   [2.2 Configure the systemd Service File](#Configure_the_systemd_Service_File)
    *   [2.3 Viewing Webserver](#Viewing_Webserver)
*   [3 Next Steps](#Next_Steps)
    *   [3.1 Trac User](#Trac_User)
    *   [3.2 Users and Permissions within Trac](#Users_and_Permissions_within_Trac)
    *   [3.3 Further Examples](#Further_Examples)

## Installation

[Install](/index.php/Install "Install") the [trac](https://www.archlinux.org/packages/?name=trac) package. Configuration is done on a per-environment basis. See below on how to create an environment. Detailed instructions can be found at [http://trac.edgewall.org/wiki/TracGuide](http://trac.edgewall.org/wiki/TracGuide).

## Getting Started Quickly

### Create and Initialize an Environment

Initialize an environment

```
# cd /srv/;
# mkdir tracenv;
# trac-admin /srv/tracenv initenv;

```

The environment configuration can be found at `/srv/tracenv/conf/trac.ini`.

### Configure the [systemd](/index.php/Systemd "Systemd") Service File

A default service file is located at `/usr/lib/systemd/system/tracd.service`. Copy this file to `/etc/systemd/system/tracd.service`, and edit it to point to your new environment. The `ExecStart` entry should look something like this:

```
ExecStart=/usr/bin/tracd -b localhost -p 8080 /srv/tracenv

```

### Viewing Webserver

After [Starting](/index.php/Start "Start") (and optionally [enabling](/index.php/Enabling "Enabling")) the service (or running `/usr/bin/tracd` directly), you can view the web interface at `[http://localhost:8080](http://localhost:8080)` using a web browser.

## Next Steps

### Trac User

It is a good idea to create a [user](/index.php/User "User") specially for the trac service. Once that user is created, you can create the environment using that user:

```
# cd /srv/;
# mkdir tracenv;
# chown trac:trac tracenv;
# sudo -u trac trac-admin /srv/tracenv initenv;

```

Add the following to the systemd unit file to make sure it is started as the `trac` user:

```
[Service]
User=trac
Group=trac

```

### Users and Permissions within Trac

(This section refers to creating users within the trac environment rather than GNU/Linux users.)

Next, you'll want to add users and give permissions to those users. To add users, see [http://trac.edgewall.org/wiki/TracStandalone#UsingAuthentication](http://trac.edgewall.org/wiki/TracStandalone#UsingAuthentication) (you will have to change your `.service` file to refer to the authentication mechanism you choose). To grant permissions to users, run the following on the trac server:

```
# trac-admin /srv/tracenv permission add <username> TRAC_ADMIN

```

### Further Examples

For a specific use case, see [SCM Example Trac](/index.php/SCM_Example_Trac "SCM Example Trac").

Retrieved from "[https://wiki.archlinux.org/index.php?title=Trac&oldid=399598](https://wiki.archlinux.org/index.php?title=Trac&oldid=399598)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Web server](/index.php/Category:Web_server "Category:Web server")