[Plymouth](http://www.freedesktop.org/wiki/Software/Plymouth) es un proyecto de Fedora que consiste en proporcionar un proceso de arranque gráfico sin parpadeo. Se basa en la [configuración del modo del kernel](/index.php/Kernel_mode_setting "Kernel mode setting") (kernel mode setting -KMS-) para ajustar la resolución nativa de la pantalla tan pronto como sea posible, proporcionando, a continuación, una pantalla de bienvenida visual amigable que se mantiene hasta el inicio del administrador de sesión.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Preparación](#Preparación)
*   [2 Instalación](#Instalación)
*   [3 Configuración](#Configuración)
    *   [3.1 Incluir plymouth en initcpio](#Incluir_plymouth_en_initcpio)
    *   [3.2 Habilitar transición de plymouth con el Gestor de pantalla](#Habilitar_transición_de_plymouth_con_el_Gestor_de_pantalla)
    *   [3.3 En la línea de órdenes del kernel](#En_la_línea_de_órdenes_del_kernel)
    *   [3.4 Cambiar el tema](#Cambiar_el_tema)
*   [4 Consejos y Trucos](#Consejos_y_Trucos)
    *   [4.1 Mostrar mensajes del kernel](#Mostrar_mensajes_del_kernel)
    *   [4.2 Agregar el logo de Arch en los temas spinner y BGRT](#Agregar_el_logo_de_Arch_en_los_temas_spinner_y_BGRT)
*   [5 Véase también](#Véase_también)

## Preparación

Plymouth utiliza principalmente [KMS](/index.php/KMS "KMS") (Kernel Mode Setting) para mostrar gráficos. Si no puede usar KMS por ejemplo, porque esté usando un controlador propietario, o si no desea utilizar EFI framebuffer, se recomienda utilizar [Uvesafb](/index.php/Uvesafb "Uvesafb") ya que puede funcionar con resoluciones de pantalla ancha.

Si no puede usar KMS, ni framebuffer, *Plymouth* caerá y la pantalla volverá de nuevo a modo de texto.

## Instalación

Plymouth no está actualmente disponible en los [Repositorios Oficiales](/index.php/Repositorios_Oficiales "Repositorios Oficiales"), y tendrá que ser instalado desde [AUR](/index.php/AUR "AUR").

La versión estable se llama [plymouth](https://aur.archlinux.org/packages/plymouth/) y la versión git [plymouth-git](https://aur.archlinux.org/packages/plymouth-git/).

## Configuración

### Incluir plymouth en initcpio

Añada Plymouth a la matriz HOOKS en `/etc/[mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf")`. Se **debe** añadir después de **base** y **udev** para que funcione:

 `/etc/mkinitcpio.conf`  `HOOKS="base udev plymouth [...] "` 
**Advertencia:** Si utiliza [cifrado de disco duro](/index.php/System_Encryption_with_LUKS_for_dm-crypt "System Encryption with LUKS for dm-crypt") el hook **encrypt** se debe reemplazar por el hook **plymouth-encrypt** con el fin de llegar a la contraseña del prompts de la TTY.

Para iniciar KMS tempranamente, añada el módulo [Radeon](/index.php/Radeon "Radeon") (para tarjetas Radeon), [i915](/index.php/Intel "Intel") (para tarjetas Intel) o [nouveau](/index.php/Nouveau "Nouveau") (para las tarjetas de nvidia) a la línea **MODULES** localizada en el archivo `/etc/mkinitcpio.conf`:

 `/etc/mkinitcpio.conf` 
```
MODULES="i915"
**o**
MODULES="radeon"
**o**
MODULES="nouveau"
```

Reconstruimos la imagen del kernel (remítase al artículo [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") para más información).

 `# mkinitcpio -p [nombre de su kernel]` 

### Habilitar transición de plymouth con el [Gestor de pantalla](/index.php/Display_manager "Display manager")

Para obtener una transición más suave al terminar la animación y pasar al gestor de pantallas es necesario reemplazar el servicio de systemd que inicia su gestor de pantalla con el que ofrece plymouth. Ejemplo:

 `# systemctl disable [display_manager].service && systemctl enable [display_manager]-plymouth.service` 

Plymouth ofrece soporte para los siguientes gestores de pantalla:

1.  gdm-plymouth.service [GDM](/index.php/GDM "GDM")
2.  sddm-plymouth.service [SDDM](/index.php/SDDM "SDDM")
3.  lightdm-plymouth.service [LightDM](/index.php/LightDM "LightDM")
4.  lxdm-plymouth.service [LXDM](/index.php/LXDM "LXDM")
5.  slim-plymouth.service [SLiM](/index.php/SLiM "SLiM")

### En la línea de órdenes del kernel

Ahora tiene que configurar `quiet splash` en la línea de órdenes del kernel, como parámetros de su gestor de arranque. Vea [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") para más información.

De modo que quedarían como sigue:

**Para Grub2:**

 `/etc/default/grub` 
```
GRUB_CMDLINE_LINUX_DEFAULT=**"quiet splash"**   
GRUB_CMDLINE_LINUX=**"splash"**
```

Y regeneramos el archivo grub:

```
 # grub-mkconfig -o /boot/grub/grub.cfg

```

### Cambiar el tema

Plymouth viene con una selección de temas:

1.  **Fade-in**: «Tema simple en el que salen y se desvanecen estrellas brillantes»
2.  **Glow**: «Tema corporativo con el progreso de arranque en modo de gráfico circular seguido de un logo brillante emergente»
3.  **Script**: «Plugin de ejemplo de secuencias de órdenes» (A pesar de la descripción parece ser un tema bastante bonito con el logotipo de Arch)
4.  **Solar**: «Tema del espacio en tono azul con la violenta quema de la estrella solar»
5.  **Spinfinity**: «Tema simple que muestra un signo de infinito que gira en el centro de la pantalla»
6.  *(**Text**: «Tema en modo texto con una barra de progreso tricolor»)*
7.  *(**Details**: «Tema en modo texto de fallback»)*

Por defecto, no hay seleccionado ningún tema, debe seleccionarlo editando `/etc/plymouth/plymouthd.conf`.

Por ejemplo:

```
[Daemon]
Theme=spinner
```

Todos los temas instalados se pueden enumerar utilizando la siguiente orden:

```
$ ls /usr/share/plymouth/themes
details  glow    solar       spinner  tribar
fade-in  script  spinfinity  text

```

Los temas pueden ser visto de antemano sin reconstruirlos, pulsando `Ctrl+Alt+F2` para cambiar de consola. Acceda como root y escriba:

```
# plymouthd
# plymouth --show-splash
```

Para salir de la vista previa, pulse `Ctrl+Alt+F2` de nuevo y escriba:

 `# plymouth --quit` 

Cada vez que se cambia un tema, la imagen del kernel debe ser reconstruida con:

 `# mkinitcpio -p <el nombre de su kernel; por ejemplo, linux>` 

Reinicie para aplicar los cambios.

## Consejos y Trucos

### Mostrar mensajes del kernel

Durante el arranque puedes ver los mensajes de arranque presionando la tecla `Home` o también `Esc`.

### Agregar el logo de Arch en los temas spinner y BGRT

Para agregar el logo de Arch en los temas *spinner* y *BGRT* simplemente copie el logo y ṕeguelo en el directorio del tema *spinner* y *BGRT* con el siguiente nombre: `watermark.png`.

```
# cp -r /usr/share/plymouth/arch-logo.png /usr/share/plymouth/themes/spinner/watermark.png

```

## Véase también

[Original Spec](http://fedoraproject.org/wiki/Releases/FeatureBetterStartup)

[A related forum thread](https://bbs.archlinux.org/viewtopic.php?id=81406)