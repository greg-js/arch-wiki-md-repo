## Contents

*   [1 Projects](#Projects)
*   [2 Articles](#Articles)
    *   [2.1 Server migration](#Server_migration)
    *   [2.2 Policies](#Policies)
    *   [2.3 Organization](#Organization)
    *   [2.4 Packaging guidelines](#Packaging_guidelines)
    *   [2.5 Packaging reference](#Packaging_reference)
    *   [2.6 Important public information](#Important_public_information)
    *   [2.7 Internals](#Internals)
    *   [2.8 Future](#Future)
    *   [2.9 Artwork and branding](#Artwork_and_branding)
    *   [2.10 Web development](#Web_development)
    *   [2.11 Release engineering](#Release_engineering)
    *   [2.12 Devops Team](#Devops_Team)
    *   [2.13 Reproducible builds](#Reproducible_builds)

## Projects

Links:

*   [cgit repository interface](https://git.archlinux.org/)
*   [GitHub organization](https://github.com/archlinux)
*   [arch-projects mailing list](https://lists.archlinux.org/listinfo/arch-projects)
*   [#archlinux-projects IRC channel](ircs://chat.freenode.net/archlinux-projects)

| Project | Description | Languages | Developer | Links |
| Pyalpm | alpm Python bindings | Python, C | Jelle | [GitHub](https://github.com/archlinux/pyalpm) |
| Pacman | Package Manager | Bash, C | Allan, agregory | [cgit](https://git.archlinux.org/pacman.git/), [bugs](https://bugs.archlinux.org/index.php?project=3&do=index&switch=1) [IRC #archlinux-pacman](ircs://chat.freenode.net/archlinux-pacman) |
| pacman-contrib | Contribution scripts to pacman | Bash, C | Demize, Polyzen | [GitHub](https://github.com/kyrias/pacman-contrib) |
| Arch Security Tracker | Python | anthraxx | [security.archlinux.org](https://security.archlinux.org), [IRC #archlinux-security](ircs://chat.freenode.net/archlinux-security) |
| [Archweb](/index.php/DeveloperWiki:Archweb "DeveloperWiki:Archweb") | The archlinux.org website | Python (Django) | jelle | [archlinux.org](https://archlinux.org), [GitHub](https://github.com/archlinux/archweb), [bugs](https://bugs.archlinux.org/index.php?string=archweb&project=1) |
| AURWeb | The page and system for the AUR website | PHP, HTML, MySQL | Lukas, Demize | [aur.archlinux.org](https://aur.archlinux.org), [cgit](https://git.archlinux.org/aurweb.git/), [bugs](https://bugs.archlinux.org/index.php?project=2&do=index&switch=1), [IRC #archlinux-aurweb](ircs://chat.freenode.net/archlinux-aurweb) |
| Infrastructure | Maintains the infrastructure to Arch Linux | Ansible, Python | Bluewind, Grazzolini and more | [cgit](https://git.archlinux.org/infrastructure.git/), [IRC #archlinux-devops](ircs://chat.freenode.net/archlinux-devops) |
| [Reproducible builds](/index.php/DeveloperWiki:Reproducible_builds "DeveloperWiki:Reproducible builds") | General project to achieve reproducible builds | Bash, PKGBUILDs | Anthraxx, Jelle, Foxboron, Eschwartz, Sangy | [reproducible-builds.org](https://reproducible-builds.org/), [Debian wiki](https://wiki.debian.org/ReproducibleBuilds), [IRC #archlinux-reproducible](ircs://chat.freenode.net/archlinux-reproducible) |
| devtools | Packaging tools for developers and packagers | Bash | All the devs | [cgit](https://git.archlinux.org/devtools.git/), [bugs](https://bugs.archlinux.org/index.php?string=devtools&project=1) |
| [dbscripts](/index.php/DeveloperWiki:dbscripts "DeveloperWiki:dbscripts") | Scripts to release and manage packages into the repositories | Bash | Pierres, Eschwartz | [GitHub](https://github.com/archlinux/dbscripts) |
| Vagrant & Docker images | Bash | Shibumi, Pierre | [arch-boxes GH](https://github.com/archlinux/arch-boxes), [archlinux-docker GH](https://github.com/archlinux/archlinux-docker) |

See also [Category:Arch projects](/index.php/Category:Arch_projects "Category:Arch projects").

## Articles

### Server migration

*   [DeveloperWiki:ServerMigration](/index.php/DeveloperWiki:ServerMigration "DeveloperWiki:ServerMigration")

### Policies

*   [DeveloperWiki:Policies](/index.php/DeveloperWiki:Policies "DeveloperWiki:Policies")

### Organization

*   [DeveloperWiki:Projects](/index.php/DeveloperWiki:Projects "DeveloperWiki:Projects")
*   [DeveloperWiki:Roll Call](/index.php/DeveloperWiki:Roll_Call "DeveloperWiki:Roll Call")
*   [DeveloperWiki:Linux Conferences](/index.php/DeveloperWiki:Linux_Conferences "DeveloperWiki:Linux Conferences")

### Packaging guidelines

*   [DeveloperWiki:HOWTO Be A Packager](/index.php/DeveloperWiki:HOWTO_Be_A_Packager "DeveloperWiki:HOWTO Be A Packager")
*   [DeveloperWiki:Systemd](/index.php/DeveloperWiki:Systemd "DeveloperWiki:Systemd")
*   [DeveloperWiki:Signing Packages](/index.php/DeveloperWiki:Signing_Packages "DeveloperWiki:Signing Packages")
*   [DeveloperWiki:Building in a Clean Chroot](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot "DeveloperWiki:Building in a Clean Chroot")
*   [DeveloperWiki:Package Submittal Rules](/index.php/DeveloperWiki:Package_Submittal_Rules "DeveloperWiki:Package Submittal Rules")
*   [DeveloperWiki:GNOME Guidelines](/index.php/DeveloperWiki:GNOME_Guidelines "DeveloperWiki:GNOME Guidelines")
*   [DeveloperWiki:Package Testing](/index.php/DeveloperWiki:Package_Testing "DeveloperWiki:Package Testing")
*   [DeveloperWiki:PKGBUILD.com](/index.php/DeveloperWiki:PKGBUILD.com "DeveloperWiki:PKGBUILD.com")

### Packaging reference

*   [DeveloperWiki:UID / GID Database](/index.php/DeveloperWiki:UID_/_GID_Database "DeveloperWiki:UID / GID Database")

### Important public information

*   [DeveloperWiki:UID / GID Database](/index.php/DeveloperWiki:UID_/_GID_Database "DeveloperWiki:UID / GID Database")

### Internals

*   [Category:DeveloperWiki:Server Configuration](/index.php/Category:DeveloperWiki:Server_Configuration "Category:DeveloperWiki:Server Configuration")
*   [DeveloperWiki:NewMirrors](/index.php/DeveloperWiki:NewMirrors "DeveloperWiki:NewMirrors")
*   [DeveloperWiki:Developer Checklist](/index.php/DeveloperWiki:Developer_Checklist "DeveloperWiki:Developer Checklist")

### Future

*   [DeveloperWiki:Goals](/index.php/DeveloperWiki:Goals "DeveloperWiki:Goals")

### Artwork and branding

*   [DeveloperWiki:TrademarkPolicy](/index.php/DeveloperWiki:TrademarkPolicy "DeveloperWiki:TrademarkPolicy")

### Web development

*   [DeveloperWiki:Website suggestions](/index.php/DeveloperWiki:Website_suggestions "DeveloperWiki:Website suggestions")

### Release engineering

*   [DeveloperWiki:iso building](/index.php/DeveloperWiki:iso_building "DeveloperWiki:iso building")

### Devops Team

*   [DeveloperWiki:Arch Services](/index.php/DeveloperWiki:Arch_Services "DeveloperWiki:Arch Services")
*   [DeveloperWiki:Server Upgrades](/index.php/DeveloperWiki:Server_Upgrades "DeveloperWiki:Server Upgrades")

### Reproducible builds

*   [DeveloperWiki:Reproducible builds](/index.php/DeveloperWiki:Reproducible_builds "DeveloperWiki:Reproducible builds")