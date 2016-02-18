## Contents

*   [1 Introducción](#Introducci.C3.B3n)
*   [2 Cuando Archivos .pac* Son Creados](#Cuando_Archivos_.pac.2A_Son_Creados)
    *   [2.1 .pacnew](#.pacnew)
    *   [2.2 .pacsave](#.pacsave)
    *   [2.3 .pacorig](#.pacorig)
*   [3 Manejando Archivos .pac*](#Manejando_Archivos_.pac.2A)
*   [4 Vínculos Externos](#V.C3.ADnculos_Externos)

## Introducción

Durante la actualización o remoción de paquetes, `pacman` a veces advierte que ciertos archivos — usualmente configuraciones en `/etc` — están siendo instalados con una extensión `.pacnew` o resguradados con una extensión `.pacsave`.

Un archivo `**.pacnew**` es creado durante la actualización de un paquete (`pacman -U` o `pacman -Su`) para evitar sobreescribir un archivo que ya existe y que fue previamente modificado por el usuario. Cuando esto pasa, un mensaje como el siguiente aparecerá en la salida de `pacman`:

```
advertencia: /etc/pam.d/usermod instalado como /etc/pam.d/usermod.pacnew

```

Un archivo `**.pacsave**` es creado durante la eliminación de un paquete (`pacman -R`, el cual es también llamado automáticamente por `pacman -U` and `pacman -Su`) cuando la base de datos de `pacman` indica que cierto archivo perteneciente al paquete debe ser renombrado con una extensión `.pacsave` si fue previamente modificado por el usuario. Cuando esto pasa, `pacman` escribe un mensaje como el siguiente:

```
advertencia: /etc/pam.d/usermod guardado como /etc/pam.d/usermod.pacsave

```

Estos archivos requieren intervención manual del usuario y es una buena práctica manejarlos inmediatamente después de cada invocación de `pacman`. Si se deja sin manejar ellos acumularán y recargarán el sistema de archivos, y el software instalado puede volverse mal configurado, causando comportamiento indeseado que puede ser dificil de resolver.

## Cuando Archivos .pac* Son Creados

### .pacnew

Por cada archivo en un paquete que se actualiza, `pacman` compara tres [sumas MD5](http://es.wikipedia.org/wiki/Md5) generadas del contenido del archivo: una suma por la versión instalada por el paquete, una para la versión actual en el sistema de archivos, y una para la versión en el nuevo paquete. Si la versión del archivo actualmente en el sistema de archivos fue modificada de la versión originalmente instalada del paquete, `pacman` no puede saber como mezclar esos cambios con la versión nueva del archivo. Por lo tanto, en vez de sobreescribir el archivo modificado cuando actualiza, `pacman` guarda la nueva versión con una extensión `.pacnew` y deja la versión modificada intacta.

Yendo a más detalles, el resultado de la comparación de tres vías de sumas MD5 resulta en lo siguiente:

	original = *X*, actual = *X*, nuevo = *X* 

	Todos las tres versiones del archivo tienen contenido idéntico, así que sobreescribir no es un problema. Sobreescribir la versión actual con la nueva versión y no notificar al usuario. (Aunque el contenido del archivo es el mismo, sobreescribir actualizará la información del sistema del archivo acerca del archivo instalado, su fecha de modificación y acceso, y también se asegura que cualquier cambio de permisos de archivo sea aplicada.)

	original = *X*, actual = *X*, nuevo = *Y* 

	El contenido de la versión actual es idéntivo al original, pero la nueva versión es diferente. Ya que el usuario no ha modificado la versión actual y la nueva versión puede contener mejoras o corregir errores, sobreescribe la versión actual con la nueva versión y no notifica al usuario. Este es la única auto-mezcla de nuevos cambios que `pacman` puede realizar.

	original = *X*, actual = *Y*, nuevo = *X* 

	El paquete original y el nuevo contienen exactamente la misma versión del archivom pero la versión actual en el sistema de archivos ha sido modificada. Deja la versión actual en su lugar y descarta la nueva versión sin notificar al usuario.

	original = *X*, actual = *Y*, nuevo = *Y* 

	La nueva versión es idéntica a la actual. Sobreescribe la versión actual con la nueva versión y no notifica al usuario. (Aunque el contenido de los archivos es el mismo, esta sobreescritura actualizará la información del sistema de archivo acerca de la fecha de instalación, modificación y acceso del archivo, así como se asegura que cualquier cambio de permisos sea aplicado.)

	original = *X*, actual = *Y*, nuevo = *Z* 

	Todas las versiones son diferentes, así que deja la versión actual en lugar, instala la versión nueva con una extensión `.pacnew` y advierte al suario acerca de la nueva versión. El usuario se espera que manualmente mezcle cualquier cambio necesario de la nueva versión a la actual.

### .pacsave

Un archivo `PKGBUILD` de un paquete especifica que archivos deben ser guardar una copia de seguridad cuando el paquete es actualizado o removido.Por ejemplo, el `PKGBUILD` del `pulseaudio` contiene la siguiente línea:

```
backup=('etc/pulse/client.conf' 'etc/pulse/daemon.conf' 'etc/pulse/default.pa')

```

Si el usuario ha modificado uno de los archivos especificados en `backup` entonces ese archivo será renombrado a la extensión `.pacsave` y permanecerá en el sistema de archivos después de que el resto del paquete sea actualizado o removido.

**Note:** El uso de la opción `-n` con `pacman -R` resultará en una completa eliminación de *todos* los archivos en el paquete especificado, así que ningún archivo `.pacsave` será creado.

### .pacorig

Cuando un archivo (usualmente una configuración ubicada en `/etc`) que es encontrado durante la instalación o actualización de un paquete no pertenece a ningún paquete instalado, pero es listado en `backup` (vea la sección `.pacsave` arriba) por el paquete en la operación actual, será guardado con una extensión `**.pacorig**` y reemplazado con la versión del archivo del paquete. Usualmente eso ocurre cuando un archivo de configuración ha sido movido de un paquete a otro. Si tal archivo no es listado en `backup`, `pacman` abortará con un error de conflicto de archivos.

**Note:** Ya que los archivos `.pacorig` tienden a ser creados para circunstancias especiales no hay una forma universal para manejarlos. Puede ser útil consultar las [Noticias de Arch](https://www.archlinux.org/news/) por instrucciones de manejo si es un caso conocido.

## Manejando Archivos .pac*

Siempre pon atención a la salida de `pacman`. Cuando actualizando o removiendo un gran número de paquetes, mensajes importantes pueden pasar de largo muy rápidamente o más allá del almacenamiento de la terminal; afortunadamente existen otras formas de descubrir si una operación de `pacman` creó algún archivo `.pac*`.

Si el usuario o un trabajo `cron` ha ejecutado `updatedb` para actualizar la base de datos de `locate` ya que `pacman` fue ejecutado recientemente, los archivos pueden ser encontrados con:

```
locate .pac

```

Un método más lento (a menos que el usuario manualmente ejecute `updatedb` antes de `locate`) que siempre devuelve resultados actualizados a la fecha es el comando `find`:

```
find / -name "*.pac*"

```

Buscando el historial de `pacman` con `egrep` puede ser tan rápido como el método `locate` anterior y siempre mostrará resultados actualizados a la fecha; sin embargo el historial no mantiene rastro de que archivos están actualmente en el sistema de archivos o cuales ya fueron removidos:

```
egrep "pac(new|orig|save)" /var/log/pacman.log

```

Una vez que todos los archivos `.pac*` existentes han sido localizados, el usuario puede manejarlos manualmente usando herramientas de mezcla — como `vimdiff` (parte de [`vim`](/index.php/Vim "Vim")), `ediff` (parte de [`emacs`](/index.php/Emacs "Emacs")), `meld` (GTK+ GUI), o `kompare` (Qt GUI) — y borrando los archivos `.pac*` que el usuario esté seguro que no necesita más. Unas pocas utilidades de terceros proveen varios niveles de acceso de automatización de estas tareas están disponibles en el repositorio `[comunitario](/index.php/Community_repository "Community repository")` y en [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") (Arch no provee utilidades oficiales para el manejo de archivos `.pac*`):

*   [Dotpac](/index.php/Dotpac "Dotpac") — Programa básico e interactivo, con una interfaz de texto basado en "ncurses" y una útil guía. Sin características de mezcla o automezcla.
*   `pacdiff` — Programa de cliente mínimo y no documentado. Parte del paquete de [pacman](https://www.archlinux.org/packages/?name=pacman) en el repositorio `comunitario`.
*   [pacdiffviewer](https://aur.archlinux.org/packages.php?ID=5863) — Programa de cliente interactivo lleno de características con capacidad de auto-mezcla. Parte del paquete [`yaourt`](/index.php/Yaourt "Yaourt").

## Vínculos Externos

*   Foros de Arch Linux: [Dealing With .pacnew Files](https://bbs.archlinux.org/viewtopic.php?id=53532)