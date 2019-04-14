**[Package creation guidelines](/index.php/Arch_packaging_standards "Arch packaging standards")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Electron](/index.php/Electron_package_guidelines "Electron package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [R](/index.php/R_package_guidelines "R package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [Rust](/index.php/Rust_package_guidelines "Rust package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – <a class="mw-selflink selflink">Web</a> – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

This page describes how to package web applications.

## Separate user

For security reasons, every web application should be run as a separate (unprivileged) user (i.e. `*$pkgname*`).

**Note:** Traditionally, many web applications were run as the `http` user/group, which can be considered unsafe, as in such a scenario applications can read each other's files.

Refer to the [systemd-sysusers(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-sysusers.8), [sysusers.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sysusers.d.5), [systemd-tmpfiles(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-tmpfiles.8) and [tmpfiles.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tmpfiles.d.5) man pages for details on how to create users and deal with ownership of files and folders for that user in a package.

## Directory structure

The layout follows the [FHS](/index.php/Frequently_asked_questions#Does_Arch_follow_the_Linux_Foundation's_Filesystem_Hierarchy_Standard_(FHS)? "Frequently asked questions").

*   `/usr/share/webapps/*$pkgname*`: The application's *data directory* holds the files of the web application. Files are owned by `root` and are therefore readonly to the application user and group `*$pkgname*`.

*   `/etc/webapps/*$pkgname*`: The *configuration directory* of the application holds configuration files for the application (symlinked to the *data directory*). Files located here have to go to the [backup](/index.php/PKGBUILD#backup "PKGBUILD") array and are owned by the user and group `*$pkgname*`.

**Warning:** Files potentially containing authentication information **must be protected** (i.e. not readable by any other user or group on the system, except `root` and `*$pkgname*`)!

*   `/run/*$pkgname*`: The *runtime directory* of the application (owned by the user and group `*$pkgname*`). It can be used for sockets (e.g. in setups facilitating [socket activation](/index.php/UWSGI#Socket_activation "UWSGI")).

**Note:** According to the package guidelines on [directories](/index.php/Arch_package_guidelines#Directories "Arch package guidelines"), `/run` must not be contained in a package. Use [tmpfiles](/index.php/Systemd#Temporary_files "Systemd") to add the directory with matching permissions.

*   `/var/cache/*$pkgname*`: The *cache directory* of the application (owned by the user and group `*$pkgname*`). It (or subfolders in it) is symlinked to the *data directory* for applications requiring writable cache directories.

*   `/var/lib/*$pkgname*`: The *persistent storage* of the application (owned by the user and group `*$pkgname*`). It (or subfolders in it) is symlinked to the *data directory* for applications requiring persistent storage directories.