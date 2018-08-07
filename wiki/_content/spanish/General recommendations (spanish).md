Artículos relacionados

*   [Preguntas frecuentes](/index.php/FAQ_(Espa%C3%B1ol) "FAQ (Español)")
*   [Guía de instalación](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)")
*   [Lista de aplicaciones](/index.php/List_of_applications_(Espa%C3%B1ol) "List of applications (Español)")

**Estado de la traducción:** este artículo es una versión traducida de [General recommendations](/index.php/General_recommendations "General recommendations"). Fecha de la última traducción/revisión: **2018-08-05**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=General_recommendations&diff=0&oldid=531455).

Este documento es un índice con anotaciones a otros artículos populares e información importante para mejorar y añadir funcionalidades al sistema Arch instalado. Se supone que los lectores han leído y seguido la [guía de instalación](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)") para instalar un sistema básico de Arch Linux. Es necesario haber leído y comprendido los conceptos explicados en [#Administración el sistema](#Administraci.C3.B3n_el_sistema) y [#Administración de paquetes](#Administraci.C3.B3n_de_paquetes) antes de continuar con las otras secciones de esta página y de otros artículos de la wiki.

## Contents

*   [1 Administración el sistema](#Administraci.C3.B3n_el_sistema)
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
    *   [4.4 Gestores de ventanas](#Gestores_de_ventanas)
    *   [4.5 Gestores de pantalla o de inicio de sesión](#Gestores_de_pantalla_o_de_inicio_de_sesi.C3.B3n)
*   [5 Gestionar la energía](#Gestionar_la_energ.C3.ADa)
    *   [5.1 Eventos de ACPI](#Eventos_de_ACPI)
    *   [5.2 Regulación de la frecuencia de la CPU](#Regulaci.C3.B3n_de_la_frecuencia_de_la_CPU)
    *   [5.3 Portátiles](#Port.C3.A1tiles)
    *   [5.4 Suspensión e hibernación](#Suspensi.C3.B3n_e_hibernaci.C3.B3n)
*   [6 Multimedia](#Multimedia)
    *   [6.1 Sonido](#Sonido)
    *   [6.2 Complementos para el navegador](#Complementos_para_el_navegador)
    *   [6.3 Códecs](#C.C3.B3decs)
*   [7 Gestionar la red](#Gestionar_la_red)
    *   [7.1 Sincronizar el reloj](#Sincronizar_el_reloj)
    *   [7.2 Seguridad DNS](#Seguridad_DNS)
    *   [7.3 Configurar un cortafuegos](#Configurar_un_cortafuegos)
    *   [7.4 Compartir recursos](#Compartir_recursos)
*   [8 Dispositivos de entrada](#Dispositivos_de_entrada)
    *   [8.1 Distribuciones de teclado](#Distribuciones_de_teclado)
    *   [8.2 Botones del ratón](#Botones_del_rat.C3.B3n)
    *   [8.3 Panel táctil del portátil](#Panel_t.C3.A1ctil_del_port.C3.A1til)
    *   [8.4 TrackPoints](#TrackPoints)
*   [9 Optimización](#Optimizaci.C3.B3n)
    *   [9.1 Benchmarking](#Benchmarking)
    *   [9.2 Mejorar el rendimiento](#Mejorar_el_rendimiento)
    *   [9.3 Unidades de estado sólido (SSD)](#Unidades_de_estado_s.C3.B3lido_.28SSD.29)
*   [10 Servicios del sistema](#Servicios_del_sistema)
    *   [10.1 Índice de archivos y búsqueda](#.C3.8Dndice_de_archivos_y_b.C3.BAsqueda)
    *   [10.2 Distribución del correo electrónico local](#Distribuci.C3.B3n_del_correo_electr.C3.B3nico_local)
    *   [10.3 Impresión](#Impresi.C3.B3n)
*   [11 Apariencia](#Apariencia)
    *   [11.1 Tipos de letras](#Tipos_de_letras)
    *   [11.2 Temas GTK+ y Qt](#Temas_GTK.2B_y_Qt)
*   [12 Mejoras para la consola](#Mejoras_para_la_consola)
    *   [12.1 Mejoras de autocompletado con Tab](#Mejoras_de_autocompletado_con_Tab)
    *   [12.2 Alias](#Alias)
    *   [12.3 Shells alternativas](#Shells_alternativas)
    *   [12.4 Complementos para bash](#Complementos_para_bash)
    *   [12.5 Salida coloreada](#Salida_coloreada)
    *   [12.6 Archivos comprimidos](#Archivos_comprimidos)
    *   [12.7 Consola del sistema](#Consola_del_sistema)
    *   [12.8 Shell emacs](#Shell_emacs)
    *   [12.9 Soporte para el ratón](#Soporte_para_el_rat.C3.B3n)
    *   [12.10 Búfer del scrollback](#B.C3.BAfer_del_scrollback)
    *   [12.11 Gestionar las sesiones](#Gestionar_las_sesiones)

## Administración el sistema

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

Consulte el artículo [Réplicas](/index.php/Mirrors_(Espa%C3%B1ol) "Mirrors (Español)") *(mirrors)* para conocer los pasos a seguir para aprovechar al máximo el uso y obtener las réplicas de los repositorios oficiales más actualizados. Como se explica en el artículo, un consejo especialmente bueno consiste en verificar periódicamente la página del [estado de las réplicas](https://www.archlinux.org/mirrors/status/) para consultar la lista de las réplicas que han sido recientemente sincronizadas.

### Sistema de construcción de Arch

Los *ports* son un sistema usado inicialmente por distribuciones BSD que consisten en secuencias de comandos *(scripts)* de compilación que se encuentran en un árbol de directorios en el sistema local. En pocas palabras, cada *port* contiene una secuencia de comandos dentro de un directorio con un nombre intuitivo que hace referencia a la aplicación de terceros instalable.

El [sistema de construcción de Arch](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)") (ABS, *Arch Build System*) ofrece la misma funcionalidad al proporcionar unas secuencias de comandos de compilación llamadas [PKGBUILDs](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)"), que se cargan con información conocida para una determinada pieza de software: control de la integridad, URL del proyecto, versión, licencia e instrucciones de compilación. Estos PKGBUILDs son analizados posteriormente por [makepkg](/index.php/Makepkg_(Espa%C3%B1ol) "Makepkg (Español)"), el programa que actualmente genera paquetes es gestionado limpiamente por pacman.

Cada paquete de los repositorios junto con los presentes en AUR están sujetos a recompilación con makepkg.

### Repositorio de usuario de Arch

Si bien el sistema de construcción de Arch (ABS) permite la posibilidad de construir los programas disponibles en los repositorios oficiales, el [repositorio de usuario de Arch](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)") (AUR, *Arch User Repository*) es el equivalente para los paquetes enviados por los usuarios. Es un repositorio sin soporte oficial de secuencias de comandos de compilación, accesibles a través de la [interfaz web](https://aur.archlinux.org/) o a través de la interfaz [Aurweb RPC](/index.php/Aurweb_RPC_interface "Aurweb RPC interface").

## Arranque

Esta sección contiene información relacionada con el proceso de arranque. Se puede encontrar una descripción general del proceso de arranque de Arch en el artículo [proceso de arranque](/index.php/Arch_boot_process_(Espa%C3%B1ol) "Arch boot process (Español)"). Para obtener más información, consulte la categoría [proceso de arranque](/index.php/Category:Boot_process_(Espa%C3%B1ol) "Category:Boot process (Español)").

### Reconocimiento automático del hardware

El hardware debe ser detectado automáticamente por [udev](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)") durante el proceso de arranque de forma predeterminada. Se puede lograr una mejora potencial en el tiempo de arranque desactivando la carga automática de los módulos y especificando los módulos requeridos manualmente, como se describe en [módulos del núcleo](/index.php/Kernel_modules_(Espa%C3%B1ol) "Kernel modules (Español)"). Además, [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)") debería ser capaz de detectar automáticamente los controladores necesarios mediante `udev`, aunque los usuarios también tienen la opción de configurar el servidor X manualmente.

### Microcódigo

Los procesadores pueden tener un [comportamiento defectuoso](http://www.anandtech.com/show/8376/intel-disables-tsx-instructions-erratum-found-in-haswell-haswelleep-broadwelly), que el núcleo puede corregir mediante la actualización del *microcódigo* al inicio. Los procesadores de Intel requieren un paquete separado para este fin. Consulte [microcódigo](/index.php/Microcode_(Espa%C3%B1ol) "Microcode (Español)") para más detalles.

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

A pesar de que [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)") proporciona el marco básico para la construcción de un entorno gráfico, componentes adicionales pueden ser necesarios para una experiencia completa del usuario. Los [Entornos de Escritorios](/index.php/Desktop_environment_(Espa%C3%B1ol) "Desktop environment (Español)") como [GNOME](/index.php/GNOME "GNOME"), [KDE](/index.php/KDE "KDE"), [LXDE](/index.php/LXDE "LXDE"), y [Xfce](/index.php/Xfce "Xfce") vienen acompañados de una amplia gama de clientes de *X*, como gestores de ventanas, paneles, administradores de archivos, emuladores de terminal, editores de texto, iconos y otras utilidades. Véase [Category:Desktop environments](/index.php/Category:Desktop_environments "Category:Desktop environments") para una lista completa y recursos adicionales.

### Gestores de ventanas

Un completo [entorno de escritorio](/index.php/Desktop_environment_(Espa%C3%B1ol) "Desktop environment (Español)") proporciona una interfaz gráfica de usuario funcional y consistente, pero también tiende a consumir una cantidad considerable de recursos del sistema. Los usuarios que buscan maximizar el rendimiento o, de otra manera, simplificar su entorno, la opción a instalar es un [window manager](/index.php/Window_manager_(Espa%C3%B1ol) "Window manager (Español)") en su lugar y añadir manualmente los extras deseados. Alternativamente, un gestor de ventanas también se puede utilizar conjuntamente con la mayoría de los entornos de escritorio. Los gestores de ventanas difieren en el manejo de la colocación de las ventanas: [dinámicas](/index.php/Category:Dynamic_WMs "Category:Dynamic WMs"), [apiladas](/index.php/Category:Stacking_WMs "Category:Stacking WMs"), y [en mosaico](/index.php/Category:Tiling_WMs "Category:Tiling WMs").

### Gestores de pantalla o de inicio de sesión

La mayoría de los entornos de escritorios incluyen un [display manager](/index.php/Display_manager "Display manager") para iniciar automáticamente el entorno gráfico y gestionar los inicios de sesión del usuario. Los usuarios sin un entorno de escritorio pueden instalar un gestor de ventanas por separado. También es posible [iniciar X al iniciar sesión](/index.php/Start_X_at_login "Start X at login") como una alternativa simple a un gestor de ventanas.

## Gestionar la energía

Esta sección puede ser de utilidad para los propietarios de portátiles o usuarios que buscan otra forma de controlar la gestión de energía. Para más información, consulte [Category:Power management](/index.php/Category:Power_management "Category:Power management").

Consulte [Power management](/index.php/Power_management "Power management") para una descripción más general.

### Eventos de ACPI

Los usuarios pueden configurar la forma en que el sistema reacciona a los eventos ACPI como al pulsar el botón de encendido o al cerrar la tapa del portátil. Para el método nuevo (recomendado) usando [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)"), véase el artículo sobre la[gestión de energía con systemd](/index.php/Power_management_(Espa%C3%B1ol)#Gesti.C3.B3n_de_energ.C3.ADa_con_systemd "Power management (Español)"). Para el método antiguo, véase [acpid](/index.php/Acpid "Acpid").

### Regulación de la frecuencia de la CPU

Los procesadores modernos pueden disminuir su frecuencia y el voltaje para reducir el calor y consumo de energía. Menos calor conduce a un sistema más silencioso y prolonga la vida del hardware. Véase [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling") para más detalles.

### Portátiles

Para los artículos relacionados con la informática portátil junto con las guías de instalación específicas de cada modelo, consulte [Category:Laptops](/index.php/Category:Laptops "Category:Laptops"). Para una descripción general de artículos y recomendaciones relacionados con el portátil, vea [Laptop](/index.php/Laptop "Laptop").

### Suspensión e hibernación

Véase el artículo [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate").

## Multimedia

La categoría [Multimedia](/index.php/Category:Multimedia "Category:Multimedia") incluye recursos adicionales.

### Sonido

El [sonido](/index.php/Sound "Sound") es proporcionado por los controladores de sonido del kernel:

*   [ALSA](/index.php/ALSA "ALSA") se incluye con el kernel y se recomienda; por lo general, funciona sin necesidad configuración adicional (basta con [activar el sonido](/index.php/Advanced_Linux_Sound_Architecture#Unmuting_the_channels "Advanced Linux Sound Architecture")).

*   [OSS](/index.php/OSS "OSS") es una alternativa viable en caso de que ALSA no funcione.

Los usuarios, además, pueden instalar y configurar un [servidor de sonido](/index.php/Sound_system#Sound_servers "Sound system") tal como [PulseAudio](/index.php/PulseAudio "PulseAudio"). Para conocer los requisitos de audio avanzados, consulte [professional audio](/index.php/Professional_audio "Professional audio").

### Complementos para el navegador

Para disfrutar de los contenidos multimedia de la web y para una *completa* experiencia de navegación, se pueden instalar [plugins al navegador](/index.php/Browser_plugins "Browser plugins") como Adobe Acrobat Reader, Adobe Flash Player y Java.

### Códecs

Los [códecs](/index.php/Codecs_(Espa%C3%B1ol) "Codecs (Español)") son ​​utilizados por las aplicaciones multimedia para codificar o decodificar transmisiones de audio o vídeo. Con el fin de reproducir secuencias codificadas, los usuarios deben asegurarse de tener instalado un códec apropiado.

## Gestionar la red

Esta sección se limita a ilustrar simples procedimientos para la mayoría de las conexiones de red. Consulte [Network](/index.php/Network "Network") para una guía completa. Para más información: [Category:Networking](/index.php/Category:Networking "Category:Networking").

### Sincronizar el reloj

El [Network Time Protocol](/index.php/Network_Time_Protocol "Network Time Protocol") (NTP) es un protocolo para sincronizar el horario de los sistemas informáticos mediante la conmutación de datos, latencia variable de datos a través de la red. Véase [Time#Time synchronization](/index.php/Time#Time_synchronization "Time") para las implementaciones de estos protocolos.

### Seguridad DNS

Para una mayor seguridad durante la navegación web, pagar en línea, conectarse a servicios [SSH](/index.php/SSH "SSH") y tareas similares, se debe considerar el uso del software habilitado para el cliente [DNSSEC](/index.php/DNSSEC "DNSSEC") que puede validar firmas certificadas por el [DNS](https://en.wikipedia.org/wiki/Domain_Name_System "wikipedia:Domain Name System"), y [DNSCrypt](/index.php/DNSCrypt "DNSCrypt") para cifrar el tráfico DNS.

### Configurar un cortafuegos

Un cortafuegos puede proporcionar una capa adicional de protección para navegar por la red con Linux. Mientras que el núcleo de Arch es capaz de usar [iptables](/index.php/Iptables "Iptables") y [nftables](/index.php/Nftables "Nftables"), ninguno está activado por defecto. Es altamente recomendable establecer algún tipo de cortafuegos. Consulte [Category:Firewalls](/index.php/Category:Firewalls "Category:Firewalls") para las guías detalladas.

### Compartir recursos

Para compartir archivos entre los equipos conectados a una red, siga el artículo [NFS](/index.php/NFS "NFS") o [SSHFS](/index.php/SSHFS "SSHFS").

Utilice [Samba](/index.php/Samba "Samba") para unirse a una red de Windows. Para configurar el equipo para utilizar «Active Directory» para la autenticación, lea [Active Directory Integration](/index.php/Active_Directory_Integration "Active Directory Integration").

Véase también [Category:Network sharing](/index.php/Category:Network_sharing "Category:Network sharing").

## Dispositivos de entrada

Esta sección contiene consejos comunes de configuración del dispositivo de entrada. Para más información, consulte [Category:Input devices](/index.php/Category:Input_devices "Category:Input devices").

### Distribuciones de teclado

Las distribuciones de teclados para idiomas distintos del inglés o teclados no estándar pueden no funcionar como se espera por defecto. Los pasos necesarios para configurar la distribución del teclado son diferentes para la consola virtual y [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)"), que se describen en [Keyboard configuration in console (Español)](/index.php/Keyboard_configuration_in_console_(Espa%C3%B1ol) "Keyboard configuration in console (Español)") y [Keyboard configuration in Xorg (Español)](/index.php/Keyboard_configuration_in_Xorg_(Espa%C3%B1ol) "Keyboard configuration in Xorg (Español)") respectivamente.

### Botones del ratón

Los propietarios de ratones inusuales o con características avanzadas pueden encontrar que no todos los botones del ratón son reconocidos por defecto, o, tal vez, deseen asignar diferentes acciones para los botones adicionales. Las instrucciones para solventar estas cuestiones se pueden encontrar en [All Mouse Buttons Working](/index.php/All_Mouse_Buttons_Working "All Mouse Buttons Working").

### Panel táctil del portátil

Muchos ordenadores portátiles utilizan dispositivos señaladores «touchpad» [Synaptics](https://www.synaptics.com/) o [ALPS](http://www.alps.com/). Para estos y otros modelos de panel táctil, puede usar tanto el controlador de entrada Synaptics como libinput; consulte [Touchpad Synaptics](/index.php/Touchpad_Synaptics_(Espa%C3%B1ol) "Touchpad Synaptics (Español)") y [libinput](/index.php/Libinput "Libinput") para la instalación y detalles de configuración.

### TrackPoints

Para configurar el dispositivo TrackPoint consulte [ThinkWiki](http://www.thinkwiki.org/wiki/How_to_configure_the_TrackPoint).

## Optimización

Esta sección pretende resumir ajustes, herramientas y opciones útiles para mejorar el sistema y el rendimiento de las aplicaciones.

### Benchmarking

[Benchmarking](/index.php/Benchmarking "Benchmarking") es un método de medición del rendimiento, a través de un procedimiento unificado y ampliamente aceptado, y la posterior comparación de los resultados con los obtenidos por otro sistema o por un estándar de referencia.

### Mejorar el rendimiento

El artículo [Improving performance](/index.php/Improving_performance "Improving performance") recoge información y constituye un resumen básico sobre cómo ganar rendimiento en Arch Linux.

### Unidades de estado sólido (SSD)

El artículo sobre [Solid State Drives](/index.php/Solid_State_Drives "Solid State Drives") trata aspectos útiles sobre diversos aspectos de las unidades de estado sólido, como, por ejemplo, cómo configurarlos para maximizar su vida útil.

## Servicios del sistema

Esta sección se refiere a los [daemons](/index.php/Daemons "Daemons"). Para más información, consulte [Category:Daemons and system services](/index.php/Category:Daemons_and_system_services "Category:Daemons and system services").

### Índice de archivos y búsqueda

La mayoría de las distribuciones tienen orden `locate` disponible para poder buscar rápidamente los archivos. Para obtener esta funcionalidad, [mlocate](https://www.archlinux.org/packages/?name=mlocate) es la instalación recomendada. Después de la instalación se debe ejecutar `updatedb` para indexar el sistema de archivos.

[Desktop search engines](/index.php/List_of_applications/Utilities#Finders "List of applications/Utilities") ofrece un servicio similar, mientras está mejor integrado en los [desktop environment](/index.php/Desktop_environment "Desktop environment").

### Distribución del correo electrónico local

Una configuración por defecto no proporciona una forma de sincronizar el correo electrónico. Para configurar Postfix, a fin de gestionar una simple bandeja local de entrega de correo, véase [Local Mail Delivery with Postfix](/index.php/Local_Mail_Delivery_with_Postfix "Local Mail Delivery with Postfix"). Otras opciones son [SSMTP](/index.php/SSMTP "SSMTP"), [Msmtp](/index.php/Msmtp "Msmtp") y [fdm](/index.php/Fdm "Fdm").

### Impresión

[CUPS](/index.php/CUPS_(Espa%C3%B1ol) "CUPS (Español)") está basado en estándares, un sistema de impresión de código abierto desarrollado por Apple. Véase [Category:Printers](/index.php/Category:Printers "Category:Printers") para artículos específicos de cada impresora.

## Apariencia

Esta sección contiene los frecuentemente buscados ajustes «Eye Candy» para una experiencia de Arch estéticamente más agradable. Para más información, consulte [Category:Eye candy](/index.php/Category:Eye_candy "Category:Eye candy").

### Tipos de letras

Es posible que desee instalar un conjunto de fuentes TrueType, ya que solo se incluyen, por defecto, en una instalación básica de Arch las fuentes bitmap no escalables. Hay varias [font families](/index.php/Fonts#Families "Fonts") de uso general que ofrecen una gran cobertura [Unicode](https://en.wikipedia.org/wiki/Unicode "wikipedia:Unicode") e incluso [metric compatibility](/index.php/Metric-compatible_fonts "Metric-compatible fonts") con fuentes de otros sistemas operativos.

Una gran cantidad de información sobre el tema se puede encontrar en los artículos [Fonts](/index.php/Fonts "Fonts") y [Font configuration](/index.php/Font_configuration "Font configuration").

Si pasa una cantidad significativa de tiempo trabajando con la consola virtual (es decir, fuera de un servidor X), puede que quiera cambiar el tipo de letra para facilitar la lectura de la consola; consulte [Fonts#Console fonts](/index.php/Fonts#Console_fonts "Fonts").

### Temas GTK+ y Qt

Gran parte de las aplicaciones que disponen de una interfaz gráfica en los sistemas Linux se basan en herramientas [GTK+](/index.php/GTK%2B "GTK+") o [Qt](/index.php/Qt "Qt"). Vea estos artículos, así como [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications") para obtener ideas de cómo mejorar la apariencia de los programas instalados y adaptarlos a su gusto.

## Mejoras para la consola

Esta sección aplica pequeñas modificaciones para mejorar la usabilidad de programas desde la línea de órdenes. Para más información, por favor, consulte [Category:Command shells](/index.php/Category:Command_shells "Category:Command shells").

### Mejoras de autocompletado con Tab

Se recomienda configurar correctamente [tab completion](https://en.wikipedia.org/wiki/Command-line_completion "wikipedia:Command-line completion") de inmediato, como se indica en el artículo de su shell elegida.

### Alias

Crear alias para una orden, o para un grupo de órdenes, es una manera de ahorrar tiempo al utilizar la consola. Esto es especialmente útil para tareas repetitivas que no necesitan una alteración significativa de los parámetros entre ejecuciones. Los alias más comunes que permiten ahorrar tiempo se pueden encontrar en [Bash#Aliases](/index.php/Bash#Aliases "Bash"), fáciles de extrapolar también a [zsh](/index.php/Zsh "Zsh").

### Shells alternativas

[Bash](/index.php/Bash "Bash") es el shell que se instala por defecto en un sistema Arch. El soporte de instalación live, sin embargo, utiliza [zsh](/index.php/Zsh "Zsh") con el paquete complementario [grml-zsh-config](https://www.archlinux.org/packages/?name=grml-zsh-config). Véase [Command shell#List of shells](/index.php/Command_shell#List_of_shells "Command shell") para conocer más alternativas.

### Complementos para bash

Una lista de ajustes variados para Bash, historial de búsquedas y macros [Readline](/index.php/Readline "Readline") está disponible en [Bash#Tips and tricks](/index.php/Bash#Tips_and_tricks "Bash").

### Salida coloreada

Esta sección se desarrolla en [Color output in console](/index.php/Color_output_in_console "Color output in console").

### Archivos comprimidos

Los archivos comprimidos se encuentran con frecuencia en un sistema GNU/Linux. [Tar](/index.php/Tar "Tar") es una de las herramientas más utilizadas de compresión, y los usuarios deben estar familiarizados con su sintaxis (los paquetes de Arch Linux, por ejemplo, son simplemente tarballs xzipped). Consulte [Archiving and compression](/index.php/Archiving_and_compression "Archiving and compression").

### Consola del sistema

La consola prompt (PS1) se puede personalizar en gran medida. Consulte [Bash/Prompt customization](/index.php/Bash/Prompt_customization "Bash/Prompt customization") o [Zsh#Prompts](/index.php/Zsh#Prompts "Zsh") si usa Bash or Zsh, respectivamente.

### Shell emacs

Emacs es conocido por incluir opciones adicionales a las funciones normales del editor de texto, una de las cuales puede consistir en un reemplazo completo de la shell. Consulte [Emacs#Colored output issues](/index.php/Emacs#Colored_output_issues "Emacs") para una revisión acerca de los caracteres distorsionados que pueden producirse al activar la salida de color.

### Soporte para el ratón

El uso de un ratón con la consola para las operaciones de copiar y pegar puede ser preferible a la forma tradicional de copiar de GNU [screen](/index.php/Screen "Screen"). Consulte [Console mouse support](/index.php/Console_mouse_support "Console mouse support") para obtener instrucciones completas. Tenga en cuenta que ya puede hacer esto en [terminal emulators](/index.php/Terminal_emulators "Terminal emulators") con el [clipboard](/index.php/Clipboard "Clipboard").

### Búfer del scrollback

Para poder guardar, fuera de la pantalla, y ver posteriormente el texto que salió en la pantalla, consulte [General troubleshooting#Scrollback](/index.php/General_troubleshooting#Scrollback "General troubleshooting").

### Gestionar las sesiones

Utilizando terminales [multiplexores](https://es.wikipedia.org/wiki/Multiplexor) como [tmux](/index.php/Tmux "Tmux") o [screen](/index.php/Screen "Screen"), los programas pueden ejecutarse en sesiones compuestas por pestañas y paneles que pueden ser separadas a voluntad, por lo que cuando el usuario cierra el emulador de terminal, termina [X](/index.php/X "X") o se cierra la sesión, los programas asociados a la sesión continuarán funcionando en segundo plano mientras el servidor del terminal multiplexor esté activo. Para poder interactuar con los programas se requiere volver a conectarse a la sesión.