<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 BBS migration](#BBS_migration)
    *   [1.1 State](#State)
    *   [1.2 Who](#Who)
    *   [1.3 Actionable](#Actionable)
*   [2 Keycloak](#Keycloak)
    *   [2.1 State](#State_2)
    *   [2.2 Who](#Who_2)
    *   [2.3 Actionable](#Actionable_2)
*   [3 archiso](#archiso)
    *   [3.1 State](#State_3)
    *   [3.2 Who](#Who_3)
    *   [3.3 Actionable](#Actionable_3)
*   [4 Borg backup keys](#Borg_backup_keys)
    *   [4.1 State](#State_4)
    *   [4.2 Who](#Who_4)
    *   [4.3 Actionable](#Actionable_4)
*   [5 archive mirroriing status](#archive_mirroriing_status)
    *   [5.1 State](#State_5)
    *   [5.2 Who](#Who_5)
    *   [5.3 Actionable](#Actionable_5)
*   [6 soyuz migration](#soyuz_migration)
    *   [6.1 State](#State_6)
    *   [6.2 Who](#Who_6)
    *   [6.3 Actionable](#Actionable_6)
*   [7 cloud-images](#cloud-images)
    *   [7.1 State](#State_7)
    *   [7.2 Who](#Who_7)
    *   [7.3 Actionable](#Actionable_7)
*   [8 PIA server status](#PIA_server_status)
    *   [8.1 State](#State_8)
    *   [8.2 Who](#Who_8)
    *   [8.3 Actionable](#Actionable_8)
*   [9 VPS](#VPS)
    *   [9.1 State](#State_9)
    *   [9.2 Who](#Who_9)
    *   [9.3 Actionable](#Actionable_9)
*   [10 AWX](#AWX)
    *   [10.1 State](#State_10)
    *   [10.2 Who](#Who_10)
    *   [10.3 Actionable](#Actionable_10)
*   [11 Forum migration](#Forum_migration)
    *   [11.1 State](#State_11)
    *   [11.2 Who](#Who_11)
    *   [11.3 Actionable](#Actionable_11)

## BBS migration

### State

*   A few issues
*   Changing your avatar does not work FS#64426

### Who

*   Jelle

### Actionable

*   Verify borg status
*   Permissions issue

## Keycloak

### State

*   Package is hardened (Thanks Levente)
*   Needs configuration

### Who

*   Sven

### Actionable

*   Investigate using ansible/terraform for configuration and making it work with GitLab (See wip/gitlab and wip/keycloak branches)

## archiso

### State

*   Gerardo stopped as main maintainer of archiso
*   Pierres wrote that he is willing to do adhoc patching, not maintenance.

### Who

*   Jelle

### Actionable

*   Mail to arch-dev-public who is interested in maintaining

## Borg backup keys

### State

*   Borg backup keys are only stored on the machines which are backed up

### Who

*   Grazzolini

### Actionable

*   Figure out how all of the devops team can have the private backup keys on his own machine or add it to the vault
*   We currently have a playbook to download the keys playbooks/tasks/fetch-borg-keys.yml

## archive mirroriing status

### State

*   Done

### Who

*   Sven

### Actionable

*   Nothing

## soyuz migration

### State

*   Nothing new

### Who

*   Sven

### Actionable

*   Create the public_html VPS
*   arch-boxes/docker

## cloud-images

### State

*   Shibumi wants to host cloud images publicly and needs hosting for it.

### Who

*   Grazzolini

### Actionable

*   Respond to shibumi's email regarding the cloud images server space hosting
*   Get more users on the vagrant organisation

## PIA server status

### State

*   Mex.mirror.pkgbuild.com has died (due to a disk failure)
*   Unable to reach PIA about this server

### Who

*   Jelle/Grazzolini

### Actionable

*   Get in contact with PIA

## VPS

### State

*   is fstrim required on the hetzner cloud vps?
*   backups, logrotate, man-db, updatedb, and sa-update all running at the same time seems suboptimal.

### Who

*   Jelle

### Actionable

*   All our hetzner vps's use localstorage so we need to use fstrim
*   Use randomizeddelay / change backup time

## AWX

### State

*   Grazzolini wants to setup AWX for playbook checking

### Who

*   Grazzolini

### Actionable

*   Discuss whether to use AWX in production

## Forum migration

### State

Some forum alternatives:

*   dlang forum
*   [https://github.com/rafalp/Misago](https://github.com/rafalp/Misago)
*   [https://github.com/thredded/thredded](https://github.com/thredded/thredded)

### Who

No one.

### Actionable

*   No-one