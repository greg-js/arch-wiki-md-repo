**Estado de la traducción**
Este artículo es una traducción de [AbiWord](/index.php/AbiWord "AbiWord"), revisada por última vez el **2019-01-02**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=AbiWord&diff=0&oldid=561374) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[AbiWord](http://www.abisource.com/) es un procesador de textos que ofrece una alternativa más liviana que [LibreOffice](/index.php/LibreOffice_(Espa%C3%B1ol) "LibreOffice (Español)") Writer y [OpenOffice](/index.php/OpenOffice "OpenOffice") Writer, mientras que al mismo tiempo proporciona una gran funcionalidad. AbiWord admite muchos tipos de documentos estándar, como documentos ODF, documentos Microsoft Word, documentos WordPerfect, documentos Rich Text Format y páginas web HTML.

## Contents

*   [1 Instalación](#Instalación)
*   [2 Directorio de configuración del usuario](#Directorio_de_configuración_del_usuario)
*   [3 Plantillas](#Plantillas)
    *   [3.1 Usar las plantillas](#Usar_las_plantillas)
    *   [3.2 Crear o cambiar plantillas](#Crear_o_cambiar_plantillas)
*   [4 Comprobación de gramática](#Comprobación_de_gramática)
*   [5 Cambiar los atajos de teclado](#Cambiar_los_atajos_de_teclado)
*   [6 Fuentes LaTeX](#Fuentes_LaTeX)
*   [7 Solución de problemas](#Solución_de_problemas)
    *   [7.1 Solución para el cuelgue del diálogo de impresión](#Solución_para_el_cuelgue_del_diálogo_de_impresión)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [abiword](https://www.archlinux.org/packages/?name=abiword). Es posible que desee instalar diccionarios si desea realizar una revisión ortográfica, el cual puede ser proporcionado por el paquete [aspell-es](https://www.archlinux.org/packages/?name=aspell-es) para el idioma español.

Para solucionar los problemas del cursor pequeño y el texto desalineado, instale o [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) o [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) y [ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont).

## Directorio de configuración del usuario

Desde la versión 3.0, AbiWord utiliza la carpeta `~/.config/abiword` para almacenar los archivos del usuario.

Las versiones anteriores de AbiWord utilizaban `~/.config/AbiSuite`, y, si se encuentra al iniciarse, se le cambiará automáticamente el nombre en consecuencia. Si tanto `~/.config/AbiSuite` como `~/.config/abiword` no existen , AbiWord **no** la creará.

## Plantillas

AbiWord proporciona un sistema de plantillas que permite acelerar la escritura de documentos comunes. Las plantillas se proporcionan como archivos *.awt*, para **A**bi**W**ord **T**emplate.

Los archivos de plantillas se buscan dentro de las carpetas `/usr/share/abiword-3.0/templates` y `~/.config/abiword/templates`.

### Usar las plantillas

En un nuevo documento, seleccione *Archivo > Nuevo utilizando una plantilla...*, luego, en el cuadro de diálogo "Nuevo documento", seleccione una de las plantillas que se encuentran listadas, o haga clic en "Abrir" para navegar por sus archivos en busca de un archivo AbiWord (no necesariamente un archivo *.awt*).

### Crear o cambiar plantillas

AbiWord le permite crear sus propios archivos de plantilla, con el estilo, texto, tablas, etc. deseados.

Para crear/cambiar un archivo de plantilla, simplemente abra un documento nuevo/existente y realice los cambios deseados al archivo. Luego, use la opción del menú "Guardar como" para nombrarlo como desee, con *.awt* como extensión (por ejemplo, *foobar.awt*) y guárdelo en `~/.config/abiword/templates`. Ahora, puede acceder a su nueva plantilla en *Archivo > Nuevo utilizando una plantilla...* por su nombre de archivo (*foobar.awt* en el ejemplo dado).

**Nota:** Si no existe, la carpeta `templates` se creará automáticamente al iniciarse dentro de `~/.config/abiword/`.

## Comprobación de gramática

Habilite la revisión gramatical desde *Editar > Preferencias > Corrección ortográfica > Verificación automática de gramática*.

## Cambiar los atajos de teclado

**Nota:** [Esta publicación de la wiki](http://www.abisource.com/wiki/Keyboard_bindings) tiene instrucciones sobre esto, pero algunas están desactualizadas y no funcionan

Puede cambiar los atajos de teclado predeterminados en AbiWord usando [KeyBindings](https://www.abisource.com/wiki/KeyBindings).

Para establecer los atajos de teclado, edite `~/.config/abiword/profile` y, dentro de la etiqueta `AbiPreferences`, agregue los *KeyBindings* deseados. Por ejemplo, puede agregar `KeyBindings="viEdit"` o `KeyBindings="emacs"`.

## Fuentes LaTeX

El paquete [abiword](https://www.archlinux.org/packages/?name=abiword) viene con una función que le permite al usuario insertar códigos LaTeX en un documento. Para que se muestren correctamente los símbolos matemáticos, es necesario descargar [latex-xft-fonts](http://movementarian.org/latex-xft-fonts-0.1.tar.gz) y guardarlo en el directorio `/usr/share/fonts`. Para instalar la fuente, extraiga el tarball y luego ejecute lo siguiente:

```
# fc-cache -fv

```

## Solución de problemas

### Solución para el cuelgue del diálogo de impresión

**Nota:** Este error ha sido reportado como inexistente para la versión 2.8.1 o superior. Sin embargo, esta sección permanecerá para las versiones anteriores o por si vuelve a aparecer

Por alguna razón, las versiones actuales de AbiWord y libgnomeprint no se llevan bien. La plantilla predeterminada `.abw` hace que el programa se bloquee cuando el usuario intenta imprimir. La solución es forzar a AbiWord a trabajar con el formato `.rtf` en su lugar. Al seguir los pasos que se muestran a continuación, establecerá el formato de guardado predeterminado a .rtf y engañará a AbiWord para que use un archivo `.rtf` como plantilla predeterminada.

Abra `~/.AbiSuite/AbiWord.Profile` y añada la siguiente línea en la segunda sección <scheme>.

```
DefaultSaveFormat=".rtf"

```

Debería ser algo así:

```
<Scheme
   name="_custom_"
   ZoomPercentage="64"
   DefaultSaveFormat=".rtf"
/>

```

Es necesario entonces cambiar la plantilla por defecto. Debe seguir exactamente estos pasos.

1.  Abra AbiWord y guarde un documento en blanco titulado `normal.rtf` en `~/.AbiSuite/templates/`. Si el directorio no existe, créelo.
2.  Cambie el nombre del archivo a *normal.awt*.

¡Sencillamente **no** guarde un archivo `.awt` en blanco! Debe engañar a AbiWord para que use una plantilla `.rtf` para que esto funcione.

Tan pronto como se resuelva el conflicto entre AbiWord y libgnomeprint, estas instrucciones ya no serán necesarias y deberán eliminarse.