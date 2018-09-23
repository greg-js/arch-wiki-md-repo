**Estado de la traducción:** este artículo es una versión traducida de [General recommendations](/index.php/General_recommendations "General recommendations"). Fecha de la última traducción/revisión: **2018-08-13**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=General_recommendations&diff=0&oldid=532688).

Artículos relacionados

*   [Preguntas frecuentes](/index.php/FAQ_(Espa%C3%B1ol) "FAQ (Español)")
*   [Guía de instalación](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)")
*   [Lista de aplicaciones](/index.php/List_of_applications_(Espa%C3%B1ol) "List of applications (Español)")

Este documento es un índice con anotaciones a otros artículos populares e información importante para mejorar y añadir funcionalidades al sistema Arch instalado. Se supone que los lectores han leído y seguido la [guía de instalación](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)") para instalar un sistema básico de Arch Linux. Es necesario haber leído y comprendido los conceptos explicados en [administración del sistema](#Administraci.C3.B3n_del_sistema) y [administración de paquetes](#Administraci.C3.B3n_de_paquetes) antes de continuar con las otras secciones de esta página y de otros artículos de la wiki.

## Contents

*   [1 Administración del sistema](#Administraci.C3.B3n_del_sistema)
    *   [1.1 Usuarios y grupos](#Usuarios_y_grupos)
    *   [1.2 Escalado de privilegios](#Escalado_de_privilegios)
    *   [1.3 Administración de servicios](#Administraci.C3.B3n_de_servicios)
    *   [1.4 Mantenimiento del sistema](#Mantenimiento_del_sistema)
*   [2 Administración de paquetes](#Administraci.C3.B3n_de_paquetes)
    *   [2.1 pacman](#pacman)
    *   [2.2 Repositorios](#Repositorios)
    *   [2.3 Servidores de réplicas](#Servidores_de_r.C3.A9plicas)
    *   [2.4 Sistema de construcción de Arch](#Sistema_de_construcci.C3.B3n_de_Arch)
    *   [2.5 Repositorio de usuario de Arch](#Repositorio_de_usuario_de_Arch)
*   [3 Arranque](#Arranque)
    *   [3.1 Reconocimiento automático del hardware](#Reconocimiento_autom.C3.A1tico_del_hardware)
    *   [3.2 Microcódigo](#Microc.C3.B3digo)
    *   [3.3 Conservar los mensajes del arranque](#Conservar_los_mensajes_del_arranque)
    *   [3.4 Activar Bloq Num al inicio](#Activar_Bloq_Num_al_inicio)
*   [4 Interfaz gráfica de usuario](#Interfaz_gr.C3.A1fica_de_usuario)
    *   [4.1 Servidor de pantalla](#Servidor_de_pantalla)
    *   [4.2 Controladores de pantalla](#Controladores_de_pantalla)
    *   [4.3 Entornos de escritorio](#Entornos_de_escritorio)
    *   [4.4 Administradores de ventanas](#Administradores_de_ventanas)
    *   [4.5 Administradores de pantalla](#Administradores_de_pantalla)
*   [5 Administración de energía](#Administraci.C3.B3n_de_energ.C3.ADa)
    *   [5.1 Eventos de ACPI](#Eventos_de_ACPI)
    *   [5.2 Regulación de la frecuencia de la CPU](#Regulaci.C3.B3n_de_la_frecuencia_de_la_CPU)
    *   [5.3 Portátiles](#Port.C3.A1tiles)
    *   [5.4 Suspensión e hibernación](#Suspensi.C3.B3n_e_hibernaci.C3.B3n)
*   [6 Multimedia](#Multimedia)
    *   [6.1 Sonido](#Sonido)
    *   [6.2 Complementos para el navegador](#Complementos_para_el_navegador)
    *   [6.3 Códecs](#C.C3.B3decs)
*   [7 Redes](#Redes)
    *   [7.1 Sincronización del reloj](#Sincronizaci.C3.B3n_del_reloj)
    *   [7.2 Seguridad DNS](#Seguridad_DNS)
    *   [7.3 Configurar un cortafuegos](#Configurar_un_cortafuegos)
    *   [7.4 Compartir recursos](#Compartir_recursos)
*   [8 Dispositivos de entrada](#Dispositivos_de_entrada)
    *   [8.1 Distribuciones de teclado](#Distribuciones_de_teclado)
    *   [8.2 Botones del ratón](#Botones_del_rat.C3.B3n)
    *   [8.3 Pantalla táctil del portátil](#Pantalla_t.C3.A1ctil_del_port.C3.A1til)
    *   [8.4 TrackPoints](#TrackPoints)
*   [9 Optimización](#Optimizaci.C3.B3n)
    *   [9.1 Benchmarking](#Benchmarking)
    *   [9.2 Mejorando el rendimiento](#Mejorando_el_rendimiento)
    *   [9.3 Discos de estado sólido](#Discos_de_estado_s.C3.B3lido)
*   [10 Servicios del sistema](#Servicios_del_sistema)
    *   [10.1 Índice de archivos y búsqueda](#.C3.8Dndice_de_archivos_y_b.C3.BAsqueda)
    *   [10.2 Entrega de correo electrónico local](#Entrega_de_correo_electr.C3.B3nico_local)
    *   [10.3 Impresión](#Impresi.C3.B3n)
*   [11 Apariencia](#Apariencia)
    *   [11.1 Tipos de letra](#Tipos_de_letra)
    *   [11.2 Temas para GTK+ y Qt](#Temas_para_GTK.2B_y_Qt)
*   [12 Mejoras para la línea de comandos](#Mejoras_para_la_l.C3.ADnea_de_comandos)
    *   [12.1 Mejoras de autocompletado con Tab](#Mejoras_de_autocompletado_con_Tab)
    *   [12.2 Alias](#Alias)
    *   [12.3 Shells alternativas](#Shells_alternativas)
    *   [12.4 Complementos para bash](#Complementos_para_bash)
    *   [12.5 Salida coloreada](#Salida_coloreada)
    *   [12.6 Archivos comprimidos](#Archivos_comprimidos)
    *   [12.7 Indicador de la línea de comandos](#Indicador_de_la_l.C3.ADnea_de_comandos)
    *   [12.8 Shell emacs](#Shell_emacs)
    *   [12.9 Soporte del ratón](#Soporte_del_rat.C3.B3n)
    *   [12.10 Búfer de desplazamiento hacia atrás](#B.C3.BAfer_de_desplazamiento_hacia_atr.C3.A1s)
    *   [12.11 Administración de las sesiones](#Administraci.C3.B3n_de_las_sesiones)

## Administración del sistema

Esta sección se ocupa de las tareas administrativas y de gestión del sistema. Para más información, consulte [Core utilities (Español)](/index.php/Core_utilities_(Espa%C3%B1ol) "Core utilities (Español)") y [Category:System administration (Español)](/index.php/Category:System_administration_(Espa%C3%B1ol) "Category:System administration (Español)").

### Usuarios y grupos

Una instalación nueva deja solamente la cuenta de [superusuario](https://en.wikipedia.org/wiki/es:Root en un servidor, [es inseguro](https://apple.stackexchange.com/questions/192365/is-it-ok-to-use-the-root-user-as-a-normal-user/192422#192422). En su lugar, debe crear y usar cuentas de usuario sin privilegios para la mayoría de las tareas, solo utilizando la cuenta root para la administración del sistema. Consulte la [administración de usuarios](/index.php/Users_and_groups_(Espa%C3%B1ol)#Administraci.C3.B3n_de_usuarios "Users and groups (Español)") para obtener más detalles.

Los usuarios y grupos son un mecanismo para el *control de acceso*; los administradores pueden ajustar la pertenencia y propiedad de grupo para otorgar o denegar a los usuarios y servicios el acceso a los recursos del sistema. Consulte el artículo [usuarios y grupos](/index.php/Users_and_groups_(Espa%C3%B1ol) "Users and groups (Español)") para más detalles y conocer potenciales riesgos de seguridad.

### Escalado de privilegios

Los comandos [su](/index.php/Su_(Espa%C3%B1ol) "Su (Español)") y [sudo](/index.php/Sudo_(Espa%C3%B1ol) "Sudo (Español)") le permiten ejecutar comandos como otro usuario. Por defecto, *su* lo transfiere a un shell de inicio de sesión como usuario root, y *sudo* le concede temporalmente privilegios de root para un solo comando. Consulte sus respectivos artículos para las diferencias.

### Administración de servicios

Arch Linux usa [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") como proceso [init](/index.php/Init "Init"), que es un administrador de sistemas y servicios para Linux. Para el mantenimiento de su instalación de Arch Linux, es una buena idea aprender los conceptos básicos al respecto. La interacción con *systemd* se realiza a través del comando *systemctl*. Consulte [uso básico de systemctl](/index.php/Systemd_(Espa%C3%B1ol)#Uso_b.C3.A1sico_de_systemctl "Systemd (Español)") para obtener más información.

### Mantenimiento del sistema

Arch es un sistema de lanzamiento continuo y cuenta con una rápida rotación de paquetes, por lo que los usuarios deben dedicar un tiempo a realizar el [mantenimiento del sistema](/index.php/System_maintenance_(Espa%C3%B1ol) "System maintenance (Español)"). Consulte [Security](/index.php/Security "Security") para obtener recomendaciones y buenas prácticas sobre el fortalecimiento *(hardening)* del sistema.

## Administración de paquetes

Esta sección contiene información útil relacionada con la administración de los paquetes. Para más información, consulte [Frequently asked questions (Español)#Administración de paquetes](/index.php/Frequently_asked_questions_(Espa%C3%B1ol)#Administraci.C3.B3n_de_paquetes "Frequently asked questions (Español)") y [Category:Package management (Español)](/index.php/Category:Package_management_(Espa%C3%B1ol) "Category:Package management (Español)").

**Nota:** Es imprescindible mantenerse al día de los cambios en Arch Linux para conocer aquellos que requieren una intervención manual, **antes** de actualizar su sistema. Suscríbase a la [arch-announce mailing list](https://mailman.archlinux.org/mailman/listinfo/arch-announce/) y compruebe la página principal de [Arch news](https://www.archlinux.org/) antes de realizar cualquier actualización. Por otro lado, puede encontrar útil suscribirse a este [RSS feed](https://www.archlinux.org/feeds/news/).

### pacman

[pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") es el *administrador de paquetes* de Arch Linux: todos los usuarios deben familiarizarse con él antes de leer cualquier otro artículo.

Consulte [pacman/Tips and tricks (Español)](/index.php/Pacman/Tips_and_tricks_(Espa%C3%B1ol) "Pacman/Tips and tricks (Español)") para obtener sugerencias sobre cómo mejorar su interacción con pacman y la administración de paquetes en general.

### Repositorios

Consulte los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)") para más detalles sobre el propósito de cada repositorio mantenido oficialmente.

Si planea utilizar aplicaciones de 32 bits, tendrá que activar el repositorio [multilib](/index.php/Official_repositories_(Espa%C3%B1ol)#multilib "Official repositories (Español)").

El artículo sobre los [repositorios no oficiales](/index.php/Unofficial_user_repositories "Unofficial user repositories") enumera otros repositorios no apoyados oficialmente.

Considere instalar el servicio [pkgstats](/index.php/Pkgstats_(Espa%C3%B1ol) "Pkgstats (Español)").

### Servidores de réplicas

Consulte el artículo sobre [réplicas](/index.php/Mirrors_(Espa%C3%B1ol) "Mirrors (Español)") *(mirrors)* para conocer los pasos a seguir para aprovechar al máximo el uso y obtener las réplicas de los repositorios oficiales más actualizados. Como se explica en el artículo, un consejo especialmente bueno consiste en verificar periódicamente la página del [estado de las réplicas](https://www.archlinux.org/mirrors/status/) para consultar la lista de las réplicas que han sido recientemente sincronizadas.

### Sistema de construcción de Arch

Los *ports* son un sistema usado inicialmente por distribuciones BSD que consisten en secuencias de comandos *(scripts)* de compilación que se encuentran en un árbol de directorios en el sistema local. En pocas palabras, cada *port* contiene una secuencia de comandos dentro de un directorio con un nombre intuitivo que hace referencia a la aplicación de terceros instalable.

El [sistema de construcción de Arch](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)") (ABS, *Arch Build System*) ofrece la misma funcionalidad al proporcionar unas secuencias de comandos de compilación llamadas [PKGBUILDs](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)"), que se cargan con información conocida para una determinada pieza de software: control de la integridad, URL del proyecto, versión, licencia e instrucciones de compilación. Estos PKGBUILDs son analizados posteriormente por [makepkg](/index.php/Makepkg_(Espa%C3%B1ol) "Makepkg (Español)"), el programa que actualmente genera paquetes es gestionado limpiamente por pacman.

Cada paquete de los repositorios junto con los presentes en AUR están sujetos a recompilación con makepkg.

### Repositorio de usuario de Arch

Si bien el sistema de construcción de Arch (ABS) permite la posibilidad de construir los programas disponibles en los repositorios oficiales, el [repositorio de usuario de Arch](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)") (AUR, *Arch User Repository*) es el equivalente para los paquetes enviados por los usuarios. Es un repositorio sin soporte oficial de secuencias de comandos de compilación, accesibles a través de la [interfaz web](https://aur.archlinux.org/) o a través de la interfaz [Aurweb RPC](/index.php/Aurweb_RPC_interface "Aurweb RPC interface").

## Arranque

Esta sección contiene información relacionada con el proceso de arranque. Se puede encontrar una descripción general del proceso de arranque de Arch en el artículo [proceso de arranque](/index.php/Arch_boot_process_(Espa%C3%B1ol) "Arch boot process (Español)"). Para obtener más información, consulte la categoría [proceso de arranque](/index.php/Category:Boot_process_(Espa%C3%B1ol) "Category:Boot process (Español)").

### Reconocimiento automático del hardware

El hardware debe ser detectado automáticamente por [udev](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)") durante el proceso de arranque de forma predeterminada. Se puede lograr una mejora potencial en el tiempo de arranque desactivando la carga automática de los módulos y especificando los módulos requeridos manualmente, como se describe en [módulos del kernel](/index.php/Kernel_modules_(Espa%C3%B1ol) "Kernel modules (Español)"). Además, [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)") debería ser capaz de detectar automáticamente los controladores necesarios mediante `udev`, aunque los usuarios también tienen la opción de configurar el servidor X manualmente.

### Microcódigo

Los procesadores pueden tener un [comportamiento defectuoso](http://www.anandtech.com/show/8376/intel-disables-tsx-instructions-erratum-found-in-haswell-haswelleep-broadwelly), que el kernel puede corregir mediante la actualización del *microcódigo* al inicio. Los procesadores de Intel requieren un paquete separado para este fin. Consulte [microcódigo](/index.php/Microcode_(Espa%C3%B1ol) "Microcode (Español)") para más detalles.

### Conservar los mensajes del arranque

Una vez que concluye el arranque, la pantalla se borra y aparece el inicio de sesión, lo que deja a los usuarios sin poder recabar información del proceso de arranque. [Desactive la eliminación de los mensajes de inicio](/index.php/General_troubleshooting_(Espa%C3%B1ol)#Mensajes_de_la_consola "General troubleshooting (Español)") para superar esta limitación.

### Activar Bloq Num al inicio

Bloq Num es una tecla de alternancia que se encuentra en la mayoría de los teclados. Para activar Bloq Num de modo que permanezca activo el teclado numérico durante el arranque, consulte [activando Bloq Num al inicio](/index.php/Activating_Numlock_on_Bootup_(Espa%C3%B1ol) "Activating Numlock on Bootup (Español)").

## Interfaz gráfica de usuario

Esta sección proporciona orientación para los usuarios que deseen ejecutar aplicaciones gráficas en su sistema. Consulte la categoría [interfaces gráficos de usuario](/index.php/Category:Graphical_user_interfaces "Category:Graphical user interfaces") para obtener información adicional.

### Servidor de pantalla

[Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)") es una aplicación pública, una implementación de código abierto del [sistema de ventanas X](https://en.wikipedia.org/wiki/es:X_Window_System "wikipedia:es:X Window System") (comúnmente X11, o X). Es necesario para ejecutar aplicaciones con interfaces gráficas de usuario (GUI), y la mayoría de los usuarios querrán instalarlo.

[Wayland](/index.php/Wayland_(Espa%C3%B1ol) "Wayland (Español)") es un protocolo de servidor de pantalla alternativo más nuevo y la implementación de referencia de Weston está disponible.

### Controladores de pantalla

El controlador de pantalla predeterminado *vesa* funcionará con la mayoría de las tarjetas de vídeo, pero el rendimiento puede mejorarse significativamente y las características adicionales pueden aprovecharse instalando el controlador apropiado para los productos [ATI](/index.php/ATI_(Espa%C3%B1ol) "ATI (Español)"), [Intel](/index.php/Intel_(Espa%C3%B1ol) "Intel (Español)"), o [NVIDIA](/index.php/NVIDIA_(Espa%C3%B1ol) "NVIDIA (Español)").

### Entornos de escritorio

Aunque Xorg proporciona el marco básico para crear un entorno gráfico, se pueden considerar necesarios componentes adicionales para una experiencia de usuario completa. Los [entornos de escritorio](/index.php/Desktop_environment_(Espa%C3%B1ol) "Desktop environment (Español)") como [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)"), [KDE](/index.php/KDE_(Espa%C3%B1ol) "KDE (Español)"), [LXDE](/index.php/LXDE_(Espa%C3%B1ol) "LXDE (Español)") y [Xfce](/index.php/Xfce_(Espa%C3%B1ol) "Xfce (Español)") combinan una amplia gama de *clientes X*, como un administrador de ventanas, un panel, un administrador de archivos, un emulador de terminal, un editor de texto, iconos y otras utilidades. Los usuarios con menos experiencia pueden querer instalar un entorno de escritorio para un entorno más familiar. Consulte la categoría [entornos de escritorio](/index.php/Category:Desktop_environments_(Espa%C3%B1ol) "Category:Desktop environments (Español)") para obtener información adicional.

### Administradores de ventanas

Un entorno de escritorio completo proporciona una interfaz gráfica de usuario completa y consistente, pero tiende a consumir una cantidad considerable de recursos del sistema. Los usuarios que buscan maximizar el rendimiento, o simplificar su entorno, pueden optar por instalar solo un [administrador de ventanas](/index.php/Window_manager_(Espa%C3%B1ol) "Window manager (Español)") y elegir manualmente los extras que quiera. La mayoría de los entornos de escritorio también permiten el uso de un administrador de ventanas alternativo. Los administradores de ventanas [dinámicos](/index.php/Category:Dynamic_WMs_(Espa%C3%B1ol) "Category:Dynamic WMs (Español)"), [apillados](/index.php/Category:Stacking_WMs_(Espa%C3%B1ol) "Category:Stacking WMs (Español)") y de [mosaico](/index.php/Category:Tiling_WMs_(Espa%C3%B1ol) "Category:Tiling WMs (Español)") difieren en la gestión de la ubicación de las ventanas.

### Administradores de pantalla

La mayoría de los entornos de escritorio incluyen un [administrador de pantalla](/index.php/Display_manager_(Espa%C3%B1ol) "Display manager (Español)") para iniciar automáticamente el entorno gráfico y administrar los inicios de sesión de los usuarios. Los usuarios sin un entorno de escritorio pueden instalar uno por separado. También puede [iniciar X al iniciar sesión](/index.php/Start_X_at_login_(Espa%C3%B1ol) "Start X at login (Español)") como una alternativa simple a un administrador de pantalla.

## Administración de energía

Esta sección puede ser de utilidad para los propietarios de portátiles o usuarios que busquen controlar de administración de energía. Para obtener más información, consulte la categoría de [administración de energía](/index.php/Category:Power_management_(Espa%C3%B1ol) "Category:Power management (Español)").

Consulte el artículo de [administración de energía](/index.php/Power_management_(Espa%C3%B1ol) "Power management (Español)") para una descripción más general.

### Eventos de ACPI

Los usuarios pueden configurar cómo reacciona el sistema a los eventos de ACPI, como presionar el botón de encendido o cerrar la tapa del portátil. Para el nuevo método (recomendado) usando [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)"), consulte la [administración de energía con systemd](/index.php/Power_management_(Espa%C3%B1ol)#Administraci.C3.B3n_de_energ.C3.ADa_con_systemd "Power management (Español)"). Para el método anterior, consulte [acpid](/index.php/Acpid_(Espa%C3%B1ol) "Acpid (Español)").

### Regulación de la frecuencia de la CPU

Los procesadores modernos pueden disminuir su frecuencia y voltaje para reducir el calor y el consumo de energía. Menos calor conduce a un sistema más silencioso y prolonga la vida útil del hardware. Consulte la [regulación de la frecuencia de la CPU](/index.php/CPU_frequency_scaling_(Espa%C3%B1ol) "CPU frequency scaling (Español)") para más detalles.

### Portátiles

Para los artículos relacionados con la informática portátil junto con las guías de instalación específicas de cada modelo, consulte la categoría [Portátiles](/index.php/Category:Laptops_(Espa%C3%B1ol) "Category:Laptops (Español)"). Para obtener una descripción general de los artículos y recomendaciones relacionados con portátiles, consulte el artículo [Portátil](/index.php/Laptop_(Espa%C3%B1ol) "Laptop (Español)").

### Suspensión e hibernación

Consulte el artículo [suspensión e hibernación](/index.php/Power_management/Suspend_and_hibernate "Power management/Suspend and hibernate").

## Multimedia

La categoría [multimedia](/index.php/Category:Multimedia_(Espa%C3%B1ol) "Category:Multimedia (Español)") ofrece información adicional.

### Sonido

El [sonido](/index.php/Sound_system_(Espa%C3%B1ol) "Sound system (Español)") es proporcionado por los controladores de sonido del kernel:

*   [ALSA](/index.php/Advanced_Linux_Sound_Architecture_(Espa%C3%B1ol) "Advanced Linux Sound Architecture (Español)") se incluye en el kernel y es el método recomendado ya que generalmente funciona sin necesidad de configuración adicional (basta con [abrir los canales de audio](/index.php/Advanced_Linux_Sound_Architecture_(Espa%C3%B1ol)#Abrir_los_canales_de_audio "Advanced Linux Sound Architecture (Español)")).

*   [OSS](/index.php/Open_Sound_System_(Espa%C3%B1ol) "Open Sound System (Español)") es una alternativa viable en caso de que ALSA no funcione.

Los usuarios también pueden querer instalar y configurar un [servidor de sonido](/index.php/Sound_system_(Espa%C3%B1ol)#Servidores_de_sonido "Sound system (Español)") tal como [PulseAudio](/index.php/PulseAudio_(Espa%C3%B1ol) "PulseAudio (Español)"). Para conocer los requisitos de audio avanzados, consulte [audio profesional](/index.php/Professional_audio "Professional audio").

### Complementos para el navegador

Para acceder a cierto contenido web, se pueden instalar [complementos del navegador](/index.php/Browser_plugins_(Espa%C3%B1ol) "Browser plugins (Español)"), tales como Adobe Acrobat Reader, Adobe Flash Player y Java.

### Códecs

Los [códecs](/index.php/Codecs_(Espa%C3%B1ol) "Codecs (Español)") son ​​utilizados por las aplicaciones multimedia para codificar o decodificar transmisiones de audio o vídeo. Para reproducir transmisiones codificadas, los usuarios deben asegurarse de tener instalado un códec apropiado.

## Redes

Esta sección se limita a pequeños procedimientos de red. Consulte el artículo de [configuración de red](/index.php/Network_configuration_(Espa%C3%B1ol) "Network configuration (Español)") para obtener una guía completa. Para más información, consulte la categoría [Redes](/index.php/Category:Networking_(Espa%C3%B1ol) "Category:Networking (Español)").

### Sincronización del reloj

El [protocolo de tiempo de red](https://en.wikipedia.org/wiki/es:Network_Time_Protocol para conocer las implementaciones de dicho protocolo.

### Seguridad DNS

Para una mayor seguridad al navegar por la web, pagos en línea, conectarse a servicios [SSH](/index.php/Secure_Shell_(Espa%C3%B1ol) "Secure Shell (Español)") y tareas similares, considere utilizar aplicaciones clientes con soporte [DNSSEC](/index.php/DNSSEC "DNSSEC") que pueda validar registros [DNS](https://en.wikipedia.org/wiki/es:Domain_Name_System para cifrar el tráfico de DNS.

### Configurar un cortafuegos

Un servidor de seguridad puede proporcionar una capa de protección adicional sobre la pila de red de Linux. Si bien el kernel de Arch es capaz de utilizar [iptables](/index.php/Iptables_(Espa%C3%B1ol) "Iptables (Español)") de [Netfilter](https://en.wikipedia.org/wiki/es:Netfilter para ver las guías disponibles.

### Compartir recursos

Para compartir archivos entre las máquinas en una red, siga el artículo [NFS](/index.php/NFS_(Espa%C3%B1ol) "NFS (Español)") o el [SSHFS](/index.php/SSHFS "SSHFS").

Utilice [Samba](/index.php/Samba_(Espa%C3%B1ol) "Samba (Español)") para unirse a una red de Windows. Para configurar la máquina para utilizar la autenticación de Active Directory, consulte la [integración con Active Directory](/index.php/Active_Directory_Integration "Active Directory Integration").

Consulte también la categoría sobre [compartir recursos](/index.php/Category:Network_sharing_(Espa%C3%B1ol) "Category:Network sharing (Español)").

## Dispositivos de entrada

Esta sección contiene consejos para la configuración de dispositivos de entrada más populares. Para obtener más información, consulte la categoría de los [dispositivos de entrada](/index.php/Category:Input_devices_(Espa%C3%B1ol) "Category:Input devices (Español)").

### Distribuciones de teclado

Los teclados que no son en inglés o que no son estándar pueden no funcionar como se espera por defecto. Los pasos necesarios para configurar la distribución de teclas, que son diferentes para la consola virtual y [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)"), se describen en los artículos [configuración del teclado en la consola](/index.php/Keyboard_configuration_in_console_(Espa%C3%B1ol) "Keyboard configuration in console (Español)") y [configuración del teclado en Xorg](/index.php/Keyboard_configuration_in_Xorg_(Espa%C3%B1ol) "Keyboard configuration in Xorg (Español)") respectivamente.

### Botones del ratón

Los propietarios de ratones avanzados o inusuales pueden descubrir que no todos los botones del ratón se reconocen por defecto, o pueden querer asignar diferentes acciones para los botones adicionales. Las instrucciones se pueden encontrar en el artículo [botones del ratón](/index.php/Mouse_buttons "Mouse buttons").

### Pantalla táctil del portátil

Muchas computadoras portátiles usan dispositivos de señalamiento [Synaptics](https://www.synaptics.com/) o [ALPS](http://www.alps.com/). Para estos y otros modelos de panel táctil, puede usar el controlador de entrada Synaptics o libinput; consulte los artículos de [Synaptics](/index.php/Touchpad_Synaptics_(Espa%C3%B1ol) "Touchpad Synaptics (Español)") y [libinput](/index.php/Libinput_(Espa%C3%B1ol) "Libinput (Español)") para más detalles sobre la instalación y configuración.

### TrackPoints

Consulte el artículo [TrackPoint](/index.php/TrackPoint "TrackPoint") para configurar su dispositivo TrackPoint.

## Optimización

Esta sección tiene como objetivo resumir los ajustes, herramientas y opciones útiles disponibles para mejorar el rendimiento del sistema y las aplicaciones.

### Benchmarking

[Benchmarking](/index.php/Benchmarking "Benchmarking") es el acto de medir el rendimiento y comparar los resultados con los resultados de otro sistema o un estándar ampliamente aceptado a través de un procedimiento unificado.

### Mejorando el rendimiento

El artículo [mejorando el rendimiento](/index.php/Improving_performance_(Espa%C3%B1ol) "Improving performance (Español)") recoge información y es un resumen básico sobre cómo ganar rendimiento en Arch Linux.

### Discos de estado sólido

El artículo sobre [discos de estado sólido](/index.php/Solid_State_Drives "Solid State Drives") cubre muchos aspectos de las unidades de estado sólido, incluyendo como configurarlos para maximizar su vida útil.

## Servicios del sistema

Esta sección se relaciona con el artículos sobre los [demonios](/index.php/Daemons_(Espa%C3%B1ol) "Daemons (Español)"). Para obtener más información, consulte la categoría [daemons y servicios del sistema](/index.php/Category:Daemons_and_system_services_(Espa%C3%B1ol) "Category:Daemons and system services (Español)").

### Índice de archivos y búsqueda

La mayoría de las distribuciones tienen un comando de localización (*locate*) disponible para poder buscar rápidamente los archivos. Para obtener esta funcionalidad en Arch Linux, se recomienda la instalación de [mlocate](https://www.archlinux.org/packages/?name=mlocate). Después de la instalación, se debe ejecutar *updatedb* para indexar los sistemas de archivos.

Los [motores de búsqueda de escritorio](/index.php/List_of_applications/Utilities_(Espa%C3%B1ol)#Gestores_de_archivos "List of applications/Utilities (Español)") ofrecen un servicio similar, mientras están mejor integrados en los [entornos de escritorio](/index.php/Desktop_environment_(Espa%C3%B1ol) "Desktop environment (Español)").

### Entrega de correo electrónico local

Una configuración predeterminada no proporciona una forma de sincronizar el correo electrónico. Para configurar *Postfix* para la entrega simple en el buzón local, consulte [Postfix](/index.php/Postfix "Postfix"). Otras opciones son [SSMTP](/index.php/SSMTP "SSMTP"), [msmtp](/index.php/Msmtp "Msmtp") y [fdm](/index.php/Fdm "Fdm").

### Impresión

[CUPS](/index.php/CUPS_(Espa%C3%B1ol) "CUPS (Español)") es un sistema de impresión de código abierto basado en estándares desarrollado por Apple. Consulte la categoría sobre [impresoras](/index.php/Category:Printers_(Espa%C3%B1ol) "Category:Printers (Español)") para los artículos específicos de cada impresora.

## Apariencia

Esta sección contiene los ajustes de las «chucherías» *(Eye Candy)*, buscados con frecuencia para una experiencia estética más agradable. Para más información, consulte la categoría sobre [Eye Candy](/index.php/Category:Eye_candy_(Espa%C3%B1ol) "Category:Eye candy (Español)").

### Tipos de letra

Es posible que quiera instalar un conjunto de fuentes TrueType, ya que solo se incluyen fuentes de mapa de bits no escalables en un sistema Arch básico. Hay varias [familias de fuentes](/index.php/Fonts#Families "Fonts") de uso general que ofrecen una gran cobertura [Unicode](https://en.wikipedia.org/wiki/es:Unicode "wikipedia:es:Unicode") e incluso [compatibilidad métrica](/index.php/Metric-compatible_fonts "Metric-compatible fonts") con fuentes de otros sistemas operativos.

Se puede encontrar una gran cantidad de información sobre el tema en los artículos sobre los [tipos de letra](/index.php/Fonts_(Espa%C3%B1ol) "Fonts (Español)") y la [configuración de los tipos de letra](/index.php/Font_configuration "Font configuration").

Si pasa una cantidad significativa de tiempo trabajando desde la consola virtual (es decir, fuera de un servidor X), puede que quiera cambiar el tipo de letra de la consola para mejorar la legibilidad; consulte [Tipos de letra de consola](/index.php/Fonts#Console_fonts "Fonts").

### Temas para GTK+ y Qt

Una gran parte de las aplicaciones con una interfaz gráfica para sistemas Linux se basan en los kits de herramientas [GTK+](/index.php/GTK%2B_(Espa%C3%B1ol) "GTK+ (Español)") o [Qt](/index.php/Qt "Qt"). Consulte dichos artículos y [Apariencia uniforme para aplicaciones Qt y GTK](/index.php/Uniform_look_for_Qt_and_GTK_applications_(Espa%C3%B1ol) "Uniform look for Qt and GTK applications (Español)") para obtener ideas de como mejorar la apariencia de los programas instalados y adaptarlos a su gusto.

## Mejoras para la línea de comandos

Esta sección contiene pequeñas modificaciones que mejoran la usabilidad de los programas de línea de comandos. Para obtener más información, consulte la categoría sobre [Command shells](/index.php/Category:Command_shells_(Espa%C3%B1ol) "Category:Command shells (Español)").

### Mejoras de autocompletado con Tab

Se recomienda configurar correctamente [autocompletado con Tab](https://en.wikipedia.org/wiki/Command-line_completion "wikipedia:Command-line completion") de inmediato, como se indica en el artículo de la shell elegida.

### Alias

Crear alias para un comando, o un grupo del mismo, es una forma de ahorrar tiempo al usar la línea de comandos. Esto es especialmente útil para tareas repetitivas que no requieren una alteración significativa de sus parámetros entre ejecuciones. Los alias más comunes que ahorran tiempo se pueden encontrar en [alias](/index.php/Bash_(Espa%C3%B1ol)#Alias "Bash (Español)"), que son fáciles de extrapolar también a [zsh](/index.php/Zsh_(Espa%C3%B1ol) "Zsh (Español)").

### Shells alternativas

[Bash](/index.php/Bash_(Espa%C3%B1ol) "Bash (Español)") es el shell que está instalado por defecto en un sistema Arch. Sin embargo, los medios de instalación en vivo usan [zsh](/index.php/Zsh_(Espa%C3%B1ol) "Zsh (Español)") con el paquete de complemento [grml-zsh-config](https://www.archlinux.org/packages/?name=grml-zsh-config). Consulte el [listado de shells](/index.php/Command-line_shell#List_of_shells "Command-line shell") para conocer más alternativas.

### Complementos para bash

En la sección [consejos y trucos](/index.php/Bash_(Espa%C3%B1ol)#Consejos_y_trucos "Bash (Español)") de Bash se encuentra disponible una lista variada de configuraciones para Bash, historial de búsqueda y macros [Readline](/index.php/Readline "Readline").

### Salida coloreada

Esta sección se desarrolla en [Color output in console](/index.php/Color_output_in_console "Color output in console").

### Archivos comprimidos

Los archivos comprimidos se encuentran con frecuencia en un sistema GNU/Linux. [Tar](/index.php/Core_utilities_(Espa%C3%B1ol)#tar "Core utilities (Español)") es una de las herramientas de archivo más comúnmente utilizadas, y los usuarios deberían estar familiarizados con su sintaxis (los paquetes de Arch Linux, por ejemplo, son simplemente archivos tar comprimidos con xzip). Consulte el artículo sobre [archivado y compresión](/index.php/Archiving_and_compression "Archiving and compression").

### Indicador de la línea de comandos

El indicador de la línea de comandos (PS1, o *console prompt*) se puede personalizar en gran medida. Consulte [personalización del indicador de Bash](/index.php/Bash/Prompt_customization "Bash/Prompt customization") o [indficadores de Zsh](/index.php/Zsh_(Espa%C3%B1ol)#Prompts "Zsh (Español)") si usa Bash o Zsh, respectivamente.

### Shell emacs

Emacs es conocido por ofrecer opciones más allá de los usuales en la edición de texto, una de ellas es un reemplazo completo de la shell. Consulte [Emacs#Colored output issues](/index.php/Emacs#Colored_output_issues "Emacs") para obtener una solución con respecto a los caracteres ilegibles que pueden producirse al habilitar la salida coloreada.

### Soporte del ratón

Se puede preferir utilizar un ratón con la línea de comandos para operaciones de copiar y pegar en lugar del modo de copia tradicional de [GNU Screen](/index.php/GNU_Screen "GNU Screen"). Consulte el artículo sobre el [soporte del ratón](/index.php/General_purpose_mouse_(Espa%C3%B1ol) "General purpose mouse (Español)") para obtener instrucciones detalladas. Tenga en cuenta que ya puede hacer esto en [emuladores de terminal](/index.php/Terminal_emulators "Terminal emulators") con el [portapapeles](/index.php/Clipboard "Clipboard").

### Búfer de desplazamiento hacia atrás

Para poder guardar y ver el texto que se ha desplazado fuera de la pantalla, consulte [desplazamiento hacia atrás](/index.php/General_troubleshooting#Scrollback "General troubleshooting").

### Administración de las sesiones

Usando multiplexores de terminal como [tmux](/index.php/Tmux_(Espa%C3%B1ol) "Tmux (Español)") o [GNU Screen](/index.php/GNU_Screen "GNU Screen"), los programas se pueden ejecutar en sesiones compuestas por pestañas y paneles que se pueden separar a voluntad, de modo que cuando el usuario mata (mediante *kill*) el emulador de terminal, termina [X](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)") o cierra la sesión, los programas asociados con la sesión continuarán ejecutándose en segundo plano, siempre que el servidor del terminal multiplexor esté activo. Para recuperar la interacción con los programas se requiere volver a conectarse a la sesión.