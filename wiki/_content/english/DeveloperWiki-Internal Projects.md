## Contents

*   [1 Introduction](#Introduction)
*   [2 Infrastructure Projects](#Infrastructure_Projects)
    *   [2.1 Developer Tooling](#Developer_Tooling)
        *   [2.1.1 TODO Items](#TODO_Items)
    *   [2.2 Mirror Control](#Mirror_Control)
        *   [2.2.1 Automated tests](#Automated_tests)
    *   [2.3 Packaging Automation](#Packaging_Automation)
    *   [2.4 Server Administration](#Server_Administration)
    *   [2.5 Developer Communication Team](#Developer_Communication_Team)
*   [3 Packaging Projects](#Packaging_Projects)
    *   [3.1 Bug Squashing](#Bug_Squashing)
    *   [3.2 Rebuild Team](#Rebuild_Team)
    *   [3.3 Package Review Team](#Package_Review_Team)
    *   [3.4 Orphan Team](#Orphan_Team)
*   [4 Web Projects](#Web_Projects)
    *   [4.1 AUR](#AUR)
    *   [4.2 BBS](#BBS)
    *   [4.3 Flyspray (bugtracker)](#Flyspray_.28bugtracker.29)
    *   [4.4 Main Site](#Main_Site)
    *   [4.5 Planet](#Planet)
    *   [4.6 Wiki](#Wiki)
*   [5 Coding Projects](#Coding_Projects)
    *   [5.1 Arch Linux Init Scripts](#Arch_Linux_Init_Scripts)
    *   [5.2 Arch Linux Release Engineering (Installer)](#Arch_Linux_Release_Engineering_.28Installer.29)
    *   [5.3 mkinitcpio](#mkinitcpio)
    *   [5.4 namcap](#namcap)
    *   [5.5 netctl](#netctl)
    *   [5.6 srcpac](#srcpac)
    *   [5.7 Pacman](#Pacman)
        *   [5.7.1 Development Team](#Development_Team)
        *   [5.7.2 Translation Team](#Translation_Team)

# Introduction

This article is part of the [DeveloperWiki](/index.php/DeveloperWiki "DeveloperWiki").

This page is meant to list a lot of the projects Arch developers keep busy with. Yes, there are things to do outside of packaging. If you are interested in anything, this page should help you get in contact with the right people. If you are looking for something to do, this is always a good place to start.

Some of these projects have dedicated discussion areas, such as the release engineering and pacman development mailing lists. Other ones are less formal- some of the communication may just be person to person emails or on the arch-dev lists if it appeals to a larger crowd. Remember that if you are interested in these less-formal projects, you should let the names listed below know so they will include you on any communication regarding the project.

# Infrastructure Projects

## Developer Tooling

Primarily developer-side tools (devtools, namcap) and server-side (db-scripts) work.

*   [Aaron Griffin](/index.php/User:Phrakture "User:Phrakture")
*   [Eric Bélanger](/index.php/User:Snowman "User:Snowman")
*   [François Charette](/index.php/User:Firmicus "User:Firmicus")
*   [Pierre Schmitz](/index.php/User:Pierre "User:Pierre")
*   [Hugo Doria](/index.php?title=User:Hdoria&action=edit&redlink=1 "User:Hdoria (page does not exist)")

### TODO Items

*   dbscripts: Rewrite db-move to allow multiple packages, getting rid of the testing2* convienence scripts
*   dbscripts: Add community repo support to db-move to let us move packages from community to core/extra and vice versa.
*   dbscripts: Add community support to the sourceballs script - needs additional logic to use alternate SVN repos
*   dbscripts: When a package is completely removed from repo, e.g. amarok-base, its sourceball remains on the server. **I have a script for that. Will send it soon. [Snowman](/index.php/User:Snowman "User:Snowman") 04:32, 6 October 2009 (EDT)**
*   dbscripts/devtools: Add support for using different compression types for packages. This way we could migrate to xz compression while keeping the old gz compressed packages.
*   dbscripts/devtools: Implement a common storage dir for packages and just link from the repo dirs. This way mirrors wont need to download every package again when it is moved from testing to extra/core.

## Mirror Control

Keep track of existing mirrors and ensure they are doing their job as good as possible (e.g. staying current). Ensure we have up to date contact information for as many mirrors as possible. Work on a tiered mirror system to relieve some stress from our primary rsync server.

*   [Roman Kyrylych](/index.php/User:Romashka "User:Romashka")
*   [Gerhard Brauer](/index.php?title=User:Gerbra&action=edit&redlink=1 "User:Gerbra (page does not exist)")

### Automated tests

*   sync state: [http://users.archlinux.de/~gerbra/mirrorcheck.html](http://users.archlinux.de/~gerbra/mirrorcheck.html)
*   additional performance tests: [http://www.archlinux.de/?page=MirrorStatus](http://www.archlinux.de/?page=MirrorStatus)
*   [Gerhard Brauer](/index.php?title=User:Gerbra&action=edit&redlink=1 "User:Gerbra (page does not exist)")
*   [Pierre Schmitz](/index.php/User:Pierre "User:Pierre")

## Packaging Automation

Automatic package generation based on changes in svn trunk. Errors should be reported to some mailing list, successful builds moved to a staging directory. Some guidelines of package moving into [extra]/[testing] should be created, for [core] we can use the current signoff procedure.

*   [Ronald van Haren](/index.php/User:Pressh "User:Pressh")
*   [Daniel Isenmann](/index.php?title=User:Ise&action=edit&redlink=1 "User:Ise (page does not exist)")
*   [Hugo Doria](/index.php?title=User:Hdoria&action=edit&redlink=1 "User:Hdoria (page does not exist)")

## Server Administration

*   [Thomas Bächler](/index.php/User:Brain0 "User:Brain0")
*   [Aaron Griffin](/index.php/User:Phrakture "User:Phrakture")
*   [Jan de Groot](/index.php?title=User:JGC&action=edit&redlink=1 "User:JGC (page does not exist)")
*   [Dan McGee](/index.php/User:Toofishes "User:Toofishes")
*   [Pierre Schmitz](/index.php/User:Pierre "User:Pierre")
*   Loui Chang (sigurd)

## Developer Communication Team

This isn't quite infrastructure, but it almost belongs here. Responsible for organizing developer meetings and making sure people attempt to be present; you newer guys might have no idea, but we used to actually schedule and have 80% of the developer staff present in IRC for 1-2 hour meetings. Responsible for any other coordination between developers, TUs, and maybe even the front page news.

*   [Aaron Griffin](/index.php/User:Phrakture "User:Phrakture")
*   [James Rayner](/index.php/User:Iphitus "User:Iphitus") -I can work on the Status Reports too if Aaron doesn't have time. I'll do dev meetings if nobody steps up.

# Packaging Projects

## Bug Squashing

Responsible for assigning bugs to package maintainers. If something is trivial and a fix can be easily made, then goes and does it. Organizes bug squashing days.

*   [Paul Mattal](/index.php?title=User:Pjmattal&action=edit&redlink=1 "User:Pjmattal (page does not exist)")
*   [Roman Kyrylych](/index.php/User:Romashka "User:Romashka")
*   ...
*   (needs several people)

## Rebuild Team

Responsible for communicating and determining what rebuilds will cycle through [testing] and in what order. They are probably also the people doing large portions of the rebuilds.

*   [Allan McRae](/index.php/User:Allan "User:Allan") (because my packages seem to cause big rebuilds...)
*   [Eric Bélanger](/index.php/User:Snowman "User:Snowman")
*   [James Rayner](/index.php/User:Iphitus "User:Iphitus") - may be able to do some building for rebuilds if it's not near exams/assessment.
*   Andreas Radke - when OpenOffice is done all the rest is fun - quad core + tmpfs ftw :)

## Package Review Team

Some packages in our repos receive little attention due to not being updated frequently. These need to be checked for being able to build (especially after major toolchain updates) and compliance with current packaging standards. It would be good for packages that have not been rebuilt in a long time to be rebuilt to take advantage of new optimisations.

## Orphan Team

Responsible for caring for those packages that no one seems to want and are being neglected. This may involve adoption by themselves or finding a foster caregiver, moving them to a willing maintainer in [community], or sending them to the AUR (or the trash).

*   [Eric Bélanger](/index.php/User:Snowman "User:Snowman") (for trivial upstream update)
*   [Giovanni Scafora](/index.php?title=User:Giovanni&action=edit&redlink=1 "User:Giovanni (page does not exist)")

# Web Projects

This is meant to be a quick overview of the web projects we have and who works on them. For more technical details, you will want to check out the [DeveloperWiki:Gudrun (web)](/index.php/DeveloperWiki:Gudrun_(web) "DeveloperWiki:Gudrun (web)") and [Category:DeveloperWiki:Server Configuration](/index.php/Category:DeveloperWiki:Server_Configuration "Category:DeveloperWiki:Server Configuration") pages.

*   [Pierre Schmitz](/index.php/User:Pierre "User:Pierre")

## AUR

Responsible for coding and deploying the AUR.

*   Lukas Fleischer

## BBS

Responsible for keeping our BBS install up to date and secure.

*   [Pierre Schmitz](/index.php/User:Pierre "User:Pierre")

## Flyspray (bugtracker)

Responsible for keeping our flyspray install up to date and secure.

*   [Roman Kyrylych](/index.php/User:Romashka "User:Romashka")

## Main Site

There are a lot of issues, things that need cleaned up, etc. Take a look at the bug tracker [Web Site](https://bugs.archlinux.org/index.php?project=1&cat%5B%5D=7&status%5B%5D=open&do=index) category.

*   [Dusty Phillips](/index.php?title=User:Dusty&action=edit&redlink=1 "User:Dusty (page does not exist)")
*   [Dan McGee](/index.php/User:Toofishes "User:Toofishes")
*   [Paul Mattal](/index.php?title=User:Pjmattal&action=edit&redlink=1 "User:Pjmattal (page does not exist)")

## Planet

Responsible for keeping the planet scripts updated and running.

*   Bartłomiej Piotrowski

## Wiki

Responsible for keeping our wiki install up to date and secure.

*   [Pierre Schmitz](/index.php/User:Pierre "User:Pierre")

# Coding Projects

## Arch Linux Init Scripts

The all-important scripts that make your machine go when you turn it on

*   [Thomas Bächler](/index.php/User:Brain0 "User:Brain0")
*   [Aaron Griffin](/index.php/User:Phrakture "User:Phrakture")
*   [Roman Kyrylych](/index.php/User:Romashka "User:Romashka")

## Arch Linux Release Engineering (Installer)

The Arch Linux Install Framework (AIF) and official installation ISOs

*   [Dieter Plaetinck](/index.php?title=User:Dieter_be&action=edit&redlink=1 "User:Dieter be (page does not exist)")
*   [Gerhard Brauer](/index.php?title=User:Gerbra&action=edit&redlink=1 "User:Gerbra (page does not exist)")

## mkinitcpio

We have a program to create initrds for Arch systems.

*   [Thomas Bächler](/index.php/User:Brain0 "User:Brain0")
*   [Aaron Griffin](/index.php/User:Phrakture "User:Phrakture")

## namcap

Responsible for maintaining and adding features to namcap.

*   Rémy Oudompheng

## netctl

Network connection and profiles

*   Jouke Witteveen

## srcpac

*   Andrea Scarpino

## Pacman

### Development Team

This team is responsible for general development, including new features and bugfixes, for the package manager that is a core part of Arch. Although many people contribute patches and code, the people listed here are generally the people that will be reviewing patches and making the final say as to what gets in the codebase.

*   [Dan McGee](/index.php/User:Toofishes "User:Toofishes")
*   Xavier Chantry
*   Nagy Gabor
*   [Allan McRae](/index.php/User:Allan "User:Allan") (focusing on makepkg)

### Translation Team

Pacman, as of September 2009, has been translated to 15 languages. The upkeep and maintenance of these translations is pretty much a job in itself, with the times immediately preceding a release being the busiest. Ideally this team is responsible for creating a translations branch when a string freeze is set, and then takes incoming translations, ensures they are valid, and merges them into their branch. When a release is not imminent, their focus may be on improving clarity and usefulness of existing messages.

*   [Giovanni Scafora](/index.php?title=User:Giovanni&action=edit&redlink=1 "User:Giovanni (page does not exist)")