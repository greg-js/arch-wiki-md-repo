<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 BBS migration](#BBS_migration)
    *   [1.1 State](#State)
    *   [1.2 Who](#Who)
    *   [1.3 Actionable](#Actionable)
*   [2 Gitlab](#Gitlab)
    *   [2.1 State](#State_2)
    *   [2.2 Who](#Who_2)
    *   [2.3 Actionable](#Actionable_2)
*   [3 archiso](#archiso)
    *   [3.1 State](#State_3)
    *   [3.2 Who](#Who_3)
    *   [3.3 Actionable](#Actionable_3)
*   [4 Backup offsite](#Backup_offsite)
    *   [4.1 State](#State_4)
    *   [4.2 Who](#Who_4)
    *   [4.3 Actionable](#Actionable_4)
*   [5 Geo mirror location](#Geo_mirror_location)
    *   [5.1 State](#State_5)
    *   [5.2 Who](#Who_5)
    *   [5.3 Actionable](#Actionable_5)
    *   [5.4 Mirroring The Archive](#Mirroring_The_Archive)
*   [6 State](#State_6)
    *   [6.1 Who](#Who_6)
    *   [6.2 Actionable](#Actionable_6)
*   [7 Make archive of DevOps meeting notes](#Make_archive_of_DevOps_meeting_notes)
    *   [7.1 Who](#Who_7)
    *   [7.2 Actionable](#Actionable_7)

## BBS migration

### State

*   The migration was set to happen last week, but was postponed.

### Who

*   Jelle
*   fukawi2

### Actionable

*   Double check if avatars are migrated properly
*   Put cookie seed in the ansible vault
*   Set up new date for migration

## Gitlab

### State

*   Keycloak and GitLab mockup is working kind of well
*   Keycloak package's security needs to be improved

### Who

*   Jerome
*   Sven

### Actionable

*   Improve Keycloak package, set up automation for it and put it on a VPS
*   Connect GitLab to this Keycloak instance
*   Write mail to arch-devops and arch-projects

## archiso

### State

*   Gerardo stepped back as developer
*   Building/testing of archiso stuff isn't automated

### Who

*   Jelle

### Actionable

*   Revoke git access for gerardo
*   Figure out who can take over upstream development (accept patches, fixes, etc)

## Backup offsite

### State

*   Asked rsync.net and they are happy to sponsor 10TB for us
*   Waiting on reply from rsync.net

### Who

*   Sven
*   Jelle

### Actionable

*   Find out how borg restoration works and where the encryption keys are actually stored
*   Write documentation for adding a host to borg backups
*   Write documentation on how to restore on the host and if the host is lost (docs/borg.txt)

## Geo mirror location

### State

*   nginx-based approach is ok but only works for HTTP
*   Should work with rsync as well
*   foxxx0 made a patch and suggestion how to do this using PowerDNS

### Who

*   foxxx0
*   Sven

### Actionable

*   Deferred

### Mirroring The Archive

## State

*   No mirrored archives

### Who

*   Sven
*   Jelle

### Actionable

*   Make a new ansible group which are allowed in the rsync config of the archive and make the PIA boxes archive.
*   Make new ansible role for rsync clients for archive mirrors
*   Make new ansible role for rsync server on orion for archive mirror provider

## Make archive of DevOps meeting notes

### Who

*   Jelle

### Actionable

*   Make wiki page with past devops meeting notes (on the devwiki)