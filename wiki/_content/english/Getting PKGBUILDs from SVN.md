This is a method for obtaining the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") files for packages residing in the [official repositories](/index.php/Official_repositories "Official repositories").

## Contents

*   [1 Prerequisites](#Prerequisites)
*   [2 Non-recursive checkout](#Non-recursive_checkout)
*   [3 Checkout a package](#Checkout_a_package)
    *   [3.1 Checkout the current version of a package](#Checkout_the_current_version_of_a_package)
    *   [3.2 Checkout an older version of a package](#Checkout_an_older_version_of_a_package)
*   [4 Updating all packages](#Updating_all_packages)
*   [5 See also](#See_also)

## Prerequisites

[Install](/index.php/Install "Install") the [subversion](https://www.archlinux.org/packages/?name=subversion) package.

## Non-recursive checkout

**Warning:** Do not download the whole repo; only follow the instructions below. The entire SVN repo is huge. Not only will it take an obscene amount of disk space, but it will also tax the archlinux.org server for you to download it. If you abuse this service, your address may be blocked. Never use the public SVN for any sort of scripting.

To checkout the core, extra, and testing [repositories](/index.php/Repositories "Repositories"):

```
$ svn checkout --depth=empty svn://svn.archlinux.org/packages

```

To checkout the community and multilib repositories:

```
$ svn checkout --depth=empty svn://svn.archlinux.org/community

```

In both cases, it simply creates an empty directory, but it does know that it is an svn checkout.

## Checkout a package

### Checkout the current version of a package

In the directory containing the svn repository you checked out (i.e., "packages" or "community"), do:

```
$ svn update *package-name*

```

This will pull the package you requested into your checkout. From now on, any time you *svn update* at the top level, this will be updated as well.

If you specify a package that does not exist, svn will not warn you. It will just print something like "At revision 115847", without creating any files. If that happens, check your spelling of the package name and that the package has not been moved to another repository (i.e. from community to the main repository).

### Checkout an older version of a package

Within the svn repository you checked out (i.e. "packages" or "community"), first examine the log:

```
$ svn log *package-name*

```

Find out the revision you want by examining the history, then speciy the revision you wish to checkout. For example, to checkout revision `r1729` you would do:

```
$ svn update -r1729 *package-name*

```

This will update an existing working copy of *package-name* to the chosen revision.

You can also specify a date. If no revision on that day exists, svn will grab the most recent package before that time. The following example checks out the revision from 2009-03-03:

```
$ svn update -r{20090303} *package-name*

```

It is possible to checkout packages at versions before they were moved to another repository as well; check the logs thoroughly for the date they were moved or the last revision number.

## Updating all packages

To update all packages you have checked out:

```
$ cd packages
$ svn update

```

## See also

*   [Arch Build Source Management Tool](https://github.com/falconindy/asp)