**Advertencia:** Los ayudantes de AUR **no estan soportados** por Arch Linux. Se recomienda familiarizarse con el [proceso manual de construcción](/index.php/Arch_User_Repository_(Espa%C3%B1ol)#Instalar_paquetes "Arch User Repository (Español)") para estar preparado para solucionar posibles problemas por su cuenta.

**Nota:** No edite esta sección antes de la discusión en [Talk:AUR helpers](/index.php/Talk:AUR_helpers "Talk:AUR helpers").

Los ayudantes de AUR están creados para automatizar ciertas tareas para el [Arch User Repository (Español)](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)").La mayoría de los ayudantes de AUR pueden buscar paquetes en el AUR y recuperar sus [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") - otros adicionalmente ayudan con el proceso de construcción e instalación.

[Pacman](/index.php/Pacman "Pacman") sólo maneja actualizaciones de paquetes pre-construidos en sus repositorios. Los paquetes AUR se redistribuyen en forma de [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") y necesitan un ayudante AUR para automatizar el proceso de reconstrucción. Sin embargo, tenga en cuenta que puede ser necesario reconstruir un paquete cuando se actualizan las dependencias de la biblioteca compartida, no sólo cuando se actualiza el propio paquete.

Dado que los ayudantes de AUR no son compatibles, no están presentes en los [Repositorios Oficiales](/index.php/Official_repositories "Official repositories").

## Legend

Las columnas de la [Tabla comparativa](#Comparison_table) tienen el siguiente significado:

	Revisión de archivos

	No obtiene el PKGBUILD *de forma predeterminada* ; o, alerta al usuario y le ofrece la oportunidad de inspeccionar el PKGBUILD manualmente antes de que se obtenga. Se sabe que algunos ayudantes obtienen PKGBUILD antes de que el usuario pueda inspeccionarlos, lo que **permite que se ejecute código malicioso**. Revise [Help:Reading (Español)#Cargar fuentes](/index.php/Help:Reading_(Espa%C3%B1ol)#Cargar_fuentes "Help:Reading (Español)")

	Vista de diferencias

	Posibilidad de ver las diferencias de paquetes en la inspección. Además de PKGBUILD, esto incluye cambios en los archivos `.install` or `.patch`.

	Clonado en Git

	Utiliza [git-clone(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-clone.1) por defecto para recuperar archivos de compilación de la AUR.

	Analizador confiable

	Habilidad para manejar paquetes complejos mediante el uso de los metadatos provistos ([RPC](/index.php/Aurweb_RPC_interface "Aurweb RPC interface")/.SRCINFO) en lugar de [analizar](https://en.wikipedia.org/wiki/Parsing#Parser "w:Parsing") PKGBUILD , como [aws-cli-git](https://aur.archlinux.org/packages/aws-cli-git/).

	Solucionador confiable

	Habilidad para resolver correctamente y construir cadenas de dependencia complejas, como [ros-lunar-desktop](https://aur.archlinux.org/packages/ros-lunar-desktop/).

	Paquetes divididos

	Habilidad para construir e instalar correctamente::

*   Múltiples paquetes de la misma base de paquetes, sin reconstruir o reinstalar varias veces, como [clion](https://aur.archlinux.org/packages/clion/)
*   Paquetes divididos que dependen de un paquete de la misma base de paquetes, como [libc++](https://aur.archlinux.org/packages/libc%2B%2B/) y [libc++abi](https://aur.archlinux.org/packages/libc%2B%2Babi/).
*   Dividir paquetes de forma independiente, como [python-pyalsaaudio](https://aur.archlinux.org/packages/python-pyalsaaudio/) y [python2-pyalsaaudio](https://aur.archlinux.org/packages/python2-pyalsaaudio/).

	Interacción por lotes

	Posibilidad de avisar antes del proceso de compilación y del paquete de transacciones, en particular:

1.  Resumen combinado de repositorio y actualizaciones de paquetes AUR;
2.  Resolución de conflictos de paquetes y elección de proveedores.

	Finalización de shell

	[Finalización de pestaña](https://en.wikipedia.org/wiki/Command-line_completion "w:Command-line completion") está disponible para los [shells](/index.php/Shell "Shell") listados.

**Nota:** *Opcional* significa que una característica está disponible, pero sólo a través de un argumento de la línea de comandos o una opción de configuración. *Parcial* significa que una característica no está totalmente implementada, o que se desvía parcialmente de los criterios dados.

## Tabla comparativa

### Búsqueda y descarga

| Nombre | Escrito en | Clonado en Git | Analizador confiable | Solucionador confiable | Finalización de shell | Especificación |
| [auracle-git](https://aur.archlinux.org/packages/auracle-git/) | C++ | [Yes](https://github.com/falconindy/auracle/commit/c73bbee) | Si | Si | bash | imprime orden de compilación |
| [pbget](https://aur.archlinux.org/packages/pbget/) | Python | Si | Si | – | – | – |
| [repoctl](https://aur.archlinux.org/packages/repoctl/) | Go | No | [Yes](https://github.com/goulash/pacman/blob/master/aur/aur.go) | – | zsh | [repositorio local](/index.php/Local_repository "Local repository") |
| [yaah](https://aur.archlinux.org/packages/yaah/) | Bash | Optional | Si | – | bash | – |
| [aurel](https://aur.archlinux.org/packages/aurel/)
<small>([discontinued](https://bbs.archlinux.org/viewtopic.php?pid=1522459#p1522459))</small> | Emacs Lisp | No | Si | – | – | integración con [emacs](/index.php/Emacs "Emacs") |
| [cower](https://aur.archlinux.org/packages/cower/)
<small>([discontinued](https://github.com/falconindy/cower#description))</small> | C | No | Si | – | bash, zsh | soporte regex |

### Download and build

| Nombre | Escrito en | Revisión de archivos | Vista de diferencias | Clonado en Git | Analizador confiable | Solucionador confiable | Paquetes divididos | Finalización de shell | Especificación |
| [aurget](https://aur.archlinux.org/packages/aurget/) | Bash | No | [No](https://github.com/pbrisbin/aurget/issues/41) | No | No | No | [No](https://github.com/pbrisbin/aurget/issues/40) | bash, zsh | – |
| [aurutils](https://aur.archlinux.org/packages/aurutils/) | Bash/C | Si | Si | Si | Si | Si | Si | bash, zsh | [modular](https://en.wikipedia.org/wiki/Modular_programming "w:Modular programming"), [repositorio local](/index.php/Local_repository "Local repository"), [firma del paquete](/index.php/Package_signing "Package signing"), [construye en un chroot limpio](/index.php/DeveloperWiki:Building_in_a_clean_chroot "DeveloperWiki:Building in a clean chroot") |
| [bauerbill](https://aur.archlinux.org/packages/bauerbill/) | Python | Si | No | Si | Si | Si | Si | bash, zsh | `bb-wrapper` para *pacman* , es un empaquetador de confianza |
| [PKGBUILDer](https://aur.archlinux.org/packages/PKGBUILDer/) | Python | No | [No](https://github.com/Kwpolska/pkgbuilder/issues/36) | Si | Si | Si | [Partial](https://github.com/Kwpolska/pkgbuilder/issues/39) | – | `pb` un empaquetador para *pacman* |
| [repofish](https://aur.archlinux.org/packages/repofish/) | Bash | No | Si | Si | No | No | No | – | [repositorio local](/index.php/Local_repository "Local repository") |
| [rua](https://aur.archlinux.org/packages/rua/) | Rust | Si | [No](https://github.com/vn971/rua/issues/1) | Si | [Yes](https://github.com/vn971/rua/commit/fc8c2f3) | Si | Si | bash, zsh, fish | [bubblewrap](/index.php/Bubblewrap "Bubblewrap"), revisa los `.pkg.tar` |
| [burgaur](https://aur.archlinux.org/packages/burgaur/)
<small>([discontinued](https://github.com/m45t3r/burgaur/issues/7#issuecomment-365599675))</small> | Python/C | No | No | No | No | No | No | – | empaquetador de *cower* |
| [spinach](https://aur.archlinux.org/packages/spinach/)
<small>([discontinued](https://github.com/floft/spinach))</small> | Bash | Si | No | No | No | No | No | – | – |

### Empaquetadores de Pacman

**Advertencia:** Los empaquetadores de [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8) resumen el trabajo del gestor de paquetes. Pueden (opcionalmente o por defecto) introducir [banderas inseguras](/index.php/System_maintenance#Avoid_certain_pacman_commands "System maintenance"), u otro comportamiento inesperado que conduzca a un sistema defectuoso.

| Nombre | Escrito en | Revisión de archivos | Vista de diferencias | Clonado en Git | Analizador confiable | Solucionador confiable | Paquetes divididos | Banderas inseguras | Finalización de shell | Especificación |
| [aura](https://aur.archlinux.org/packages/aura/) | Haskell | No | [Parcial](https://github.com/aurapm/aura/blob/89bf702/aura/src/Aura/Pkgbuild/Records.hs) | [No](https://github.com/aurapm/aura/pull/346) | [Yes](https://github.com/aurapm/aura/commit/7848e983) | No | [No](https://github.com/aurapm/aura/issues/353) | – | bash, zsh | – |
| [packer-aur-git](https://aur.archlinux.org/packages/packer-aur-git/) | Bash | No | No | No | No | No | No | – | – | – |
| [pakku](https://aur.archlinux.org/packages/pakku/) | Nim | Si | [Yes](https://github.com/kitsunyan/pakku/commit/396e9f4) | Si | Si | Si | Si | [-Sy](https://github.com/kitsunyan/pakku/wiki/Native-Pacman-Explanation) | bash, zsh | buscar claves PGP |
| [pikaur](https://aur.archlinux.org/packages/pikaur/) | Python | Si | Si | Si | Si | Si | Si | [-Sy](https://github.com/actionless/pikaur#pikaur) | bash, fish, zsh | [usuarios dinámicos](http://0pointer.net/blog/dynamic-users-with-systemd.html), interacción por lotes (1,2) |
| [trizen](https://aur.archlinux.org/packages/trizen/) | Perl | Si | Si | [Yes](https://github.com/trizen/trizen/commit/6fb0cc9) | [Yes](https://github.com/trizen/trizen/commit/7ab7ee5f) | Si | [Parcial](https://github.com/trizen/trizen/issues/46) | [-Ud*](https://github.com/trizen/trizen/commit/9e7b40e) | bash, fish, zsh | – |
| [wrapaur](https://aur.archlinux.org/packages/wrapaur/) | Bash | Si | No | Si | No | No | No | – | – | – |
| [yay](https://aur.archlinux.org/packages/yay/) | Go | Si | [Yes](https://github.com/Jguer/yay/pull/447) | [Yes](https://github.com/Jguer/yay/pull/297) | Si | [Yes](https://github.com/Jguer/yay/pull/866) | Si | [-Sy*](https://github.com/Jguer/yay/commit/3bdb534)
[--ask*](https://github.com/Jguer/yay/commit/ea5a94e) | bash, fish, zsh | busca claves PGP, interacción por lotes (1,2) |
| [aurman](https://aur.archlinux.org/packages/aurman/)
<small>([discontinued](https://github.com/polygamma/aurman#stopped-development-for-public-use))</small> | Python | Si | Si | Si | Si | [No](https://github.com/polygamma/aurman/issues/259) | Si | [-Sy*](https://github.com/polygamma/aurman/commit/6c02ba3)
[--ask*](https://github.com/polygamma/aurman#make-use-of-the-undocumented---ask-flag-of-pacman) | bash, fish | busca claves PGP, interacción por lotes (1,2) |
| [yaourt](https://aur.archlinux.org/packages/yaourt/)
<small>([discontinued](https://github.com/archlinuxfr/yaourt/issues/382#issuecomment-437461631))</small> | Bash/C | [No](https://github.com/archlinuxfr/yaourt/blob/34b5c0b/src/lib/aur.sh#L54-L72) | Opcional | Opcional | No | [No](https://github.com/archlinuxfr/yaourt/issues/186) | [No](https://github.com/archlinuxfr/yaourt/issues/85) | [-Sy](https://github.com/archlinuxfr/yaourt/blob/d30823e/yaourt/yaourt#L1773) | bash, fish, zsh | [construcción sucia](https://lists.archlinux.org/pipermail/aur-general/2015-August/031314.html), interacción por lotes (1) |

## Graphical

**Warning:** Usage of graphical AUR helpers may lead to a defective system, for example through unattended [partial upgrades](/index.php/Partial_upgrades "Partial upgrades").

*   **Argon** — GTK+ 3 pacman wrapper written in Python.

	[https://github.com/14mRh4X0r/arch-argon](https://github.com/14mRh4X0r/arch-argon) || [argon](https://aur.archlinux.org/packages/argon/)

*   **Cylon** — TUI pacman wrapper written in Bash.

	[https://github.com/gavinlyonsrepo/cylon](https://github.com/gavinlyonsrepo/cylon) || [cylon](https://aur.archlinux.org/packages/cylon/)

*   **Pamac** — Standalone GTK+ 3 package manager using [libalpm(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libalpm.3) written in Vala.

	[https://gitlab.manjaro.org/applications/pamac](https://gitlab.manjaro.org/applications/pamac) || [pamac-aur](https://aur.archlinux.org/packages/pamac-aur/)

*   **Pakku GUI** — GTK+ 3 frontend for pakku written in Python.

	[https://gitlab.com/mrvik/pakku-gui](https://gitlab.com/mrvik/pakku-gui) || [pakku-gui](https://aur.archlinux.org/packages/pakku-gui/)

*   **PkgBrowser** — Qt 5 read-only browser for repository packages and AUR written in Python.

	[https://bitbucket.org/kachelaqa/pkgbrowser](https://bitbucket.org/kachelaqa/pkgbrowser) || [pkgbrowser](https://aur.archlinux.org/packages/pkgbrowser/)

*   **Octopi** — Qt 5 pacman wrapper written in C++. May lead to defective system as [enabled on install](https://github.com/aarnt/octopi/blob/271c7e1/octopi.install) notifier service [regularly performs](https://github.com/aarnt/octopi/issues/134#issuecomment-142099266) [partial upgrades](/index.php/Partial_upgrades "Partial upgrades").

	[https://octopiproject.wordpress.com/](https://octopiproject.wordpress.com/) || [octopi](https://aur.archlinux.org/packages/octopi/)

## Mantenimiento

*   **aur-out-of-date** — Utiliza APIs de *hoster* para comprobar si hay cambios en los paquetes AUR.

	[https://github.com/simon04/aur-out-of-date](https://github.com/simon04/aur-out-of-date) || [aur-out-of-date](https://aur.archlinux.org/packages/aur-out-of-date/)

*   **pkgbuild-watch** — Busca cambios en las páginas web anteriores

	[http://kmkeen.com/pkgbuild-watch](http://kmkeen.com/pkgbuild-watch) || [pkgbuild-watch](https://aur.archlinux.org/packages/pkgbuild-watch/)

*   **pkgbuildup** — Ayuda a los mantenedores de paquetes AUR a actualizar automáticamente los archivos PKGBUILD. Soporta una sintaxis de variables de plantillas.

	[https://github.com/fasheng/pkgbuildup](https://github.com/fasheng/pkgbuildup) || [pkgbuildup-git](https://aur.archlinux.org/packages/pkgbuildup-git/)

*   **pkgoutofdate** — Analiza la URL de origen de PKGBUILDs e intenta encontrar nuevas versiones de paquetes incrementando el número de versión y enviando peticiones al servidor web.

	[https://github.com/anatol/pkgoutofdate](https://github.com/anatol/pkgoutofdate) || [pkgoutofdate-git](https://aur.archlinux.org/packages/pkgoutofdate-git/)

## Subida

*   [aur4_import.sh](https://github.com/JonnyJD/PKGBUILDs/blob/master/_bin/aur4_import.sh) — Divide un paquete de un repositorio git con múltiples paquetes, añadiendo/actualizando `.SRCINFO` para cada confirmación.
*   [aur4_make_submodule.sh](https://github.com/JonnyJD/PKGBUILDs/blob/master/_bin/aur4_make_submodule.sh) — Reemplaza un paquete en un repositorio git más grande con un submódulo AUR 4, incluyendo `.SRCINFO`.