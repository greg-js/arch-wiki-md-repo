## Contents

*   [1 Current setup](#Current_setup)
    *   [1.1 luna.archlinux.org](#luna.archlinux.org)
    *   [1.2 nymeria.archlinux.org](#nymeria.archlinux.org)
    *   [1.3 dragon.archlinux.org](#dragon.archlinux.org)
    *   [1.4 alberich.archlinux.org](#alberich.archlinux.org)
    *   [1.5 gudrun.archlinux.org [turned off]](#gudrun.archlinux.org_.5Bturned_off.5D)
    *   [1.6 gerolde.archlinux.org [turned off]](#gerolde.archlinux.org_.5Bturned_off.5D)
    *   [1.7 celestia.archlinux.org [turned off]](#celestia.archlinux.org_.5Bturned_off.5D)
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

*   mail [turned off]
*   repos/rsync [turned off]

## dragon.archlinux.org

*   backups. still in use until nymeria/luna are turned off

## alberich.archlinux.org

*   releng stuff. no idea
*   tracker

## gudrun.archlinux.org [turned off]

*   planet [turned off]
*   bugs [turned off]
*   archweb [turned off]
*   patchwork [turned off]
*   projects [turned off]

## gerolde.archlinux.org [turned off]

## celestia.archlinux.org [turned off]

*   pkgbuild.com

# Desired setup

## vostok.archlinux.org (Intel Xeon E3-1245 2 x 3 TB 16GB ECC RAM)

*   backups [done]

## apollo.archlinux.org ([[1]](https://www.hetzner.de/de/hosting/produkte_rootserver/px61ssd))

*   bbs [wip]
*   wiki [wip]
*   aur
*   mailman
*   planet [done]
*   bugs [done]
*   archweb [done]
*   patchwork [wip]
*   projects

## soyuz.archlinux.org ([[2]](https://www.hetzner.de/de/hosting/produkte_rootserver/px61ssd))

NOTE: Talk to heftig about server specs before ordering.

*   pkgbuild.com [done]
*   releng stuff. no idea
*   tracker. no idea

## orion.archlinux.org (Intel Xeon E3-1245V2 32GB ECC 2x3TB)

*   repos/rsync [done]
*   sources [done]
*   archive
*   mail [done]

# Plan of attack

*   Get new servers (2 [px61-ssd](https://www.hetzner.de/de/hosting/produkte_rootserver/px61ssd))
*   Write ansible scripts for all services
*   Services are to be split into 2 servers so that one is the webhost with outside-facing stuff and one is for internal stuff
*   Delete all old stuff in the wiki about old setups

# misc TODO

*   Set up backup monitoring

*   Migrate patchwork. Reference: [https://github.com/getpatchwork/patchwork/blob/master/docs/deployment.md](https://github.com/getpatchwork/patchwork/blob/master/docs/deployment.md)
    *   Add automatic updates when patches are pushed to a repo (at the bottom of the above link)