*Uma vez que existe uma enorme confusão acerca dos repositórios de Arch, esta wiki tenta explicar o seu significado:*

## Contents

*   [1 Revisão histórica](#Revis.C3.A3o_hist.C3.B3rica)
*   [2 Lista de repositórios](#Lista_de_reposit.C3.B3rios)
    *   [2.1 [core]](#.5Bcore.5D)
    *   [2.2 [extra]](#.5Bextra.5D)
    *   [2.3 [community]](#.5Bcommunity.5D)
    *   [2.4 [testing]](#.5Btesting.5D)
    *   [2.5 [unsupported]](#.5Bunsupported.5D)

# Revisão histórica

A maioria das divisões ocorreram por razões históricas. Originalmente, quando esta distribuição tinha ainda muito poucos utilizadores, havia um só repositório, que hoje corresponde ao [core] -- chamado [official]. Este repositório era composto, basicamente, pelas aplicações favoritas do Judd, apesar de não ser esse o caso hoje em dia. Está desenhado de maneira a ter apenas um de cada "tipo" de programa -- um desktop environment, um browser, etc.

Nessa altura havia utilizadores que não gostavam das preferências de Judd, como o [Arch Build System](/index.php/Arch_Build_System "Arch Build System") é tão simples de usar, começaram a criar os seus próprios pacotes. Estes pacotes foram para um repositório chamado [unofficial] e eram mantidos por programadores que não Judd. Os dois repositórios tornaram-se igualmente suportados pelos programadores e os nomes[oficial] e [unofficial] já não faziam sentido. Estes mudaram de nome para [current] e [extra], por volta do lançamento versão 0.5. Pouco depois do lançamento da 2007.08.1, [current] mudou para [core] para evitar confusões relativamente ao que realmente contém. Os repositórios são hoje bastante iguais aos olhos quer da equipa quer da comunidade, mas o [core] tem algumas diferenças, sendo que a principal é a de que os CDs de instalação têm os pacotes apenas do [core]. Este repositório dá um sistema GNU/Linux completo, mas pode não ser o que se quer.

Algures entre as versões 0.5 e 0.6, verificou-se que havia muitos pacotes que a equipa não queria manter. Um dos programadores (Xentac) configurou os "Repositórios de Utilizadores de Confiança (Trusted User Repositories)", que eram repositórios não-oficiais onde utilizadores de confiança (UC) podiam pôr os pacotes que criavam. Havia um repositório [staging] onde os pacotes podiam ser promovidos pela equipa para entrar nos repositórios oficiais, mas à parte disto a equipa e esses utilizadores eram mais ou menos de confiança.

Isto funcionou por algum tempo, excepto quando os utilizadores de confiança se cansaram dos seus repositórios e os restantes utilizadores queriam também partilhar os seus pacotes. Isto levou ao desenvolvimento do [AUR](https://aur.archlinux.org/). Os utilizadores de confiança foram conglomerados num grupo bastante restrito e hoje mantêm em conjunto o repositório [community]. Os UC ainda são um grupo separado da equipa principal e não há muita comunicação entre eles. No entanto, pacotes populares são por vezes promovidos do [community] para o [extra]. O [AUR](https://aur.archlinux.org/) também que permite os restantes utilizadores submetam os seus [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") para que outros os usem, se assim desejarem. Estes pacotes não são suportados, daí o repositório se chamar [unsupported], apesar de nenhuns binários serem distribuidos, pelo que o [unsupported] não é bem um repositório. Os UC podem adoptar pacotes do [unsupported] para o [community] à sua discrição, quer seja por o pacote ser popular ou por terem interesse em mantê-lo.

# Lista de repositórios

## [core]

O repositório [core] pode ser encontrado no *core/os/i686* ou *core/os/x86_64* no teu mirror favorito. Contém os pacotes principais de Arch e algum software adicional e irá fornecer um sistema básico totalmente funcional.

*O CD de Instalação não é mais do que um script de instalação e uma cópia do repositório [core]*

## [extra]

O repositório [extra] pode ser encontrado em *extra/os/i686* ou *extra/os/x86_64* no teu mirror favorito. Contém todos os pacotes oficiais de Arch que não foram para o [core]. Por exemplo: X.org, gerenciadores de janela, servidores web, reprodutores de media, línguas como Python, Ruby e Perl, e bastante mais.

## [community]

O repositório [community] pode ser encontrado em *community/os/i686* ou *community/os/x86_64* no teu mirror favorito. Este é mantido pelos *Utilizadores de Confiança (UC)* e faz parte do *Arch User Repository (AUR)*. Contém os pacotes do *AUR* com votos suficientes ou que tenham sido adoptados por um *UC*.

## [testing]

O repositório [testing] pode ser encontrado em *testing/os/i686* ou *testing/os/x86_64* no teu mirror favorito. [testing] é especial. Este contém pacotes que são candidatos ao [core], [extra] ou ao [unstable]. Pacotes novos vão para o [testing] se:

*   podem danificar alguma coisa após o update e precisam de ser testados primeiro.
*   exigem outros pacotes para ser reconstruidos. Neste caso, todos os pacotes que precisam de ser reconstruidos são colocados no [testing] primeiro e quando todos estiverem concluidos, são movidos para o repositório respectivo.

[testing] é o único repositório que pode ter colisões nos nomes com outros repositórios oficiais. Se activo, tem de ser o primeiro listado no ficheiro `/etc/pacman.conf`.

Cuidado ao activar o repositório [testing]. O teu sistema pode ficar danificado após updates com pacotes provenientes do [testing]. O seu uso deve estar limitado a uilizadores que sabem o que estão a fazer.

## [unsupported]

O repositório [unsupported] não é bem um repositório. Ao contrário dos outros repositórios, este não contém pacotes binários. É usado para referir a colecção [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") no AUR que foram submetidos por utilizadores comuns, pelo que o [unsupported] não é verdeiramente oficial. Não se pode descarregar ou instalar pacotes do [unsupported] com o [pacman](/index.php/Pacman "Pacman"). Tem de se descarreguegá-los manualmente e compilar os binários, ou usar um do popular [AUR helpers](/index.php/AUR_helpers "AUR helpers") para fazer isso automaticamente.