Artículos relacionados

*   [CUPS printer sharing](/index.php/CUPS_printer_sharing "CUPS printer sharing")
*   [CUPS printer-specific problems](/index.php/CUPS_printer-specific_problems "CUPS printer-specific problems")
*   [Samba](/index.php/Samba "Samba")

De la [web de CUPS](http://www.cups.org/index.php):

	«*[CUPS](https://en.wikipedia.org/wiki/es:Common_Unix_Printing_System "wikipedia:es:Common Unix Printing System") es el sistema de impresión, basado en estándares y de código abierto, desarrollado por Apple Inc. para Mac OS® X y otros sistemas operativos basados en UNIX®*».

Aunque hay otras alternativas de impresión como LPRng, el Sistema de Impresión Común de Unix (***C**ommon **U**nix **P**rinting **S**ystem*) es la opción más popular debido a su relativa facilidad de uso.

## Contents

*   [1 Cups Linux Printing workflow](#Cups_Linux_Printing_workflow)
*   [2 Instalar el paquete del cliente](#Instalar_el_paquete_del_cliente)
    *   [2.1 Configuración avanzada opcional para la red](#Configuraci.C3.B3n_avanzada_opcional_para_la_red)
    *   [2.2 Instalar CUPS en un entorno chroot de 32 bits](#Instalar_CUPS_en_un_entorno_chroot_de_32_bits)
*   [3 Instalar los paquetes del servidor](#Instalar_los_paquetes_del_servidor)
    *   [3.1 Controladores para la imprerosa](#Controladores_para_la_imprerosa)
        *   [3.1.1 Descargar el PPD de la impresora](#Descargar_el_PPD_de_la_impresora)
        *   [3.1.2 Otros recursos para los controladores de la impresora](#Otros_recursos_para_los_controladores_de_la_impresora)
*   [4 Configuración y soporte técnico del hardware](#Configuraci.C3.B3n_y_soporte_t.C3.A9cnico_del_hardware)
    *   [4.1 Impresoras USB](#Impresoras_USB)
        *   [4.1.1 Introducir en blacklisting el módulo usblp](#Introducir_en_blacklisting_el_m.C3.B3dulo_usblp)
    *   [4.2 Impresoras en puerto paralelo](#Impresoras_en_puerto_paralelo)
    *   [4.3 Impresora HP](#Impresora_HP)
*   [5 Configuración](#Configuraci.C3.B3n)
    *   [5.1 El demonio CUPS](#El_demonio_CUPS)
    *   [5.2 Interfaz web y herramientas](#Interfaz_web_y_herramientas)
        *   [5.2.1 Administración de CUPS](#Administraci.C3.B3n_de_CUPS)
        *   [5.2.2 Acceso remoto a la interfaz web](#Acceso_remoto_a_la_interfaz_web)
    *   [5.3 Configuración a través de línea de órdenes](#Configuraci.C3.B3n_a_trav.C3.A9s_de_l.C3.ADnea_de_.C3.B3rdenes)
    *   [5.4 Interfaz CUPS alternativas](#Interfaz_CUPS_alternativas)
        *   [5.4.1 GNOME](#GNOME)
        *   [5.4.2 KDE](#KDE)
        *   [5.4.3 Otro](#Otro)
*   [6 Impresora virtual PDF](#Impresora_virtual_PDF)
    *   [6.1 Imprimir en postscript](#Imprimir_en_postscript)
*   [7 Solución de Problemas](#Soluci.C3.B3n_de_Problemas)
    *   [7.1 Problemas relacionados con las actualizaciones](#Problemas_relacionados_con_las_actualizaciones)
        *   [7.1.1 CUPS deja de funcionar](#CUPS_deja_de_funcionar)
        *   [7.1.2 Todos los trabajos están «detenidos»](#Todos_los_trabajos_est.C3.A1n_.C2.ABdetenidos.C2.BB)
        *   [7.1.3 Todos los trabajos derivan a «The printer is not responding» (La impresora no responde)](#Todos_los_trabajos_derivan_a_.C2.ABThe_printer_is_not_responding.C2.BB_.28La_impresora_no_responde.29)
        *   [7.1.4 La versión PPD no es compatible con gutenprint](#La_versi.C3.B3n_PPD_no_es_compatible_con_gutenprint)
    *   [7.2 Otros](#Otros)
        *   [7.2.1 Errores de permisos CUPS](#Errores_de_permisos_CUPS)
        *   [7.2.2 La impresora HPLIP envía como error «/usr/lib/cups/backend/hp failed»](#La_impresora_HPLIP_env.C3.ADa_como_error_.C2.AB.2Fusr.2Flib.2Fcups.2Fbackend.2Fhp_failed.C2.BB)
        *   [7.2.3 HPLIP indica que todos los trabajos se han completado pero la impresora no responde](#HPLIP_indica_que_todos_los_trabajos_se_han_completado_pero_la_impresora_no_responde)
        *   [7.2.4 hp-setup solicita que especifique el archivo PPD para la impresora descubierta](#hp-setup_solicita_que_especifique_el_archivo_PPD_para_la_impresora_descubierta)
        *   [7.2.5 Qt instalado, pero hp-setup informa: "Qt/PyQt 4 initialization failed" (*«no se puede iniciar Qt/PyQt 4»*)](#Qt_instalado.2C_pero_hp-setup_informa:_.22Qt.2FPyQt_4_initialization_failed.22_.28.C2.ABno_se_puede_iniciar_Qt.2FPyQt_4.C2.BB.29)
        *   [7.2.6 hp-setup encuentra la impresora automáticamente, pero informa que "Unable to communicate with device" (*«No se puede comunicar con el dispositivo»*) inmediatamente después de imprimir la página de prueba](#hp-setup_encuentra_la_impresora_autom.C3.A1ticamente.2C_pero_informa_que_.22Unable_to_communicate_with_device.22_.28.C2.ABNo_se_puede_comunicar_con_el_dispositivo.C2.BB.29_inmediatamente_despu.C3.A9s_de_imprimir_la_p.C3.A1gina_de_prueba)
        *   [7.2.7 hp-toolbox envía como error, «Unable to communicate with device» («No se puede comunicar con el dispositivo»)](#hp-toolbox_env.C3.ADa_como_error.2C_.C2.ABUnable_to_communicate_with_device.C2.BB_.28.C2.ABNo_se_puede_comunicar_con_el_dispositivo.C2.BB.29)
        *   [7.2.8 CUPS responde '«foomatic-rip» not available/stopped with status 3' con una impresora HP](#CUPS_responde_.27.C2.ABfoomatic-rip.C2.BB_not_available.2Fstopped_with_status_3.27_con_una_impresora_HP)
        *   [7.2.9 La impresora falla indicando error de autorización](#La_impresora_falla_indicando_error_de_autorizaci.C3.B3n)
        *   [7.2.10 Botón de impresora bloqueado en aplicaciones GNOME](#Bot.C3.B3n_de_impresora_bloqueado_en_aplicaciones_GNOME)
        *   [7.2.11 Formato soportado desconocido: application/postscript](#Formato_soportado_desconocido:_application.2Fpostscript)
        *   [7.2.12 Cambiar los URI para los servidores de la impresora de Windows](#Cambiar_los_URI_para_los_servidores_de_la_impresora_de_Windows)
        *   [7.2.13 Error de impresora client-error-document-format-not-supported](#Error_de_impresora_client-error-document-format-not-supported)
        *   [7.2.14 Error /usr/lib/cups/backend/hp](#Error_.2Fusr.2Flib.2Fcups.2Fbackend.2Fhp)
        *   [7.2.15 «Unable to get list of printer drivers»](#.C2.ABUnable_to_get_list_of_printer_drivers.C2.BB)
        *   [7.2.16 lp: Error - Scheduler Not Responding](#lp:_Error_-_Scheduler_Not_Responding)
        *   [7.2.17 CUPS imprime solo un vacío y una página de mensajes de error en HP LaserJet](#CUPS_imprime_solo_un_vac.C3.ADo_y_una_p.C3.A1gina_de_mensajes_de_error_en_HP_LaserJet)
        *   [7.2.18 Mensaje de error «Using invalid Host»](#Mensaje_de_error_.C2.ABUsing_invalid_Host.C2.BB)
        *   [7.2.19 La impresora no funciona o devuelve como error «Filter failed» en la interfaz web de CUPS (HP printer)](#La_impresora_no_funciona_o_devuelve_como_error_.C2.ABFilter_failed.C2.BB_en_la_interfaz_web_de_CUPS_.28HP_printer.29)
        *   [7.2.20 La impresora no imprime con un mensaje de "Filter failed" en la interfaz web de CUPS (impresora HP conectada por red)](#La_impresora_no_imprime_con_un_mensaje_de_.22Filter_failed.22_en_la_interfaz_web_de_CUPS_.28impresora_HP_conectada_por_red.29)
        *   [7.2.21 HPLIP 3.13: el plugin está instalado, pero el administrador de dispositivos de HP se queja de que no es así](#HPLIP_3.13:_el_plugin_est.C3.A1_instalado.2C_pero_el_administrador_de_dispositivos_de_HP_se_queja_de_que_no_es_as.C3.AD)
        *   [7.2.22 La impresora no es reconocida por CUPS](#La_impresora_no_es_reconocida_por_CUPS)
        *   [7.2.23 No se puede cargar /etc/samba/smb.conf](#No_se_puede_cargar_.2Fetc.2Fsamba.2Fsmb.conf)
        *   [7.2.24 El servicio systemd de CUPS no se inicia aunque está activado](#El_servicio_systemd_de_CUPS_no_se_inicia_aunque_est.C3.A1_activado)
*   [8 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Cups Linux Printing workflow

Desde la versión 1.5.3-3 de [cups](https://www.archlinux.org/packages/?name=cups), Arch Linux utiliza el sistema de impresión completamente nuevo pdf-based. Para obtener más información, consulte el artículo [PDF standard printing job format](http://www.linuxfoundation.org/collaborate/workgroups/openprinting/pdfasstandardprintjobformat) y este otro más antiguo [Cups filtering chart](https://wiki.linuxfoundation.org/en/OpenPrinting/Database/CUPS-Filter-Chart) para conocer la historia e ilustrarse. Un buen punto de partida para comprender mejor cómo se gestiona todo el proceso de impresión es [este artículo](http://www.linuxfoundation.org/collaborate/workgroups/openprinting).

Hay dos maneras de configurar una impresora:

*   Si tiene un servidor CUPS de Linux ejecutándose en su red y una impresora compartida, solo necesita instalar el paquete cliente.
*   Si la impresora está conectada directamente a su sistema o si tiene acceso a una impresora de red IPP, entonces configure un servidor CUPS local.

## Instalar el paquete del cliente

El paquete [libcups](https://www.archlinux.org/packages/?name=libcups) es el único necesario. [Instálelo](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

A continuación, agregue la dirección IP del servidor CUPS o el nombre del equipo en `/etc/cups/client.conf`. Eso es todo lo que se necesita. Cada solicitud debe rápidamente encontrar la impresora(s) compartida por el servidor CUPS.

### Configuración avanzada opcional para la red

Es posible ejecutar una instancia de cupsd+cups-browsed en el propio cliente con la ayuda de Avahi habilitado en el navegador para descubrir las IP de las impresoras que se comparten en red. Esto tiene sentido en configuraciones de grandes redes, donde el servidor es desconocido.

**Nota:**

*   Este comportamiento no ha cambiado con cups 1.6.x - la diferencia es que hasta la versión 1.5.x, la interfaz web de cupsd era capaz de hacer este proceso por sí sola y ahora necesita del auxilio de avahi para descubrir las impresoras conectadas.
*   Para conseguir que un cliente cupsd local reconozca otras impresoras compartidas ofrecidas por un servidor cupds remoto, se necesita ejecutar una instancia del navegador cups local (soporte proporcionado por cups-filters 1.0.26) mediante Avahi para descubrir impresoras desconocidas.
*   Hay [buenas noticias](https://bbs.archlinux.org/viewtopic.php?id=161440) de Abril 2013 (aún tiene que ser incorporado lo anterior).

### Instalar CUPS en un entorno chroot de 32 bits

Si tiene una instalación base de 64 bit con un [entorno chroot de 32 bit](/index.php/Install_bundled_32-bit_system_in_Arch64 "Install bundled 32-bit system in Arch64"), no es necesaria la instalación explícita de CUPS en un entorno de 32 bit. Para acceder desde el entorno chroot a las impresoras CUPS instaladas, es necesario unir el directorio `/var/run/cups` a la misma ubicación con respecto a la del entorno chroot. Basta con crear el directorio en el entorno chroot (que probablemente no exista), montarlo (con la opción `-o bind` añadida a la orden), y las impresoras deben estar disponibles para las aplicaciones en el entorno chroot de 32 bit inmediatamente.

```
# mkdir /ruta/al/entorno_chroot/var/run/cups
# Ejemplo: # mkdir /opt/arch32/var/run/cups

# mount -o bind /var/run/cups /ruta/al/entorno_chroot/var/run/cups
```

## Instalar los paquetes del servidor

Son necesarios los siguientes paquetes y algunos controladores de impresora. [Instálelos](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

*   [cups](https://www.archlinux.org/packages/?name=cups) - el demonio CUPS presente.
*   [ghostscript](https://www.archlinux.org/packages/?name=ghostscript) - (opcional) el intérprete para el lenguaje PostScript.
*   [gsfonts](https://www.archlinux.org/packages/?name=gsfonts) - el tipo de letra estándar GhostScript Type1.

Para poder usar la impresora en red es necesario intalar también [avahi](https://www.archlinux.org/packages/?name=avahi) y activar `avahi-daemon.service` [con systemd](/index.php/Systemd_(Espa%C3%B1ol)#Usar_las_unidades "Systemd (Español)").

Si el sistema está conectado a una impresora en red utilizando el protocolo [Samba](/index.php/Samba "Samba") o si el sistema va a ser utilizado como un servidor de impresión para clientes de Windows, instale también el paquete [samba](https://www.archlinux.org/packages/?name=samba).

### Controladores para la imprerosa

A continuación se relacionan algunos paquetes de controladores. Elegir el controlador adecuado dependerá, obviamente, de su impresora:

*   [gutenprint](https://www.archlinux.org/packages/?name=gutenprint) - Una recolección de controladores de alta calidad para impresoras Canon, Epson, Lexmark, Sony, Olympus; y para impresoras PCL para usar con GhostSscript, CUPS, Foomatic y [GIMP](/index.php/GIMP "GIMP")
*   [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db), [foomatic-db-engine](https://www.archlinux.org/packages/?name=foomatic-db-engine) y [foomatic-db-nonfree](https://www.archlinux.org/packages/?name=foomatic-db-nonfree) - Foomatic es un sistema orientado a base de datos para integrar controladores de impresión de software libre con colas de impresión comunes en entornos Unix.
*   [hplip](https://www.archlinux.org/packages/?name=hplip) - Controladores HP para DeskJet, OfficeJet, Photosmart, Business Inkjet y algunos modelos de impresoras LaserJet, así como útil para algunas impresoras Brother.
*   [splix](https://www.archlinux.org/packages/?name=splix) - Controlador de Samsung para impresoras SPL (Samsung Printer Language).
*   [foo2zjs](https://aur.archlinux.org/packages/foo2zjs/) - Controladores para el protocolo ZjStream usados por impresoras como HP Laserjet 1018\. Más información [aquí](http://foo2zjs.rkkda.com). El paquete está disponible en [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)").
*   [hpoj](https://aur.archlinux.org/packages/hpoj/) - Si está utilizando una HP Officejet , también debe instalar este paquete y siga las instrucciones para evitar problemas como el indicado en [este hilo](https://answers.launchpad.net/hplip/+question/133425). El paquete está disponible en [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)").
*   [samsung-unified-driver](https://aur.archlinux.org/packages/samsung-unified-driver/) - Controlador de Linux unificado para impresoras y escáneres Samsung. Requerido por las impresoras nuevas tales como ML-2160\. El paquete está disponible en [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)").
*   [cndrvcups-lb](https://aur.archlinux.org/packages/cndrvcups-lb/) - Controlador UFR2 de Canon UFR2 con soporte para LBP, iR e impresoras de la serie MF. El paquete está disponible en [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)").
*   [cups-pdf](https://www.archlinux.org/packages/?name=cups-pdf) - Un paquete que permite configurar una impresora virtual PDF que genera un archivo PDF de los documentos enviados a ella.

Si no está seguro de qué controladores instalar o si el controlador actual que usa no está funcionando, puede ser más fácil instalar todos los controladores, dado que algunos de los nombres de los paquetes son engañosos, en cuanto que las impresoras de otras marcas pueden ser compatibles o depender de ellos. Por ejemplo, la impresora Brother HL-2140 necesita tener instalado el controlador hplip.

#### Descargar el PPD de la impresora

Dependiendo de la impresora, este paso es opcional y puede no ser necesario, ya que la instalación estándar de CUPS incluye un cierto número de archivos PPD (PostScript Printer Description). Por otra parte, los paquetes *foomatic-filters*, *gimp-print* y *hplip* ya incluyen un buen número de archivos PPD que serán automáticamente detectados por CUPS.

He aquí una explicación del sitio web de impresión de Linux sobre el significado del archivo PPD:

	«*Para todas las impresoras PostScript los fabricantes pueden proporcionar un archivo PPD que contiene toda la información específica del particular modelo de impresora: esto es, las capacidades básicas de la impresora, como, por ejemplo, si la impresora es a color, las fuentes, el nivel de PostScript, etc., y, sobre todo, la opciones configurables por el usuario, como el tamaño del papel, la resolución, etc.*»

Si el PPD para la impresora *no* está incluido en CUPS, entonces:

*   Compruebe en [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)") si hay paquetes para la impresora/fabricante
*   Visite la base de datos [OpenPrinting](http://www.openprinting.org/printers) y seleccione el fabricante y el modelo de la impresora
*   Visite el sitio del fabricante para realizar una búsqueda de los drivers GNU/Linux

**Nota:** Los archivos PPD residen en la carpeta `/usr/share/cups/model/`

#### Otros recursos para los controladores de la impresora

[Turboprint](http://www.turboprint.de/english.html) es un controlador propietario para muchas impresoras aún no soportadas por GNU/Linux (Canon i*, por ejemplo). A diferencia de CUPS, normalmente las impresiones de alta calidad son, o bien señaladas con una marca de agua, o bien son ofrecidas únicamente como un servicio de pago.

## Configuración y soporte técnico del hardware

### Impresoras USB

**Sugerencia:** La mayoría de impresoras USB deberían funcionar una vez instaladas, por tanto, puede saltarse esta sección y regresar si no puede conseguir que la impresora funcione.

Se puede tener acceso a las impresoras USB de dos modos: a través de los módulos del kernel `usblp` y `libusb`. El primero es el modo clásico y el más simple: los datos se envían a la impresora mediante una simple corriente de datos en serie. El mismo archivo tiene un acceso «bidireccional», a fin de permitir ver el nivel de tinta, el estado o la información de la capacidad de la impresora (PJL). Este método funciona muy bien para las impresoras simples, pero no es adecuado para los dispositivos multifunción (impresora/escáner), de ahí que fabricantes como HP proporcionen sus propios backends. (fuente: [aquí](http://lists.linuxfoundation.org/pipermail/printing-architecture/2012/002412.html))

#### Introducir en blacklisting el módulo usblp

**Advertencia:** Desde la versión 1.6.0 de [cups](https://www.archlinux.org/packages/?name=cups) no tendría que ser necesario introducir en [blacklist](/index.php/Kernel_modules_(Espa%C3%B1ol)#Blacklisting "Kernel modules (Español)") el módulo `usblp`. Si nota que al poner dicho módulo en blaklist soluciona algún problema, por favor informe del fallo a los desarrolladores en el «seguimiento de errores de CUPS» y, quizás, también puede ponerse en contacto con Till Kamppeter. Consulte [upstream bug](http://cups.org/str.php?L4128) para más información.

Algunos usuarios de impresoras USB, pueden, sin embargo, a modo de prevención, querer todavía introducir en blacklisting el [módulo de kernel](/index.php/Kernel_modules_(Espa%C3%B1ol) "Kernel modules (Español)") `usblp`, que se haría como sigue:

 `/etc/modprobe.d/blacklistusblp.conf` 
```
blacklist usblp

```

Los usuarios con un kernel personalizado pueden necesitar cargar manualmente el [módulo de kernel](/index.php/Kernel_modules_(Espa%C3%B1ol) "Kernel modules (Español)") `usbcore` antes de continuar.

Una vez que los módulos están instalados, conecte la impresora y compruebe si el kernel los ha detectado, ejecutando lo siguiente:

```
# tail /var/log/messages.log

```

o

```
# dmesg

```

Si está utilizando `usblp`, la salida debería indicar que la impresora ha sido detectada, de este modo:

```
Feb 19 20:17:11 kernel: printer.c: usblp0: USB Bidirectional
printer dev 2 if 0 alt 0 proto 2 vid 0x04E8 pid 0x300E
Feb 19 20:17:11 kernel: usb.c: usblp driver claimed interface cfef3920
Feb 19 20:17:11 kernel: printer.c: v0.13: USB Printer Device Class driver

```

Si se ha introducido en blacklisted el módulo `usblp`, debería obtener una salida similar a esta:

```
usb 3-2: new full speed USB device using uhci_hcd and address 3
usb 3-2: configuration #1 chosen from 1 choice

```

### Impresoras en puerto paralelo

Para la utilización de la impresora conectada a un puerto paralelo, necesita cargar los [módulos de kernel](/index.php/Kernel_modules_(Espa%C3%B1ol) "Kernel modules (Español)") `lp`, `parport` y `parport_pc`.

Una vez más, compruebe la configuración, ejecutando:

```
# tail /var/log/messages.log

```

Se debería ver algo como esto:

```
lp0: using parport0 (polling).

```

Si está utilizando un adaptador de USB para un puerto paralelo, CUPS no será capaz de detectar la impresora. Para solucionar este problema, agregue la impresora utilizando un tipo de conexión diferente y luego cambie DeviceID en `/etc/cups/printers.conf`, así:

```
DeviceID = parallel:/dev/usb/lp0

```

### Impresora HP

Las impresoras HP también se pueden instalar a través de la herramienta de configuración de Linux de HP. Intálela con el paquete [hplip](https://www.archlinux.org/packages/?name=hplip) desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

Para ejecutar con la interfaz qt:

```
# hp-setup -u

```

Para ejecutar en la línea de órdenes:

```
# hp-setup -i

```

Los archivos PPD están en `/usr/share/ppd/HP/`.

**Nota:** Si obtiene un error de sintaxis durante la instalación, puede volver a vincular *temporalmente* la orden `python` a la orden `python2` (regrese a la orden `python3` después de configurar).

Si obtiene errores respecto a dependencias que faltan de gobject/dbus, instale [python2-gobject2](https://www.archlinux.org/packages/?name=python2-gobject2) y [python2-dbus](https://www.archlinux.org/packages/?name=python2-dbus). Para obtener más detalles véase este [informe de error](https://bugs.archlinux.org/task/26666).

Para las impresoras que requieren el plugin propietario de HP ((como la impresora Laserjet Pro P1102w), instale el paquete [hplip-plugin](https://aur.archlinux.org/packages/hplip-plugin/) desde [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)").

**Nota:** [hplip](https://www.archlinux.org/packages/?name=hplip) depende de [foomatic-db-engine](https://www.archlinux.org/packages/?name=foomatic-db-engine) que impide mostrar la lista de controladores que debería aparecer al agregar una impresora a CUPS a través de la interfaz web del usuario (muestra el error siguiente: «Unable to get list of printer drivers»). La solución consiste en instalar [hplip](https://www.archlinux.org/packages/?name=hplip) primero, recuperar el archivo PPD correspondiente desde `/usr/share/ppd/HP/`, y, a continuación, eliminar [hplip](https://www.archlinux.org/packages/?name=hplip) completamente y las dependencias innecesarias. Por último , instale la impresora manualmente utilizando la interfaz web de CUPS, seleccione el archivo PPD recuperado y reinstale [hplip](https://www.archlinux.org/packages/?name=hplip). Después de reiniciar el sistema, debería tener una impresora totalmente funcional .

## Configuración

Ahora que CUPS está instalado, tenomos una variedad de opciones sobre cómo configurar soluciones de impresión. Como siempre, el conocido método de la línea de órdenes está a su disposición. Del mismo modo, varios entornos de escritorio, como GNOME y KDE, tienen programas útiles que pueden ayudar a gestionar las impresoras. Sin embargo, para que esta explicación llegue al mayor número posible de usuarios, este artículo se centrará en el método que usa la interfaz web proporcionada por CUPS.

Si está planificando una conexión a una impresora en red, en lugar de una conectada directamente al ordenador, es posible que desee leer primero la página sobre el [uso compartido de impresoras CUPS](/index.php/CUPS_printer_sharing "CUPS printer sharing"). El uso compartido de impresoras entre sistemas GNU/Linux es muy fácil y consiste en una configuración muy sencilla, mientras que compartir impresoras entre sistemas Windows y GNU/Linux requiere un esfuerzo un poco mayor.

### El demonio CUPS

Con el módulo del kernel instalado, ahora puede iniciar **cups** y, opcionalmente, el [demonio](/index.php/Daemons_(Espa%C3%B1ol) "Daemons (Español)") **cups-browsed**. Tenga en cuenta que a partir de **cups v. 2.0.0** el nombre del demonio ha cambiado de **cups** a **org.cups.cupsd**. Si tiene activado el viejo servicio primero deberá desactivarlo:

```
# systemctl disable cups.service

```

Y activar el nuevo en su lugar:

```
# systemctl enable org.cups.cupsd.service
# systemctl daemon-reload
# systemctl start org.cups.cupsd.service

```

### Interfaz web y herramientas

Una vez iniciado el demonio, abra un navegador y escriba en la barra de navegación: [http://localhost:631](http://localhost:631) (*El término **localhost** puede que tengamos que reemplazarlo con el nombre del equipo establecido en* `/etc/hosts`).

Desde aquí, siga los distintos asistentes que le vayan apareciendo en pantalla para agregar la impresora. Un procedimiento habitual es empezar haciendo clic en *Añadir impresoras y clases* y después en *Añadir Impresora*. Cuando se le pida un nombre de usuario y contraseña, inicie la sesión como root. El nombre asignado a la impresora no tiene importancia, lo mismo que para los campos 'ubicación' y 'descripción'. A continuación, se presentará una lista de dispositivos para seleccionar. El nombre real de la impresora aparece junto a la etiqueta (por ejemplo, al lado de *USB Printer #1* para impresoras USB). Por último, seleccione los controladores adecuados, para completar la configuración.

Ahora pruebe la configuración pulsando *Administración*, en el menú desplegable, y seleccione *Imprimir página de prueba*. Si no se imprime y la configuración es correcta, entonces lo más probable sea que el controlador seleccionado no es el adecuado para la impresora.

**Sugerencia:** Véase: [Interfaces alternativas para CUPS](#Interfaz_CUPS_alternativas) para conocer otros tipos de interfaces.

**Nota:**

*   Cuando se configura una impresora USB, esta debe aparecer listada en la página *Agregar Impresora*. Si solo se puede ver una «impresora SCSI», probablemente significa que CUPS no ha reconocido la impresora.
*   Para habilitar el escaneo de redes inalámbricas en determinados dispositivos multifunción HP, utilizando el paquete [hplip](https://www.archlinux.org/packages/?name=hplip), puede que tenga que agregar la impresora como una impresora de red, utilizando http:// protocol. Para determinar el URI correcto a usar, ejecute la orden `hp-makeuri`.

#### Administración de CUPS

Para administrar la impresora mediante la interfaz web es necesario proporcionar un nombre de usuario y una contraseña, para realizar tareas como, por ejemplo: añadir o eliminar impresoras, detención de tareas de impresión, etc. El nombre de usuario, por defecto es el asignado al grupo *sys* , o root (para cambiar el grupo modifique `/etc/cups/cupsd.conf` en la línea *SystemGroup*).

Si la cuenta de root se ha bloqueado (es decir, cuando se utiliza sudo), no será posible iniciar una sesión en la interfaz de administración de CUPS con el nombre de usuario y contraseña por defecto. En este caso, siga [estas instrucciones](http://www.cups.org/articles.php?L237+T+Qprintadmin) en el FAQ de CUPS. También puede resultarle interesante [este post](https://bbs.archlinux.org/viewtopic.php?id=35567).

#### Acceso remoto a la interfaz web

Por defecto, la interfaz web de CUPS es accesible solo por *localhost*, es decir, el equipo sobre el que está instalado. Para acceder a la interfaz remota, será necesario realizar los siguientes cambios, modificando el archivo `/etc/cups/cupsd.conf`. Cambien la línea:

```
Listen localhost:631

```

con

```
Port 631

```

para que CUPS escuche las solicitudes entrantes.

Tres niveles de acceso se pueden conceder:

```
<Location />           #acceso al servidor
<Location /admin>	#acceso a las páginas de administración
<Location /admin/conf>	#acceso a los archivos de configuración

```

Para conceder a los hosts remotos acceso a uno de estos niveles, añada una declaración afirmativa, `Allow`, a la sección de dicho nivel. Una declaración `Allow` puede formularse de diversas maneras como se enumeran a continuación:

```
Allow all
Allow host.domain.com
Allow *.domain.com
Allow ip-address
Allow ip-address/netmask

```

La declaración negativa, `Deny`, también puede ser utilizada. Por ejemplo, si quiere dar acceso completo a todos los host de la subred 192.168.1.0/255.255.255.0, incluya en el archivo `/etc/cups/cupsd.conf` lo siguiente:

```
# Restrict access to the server...
# By default only localhost connections are possible
<Location />
   Order allow,deny
   Allow From localhost
   **Allow From 192.168.1.0/255.255.255.0**
</Location>

# Restrict access to the admin pages...
<Location /admin>
   # Encryption disabled by default
   #Encryption Required
   Order allow,deny
   Allow From localhost
   **Allow From 192.168.1.0/255.255.255.0**
</Location>

# Restrict access to configuration files...
<Location /admin/conf>
   AuthType Basic
   Require user @SYSTEM
   Order allow,deny
   Allow From localhost
   **Allow From 192.168.1.0/255.255.255.0**
</Location>

```

Puede también ser necesario añadir:

```
DefaultEncryption Never

```

Esto debería evitar el error: 426 - Es necesaria la actualización cuando se utiliza la interfaz web de CUPS desde una máquina remota.

### Configuración a través de línea de órdenes

CUPS puede ser totalmente controlado desde la línea de órdenes con herramientas sencillas, *es decir* el conjunto de órdenes de lp* y cups*.

En Arch Linux, la mayoría de las órdenes vienen con apoyo de aut-completado en las consolas comunes. Tenga en cuenta igualemente que las órdenes no se pueden agrupar en una sola línea.

	Lista los dispositivos

```
# lpinfo -v

```

	Lista los controladores

```
# lpinfo -m

```

	Añade una nueva impresora

```
# lpadmin -p <printer> -E -v <device> -P <ppd>

```

El nombre de la impresora (<printer>) es de su elección. El dispositivo (<device>) se puede obtener de la orden 'lpinfo -i'. He aquí un ejemplo:

```
# lpadmin -p HP_DESKJET_940C -E -v "usb://HP/DESKJET%20940C?serial=CN16E6C364BH"  -P /usr/share/ppd/HP/hp-deskjet_940c.ppd.gz

```

En los ejemplos siguientes, la referencia a <printer> es el nombre que se ha utilizado para configurar la impresora.

	Establecer la impresora predeterminada

```
$ lpoptions -d <printer>

```

	Comprobar el estado

```
$ lpstat -s
$ lpstat -p <printer>

```

	Desactivar una impresora

```
# cupsdisable <printer>

```

	Activar una impresora

```
# cupsenable <printer>

```

	Eliminar una impresora

Primero, configúrela para rechazar todas las entradas que lleguen:

```
# cupsreject <printer>

```

A continuación, desactívela.

```
# cupsdisable <printer>

```

Por último, elimínela.

```
# lpadmin -x <printer>

```

	Imprimir un archivo

```
$ lpr <archivo>
$ lpr -# 17 <archivo>              # imprime el archivo 17 veces
$ echo "Hello, world!" | lpr -p    # imprime el resultado de la orden. El parámetro -p añade un encabezado.

```

	Comprobar la cola de impresión

```
$ lpq
$ lpq -a # en todas las impresoras

```

	Limpiar la cola de impresión

```
# lprm   # elimina únicamente la última entrada
# lprm - # elimina todas las entradas

```

### Interfaz CUPS alternativas

#### GNOME

Si usa [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)"), tiene la posibilidad de gestionar y configurar la impresora [instalando](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") [system-config-printer](https://www.archlinux.org/packages/?name=system-config-printer).

Para hacer system-config-printer realmente funcional, será necesario ejecutarlo como root, o, alternativamente, establecer permisos a un usuario «normal» para administrar CUPS (en este último caso **siga los pasos 1-3**):

1\. Cree un grupo para administrar el programador cups:

```
# groupadd lpadmin

```

2\. Agregue su usuario al grupo recién creado:

```
# usermod -aG lpadmin *username*

```

3\. Informe a cups para que acepte el grupo recién creado

 `/etc/cups/cups-files.conf` 
```
 ...
 SystemGroup sys root **lpadmin**
 ...
```

4\. Reinicie cups:

```
# systemctl restart cupsd

```

5\. Reinicie la sesión de usuario (o reinicie el ordenador).

#### KDE

Los usuarios de [KDE](/index.php/KDE "KDE") pueden gestionar las impresoras desde el Centro de Control. Los usuarios de estos entornos de escritorios (Gnome, KDE), deben remitirse a la documentación de sus respectivos escritorios «para más información sobre cómo utilizar las interfaces».

#### Otro

Otra interfaz útil es [gtklp](https://aur.archlinux.org/packages/gtklp/) disponible desde [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)")

## Impresora virtual PDF

[cups-pdf](https://www.archlinux.org/packages/?name=cups-pdf) es un paquete interesante, que permite configurar una impresora virtual que va a generar un archivo PDF a partir de cualquier documento que se ​​le envíe. Obviamente, este paquete no es necesario, pero puede ser bastante útil.

Después de instalar el paquete, debe configurarse como si se tratara de cualquier otra impresora mediante la interfaz web. Acceda a la administración de la impresora cups: [http://localhost:631](http://localhost:631) y seleccione:

```
Administración -> Añadir Impresora
Seleccionar CUPS-PDF (Virtual PDF), elegir marca y driver:
Marca:   Generic
Driver:  Generic CUPS-PDF Printer

```

Los documentos PDF generados se encuentran en un subdirectorio ubicado en `/var/spool/cups-pdf`. Normalmente, el subdirectorio lleva el nombre del usuario que realizó el trabajo. Un pequeño arreglo le ayudará a ubicar (y, por tanto, encontrar con más facilidad) sus documentos PDF impresos en el directorio que desee. Edite `/etc/cups/cups-pdf.conf`, descomente la siguiente línea:

```
#Out /var/spool/cups-pdf/${USER}

```

y modifíquela poniendo la ruta a la carpeta donde desee que tengan su salida los documentos imprimidos por CUPS-PDF, por ejemplo:

```
Out ${HOME}

```

### Imprimir en postscript

El CUPS-PDF (Virtual PDF Printer) en realidad crea un archivo PostScript y después crea el PDF con la utilidad ps2pdf. Para imprimir en PostScript, imprima como de costumbre, en el diálogo de impresión seleccione «CUPS-PDF» como impresora, luego seleccione la casilla de verificación «imprimir en archivo», pinche en Imprimir, introduzca el nombre del archivo (extensión .ps) y haga clic en guardar. Esto es útil para faxes, etc.

## Solución de Problemas

La mejor manera de conocer cómo funciona la impresora es establecer 'LogLevel' en `/etc/cups/cupsd.conf`, de este modo:

```
LogLevel debug

```

Y luego, analizando la salida desde `/var/log/cups/error_log`, como sigue:

```
# tail -n 100 -f /var/log/cups/error_log

```

Los resultados a la izquierda de la salida son:

*   D=Debug
*   E=Error
*   I=Información
*   Y así...

Estos archivos también pueden ser útiles para:

*   `/var/log/cups/page_log` - Reproduce una nueva entrada cada vez que la impresión es satisfactoria
*   `/var/log/cups/access_log` - Lista todas las actividades del servidor cupsd http1.1

Por supuesto, es importante saber cómo funciona CUPS para poder hacer frente a eventuales problemas:

1.  Una aplicación envía un archivo .ps (PostScript, un lenguaje de script que detalla cómo debe verse la página) a CUPS cuando la opción 'imprimir' ha sido seleccionada (esto viene con la mayoría de los programas).
2.  CUPS después analiza el archivo PPD de la impresora (archivo de descripción de impresora) y encuentra los filtros que debe utilizar para convertir el archivo .ps a un lenguaje que entienda la impresora (como PJL, PCL), usualmente GhostScript.
3.  GhostScript recibe la entrada y decide qué filtros debe utilizar, a continuación, los aplica y convierte el archivo .ps a un formato entendible por la impresora.
4.  Por último, envía un back-end. Por ejemplo, si la impresora está conectada a un puerto USB, utiliza el back-end USB.

Imprima un documento y vea `error_log` para obtener una imagen más detallada y correcta del proceso de impresión.

### Problemas relacionados con las actualizaciones

*Problemas que aparecieron despues que los paquetes CUPS y programas relacionados fueron actualizados a una versión más reciente.*

#### CUPS deja de funcionar

Puede suceder que, como resultado de una actualización hay cambios en el archivo de configuración. Mensajes como "404 - page not found" (*«404 - página no encontrada»*) puede ser consecuencia de tratar de administrar CUPS a través de localhost:631, por ejemplo.

Para utilizar la nueva configuración, copie `/etc/cups/cupsd.conf.default` a `/etc/cups/cupsd.conf` (respalde la configuración antigua si es necesario) y reinicie CUPS para emplear la nueva configuración.

#### Todos los trabajos están «detenidos»

Si todos los trabajos enviados a la impresora se «detuvieron», elimine la impresora y vuelva a agregarla. Usando la [interfaz web de CUPS](http://localhost:631), vaya a Impresoras > Eliminar impresora.

Para comprobar la configuración de la impresora vaya a *Impresoras*, luego *Modificar Impresora*. Copie la información mostrada, seleccione 'Modificar Impresora' para pasar a la página siguiente(s), y así sucesivamente.

#### Todos los trabajos derivan a «The printer is not responding» (La impresora no responde)

En las impresoras en red, compruebe que el nombre que CUPS utiliza como su URI de conexión tiene la IP de la impresora a través del DNS, por ejemplo, si la conexión de la impresora es la siguiente:

```
lpd://BRN_020554/BINARY_P1

```

entonces el nombre del equipo 'BRN_020554' es el que se necesita para resolver la IP de la impresora desde el servidor donde se ejecuta CUPS.

#### La versión PPD no es compatible con gutenprint

Ejecute:

```
# /usr/sbin/cups-genppdupdate

```

Y reinicie CUPS (como señala el mensaje post-instalación de gutenprint)

### Otros

##### Errores de permisos CUPS

*   Algunos usuarios reportan errores del tipo 'NT_STATUS_ACCESS_DENIED' (Windows clients) utilizando una sintaxis ligeramente diferente:

```
smb://workgroup/username:password@hostname/printer_name

```

*   A veces, el dispositivo completo tiene permisos incorrectos:

```
# ls /dev/usb/
lp0
# chgrp lp /dev/usb/lp0

```

#### La impresora HPLIP envía como error «/usr/lib/cups/backend/hp failed»

Asegúrese de tener instalado dbus y de haberlo iniciado. Si el error persiste, pruebe iniciando avahi-daemon.

Trate de añadir la impresora como una impresora de red utilizando el protocolo http:// protocol. Genere el URI de la impresora con `hp-makeuri`.

**Nota:** Existe la posibilidad de que sea necesario cambiar los permisos. Siga las indicaciones de [CUPS#Device node permissions](/index.php/CUPS#Device_node_permissions "CUPS").

#### HPLIP indica que todos los trabajos se han completado pero la impresora no responde

Esto sucede en las impresoras HP cuando se selecciona el controlador (antiguo) hpijs (por ejemplo, la Deskjet series D1600). En su lugar, seleccione el controlador hpcups al añadir la impresora.

Algunas impresoras hp (por ejemplo hp Laserjet) requieren firmware para ser descargado desde el ordenador cada vez que se enciende la impresora. Si hay un problema con udev (o equivalente) y el estado de descarga de firmware nunca es encendido, puede experimentar este problema. Para solucionar el problema, puede descargar manualmente el firmware a la impresora. Asegúrese de que la impresora esté conectada y encendida, y, a continuación, introduzca

```
hp-firmware -n

```

#### hp-setup solicita que especifique el archivo PPD para la impresora descubierta

Instale CUPS antes de ejecutar hp-setup.

#### Qt instalado, pero hp-setup informa: "Qt/PyQt 4 initialization failed" (*«no se puede iniciar Qt/PyQt 4»*)

«hp-check -t» no le dará información útil para encontrar el paquete necesario. Hay que instalar todos los «paquetes dependientes» que contengan el prefijo «python2» en [hplip](https://www.archlinux.org/packages/?name=hplip)

#### hp-setup encuentra la impresora automáticamente, pero informa que "Unable to communicate with device" (*«No se puede comunicar con el dispositivo»*) inmediatamente después de imprimir la página de prueba

Esto, al menos, pasa con hplip 3.13.5-2 para HP Officejet 6500A través de la conexión de red local. Para resolver el problema, especifique la dirección IP de la impresora HP a hp-setup para que pueda localizarla.

#### hp-toolbox envía como error, «Unable to communicate with device» («No se puede comunicar con el dispositivo»)

Si se ejecuta hp-toolbox como un usuario normal se obtiene:

```
# hp-toolbox
# error: Unable to communicate with device (code=12): hp:/usb/<printer id>

```

o, «`Unable to communicate with device`», entonces puede ser necesario [añadir al usuario al grupo lp y sys](/index.php/Users_and_groups_(Espa%C3%B1ol)#Gesti.C3.B3n_de_grupos "Users and groups (Español)").

Esto también puede ser causado por las impresoras P1102 que proporiconan una unidad CD-ROM virtual con el controlador para MS-Windows. El dispositivo lp aparece y luego desaparece. En ese caso, pruebe los paquetes **usb-modeswitch** y **usb-modeswitch-data**, que permiten intercambiar la «Smart Drive» (reglas de udev incluidas en dichos paquetes).

Esto también puede ocurrir con las impresoras conectadas en red, si el demonio [avahi-daemon](/index.php/Avahi "Avahi") no se está ejecutando.

#### CUPS responde '«foomatic-rip» not available/stopped with status 3' con una impresora HP

Si recibe alguno de los siguientes mensajes de error en `/var/log/cups/error_log` mientras se utiliza una impresora HP, con trabajos que se muestran para ser procesados ​​mientras que el resto de trabajos ya procesados no los completa y su estado se establece en 'parado':

```
 Filter "foomatic-rip" for printer "<nombre_impresora>" not available: No such file or director

```

o:

```
PID 5771 (/usr/lib/cups/filter/foomatic-rip) stopped with status 3!

```

asegúrese que [hplip](https://www.archlinux.org/packages/?name=hplip) se ha instalado, además de [los paquetes mencionados arriba](#Instalaci.C3.B3n). Consulte [este mensaje en el foro](https://bbs.archlinux.org/viewtopic.php?id=65615).

```
# pacman -S hplip

```

#### La impresora falla indicando error de autorización

Si el usuario se ha añadido al grupo lp, y está autorizado para imprimir (establecido en `cupsd.conf`), entonces el problema se encuentra en `/etc/cups/printers.conf`. Esta línea podría ser la culpable:

```
AuthInfoRequired negotiate

```

Comentela y reinicie CUPS.

#### Botón de impresora bloqueado en aplicaciones GNOME

	*<small>Fuente (en inglés): [No es posible imprimir con las aplicaciones GNOME. - Arch Forums](https://bbs.archlinux.org/viewtopic.php?id=70418)</small>*

Asegúrese de que el paquete: **libgnomeprint** está instalado.

Edite el archivo `/etc/cups/cupsd.conf` y añada:

```
# HostNameLookups Double

```

Reinicie org.cups.cupsd.service.

#### Formato soportado desconocido: application/postscript

Comente las líneas:

```
application/octet-stream        application/vnd.cups-raw        0      -

```

en el archivo `/etc/cups/mime.convs`, y:

```
application/octet-stream

```

en `/etc/cups/mime.types`.

#### Cambiar los URI para los servidores de la impresora de Windows

A veces, Windows es poco intuitivo en la definición exacta del dispositivo URI (ubicación del dispositivo). Si tiene problemas para especificar la ubicación del dispositivo correcto en CUPS, ejecute la orden siguiente para listar todas las acciones disponibles para un determinado nombre de usuario de Windows:

```
 $ smbtree -U *windowsusername*

```

Esta orden enumerará cada recurso compartido disponible para un determinado nombre de usuario de Windows en la subred LAN local, siempre que Samba esté configurado y funcionando correctamente. Debe devolver algo como esto:

```
 WORKGROUP
	\\REGULATOR-PC   		
		\\REGULATOR-PC\Z              	
		\\REGULATOR-PC\Public         	
		\\REGULATOR-PC\print$         	Printer Drivers
		\\REGULATOR-PC\G              	
		\\REGULATOR-PC\EPSON Stylus CX8400 Series	EPSON Stylus CX8400 Series
```

Lo que se necesita de este ejemplo es la primera parte de la última línea, el recurso que coincide con la descripción de la impresora. Así que para imprimir en la impresora EPSON Stylus, se podría insertar como URI:

```
 smb://username.password@REGULATOR-PC/EPSON Stylus CX8400 Series

```

en CUPS. Advierta que los espacios en blanco son permitidos en URIs, mientras se reemplazan las barras invertidas con barras diagonales. Si esto no funciona, pruebe con '% 20' en lugar de espacios.

#### Error de impresora client-error-document-format-not-supported

Pruebe instalando los paquetes foomatic y usar un controlador foomatic.

#### Error /usr/lib/cups/backend/hp

Cambie

```
 SystemGroup sys root

```

por

```
 SystemGroup lp root

```

en `/etc/cups/cupsd.conf`

Los siguientes pasos 1-3 en las interfaces Alternativas de CUPS que figuran a continuación puede ser una mejor solución, ya que hay nuevas versiones de cups que no permitirán que el mismo grupo realice conjuntamente operaciones normales y de admninistración.

#### «Unable to get list of printer drivers»

*   Compruebe su ServerName en /etc/cups/client.conf que esté escrito sin http://

```
ServerName localhost:631

```

*   Pruebe eliminando los drivers Foomatic.

#### lp: Error - Scheduler Not Responding

Si recibe este error al imprimir un documento mediante:

```
$ lp document-to-print

```

Pruebe a establecer la variable de entorno CUPS_SERVER:

```
$ export CUPS_SERVER=localhost

```

Si esto resuelve el problema, haga la solución permanente añadiendo la línea export de arriba en ~/.bash_profile.

#### CUPS imprime solo un vacío y una página de mensajes de error en HP LaserJet

Hay un bug que hace que CUPS falle al imprimir imágenes en impresoras HP LaserJet (como es el caso de 3380). El error ha sido reportado y se repara por [Ubuntu](https://bugs.launchpad.net/ubuntu/+source/cups-filters/+bug/998087). La primera página está vacía, la segunda página contiene el siguiente mensaje de error:

```
 ERROR:
 invalidaccess
 OFFENDING COMMAND:
 filter
 STACK:
 /SubFileDecode
 endstream
 ...

```

Con el fin de solucionar el problema, utilice la siguiente orden (como superusuario):

```
 lpadmin -p <printer> -o pdftops-renderer-default=pdftops

```

#### Mensaje de error «Using invalid Host»

Pruebe añadiendo "ServerAlias *" en cupsd.conf

#### La impresora no funciona o devuelve como error «Filter failed» en la interfaz web de CUPS (HP printer)

Cambie los permisos del puerto USB de la impresora:

Busque los números del dispositivo y de bus con la orden lsusb, y, a continuación, establezca los permisos oportunos ejecutando:

```
# chmod 0666 /dev/bus/usb/<número del bus>/<número del dispositivo>

```

Para hacer el cambio de permisos permanentes que se activen automáticamente cada vez que se reinicia el equipo, agregue la siguiente línea.

 `/etc/udev/rules.d/10-local.rules`  `SUBSYSTEM=="usb", ATTRS{idVendor}=="Printer_idVendor", ATTRS{idProduct}=="Printer_idProduct", GROUP="lp", MODE:="666"` 

Obtenga la información correcta mediante el uso de la orden `lsusb`, y sustituya los parámetros `Printer_idVendor` & `Printer_idProduct` con los apropiados.

```
Bus 002 Device 002: ID xxxx:yyyy Hewlett-Packard DeskJet D1360

```

xxxx es el Printer_idVendor; yyyy es el Printer_idProduct

Cada sistema puede variar, por lo tanto consulte la página de la wiki sobre el [listado de atributos de los dispositivos](/index.php/Udev_(Espa%C3%B1ol)#Listar_los_atributos_de_un_dispositivo "Udev (Español)").

#### La impresora no imprime con un mensaje de "Filter failed" en la interfaz web de CUPS (impresora HP conectada por red)

Iniciar, activar y reiniciar el demonio avahi.

#### HPLIP 3.13: el plugin está instalado, pero el administrador de dispositivos de HP se queja de que no es así

La cuestión tiene que ver con el cambio de permisos del archivo realizado en `/var/lib/hp/hplip.state`. Para corregir el problema, una simple modificación con `chmod 644 /var/lib/hp/hplip.state` y `chmod 755 /var/lib/hp` debería bastar. Para más información, lea este [enlace](https://bugs.launchpad.net/hplip/+bug/1131596).

#### La impresora no es reconocida por CUPS

Si la impresora no aparece listada en la página «Añadir impresoras» de la interfaz web de CUPS, ni por la orden lpinfo -v, pruebe lo siguiente (sugerido en [este hilo](https://bbs.archlinux.org/viewtopic.php?pid=1037279#p1037279)):

*   Elimine `usblp` de la lista negra (blacklist).
*   Cargue el módulo `usblp`:

```
modprobe usblp

```

*   Detenga cups.
*   Añada la siguiente regla udev en un nuevo archivo de regla udev:

 `/etc/udev/rules.d/10-cups_device_link.rules`  `KERNEL=="lp[0-9]", SYMLINK+="%k", GROUP="lp"` 

*   Recarge las reglas udev:

```
# udevadm control --reload-rules

```

*   Desconcecte y vuelva a conectar la impresora.
*   Espere un poco y luego inicie de nuevo cups.

#### No se puede cargar /etc/samba/smb.conf

Si va a imprimir en una impresora remota a través de SMB y obtiene este mensaje de error: "Can't load /etc/samba/smb.conf - run testparm to debug it", entonces cree un archivo smb.conf vacío:

```
# mkdir /etc/samba
# touch /etc/samba/smb.conf

```

y reinicie cupsd.

#### El servicio systemd de CUPS no se inicia aunque está activado

El archivo .service de systemd proporcionado por CUPS utiliza socket, es decir, el servicio solo se inicia cuando un aplicación se conecta al socket de CUPS. Sin embargo, el archivo .socket de systemd proporcionado por cups solo funciona para el socket local `/run/cups/cups.sock`.

A fin de comenzar cupsd cuando se inicia un trabajo de impresora a través de la red, cree el siguiente archivo:

 `/etc/systemd/system/org.cups.cupsd.socket` 
```
.include /usr/lib/systemd/system/org.cups.cupsd.socket

[Socket]
ListenStream=0.0.0.0:631
ListenDatagram=0.0.0.0:631
BindIPv6Only=ipv6-only

```

A continuación, recargue systemd:

```
# systemctl --system daemon-reload

```

Confirme que todo está funcionando correctamente:

```
# systemctl is-enabled org.cups.cupsd.service || systemctl enable org.cups.cupsd.service
# systemctl status org.cups.cupsd.socket
org.cups.cupsd.socket - CUPS Printing Service Sockets
         Loaded: loaded (/etc/systemd/system/org.cups.cupsd.socket; enabled)
         Active: inactive (dead)
         Listen: /run/cups/cups.sock (Stream)
                 0.0.0.0:631 (Stream)
                 0.0.0.0:631 (Datagram)

```

Ahora CUPS debería comenzar automáticamente cuando se imprime localmente o en red.

## Véase también

*   [Official CUPS documentation](http://localhost:631/documentation.html), *locally installed*
*   [Official CUPS Website](http://www.cups.org/)
*   [Linux Printing](http://www.linuxprinting.org/), *[The Linux Foundation](http://www.linuxfoundation.org)*
*   [Gentoo's Printing Guide](http://www.gentoo.org/doc/en/printing-howto.xml), *[Gentoo Documentation Resources](http://www.gentoo.org/doc/en)*
*   [Arch Linux User Forums](https://bbs.archlinux.org/)
*   [Install HP Printers Easy Way](http://wiki.gotux.net/config/hp-printer)