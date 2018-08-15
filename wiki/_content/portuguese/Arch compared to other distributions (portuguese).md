Artigos relacionados

*   [Arch Linux](/index.php/Arch_Linux_(Portugu%C3%AAs) "Arch Linux (Português)")
*   [Distribuições baseadas no Arch](/index.php/Distribui%C3%A7%C3%B5es_baseadas_no_Arch "Distribuições baseadas no Arch")
*   [Pacman/Rosetta](/index.php/Pacman/Rosetta "Pacman/Rosetta")

Esta página tenta estabelecer uma comparação entre o Arch Linux e outras distribuições GNU/Linux populares e sistemas operacionais semelhantes ao UNIX. Os resumos que se seguem são descrições breves que podem ajudar uma pessoa a decidir se o Arch Linux atenderá às suas necessidades. Embora revisões e descrições possam ser úteis, a experiência de primeira mão é invariavelmente a melhor maneira de comparar distribuições.

Para uma comparação mais completa, veja [w:Comparison of operating systems](https://en.wikipedia.org/wiki/Comparison_of_operating_systems "w:Comparison of operating systems") e [w:Comparison of Linux distributions](https://en.wikipedia.org/wiki/Comparison_of_Linux_distributions "w:Comparison of Linux distributions").

Em todos os itens a seguir, apenas o Arch Linux é comparado com outras distribuições. Os *ports* comunitários que suportam arquiteturas diferentes de x86_64 podem ser encontradas listadas entre as [distribuições baseadas no Arch](/index.php/Distribui%C3%A7%C3%B5es_baseadas_no_Arch "Distribuições baseadas no Arch").

## Contents

*   [1 Baseados em código-fonte](#Baseados_em_c.C3.B3digo-fonte)
    *   [1.1 CRUX](#CRUX)
    *   [1.2 LFS](#LFS)
    *   [1.3 Gentoo/Funtoo Linux](#Gentoo.2FFuntoo_Linux)
*   [2 Geral](#Geral)
    *   [2.1 Debian](#Debian)
    *   [2.2 Fedora](#Fedora)
    *   [2.3 Slackware](#Slackware)
*   [3 Amigáveis para iniciantes](#Amig.C3.A1veis_para_iniciantes)
    *   [3.1 Ubuntu](#Ubuntu)
    *   [3.2 Linux Mint](#Linux_Mint)
    *   [3.3 openSUSE](#openSUSE)
    *   [3.4 Mandriva/Mageia](#Mandriva.2FMageia)
*   [4 Os *BSDs](#Os_.2ABSDs)
*   [5 Veja também](#Veja_tamb.C3.A9m)

## Baseados em código-fonte

As distribuições baseadas em fontes são altamente portáteis, proporcionando a vantagem de controlar e compilar todo o sistema operacional e aplicativos para uma arquitetura máquina e esquema de uso em particular, com a desvantagem da natureza demorada da compilação de origem. A base do Arch e todos os pacotes são compilados apenas para a arquitetura x86_64.

### CRUX

*   [CRUX](https://crux.nu/) é uma distribuição leve que se concentra no princípio [KISS](/index.php/Terminologia_do_Arch#KISS "Terminologia do Arch"). CRUX inspirou Judd Vinet a criar o Arch.
*   CRUX usa scripts init no estilo BSD, enquanto o Arch usa systemd.
*   Enquanto o Arch usa o sistema de lançamento contínuo *(rolling release)*, o CRUX tem lançamentos mais ou menos anual.
*   Ambos são enviados com sistemas do tipo *ports* e, como * BSD, ambos fornecem um ambiente base para construir.
*   O Arch possui o pacman, que lida com o gerenciamento do pacote de sistema binário e funciona perfeitamente com o [sistema de compilação do Arch](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)"). O CRUX usa um sistema de contribuição comunitária chamado *prt-get* , que, em combinação com seu próprio sistema de *ports*, lida com a resolução de dependência, mas constrói todos os pacotes do fonte (embora a instalação da base do CRUX seja binária).
*   Arch e CRUX oficialmente apenas apoiam a arquitetura x86_64.
*   O Arch possui uma grande variedade de repositórios de pacotes binários, bem como o [Arch User Repository](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)"). O CRUX fornece um sistema de *ports* oficialmente mais lento e suportado oficialmente, além de um repositório comunitário comparativamente modesto.

### LFS

*   O [LFS](http://www.linuxfromscratch.org/lfs/) (ou Linux From Scratch) existe simplesmente como documentação. O livro instrui o usuário a obter o código-fonte para um pacote de base mínimo definido para um sistema GNU/Linux funcional e como compilar, corrigir e configurá-lo manualmente a partir do zero. O LFS é tão mínimo quanto obtém, e oferece um processo excelente e educacional de construção e personalização de um sistema base.
*   O LFS não fornece repositórios on-line; os fontes são obtidas manualmente, compilados e instalados com *make*. (Existem vários métodos manuais de gerenciamento de pacotes e são mencionados em LFS Hints).
*   O Arch fornece esses mesmos pacotes, além do [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)"), algumas ferramentas extras e o poderoso gerenciador de pacotes [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") como seu sistema base, já compilado para x86_64\. Junto com o sistema de base mínimo do Arch, a comunidade Arch e os desenvolvedores fornecem e mantêm muitos milhares de pacotes binários instaláveis via pacman, bem como os scripts de compilação [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") para uso com o [sistema de compilação do Arch](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)"). O Arch também inclui a ferramenta [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") para construir ou personalizar de forma conveniente pacotes *.pkg.tar.xz*, facilmente instaláveis pelo pacman.
*   Judd Vinet compilou o Arch do zero e então escreveu o pacman em C. Historicamente, o Arch às vezes foi descrito com humor simplesmente como "Linux, com um bom gerenciador de pacotes."

### Gentoo/Funtoo Linux

*   Tanto o Arch Linux quanto o [Gentoo Linux](https://gentoo.org/) são sistemas de lançamento contínuo (*rolling release*), tornando os pacotes disponíveis para a distribuição um curto período de tempo depois que eles são lançados pelo *upstream*.
*   Os pacotes e o sistema base do Gentoo são construídos diretamente do código-fonte de acordo com os "USE flags" especificados pelo usuário. O Arch fornece um sistema tipo *ports* para criar pacotes a partir do fonte, embora o sistema base do Arch seja projetado para ser instalado como binário em x86_64 pré-compilado. Isso geralmente torna o Arch mais rápido para compilar e atualizar, e permite que o Gentoo seja mais sistematicamente personalizável.
*   O Arch apenas oferece suporte a x86_64 enquanto o Gentoo oferece suporte oficialmente às arquiteturas x86 (i486/i686), x86_64, PPC/PPC64, SPARC, Alpha, ARM, MIPS, HPPA, S/390 e Itanium.
*   O pacote oficial do Gentoo e as ferramentas de gerenciamento de sistema tendem a ser bastante mais complexas e "poderosas" do que as fornecidas pelo Arch, e certas características que estão no coração do Gentoo *([USE flags](https://wiki.gentoo.org/wiki/Handbook:X86/Working/USE), [SLOTs](https://wiki.gentoo.org/wiki/Handbook:X86/Working/Portage#Terminology), etc.)* não possui nenhum equivalente direto do Arch Linux. Parte disso é devido ao fato de que o Arch é principalmente uma distro binária, mas as diferenças na [filosofia do design](/index.php/Arch_Linux_(Portugu%C3%AAs)#Princ.C3.ADpios "Arch Linux (Português)") também desempenham um papel importante, com o Arch assumindo uma posição mais baseada em princípios em favor da simplicidade arquitetural e evitando excesso de engenharia.
*   Como ambas as instalações do Gentoo e Arch incluem apenas um sistema base, ambos são considerados altamente personalizáveis. Se confortáveis com [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)"), os usuários do Gentoo também se sentirão geralmente à vontade com a maioria dos outros aspectos do Arch.

## Geral

Essas distribuições oferecem uma ampla gama de vantagens e pontos fortes e podem ser feitas para atender a maioria dos usos do sistema operacional.

### Debian

*   [Debian](https://www.debian.org/) é a maior upstream de distribuição Linux com uma comunidade maior e possui ramos estáveis, testes e instáveis, oferecendo mais de 43.000 [pacotes](https://packages.debian.org/unstable/). O número disponível de pacotes binários do Arch é mais modesto. No entanto, ao incluir o AUR, as quantidades são comparáveis.
*   Debian tem uma postura mais veemente sobre o software livre, mas ainda inclui software não livre em seus repositórios não livres. O Arch é mais leniente e, portanto, inclusivo, em relação a "pacotes não livres", conforme definido pelo GNU.
*   Debian se concentra em testes rigorosos do ramo estável, que está "congelado" e há suporte por até [cinco anos](https://wiki.debian.org/LTS "debian:LTS"). Os pacotes Arch são mais atuais do que o Stable do Debian, sendo mais comparável a ramos Testing e Unstable do Debian e não tem um agendamento de lançamento fixo.
*   Debian está disponível para muitas arquiteturas, incluindo alpha, arm, hppa, i386, x86_64, ia64, m68k, mips, mipsel, powerpc, s390 e sparc, enquanto o Arch é x86_64 apenas.
*   O Arch fornece suporte mais conveniente para a construção de pacotes personalizados e instaláveis de fontes externas, com um sistema de compilação de pacotes tipos *ports*. O Debian não oferece um sistema de *ports*, confiando em vez dos seus grandes repositórios binários.
*   O sistema de instalação do Arch só oferece uma base mínima, exposta de forma transparente durante a configuração do sistema, enquanto os métodos da Debian, como o uso de *tasks* do apt para instalar grupos pré-selecionados de pacotes, oferecem uma abordagem mais configurada automaticamente, bem como vários métodos alternativos de instalação.
*   O Arch geralmente agrupa bibliotecas de software junto com seus arquivos de cabeçalho, enquanto que os arquivos de cabeçalho Debian precisam ser baixados separadamente.
*   O Arch mantém o mínimo possível, evitando problemas que o *upstream* são incapazes de revisar, enquanto o Debian aplica *patches* em seus pacotes de forma mais liberal para um público mais amplo.

### Fedora

*   O [Fedora](https://getfedora.org/) é desenvolvido pela comunidade, ainda que corporativamente apoiado pela Red Hat; muitas vezes é apresentado como um sistema de lançamento de teste. Os pacotes e projetos do Fedora migram para a RHEL e alguns eventualmente são adotados por outras distribuições. O Arch não possui lançamentos fixos e não serve como um ramo de teste para outra distribuição.

*   Os pacotes do Fedora usam o formato RPM com o gerenciador de pacotes DNF. Arch usa [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") para gerenciar pacotes tar.xz.

*   O Fedora se recusa a incluir software não livre em repositórios oficiais devido à sua dedicação ao software livre, embora repositórios de terceiros estejam disponíveis para esses pacotes. Arch é mais indulgente em sua disposição para software não livre, deixando o discernimento para o usuário.

*   O Fedora oferece muitas opções de instalação, incluindo um instalador gráfico, bem como uma opção mínima. Os "spins" do Fedora também oferecem sortimentos alternativos de ambientes de desktop para escolher, cada um com uma modesta variedade de pacotes padrão. O Arch, por outro lado, fornece apenas alguns scripts destinados a facilitar o processo de uma instalação mínima do sistema base.

*   O Fedora possui um ciclo de lançamento programado, mas oferece suporte oficial a atualizações de versões discretas com a ferramenta FedUp. O Arch é um sistema de lançamento contínuo (*rolling release*).

*   O Arch possui um sistema de *ports*, enquanto o Fedora não.

*   Arch e Fedora são direcionados para usuários experientes e desenvolvedores. Ambos incentivam fortemente os seus usuários a contribuir para o desenvolvimento do projeto.

*   O Fedora ganhou muito reconhecimento comunitário pela integração do SELinux, pacotes compilados GCJ (para remover a necessidade do JRE da Oracle) e contribuição prolífica de *upstream*; Red Hat e, portanto, os desenvolvedores do Fedora, por extensão, contribuem com a maior percentagem do código do kernel do Linux em comparação com qualquer outro projeto.

*   O Arch Linux fornece o que é amplamente considerado como o wiki de distribuição mais abrangente e compreensivo. O wiki do Fedora é usado no sentido original da palavra "wiki", ou uma maneira de trocar informações rapidamente entre desenvolvedores, testadores e usuários. Não se destina a ser uma base de conhecimento de usuários finais como do Arch. O wiki do Fedora se assemelha a um rastreador de problemas ou a uma wiki corporativa.

### Slackware

*   O [Slackware](http://www.slackware.com/) usa scripts de inicialização do tipo BSD, enquanto o Arch usa [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)").

*   O Arch fornece um sistema de gerenciamento de pacotes no [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") que, ao contrário das ferramentas padrão do Slackware, oferece resolução de dependência automática e permite atualizações automatizadas do sistema. Os usuários do Slackware geralmente preferem seu método de resolução de dependência manual, citando o nível de controle do sistema que os concede, bem como o excelente fornecimento de bibliotecas pré-instaladas e dependências da Slackware.

*   O Arch é um sistema de lançamento contínua. O Slackware é visto como mais conservador em seu ciclo de lançamento, preferindo pacotes comprovadamente estáveis. O Arch é mais "bleeding edge" a este respeito.

*   O Arch Linux fornece muitos milhares de pacotes binários dentro de seus repositórios oficiais, enquanto os repositórios oficiais do Slackware são mais modestos.

*   O Arch oferece o [Arch Build System](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)"), um sistema de *ports* reais e também [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)"), uma coleção muito grande de PKGBUILDs contribuídos pelos usuários. O Slackware oferece um sistema similar, embora mais fino, em [slackbuilds.org](http://www.slackbuilds.org), que é um repositório semioficial de Slackbuilds, que é análogo ao Arch PKGBUILDs. Os usuários do Slackware geralmente serão bastante confortáveis com a maioria dos aspectos do Arch.

## Amigáveis para iniciantes

Às vezes chamadas de "distros de novatos", as distribuições amigáveis para iniciantes compartilham muitas semelhanças, embora o Arch seja bastante diferente delas. O Arch pode ser uma escolha melhor se você quiser aprender sobre o GNU/Linux construindo a partir de uma base pequena, uma vez que uma instalação do Arch instala alguns pacotes em comparação. Diferenças específicas entre as distribuições são descritas abaixo.

### Ubuntu

*   O [Ubuntu](https://www.ubuntu.com/) é uma distribuição popular baseada no Debian e patrocinada comercialmente pela Canonical Ltd., enquanto o Arch é um sistema desenvolvido de forma independente criado a partir do zero.

*   Os dois projetos têm objetivos muito diferentes e são direcionados para uma base de usuários diferente. O Arch é projetado para usuários que desejam uma abordagem "faça você mesmo", enquanto o Ubuntu fornece um sistema pré-configurado. O Arch apresenta um design mais simples a partir da instalação base em diante, confiando no usuário para personalizá-lo para suas próprias necessidades específicas. Muitos usuários do Arch começaram no Ubuntu e, eventualmente, migraram para o Arch.

*   O desenvolvimento do Arch não é direcionado a uma interface de usuário específica, além do que a comunidade oferece suporte. Além disso, a natureza comercial da Canonical levou-os a algumas decisões controversas, como a inclusão de propagandas no menu *Dash* da Unity e a coleta de dados do usuário. Arch é um projeto independente, liderado pela comunidade sem agenda comercial.

*   Ubuntu move entre lançamentos discretos a cada 6 meses, enquanto o Arch é um sistema de lançamento contínuo.

*   O Arch oferece um sistema de compilação de pacotes de portas e o [Arch User Repository](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)"), onde os usuários podem compartilhar pacotes de origem para o gerenciador de pacotes [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)"). O Ubuntu usa um [apt](https://en.wikipedia.org/wiki/pt:Advanced_Packaging_Tool "wikipedia:pt:Advanced Packaging Tool") mais complexo e permite a redistribuição de pacotes binários através de [Personal Package Archives](https://launchpad.net/ubuntu/+ppas).

*   As duas comunidades também diferem em alguns aspectos. A comunidade do Arch é muito menor e é fortemente encorajada a contribuir para a distribuição. Em contraste, a comunidade Ubuntu é relativamente grande e, portanto, pode tolerar uma porcentagem muito maior de usuários que não contribuem ativamente para o desenvolvimento, empacotamento ou a manutenção do repositório.

### Linux Mint

*   [Linux Mint](https://www.linuxmint.com/) nasceu como uma derivação do [Ubuntu](#Ubuntu) e, posteriormente, adicionou o LMDE (Linux Mint Debian Edition), que é baseado no [#Debian](#Debian). Por outro lado, o Arch é uma distribuição independente que depende do seu próprio [sistema de compilação](/index.php/ABS_(Portugu%C3%AAs) "ABS (Português)") e [repositórios](/index.php/Reposit%C3%B3rios "Repositórios").
*   O Mint inclui várias ferramentas gráficas para facilitar a manutenção, chamadas *MintTools*. O Arch fornece apenas ferramentas de linha de comando simples, como o [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") e deixa o gerenciamento do sistema ser organizado pelo usuário.
*   O Mint é fornecido principalmente com [Cinnamon](/index.php/Cinnamon "Cinnamon") ou [MATE](/index.php/MATE "MATE") como sua interface gráfica e, alternativamente, [KDE](/index.php/KDE "KDE") ou [Xfce4](/index.php/Xfce4 "Xfce4").
*   Novas versões do Mint são lançadas a cada seis meses, cerca de um mês após o Ubuntu. Cada lançamento é baseado no Ubuntu LTS mais recente e há suporte por cinco anos. O Linux Mint Debian Edition (LMDE) é baseado em Debian Stable e só recebe atualizações em pacotes do Mint e atualizações de segurança. O Arch é, em vez disso, uma distribuição completamente de lançamento contínuo.

### openSUSE

O [openSUSE](https://www.opensuse.org/) é centrado em torno do formato do pacote RPM e da bem-considerada ferramenta de configuração orientada por interface gráfica YaST2\. O Arch não oferece tal facilidade. O openSUSE, portanto, pode ser mais apropriado para usuários que desejam um ambiente mais orientado a interface gráfica, configuração automática ou funcionalidade esperada fora da caixa enquanto ainda permite a profundidade de personalização.

### Mandriva/Mageia

O Mandriva Linux (anteriormente Mandrake Linux) foi criado em 1998 com o objetivo de tornar o GNU/Linux fácil de usar para todos; é baseado em RPM e usa o gerenciador de pacotes urpmi. Mageia é um *fork* do Mandriva criado por ex-funcionários do Mandriva que se opõe à posição comercial de sua distribuição principal, sendo um projeto sem fins lucrativos e orientado pela comunidade. O Arch assume uma abordagem mais simples do que Mandriva ou Mageia, sendo baseada em texto e confia mais na configuração manual e destina-se a usuários intermediários a avançados.

## Os *BSDs

*   Os *BSDs compartilham uma origem comum e descem diretamente do trabalho realizado na Universidade da Califórnia em Berkeley para produzir um sistema UNIX redistribuível livremente e sem custo. Eles não são distribuições GNU/Linux, mas sim sistemas operacionais semelhantes a UNIX, e derivam do código original do UNIX da AT&T.

*   O Arch e os *BSDs compartilham o conceito de um sistema base bem integrado e de *ports*. No entanto, ao contrário das distribuições GNU/Linux, como o Arch, o kernel e os programas de *userland* do BSD (como o shell e os utilitários principais, como *ls*, *cp*, *cat* e *ps*) são desenvolvidos juntos em um único repositório de fontes.

*   A licença BSD geralmente é mais protetora do *codificador*, em contraste com a GPL, que favorece a proteção do *código* em si. O Arch é lançado sob a GPL.

*   Para aprender mais sobre as variantes *BSD, veja [Wikipedia:Comparison of BSD operating systems](https://en.wikipedia.org/wiki/Comparison_of_BSD_operating_systems "wikipedia:Comparison of BSD operating systems").

## Veja também

*   [DistroWatch](https://distrowatch.com/) - Notícias e análises de distribuições Linux
*   [The Live CD List](https://www.livecdlist.com) - Lista de imagens de sistemas operacionais *live*