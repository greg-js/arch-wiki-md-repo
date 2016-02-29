**Trusted Users (TU)** are members of the community charged with keeping the AUR in working order. They maintain popular packages ([communicating with and sending patches upstream as needed](https://mailman.archlinux.org/pipermail/aur-general/2010-September/010649.html)), and votes in administrative matters. A TU is elected from active community members by current TUs in a democratic process. TUs are the only members who have a final say in the direction of the AUR.

The TUs are governed using the [TU bylaws](https://aur.archlinux.org/trusted-user/TUbylaws.html)

## Contents

*   [1 TODO list for new Trusted Users](#TODO_list_for_new_Trusted_Users)
*   [2 The TU and [unsupported]](#The_TU_and_.5Bunsupported.5D)
*   [3 The TU and [community], Guidelines for Package Maintenance](#The_TU_and_.5Bcommunity.5D.2C_Guidelines_for_Package_Maintenance)
    *   [3.1 Rules for Packages Entering the [community] Repo](#Rules_for_Packages_Entering_the_.5Bcommunity.5D_Repo)
    *   [3.2 Accessing and Updating the Repository](#Accessing_and_Updating_the_Repository)
    *   [3.3 Disowning packages](#Disowning_packages)
    *   [3.4 Moving packages from unsupported to [community]](#Moving_packages_from_unsupported_to_.5Bcommunity.5D)
    *   [3.5 Moving packages from [community] to unsupported](#Moving_packages_from_.5Bcommunity.5D_to_unsupported)
    *   [3.6 Moving packages from [community-testing] to [community]](#Moving_packages_from_.5Bcommunity-testing.5D_to_.5Bcommunity.5D)
    *   [3.7 Deleting packages from unsupported](#Deleting_packages_from_unsupported)
    *   [3.8 See also](#See_also)

## TODO list for new Trusted Users

1.  Read this entire wiki article.
2.  Read the [TU Bylaws](https://aur.archlinux.org/trusted-user/TUbylaws.html).
3.  Make sure your account details on the [AUR](/index.php/AUR "AUR") are up-to-date.
4.  Add yourself to the [Trusted Users](/index.php/Trusted_Users "Trusted Users") page.
5.  Subscribe to the public mailing list for Arch Linux development, [arch-dev-public](https://lists.archlinux.org/listinfo/arch-dev-public).
6.  Remind a [BBS admin](https://bbs.archlinux.org/userlist.php?username=&show_group=1&sort_by=username&sort_dir=ASC&search=Submit) to change your account on forums.
7.  Ask some TU for the #archlinux-tu@freenode key and hang out with us in the channel. You do not have to do this, but it would be neat since this is where most dark secrets are spilled and where many new ideas are conceived.
8.  Create a PGP key for [package signing](/index.php/Package_signing "Package signing").
9.  Send Ionuț Bîru (ibiru@archlinux.org) or Florian Pritz (bluewind@xinu.at) with all the information based on this [template](https://www.archlinux.org/trustedusers/) to have access on dev interface (archweb).
10.  Send a signed email to Florian:
    *   Attach one SSH public key. If you do not have one, use `ssh-keygen` to generate one. Check the [Using SSH Keys](/index.php/Using_SSH_Keys "Using SSH Keys") wiki page for more information about SSH keys.
    *   Ask him to whitelist you from arch-dev-public.
    *   Tell him if you want an @archlinux.org email.
11.  Ask your sponsor:
    *   to give you TU status on the AUR.
    *   to open a new task in the "Keyring" project of the bug tracker following the instructions in [this message](https://lists.archlinux.org/pipermail/arch-dev-public/2013-September/025456.html) in order to have your PGP key signed by three master key holders.
12.  Install the [devtools](https://www.archlinux.org/packages/?name=devtools) package.
13.  Make the directories `~/staging/community` and `~/staging/community-testing` (and `~/staging/multilib` if you are interested in maintaining multilib packages) on nymeria.archlinux.org. This step is **important** as the devtools scripts use this directory to process incoming packages.
14.  If you are not upgraded to a Trusted User group on bug tracker in two days, report this as a bug to arch-dev-public.
15.  Start contributing!

## The TU and [unsupported]

The TUs should also make an effort to check package submissions in UNSUPPORTED for malicious code and good PKGBUILDing standards. In around 80% of cases the PKGBUILDs in the UNSUPPORTED are very simple and can be quickly checked for sanity and malicious code by the TU team.

TUs should also check PKGBUILDs for minor mistakes, suggest corrections and improvements. The TU should endeavor to confirm that all pkgs follow the Arch Packaging Guidelines/Standards and in doing so share their skills with other package builders in an effort to raise the standard of package building across the distro.

TUs are also in an excellent position to document recommended practices.

## The TU and [community], Guidelines for Package Maintenance

### Rules for Packages Entering the [community] Repo

*   A package must not already exist in any of the Arch Linux repositories. You should take necessary precautions to ensure no other packager is in the process of promoting the same package. Double-check the AUR package comments, read the latest subject headings in [aur-general](https://mailman.archlinux.org/mailman/listinfo/aur-general), search [all projects in the bugtracker](https://bugs.archlinux.org/index.php?project=0&do=index&switch=1), [grep](https://en.wikipedia.org/wiki/Grep "wikipedia:Grep") the [Subversion log](http://svnbook.red-bean.com/en/1.7/svn.ref.svn.c.log.html), and send a quick message to the private TU [IRC channel](/index.php/IRC_channel "IRC channel").

*   Only "popular" packages may enter the repo, as defined by 1% usage from [pkgstats](https://www.archlinux.de/?page=PackageStatistics) or 10 votes on the AUR.

*   Automatic exceptions to this rule are:
    *   i18n packages
    *   accessibility packages
    *   drivers
    *   dependencies of packages who satisfy the definition of popular, including makedeps and optdeps
    *   packages that are part of a collection and are intended to be distributed together, provided a part of this collection satisfies the definition of popular

*   Any additions not covered by the above criteria must first be proposed on the aur-general mailing list, explaining the reason for the exemption (e.g. renamed package, new package). The agreement of three other TUs is required for the package to be accepted into [community]. Proposed additions from TUs with large numbers of "non-popular" packages are more likely to be rejected.

*   TUs are strongly encouraged to move packages they currently maintain from [community] if they have low usage. No enforcement will be made, although resigning TUs packages may be filtered before adoption can occur.

*   It is good practice to always bump the **pkgrel** by *1* (in other words, set it to *n + 1*) when promoting a package from AUR. This is to facilitate automatic updates for those who already have the package installed, so that they may continue to receive updates from the official channel. Another positive effect of this is that users are not warned that their local copy is newer, as is the case if a packager does reset the **pkgrel** to *1*.

### Accessing and Updating the Repository

The [community] repository now uses **devtools** which is the same system used for uploading packages to [core] and [extra], except that it uses another server `nymeria.archlinux.org` instead of `gerolde.archlinux.org`. Thus most of the instructions in [Packager Guide](/index.php/DeveloperWiki:HOWTO_Be_A_Packager "DeveloperWiki:HOWTO Be A Packager") work without any change. Information which is specific for the [community] repository (like changed URLs) have been put here. The devtools require packagers to [set the PACKAGER variable](/index.php/Arch_Build_System#Set_the_PACKAGER_variable_in_.2Fetc.2Fmakepkg.conf "Arch Build System"). This is done in `/usr/share/devtools/makepkg-{i686,x86_64}.conf` since the regular configuration file does not get placed in a clean chroot.

Initially you should do a **non-recursive checkout** of the [community] repository:

```
svn checkout -N svn+ssh://svn-community@nymeria.archlinux.org/srv/repos/svn-community/svn

```

This creates a directory named "svn" which contains nothing but a ".svn" folder.

For **checking** out, **updating** all packages or **adding** a package see the [Packager Guide](/index.php/DeveloperWiki:HOWTO_Be_A_Packager "DeveloperWiki:HOWTO Be A Packager").

To **remove** a package:

```
ssh nymeria.archlinux.org /community/db-repo-remove community arch pkgname

```

Here and in the following text, *arch* can be one of *i686* or *x86_64* which are the two architectures supported by Arch Linux.

When you are done with editing the PKGBUILD, etc., you should **commit** the changes (`svn commit`).

Build the package with `mkarchroot` or the helper scripts `extra-i686-build` and `extra-x86_64-build`.

Sign the package with `gpg --detach-sign *.pkg.tar.xz`.

When you want to **release** a package, first copy the package along with its signatures to the *staging/community* directory on *nymeria.archlinux.org* using `scp` and then **tag** the package by going to the *pkgname/trunk* directory and issuing `archrelease community-arch`. This makes an svn copy of the trunk entries in a directory named *community-i686* or *community-x86_64* indicating that this package is in the community repository for that architecture.

***Note:** In some cases, especially for community packages, an x86_64 TU might bump the pkgrel by .1 (and not +1). This indicates that the change to the PKGBUILD is x86_64 specific and i686 maintainers **should not** rebuild the package for i686\. When the TU decides to bump the pkgrel, it should be done with the usual increment of +1\. However, a previous pkgrel=2.1 must not become pkgrel=3.1 when bumped by the TU and must instead be pkgrel=3\. In a nutshell, leave dot (.) releases exclusive to the x86_64 TU's to avoid confusion.*

**Package update summary:**

*   **Update** the package directory: `svn update some-package`.
*   **Change** to the package trunk directory: `cd some-package/trunk`.
*   **Edit** the PKGBUILD, make necessary changes
*   **Build** the package: either `makechrootpkg` or `extra-i686-build` and `extra-x86_64-build`. It is **mandatory** to build in a [clean chroot](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot "DeveloperWiki:Building in a Clean Chroot").
*   **[Namcap](/index.php/Namcap "Namcap")** the PKGBUILD and the binary `pkg.tar.gz`.
*   **Commit**, **Sign**, **Copy** and **Tag** the package using `communitypkg "commit message"`. This automates the following:
    *   **Commit** the changes to trunk: `svn commit`.
    *   **Sign** the package: `gpg --detach-sign *.pkg.tar.xz`.
    *   **Copy** the package and its signature to *nymeria.archlinux.org*: `scp *.pkg.tar.xz *.pkg.tar.xz.sig nymeria.archlinux.org:staging/community/`.
    *   **Tag** the package: `archrelease community-{i686,x86_64`}.
*   **Update** the repository: `ssh nymeria.archlinux.org /community/db-update`.

Also see the *Miscellaneous* section in the [Packager Guide](/index.php/DeveloperWiki:HOWTO_Be_A_Packager "DeveloperWiki:HOWTO Be A Packager"). For the section *Avoid having to enter your password all the time* use *nymeria.archlinux.org* instead of *gerolde.archlinux.org*.

### Disowning packages

If a TU cannot or does not want to maintain a package any longer, a notice should be posted to the AUR Mailing List, so another TU can maintain it. A package can still be disowned even if no other TU wants to maintain it, but the TUs should try not to drop many packages (they should not take on more than they have time for). If a package has become obsolete or is not used any longer, it can be removed completely as well.

If a package has been removed completely, it can be uploaded once again (fresh) to UNSUPPORTED, where a regular user can maintain the package instead of the TU.

### Moving packages from unsupported to [community]

Follow the normal procedures for adding a package community, but remember to delete the corresponding package from unsupported!

### Moving packages from [community] to unsupported

Remove the package using the instructions above and upload your source to the AUR.

### Moving packages from [community-testing] to [community]

```
ssh nymeria.archlinux.org /srv/repos/svn-community/dbscripts/db-move community-testing community package

```

### Deleting packages from unsupported

There is no point in removing dummy packages, because they will be re-created in an attempt to track dependencies. If someone uploads a real package then all dependents will point to the correct place.

### See also

*   [DeveloperWiki#Packaging Guidelines](/index.php/DeveloperWiki#Packaging_Guidelines "DeveloperWiki")