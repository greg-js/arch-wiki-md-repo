# Flumotion

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:Flumotion#](https://wiki.archlinux.org/index.php/Talk:Flumotion))

[Flumotion](http://www.flumotion.net) is a streaming media server created with the backing of Fluendo. It features intuitive graphical administration tools, making the task of setting up and manipulating audio and video streams easy for even novice system administrators.

## Contents

*   [1 Installation](#Installation)
*   [2 Changing the Default User and Pass](#Changing_the_Default_User_and_Pass)
*   [3 Starting the manager](#Starting_the_manager)
*   [4 Starting the worker](#Starting_the_worker)
*   [5 Starting Config App](#Starting_Config_App)

## Installation

[Install](/index.php/Install "Install") [flumotion](https://www.archlinux.org/packages/?name=flumotion) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Changing the Default User and Pass

Run:

```
htpasswd -nb user password

```

Replace user:PSfNpHTkpTx1M with the output of htpasswd in /etc/flumotion/managers/default/planet.xml

Next, place your user and password in the proper places in /etc/flumotion/workers/default.xml

## Starting the manager

```
flumotion-manager -d 3 /etc/flumotion/managers/default/planet.xml

```

**Note:** You can specify a different PEM certificate file by passing the --certificate parameter to the manager.

## Starting the worker

```
flumotion-worker -d 3 -u user -p password

```

## Starting Config App

*   GUI: `flumotion-admin`
*   ncurses: `flumotion-admin-text`

Retrieved from "[https://wiki.archlinux.org/index.php?title=Flumotion&oldid=374386](https://wiki.archlinux.org/index.php?title=Flumotion&oldid=374386)"