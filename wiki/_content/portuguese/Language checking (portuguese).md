**Status de tradução:** Esse artigo é uma tradução de [Language checking](/index.php/Language_checking "Language checking"). Data da última tradução: 2018-12-17\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Language_checking&diff=0&oldid=559295) na versão em inglês.

Esse artigo cobre softwares verificadores/[corretores ortográficos](https://en.wikipedia.org/wiki/pt:Corretor_ortogr%C3%A1fico "wikipedia:pt:Corretor ortográfico") e [corretores gramaticais](https://en.wikipedia.org/wiki/pt:Corretor_gramatical "wikipedia:pt:Corretor gramatical").

## Contents

*   [1 Corretores ortográficos](#Corretores_ortográficos)
    *   [1.1 Específico do idioma](#Específico_do_idioma)
    *   [1.2 Enchant](#Enchant)
    *   [1.3 Aplicativos](#Aplicativos)
*   [2 Corretores gramaticais](#Corretores_gramaticais)
    *   [2.1 Aplicativos](#Aplicativos_2)

## Corretores ortográficos

*   **[GNU Aspell](https://en.wikipedia.org/wiki/GNU_Aspell "wikipedia:GNU Aspell")** — Corretor ortográfico projetado para eventualmente substituir o Ispell, veja também [aspell(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/aspell.1) e o [documento info](http://aspell.net/man-html/index.html).

	[http://aspell.net/](http://aspell.net/) || [aspell](https://www.archlinux.org/packages/?name=aspell), [dicionários](https://www.archlinux.org/packages/?q=aspell-)

*   **[Hunspell](https://en.wikipedia.org/wiki/pt:Hunspell "wikipedia:pt:Hunspell")** — Corretor ortográfico e biblioteca e programa de analisador morfológico, veja também [hunspell(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hunspell.1).

	[https://hunspell.github.io/](https://hunspell.github.io/) || [hunspell](https://www.archlinux.org/packages/?name=hunspell), [dicionários](https://www.archlinux.org/packages/?q=hunspell-)

*   **[Ispell](https://en.wikipedia.org/wiki/Ispell "wikipedia:Ispell")** — Programa de correção ortográfica interativa para o Unix, veja também [ispell(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ispell.1).

	[https://www.cs.hmc.edu/~geoff/ispell.html](https://www.cs.hmc.edu/~geoff/ispell.html) || [ispell](https://www.archlinux.org/packages/?name=ispell)

### Específico do idioma

*   **Hspell** — Corretor ortográfico hebraico

	[http://www.ivrix.org.il/projects/spell-checker/](http://www.ivrix.org.il/projects/spell-checker/) || [hspell](https://www.archlinux.org/packages/?name=hspell)

*   **Voikko** — Programa finlandês corretor ortográfico e gramatical, hifenizador e coleçaõ de dados relacionados a linguística

	[https://voikko.sourceforge.net](https://voikko.sourceforge.net) || [libvoikko](https://www.archlinux.org/packages/?name=libvoikko)

### Enchant

[Enchant](https://en.wikipedia.org/wiki/Enchant_(software) é uma biblioteca interfaceadora para a correção ortográfica genérica, desenvolvido como parte do [Abiword](/index.php/Abiword "Abiword"), com suporte a todos os verificadores ortográficos acima, com exceção do Ispell.

Enchant está disponível como o pacote [enchant](https://www.archlinux.org/packages/?name=enchant). Para seu uso e arquivo de ordem, veja [enchant-2(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/enchant-2.1).

Enchant é usado por vários aplicativos pelas bibliotecas [GTK](/index.php/GTK "GTK") a seguir:

*   **gspell** — API flexível para implementar correção ortográfica em aplicativos GTK+.

	[https://wiki.gnome.org/Projects/gspell](https://wiki.gnome.org/Projects/gspell) || [gspell](https://www.archlinux.org/packages/?name=gspell)

*   **GtkSpell** — Fornece realce no estilo de processador de texto e substituição de palavras com erro de escrita em um widget GtkTextView.

	[http://gtkspell.sourceforge.net/](http://gtkspell.sourceforge.net/) || [gtkspell](https://www.archlinux.org/packages/?name=gtkspell), [gtkspell3](https://www.archlinux.org/packages/?name=gtkspell3)

### Aplicativos

[Firefox](/index.php/Firefox "Firefox"), [Thunderbird](/index.php/Thunderbird "Thunderbird"), [Chromium](/index.php/Chromium "Chromium") e [LibreOffice](/index.php/LibreOffice "LibreOffice") podem todos usar dicionários Hunspell instalados no sistema, assim como dicionários/outros corretores ortográficos instalados por meio de seu próprio sistema de extensão. Veja as seções a seguir:

*   [Firefox#Spell checking](/index.php/Firefox#Spell_checking "Firefox")
*   [Thunderbird#Spell checking](/index.php/Thunderbird#Spell_checking "Thunderbird")
*   [LibreOffice#Spell checking](/index.php/LibreOffice#Spell_checking "LibreOffice")

[Abiword](/index.php/Abiword "Abiword") e [Gedit](/index.php/Gedit "Gedit") usam o Enchant.

## Corretores gramaticais

*   **LanguageTool** — Verificador de idioma de código aberto, escrito em [Java](/index.php/Java "Java").

	[https://www.languagetool.org](https://www.languagetool.org) || [languagetool](https://www.archlinux.org/packages/?name=languagetool)

*   **Style and Diction** — Dction identifica frases prolixas e comumente mal utilizadas. Style analisa as características da superfície de um documento.

	[https://www.gnu.org/software/diction/](https://www.gnu.org/software/diction/) || [diction](https://aur.archlinux.org/packages/diction/)

### Aplicativos

[Firefox](/index.php/Firefox "Firefox"), [Thunderbird](/index.php/Thunderbird "Thunderbird"), [Chromium](/index.php/Chromium "Chromium") e [LibreOffice](/index.php/LibreOffice "LibreOffice") todos possuem suporte a correção gramatical apenas por meio de extensões. Para o LibreOffice, veja [LibreOffice#Grammar checking](/index.php/LibreOffice#Grammar_checking "LibreOffice").

[Abiword](/index.php/Abiword "Abiword") possui um corretor gramatical interno, veja [Abiword#Grammar checking](/index.php/Abiword#Grammar_checking "Abiword").