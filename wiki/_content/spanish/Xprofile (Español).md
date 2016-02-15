`~/.xprofile` y `/etc/xprofile` permiten ejecutar comandos al comienzo de la sesión de usuario de X, antes de que se inicie el [gestor de ventanas](/index.php/Window_Manager_(Espa%C3%B1ol) "Window Manager (Español)"). Por lo tanto, no se pueden utilizar para iniciar aplicaciones basadas ​​en ventanas. Véase para ello [Autostarting (Español)#Gráfica](/index.php/Autostarting_(Espa%C3%B1ol)#Gr.C3.A1fica "Autostarting (Español)").

`xprofile` es similar a [xinitrc](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)") (`~/.xinitrc` y `/etc/X11/xinit/xinitrc.d/`).

## Compatibilidad

xprofiles se proveen de forma nativa por:

*   [GDM](/index.php/GDM "GDM") (`/etc/gdm/Xsession`)
*   [KDM](/index.php/KDM "KDM") (`/usr/share/config/kdm/Xsession`)
*   [LightDM](/index.php/LightDM "LightDM") (`/etc/lightdm/Xsession`)
*   [LXDM](/index.php/LXDM "LXDM") (`/etc/lxdm/Xsession`)

### Hacerlo compatible con xinit

Es posible hacer que los archivos xprofiles sean compatibles con estos programas:

*   `startx`
*   `xinit`
*   [XDM](/index.php/XDM "XDM")
*   [SLiM](/index.php/SLiM "SLiM")
*   cualquier otro [Display Manager (Español)](/index.php/Display_Manager_(Espa%C3%B1ol) "Display Manager (Español)") que utilice los archivos `~/.xsession` o `~/.xinitrc`

Todos ellos ejecutan, directa o indirectamente, `~/.[xinitrc (Español)](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)")` (normalmente se obtienen de `/etc/skel/.xinitrc`), o de `/etc/X11/xinit/xinitrc` si no existe aquél. Es por ello que tenemos contenidos de xprofiles en esos archivos.

 `~/.xinitrc and /etc/X11/xinit/xinitrc and /etc/skel/.xinitrc` 

```
#!/bin/sh

# Asegúrese de que esto se coloca antes de la orden 'exec' o no se ejecutará.
[ -f /etc/xprofile ] && source /etc/xprofile
[ -f ~/.xprofile ] && source ~/.xprofile

...

```