<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 AUR](#AUR)
    *   [1.1 State](#State)
    *   [1.2 Who](#Who)
    *   [1.3 Actionable](#Actionable)
*   [2 IPXE](#IPXE)
    *   [2.1 State](#State_2)
    *   [2.2 Who](#Who_2)
    *   [2.3 Actionable](#Actionable_2)
*   [3 Soyuz retired](#Soyuz_retired)
    *   [3.1 State](#State_3)
    *   [3.2 Who](#Who_3)
    *   [3.3 Actionable](#Actionable_3)
*   [4 Backups homedir](#Backups_homedir)
    *   [4.1 State](#State_4)
    *   [4.2 Who](#Who_4)
    *   [4.3 Actionable](#Actionable_4)
*   [5 Hetzner login changed](#Hetzner_login_changed)
    *   [5.1 State](#State_5)
    *   [5.2 Who](#Who_5)
    *   [5.3 Actionable](#Actionable_5)
*   [6 Password manager](#Password_manager)
    *   [6.1 State](#State_6)
    *   [6.2 Who](#Who_6)
    *   [6.3 Actionable](#Actionable_6)

## AUR

### State

*   sshd role stuff has been figured out and will soon be committed in Git
*   Cgit stuff has been discussed with the AUR team but they haven't responded yet. For now we will package it and look for a maintainer for it (possible eworm who maintains cgit too)

### Who

*   grazollini

### Actionable

*   Package cgit
*   Commit sshd AUR include

## IPXE

### State

*   The SSL cipher issue has been fixed by creating a new subdomain ipxe.archlinux.org with a weaker ciphers.

### Who

*   Grazollini and Sangy

### Actionable

We might want to put a notice that we use a weaker chiper for IPXE

## Soyuz retired

### State

*   Soyuz has been retired, we still have backups if people need them

### Who

*   Svenstaro

### Actionable

None

## Backups homedir

### State

*   Svenstaro and sangy will discuss how to implement a solution Saturday.

### Who

*   Svenstaro, sangyo

### Actionable

Support multiple btrfs volumes when backing up

## Hetzner login changed

### State

*   We had to switch to a different login name for our Hetzner login from username to email address.

### Who

*   Svenstaro

### Actionable

None

## Password manager

### State

*   Currently the ansible vault is (ab)used as password manager, but limits us to not allow sharing sharing the passwords of some services such as pypi for pyalpm.

### Who

*   Jelly, Grazollini

### Actionable

Find a password manager to use for the whole Arch team:

*   password-store
*   keepass
*   gopass