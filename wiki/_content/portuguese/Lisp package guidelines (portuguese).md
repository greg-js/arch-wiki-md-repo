**Status de tradução:** Esse artigo é uma tradução de [Lisp package guidelines](/index.php/Lisp_package_guidelines "Lisp package guidelines"). Data da última tradução: 2018-11-02\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Lisp_package_guidelines&diff=0&oldid=552575) na versão em inglês.

**[Diretrizes de criação de pacotes](/index.php/Padr%C3%B5es_de_empacotamento_do_Arch "Padrões de empacotamento do Arch")**

* * *

[CLR](/index.php/Diretrizes_de_pacotes_CLR "Diretrizes de pacotes CLR") – [Cross](/index.php/Diretrizes_de_pacotes_de_ferramentas_de_compila%C3%A7%C3%A3o_cruzada "Diretrizes de pacotes de ferramentas de compilação cruzada") – [Eclipse](/index.php/Diretrizes_de_pacotes_de_plugin_do_Eclipse "Diretrizes de pacotes de plugin do Eclipse") – [Free Pascal](/index.php/Diretrizes_de_pacotes_Free_Pascal "Diretrizes de pacotes Free Pascal") – [GNOME](/index.php/Diretrizes_de_pacotes_GNOME "Diretrizes de pacotes GNOME") – [Go](/index.php/Diretrizes_de_pacotes_Go "Diretrizes de pacotes Go") – [Haskell](/index.php/Diretrizes_de_pacotes_Haskell "Diretrizes de pacotes Haskell") – [Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java") – [KDE](/index.php/Diretrizes_de_pacotes_KDE "Diretrizes de pacotes KDE") – [Kernel](/index.php/Diretrizes_de_pacotes_de_m%C3%B3dulos_de_kernel "Diretrizes de pacotes de módulos de kernel") – [Lisp](/index.php/Diretrizes_de_pacotes_Lisp "Diretrizes de pacotes Lisp") – [MinGW](/index.php/Diretrizes_de_pacotes_MinGW "Diretrizes de pacotes MinGW") – [Node.js](/index.php/Diretrizes_de_pacotes_Node.js "Diretrizes de pacotes Node.js") – [Nonfree](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") –[OCaml](/index.php/Diretrizes_de_pacotes_OCaml "Diretrizes de pacotes OCaml") – [Perl](/index.php/Diretrizes_de_pacotes_Perl "Diretrizes de pacotes Perl") – [PHP](/index.php/Diretrizes_de_pacotes_PHP "Diretrizes de pacotes PHP") – [Python](/index.php/Diretrizes_de_pacotes_Python "Diretrizes de pacotes Python") – [R](/index.php/Diretrizes_de_pacotes_R "Diretrizes de pacotes R") – [Ruby](/index.php/Diretrizes_de_pacotes_Ruby_Gem "Diretrizes de pacotes Ruby Gem") – [VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") – [Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web") – [Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine")

No momento, há relativamente poucos pacotes [Lisp](https://en.wikipedia.org/wiki/pt:Lisp "wikipedia:pt:Lisp") disponíveis nos repositórios do Arch. Isso significa que, em algum momento ou outro, mais provavelmente aparecerá. É útil, portanto, descobrir agora, enquanto há poucos pacotes, como eles devem ser empacotados.

## Contents

*   [1 Nomenclatura e estrutura de diretórios](#Nomenclatura_e_estrutura_de_diret.C3.B3rios)
*   [2 ASDF](#ASDF)
*   [3 Empacotamento específico do Lisp](#Empacotamento_espec.C3.ADfico_do_Lisp)
*   [4 Coisas que você, o leitor, pode fazer](#Coisas_que_voc.C3.AA.2C_o_leitor.2C_pode_fazer)

## Nomenclatura e estrutura de diretórios

Há pelo menos um pacote no repositório base ([libgpg-error](https://www.archlinux.org/packages/?name=libgpg-error)) que inclui arquivos lisp, que são colocados em `/usr/share/common-lisp/source/gpg-error`. De acordo com isso, outros pacotes lisp também devem colocar seus arquivos em `/usr/share/common-lisp/source/*pkgname*`.

O diretório do pacote deve ser o nome do pacote lisp, não o que é chamado nos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais") do Arch (ou no [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)")). Isso se aplica até mesmo a pacotes de arquivo único.

Por exemplo, um pacote Lisp chamado *"cl-ppcre"* deve ser chamado `cl-ppcre` no AUR e residir em `/usr/share/common-lisp/source/**cl-ppcre**`. Um pacote Lisp chamado *"alexandria"* deve ser chamado `cl-alexandria` no AUR e residir em `/usr/share/common-lisp/source/**alexandria**`.

## ASDF

Tente evitar o uso do ASDF-Install como um meio de instalar esses pacotes em todo o sistema.

O próprio ASDF pode ser necessário ou útil como meio de compilar e/ou carregar pacotes. Nesse caso, sugere-se que o diretório usado para o registro central (a localização de todos os links simbólicos para `*.asd`) seja `/usr/share/common-lisp/systems/`.

No entanto, tenho observado problemas em fazer a compilação com asdf como parte do processo de compilação de pacotes. No entanto, ele funciona durante uma instalação, através do uso de um arquivo `*pacote*.install`. Esse arquivo pode ser assim:

 `cl-ppcre.install` 
```
# arg 1:  the new package version
post_install() {
    echo "---> Compiling lisp files <---"

    clisp --silent -norc -x \
        "(load #p\"/usr/share/common-lisp/source/asdf/asdf\") \
        (pushnew #p\"/usr/share/common-lisp/systems/\" asdf:*central-registry* :test #'equal) \
        (asdf:operate 'asdf:compile-op 'cl-ppcre)"

    echo "---> Done compiling lisp files <---"

    cat << EOM

    To load this library, load asdf and then place the following lines
    in your ~/.clisprc.lisp file:

    (push #p"/usr/share/common-lisp/systems/" asdf:*central-registry*)
    (asdf:operate 'asdf:load-op 'cl-ppcre)
EOM
}

post_upgrade() {
    post_install $1
}

pre_remove() {
    rm /usr/share/common-lisp/source/cl-ppcre/{*.fas,*.lib}
}

op=$1
shift

$op $*

```

Obviamente, para este exemplo funcionar, é necessário que haja um link simbólico para *pacote*.asd no diretório do sistema asdf. Durante a compilação do pacote, um bloco como essa fará o truque...

```
pushd ${_lispdir}/systems
ln -s ../source/cl-ppcre/cl-ppcre.asd .
ln -s ../source/cl-ppcre/cl-ppcre-test.asd .
popd

```

...sendo que `$_lispdir` é `$pkgdir/usr/share/common-lisp`. Ao vincular a um caminho relativo, em vez de absoluto, é possível garantir que o link não interromperá a pós-instalação.

## Empacotamento específico do Lisp

Quando possível, não crie pacotes específicos para uma única implementação de lisp; tente ser tão multiplataforma quanto o próprio pacote permitir. Se, no entanto, o pacote for projetado especificamente para uma implementação única de lisp (ou seja, os desenvolvedores ainda não conseguiram adicionar suporte para outros, ou o propósito do pacote é especificamente fornecer um recurso integrado a outra implementação de lisp), é apropriado tornar o seu pacote Arch específico de lisp.

Para evitar tornar os pacotes específicos da implementação, idealmente todos os pacotes de implementação (SBCL, cmucl, clisp) seriam construídos com o campo [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") **common-lisp**. No entanto, esse não é o caso (e isso provavelmente causaria problemas para pessoas que preferem ter vários lisps na ponta dos dedos). Enquanto isso, você poderia (a) não fazer com que seu pacote dependa de *qualquer* lisp e incluir uma declaração no arquivo *package*.install informando às pessoas para ter certeza de que possuem um lisp instalado (não ideal) ou (b) se baseie no PKGBUILD do *sbcl* e inclua uma declaração condicional para descobrir qual lisp é necessário (que envolve muito hacking e, novamente, longe do ideal). Outras ideias são bem-vindas.

Observe também que se o ASDF for necessário para instalar/compilar/carregar o pacote, as coisas podem ficar estranhas no que diz respeito às dependências, já que o SBCL vem com asdf instalado, enquanto o clisp não, mas há um pacote AUR e a CMUCL pode ou não tê-lo.

As pessoas que atualmente mantêm pacotes específicos de lisp que não precisam ser específicos de lisp devem considerar fazer pelo menos um dos seguintes procedimentos:

*   Editar seus PKGBUILDs para serem multiplataformas, desde que outra pessoa não esteja mantendo o mesmo pacote para um lisp diferente.
*   Se oferecer para assumir a manutenção ou ajudar na manutenção do mesmo pacote para um lisp diferente e, em seguida, combiná-los em um único pacote.
*   Oferecer seu pacote ao mantenedor de uma versão diferente do mesmo pacote, para permitir que essa pessoa os combine em um único pacote.

## Coisas que você, o leitor, pode fazer

*   Manter pacotes lisp seguindo essas diretrizes
*   Atualizar e corrigir problemas com essas diretrizes
*   Se manter atualizado com o que foi alterado aqui
*   Fornecer ideias, feedback e sugestões (educados) tanto para esse documento quanto para o trabalho das pessoas.
*   Traduzir essa página e atualizações futuras a esta página.