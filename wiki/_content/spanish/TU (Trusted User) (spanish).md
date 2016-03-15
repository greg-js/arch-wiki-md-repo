## Contents

*   [1 The Trusted User (Usuario Confiable)](#The_Trusted_User_.28Usuario_Confiable.29)
    *   [1.1 Deberes](#Deberes)
        *   [1.1.1 Los TU y UNSUPPORTED](#Los_TU_y_UNSUPPORTED)
            *   [1.1.1.1 Reglamento para "Flag Safe"](#Reglamento_para_.22Flag_Safe.22)
        *   [1.1.2 Los UC y [community], Reglamento para el Mantenimiento de Paquetes](#Los_UC_y_.5Bcommunity.5D.2C_Reglamento_para_el_Mantenimiento_de_Paquetes)
            *   [1.1.2.1 Accediendo al Repositorio](#Accediendo_al_Repositorio)
            *   [1.1.2.2 Subiendo paquetes de la arquitectura x86_64 a community](#Subiendo_paquetes_de_la_arquitectura_x86_64_a_community)
            *   [1.1.2.3 Adoptando Paquetes](#Adoptando_Paquetes)
            *   [1.1.2.4 Renunciar Paquetes](#Renunciar_Paquetes)
            *   [1.1.2.5 Borrando paquetes de [community]](#Borrando_paquetes_de_.5Bcommunity.5D)
        *   [1.1.3 AURtools](#AURtools)

# The Trusted User (Usuario Confiable)

El **Trusted User (TU = Iniciales de Usuario Confiable en inglés)** es un miembro de la comunidad encargado de mantener AUR en orden y funcionamiento. El/Ella mantiene paquetes populares, votos en materias de administración. Un TU es electo desde la comunidad por los Usuarios Confiables actuales mediante un proceso democrático. Los TUs son los miembros que tienen la última palabra en AUR.

Los mismos son gobernados usando [estas reglas](https://archlinux.org/~simo/TUbylaws.html)

## Deberes

### Los TU y UNSUPPORTED

Los TUs deberían esforzarse para chequear los envíos de paquetes en UNSUPPORTED para evitar código maligno y tener excelentes estandares para los PKGBUILDs. Acerca 80% los PKGBUILDs en UNSUPPORTED son sencillos y pueden ser chequeados para ver si tienen código maligno.

Los TUs también deben chequear los PKGBUILDs para pequeños errores, sugerir correcciones y mejoras. Ellos deberían asegurarse de confirmar que todos los paquetes siguen los reglamentos de empaquetado junto con otros mantenedores de paquetes para asegurarse de que se popularice la estandarización de empaquetado en la distro.

#### Reglamento para "Flag Safe"

Existe un nueva funcionalidad en AUR que permite a los TUs marcar paquetes como chequeados. Sin embargo, los usuarios son también responsables de chequear los PKGBUILDs por ellos mismos.

### Los UC y [community], Reglamento para el Mantenimiento de Paquetes

#### Accediendo al Repositorio

Sigue las siguientes instrucciones para subir/modificar paquetes una vez que te haz convertido en TU:

1.  Instala el paquete "aurtools". Asegúrate de que leas el [Tutorial de AURtools](/index.php?title=Tutorial_de_AURtools&action=edit&redlink=1 "Tutorial de AURtools (page does not exist)")
2.  Necesitas enviar por correo la salida de tu "htpasswd -n" a quien este cargo del repositorio AUR CVS( Paul Mattal = paul@mattal.com ). El cual viene con Apache.

```
htpasswd -n <userid>

```

4.  Ejecuta lo siguiente para chequear AUR CVS:

    ```
     export CVSROOT=":pserver:<userid>@cvs.archlinux.org:/home/cvs-community"
     cvs login
     cvs co community
    ```

5.  Para agregar un nuevo paquete:

```
 cvs add <directory>
 cd <directory>
 cvs add PKGBUILD

```

7.  Hacer un commit:

```
cvs commit

```

9.  Subir un paquete binario:

Por favor tenga en cuenta que la password AUR es para usarse con tupkg (NO la password del CVS)

```
tupkg --user <userid> --password <aur-password> <packagefile.pkg.tar.gz>

```

12.  Después de subir un paquete binario y realizar los archivos (commit), agrégale tags a los archivos con:

```
cvs tag -cFR CURRENT <newpackagebuilddir>

```

Package changes become available on every full and half of hour. Verify everything was uploaded properly, then select the newly added or updated package in the web interface and set yourself as the maintainer.

***Nota:** Pasos 5-7 pueden ser ejecutados con communitypkg en un comando como se menciona mas abajo en el [Tutorial de AURtools](/index.php?title=Tutorial_de_AURtools&action=edit&redlink=1 "Tutorial de AURtools (page does not exist)")*

*
```
  **Nota:** en algunos casos, especialmente para los paquetes de la comunidad, un TU de x86_64 puede cambiar el
  pkgrel por .1 (y no +1). Esto indica que el **el cambio al PKGBUILD es específico a x86_64** y para   i686 los
  mantenedores ** no deben** reconstruir el paquete para i686\. Cuando el TU decide modificar el pkgrel , debería
  ser con el incremento usuarl de +1\. Sin embargo, un anterior pkgrel=2.1 no debería ser un
  pkgrel=3.1 cuando sea modificado por el TU.

```
*

#### Subiendo paquetes de la arquitectura x86_64 a community

*   Pasos del 1 hasta el 5 son los mismos mencionados anteriormente.
*   Cuando se use tupkg agrega "--port 1035" a la lista de parámetros.
*   Marca el paquete como "cvs tag -cFR CURRENT-64"

#### Adoptando Paquetes

Un TU puede adoptar cualquier paquete cuando sea. Pero como el tiempo de los TU'ses limitado, el/ella debería intentar solo adoptar los paquetes populares. El mecanismo de voto en AUR permite a un TU rápidamente saber que paquetes los usuarios desean.

Un mantenedor debería adoptar paquetes por medio de la web. El mantenedor es responsable de los arreglos de bugs y actualizaciones de nuevas versiones. Los paquetes deben ser limpiados antes de la adopción.

#### Renunciar Paquetes

Tu puedes renunciar paquetes seleccionando "Disown Packages" en la web de AUR.

Si un TU no puede o no desea mantener mas un paquete, una noticia debe ser anunciada en lista de correo de AUR para que otro TU puede mantenerlo. Un paquete puede seguir siendo renunciado a pesar que ningun TU desee mantenerlo, pero los TUs no debería intentar adoptar mas paquetes de los que pueden. Si un paquete se ha vuelto obsoleto o no es usando puede ser removido sin problemas.

Si un paquete ha sido removido completamente, puede ser subido de nuevo (hecho desde 0) a UNSUPPORTED, donde un usuario normal puede mantener el paquete en vez de un TU.

#### Borrando paquetes de [community]

Borrar un paquetes de [community] es fácil pero no lineal. Después que ha sido removido de community, puede volver a ser agregado a unsupported (¡asegúrate de mantener una copia!) y colócalo huérfano, para que sea adoptado en unsupported por otro usuario.

Para borrar un paquetes, todo lo que necesitas es quitar la etiqueta CURRENT del PKGBUILD. Hazlo haciendo:

```
 cvs tag -d CURRENT PKGBUILD

```

Si deseas mover el resto del contenido del paquete de CVS para futuras revisiones (porque tu no deseas tener cosas viejas por ahi), puedes hacer lo siguiente **DESDE EL DIRECTORIO DEL PAQUETE** en la versión que has elaborado en cvs:

```
 cd /path/to/<packagedirname>
 cvs tag -dl CURRENT
 cvs rm -fl
 cvs commit

```

¡**SE CUIDADOSO** con los comandos de borrado del CVS! Cambiando la etiqueta current en todo el repositorio, arriesgas remover **TODO** en [community]. Arriba se colocan comando que minimizan la posibilidad pero existe una pequeña posibilidad. Nótese que el comando toma efecto apenas se ejecuta así que se cuidadoso.

También, debido a lo extraño de CVS, eliminar el directorio del paquete es imposible. El mismo se mostrará en una versión chequeada. Esto es CVS y con eso debemos vivir por ahora.

Cualquier TU puede eliminar cualquier paquete de [community] así que ten cuidado con esta herramienta.

### AURtools

Para ayudar a los usuarios confiables con sus deberes, existe algo llamado AURtools basado en la herramienta **tupkg**. Si tu eres un Trusted User, es recomendable usar AURtools. El [Tutorial de AURtools](/index.php?title=Tutorial_de_AURtools&action=edit&redlink=1 "Tutorial de AURtools (page does not exist)") fue escrito para que te acostumbres a usarlo.