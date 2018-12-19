**Estado de la traducción**
Este artículo es una traducción de [GNOME/Keyring](/index.php/GNOME/Keyring "GNOME/Keyring"), revisada por última vez el **2018-12-16**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=GNOME/Keyring&diff=0&oldid=559215) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

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
*   [4 Claves SSH](#Claves_SSH)
    *   [4.1 Iniciar los componentes SSH y Secrets del demonio del llavero](#Iniciar_los_componentes_SSH_y_Secrets_del_demonio_del_llavero)
    *   [4.2 Desactivar los componentes del demonio del llavero](#Desactivar_los_componentes_del_demonio_del_llavero)
*   [5 Consejos y trucos](#Consejos_y_trucos)
    *   [5.1 Integración con aplicaciones](#Integración_con_aplicaciones)
    *   [5.2 Limpiando frases de contraseña](#Limpiando_frases_de_contraseña)
    *   [5.3 Integración con Git](#Integración_con_Git)
*   [6 Solución de problemas](#Solución_de_problemas)
    *   [6.1 Las contraseñas no son recordadas](#Las_contraseñas_no_son_recordadas)
    *   [6.2 Restableciendo el llavero](#Restableciendo_el_llavero)
*   [7 Problemas conocidos](#Problemas_conocidos)
    *   [7.1 No se pueden manejar claves ECDSA y Ed25519](#No_se_pueden_manejar_claves_ECDSA_y_Ed25519)
*   [8 Véase también](#Véase_también)

## Instalación

Cuando se utiliza GNOME, [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring) se instala automáticamente como parte del grupo [gnome](https://www.archlinux.org/groups/x86_64/gnome/). De lo contrario [instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring). Instale [libsecret](https://www.archlinux.org/packages/?name=libsecret) para permitir que las aplicaciones usen sus llaveros. [libgnome-keyring](https://www.archlinux.org/packages/?name=libgnome-keyring) está en desuso, sin embargo, algunas aplicaciones pueden requerirlo.

Las utilidades adicionales relacionadas con el llavero de GNOME incluyen:

*   **secret-tool** — Acceso al llavero de GNOME (y cualquier otro servicio que implemente la [API del servicio DBus Secret](http://standards.freedesktop.org/secret-service/)) desde la línea de órdenes.

	[https://wiki.gnome.org/Projects/Libsecret](https://wiki.gnome.org/Projects/Libsecret) || [libsecret](https://www.archlinux.org/packages/?name=libsecret)

*   **gnome-keyring-query** — Proporciona una herramienta simple de línea de órdenes para consultar contraseñas del almacén de contraseñas del llavero de GNOME. (utiliza el obsoleto [libgnome-keyring](https://www.archlinux.org/packages/?name=libgnome-keyring))

	|| [gnome-keyring-query](https://aur.archlinux.org/packages/gnome-keyring-query/)

*   **gkeyring** — Consulta contraseñas desde la línea de órdenes. (utiliza el obsoleto [libgnome-keyring](https://www.archlinux.org/packages/?name=libgnome-keyring))

	[https://github.com/kparal/gkeyring](https://github.com/kparal/gkeyring) || [gkeyring](https://aur.archlinux.org/packages/gkeyring/), [gkeyring-git](https://aur.archlinux.org/packages/gkeyring-git/)

## Administrar utilizando la GUI

Puede administrar los contenidos del llavero de GNOME utilizando Seahorse. [Instálelo](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") con el paquete [seahorse](https://www.archlinux.org/packages/?name=seahorse).

Es posible dejar la contraseña del llavero de GNOME en blanco o cambiarla. En Seahorse, en el menú desplegable "Ver", seleccione "Por llavero". En la pestaña Contraseñas, pulse con el botón derecho en "Contraseñas: iniciar sesión" y seleccione "Cambiar contraseña". Introduzca la contraseña anterior y deje vacía la nueva contraseña. Se le advertirá sobre el uso de almacenamiento no cifrado; continúe presionando "Usar almacenamiento no seguro".

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

## Claves SSH

Para añadir su clave SSH:

```
$ ssh-add ~/.ssh/id_rsa
Enter passphrase for /home/mith/.ssh/id_rsa:

```

Para listar las claves cargadas automáticamente:

```
$ ssh-add -L

```

Para desactivar todas las claves:

```
$ ssh-add -D

```

Ahora, cuando se conecte a un servidor, se encontrará la clave y aparecerá un cuadro de diálogo que le pedirá la contraseña. Tiene una opción para desbloquear automáticamente la clave cuando inicie sesión. ¡Si marca esto, no necesitará ingresar su contraseña nuevamente!

Alternativamente, para guardar de forma permanente la frase de la contraseña en el llavero, utilice ssh-askpass del paquete [seahorse](https://www.archlinux.org/packages/?name=seahorse):

```
/usr/lib/seahorse/ssh-askpass my_key

```

**Nota:** Debe tener el archivo `.pub` correspondiente en el mismo directorio que la clave privada (`~/.ssh/id_rsa.pub` en el ejemplo). Además, asegúrese de que la clave pública sea el nombre del archivo de la clave privada más `.pub` (por ejemplo, `mi_clave.pub`).

### Iniciar los componentes SSH y Secrets del demonio del llavero

Si está iniciando el llavero de Gnome con un gestor de pantalla o el método Pam descrito anteriormente y NO está utilizando Gnome, Unity o Mate como su escritorio, es posible que los componentes de SSH y Secrets no se inicien automáticamente. Puede solucionar esto copiando los archivos de escritorio gnome-keyring-ssh.desktop y gnome-keyring-secrets.desktop desde /etc/xdg/autostart/ a ~/.config/autostart/ y eliminando la línea OnlyShowIn.

```
$ cp /etc/xdg/autostart/{gnome-keyring-secrets.desktop,gnome-keyring-ssh.desktop} ~/.config/autostart/
$ sed -i '/^OnlyShowIn.*$/d' ~/.config/autostart/gnome-keyring-secrets.desktop
$ sed -i '/^OnlyShowIn.*$/d' ~/.config/autostart/gnome-keyring-ssh.desktop

```

### Desactivar los componentes del demonio del llavero

Si desea ejecutar un agente SSH alternativo (por ejemplo, [ssh-agent](/index.php/SSH_keys_(Espa%C3%B1ol)#ssh-agent "SSH keys (Español)") o [gpg-agent](/index.php/GnuPG_(Espa%C3%B1ol)#gpg-agent "GnuPG (Español)"), debe desactivar el componente `ssh` del llavero de GNOME. Para hacerlo de una manera local en una cuenta, copie `/etc/xdg/autostart/gnome-keyring-ssh.desktop` a `~/.config/autostart` y luego añada la línea `Hidden=true` al archivo copiado. A continuación, cierre la sesión.

**Nota:** En caso de que utilice [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)") 3.24 o anterior en [Wayland](/index.php/Wayland_(Espa%C3%B1ol) "Wayland (Español)"), gnome-shell sobrescribirá `SSH_AUTH_SOCK` para apuntar a gnome-keyring sin importar si se está ejecutando o no. Para evitar esto, debe configurar la variable de entorno GSM_SKIP_SSH_AGENT_WORKAROUND antes de iniciar gnome-shell. Una forma de hacer esto es añadiendo la línea `GSM_SKIP_SSH_AGENT_WORKAROUND DEFAULT=1` a `~/.pam_environment`.

## Consejos y trucos

### Integración con aplicaciones

*   [Firefox](/index.php/Firefox_(Espa%C3%B1ol)#Integración_con_Gnome "Firefox (Español)")

### Limpiando frases de contraseña

```
gnome-keyring-daemon -r -d

```

Esta orden inicia gnome-keyring-daemon, cerrando instancias previamente en ejecución.

### Integración con Git

El llavero de GNOME es útil en conjunción con [Git](/index.php/Git_(Espa%C3%B1ol) "Git (Español)") cuando se utiliza sobre HTTPS.

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [libsecret](https://www.archlinux.org/packages/?name=libsecret).

Configure Git para utilizar el ayudante:

```
$ git config --global credential.helper /usr/lib/git-core/git-credential-libsecret

```

La próxima vez que haga un *git push*, se le pedirá que desbloquee su llavero, si no lo está ya.

## Solución de problemas

### Las contraseñas no son recordadas

Si recibe una solicitud de contraseña cada vez que inicia sesión y descubre que las contraseñas no se guardan, es posible que deba crear/configurar un llavero predeterminado.

Asegúrese de que el paquete [seahorse](https://www.archlinux.org/packages/?name=seahorse) esté [instalado](/index.php/Install_(Espa%C3%B1ol) "Install (Español)"), ábralo ("Contraseñas y claves" en la configuración del sistema) y seleccione *Ver* > *Por llavero*.

Si no hay un llavero en la columna izquierda (se marcará con un icono de candado), vaya a *Archivo* > *Nuevo* > *Llavero de contraseña* y asígnele un nombre. Se le pedirá que introduzca una contraseña. Si no le asigna una contraseña al llavero, se desbloqueará automáticamente, incluso cuando se utilice el inicio de sesión automático, pero las contraseñas no se almacenarán de forma segura. Finalmente, pulse con el botón derecho en el llavero que acaba de crear y seleccione "Establecer como predeterminado".

### Restableciendo el llavero

Si aparece el error "La contraseña que utiliza para iniciar sesión en su computadora ya no coincide con la de su llavero de inicio de sesión" *("The password you use to login to your computer no longer matches that of your login keyring" en inglés)*, puede simplemente restablecer su llavero de gnome.

Elimine "login.keyring" y "user.keystore" de */home/{usuario}/.local/share/keyrings/*. Después de eliminar los archivos, simplemente cierre la sesión y vuelva a iniciarla. Obviamente, esto eliminará las claves guardadas.

## Problemas conocidos

### No se pueden manejar claves ECDSA y Ed25519

A partir de enero de 2018, el llavero de GNOME no maneja claves ECDSA[[1]](https://bugzilla.gnome.org/show_bug.cgi?id=641082) ni Ed25519[[2]](https://bugzilla.gnome.org/show_bug.cgi?id=723274). Puede recurrir a otros [agentes SSH](/index.php/SSH_keys_(Espa%C3%B1ol)#Agentes_de_SSH "SSH keys (Español)") si necesita soporte para ellos.

**Nota:** A partir de GNOME 3.28, gnome-keyring reemplazó su implementación del agente SSH con un envoltorio alrededor de la herramienta ssh-agent que viene con [openssh](https://www.archlinux.org/packages/?name=openssh) [[3]](https://bugzilla.gnome.org/show_bug.cgi?id=775981). Como resultado, cualquier tipo de clave compatible con ssh-agent ahora también es compatible con gnome-keyring, incluidas las claves ECDSA y Ed25519.

## Véase también

*   [Wiki de GNOME](https://wiki.gnome.org/action/show/Projects/GnomeKeyring)