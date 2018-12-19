**Estado de la traducción**
Este artículo es una traducción de [Language checking](/index.php/Language_checking "Language checking"), revisada por última vez el **2018-12-18**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Language_checking&diff=0&oldid=559466) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Este arículo cubre los programas de [corrección ortográfica](https://en.wikipedia.org/wiki/es:Corrector_ortogr%C3%A1fico "wikipedia:es:Corrector ortográfico") y de [corrección gramatical](https://en.wikipedia.org/wiki/Grammar_checker "wikipedia:Grammar checker").

## Contents

*   [1 Correctores ortográficos](#Correctores_ortográficos)
    *   [1.1 Idioma específico](#Idioma_específico)
    *   [1.2 Enchant](#Enchant)
    *   [1.3 Aplicaciones](#Aplicaciones)
*   [2 Correctores gramaticales](#Correctores_gramaticales)
    *   [2.1 Aplicaciones](#Aplicaciones_2)

## Correctores ortográficos

*   **[GNU Aspell](https://en.wikipedia.org/wiki/GNU_Aspell "wikipedia:GNU Aspell")** — Corrector ortográfico diseñado para reemplazar eventualmente a Ispell, véase también [aspell(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/aspell.1) y el [documento de información](http://aspell.net/man-html/index.html).

	[http://aspell.net/](http://aspell.net/) || [aspell](https://www.archlinux.org/packages/?name=aspell), [dictionaries](https://www.archlinux.org/packages/?q=aspell-)

*   **[Hunspell](https://en.wikipedia.org/wiki/es:Hunspell "wikipedia:es:Hunspell")** — Corrector ortográfico y biblioteca y programa del analizador morfológico, véase también [hunspell(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hunspell.1).

	[https://hunspell.github.io/](https://hunspell.github.io/) || [hunspell](https://www.archlinux.org/packages/?name=hunspell), [dictionaries](https://www.archlinux.org/packages/?q=hunspell-)

*   **[Ispell](https://en.wikipedia.org/wiki/es:Ispell "wikipedia:es:Ispell")** — Programa interactivo de corrección ortográfica para Unix, véase también [ispell(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ispell.1).

	[https://www.cs.hmc.edu/~geoff/ispell.html](https://www.cs.hmc.edu/~geoff/ispell.html) || [ispell](https://www.archlinux.org/packages/?name=ispell)

### Idioma específico

*   **Hspell** — Corrector ortográfico hebreo

	[http://www.ivrix.org.il/projects/spell-checker/](http://www.ivrix.org.il/projects/spell-checker/) || [hspell](https://www.archlinux.org/packages/?name=hspell)

*   **Voikko** — Corrector ortográfico y gramatical finlandés, separador de palabras y recopilación de datos lingüísticos relacionados

	[https://voikko.sourceforge.net](https://voikko.sourceforge.net) || [libvoikko](https://www.archlinux.org/packages/?name=libvoikko)

### Enchant

[Enchant](https://en.wikipedia.org/wiki/es:Enchant_(software) es una biblioteca para el corrector ortográfico genérico, desarrollada como parte de [Abiword](/index.php/Abiword_(Espa%C3%B1ol) "Abiword (Español)"), que admite todos los correctores ortográficos anteriores, aparte de Ispell.

Enchant está disponible con el paquete [enchant](https://www.archlinux.org/packages/?name=enchant). Para su uso y ordenación de archivo, véase [enchant-2(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/enchant-2.1).

Enchant es utilizado por muchas aplicaciones a través de las siguientes bibliotecas [GTK](/index.php/GTK_(Espa%C3%B1ol) "GTK (Español)"):

*   **gspell** — API flexible para implementar la corrección ortográfica en aplicaciones GTK+.

	[https://wiki.gnome.org/Projects/gspell](https://wiki.gnome.org/Projects/gspell) || [gspell](https://www.archlinux.org/packages/?name=gspell)

*   **GtkSpell** — Proporciona resaltado y reemplazo de palabras mal escritas al estilo de un procesador de textos en un widget GtkTextView.

	[http://gtkspell.sourceforge.net/](http://gtkspell.sourceforge.net/) || [gtkspell](https://www.archlinux.org/packages/?name=gtkspell), [gtkspell3](https://www.archlinux.org/packages/?name=gtkspell3)

### Aplicaciones

[Firefox](/index.php/Firefox_(Espa%C3%B1ol) "Firefox (Español)"), [Thunderbird](/index.php/Thunderbird "Thunderbird"), [Chromium](/index.php/Chromium_(Espa%C3%B1ol) "Chromium (Español)") y [LibreOffice](/index.php/LibreOffice_(Espa%C3%B1ol) "LibreOffice (Español)") pueden todos utilizar los diccionarios Hunspell instalados en todo el sistema, así como los diccionarios/otros correctores ortográficos instalados a través de sus propios sistemas de extensión. Véase las siguientes secciones:

*   [Firefox#Spell checking](/index.php/Firefox#Spell_checking "Firefox")
*   [Thunderbird#Spell checking](/index.php/Thunderbird#Spell_checking "Thunderbird")
*   [LibreOffice#Spell checking](/index.php/LibreOffice#Spell_checking "LibreOffice")

[Abiword](/index.php/Abiword_(Espa%C3%B1ol) "Abiword (Español)") y [Gedit](/index.php/Gedit_(Espa%C3%B1ol) "Gedit (Español)") utilizan Enchant.

## Correctores gramaticales

*   **LanguageTool** — Corrector de lenguaje de código abierto, escrito en [Java](/index.php/Java_(Espa%C3%B1ol) "Java (Español)").

	[https://www.languagetool.org](https://www.languagetool.org) || [languagetool](https://www.archlinux.org/packages/?name=languagetool)

*   **Style and Diction** — Diction identifica frases largas y mal utilizadas. Style analiza las características superficiales de un documento.

	[https://www.gnu.org/software/diction/](https://www.gnu.org/software/diction/) || [diction](https://aur.archlinux.org/packages/diction/)

### Aplicaciones

[Firefox](/index.php/Firefox_(Espa%C3%B1ol) "Firefox (Español)"), [Thunderbird](/index.php/Thunderbird "Thunderbird"), [Chromium](/index.php/Chromium_(Espa%C3%B1ol) "Chromium (Español)") y [LibreOffice](/index.php/LibreOffice_(Espa%C3%B1ol) "LibreOffice (Español)") soportan todos la corrección gramatical solo a través de extensiones. Para LibreOffice, véase [LibreOffice#Grammar checking](/index.php/LibreOffice#Grammar_checking "LibreOffice").

[Abiword](/index.php/Abiword_(Espa%C3%B1ol) "Abiword (Español)") tiene un corrector gramatical incorporado, véase [Abiword#Grammar checking](/index.php/Abiword#Grammar_checking "Abiword").