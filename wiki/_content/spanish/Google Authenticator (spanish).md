[Google Authenticator](https://github.com/google/google-authenticator) provee un procedimiento de autenticación de dos pasos que utiliza contraseñas de un sólo uso (OTP). La aplicación generadora de OTP está disponible para iOS, Android y Blackberry. Semejante a [S/KEY Authentication](/index.php/S/KEY_Authentication "S/KEY Authentication") el mecanismo de autenticación se integra en el sistema [PAM](/index.php/PAM "PAM") de Linux. Ésta guía muestra la instalación y configuración de éste mecanismo.

## Contents

*   [1 Installación](#Installaci.C3.B3n)
*   [2 Setting up the PAM](#Setting_up_the_PAM)
*   [3 Generar un fichero de clave secreta](#Generar_un_fichero_de_clave_secreta)
*   [4 Configurando tu generador de OTP](#Configurando_tu_generador_de_OTP)
*   [5 Probando](#Probando)
*   [6 Inicio de sesión en escritorio](#Inicio_de_sesi.C3.B3n_en_escritorio)

## Installación

Instalar el paquete [libpam-google-authenticator](https://aur.archlinux.org/packages/libpam-google-authenticator/) desde [AUR](/index.php/AUR "AUR"). La versión de desarrollo también está disponible cómo [google-authenticator-libpam-git](https://aur.archlinux.org/packages/google-authenticator-libpam-git/).

## Setting up the PAM

**Warning:** Si haces toda la configuración via SSH no cierres la sesión antes de comprobar que todo funciona correctamente, si no puedes bloquearte a ti mismo. A demás considera crear una llave SSH (véase [SSH_keys_(Español)](/index.php/SSH_keys_(Espa%C3%B1ol) "SSH keys (Español)")) antes de activar PAM.

Por lo general, se quiere una autenticación de dos pasos sólo para el inicio de sesión remoto. El correspondiente fichero de configuración de PAM es `/etc/pam.d/sshd`. En caso de que quieras usar Google Authenticator de manera global Tendrías que cambiar `/etc/pam.d/system-auth`, sin embargo, en éste caso procede con extremo cuidado para no bloquearse a si mismo. En ésta guía procedemos a editar `/etc/pam.d/sshd` con ésta configuración que es más segura (pero no necesariamente) en una sesión local.

Para ingresar ambos, tu contraseña Unix y tu contraseña OTP, agrega `pam_google_authenticator.so` encima de las lineas system-remote-login en `/etc/pam.d/sshd`:

```
 **auth            required        pam_google_authenticator.so**
 auth            include         system-remote-login
 account         include         system-remote-login
 password        include         system-remote-login
 session         include         system-remote-login

```

Ésto le preguntará por la contraseña OTP antes de mostrar el prompt para introducir tu contraseña Unix. Cambiar el orden de los dos módulos invertirá el orden.

**Warning:** Sólo usuarios que hayan generado un fichero de clave secreta (vea abajo) tendrán permitido logearse usando SSH.

Para permitir el inicio de sesión con la contraseña de OTP o de Unix usar:

```
 auth            **sufficient**      pam_google_authenticator.so

```

Activar challenge-response authentication en `/etc/ssh/**sshd_config**`:

```
 ChallengeResponseAuthentication yes

```

Finalmente, [reload](/index.php/Reload "Reload") el servicio `sshd`.

**Warning:** OpenSSH ignorará todo esto si se está autenticando con un par de claves SSH y tiene [disabled password logins](/index.php/Secure_Shell#Force_public_key_authentication "Secure Shell"). A demás, a partir de OpenSSH 6.2, puedes añadir `AuthenticationMethods` permitir ambos: two-factor and key-based authentication. See [Secure Shell#Two-factor authentication and public keys](/index.php/Secure_Shell#Two-factor_authentication_and_public_keys "Secure Shell").

## Generar un fichero de clave secreta

**Tip:** Instalar [qrencode](https://www.archlinux.org/packages/?name=qrencode) para generar un código QR escaneable. Escanea el código QR con la app Google Authenticator para configurar automáticamente la clave.

Todos los usuarios que quieran usar autenticación en dos pasos necesitarán generar un fichero de clave secreta en su directorio personal. Ésto se puede hacer muy fácilmente usando *google-authenticator*:

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

Es recomendable **store the emergency scratch codes safely** (imprimirlos y mantenerlos en un lugar seguro) ya que son la única manera de iniciar sesión (via SSH) cuándo pierdes tu smartphone (p.e. tu generador-OTP). También se almacenan en `~/.google_authenticator`, por lo que puedes mirarlos en cualquier momento, siempre y cuándo ya estés conectado. No elimines (o sí) los códigos de ése fichero, ya que es de ahí de donde lee los códigos de emergencia, también puedes agregar códigos nuevos.

## Configurando tu generador de OTP

Instala el generador de OTP en tu móvil desde [Android market](http://m.google.com/authenticator) (e.g. [FreeOTP](https://play.google.com/store/apps/details?id=org.fedorahosted.freeotp)) o desde [F-Droid](https://f-droid.org/repository/browse/?fdfilter=google&fdid=com.google.android.apps.authenticator2). Clickea en el menú de la aplicación el botón correspondiente para crear una nueva cuenta y ya sea escaneando el código QR desde la URL donde se generó la clave secreta, o introduciendo la clave secreta (en el ejemplo 'ZVZG5UZU4D7MY4DH') manualmente.

Ahora deberías ver un nuevo token de código de acceso generado cada 30 segundos en tu teléfono.

## Probando

Conéctate por SSH al equipo:

```
 $ ssh hostname
 login as: <username>
 Verification code: <generated/backup-code>
 Password: <password>
 $

```

## Inicio de sesión en escritorio

EL plugin de PAM Google Authenticator también puede ser usado para inicios de sesión en la consola y con GDM. Solo añada lo siguiente en el fichero `/etc/pam.d/login` o en `/etc/pam.d/gdm-password`:

```
   auth required pam_google_authenticator.so

```