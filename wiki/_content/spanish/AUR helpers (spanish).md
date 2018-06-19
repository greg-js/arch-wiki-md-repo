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

*   *Seguro* : no [Recarga](/index.php/Help:Reading_(Espa%C3%B1ol) "Help:Reading (Español)") el PKGBUILD de forma predeterminada; o bien, alerta al usuario y le ofrece la oportunidad de inspeccionar el PKGBUILD manualmente antes de que se obtenga. Se sabe que algunos ayudantes crean PKGBUILDs antes de que el usuario pueda inspeccionarlos, **permitiendo que se ejecute código malicioso**. *Opcional* significa que hay un indicador de línea de comandos o una opción de configuración para evitar el abastecimiento automático antes de la visualización.
*   *Compilación limpia* : no exporta nuevas variables que pueden evitar un proceso de compilación con exito.
*   *Pacman nativo*: cuando se utiliza como sustituto de [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8) como por ejemplo `pacman -Syu`, los siguientes son obedecidos *por defecto* :[[2]](https://wiki.archlinux.org/index.php?title=Talk:AUR_helpers&oldid=515160#Add_.22pacman_wrap.22_column)

	-no separar comandos, por ejemplo `pacman -Syu` no se divide en `pacman -Sy` y `pacman -S *packages*`;

	- use *pacman* directamente en lugar de la manipulación manual de la base de datos o el uso de [libalpm(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libalpm.3).

	Además,potencialmente [Evite ciertos comandos de pacman](/index.php/System_maintenance_(Espa%C3%B1ol)#Evite_ciertos_comandos_de_pacman "System maintenance (Español)") como `pacman -Ud`, `pacman -Rdd`, `pacman --ask` o `pacman --force` **no** se utilizan.

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

*   *Finalización de shell*: [tab completion](https://en.wikipedia.org/wiki/Command-line_completion "w:Command-line completion") está disponible para los [shells](/index.php/Shell "Shell") listados.

**Nota:**

*   Las filas de la tabla están ordenadas por valores de columna, donde *Sí* o *N/A* tienen prioridad sobre *Parcial* u *Opcional* y *No*, o alfabéticamente si los valores son iguales.
*   *Opcional* significa que una característica está disponible, pero sólo a través de un argumento de la línea de comandos o una opción de configuración. Por "parcial" se entiende que una característica no se aplica plenamente o que se desvía parcialmente de los criterios dados.

### Activo

### Sólo búsqueda

### Descontinuado o problemático

## Librerías

## Mantenimiento

## Subida