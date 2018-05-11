## Contents

*   [1 Explorando dispositivos de Android](#Explorando_dispositivos_de_Android)
*   [2 Desarrollo en Android](#Desarrollo_en_Android)
    *   [2.1 Android Studio](#Android_Studio)
    *   [2.2 Instalación manual del SDK](#Instalaci.C3.B3n_manual_del_SDK)
        *   [2.2.1 Componentes básicos del SDK de Android](#Componentes_b.C3.A1sicos_del_SDK_de_Android)
        *   [2.2.2 API de plataforma del SDK de Android](#API_de_plataforma_del_SDK_de_Android)
        *   [2.2.3 Imágenes de sistema de Android](#Im.C3.A1genes_de_sistema_de_Android)
    *   [2.3 Puente de depurado de Android](#Puente_de_depurado_de_Android)
        *   [2.3.1 Conectar dispositivo](#Conectar_dispositivo)

## Explorando dispositivos de Android

Cuando un dispositivo moderno de Android se conecta a un computador con el cable USB, se puede usar el [Protocolo de transferencia de medios](/index.php/Media_Transfer_Protocol "Media Transfer Protocol") (MTP en ingles) para transferir archivos y el [#Puente de depurado de Android](#Puente_de_depurado_de_Android) (ADB en ingles) para depurar.

Archivos pueden ser transferidos con varios protocolos ([SSH](/index.php/Secure_Shell_(Espa%C3%B1ol) "Secure Shell (Español)"), [FTP](/index.php/Category:File_Transfer_Protocol_(Espa%C3%B1ol) "Category:File Transfer Protocol (Español)"), [Samba](/index.php/Samba_(Espa%C3%B1ol) "Samba (Español)"), HTTP). Solo es necesario establecer un servidor y un cliente, mediante aplicaciones Android puede convertirse en uno de estos.

Para restaurar un sistema o sobrescribir sus sistema actual vea [#Restaurar Android](#Restaurar_Android).

Para conectarse con Android vea [#Software de conexión](#Software_de_conexi.C3.B3n) por las diferentes opciones existentes en Arch Linux.

## Desarrollo en Android

Para desarrollar aplicaciones en Android necesita tres requisitos:

*   el componente básico de Android SDK
*   uno o múltiples paquetes de plataforma de Android SDK
*   interfaz de usuario

La interfaz oficial es [#Android Studio](#Android_Studio), la cual contiene su propio gestor de SDK.

### Android Studio

[Android Studio](https://developer.android.com/studio/index.html) es el entorno oficial de desarrollo de Android basado en [IntelliJ Idea](https://www.jetbrains.com/idea/). Contiene herramientas de desarrollo y depuración de Android integradas.

Se puede [instalar](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") con el paquete [android-studio](https://aur.archlinux.org/packages/android-studio/). Si obtiene errores sobre SDK faltantes refiérase a [#Android SDK platform API](#Android_SDK_platform_API).

**Nota:**

*   Asegurese de [establecer su ambiente de java](/index.php/Java_(Espa%C3%B1ol)#Cambiar_el_ambiente_de_Java "Java (Español)") de lo contrario Android Studio no arrancara.

Normalmente, aplicaciones son construidas en el GUI de Android Studio. Para construir desde una terminal de comandos usando por ejemplo `./gradlew assembleDebug`), agregue lo siguiente a su archivo `~/.bashrc`:

```
export ANDROID_HOME=/opt/android-sdk

```

### Instalación manual del SDK

Si esta usando [#Android Studio](#Android_Studio) y desea que la interfaz gestione la instalación del SDK, puede saltar esta sección.

#### Componentes básicos del SDK de Android

**Nota:** El SDK de Android contiene binarios de 32-bit, debe habilitar el repositorio [multilib](/index.php/Multilib_(Espa%C3%B1ol) "Multilib (Español)"). De lo contrario encontrara un error `error: target not found: lib32-*`.

Antes de desarrollar aplicaciones de Android, es necesario instalar el SDK de Android, esta compuesto por 4 paquetes diferentes, todos [instalables](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") desde [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)"):

1.  [android-platform](https://aur.archlinux.org/packages/android-platform/)
2.  [android-sdk](https://aur.archlinux.org/packages/android-sdk/)
3.  [android-sdk-platform-tools](https://aur.archlinux.org/packages/android-sdk-platform-tools/)
4.  [android-sdk-build-tools](https://aur.archlinux.org/packages/android-sdk-build-tools/)

Si se desea soportar dispositivos antiguos o se trabaja con código antiguo, los paquetes [android-support](https://aur.archlinux.org/packages/android-support/) y [android-support-repository](https://aur.archlinux.org/packages/android-support-repository/) pueden ser requeridos.

El SDK de Android será instalado en `/opt/android-sdk/`. Esta carpeta tiene permisos de root, así que debe ejecutar el gestor de SDK como root, de lo contrario no podrá modificar nada en esta carpeta. Si desea usar su usuario regular, es necesario crear el grupo sdkusers:

```
# groupadd sdkusers

```

Agregue su usuario a este grupo:

```
# gpasswd -a <ususario> sdkusers

```

Cambie el grupo de la carpeta:

```
# chown -R :sdkusers /opt/android-sdk/

```

Cambie los permisos de la carpeta para que el usuario agregado a este grupo pueda hacer cambios:

```
# chmod -R g+w /opt/android-sdk/

```

Reinicie sesión o como su <usuario> ejecute en una terminal:

```
$ newgrp sdkusers

```

**Nota:** Como una alternativa a la instalación global con los paquetes de [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)"), el SDK pude ser instalado en la carpeta raíz del usuario con las siguientes [instrucciones](https://developer.android.com/sdk/index.html)(en ingles). También se pueden usar los paquetes android-*-dummy del [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)") para manejar dependencias del sistema.

#### API de plataforma del SDK de Android

Instale la plataforma deseada de los paquetes del [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)"):

*   [android-platform](https://aur.archlinux.org/packages/android-platform/) – el API mas reciente
*   [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)") también contiene APIs antiguos. [[1]](https://aur.archlinux.org/packages/?K=android-platform-)

#### Imágenes de sistema de Android

Instale la [imagen deseada de Android](https://aur.archlinux.org/packages/?K=android-+system+image) desde [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)"). Las imágenes son necesarias para la emulación de dispositivos específicos. No son necesarias si desea desarrollar con un teléfono de Android.

### Puente de depurado de Android

Esta sección se refiere a lo que generalmente se conoce como **ADB (Android Debug Bridge)**, si existe alguna referencia a *ADB* es simplemente la versión en ingles.

**Sugerencia:**

*   En algunos dispositivos, puede ser necesario activar la opción de transferencia de datos (MTP), antes que el puente de depurado funcione. Otros dispositivos requieren el modo PTP para que funcione.
*   Las reglas de udev para muchos dispositivos vienen configuradas con el paquete [libmtp](https://www.archlinux.org/packages/?name=libmtp), así que si lo tiene instalado los siguientes pasos puede que no sean necesarios.
*   Asegúrese que su cable de USB funciona para recargar batería y para transferencia de datos. Bastantes cables de USB que vienen con el dispositivo no tienen el pin para transferencia de datos.

#### Conectar dispositivo

Para conectar a un dispositivo o teléfono mediante el puente de depurado es necesario:

1.  Instalar el paquete [android-tools](https://www.archlinux.org/packages/?name=android-tools). Adicionalmente, es recomendable instalar el paquete [android-udev](https://www.archlinux.org/packages/?name=android-udev) si desea conectar el dispositivo con la entrada apropiada en `/dev/`.
2.  conecte el dispositivo de Android con el cable USB al computador.
3.  Habilite depurado por USB en el dispositivo:
    *   Android Jelly Bean (4.2) y nuevos: en *Configuración > Acerca del dispositivo* clic *Numero de compilación* 7 veces hasta que vea una notificación que se ha vuelto programador. Después vaya a *Configuración > Opciones de programador > Depuración en Android* y active esta opción. El dispositivo preguntara para aceptar el computador con la huella digital pertinente, permitir de manera permanente copiara el archivo `$HOME/.android/adbkey.pub` en la carpeta `/data/misc/adb/adb_keys` del dispositivo.
    *   Versiones anterioes: generalmente se activa en *Configuración > Aplicaciones > Desarrollo > Depurado en Android*. Reinicie el teléfono después de activar esta opción para asegurarse que el depurado esta habilitado.

Si el [puente reconoce su dispositivo](#Detectar_dispositivo), o el comando `adb devices` muestra `"device"` y no `"unauthorized"`, o es visible desde el su entorno de desarrollo; la conexión funciona. De lo contrario vea las instrucciones en la parte inferior.