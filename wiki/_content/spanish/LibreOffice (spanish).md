de [Home - LibreOffice](http://www.libreoffice.org/):

	"LibreOffice es la poderosa suite de productividad personal de código abierto para Windows, Macintosh y Linux, que le ofrece seis aplicaciones ricas en funcionalidades para todas las necesidades de procesamiento de documentos y datos: Writer, Calc, Impress, Draw, Matemáticas y Base. Nuestra gran comunidad de diligentes usuarios, colaboradores y desarrolladores le ofrecen [asistencia](http://es.libreoffice.org/asistencia/) gratuita. ¡Usted también puede [participar](http://es.libreoffice.org/participe/)!

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 LibreOffice en Arch Linux](#LibreOffice_en_Arch_Linux)
*   [2 Instalación](#Instalación)
*   [3 Extensiones de gestión](#Extensiones_de_gestión)
*   [4 Configuración del lenguaje](#Configuración_del_lenguaje)
    *   [4.1 Corrección de ortografía](#Corrección_de_ortografía)
    *   [4.2 Reglas de división de palabras](#Reglas_de_división_de_palabras)
    *   [4.3 Sinónimos](#Sinónimos)
    *   [4.4 Gramática](#Gramática)
*   [5 Instalando Macros](#Instalando_Macros)
*   [6 Ejecutar LibreOffice](#Ejecutar_LibreOffice)
*   [7 Acelerar LibreOffice](#Acelerar_LibreOffice)
*   [8 Solución de problemas](#Solución_de_problemas)
    *   [8.1 Sustitución de fuentes](#Sustitución_de_fuentes)
    *   [8.2 No se pueden ingresar acentos](#No_se_pueden_ingresar_acentos)

## LibreOffice en Arch Linux

El apoyo oficial a [OpenOffice.org](/index.php/OpenOffice.org "OpenOffice.org") se abandonó en favor de LibreOffice. Más información: [Quitar OpenOffice Oracle (Arch-general)](https://mailman.archlinux.org/pipermail/arch-general/2011-March/018819.html).

LibreOffice es el fork de la *Document Foundation* en el repositorio extra, que incluye mejoras y nuevas características.

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") una de los siguientes paquetes de los repositorios oficiales:

*   [libreoffice-fresh](https://www.archlinux.org/packages/?name=libreoffice-fresh) es la rama principal, con las mejoras nuevas.
*   [libreoffice-still](https://www.archlinux.org/packages/?name=libreoffice-still) es la rama de mantenimiento.

Descargar un paquete de idioma Español de acuerdo a la rama que instalo en el paso anterior:

*   [libreoffice-still-es](https://www.archlinux.org/packages/?name=libreoffice-still-es).
*   [libreoffice-fresh-es](https://www.archlinux.org/packages/?name=libreoffice-fresh-es).

Examine las dependencias opcionales que pacman sugiere. Por ejemplo, puede instalar un entorno de ejecución Java (opcional pero muy recomendable). Ver: [Java](/index.php/Java "Java")

## Extensiones de gestión

Arch ofrece algunas extensiones adicionales. En este momento son:nlpsolver, presentation-minimizer, report-builder, wiki-publisher.

*   Si usted considera que algunas de ellas pueden serle útiles, instálelas

```
 # pacman-S libreoffice-extension-nlpsolver libreoffice-extension-fu ...

```

Compruebe el gestor de Extensiones incorporado en LibreOffice, u [Obtenga extensiones en Internet](http://libreplanet.org/wiki/Group:OpenOfficeExtensions/List) si desea instalar más extensiones.

## Configuración del lenguaje

### Corrección de ortografía

Para revisar la ortografía necesitará hunspell y diccionario de hunspell: [hunspell](https://www.archlinux.org/packages/?name=hunspell), [hunspell-es_es](https://www.archlinux.org/packages/?name=hunspell-es_es) y [hunspell-es_any](https://www.archlinux.org/packages/?name=hunspell-es_any).

### Reglas de división de palabras

Para disponer de las reglas de división también necesitará hyphen: [hyphen](https://www.archlinux.org/packages/?name=hyphen) y [hyphen-es](https://www.archlinux.org/packages/?name=hyphen-es).

### Sinónimos

Para la opción Sinónimos necesitará mythes: [mythes-es](https://www.archlinux.org/packages/?name=mythes-es).

### Gramática

Para la opción de corrección de gramática son necesarios instalar los paquetes: [languagetool](https://www.archlinux.org/packages/?name=languagetool), [libreoffice-extension-languagetool](https://aur.archlinux.org/packages/libreoffice-extension-languagetool/) y [languagetool-ngrams-es](https://aur.archlinux.org/packages/languagetool-ngrams-es/).

## Instalando Macros

En la mayoría de las distros linux, la ruta predeterminada para las macros es la siguiente:

```
~/.openoffice.org/3/user/Scripts/

```

La ruta de este directorio para LibreOffice en Arch Linux es:

```
~/.config/libreoffice/4/user/Scripts/

```

Otra cosa a tener en cuenta es que si desea utilizar las macros, debe tener habilitado JRE. El uso de un JRE es la opción por defecto, pero desactivar su uso es uno de los consejos que se dan más abajo para acelerar la velocidad de LibreOffice.

## Ejecutar LibreOffice

Si desea ejecutar un módulo específico de LibreOffice (en lugar del Centro de Inicio de LibreOffice (soffice todavía se incluye por razones de compatibilidad)), por ejemplo, el procesador de texto (Write), hoja de cálculo (Calc) o el programa de presentaciones (Impress), pruebe los siguientes scripts:

Writer

```
 /usr/bin/libreoffice --writer or /usr/bin/soffice -writer

```

Calc

```
 /usr/bin/libreoffice --calc

```

Impress

```
 /usr/bin/libreoffice --impress

```

Draw

```
 /usr/bin/libreoffice --draw

```

Math (Editor de formulas)

```
 /usr/bin/libreoffice --math

```

Base (Interface de base de datos)

```
 /usr/bin/libreoffice --base

```

## Acelerar LibreOffice

Algunos ajustes pueden mejorar el tiempo de carga LibreOffice y la capacidad de respuesta. Sin embargo, algunos también aumentar el uso de memoria RAM, así que úselos con cuidado. Se puede acceder a todos ellos en "Herramientas> Opciones".

*   Bajo "memoria":
    *   Reducir el número de pasos de Deshacer a una cifra inferior a 100, por ejemplo entre 20 y 30 pasos.
    *   En caché para gráficos, configure Uso para LibreOffice a 128 MB (desde el valor original de 20MB).
    *   Configure la memoria para cada objeto a 20 MB (desde el valor predeterminado de 5 MB).
    *   Si utiliza LibreOffice menudo, pruebe el Inicio Rápido de LibreOffice.
*   En Java'**, desactive Usar un entorno de ejecución Java.**

{{Nota | Para obtener una lista de las funciones que dependen de Java, consulte esta página: [http://wiki.services.openoffice.org/wiki/Java](http://wiki.services.openoffice.org/wiki/Java) - Aún se necesita}?}

## Solución de problemas

### Sustitución de fuentes

Esta configuración se puede cambiar en las opciones LibreOffice. En el menú desplegable, seleccione *Herramientas> Opciones> LibreOffice> Fuentes*. Marque la casilla que dice*Aplicar*sustitución de tablas. Escriba `Andale Sans UI` en el cuadro Fuente y elija su tipo de letra seado para la opción de reemplazar*con*. Cuando termine, haga clic en la*marca*. A continuación, seleccione el*siempre*y*sólo*opciones de pantalla en el cuadro a continuación. Haga clic en Aceptar. A continuación, tendrá que ir a*Herramientas> Opciones LibreOffice>*> Ver y desmarque la opción "Usar fuente del sistema para la interfaz de usuario ". Si utiliza una fuente no antialised, como Arial, también tendrá que desactivar "anti-aliasing de pantalla de la fuente" antes de las fuentes de menú procesar correctamente.

### No se pueden ingresar acentos

Descripción del problema: En las otras aplicaciones los acentos funcionan bien, en libreoffice no los puedo ingresar usando el teclado, el problema parecen ser las teclas muertas pues la ñ si funciona pero las tíldes no, adicionalmente puedo copiar (por ejemplo de Firefox) y pegar las letras con tildes.

Solución:

En /etc/locale.gen desmarcar (quitar #) de:

*   es_ES.UTF-8
*   es_ES.ISO-8859-1
*   en_US.UTF-8
*   en_US.ISO-8859-1

luego en la consola como root

```
# locale-gen

```

y en libreoffice Opciones -> Configuración del Idioma -> Idioma de: --> Interfaz del Usuario: Predeterminado - Español - España