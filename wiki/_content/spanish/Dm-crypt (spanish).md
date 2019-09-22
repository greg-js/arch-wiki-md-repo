**<a class="mw-selflink selflink">dm-crypt (Español)</a>**

* * *

[Preparar dispositivo](/index.php/Dm-crypt_(Espa%C3%B1ol)/Drive_preparation_(Espa%C3%B1ol) "Dm-crypt (Español)/Drive preparation (Español)") – [Cifrar dispositivo](/index.php/Dm-crypt_(Espa%C3%B1ol)/Device_encryption_(Espa%C3%B1ol) "Dm-crypt (Español)/Device encryption (Español)") – [Cifrar sistema de archivos no root](/index.php/Dm-crypt_(Espa%C3%B1ol)/Encrypting_a_non-root_file_system_(Espa%C3%B1ol) "Dm-crypt (Español)/Encrypting a non-root file system (Español)") – [Cifrar un sistema completo](/index.php/Dm-crypt_(Espa%C3%B1ol)/Encrypting_an_entire_system_(Espa%C3%B1ol) "Dm-crypt (Español)/Encrypting an entire system (Español)") – [Cifrar espacio de intercambio](/index.php/Dm-crypt_(Espa%C3%B1ol)/Swap_encryption_(Espa%C3%B1ol) "Dm-crypt (Español)/Swap encryption (Español)") – [Montar y acceder a /home cifrado](/index.php/Dm-crypt_(Espa%C3%B1ol)/Mounting_at_login_(Espa%C3%B1ol) "Dm-crypt (Español)/Mounting at login (Español)") – [Configurar el sistema](/index.php/Dm-crypt_(Espa%C3%B1ol)/System_configuration_(Espa%C3%B1ol) "Dm-crypt (Español)/System configuration (Español)") – [Especialidades](/index.php/Dm-crypt_(Espa%C3%B1ol)/Specialties_(Espa%C3%B1ol) "Dm-crypt (Español)/Specialties (Español)")

**Estado de la traducción**
Este artículo es una traducción de [dm-crypt](/index.php/Dm-crypt "Dm-crypt"), revisada por última vez el **2019-09-18**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Dm-crypt&diff=0&oldid=579171) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Disk encryption (Español)](/index.php/Disk_encryption_(Espa%C3%B1ol) "Disk encryption (Español)")
*   [Removing system encryption (Español)](/index.php/Removing_system_encryption_(Espa%C3%B1ol) "Removing system encryption (Español)")

dm-crypt es el [mapeador de dispositivos](https://en.wikipedia.org/wiki/device_mapper "wikipedia:device mapper") del kernel de Linux con el soporte crypto. De [Wikipedia:dm-crypt](https://en.wikipedia.org/wiki/dm-crypt "wikipedia:dm-crypt"), es:

	un subsistema de cifrado de discos que provee cifrado transparente de dispositivos de bloque en [el] kernel de Linux... [El mismo] es implementado como un soporte para mapear dispositivos y puede ser apilado sobre otras estructuras del mapeador de dispositivos. De este modo, puede cifrar discos completos (incluidos medios extraíbles), particiones, volúmenes RAID por software, volúmenes lógicos y archivos. Se muestra como un dispositivo de bloque, que se puede utilizar para respaldar sistemas de archivos, espacios de intercambio o como un volumen físico LVM.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Escenarios comunes](#Escenarios_comunes)
*   [2 Preparar la unidad](#Preparar_la_unidad)
*   [3 Cifrar un dispositivo](#Cifrar_un_dispositivo)
*   [4 Configurar el sistema](#Configurar_el_sistema)
*   [5 Cifrar el espacio de intercambio](#Cifrar_el_espacio_de_intercambio)
*   [6 Especialidades](#Especialidades)
*   [7 Véase también](#Véase_también)

## Escenarios comunes

Esta sección presenta los escenarios más comunes para emplear *dm-crypt* con el fin de cifrar un sistema o los puntos de montajes de sistemas de archivos individuales. Los escenarios descritos remiten a otras subpáginas para su desarrollo. Este documento se entiende, por tanto, como punto de partida para familiarizarse con las diferentes prácticas en los procedimientos de cifrado. Los escenarios se entrecruzan con las otras subpáginas cuando es necesario.

Consulte [Dm-crypt (Español)/Encrypting a non-root file system (Español)](/index.php/Dm-crypt_(Espa%C3%B1ol)/Encrypting_a_non-root_file_system_(Espa%C3%B1ol) "Dm-crypt (Español)/Encrypting a non-root file system (Español)") si desea cifrar un dispositivo que no se utiliza para arrancar un sistema, como puede ser una [partición](/index.php/Dm-crypt_(Espa%C3%B1ol)/Encrypting_a_non-root_file_system_(Espa%C3%B1ol)#Partición "Dm-crypt (Español)/Encrypting a non-root file system (Español)") o un [dispositivo loop](/index.php/Dm-crypt_(Espa%C3%B1ol)/Encrypting_a_non-root_file_system_(Espa%C3%B1ol)#Dispositivo_loop "Dm-crypt (Español)/Encrypting a non-root file system (Español)").

Consulte [Dm-crypt (Español)/Encrypting an entire system (Español)](/index.php/Dm-crypt_(Espa%C3%B1ol)/Encrypting_an_entire_system_(Espa%C3%B1ol) "Dm-crypt (Español)/Encrypting an entire system (Español)") si desea cifrar el sistema completo, en especial una partición raíz. En este caso hay varios escenarios posibles, incluyendo la utilización de *dm-crypt* con la extensión *LUKS*, la modalidad de cifrado *plain* y el cifrado más *LVM*.

## Preparar la unidad

[Dm-crypt (Español)/Drive preparation (Español)](/index.php/Dm-crypt_(Espa%C3%B1ol)/Drive_preparation_(Espa%C3%B1ol) "Dm-crypt (Español)/Drive preparation (Español)") se ocupará de operaciones tales como [borrar con seguridad un dispositivo](/index.php/Dm-crypt_(Espa%C3%B1ol)/Drive_preparation_(Espa%C3%B1ol)#Borrar_de_forma_segura_la_unidad_de_disco_duro "Dm-crypt (Español)/Drive preparation (Español)") y [particionarlo](/index.php/Dm-crypt_(Espa%C3%B1ol)/Drive_preparation_(Espa%C3%B1ol)#Particionar "Dm-crypt (Español)/Drive preparation (Español)").

## Cifrar un dispositivo

[Dm-crypt (Español)/Device encryption (Español)](/index.php/Dm-crypt_(Espa%C3%B1ol)/Device_encryption_(Espa%C3%B1ol) "Dm-crypt (Español)/Device encryption (Español)") explicará cómo utilizar manualmente dm-crypt para cifrar un sistema con la orden [cryptsetup](/index.php/Dm-crypt_(Espa%C3%B1ol)/Device_encryption_(Espa%C3%B1ol)#Utilización_de_cryptsetup "Dm-crypt (Español)/Device encryption (Español)"). Se presentan ejemplos de las [opciones de cifrado con dm-crypt](/index.php/Dm-crypt_(Espa%C3%B1ol)/Device_encryption_(Espa%C3%B1ol)#Opciones_de_cifrado_con_dm-crypt "Dm-crypt (Español)/Device encryption (Español)"), acompañados con la creación de [archivo de claves](/index.php/Dm-crypt_(Espa%C3%B1ol)/Device_encryption_(Espa%C3%B1ol)#Archivos_de_claves "Dm-crypt (Español)/Device encryption (Español)"), órdenes específicas de LUKS para la [gestión de claves](/index.php/Dm-crypt_(Espa%C3%B1ol)/Device_encryption_(Espa%C3%B1ol)#Gestión_de_claves "Dm-crypt (Español)/Device encryption (Español)"), así como para la creación de [copias de respaldo y restauración](/index.php/Dm-crypt_(Espa%C3%B1ol)/Device_encryption_(Espa%C3%B1ol)#Copia_de_seguridad_y_restauración "Dm-crypt (Español)/Device encryption (Español)").

## Configurar el sistema

[Dm-crypt/System configuration](/index.php/Dm-crypt/System_configuration "Dm-crypt/System configuration") ilustrará sobre cómo configurar [mkinitcpio](/index.php/Dm-crypt_(Espa%C3%B1ol)/System_configuration_(Espa%C3%B1ol)#mkinitcpio "Dm-crypt (Español)/System configuration (Español)"), el [gestor de arranque](/index.php/Dm-crypt_(Espa%C3%B1ol)/System_configuration_(Espa%C3%B1ol)#Cargador_de_arranque "Dm-crypt (Español)/System configuration (Español)") y el archivo [crypttab](/index.php/Dm-crypt_(Espa%C3%B1ol)/System_configuration_(Espa%C3%B1ol)#crypttab "Dm-crypt (Español)/System configuration (Español)") durante el cifrado del sistema.

## Cifrar el espacio de intercambio

[Dm-crypt (Español)/Swap encryption (Español)](/index.php/Dm-crypt_(Espa%C3%B1ol)/Swap_encryption_(Espa%C3%B1ol) "Dm-crypt (Español)/Swap encryption (Español)") versará sobre cómo añadir una partición de intercambio a un sistema cifrado, si se necesita. La partición de intercambio puede estar cifrada para proteger los datos de intercambio expuestos del sistema. Esta parte detalla métodos [con](/index.php/Dm-crypt_(Espa%C3%B1ol)/Swap_encryption_(Espa%C3%B1ol)#Con_soporte_para_suspensión_en_disco "Dm-crypt (Español)/Swap encryption (Español)") y [sin](/index.php/Dm-crypt_(Espa%C3%B1ol)/Swap_encryption_(Espa%C3%B1ol)#Sin_soporte_para_suspensión_en_disco "Dm-crypt (Español)/Swap encryption (Español)") soporte para suspender-en-disco.

## Especialidades

[Dm-crypt (Español)/Specialties (Español)](/index.php/Dm-crypt_(Espa%C3%B1ol)/Specialties_(Espa%C3%B1ol) "Dm-crypt (Español)/Specialties (Español)") tratará sobre operaciones especiales como [proteger la partición de arranque no cifrada](/index.php/Dm-crypt_(Espa%C3%B1ol)/Specialties_(Espa%C3%B1ol)#Asegurar_la_partición_de_arranque_no_cifrada "Dm-crypt (Español)/Specialties (Español)"), [utilizar archivos de claves cifrados con GPG o OpenSSL](/index.php/Dm-crypt_(Espa%C3%B1ol)/Specialties_(Espa%C3%B1ol)#Utilizar_archivos_de_claves_cifrados_con_GPG,_LUKS_o_OpenSSL "Dm-crypt (Español)/Specialties (Español)"), un método para [arrancar y desbloquear a través de la red](/index.php/Dm-crypt_(Espa%C3%B1ol)/Specialties_(Espa%C3%B1ol)#Desbloqueo_remoto_de_la_partición_(u_otro_volumen)_raíz "Dm-crypt (Español)/Specialties (Español)"), otro para [configurar discard/TRIM para un disco SSD](/index.php/Dm-crypt_(Espa%C3%B1ol)/Specialties_(Espa%C3%B1ol)#Soporte_Discard/TRIM_para_unidades_de_estado_sólido_(SSD) "Dm-crypt (Español)/Specialties (Español)") y secciones que se ocupan del [hook encrypt y múltiples discos](/index.php/Dm-crypt_(Espa%C3%B1ol)/Specialties_(Espa%C3%B1ol)#El_hook_encrypt_y_varios_discos "Dm-crypt (Español)/Specialties (Español)").

## Véase también

*   [dm-crypt](https://gitlab.com/cryptsetup/cryptsetup/wikis/DMCrypt) - La página principal del proyecto.
*   [cryptsetup](https://gitlab.com/cryptsetup/cryptsetup) - La página principal de LUKS y [FAQ](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions) - el principal y más importante recurso de ayuda.
*   [Repositorio de cryptsetup](https://git.kernel.org/cgit/utils/cryptsetup/cryptsetup.git/) y el archivo [release](https://www.kernel.org/pub/linux/utils/cryptsetup/).