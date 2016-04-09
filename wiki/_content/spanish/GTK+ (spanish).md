# Aplicaciones GTK1

Si utiliza aplicaciones GTK1 antiguas (como xmms), probablemente ya sabe que no tienen buen aspecto. Esto se debe a que usan por defecto un tema feo. Para cambiarlo, necesita:

1.  descargar e instalar algún tema bonito
2.  cambiar el tema

Hay algunos temas bonitos en [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)"): [gtk-smooth-engine](https://aur.archlinux.org/packages/gtk-smooth-engine/) y [gtk-theme-switch-ex](https://aur.archlinux.org/packages/gtk-theme-switch-ex/).

Ejecútelo entonces con la orden 'switch'. Eso es todo. ¿No están mejor ahora? :)

# Aplicaciones GTK2

Para las aplicaciones GTK2 (p.ej. pidgin) puede hacer lo mismo con 'gtk-theme-switch2' o 'gtk2_prefs' (que es la que yo uso y recomiendo). Está además 'lxappearance', una herramienta independiente de configuración del Proyecto LXDE. Esta no requiere ninguna otra parte del entorno LXDE. De manera que, una vez que se haya decidido haga:

```
# pacman -S gtk-theme-switch2

```

o:

```
# pacman -S gtk2_prefs

```

o bien:

```
# pacman -S lxappearance

```

Probablemente quiera instalar también algunos temas:

```
# pacman -S gtk-engines

```

Ahora ejecute bien 'switch2' o 'gtk2_prefs', dependiendo de cual eligió antes y cambie el tema por uno de su gusto.

Si quiere cambiar el tema de los iconos de las aplicaciones GTK2, tiene que modificar entonces el archivo ~/.gtkrc-2.0, añadiendo la siguiente línea (aquí se selecciona el tema de iconos Tango):

```
gtk-icon-theme-name = "Tango"
...más configuración para gtk2 ...

```

# GTK con QT

Si tiene en su escritorio aplicaciones GTK y QT (KDE) sabrá que su aspecto no enaja bien. Si desea hacer que coincidan los estilos GTK y QT lea por favor [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications").