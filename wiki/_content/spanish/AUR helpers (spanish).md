**Nota:** En proceso de traducción

**Warning:**

*   Los ayudantes de AUR **no** estan [soportados](https://bbs.archlinux.org/viewtopic.php?pid=828254#p828254) por Arch Linux. Se recomienda familiarizarse con el [proceso manual de construcción](/index.php/Arch_User_Repository_(Espa%C3%B1ol)#Instalar_paquetes "Arch User Repository (Español)") para estar preparado para solucionar posibles problemas por su cuenta.
*   Los ayudantes de AUR pueden replicar el uso de [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8) para los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"), como `pacman -Syu`. Este uso puede desviarse de *pacman* de varias maneras; por lo tanto **no** es soportado o recomendado.

Los ayudantes de AUR están creados para automatizar ciertas tareas para el [Arch User Repository (Español)](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)").

## Contents

*   [1 Construir y buscar](#Construir_y_buscar)
    *   [1.1 Activo](#Activo)
    *   [1.2 Sólo búsqueda](#S.C3.B3lo_b.C3.BAsqueda)
    *   [1.3 Descontinuado o problemático](#Descontinuado_o_problem.C3.A1tico)
*   [2 Librerías](#Librer.C3.ADas)
*   [3 Mantenimiento](#Mantenimiento)
*   [4 Subida](#Subida)

## Construir y buscar

**Nota:** No edite esta sección antes de la discusión en [Talk:AUR helpers](/index.php/Talk:AUR_helpers "Talk:AUR helpers").

Las columnas tienen el siguiente significado:

*   *Seguro* : no [Recarga](https://wiki.archlinux.org/index.php/Help:Reading_(Espa%C3%B1ol)#Recarga) el PKGBUILD de forma predeterminada; o bien, alerta al usuario y le ofrece la oportunidad de inspeccionar el PKGBUILD manualmente antes de que se obtenga. Se sabe que algunos ayudantes crean PKGBUILDs antes de que el usuario pueda inspeccionarlos, **permitiendo que se ejecute código malicioso**. *Opcional* significa que hay un indicador de línea de comandos o una opción de configuración para evitar el abastecimiento automático antes de la visualización.
*   *Compilación limpia* : no exporta nuevas variables que pueden impedir un proceso de compilación con exito.
*   *Pacman nativo*: cuando se utiliza como sustituto de [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8) como por ejemplo `pacman -Syu`, los siguientes son obedecidos *por defecto* :[[2]](https://wiki.archlinux.org/index.php?title=Talk:AUR_helpers&oldid=515160#Add_.22pacman_wrap.22_column)

	-no separar comandos, por ejemplo `pacman -Syu` no se divide en `pacman -Sy` y `pacman -S *packages*`;

	- use *pacman* directamente en lugar de la manipulación manual de la base de datos o el uso de [libalpm(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libalpm.3).

	Además [Evite ciertos comandos de pacman](/index.php/System_maintenance_(Espa%C3%B1ol)#Evite_ciertos_comandos_de_pacman "System maintenance (Español)") como `pacman -Ud`, `pacman -Rdd`, `pacman --ask` o `pacman --force` **no** se utilizan.

*   *Analizador fiable*: capacitado para manejar paquetes complejos utilizando los metadatos proporcionados (RPC/.SRCINFO) en vez de PKGBUILD [parsing](https://en.wikipedia.org/wiki/Parsing#Parser "w:Parsing"), como [aws-cli-git](https://aur.archlinux.org/packages/aws-cli-git/).
*   *Solucionador fiable*:capacitado para resolver correctamente y construir cadenas de dependencia complejas, como [ros-lunar-desktop](https://aur.archlinux.org/packages/ros-lunar-desktop/).
*   *Paquetes divididos*:capacitado de construir e instalar correctamente:

	-Múltiples paquetes desde la misma base de paquetes, sin necesidad de reconstruir o reinstalar varias veces, tales como [clion](https://aur.archlinux.org/packages/clion/)

	-Dividir paquetes que dependen de un paquete de la misma base de paquetes, tales como [libc++](https://aur.archlinux.org/packages/libc%2B%2B/) y [libc++abi](https://aur.archlinux.org/packages/libc%2B%2Babi/).

	-Divide los paquetes de forma independiente, como por ejemplo [python-pyalsaaudio](https://aur.archlinux.org/packages/python-pyalsaaudio/) y [python2-pyalsaaudio](https://aur.archlinux.org/packages/python2-pyalsaaudio/).

*   *Clon de Git*: usa [git-clone(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-clone.1) por defecto para recuperar los archivos de compilación desde el AUR.
*   *Vista de diferencia*: capacitado de provocar una sucesión directa, en particular de: capacidad de ver las diferencias de paquetes en la inspección. Además de la PKGBUILD, esto incluye cambios en archivos como `.install` o `.patch`.
*   *Interacción por lotes*: capacidad de provocar una sucesión directa, en particular de:

1.  Inspección de PKGBUILDs;
2.  Resumen de actualizaciones de paquetes;
3.  Resolución de conflictos de paquetes e instalaciones.

	Un asterisco denota funcionalidad habilitada específicamente por el usuario.

*   *Completado de shell*: [tab completion](https://en.wikipedia.org/wiki/Command-line_completion "w:Command-line completion") está disponible para los [shells](/index.php/Shell "Shell") listados.

**Nota:**

*   Las filas de la tabla están ordenadas por valores de columna, donde *Sí* o *N/A* tienen prioridad sobre *Parcial* u *Opcional* y *No*, o alfabéticamente si los valores son iguales.
*   *Opcional* significa que una característica está disponible, pero sólo a través de un argumento de la línea de comandos o una opción de configuración. Por "parcial" se entiende que una característica no se aplica plenamente o que se desvía parcialmente de los criterios dados.

### Activo

| Nombre | Escrito en | Seguro | Compilación limpia | Nativo de pacman | Analizador fiable | Solucionador fiable | Paquetes divididos | Clonado en Git | Vista de diferencias | Interacción por lotes | Completado de shell | Especificación |
| [aurman](https://aur.archlinux.org/packages/aurman/) | Python | Si | Si | Si | Si | [Si](https://github.com/polygamma/aurman/wiki/Description-of-the-aurman-dependency-solving) | Si | Si | Si | 1, [2*, 3*](https://github.com/polygamma/aurman#question-5) | bash, fish | obtiene claves pgp, ordena por popularidad |
| [aurutils](https://aur.archlinux.org/packages/aurutils/) | Bash/C | Si | Si | N/A | Si | Si | Si | Si | Si | 1 | zsh | [vifm](/index.php/Vifm "Vifm"), [Repositorio local personalizado](https://wiki.archlinux.org/index.php/Pacman/Tips_and_tricks_(Espa%C3%B1ol)#Repositorio_local_personalizado), [Package signing](https://wiki.archlinux.org/index.php/Pacman/Package_signing_(Espa%C3%B1ol)), soporta [clean chroot](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot "DeveloperWiki:Building in a Clean Chroot") , ordena por votos / popularidad |
| [pakku](https://aur.archlinux.org/packages/pakku/) | Nim | Si | [Si](https://github.com/kitsunyan/pakku/commit/864cc0373fd6095295f68cc44d1657bd17269732) | [Parcial](https://github.com/kitsunyan/pakku/wiki/Native-Pacman-Explanation) | Si | Si | Si | Si | [Si](https://github.com/kitsunyan/pakku/commit/396e9f44c4f5a79c7b9238835599387f6ff418fe) | 1 | bash, zsh | soporta [ABS](https://wiki.archlinux.org/index.php/Arch_Build_System_(Espa%C3%B1ol)) , comentarios AUR, obtiene claves PGP |
| [yay](https://aur.archlinux.org/packages/yay/) | Go | Si | Si | [Parcial](https://github.com/Jguer/yay/issues/464) | Si | Si | Si | [Si](https://github.com/Jguer/yay/pull/297) | [Si](https://github.com/Jguer/yay/pull/447) | 1, 2, 3 | bash, fish, zsh | ordena por votos, recupera claves GP,[prompt architecture](https://github.com/Jguer/yay/commit/4bcd3a6297052714e91e3f886602ce5c12d15786) |
| [bauerbill](https://aur.archlinux.org/packages/bauerbill/) | Python | Si | Si | Si | Si | Si | Si | Si | No | 1 | bash, zsh | Administrador de confianza, soporta [ABS](https://wiki.archlinux.org/index.php/Arch_Build_System_(Espa%C3%B1ol)) , extensión de Powerpill |
| [PKGBUILDer](https://aur.archlinux.org/packages/PKGBUILDer/) | Python | Opcional | Si | [Si](https://github.com/Kwpolska/pkgbuilder/blob/master/docs/wrapper.rst) | Si | Si | [Parcial](https://github.com/Kwpolska/pkgbuilder/issues/39) | Si | [No](https://github.com/Kwpolska/pkgbuilder/issues/36) | 1* | - | Compilaciones automáticas por defecto, use `-F` para desabilitar; multilenguaje |
| [naaman](https://aur.archlinux.org/packages/naaman/) | Python | Opcional | Si | N/A | Si | [Parcial](https://github.com/enckse/naaman/issues/19) | [Parcial](https://github.com/enckse/naaman/issues/20) | Si | No | 1* | bash | Compilaciones automáticas por defecto, use `--fetch` para desabilitar, use `-d` para habilitar soluciones |
| [aura](https://aur.archlinux.org/packages/aura/) | Haskell | Opcional | Si | [Si](https://github.com/aurapm/aura/blob/master/aura/src/Aura/Pacman.hs) | [Si](https://github.com/aurapm/aura/commit/7848e9830cd880215f1d12a1c0294992428ea778) | No | [No](https://github.com/aurapm/aura/issues/353) | [No](https://github.com/aurapm/aura/pull/346) | [Parcial](https://github.com/aurapm/aura/blob/89bf702bd0539fa757265c4c54ea2192155f85ed/aura/src/Aura/Pkgbuild/Records.hs) | 1* | bash, zsh | Compilaciones automáticas por defecto, use `--dryrun` para desabilitar, soporta [downgrade](/index.php/Downgrade "Downgrade") , multilenguaje |
| [repofish](https://aur.archlinux.org/packages/repofish/) | Bash | Opcional | Si | N/A | No | No | No | Si | Si | 1* | - | Compilaciones automáticas por defecto, use `check` o `update` para desabilitar, soporta [Repositorio local personalizado](https://wiki.archlinux.org/index.php/Pacman/Tips_and_tricks_(Espa%C3%B1ol)#Repositorio_local_personalizado) |
| [wrapaur](https://aur.archlinux.org/packages/wrapaur/) | Bash | Si | Si | Si | No | No | No | Si | No | - | - | Actualiza mirrors, publica noticias y comentarios AUR |
| [aurget](https://aur.archlinux.org/packages/aurget/) | Bash | Opcional | Si | N/A | No | No | [No](https://github.com/pbrisbin/aurget/issues/40) | No | [No](https://github.com/pbrisbin/aurget/issues/41) | - | bash, zsh | ordenar por votos |

### Sólo búsqueda

| Nombre | Escrito en | Seguro | Analizador fiable | Solucionador fiable | Clonado en Git | Completado de shell | Especificación |
| [pbget](https://aur.archlinux.org/packages/pbget/) | Python | Si | Si | N/A | Si | - | - |
| [yaah](https://aur.archlinux.org/packages/yaah/) | Bash | Si | Si | N/A | Opcional | bash | - |
| [auracle-git](https://aur.archlinux.org/packages/auracle-git/) | C++ | Si | Si | Si | No | - | muestra ordenes de compilación |
| [cower](https://aur.archlinux.org/packages/cower/) | C | Si | Si | N/A | No | bash/zsh | soporta regex , ordenada por votos / popularidad |
| [package-query](https://aur.archlinux.org/packages/package-query/) | C | Si | No [[3]](https://github.com/archlinuxfr/package-query/issues/135) | N/A | N/A | - | - |
| [repoctl](https://aur.archlinux.org/packages/repoctl/) | Go | Si | Si [[4]](https://github.com/goulash/pacman/blob/master/aur/aur.go) | N/A | No | zsh | soporta repositorio local |

### Descontinuado o problemático

## Librerías

## Mantenimiento

## Subida