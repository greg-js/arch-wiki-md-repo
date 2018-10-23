Artículos relacionados

*   [Display Manager (Español)](/index.php/Display_Manager_(Espa%C3%B1ol) "Display Manager (Español)")
*   [GNOME (Español)](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)")

De [GDM - GNOME Display Manager](http://projects.gnome.org/gdm/about.html):

	GDM, el gestor de pantallas de GNOME, es un pequeño programa que se ejecuta en segundo plano, dirige las sesiones de X, le presenta una pantalla de inicio de sesión y, luego, le impide el acceso hasta tanto le sea suministrada la contraseña. Hace casi prácticamente todo lo que desearía hacer con xdm, pero sin los problemas de este último. GDM no utiliza ningún código de xdm. Es compatible con XDMCP, y, de hecho, extiende XDMCP a aspectos a los que no llegaba xdm (pero sigue siendo compatible con XDMCP de xdm).

Los [gestores de pantallas](/index.php/Display_manager_(Espa%C3%B1ol) "Display manager (Español)") proporcionan a los usuarios de [X Window System](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)") un inicio de sesión gráfico.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
    *   [1.1 GDM como la pantalla de bienvenida predeterminada](#GDM_como_la_pantalla_de_bienvenida_predeterminada)
*   [2 Configuración](#Configuraci.C3.B3n)
    *   [2.1 GDM 3.10](#GDM_3.10)
        *   [2.1.1 Herramienta gráfica de configuración](#Herramienta_gr.C3.A1fica_de_configuraci.C3.B3n)
        *   [2.1.2 Cambiar el idioma](#Cambiar_el_idioma)
    *   [2.2 Configuración antigua](#Configuraci.C3.B3n_antigua)
    *   [2.3 Iniciar sesión automáticamente](#Iniciar_sesi.C3.B3n_autom.C3.A1ticamente)
    *   [2.4 Iniciar sesión sin contraseña](#Iniciar_sesi.C3.B3n_sin_contrase.C3.B1a)
    *   [2.5 Cerrar sin contraseña](#Cerrar_sin_contrase.C3.B1a)
    *   [2.6 Cambiar la sesión predeterminada de GDM](#Cambiar_la_sesi.C3.B3n_predeterminada_de_GDM)
    *   [2.7 GDM antiguo](#GDM_antiguo)
*   [3 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [3.1 GDM falla al registrase](#GDM_falla_al_registrase)
    *   [3.2 gconf-sanity-check-2 sale con el estado 256](#gconf-sanity-check-2_sale_con_el_estado_256)
    *   [3.3 Iniciar sesión como root en GDM](#Iniciar_sesi.C3.B3n_como_root_en_GDM)
    *   [3.4 GDM utiliza por defecto la distribución del teclado de Estados Unidos](#GDM_utiliza_por_defecto_la_distribuci.C3.B3n_del_teclado_de_Estados_Unidos)
        *   [3.4.1 GDM 2.x](#GDM_2.x)
        *   [3.4.2 GDM 3.x](#GDM_3.x)
        *   [3.4.3 GDM no se carga después de intentar configurar el inicio de sesión automático](#GDM_no_se_carga_despu.C3.A9s_de_intentar_configurar_el_inicio_de_sesi.C3.B3n_autom.C3.A1tico)
        *   [3.4.4 GDM no arranca después de actualizar a la versión 3.8 si se utiliza una tarjeta gráfica Intel](#GDM_no_arranca_despu.C3.A9s_de_actualizar_a_la_versi.C3.B3n_3.8_si_se_utiliza_una_tarjeta_gr.C3.A1fica_Intel)

## Instalación

GDM (que también forma parte de [gnome](https://www.archlinux.org/groups/x86_64/gnome/)) puede ser [instalado](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") con el paquete [gdm](https://www.archlinux.org/packages/?name=gdm), disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

### GDM como la pantalla de bienvenida predeterminada

Para que el método gráfico predeterminado de acceso al sistema sea GDM, utilice el archivo de servicio suministrado para systemd, `gdm.service`. Basta con ejecutar la siguiente orden, una vez, para hacer que GDM se inicie en el arranque:

```
# systemctl enable gdm.service

```

Los argumentos que se pasan al servidor X por `~/.xinitrc` (como los de `xmodmap` y `xsetroot`) también pueden ser añadidos a través de [xprofile](/index.php/Xprofile_(Espa%C3%B1ol) "Xprofile (Español)"):

 `~/.xprofile` 
```
#!/bin/sh

#
# ~/.xprofile
#
# Ejecutado por gdm al iniciar la sesión
#

xmodmap -e "pointer=1 2 3 6 7 4 5" # Establece los botones del ratón de forma correcta
xsetroot -solid black              # Establece el fondo en negro

```

## Configuración

### GDM 3.10

#### Herramienta gráfica de configuración

Puede [instalar](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") [gdm3setup](https://aur.archlinux.org/packages/gdm3setup/) desde AUR para configurar GDM. Se le permitirá cambiar algunas opciones de configuración, como el tema, la conexión automática o el formato de fecha, etc.

Sin embargo, no tiene la opción de cambiar el idioma.

#### Cambiar el idioma

**Advertencia:** Esto podría no ser la manera oficial de cambiar el idioma de GDM, pero al parecer no hay documentación al respecto hasta la fecha (2.11.2013).

Para cambiar el idioma de GDM, edite el archivo `/var/lib/AccountsService/users/gdm` y cambie la línea «Language». Debería mostrar algo como lo que sigue:

 `/var/lib/AccountsService/users/gdm` 
```
[User]
Language=es_ES.UTF-8
XSession=
SystemAccount=true
```

Ahora solo queda reiniciar el equipo.

Una vez que hayamos reiniciado, si nos fijamos en el archivo `/var/lib/AccountsService/users/gdm` de nuevo, veremos que la línea Language está borrada. No obstante ello, el cambio del idioma establecido permanece para los próximos reinicios.

### Configuración antigua

Ya no se puede utilizar la orden *«gdmsetup»* para configurar GDM a partir de la versión 2.28\. La orden se ha eliminado, y se ha estandarizado GDM e integrado con el resto de GNOME.

Puede utilizar las siguientes instrucciones:

*   Para configurar permisos de acceso al servidor X: `# xhost +SI:localuser:gdm` 

*   Para cambiar el tema: `$ sudo -u gdm gnome-control-center` 

*   Para obtener más opciones de configuración: `$ sudo -u gdm gconf-editor` 

	y modifique las jerarquías siguientes:
```
/apps/gdm/simple-greeter
/desktop/gnome/interface
/desktop/gnome/background
```

Si estas órdenes fallan, mostrando un error (por ejemplo, `Cannot open display` - «No se puede abrir la pantalla») usted puede poner las dos ventanas cuando GDM comienza, agregándolas al inicio automático de GDM. Para ello, primero debe crear la entrada:

 `# cp -t /usr/share/gdm/autostart/LoginWindow/ /usr/share/applications/gnome-appearance-properties.desktop /usr/share/applications/gconf-editor.desktop` 

A continuación regrese a GDM, realice los cambios y vuelva a entrar. Cuando haya terminado y desee que la ventana se visualice, ejecute lo siguiente para detener la apertura de GDM:

 `# rm /usr/share/gdm/autostart/LoginWindow/gnome-appearance-properties.desktop /usr/share/gdm/autostart/LoginWindow/gconf-editor.desktop` 
**Nota:** Al utilizar el método registrar/configurar, puede ver los cambios mientras los está haciendo.

Para obtener más información y ajustes avanzados lea [esto](http://library.gnome.org/admin/gdm/stable/configuration.html.en).

### Iniciar sesión automáticamente

Para activar el ingreso automático con GDM, añada lo siguiente al archivo `/etc/gdm/custom.conf` (sustituya el *nombredeusuario* por el suyo):

 `/etc/gdm/custom.conf` 
```
[daemon]
# activar acceso automático para el usuario
AutomaticLogin=*nombredeusuario*
AutomaticLoginEnable=True
```

o, para demorar el ingreso automático:

 `/etc/gdm/custom.conf` 
```
[daemon]
# para acceder automáticamente con retardo
TimedLoginEnable=true
TimedLogin=*nombredeusuario*
TimedLoginDelay=1
```

### Iniciar sesión sin contraseña

Si desea omitir la solicitud de contraseña en GDM, basta con añadir la siguiente línea a `/etc/pam.d/gdm-password`:

```
auth sufficient pam_succeed_if.so user ingroup nopasswdlogin

```

Asegúrese de que esta línea va a la derecha **antes** de la línea `pam_unix.so` `auth`.

A continuación, agregue el grupo `nopasswdlogin` a su sistema. Véase [Users and Groups](/index.php/Users_and_groups_(Espa%C3%B1ol) "Users and groups (Español)") para conocer una descripción de los grupos y su gestión.

Ahora, agregue el usuario al grupo `nopasswdlogin` y entonces bastará hacer clic en el nombre de usuario para iniciar sesión.

**Advertencia:**

*   **No** haga esto con la cuenta de **root**.
*   Después de realizar esta operación, no será capaz de cambiar el tipo de sesión una vez iniciada sesión con GDM. Si desea cambiar el tipo de sesión por defecto, primero tendrá que eliminar su usuario del grupo `nopasswdlogin`.

### Cerrar sin contraseña

GDM usa polkit y logind para obtener los permisos para cerrar. Ello se puede hacer sin solicitar primero una contraseña configurando:

 `/etc/polkit-1/localauthority.conf.d/org.freedesktop.logind.policy` 
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE policyconfig PUBLIC
 "-//freedesktop//DTD PolicyKit Policy Configuration 1.0//EN"
 "[http://www.freedesktop.org/standards/PolicyKit/1.0/policyconfig.dtd](http://www.freedesktop.org/standards/PolicyKit/1.0/policyconfig.dtd)">

<policyconfig>

  <action id="org.freedesktop.login1.power-off-multiple-sessions">
    <description>Shutdown the system when multiple users are logged in</description>
    <message>System policy prevents shutting down the system when other users are logged in</message>
    <defaults>
      <allow_inactive>yes</allow_inactive>
      <allow_active>yes</allow_active>
    </defaults>
  </action>

</policyconfig>
```

Puede encontrar todas las opciones logind disponibles (por ejemplo, reinicio de múltiples sesiones) [aquí](http://www.freedesktop.org/wiki/Software/systemd/logind#Security).

### Cambiar la sesión predeterminada de GDM

Si desea cambiar la sesión de GDM por defecto, tiene que crear (o modificar) el archivo `~/.dmrc` [[1]](http://library.gnome.org/admin/gdm/stable/configuration.html.en#userconfig).

**Nota:** Esto está en función de cada usuario. Si desea cambiar el valor predeterminado para más de un usuario, tendrá que crear este archivo para cada usuario.

He aquí un ejemplo para establecer la sesión predeterminada para [Cinnamon](/index.php/Cinnamon "Cinnamon"):

 `~/.dmrc` 
```
[Desktop]
Session=cinnamon

```

### GDM antiguo

Si desea utilizar el antiguo GDM, que también cuenta con una herramienta para configurar sus opciones, compile e instale [gdm-old](https://aur.archlinux.org/packages/gdm-old/) desde [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)").

## Solución de problemas

### GDM falla al registrase

Si GDM se inicia correctamente en el arranque, para falla después de repetidos intentos al registrarse, pruebe a añadir esta línea a la sección daemon de `/etc/gdm/custom.conf`:

```
GdmXserverTimeout=60

```

### gconf-sanity-check-2 sale con el estado 256

Si GDM muestra un error acerca de `gconf-sanity-check-2`, compruebe los permisos en `/home` y `/etc/gconf/gconf.xml.system` (este último debe ser `755`). Si GDM está imprimiendo el mensaje, intente vaciar el home de gdm. Ejecute como root:

```
rm -rf /var/lib/gdm/.*

```

Si esto no ayuda, trate de establecer `/tmp` al propietario y los permisos para:

```
# chown -R root:root /tmp
# chmod 777 /tmp

```

### Iniciar sesión como root en GDM

No se recomienda iniciar sesión como root, pero si es necesario, puede editar `/etc/pam.d/gdm-password` y añadir la siguiente línea antes de la línea `auth required pam_deny.so`: `/etc/pam.d/gdm-password`

```
auth            sufficient      pam_succeed_if.so uid eq 0 quiet

```

El archivo debe quedar de un modo similar a esto: `/etc/pam.d/gdm-password`

```
...
auth            sufficient      pam_succeed_if.so uid eq 0 quiet
auth            sufficient      pam_succeed_if.so uid >= 1000 quiet
auth            required        pam_deny.so
...

```

Después de reiniciar GDM debería ser capaz de iniciar sesión como root.

### GDM utiliza por defecto la distribución del teclado de Estados Unidos

Problema: La distribución del teclado siempre cambia al de Estados Unidos; la distribución se restablece cuando un nuevo teclado se enchufa.

#### GDM 2.x

Solución: modifique el archivo `~/.dmrc`

 `~/.dmrc` 
```
[Desktop]
Language=es_ES.UTF-8   # cambiar a su lengua predeterminada
Layout=es   nodeadkeys # cambiar a su distribución de teclado
```

#### GDM 3.x

Solución: añada la siguiente línea a `/etc/X11/xorg.conf.d/10-evdev.conf`, para establecer la distribución del teclado español.

 `/etc/X11/xorg.conf.d/10-evdev.conf` 
```
Section "InputClass"
        Identifier      "evdev keyboard catchall"
        MatchIsKeyboard "on"
        MatchDevicePath "/dev/input/event*"
        Driver          "evdev"
        **Option          "XkbLayout" "es"**
EndSection
```

**Advertencia:** Añada la línea anterior a la sección `Section InputClass` de `**keyboard**`, no a una sección `pointer`.

#### GDM no se carga después de intentar configurar el inicio de sesión automático

Para resolver este problema, modifique `/etc/gdm/custom.conf` desde una TTY y comente las líneas «AutomaticLoginEnable» y «AutomaticLogin».

```
# GDM configuration storage

[daemon]

#AutomaticLoginEnable=True
#AutomaticLogin=nombredeusuario

[security]

[xdmcp]

[greeter]

[chooser]

[debug]
```

#### GDM no arranca después de actualizar a la versión 3.8 si se utiliza una tarjeta gráfica Intel

Para resolver este problema, es posible que tenga que establecer el método de aceleración a SNA. Para obtener más información, consulte el artículo de Intel sobre [cómo elegir el método de aceleración](/index.php/Intel_(Espa%C3%B1ol)#Elegir_el_m.C3.A9todo_de_aceleraci.C3.B3n "Intel (Español)").