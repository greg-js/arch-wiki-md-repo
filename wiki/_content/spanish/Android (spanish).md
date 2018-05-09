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