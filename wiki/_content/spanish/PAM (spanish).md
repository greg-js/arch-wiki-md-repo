**Estado de la traducción**
Este artículo es una traducción de [PAM](/index.php/PAM "PAM"), revisada por última vez el **2019-02-10**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=PAM&diff=0&oldid=566242) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Security](/index.php/Security "Security")
*   [pam_mount](/index.php/Pam_mount "Pam mount")
*   [pam_usb](/index.php/Pam_usb "Pam usb")
*   [pam_abl](/index.php/Pam_abl "Pam abl")
*   [pam_oath](/index.php/Pam_oath "Pam oath")

Los [módulos de autenticación conectables de Linux](http://www.linux-pam.org/) (Linux Pluggable Authentication Modules, o simplemente PAM) proporcionan un marco para la autenticación de usuarios en todo el sistema. Para citar el [proyecto](http://www.linux-pam.org/whatispam.html):

	PAM proporciona una manera de desarrollar programas que son independientes del esquema de autenticación. Estos programas necesitan "módulos de autenticación" que se deben adjuntar en tiempo de ejecución para que funcionen. El módulo de autenticación que se adjuntará depende de la configuración del sistema local y queda a discreción del administrador del sistema local.

Este artículo explica los valores predeterminados de configuración base de Arch Linux para PAM para autenticar usuarios locales y remotos. La aplicación de cambios a los valores predeterminados está sujeta a artículos especializados reticulados por tema.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
    *   [2.1 Parámetros de seguridad](#Parámetros_de_seguridad)
    *   [2.2 Apilado base de PAM](#Apilado_base_de_PAM)
        *   [2.2.1 Ejemplos](#Ejemplos)
*   [3 Configuración guiada](#Configuración_guiada)
    *   [3.1 Configuración de los parámetros de seguridad](#Configuración_de_los_parámetros_de_seguridad)
    *   [3.2 Configuración del apilado y los módulos de PAM](#Configuración_del_apilado_y_los_módulos_de_PAM)
*   [4 Otros paquetes de PAM](#Otros_paquetes_de_PAM)
*   [5 Véase también](#Véase_también)

## Instalación

El paquete [pam](https://www.archlinux.org/packages/?name=pam) es parte del [grupo base](/index.php/Base_group_(Espa%C3%B1ol) "Base group (Español)") de paquetes y, por lo tanto, instalado normalmente en un sistema Arch. Los módulos PAM están instalados exclusivamente en `/usr/lib/security`.

Los repositorios contienen una serie de paquetes PAM opcionales, en [#Configuración guiada](#Configuración_guiada) se muestran unos ejemplos.

## Configuración

Un número de rutas en `/etc` son relevantes para PAM, ejecute `pacman -Ql pam |grep /etc` para ver los archivos de configuración por defecto creados. Se relacionan con los [#Parámetros de seguridad](#Parámetros_de_seguridad) para los módulos, o la configuración [#Apilado base de PAM](#Apilado_base_de_PAM).

### Parámetros de seguridad

La ruta `/etc/security` contiene la configuración específica del sistema para las variables que ofrecen los métodos de autenticación. La instalación básica lo puebla con los archivos de configuración predeterminados.

Note que Arch Linux no proporciona una configuración específica de distribución para estos archivos. Por ejemplo, el archivo `/etc/security/pwquality.conf` se puede utilizar para definir los valores predeterminados de todo el sistema para la calidad de la contraseña. Sin embargo, para activarlo, el módulo `pam_pwquality.so` debe añadirse al [#Apilado base de PAM](#Apilado_base_de_PAM) de los módulos, que no es el caso por defecto.

Véase [#Configuración de los parámetros de seguridad](#Configuración_de_los_parámetros_de_seguridad) para algunas de las posibilidades.

### Apilado base de PAM

La ruta `/etc/pam.d/` es exclusiva de la configuración de PAM para vincular las aplicaciones a los esquemas individuales de autenticación de los sistemas. Durante la instalación de la base del sistema se puebla con:

*   el paquete [pambase](https://www.archlinux.org/packages/?name=pambase), que contiene la pila base de la configuración PAM específica de Arch Linux para ser utilizada por las aplicaciones, y
*   otros paquetes base. Por ejemplo, [util-linux](https://www.archlinux.org/packages/?name=util-linux) añade la configuración para el *inicio de sesión* central y otros programas, el paquete [shadow](https://www.archlinux.org/packages/?name=shadow) añade los valores predeterminados de Arch Linux para proteger y modificar la base de datos del usuario (véase [Usuarios y grupos](/index.php/Users_and_groups_(Espa%C3%B1ol) "Users and groups (Español)")).

Los diferentes archivos de configuración de la instalación base se apilan durante el tiempo de ejecución. Por ejemplo, en el inicio de sesión de un usuario local, la aplicación *login* carga la política `system-local-login`, que a su vez carga otros:

 `/etc/pam.d/`  `login -> system-local-login -> system-login -> system-auth` 

Para una aplicación diferente, se puede aplicar una ruta diferente. Por ejemplo, [openssh](https://www.archlinux.org/packages/?name=openssh) instala su política de PAM `sshd`:

 `/etc/pam.d/`  `sshd -> system-remote-login -> system-login -> system-auth` 

En consecuencia, la elección del archivo de configuración en la pila es importante. Para el ejemplo anterior, se podría requerir un método de autenticación especial solo para `sshd` o para todos los inicios de sesión remotos cambiando `system-remote-login`; ambos cambios no afectarían los inicios de sesión locales. Aplicar el cambio a `system-login` o `system-auth` en cambio afectaría los inicios de sesión locales y remotos.

Al igual que en el ejemplo de `sshd`, se requiere que cualquier aplicación **consciente de PAM** instale su política en `/etc/pam.d` para integrar y confiar en la pila de PAM apropiadamente. Si una aplicación no lo hace, se aplica la política predeterminada para denegar de `/etc/pam.d/other` y se registra una advertencia.

**Sugerencia:** PAM está enlazado dinámicamente en tiempo de ejecución. Por ejemplo: `$ ldd /usr/bin/login |grep pam` 
```
libpam.so.0 => /usr/lib/libpam.so.0 (0x000003d8c32d6000)
libpam_misc.so.0 => /usr/lib/libpam_misc.so.0 (0x000003d8c30d2000)
```
la aplicación *login* es consciente de PAM y **debe**, por lo tanto, tener una política.

Las páginas del manual del paquete PAM [pam(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pam.8) y [pam.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pam.d.5) describen el contenido estandarizado de los archivos de configuración. En particular, explican los cuatro grupos de PAM: gestión de cuentas, autenticación, contraseña y sesión, así como los valores de control que pueden utilizarse para configurar el apilamiento y el comportamiento de los módulos.

Además, se ha instalado una extensa documentación en `/usr/share/doc/Linux-PAM/index.html` que, entre varias guías, contiene páginas de manual navegables para cada uno de los módulos estándar.

**Advertencia:** Los cambios en la configuración de PAM afectan fundamentalmente a la autenticación del usuario. Los cambios erróneos pueden dar como resultado que **todos** o **algún** usuario no pueda iniciar sesión. Dado que los cambios no son efectivos para usuarios ya autenticados, una buena precaución es realizar cambios con un usuario y probar el resultado con otro usuario en una consola separada.

#### Ejemplos

Dos ejemplos breves para ilustrar la advertencia anterior.

Primero, tomamos las siguientes dos líneas:

 `/etc/pam.d/system-auth` 
```
auth      required  pam_unix.so     try_first_pass nullok
auth      optional  pam_permit.so
```

De [pam_unix(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pam_unix.8): "El componente de autenticación `pam_unix.so` realiza la tarea de verificar las credenciales (contraseña) de los usuarios. La acción predeterminada de este módulo es no permitir que el usuario acceda a un servicio si su contraseña oficial está en blanco." - siendo lo último para lo que se utiliza `pam_permit.so`. Basta con intercambiar los valores de control `required` y `optional` para desactivar la autenticación de contraseña, es decir, cualquier usuario puede iniciar sesión sin proporcionar una contraseña.

Segundo, como ejemplo contrario, por configuración predeterminada creando el siguiente archivo:

```
# touch /etc/nologin 

```

da como resultado que ningún usuario que no sea root pueda iniciar sesión (si se permiten inicios de sesión del superusuario, otro valor predeterminado para Arch Linux). Para volver a permitir los inicios de sesión, elimine el archivo desde la consola con la que lo creó.

Con eso como fondo, véase [#Configuración del apilado y los módulos de PAM](#Configuración_del_apilado_y_los_módulos_de_PAM) para configuraciones de casos de uso particulares.

## Configuración guiada

Esta sección proporciona una descripción general del contenido que detalla cómo aplicar cambios a la configuración de PAM y cómo integrar nuevos módulos PAM especiales en la pila de PAM. Tenga en cuenta que, por lo general, se puede acceder a las páginas del manual de los módulos al eliminar la extensión `.so`.

### Configuración de los parámetros de seguridad

Las siguientes secciones describen ejemplos para cambiar la configuración predeterminada de parámetros de PAM:

*   [Security#Enforcing strong passwords using pam_cracklib](/index.php/Security#Enforcing_strong_passwords_using_pam_cracklib "Security")

	muestra cómo forzar contraseñas seguras con `pam_cracklib.so`.

*   [Security#Lockout user after three failed login attempts](/index.php/Security#Lockout_user_after_three_failed_login_attempts "Security")

	muestra cómo limitar los intentos de inicio de sesión con `pam_tally.so`.

*   [Security#Allow only certain users](/index.php/Security#Allow_only_certain_users "Security")

	limita los inicios de sesión de usuario con `pam_wheel.so`.

*   [Realtime process management#Configuring PAM](/index.php/Realtime_process_management#Configuring_PAM "Realtime process management") and [Security#Limit amount of processes](/index.php/Security#Limit_amount_of_processes "Security")

	detalla cómo configurar los límites del proceso del sistema con `pam_limits.so`.

*   [Environment variables#Using pam_env](/index.php/Environment_variables#Using_pam_env "Environment variables")

	muestra ejemplos para establecer variables de entorno a través de `pam_env.so`.

### Configuración del apilado y los módulos de PAM

Los siguientes artículos detallan cómo cambiar el [#Apilado base de PAM](#Apilado_base_de_PAM) para casos de uso especiales.

Módulos PAM de los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"):

*   [pam_mount](/index.php/Pam_mount "Pam mount")

	ejemplos detallados para utilizar `pam_mount.so` para montar automáticamente las rutas de directorio cifradas en el inicio de sesión del usuario.

*   [ECryptfs#Auto-mounting](/index.php/ECryptfs#Auto-mounting "ECryptfs")

	utiliza `pam_ecryptfs.so` para montar automáticamente un directorio cifrado.

*   [Dm-crypt/Mounting at login (Español)](/index.php/Dm-crypt/Mounting_at_login_(Espa%C3%B1ol) "Dm-crypt/Mounting at login (Español)")

	muestra cómo utilizar `pam_exec.so` para ejecutar un script personalizado en un inicio de sesión de usuario.

*   [Active Directory integration#Configuring PAM](/index.php/Active_Directory_integration#Configuring_PAM "Active Directory integration")

	utiliza `pam_winbind.so` y `pam_krb5.so` para que los usuarios se identifiquen a través de servicios Active Directory (LDAP, [Kerberos](/index.php/Kerberos "Kerberos")).

*   [LDAP authentication](/index.php/LDAP_authentication "LDAP authentication") con su sección [LDAP authentication#NSS and PAM](/index.php/LDAP_authentication#NSS_and_PAM "LDAP authentication")

	es un artículo sobre la integración de la autenticación de cliente o servidor LDAP con `pam_ldap.so`.

*   [YubiKey#Two-factor authentication with SSH](/index.php/YubiKey#Two-factor_authentication_with_SSH "YubiKey")

	se basa en `pam_yubico.so` en la pila de PAM para activar la autenticación a través del protocolo propietario Yubikey.

*   [pam_oath](/index.php/Pam_oath "Pam oath")

	muestra un ejemplo para implementar la autenticación de dos factores *(two-factor)* basada en software con `pam_oath.so`.

*   [fprint](/index.php/Fprint "Fprint")

	emplea `pam_fprintd.so` para configurar la autenticación mediante huellas digitales.

Módulos PAM del [repositorio de usuarios de Arch](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)"):

*   [pam_usb](/index.php/Pam_usb "Pam usb")

	muestra cómo configurar `pam_usb.so` para utilizar un dispositivo USB para autenticar, opcionalmente, mediante dos factores.

*   [SSH keys#pam_ssh](/index.php/SSH_keys#pam_ssh "SSH keys")

	utiliza `pam_ssh.so` para autenticar como un usuario remoto.

*   [pam_abl](/index.php/Pam_abl "Pam abl")

	explica cómo se puede utilizar `pam_abl.so` para limitar los ataques de fuerza bruta a través de ssh.

*   [EncFS](/index.php/EncFS#.2Fetc.2Fpam.d.2F "EncFS")

	puede ser montado automáticamente a través `pam_encfs.so`.

*   [Google Authenticator](/index.php/Google_Authenticator_(Espa%C3%B1ol) "Google Authenticator (Español)")

	muestra cómo configurar la autenticación de dos factores con `pam_google_authenticator.so`.

*   [Very Secure FTP Daemon (Español)#PAM con usuarios virtuales](/index.php/Very_Secure_FTP_Daemon_(Espa%C3%B1ol)#PAM_con_usuarios_virtuales "Very Secure FTP Daemon (Español)")

	explica cómo configurar un chroot FTP con `pam_pwdfile.so` para autenticar usuarios sin una cuenta local de sistema.

## Otros paquetes de PAM

Aparte de los paquetes mencionados hasta ahora, el [repositorio de usuarios de Arch](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)") Contiene varios módulos y herramientas PAM adicionales.

Las utilidades de propósito general relacionadas con PAM son:

*   **[libx32_pam](https://github.com/ArchLinux-x32/libx32-pam)** — Biblioteca Arch Linux PAM x32 ABI

	[http://linux-pam.org/](http://linux-pam.org/) || [libx32-pam](https://aur.archlinux.org/packages/libx32-pam/)

*   **[Pamtester](http://linux.die.net/man/1/pamtester)** — Programa para probar la instalación de los módulos de autenticación conectables (PAM)

	[http://pamtester.sourceforge.net/](http://pamtester.sourceforge.net/) || [pamtester](https://aur.archlinux.org/packages/pamtester/)

Tenga en cuenta que AUR cuenta con una etiqueta de palabra clave para [PAM](https://aur.archlinux.org/packages/?O=0&SeB=k&K=pam&outdated=off&SB=p&SO=d&PP=50&do_Search=Go), pero no todos los paquetes disponibles se actualizan para incluirlo. Por lo tanto, puede ser necesario buscar en la [descripción del paquete](https://aur.archlinux.org/packages/?O=0&SeB=nd&K=pam&outdated=off&SB=p&SO=d&PP=50&do_Search=Go).

## Véase también

*   [linux-pam.org](http://www.linux-pam.org/) - La página de inicio del proyecto
*   [Entendiendo y configurando PAM](https://www.ibm.com/developerworks/linux/library/l-pam/index.html) - Un artículo introductorio