Related articles

*   [Creating packages](/index.php/Creating_packages "Creating packages")

[Arch is the best](/index.php/Arch_is_the_best "Arch is the best"). But you may still want to package for other distributions.

## Contents

*   [1 General](#General)
*   [2 Debian](#Debian)
    *   [2.1 Tips and Tricks](#Tips_and_Tricks)
        *   [2.1.1 Override dependency handling](#Override_dependency_handling)
        *   [2.1.2 Set up a chroot](#Set_up_a_chroot)
    *   [2.2 See also](#See_also)
*   [3 Fedora](#Fedora)
    *   [3.1 See also](#See_also_2)
*   [4 openSUSE](#openSUSE)
    *   [4.1 Creating Arch Packages in OBS with OSC](#Creating_Arch_Packages_in_OBS_with_OSC)
        *   [4.1.1 Creating a Package](#Creating_a_Package)
        *   [4.1.2 Managing a Package](#Managing_a_Package)
        *   [4.1.3 Tips and tricks](#Tips_and_tricks_2)
        *   [4.1.4 ca-certificates-utils package problem](#ca-certificates-utils_package_problem)
        *   [4.1.5 See also](#See_also_3)
*   [5 See also](#See_also_4)

## General

*   [Virtualization](/index.php/Virtualization "Virtualization") is an obvious way, but requires maintaining additional system(s).
*   Use distribution-specific packaging tools. Examples: [dh-make](https://aur.archlinux.org/packages/dh-make/), [dpkg](https://aur.archlinux.org/packages/dpkg/) (Debian), [rpm-org](https://aur.archlinux.org/packages/rpm-org/) (Fedora). Shortcuts such as [dpkg-deb](http://tldp.org/HOWTO/html_single/Debian-Binary-Package-Building-HOWTO/) or [checkinstall](https://aur.archlinux.org/packages/checkinstall/) may be suited for less complex tasks.
*   [Chroot](/index.php/Chroot "Chroot") to create a base system inside (yet separate from) Arch. Examples: [debootstrap](https://www.archlinux.org/packages/?name=debootstrap) (Debian), [dnf](https://aur.archlinux.org/packages/dnf/) (Fedora). This has the added benefit of building in a minimal, clean environment.
*   Use chroot with packaging tools in an an automated fashion. Examples: [pbuilder-ubuntu](https://aur.archlinux.org/packages/pbuilder-ubuntu/) (Debian), [mock-git](https://aur.archlinux.org/packages/mock-git/) (Fedora).
*   A different way to handle (possibly incompatible) depends is [static linking](http://jurjenbokma.com/ApprenticesNotes/getting_statlinked_binaries_on_debian.xhtml). Please note that most distributions frown on this practice.
*   Common practice applies regardless of distribution used. For example, do [not build packages as root](https://bbs.archlinux.org/viewtopic.php?id=67561).

## Debian

The [Debian Packaging Tutorial](https://www.debian.org/doc/manuals/packaging-tutorial/packaging-tutorial.pdf) explains the groundwork. It describes use of the following tools:

**cowdancer** — Copy-on-write wrapper for pbuilder

	[https://packages.debian.org/sid/cowdancer](https://packages.debian.org/sid/cowdancer) || [cowdancer](https://aur.archlinux.org/packages/cowdancer/)

**debootstrap** — A tool used to create a Debian base system from scratch, without requiring the availability of dpkg or apt.

	[https://packages.debian.org/sid/debootstrap](https://packages.debian.org/sid/debootstrap) || [debootstrap](https://www.archlinux.org/packages/?name=debootstrap)

**devscripts** — Scripts to make the life of a Debian Package maintainer easier

	[https://packages.debian.org/sid/devscripts](https://packages.debian.org/sid/devscripts) || [devscripts](https://aur.archlinux.org/packages/devscripts/)

**dh-autoreconf** — Debhelper add-on to call autoreconf and clean up after the build

	[https://packages.debian.org/sid/dh-autoreconf](https://packages.debian.org/sid/dh-autoreconf) || [dh-autoreconf](https://aur.archlinux.org/packages/dh-autoreconf/)

**dh-make** — Tool that converts source archives into Debian package source

	[https://packages.debian.org/sid/dh-make](https://packages.debian.org/sid/dh-make) || [dh-make](https://aur.archlinux.org/packages/dh-make/)

**[dpkg](https://en.wikipedia.org/wiki/dpkg "wikipedia:dpkg")** — The Debian Package Manager

	[https://packages.debian.org/sid/dpkg](https://packages.debian.org/sid/dpkg) || [dpkg](https://aur.archlinux.org/packages/dpkg/)

**dput** — Debian package upload tool

	[https://packages.debian.org/sid/dput](https://packages.debian.org/sid/dput) || [dput](https://aur.archlinux.org/packages/dput/)

**equivs** — Circumvent Debian package dependencies

	[https://launchpad.net/ubuntu/+source/equivs](https://launchpad.net/ubuntu/+source/equivs) || [equivs](https://aur.archlinux.org/packages/equivs/)

**git-buildpackage** — Tools from Debian to integrate the package build system with Git

	[https://honk.sigxcpu.org/piki/projects/git-buildpackage/](https://honk.sigxcpu.org/piki/projects/git-buildpackage/) || [git-buildpackage](https://aur.archlinux.org/packages/git-buildpackage/)

**pbuilder-ubuntu** — Chroot environment for building Debian packages

	[https://launchpad.net/ubuntu/+source/pbuilder](https://launchpad.net/ubuntu/+source/pbuilder) || [pbuilder-ubuntu](https://aur.archlinux.org/packages/pbuilder-ubuntu/)

**[quilt](https://en.wikipedia.org/wiki/Quilt_(software) "wikipedia:Quilt (software)")** — Manage a series of patches by keeping track of the changes each patch makes

	[http://savannah.nongnu.org/projects/quilt](http://savannah.nongnu.org/projects/quilt) || [quilt](https://www.archlinux.org/packages/?name=quilt)

### Tips and Tricks

#### Override dependency handling

*dpkg* does not recognize dependencies installed by [pacman](/index.php/Pacman "Pacman"). This means `dpkg-buildpackage` will generally fail with errors such as:

```
dpkg-checkbuilddeps: Unmet build dependencies: build-essential:native debhelper (>= 8.0.0)
dpkg-buildpackage: warning: build dependencies/conflicts unsatisfied; aborting

```

To override this, use the -d flag:

```
$ dpkg-buildpackage -d -us -uc

```

You may also need to override `dh_shlibdeps` by adding the following lines to `debian/rules`:

```
override_dh_shlibdeps:
   dh_shlibdeps --dpkg-shlibdeps-params=--ignore-missing-info

```

**Note:** Any run-time dependencies (and matching version numbers) should be added manually to `debian/control`, where `${shlibs:Depends}` now has no meaning.

**Warning:** Even *if* you manage to successfully build a package this way, it is **strongly recommended** to build in a clean environment (such as chroot) to prevent any incompatibilities.

#### Set up a chroot

See the [Pbuilder How-To](https://wiki.ubuntu.com/PbuilderHowto) for an introduction to *pbuilder-ubuntu*. Using *cowdancer* in addition is recommended as [copy-on-write](https://en.wikipedia.org/wiki/Copy-on-write "wikipedia:Copy-on-write") offers a significant performance benefit.

*   [debian-archive-keyring](https://www.archlinux.org/packages/?name=debian-archive-keyring), [ubuntu-keyring](https://aur.archlinux.org/packages/ubuntu-keyring/) and [gnupg1](https://aur.archlinux.org/packages/gnupg1/) from the [AUR](/index.php/AUR "AUR") are required.
*   *eatmydata* is available as [libeatmydata](https://aur.archlinux.org/packages/libeatmydata/) and [lib32-libeatmydata](https://aur.archlinux.org/packages/lib32-libeatmydata/) in the [AUR](/index.php/AUR "AUR"). To prevent `LD_PRELOAD` errors, it must be installed both inside and outside the chroot. As the paths are different in Arch and Debian, create the following symbolic links:

```
# ln -s /usr/lib/libeatmydata.so.1.1.1 /usr/lib/libeatmydata/libeatmydata.so
# ln -s /usr/lib/libeatmydata.so.1.1.1 /usr/lib/libeatmydata/libeatmydata.so.1

```

*   [Sample pbuilderrc](https://gist.githubusercontent.com/AladW/71352540eca7de2197c7/raw/c28f6d96c0beb116f99e1ff0bd16599c356855ed/gistfile1.sh)
*   To create a source package for pbuilder to handle:

```
$ dpkg-buildpackage -d -us -uc -S

```

### See also

*   [Debian Policy](https://www.debian.org/doc/debian-policy/)
*   [New Maintainers' Guide](https://www.debian.org/doc/manuals/maint-guide/)
*   [Quilt in Debian packaging](http://raphaelhertzog.com/2012/08/08/how-to-use-quilt-to-manage-patches-in-debian-packages/)

## Fedora

[How to create an RPM package](https://fedoraproject.org/wiki/How_to_create_an_RPM_package)

**rpm-org** — RPM.org fork, used in major RPM distros

	[http://www.rpm.org/](http://www.rpm.org/) || [rpm-org](https://aur.archlinux.org/packages/rpm-org/)

**mock** — Takes Source RPMs and builds RPMs from them in a chroot

	[http://fedoraproject.org/wiki/Projects/Mock](http://fedoraproject.org/wiki/Projects/Mock) || [mock-git](https://aur.archlinux.org/packages/mock-git/)

### See also

*   [Projects/Mock](http://fedoraproject.org/wiki/Projects/Mock)
*   [Copr](https://copr.fedoraproject.org/)

## openSUSE

The [Open Build Service (OBS)](http://openbuildservice.org/) is a generic system to build and distribute packages from sources in an automatic, consistent and reproducible way. It supports at least .deb, .rpm and Arch packages.

### Creating Arch Packages in OBS with OSC

**Note:** For building, you must upload you PKGBUILD file as well as the source files (by uploading or letting OBS download the files). OBS uses virtual machines without networking support and cannot download any file.

#### Creating a Package

1.  Create an account in [[1]](https://build.opensuse.org/)
2.  [Install](/index.php/Install "Install") the [osc](https://aur.archlinux.org/packages/osc/) package. Upstream documentation is available [here](http://en.opensuse.org/openSUSE:OSC).
3.  Create an example `home:foo` project.
4.  Create an example `home:foo:bar` subproject (optional, but recommended).
5.  Create a new `ham` example package with `osc meta pkg -e home:foo:bar ham`. Save the created XML then exit.
6.  Switch to a clean working directory then checkout the project you've just created: `osc co home:foo:bar/ham`.
7.  Now cd into it: `cd home:foo:bar/ham`.

#### Managing a Package

Now it is time to decide how we will manage our project. There are two practical ways to do this:

1.  Maintain a PKGBUILD plus its helper files (such as *.install scripts) in a version control system (such as git, hg) then just make OBS track it;
2.  Maintain a package entirely in OBS itself.

The first version is more flexible and dynamic. To proceed:

*   From your project directory, create a `_service` file with the following contents:

```
<services>
  <service name="tar_scm">
    <param name="scm">git</param>
    <param name="url">git://<your_repo_here></param>
    <param name="versionformat">git%cd~%h</param>
    <param name="versionprefix"><your_version_here></param>
    <param name="filename"><name_of_your_package></param>
  </service>
  <service name="recompress">
    <param name="file">*.tar</param>
    <param name="compression">xz</param>
  </service>
  <service name="set_version"/>
</services>
```

Here is an example for [gimp-git](https://aur.archlinux.org/packages/gimp-git/):

```
<services>
  <service name="tar_scm">
    <param name="scm">git</param>
    <param name="url">git://git.gnome.org/gimp.git</param>
    <param name="versionformat">git%cd~%h</param>
    <param name="versionprefix">2.9.1</param>
    <param name="filename">gimp-git</param>
  </service>
  <service name="recompress">
    <param name="file">*.tar</param>
    <param name="compression">xz</param>
  </service>
  <service name="set_version"/>
</services>
```

*   Make OBS track it: `osc add _service`
*   If you have any other files to include into the repo, just proceed as before: add the files in the project directory, then make OBS track them (OBS uses subversion as its underlying SCM, so this process might already be familiar for you)
*   Check-in (=upload) your files into the repo `osc ci -m "commit message (e.g. bumped package xxx to version yyy"`.

Now, after a while, OBS will begin building your package.

#### Tips and tricks

*   To see the build progress of your package, cd into its working directory, then: `osc results`.
*   There are two repositories, Arch_Core and Arch_Extra. You'll probably want Arch_Extra, since it is more complete. [community] isn't currently available there as of this edit, so if your project has any dependencies in [community], you should include them (manually) in your (sub)project too.
*   There is an unofficial arch-community repo [here](https://build.opensuse.org/project/show/home:roman-neuhauser:arch-community). You might clone a package from there with `osc branch home:roman-neuhauser:arch-community/<package-name> home:foo:bar/<package-name>`.

#### ca-certificates-utils package problem

If OBS build fails because of the ca-certificates-utils package, you can add this line to your project config (from your project page, go to Advanced -> Project Config).

```
Prefer: ca-certificates-utils ca-certificates

```

#### See also

*   Example repo: [arch-deepin](https://build.opensuse.org/project/show/home:metakcahura:arch-deepin)
*   [openSUSE packaging guidelines](http://en.opensuse.org/openSUSE:Packaging_guidelines)
*   [Portal:Packaging from openSUSE wiki](http://en.opensuse.org/Portal:Packaging)

## See also

*   [BBS - PKGBUILD equivalents for other distros](https://bbs.archlinux.org/viewtopic.php?id=175409)
*   [BBS - Original discussion](https://bbs.archlinux.org/viewtopic.php?id=182198)