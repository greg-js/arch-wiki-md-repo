[KDE Wallet Manager](http://utils.kde.org/projects/kwalletmanager/) es una herramienta para gestionar las contraseñas en un escritorio KDE. El uso de KDE Wallet no solo te permite mantener tu información secreta, sino también acceder y gestionar las contraseñas de cada aplicación que se integre con KDE Wallet.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Desbloquear KDE Wallet automáticamente al iniciar la sesión](#Desbloquear_KDE_Wallet_automáticamente_al_iniciar_la_sesión)
*   [2 Usar KDE Wallet para almacenar claves de ssh](#Usar_KDE_Wallet_para_almacenar_claves_de_ssh)
*   [3 Usar KDE Wallet para almacenar credenciales Git http/https](#Usar_KDE_Wallet_para_almacenar_credenciales_Git_http/https)
*   [4 KDE Wallet para Firefox](#KDE_Wallet_para_Firefox)
*   [5 KDE Wallet para Chromium](#KDE_Wallet_para_Chromium)

## Desbloquear KDE Wallet automáticamente al iniciar la sesión

**Advertencia:** Esta funcionalidad no es compatible con el uso de claves [GnuPG](/index.php/GnuPG_(Espa%C3%B1ol) "GnuPG (Español)") para el cifrado de la cartera de KDE Wallet. Es necesario que el método de cifrado sea *blowfish*.

**Advertencia:** Para que este sistema funcione, es necesario que el nombre de la *cartera* que se desea desbloquear al iniciar sesión sea "kdewallet". Si por alguna razón necesitas cambiar de cartera, tendrás que renombrarla para que esto funcione.

Si tu contraseña de KDE Wallet es la misma que tu contraseña de usuario, puedes desbloquear automáticamente tu cartera al iniciar la sesión.

Instala [kwallet-pam](https://www.archlinux.org/packages/?name=kwallet-pam).

Después, edita `/etc/pam.d/kde` y añade estas dos líneas bajo las secciones correspondientes:

```
auth            optional        pam_kwallet.so kdehome=.kde4
session         optional        pam_kwallet.so
```
 `Ejemplo /etc/pam.d/kde` 
```
#%PAM-1.0
auth            include         system-login
auth            optional        pam_kwallet.so kdehome=.kde4 

account         include         system-login

password        include         system-login

session         include         system-login
session         optional        pam_kwallet.so
```

Tras reiniciar el equipo, tu cartera debería desbloquearse automáticamente si tu contraseña de usuario es la misma que tu contraseña de KDE Wallet y usas un gestor de acceso como [KDM](/index.php?title=KDM_(Espa%C3%B1ol)&action=edit&redlink=1 "KDM (Español) (page does not exist)").

## Usar KDE Wallet para almacenar claves de ssh

Instala [ksshaskpass](https://www.archlinux.org/packages/?name=ksshaskpass) desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

Crea el archivo `~/.kde4/Autostart/ssh-add.sh` con este contenido:

```
#!/bin/sh
ssh-add </dev/null

```

Hazlo ejecutable y ejecútalo:

```
$ chmod +x ~/.kde4/Autostart/ssh-add.sh
$ ~/.kde4/Autostart/ssh-add.sh

```

**Nota:** Es necesario que un [agente SSH](/index.php/SSH_keys_(Espa%C3%B1ol)#Agentes_de_SSH "SSH keys (Español)") esté en ejecución.

También puedes necesitar ejecutar mediante `source` el *script* que establece la variable de entorno `SSH_ASKPASS`:

```
. /etc/profile.d/ksshaskpass.sh

```

Te preguntará tu contraseña y desbloqueará tus claves SSH.

## Usar KDE Wallet para almacenar credenciales Git http/https

Git puede delegar la gestión de credenciales a KDE Wallet usando una herramienta como [ksshaskpass](https://www.archlinux.org/packages/?name=ksshaskpass)

Instala [ksshaskpass](https://www.archlinux.org/packages/?name=ksshaskpass) desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

Ejecuta el siguiente comando para configurar Git:

```
$ git config --global core.askpass /usr/bin/ksshaskpass

```

Ver [documentación gitcredentials](https://git-scm.com/docs/gitcredentials) para más detalles.

## KDE Wallet para Firefox

Hay un complemento para hacer que [Firefox](/index.php/Firefox_(Espa%C3%B1ol) "Firefox (Español)") almacene sus contraseñas con KDE Wallet.

[http://kde-apps.org/content/show.php/Firefox+addon+for+kwallet?content=116886](http://kde-apps.org/content/show.php/Firefox+addon+for+kwallet?content=116886)

## KDE Wallet para Chromium

Chromium incluye por defecto la integración con KDE Wallet.

Para activarla deberías ejecutar el navegador Chromium con los parámetros `--password-store=kwallet` o `--password-store=detect`.