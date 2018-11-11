**Advertencia:**

*   Los ayudantes de AUR **no** estan [soportados](https://bbs.archlinux.org/viewtopic.php?pid=828254#p828254) por Arch Linux. Se recomienda familiarizarse con el [proceso manual de construcción](/index.php/Arch_User_Repository_(Espa%C3%B1ol)#Instalar_paquetes "Arch User Repository (Español)") para estar preparado para solucionar posibles problemas por su cuenta.
*   Los ayudantes de AUR pueden replicar el uso de [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8) para los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"), como `pacman -Syu`. Este uso puede desviarse de *pacman* de varias maneras; por lo tanto **no** es soportado o recomendado.

Los ayudantes de AUR están creados para automatizar ciertas tareas para el [Arch User Repository (Español)](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)").

## Contents

*   [1 Construir y buscar](#Construir_y_buscar)
    *   [1.1 Activo](#Activo)
    *   [1.2 Sólo búsqueda](#S.C3.B3lo_b.C3.BAsqueda)
    *   [1.3 Descontinuado o problemático](#Descontinuado_o_problem.C3.A1tico)
*   [2 Bibliotecas](#Bibliotecas)
*   [3 Mantenimiento](#Mantenimiento)
*   [4 Subida](#Subida)

## Construir y buscar

**Nota:** No edite esta sección antes de la discusión en [Talk:AUR helpers](/index.php/Talk:AUR_helpers "Talk:AUR helpers").

Las columnas tienen el siguiente significado:

*   **Seguro**: no [Recarga](/index.php/Help:Reading_(Espa%C3%B1ol)#Recarga "Help:Reading (Español)") el PKGBUILD de forma predeterminada; o bien, alerta al usuario y le ofrece la oportunidad de inspeccionar el PKGBUILD manualmente antes de que se obtenga. Se sabe que algunos ayudantes crean PKGBUILDs antes de que el usuario pueda inspeccionarlos, **permitiendo que se ejecute código malicioso**. **Opcional** significa que hay un indicador de línea de comandos o una opción de configuración para evitar el abastecimiento automático antes de la visualización.
*   **Construcción limpia**: no exporta nuevas variables que pueden impedir un proceso de compilación con exito.
*   **Pacman nativo**: cuando se utiliza como sustituto de [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8) como por ejemplo `pacman -Syu`, los siguientes son obedecidos *por defecto* :[[1]](https://wiki.archlinux.org/index.php?title=Talk:AUR_helpers&oldid=515160#Add_.22pacman_wrap.22_column)

	-no separar comandos, por ejemplo `pacman -Syu` no se divide en `pacman -Sy` y `pacman -S *packages*`;

	- use *pacman* directamente en lugar de la manipulación manual de la base de datos o el uso de [libalpm(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libalpm.3).

	Además [Evite ciertos comandos de pacman](/index.php/System_maintenance_(Espa%C3%B1ol)#Evite_ciertos_comandos_de_pacman "System maintenance (Español)") como `pacman -Ud`, `pacman -Rdd`, `pacman --ask` o `pacman --force` **no** se utilizan.

*   **Analizador confiable**: capacitado para manejar paquetes complejos utilizando los metadatos proporcionados (RPC/.SRCINFO) en vez de PKGBUILD [parsing](https://en.wikipedia.org/wiki/Parsing#Parser "w:Parsing"), como [aws-cli-git](https://aur.archlinux.org/packages/aws-cli-git/).
*   **Solucionador confiable**: capacitado para resolver correctamente y construir cadenas de dependencia complejas, como [ros-lunar-desktop](https://aur.archlinux.org/packages/ros-lunar-desktop/).
*   **Paquetes divididos**: capacitado de construir e instalar correctamente:

	-Múltiples paquetes desde la misma base de paquetes, sin necesidad de reconstruir o reinstalar varias veces, tales como [clion](https://aur.archlinux.org/packages/clion/)

	-Dividir paquetes que dependen de un paquete de la misma base de paquetes, tales como [libc++](https://aur.archlinux.org/packages/libc%2B%2B/) y [libc++abi](https://aur.archlinux.org/packages/libc%2B%2Babi/).

	-Divide los paquetes de forma independiente, como por ejemplo [python-pyalsaaudio](https://aur.archlinux.org/packages/python-pyalsaaudio/) y [python2-pyalsaaudio](https://aur.archlinux.org/packages/python2-pyalsaaudio/).

*   **Clonado en Git**: usa [git-clone(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-clone.1) por defecto para recuperar los archivos de compilación desde el AUR.
*   **Vista de diferencias**: capacitado para ver las diferencias de paquetes en la inspección. Además de la PKGBUILD, esto incluye cambios en archivos como `.install` o `.patch`.
*   **Interacción por lotes**: capacidad de provocar una sucesión directa, en particular de:

1.  Inspección de PKGBUILDs;
2.  Resumen de actualizaciones de paquetes;
3.  Resolución de conflictos de paquetes e instalaciones.

	Un asterisco denota funcionalidad habilitada específicamente por el usuario.

*   **Completado de shell**: [tab completion](https://en.wikipedia.org/wiki/Command-line_completion "w:Command-line completion") está disponible para los [intérpretes de línea de órdenes](/index.php/Shell_(Espa%C3%B1ol) "Shell (Español)") listados.

**Nota:**

*   Las filas de la tabla están ordenadas por valores de columna, donde *Sí* o *N/A* tienen prioridad sobre *Parcial* u *Opcional* y *No*, o alfabéticamente si los valores son iguales.
*   *Opcional* significa que una característica está disponible, pero sólo a través de un argumento de la línea de comandos o una opción de configuración. Por "parcial" se entiende que una característica no se aplica plenamente o que se desvía parcialmente de los criterios dados.

### Activo

| Nombre | Escrito en | Seguro | Construcción limpia | Nativo de pacman | Analizador confiable | Solucionador confiable | Paquetes divididos | Clonado en Git | Vista de diferencias | Interacción por lotes | Completado de shell | Especificación |
| [aurman](https://aur.archlinux.org/packages/aurman/) | Python | Si | Si | Si | Si | [Si](https://github.com/polygamma/aurman/wiki/Description-of-the-aurman-dependency-solving) | Si | Si | Si | 1, [2*, 3*](https://github.com/polygamma/aurman#question-5) | bash, fish | obtiene claves pgp, ordena por popularidad |
| [aurutils](https://aur.archlinux.org/packages/aurutils/) | Bash/C | Si | Si | N/A | Si | Si | Si | Si | Si | 1 | zsh | [vifm](/index.php/Vifm "Vifm"), [Repositorio local personalizado](/index.php/Pacman/Tips_and_tricks_(Espa%C3%B1ol)#Repositorio_local_personalizado "Pacman/Tips and tricks (Español)"), [Package signing](/index.php/Pacman/Package_signing_(Espa%C3%B1ol) "Pacman/Package signing (Español)"), soporta [clean chroot](/index.php/DeveloperWiki:Building_in_a_clean_chroot "DeveloperWiki:Building in a clean chroot") , ordena por votos / popularidad |
| [pakku](https://aur.archlinux.org/packages/pakku/) | Nim | Si | [Si](https://github.com/kitsunyan/pakku/commit/864cc0373fd6095295f68cc44d1657bd17269732) | [Parcial](https://github.com/kitsunyan/pakku/wiki/Native-Pacman-Explanation) | Si | Si | Si | Si | [Si](https://github.com/kitsunyan/pakku/commit/396e9f44c4f5a79c7b9238835599387f6ff418fe) | 1 | bash, zsh | soporta [ABS](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)") , comentarios AUR, obtiene claves PGP |
| [yay](https://aur.archlinux.org/packages/yay/) | Go | Si | Si | [Parcial](https://github.com/Jguer/yay/issues/464) | Si | Si | Si | [Si](https://github.com/Jguer/yay/pull/297) | [Si](https://github.com/Jguer/yay/pull/447) | 1, 2, 3 | bash, fish, zsh | ordena por votos, recupera claves GP,[prompt architecture](https://github.com/Jguer/yay/commit/4bcd3a6297052714e91e3f886602ce5c12d15786) |
| [bauerbill](https://aur.archlinux.org/packages/bauerbill/) | Python | Si | Si | Si | Si | Si | Si | Si | No | 1 | bash, zsh | Administrador de confianza, soporta [ABS](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)") , extensión de Powerpill |
| [PKGBUILDer](https://aur.archlinux.org/packages/PKGBUILDer/) | Python | Opcional | Si | [Si](https://github.com/Kwpolska/pkgbuilder/blob/master/docs/wrapper.rst) | Si | Si | [Parcial](https://github.com/Kwpolska/pkgbuilder/issues/39) | Si | [No](https://github.com/Kwpolska/pkgbuilder/issues/36) | 1* | - | Construcciones automáticas por defecto, use `-F` para desabilitar; multilenguaje |
| [naaman](https://aur.archlinux.org/packages/naaman/) | Python | Opcional | Si | N/A | Si | [Parcial](https://github.com/enckse/naaman/issues/19) | [Parcial](https://github.com/enckse/naaman/issues/20) | Si | No | 1* | bash | Construcciones automáticas por defecto, use `--fetch` para desabilitar, use `-d` para habilitar soluciones |
| [aura](https://aur.archlinux.org/packages/aura/) | Haskell | Opcional | Si | [Si](https://github.com/aurapm/aura/blob/master/aura/src/Aura/Pacman.hs) | [Si](https://github.com/aurapm/aura/commit/7848e9830cd880215f1d12a1c0294992428ea778) | No | [No](https://github.com/aurapm/aura/issues/353) | [No](https://github.com/aurapm/aura/pull/346) | [Parcial](https://github.com/aurapm/aura/blob/89bf702bd0539fa757265c4c54ea2192155f85ed/aura/src/Aura/Pkgbuild/Records.hs) | 1* | bash, zsh | Construcciones automáticas por defecto, use `--dryrun` para desabilitar, soporta [downgrade](/index.php/Downgrade "Downgrade") , multilenguaje |
| [repofish](https://aur.archlinux.org/packages/repofish/) | Bash | Opcional | Si | N/A | No | No | No | Si | Si | 1* | - | Construcción automática por defecto, use `check` o `update` para desabilitar, soporta [Repositorio local personalizado](/index.php/Pacman/Tips_and_tricks_(Espa%C3%B1ol)#Repositorio_local_personalizado "Pacman/Tips and tricks (Español)") |
| [wrapaur](https://aur.archlinux.org/packages/wrapaur/) | Bash | Si | Si | Si | No | No | No | Si | No | - | - | Actualiza mirrors, publica noticias y comentarios AUR |
| [aurget](https://aur.archlinux.org/packages/aurget/) | Bash | Opcional | Si | N/A | No | No | [No](https://github.com/pbrisbin/aurget/issues/40) | No | [No](https://github.com/pbrisbin/aurget/issues/41) | - | bash, zsh | ordenar por votos |

### Sólo búsqueda

| Nombre | Escrito en | Seguro | Analizador confiable | Solucionador confiable | Clonado en Git | Completado de shell | Especificación |
| [pbget](https://aur.archlinux.org/packages/pbget/) | Python | Si | Si | N/A | Si | - | - |
| [yaah](https://aur.archlinux.org/packages/yaah/) | Bash | Si | Si | N/A | Opcional | bash | - |
| [auracle-git](https://aur.archlinux.org/packages/auracle-git/) | C++ | Si | Si | Si | No | - | muestra ordenes de construcción |
| [cower](https://aur.archlinux.org/packages/cower/) | C | Si | Si | N/A | No | bash/zsh | soporta regex , ordenada por votos / popularidad |
| [package-query](https://aur.archlinux.org/packages/package-query/) | C | Si | No [[2]](https://github.com/archlinuxfr/package-query/issues/135) | N/A | N/A | - | - |
| [repoctl](https://aur.archlinux.org/packages/repoctl/) | Go | Si | Si [[3]](https://github.com/goulash/pacman/blob/master/aur/aur.go) | N/A | No | zsh | soporta repositorio local |

### Descontinuado o problemático

Esta tabla describe proyectos que o bien estan descontinuados por sus autores, o tienen problemas en *Seguridad* , *Construcción limpia* o *Pacman nativo* (ver [Activo](#Activo)) desatendido en los últimos 6 meses.

| Nombre | Escrito en | Seguro | Compilación limpia | Nativo de pacman | Analizador confiable | Solucionador confiable | Paquetes divididos | Clonado en Git | Vista de diferencias | Interacción por lotes | Completado de shell | Especificación |
| [aurel](https://aur.archlinux.org/packages/aurel/) [[4]](https://bbs.archlinux.org/viewtopic.php?pid=1522459#p1522459) | Emacs Lisp | Si | N/A | N/A | N/A | N/A | N/A | No | N/A | N/A | N/A | Integración Emacs ,no construye automáticamente |
| [pacaur](https://aur.archlinux.org/packages/pacaur/) [[5]](https://bbs.archlinux.org/viewtopic.php?pid=1755144#p1755144) | Bash/C | Si | Si | [No](https://github.com/rmarquis/pacaur/commit/d8f49188452785fb28afc017baadd01d9e24ba21) | Si | Si | Si | Si | Si | 1, 3 | bash, zsh | multilenguaje, ordena por votos / popularidad |
| [trizen](https://aur.archlinux.org/packages/trizen/) | Perl | Si | Si | [No](https://github.com/trizen/trizen/commit/ba687bc3c3e306e6f3942e95f825ed6a55d3ad69) | [Si](https://github.com/trizen/trizen/commit/7ab7ee5f9f1f5d971b731d092fc8e1dd963add4b) | Si | [Si](https://github.com/trizen/trizen/commit/3c94434c66ede793758f2bf7de84d68e3174e2ac) | [Si](https://github.com/trizen/trizen/commit/6fb0cc9e0ab66b8cca9493b0618ba4bab5fd2252) | Si | 1* | bash, zsh, fish | Construciones automáticas por defecto, use `-G` para deshabilitar, comentarios de AUR |
| [spinach](https://aur.archlinux.org/packages/spinach/) [[6]](https://github.com/floft/spinach) | Bash | [Si](https://github.com/floft/spinach/commit/545574700812eb369b9537370f085ec9e5c3f01a) | Si | N/A | No | No | No | No | No | - | - | - |
| [burgaur](https://aur.archlinux.org/packages/burgaur/) [[7]](https://github.com/m45t3r/burgaur/issues/7#issuecomment-365599675) | Python/C | Optional | Si | N/A | No | No | No | No | No | - | - | Wrapper de *cower* |
| [packer](https://www.archlinux.org/packages/?name=packer) | Bash | No | Si | Si | No | No | No | No | No | - | - | - |
| [yaourt](https://aur.archlinux.org/packages/yaourt/) | Bash/C | No [[8]](https://github.com/archlinuxfr/yaourt/blob/f373121d23d87031a24135fee593115832d803ec/src/lib/aur.sh#L47) [[9]](https://github.com/archlinuxfr/yaourt/blob/d9790e29cd7194535c793f51d185b7130a396916/src/lib/pkgbuild.sh.in#L415-L438) | [No](https://lists.archlinux.org/pipermail/aur-general/2015-August/031314.html) | No | No | [No](https://github.com/archlinuxfr/yaourt/issues/186) | [No](https://github.com/archlinuxfr/yaourt/issues/85) | Opcional | Opcional | 2 | bash, zsh, fish | Respaldo, soporte ABS, comentarios AUR, multilenguaje |

## Bibliotecas

*   **haskell-archlinux** — Biblioteca para acceder al AUR y metadatos del paquete desde el lenguaje de programación Haskell

	[http://hackage.haskell.org/package/archlinux](http://hackage.haskell.org/package/archlinux) || [haskell-archlinux](https://aur.archlinux.org/packages/haskell-archlinux/)

*   **python3-aur** — Python 3 módulos para acceder a la información del paquete AUR y automatizar las interacciones AUR.

	[http://xyne.archlinux.ca/projects/python3-aur](http://xyne.archlinux.ca/projects/python3-aur) || [python3-aur](https://aur.archlinux.org/packages/python3-aur/)

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