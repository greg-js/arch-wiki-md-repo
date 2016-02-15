## Contents

*   [1 ¿Como crear un PDF desde un PS de manera sencilla?](#.C2.BFComo_crear_un_PDF_desde_un_PS_de_manera_sencilla.3F)
*   [2 ps2pdf](#ps2pdf)
    *   [2.1 Explicación](#Explicaci.C3.B3n)
    *   [2.2 Equivocaciones](#Equivocaciones)

# ¿Como crear un PDF desde un PS de manera sencilla?

Esta pagina debería ayudar a las personas que se preguntan a si mismos (tal vez por segunda, tercera o mas veces) esta pregunta y tal vez encontraron la respuesta alguna vez, pero nunca la han escrito o recordado correctamente.

# ps2pdf

Un comando lo hace todo:

```
ps2pdf -sPAPERSIZE=a4 -dOptimize=true -dEmbedAllFonts=true archivops.ps

```

## Explicación

*   ps2pdf es la envoltura a ghostscript (ps2pdf es parte del paquete ghostscript)
*   con -sPAPERSIZE=algo definís el tamaño del papel

**Tip:** ¿Preguntándose acerca de tamaños de papel validos? Mire [aquí](http://www.cs.wisc.edu/~ghost/doc/cvs/Use.htm#Known_paper_sizes)

*   -dOptimize=true permite al PDF creado ser optimizado para cargar
*   -dEmbedAllFonts=true hace que las fuentes se vean siempre bien

## Equivocaciones

*   Vos no podes elegir la orientación del papel con ps2pdf. Si tu archivo PS esta "sano", este contiene la orientación del papel. Si estas intentando usar un archivo PS encapsulado, vas a tener problemas si este no encaja en el -sPAPERSIZE que especificaste, ya que los archivos EPS usualmente no contienen información acerca de la orientación del papel. Una solución es crear un nuevo papel en la configuración de Ghostscript (y llamarlo, por ejemplo, "slide") y usarlo como -sPAPERSIZE=slide