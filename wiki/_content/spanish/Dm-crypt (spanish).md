Artículos relacionados

*   [Disk encryption (Español)](/index.php/Disk_encryption_(Espa%C3%B1ol) "Disk encryption (Español)")
*   [Removing System Encryption](/index.php/Removing_System_Encryption "Removing System Encryption")

<center>**Subpáginas de dm-crypt**</center>

<center>[Preparar la unidad](/index.php/Dm-crypt/Drive_preparation_(Espa%C3%B1ol) "Dm-crypt/Drive preparation (Español)") — [Cifrar un dispositivo](/index.php/Dm-crypt/Device_encryption "Dm-crypt/Device encryption") — [Cifrar el espacio de intercambio](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption") — [Cifrar un sistema de archivos no root](/index.php/Dm-crypt/Encrypting_a_non-root_file_system "Dm-crypt/Encrypting a non-root file system") — [Cifrar un sistema completo](/index.php/Dm-crypt/Encrypting_an_entire_system_(Espa%C3%B1ol) "Dm-crypt/Encrypting an entire system (Español)") — [Configurar el sistema](/index.php/Dm-crypt/System_configuration "Dm-crypt/System configuration") — [Especialidades](/index.php/Dm-crypt/Specialties "Dm-crypt/Specialties")</center>

* * *

**Estado de la traducción:** este artículo es una versión traducida de [dm-crypt](/index.php/Dm-crypt "Dm-crypt"). Fecha de la última traducción/revisión: **2015-06-25**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=Dm-crypt&diff=0&oldid=379508).

* * *

De la [wiki](https://gitlab.com/cryptsetup/cryptsetup/wikis/DMCrypt) del proyecto cryptsetup:

	Device-mapper es la infraestructura en el kernel de Linux 2.6 y 3.x que proporciona una forma genérica para crear capas virtuales de dispositivos de bloque. El objetivo de crypt de device-mapper proporciona cifrado transparente de los dispositivos de bloque utilizando la API de criptografía del kernel. El usuario puede especificar básicamente uno de los algoritmos de cifrado simétrico, una modalidad de cifrado, una clave (de cualquier tamaño permitido), una modalidad de generación del vector de inicialización y, luego, puede crear un nuevo dispositivo de bloque en /dev. Lo escrito en dicho dispositivo será cifrado y al leerlo será descifrado. Puede montar el sistema de archivos en el mismo como de costumbre o en un dispositivo dm-crypt apilado con otro dispositivo como RAID o volumen LVM. La documentación básica de la tabla de asignación de dm-crypt viene con las fuentes del kérnel y la última versión está disponible en el repositorio git.

## Contents

*   [1 Escenarios comunes](#Escenarios_comunes)
*   [2 Preparar la unidad](#Preparar_la_unidad)
*   [3 Cifrar un dispositivo](#Cifrar_un_dispositivo)
*   [4 Configurar el sistema](#Configurar_el_sistema)
*   [5 Cifrar el espacio de intercambio](#Cifrar_el_espacio_de_intercambio)
*   [6 Especialidades](#Especialidades)
*   [7 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Escenarios comunes

Esta sección presenta los escenarios más comunes para emplear *dm-crypt* con el fin de cifrar un sistema o los puntos de montajes de sistemas de archivos individuales. Los escenarios descritos remiten a otras subpáginas para su desarrollo. Este documento se entiende, por tanto, como punto de partida para familiarizarse con las diferentes prácticas en los procedimientos de cifrado.

Véase [Dm-crypt/Encrypting a non-root file system](/index.php/Dm-crypt/Encrypting_a_non-root_file_system "Dm-crypt/Encrypting a non-root file system") si desea cifrar un dispositivo que el sistema no lo utiliza para arrancar, como puede ser una [partición](/index.php/Dm-crypt/Encrypting_a_non-root_file_system#Partition "Dm-crypt/Encrypting a non-root file system") o un [dispositivo loop](/index.php/Dm-crypt/Encrypting_a_non-root_file_system#Loop_device "Dm-crypt/Encrypting a non-root file system").

Véase [Dm-crypt/Encrypting an entire system](/index.php/Dm-crypt/Encrypting_an_entire_system "Dm-crypt/Encrypting an entire system") si desea cifrar el sistema completo, en especial una partición raíz. En este caso hay varios escenarios posibles, incluyendo la utilización de *dm-crypt* con la extensión *LUKS*, la modalidad de cifrado *plain* y la encriptación más *LVM*.

## Preparar la unidad

Este paso se ocupará de las operaciones como [borrar con seguridad el dispositivo](/index.php/Dm-crypt/Drive_preparation#Secure_erasure_of_the_hard_disk_drive "Dm-crypt/Drive preparation") y [particionarlo](/index.php/Dm-crypt/Drive_preparation#Partitioning "Dm-crypt/Drive preparation").

Véase [Dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation").

## Cifrar un dispositivo

En esta sección se explicará cómo utilizar manualmente dm-crypt para cifrar un sistema con la orden [cryptsetup](/index.php/Dm-crypt/Device_encryption#Cryptsetup_usage "Dm-crypt/Device encryption"). Se presentan ejemplos de las [opciones de cifrado con dm-crypt](/index.php/Dm-crypt/Device_encryption#Encryption_options_with_dm-crypt "Dm-crypt/Device encryption"), acompañados con la creación de [archivo de claves](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption"), órdenes específicas de LUKS para la [gestión de claves](/index.php/Dm-crypt/Device_encryption#Key_management "Dm-crypt/Device encryption"), así como para la creación de [copias de respaldo y restauración](/index.php/Dm-crypt/Device_encryption#Backup_and_restore "Dm-crypt/Device encryption").

Véase [Dm-crypt/Device encryption](/index.php/Dm-crypt/Device_encryption "Dm-crypt/Device encryption").

## Configurar el sistema

Esta página mostrará cómo configurar [mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration"), el [gestor de arranque](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") y el archivo [crypttab](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration") durante el cifrado del sistema.

Véase [Dm-crypt/System configuration](/index.php/Dm-crypt/System_configuration "Dm-crypt/System configuration").

## Cifrar el espacio de intercambio

Es posible añadir una partición de intercambio a un sistema cifrado, si se necesita. La partición swap puede estar cifrada para proteger los datos de intercambio expuestos del sistema. Esta parte detalla métodos [sin](/index.php/Dm-crypt_with_LUKS/Swap_Encryption#Without_suspend-to-disk_support "Dm-crypt with LUKS/Swap Encryption") y [con](/index.php/Dm-crypt_with_LUKS/Swap_Encryption#With_suspend-to-disk_support "Dm-crypt with LUKS/Swap Encryption") soporte para suspender-en-disco.

Véase [Dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption").

## Especialidades

Esta parte tratará sobre operaciones especiales como [proteger la partición de arranque no cifrada](/index.php/Dm-crypt/Specialties#Securing_the_unencrypted_boot_partition "Dm-crypt/Specialties"), [utilizar archivos de claves cifrados con GPG o OpenSSL](/index.php/Dm-crypt/Specialties#Using_GPG_or_OpenSSL_Encrypted_Keyfiles "Dm-crypt/Specialties"), un método para [arrancar y desbloquear a través de la red](/index.php/Dm-crypt/Specialties#Remote_unlocking_of_the_root_.28or_other.29_partition "Dm-crypt/Specialties"), otro para [configurar discard/TRIM para un disco SSD](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_drives_.28SSD.29 "Dm-crypt/Specialties") y secciones que se ocupan del [hook encrypt y múltiples discos](/index.php/Dm-crypt/Specialties#The_encrypt_hook_and_multiple_disks "Dm-crypt/Specialties").

Véase [Dm-crypt/Specialties](/index.php/Dm-crypt/Specialties "Dm-crypt/Specialties").

## Véase también

*   [dm-crypt](https://code.google.com/p/cryptsetup/wiki/DMCrypt) - The project homepage
*   [cryptsetup](http://code.google.com/p/cryptsetup/) - The LUKS homepage and [FAQ](https://code.google.com/p/cryptsetup/wiki/FrequentlyAskedQuestions) - the main and foremost help resource.
*   [cryptsetup repository](https://git.kernel.org/cgit/utils/cryptsetup/cryptsetup.git/) and [release](https://www.kernel.org/pub/linux/utils/cryptsetup/) archive.
*   [FreeOTFE](https://en.wikipedia.org/wiki/FreeOTFE "wikipedia:FreeOTFE") - Supports unlocking LUKS encrypted volumes in Microsoft Windows.