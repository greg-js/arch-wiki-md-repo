**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

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