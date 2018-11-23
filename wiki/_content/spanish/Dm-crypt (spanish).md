**<a class="mw-selflink selflink">dm-crypt (Español)</a>**

* * *

[Preparar dispositivo](/index.php/Dm-crypt/Drive_preparation_(Espa%C3%B1ol) "Dm-crypt/Drive preparation (Español)") – [Cifrar dispositivo](/index.php/Dm-crypt/Device_encryption_(Espa%C3%B1ol) "Dm-crypt/Device encryption (Español)") – [Cifrar sistema de archivos no root](/index.php/Dm-crypt/Encrypting_a_non-root_file_system_(Espa%C3%B1ol) "Dm-crypt/Encrypting a non-root file system (Español)") – [Cifrar un sistema completo](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol) "Dm-crypt/Encrypting an entire system (Español)") – [Cifrar espacio de intercambio](/index.php/Dm-crypt/Swap_encryption_(Espa%C3%B1ol) "Dm-crypt/Swap encryption (Español)") – [Montar y acceder a /home cifrado](/index.php/Dm-crypt/Mounting_at_login_(Espa%C3%B1ol) "Dm-crypt/Mounting at login (Español)") – [Configurar el sistema](/index.php/Dm-crypt/System_configuration_(Espa%C3%B1ol) "Dm-crypt/System configuration (Español)") – [Especialidades](/index.php/Dm-crypt/Specialties_(Espa%C3%B1ol) "Dm-crypt/Specialties (Español)")

**Estado de la traducción**
Este artículo es una traducción de [dm-crypt](/index.php/Dm-crypt "Dm-crypt"), revisada por última vez el **2018-11-22**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Dm-crypt&diff=0&oldid=543196) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Disk encryption (Español)](/index.php/Disk_encryption_(Espa%C3%B1ol) "Disk encryption (Español)")
*   [Removing System Encryption (Español)](/index.php/Removing_System_Encryption_(Espa%C3%B1ol) "Removing System Encryption (Español)")

dm-crypt es el [mapeador de dispositivos](https://en.wikipedia.org/wiki/device_mapper "wikipedia:device mapper") del kernel de Linux con el soporte crypto. De [Wikipedia:dm-crypt](https://en.wikipedia.org/wiki/dm-crypt "wikipedia:dm-crypt"), es:

	un subsistema de cifrado de discos que provee cifrado transparente de dispositivos de bloque en [el] kernel de Linux... [El mismo] es implementado como un soporte para mapear dispositivos y puede ser apilado sobre otras estructuras del mapeador de dispositivos. De este modo, puede cifrar discos completos (incluidos medios extraíbles), particiones, volúmenes RAID por software, volúmenes lógicos y archivos. Se muestra como un dispositivo de bloque, que se puede utilizar para respaldar sistemas de archivos, espacios de intercambio o como un volumen físico LVM.

## Contents

*   [1 Escenarios comunes](#Escenarios_comunes)
*   [2 Preparar la unidad](#Preparar_la_unidad)
*   [3 Cifrar un dispositivo](#Cifrar_un_dispositivo)
*   [4 Configurar el sistema](#Configurar_el_sistema)
*   [5 Cifrar el espacio de intercambio](#Cifrar_el_espacio_de_intercambio)
*   [6 Especialidades](#Especialidades)
*   [7 Véase también](#Véase_también)

## Escenarios comunes

Esta sección presenta los escenarios más comunes para emplear *dm-crypt* con el fin de cifrar un sistema o los puntos de montajes de sistemas de archivos individuales. Los escenarios descritos remiten a otras subpáginas para su desarrollo. Este documento se entiende, por tanto, como punto de partida para familiarizarse con las diferentes prácticas en los procedimientos de cifrado. Los escenarios se entrecruzan con las otras subpáginas cuando es necesario.

Consulte [Dm-crypt/Encrypting a non-root file system](/index.php/Dm-crypt/Encrypting_a_non-root_file_system "Dm-crypt/Encrypting a non-root file system") si desea cifrar un dispositivo que no se utiliza para arrancar un sistema, como puede ser una [partición](/index.php/Dm-crypt/Encrypting_a_non-root_file_system#Partition "Dm-crypt/Encrypting a non-root file system") o un [dispositivo loop](/index.php/Dm-crypt/Encrypting_a_non-root_file_system#Loop_device "Dm-crypt/Encrypting a non-root file system").

Consulte [Dm-crypt/Encrypting an entire system](/index.php/Dm-crypt/Encrypting_an_entire_system "Dm-crypt/Encrypting an entire system") si desea cifrar el sistema completo, en especial una partición raíz. En este caso hay varios escenarios posibles, incluyendo la utilización de *dm-crypt* con la extensión *LUKS*, la modalidad de cifrado *plain* y el cifrado más *LVM*.

## Preparar la unidad

[Dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation") se ocupará de operaciones tales como [borrar con seguridad un dispositivo](/index.php/Dm-crypt/Drive_preparation#Secure_erasure_of_the_hard_disk_drive "Dm-crypt/Drive preparation") y [particionarlo](/index.php/Dm-crypt/Drive_preparation#Partitioning "Dm-crypt/Drive preparation").

## Cifrar un dispositivo

[Dm-crypt/Device encryption](/index.php/Dm-crypt/Device_encryption "Dm-crypt/Device encryption") explicará cómo utilizar manualmente dm-crypt para cifrar un sistema con la orden [cryptsetup](/index.php/Dm-crypt/Device_encryption#Cryptsetup_usage "Dm-crypt/Device encryption"). Se presentan ejemplos de las [opciones de cifrado con dm-crypt](/index.php/Dm-crypt/Device_encryption#Encryption_options_with_dm-crypt "Dm-crypt/Device encryption"), acompañados con la creación de [archivo de claves](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption"), órdenes específicas de LUKS para la [gestión de claves](/index.php/Dm-crypt/Device_encryption#Key_management "Dm-crypt/Device encryption"), así como para la creación de [copias de respaldo y restauración](/index.php/Dm-crypt/Device_encryption#Backup_and_restore "Dm-crypt/Device encryption").

## Configurar el sistema

[Dm-crypt/System configuration](/index.php/Dm-crypt/System_configuration "Dm-crypt/System configuration") ilustrará sobre cómo configurar [mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration"), el [gestor de arranque](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") y el archivo [crypttab](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration") durante el cifrado del sistema.

## Cifrar el espacio de intercambio

[Dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption") versará sobre cómo añadir una partición de intercambio a un sistema cifrado, si se necesita. La partición de intercambio puede estar cifrada para proteger los datos de intercambio expuestos del sistema. Esta parte detalla métodos [con](/index.php/Dm-crypt/Swap_encryption#With_suspend-to-disk_support "Dm-crypt/Swap encryption") y [sin](/index.php/Dm-crypt/Swap_encryption#Without_suspend-to-disk_support "Dm-crypt/Swap encryption") soporte para suspender-en-disco.

## Especialidades

[Dm-crypt/Specialties](/index.php/Dm-crypt/Specialties "Dm-crypt/Specialties") tratará sobre operaciones especiales como [proteger la partición de arranque no cifrada](/index.php/Dm-crypt/Specialties#Securing_the_unencrypted_boot_partition "Dm-crypt/Specialties"), [utilizar archivos de claves cifrados con GPG o OpenSSL](/index.php/Dm-crypt/Specialties#Using_GPG,_LUKS,_or_OpenSSL_Encrypted_Keyfiles "Dm-crypt/Specialties"), un método para [arrancar y desbloquear a través de la red](/index.php/Dm-crypt/Specialties#Remote_unlocking_of_the_root_.28or_other.29_partition "Dm-crypt/Specialties"), otro para [configurar discard/TRIM para un disco SSD](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_drives_.28SSD.29 "Dm-crypt/Specialties") y secciones que se ocupan del [hook encrypt y múltiples discos](/index.php/Dm-crypt/Specialties#The_encrypt_hook_and_multiple_disks "Dm-crypt/Specialties").

## Véase también

*   [dm-crypt](https://gitlab.com/cryptsetup/cryptsetup/wikis/DMCrypt) - La página principal del proyecto.
*   [cryptsetup](https://gitlab.com/cryptsetup/cryptsetup) - La página principal de LUKS y [FAQ](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions) - el principal y más importante recurso de ayuda.
*   [Repositorio de cryptsetup](https://git.kernel.org/cgit/utils/cryptsetup/cryptsetup.git/) y el archivo [release](https://www.kernel.org/pub/linux/utils/cryptsetup/).
*   [DOXBOX](https://github.com/t-d-k/doxbox) - Admite el desbloqueo de volúmenes cifrados LUKS en Microsoft Windows.