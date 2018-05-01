[tint2](https://gitlab.com/o9000/tint2) es un panel/barra de tareas creado para Linux. Es descrito por sus desarroladores como "simple, ligero y discreto". Tiene gran flexibilidad para ser configurado y ofrece bastantes posibilidades. Convirtiendolo en una buena idea en combinacion con gestores de ventanas que no tienen paneles, como [Openbox](/index.php/Openbox_(Espa%C3%B1ol) "Openbox (Español)").

## Contents

*   [1 Características](#Caracter.C3.ADsticas)
*   [2 Instalación](#Instalaci.C3.B3n)
*   [3 Ejecutando Tint](#Ejecutando_Tint)
*   [4 Otros Recursos](#Otros_Recursos)

### Características

*   background button-border effect (see screenshot)
*   font shadow
*   option to center tasks
*   option to change panel width/height
*   tasks do now squeeze (more or less) when they hit panel edge
*   middle-click closes window
*   left-click toggles shade

## Instalación

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [tint2](https://www.archlinux.org/packages/?name=tint2) disponible desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

El archivo de configuración sera creado con la primera ejecución de tint2 en `~/.config/tint2/tint2rc`.

## Ejecutando Tint

Ahora puede iniciar Tint como cualquier otra aplicación (Por ejempo: Alt+F2 -> tint). Para ejecutarlo al inicio, puede agregarlo en el archivo ~/.xinitrc, o en ~/.config/openbox/autostart.sh, por ejemplo:

```
xscreensaver -no-splash &
eval `cat $HOME/.fehbg` &
conky &
visibility &
***tint &***
exec openbox-session

```

## Otros Recursos

[Tint 0.6 Documentation (PDF)](http://tint2.googlecode.com/files/tint-0.6.pdf)

[Tint2 0.7 Documentation (PDF)](http://tint2.googlecode.com/files/tint2-0.7.pdf)