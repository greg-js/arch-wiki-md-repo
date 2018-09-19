## Contents

*   [1 Summary](#Summary)
*   [2 Owner](#Owner)
*   [3 Current status](#Current_status)
*   [4 Description](#Description)
    *   [4.1 Git repository layout](#Git_repository_layout)
    *   [4.2 dbscripts](#dbscripts)
        *   [4.2.1 Addition of a package](#Addition_of_a_package)
        *   [4.2.2 Removal of a package](#Removal_of_a_package)
        *   [4.2.3 Moving of a package](#Moving_of_a_package)
    *   [4.3 devtools](#devtools)
    *   [4.4 abs](#abs)
*   [5 Testing](#Testing)
*   [6 Migration](#Migration)
*   [7 Security](#Security)

## Summary

The goal is to move away from using svn internally to manage PKGBUILDs to using git. This enables developers to use tools they are more familiare with and facilitate future outside contributions.

*   Kanboard: [https://kanboard.archlinux.org/public/board/79027046d03d974519740f759f4c7a4cdb6edd6ef4683fb123aa1f148882](https://kanboard.archlinux.org/public/board/79027046d03d974519740f759f4c7a4cdb6edd6ef4683fb123aa1f148882)
*   Project repo: TBA

## Owner

*   Name: [User:eschwartz](/index.php/User:Eschwartz "User:Eschwartz")
*   Name: [User:brtln](/index.php?title=User:Brtln&action=edit&redlink=1 "User:Brtln (page does not exist)")

## Current status

*   First meeting help 17th of September 2018
    *   Project leaders decided

## Description

### Git repository layout

The proposal is to have one repository for each package. This enables packagers to decide on their own workflow, like having a branch for testing and proposed changes or rework of packages. Managing one repository with 10,000 sub directories would leave developers with less options and create a somewhat large repository (See homebrew, void linux or gentoo).

On the server this would be maintained inside one directory, and ACL would be applied to keep permissions consistent between packager roles.

```
/srv/git/repos/*.git

```

Tagging is required on the repository, and most likely enforced to a format that resembles the package format. This helps us keep track of changes, and

```
${epoch}:${pkgver}-${pkgrel}

```

dbscripts would maintain a separate git repository responsible for keeping track of the package version between releases. Each pkgbase is represented as a file denoting the package version. This repository is tagged with an incremental value in the same fashion as todays SVN repository.

```
dbscripts
└── x86_64
    ├── community
    │   └── ...
    ├── core
    │   ├── bash
    │   ├── linux
    │   └── vim
    └── extra
        └── ...

```
 `/srv/dbscripts/x86_64/core/bash`  `bash 4.4.023-1` 

### dbscripts

The proposal is to move *pkg to dbscripts for easier testing, development and migration for git migrations. ((might be moved to the debug package proposal))

#### Addition of a package

#### Removal of a package

#### Moving of a package

### devtools

### abs

How will asp/abs look for users?

## Testing

## Migration

For every directory in our svn repositority (svn-community/svn-packages) a git repository has to be created. Anthraxx has created a svn to git migration [script](https://github.com/anthraxx/arch-svn-package-to-git).

Open points:

*   How do we track which package was from which repo ([core]/[extra])?
*   How do we populate the dbscripts database?

Software dependent on svn and requiring migration:

*   arch-commits - svn hook and perl script maintained in infrastructure.git
*   archweb - [populate_signoffs hook](https://git.archlinux.org/archweb.git/tree/packages/management/commands/populate_signoffs.py), fetches commit message from svn to be shown in signoffs)
*   infrastructure - disable [svnlog](https://git.archlinux.org/infrastructure.git/tree/roles/dbscripts/files/svnlog), arch-svntogit

## Security

*   Enforce git signed commits
*   Verify git signed commits in a git hook and against the keys in the pacman keyring.
*   Disallow force pushes
*   Use git tags to match the checksum of the uploaded PKGBUILD with the built package