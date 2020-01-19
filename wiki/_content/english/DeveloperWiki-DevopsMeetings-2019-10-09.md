<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Mirroring of Arch Linux Archive](#Mirroring_of_Arch_Linux_Archive)
    *   [1.1 State](#State)
    *   [1.2 Actionable](#Actionable)
    *   [1.3 Who](#Who)
*   [2 Gitlab PoC](#Gitlab_PoC)
    *   [2.1 State](#State_2)
    *   [2.2 Actionable](#Actionable_2)
    *   [2.3 Who](#Who_2)
*   [3 Planet migration](#Planet_migration)
    *   [3.1 State](#State_3)
    *   [3.2 Actionable](#Actionable_3)
    *   [3.3 Who](#Who_3)
*   [4 Mailman 3](#Mailman_3)
    *   [4.1 State](#State_4)
    *   [4.2 Actionable](#Actionable_4)
    *   [4.3 Who](#Who_4)
*   [5 Lack of overview of services/hosts](#Lack_of_overview_of_services/hosts)
    *   [5.1 State](#State_5)
    *   [5.2 Actionable](#Actionable_5)
*   [6 Forum migration](#Forum_migration)
    *   [6.1 State](#State_6)
    *   [6.2 Actionable](#Actionable_6)
    *   [6.3 Who](#Who_5)
*   [7 Soyuz retirement](#Soyuz_retirement)
    *   [7.1 State](#State_7)
    *   [7.2 Actionable](#Actionable_7)
    *   [7.3 Who](#Who_6)
*   [8 Getting a storage box instead of vostok](#Getting_a_storage_box_instead_of_vostok)
    *   [8.1 State](#State_8)
    *   [8.2 Actionable](#Actionable_8)
    *   [8.3 Who](#Who_7)
*   [9 Backup the archive](#Backup_the_archive)
    *   [9.1 State](#State_9)
    *   [9.2 Actionable](#Actionable_9)
    *   [9.3 Who](#Who_8)
*   [10 Offsite backups](#Offsite_backups)
    *   [10.1 State](#State_10)
    *   [10.2 Actionable](#Actionable_10)
    *   [10.3 Who](#Who_9)

## Mirroring of Arch Linux Archive

### State

*   Archive not mirrored atm

### Actionable

*   runner2.archlinux.org becomes ger.mirror.pkgbuild.com
*   use all PIA boxes as public mirrors for Archive AND repos

### Who

*   svenstaro

## Gitlab PoC

### State

*   Gitlab is running

### Actionable

*   Need to re-package keyclock for better security

### Who

*   anthraxx

## Planet migration

### State

Planet is Python 2 which will become EOL

### Actionable

*   Make planet.archlinux.org part of archweb

### Who

*   jelle

## Mailman 3

### State

*   Ask fedora regarding their mailman migration
*   Blocker [https://gitlab.com/mailman/mailman/issues/343](https://gitlab.com/mailman/mailman/issues/343)

### Actionable

*   Create a package and test migration

### Who

*   Jerome

## Lack of overview of services/hosts

### State

*   Unclear where what runs

### Actionable

*   Deferred

## Forum migration

### State

*   It was decided to migrate it to a VPS

### Actionable

*   Migrate the forum to a VPS

### Who

*   jelle
*   fukawi2

## Soyuz retirement

### State

*   We are going to point internal mirroring to repos.archlinux.org
*   Create new server and migrate content for public_html.

### Actionable

*   We are going to point internal mirroring to repos.archlinux.org
*   Create new server and migrate content for public_html.

### Who

*   jelle
*   svenstaro

## Getting a storage box instead of vostok

### State

*   Move to storage box for backups (create a kanban ticket and figure out automation). We currently pay 30 euros

### Actionable

### Who

## Backup the archive

### State

*   Requires a larger backup server (currently 1.2TB free on vostok)

### Actionable

### Who

## Offsite backups

### State

*   Decide if borg will handle it or we are doubling the backup with another tool. Settle on external service:
    *   borgbase
    *   glacier
    *   online.net cold storage
    *   dedicated server

### Actionable

### Who