Related articles

*   [Xorg](/index.php/Xorg "Xorg")
*   [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics")
*   [Wayland](/index.php/Wayland "Wayland")

Desde la wiki de [libinput](https://freedesktop.org/wiki/Software/libinput/):

	libinput es una librería para manejar dispositivos de entrada en compositores de Wayland y para proveer un controlador genérico en X.Org. Implementa detección y manejo de dispositivos, procesamiento de eventos en dispositivos de entrada y abstracción, minimizando así la cantidad de código modificado que los compositores necesitan proveer con la funcionalidad que los usuarios esperan.

El controlador de entrada X.Org soporta la mayoría de [Xorg#dispositivos de entrada](/index.php/Xorg_(Espa%C3%B1ol)#Los_dispositivos_de_entrada "Xorg (Español)"). particularmente interesante es la intención del proyecto de proveer soporte avanzado a dispositivos táctiles (multitouch y gestos) como pantallas táctiles. Vea la documentación de [libinput](http://wayland.freedesktop.org/libinput/doc/latest/pages.html) para mas información.

## Instalación

Si desea utilizar *libinput* en [Wayland](/index.php/Wayland_(Espa%C3%B1ol) "Wayland (Español)") no es necesario hacer nada. El paquete [libinput](https://www.archlinux.org/packages/?name=libinput) debe ser instalado automáticamente como una dependencia de cualquier entorno gráfico que soporta Wayland, ningún controlador adicional es necesario.

Si desea usar *libinput* con [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)"), [instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput), el cual es una envoltura de libinput y habilita el uso de dispositivos de entrada en X. Este controlador puede ser usado como un remplazo total para edev y Synaptics. En otras palabras, este controlador puede ser usado para reemplazar paquetes del estilo `xf86-input-`.

Es deseable instalar el paquete [xorg-xinput](https://www.archlinux.org/packages/?name=xorg-xinput) para modificar configuraciones al iniciar el sistema.

## Configuración

Para [Wayland](/index.php/Wayland_(Espa%C3%B1ol) "Wayland (Español)") no hay archivos de configuración, las opciones de configuración dependen del progreso en el soporte de cada entorno de escritorio; vea [libinput#Graphical tools](/index.php/Libinput#Graphical_tools "Libinput").

Para [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)"), por defecto un archivo es instalado en `/usr/share/X11/xorg.conf.d/40-libinput.conf`. No es necesario modificar este archivo para que auto detecte teclados, paneles o pantallas tactiles o cualquier dispositivo soportado.