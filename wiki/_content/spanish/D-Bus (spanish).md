[D-Bus](https://en.wikipedia.org/wiki/es:D-Bus "wikipedia:es:D-Bus") es un sistema bus de mensajes que proporciona una manera fácil para la comunicación entre procesos. Se trata de un demonio, que se puede ejecutar tanto en todo el sistema como para cada sesión de usuario, y un conjunto de bibliotecas que permiten a las aplicaciones utilizar D-Bus.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Iniciar la sesión de usuario](#Iniciar_la_sesi.C3.B3n_de_usuario)
*   [3 Depurador de errores](#Depurador_de_errores)
*   [4 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalación

Debido a que [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") depende de [dbus](https://www.archlinux.org/packages/?name=dbus), D-Bus es habilitado automáticamente cuando se usa systemd.

## Iniciar la sesión de usuario

[gnome-session](/index.php/GNOME "GNOME"), [startkde](/index.php/KDE "KDE") y [startxfce4](/index.php/Xfce "Xfce") iniciarán automáticamente una sesión de D-Bus si no se está ejecutando. El archivo `~/.xinitrc` hará lo mismo.

## Depurador de errores

[d-feet](https://www.archlinux.org/packages/?name=d-feet) es una cómoda utilidad gráfica para depurar errores de D-Bus. D-Feet se pueden utilizar para inspeccionar las interfaces D-Bus al ejecutar programas e invocar métodos en otras interfaces. Véase [su página principal](https://wiki.gnome.org/DFeet) para más información.

## Véase también

*   [Página de D-Bus en freedesktop.org](http://www.freedesktop.org/wiki/Software/dbus)
*   [Introducción a D-Bus](http://www.freedesktop.org/wiki/IntroductionToDBus) en freedesktop.org