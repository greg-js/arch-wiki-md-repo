## Contents

*   [1 The Big Idea Page](#The_Big_Idea_Page)
    *   [1.1 Move to better Bug Tracker](#Move_to_better_Bug_Tracker)
    *   [1.2 Moving repository management to git](#Moving_repository_management_to_git)
    *   [1.3 Signing database files](#Signing_database_files)
    *   [1.4 Auto rebuild script](#Auto_rebuild_script)
    *   [1.5 More packaging automation](#More_packaging_automation)
    *   [1.6 Orphan packages](#Orphan_packages)
    *   [1.7 Datacenter software](#Datacenter_software)
    *   [1.8 Delta packages in repos](#Delta_packages_in_repos)
    *   [1.9 Encourage people to contribute to Arch projects](#Encourage_people_to_contribute_to_Arch_projects)
    *   [1.10 Better namcap errors for version bumps](#Better_namcap_errors_for_version_bumps)
    *   [1.11 Listing all direct dependencies](#Listing_all_direct_dependencies)
    *   [1.12 Multiple kernel support](#Multiple_kernel_support)
    *   [1.13 ~~Out-of-tree kernel modules management~~](#Out-of-tree_kernel_modules_management)

## The Big Idea Page

This page is for generating a collection of ideas that would improve Arch Linux. It will allow us to assess areas in which we can improve and whether we need more "staff" to move forward.

#### Move to better Bug Tracker

Moving the bug tracker to Bugzilla or Roundup would have many advantages (see also [FS#24999](https://bugs.archlinux.org/task/24999)):

*   It is more well maintained upstream than Flyspray
*   Bugs could be handled via email
*   ...

Florian has a script that will convert our bug database into Bugzilla format. Currently no-one is interested in maintaining the install.

#### Moving repository management to git

Using git instead of SVN is not really the primary goal, although it is a nice bonus. We also gain other stuff (split packages with different architectures, debug package repos, ...) Florian has made great advances in this realm. [User:Bluewind/dbscripts-rewrite](/index.php/User:Bluewind/dbscripts-rewrite "User:Bluewind/dbscripts-rewrite")

#### Signing database files

Our package security would be improved by signing repository databases. This requires working with upstream GPG developers to allow signing of files over ssh.

#### Auto rebuild script

Simplfing package rebuilds.

```
rebuildpkg pkg1 pkg2 pkg3

```

#### More packaging automation

Not a very big idea but very much related to "auto rebuild script". Yet another wrapper or a full-blown "packaging shell", this time abstracting away the underlying independent build tools (svn, devtools, etc.), providing auto-completion of package names, committing to the correct repo, building on remote build server if wanted, rebuilding single packages or a package dependency list (with bumps and auto push to a staging or testing repo; there is no need to test successful rebuilds locally; also send e-mails to maintainers of failed builds), getting packages and signing them if built remotely, starting up a container or a VM with the newly built package and all dependencies to allow real, live testing (especially for graphical stuff). Will allow anyone to build, release and push depending on permissions to a repo (all users by default have permission to custom repos); this is defined in a file. Does packaging and does it well. Very distro-specific, will have zero compatibility with other pacman distros. Will look stupid at first. Will be useful in the long-run. Will become obsolete if systemd solves the whole Linux packaging problem.

#### Orphan packages

There are LOTS of these. Any common themes that would be worth recruiting a new packager for?

#### Datacenter software

Maintain software used in datacenters in the repo for easier installation? (ceph, puppet, nagios, ...)

#### Delta packages in repos

pacman already supports delta packages, but repo scripts don't generate the necessary delta files. See: [Deltup](/index.php/Deltup "Deltup"), [FS#18590](https://bugs.archlinux.org/task/18590).

#### Encourage people to contribute to Arch projects

Github and the like encourage contributions by making the source obvious and easy to navigate. We currently lack this with Arch projects (and possibly packages). I think slapping our projects onto Github or an in-house Gitlab would increase contributions. The cgit + mailing list thing seems archaic nowadays where developers grow up with pull requests. Perhaps we should adapt where it makes sense? This might in fact alleviate some of our staff trouble as we allow others to more easily help us out.

#### Better namcap errors for version bumps

namcap should emit errors for packages when their updated version would break other apps due to soname bumps. Sadly, this can't work just by dependencies alone because our packages don't list all the dependencies directly. This is currently done on pkgbuild.com using sogrep and some manual note keeping which seems backward. sogrep is not readily available in devtools because it requires having a full mirror on the local drive. Since a full mirror is still less than 20 GiB, I don't believe this is a big problem and sogrep should be packaged in devtools to allow namcap to have some new features. Failing that, either a generated database for sonames should be generated by our tools (basically ldd over all dynamically linked objects) or an API for sogrep-like operations should be provided.

When such a tool is available, namcap could be improved to have this feature and henceforth version bumping would require less manual effort upfront and would be less error prone.

#### Listing all direct dependencies

As a follow up to this, the fact that Arch packages only list "first level" dependencies has long been a source of maintenance burden. I can see two reasons for why people (Judd?) decided this:

1.  It makes it easier for new packagers to contribute.
2.  It prevents overly verbose output of "pacman -Qi".

The newbie friendliness can be kept if we continue to allow "first level only" packages in the AUR. However, I think official repositories should list every library dependency in the depends array. This will require a pkgrel bump of every package, but we only need to do it once. For those who still want short "pacman -Qi" output, we can introduce a new switch to pacman which will automatically trim second level deps. This is much faster than doing the opposite and trying to run namcap each time.

One should not have to use separate tools to generate a rebuild list. The "Required by" field of a pacman query should be enough. As it stands, this field is useless because rebuilds don't care about "Required at the first level by". A short-lived alternative proposal was to achieve this with [hooks](/index.php/User:Allan/Pacman_Hooks "User:Allan/Pacman Hooks"). However, [as discussed](https://lists.archlinux.org/pipermail/pacman-dev/2014-April/018994.html), it is very ugly to expose the .PKGINFO file and let scripts alter dependencies as packages are installed.

#### Multiple kernel support

Our current way of managing kernel should be improved:

1.  Updating a kernel need an immediate reboot
    Kernel modules of the current running kennel is removed and replaced by another kernel module. So you cannot load modules anymore. In servers environment, it's difficult to restart your server everytime a stable release is out.
2.  We cannot have more than one version of the kernel (see [FS#16702](https://bugs.archlinux.org/task/16702)).
    If the last update cause an issue, you cannot select an older one in your favoring boot loader. You need an USB rescue key, if the server is not close to you, Houston, we've had a problem.

<u>Possible solution:</u> A simple solution would be to put the kernel name inside the package name and use a meta package to pull the last version. Letting for example 3 kernels generations (3.17.x, 3.16.x, 3.15.x) before removing them (by conflicts).

#### ~~Out-of-tree kernel modules management~~

Currently, we have 3 kernels (-arch, -lts, -grsec) and updating out-of-tree kernel modules is something time consuming. The frequency and the testing phase make things even more error prone.

To simplify the situation, I'm suggesting to let DKMS manage them. This is particularly useful if we implement previous idea of multiple kernel support and make the number of kernel modules scalable.

Of course, that make compilation of modules being done by every users, but, it mays be a fair trade as these modules don't make enough effort to be mainlined.

	We now offer dkms versions of module packages as a matter of course, and, usually, compiled versions for at least the primary kernel. This is the best of both worlds. -- [Eschwartz](/index.php/User:Eschwartz "User:Eschwartz") ([talk](/index.php/User_talk:Eschwartz "User talk:Eschwartz")) 01:39, 11 November 2018 (UTC)