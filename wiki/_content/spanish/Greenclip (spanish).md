**Estado de la traducción**
Este artículo es una traducción de [Greenclip](/index.php/Greenclip "Greenclip"), revisada por última vez el **2019-01-18**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Greenclip&diff=0&oldid=563814) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Greenclip](https://github.com/erebe/greenclip) es un [gestor de portapapeles](/index.php/Clipboard_(Espa%C3%B1ol)#Gestores "Clipboard (Español)") sencillo diseñado para integrarse con [rofi](/index.php/Rofi "Rofi") y escrito en Haskell.

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [rofi-greenclip](https://aur.archlinux.org/packages/rofi-greenclip/) del [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)").

Para integrar el inicio del daemon durante el arranque es posible crear un servicio:

 `/usr/lib/systemd/user/greenclip.service` 
```
[Unit]
Description=Start greenclip daemon
After=display-manager.service

[Service]
ExecStart=/usr/bin/greenclip daemon
Restart=always

[Install]
WantedBy=default.target

```

Después, [active](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)") el servicio para que se inicie durante el arranque:

`systemctl --user enable greenclip.service`

## Utilización

1.  Genere el daemon con `/usr/bin/greenclip daemon` o [inicie/active](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)") el servicio con `systemctl --user start greenclip.service`
2.  Mostrar las entradas como una lista dentro de [rofi](/index.php/Rofi "Rofi") usando: `rofi -modi "clipboard:greenclip print" -show clipboard -run-command '{cmd}'`
3.  La entrada que ha seleccionado estará ahora en su [portapapeles](/index.php/Clipboard_(Espa%C3%B1ol) "Clipboard (Español)")
4.  El archivo de configuración se encuentra en `~/.config/greenclip.cfg`
5.  Para borrar todo el historial del portapapeles, ejecute `greenclip clear`

## Ejemplo de configuración

 `~/.config/greenclip.cfg` 
```
Config {
 maxHistoryLength = 250,
 historyPath = "~/.cache/greenclip.history",
 staticHistoryPath = "~/.cache/greenclip.staticHistory",
 imageCachePath = "/tmp/",
 usePrimarySelectionAsInput = False,
 blacklistedApps = [],
 trimSpaceFromSelection = True
}

```