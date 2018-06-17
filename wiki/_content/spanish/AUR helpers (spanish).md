**Warning:**

*   Los ayudantes de AUR **no** estan [soportados](https://bbs.archlinux.org/viewtopic.php?pid=828254#p828254) por Arch Linux. Se recomienda familiarizarse con el [proceso manual de construcción](/index.php/Arch_User_Repository_(Espa%C3%B1ol)#Instalar_paquetes "Arch User Repository (Español)") para estar preparado para solucionar posibles problemas por su cuenta.
*   Los ayudantes de AUR pueden replicar a [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8) en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"), como `pacman -Syu`. Este uso puede desviarse de *pacman* de varias maneras; por lo tanto **no** es soportado o recomendado.

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

### Activo

### Sólo búsqueda

### Descontinuado o problemático

## Librerías

## Mantenimiento

## Subida