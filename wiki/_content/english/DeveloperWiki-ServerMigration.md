## Contents

*   [1 Current setup](#Current_setup)
    *   [1.1 luna.archlinux.org](#luna.archlinux.org)
    *   [1.2 nymeria.archlinux.org](#nymeria.archlinux.org)
    *   [1.3 dragon.archlinux.org](#dragon.archlinux.org)
    *   [1.4 alberich.archlinux.org](#alberich.archlinux.org)
    *   [1.5 gudrun.archlinux.org](#gudrun.archlinux.org)
    *   [1.6 gerolde.archlinux.org](#gerolde.archlinux.org)
    *   [1.7 celestia.archlinux.org](#celestia.archlinux.org)
*   [2 Desired setup](#Desired_setup)
    *   [2.1 vostok.archlinux.org (Intel Xeon E3-1245 2 x 3 TB 16GB ECC RAM)](#vostok.archlinux.org_.28Intel_Xeon_E3-1245_2_x_3_TB_16GB_ECC_RAM.29)
    *   [2.2 apollo.archlinux.org ([1])](#apollo.archlinux.org_.28.5B1.5D.29)
    *   [2.3 soyuz.archlinux.org ([2])](#soyuz.archlinux.org_.28.5B2.5D.29)
    *   [2.4 orion.archlinux.org (Intel Xeon E3-1245V2 32GB ECC 2x3TB)](#orion.archlinux.org_.28Intel_Xeon_E3-1245V2_32GB_ECC_2x3TB.29)
*   [3 Plan of attack](#Plan_of_attack)
*   [4 misc TODO](#misc_TODO)

# Current setup

## luna.archlinux.org

*   bbs
*   wiki
*   aur
*   mailman

## nymeria.archlinux.org

*   mail
*   repos/rsync [turned off]

## dragon.archlinux.org

*   backups [turned off]

## alberich.archlinux.org

*   releng stuff. no idea
*   tracker

## gudrun.archlinux.org

*   planet [turned off]
*   bugs
*   archweb
*   patchwork
*   projects [turned off]

## gerolde.archlinux.org

## celestia.archlinux.org

*   pkgbuild.com

# Desired setup

## vostok.archlinux.org (Intel Xeon E3-1245 2 x 3 TB 16GB ECC RAM)

*   backups [done]

## apollo.archlinux.org ([[1]](https://www.hetzner.de/de/hosting/produkte_rootserver/px61ssd))

*   bbs
*   wiki
*   aur
*   mailman
*   planet [done]
*   bugs
*   archweb
*   patchwork
*   projects
*   mail

## soyuz.archlinux.org ([[2]](https://www.hetzner.de/de/hosting/produkte_rootserver/px61ssd))

NOTE: Talk to heftig about server specs before ordering.

*   pkgbuild.com
*   releng stuff. no idea
*   tracker

## orion.archlinux.org (Intel Xeon E3-1245V2 32GB ECC 2x3TB)

*   repos/rsync [done]
*   sources [done]
*   archive

# Plan of attack

*   Get new servers (2 [px61-ssd](https://www.hetzner.de/de/hosting/produkte_rootserver/px61ssd))
*   Write ansible scripts for all services
*   Services are to be split into 2 servers so that one is the webhost with outside-facing stuff and one is for internal stuff
*   Delete all old stuff in the wiki about old setups

# misc TODO

*   Run local resolving nameserver on mail server to make sure blacklist/whitelist checks are not blocked because the hetzner ns has hit some limits (install local unbound + change DNS in networkd file)

*   Set up email on vostok
*   Set up status backup checking script (ask Florian, simple find command) on vostok

*   Set up orion
    *   Migrate archive from seblu's server

*   Migrate patchwork. Reference: [https://github.com/getpatchwork/patchwork/blob/master/docs/deployment.md](https://github.com/getpatchwork/patchwork/blob/master/docs/deployment.md)
    *   Add automatic updates when patches are pushed to a repo (at the bottom of the above link)