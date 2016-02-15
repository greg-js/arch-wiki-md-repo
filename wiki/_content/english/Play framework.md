[Play framework](http://playframework.org/) is an open source web application framework, written in Java, which follows the model-view-controller architectural pattern. Build and deployment is all handled by Python scripts. It aims to optimize developer productivity by using convention over configuration, hot code reloading and display of errors in the browser.

This document describes how to configure and run your play applications on Arch Linux system.

For play framework related documentation, see [playframework.org documentation](http://playframework.org/documentation).

## Contents

*   [1 Installation](#Installation)
*   [2 Play framework usage](#Play_framework_usage)
*   [3 Configuring a play application daemon](#Configuring_a_play_application_daemon)
    *   [3.1 Instructions](#Instructions)
    *   [3.2 Configuration file](#Configuration_file)
    *   [3.3 Autorun on boot](#Autorun_on_boot)
    *   [3.4 Stop / Start / Restart a play application](#Stop_.2F_Start_.2F_Restart_a_play_application)
*   [4 References](#References)
*   [5 Other links](#Other_links)

## Installation

The package can be installed from the [AUR](/index.php/AUR "AUR"):

*   [playframework](https://aur.archlinux.org/packages/playframework/)

It provides:

*   The **Play Framework** itself ( installed in the system )
*   A **bash completion** for Play ( installed in `/etc/bash_completion.d/` )
*   A **play framework ArchLinux daemon** to help you to configure multiple instance of play applications in a more Linux way (start, stop, restart, auto start on boot...)

## Play framework usage

To use play framework, type **"play"** in commandline.

*   `play new <path>` creates a new application.
*   `play run <path>` runs a play application.
*   `play help` gives you all available commands.

With the AUR package, play is installed in `/usr/share/playframework-{version}`.

Hence some global changing state command need to be run in root. It only concerns 2 commands. Hopefully, these two commands have alternatives:

*   `play id` : you can override the play id with **"--%id"** option
*   `play install <module>` : prefer using **play dependencies** to keep modules inside each play applications (more independent).

## Configuring a play application daemon

The playframework AUR package install a generic daemon script `/etc/rc.d/skeleton_playapp` and a configuration example `/etc/conf.d/playapp_sample`.

The idea is to create a standalone daemon foreach of your play application. See instructions bellow (also available in [/etc/conf.d/playapp_sample](https://raw.github.com/gre/play-packages/master/ArchLinux_AUR/playapp_sample)):

### Instructions

**Note:** Choose a **unique daemon name _{appname}_** of your application. You could use the domain you use to run the application but replacing **_** by **.** ( example: blog_greweb_fr )

1.  Create a symlink of `/etc/rc.d/skeleton_playapp` in `/etc/rc.d/{appname}`
2.  Copy this `/etc/conf.d/playapp_sample` file in `/etc/conf.d/{appname}`
3.  Modify variables below to fit your needs.

**Example:**

```
# appname=blog_greweb_fr
# ln -s /etc/rc.d/skeleton_playapp /etc/rc.d/${appname}
# cp /etc/conf.d/playapp_sample /etc/conf.d/${appname}

```

### Configuration file

The configuration file contains variables defining your play application instance.

 `/etc/conf.d/{appname}` 

```
PLAY_APP=  # (required) Path of your play application
PLAY_USER= # (optional) The Linux user to use to run the play server. Using root if not setted
PLAY_ARGS= # (optional) The play args to run the play server with. 
           #            Setting to "--%prod" can be useful to override the play profile id
```

**Example:**

 `/etc/conf.d/blog_greweb_fr` 

```
PLAY_APP=/home/gre/sites/blog.greweb.fr
PLAY_USER=gre
PLAY_ARGS=--%prod
```

### Autorun on boot

If you want to autorun your play application on boot: add **{appname}** in the `/etc/rc.conf` **DAEMONS** variable.

You could prefix the daemon name with an **@** to run it in background.

**Example:**

 `/etc/rc.conf`  `DAEMONS=(syslog-ng network netfs crond named sshd mysqld nginx **@blog_greweb_fr**)` 

### Stop / Start / Restart a play application

You can manually stop, start or restart your application **in root**.

```
# rc.d stop ${appname}
# rc.d start ${appname}
# rc.d restart ${appname}
```

**Example:**

 `# rc.d start blog_greweb_fr` 

```
 :: Starting Play framework /home/gre/sites/blog.greweb.fr app       [BUSY] 
 ~        _            _ 
 ~  _ __ | | __ _ _  _| |
 ~ | '_ \| |/ _' | || |_|
 ~ |  __/|_|\____|\__ (_)
 ~ |_|            |__/   
 ~
 ~ play! 1.2.3, http://www.playframework.org
 ~ framework ID is prod
 ~
 ~ OK, /home/gre/sites/pro.grenlibre.fr is started
 ~ output is redirected to /home/gre/sites/blog.greweb.fr/logs/system.out
 ~ pid is 31751
 ~
```

## References

*   [Play framework website](http://playframework.org/)
*   [documentation](http://playframework.org/)
*   [mailing list](http://groups.google.com/group/play-framework)
*   [bug tracker](http://play.lighthouseapp.com/)

## Other links

*   [Video demonstration](http://blog.greweb.fr/2011/10/how-to-deploy-your-play-applications-on-archlinux-with-daemons/)