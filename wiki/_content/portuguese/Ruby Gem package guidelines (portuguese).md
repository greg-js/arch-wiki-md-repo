**Status de tradução:** Esse artigo é uma tradução de [Ruby Gem package guidelines](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines"). Data da última tradução: 2018-11-01\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Ruby_Gem_package_guidelines&diff=0&oldid=552527) na versão em inglês.

**[Diretrizes de criação de pacotes](/index.php/Padr%C3%B5es_de_empacotamento_do_Arch "Padrões de empacotamento do Arch")**

* * *

[CLR](/index.php/Diretrizes_de_pacotes_CLR "Diretrizes de pacotes CLR") – [Cross](/index.php/Diretrizes_de_pacotes_de_ferramentas_de_compila%C3%A7%C3%A3o_cruzada "Diretrizes de pacotes de ferramentas de compilação cruzada") – [Eclipse](/index.php/Diretrizes_de_pacotes_de_plugin_do_Eclipse "Diretrizes de pacotes de plugin do Eclipse") – [Free Pascal](/index.php/Diretrizes_de_pacotes_Free_Pascal "Diretrizes de pacotes Free Pascal") – [GNOME](/index.php/Diretrizes_de_pacotes_GNOME "Diretrizes de pacotes GNOME") – [Go](/index.php/Diretrizes_de_pacotes_Go "Diretrizes de pacotes Go") – [Haskell](/index.php/Diretrizes_de_pacotes_Haskell "Diretrizes de pacotes Haskell") – [Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java") – [KDE](/index.php/Diretrizes_de_pacotes_KDE "Diretrizes de pacotes KDE") – [Kernel](/index.php/Diretrizes_de_pacotes_de_m%C3%B3dulos_de_kernel "Diretrizes de pacotes de módulos de kernel") – [Lisp](/index.php/Diretrizes_de_pacotes_Lisp "Diretrizes de pacotes Lisp") – [MinGW](/index.php/Diretrizes_de_pacotes_MinGW "Diretrizes de pacotes MinGW") – [Node.js](/index.php/Diretrizes_de_pacotes_Node.js "Diretrizes de pacotes Node.js") – [Nonfree](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") –[OCaml](/index.php/Diretrizes_de_pacotes_OCaml "Diretrizes de pacotes OCaml") – [Perl](/index.php/Diretrizes_de_pacotes_Perl "Diretrizes de pacotes Perl") – [PHP](/index.php/Diretrizes_de_pacotes_PHP "Diretrizes de pacotes PHP") – [Python](/index.php/Diretrizes_de_pacotes_Python "Diretrizes de pacotes Python") – [R](/index.php/Diretrizes_de_pacotes_R "Diretrizes de pacotes R") – [Ruby](/index.php/Diretrizes_de_pacotes_Ruby_Gem "Diretrizes de pacotes Ruby Gem") – [VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") – [Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web") – [Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine")

Escrever [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") para softwares escritos no [Ruby](/index.php/Ruby "Ruby").

## Contents

*   [1 Nomenclatura de pacote](#Nomenclatura_de_pacote)
    *   [1.1 Pacotes versionados](#Pacotes_versionados)
*   [2 Exemplos](#Exemplos)
*   [3 Notas](#Notas)
    *   [3.1 Quarry](#Quarry)
*   [4 Pegadinhas](#Pegadinhas)
    *   [4.1 Pacote contém referência a $pkgdir](#Pacote_cont.C3.A9m_refer.C3.AAncia_a_.24pkgdir)

## Nomenclatura de pacote

Para bibliotecas, use `ruby-$gemname`. Para aplicativos, use o nome do programa. Em ambos casos, o nome deve estar totalmente em letras minúsculas.

Sempre use o prefixo `ruby-`, mesmo se `$gemname` já iniciar com a palavra `ruby`. É necessário evitar futuros confrontos de nomes no caso de aparecer uma gem com nome mais curto. Também torna os nomes mais fáceis de serem interpretados por ferramentas (pense nos geradores/versão ou nos verificadores de dependência do PKGBUILD, etc ...).

### Pacotes versionados

Se você precisar adicionar um pacote versionado, então use `ruby-$gemname-$versão`, p. ex., `ruby-builder-3.2.1`. Então, a dependência rubygem `builder=3.2.1` se tornará o pacote Arch `ruby-builder-3.2.1`.

No caso, se você precisar resolver uma dependência "aproximadamente maior" `~>`, o pacote deverá usar a versão sem a última parte, por exemplo, dependência rubygem `builder ~> 3.2.1` se transformará em `ruby-builder-3.2`. Uma exceção para esta regra é quando a dependência "aproximadamente maior" corresponde à versão mais recente da gem - neste caso, evite introduzir um novo pacote versionado e use apenas `ruby-$gemname` (a versão HEAD).

Outro problema com pacotes com versão é que pode entrar em conflito com outras versões, p. ex. porque os pacotes instalam os mesmos arquivos em `/usr/bin`. Uma solução para este problema é que pacotes com versões não devem instalar tais arquivos - somente o pacote de versão HEAD pode fazer isso.

## Exemplos

Por exemplos, por favor, veja [ruby-json_pure](https://aur.archlinux.org/packages/ruby-json_pure/) ou [ruby-hpricot](https://www.archlinux.org/packages/?name=ruby-hpricot).

## Notas

Adicione `--verbose` aos argumentos do **gem** para receber informações adicionais no caso de haver problemas.

**Nota:** O uso do argumento `--no-user-install` do **gem** é obrigatório já que as versões mais recentes do Ruby (Veja [FS#28681](https://bugs.archlinux.org/task/28681) para detalhes).

### Quarry

Como uma alternativa ao gerenciamento manual de gemfiles, você também pode querer considerar quarry, um repositório não oficial de pacotes de pacotes binários pré-compilados. Veja [Quarry](/index.php/Quarry "Quarry") para detalhes.

## Pegadinhas

### Pacote contém referência a $pkgdir

Às vezes, quando você compila o pacote, você pode ver o seguinte aviso `AVISO: O pacote contém referência para $pkgdir`. Alguns arquivos empacotados contêm o caminho absoluto do diretório no qual você compilou o pacote. Para encontrar esses arquivos, execute `cd pkg && grep -R "$(pwd)"`. O mais provável é que o motivo seja o caminho codificado em `.../ext/Makefile`.

**Nota:** A pasta `ext` contém código de extensão nativo geralmente escrito em C. Durante a instalação do pacote, rubygems gera um Makefile usando a biblioteca `mkmf`. Então, `make` é chamado, ele compila uma biblioteca compartilhada e copia uma para o diretório gem `lib`.

Depois que `gem install` acabar, o `Makefile` não será mais necessário. Na verdade, nenhum dos arquivos em `ext` é necessário e podem ser completamente removidos adicionando `rm -rf "$pkgdir/$_gemdir/gems/$_gemname-$pkgver/ext"` ao `package()` function.