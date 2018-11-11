Related articles

*   [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")

**Trusted Users (TU)** are members of the community charged with keeping the AUR in working order. They maintain popular packages ([communicating with and sending patches upstream as needed](https://mailman.archlinux.org/pipermail/aur-general/2010-September/010649.html)), and vote in administrative matters. A TU is elected from active community members by current TUs in a democratic process. TUs are the only members who have a final say in the direction of the AUR.

The TUs are governed using the [TU bylaws](https://aur.archlinux.org/trusted-user/TUbylaws.html)

## Contents

*   [1 TODO list for new Trusted Users](#TODO_list_for_new_Trusted_Users)
*   [2 The TU and the AUR](#The_TU_and_the_AUR)
*   [3 The TU and [community], Guidelines for Package Maintenance](#The_TU_and_.5Bcommunity.5D.2C_Guidelines_for_Package_Maintenance)
    *   [3.1 Rules for Packages Entering the [community] Repo](#Rules_for_Packages_Entering_the_.5Bcommunity.5D_Repo)
    *   [3.2 Accessing and Updating the Repository](#Accessing_and_Updating_the_Repository)
    *   [3.3 Disowning packages](#Disowning_packages)
    *   [3.4 Moving packages from unsupported to [community]](#Moving_packages_from_unsupported_to_.5Bcommunity.5D)
    *   [3.5 Moving packages from [community] to unsupported](#Moving_packages_from_.5Bcommunity.5D_to_unsupported)
    *   [3.6 Moving packages from [community-testing] to [community]](#Moving_packages_from_.5Bcommunity-testing.5D_to_.5Bcommunity.5D)
    *   [3.7 Deleting packages from unsupported](#Deleting_packages_from_unsupported)
    *   [3.8 Remote build on PKGBUILD.com](#Remote_build_on_PKGBUILD.com)
*   [4 TODO list retiring a Trusted User](#TODO_list_retiring_a_Trusted_User)
*   [5 See also](#See_also)

## TODO list for new Trusted Users

1.  Read this entire wiki article.
2.  Read the [TU Bylaws](https://aur.archlinux.org/trusted-user/TUbylaws.html).
3.  Make sure your account details on the [AUR](/index.php/AUR "AUR") are up-to-date.
4.  Add yourself to the [Trusted Users](/index.php/Trusted_Users "Trusted Users") page.
5.  Subscribe to the public mailing list for Arch Linux development, [arch-dev-public](https://lists.archlinux.org/listinfo/arch-dev-public).
6.  Remind a [BBS admin](https://bbs.archlinux.org/userlist.php?username=&show_group=1&sort_by=username&sort_dir=ASC&search=Submit) to change your account on forums.
7.  Ask some TU for the #archlinux-tu@freenode key and hang out with us in the channel. You do not have to do this, but it would be neat since this is where most dark secrets are spilled and where many new ideas are conceived.
    *   Once in the channel, if you want an @archlinux/trusteduser/* cloak ask our [group contact](https://freenode.net/groupreg#two-types-of-group-contacts-exist-for-freenode), ioni, to get you one.
8.  Create a PGP key for [package signing](/index.php/Package_signing "Package signing") or use your existing PGP key. Make sure the key also contains an encryption subkey so you can receive encrypted verification tokens.
9.  Send a signed email to Florian Pritz (bluewind@xinu.at) or Bartłomiej Piotrowski (bpiotrowski@archlinux.org):
    *   Attach one SSH public key. If you do not have one, use `ssh-keygen` to generate one. Check the [Using SSH Keys](/index.php/Using_SSH_Keys "Using SSH Keys") wiki page for more information about SSH keys.
    *   Ask him to whitelist you from arch-dev-public.
    *   Tell him if you want an @archlinux.org email.
    *   All the information based on this [template](https://www.archlinux.org/people/trusted-users/) to have access on dev interface (archweb). If you already have an account, ask to be added to the Trusted Users group.
10.  Ask your sponsor:
    *   to give you TU status on the AUR.
    *   to open a new task in the "Keyring" project of the bug tracker following the instructions in [this message](https://lists.archlinux.org/pipermail/arch-dev-public/2013-September/025456.html) in order to have your PGP key signed by three master key holders.
11.  Install the [devtools](https://www.archlinux.org/packages/?name=devtools) package.
12.  [Configure your private ssh key](/index.php/Arch_User_Repository#Authentication "Arch User Repository") for `orion.archlinux.org` and `repos.archlinux.org` hosts.
13.  Ssh to yourname@orion.archlinux.org (once you have permissions).
14.  If you are not upgraded to a Trusted User group on bug tracker in two days, report this as a bug to arch-dev-public.
15.  Start contributing!

## The TU and the AUR

The TUs should also make an effort to check package submissions in the [AUR](/index.php/AUR "AUR") for malicious code and good PKGBUILDing standards. In around 80% of cases the PKGBUILDs in the UNSUPPORTED are very simple and can be quickly checked for sanity and malicious code by the TU team.

TUs should also check PKGBUILDs for minor mistakes, suggest corrections and improvements. The TU should endeavor to confirm that all pkgs follow the Arch Packaging Guidelines/Standards and in doing so share their skills with other package builders in an effort to raise the standard of package building across the distro.

TUs are also in an excellent position to document recommended practices.

## The TU and [community], Guidelines for Package Maintenance

### Rules for Packages Entering the [community] Repo

*   A package must not already exist in any of the Arch Linux repositories. You should take necessary precautions to ensure no other packager is in the process of promoting the same package. Double-check the AUR package comments, read the latest subject headings in [aur-general](https://mailman.archlinux.org/mailman/listinfo/aur-general), search [all projects in the bugtracker](https://bugs.archlinux.org/index.php?project=0&do=index&switch=1), [grep](https://en.wikipedia.org/wiki/Grep "wikipedia:Grep") the [Subversion log](http://svnbook.red-bean.com/en/1.7/svn.ref.svn.c.log.html), and send a quick message to the private TU [IRC channel](/index.php/IRC_channel "IRC channel").

*   AUR helpers, as a special exception, will never be permitted.

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

The [community] repository now uses **devtools** which is the same system used for uploading packages to [core] and [extra], except that it uses another server `orion.archlinux.org` instead of `gerolde.archlinux.org`. Thus most of the instructions in [Packager Guide](/index.php/DeveloperWiki:HOWTO_Be_A_Packager "DeveloperWiki:HOWTO Be A Packager") work without any change. Information which is specific for the [community] repository (like changed URLs) have been put here. The devtools require packagers to [set the PACKAGER variable](/index.php/Makepkg#Packager_information "Makepkg") in `makepkg.conf`.

Initially you should do a **non-recursive checkout** of the [community] repository:

```
svn checkout -N svn+ssh://svn-community@repos.archlinux.org/srv/repos/svn-community/svn svn-community

```

This creates a directory named "svn-community" which contains nothing but a ".svn" folder.

For **checking** out, **updating** all packages or **adding** a package see the [Packager Guide](/index.php/DeveloperWiki:HOWTO_Be_A_Packager "DeveloperWiki:HOWTO Be A Packager").

To **remove** a package:

```
ssh orion.archlinux.org /community/db-repo-remove community arch pkgname

```

Here and in the following text, *arch* should be *x86_64* which is the only architecture supported by Arch Linux since [i686 support has been deprecated](https://www.archlinux.org/news/the-end-of-i686-support/).

**Note:** If you are editing packages of the *any* architecture you can simply run the x86_64 scripts which will also work.

When you are done with editing the PKGBUILD, etc., you should **commit** the changes (`svn commit`).

Build the package with `mkarchroot` or the helper script `extra-x86_64-build`. If you want to upload to testing you also need to build with the testing script `testing-x86_64-build`.

Sign the package with `gpg --detach-sign *.pkg.tar.xz`. If you are using a different PGP key for package signing you can add it to `~/.makepkg.conf` with `GPGKEY=<identifier>`.

When you want to **release** a package, first copy the package along with its signatures to the *staging/community* directory on *orion.archlinux.org* using `scp` and then **tag** the package by going to the *pkgname/trunk* directory and issuing `archrelease community-arch`. This makes an svn copy of the trunk entries in a directory named *community-x86_64* indicating that this package is in the community repository for that architecture. Note that the staging directory is different from the staging repository and every package needs to be uploaded to the staging directory. This process can be automated with the `communitypkg` script, see the summary below.

**Package update summary:**

*   **Update** the package directory: `svn update some-package`.
*   **Change** to the package trunk directory: `cd some-package/trunk`.
*   **Edit** the PKGBUILD, make necessary changes, update hashes with `updpkgsums`.
*   **Build** the package: `makechrootpkg` or `extra-x86_64-build`. It is **mandatory** to build in a [clean chroot](/index.php/DeveloperWiki:Building_in_a_clean_chroot "DeveloperWiki:Building in a clean chroot").
*   **[Namcap](/index.php/Namcap "Namcap")** the PKGBUILD and the binary `pkg.tar.gz`.
*   **Commit**, **Sign**, **Copy** and **Tag** the package using `communitypkg "commit message"`. This automates the following:
    *   **Commit** the changes to trunk: `svn commit`.
    *   **Sign** the package: `gpg --detach-sign *.pkg.tar.xz`.
    *   **Copy** the package and its signature to *orion.archlinux.org*: `scp *.pkg.tar.xz *.pkg.tar.xz.sig orion.archlinux.org:staging/community/`.
    *   **Tag** the package: `archrelease community-x86_64`.
*   **Update** the repository: `ssh orion.archlinux.org /community/db-update`.

Also see the *Miscellaneous* section in the [Packager Guide](/index.php/DeveloperWiki:HOWTO_Be_A_Packager "DeveloperWiki:HOWTO Be A Packager") and [SSH keys#ssh-agent](/index.php/SSH_keys#ssh-agent "SSH keys"). For the section *Avoid having to enter your password all the time* use *orion.archlinux.org* instead of *gerolde.archlinux.org*.

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

### Remote build on PKGBUILD.com

**Warning:** The following procedures defeats the Web Of Trust model: a user with root access to PKGBUILD.com could alter the package and/or the signature before it gets published.

Trusted users and developers can connect to [PKGBUILD.com](http://pkgbuild.com/) via SSH to, among others, build packages using the devtools. This has numerous advantages over a local setup:

*   Builds are fast and network speed is high.
*   The environment needs setup only once.
*   Your local system need not be Arch Linux.

The process is similar to that of a local setup with devtools. Your GnuPG private is required for signing but you don't want to upload it to soyuz for obvious security reasons. As such, you'll need to forward the GnuPG agent socket from your local machine to the server: this will allow you to sign packages on soyuz without communicating your key. This also means that we need to disable the agent on the server before we can run anything.

First, connect to soyuz and disable

```
 $ ssh soyuz.archlinux.org
 $ systemctl --user mask gpg-agent.service

```

Make sure gpg-agent is not running (`systemctl --user stop gpg-agent.service`). At this point, make sure that no sockets exist in the folder pointed by `gpgconf --list-dir socketdir`. If they do, remove them or log out and in again. If you have a custom $GNUPGHOME (eg. to move it to `~/.config/gnupg`), you'll need to unset that, as it is not possible in gnupg to set the homedir without setting the socketdir. On soyuz, *StreamLocalBindUnlink yes* is set in *sshd_config*, therefore removing the sockets manually on logout is not necessary.

While the PGP private keys remain on your local machine, the public keys **must** be on soyuz. Export your public ring to soyuz, e.g. from you local machine

```
 $ scp ~/.gnupg/pubring.gpg soyuz.archlinux.org:~/.gnupg/pubring.gpg

```

SSH is required to checkout and commit to the SVN repository. You can either set up a new SSH key pair on the server (it's highly discouraged to put your local private key on soyuz for security reasons) or reuse your local keys via socket forwarding. If you opt for the latter, make sure to disable ssh-agent on soyuz if you had enabled it previously (it's not running by default).

Configure you build environment on soyuz:

 `~/.makepkg.conf` 
```
PACKAGER="John Doe <john@doe.example>"
## Optional
PKGDEST="/home/johndoe/packages"
SRCDEST="/home/johndoe/sources"
SRCPKGDEST="/home/johndoe/srcpackages"
LOGDEST="/home/johndoe/logs"
## If your PGP key is not the default, specify the right fingerprint:
GPGKEY="ABCD1234..."
```

**Warning:** Forwarding your gpg-agent socket to a remote machine makes it possible for anyone with root access to that system to use your unlocked GPG credentials. To circumvent this issue, we need to disable passphrase caching.

Disable passphrase caching with the following settings:

 `gpg-agent.conf` 
```
default-cache-ttl 0
max-cache-ttl 0

```

Because we will want to keep our usual GPG agent running with its current settings, we are going to run another GPG agent dedicated to the task at hand. Create a `~/.gnupg-archlinux` folder and symlink everything from `~/.gnupg` there, except `~/.gnupg/gpg-agent.conf`. Configure the new GPG agent:

 `~/.gnupg-archlinux` 
```
extra-socket /home/doe/.gnupg-archlinux/S.gpg-agent.extra
default-cache-ttl 0
max-cache-ttl 0
pinentry-program /usr/bin/pinentry-gtk-2

```

The `gpg-agent-extra.socket` will be forwarded to PKGBUILD.com.

Start the dedicated agent with

```
 $ gpg-agent --homedir ~/.gnupg-archlinux --daemon

```

Connect with:

```
 $ ssh -R $REMOTE_SSH_AUTH_SOCK:$SSH_AUTH_SOCK -R /run/user/$REMOTE_UID/gnupg/S.gpg-agent:/home/doe/.gnupg-archlinux/S.gpg-agent.extra soyuz.archlinux.org

```

or, if using GnuPG as your SSH agent:

```
 $ ssh -R /run/user/$REMOTE_UID/gnupg/S.gpg-agent.ssh:/run/user/$LOCAL_UID/gnupg/S.gpg-agent.ssh -R /run/user/$REMOTE_UID/gnupg/S.gpg-agent:/home/doe/.gnupg-archlinux/S.gpg-agent.extra soyuz.archlinux.org

```

Replace *$REMOTE_UID* and *$LOCAL_UID* by your user identifier as returned by `id -u` on soyuz and locally, respectively. If using ssh-agent, replace *$REMOTE_SSH_AUTH_SOCK* by the path to the SSH socket on the remote host (it can be anything).

You can make the forwarding permanent for that host. For instance with gpg-agent.ssh:

 `~/.ssh/config` 
```
Host soyuz.archlinux.org
  RemoteForward /run/user/$REMOTE_UID/gnupg/S.gpg-agent /run/user/$LOCAL_UID/gnupg/S.gpg-agent.extra
  RemoteForward /run/user/$REMOTE_UID/gnupg/S.gpg-agent.ssh /run/user/$LOCAL_UID/gnupg/S.gpg-agent.ssh

```

Again, replace *$REMOTE_UID* and *$LOCAL_UID* with their respective values.

From then on, the procedure should be exactly the same as a local build:

```
 $ ssh soyuz.archlinux.org
 $ svn checkout -N svn+[ssh://svn-community@repos.archlinux.org/srv/repos/svn-community/svn](ssh://svn-community@repos.archlinux.org/srv/repos/svn-community/svn) svn-community
 $ ...

```

**Note:** pinentry-curses might not work with socket forwarding. If it fails for you, try using a different pinentry.

## TODO list retiring a Trusted User

When a TU resigns the following list has be followed, these steps do not apply when a TU resigns but is still a Developer.

1.  All packages packaged by the retiree should be resigned (so rebuild). Packages packaged by the retiree can be found in Archweb [https://www.archlinux.org/packages/?sort=&q=&packager=$packager&flagged=](https://www.archlinux.org/packages/?sort=&q=&packager=$packager&flagged=) where packager is the username on Archweb.
2.  The account of the retiree should be disabled on Archweb and added to the 'Retired Trusted users' group. The retiree should be removed from the 'Trusted Users' and the repository permissions should be reduced to none.
3.  The shell access to our servers should be disabled. (notably repos.archlinux.org, pkgbuild.com)
4.  The GPG key should be removed and a new archlinux-keyring package should be pushed to the repos. Create bug reports in the keyring project to remove the keys of the retired Trusted Users.
5.  Remove the TU group from their AUR account.

## See also

*   [DeveloperWiki#Packaging Guidelines](/index.php/DeveloperWiki#Packaging_Guidelines "DeveloperWiki")