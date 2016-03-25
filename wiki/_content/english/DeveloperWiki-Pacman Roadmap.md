This page does not provide a traditional roadmap. [Pacman](/index.php/Pacman "Pacman") releases are generally made after a major feature has been added and these get added in the order that patches are contributed.

Instead, this page provides a brief overview of major features being discussed for future inclusion in pacman. This does not represent a complete list of all areas of pacman development (or even areas currently being developed...). All discussion about pacman development should take place on the [pacman-dev](https://mailman.archlinux.org/pipermail/pacman-dev/) mailing list.

## Contents

*   [1 Potential Release Schedule](#Potential_Release_Schedule)
    *   [1.1 Pacman 5.1](#Pacman_5.1)
*   [2 New Feature Ideas](#New_Feature_Ideas)
    *   [2.1 Package Signing - Polishing](#Package_Signing_-_Polishing)
    *   [2.2 Optdepend Handling](#Optdepend_Handling)
    *   [2.3 Parallel operations](#Parallel_operations)
    *   [2.4 Iterator interface for databases](#Iterator_interface_for_databases)
*   [3 Future Release Plans](#Future_Release_Plans)

## Potential Release Schedule

This is **not** a for sure list by any means. This is simply to keep the main development team focused on a given release and what needs to be polished before we can push a major version out the door.

### Pacman 5.1

Applied:

## New Feature Ideas

### Package Signing - Polishing

**Idea:** Tidy up our current implementation of package signing.

**Flyspray:** [FS#28014](https://bugs.archlinux.org/task/28014) [FS#34741](https://bugs.archlinux.org/task/34741)

### Optdepend Handling

**Idea:** Currently optdepends in pacman serve no purpose other than informational. It would be useful if these could be handled in a similar fashion to regular dependencies for many operations. See [here](/index.php/User:Allan/Pacman_OptDepends "User:Allan/Pacman OptDepends") for a more detailed description of what is currently being implemented.

**Flyspray:** [FS#12708](https://bugs.archlinux.org/task/12708) (and others)

**Mailing List:** [https://mailman.archlinux.org/pipermail/pacman-dev/2011-August/013961.html](https://mailman.archlinux.org/pipermail/pacman-dev/2011-August/013961.html)

**Development branch:** [https://github.com/moben/pacman/tree/optdep](https://github.com/moben/pacman/tree/optdep)

### Parallel operations

**Idea:** Some things libalpm does are embarrassingly parallel, make it happen. Also, simply allow the library to be used in multithreaded environments even if we do not do parallel stuff on our own- namely DB loading stuff needs to be protected.

**Flyspray:** (None)

**Mailing List:** [https://mailman.archlinux.org/pipermail/pacman-dev/2011-February/012466.html](https://mailman.archlinux.org/pipermail/pacman-dev/2011-February/012466.html), [https://mailman.archlinux.org/pipermail/pacman-dev/2011-February/012508.html](https://mailman.archlinux.org/pipermail/pacman-dev/2011-February/012508.html)

### Iterator interface for databases

**Idea:** Provide an iterator interface for databases, especially those with 'files' entries, to keep memory usage in check.

**Mailing List:** [https://mailman.archlinux.org/pipermail/pacman-dev/2011-July/013816.html](https://mailman.archlinux.org/pipermail/pacman-dev/2011-July/013816.html)

## Future Release Plans

See [flyspray roadmap](https://bugs.archlinux.org/roadmap/proj3)