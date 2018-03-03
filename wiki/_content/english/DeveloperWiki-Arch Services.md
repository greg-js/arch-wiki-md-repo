## Archweb

**Description:** Main web site.

**URI:**

*   [https://www.archlinux.org](https://www.archlinux.org)
*   [https://master-key.archlinux.org](https://master-key.archlinux.org)

**Notes:**

*   Running on gudrun.archlinux.org
*   Sources hosted on [projects.archlinux.org](https://projects.archlinux.org/archweb.git)
*   Developed in django.

## Wiki

**Description:** Documentation

**URI:** [https://wiki.archlinux.org](https://wiki.archlinux.org)

**Notes:**

#### Migration Notes

Steps taken to migrate from luna to apollo (the commands are not the exact commands used or are high level steps):

1.  ~~Change the TTL of the wiki.archlinux.org DNS record to 300 to aid the migration/rollback.~~
2.  ~~Put the wiki on luna in maintenance mode. We have a template page that is used for that.~~
3.  ~~Create a database dump using mysqldump archwiki | gzip > dump.sql~~
4.  ~~Create a tar file containing the cache, sessions and uploads dir: tar zcvf wiki-files.tar.gz cache sessions uploads~~
5.  ~~Push the mariadb role to apollo (need to restart mysqld)~~
6.  ~~Restart mysql and take the bugs.archlinux.org out of maintenance mode~~
7.  ~~Push the php-fom role to apollo (new extensions)~~
8.  ~~Push the wiki role to apollo~~
9.  ~~Manually disable the wiki services/timers (there's no DB for them to run)~~
10.  ~~Change the DNS record to point to apollo (CNAME)~~
11.  ~~Manually change the nginx config again to put the wiki on maintenance mode on apollo as well~~
12.  ~~Copy the DB dump and files from luna to apollo and extract them (use checksums)~~
13.  ~~Run mysqldump db_name < dump.sql (this takes a long time)~~
14.  ~~Extract the files to their respective directories (the role creates them)~~
15.  ~~Fix the permissions with chown -R archwiki~~
16.  ~~Run the wiki role again to take it out of maintenance and also re-enable/restart the services~~
17.  ~~Copied the missing files under /srv/http/vhosts/wiki.archlinux.org/public/images (they were on .gitignore). Copied them to the respective directory on apollo.~~
18.  ~~Check if the services are running~~
19.  Change the TTL of the wiki.archlinux.org DNS record back to the default

## Forum

**Description:** Web forum

**URI:** [https://bbs.archlinux.org](https://bbs.archlinux.org)

**Notes:**

## Bug Tracker

**Description:** Bug management system

**URI:** [https://bugs.archlinux.org](https://bugs.archlinux.org)

**Notes:**

## Projects

**Description:** Projects service provide git repositories to arch devs.

**URI:**

*   [https://projects.archlinux.org/](https://projects.archlinux.org/)
*   [ssh://gerolde.archlinux.org/](ssh://gerolde.archlinux.org/)

**Notes:**

*   Web interfaces on gudrun.
*   Git repositories on gerolde.

## AUR

**Description:** Arch Linux User Repositories

**URI:**

*   [https://aur.archlinux.org](https://aur.archlinux.org)
*   [https://aur-dev.archlinux.org](https://aur-dev.archlinux.org)

**Notes:**

## Sources

**Description:** Provide GPLv2 sources

**URI:** [https://sources.al.org](https://sources.al.org)

**Notes:**

## Planet

**Description:** Blog

**URI:** [https://planet.archlinux.org](https://planet.archlinux.org)

**Notes:**

## Lists

**Description:** Mailing list services.

**URI:**

*   [https://lists.archlinux.org](https://lists.archlinux.org)
*   [https://mailman.archlinux.org](https://mailman.archlinux.org)

**Notes:**

*   Use mailman

## Archive

**Description:** Arch Linux Archive of repositories/sources/iso.

**URI:** [https://archive.archlinux.org](https://archive.archlinux.org)

**Notes:**

*   Currently hosted on achille.seblu.net

## MX

**Description:** Mail routing

**URI:** smtp://mx.archlinux.org

**Domains:**

*   archlinux.org
*   master-key.archlinux.org

**Notes:**

*   Serveur is postfix
*   Hosted on nymeria

## DNS

**Description:** Provide DNS resolution for Arch Linux domains.

**URI:**

*   ns1.first-ns.de.
*   robotns2.second-ns.de.
*   robotns3.second-ns.com.

**Notes:**

*   We use a SAAS DNS service from hetzner.de

# Dev web space

**Description:** Developers and TU's web hosting

**URI:** [https://dev.archlinux.org](https://dev.archlinux.org)

**Notes:**

## Build Server

**Description:** Build machine for dev/tu

**URI:**

*   [https://pkgbuild.com](https://pkgbuild.com)
*   [ssh://pkgbuild.com](ssh://pkgbuild.com)

**Notes:**

*   run on celestia

## IRC

**Description:** Arch related IRC channels.

**URI:** [IRC_channel](/index.php/IRC_channel "IRC channel")

**Notes:**

## Rsync

**Description:** Sync service / Mirrors

**URI:** rsync://rsync.archlinux.org

**Notes:**