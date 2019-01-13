**Estado de la traducción**
Este artículo es una traducción de [Lenovo IdeaPad y530](/index.php/Lenovo_IdeaPad_y530 "Lenovo IdeaPad y530"), revisada por última vez el **2019-01-12**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Lenovo_IdeaPad_y530&diff=0&oldid=562932) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

## Contents

*   [1 Hacer que las cosas funcionen](#Hacer_que_las_cosas_funcionen)
    *   [1.1 Habilitar todos los altavoces](#Habilitar_todos_los_altavoces)
    *   [1.2 Solución para el problema del brillo](#Solución_para_el_problema_del_brillo)
    *   [1.3 Activar/desactivar el wifi mientras se trabaja](#Activar/desactivar_el_wifi_mientras_se_trabaja)

## Hacer que las cosas funcionen

### Habilitar todos los altavoces

```
echo "options snd_hda_intel model=lenovo-sky" >> /etc/modprobe.d/modprobe.conf

```

### Solución para el problema del brillo

El Lenovo Ideapad Y530 tiene una implementación inusual del sistema ACPI. Se está desarrollando un parche para el kernel (2.6.29). Hasta su lanzamiento, la siguiente solución debería ayudar a controlar el brillo de la pantalla más allá de la limitada capacidad de los atajos del teclado.

Para ver una lista de las opciones disponibles:

```
    cat /proc/acpi/video/VGA/LCDD/brightness

```

Reemplace el parámetro XX en la siguiente orden por la intensidad de visualización que desee:

```
    echo XX > /proc/acpi/video/VGA/LCDD/brightness

```

Para máxima intensidad:

```
   echo 65 > /proc/acpi/video/VGA/LCDD/brightness

```

### Activar/desactivar el wifi mientras se trabaja

¿Alguna idea? Actualmente se tiene que reiniciar para hacer que funcione.