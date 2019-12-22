**Estado de la traducción**
Este artículo es una traducción de [Pacman/Pacnew and Pacsave](/index.php/Pacman/Pacnew_and_Pacsave "Pacman/Pacnew and Pacsave"), revisada por última vez el **2018-12-21**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Pacman/Pacnew_and_Pacsave&diff=0&oldid=523844) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Cuando *pacman* elimina un paquete que tiene un archivo de configuración, normalmente crea una copia de respaldo de ese archivo de configuración y agrega *.pacsave* al nombre del archivo. Del mismo modo, cuando *pacman* actualiza un paquete que incluye un nuevo archivo de configuración creado por el mantenedor que difiere del archivo que se instala, guarda un archivo *.pacnew* con la nueva configuración. *pacman* avisa de estas operacoines cuando se escriben dichos archivos.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Por qué se crean estos archivos](#Por_qué_se_crean_estos_archivos)
*   [2 Copias de seguridad de archivos de paquetes](#Copias_de_seguridad_de_archivos_de_paquetes)
*   [3 Explicación de los tipos](#Explicación_de_los_tipos)
    *   [3.1 .pacnew](#.pacnew)
    *   [3.2 .pacsave](#.pacsave)
*   [4 Localizar archivos .pac*](#Localizar_archivos_.pac*)
*   [5 Gestionar archivos .pacnew](#Gestionar_archivos_.pacnew)
    *   [5.1 pacdiff](#pacdiff)
    *   [5.2 Utilidades de terceros](#Utilidades_de_terceros)

## Por qué se crean estos archivos

Se puede crear un archivo *.pacnew* durante la actualización de un paquete (con `pacman -Syu`, `pacman -Su` o `pacman -U`) para evitar sobrescribir un archivo que ya existe y fue modificado previamente por el usuario. Cuando esto sucede, aparecerá un mensaje como el siguiente en la salida de *pacman*:

```
advertencia: /etc/pam.d/usermod instalado como /etc/pam.d/usermod.pacnew

```

Se puede crear un archivo *.pacsave* durante la eliminación de un paquete (con `pacman -R`), o mediante una actualización del paquete (el paquete debe eliminarse primero). Cuando la base de datos de pacman tiene registro de que se debe hacer una copia de seguridad de un determinado archivo que pertenece a un paquete, se creará un archivo *.pacsave*. Cuando esto sucede, pacman envía un mensaje como el siguiente:

```
advertencia: /etc/pam.d/usermod guardado como /etc/pam.d/usermod.pacsave

```

Estos archivos requieren la intervención manual del usuario y es una buena práctica manejarlos inmediatamente después de cada actualización o eliminación de un paquete. Si no se manejan, las configuraciones incorrectas pueden dar como resultado un mal funcionamiento del software, o que el mismo no se ejecute al completo.

## Copias de seguridad de archivos de paquetes

El archivo `PKGBUILD` de un paquete especifica qué archivos deben conservarse o respaldarse cuando el paquete se actualiza o se elimina. Por ejemplo, `PKGBUILD` para `pulseaudio` contiene la siguiente línea:

```
backup=('etc/pulse/client.conf' 'etc/pulse/daemon.conf' 'etc/pulse/default.pa')

```

Para evitar que cualquier paquete sobrescriba un archivo determinado, consulte [Pacman (Español)#Evitar la instalación de archivos en el sistema](/index.php/Pacman_(Espa%C3%B1ol)#Evitar_la_instalación_de_archivos_en_el_sistema "Pacman (Español)").

## Explicación de los tipos

### .pacnew

Para cada uno de las [#Copias de seguridad de archivos de paquetes](#Copias_de_seguridad_de_archivos_de_paquetes) que se están actualizando, pacman compara tres [md5sums](https://en.wikipedia.org/wiki/es:md5sum "wikipedia:es:md5sum") generados a partir del contenido del archivo: una suma para la versión instalada originalmente por el paquete, otra para la versión actualmente en el sistema de archivos y otra última para la versión en el nuevo paquete. Si la versión del archivo que se encuentra actualmente en el sistema de archivos se modificó con respecto a la versión instalada originalmente por el paquete, pacman no puede saber cómo combinar esos cambios con la nueva versión del archivo. Por lo tanto, en lugar de sobrescribir el archivo modificado al actualizar, pacman guarda la nueva versión con una extensión *.pacnew* y deja la versión modificada sin tocar.

Para más detalles, la comparación de la suma MD5 a tres bandas dará uno de los siguientes resultados:

	original = *X*, actual = *X*, nuevo = *X* 

	las tres versiones del archivo tienen un contenido idéntico, por lo que la sobrescritura no es un problema. Sobrescribe la versión actual con la nueva versión y no lo notifica al usuario (aunque el contenido del archivo es el mismo, esta sobrescritura actualizará la información del sistema de archivos con respecto a los archivos instalados, modificados y tiempos de accesos, y asegurará que cualquier cambio en los permisos del archivo se aplicarán).

	original = *X*, actual = *X*, nuevo = *Y* 

	el contenido de la versión actual es idéntico al del original, pero la nueva versión es diferente. Dado que el usuario no ha modificado la versión actual y la nueva versión puede contener mejoras o correcciones de errores, sobrescribe la versión actual con la nueva versión y no lo notifica al usuario. Esta es la única fusión automática de cambios nuevos que es capaz de realizar pacman.

	original = *X*, actual = *Y*, nuevo = *X* 

	el paquete original y el nuevo paquete contienen exactamente la misma versión del archivo, pero la versión actualmente en el sistema de archivos ha sido modificada. Deja la versión actual en su lugar y descarta la nueva versión sin notificarla al usuario.

	original = *X*, actual = *Y*, nuevo = *Y* 

	la nueva versión es idéntica a la versión actual. Sobrescribe la versión actual con la nueva versión y no lo notifica al usuario (aunque el contenido del archivo es el mismo, esta sobrescritura actualizará la información del sistema de archivos con respecto a los archivos instalados, modificados y tiempos de accesos, y asegurará que cualquier cambio en los permisos del archivo se aplicarán).

	original = *X*, actual = *Y*, nuevo = *Z* 

	las tres versiones son diferentes, así que deja la versión actual en su lugar, instala la nueva versión con una extensión *.pacnew* y advierte al usuario sobre la nueva versión. Se espera que el usuario combine manualmente los cambios necesarios de la nueva versión con la versión en vigor.

### .pacsave

Si el usuario ha modificado uno de los archivos especificados en `backup`, ese archivo cambiará de nombre con una extensión *.pacsave* y permanecerá en el sistema de archivos después de que se elimine el resto del paquete.

**Nota:** el uso de la opción `-n` con `pacman -R` dará como resultado la eliminación completa de *todos* los archivos del paquete especificado, por lo tanto, no se creará ningún archivo *.pacsave*.

## Localizar archivos .pac*

pacman no trata los archivos *.pacnew* automáticamente: deben mantenerse por el usuario. Algunas herramientas se presentan en la siguiente sección. Para hacer esto manualmente, primero necesitará localizarlos. Al actualizar o eliminar una gran cantidad de paquetes, se pueden perder los archivos *.pac** actualizados. Para descubrir si se ha instalado algún archivo *.pac**, use una de la órdenes siguientes:

*   Para buscar dentro de `/etc` donde se almacenan la mayoría de las configuraciones globales: `$ find /etc -regextye posix-extended -regex ".+\.pac(new|save)" 2> /dev/null` o para buscar en todo el disco, sustituya `/etc` por `/` en la orden anterior
*   Si está instalado, [mlocate (Español)](/index.php/Mlocate_(Espa%C3%B1ol) "Mlocate (Español)") también se puede usar. Primero vuelva a indexar la base de datos: `# updatedb` Luego ejecute: `$ locate --existing --regex "\.pac(new|save)$"` 
*   Utilice el registro de pacman para encontrarlos: `$ grep --extended-regexp "pac(new|save)" /var/log/pacman.log` Tenga en cuenta que el registro no pierde de vista los archivos que se encuentran actualmente en el sistema de archivos ni los que ya se han eliminado; la orden anterior mostrará una lista de todos los archivos *.pac** que hayan existido en su sistema. Para obtener solo los 10 archivos *.pac** más recientes, canalice el resultado con `tail`.

## Gestionar archivos .pacnew

### pacdiff

[pacman-contrib](https://www.archlinux.org/packages/?name=pacman-contrib) proporciona una sencilla herramienta, *pacdiff*, para gestionar archivos pacnew/pacsave. Buscará todos los archivos *.pacnew* y *.pacsave* y solicitará cualquier acción sobre ellos. Utiliza [vimdiff](/index.php/Vim#Merging_files "Vim") de forma predeterminada, pero puede especificar una herramienta diferente con `DIFFPROG=*your_editor* pacdiff`. Vea [List of applications/Utilities#Comparison, diff, merge](/index.php/List_of_applications/Utilities#Comparison,_diff,_merge "List of applications/Utilities") para otras herramientas de comparación comunes.

### Utilidades de terceros

En [AUR (Español)](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)") dispone de algunas utilidades de terceros que proporcionan varios niveles de automatización para estas tareas.

Algunas de dichas herramientas son las siguientes:

*   **dotpac** — Script interactivo básico con una interfaz de texto basada en ncurses y un tutorial útil. No proporciona características de fusión o fusión automática.

	[https://github.com/AladW/dotpac](https://github.com/AladW/dotpac) || [dotpac](https://aur.archlinux.org/packages/dotpac/)

*   **etc-update** — Puerto de Arch de la utilidad *etc-update* de Gentoo, que proporciona un CLI simple para ver, combinar y editar interactivamente los cambios. Los cambios triviales (como los comentarios) pueden ser mezclados automáticamente.

	[https://wiki.gentoo.org/wiki/Handbook:Parts/Portage/Tools#etc-update](https://wiki.gentoo.org/wiki/Handbook:Parts/Portage/Tools#etc-update) || [etc-update](https://aur.archlinux.org/packages/etc-update/)

*   **pacnew-auto** — Fusionar automáticamente `pacnew` utilizando rebase de [git](https://www.archlinux.org/packages/?name=git).

	[https://github.com/joanrieu/pacnew-auto](https://github.com/joanrieu/pacnew-auto) || [pacnew-auto-git](https://aur.archlinux.org/packages/pacnew-auto-git/)

*   **pacnews-git** — Un script simple destinado a encontrar todos los archivos *.pacnew*, para luego editarlos con [vimdiff](/index.php/Vim#Merging_files "Vim").

	[https://github.com/pbrisbin/scripts/blob/master/pacnews](https://github.com/pbrisbin/scripts/blob/master/pacnews) || [pacnews-git](https://aur.archlinux.org/packages/pacnews-git/)