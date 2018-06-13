Related articles

*   [Midnight Commander](/index.php/Midnight_Commander "Midnight Commander")
*   [vifm](/index.php/Vifm "Vifm")

**Note:** Esta pagina se encuentra en proceso de traducción .

[ranger](http://ranger.github.io/) es un administrador de archivos que se ejecuta directamente en la terminal, esta escrito en [Python](/index.php/Python "Python"). Los directorios se muestran en un panel con tres columnas. Para moverse entre ellas se usan las flechas de teclado, marcadores, el ratón o el historial de comandos. Las vistas previas y los contenidos se muestran automáticamente para la linea que se encuentre seleccionada.

Entre sus características se encuentran: atajos de teclado vi-style, marcadores, seleccion de archivos o directorios, etiquetado, pestañas, historial de comandos, la posibilidad de hacer links simbólicos, múltiples modos de consola, y un visor de tareas. *ranger* tiene la posibilidad de editar sus atajos de teclado, incluyendo enlaces a scripts externos. Ranger tiene su propio [file opener](/index.php/File_opener "File opener"), [rifle(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/rifle.1). Sus competidores mas cercanos [Vifm](/index.php/Vifm "Vifm") y [lf](https://github.com/gokcehan/lf).

## Instalación

Ranger puede ser [instalado](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") con el paquete [ranger](https://www.archlinux.org/packages/?name=ranger), o [ranger-git](https://aur.archlinux.org/packages/ranger-git/) para obtener la versión de desarrollo.

## Uso basico

Para iniciar ranger, abre una [terminal](/index.php/List_of_applications#Terminal_emulators "List of applications") y corre el comando`ranger`.

<caption></caption>
| Key | Command |
| `?` | Abre el manual de atajos de teclado, comandos y configuraciones |
| `l`, `Enter` | Abre directorios o archivos. |

## Configuración

Después de ser iniciado, *ranger* crea el directorio `~/.config/ranger`. Para cargar la configuración predeterminada usa el siguiente comando:

```
$ ranger --copy-config=all

```

*   `rc.conf` - comandos de inicio y atajos de teclado
*   `commands.py` - comandos que son ejecutados con `:`
*   `rifle.conf` - que aplicación se debe usar para determinado tipo de archivo.

Mira [ranger(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ranger.1) para la configuración general.