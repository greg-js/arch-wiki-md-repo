# Namcap

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Namcap is a tool to check binary packages and source PKGBUILDs for common packaging mistakes, which can also be automatically enabled. It was created by [Jason Chu](https://www.archlinux.org/fellows/#jason).

**Changes**: The [NEWS](https://projects.archlinux.org/namcap.git/tree/NEWS) file in the git repository contains the changes from the previous version concisely.

**Development Branch**: [https://projects.archlinux.org/?p=namcap.git;a=summary](https://projects.archlinux.org/?p=namcap.git;a=summary)

To **report a bug** or a **feature request** for namcap, file a bug in the _Packages:Extra_ section of the Arch Linux [bugtracker](https://bugs.archlinux.org) and the set the importance accordingly. If you are reporting a bug, please give concrete examples of packages where the problem occurs and remember to insert the version number.

If you have a patch (fixing a bug or a new namcap module), then you can send it to the [arch-projects](mailto:arch-projects@archlinux.org) mailing list. Namcap development is managed with git, so git-formatted patches are preferred.

## Contents

*   [1 Installation](#Installation)
*   [2 How to use it](#How_to_use_it)
*   [3 Understanding the output](#Understanding_the_output)
*   [4 Tags](#Tags)
    *   [4.1 Symbolic Links](#Symbolic_Links)
    *   [4.2 Dependencies](#Dependencies)
    *   [4.3 Licenses](#Licenses)
    *   [4.4 Files](#Files)
    *   [4.5 Miscellaneous](#Miscellaneous)
    *   [4.6 PKGBUILDs](#PKGBUILDs)
    *   [4.7 Unreleased](#Unreleased)
*   [5 Making a namcap module](#Making_a_namcap_module)
*   [6 Namcap reports](#Namcap_reports)

## Installation

[Install](/index.php/Pacman "Pacman") package [namcap](https://www.archlinux.org/packages/?name=namcap) from the [official repositories](/index.php/Official_repositories "Official repositories").

## How to use it

To run namcap on a file, where _filename_ is `PKGBUILD` or the name of a binary `pkg.tar.xz`:

```
$ namcap _filename_

```

If you want to see extra informational messages, then invoke namcap with the `-i` flag:

```
$ namcap -i _filename_

```

You can also see the namcap(1) manual by typing _man namcap_ at the command line.

## Understanding the output

Namcap uses a system of **tags** to classify the output. Currently, tags are of three types, _errors_ (denoted by E), _warnings_ (denoted by W) and _informational_ (denoted by I). An error is important and should be fixed immediately; mostly they relate to insufficient security, missing licenses or permission problems.

Normally namcap prints a human-readable explanation (sometimes with suggestions on how to fix the problem). If you want output which can be easily parsed by a program, then pass the -m (_machine-readable_) flag to namcap (this feature is currently in the development branch).

## Tags

### Symbolic Links

*   **symlink-found** (_informational_) Reports any **symbolic links** present in the package.
*   **hardlink-found** (_informational_) Reports any **hard links** present in the package.
*   **dangling-symlink** (_error_) Reports occurrences of symbolic links which point to a file which is not present in the package.
*   **dangling-hardlink** (_error_) Reports occurrences of hard links which point to a file which is not present in the package.

### Dependencies

*   **link-level-dependence** (_informational_) Informs about a library to which a package is dynamically linked.
*   **dependency-is-testing-release** (_warning_) The package dependency listed is in the [testing] repository. While packages are being built for the official Arch Linux repositories (core, extra and community), then they **should not be built** against packages from [testing]. For [core] and [extra] packages, packages built against [testing] should be put in the [testing] repository.
*   **dependency-covered-by-link-dependence** (_informational_) Dependency covered by dependencies from link dependence. Thus this is a redundant dependency.
*   **dependency-detected-not-included** (_error_) The file referred to has a dependency which is not listed in the depends array. Ignore this error if the named dependency is listed in the optdepends array.
*   **dependency-already-satisfied** (_warning_) The dependency is already satisfied (as the dependency of some package already listed as a dependency for example) and thus is redundant. You can use the `pactree` tool from [pacman](https://www.archlinux.org/packages/?name=pacman) to view the dependency tree of your package.
*   **dependency-not-needed** (_warning_) This dependency is not required by any file present in the program (as far as namcap could deduce). This does not work properly yet for scripts (like python or perl packages) though; there you will have to figure out the dependencies on your own.
*   **depends-by-namcap-sight** (_informational_) A list of dependencies according to namcap.

### Licenses

*   **missing-license** (_error_) This package is missing a license. Licenses should be put in the `license=()` array of the PKGBUILD. See the [Arch packaging standards](/index.php/Arch_packaging_standards "Arch packaging standards") for more information. It is **very important** to fix this error as soon as possible, since not including a license is a copyright violation in many cases.
*   **missing-custom-license-dir** (_error_) The license specified is _custom_ but no license directory was found under _/usr/share/licenses/_ as specified in the packaging guidelines.
*   **missing-custom-license-file** (_error_) The license specified is _custom_ but no license file was found in _/usr/share/licenses/$pkgname_.
*   **not-a-common-license** (_error_) The license specified is **not** _custom_ but it is not present in the common [licenses](https://www.archlinux.org/packages/core/any/licenses/) package shipped in the Arch Linux distribution.

### Files

This section describes the tags which relate to incorrect permissions of files or files not being installed in accordance with the FHS guidelines.

*   **script-link-detected** (_informational_) The following file is a script.
*   **file-in-non-standard-dir** (_warning_) The following file is in a non-standard directory as defined by the [FHS guidelines](http://proton.pathname.com/fhs/pub/fhs-2.3.html). The allowed directories are: _bin/_, _etc/_, _usr/bin/_, _usr/sbin/_, _usr/lib_, _usr/include/_, _usr/share/_, _opt/_, _lib/_, _sbin/_, _srv/_, _var/lib/_, _var/opt/_, _var/spool/_, _var/lock/_, _var/state/_, _var/run/_, _var/log/_.
*   **elffile-not-in-allowed-dirs** (_error_) ELF files should only be in these directories: _/lib_, _/bin_, _/sbin_, _/usr/bin_, _/usr/sbin_, _/lib_, _/usr/lib_, _/opt/$pkgname/_.
*   **empty-directory** (_warning_) The following directory in the package is empty.
*   **non-fhs-man-page** (_error_) The package installs manual pages into a location other than _/usr/share/man_ which is the directory for manual pages according to the [FHS guidelines](http://www.pathname.com/fhs/pub/fhs-2.3.html#USRSHAREMANMANUALPAGES).
*   **potential-non-fhs-man-page** (_warning_) This file seems to be a manual page which is not installed in _/usr/share/man_ but namcap is not too sure about it.
*   **non-fhs-info-page** (_error_) The package installs info pages into a location other than _/usr/share/info_ which is where architecture independent data should be installed according to the [FHS guidelines](http://www.pathname.com/fhs/pub/fhs-2.3.html#USRSHAREARCHITECTUREINDEPENDENTDATA)
*   **potential-non-fhs-info-page** (_warning_) This file seems to be a info page which is not installed in _/usr/share/info_ but namcap is not too sure about it.
*   **incorrect-permissions** (_error_) This file has incorrect ownership. The ownership of files in binary packages should be `root/root`.
*   **file-not-world-readable** (_warning_) The file is not readable by everyone; usually this should not be the case.
*   **file-world-writable** (_warning_) Anyone can write to this file; again not a typical case.
*   **directory-not-world-executable** (_warning_) The directory does not have the world executable bit set. This disallows access to the directory for programs running under user privileges.
*   **incorrect-library-permissions** (_warning_) The static library file (.a) does not have permission 644 (readable and writable by root, readable by anyone else).
*   **libtool-file-present** (_warning_) This file is a libtool (.la) file and should not be normally present. One can use the `!libtool` option in the _options_ array of the PKGBUILD to remove these files automatically.
*   **perllocal-pod-present** (_error_) The file perllocal.pod should not be present in a perl package; see the [Perl package guidelines](/index.php/Perl_package_guidelines "Perl package guidelines") for more information.
*   **scrollkeeper-dir-exists** (_error_) A scrollkeeper directory was found in the package. scrollkeeper should not be run till post_{install,upgrade,remove}.
*   **info-dir-file-present** (_error_) The info directory file _/usr/share/info/dir_ was found in the package. This file should not be present.
*   **gnome-mime-file** (_error_) The file is an autogenerated GNOME mime file and should not be present in the package.

### Miscellaneous

*   **mime-cache-not-updated** (_error_) The package installs mime files but does not call update-mime-database to update them.
*   **hicolor-icon-cache-not-updated** (_error_) There are files in _/usr/share/icons/hicolor_ but the hicolor icon cache has not been updated. One should use _gtk-update-icon-cache_ (for packages depending on _gtk_) or _xdg-icon-resource_ to update the icon cache. If you use _xdg-icon-resource_ then you should declare a dependency on [xdg-utils](https://www.archlinux.org/packages/extra/i686/xdg-utils/).
*   **insecure-rpath** (_error_) An RPATH (for an executable) is outside _/usr/lib_. An RPATH to an insecure location is a potential security issue. See [FS#14049](https://bugs.archlinux.org/task/14049) for discussion.

### PKGBUILDs

These are the tags related to the PKGBUILDs. Some of these might also apply for binary packages.

*   **variable-not-array** (_warning_) The variable should be a bash array instead of a string. These are the variables which should be written as arrays: _arch_, _license_, _depends_, _makedepends_, _optdepends_, _provides_, _conflicts_, _replaces_, _backup_, _source_, _noextract_, _md5sums_
*   **backups-preceding-slashes** (_error_) The file mentioned in the backup array begins with a slash ('/').
*   **package-name-in-uppercase** (_error_) There should not be any upper case letters in package names.
*   **specific-host-type-used** (_warning_) Instead of using a specific host type (like i686 or x86_64) use the generic $CARCH variable.
*   **extra-var-begins-without-underscore** (_warning_) The variable is not one of the standard variables defined in the PKGBUILD manual, yet it does not begin with an underscore.
*   **file-referred-in-startdir** (_error_) A file was referenced in _$startdir_ outside of _$startdir/pkg_ and _$startdir/src_.
*   **missing-md5sums** (_error_) MD5sums corresponding to the source files are missing. These can be added to the PKGBUILD using `updpkgsums`.
*   **not-enough-md5sums** (_error_) There are more source files than MD5sums provided in the PKGBUILD.
*   **too-many-md5sums** (_error_) There are more MD5sums than source files in the PKGBUILD.
*   **improper-md5sum** (_error_) An improper MD5sum was found. MD5sums are of 32 characters in length.
*   **specific-sourceforge-mirror** (_warning_) The PKGBUILD uses a specific sourceforge mirror. [http://downloads.sourceforge.net](http://downloads.sourceforge.net) should be used instead.
*   **using-dl-sourceforge** (_warning_) The deprecated [http://dl.sourceforge.net](http://dl.sourceforge.net) domain is being used in the source array. [http://downloads.sourceforge.net](http://downloads.sourceforge.net) should be used instead.
*   **missing-contributor** (_warning_) The contributor tag is missing.
*   **missing-maintainer** (_warning_) The maintainer tag is missing.
*   **missing-url** (_error_) The package does not have an upstream homepage set. Use the `url` variable for this.
*   **pkgname-in-description** (_warning_) Description should not contain the package name.
*   **recommend-use-pkgdir** (_informational_) _$startdir/pkg_ is deprecated, use _$pkgdir_ instead.
*   **recommend-use-srcdir** (_informational_) _$startdir/src_ is deprecated, use _$srcdir_ instead.

### Unreleased

There are currently no new tags in the development version.

## Making a namcap module

This section documents the innards of namcap and specifies how to create a new namcap module.

The main namcap program namcap.py takes as parameters the filename of a package or a PKGBUILD and makes a pkginfo object, which it passes to a list of rules defined in `__tarball__` and `__pkgbuild__`.

*   ___tarball___ defines the rules which process binary packages.
*   ___pkgbuild___ defines the rules which process PKGBUILDs

Once your module is finalized, remember to add it to the appropriate array (___tarball___ or ___pkgbuild___) defined in _Namcap/__init__.py_

A sample namcap module is like this:

 `namcap/url.py` 

```
  import pacman

  class package:
  	def short_name(self):
		return "url"
	def long_name(self):
		return "Verifies url is included in a PKGBUILD"
	def prereq(self):
		return ""
	def analyze(self, pkginfo, tar):
		ret = [[],[],[]]
		if not hasattr(pkginfo, 'url'):
			ret[0].append(("missing-url", ()))
		return ret
	def type(self):
		return "pkgbuild"

```

Mostly, the code is self-explanatory. The following are the list of the methods that each namcap module must have:

*   **short_name**(self) Returns a string containing a short name of the module. Usually, this is the same as the basename of the module file.
*   **long_name**(self) Returns a string containing a concise description of the module. This description is used when listing all the rules using `namcap -r list`.
*   **prereq**(self) Return a string containing the prerequisites needed for the module to operate properly. Usually "" for modules processing PKGBUILDs and "tar" for modules processing package files. "extract" should be specified if the package contents should be extracted to a temporary directory before further processing.
*   **analyze**(self, pkginfo, tar) Should return a list comprising in turn of three lists: of error tags, warning tags and information tags respectively. Each member of these tag lists should be a tuple consisting of two components: **the short, hyphenated form** of the tag with the appropriate format specifiers (%s, etc.) The first word of this string must be the tag name. The human readable form of the tag should be put in the tags file. The format of the tags file is described below; and **the parameters** which should replace the format specifier tokens in the final output.
*   **type**(self) "pkgbuild" for a module processing PKGBUILDs, "tarball" for a module processing a binary package file.

The tags file consists of lines specifying the human readable form of the hyphenated tags used in the namcap code. A line beginning with a '#' is treated as a comment. Otherwise the format of the file is:

```
 machine-parseable-tag %s :: This is machine parseable tag %s

```

Note that a double colon (::) is used to separate the hyphenated tag from the human readable description.

## Namcap reports

**namcap-reports** is an automatically generated report obtained after running namcap against the core, extra and community trees.

How it works:

*   namcap is run against the entire [ABS](/index.php/ABS "ABS") tree to make `namcap.log`.
*   The packages in core, extra and community are put in files named core, extra and community respectively (using `pacman -Slq`).
*   `namcap-report.py` takes the code and prepares the report and RSS feeds, which is then copied to the webserver.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Namcap&oldid=376934](https://wiki.archlinux.org/index.php?title=Namcap&oldid=376934)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Package management](/index.php/Category:Package_management "Category:Package management")
*   [Package development](/index.php/Category:Package_development "Category:Package development")