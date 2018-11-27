**Estado de la traducción**
Este artículo es una traducción de [GNOME/Keyring](/index.php/GNOME/Keyring "GNOME/Keyring"), revisada por última vez el **2018-11-24**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=GNOME/Keyring&diff=0&oldid=557005) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[GNOME Keyring](https://wiki.gnome.org/Projects/GnomeKeyring) (*llavero de GNOME*) es "una colección de componentes en GNOME que almacenan secretos, contraseñas, claves, certificados y los ponen a disposición de las aplicaciones".

## Contents

*   [1 Instalación](#Instalación)
*   [2 Administrar utilizando la GUI](#Administrar_utilizando_la_GUI)
*   [3 Utilizando el llavero fuera de GNOME](#Utilizando_el_llavero_fuera_de_GNOME)
    *   [3.1 Sin un gestor de pantalla](#Sin_un_gestor_de_pantalla)
        *   [3.1.1 Inicio de sesión automático](#Inicio_de_sesión_automático)
        *   [3.1.2 Inicio de sesión de consola](#Inicio_de_sesión_de_consola)
            *   [3.1.2.1 Método PAM](#Método_PAM)
            *   [3.1.2.2 Método xinitrc](#Método_xinitrc)
    *   [3.2 Con un gestor de pantalla](#Con_un_gestor_de_pantalla)
*   [4 SSH keys](#SSH_keys)
    *   [4.1 Start SSH and Secrets components of keyring daemon](#Start_SSH_and_Secrets_components_of_keyring_daemon)
    *   [4.2 Disable keyring daemon components](#Disable_keyring_daemon_components)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Integration with applications](#Integration_with_applications)
    *   [5.2 Flushing passphrases](#Flushing_passphrases)
    *   [5.3 Git integration](#Git_integration)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Passwords are not remembered](#Passwords_are_not_remembered)
    *   [6.2 Resetting the keyring](#Resetting_the_keyring)
*   [7 Known issues](#Known_issues)
    *   [7.1 Cannot handle ECDSA and Ed25519 keys](#Cannot_handle_ECDSA_and_Ed25519_keys)
*   [8 Véase también](#Véase_también)

## Instalación

Cuando se utiliza GNOME, [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring) se instala automáticamente como parte del grupo [gnome](https://www.archlinux.org/groups/x86_64/gnome/). De lo contrario [instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring). Instale [libsecret](https://www.archlinux.org/packages/?name=libsecret) para permitir que las aplicaciones usen sus llaveros. [libgnome-keyring](https://www.archlinux.org/packages/?name=libgnome-keyring) está en desuso, sin embargo, algunas aplicaciones pueden requerirlo.

Las utilidades adicionales relacionadas con GNOME Keyring incluyen:

*   **secret-tool** — Acceso a GNOME keyring (y cualquier otro servicio que implemente la [API del servicio DBus Secret](http://standards.freedesktop.org/secret-service/)) desde la línea de órdenes.

	[https://wiki.gnome.org/Projects/Libsecret](https://wiki.gnome.org/Projects/Libsecret) || [libsecret](https://www.archlinux.org/packages/?name=libsecret)

*   **gnome-keyring-query** — Proporciona una herramienta simple de línea de órdenes para consultar contraseñas del almacén de contraseñas del GNOME Keyring. (utiliza el obsoleto [libgnome-keyring](https://www.archlinux.org/packages/?name=libgnome-keyring))

	|| [gnome-keyring-query](https://aur.archlinux.org/packages/gnome-keyring-query/)

*   **gkeyring** — Consulta contraseñas desde la línea de órdenes. (utiliza el obsoleto [libgnome-keyring](https://www.archlinux.org/packages/?name=libgnome-keyring))

	[https://github.com/kparal/gkeyring](https://github.com/kparal/gkeyring) || [gkeyring](https://aur.archlinux.org/packages/gkeyring/), [gkeyring-git](https://aur.archlinux.org/packages/gkeyring-git/)

## Administrar utilizando la GUI

Puede administrar los contenidos de GNOME Keyring utilizando Seahorse. [Instálelo](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") con el paquete [seahorse](https://www.archlinux.org/packages/?name=seahorse).

Es posible dejar la contraseña de GNOME keyring en blanco o cambiarla. En Seahorse, en el menú desplegable "Ver", seleccione "Por llavero". En la pestaña Contraseñas, pulse con el botón derecho en "Contraseñas: iniciar sesión" y seleccione "Cambiar contraseña". Introduzca la contraseña anterior y deje vacía la nueva contraseña. Se le advertirá sobre el uso de almacenamiento no cifrado; continúe presionando "Usar almacenamiento no seguro".

## Utilizando el llavero fuera de GNOME

### Sin un gestor de pantalla

#### Inicio de sesión automático

Si está utilizando el inicio de sesión automático, puede desactivar el gestor de claves configurando una contraseña en blanco en el llavero de inicio de sesión.

**Nota:** En este caso las contraseñas se almacenan sin cifrar.

#### Inicio de sesión de consola

Cuando se utiliza el inicio de sesión basado en la consola, el demonio del llavero puede iniciarse mediante [PAM](/index.php/PAM "PAM") o [xinitrc](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)"). PAM también puede desbloquear el llavero automáticamente al iniciar sesión.

##### Método PAM

Inicie gnome-keyring-daemon desde `/etc/pam.d/login`:

Añada `auth optional pam_gnome_keyring.so` al final de la sección `auth` y `session optional pam_gnome_keyring.so auto_start` al final de la sección `session`.

 `/etc/pam.d/login` 
```
#%PAM-1.0

auth       required     pam_securetty.so
auth       requisite    pam_nologin.so
auth       include      system-local-login
auth       optional     pam_gnome_keyring.so
account    include      system-local-login
session    include      system-local-login
session    optional     pam_gnome_keyring.so auto_start
```

Para [SDDM](/index.php/SDDM "SDDM"), edite en su lugar el archivo de configuración `/etc/pam.d/sddm`.

A continuación, para [GDM](/index.php/GDM_(Espa%C3%B1ol) "GDM (Español)"), añada `password optional pam_gnome_keyring.so` al final de `/etc/pam.d/passwd`.

 `/etc/pam.d/passwd` 
```
#%PAM-1.0

#password	required	pam_cracklib.so difok=2 minlen=8 dcredit=2 ocredit=2 retry=3
#password	required	pam_unix.so sha512 shadow use_authtok
password	required	pam_unix.so sha512 shadow nullok
password	optional	pam_gnome_keyring.so
```

**Nota:**

*   Para utilizar el desbloqueo automático, se debe configurar la misma contraseña para la cuenta de usuario y el llavero.
*   Aún necesitarás el código de abajo en `~/.xinitrc` Para exportar las variables de entorno requeridas.

##### Método xinitrc

Inicie gnome-keyring-daemon desde [xinitrc](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)"):

 `~/.xinitrc` 
```
eval $(/usr/bin/gnome-keyring-daemon --start --components=pkcs11,secrets,ssh)
export SSH_AUTH_SOCK

```

Véase [Xfce#SSH agents](/index.php/Xfce#SSH_agents "Xfce") para utilizarlo en Xfce.

Si utiliza [i3](/index.php/I3 "I3") y ssh no está mostrando la solicitud de contraseña, dando el siguiente error

```
sign_and_send_pubkey: signing failed: agent refused operation
Permission denied (publickey).

```

necesita añadir la variable de entorno DISPLAY a dbus-daemon en su .xinitrc, tal que así:

 `~/.xinitrc` 
```
dbus-update-activation-environment --systemd DISPLAY
eval $(/usr/bin/gnome-keyring-daemon --start --components=pkcs11,secrets,ssh)
export SSH_AUTH_SOCK

...
exec i3

```

### Con un gestor de pantalla

Cuando se utiliza un gestor de pantalla, el llavero funciona de manera inmediata para la mayoría de los casos. Los siguientes gestores de pantalla desbloquean automáticamente el llavero una vez que inicie sesión:

*   [GDM](/index.php/GDM_(Espa%C3%B1ol) "GDM (Español)")
*   [LightDM](/index.php/LightDM_(Espa%C3%B1ol) "LightDM (Español)")
*   [LXDM](/index.php/LXDM "LXDM")
*   [SDDM](/index.php/SDDM "SDDM")

En GDM y LightDM, advierta que el llavero [debe ser](https://wiki.gnome.org/Projects/GnomeKeyring/Pam) nombrado como *login* para ser desbloqueado automáticamente.

Para activar el llavero para las aplicaciones que se ejecutan a través del terminal, como SSH, añada lo siguiente a su `~/.bash_profile`, `~/.zshenv`, o similar:

 `~/.bash_profile` 
```
if [ -n "$DESKTOP_SESSION" ];then
    eval $(gnome-keyring-daemon --start)
    export SSH_AUTH_SOCK
fi
```

## SSH keys

To add your SSH key:

```
$ ssh-add ~/.ssh/id_rsa
Enter passphrase for /home/mith/.ssh/id_rsa:

```

To list automatically loaded keys:

```
$ ssh-add -L

```

To disable all keys;

```
$ ssh-add -D

```

Now when you connect to a server, the key will be found and a dialog will popup asking you for the passphrase. It has an option to automatically unlock the key when you log in. If you check this, you will not need to enter your passphrase again!

Alternatively, to permanently save the a passphrase in the keyring, use ssh-askpass from package [seahorse](https://www.archlinux.org/packages/?name=seahorse):

```
/usr/lib/seahorse/ssh-askpass my_key

```

**Note:** You have to have the corresponding `.pub` file in the same directory as the private key (`~/.ssh/id_rsa.pub` in the example). Also, make sure that the public key is the file name of the private key plus `.pub` (for example, `my_key.pub`).

### Start SSH and Secrets components of keyring daemon

If you are starting Gnome Keyring with a display manager or the Pam method described above and you are NOT using Gnome, Unity or Mate as your desktop you may find that the SSH and Secrets components are not being started automatically. You can fix this by copying the desktop files gnome-keyring-ssh.desktop and gnome-keyring-secrets.desktop from /etc/xdg/autostart/ to ~/.config/autostart/ and deleting the OnlyShowIn line.

```
$ cp /etc/xdg/autostart/{gnome-keyring-secrets.desktop,gnome-keyring-ssh.desktop} ~/.config/autostart/
$ sed -i '/^OnlyShowIn.*$/d' ~/.config/autostart/gnome-keyring-secrets.desktop
$ sed -i '/^OnlyShowIn.*$/d' ~/.config/autostart/gnome-keyring-ssh.desktop

```

### Disable keyring daemon components

If you wish to run an alternative SSH agent (e.g. [ssh-agent](/index.php/SSH_keys#ssh-agent "SSH keys") or [gpg-agent](/index.php/GnuPG#gpg-agent "GnuPG"), you need to disable the `ssh` component of GNOME Keyring. To do so in an account-local way, copy `/etc/xdg/autostart/gnome-keyring-ssh.desktop` to `~/.config/autostart` and then append the line `Hidden=true` to the copied file. Then log out.

**Note:** In case you use [GNOME](/index.php/GNOME "GNOME") 3.24 or older on [Wayland](/index.php/Wayland "Wayland"), gnome-shell will overwrite `SSH_AUTH_SOCK` to point to gnome-keyring regardless if it is running or not. To prevent this, you need to set the environment variable GSM_SKIP_SSH_AGENT_WORKAROUND before gnome-shell is started. One way to do this is to add the line `GSM_SKIP_SSH_AGENT_WORKAROUND DEFAULT=1` to `~/.pam_environment`.

## Tips and tricks

### Integration with applications

*   [Firefox](/index.php/Firefox#KDE.2FGNOME_integration "Firefox")

### Flushing passphrases

```
gnome-keyring-daemon -r -d

```

This command starts gnome-keyring-daemon, shutting down previously running instances.

### Git integration

The GNOME keyring is useful in conjuction with [Git](/index.php/Git "Git") when you are pushing over HTTPS.

Install the [libsecret](https://www.archlinux.org/packages/?name=libsecret) package.

Set Git up to use the helper:

```
$ git config --global credential.helper /usr/lib/git-core/git-credential-libsecret

```

Next time you do a *git push*, you are asked to unlock your keyring, if not unlocked already.

## Troubleshooting

### Passwords are not remembered

If you get a password prompt every time you login, and you find that passwords are not saved, you might need to create/set a default keyring.

Ensure that the [seahorse](https://www.archlinux.org/packages/?name=seahorse) package is installed, open it ("Passwords and Keys" in system settings) and select *View* > *By Keyring* If there is no keyring in the left column (it will be marked with a lock icon), go to *File* > *New* > *Password Keyring* and give it a name. You will be asked to enter a password. If you do not give the keyring a password it will be unlocked automatically, even when using autologin, but passwords will not be stored securely. Finally, right-click on the keyring you just created and select "Set as default".

### Resetting the keyring

If you get the error "The password you use to login to your computer no longer matches that of your login keyring", you can simply reset your gnome keyring.

Remove "login.keyring" and "user.keystore" from */home/{username}/.local/share/keyrings/*. After removing the files, simply log out and log in again. Obviously, this will remove your saved keys.

## Known issues

### Cannot handle ECDSA and Ed25519 keys

As of January 2018, GNOME Keyring doesn't handle ECDSA[[1]](https://bugzilla.gnome.org/show_bug.cgi?id=641082) nor Ed25519[[2]](https://bugzilla.gnome.org/show_bug.cgi?id=723274) keys. You can turn to other [SSH agents](/index.php/SSH_keys#SSH_agents "SSH keys") if you need support for those.

**Note:** As of GNOME 3.28, gnome-keyring replaced its SSH agent implementation with a wrapper around the ssh-agent tool that comes with [openssh](https://www.archlinux.org/packages/?name=openssh) [[3]](https://bugzilla.gnome.org/show_bug.cgi?id=775981). As a result, any type of key supported by the upstream ssh-agent is now also supported by gnome-keyring, including ECDSA and Ed25519 keys.

## Véase también

*   [Wiki de GNOME](https://wiki.gnome.org/action/show/Projects/GnomeKeyring)