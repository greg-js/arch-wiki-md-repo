<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 borg backup keys](#borg_backup_keys)
    *   [1.1 State](#State)
    *   [1.2 Who](#Who)
    *   [1.3 Actionable](#Actionable)
*   [2 homedir server review](#homedir_server_review)
    *   [2.1 State](#State_2)
    *   [2.2 Who](#Who_2)
    *   [2.3 Actionable](#Actionable_2)
*   [3 enabling linger for everyone](#enabling_linger_for_everyone)
    *   [3.1 State](#State_3)
    *   [3.2 Who](#Who_3)
    *   [3.3 Actionable](#Actionable_3)
*   [4 rsync.net](#rsync.net)
    *   [4.1 State](#State_4)
    *   [4.2 Who](#Who_4)
    *   [4.3 Actionable](#Actionable_4)
*   [5 zabbix problems/upgrading servers](#zabbix_problems/upgrading_servers)
    *   [5.1 State](#State_5)
    *   [5.2 Who](#Who_5)
    *   [5.3 Actionable](#Actionable_5)
*   [6 soyuz migration](#soyuz_migration)
    *   [6.1 State](#State_6)
    *   [6.2 Who](#Who_6)
    *   [6.3 Actionable](#Actionable_6)
*   [7 AUR ansiblification](#AUR_ansiblification)
    *   [7.1 State](#State_7)
    *   [7.2 Who](#Who_7)
    *   [7.3 Actionable](#Actionable_7)
*   [8 PIA boxes](#PIA_boxes)
    *   [8.1 State](#State_8)
    *   [8.2 Who](#Who_8)
    *   [8.3 Actionable](#Actionable_8)
*   [9 Moving flyspray to a VPS](#Moving_flyspray_to_a_VPS)
    *   [9.1 State](#State_9)
    *   [9.2 Who](#Who_9)
    *   [9.3 Actionable](#Actionable_9)

## borg backup keys

### State

*   Everyone developer has to fetch the borg keys locally

### Who

*   Everyone

### Actionable

*   Document how devops can download the borg backup keys on their machine

## homedir server review

### State

*   Migrated and has a new server now but no backups are created

### Who

*   ???

### Actionable

*   Extend the borg backup script to also backup the home directory on homedir.archlinux.org

## enabling linger for everyone

### State

*   Deferred for now

### Who

*   None

### Actionable

## rsync.net

### State

*   Nothing new

### Who

*   Svenstaro

### Actionable

## zabbix problems/upgrading servers

### State

*   Upgrade issue with firewalld when you upgrade the kernel and run checkservices (firewalld

### Who

### Actionable

*   OK systemd failures do not show what is fixed
*   Make notifications appear on IRC
*   Make sgp.mirror.pkgbuild.com not a build server anymore

## soyuz migration

### State

*   Only the docker service is left over on soyuz.

### Who

*   Jelle

### Actionable

Blockers:

*   homedir.archlinux.org is not backed up right now
*   move the docker building job

## AUR ansiblification

### State

*   AUR should be ansibled

### Who

*   Jelle/grazzolini

### Actionable

*   Figure out sshd template solution.
*   Package aurweb-cgit
*   Deploy [https://aur-dev.archlinux.org/](https://aur-dev.archlinux.org/) on a CX11 vps

## PIA boxes

### State

*   Boxes are dying

### Who

*   Svenstaro

### Actionable

*   If they don't reply on our support request till the first of January remove the logo from website.

## Moving flyspray to a VPS

### State

*   Since flyspray's security record isn't great, isolate it from our other services by moving it to a VPS.

### Who

*   grazzolini

### Actionable

*   Migrate it to a VPS