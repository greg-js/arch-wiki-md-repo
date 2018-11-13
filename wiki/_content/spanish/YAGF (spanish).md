Artículos relacionados

*   [Listado de aplicaciones#Software OCR](/index.php/List_of_applications_(Espa%C3%B1ol)#Software_de_reconocimiento_.C3.B3ptico_de_caracteres_.28siglas_en_ingl.C3.A9s_OCR.29 "List of applications (Español)")

[YAGF](http://sourceforge.net/projects/yagf-ocr/) es una interfaz gráfica para el programa ROC (Reconocimiento Óptico de Caracteres) [cuneiform](https://en.wikipedia.org/wiki/CuneiForm_(software) en la plataforma Linux. Con YAGF puede escanear imágenes vía XSane, realizar el preprocesado de las imágenes y reconocer textos usando cuneiform desde un centro de comandos único. YAGF también facilita el escaneado y reconocimiento de múltiples imágenes de forma secuencial.

## Contents

*   [1 Instalación](#Instalación)
*   [2 Idiomas soportados](#Idiomas_soportados)
*   [3 Uso](#Uso)
    *   [3.1 Adquisición de imágenes](#Adquisición_de_imágenes)
    *   [3.2 Preprocesado de imágenes](#Preprocesado_de_imágenes)
    *   [3.3 El reconocimiento de texto](#El_reconocimiento_de_texto)
    *   [3.4 Guardando los resultados](#Guardando_los_resultados)
*   [4 Véase también](#Véase_también)

## Instalación

YAGF tiene como dependencias Qt4 y el paquete de corrección ortográfica [aspell](https://www.archlinux.org/packages/?name=aspell). Si desea poder cargar imágenes en YAGF desde un escáner directamente, debe instalar el software [XSane](/index.php/SANE_(Espa%C3%B1ol) "SANE (Español)"). Además tendrá que instalar [cuneiform](https://www.archlinux.org/packages/?name=cuneiform) para el reconocimiento de texto.

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") [yagf](https://aur.archlinux.org/packages/yagf/) desde AUR.

## Idiomas soportados

Los siguiente idiomas están disponibles para el reconocimiento: alemán, checo, danés, estonio, español, francés, holandés, húngaro, inglés, italiano, letón, lituano, polaco, portugués, rumano, ruso, sueco, ucraniano.

## Uso

La digitalización de textos con YAGF se compone de varias etapas: adquisición de imágenes, procesamiento de imágenes (si fuera necesario), el reconocimiento en si mismo, y guardar los resultados.

### Adquisición de imágenes

Puede reconocer texto de imágenes almacenadas en su disco duro, o puede escanear imágenes y pasárselas directamente a YAGF. Haga clic en Archivo/Abrir imagen... para cargar una imagen desde su disco duro. YAGF soporta la mayoría de los formatos de imágenes rasterizadas (JPEG, PNG, BMP, TIFF, GIF, PNM, PPM, PBM). Si el nombre del archivo cargado tiene la forma *nombreXXX.ext*, donde *XXX* es algún número, puede moverse hacia el siguiente/hacia el anterior fichero en la serie correspondiente con los botones de navegación. Por ejemplo, si carga un fichero que se llame *MiPag06.jpg*, El botón "Ir a la siguiente imagen" intentará abrir el fichero *MiPag07.jpg*. Todas las imágenes abiertas se mostrarán en la barra de imágenes.

Puede adquirir también las imágenes directamente desde un escáner con XSane. Cuando en YAGF haga clic en Archivo/Escanear, XSane se iniciará. Configure las opciones de escaneado de XSane y haga clic en el botón *Escanear* de XSane. Cuando haya finalizado el escaneado, la imagen se abrirá en la ventana de imágenes de YAGF. Si quieres escanear varias imágenes, puede repetir este proceso tantas veces como desee. En cada ocasión se mostrará en YAGF la última imagen escaneada. Puede moverse entre las diferentes imágenes usando los botones de navegación. Puede mantener la ventana de Izquierda abierta mientras trabaje con YAGF. Cuando salga de YAGF, se cerrará automáticamente la ventana de XSane. Todas las imágenes adquiridas se mostrarán como miniaturas en la barra de imágenes de la izquierda. Puede guardar estas imágenes en un directorio a parte use el botón Guardar Imagen de la barra de imágenes.

### Preprocesado de imágenes

Existen varias opciones de preprocesado disponibles en YAGF. Puede rotar las imágenes ya cargadas si no están correctamente posicionadas. Las imágenes pueden rotarse de 90 en 90 grados en ambos sentidos y en 180 grados. Hay botones especiales para ello en la parte superior de ventana de visualización de las imágenes. Si lo que desea es reconocer solo una parte de una página, puede seleccionar un bloque rectangular para el reconocimiento. El bloque es seleccionado en la ventana de visualización de imágenes. El bloque es redimensionable, arrastrando con el ratón los bordes del rectángulo. Aunque generalmente la imagen escaneada no encaja dentro de la ventana de visualización , puede escalar la imagen, agrandándola o encogiéndola, para afinar el proceso de selección. Esta operación no cambia la resolución de la imagen pasada a cuneiform para su reconocimiento. También puede usar `Ctrl++` y `Ctrl+-` o la rueda del ratón mientras mantiene pulsado `Ctrl` para escalar las imágenes. Puede cambiar el tamaño de la fuente en el editor de texto de la misma forma.

### El reconocimiento de texto

Previamente al reconocimiento del texto, debe seleccionar el idioma (o el conjunto de idiomas si el documento está escrito en varios idiomas) de reconocimiento.

Cada fragmento de texto reconocido se añade a la venta del editor de texto al final del texto ya reconocido como un nuevo párrafo.

Por defecto YAGF, comprueba comprueba la ortografía en los textos usando libaspell. Normalmente aspell está instalado en su sistema con diccionarios para el idioma configurado en su sistema y el inglés(Si este no es el idioma configurado) . Si desea corrección ortográfica para textos en otros idiomas, tiene que instalar diccionarios aspell aparte (generalmente disponible en el repositorio de software de su sistema). YAGF le advertirá cuando no puede encontrar un diccionario para el idioma seleccionado. Desactive la corrección ortográfica si no desea ver estos avisos.

Si tiene varias imágenes abiertas en la barra de imágenes, puede usar el reconocimiento por lotes para reconocer el texto de todas las imágenes secuencialmente. Haga clic en el botón "Reconocer todas las páginas. Las imágenes serán automáticamente cargadas y reconocidas una tras otra y aparecerá un diálogo con su progreso . Puede parar el reconocimiento haciendo clic en el botón *Abortar* del diálogo.

### Guardando los resultados

El texto reconocido puede salvarse a disco como un fichero de texto plano o como html codificado en UTF-8 o copiado al portapapeles del sistema. El botón "Copiar al portapapeles" copia tanto un fragmento de texto seleccionado como todo el texto en caso de que ningún fragmento de texto sea seleccionado.

## Véase también

*   [Listado de aplicaciones#Software OCR](/index.php/List_of_applications_(Espa%C3%B1ol)#Software_de_reconocimiento_.C3.B3ptico_de_caracteres_.28siglas_en_ingl.C3.A9s_OCR.29 "List of applications (Español)")
*   [http://symmetrica.net/cuneiform-linux/yagf-en.html](http://symmetrica.net/cuneiform-linux/yagf-en.html) - YAGF home page
*   [https://launchpad.net/cuneiform-linux](https://launchpad.net/cuneiform-linux) - Linux port of Cuneiform