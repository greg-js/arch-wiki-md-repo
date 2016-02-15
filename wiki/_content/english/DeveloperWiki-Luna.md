## Contents

*   [1 Specs](#Specs)
*   [2 Partition layout](#Partition_layout)
*   [3 Services](#Services)
*   [4 Maintainer](#Maintainer)
    *   [4.1 bbs.archlinux.org](#bbs.archlinux.org)
    *   [4.2 wiki.archlinux.org](#wiki.archlinux.org)
    *   [4.3 aur.archlinux.org](#aur.archlinux.org)
*   [5 Trivia](#Trivia)
*   [6 History](#History)

## Specs

*   Intel Xeon e3-1270v3
*   32GB ECC Ram
*   2x240GB SSD as Raid1
*   30TB Traffic
*   1000Mbit/s Uplink

## Partition layout

/dev/sda1 and /dev/sdb1 all the space -> /dev/md0

/dev/md0 contains an [LVM](/index.php/LVM "LVM") (vg0) which contains the following volumes:

*   home /home
*   root /
*   srv /srv
*   log /var/log
*   mysql /var/lib/mysql

## Services

*   postfix (for outbound email and mailman)
*   nginx
*   mysql
*   bbs, wiki, AUR
*   mailman

## Maintainer

System (sudo): ioni,dan,bluewind,pierre

### bbs.archlinux.org

*   Maintainer: Pierre
*   Upstream: [http://fluxbb.org/](http://fluxbb.org/)
*   Dependencies: php, mysql
*   Public git repo: [https://projects.archlinux.org/vhosts/bbs.archlinux.org.git/](https://projects.archlinux.org/vhosts/bbs.archlinux.org.git/)

### wiki.archlinux.org

*   Maintainer: Pierre
*   Upstream: [http://www.mediawiki.org/wiki/MediaWiki](http://www.mediawiki.org/wiki/MediaWiki)
*   Dependencies: php, mysql
*   Public git repo: [https://projects.archlinux.org/vhosts/wiki.archlinux.org.git/](https://projects.archlinux.org/vhosts/wiki.archlinux.org.git/)

### aur.archlinux.org

*   Maintainer: Lukas Fleischer
*   Dependencies: php, mysql
*   Public git repo: [https://projects.archlinux.org/aur.git/](https://projects.archlinux.org/aur.git/)

## Trivia

*   bootloader is [grub2](/index.php/Grub2 "Grub2") (is this still correct?)
*   network is configured via network_simple.service

## History

*   12.12.11: removed pkgbuild from alderaan
*   12.12.11: moved bbs and wiki to alderaan
*   15.12.11: moved pkgbuild to brynhild