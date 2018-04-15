Related articles

*   [AurJson](/index.php/AurJson "AurJson")

This article provides documentation for the web interface through which it is possible to query the official repositories and obtain results in JSON format.

## Contents

*   [1 Package information](#Package_information)
    *   [1.1 Details](#Details)
    *   [1.2 Files](#Files)
*   [2 Package search](#Package_search)
    *   [2.1 Name or description](#Name_or_description)
    *   [2.2 Exact name](#Exact_name)
    *   [2.3 Description](#Description)
    *   [2.4 Repository](#Repository)
    *   [2.5 Architecture](#Architecture)
    *   [2.6 Maintainer](#Maintainer)
    *   [2.7 Packager](#Packager)
    *   [2.8 Flagged](#Flagged)
*   [3 See also](#See_also)

## Package information

Base URL: `https://www.archlinux.org/packages/`

### Details

Syntax: `/*repository*/*architecture*/*package*/json`

Example: [https://www.archlinux.org/packages/core/x86_64/coreutils/json/](https://www.archlinux.org/packages/core/x86_64/coreutils/json/)

### Files

Syntax: `/*repository*/*architecture*/*package*/files/json`

Example: [https://www.archlinux.org/packages/core/i686/coreutils/files/json/](https://www.archlinux.org/packages/core/i686/coreutils/files/json/)

## Package search

The interface supports the same query parameters as the [HTML search form](https://www.archlinux.org/packages/), except for `sort`.

Base URL: `https://www.archlinux.org/packages/search/json`

### Name or description

Parameter: `q`

Example: [https://www.archlinux.org/packages/search/json/?q=pacman](https://www.archlinux.org/packages/search/json/?q=pacman)

### Exact name

Parameter: `name`

Example: [https://www.archlinux.org/packages/search/json/?name=coreutils](https://www.archlinux.org/packages/search/json/?name=coreutils)

### Description

Parameter: `desc`

Example: [https://www.archlinux.org/packages/search/json/?desc=pacman](https://www.archlinux.org/packages/search/json/?desc=pacman)

### Repository

It is possible to use this parameter more than once in order to search in more than one repository (but note that omitting it altogether will search in all repositories).

Parameter: `repo`

Values: `Core`, `Extra`, `Testing`, `Multilib`, `Multilib-Testing`, `Community`, `Community-Testing`

Example: [https://www.archlinux.org/packages/search/json/?q=cursor&repo=Community&repo=Extra](https://www.archlinux.org/packages/search/json/?q=cursor&repo=Community&repo=Extra)

### Architecture

It is possible to use this parameter more than once in order to search for more than one architecture (but note that omitting it altogether will search for all architectures).

Parameter: `arch`

Values: `any`, `i686`, `x86_64`

Example: [https://www.archlinux.org/packages/search/json/?q=cursor&arch=any&arch=x86_64](https://www.archlinux.org/packages/search/json/?q=cursor&arch=any&arch=x86_64)

### Maintainer

Parameter: `maintainer`

Example: [https://www.archlinux.org/packages/search/json/?repo=Community&maintainer=orphan](https://www.archlinux.org/packages/search/json/?repo=Community&maintainer=orphan)

### Packager

Parameter: `packager`

### Flagged

Parameter: `flagged`

Values: `Flagged`, `Not+Flagged`

Example: [https://www.archlinux.org/packages/search/json/?arch=x86_64&flagged=Flagged](https://www.archlinux.org/packages/search/json/?arch=x86_64&flagged=Flagged)

## See also

*   [Forum thread](https://bbs.archlinux.org/viewtopic.php?id=170892)
*   Initial feature request: [FS#13026](https://bugs.archlinux.org/task/13026)
*   [Kittypack: A silly little tool to poke archlinux.org/packages for info](https://github.com/MrElendig/kittypack)