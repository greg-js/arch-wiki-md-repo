dmenu es un lanzador de menú rápido, dinámico y ligero para X. Puede compararse con 'Quicksilver' en OS X, o con 'Launchy' en Windows. Con la pulsación de un tecla, aparece el menu dmenu, permitiéndole teclear el nombre del programa que desse arrancar.

# Instalación

Instalar dmenu es sencillo:

```
pacman -S dmenu

```

Una vez instalado, necesitará crear un guión de shell para ejecutarlo. El siguiente guión presenta una configuración habitual:

```
#!/bin/sh
`dmenu_path | dmenu -fn '-*-terminus-*-r-normal-*-*-120-*-*-*-*-iso8859-*' -nb '#000000' -nf '#FFFFFF' -sb '#0066ff'` && eval "exec $exe"

```

Grabe el guión en algún sitio (~/bin es una buena elección) y haga que sea ejecutable.

# Configuración

Ahora, necesitará ligar dicho guión a una combinación de teclas. Esto puede hacerse bien via su gestor de ventanas o configuración de su entorno de escritorio, bien con un programa tal como xbindkeys. Vea el artículo [Hotkeys](/index.php/Hotkeys "Hotkeys") para obtener más información.

# Recursos adicionales

*   [dmenu](http://www.suckless.org/wiki/tools/xlib) - El sitio web oficial de dmenu