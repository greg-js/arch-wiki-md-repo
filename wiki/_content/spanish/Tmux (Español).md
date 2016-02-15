Tmux es una terminal multiplexora del sistema BSD. Permite tener diferentes sesiones donde se ejecuten aplicaciones en una terminal o en una shell. Permite dividir la pantalla de manera horizontal o vertical para el uso de esta sesiones.

tmux utiliza un modelo cliente-servidor. El servidor tiene varias sesiones y cada ventana es una entidad independiente que puede ser libremente vinculado a otras sesiones. En cada sesión se podrán visualizar y aceptar la entrada de teclado de varios clientes.

Muy parecido a [screen](http://www.gnu.org/software/screen/), pero diferente. (¿Quien dijo que mejor?)

Para mas información en su [web oficial](http://tmux.sourceforge.net/)

## Instalación

```
# pacman -S tmux

```

## Configuración

Los archivos de configuración se encuentran en /usr/share/tmux/. Por defecto, la combinacion de teclas es: C-b (donde C- es la tecla de control [Ctrl])

A fin de tener una configuración «Que se comporte como screen», use el siguiente comando:

```
$ cp /usr/share/tmux/screen-keys.conf ~/.tmux.conf

```

Para ampliar más la configuración, puede consultar el manual de tmux

```
$ man tmux

```

Aqui una configuración sencilla:

```
# Mover las ventanas izquierda o derecha en la sesión
bind-key -n C-right next
bind-key -n C-left prev
# Nueva combinacion Ctrl + z + (Las teclas a continuación abajo)
set -g prefix C-z
# Desatamos la tecla predeterminada Ctrl + b y utilizamos la nueva combinación Ctrl + z + [tecla] 
unbind-key C-b
bind-key C-z send-prefix
# Nueva ventana
bind-key C-n new-window
# Dividir la ventana en forma horizontal
bind-key C-h split-window -h
# Dividir la ventana en forma vertical
bind-key C-v split-window -v
# Movernos al panel arriba
bind-key C-up select-pane -U
# Movernos al panel abajo
bind-key C-down select-pane -D
# Movernos al panel a la izquierda
bind-key C-left select-pane -L
# Movernos al panel a la derecha
bind-key C-right select-pane -R
# Ocultar la session para volver a entrar solo tipeamos en consola: tmux attach-session ó tmux attach
bind-key C-d detach
# Habilitar que el mouse selecciones los paneles
set-option -g mouse-select-pane on
set-option -g set-titles on
# Sin actividad visual
set -g visual-activity on
set -g visual-bell on
# Barra de estado
set-option -g status-utf8 on
set-option -g status-justify right
set-option -g status-bg black
set-option -g status-fg green
set-option -g status-interval 5
set-option -g status-left-length 30
set-option -g status-left '#[fg=magenta]» #[fg=blue,bold]#T#[default]'
set-option -g status-right '#[fg=cyan]»» #[fg=blue,bold] #[fg=magenta]%D %k:%M#[default]'
set-option -g visual-activity on
set-window-option -g monitor-activity on
set-window-option -g window-status-current-fg green
set-window-option -g clock-mode-colour white 
set-window-option -g clock-mode-style 24

```

## Ver más

*   [GNU Screen](https://wiki.archlinux.org/index.php/Screen_Tips)
*   [Tmux tutorial from OpenBSD FAQ](http://www.openbsd.org/faq/faq7.html#tmux)
*   [Tmux/Screen cheat sheet](http://www.dayid.org/os/notes/tm.html)