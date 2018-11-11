Artículos relacionados

*   [Repositorio de usuario de Arch](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)")

El **Usuario de confianza (UC)** es un miembro de la comunidad encargado de mantener AUR en funcionamiento. El/ella mantiene paquetes populares, los votos y otras cuestiones administrativas. Un UC es elegido por todos los miembros de la comunidad UC en un proceso democrático. La UC son los únicos que tienen la última palabra en la administración de AUR.

Los UC se rigen por el [Estatuto UC](https://aur.archlinux.org/trusted-user/TUbylaws.html)

## Contents

*   [1 Deberes del UC](#Deberes_del_UC)
    *   [1.1 TODO lista para el nuevo usuario de confianza](#TODO_lista_para_el_nuevo_usuario_de_confianza)
    *   [1.2 El UC y UNSUPPORTED](#El_UC_y_UNSUPPORTED)
    *   [1.3 El UC y [community], Guías para Mantenimiento de Paquetes](#El_UC_y_.5Bcommunity.5D.2C_Gu.C3.ADas_para_Mantenimiento_de_Paquetes)
        *   [1.3.1 Reglas para paquetes que entren al [community] Repo](#Reglas_para_paquetes_que_entren_al_.5Bcommunity.5D_Repo)
        *   [1.3.2 Accediendo y Actualizando el Repositorio](#Accediendo_y_Actualizando_el_Repositorio)
        *   [1.3.3 Dejar de mantener paquetes](#Dejar_de_mantener_paquetes)
        *   [1.3.4 Borrando paquetes de unsupported](#Borrando_paquetes_de_unsupported)
        *   [1.3.5 Moviendo paquetes de [community] a unsupported](#Moviendo_paquetes_de_.5Bcommunity.5D_a_unsupported)

## Deberes del UC

### TODO lista para el nuevo usuario de confianza

*   Instalar el paquete [devtools](https://www.archlinux.org/packages/?name=devtools).
*   Envíar su clave pública ssh public a Lukas Fleischer. Si no tienes una, usa [ssh-keygen(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ssh-keygen.1) para generarla. Puedes revisar la página del wiki [SSH keys (Español)](/index.php/SSH_keys_(Espa%C3%B1ol) "SSH keys (Español)") para mas información sobre como crear claves ssh y configurar un cliente-ssh para usar esta.
*   Crear el directorio *staging/community* dentro de tu carpeta personal en aur.archlinux.org. Este es un paso **importante**, porque devtools scripts usa este directorio para procesar los paquetes entrantes.
*   Recuerde a Allan a cambiar su cuenta en los foros
*   Asegúrese que su sponsor le ha dado estado de UC en AUR
*   Pregunte a algunos UC por el canal #archlinux-tu@freenode key
*   Agregarse a la página [Usuarios de Confianza](/index.php/Trusted_Users "Trusted Users")
*   Lea la [Guía de usuarios de confianza](/index.php/AUR_Trusted_User_Guidelines "AUR Trusted User Guidelines").
*   Si no se actualizan a un grupo de usuarios de confianza en bugtracker en dos días, informe esto como un error a Roman
*   ¡Empiece a contribuir!

### El UC y UNSUPPORTED

Los UCs deberían hacer un esfuerzo para revisar los paquetes agregados en UNSUPPORTED en busca de código malicioso y respeto de los standards en la construcción de los PKGBUILD. Alrededor del 80% de los casos de PKGBUILDs en UNSUPPORTED son muy sencillos y puede revisarse rápidamente la coherencia y el código malicioso por el equipo de UC.

Los UCs deben también revisar en los PKGBUILDs los errores de menor importancia, sugerir correcciones y mejoras. El UC debe confirmar que todos los pkgs siguen las Guías/Standards de Empaquetado de Arch y al hacerlo compartir sus conocimientos con otros empaquetadores en un esfuerzo por elevar el nivel de construcción de paquetes en toda la distribución.

Los UCs se encuentran en una excelente posición para documentar las prácticas recomendadas.

### El UC y [community], Guías para Mantenimiento de Paquetes

#### Reglas para paquetes que entren al [community] Repo

Cualquier paquete a ser añadido al repositorio [community] debe cumplir con las directrices que figuran en [esta](/index.php/Rules_Governing_the_Community_Repo "Rules Governing the Community Repo") página.

#### Accediendo y Actualizando el Repositorio

El repositorio [community] utiliza ahora **devtools** que es el mismo sistema para cargar paquetes a [core] y [extra], excepto que usa otro servidor [https://aur.archlinux.org](https://aur.archlinux.org) en lugar de [https://archlinux.org](https://archlinux.org). Así, la mayoría de las instrucciones en [Packager Guide](/index.php/DeveloperWiki:HOWTO_Be_A_Packager "DeveloperWiki:HOWTO Be A Packager") funcionan sin ningún cambio. Información que es específica para el repositorio [community](como cambiar las URLs) se ha puesto aquí.

Inicialmente debes hacer una **revisión non recursiva** del repositorio [community]:
`svn checkout -N svn+[ssh://aur.archlinux.org/srv/svn-packages](ssh://aur.archlinux.org/srv/svn-packages)`

Esto crea un direrctorio llamado "svn-packages" que no contiene nada. It does, however, know that it is an svn checkout.

Para **revisión**, **actualización** de todos los paquetes o **agregar** un paquete vea [Packager Guide](/index.php/DeveloperWiki:HOWTO_Be_A_Packager "DeveloperWiki:HOWTO Be A Packager").

Para **eliminar** un paquete
`ssh aur.archlinux.org /arch/db-remove community pkgname arch`

Aquí y en el texto siguiente, arch puede ser i686 o x86_64 que son las dos arquitecturas soportadas por Arch Linux.

Cuando hayas terminado con la edición del PKGBUILD, etc, debes hacer un **commit** de los cambios (`svn commit`).
Cuando desees **entregar** un paquete, primero copia el paquete a la carpeta *staging/community* en aur.archlinux.org usando scp y luego **mearca** el paquete yendo a la carpeta *pkgname/trunk*y la emisión de `archrelease community-arch`.

Esto hace una copia svn copy de la entradas de trunk en un directorio llamado *community-i686* o *community-x86_64* señalando que este paquete está en el repositorio community para esa arquitectura.

***Nota:** En algunos casos, especialmente para los paquetes en community, un UC x86_64 podría sumar al pkgrel un .1 (y no +1). esto indica que el **cambio al PKGBUILD es específico para x86_64** y los mantenedores de i686 **no deben** reconstruir el paquete para i686\. Cuando el UC decide marcar el pkgrel , se debe hacer con el incremento habitual de +1\. Sin embargo, un pkgrel=2.1 anterior no debe convertirse en pkgrel=3,1 cuando son golpeadas por la TU y en su lugar debe ser pkgrel=3\. En pocas palabras, dejar de punto (.) Comunicados exclusiva a la x86_64 de TU para evitar confusiones.*

Así, el **proceso** de actualización de un paquete puede resumirse como

*   **Actualizar** el directorio del paquete (`SVN actualizar algunos paquetes`)
*   **Cambie** al directorio del paquete raiz (`cd algunos paquetes/raiz`)
*   **Modificar** el PKGBUILD, hacer los cambios necesarios y `makepkg`. Se recomienda construir en un entorno chroot limpio. [chroot](/index.php/DeveloperWiki:Building_in_a_clean_chroot "DeveloperWiki:Building in a clean chroot").
*   **[Namcap](/index.php/Namcap "Namcap")** el PKGBUILD y el pkg.tar.gz binario.
*   **Confirmar** los cambios en el tronco (`confirmar svn`)
*   **Copiar** el paquete a aur.archlinux.org (`scp pkgname-ver-rel-arch.pkg.tar.gz aur.archlinux.org:staging/community/`)
*   **Etiqueta** del paquete (`archrelease community-{i686,x86_64}`)
*   **Actualizar** el repositorio (`ssh aur.archlinux.org /arch/db-community{,64}`)

Ver también la secciòn *Varios* en la [Guía de paquetes](/index.php/DeveloperWiki:HOWTO_Be_A_Packager "DeveloperWiki:HOWTO Be A Packager"). Para la sección *Evite tener que introducir su contraseña todo el tiempo* use aur.archlinux.org en lugar de archlinux.org y svn.archlinux.org.

#### Dejar de mantener paquetes

Si un UC no quiere o no puede mantener más un paquete, debe enviar una notificación a la lista de correo de AUR, para que otro UC pueda mantenerlo. Un paquete pede ser dejado incluso si no hay otro UC que quiera mantenerlo, pero los UCs no deben dejar muchos paquetes a al mismo tiempo(esto no debería tomar mas del tiempo que tarda en encontrar otro mantenedor). Si un paqete se vuelve obsoleto o no es usado mas, puede ser removido completamente también.

Si un paquete ha sido completamente eliminado, puede que sea nuevamente subido (fresco) a UNSUPPORTED, donde un usuario normal puede mantenerlo en vez de un UC.

#### Borrando paquetes de unsupported

No hay ningún punto en la eliminación de paquetes dummy, porque se puede volver a re-crear en un intento de rastrear las dependencias. si alguien carga el paquete real, entonces todos dependen de que indique el lugar correcto.

For an example of a dummy package see: [https://aur.archlinux.org/packages.php?ID=23600](https://aur.archlinux.org/packages.php?ID=23600)

#### Moviendo paquetes de [community] a unsupported

Retire el paquete usando las instrucciones de arriba y suba su archivo tarball a AUR.