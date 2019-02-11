Artículos relacionados

*   [Xorg (Español)](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)")
*   [Touchpad Synaptics (Español)](/index.php/Touchpad_Synaptics_(Espa%C3%B1ol) "Touchpad Synaptics (Español)")
*   [Wayland (Español)](/index.php/Wayland_(Espa%C3%B1ol) "Wayland (Español)")

Desde la wiki de [libinput](https://freedesktop.org/wiki/Software/libinput/):

	libinput es una librería para manejar dispositivos de entrada en compositores de Wayland y para proveer un controlador genérico en X.Org. Implementa detección y manejo de dispositivos, procesamiento de eventos en dispositivos de entrada y abstracción, minimizando así la cantidad de código modificado que los compositores necesitan proveer con la funcionalidad que los usuarios esperan.

El controlador de entrada X.Org soporta la mayoría de [Xorg#dispositivos de entrada](/index.php/Xorg_(Espa%C3%B1ol)#Los_dispositivos_de_entrada "Xorg (Español)"). particularmente interesante es la intención del proyecto de proveer soporte avanzado a dispositivos táctiles (multitouch y gestos) como pantallas táctiles. Vea la documentación de [libinput](http://wayland.freedesktop.org/libinput/doc/latest/pages.html) para mas información.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
    *   [2.1 Via xinput](#Via_xinput)
    *   [2.2 Herramientas gráficas](#Herramientas_gráficas)
*   [3 Consejos y trucos](#Consejos_y_trucos)
    *   [3.1 Re-configurar botones](#Re-configurar_botones)
    *   [3.2 Inhabilitar paneles táctiles](#Inhabilitar_paneles_táctiles)

## Instalación

Si desea utilizar *libinput* en [Wayland](/index.php/Wayland_(Espa%C3%B1ol) "Wayland (Español)") no es necesario hacer nada. El paquete [libinput](https://www.archlinux.org/packages/?name=libinput) debe ser instalado automáticamente como una dependencia de cualquier entorno gráfico que soporta Wayland, ningún controlador adicional es necesario.

Si desea usar *libinput* con [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)"), [instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput), el cual es una envoltura de libinput y habilita el uso de dispositivos de entrada en X. Este controlador puede ser usado como un remplazo total para edev y Synaptics. En otras palabras, este controlador puede ser usado para reemplazar paquetes del estilo `xf86-input-`.

Es deseable instalar el paquete [xorg-xinput](https://www.archlinux.org/packages/?name=xorg-xinput) para modificar configuraciones al iniciar el sistema.

## Configuración

Para [Wayland](/index.php/Wayland_(Espa%C3%B1ol) "Wayland (Español)") no hay archivos de configuración, las opciones de configuración dependen del progreso en el soporte de cada entorno de escritorio; vea [libinput#Graphical tools](/index.php/Libinput#Graphical_tools "Libinput").

Para [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)"), por defecto un archivo es instalado en `/usr/share/X11/xorg.conf.d/40-libinput.conf`. No es necesario modificar este archivo para que auto detecte teclados, paneles o pantallas táctiles o cualquier dispositivo soportado.

### Via xinput

En primer lugar ejecute:

```
# libinput list-devices

```

Se mostraran los dispositivos en el sistema y sus características que están soportadas por libinput.

Después de [reiniciar](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)") el entorno gráfico, los dispositivos deberían ser controlados por libinput con la configuración por defecto, en caso de que ningún otro controlador este configurado para tener preferencia.

Vea [libinput(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libinput.4) para opciones generales de opciones y valores validos. La herramienta *xinput* es usada para mostrar o cambiar valores de algún dispositivo, por ejemplo el comando:

```
$ xinput list

```

es usado para mostrar todos los dispositivos y sus respectivos números. En los siguientes comandos `*dispositivo*` describe ya sea el nombre o numero identificador del dispositivo a investigar/modificar.

```
$ xinput list-props *dispositivo*

```

para mostrar las propiedades de un dispositivo, y:

```
$ xinput set-prop *dispositivo* *numero-de-opción* *propiedad*

```

para cambiar una propiedad. Por ejemplo, para cambiar la propiedad de libinput *Método de hacer clic habilitado (303)*, el siguiente comando es ejecutado

```
$ xinput set-prop 14 303 {1 1}

```

### Herramientas gráficas

Existen diferentes herramientas con GUI:

*   [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)"):
    *   Centro de control tiene una interfaz de usuario básica.
    *   El paquete [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks) ofrece algunas configuraciones adicionales.
*   [Cinnamon](/index.php/Cinnamon "Cinnamon"):
    *   Similar a la interfaz de GNOME, con mas opciones.
*   [KDE Plasma](/index.php/KDE_(Espa%C3%B1ol) "KDE (Español)"):
    *   Configurar teclado, ratón y paneles táctiles. Algunas opciones non están implementadas todavía.
    *   [dispositivos-kcm](https://github.com/amezin/pointing-devices-kcm) con el paquete [kcm-pointing-devices-git](https://aur.archlinux.org/packages/kcm-pointing-devices-git/)(ahora abandonado) es una implementación para todos los dispositivos de entrada soportados por libinput.

## Consejos y trucos

### Re-configurar botones

Un ejemplo fácil de usar es el de cambiar el pegado haciendo clic en el panel táctil con tres dedos a dos dedos. Para cambiar esta propiedad se modifica la opción `TappingButtonMap` en el archivo de configuración de [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)"). Para modificar la opción de tap de 1/2/3 dedos de acuerdo a los botones del ratón izquierdo/derecho/centro, se modifica la opción `TappingButtonMap` de `lrm` (**l**eft/**r**ight/**m**iddle) en ingles a `lmr` (**l**eft/**m**iddle/**r**ight) en ingles .

 `/etc/X11/xorg.conf.d/30-touchpad.conf` 
```
Section "InputClass"
    Identifier "touchpad"
    Driver "libinput"
    MatchIsTouchpad "on"
    Option "Tapping" "on"
    Option "TappingButtonMap" "lmr"
EndSection
```

Recuerde de remover `MatchIsTouchpad "on"` si su dispositivo no es un panel tactil y modificar el identificador `Identifier` respectivamente.

### Inhabilitar paneles táctiles

Para inhabilitar un panel táctil, obtenga el nombre apropiado con el comando `xinput list`, y luego inhabilitelo con el comando `xinput disable *nombre*`.

**Sugerencia:**

*   Es recomendable usar el nombre del dispositivo y no el numero de identificación, ya que bajo ciertas circunstancias este numero puede cambiar.
*   Si el nombre contiene espacios, es necesario ponerlo entre comillas.

Para hacer el cambio permanente vea [inicio automático](/index.php/Autostarting_(Espa%C3%B1ol) "Autostarting (Español)").