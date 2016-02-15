## Contents

*   [1 Packagers](#Packagers)
    *   [1.1 Plan](#Plan)
    *   [1.2 Packages](#Packages)
    *   [1.3 Todo / Notes](#Todo_.2F_Notes)
        *   [1.3.1 common tasks](#common_tasks)
        *   [1.3.2 packages to be removed](#packages_to_be_removed)
        *   [1.3.3 packages to move with KDE](#packages_to_move_with_KDE)
*   [2 Packaging](#Packaging)
    *   [2.1 Known issues](#Known_issues)
    *   [2.2 Changes from 4.13](#Changes_from_4.13)
        *   [2.2.1 Removed packages](#Removed_packages)
        *   [2.2.2 New packages](#New_packages)
    *   [2.3 Broken packages which are not part of KDE SC](#Broken_packages_which_are_not_part_of_KDE_SC)

# Packagers

## Plan

1.  check for new/removed dependencies
2.  check for new/removed sub modules
    1.  check if we should probably add some replaces
3.  recheck kde-meta
4.  review build logs
5.  review namcap logs
6.  check packages which are not part of KDE SC but depend on it
7.  check packages which depends on split libraries

## Packages

*   kdeaccessibility-kmag (miss libkdeaccessibilityclient, it hasn't a stable release)
*   kdebindings-kimono (miss soprano, nepomuk, akonadi bindings)
*   kdebindings-kross (miss falcon)
*   kdebindings-perlkde (miss akonadi)
*   kdebindings-smokekde (miss akonadi)
*   kdeedu-kig (miss boost-python?)
*   kdeedu-kstars (miss xplanet, astrometry)
*   kdeedu-marble (miss libshp, qextserialport, libwlocate, it hasn't a stable release)
*   kdenetwork-kopete (miss XMSS, libmeanwhile)

## Todo / Notes

### common tasks

*   change url to application homepage (e.g. [http://kde.org/applications/utilities/ark/](http://kde.org/applications/utilities/ark/) or [https://projects.kde.org/projects/kde/kdemultimedia/libkcddb](https://projects.kde.org/projects/kde/kdemultimedia/libkcddb) instead of just kde.org)
*   check this Bug report: [https://bugs.kde.org/show_bug.cgi?id=189465](https://bugs.kde.org/show_bug.cgi?id=189465)
*   update [KDE](/index.php/KDE "KDE") and [KDE Packages](/index.php/KDE_Packages "KDE Packages")

### packages to be removed

### packages to move with KDE

*   akonadi
*   libkgapi

# Packaging

## Known issues

If any problem occurs try a new user or (re)move ~/.kde4 /tmp/kde-* /var/tmp/kdecache-*

*   Nepomuk does not work in application X: KDE SC 4.13 has been built without Nepomuk support.

## Changes from 4.13

### Removed packages

### New packages

## Broken packages which are not part of KDE SC

*   digikam (must be rebuilt with newer kdeedu-marble)