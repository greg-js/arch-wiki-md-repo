**Status de tradução:** Esse artigo é uma tradução de [Language checking](/index.php/Language_checking "Language checking"). Data da última tradução: 2019-07-07\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Language_checking&diff=0&oldid=576590) na versão em inglês.

Esse artigo cobre softwares corretores/[verificadores ortográficos](https://en.wikipedia.org/wiki/pt:Corretor_ortogr%C3%A1fico "wikipedia:pt:Corretor ortográfico") e [verificadores gramaticais](https://en.wikipedia.org/wiki/pt:Corretor_gramatical "wikipedia:pt:Corretor gramatical").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Verificadores ortográficos](#Verificadores_ortográficos)
    *   [1.1 Específico do idioma](#Específico_do_idioma)
    *   [1.2 Enchant](#Enchant)
    *   [1.3 Aplicativos](#Aplicativos)
*   [2 Verificadores gramaticais](#Verificadores_gramaticais)
    *   [2.1 Aplicativos](#Aplicativos_2)

## Verificadores ortográficos

*   **[GNU Aspell](https://en.wikipedia.org/wiki/GNU_Aspell "wikipedia:GNU Aspell")** — Verificador ortográfico projetado para eventualmente substituir o Ispell, veja também [aspell(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/aspell.1) e o [documento info](http://aspell.net/man-html/index.html).

	[http://aspell.net/](http://aspell.net/) || [aspell](https://www.archlinux.org/packages/?name=aspell), [dicionários](https://www.archlinux.org/packages/?q=aspell-)

*   **[Hunspell](https://en.wikipedia.org/wiki/pt:Hunspell "wikipedia:pt:Hunspell")** — Verificador ortográfico e biblioteca e programa de analisador morfológico, veja também [hunspell(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hunspell.1).

	[https://hunspell.github.io/](https://hunspell.github.io/) || [hunspell](https://www.archlinux.org/packages/?name=hunspell), [dicionários](https://www.archlinux.org/packages/?q=hunspell-)

*   **[Ispell](https://en.wikipedia.org/wiki/Ispell "wikipedia:Ispell")** — Programa de verificação ortográfica interativa para o Unix, veja também [ispell(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ispell.1).

	[https://www.cs.hmc.edu/~geoff/ispell.html](https://www.cs.hmc.edu/~geoff/ispell.html) || [ispell](https://www.archlinux.org/packages/?name=ispell)

### Específico do idioma

*   **Hspell** — Verificador ortográfico hebraico

	[http://www.ivrix.org.il/projects/spell-checker/](http://www.ivrix.org.il/projects/spell-checker/) || [hspell](https://www.archlinux.org/packages/?name=hspell)

*   **Voikko** — Programa finlandês Verificador ortográfico e gramatical, hifenizador e coleção de dados relacionados a linguística

	[https://voikko.sourceforge.net](https://voikko.sourceforge.net) || [libvoikko](https://www.archlinux.org/packages/?name=libvoikko)

### Enchant

[Enchant](https://en.wikipedia.org/wiki/Enchant_(software) é uma biblioteca interfaceadora para a verificação ortográfica genérica, desenvolvido como parte do [AbiWord](/index.php/AbiWord_(Portugu%C3%AAs) "AbiWord (Português)"), com suporte a todos os verificadores ortográficos acima, com exceção do Ispell.

Enchant está disponível como o pacote [enchant](https://www.archlinux.org/packages/?name=enchant). Para seu uso e arquivo de ordem, veja [enchant-2(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/enchant-2.1).

Enchant é usado por vários aplicativos pelas bibliotecas [GTK](/index.php/GTK "GTK") a seguir:

*   **gspell** — API flexível para implementar verificação ortográfica em aplicativos GTK.

	[https://wiki.gnome.org/Projects/gspell](https://wiki.gnome.org/Projects/gspell) || [gspell](https://www.archlinux.org/packages/?name=gspell)

*   **GtkSpell** — Fornece realce no estilo de processador de texto e substituição de palavras com erro de escrita em um widget GtkTextView.

	[http://gtkspell.sourceforge.net/](http://gtkspell.sourceforge.net/) || [gtkspell](https://www.archlinux.org/packages/?name=gtkspell), [gtkspell3](https://www.archlinux.org/packages/?name=gtkspell3)

### Aplicativos

[Firefox](/index.php/Firefox "Firefox"), [Thunderbird](/index.php/Thunderbird "Thunderbird"), [Chromium](/index.php/Chromium "Chromium") e [LibreOffice](/index.php/LibreOffice "LibreOffice") podem todos usar dicionários Hunspell instalados no sistema, assim como dicionários/outros verificadores ortográficos instalados por meio de seu próprio sistema de extensão. Veja as seções a seguir:

*   [Firefox#Spell checking](/index.php/Firefox#Spell_checking "Firefox")
*   [Thunderbird#Spell checking](/index.php/Thunderbird#Spell_checking "Thunderbird")
*   [LibreOffice#Spell checking](/index.php/LibreOffice#Spell_checking "LibreOffice")

[AbiWord](/index.php/AbiWord_(Portugu%C3%AAs) "AbiWord (Português)") e [Gedit](/index.php/Gedit "Gedit") usam o Enchant.

## Verificadores gramaticais

*   **LanguageTool** — Verificador de idioma de código aberto, escrito em [Java](/index.php/Java_(Portugu%C3%AAs) "Java (Português)").

	[https://www.languagetool.org](https://www.languagetool.org) || [languagetool](https://www.archlinux.org/packages/?name=languagetool)

*   **Style and Diction** — Diction identifica frases prolixas e comumente mal utilizadas. Style analisa as características da superfície de um documento.

	[https://www.gnu.org/software/diction/](https://www.gnu.org/software/diction/) || [diction](https://aur.archlinux.org/packages/diction/)

### Aplicativos

[Firefox](/index.php/Firefox "Firefox"), [Thunderbird](/index.php/Thunderbird "Thunderbird"), [Chromium](/index.php/Chromium "Chromium") e [LibreOffice](/index.php/LibreOffice "LibreOffice") todos possuem suporte a verificação gramatical apenas por meio de extensões. Para o LibreOffice, veja [LibreOffice#Grammar checking](/index.php/LibreOffice#Grammar_checking "LibreOffice").

[AbiWord](/index.php/AbiWord_(Portugu%C3%AAs) "AbiWord (Português)") possui um verificador gramatical interno, veja [AbiWord (Português)#Verificação gramatical](/index.php/AbiWord_(Portugu%C3%AAs)#Verificação_gramatical "AbiWord (Português)").