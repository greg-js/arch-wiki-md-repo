Esta página contém um resumo de algumas das similaridades e diferenças entre Arch Linux e outras distribuições. Esta questão surge repetidamente e seria interessante ter uma resposta padrão. Por favor note: a melhor forma de comparar Arch com outras distribuições é instalá-la e experimentar por si mesmo. Arch tem uma maravilhosa comunidade que está sempre disposta a ajudar novos usuários. Os sumários abaixo têm a intenção apenas de lhe dar informação o suficiente para decidir se Arch é realmente para você.

## Contents

*   [1 Arch x Gentoo](#Arch_x_Gentoo)
*   [2 Arch x Slackware](#Arch_x_Slackware)
*   [3 Arch x Debian](#Arch_x_Debian)
*   [4 Arch x Ubuntu](#Arch_x_Ubuntu)
*   [5 Arch x Crux](#Arch_x_Crux)
*   [6 Arch x Distribuições Gráficas](#Arch_x_Distribui.C3.A7.C3.B5es_Gr.C3.A1ficas)
*   [7 Arch x Distribuições baseadas em RPM](#Arch_x_Distribui.C3.A7.C3.B5es_baseadas_em_RPM)
*   [8 Arch x Fedora](#Arch_x_Fedora)
*   [9 Arch x Mandrake](#Arch_x_Mandrake)
*   [10 Arch x SuSE](#Arch_x_SuSE)

## Arch x Gentoo

Tanto Arch quanto Gentoo são sistemas "rolling release", disponibilizando seus pacotes para a comunidade após um curto período de tempo depois de lançados. Os pacotes do Gentoo, bem como o sistema base, são construídos diretamente a partir do código-fonte, de acordo com 'flags USE' especificadas pelo usuário. Arch disponibiliza um sistema para construir pacotes a partir do código, apesar de o sistema base ter sido projetado para ser instalado como um binário i686/x86_64 pré-construído. Geralmente, isso faz com que Arch seja construído e atualizado mais rapidamente, e permite que Gentoo seja mais sistemicamente personalizável. Arch suporta apenas as arquiteturas i686 e x86_64, enquanto Gentoo suporta oficialmente as arquiteturas x86, PPC, SPARC, Alpha, AMD64, ARM, MIPS, HP/PA, S/390, sh e Itanium. Devido ao fato de tanto o Arch quanto Gentoo incluírem apenas o sistema básico, ambos são considerados altamente personalizáveis. Usuários de Gentoo geralmente se sentirão confortáveis com muitos aspectos do Arch.

## Arch x Slackware

Tanto Slackware quanto Arch são distribuições 'simples'. Ambas usam init scripts de estilo BSD. Arch fornece um sistema de gerenciamento de pacotes muito mais robusto com o pacman que, ao contrário das ferramentas padrão do Slackware, permite atualizações automáticas do sistema de forma simples. Slackware é vista como mais conservadora no seu ciclo de versões, preferindo pacotes comprovadamente estáveis. Arch é muito mais arrojado a este respeito. Arch é apenas para i686 enquanto Slackware pode rodar em sistemas i486\. Arch é um sistema muito bom para usuários Slackware que querem gerenciamento de pacotes mais robusto ou pacotes mais atualizados.

## Arch x Debian

Arch é mais simples que o Debian. Arch tem menos pacotes. Arch provê melhor suporte para construir seus próprios pacotes do que o Debian. Arch é mais tolerante quando se trata de pacotes 'não livres' como definido pelo GNU. Arch é otimizado para i686 e portanto mais rápido do que o Debian. Pacotes Arch são mais atualizados que os do Debian (o repositório current [atual] do Arch frequentemente é mais atualizado que o unstable [instável] do Debian!)

## Arch x Ubuntu

Arch tem um alicerce mais simples que o Ubuntu. Se você gosta de compilar seus próprios kernels, experimente projetos disponíveis apenas em CVS, ou monte um programa a partir dos fontes de vez em quando, Arch é melhor apropriado para isso. Se você quer ir rodando logo e não mexer com as entranhas do sistema, Ubuntu é mais adequado. Em geral desenvolvedores e 'fuçadores' gostarão mais de Arch que do Ubuntu.

## Arch x Crux

O Arch Linux é descendente do Crux. Judd uma vez sumarizou as diferenças:

	"Eu usei Crux antes de iniciar o Arch. Arch começou como o Crux, basicamente. Então eu escrevi pacman e makepkg para substituir meus pseudo scripts de empacotamento em bash (eu construí Arch como um sistema LFS inicialmente). Agora as duas distribuições são completamente separadas, mas tecnicamente, são quase a mesma. Nós temos suporte a dependências (oficialmente) por exemplo, embora Crux tenha uma comunidade que provenha outras funcionalidades. O prt-get do CLC possui lógica de dependência rudimentar. Crux chega a ignorar muitos dos problemas que nós temos, uma vez que é um conjunto de pacotes muito minimalístico, basicamente o que Per usa e nada mais."

## Arch x Distribuições Gráficas

As distribuições gráficas tem muitas semelhanças entre si, e Arch é muito diferente de qualquer uma delas. Arch é baseada em modo texto e é orientada a linha de comando. Arch é uma distribuição melhor se você quer realmente aprender Linux. Distribuições baseadas em modo gráfico tendem a ter instaladores gráficos (como o Anaconda do Fedora) e ferramentas gráficas de configuração do sistema (como o Yast do SuSe). Diferenças específicas entre distribuições são descritas abaixo.

## Arch x Distribuições baseadas em RPM

Pacotes RPM estão disponíveis a partir de muitos locais, entretanto pacotes de terceiros frequentemente tem problemas com dependências, como por exemplo requerer uma versão mais antiga de uma biblioteca. Também existe confusão entre pacotes RPM para Red Hat x pacotes RPM para Mandrake. (Estes são problemas que tive como usuário iniciante com Mandrake 8.2, e talvez não reflita a situação atual.) pacman é muito mais poderoso e confiável que RPM.

## Arch x Fedora

Fedora é derivada da distribuição RedHat e tem sido constantemente uma das distribuições mais populares até hoje. Portanto há uma maciça comunidade e montes de pacotes pré-construidos e suporte disponível. Como todas as distribuições baseadas em RPM, gerenciamento de pacotes é um problema. Fedora fornece Yum como uma interface para gerenciar a aquisição de RPMs e resolução de dependências. O sistema carece de uma sólida integração com o Yum e partes consideráveis do Fedora ainda usam o sistema up2date/anaconda/rpm que está desatualizado e não funciona corretamente. Fedora inovou e recentemente mereceu fama pela integração do SELinux e pacotes compilados do GCJ por remover a necessidade do JRE da Sun. Fedora é famoso por não tentar suportar o formato de mídia mp3 devido a assuntos ligados a patentes.

## Arch x Mandrake

Mandrake, embora famoso por seu instalador é uma distribuição muito tutelar [leva o usuário pela mão] que pode se tornar aborrecida depois de algum tempo. Outro problema é que é uma distribuição baseada em RPM, como discutido acima. Arch permite muito mais liberdade e menos tutela. Você realmente aprende.

## Arch x SuSE

Suse é centrada em sua bem considerada ferramenta de configuração Yast. Este é um ponto central único para as necessidades de configuração da maioria dos usuários. Arch não oferece tal facilidade uma vez que isso vai contra [O Jeito Arch](/index.php/The_Arch_Way_(Portugu%C3%AAs) "The Arch Way (Português)"). Suse, portanto, é vista como mais apropriada para os usuários menos experientes ou para aqueles que querem uma vida mais simples com as coisas funcionando logo de cara. Suse não oferece suporte a mp3 logo após a instalação. Entretanto ele pode ser facilmente adicionado através do Yast num momento posterior.