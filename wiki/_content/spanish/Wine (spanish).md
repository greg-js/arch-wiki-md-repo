[Wine](http://www.winehq.org/) es una capa de adaptación (un cargador) capaz de ejecutar aplicaciones de Windows en Linux y otros sistemas operativos compatibles con POSIX. Aplicaciones Windows ejecutadas en Wine se comportan como los programas nativos, ejecutandose sin las restricciones de memoria o comportamiento de un emulador, y con una apariencia similar a la de otras aplicaciones en tu escritorio.

**Advertencia:** SI su usuario puede acceder algun archivo o recurso, programas que sean ejecutados con Wine también tienen acceso. Vea [#Running Wine under a separate user account](#Running_Wine_under_a_separate_user_account) y [Security#Sandboxing applications](/index.php/Security#Sandboxing_applications "Security") para precauciones posibles.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Configuración](#Configuraci.C3.B3n)
*   [3 Fuentes](#Fuentes)
*   [4 Submenú](#Submen.C3.BA)
    *   [4.1 Crear entrada en el menú](#Crear_entrada_en_el_men.C3.BA)
    *   [4.2 Arreglar el menú en KDE 4](#Arreglar_el_men.C3.BA_en_KDE_4)
*   [5 Usando wine para ejecutar binarios de Win16 / Win32](#Usando_wine_para_ejecutar_binarios_de_Win16_.2F_Win32)
*   [6 Utilidades para configurar Wine](#Utilidades_para_configurar_Wine)
    *   [6.1 WineTricks](#WineTricks)
    *   [6.2 Asistente WineTools](#Asistente_WineTools)
    *   [6.3 Utilidad de Configuración de Wine Sidenet Wine](#Utilidad_de_Configuraci.C3.B3n_de_Wine_Sidenet_Wine)
    *   [6.4 Wine-doors](#Wine-doors)
*   [7 Alternativos a binarios Win16 / Win32](#Alternativos_a_binarios_Win16_.2F_Win32)
*   [8 See also](#See_also)

## Instalación

Wine se puede instalar habilitando el repositorio [Multilib](/index.php/Multilib_(Espa%C3%B1ol) "Multilib (Español)") e [instalando](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [wine](https://www.archlinux.org/packages/?name=wine) (estable) o [wine-staging](https://www.archlinux.org/packages/?name=wine-staging) (desarrollo).

Considere la instalación de [wine_gecko](https://www.archlinux.org/packages/?name=wine_gecko) o [wine-mono](https://www.archlinux.org/packages/?name=wine-mono) para aplicaciones que dependen en Internet Explorer o .NET respectivamente. Estos paquetes no son necesariamente requeridos ya que Wine descargara los archivos que necesite automaticamente. De todas maneras, tener estos archivos de ante mano permite trabajar sin tener que estar conectado a Internet y también no es necesario descargar de nuevo para cada prefix.

## Configuración

Para crear los archivos de configuración

```
 winecfg

```

revisa los ajustes y da en ok para salvarlas. El directorio wine con los archivos de configuración se encuentra en

```
 ~/.wine

```

y C:\> apunta por default a

```
 ~/.wine/drive_c

```

¡Perfecto! Esta es la configuración básica. Puedes probarla ejecutando algo como:

```
 wine /ruta/a/aplicacion.exe

```

Si tienes problemas para ejecutar una aplicación DirectX correctamente, intenta agregar la flag **-opengl**:

```
 wine /ruta/a/juego_3d.exe **-opengl**

```

## Fuentes

*   Si las aplicaciones Wine muestran fuentes ilegibles, puede que no tengas instaladas las fuentes Truetype de Microsoft. Puede instalar el paquete ttf-ms-fonts desde [AUR](/index.php/AUR "AUR").

Luego mate todos los servidores wine y ejecute winecfg; las fuentes deben ser legibles ahora.

Otras fuentes TTF que desee instalar deben colocarse en $C_DRIVE/windows/fonts/ (donde $C_DRIVE esta por lo general en ~/.wine/drive_c) para que wine las reconozca.

Sí las fuentes se ven serruchadas, entre en el directorio wine y cree el archivo fontrender.txt con el siguiente contenido:

```
[HKEY_CURRENT_USER\Software\Wine\X11 Driver]
"ClientSideWithRender"="N"

```

Agrega la llave a tu configuración de wine ejecutando el siguiente comando:

```
regedit fontrender.txt

```

*   **Como habilitar el anti-aliasing en la fuentes de Wine ?**

Crea un archivo .reg (por ejemplo: aa.reg) con lo siguiente :

```
REGEDIT4

[HKEY_CURRENT_USER\Control Panel\Desktop]
"FontSmoothing"="2"
"FontSmoothingType"=dword:00000002
"FontSmoothingGamma"=dword:00000578
"FontSmoothingOrientation"=dword:00000001

```

Ejecuta

```
regedit 

```

y elije

```
File -> Import registry file... 

```

y selecciona tu archivo .reg. El anti-aliasing de las fuentes se reflejara después de cerrar regedit, y volver a ejecutar las aplicaciones.

## Submenú

Después de la instalación, probablemente no habrá un menú en tu Entorno Gráfico. Después de instalar un programa utilizando Wine, este creara un menú con los programas en el. Si deseas agregar al menu un submenu para wine, entonces debes seguir las primereas instrucciones:

### Crear entrada en el menú

Primero, instala una aplicación Windows usando Wine para crear un menú base. Después de que el menú base se haya creado, puedes empezar a agregar las entradas al menú. En GNOME, da boton secundario en el escritorio y selecciona "*Crear Lanzador...*" . Los pasos pueden ser diferentes para KDE/Xfce. Haz tres lanzadores usando estos parametros.

```
**Type**: Application
**Name**: Configuración 
**Command**: winecfg
**Comment**: Configura los ajustes de Wine

```

```
**Type**: Application
**Name**: Desinstalar Programas
**Command**: wine uninstaller
**Comment**: Desinstala programas de Wine apropiadamente 

```

```
**Type**: Application
**Name**: Navegar en la unidad C:\ 
**Command**: wine winebrowser c:\\
**Comment**: Navega en los archivos de disco virtual C:\ de Wine

```

Ahora ya tienes estos tres lanzadores en tu escritorio, es momento de ponerlos en el menú. Pero primero debes cambiar los lanzadores para que cambien los iconos de manera automática al cambiar de tema. Para hacer esto, abre los lanzadores que acabas de crear y teclea esto en tu editor de texto favorito. Cambia los siguientes parámetros a estos valores:

Lanzador *Configuración*:

```
Icon[en_US]=wine-winecfg
Icon=wine-winecfg

```

Lanzador *Desinstalar Programas*:

```
Icon[en_US]=wine-uninstaller
Icon=wine-uninstaller

```

Lanzador *Navegar en la unidad C:\*:

```
Icon[en_US]=wine-winefile
Icon=wine-winefile

```

Si esta configuración produce un icono feo/inexistente, quiere decir que no hay iconos para estos lanzadores en el tema de iconos que estas usando. Debes reemplazar el icono con la localización exacta del icono que quieres usar. Dar click en las propiedades del lanzador tendrá el mismo efecto. Un gran tema de iconos que contiene los iconos para estos lanzadores es [GNOME-colors](http://www.gnome-look.org/content/show.php/GNOME-colors?content=82562).

Ahora que los lanzadores están completamente configurados, es el momento de ponerlos en el menú. Colocalos en "*~/.local/share/applications/wine/*" usando una terminal o un navegador de archivos.

Espera un momento, ¡aun no esta en el menú! Hay un último paso. Copia el siguiente texto en un archivo llamado "*wine-utilities.menu*".

```
<!DOCTYPE Menu PUBLIC "-//freedesktop//DTD Menu 1.0//EN"
"[http://www.freedesktop.org/standards/menu-spec/menu-1.0.dtd](http://www.freedesktop.org/standards/menu-spec/menu-1.0.dtd)">
<Menu>
  <Name>Applications</Name>
  <Menu>
    <Name>wine-wine</Name>
    <Directory>wine-wine.directory</Directory>
    <Include>
	<Filename>wine-Configuración.desktop</Filename>
    </Include>
    <Include>
	<Filename>wine-Navegar en la unidad C:\.desktop</Filename>
    </Include>
    <Include>
	<Filename>wine-Desinstalar Programas.desktop</Filename>
    </Include>
  </Menu>
</Menu>

```

Ahora, solo mueve el nuevo archivo en la carpeta "*~/.config/menus/applications-merged/*". Ahora solo revisa el menú y las opciones deberán estar ahí, listas para ser usadas.

### Arreglar el menú en KDE 4

Los items del menú de Wine pueden aparecer en "Lost & Found" en lugar del menu de Wine para KDE 4\. Esto es porque las kde-applications.menu falta en la opción MergeDir.

Edita **/etc/xdg/menus/kde-applications.menu**

Al final del archivo agrega <MergeDir>applications-merged</MergeDir> después <DefaultMergeDirs/>, debe verse así:

```
        <Include>
                <And>
                        <Category>KDE</Category>
                        <Category>Core</Category>
                </And>
        </Include>
        <DefaultMergeDirs/>
        <MergeDir>applications-merged</MergeDir>
        <MergeFile>applications-kmenuedit.menu</MergeFile>
</Menu>

```

Referencia [[1]](https://bugs.launchpad.net/ubuntu/+source/wine/+bug/263041)

## Usando wine para ejecutar binarios de Win16 / Win32

Puedes ejecutar binarios invocando **wine** manualmente

```
wine programa.exe

```

Tambien es posible decirle al kernel que use **wine** como un interprete para todos los binarios Win16/Win32\. Primero monta el sistema de archivos binfmt_misc:

```
mount -t binfmt_misc none /proc/sys/fs/binfmt_misc

```

o agrega esta línea a tu **/etc/fstab**

```
none  /proc/sys/fs/binfmt_misc binfmt_misc defaults 0 0

```

Después dile al kernel como interpretar binarios Win16 y Win32:

```
echo ':DOSWin:M::MZ::/usr/bin/wine:' > /proc/sys/fs/binfmt_misc/register

```

Puedes agregar esta línea a tu **/etc/rc.local** para hacer esta configuración permanente. En este caso puede que quieras ignorar stderr para evitar errores cuando cambies de runlevels:

```
{ echo ':DOSWin:M::MZ::/usr/bin/wine:' > /proc/sys/fs/binfmt_misc/register; } 2>/dev/null

```

Ahora intenta esto:

```
chmod 755 exefile.exe
./exefile.exe

```

Puedes remover la **.exe** extensión, porque el kernel no identifica un archivo por su extensión.

## Utilidades para configurar Wine

Estas utilidades te ayudaran en la instalación de componente típicos de Windows. En la mayoría de los casos deben ser usados como última alternativa, ya que modificaran tu configuración de Wine.

### WineTricks

[Winetricks](http://wiki.winehq.org/winetricks) es un script rápido (y ligeramente sucio) que te permitira instalar los requerimientos básicos necesarios para ejecutar algunas algunos programas de Windows. Los componentes instalables incluyen DirectX 9.x, msxml (Office 2007 / Requerimiento de IE), visual runtimes y muchos mas.

Para instalar simplemente:

```
pacman -S winetricks

```

Ahora puedes usar winetricks (¡como usuarios normal!) con:

```
winetricks

```

### Asistente WineTools

(actualmente ligeramente obsoleto, pero funcional)

Winetools es un programa (mas que un script) que facilita la instalación de algunos componentes básicos para wine para poder instalar otros programas. No son necesarios para wine, pero ayudan si quieres ejecutar Internet Explorer.

[Sitio de WineTools](http://www.von-thadden.de/Joachim/WineTools/)

Recuerda, Microsoft dice que debes tener una licencias para IE6 para poder instalar DCOM98 o Internet Explorer 6\. Si alguna vez tuviste una copia (original) de Windows, no deberías tener problemas. Aunque estoy seguro que nadie va a ponerle precio a tu cabeza si no tienes licencia.

Ahora consigue el [PKGBUILD](https://aur.archlinux.org/packages.php?ID=8913) del AUR: [https://aur.archlinux.org/packages.php?ID=8913](https://aur.archlinux.org/packages.php?ID=8913)

y compila el paquete como lo harías con cualquier PKGBUILD (Si no sabes como: [Arch Build System](/index.php/Arch_Build_System "Arch Build System"))

### Utilidad de Configuración de Wine Sidenet Wine

[wine-config](http://sidenet.ddo.jp/winetips/config.html)

*   Descarga la última versión
*   Descomprimela
*   LEE EL README
*   ejecuta

```
./setup

```

*   Sigue las instrucciones

**Recuerda**: Como lo dice en el [sitio](http://sidenet.ddo.jp/winetips/config.html), solo se te permite instalar DCOM98 si posees una licencia valida de Windows98.

### Wine-doors

[Wine-doors](http://www.wine-doors.org/)

Wine-doors es un reemplazo de WineTools. Tiene una GUI para GNOME y funciona como un administrador de paquetes. Funciona bien en 64bit. Puedes [encontrarlo en AUR](https://aur.archlinux.org/packages.php?ID=11823).

## Alternativos a binarios Win16 / Win32

*   [Codeweavers](/index.php/Codeweavers "Codeweavers") - Codeweavers' Crossover Office; Orientado a usuarios de Office

## See also

*   [http://www.winehq.com/](http://www.winehq.com/)