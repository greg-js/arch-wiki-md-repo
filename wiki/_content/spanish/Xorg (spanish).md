Artículos relacionados

*   [Start X at Login (Español)](/index.php/Start_X_at_Login_(Espa%C3%B1ol) "Start X at Login (Español)")
*   [Execute commands after X start](/index.php/Execute_commands_after_X_start "Execute commands after X start")
*   [Display Manager (Español)](/index.php/Display_Manager_(Espa%C3%B1ol) "Display Manager (Español)")
*   [Window Manager (Español)](/index.php/Window_Manager_(Espa%C3%B1ol) "Window Manager (Español)")
*   [Font configuration](/index.php/Font_configuration "Font configuration")
*   [Cursor Themes](/index.php/Cursor_Themes "Cursor Themes")
*   [Desktop Environment (Español)](/index.php/Desktop_Environment_(Espa%C3%B1ol) "Desktop Environment (Español)")
*   [Wayland](/index.php/Wayland "Wayland")

De [http://www.x.org/wiki/](http://www.x.org/wiki/):

	El proyecto X.Org proporciona una implementación de código abierto del sistema de ventanas X. El trabajo de desarrollo se está haciendo conjuntamente con la comunidad freedesktop.org. La Fundación X.Org es una corporación educativa sin fines de lucro cuyo Consejo sirve a este fin, y cuyos Miembros encaminan este trabajo.

**Xorg** es una aplicación pública, una implementación en código abierto del sistema X window versión 11\. Desde el momento que Xorg se convierte en la opción más popular entre los usuarios de Linux, su omnipresencia ha dado lugar a que sea un requisito cada vez más utilizado por las aplicaciones GUI (**G**raphical **U**ser **I**nterface), con la consiguiente adopción masiva por la mayoría de las distribuciones. Consulte el artículo de Wikipedia sobre [Xorg](https://en.wikipedia.org/wiki/X.Org_ServerX.Org "wikipedia:X.Org ServerX.Org") o visite el [sitio web de Xorg](http://www.x.org/wiki/) para más detalles.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
    *   [1.1 Instalación del controlador](#Instalaci.C3.B3n_del_controlador)
*   [2 Ejecución](#Ejecuci.C3.B3n)
*   [3 Configuración](#Configuraci.C3.B3n)
    *   [3.1 Usar archivos .conf](#Usar_archivos_.conf)
    *   [3.2 Usar xorg.conf](#Usar_xorg.conf)
    *   [3.3 Configuraciones de muestra](#Configuraciones_de_muestra)
*   [4 Los dispositivos de entrada](#Los_dispositivos_de_entrada)
    *   [4.1 Aceleración del ratón](#Aceleraci.C3.B3n_del_rat.C3.B3n)
    *   [4.2 Botones extras del ratón](#Botones_extras_del_rat.C3.B3n)
    *   [4.3 Touchpad Synaptics](#Touchpad_Synaptics)
    *   [4.4 Configuración del teclado](#Configuraci.C3.B3n_del_teclado)
*   [5 Configuraciones del monitor](#Configuraciones_del_monitor)
    *   [5.1 Primeros pasos](#Primeros_pasos)
    *   [5.2 Múltiples monitores](#M.C3.BAltiples_monitores)
        *   [5.2.1 Más de una tarjeta gráfica](#M.C3.A1s_de_una_tarjeta_gr.C3.A1fica)
    *   [5.3 Tamaño de la pantalla y DPI](#Tama.C3.B1o_de_la_pantalla_y_DPI)
        *   [5.3.1 Configuración manual de DPI](#Configuraci.C3.B3n_manual_de_DPI)
    *   [5.4 DPMS](#DPMS)
*   [6 Composite](#Composite)
*   [7 Consejos y trucos](#Consejos_y_trucos)
    *   [7.1 Ajustar el arranque de X (startx)](#Ajustar_el_arranque_de_X_.28startx.29)
    *   [7.2 Sesión anidada de X](#Sesi.C3.B3n_anidada_de_X)
    *   [7.3 Iniciar programas GUI remótamente](#Iniciar_programas_GUI_rem.C3.B3tamente)
    *   [7.4 Activar y desactivar bajo demanda las fuentes de entrada](#Activar_y_desactivar_bajo_demanda_las_fuentes_de_entrada)
*   [8 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [8.1 Problemas más comunes](#Problemas_m.C3.A1s_comunes)
    *   [8.2 Tecla CTRL derecha no funciona con la distribución del teclado oss](#Tecla_CTRL_derecha_no_funciona_con_la_distribuci.C3.B3n_del_teclado_oss)
    *   [8.3 Erro iniciando el cliente X con "su"](#Erro_iniciando_el_cliente_X_con_.22su.22)
    *   [8.4 Programas que requieren "font '(null)'"](#Programas_que_requieren_.22font_.27.28null.29.27.22)
    *   [8.5 Problemas con el modo Frame-buffer](#Problemas_con_el_modo_Frame-buffer)
    *   [8.6 DRI deja de funcionar con tarjetas Matrox](#DRI_deja_de_funcionar_con_tarjetas_Matrox)
    *   [8.7 Recuperación: deshabilitar Xorg antes de la pantalla de inicio de sesión](#Recuperaci.C3.B3n:_deshabilitar_Xorg_antes_de_la_pantalla_de_inicio_de_sesi.C3.B3n)
    *   [8.8 Error de X al iniciar: inicialización del teclado fallido](#Error_de_X_al_iniciar:_inicializaci.C3.B3n_del_teclado_fallido)
    *   [8.9 Pantalla en negro, Sin protocolo especificado..., recursos temporalmente no disponibles para todos o algunos usuarios](#Pantalla_en_negro.2C_Sin_protocolo_especificado....2C_recursos_temporalmente_no_disponibles_para_todos_o_algunos_usuarios)

## Instalación

En primer lugar, tendrá que [instalar](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el servidor X con el paquete [xorg-server](https://www.archlinux.org/packages/?name=xorg-server), disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

Por otro lado, algunos paquetes del grupo [xorg-apps](https://www.archlinux.org/groups/x86_64/xorg-apps/) pueden ser útiles para realizar ciertas tareas de configuración, las cuales se señalan en la sección/página correspondiente.

**Sugerencia:** El entorno X, por defecto, es bastante árido, y normalmente preferirá instalar un [Gestor de Ventanas](/index.php/Window_manager_(Espa%C3%B1ol) "Window manager (Español)") o un [Entorno de Escritorio](/index.php/Desktop_environment_(Espa%C3%B1ol) "Desktop environment (Español)") para complementar X.

### Instalación del controlador

El kernel de Linux incluye controladores de vídeo de código abierto y apoyo a los framebuffers de hardware acelerados. Sin embargo , se requiere apoyo en el espacio de usuario para OpenGL y para la aceleración 2D en X11.

En primer lugar, identifique su tarjeta :

```
$ lspci | grep VGA

```

A continuación, instale el controlador apropiado. Puede buscar en la base de datos de los paquetes para obtener una lista completa de los controladores de vídeo de código abierto :

```
$ pacman -Ss xf86-video

```

El controlador de gráficos por defecto es *vesa* (paquete [xf86-video-vesa](https://www.archlinux.org/packages/?name=xf86-video-vesa)), que maneja un gran número de chipsets, pero no incluye ninguna aceleración 2D o 3D. Si no se encuentra o no se puede cargar un controlador mejor, Xorg recurrirá a *vesa*.

A fin de que pueda funcionar la aceleración de vídeo y, muchas veces, dejar expuestos los modos de la GPU para ajustarlos, se requiere un controlador de vídeo correcto:

| Marca | Tipo | Controlador | Paquete [Multilib](/index.php/Multilib "Multilib")
(Para ejecutar aplicaciones de 32-bit en Arch x86_64) |  Documentación  |
| ** AMD/ATI ** |  Código abierto  | [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) | [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) | [ATI](/index.php/ATI "ATI") |
| Propietario | [catalyst-dkms](https://aur.archlinux.org/packages/catalyst-dkms/) | [lib32-catalyst-utils](https://aur.archlinux.org/packages/lib32-catalyst-utils/) | [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst") |
| **Intel** | Código abierto | [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) | [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) | [Intel graphics](/index.php/Intel_graphics "Intel graphics") |
| **Nvidia** | Código abierto | [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) | [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) | [Nouveau](/index.php/Nouveau "Nouveau") |
| [xf86-video-nv](https://aur.archlinux.org/packages/xf86-video-nv/) | – | (controlador legacy) |
| Propietario | [nvidia](https://www.archlinux.org/packages/?name=nvidia) | [lib32-nvidia-libgl](https://www.archlinux.org/packages/?name=lib32-nvidia-libgl) | [NVIDIA](/index.php/NVIDIA "NVIDIA") |
| [nvidia-304xx](https://www.archlinux.org/packages/?name=nvidia-304xx) | [lib32-nvidia-304xx-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-304xx-utils) |
| [nvidia-173xx](https://aur.archlinux.org/packages/nvidia-173xx/) | [lib32-nvidia-173xx-utils](https://aur.archlinux.org/packages/lib32-nvidia-173xx-utils/) |
| [nvidia-96xx](https://aur.archlinux.org/packages/nvidia-96xx/) | [lib32-nvidia-96xx-utils](https://aur.archlinux.org/packages/lib32-nvidia-96xx-utils/) |
| **VIA** | Código abierto | [xf86-video-openchrome](https://www.archlinux.org/packages/?name=xf86-video-openchrome) | – | [VIA](/index.php/Via "Via") |

Xorg debería funcionar sin problemas y sin necesidad de controladores privativos, los cuales normalmente son necesarios solo para desplegar funciones avanzadas como el renderizado rápido con aceleración 3D para juegos, configuraciones de pantalla doble, y TV-out.

## Ejecución

*Consulte también: [Start X at Login](/index.php/Start_X_at_login_(Espa%C3%B1ol) "Start X at login (Español)")*

**Sugerencia:** La forma más fácil de arrancar X es usando un [gestor de pantalla](/index.php/Display_manager_(Espa%C3%B1ol) "Display manager (Español)") como [GDM](/index.php/GDM "GDM") o [SLiM](/index.php/SLiM "SLiM").

Si desea arrancar X sin un gestor de pantalla, [instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [xorg-xinit](https://www.archlinux.org/packages/?name=xorg-xinit). Opcionalmente, los paquetes [xorg-twm](https://www.archlinux.org/packages/?name=xorg-twm), [xorg-xclock](https://www.archlinux.org/packages/?name=xorg-xclock) y [xterm](https://www.archlinux.org/packages/?name=xterm) permiten un entorno por defecto, como se describe a continuación.

Los comandos `startx` y `xinit` inician el servidor X y los clientes (el script `startx` es simplemente un front-end para hacer más versátil la orden `xinit`). Para determinar el cliente a ejecutar, `startx`/`xinit` se dirigirán primero a analizar el archivo `~/.xinitrc` en el directorio home del usuario. En ausencia del archivo específico del usuario `~/.xinitrc`, el valor predeterminado en el archivo global del sistema `/etc/X11/xinit/xinitrc`, será iniciar, por defecto, un entorno básico con el gestor de ventanas [Twm](/index.php/Twm "Twm") , [Xclock](https://en.wikipedia.org/wiki/Xclock "wikipedia:Xclock") y [Xterm](/index.php/Xterm "Xterm"). Para obtener más información, consulte [xinitrc](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)").

**Nota:**

*   X siempre se debe ejecutar en la misma tty donde se produjo el inicio de sesión, para conservar la sesión logind. Esto es manejado de forma predeterminada por `/etc/X11/xinit/xserverrc`. Véase [General troubleshooting#Session permissions](/index.php/General_troubleshooting#Session_permissions "General troubleshooting") para más detalles.
*   Si se produce un problema, proceda en primer lugar, a comprobar el registro en el archivo `/var/log/Xorg.0.log`. Preste atención a las líneas que comienzan con `(EE)`, que representan los errores, y también con `(WW)`, relativo a advertencias, que podrían indicar otros problemas.
*   Si el archivo `.xinitrc` ubicado en su directorio `$HOME` está vacío, elimínelo o modifíquelo adecuadamente para que X pueda iniciar correctamente. Si no lo hace, X mostrará una pantalla en negro que se volcará como un error en su `Xorg.0.log`. Borrarlo, simplemente hará poner en marcha un entorno X por defecto.

**Advertencia:** Si opta por usar `xinit` en lugar de `startx`, debe responsabilizarse de transmitir `-nolisten tcp` y asegurar así que la sesión no se rompe al iniciar X en otra tty.

## Configuración

**Nota:** Arch proporciona, de forma predeterminada, archivos de configuración en `/etc/X11/xorg.conf.d`, y, en la mayoría de los casos, no es necesaria una configuración anterior.

Xorg utiliza un archivo de configuración llamado `xorg.conf` y archivos que terminan en el sufijo `.conf` para su configuración inicial: la lista completa de las carpetas en las que buscar estos archivos se puede encontrar en [[1]](http://www.x.org/releases/current/doc/man/man5/xorg.conf.5.xhtml) o mediante la ejecución de [xorg.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xorg.conf.5), que viene acompañado de una explicación detallada de todas las opciones disponibles.

### Usar archivos .conf

La carpeta `/etc/X11/xorg.conf.d/` guarda la configuración específica del usuario. Cada usuario es libre de añadir archivos de configuración a `/etc/X11/xorg.conf.d/`, pero tengan en cuenta que dichos archivos deben comenzar con `*XX*-` (donde XX es un número) y tienen que terminar en `.conf` (10 se lee antes que 20, por ejemplo). Estos archivos son analizados por el servidor X al arrancar y son tratados como parte del archivo de configuración `xorg.conf` tradicional. El servidor X, esencialmente, lo que hace es tratar dicha colección de archivos de configuración como un único archivo de gran tamaño con las entradas desde `xorg.conf` al final.

### Usar xorg.conf

Xorg también se puede configurar mediante los archivo `/etc/X11/xorg.conf` o `/etc/xorg.conf`. También puede generar la estructura de `xorg.conf` con:

```
 # Xorg :0 -configure

```

Esto debería crear un archivo `xorg.conf.new` en `/root/` que se puede copiar a `/etc/X11/xorg.conf`. Para obtener más información, consulte [xorg.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xorg.conf.5) .

Como alternativa, los controladores de las tarjetas de vídeo pueden proporcionar una herramienta para configurar automáticamente Xorg: consulte el artículo del controlador de vídeo en cuestión para obtener más información, por ejemplo [NVIDIA](/index.php/NVIDIA_(Espa%C3%B1ol) "NVIDIA (Español)") o [AMD Catalyst](/index.php/AMD_Catalyst_(Espa%C3%B1ol) "AMD Catalyst (Español)").

**Nota:** Las palabras claves del archivo de configuración distinguen entre mayúsculas y minúsculas, y los caracteres “_” son ignorados. La mayoría de las cadenas (incluyendo nombres de opciones) también distinguen entre mayúsculas y minúsculas, y son indiferentes a los espacios en blanco y los caracteres “_” .

### Configuraciones de muestra

**`xorg.conf`**

1.  [Muestra 1](http://pastebin.com/raw.php?i=EuSKahkn)
    *   **Nota:** El archivo de configuración de muestra usa `/etc/X11/xorg.conf.d/10-evdev.conf` para la distribución del teclado. Advierta las entradas comentadas en las secciones `InputDevice`.

**`/etc/X11/xorg.conf.d/10-evdev.conf`**

1.  [Muestra 1](http://pastebin.com/raw.php?i=4mPY35Mw)
    *   **Nota:** Este es el archivo `10-evdev.conf` que acompaña a la muestra 1 del archivo xorg.conf.

**`/etc/X11/xorg.conf.d/10-monitor.conf`**

1.  [VMware](http://pastebin.com/raw.php?i=fJv8EXGb)
2.  [KVM](http://pastebin.com/raw.php?i=NRz7v0Kn)
3.  [NVIDIA](https://gist.github.com/daemox/6325050)
    *   **Nota:** Controlador binario nvidia-ck (v325); GPU Dual, Monitor Dual, Pantalla Dual; Sin Twinview, Sin Xinerama; rotada y colocada verticalmente la pantalla 1 (screen1) antes que la pantalla 0 (screen0).

## Los dispositivos de entrada

[Udev](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)") detectará el hardware y [evdev](https://en.wikipedia.org/wiki/evdev es proporcionado por [systemd](https://www.archlinux.org/packages/?name=systemd), y [xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev) es requerido por [xorg-server](https://www.archlinux.org/packages/?name=xorg-server), de modo que no hay necesidad de instalar explícitamente dichos paquetes. Si evdev no es compatible con su dispositivo, instale el controlador adecuado del grupo [xorg-drivers](https://www.archlinux.org/groups/x86_64/xorg-drivers/).

Debe tener el archivo `10-evdev.conf` en el directorio `/etc/X11/xorg.conf.d`, que gestiona el teclado, el ratón, el panel táctil (touchpad) y la pantalla táctil (touchscreen).

### Aceleración del ratón

Véase la página principal: [Mouse acceleration](/index.php/Mouse_acceleration "Mouse acceleration")

### Botones extras del ratón

Véase la página principal: [All Mouse Buttons Working](/index.php/All_Mouse_Buttons_Working "All Mouse Buttons Working")

### Touchpad Synaptics

Véase la página principal: [Touchpad Synaptics](/index.php/Touchpad_Synaptics_(Espa%C3%B1ol) "Touchpad Synaptics (Español)")

### Configuración del teclado

Véase la página principal: [Keyboard Configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg_(Espa%C3%B1ol) "Keyboard configuration in Xorg (Español)")

## Configuraciones del monitor

### Primeros pasos

**Nota:** La nuevas versiones de Xorg son autoconfigurables, por lo que no necesitan este paso.

En primer lugar, cree un nuevo archivo de configuración, como por ejemplo `/etc/X11/xorg.conf.d/**10-monitor.conf**`.

 `/etc/X11/xorg.conf.d/10-monitor.conf` 
```
Section "Monitor"
    Identifier             "Monitor0"
EndSection

Section "Device"
    Identifier             "Device0"
    Driver                 "vesa" #Elija el controlador que se utilice para este monitor
EndSection

Section "Screen"
    Identifier             "Screen0"  #Contraiga la sección Monitor y Device a la sección Screen
    Device                 "Device0"
    Monitor                "Monitor0"
    DefaultDepth            16 #Cambie la profuncidad (16||24)
    SubSection             "Display"
        Depth               16
        Modes              "1024x768_75.00" #Elija la resolución
    EndSubSection
EndSection

```

### Múltiples monitores

Véase el artículo principal main article [Multihead](/index.php/Multihead "Multihead") para obtener información general

Véanse también las instruccines específicas para su GPU:

*   [NVIDIA (Español)#Varios monitores](/index.php/NVIDIA_(Espa%C3%B1ol)#Varios_monitores "NVIDIA (Español)")
*   [Nouveau (Español)#Dual Head](/index.php/Nouveau_(Espa%C3%B1ol)#Dual_Head "Nouveau (Español)")* [ATI Catalyst (Español)#Doble Pantalla (Dual Head / Dual Screen / Xinerama)](/index.php/ATI_Catalyst_(Espa%C3%B1ol)#Doble_Pantalla_.28Dual_Head_.2F_Dual_Screen_.2F_Xinerama.29 "ATI Catalyst (Español)")
*   [ATI (Español)#Configuración Dual Head](/index.php/ATI_(Espa%C3%B1ol)#Configuraci.C3.B3n_Dual_Head "ATI (Español)")

#### Más de una tarjeta gráfica

Debe definir el controlador adecuado para utilizar y poner el ID bus de sus tarjetas gráficas.

```
Section "Device"
    Identifier             "Screen0"
    Driver                 "nouveau"
    BusID                  "PCI:0:12:0"
EndSection

Section "Device"
    Identifier             "Screen1"
    Driver                 "radeon"
    BusID                  "PCI:1:0:0"
EndSection

```

Para obtener el ID bus:

```
$ lspci | grep VGA
01:00.0 VGA compatible controlador: nVidia Corporation G96 [GeForce 9600M GT] (rev a1)

```

En el ejemplo, la salida 01:00:0 es el ID bus que pasaría al archivo de configuración con el formato 1:0:0

### Tamaño de la pantalla y DPI

El DPI del servidor X se determina de la siguiente manera:

1.  La opción de la línea de comandos -dpi tiene la más alta prioridad.
2.  Si esta opción no se utiliza, el ajuste del tamaño de la pantalla en el archivo de configuración de X se utiliza para deducir el DPI, dada la resolución de la pantalla.
3.  Si no viene proporcionado el tamaño de la pantalla, los valores de dimensión del monitor DDC se utilizan para deducir el DPI, dada la resolución de la pantalla.
4.  Si DDC no especifica un tamaño, el valor DPI 75 se utiliza por defecto.

Con el fin de obtener una correcta configuración de los puntos por pulgada (DPI), el tamaño de la pantalla hay que conocerlo o establecerlo. La configuración correcta del DPI es especialmente necesaria cuando se requiere una resolución fina (como, por ejemplo, renderizado de la tipografía). Anteriormente, los fabricantes trataron de crear un estándar para 96 DPI (para un monitor de 10,3" sería una pantalla en diagonal de 800x600, para un monitor de 13,2" sería 1024x768). Hoy en día, los DPI de la pantalla varían y pueden no ser iguales horizontal y verticalmente. Por ejemplo, un LCD de 19" de pantalla ancha de 1440x900 puede tener una DPI de 89x87\. Para poder establecer el DPI, el servidor Xorg intenta detectar automáticamente el tamaño de pantalla de su monitor físico a través de la tarjeta gráfica con [DDC](https://en.wikipedia.org/wiki/Display_Data_Channel "wikipedia:Display Data Channel"). ~~Cuando el servidor Xorg conoce el tamaño de la pantalla física, será capaz de establecer el correcto DPI dependiendo del tamaño de la resolución.~~

Para ver si el tamaño de la pantalla y DPI han sido detectados/calculados correctamente, escriba:

```
$ xdpyinfo | grep -B2 resolution

```

Compruebe que las dimensiones coincidan con el tamaño de la pantalla. Si el servidor Xorg no es capaz de calcular correctamente el tamaño de la pantalla, por defecto será 75x75 DPI y tendrá que calcularlo usted mismo.

Si tiene especificaciones sobre el tamaño físico de la pantalla, se puede introducir en el archivo de configuración de Xorg para que el DPI correcto venga calculado como sigue:

```
Section "Monitor"
    Identifier       "Monitor0"
    DisplaySize      286 1796   # En milímetros
EndSection

```

Si solo desea introducir la especificación del monitor **sin** crear un archivo xorg.conf completo, cree un nuevo archivo de configuración específico. Por ejemplo (`/etc/X11/xorg.conf.d/**90-monitor.conf**`):

```
Section "Monitor"
    Identifier       "<monitor predeterminado>"
    DisplaySize      286 179    # En milímetros
EndSection

```

Si no tiene las especificaciones de anchura y altura de la pantalla física (la mayoría de las especificaciones de hoy en día solo proporcionan el tamaño de la distancia diagonal), se puede utilizar la resolución nativa del monitor (o la relación de aspecto) y la longitud diagonal para calcular las dimensiones físicas horizontales y verticales. Usando el teorema de Pitágoras, en una pantalla de 13,3" de longitud de la diagonal, con una resolución nativa de 1280x800 (o relación de aspecto 16:10), sería:

```
echo 'scale=5;sqrt(1280^2+800^2)' | bc  # 1509.43698

```

Esto le dará la longitud de la diagonal en píxeles y con este valor se pueden descubrir las longitudes físicas horizontales y verticales (y convertirlas a milímetros):

```
echo 'scale=5;(13.3/1509)*1280*25.4' | bc  # 286.43072
echo 'scale=5;(13.3/1509)*800*25.4'  | bc  # 179.01920

```

**Nota:** Este cálculo funciona para monitores con píxeles cuadrados; sin embargo, todavía hay monitores que no pueden comprimir la relación de aspecto (por ejemplo, la resolución de aspecto 16:10 a 16:09). Si este es el caso, debe medir el tamaño de su pantalla de forma manual.

#### Configuración manual de DPI

El DPI puede ser ajustado manualmente si solo se prevee utilizar una resolución ([calculadora DPI](http://pxcalc.com/)):

```
Section "Monitor"
    Identifier        "Monitor0"
    Option            "DPI"       "96 x 96"
EndSection

```

Si utiliza una tarjeta NVIDIA, puede configurar manualmente el DPI añadiendo las siguientes opciones en el archivo `/ etc/X11/xorg.conf.d/20-nvidia.conf` (dentro de la sección **Device**):

```
Option              "UseEdidDpi" "False"
Option              "DPI"        "96 x 96"

```

Para los controladores compatibles con RandR, se puede establecer a través de:

```
xrandr --dpi 96

```

Consulte [Ejecutar comandos después de iniciar X](/index.php/Execute_commands_after_X_start "Execute commands after X start") para hacerlo permanente.

**Nota:** Si bien se puede establecer cualquier dpi que guste y aplicaciones usando Qt y GTK con la escala correspondiente, se recomienda establecerla en 96, 120 (25% más), 144 (50% más), 168 (75% más), 192 (100% más) etc., para reducir las alteraciones de escala en las GUI que utilizan mapas de bits. La reducción por debajo de 96 ppp no produce el efecto de reducir los elementos gráficos dado que normalmente la DPI más baja de los iconos es de 96.

### DPMS

DPMS (Display Power Management Signaling) es una tecnología que permite un comportamiento de ahorro de energía de los monitores cuando el equipo no está en uso. Esto permitirá que los monitores entren automáticamente en modo de espera después de un período de tiempo predefinido. Consulte: [DPMS](/index.php/DPMS "DPMS")

## Composite

La extensión Composite de X hace que todo un sub-árbol de la jerarquía de ventanas se destine a un búfer fuera de la pantalla. Las aplicaciones pueden tomar el contenido de ese búfer y hacer lo que les es propio. El búfer fuera de la pantalla puede ser automáticamente anexado a la ventana padre o fusinado con programas externos, llamados gestores de composición. Consulte los siguientes artículos para obtener más información:

*   [Compiz](/index.php/Compiz "Compiz") -- El auténtico gestor de ventanas/composite de Novell
*   [Xcompmgr](/index.php/Xcompmgr "Xcompmgr") -- Un sencillo gestor composite capaz de sombras y transparencias básicas.
*   [Compton](/index.php/Compton "Compton") -- Un fork de [xcompmgr](/index.php/Xcompmgr "Xcompmgr") con funciones mejoradas y errores corregidos.
*   [Wikipedia:es:Gestor de composición de ventanas](https://en.wikipedia.org/wiki/es:Gestor_de_composici%C3%B3n_de_ventanas "wikipedia:es:Gestor de composición de ventanas")

## Consejos y trucos

### Ajustar el arranque de X (startx)

Para tener una referencia de las opciones de X, consulte:

```
$ man Xserver

```

Las siguientes opciones tienen que ser añadidos a la variable `"defaultserverargs"` en el archivo `/usr/bin/startx`:

*   Habilitar la carga diferida de glyph por fuentes a 16 bits:

```
-deferglyphs 16

```

### Sesión anidada de X

Para ejecutar una sesión anidada de X en otro entorno de escritorio:

```
$ /usr/bin/Xnest :1 -geometry 1024x768+0+0 -ac -name Windowmaker & wmaker -display :1

```

Esto iniciará una sesión de Window Maker en una ventana con una resolución de 1024 por 768 dentro de su sesión X actual.

Esto requiere tener [instalado](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [xorg-server-xnest](https://www.archlinux.org/packages/?name=xorg-server-xnest).

### Iniciar programas GUI remótamente

Véase la página principal: [SSH#X11 forwarding](/index.php/SSH#X11_forwarding "SSH").

### Activar y desactivar bajo demanda las fuentes de entrada

Con la ayuda de `xinput` podemos activar o desactivar temporalmente las fuentes de entrada. Esto puede ser útil, por ejemplo, en sistemas que tienen más de un ratón, como los ThinkPads, y preferimos usar uno solo para evitar clics no deseados del ratón. Vamos a ver cómo lograr esto.

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [xorg-xinput](https://www.archlinux.org/packages/?name=xorg-xinput) disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

Busque el ID del dispositivo que deseamos desactivar: `xinput` 

Por ejemplo, en un Lenovo ThinkPad T500, la salida se vería así:

 `$ xinput` 
```
⎡ Virtual core pointer                    	id=2	[master pointer  (3)]
⎜   ↳ Virtual core XTEST pointer              	id=4	[slave  pointer  (2)]
⎜   ↳ TPPS/2 IBM TrackPoint                   	id=11	[slave  pointer  (2)]
⎜   ↳ SynPS/2 Synaptics TouchPad              	id=10	[slave  pointer  (2)]
⎣ Virtual core keyboard                   	id=3	[master keyboard (2)]
    ↳ Virtual core XTEST keyboard             	id=5	[slave  keyboard (3)]
    ↳ Power Button                            	id=6	[slave  keyboard (3)]
    ↳ Video Bus                               	id=7	[slave  keyboard (3)]
    ↳ Sleep Button                            	id=8	[slave  keyboard (3)]
    ↳ AT Translated Set 2 keyboard            	id=9	[slave  keyboard (3)]
    ↳ ThinkPad Extra Buttons                  	id=12	[slave  keyboard (3)]

```

Desactivamos el dispositivo con `xinput --disable device_id`, donde *device_id* es el ID del dispositivo que deseamos desactivar. En este ejemplo vamos a desactivar el Synaptics Touchpad, con el ID 10:

 `xinput --disable 10` 

Para volver a activar el dispositivo, simplemente ejecutamos la orden opuesta:

 `xinput --enable 10` 

## Solución de problemas

### Problemas más comunes

Si Xorg no arranca, la pantalla se muestra completamente en negro, el teclado y el ratón no funcionan, etc., lo primero es seguir los siguientes pasos:

*   Compruebe el archivo de registro: `cat /var/log/Xorg.0.log`
*   Instale el driver de entrada (teclado, ratón, joystick, tabletas, etc.):
*   Por último, busque los problemas comunes tratados en los artículos [ATI](/index.php/ATI_(Espa%C3%B1ol) "ATI (Español)"), [Intel](/index.php/Intel_(Espa%C3%B1ol) "Intel (Español)") y [NVIDIA](/index.php/NVIDIA_(Espa%C3%B1ol) "NVIDIA (Español)").

### Tecla CTRL derecha no funciona con la distribución del teclado oss

Edite como root `/usr/share/X11/xkb/symbols/fr`, y cambie la línea:

```
include "level5(rctrl_switch)"

```

por

```
// include "level5(rctrl_switch)"

```

A continuación, reinicie X, reinicie el sistema o ejecute:

```
setxkbmap fr oss

```

### Erro iniciando el cliente X con "su"

Si recibe un mensaje de getting diciendo "Client is not authorized to connect to server" (Cliente no autorizado para conectarse al servidor), pruebe añadiendo la línea:

```
session     optional     pam_xauth.so

```

a `/etc/pam.d/su`. `pam_xauth` configurará entonces correctamente las variables de entorno y `xauth` gestionará las teclas.

### Programas que requieren "font '(null)'"

*   Mensaje de error: "*unable to load font '(null)'.*"

Algunos programas solo funcionan con fuentes bitmap. Están disponibles dos paquetes principales con fuentes de mapa de bits, [xorg-fonts-75dpi](https://www.archlinux.org/packages/?name=xorg-fonts-75dpi) y [xorg-fonts-100dpi](https://www.archlinux.org/packages/?name=xorg-fonts-100dpi). No es necesario instalar ambos, con uno debería ser suficiente. Para saber cuál sería el mejor en su caso, intente lo siguiente:

```
$ xdpyinfo | grep resolution

```

y utilice el número dpi que esté más cerca del obtenido en la salida de la orden anterior (colocando 75 o 100 en lugar de XX)

```
# pacman -S xorg-fonts-XXdpi

```

### Problemas con el modo Frame-buffer

Si el servidor X no se inicia, mostrando los mensajes de registro siguientes:

```
(WW) Falling back to old probe method for fbdev
(II) Loading sub module "fbdevhw"
(II) LoadModule: "fbdevhw"
(II) Loading /usr/lib/xorg/modules/linux//libfbdevhw.so
(II) Module fbdevhw: vendor="X.Org Foundation"
       compiled for 1.6.1, module version=0.0.2
       ABI class: X.Org Video Driver, version 5.0
(II) FBDEV(1): using default device

Fatal server error:
Cannot run in framebuffer mode. Please specify busIDs for all framebuffer devices

```

desinstale fbdev:

```
# pacman -R xf86-video-fbdev

```

### DRI deja de funcionar con tarjetas Matrox

Si utiliza una tarjeta Matrox y DRI deja de funcionar después de actualizar Xorg, pruebe a añadir la línea:

```
Option "OldDmaInit" "On"

```

a la sección Device que hace referencia a la tarjeta de video en `xorg.conf`.

### Recuperación: deshabilitar Xorg antes de la pantalla de inicio de sesión

Si Xorg está configurado para arrancar automáticamente y por alguna razón es necesario evitar que se inicie antes de que se abra el gestor de sesión/ventanas (si el sistema está configurado incorrectamente y Xorg no reconoce el mouse o el teclado de entrada, por ejemplo), puede realizar esta tarea con dos métodos.

*   Cambie el targer por defecto a rescue.target. Véase [systemd#Change default target to boot into](/index.php/Systemd#Change_default_target_to_boot_into "Systemd").
*   Si no solo tiene un sistema defectuoso que hace Xorg inutilizable, sino que también ha creado un menú de GRUB con tiempo de espera a cero, y, por lo tanto, no se puede utilizar GRUB (para entrar en la línea de órdenes del kernel) para prevenir el inicio de Xorg desde el arranque, puede utilizar el Live CD de Arch Linux. Arranque el CD y acceda como root. Es necesario un punto de montaje, como /mnt, y también necesita saber el nombre de la partición que desea montar.

Puede utilizar la orden:

```
# fdisk -l

```

para ver las particiones. Por lo general, encontrará algo que se asemeje a `/dev/sda1`. Luego, para montar esta partición en `/mnt`, utilice:

```
# mount /dev/sda1 /mnt

```

A continuación, se mostrará el sistema de archivos en `/mnt`.Desde aquí se puede eliminar el demonio `gdm` que evitará que Xorg arranque normalmente o le permitirá realizar otros cambios necesarios en la configuración.

### Error de X al iniciar: inicialización del teclado fallido

Si el disco duro está lleno, startx fallará. La salida de `/var/log/Xorg.0.log` será:

```
(EE) Error compiling keymap (server-0)
(EE) XKB: Couldn't compile keymap
(EE) XKB: Failed to load keymap. Loading default keymap instead.
(EE) Error compiling keymap (server-0)
(EE) XKB: Couldn't compile keymap
XKB: Failed to compile keymap
Keyboard initialization failed. This could be a missing or incorrect setup of xkeyboard-config.
Fatal server error:
Failed to activate core devices.
Please consult the The X.Org Foundation support  at [http://wiki.x.org](http://wiki.x.org)
for help.
Please also check the log file at "/var/log/Xorg.0.log" for additional information.
 (II) AIGLX: Suspending AIGLX clients for VT switch

```

Libere un poco de espacio en la partición raíz y X se iniciará.

### Pantalla en negro, Sin protocolo especificado..., recursos temporalmente no disponibles para todos o algunos usuarios

X crea archivos de configuración y archivos temporales en el directorio home del usuario actual. Debemos asegurarnos de que haya espacio libre suficiente en la partición del disco donde reside el directorio home. Por desgracia, el servidor X no proporciona ninguna información acerca de la falta de espacio en el disco, sobre este asunto.