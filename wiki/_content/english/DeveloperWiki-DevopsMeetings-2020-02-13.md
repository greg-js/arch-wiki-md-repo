<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 AUR progress](#AUR_progress)
    *   [1.1 State](#State)
    *   [1.2 Who](#Who)
    *   [1.3 Actionable](#Actionable)
*   [2 Mailman 3](#Mailman_3)
    *   [2.1 State](#State_2)
    *   [2.2 Who](#Who_2)
    *   [2.3 Actionable](#Actionable_2)
*   [3 Keycloak progress](#Keycloak_progress)
    *   [3.1 State](#State_3)
    *   [3.2 Who](#Who_3)
    *   [3.3 Actionable](#Actionable_3)
*   [4 Rsync.net offsite backups](#Rsync.net_offsite_backups)
    *   [4.1 State](#State_4)
    *   [4.2 Who](#Who_4)
    *   [4.3 Actionable](#Actionable_4)
*   [5 Ansible testing](#Ansible_testing)
    *   [5.1 State](#State_5)
    *   [5.2 Who](#Who_5)
    *   [5.3 Actionable](#Actionable_5)

## AUR progress

### State

*   Everything is done for the ansible role [https://git.archlinux.org/infrastructure.git/log/?h=wip/aur](https://git.archlinux.org/infrastructure.git/log/?h=wip/aur)

### Who

*   grazzolini

### Actionable

*   Set a new password on the MySQL DB
*   Create a new vps to host the AUR, change the postfwd role to give the newly created AUR user unlimited sending
*   The AUR will be migrated next week

## Mailman 3

### State

*   mailman is fully packaged in community-testing
*   mailman needs to ansible'd
*   check if bounce handling is already in a release

### Who

*   jelle/dvzrv

### Actionable

*   Test if we can migrate our lists

## Keycloak progress

### State

*   We made progress with keycloak and gitlab and currently svenstaro is re-deploying the Keycloak to test if it fully works
*   The gitlab admins roles are added from Keycloak
*   mediawiki does not verify emails on signup
*   AUR requires verification of the email address of an account.
*   [sso migration wiki](https://wiki.archlinux.org/index.php/DeveloperWiki:SSOMigration)

### Who

*   svenstaro

### Actionable

*   Finish re-deploying and check if everything works.

## Rsync.net offsite backups

### State

*   We have a payed rsync.net account and paid for by the SPI and we have 10TB's

### Who

*   svenstaro

### Actionable

*   Give access to all other devops
*   Change the email to everything all devops can join
*   Actual make use of rsync.net for offsite backups

## Ansible testing

### State

*   Shibumi wrote a blog about testing our [infrastructure roles](https://nullday.de/posts/tests-for-the-arch-linux-infrastructure/)

### Who

*   anyone

### Actionable

*   Figure out how we can get some basic tests running
*   Get tests merged/documented