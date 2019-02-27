Artículos relacionados

*   [GIMP/CMYK support (Español)](/index.php?title=GIMP/CMYK_support_(Espa%C3%B1ol)&action=edit&redlink=1 "GIMP/CMYK support (Español) (page does not exist)")
*   [List of applications/Multimedia (Español)#Editores de imágenes matriciales o ráster](/index.php/List_of_applications/Multimedia_(Espa%C3%B1ol)#Editores_de_imágenes_matriciales_o_ráster "List of applications/Multimedia (Español)")

[GIMP](https://en.wikipedia.org/wiki/GIMP "wikipedia:GIMP") es un potente programa de edición de imágenes ráster, y comunmente usado para el retoque fotográico, composición de imágenes, y trabajo de diseño gráfico general. Puede ser usado como un simple programa de pintura, un programa de calidad de retoque fotográfico de calidad profesional, un sistema en línea de procesamiento por lotes, un procesador de imágenes de producción en masa, un convertidor de formato de imagen, etc.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Tips y trucos](#Tips_y_trucos)
    *   [2.1 Subtítulos](#Subtítulos)
    *   [2.2 Crear un círculo](#Crear_un_círculo)
*   [3 Solución de problemas](#Solución_de_problemas)
    *   [3.1 Texto verde](#Texto_verde)
    *   [3.2 Ocultar Noto](#Ocultar_Noto)
    *   [3.3 Archivos PDF](#Archivos_PDF)
*   [4 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [gimp](https://www.archlinux.org/packages/?name=gimp).

**Tip:** GIMP implementa un de sistema de complementos y los repositorios ([official](https://www.archlinux.org/packages/?sort=&q=gimp&maintainer=&flagged=), [AUR](https://aur.archlinux.org/packages/?O=0&SeB=nd&K=gimp&outdated=off&SB=n&SO=a&PP=50&do_Search=Go)) contienen más complementos que los listados en las dependencias opcionales del paquete.

## Tips y trucos

### Subtítulos

Para subtitular una imagen siga éstos pasos después de introducir el texto deseado:

1.  Clic *Capa* y *Texto a ruta*
2.  Clic *Selección* y *A patir de selección*
3.  Clic *Selección* e *Invertir*
4.  Clic *Editar* y *Trazar selección*

### Crear un círculo

Para dibujar un círculo en GIMP siga éstos pasos:

1.  Seleccione la *Herramienta de selección elíptica* y sostenga `Shift`
2.  Clic *Editar* y *Rellenar con color*
3.  Clic *Selección* y *Encoger*
4.  Presione `Delete`

**Tip:** *Agrandar* y *Borde* dan el mismo resultado.

## Solución de problemas

### Texto verde

Agrega lo siguiente a `~/.config/GIMP/2.10/fonts.conf` si ve un tinte verde alrededor las letras con antialiasing habilitado:

```
<?xml version='1.0'?>
<!DOCTYPE fontconfig SYSTEM 'fonts.dtd'>
<fontconfig>
  <match target="font">
    <edit name="rgba" mode="assign">
      <const>none</const>
    </edit>
  </match>
</fontconfig>

```

### Ocultar Noto

Agregue lo siguiente `~/.config/GIMP/2.10/fonts.conf` si tiene instaladas [noto-fonts](https://www.archlinux.org/packages/?name=noto-fonts) y le gustaría removerlas desde la lista de fuentes de GIMP:

```
<?xml version='1.0'?>
<!DOCTYPE fontconfig SYSTEM 'fonts.dtd'>
<fontconfig>
  <rejectfont>
    <glob>/usr/share/fonts/noto</glob>
  </rejectfont>
</fontconfig>

```

Vea [fonts-conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fonts-conf.5) y [Configuración de fuentes#Lista blanca y lista negra de fuentes](/index.php/Font_configuration_(Espa%C3%B1ol) "Font configuration (Español)") para más información.

### Archivos PDF

GIMP requiere de la biblioteca [poppler-glib](https://www.archlinux.org/packages/?name=poppler-glib) para abrir archivos PDF o informará que son no están reconocidos.

Dado que GIMP rasteriza archivos PDF desde el principio, no explotará las capacidades intrínsecas de los PDF mientras se editan. Otros programas (como [LibreOffice Draw](/index.php/LibreOffice "LibreOffice")) pueden ser usados para una mejor edición de archivos PDF.

## Véase también

*   [Official website](https://www.gimp.org/)
*   [debian:GIMP](https://wiki.debian.org/GIMP "debian:GIMP")
*   [GIMP Magazine](https://gimpmagazine.org/resources/) - Index of GIMP resources, tutorials, communities
*   [GIMP Forum](http://gimp-forum.net/)