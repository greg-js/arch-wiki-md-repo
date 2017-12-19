Artigos relacionados

*   [Arch Linux](/index.php/Arch_Linux_(Portugu%C3%AAs) "Arch Linux (Português)")
*   [Distribuições baseadas no Arch](/index.php/Arch_based_distributions "Arch based distributions")
*   [Pacman/Rosetta](/index.php/Pacman/Rosetta "Pacman/Rosetta")

Esta página tenta estabelecer uma comparação entre o Arch Linux e outras distribuições GNU/Linux populares e sistemas operacionais semelhantes ao UNIX. Os resumos que se seguem são descrições breves que podem ajudar uma pessoa a decidir se o Arch Linux atenderá às suas necessidades. Embora revisões e descrições possam ser úteis, a experiência de primeira mão é invariavelmente a melhor maneira de comparar distribuições.

Para uma comparação mais completa, veja [w:Comparison of operating systems](https://en.wikipedia.org/wiki/Comparison_of_operating_systems "w:Comparison of operating systems") e [w:Comparison of Linux distributions](https://en.wikipedia.org/wiki/Comparison_of_Linux_distributions "w:Comparison of Linux distributions").

## Contents

*   [1 Baseados em código-fonte](#Baseados_em_c.C3.B3digo-fonte)
    *   [1.1 CRUX](#CRUX)
    *   [1.2 LFS](#LFS)
    *   [1.3 Gentoo/Funtoo Linux](#Gentoo.2FFuntoo_Linux)
*   [2 Geral](#Geral)
    *   [2.1 Debian](#Debian)
    *   [2.2 Fedora](#Fedora)
    *   [2.3 Slackware](#Slackware)
*   [3 Amigável para iniciantes](#Amig.C3.A1vel_para_iniciantes)
    *   [3.1 Ubuntu](#Ubuntu)
    *   [3.2 Linux Mint](#Linux_Mint)
    *   [3.3 openSUSE](#openSUSE)
    *   [3.4 Mandriva/Mageia](#Mandriva.2FMageia)
*   [4 Os *BSDs](#Os_.2ABSDs)
*   [5 Veja também](#Veja_tamb.C3.A9m)

## Baseados em código-fonte

As distribuições baseadas em fontes são altamente portáteis, proporcionando a vantagem de controlar e compilar todo o sistema operacional e aplicativos para uma arquitetura máquina e esquema de uso em particular, com a desvantagem da natureza demorada da compilação de origem. A base do Arch e todos os pacotes são compilados apenas para a arquitetura x86_64.

### CRUX

*   Antes de criar o Arch, Judd Vinet admirava e usava o CRUX; uma distribuição minimalista criada por Per Lidén. Originalmente inspirado por ideias em comum com CRUX e BSD, o Arch foi construído a partir do zero, e o [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") foi então codificado em C.
*   Ambos são enviados com sistemas do tipo *ports* e, como * BSD, ambos fornecem um ambiente base para construir.
*   O Arch possui o pacman, que lida com o gerenciamento do pacote de sistema binário e funciona perfeitamente com o [sistema de compilação do Arch](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)"). O CRUX usa um sistema de contribuição comunitária chamado *prt-get* , que, em combinação com seu próprio sistema de *ports*, lida com a resolução de dependência, mas constrói todos os pacotes do fonte (embora a instalação da base do CRUX seja binária).
*   Arch e CRUX oficialmente apenas apoiam a arquitetura x86_64.
*   O Arch usa um sistema de lançamento contínuo e possui uma grande variedade de repositórios de pacotes binários, bem como o [Arch User Repository](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)"). O CRUX fornece um sistema de *ports* oficialmente mais lento e suportado oficialmente, além de um repositório comunitário comparativamente modesto.

### LFS

*   O LFS (ou Linux From Scratch) existe simplesmente como documentação. O livro instrui o usuário a obter o código-fonte para um pacote de base mínimo definido para um sistema GNU/Linux funcional e como compilar, corrigir e configurá-lo manualmente a partir do zero. O LFS é tão mínimo quanto obtém, e oferece um processo excelente e educacional de construção e personalização de um sistema base.
*   O LFS não fornece repositórios on-line; os fontes são obtidas manualmente, compilados e instalados com *make*. (Existem vários métodos manuais de gerenciamento de pacotes e são mencionados em LFS Hints).
*   O Arch fornece esses mesmos pacotes, além do [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)"), algumas ferramentas extras e o poderoso gerenciador de pacotes [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") como seu sistema base, já compilado para x86_64\. Junto com o sistema de base mínimo do Arch, a comunidade Arch e os desenvolvedores fornecem e mantêm muitos milhares de pacotes binários instaláveis via pacman, bem como os scripts de compilação [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") para uso com o [sistema de compilação do Arch](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)"). O Arch também inclui a ferramenta [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") para construir ou personalizar de forma conveniente pacotes *.pkg.tar.xz*, facilmente instaláveis pelo pacman.
*   Judd Vinet compilou o Arch do zero e então escreveu o pacman em C. Historicamente, o Arch às vezes foi descrito com humor simplesmente como "Linux, com um bom gerenciador de pacotes."

### Gentoo/Funtoo Linux

*   Tanto o Arch Linux quanto o Gentoo Linux são sistemas de lançamento contínuo (*rolling release*), tornando os pacotes disponíveis para a distribuição um curto período de tempo depois que eles são lançados pelo *upstream*.
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
*   Debian está disponível para muitas arquiteturas, incluindo alpha, arm, hppa, i386, x86_64, ia64, m68k, mips, mipsel, powerpc, s390 e sparc, enquanto o Arch é oficialmente x86_64, com *ports* da comunidade para i686 ([Arch Linux 32](https://archlinux32.org/)) e ARM ([Arch Linux ARM](https://archlinuxarm.org/)) apenas.
*   O Arch fornece suporte mais conveniente para a construção de pacotes personalizados e instaláveis de fontes externas, com um sistema de compilação de pacotes tipos *ports*. O Debian não oferece um sistema de *ports*, confiando em vez dos seus grandes repositórios binários.
*   O sistema de instalação do Arch só oferece uma base mínima, exposta de forma transparente durante a configuração do sistema, enquanto os métodos da Debian, como o uso de *tasks* do apt para instalar grupos pré-selecionados de pacotes, oferecem uma abordagem mais configurada automaticamente, bem como vários métodos alternativos de instalação.
*   O Arch geralmente agrupa bibliotecas de software junto com seus arquivos de cabeçalho, enquanto que os arquivos de cabeçalho Debian precisam ser baixados separadamente.
*   O Arch mantém o mínimo possível, evitando problemas que o *upstream* são incapazes de revisar, enquanto o Debian aplica *patches* em seus pacotes de forma mais liberal para um público mais amplo.

### Fedora

*   O Fedora é desenvolvido pela comunidade, ainda que corporativamente apoiado pela Red Hat; muitas vezes é apresentado como um sistema de lançamento de teste. Os pacotes e projetos do Fedora migram para a RHEL e alguns eventualmente são adotados por outras distribuições. O Arch não possui lançamentos fixos e não serve como um ramo de teste para outra distribuição.

*   Os pacotes do Fedora usam o formato RPM com o gerenciador de pacotes DNF. Arch usa [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") para gerenciar pacotes tar.xz.

*   O Fedora se recusa a incluir software não livre em repositórios oficiais devido à sua dedicação ao software livre, embora repositórios de terceiros estejam disponíveis para esses pacotes. Arch é mais indulgente em sua disposição para software não livre, deixando o discernimento para o usuário.

*   O Fedora oferece muitas opções de instalação, incluindo um instalador gráfico, bem como uma opção mínima. Os "spins" do Fedora também oferecem sortimentos alternativos de ambientes de desktop para escolher, cada um com uma variedade variada de pacotes padrão. O Arch, por outro lado, fornece apenas alguns scripts destinados a facilitar o processo de uma instalação mínima do sistema base.

*   O Fedora possui um ciclo de lançamento programado, mas oferece suporte oficial a atualizações de versões discretas com a ferramenta FedUp. O Arch é um sistema de lançamento contínuo (*rolling release*).

*   O Arch possui um sistema de *ports*, enquanto o Fedora não.

*   Arch e Fedora são direcionados para usuários experientes e desenvolvedores. Ambos incentivam fortemente os seus usuários a contribuir para o desenvolvimento do projeto.

*   O Fedora ganhou muito reconhecimento comunitário pela integração do SELinux, pacotes compilados GCJ (para remover a necessidade do JRE da Oracle) e contribuição prolífica de *upstream*; Red Hat e, portanto, os desenvolvedores do Fedora, por extensão, contribuem com a maior percentagem do código do kernel do Linux em comparação com qualquer outro projeto.

*   O Arch Linux fornece o que é amplamente considerado como o wiki de distribuição mais abrangente e compreensivo. O wiki do Fedora é usado no sentido original da palavra "wiki", ou uma maneira de trocar informações rapidamente entre desenvolvedores, testadores e usuários. Não se destina a ser uma base de conhecimento de usuários finais como do Arch. O wiki do Fedora se assemelha a um rastreador de problemas ou a uma wiki corporativa.

### Slackware

*   O Slackware usa scripts de inicialização do tipo BSD, enquanto o Arch usa [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)").

*   O Arch fornece um sistema de gerenciamento de pacotes no [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") que, ao contrário das ferramentas padrão do Slackware, oferece resolução de dependência automática e permite atualizações automatizadas do sistema. Os usuários do Slackware geralmente preferem seu método de resolução de dependência manual, citando o nível de controle do sistema que os concede, bem como o excelente fornecimento de bibliotecas pré-instaladas e dependências da Slackware.

*   O Arch é um sistema de lançamento contínua. O Slackware é visto como mais conservador em seu ciclo de lançamento, preferindo pacotes comprovadamente estáveis. O Arch é mais "bleeding edge" a este respeito.

*   O Arch Linux fornece muitos milhares de pacotes binários dentro de seus repositórios oficiais, enquanto os repositórios oficiais do Slackware são mais modestos.

*   O Arch oferece o [Arch Build System](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)"), um sistema de *ports* reais e também [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)"), uma coleção muito grande de PKGBUILDs contribuídos pelos usuários. O Slackware oferece um sistema similar, embora mais fino, em [slackbuilds.org](http://www.slackbuilds.org), que é um repositório semioficial de Slackbuilds, que é análogo ao Arch PKGBUILDs. Os usuários do Slackware geralmente serão bastante confortáveis com a maioria dos aspectos do Arch.

## Amigável para iniciantes

Sometimes called "newbie distros", the beginner-friendly distributions share a lot of similarities, though Arch is quite different from them. Arch may be a better choice if you want to learn about GNU/Linux by building up from a small base, as an installation of Arch installs few packages in comparison. Specific differences between distributions are described below.

### Ubuntu

*   Ubuntu is a popular Debian-based distribution commercially sponsored by Canonical Ltd., while Arch is an independently developed system built from scratch.

*   The two projects have very different goals and are targeted at a different user base. Arch is designed for users who desire a do-it-yourself approach, whereas Ubuntu provides a preconfigured system. Arch presents a simpler design from the base installation onward, relying on the user to customize it to their own specific needs. Many Arch users have started on Ubuntu and eventually migrated to Arch.

*   Arch development is not biased towards any one particular user interface beyond what its community provide support for. Furthermore, Canonical's commercial nature has led them to some controversial decisions, such as the inclusion of advertisements in Unity's *Dash* menu and user data collection. Arch is an independent, community-driven project with no commercial agenda.

*   Ubuntu moves between discrete releases every 6 months, whereas Arch is a rolling-release system.

*   Arch offers a ports-like package build system and the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"), where users can share source packages for the [pacman](/index.php/Pacman "Pacman") package manager. Ubuntu uses the more complex [apt](https://en.wikipedia.org/wiki/Advanced_Packaging_Tool "wikipedia:Advanced Packaging Tool"), and allows redistribution of binary packages via [Personal Package Archives](https://launchpad.net/ubuntu/+ppas).

*   The two communities differ in some ways as well. The Arch community is much smaller and is strongly encouraged to contribute to the distribution. In contrast, the Ubuntu community is relatively large and can therefore tolerate a much larger percentage of users who do not actively contribute to development, packaging, or repository maintenance.

### Linux Mint

*   [Linux Mint](http://www.linuxmint.com/) was born as an [Ubuntu](#Ubuntu) derivative, and later added the LMDE (Linux Mint Debian Edition) that is instead based on [#Debian](#Debian). On the other hand, Arch is an independent distribution that relies on its own [build system](/index.php/ABS "ABS") and [repositories](/index.php/Repositories "Repositories").
*   Mint includes several graphical tools for easier maintenance, called *MintTools*. Arch only provides simple command-line tools like [pacman](/index.php/Pacman "Pacman") and leaves system management to be organized by the user.
*   Mint mainly ships with [Cinnamon](/index.php/Cinnamon "Cinnamon") or [MATE](/index.php/MATE "MATE") as its GUI, and alternatively [KDE](/index.php/KDE "KDE") or [Xfce4](/index.php/Xfce4 "Xfce4").
*   New versions of Mint are released every six months, about a month after Ubuntu. Each release is based on the most recent Ubuntu LTS and is supported for five years. Linux Mint Debian Edition (LMDE) is based on Debian Stable and only receives updates in Mint packages and security updates. Arch is instead a full rolling-release distribution.

### openSUSE

openSUSE is centered around the RPM package format and its well-regarded YaST2 GUI-driven configuration tool. Arch does not offer such a facility. openSUSE, may therefore be more appropriate for users who want a more GUI-driven environment, automatic configuration, or expected functionality out of the box while still allowing depth of customization.

### Mandriva/Mageia

Mandriva Linux (formerly Mandrake Linux) was created in 1998 with the goal of making GNU/Linux easy to use for everyone; it is RPM-based and uses the urpmi package manager. Mageia is a Mandriva fork created by former Mandriva employees which opposes its parent distribution's commercial position, being a non-profit and community-driven project. Arch takes a simpler approach than Mandriva or Mageia, being text-based and relying on more manual configuration, and is aimed at intermediate to advanced users.

## Os *BSDs

*   The *BSDs share a common origin and descend directly from the work done at UC Berkeley to produce a freely redistributable, free of cost, UNIX system. They are not GNU/Linux distributions, but rather, UNIX-like operating systems, and derived from the original AT&T UNIX code.

*   Arch and the *BSDs share the concept of a tightly-integrated base and ports system. However, unlike GNU/Linux distributions such as Arch, the *BSD kernel and userland programs (such as the shell and core utilities like *ls*, *cp*, *cat*, and *ps*) are developed together in a single source repository.

*   The BSD license is generally more protective of the *coder*, in contrast to the GPL, which favors protection of the *code* itself. Arch is released under the GPL.

*   To learn more about the *BSD variants, see [Wikipedia:Comparison of BSD operating systems](https://en.wikipedia.org/wiki/Comparison_of_BSD_operating_systems "wikipedia:Comparison of BSD operating systems").

## Veja também

*   [DistroWatch](http://distrowatch.com/) - Linux distributions news and reviews
*   [The Live CD List](http://www.livecdlist.com) - List of Live operating systems images