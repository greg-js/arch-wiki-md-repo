## Contents

*   [1 Specs](#Specs)
*   [2 Partition layout](#Partition_layout)
*   [3 Services](#Services)
*   [4 Maintainer](#Maintainer)
*   [5 Trivia](#Trivia)
*   [6 History](#History)

## Specs

*   Intel Dual E2160
*   4GB Ram
*   2x500GB HDD as Raid1
*   5TB Traffic
*   100Mbit/s Uplink

## Partition layout

/dev/sda1 and /dev/sdb1 10 GB -> /dev/md1; contains /

/dev/sda2 and /dev/sdb2 1 GB -> /dev/md2; swap

/dev/sda3 and /dev/sdb3 rest of space -> /dev/md3; /home

## Services

*   ssh

## Maintainer

System (sudo): ioni,bluewind

## Trivia

*   bootloader is [syslinux](/index.php/Syslinux "Syslinux")

## History