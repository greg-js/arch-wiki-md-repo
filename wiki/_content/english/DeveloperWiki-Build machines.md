## Contents

*   [1 Introduction](#Introduction)
*   [2 Server Information](#Server_Information)
    *   [2.1 Server address](#Server_address)
    *   [2.2 Server purpose](#Server_purpose)
    *   [2.3 Development tools](#Development_tools)
    *   [2.4 Server admin](#Server_admin)
    *   [2.5 Gaining access](#Gaining_access)

## Introduction

This article is part of the [DeveloperWiki](/index.php/DeveloperWiki "DeveloperWiki").

## Server Information

#### Server address

*   [http://pkgbuild.com](http://pkgbuild.com)

#### Server purpose

*   PKGBUILD.com is an attempt to create a unified build environment for Arch Linux

#### Development tools

*   makechrootpkg - PKGBUILD.com uses a modified version of the standard makechrootpkg implementation that adds queueing and integrated architecture selection.
*   chrootupdate - Allows the update of all supported chroots by an otherwise unprivileged user.
*   chrootstatus - CLI version of the status indicator on the website.
*   unlock - Allows the removal of stale lockfiles by otherwise unprivileged users.
*   Users may set the makepkg.conf PACKAGER variable by creating a file called .packager in their home directory. Whatever is included on the first line of that file will replace the default packager (PKGBUILD.com Build Server).
*   Everything else falls under the standard devtools suite

#### Server admin

*   Ionut Biru (ioni/wonder)

#### Gaining access

If you need access to the build server, please send me an email at ibiru@archlinux.org with [Build Server] in the subject line.