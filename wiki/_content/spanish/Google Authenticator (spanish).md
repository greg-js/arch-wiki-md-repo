**Estado de la traducción**
Este artículo es una traducción de [Google Authenticator](/index.php/Google_Authenticator "Google Authenticator"), revisada por última vez el **2019-03-11**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Google_Authenticator&diff=0&oldid=567347) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Google Authenticator](https://github.com/google/google-authenticator) proporciona un procedimiento de autenticación de dos pasos que utiliza códigos de acceso de un solo uso ([OTP](https://en.wikipedia.org/wiki/One-time_pad de Linux. Esta guía muestra la instalación y configuración de este mecanismo.

Para la operación inversa (generar códigos compatibles con Google Authenticator en Linux), véase [#Generación de código](#Generación_de_código) a continuación.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Configurando PAM](#Configurando_PAM)
    *   [2.1 Solicitar OTP solo cuando se conecte desde fuera de su red local](#Solicitar_OTP_solo_cuando_se_conecte_desde_fuera_de_su_red_local)
*   [3 Generar un archivo de clave secreta](#Generar_un_archivo_de_clave_secreta)
*   [4 Configurando su generador de OTP](#Configurando_su_generador_de_OTP)
*   [5 Probando](#Probando)
*   [6 Ubicación de almacenamiento](#Ubicación_de_almacenamiento)
*   [7 Inicios de sesión del escritorio](#Inicios_de_sesión_del_escritorio)
*   [8 Generación de código](#Generación_de_código)
    *   [8.1 Línea de órdenes](#Línea_de_órdenes)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [libpam-google-authenticator](https://www.archlinux.org/packages/?name=libpam-google-authenticator). La versión de desarrollo también está disponible con [google-authenticator-libpam-git](https://aur.archlinux.org/packages/google-authenticator-libpam-git/).

## Configurando PAM

**Advertencia:** Si realiza toda la configuración a través de [SSH](/index.php/SSH_(Espa%C3%B1ol) "SSH (Español)"), no cierre la sesión antes de comprobar que todo funciona, de lo contrario, puede bloquearse. Además, considere generar el archivo de clave antes de activar el PAM.

Por lo general, se requiere una autenticación de dos pasos solo para el inicio de sesión remoto. El archivo de configuración de PAM correspondiente es `/etc/pam.d/sshd`. En caso de que desee utilizar Google Authenticator globalmente, tendría que cambiar `/etc/pam.d/system-auth`, sin embargo, en este caso, proceda con extrema precaución para no bloquearse. En esta guía, procedemos con la edición de `/etc/pam.d/sshd` que se realiza de forma más segura (pero no necesariamente) en una sesión local.

Para introducir la contraseña de Unix y su OTP, añada `pam_google_authenticator.so` por encima de las líneas system-remote-login en `/etc/pam.d/sshd`:

```
 **auth            required        pam_google_authenticator.so**
 auth            include         system-remote-login
 account         include         system-remote-login
 password        include         system-remote-login
 session         include         system-remote-login

```

Esto le solicitará la OTP antes de su contraseña de Unix. Cambiar el orden de los dos módulos invertirá este orden.

**Advertencia:** Solo los usuarios que hayan generado un archivo de clave secreta (véase a continuación) podrán iniciar sesión usando SSH.

Para permitir el inicio de sesión con OTP o su contraseña de Unix, utilice:

```
 auth            **sufficient**      pam_google_authenticator.so

```

Activar la autenticación desafío-respuesta *(challenge-response)* en `/etc/ssh/**sshd_config**`:

```
 ChallengeResponseAuthentication yes

```

Finalmente, [reinicie](/index.php/Reload_(Espa%C3%B1ol) "Reload (Español)") el servicio `sshd`.

**Advertencia:** OpenSSH ignorará todo esto si se autentica con un par de claves SSH y tiene los [inicios de sesión de contraseña desactivados](/index.php/OpenSSH_(Espa%C3%B1ol)#Forzamiento_de_autenticación_con_claves_públicas "OpenSSH (Español)"). Sin embargo, a partir de OpenSSH 6.2, puede añadir `AuthenticationMethods` para permitir ambas: la autenticación basada en dos factores y por clave. Véase [Autenticación de dos factores y claves públicas](/index.php/OpenSSH_(Espa%C3%B1ol)#Autenticación_de_dos_factores_y_claves_públicas "OpenSSH (Español)")

### Solicitar OTP solo cuando se conecte desde fuera de su red local

A veces, solo queremos activar la capacidad 2FA solo cuando nos conectamos desde fuera de nuestra red local. Para lograr esto, cree un archivo (por ejemplo, `/etc/secutiry/access-local.conf`) y añada las redes desde las que desea omitir el 2FA:

```
# Permitir solo desde el rango de IP local
+ : ALL : 192.168.20.0/24
# Red adicional: VPN en el túnel IP (en caso de que tenga uno)
+ : ALL : 10.8.0.0/24
+ : ALL : LOCAL
- : ALL : ALL

```

Luego edite su `/etc/pam.d/sshd` y añada la línea:

```
#%PAM-1.0
#auth     required  pam_securetty.so     #disable remote root
**auth [success=1 default=ignore] pam_access.so accessfile=/etc/security/access-local.conf**
auth      required  pam_google_authenticator.so
auth      include   system-remote-login
account   include   system-remote-login
password  include   system-remote-login
session   include   system-remote-login

```

## Generar un archivo de clave secreta

**Sugerencia:** [Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [qrencode](https://www.archlinux.org/packages/?name=qrencode) para generar un código QR escaneable. Escanee el código QR con la aplicación autenticadora para configurar automáticamente la clave.

Todo usuario que quiera usar la autenticación de dos pasos necesita generar un archivo de clave secreta en su carpeta de inicio. Esto se puede hacer muy fácilmente utilizando *google-authenticator*:

```
   $ google-authenticator
   Do you want authentication tokens to be time-based (y/n) y
   <Here you will see generated QR code>
   Your new secret key is: ZVZG5UZU4D7MY4DH
   Your verification code is 269371
   Your emergency scratch codes are:
     70058954
     97277505
     99684896
     56514332
     82717798

   Do you want me to update your "/home/username/.google_authenticator" file (y/n) y

   Do you want to disallow multiple uses of the same authentication
   token? This restricts you to one login about every 30s, but it increases
   your chances to notice or even prevent man-in-the-middle attacks (y/n) y

   By default, tokens are good for 30 seconds and in order to compensate for
   possible time-skew between the client and the server, we allow an extra
   token before and after the current time. If you experience problems with poor
   time synchronization, you can increase the window from its default
   size of 1:30min to about 4min. Do you want to do so (y/n) n

   If the computer that you are logging into is not hardened against brute-force
   login attempts, you can enable rate-limiting for the authentication module.
   By default, this limits attackers to no more than 3 login attempts every 30s.
   Do you want to enable rate-limiting (y/n) y

```

Se recomienda **guardar los códigos de emergencia de manera segura** (imprimirlos y guardarlos en un lugar seguro) ya que son su única forma de iniciar sesión (a través de SSH) cuando pierda su teléfono móvil (es decir, su generador de OTP). También se almacenan en `~/.google_authenticator`, por lo que puede buscarlos en cualquier momento siempre y cuando haya iniciado sesión.

## Configurando su generador de OTP

Instale una aplicación generadora en su teléfono móvil (por ejemplo):

*   **FreeOTP** para [Android](https://play.google.com/store/apps/details?id=org.fedorahosted.freeotp)/[iOS](https://itunes.apple.com/es/app/freeotp-authenticator/id872559395).
*   **Google Authenticator** para [Android](https://play.google.com/store/apps/details?id=com.google.android.apps.authenticator2)/[iOS](https://itunes.apple.com/es/app/google-authenticator/id388497605).

En la aplicación móvil, cree una nueva cuenta y, o bien escanee el código QR de la URL que le indicaron al generar el archivo de clave secreta, o introduzca manualmente la clave secreta (en el ejemplo anterior 'ZVZG5UZU4D7MY4DH').

Ahora debería ver un nuevo token de código de acceso que se genera cada 30 segundos en su teléfono.

## Probando

Conecte por SSH a su host desde otra máquina y/o desde otra ventana de terminal:

```
 $ ssh hostname
 login as: <usuario>
 Verification code: <generado/emergencia>
 Password: <contraseña>
 $

```

## Ubicación de almacenamiento

Si desea cambiar la ruta de almacenamiento de los archivos de clave secreta, puede utilizar la opción `--secret`:

```
$ google-authenticator --secret="/**RUTA_CARPETA**/**USUARIO**"

```

Entonces, no olvide cambiar la ruta de ubicación de PAM, en `/etc/pam.d/sshd`:

 `/etc/pam.d/sshd`  `auth required pam_google_authenticator.so user=root secret=/**RUTA_CARPETA**/${USER}` 

`user=root` se utiliza para forzar a PAM a buscar el archivo utilizando un superusuario.

Además, tenga cuidado con los permisos del archivo de clave secreta. De hecho, el archivo **debe** ser solo legible por el propietario (chmod: `400`). Aquí, el propietario es el superusuario *(root)*.

```
$ chown root.root /**RUTA_ARCHIVO**/**ARCHIVOS_CLAVE_SECRETA**
  chmod 400 /**RUTA_ARCHIVO**/**ARCHIVOS_CLAVE_SECRETA**

```

## Inicios de sesión del escritorio

El complemento PAM de Google Authenticator también se puede utilizar para inicios de sesión de consola y con GDM. Simplemente añada lo siguiente a `/etc/pam.d/login` o al archivo `/etc/pam.d/gdm-password`:

```
   auth required pam_google_authenticator.so

```

## Generación de código

Si tiene Google Authenticator configurado con otros sistemas, perder su dispositivo puede impedirle iniciar sesión en estos. Tener formas adicionales de generar los códigos puede ser útil.

### Línea de órdenes

La forma más fácil de generar códigos es con `oath-tool`. Está disponible en el paquete [oath-toolkit](https://www.archlinux.org/packages/?name=oath-toolkit), y se puede utilizar de la siguiente manera:

```
oathtool --totp -b ABC123

```

Donde `ABC123` es la clave secreta.

En la mayoría de los sistemas Android con acceso de usuario suficiente, la base de datos de Google Authenticator se puede copiar del dispositivo y acceder directamente, ya que es una base de datos sqlite3\. Este script de shell leerá una base de datos de Google Authenticator y generará códigos en vivo para cada clave encontrada:

 `google-authenticator.sh` 
```
#!/bin/sh

# Esta es la ruta al archivo de la aplicación Google Authenticator. Se suele ubicar
# en /data bajo Android. Cópielo en su PC en un lugar seguro y especifique la
# ruta aquí.
DB="/ruta/a/com.google.android.apps.authenticator/databases/databases"

sqlite3 "$DB" 'SELECT email,secret FROM accounts;' | while read A
do
        NAME=`echo "$A" | cut -d '|' -f 1`
        KEY=`echo "$A" | cut -d '|' -f 2`
        CODE=`oathtool --totp -b "$KEY"`
        echo -e "\e[1;32m$CODE\e[0m - \e[1;33m$NAME\e[0m"
done
```