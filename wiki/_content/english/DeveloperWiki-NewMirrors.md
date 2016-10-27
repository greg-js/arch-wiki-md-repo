## Contents

*   [1 Adding a new mirror](#Adding_a_new_mirror)
*   [2 2-tier mirroring scheme](#2-tier_mirroring_scheme)
*   [3 For the mirror administrator](#For_the_mirror_administrator)
    *   [3.1 Tier 2 requirements](#Tier_2_requirements)
    *   [3.2 Tier 1 requirements](#Tier_1_requirements)
    *   [3.3 Create a feature-request](#Create_a_feature-request)
    *   [3.4 Contact info and mailing lists](#Contact_info_and_mailing_lists)
*   [4 The Arch Linux side](#The_Arch_Linux_side)
*   [5 Mirror size](#Mirror_size)

### Adding a new mirror

This text should outline the procedure for adding a new mirror for Arch packages.

## 2-tier mirroring scheme

Due to the high load and bandwidth limits Arch Linux uses 2-tier mirroring scheme.

There are few tier 1 mirrors that sync directly from archlinux.org every hour.

All other mirrors should sync from one of tier 1 mirrors. Syncing from archlinux.org is not allowed.

## For the mirror administrator

#### Tier 2 requirements

*   Disk-space >= 60 GB
*   Sync off a tier 1 mirror (see [https://archlinux.org/mirrors](https://archlinux.org/mirrors))
*   Sync all contents of the upstream mirror (i.e. do not sync only some repositories)
*   Do not sync more often than every hour, but you should sync at least once a day
*   Sync on a random minute so it is more likely the requests will be spaced out with other mirrors
*   Use the following [rsync](/index.php/Rsync "Rsync") options: **-rtlvH --delete-after --delay-updates --safe-links**
*   If you ever wish to send downtime notifications to our users, please use the [arch-mirrors-announce](https://mailman.archlinux.org/mailman/listinfo/arch-mirrors-announce) list. You do not need to subscribe to be able to post.
*   http support

#### Tier 1 requirements

*   Tier 2 requirements
*   Bandwidth >= 100Mbit/s
*   [rsync](/index.php/Rsync "Rsync") support
*   Proven reliability (be a tier 2 mirror for a while and have reasonable uptime, response to out-of-sync notifications etc.)

You can use rsync directly or [this script](https://git.server-speed.net/users/flo/bin/tree/syncrepo.sh) as a starting point. Please note that the script tries to minimize load and bandwidth used (about 5MiB as of 2014-01-21) in case there are no changes. Feel free to remove this check if you don't sync very often or your upstream mirror does not provide the lastupdate file.

### Create a feature-request

**Note:** We are not accepting new ftp mirrors.

Go to [https://bugs.archlinux.org](https://bugs.archlinux.org/newtask/proj1) and create a feature-request (category: mirrors) containing the following information:

*   Mirror domain name
*   Geographical location of the mirror (country)
*   URLs for supported access methods (http(s), [rsync](/index.php/Rsync "Rsync")) (no ftp)
*   Your mirror's available bandwidth
*   An administrative contact email
*   An alternative administrative contact email (optional)
*   (tier 1 mirrors) Rsync IPs so your server(s) can be allowed to sync off tier 0 (rsync.archlinux.org)
*   (tier 2 mirrors) The name of tier 1 mirror you are syncing from. You can find available tier 1 mirrors [here](https://www.archlinux.org/mirrors/) (sort using the tier column)

### Contact info and mailing lists

Feel free to join the [arch-mirrors mailing list](https://mailman.archlinux.org/mailman/listinfo/arch-mirrors) which can be used for general discussion about our mirrors. If you want to inform our users about downtime of your mirror please use the [arch-mirrors-announce](https://lists.archlinux.org/listinfo/arch-mirrors-announce) mailing list. You do not need to subscribe to be able to post to arch-mirrors-announce.

If you want to reach the Arch Linux staff for questions, you can either use the arch-mirrors list, you can open a bug report on our tracker or you can send a mail to [mirrors@archlinux.org](mailto:mirrors@archlinux.org).

## The Arch Linux side

*   Add the mirror info to the Django admin site
*   Regenerate the rsync whitelist with the gen_rsyncd.conf.pl script - only for tier 1 mirrors, or when disabling access to a previously untiered mirror (also done by an hourly cronjob)
*   Regenerate the pacman-mirrorlist package

## Mirror size

To give you an impression how much space will be needed for a mirror here are some numbers (as of 2016-10-25):

Mandatory:

*   pool (all packages) - 48GB
*   repositories (core, community, extra, testing, gnome-unstable, kde-unstable, multilib) - total ~200MB

Optional:

*   iso - 9GB (encouraged)
*   archive - 15GB (permanently frozen)
*   other - 13GB
*   sources - 50GB

Most mirrors do not sync archive, other and sources directories, but sync everything else (including temporary repositories), so usually you will need about 50GB reserved for Arch Linux mirror.

However, note that the required space may temporarily increase when a big rebuild happens and thus many packages exist twice in different versions. Please plan in a buffer of 30GB to 50GB on top of the above mentioned values.