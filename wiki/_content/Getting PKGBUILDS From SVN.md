# Getting PKGBUILDS From SVN

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

## Contents

*   [1 Do NOT download the whole repo](#Do_NOT_download_the_whole_repo)
*   [2 Non-recursive checkout](#Non-recursive_checkout)
*   [3 Checkout a package](#Checkout_a_package)
*   [4 Updating all packages](#Updating_all_packages)
*   [5 Checkout an older revision of a package](#Checkout_an_older_revision_of_a_package)

### Do NOT download the whole repo

**Warning:** The entire SVN repo is huge. Not only will it take an obscene amount of disk space, but it will also tax the archlinux.org server for you to download it. Do not download the whole repo, only follow the instructions below.

If you abuse this service, your address may be blocked.

Never use the public SVN for any sort of scripting.

### Non-recursive checkout

For core,extra,testing:

```
  svn checkout --depth=empty [svn://svn.archlinux.org/packages](svn://svn.archlinux.org/packages) 

```

For community:

```
  svn checkout --depth=empty [svn://svn.archlinux.org/community](svn://svn.archlinux.org/community) 

```

In both cases, it simply creates an empty directory, but it does know that it is an svn checkout.

In the sections below, just replace the _packages_ directory name by _community_ when working with community packages.

### Checkout a package

```
  cd packages
  svn update package-name

```

This will pull the package you requested into your checkout. From now on, any time you _svn update_ at the top level, this will be updated as well.

If you specify a package that doesn't exist, svn won't warn you. It will just print something like "At revision 115847", without creating any files. If that happens, check your spelling of the package name and that the package has not been moved to another repository (ie. from community to the main repository).

### Updating all packages

```
  cd packages
  svn update

```

### Checkout an older revision of a package

```
  cd packages
  svn log package-name

```

Find out the revision you want by examining the history, then:

```
  svn update -r1729 package-name

```

This will update an existing working copy of _package-name_ to the chosen revision.

You can also specify a date. If no revision on that day exists, svn will grab the most recent package before that time:

```
  svn update -r{20090303} package-name

```

It is possible to checkout packages at versions before they were moved to another repository as well; check the logs thoroughly for the date they were moved or the last revision number.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Getting_PKGBUILDS_From_SVN&oldid=369685](https://wiki.archlinux.org/index.php?title=Getting_PKGBUILDS_From_SVN&oldid=369685)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Package development](/index.php/Category:Package_development "Category:Package development")