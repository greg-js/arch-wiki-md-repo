<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Luna AUR Ansible role](#Luna_AUR_Ansible_role)
    *   [1.1 State](#State)
    *   [1.2 Who](#Who)
    *   [1.3 Actionable](#Actionable)
*   [2 Luna cgit](#Luna_cgit)
    *   [2.1 State](#State_2)
    *   [2.2 Who](#Who_2)
    *   [2.3 Actionable](#Actionable_2)
*   [3 IPXE](#IPXE)
    *   [3.1 State](#State_3)
    *   [3.2 Who](#Who_3)
    *   [3.3 Actionable](#Actionable_3)
*   [4 Backups homedir](#Backups_homedir)
    *   [4.1 State](#State_4)
    *   [4.2 Who](#Who_4)
    *   [4.3 Actionable](#Actionable_4)

## Luna AUR Ansible role

### State

*   The sshd part is missing for the migration of the AUR to ansible,

### Who

*   grazzolini

### Actionable

*   Resolve the sshd situation
*   Test the AUR with PHP 7.4
*   Deploy aur-dev to a VPS

## Luna cgit

### State

*   aurweb cgit is a custom fork

### Who

*   Grazzolini

### Actionable

*   Create cgit-aur package for [https://git.archlinux.org/users/lfleischer/cgit.git/log/?h=aurweb](https://git.archlinux.org/users/lfleischer/cgit.git/log/?h=aurweb)

## IPXE

### State

*   ipxe is currently broken due to too strong encryption (ipxe does not support anything which is not TLS_RSA_WITH_AES_256_CBC_SHA256)

### Who

*   Grazzolini and Sangy

### Actionable

*   Create a nginx redirection for all locations except the ipxe file to the main site, so we can serve only the necessary IPXE file with weaker ciphers and not all the website under ipxe.archlinux.org.

## Backups homedir

### State

*   The current backup script only back's up / and is unable to handle two btrfs mount points. homedir.archlinux.org has a / and /home (blockstorage) block parition)

### Who

*   Svenstaro/sangy

### Actionable

*   Figure out how to backup both mounted btrfs partitions (/ /home)