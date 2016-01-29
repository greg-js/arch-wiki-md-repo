# getty

A **getty** is the generic name for a program which manages a terminal line and its connected terminal. Its purpose is to protect the system from unauthorized access. Generally, each getty process is started by [init](/index.php/Init "Init") and manages a single terminal line. Within the context of a typical Arch Linux installation, the terminals managed by the getty processes are implemented as virtual consoles. Six of these virtual consoles are provided by default and they are usually accessible by pressing `Ctrl+Alt+F1` through `Ctrl+Alt+F6`.

## Contents

*   [1 agetty](#agetty)
*   [2 fgetty](#fgetty)
*   [3 Others](#Others)
*   [4 See also](#See_also)

## agetty

The `agetty` program is the default getty in Arch Linux and is part of the [util-linux](https://www.archlinux.org/packages/?name=util-linux) package which is included in the base Arch Linux installation. It modifies the TTY settings while waiting for a login so that newlines are not translated to CR–LFs. This tends to cause a "staircase effect" for messages printed to the console (printed by programs started by [Init](/index.php/Init "Init") for instance).

## fgetty

The [fgetty](https://aur.archlinux.org/packages/fgetty/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/fgetty)]</sup> unofficial package is available in the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") and is derived from mingetty. It does not cause the "staircase effect". The patched [fgetty-pam](https://aur.archlinux.org/packages/fgetty-pam/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/fgetty-pam)]</sup> is currently required for [Pluggable Authentication Module](https://en.wikipedia.org/wiki/Pluggable_authentication_module "wikipedia:Pluggable authentication module") (including SHA-2) support.

## Others

*   **mingetty** AUR [mingetty](https://aur.archlinux.org/packages/mingetty/)<sup><small>AUR</small></sup>
*   **[qingy](/index.php/Qingy "Qingy")** AUR package: [qingy](https://aur.archlinux.org/packages/qingy/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/qingy)]</sup>
*   **fbgetty** official package: [fbgetty](https://www.archlinux.org/packages/?name=fbgetty)
*   **ngetty** AUR: [ngetty](https://aur.archlinux.org/packages/ngetty/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ngetty)]</sup>
*   **rungetty** AUR: [rungetty](https://aur.archlinux.org/packages/rungetty/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/rungetty)]</sup>
*   **mgetty** AUR: [mgetty](https://aur.archlinux.org/packages/mgetty/)<sup><small>AUR</small></sup>

## See also

*   [Display manager](/index.php/Display_manager "Display manager")
*   [Disable clearing of boot messages](/index.php/Disable_clearing_of_boot_messages "Disable clearing of boot messages")
*   [Automatic login to virtual console](/index.php/Automatic_login_to_virtual_console "Automatic login to virtual console")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Getty&oldid=399048](https://wiki.archlinux.org/index.php?title=Getty&oldid=399048)"