_Este documento describe como configurar un menú gráfico de arranque utilizando [lilo](/index.php/Lilo "Lilo"). Se esboza una manera genérica de hacerlo por usted mismo, y se le proporcionan además algunos valores que hacen que quede bonito en Arch._

## Prepare su imagen

*   Encuentre un fondo de pantalla que quiera utilizar. Debería ser sencillo porque tiene que dejarlo en 16 colores.
*   Ábralo con El Gimp.
*   Ajústelo a 640x480.
*   Cámbielo a modo indexado (Imagen-->Modo-->Indexado).
*   Seleccione "Crear paleta optima" y ajústela a 16 colores. Elija el modo de difuminado que más le guste.
*   Abra el cuadro de diálogo "Paleta indexada". Tome nota de qué colores quiere utilizar para las entradas de texto del menú, el reloj, etc. En su archivo `lilo.conf`, usted se referirá a los colores por el índice.
*   Grabe la imagen como formato bmp en su directorio /boot.

Si le apetece, puede utilizar [https://www.archlinux.org/~dusty/arch-lilo.bmp](https://www.archlinux.org/~dusty/arch-lilo.bmp)
O puede usar ésta: [http://www.kde-look.org/content/show.php?content=18187](http://www.kde-look.org/content/show.php?content=18187)

## Prepare su archivo lilo.conf

*   pacman -S lilo
*   Lea `man lilo.conf`.
*   lea de nuevo `man lilo.conf`.
*   Hay algunas opciones específicas para el menú grafico:
    *   bitmap=<archivo-tipo-bitmap> Establezca ésta apuntando al archivo de imagen que grabó anteriormente. Por ejemplo:

```
bitmap=/boot/arch-lilo.bmp
bmp-colors=<fg>,<bg>,<sh>,<hfg>,<hbg>,<hsh>

```

Estos son los colores de las entradas del menún. Se refieren al primer plano de la pantalla ("foreground"), al segundo plano ("background")", y los colores para la sombra ("shadow colours")" respectivamente, seguido por los mismos pero para texto resaltado. No inserte espacios. Los valores utilizados son indices que apuntan a la paleta de colores que descubrió en la etapa anterior. Si lo prefiere, puede dejar un valor en blanco (pero no se olvide de la coma). El fondo por defecto es transparente, la sombra por defecto es no tener ninguna.

*   bmp-table=<x>,<y>,<ncol>,<nrow>,<xsep>,<spill> Esta opción especifica donde se situará el menú. x e y son las coordenadas (medidas en número de caracteres). Puede tambień aplicar el sufijo p para indicar que las coordenadas son en número de pixels. Lea man lilo.conf para ver más opciones.
*   bmp-timer=<x>,<y>,<fg>,<bg>,<sh> Esta opción especifica las coordenadas y el color del indicador de tiempo que descuenta el tiempo restante para que arranque la entrada por defecto. Utiliza indices de colores para los colores, y coordenadas en caracteres (o en pixels).
*   Puede utilizar éstas con el archivo arch-lilo.bmp de antes:

```
  bitmap=/boot/arch-lilo.bmp
  bmp-colors=1,0,8,3,8,1
  bmp-table=250p,150p,1,18
  bmp-timer=250p,350p,3,8,1

```

*   Grabe su archivo `lilo.conf`
*   Ejecute `lilo` como root
*   Reinicie y vea como queda