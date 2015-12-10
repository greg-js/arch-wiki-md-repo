# Bisecting bugs

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Often when reporting bugs encountered with projects such as Mesa or Linux kernel, a user may be asked to bisect between the last known version that worked for them and the newer version which is causing them problems in order to see what is the troublesome commit. On Arch this can be done fairly trivially thanks to the functionality of the [AUR](/index.php/AUR "AUR").

## Contents

*   [1 Reverting to an older release](#Reverting_to_an_older_release)
*   [2 Building package from git](#Building_package_from_git)
*   [3 Setting up the Bisect](#Setting_up_the_Bisect)
*   [4 Bisecting](#Bisecting)
*   [5 Speeding up builds](#Speeding_up_builds)
*   [6 Restoring package](#Restoring_package)
*   [7 See also](#See_also)

## Reverting to an older release

It might be useful to confirm that it is the new package release that is causing the problem. [Downgrading packages](/index.php/Downgrading_packages "Downgrading packages") on Arch can be accomplished trivially as long as an older version of the package is still stored as cache on your system, or you can use [Arch Rollback Machine](/index.php/Downgrading_packages#Arch_Rollback_Machine "Downgrading packages").

**Note:** Even if the older version fixes the problem it is still possible that is not a bug within the program, but a problem with the packages as provided by Arch.

## Building package from git

In order to bisect we are going to need to build a version of package from [git](/index.php/Git "Git"). This can be accomplished by building the _-git_ package from the [AUR](/index.php/AUR "AUR").

## Setting up the Bisect

Once package is successfully built you need to change into the git root directory in the `src/` directory. The name of the git root directory is often the same as `_pkgname_` (or without the `-git` suffix):

```
$ cd src/_git_root_

```

From there you can start the process of bisecting:

```
$ git bisect start

```

The following command will show you all the tags you can use to specify where to bisect:

```
$ git tag

```

Following on from the earlier example, we will assume that the version _oldver_ worked for us while _newver_ did not:

```
$ git bisect good _oldver_
$ git bisect bad _newver_

```

Now that we have our good and bad versions tagged we can proceed to test commits.

## Bisecting

Change back into the directory with the PKGBUILD. If you are still in the directory mentioned in the previous section this can be accomplished like so:

```
$ cd ../..

```

You can now rebuild and install the specific revision of the package:

```
$ makepkg -efsi

```

**Note:** It is very important to keep the `-e` prefix intact as otherwise it will remove all the changes you have made.

Once the new package is installed you can test for your previously discovered error. Return to the directory you were in the previous section:

```
$ cd src/_git_root_

```

If you encountered your problem, tell that the revision was bad:

```
$ git bisect bad

```

If you did not encounter your problem, tell that the revision it was good:

```
$ git bisect good

```

Then do as described at the beginning of this section again and repeat until git bisect names the troublesome commit.

**Note:** It will actually count down the number of steps all the way down to zero, so it is important not to stop until it actually names the first bad commit.

## Speeding up builds

If you're bisecting the Linux kernel or another large project built using `gcc`, you can reduce build times by enabling [ccache](/index.php/Ccache "Ccache"). It may take several build iterations before you start to see benefits from the cache, however. The likelihood of cache hits generally increases as the distance between bisection points decreases.

You can also shorten kernel build times by building only the modules required by the local system using [modprobed-db](/index.php/Modprobed-db "Modprobed-db").

## Restoring package

Reverting to an original version of the package can be done by installing the package from repositories with [pacman](/index.php/Pacman "Pacman").

## See also

*   [Fighting regressions with git bisect](http://git-scm.com/docs/git-bisect-lk2009.html)
*   [git-bisect(1)](https://www.kernel.org/pub/software/scm/git/docs/git-bisect.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Bisecting_bugs&oldid=408010](https://wiki.archlinux.org/index.php?title=Bisecting_bugs&oldid=408010)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Package management](/index.php/Category:Package_management "Category:Package management")
*   [Version Control System](/index.php/Category:Version_Control_System "Category:Version Control System")