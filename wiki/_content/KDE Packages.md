# KDE Packages

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Pacman#Installing packages](/index.php/Pacman#Installing_packages "Pacman").**

**Notes:** Content unrelated to pacman should probably go in [Creating packages](/index.php/Creating_packages "Creating packages"). (Discuss in [Talk:KDE Packages#Outdated package names](https://wiki.archlinux.org/index.php/Talk:KDE_Packages#Outdated_package_names))

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** KDE Plasma 4 is unmaintained since August 2015\. This article needs to be updated for Plasma 5, Frameworks and Applications. (Discuss in [Talk:KDE Packages#](https://wiki.archlinux.org/index.php/Talk:KDE_Packages))

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** [pacman](/index.php/Pacman "Pacman") commands should be removed as per [Help:Style#Package_management_instructions](/index.php/Help:Style#Package_management_instructions "Help:Style"). (Discuss in [Talk:KDE Packages#](https://wiki.archlinux.org/index.php/Talk:KDE_Packages))

Related articles

*   [KDE](/index.php/KDE "KDE")

Since KDE SC 4.3, separate (split) packages for each application are provided. This article describes the concepts of groups and meta-packages.

## Contents

*   [1 Terminology](#Terminology)
    *   [1.1 Why use groups?](#Why_use_groups.3F)
        *   [1.1.1 Advantages](#Advantages)
        *   [1.1.2 Disadvantages](#Disadvantages)
    *   [1.2 Who is it for?](#Who_is_it_for.3F)
    *   [1.3 Why use meta-packages?](#Why_use_meta-packages.3F)
        *   [1.3.1 Advantages](#Advantages_2)
        *   [1.3.2 Disadvantages](#Disadvantages_2)
    *   [1.4 Who is it for?](#Who_is_it_for.3F_2)
*   [2 Listing the member packages](#Listing_the_member_packages)

## Terminology

**module**

The KDE software compilation source code is organized into several categories called _modules_. Examples include kdebase, kdeutils etc. See the [Coordinator List](http://techbase.kde.org/Projects/Release_Team#Coordinator_List) for more details.

**package group**

A package group is simply a group of packages. [Pacman](/index.php/Pacman "Pacman") is able to select multiple packages by their group(s) during installation or removal.

**meta-package**

A meta-package is an empty package which just connects several packages by using dependencies.

### Why use groups?

#### Advantages

*   Using groups makes it easier to install or remove a set of packages. This allows you to use a single command (like above) to install or remove all packages in a module.
*   There is no hard dependency between a group and its packages. This means that there is no reason to have all member packages in a group installed. You may freely remove member packages that belong to a group without touching other member packages of the same group.

#### Disadvantages

*   [Pacman](/index.php/Pacman "Pacman") will not install any new packages that may be added to a group at a later date. For instance, if the next release of the KDE software compilation includes new applications in one or more modules, these new applications will not be automatically installed when you upgrade your system. You will have to manually install these new packages. To overcome this, use meta-packages (see next section).

### Who is it for?

Install package groups if you only want some modules of the current KDE software compilation release. Groups are also useful for those users who only want to retain some packages from a group, while opting to remove the others.

### Why use meta-packages?

#### Advantages

*   Like package groups, meta-packages make it easy to install and maintain a set of packages. This allows you to use a single command (`# pacman -S meta-package`) to install all packages in a module.
*   Use of meta-packages ensures that [pacman](/index.php/Pacman "Pacman") will install any new member packages automatically when you upgrade your system.

#### Disadvantages

*   Meta-packages have a hard dependency on all the member packages that are part of it. This means that you cannot freely remove member packages that are part of a meta-package without removing the meta-package first. For example, if you installed **kde-meta-kdebase** and would now like to remove a member package such as, **kdebase-kwrite**, you will first need to remove the meta-package before removing the member package:

```
# pacman -R kde-meta-kdebase
# pacman -R kdebase-kwrite

```

Doing this will not remove other member packages in the **kde-meta-kdebase** meta-package, but it will also no longer automatically add new packages in that module (possibly from the next release) when you upgrade the system using pacman -Syu. You may re-install **kde-meta-kdebase** meta-package at any time to return to the monolithic package behavior.

If you installed the kde-meta package, you can remove all meta-packages at once by using:

```
# pacman -R kde-meta

```

This will only remove the meta-packages and not the actual member packages.

### Who is it for?

Use meta-packages if you desire to install the entire KDE software compilation or one or more of its modules in its entirety. This ensures a smooth upgrade path by automatically adding new split packages from subsequent releases.

## Listing the member packages

To get a complete list of KDE applications use

```
pacman -Sg kde

```

Get a list of all meta packages:

```
pacman -Sg kde-meta

```

Get a list of all KDE module groups:

```
for i in $(pacman -Sqg kde-meta); do echo ${i#kde-meta-};done

```

Get a list of all KDE packages and their module group:

```
for i in $(pacman -Sqg kde-meta); do pacman -Sg ${i#kde-meta-};done

```

You could also use the web interface at [archlinux.de](https://www.archlinux.de/?page=Packages;group=5) to browse package groups.

Retrieved from "[https://wiki.archlinux.org/index.php?title=KDE_Packages&oldid=409995](https://wiki.archlinux.org/index.php?title=KDE_Packages&oldid=409995)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [KDE](/index.php/Category:KDE "Category:KDE")