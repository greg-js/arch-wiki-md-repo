**Estado de la traducción**
Este artículo es una traducción de [PAM](/index.php/PAM "PAM"), revisada por última vez el **2019-01-18**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=PAM&diff=0&oldid=563734) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Security](/index.php/Security "Security")
*   [pam_mount](/index.php/Pam_mount "Pam mount")
*   [pam_usb](/index.php/Pam_usb "Pam usb")
*   [pam_abl](/index.php/Pam_abl "Pam abl")
*   [pam_oath](/index.php/Pam_oath "Pam oath")

Los [módulos de autenticación conectables de Linux](http://www.linux-pam.org/) (Linux Pluggable Authentication Modules, o simplemente PAM) proporcionan un marco para la autenticación de usuarios en todo el sistema. Para citar el [proyecto](http://www.linux-pam.org/whatispam.html):

	PAM proporciona una manera de desarrollar programas que son independientes del esquema de autenticación. Estos programas necesitan "módulos de autenticación" que se deben adjuntar en tiempo de ejecución para que funcionen. El módulo de autenticación que se adjuntará depende de la configuración del sistema local y queda a discreción del administrador del sistema local.

Este artículo explica los valores predeterminados de configuración base de Arch Linux para PAM para autenticar usuarios locales y remotos. La aplicación de cambios a los valores predeterminados está sujeta a artículos especializados reticulados por tema.

## Contents

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

Al igual que en el ejemplo de `sshd`, se requiere que cualquier aplicación **consciente de PAM** instale su política en `/etc/pam.d` para integrar y confiar en la pila de PAM apropiadamente. Si una aplicación no lo hace, la política de `/etc/pam.d/other` se aplica por defecto. Se instala una política permisiva por defecto ([FS#48650](https://bugs.archlinux.org/task/48650)).

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

This section provides an overview of content detailing how to apply changes to the PAM configuration and how to integrate special new PAM modules into the PAM stack. Note the man pages for the modules can generally be reached dropping the `.so` extension.

### Configuración de los parámetros de seguridad

The following sections describe examples to change the default PAM parameter configuration:

*   [Security#Enforcing strong passwords using pam_cracklib](/index.php/Security#Enforcing_strong_passwords_using_pam_cracklib "Security")

	shows how to enforce strong passwords with `pam_cracklib.so`.

*   [Security#Lockout user after three failed login attempts](/index.php/Security#Lockout_user_after_three_failed_login_attempts "Security")

	shows how to limit login attempts with `pam_tally.so`.

*   [Security#Allow only certain users](/index.php/Security#Allow_only_certain_users "Security")

	limits user logons with `pam_wheel.so`.

*   [Realtime process management#Configuring PAM](/index.php/Realtime_process_management#Configuring_PAM "Realtime process management") and [Security#Limit amount of processes](/index.php/Security#Limit_amount_of_processes "Security")

	detail how to configure system process limits with `pam_limits.so`.

*   [Environment variables#Using pam_env](/index.php/Environment_variables#Using_pam_env "Environment variables")

	shows examples to set environment variables via `pam_env.so`.

### Configuración del apilado y los módulos de PAM

The following articles detail how to change the [#Apilado base de PAM](#Apilado_base_de_PAM) for special use-cases.

PAM modules from the [Official repositories](/index.php/Official_repositories "Official repositories"):

*   [pam_mount](/index.php/Pam_mount "Pam mount")

	detail examples for using `pam_mount.so` to automount encrypted directory paths on user login.

*   [ECryptfs#Auto-mounting](/index.php/ECryptfs#Auto-mounting "ECryptfs")

	uses `pam_ecryptfs.so` to automount an encrypted directory.

*   [Dm-crypt/Mounting at login](/index.php/Dm-crypt/Mounting_at_login "Dm-crypt/Mounting at login")

	shows how to use `pam_exec.so` to execute a custom script on a user login.

*   [Active Directory Integration#Configuring PAM](/index.php/Active_Directory_Integration#Configuring_PAM "Active Directory Integration")

	uses `pam_winbind.so` and `pam_krb5.so` to let users authenticate via Active Directory (LDAP, [Kerberos](/index.php/Kerberos "Kerberos")) services.

*   [LDAP authentication](/index.php/LDAP_authentication "LDAP authentication") with its [LDAP authentication#NSS and PAM](/index.php/LDAP_authentication#NSS_and_PAM "LDAP authentication") section

	is an article about integrating LDAP client or server-side authentication with `pam_ldap.so`.

*   [YubiKey#Two-factor authentication with SSH](/index.php/YubiKey#Two-factor_authentication_with_SSH "YubiKey")

	relies on `pam_yubico.so` in the PAM stack to enable authentication via the proprietary Yubikey.

*   [pam_oath](/index.php/Pam_oath "Pam oath")

	shows an example to implement software based two-factor authentication with `pam_oath.so`.

*   [fprint](/index.php/Fprint "Fprint")

	employs `pam_fprintd.so` to setup fingerprint authentication.

PAM modules from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"):

*   [pam_usb](/index.php/Pam_usb "Pam usb")

	shows how to configure `pam_usb.so` to use an usb-device for, optionally two-factor, authentication.

*   [SSH keys#pam_ssh](/index.php/SSH_keys#pam_ssh "SSH keys")

	uses `pam_ssh.so` to authenticate as a remote user.

*   [pam_abl](/index.php/Pam_abl "Pam abl")

	explains how `pam_abl.so` can be used to limit brute-forcing attacks via ssh.

*   [EncFS](/index.php/EncFS#.2Fetc.2Fpam.d.2F "EncFS")

	may get automounted via `pam_encfs.so`.

*   [Google Authenticator](/index.php/Google_Authenticator "Google Authenticator")

	shows how to set up two-factor authentication with `pam_google_authenticator.so`.

*   [Very Secure FTP Daemon#PAM with virtual users](/index.php/Very_Secure_FTP_Daemon#PAM_with_virtual_users "Very Secure FTP Daemon")

	explains how to configure a FTP chroot with `pam_pwdfile.so` to authenticate users without a local system account.

## Otros paquetes de PAM

Other than those packages mentioned so far, the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") contains a number of additional PAM modules and tools.

General purpose utilities relating to PAM are:

*   **[libx32_pam](https://github.com/ArchLinux-x32/libx32-pam)** — Arch Linux PAM x32 ABI library

	[http://linux-pam.org/](http://linux-pam.org/) || [libx32-pam](https://aur.archlinux.org/packages/libx32-pam/)

*   **[Pamtester](http://linux.die.net/man/1/pamtester)** — Program to test the pluggable authentication modules (PAM) facility

	[http://pamtester.sourceforge.net/](http://pamtester.sourceforge.net/) || [pamtester](https://aur.archlinux.org/packages/pamtester/)

Note the AUR features a keyword tag for [PAM](https://aur.archlinux.org/packages/?O=0&SeB=k&K=pam&outdated=off&SB=p&SO=d&PP=50&do_Search=Go), but not all available packages are updated to include it. Hence, searching the [package description](https://aur.archlinux.org/packages/?O=0&SeB=nd&K=pam&outdated=off&SB=p&SO=d&PP=50&do_Search=Go) may be necessary.

## Véase también

*   [linux-pam.org](http://www.linux-pam.org/) - The project homepage
*   [Understanding and configuring PAM](https://www.ibm.com/developerworks/linux/library/l-pam/index.html) - An introductory article