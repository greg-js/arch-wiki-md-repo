**Estado de la traducción**
Este artículo es una traducción de [Getting and installing Arch](/index.php/Getting_and_installing_Arch "Getting and installing Arch"), revisada por última vez el **2018-09-27**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Getting_and_installing_Arch&diff=0&oldid=544121) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

La imagen de instalación y su firma [GnuPG](/index.php/GnuPG_(Espa%C3%B1ol) "GnuPG (Español)") pueden ser descargadas desde la pagina de [Descargas](https://archlinux.org/download/).

## Verificar firma

Es recomendado verificar la imagen de instalación antes de usarla, especialmente al descargala de un mirror *HTTP*, donde es mas posible que la imagen sea interceptada para [servir imagenes maliciosas](http://www.cs.arizona.edu/stork/packagemanagersecurity/attacks-on-package-managers.html#explanation).

En un sistema con [GnuPG](/index.php/GnuPG_(Espa%C3%B1ol) "GnuPG (Español)") instalado, descargue la firma *PGP signature* (en la sección *Checksums*) en el mismo directorio donde descargo la ISO, y [verifique](/index.php/GnuPG_(Espa%C3%B1ol)#Verificaci.C3.B3n_de_firmas "GnuPG (Español)") la firma ejecutando `gpg --keyserver pgp.mit.edu --keyserver-options auto-key-retrieve --verify archlinux-<version>-x86_64.iso.sig`.

En un sistema Arch Linux puede ejecutar `pacman-key -v archlinux-<version>-x86_64.iso.sig` con privilegios de root.

**Nota:**

*   La firma puede en si ser manipulada si se descarga de un mirror y no de [archlinux.org](https://archlinux.org/download/). En este caso asegúrese que la clave pública usada para descifrar la firma esta firmada por una clave conocida. El comando `gpg` mostrara la huella digital de la clave pública.
*   Otro método para verificar la autenticidad de la firma es cerciorándose que la huella digital de la clave pública es idéntica a la huella digital del [desarrollador de Arch Linux](https://www.archlinux.org/people/developers/) que firmo la ISO. Vea [Wikipedia#Criptografía asimétrica](https://es.wikipedia.org/wiki/Criptograf%C3%ADa_asim%C3%A9trica) para mayor información sobre el proceso de clave pública para autenticar claves.

## Métodos de instalación

La tabla a continuación ofrece un resumen de los métodos mas comunes para iniciar su sistema. Ya que el proceso de instalación obtiene paquetes desde un repositorio remoto, estos métodos requieren una conexión a Internet. Vea [Instalación de paquetes offline](/index.php/Offline_installation_of_packages_(Espa%C3%B1ol) "Offline installation of packages (Español)") y [Archiso#Installation without Internet access](/index.php/Archiso#Installation_without_Internet_access "Archiso") cuando una conexión no esta disponible.

**Nota:**

*   Para poder encender su sistema con el dispositivo que contiene Arch Linux se debe presionar una tecla (v.g. F11, F2, etc.) en la fase [POST](https://es.wikipedia.org/wiki/POST) en el proceso de encendido. Consulte el manual de su tarjeta madre para mas detalles.
*   Cuando el menú de Arch Linux aparece, seleccione *Boot Arch Linux*y presione `Intro` para entrar al ambiente de instalación.
*   Vea [README.bootparams](https://projects.archlinux.org/archiso.git/tree/docs/README.bootparams) para una lista de [parámetros de encendido](/index.php/Kernel_parameters_(Espa%C3%B1ol)#Configuraci.C3.B3n "Kernel parameters (Español)"), y [packages.both](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.both) para una lista de paquetes incluidos.

| Método | Artículos | Condiciones |
| Queme la ISO en USB o un CD, después encienda desde este. | 

*   [Instalación en USB](/index.php/USB_flash_installation_media_(Espa%C3%B1ol) "USB flash installation media (Español)")
*   [Grabación de Disco Óptico CD](/index.php/Optical_disc_drive_(Espa%C3%B1ol)#Grabaci.C3.B3n "Optical disc drive (Español)")

 | 

*   Instalación en uno o algunos computadores
*   Se obtiene un medio que se puede encender directamente

 |
| Monte la image en un servidor y haga que los clientes arranquen de esta en red. | 

*   [PXE](/index.php/PXE_(Espa%C3%B1ol) "PXE (Español)")
*   [Diskless system](/index.php/Diskless_system "Diskless system")

 | 

*   Modelo Servidor-Cliente
*   Red cableada de (1Gbit+) es recomendado

 |
| Monte la imagen en un sistema de Linux e instale Arch desde un ambiente chroot. | 

*   [Instalar desde un Linux existente](/index.php/Install_from_existing_Linux_(Espa%C3%B1ol) "Install from existing Linux (Español)")
*   [Instalar desde SSH](/index.php/Install_from_SSH_(Espa%C3%B1ol) "Install from SSH (Español)")

 | 

*   Reemplace un sistema existente con tiempo de baja minimo.
*   Instale en una maquina local, o en una remota con [VNC](/index.php/TigerVNC_(Espa%C3%B1ol) "TigerVNC (Español)") o [SSH](/index.php/Secure_Shell_(Espa%C3%B1ol) "Secure Shell (Español)")

 |
| Instale Arch Linux en una maquina virtual como huésped. | 

*   [Category:Hypervisors_(Español)](/index.php/Category:Hypervisors_(Espa%C3%B1ol) "Category:Hypervisors (Español)")
*   [Moving an existing install into (or out of) a virtual machine](/index.php/Moving_an_existing_install_into_(or_out_of)_a_virtual_machine "Moving an existing install into (or out of) a virtual machine")

 | 

*   Sistema operativo compatible con virtualización
*   Se obtiene un sistema aislado para aprender, examinar o depurar

 |
| Instalar Arch contiguamente con Windows. | 

*   [Dual boot with Windows (Español)](/index.php/Dual_boot_with_Windows_(Espa%C3%B1ol) "Dual boot with Windows (Español)")

 | 

*   Maquina compartida con usuarios de Windows
*   Fácilmente se restaura la configuración de fabrica en un sistema pre instalado con Windows

 |

## Véase también

*   [README.transfer](https://projects.archlinux.org/archiso.git/tree/docs/README.transfer)
*   [README.altbootmethods](https://projects.archlinux.org/archiso.git/tree/docs/README.altbootmethods)