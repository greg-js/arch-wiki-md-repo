E17 es la versión de desarrollo número 17 (DR17) del entorno de escritorio Enlightenment.

E17 está actualmente bajo profundo desarrollo, y aun está en las etapas pre-alfa. Aunque es muy reciente, E17 es ya bastante estable. Mucha gente lo utiliza como un entorno para el día a día.

Se publican diariamente nuevas versiones via CVS, aunque para facilitar la instalación se proporcionan también versiones periódicas ("snapshots"). A continuación se dan instrucciones sobre cómo instalar un "snapshot" de CVS desde los repositorios de la comunidad de Arch.

## Contents

*   [1 Instalando E17](#Instalando_E17)
    *   [1.1 Editando /etc/pacman.conf](#Editando_.2Fetc.2Fpacman.conf)
*   [2 Instalando temas](#Instalando_temas)
*   [3 Resolución de problemas](#Resoluci.C3.B3n_de_problemas)
*   [4 Enlaces externos](#Enlaces_externos)

## Instalando E17

*   Lo primero que debe hacer es editar el archivo /etc/pacman.conf y descomentar los repositorios extra quitando el símbolo de número (también "almohadilla" o "hash" en inglés) al comienzo dela línea en cuestión. Debería acabar con algo parecido a lo siguiente:

#### Editando /etc/pacman.conf

```
...
# Añada aquí sus servidores favoritos, se utilizarán en primer lugar
Include = /etc/pacman.d/extra
...

```

*   A continuación, ejecute 'pacman -Syu' para actualizar, usando ya los nuevos repositorios "extra"
*   Instale enlightenment17: 'pacman -S enlightenment17'

*   Si necesita una versión del paquete e17 que no esté (todavía) disponible en el repositorio [extra], vea si lo puede encontrar en el [AUR](https://aur.archlinux.org/).

Ahora está ya preparado para iniciar e17\. Puede hacer esto de varias maneras:

*   Añada una línea que ponga 'enlightenment_start' en su ~/.xinitrc
*   Inicie un gestor de control de entrada añadiendo 'entranced' al array de módulos en /etc/rc.conf
*   arranque el gestor de control de entrada utilizando la línea 'x:5:respawn:/usr/sbin/entranced --nodaemon >& /dev/null' en el archivo /etc/inittab

¡A disfrutarlo!

Nota : e17 es todavía software en estado alfa. Puede que en algún momento las cosas dejen de funcionar como se espera de ellas. Aunque todos los paquetes han sido probados antes de se añadidos al repositorio [extra], puede que las cosas dejen de funcionar en su sistema. Se le anima por tanto a conservar los paquetes de versiones previas en su computadora, permitiéndole si es necesario una desactualización.

Si encuentra algín comportamiento inesperado, hay algunas cosas que puede hacer.. Compruebe primero si se da dicho comportamiento en el tema por defecto. En segundo lugar elimine ~/.e (puede que quiera hacer una copia de respaldo antes de hacer esto). Si está seguro de haber encontrado un error informe directamente por favor al proveedor original del paquete. Si no está seguro de que haya un fallo en el software o en el paquete, informe de él en el [extra] bug tracker.

## Instalando temas

Hay disponibles más temas para personalizar la apariencia en [E17 Exchange](http://exchange.enlightenment.org). Asegúrese de visitar también [e17-stuff.org](http://www.e17-stuff.org), así como darle un vistazo al AUR.

Puede instalar los temas (que vienen en formato .edj) desde el cuadro de diálogo de configuración.

Puede cambiar también el tema para el sistema de herramientas etk (el que es utilizado por exhibit). Para cambiar de sistema de herramientas etk, puede iniciar el cuadro de diálogo ejecutando /usr/bin/etk_prefs

## Resolución de problemas

*   Si X se queja acerca de no están disponibles los cursores X, hágase con el paquete 'libxcursor'.

## Enlaces externos

*   [Portal DR17 de Enlightenment, con temas, fondos de pantalla, módulos, etc.](http://get-e.org)
*   [Guía del usuario de Enlightenment DR 17](http://get-e.org/E17_User_Guide/English/)
*   [Guía del usuario de las bibliotecas fundamentales de Enlightenment](http://get-e.org/EFL_User_Guide/English/)
*   [Howto de e17 para Gentoo](http://gentoo-wiki.com/HOWTO_emerge_e17);
    *   Específicamente, [Añadiendo aplicaciones a iBar](http://gentoo-wiki.com/HOWTO_emerge_e17#Adding_Apps_to_ibar)
*   [Aplicaciones recomendadas](http://archux.com/page/application-recommendations)