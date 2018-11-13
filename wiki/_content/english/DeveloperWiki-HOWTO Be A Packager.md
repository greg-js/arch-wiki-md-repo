## Contents

*   [1 Follow Package Guidelines](#Follow_Package_Guidelines)
*   [2 Preparation and Setup](#Preparation_and_Setup)
    *   [2.1 Installing the Packages](#Installing_the_Packages)
    *   [2.2 SSH Config](#SSH_Config)
    *   [2.3 makepkg Config](#makepkg_Config)
    *   [2.4 Local SVN Setup using Non-Recursive Checkouts](#Local_SVN_Setup_using_Non-Recursive_Checkouts)
    *   [2.5 Helper Scripts (optional)](#Helper_Scripts_(optional))
        *   [2.5.1 ch](#ch)
*   [3 The Workflow](#The_Workflow)
    *   [3.1 Checkout/update your Local Repository](#Checkout/update_your_Local_Repository)
    *   [3.2 Adding a new Package](#Adding_a_new_Package)
    *   [3.3 Updating the needed Package](#Updating_the_needed_Package)
    *   [3.4 Change and build](#Change_and_build)
    *   [3.5 Run namcap on both PKGBUILD and Package](#Run_namcap_on_both_PKGBUILD_and_Package)
    *   [3.6 Run checkpkg on the Package](#Run_checkpkg_on_the_Package)
    *   [3.7 Use devtools to sign, upload and commit](#Use_devtools_to_sign,_upload_and_commit)
    *   [3.8 Update the Repository](#Update_the_Repository)
*   [4 Other Operations](#Other_Operations)
    *   [4.1 Removing a Package](#Removing_a_Package)
    *   [4.2 Moving a package between repos](#Moving_a_package_between_repos)
    *   [4.3 "Tagging" releases](#"Tagging"_releases)
*   [5 Miscellaneous Stuff](#Miscellaneous_Stuff)
    *   [5.1 Cleaning up your checkout](#Cleaning_up_your_checkout)
    *   [5.2 Avoid having to enter your password all the time](#Avoid_having_to_enter_your_password_all_the_time)

## Follow Package Guidelines

Package guidelines can be found in the Arch Linux documentation. Please follow them closely.

[Arch packaging standards](/index.php/Arch_packaging_standards "Arch packaging standards")

## Preparation and Setup

### Installing the Packages

Make sure you have the packages `devtools` and `namcap` installed.

### SSH Config

If you have multiple SSH keys in your SSH Agent, you will need to make sure that the correct key is being used to contact the Arch servers. Also, when your local username differs from the one being used on the Arch servers, you need to take care of that too.

Example `~/.ssh/config` excerpt:

```
host repos.archlinux.org
	hostname repos.archlinux.org
	port 22
	user foobar
	IdentityFile ~/.ssh/id_arch
	IdentitiesOnly yes

```

### makepkg Config

Make sure to configure your `~/.makepkg.conf` with the correct `PACKAGER` and `GPGKEY` variables. Wrong signatures or missing `PACKAGER` will prevent your packages from entering the repository.

```
PACKAGER="Foo Bar <foo.bar@archlinux.org>"
GPGKEY="0x0123456789abcdef"

```

### Local SVN Setup using Non-Recursive Checkouts

As SVN provides the ability to do scoped checkouts you can initialize an empty local checkout and later on only fetch the packages that you want. To setup the local checkouts run the following commands.

For core, extra, testing and staging repos:

```
  svn checkout -N svn+[ssh://svn-packages@repos.archlinux.org/srv/repos/svn-packages/svn](ssh://svn-packages@repos.archlinux.org/srv/repos/svn-packages/svn) svn-packages

```

For community, community-testing, community-staging, multilib, multilib-testing, multilib-staging:

```
  svn checkout -N svn+[ssh://svn-community@repos.archlinux.org/srv/repos/svn-community/svn](ssh://svn-community@repos.archlinux.org/srv/repos/svn-community/svn) svn-community

```

This creates two directories named `svn-packages` and `svn-community` which contain nothing but are properly setup as svn repositories.

### Helper Scripts (optional)

#### ch

This shell script eases setting up and maintaining the chroots for building the packages immensely. The script has been developed by [Bluewind](https://www.archlinux.org/people/developers/#bluewind) and can be found here: [ch](https://git.server-speed.net/users/flo/bin/plain/ch).

As this script relies on [Btrfs](/index.php/Btrfs "Btrfs"), you have to create a Btrfs volume (20GiB is mostly sufficient), which can either be a file, a logical volume or a dedicated partition. Furthermore by default this script assumes that the Btrfs for the chroots is mounted at `/mnt/chroots/arch`.

Afterwards you can create a 64bit package using:

```
  ch build 64

```

(automatically and conveniently invokes makechrootpkg with all required arguments)

For further details please take a look at the head of the script, it provides some explanations and usage examples.

## The Workflow

### Checkout/update your Local Repository

```
  cd svn-community
  svn update

```

### Adding a new Package

This step is only required when adding a new package to the repository for the first time.

```
  cd svn-community
  mkdir -p new-package/{repos,trunk}
  cd new-package
  $EDITOR trunk/PKGBUILD
  svn add .
  svn commit

```

### Updating the needed Package

```
  svn update some-package

```

### Change and build

```
  cd some-package/trunk/
  $EDITOR PKGBUILD
  extra-x86_64-build

```

It is **mandatory** to build your package using a clean [chroot](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot "DeveloperWiki:Building in a Clean Chroot").

Or, if you are using the [ch](/index.php/DeveloperWiki:HOWTO_Be_A_Packager#ch "DeveloperWiki:HOWTO Be A Packager") helper, simply do:

```
  cd some-package/trunk/
  $EDITOR PKGBUILD
  ch clean 64
  ch update 64
  ch build 64

```

### Run namcap on both PKGBUILD and Package

```
  namcap PKGBUILD
  namcap some-package-1.0-1-x86_64.pkg.tar.xz

```

### Run checkpkg on the Package

Run in the directory with your freshly built package to get a file list diff compared with the package version currently in the repos. This can be skipped when adding a new package to the repository for the first time (e.g. by importing it from [AUR](/index.php/AUR "AUR") to *community*).

### Use devtools to sign, upload and commit

Once you are satisfied with the package, you need to make sure all your changes are tracked in the repository. Run:

```
  svn status

```

in the `some-package/trunk/` directory and check the output carefully. If, for example, you have added a new `some-package.install` file, you need to tell svn to track that file, e.g.:

```
  svn add some-package.install

```

Make sure to **never** add the binary packages, makepkg logs, etc. to the repository!

When you're ready to proceed, you can run the devtools script to sign, upload and commit your work. This is repo dependent. For *extra* you use `extrapkg`, `communitypkg` for *community*, etc.

```
  extrapkg "update to 1.2.3, add post_upgrade hook to fix permissions"

```

Please try to write concise commit messages. If the package is simply an upstream change, that is fine, but if anything more complex changes, please inform us by writing an appropriate commit message.

### Update the Repository

Using `db-update` will find new packages for any repository.

For example:

```
  ssh repos.archlinux.org "/packages/db-update"

```

or:

```
  ssh repos.archlinux.org "/community/db-update"

```

## Other Operations

### Removing a Package

```
  ssh repos.archlinux.org "/packages/db-remove repo-name arch packagename"

```

i.e.:

```
  ssh repos.archlinux.org "/packages/db-remove core x86_64 openssh"

```

And if you want to really kill the package, you will need to `svn rm` the entire package directory after the above steps and commit the deletion.

Sometime the previous command yields:

```
   svn: E155035: "'/path/to/pkg/<PKG>' is the root of a working copy and cannot be deleted"

```

You can remotely remove it with:

```
   svn rm svn+[ssh://svn-packages@repos.archlinux.org/srv/repos/svn-packages/svn/](ssh://svn-packages@repos.archlinux.org/srv/repos/svn-packages/svn/)<PKG>

```

### Moving a package between repos

```
  ssh repos.archlinux.org "/packages/db-move fromrepo torepo packagename"

```

i.e.:

```
  ssh repos.archlinux.org "/packages/db-move testing core openssh"

```

Alternatively, the move from testing is so common we have helper scripts:

```
  /packages/testing2x openssh bzip2 coreutils
  /packages/testing2x64 openssh bzip2 coreutils

```

These scripts only work if the packages on the commandline are either in *core* or *extra*. If a package is only in testing, you have to use *testing2core*, *testing2core64*, *testing2extra* or *testing2extra64*.

### "Tagging" releases

Fetch the package dir using `archco` or `communityco` or from an svn checkout. Then:

```
  cd package-name/trunk
  archrelease extra-x86_64

```

This makes an svn copy of the trunk entries in a directory named `extra-x86_64` indicating that this package is in the extra repository for the *x86_64* architecture. This will be done automatically when using tools such as `extrapkg` (see [Use devtools to sign, upload and commit](/index.php/DeveloperWiki:HOWTO_Be_A_Packager#Use_devtools_to_sign.2C_upload_and_commit "DeveloperWiki:HOWTO Be A Packager")).

## Miscellaneous Stuff

### Cleaning up your checkout

Since you are now maintaining a non-recursive checkout, you may want to get rid of packages that you are no longer tracking:

```
  svn update package1 package2 --set-depth exclude

```

Or if you want an empty toplevel again:

```
  svn update --set-depth empty

```

### Avoid having to enter your password all the time

When working with `extrapkg` and the other devtools, quite a few ssh connections are established, even when using ssh keys and the ssh agent. You can work around that.

Add this to your `~/.ssh/config`:

```
  ControlPath ~/.ssh/master-%h-%p-%r

  Host repos.archlinux.org

```

Now, before you start working, open a ssh session with

```
  ssh -M repos.archlinux.org

```

Enter your password and leave that session open until you are finished. All ssh sessions (including scp and svn+ssh) will now be tunneled through this connection.