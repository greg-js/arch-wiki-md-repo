A list of reproducible build meetings and work in progress documentation.

[Reproducible build results](https://tests.reproducible-builds.org/archlinux/archlinux.html)

## Contents

*   [1 Helping out](#Helping_out)
*   [2 To-do list](#To-do_list)
*   [3 Reproducible Build Arch Update 09-12-2018](#Reproducible_Build_Arch_Update_09-12-2018)
    *   [3.1 Pacman](#Pacman)
    *   [3.2 BUILDINFO](#BUILDINFO)
    *   [3.3 The repro tool](#The_repro_tool)
    *   [3.4 Reproducible Builds environment](#Reproducible_Builds_environment)
    *   [3.5 Packaging](#Packaging)
*   [4 Agenda meeting 10-01-2018](#Agenda_meeting_10-01-2018)

## Helping out

Arch Linux is currently in the process of having it 100% reproducible, for the exact definition of reproducible builds and it's benefits take a look at the [project website](https://reproducible-builds.org/).

Arch users can help contribute to Reproducible Build issues by looking at the [continuous reproducing environment](https://tests.reproducible-builds.org/archlinux/archlinux.html). There are various issues which can be sorted out:

*   FTBS (failed to build from source): reproduce the build failure locally and create a bug report if the package can't be [built from a clean chroot](/index.php/DeveloperWiki:Building_in_a_clean_chroot "DeveloperWiki:Building in a clean chroot") (extra-x86_64-build or multilib-build).
*   Failed to download sources, reproduce the issue (makepkg -o -d) and create a bug report on the Arch bugtracker.
*   Failed to reproduce. Locally you can reproduce packages using {pkg|reprotest}. Note that not all variations can be used. For simple time related testing:

```
 reprotest --variations '+time' 'sudo extra-x86_64-build' '*.pkg.tar.xz' 

```

There might be various reasons for a package to not be reproducible, but before digging in take a look at the upstream repository or the reproducible status in [Debian](https://tests.reproducible-builds.org/debian/reproducible.html)

*   Failed to run tests, these failures are heavily on the testing env. Most likely due to to LANG=C being set and Arch not supporting LANG=C.UTF-8

If you are interested in the code which runs the continuous reproducing environment, the first build code starts here on [salsa](https://salsa.debian.org/qa/jenkins.debian.net/blob/master/bin/reproducible_build_archlinux_pkg.sh#L115)

## To-do list

*   Arch Linux Archive cleanup script
*   Arch Linux Reproducible script

*   A script to locally reproduce an installed package

*   Resolve reproducible build issues
*   Documentation about reproducing a build

## Reproducible Build Arch Update 09-12-2018

As Bernhard did a wonderful writeup for the rpm ecosystem ahead of the Paris summit, we thought we should attempt the same thing. We have summarized the work Arch Linux has done towards reproducible builds the past year(s). Hopefully it will be somewhat interesting! Feel free to ask if there are any questions.

1\. Pacman 2\. BUILDINFO 3\. The repro tool 4\. Reproducible Builds environment 5\. Packaging

### Pacman

Support for SOURCE_DATE_EPOCH was added to makepkg in May of 2017 [1]. makepkg is the tool used to create packages from PKGBUILD files. After some testing it was later discovered that we also needed to make sure that files inside packages need to have the correct time, as build artifacts sometimes embed the timestamps [2]. In May 2018 we released pacman 5.1.0 which included support for reproducible builds.

[1]: [https://git.archlinux.org/pacman.git/commit/?id=d30878763ce1b5be453b563f2729d7333242e79b](https://git.archlinux.org/pacman.git/commit/?id=d30878763ce1b5be453b563f2729d7333242e79b) [2]: [https://git.archlinux.org/pacman.git/commit/?id=4dae3fde17d663bf39a17978c2ee365696a54fb0](https://git.archlinux.org/pacman.git/commit/?id=4dae3fde17d663bf39a17978c2ee365696a54fb0)

### BUILDINFO

Recording of build information in a .BUILDINFO file was added to pacman in 2015[1].

The intial file included:

```
   - builddir
   - pkgbuild_sha256sum
   - buildenv (makepkg configuration option which affects the build 

```

environment)

```
   - options (options which affect packaging, removing debug symbols, 

```

staticlibs, etc.)

```
   - installed

```

The initial file was expanded in 2017 with the following fields[2]:

```
   - format (version of buildinfo file format)
   - pkgname
   - pkgbase
   - pkgver
   - packager
   - builddate

```

In 2018 a man page was written which describes the BUILDINFO file [3].

During development of tools to reproduce packages, we discovered the BUILDINFO file was lacking the architecture information of installed packages. As Arch Linux produces packages with different architectures, such as 'x86_64' and 'any', we had to guess the architecture of the package when fetching from our archive. This was subsequently fixed. [4]

[1]: [https://git.archlinux.org/pacman.git/commit/?id=137ea39fa11c321a9c33000ff1b5c6cc3c59b47d](https://git.archlinux.org/pacman.git/commit/?id=137ea39fa11c321a9c33000ff1b5c6cc3c59b47d) [2]: [https://git.archlinux.org/pacman.git/commit/?id=c44c649a5280189ea28a54b82e60fc38279fed23](https://git.archlinux.org/pacman.git/commit/?id=c44c649a5280189ea28a54b82e60fc38279fed23) [3]: [https://git.archlinux.org/pacman.git/commit/?id=a7dbe4635b4af9b5bd927ec0e7a211d1f6c1b0f2](https://git.archlinux.org/pacman.git/commit/?id=a7dbe4635b4af9b5bd927ec0e7a211d1f6c1b0f2) [4]: [https://git.archlinux.org/pacman.git/commit/?id=f173f6d0da3793952691416d80441b46af12fc94](https://git.archlinux.org/pacman.git/commit/?id=f173f6d0da3793952691416d80441b46af12fc94)

### The repro tool

repro is a tool to aid in verification of Arch Linux packages. It creates a chroot, fetches the correct PKGBUILD and installs the needed dependencies as described by a BUILDINFO file.

The tool has the following goals:

```
   - Easily auditable
   - Distribution independent
   - Do not duplicate features from other tools, like reprotest[2].

```

This helps us in making it easier for users, or other interested parties, to audit Arch packages in the future. It is currently very much a work in progress, however it is capable of reproducing archive packages in its current state.

[1]: [https://github.com/archlinux/archlinux-repro](https://github.com/archlinux/archlinux-repro) [2]: [https://salsa.debian.org/reproducible-builds/reprotest](https://salsa.debian.org/reproducible-builds/reprotest)

### Reproducible Builds environment

The continuous reproducing environment has been continuously improved by Holger and numerous others. It now uses a database to render the HTML pages which allows showing the reproducibility status. We have also donated some servers which where sponsored by Private Internet Access to help reproduce packages.

[https://tests.reproducible-builds.org/archlinux/archlinux.html](https://tests.reproducible-builds.org/archlinux/archlinux.html)

### Packaging

As for packaging, Arch tries to be as vanilla as possible and therefore does not patch packages specifically for reproducible builds and tries to upstream the found issues instead. There are some issues with the actual packaging which made packages reproducible, for example convert was used in PKGBUILDs to convert images to a different format mostly for for desktop files. Imagemagick's convert by default is not reproducible since it embeds dates in the converted files, this was fixed in our PKGBUILDs. [1]

Another issue was found using the repro tool with our SVN propsets making it unreproducible, the propsets are now removed from our PKGBUILDs - also due to not being useful anymore. [2]

Apart from these issues, numerous 404 sources have been fixed (since Arch does not mirror the upstream source tarballs) and fixed FTBS packages, especially for the [core] repository.

[1]: [https://git.archlinux.org/svntogit/community.git/tree/trunk/PKGBUILD?h=packages/bt747](https://git.archlinux.org/svntogit/community.git/tree/trunk/PKGBUILD?h=packages/bt747) [2]: [https://www.mail-archive.com/arch-dev-public@archlinux.org/msg25744.html](https://www.mail-archive.com/arch-dev-public@archlinux.org/msg25744.html)

## Agenda meeting 10-01-2018

*   UTF-8 failures with Python.

    	There are a lot of reproducible build issues due to the lack of LANG=$lang-UTF-8\. Do we need to explicitly set the LANG in the PKGBUILD

    	See for example [https://tests.reproducible-builds.org/archlinux/community/python-cssselect2/build1.log](https://tests.reproducible-builds.org/archlinux/community/python-cssselect2/build1.log)

*   Package disorderfs

    	Not high important right now, I've added it on my todolist. This could be used later in combination with the reproducible build script

*   Pacman release

    	How do we convince the Pacman team to create a new release, are there any known blockers they waiting on?

*   Reproducible build script progress

    	Discuss what the script exactly should do, create an RFC? To describe it's functionality.

    	FIXME: add issues I encountered.

*   Arch Linux Archive: Don't remove packages mentioned in BUILDINFO file

    	There is currently no script to remove old packages from the archive, it is not sure how long we want to keep old packges

    	Sangy was working on this if I recall correctly, what is the status? [poc script](https://github.com/SantiagoTorres/reproarch-dependency-crawler)

*   Write documentation what this script should do. (Specification)

*   Killed builds

    	Someone should investigate this, how do we reproduce this locally? Hints?

*   SSL verification issues

    	How do we circumvent SSL issues from reproducing a package locally which was build earlier, when the SSL certificate was valid. HG and SVN are still left to be fixed.

*   Create a public to-do list

    	We should get more people in to work on reproducible builds, how can we guide them and where do we keep track of the progress made and issues which require attention.

The meeting minute can be seen [here](https://arch.nyu.wtf/logs/archlinux-reproducible/2018/archlinux-reproducible.2018-01-10-19.04.html).