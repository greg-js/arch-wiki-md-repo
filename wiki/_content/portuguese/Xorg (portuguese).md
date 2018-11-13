## Contents

*   [1 Introdução](#Introdução)
*   [2 Instalação do Xorg](#Instalação_do_Xorg)
*   [3 Configurar o xorg](#Configurar_o_xorg)
    *   [3.1 hwd](#hwd)
    *   [3.2 xorgconfig](#xorgconfig)
    *   [3.3 Xorg -configure](#Xorg_-configure)
    *   [3.4 nvidia-xconfig](#nvidia-xconfig)
*   [4 Editar xorg.conf](#Editar_xorg.conf)
    *   [4.1 Definições do Monitor](#Definições_do_Monitor)
        *   [4.1.1 Horizontal Sync](#Horizontal_Sync)
        *   [4.1.2 Refresh Rate](#Refresh_Rate)
        *   [4.1.3 Colour Depth](#Colour_Depth)
        *   [4.1.4 Resolution](#Resolution)
    *   [4.2 Keyboard Settings](#Keyboard_Settings)
        *   [4.2.1 Keyboard Layout](#Keyboard_Layout)
        *   [4.2.2 Keyboard Model](#Keyboard_Model)
    *   [4.3 Display Size/DPI](#Display_Size/DPI)
    *   [4.4 Proprietary Drivers](#Proprietary_Drivers)
    *   [4.5 Fonts](#Fonts)
    *   [4.6 Sample Xorg.conf Files](#Sample_Xorg.conf_Files)
*   [5 Running Xorg](#Running_Xorg)
*   [6 X startup (/usr/bin/startx) tweaking](#X_startup_(/usr/bin/startx)_tweaking)
*   [7 Changes with modular Xorg](#Changes_with_modular_Xorg)
    *   [7.1 Most Common Packages](#Most_Common_Packages)
    *   [7.2 OpenGL 3D Acceleration](#OpenGL_3D_Acceleration)
    *   [7.3 Glxgears and Glxinfo](#Glxgears_and_Glxinfo)
    *   [7.4 Changed paths (and configuration)](#Changed_paths_(and_configuration))
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 Keyboard Problems](#Keyboard_Problems)
    *   [8.2 A Quick Fix for the Bitstream-Vera Conflict](#A_Quick_Fix_for_the_Bitstream-Vera_Conflict)
    *   [8.3 A Quick Fix for file conflicts in /usr/include](#A_Quick_Fix_for_file_conflicts_in_/usr/include)
    *   [8.4 Mouse wheel not working](#Mouse_wheel_not_working)
    *   [8.5 Extra mouse buttons not working](#Extra_mouse_buttons_not_working)
    *   [8.6 Keyboard problems](#Keyboard_problems_2)
        *   [8.6.1 AltGR (Compose Key) not working properly](#AltGR_(Compose_Key)_not_working_properly)
        *   [8.6.2 Can't set qwerty layouts using the setxkbmap command](#Can't_set_qwerty_layouts_using_the_setxkbmap_command)
        *   [8.6.3 Setup French Canadian (old ca_enhanced) layout](#Setup_French_Canadian_(old_ca_enhanced)_layout)
    *   [8.7 Missing libraries](#Missing_libraries)
    *   [8.8 Some packages fail to build and complain about missing X11 includes](#Some_packages_fail_to_build_and_complain_about_missing_X11_includes)
    *   [8.9 Unable to load font '(null)'](#Unable_to_load_font_'(null)')
    *   [8.10 KDE Taskbar/Desktop Icons Broken](#KDE_Taskbar/Desktop_Icons_Broken)
    *   [8.11 Updating from testing version to current (missing files)](#Updating_from_testing_version_to_current_(missing_files))
    *   [8.12 Problem with MIME types in various desktop environments](#Problem_with_MIME_types_in_various_desktop_environments)
    *   [8.13 DRI stops working with Matrox cards](#DRI_stops_working_with_Matrox_cards)
    *   [8.14 Cannot start any clients under Xephyr](#Cannot_start_any_clients_under_Xephyr)
*   [9 Links](#Links)

## Introdução

O **Xorg** é uma implementação pública e código-aberto do sistema *X11 X Window System*. (Ver [https://pt.wikipedia.org/wiki/X.Org](https://pt.wikipedia.org/wiki/X.Org) para mais detalhes.) Basicamente, se quer um GUI (Interface Gráfica de Utilizador) no Arch, vai precisar do Xorg.

## Instalação do Xorg

Antes de começar, tenha a certeza do seguinte:

```
# Ter o [Pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") atualizado e configurado.
# Se está a correr outro servidor X pode fechá-lo agora. `ctrl+alt+backspace`
# Fazer uma nota sobre *drivers* de terceiros (ex: driver nVidia ou ATI)

```

Agora vamos instalar o servidor Xorg:

```
pacman -S xorg-server

```

Muita gente irá querer suporte para o rato e teclado.

```
pacman -S xf86-input-mouse xf86-input-keyboard

```

É preciso também um *driver* de vídeo. Pode escrever este comando e listar todos os *drivers* de vídeo disponíveis:

```
pacman -Ss xf86-video

```

Procure pelo driver da sua placa. Se não tem a certeza de qual é, instale o *vesa*, mas lembre-se da sua escolha quando configurar o xorg.

```
pacman -S xf86-video-vesa

```

Irá querer o *startx* e o *xinit*

```
pacman -S xorg-xinit

```

Os preguiçosos poderão copiar este comando:

```
pacman -S xorg-server xf86-input-mouse xf86-input-keyboard xf86-video-vesa xorg-xinit

```

Se o xorg foi bem instalado, é hora de fazer o `xorg.conf`

## Configurar o xorg

Antes que possa correr o xorg, necessita de o configurar para que saiba qual é a placa gráfica, monitor, rato e teclado. Existem vários métodos para automatizar este processo:

### hwd

Talvez a maneira mais facil para ter o Xorg a correr rapidamente é usar o <tt>hwd</tt>, uma ferramenta escrita por utilizadores da comunidade do Arch Linux. Basicamente é uma ferramenta de detecção do hardware que tem vários usos, um deles é configurar um servidor X. Felizmente, o hwd é muito mais directo do que correr o `xorgconf` e não necessita que se escreva muito.

Primeiro, instale o pacote do <tt>hwd</tt>:

```
# pacman -S hwd

```

Agora simplesmente corra o seguinte comando como root para gerar um ficheiro `xorg.conf`:

```
# hwd -xa

```

Isto irá escrever o /etc/X11/xorg.conf existente com uma série de valores baseados na detecção de hardware feita pelo <tt>hwd</tt>.

Pode também gerar uma configuração de exemplo do Xorg (/etc/X11/xorg.conf.hwd) sem reescrever a configuração existente. Para fazer isto, corra <tt>hwd</tt> com o argumento **-x**:

```
# hwd -x

```

Para utilizar esta configuração de exemplo, deve alterar o nome do ficheiro manualmente:

```
# mv /etc/X11/xorg.conf.hwd /etc/X11/xorg.conf

```

### xorgconfig

Para iniciar o <tt>xorgconfig</tt>:

```
# xorgconfig

```

Isto irá gerar um <tt>xorg.conf</tt>.

Responde às perguntas feitas e o programa irá criar o ficheiro automaticamente. Este programa, na realidade, não é muito bom, mas é um começo e pode depois acrescentar/modificar os valores do xorg.conf manualmente.

### Xorg -configure

Pode utilizar

```
# Xorg -configure

```

ou

```
# X -configure

```

### nvidia-xconfig

Utilizadores com placas nVidia podem utilizar isto:

```
# nvidia-xconfig

```

assim que tiverem os drivers [instalados](/index.php/NVIDIA "NVIDIA").

## Editar xorg.conf

Poderá querer editar a configuração depois de ser gerada. Para abrir a configuração no seu editor de texto favorito, como por exemplo o Vim (em root):

```
# vim /etc/X11/xorg.conf

```

Se deseja definir suporte à roda do rato, veja [Get All Mouse Buttons Working](/index.php/Get_All_Mouse_Buttons_Working "Get All Mouse Buttons Working").

### Definições do Monitor

Depending on your hardware, Xorg may fail to detect your monitor capabilities correctly, or you may simply wish to use a lower resolution than your monitor is capable of. You might want to look up the following values in your monitor's manual before setting them. The following settings are specified in the Monitor section:

#### Horizontal Sync

```
HorizSync 28-64

```

#### Refresh Rate

```
VertRefresh 60

```

The following are specified in the Screen section:

#### Colour Depth

```
Depth 24

```

#### Resolution

```
Modes "1280x1024" "1024x768" "800x600"

```

### Keyboard Settings

Xorg may fail to detect your keyboard correctly. This might give problems with your keyboard layout or keyboard model not being set correctly.

To see a full list of keyboard models, layouts, variants and options, open.

```
/usr/share/X11/xkb/rules/xorg.lst

```

#### Keyboard Layout

To change the keyboard layout, use the XkbLayout option in the keyboard InputDevice section. For example, if you have a keyboard with English layout:

```
Option "XkbLayout" "gb"

```

#### Keyboard Model

To change the keyboard model, use the XkbModel option in the keyboard InputDevice section. For exsample, if you have a Microsoft Wireless Multimedia Keyboard:

```
Option "XkbModel" "microsoftmult"

```

### Display Size/DPI

In order to get correct sizing for fonts the display size must be set for your desired DPI. In the section `"Monitor"` put in your display size in mm:

```
Section "Monitor"
   ...
 DisplaySize 336 252 # 96 DPI @ 1280x960
   ...
EndSection

```

The formula for calculating the DisplaySize values is Width x 25.4 / DPI and Height x 25.4 / DPI. If you're running Xorg with a resolution of 1024x768 and want a DPI of 96, use 1024 x 25.4 / 96 and 768 x 25.4 / 96\. Round numbers down.

```
# calc: (x|y)pixels * 25.4 / dpi
# DisplaySize 168 126 # 96 DPI @ 640x480
# DisplaySize 210 157 # 96 DPI @ 800x600
# DisplaySize 269 201 # 96 DPI @ 1024x768
# DisplaySize 302 227 # 96 DPI @ 1152x864
# DisplaySize 336 252 # 96 DPI @ 1280x960
# DisplaySize 336 269 # 96 DPI @ 1280x1024 (non 4:3 aspect)
# DisplaySize 370 277 # 96 DPI @ 1400x1050
# DisplaySize 420 315 # 96 DPI @ 1600x1200
# DisplaySize 506 315 # 96 DPI @ 1920x1200

```

For nVidia drivers you may have to disable automatic detection of DPI to set it manually. There is also an easier way to set DPI on these cards. Either or both of the following lines can be set in the device section for your nVidia card.

```
  Option   "UseEdidDpi" "false"
  Option   "DPI" "96 x 96"

```

Results can be checked by issuing the following command, which should return 96x96 dots per inch if you set DPI @ 96.

```
$ xdpyinfo | grep -B1 dot

```

### Proprietary Drivers

If you wish to use third-party graphics drivers, do check first that the X server runs OK first. Xorg should run smoothly without official drivers, which are typically needed only for advanced features such as 3D-accelerated rendering for games, dual-screen setups, and TV-out. Refer to the [NVIDIA](/index.php/NVIDIA "NVIDIA") and [ATI](/index.php/ATI "ATI") wikis for help with driver installation.

### Fonts

There some tips for setting up fonts in [Xorg Font Configuration](/index.php/Xorg_Font_Configuration "Xorg Font Configuration").

### Sample Xorg.conf Files

Anyone who has an Xorg.conf file written up that works, go ahead and post a link to it here for others to look at! Please don't inline the entire conf file; upload it somewhere else and link. Thanks!

*   Shadowhand (nv and nvidia drivers): [http://people.os-zen.net/shadowhand/configs/xorg.conf](http://people.os-zen.net/shadowhand/configs/xorg.conf)
*   Cerebral (fglrx and radeon drivers): [http://www.student.cs.uwaterloo.ca/~tjwillar/configs/xorg.conf](http://www.student.cs.uwaterloo.ca/~tjwillar/configs/xorg.conf)
*   raskolnikov (via unichrome and synaptics drivers): [http://athanatos.free.fr/Arch/xorg.conf](http://athanatos.free.fr/Arch/xorg.conf)
*   Leigh (Three independent screens - Three nvidia cards): [http://files.myopera.com/allisonleigh/linuxbackup/xorg.conf](http://files.myopera.com/allisonleigh/linuxbackup/xorg.conf)

## Running Xorg

This is done simply by typing:

```
$ startx

```

The default X environment is rather bare, and you will typically seek to install window managers or desktop environments to supplement X.

To test the config file you have created:

```
$ X -config *<your config file>*

```

If a problem occurs, then view the log at <tt>/var/log/Xorg.0.log</tt>. Be on the lookout for any lines beginning with *(EE)* which represent errors, and also *(WW)* which are warnings that could indicate other issues.

**Note:** Using startx requires a *~/.xinitrc* file, so that X knows what to run when it starts. See [Xinitrc](/index.php/Xinitrc_(Portugu%C3%AAs) "Xinitrc (Português)") for detail.

If you are using GNOME it is best to start GNOME through gdm to avoid HAL permission problems.

In addition, you can also install twm and xterm (via pacman), which will be used as a fallback if ~/.xinitrc does not exist (as stated in /etc/X11/xinit/xinitrc).

## X startup (/usr/bin/startx) tweaking

For X's option reference see

```
$ man Xserver

```

The following options have to be appended to the variable "defaultserverargs" in the /usr/bin/startx file.

prevent X from listening on tcp:

```
-nolisten tcp

```

getting rid of the gray weave pattern while X is starting and let X set a black root window:

```
-br

```

enable deferred glyph loading for 16 bit fonts:

```
-deferglyphs 16

```

Note: If you start X with kdm, the startx script seems not executed. These options must be appended to the variable "ServerCmd" in the /opt/kde/share/config/kdm/kdmrc file.

## Changes with modular Xorg

### Most Common Packages

Make sure you install drivers for mouse, keyboard and videocard. For mouse and keyboard, **xf86-input-keyboard** and **xf86-input-mouse** should get installed. Other **xf86-input-*** packages are available for different input devices.

For the videocard, find out which driver is required and install the right **xf86-video-*** package. ATI and Nvidia users may wish to install the non-free drivers for their hardware instead ([NVIDIA](/index.php/NVIDIA "NVIDIA"), [ATI](/index.php/ATI "ATI")).

To install all drivers in one run, the **xorg-input-drivers** and **xorg-video-drivers** are available.

### OpenGL 3D Acceleration

X.Org 7.0 on Arch Linux uses a modular design for mesa, the OpenGL rendering system. Several implementations are available:

*   libgl-dri: Open-source DRI OpenGL implementation. Falls back to software rendering when no DRI driver is installed
*   some other driver providing libGL (ati, nvidia)

When pacman installs an application that needs mesa, it will install one of these packages. To be sure about the right library for your setup, install the library you want prior to installing Xorg. Installing the right package afterwards is also possible, though this gives some dependency errors sometimes, which can be ignored with the -d switch.

### Glxgears and Glxinfo

These apps are included in the mesa package.

### Changed paths (and configuration)

**See this entry for additional upgrade info:** [https://www.archlinux.org/blog/2006/01/02/how-to-upgrade-xorg/](https://www.archlinux.org/blog/2006/01/02/how-to-upgrade-xorg/)

Modular X.Org 7 installs everything in `/usr`, where the older versions installed in `/usr/X11R6`. Several configuration files need updates:

*   */etc/X11/xorg.conf*
    *   Fontpaths live in /usr/share/fonts now
    *   RGB database is in /usr/share/X11/rgb
    *   module path is /usr/lib/xorg/modules

Also note that some X configuration tools might stop working. The easiest way to configure X.org is by installing the correct driver packages and running *Xorg -configure*, which results in a `/root/xorg.conf.new` which only needs modification in the resolutions, mouse configuration and keyboard layouts.

Some packages have hard-coded references to `/usr/X11R6`. These packages need fixing. In the meantime, look what packages install files in `/usr/X11R6`, uninstall those, make a symlink from `/usr` to `/usr/X11R6` and reinstall the affected packages. Another option is to move the contents of `/usr/X11R6` to `/usr` and make the symlink.

Or you can just add a second module path via `ModulePath "/usr/X11R6/lib/modules"` This works e.g. for Nvidia 76.76

## Troubleshooting

### Keyboard Problems

Auto-generated xorg.conf files may cause you problems. If you cannot get to tty1 by holding CTRL-ALT and pressing F1 or cannot get the £ sign for gb people, check to see if the following entries are in your /etc/X11/xorg.conf:

```
Option "XkbLayout"  "uk"         #"uk" is not a real layout, look in /usr/share/X11/xkb/symbols/ for a list of real ones.
Option "XkbRules"   "xfree86"    #this should be "xorg"
Option "XkbVariant" "nodeadkeys" #This line is also known to cause the problems described, try commenting it out.

```

To switch between layouts with Alt+Shift:

```
Option "XkbOptions" "grp:alt_shift_toggle,grp_led:scroll"

```

### A Quick Fix for the Bitstream-Vera Conflict

If you see a message that ttf-bitstream-vera conflicts with xorg:

1.  Exit the pacman session by answering no.
2.  Run `pacman -Rd xorg`
3.  Run `pacman -Syu`
4.  Run `pacman -S xorg`
5.  Update your paths in /etc/X11/xorg.conf

### A Quick Fix for file conflicts in /usr/include

If you see messages about file conflicts in /usr/include/X11 and /usr/include/GL:

1.  Run `rm /usr/include/{GL,X11}`
2.  Run `pacman -Su`

The symlinked directories removed by this operation are replaced by real directories in the new xorg package, causing these file conflicts to appear.

### Mouse wheel not working

The "Auto" protocol doesn't seem to work properly in Xorg 7 any more. In the InputDevice section for your mouse, change:

```
Option         "Protocol" "auto"

```

to

```
Option         "Protocol" "IMPS/2"

```

or

```
Option         "Protocol" "ExplorerPS/2"

```

### Extra mouse buttons not working

USB Mice users should read [Get All Mouse Buttons Working](/index.php/Get_All_Mouse_Buttons_Working "Get All Mouse Buttons Working").

Intellimouse (ExplorerPS/2) users might find their scroll and side buttons aren't behaving as they used to. Previously xorg.conf needed:

```
Option      "Buttons" "7"
Option      "ZAxisMapping" "6 7"

```

and users also had to run xmodmap to get the side buttons working with a command like:

```
xmodmap -e "pointer = 1 2 3 6 7 4 5"

```

Now xmodmap is no longer required. Instead, make xorg.conf look like this:

```
Option      "Buttons" "5"
Option      "ZAxisMapping" "4 5"
Option      "ButtonMapping" "1 2 3 6 7"

```

and the side buttons on a 7-button Intellimouse will work like they used to, without needing to run xmodmap.

### Keyboard problems

Some keyboard layouts have changed. I wondered why:

*   I wasn't able to Ctrl+Alt+Fx to switch to console
*   I wasn't able to use layouts

The problem was that the *sk_qwerty* layout doesn't exist anymore. I had to replace

```
Option         "XkbLayout" "us,sk_qwerty"

```

with

```
Option         "XkbLayout" "us,sk"
Option         "XkbVariant" ",qwerty"

```

Another thing to look for if your keyboard isn't properly functioning is the XkbRules option:
You'll need to change

```
Option         "XkbRules" "xfree86"

```

to

```
Option         "XkbRules" "xorg"

```

#### AltGR (Compose Key) not working properly

If, after the update, you can't use the AltGr key as expected any more, try adding this to your keyboard section:

```
Option      "XkbOptions" "compose:ralt"

```

This is not the correct way to activate the AltGr Key on a German keyboard (for example, to use the '|' and '@' keys on German keyboards). Just choose a valid keyboard variant for it to work again, for example (the example is for a German keyboard):

```
Option      "XkbLayout" "de"
Option      "XkbVariant" "nodeadkeys"

```

The solutions above don't work on an Italian keyboard. To activate the AltGr key on an Italian keyboard make sure you have the following lines set up properly:

```
 Driver          "kbd"
 Option          "XkbRules"      "xorg"
 Option          "XkbVariant"    ""

```

#### Can't set qwerty layouts using the setxkbmap command

After the update, there aren't qwerty layouts as for example sk_qwerty. If you want to switch your present keyboard layout to any qwerty keyboard layout use this command:

```
$ setxkbmap NAME_OF_THE_LAYOUT qwerty

```

e.g.: for sk_qwerty use:

```
$ setxkbmap sk qwerty

```

After the update, trying the above command I had this message "Error loading new keyboard description". I find out that the xserver doesn't have the rights to write, execute, read in the directory /var/tmp So give the permissions to that directory. Restart the xserver and you will have your deadkeys back! Don't believe? Try out the code e.g.: it layout

```
$ setxkbmap -layout it

```

#### Setup French Canadian (old ca_enhanced) layout

With Xorg7, "ca_enhanced" is no more. You have to do a little trick to get the same layout that you are used to: Switch the old:

```
       Option          "XkbLayout"     "ca_enhanced"

```

To:

```
       Option          "XkbLayout"     "ca"
       Option          "XkbVariant"    "fr"

```

It will be similar with other layout, I presume. You can refer to Gentoo HowTo there: [http://www.gentoo.org/proj/en/desktop/x/x11/modular-x-howto.xml](http://www.gentoo.org/proj/en/desktop/x/x11/modular-x-howto.xml)

### Missing libraries

*   **Help! I get an error message running my favourite app saying "libXsomething" doesn't exist!**

In most cases, all you need to do is take the name of the library (eg libXau.so.1), convert it all to lowercase, remove the extension, and pacman for it:

```
# pacman -S libxau

```

This will install the library you're missing, and all will be well again!

### Some packages fail to build and complain about missing X11 includes

Just reinstall the packages xproto and libx11, even if they are already installed.

### Unable to load font '(null)'

*   **Some programs don't work and say unable to load font `(null)'.**

These packages would like some extra fonts. Some programs only work with bitmap fonts. Two major packages with bitmap fonts are available, xorg-fonts-75dpi and xorg-fonts-100dpi. You don't need both; one should be enough. To find out which one would be better in your case, try this:

```
$ xdpyinfo | grep resolution

```

and grab what is closer to you (75 or 100 instead of XX)

```
# pacman -S xorg-fonts-XXdpi

```

### KDE Taskbar/Desktop Icons Broken

*   **KDE taskbar doesn't work and the desktop icons disappear**

Install the packages libxcomposite and libxss. It will be fine.

```
# pacman -S libxcomposite libxss

```

### Updating from testing version to current (missing files)

If you've updated from Xorg 7 in testing to Xorg 7 in current and are finding that many files seem to be missing (including startx, /usr/share/X11/rgb.txt, and others), you may have lost many files due to the xorg-clients package splitting from a single package into many smaller sub packages.

You need to reinstall all the packages that are dependencies of xorg-clients:

```
# pacman -S xorg-apps xorg-font-utils xorg-res-utils xorg-server-utils \
          xorg-twm xorg-utils xorg-xauth xorg-xdm xorg-xfs xorg-xfwp \
          xorg-xinit xorg-xkb-utils xorg-xsm

```

This should fix the problem.

### Problem with MIME types in various desktop environments

If you noticed icons missing and can't click-open files in desktop environments, add the following lines to /etc/profile or your preferred init script and reboot.

```
XDG_DATA_DIRS=$XDG_DATA_DIRS:/usr/share
export XDG_DATA_DIRS

```

### DRI stops working with Matrox cards

If you use a Matrox card and DRI stops working after upgrading to xorg7, try adding the line

```
Option "OldDmaInit" "On"

```

to the Device section that references the video card in xorg.conf.

### Cannot start any clients under Xephyr

The client connections are rejected by the X server's security mechanism, you can find a complete explanation and solution in [[1]](http://wiki.debian.org/XStrikeForce/FAQ#howtoxnest).

## Links

See also:

*   [Gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição")
*   [Iniciar X no login](/index.php/Iniciar_X_no_login "Iniciar X no login")
*   [Xorg Font Configuration](/index.php/Xorg_Font_Configuration "Xorg Font Configuration")
*   Proprietary Video Drivers
    *   [ATI](/index.php/ATI "ATI")
    *   [NVIDIA](/index.php/NVIDIA "NVIDIA")
*   [Ambiente de desktop](/index.php/Ambiente_de_desktop "Ambiente de desktop")
    *   [KDE](/index.php/KDE "KDE")
    *   [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)")
    *   [Xfce](/index.php/Xfce "Xfce")
    *   [Enlightenment](/index.php/Enlightenment "Enlightenment")
    *   [Fluxbox](/index.php/Fluxbox_(Portugu%C3%AAs) "Fluxbox (Português)")

External Links:

*   [X.org Wikipedia Article](https://en.wikipedia.org/wiki/X.Org_Server "wikipedia:X.Org Server")
*   [X.org](http://wiki.x.org/wiki/)