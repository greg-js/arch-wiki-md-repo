O Arch Linux é uma distribuição GNU/Linux i686/x86_64 de uso geral desenvolvida independentemente e versátil o suficiente para cumprir qualquer papel. O desenvolvimento é focado na simplicidade, minimalismo e elegância de código. O Arch é instalado como um sistema de base mínimo a partir do qual o usuário configura seu ambiente ideal, instalando apenas o que for requerido ou desejado para seus propósitos pessoais. Utilitários GUI (Graphical User Interface) de configuração não são providos oficialmente, e a maioria da configuração do sistema é realizada no terminal, editando simples arquivos de texto. Baseado no modelo de _rolling-release_, o Arch se esforça para se manter _bleeding edge_, e tipicamente oferece as últimas versões estáveis da maioria dos softwares.

## Contents

*   [1 História](#Hist.C3.B3ria)
*   [2 Simplicidade](#Simplicidade)
*   [3 Modernidade](#Modernidade)
*   [4 Empacotamento de Software](#Empacotamento_de_Software)
*   [5 Integridade do Código-Fonte](#Integridade_do_C.C3.B3digo-Fonte)
*   [6 Comunidade](#Comunidade)
*   [7 Resumo](#Resumo)

## História

O Arch Linux foi fundado pelo programador canadense Judd Vinet. Seu primeiro lançamento formal, o Arch Linux 0.1, foi em 11 de março de 2002\. Embora o Arch seja completamente independente, ele se inspira na simplicidade de outras distribuições, incluindo o [Slackware](http://slackware.com), o [CRUX](http://www.crux.nu) e o [BSD](http://en.wikipedia.org/wiki/Berkeley_Software_Distribution). Em julho de 2007, Judd Vinet deixou o cargo de Líder de Projeto para perseguir outros interesses e foi substituído por Aaron Griffin, que permanece como líder do projeto até hoje.

Veja também: [History of Arch Linux (Português)](/index.php/History_of_Arch_Linux_(Portugu%C3%AAs) "History of Arch Linux (Português)").

## Simplicidade

Seguindo a filosofia [The Arch Way (Português)](/index.php/The_Arch_Way_(Portugu%C3%AAs) "The Arch Way (Português)"), o Arch Linux é leve, flexível, simples e visa ser bastante UNIX-_like_.Um ambiente mínimo (sem GUI) compilado para as arquiteturas i686/x86_64 é proporcionado após a instalação: ao invés de ter de desinstalar pacotes desnecessários ou indesejados, é oferecida ao usuário avançado a habilidade de construir a partir de um alicerce mínimo, sem quaisquer padrões escolhidos antecipadamente. A filosofia de design do Arch e sua implementação tornam fácil estendê-lo ou moldá-lo em qualquer tipo de sistema requerido, de um console minimalista aos mais grandiosos e completos ambientes de desktop disponíveis: é _o usuário_ quem decide o que o seu sistema Arch será.

O simples sistema init do Arch foi profundamente inspirado pela maneira como os *BSD incorporam chamadas de um _único arquivo_ ([rc.conf (Português)](/index.php?title=Rc.conf_(Portugu%C3%AAs)&action=edit&redlink=1 "Rc.conf (Português) (page does not exist)")) ao invés da estrutura de diretórios do SysVinit, contendo dezenas de links simbólicos para cada runlevel. A configuração do sistema é feita editando simples arquivos de texto.

## Modernidade

O Arch Linux se empenha em oferecer as últimas versões estáveis de seus pacotes, e é baseado no sistema de _rolling-release_, que permite uma única instalação e upgrades contínuos e ininterruptos, sem nunca ter de instalar ou realizar elaborados upgrades de sistema de uma versão para a próxima. Com apenas um comando, o Arch é mantido atualizado e na vanguarda absoluta.

O Arch incorpora muitas das mais novas funcionalidades disponíveis para os usuários do GNU/Linux, incluindo sistemas de arquivos modernos (Ext2/3/4, Reiser, XFS, JFS), LVM2/EVMS, RAID via software, suporte ao udev e initcpio, bem como os últimos kernels.

## Empacotamento de Software

O Arch é apoiado pelo [pacman (Português)](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)"), um gerenciador de pacotes binário e fácil de usar que permite que você faça o upgrade do sistema inteiro com apenas um comando. O pacman é programado em _C_ e projetado desde o começo para ser leve, simples e muito rápido. O Arch Linux também possui o [Arch Build System (Português)](/index.php?title=Arch_Build_System_(Portugu%C3%AAs)&action=edit&redlink=1 "Arch Build System (Português) (page does not exist)"), sistema parecido com o ports que torna fácil compilar e instalar pacotes a partir da fonte, e que também podem ser sincronizados com um comando. Você pode até mesmo recompilar seu sistema inteiro com apenas um comando.

Suportando as arquiteturas i686 e x86_64, os [Official Repositories (Português)](/index.php/Official_Repositories_(Portugu%C3%AAs) "Official Repositories (Português)") do Arch fornecem vários milhares de pacotes de alta qualidade para atender às suas demandas de software. Além disso, o Arch encoraja o crescimento da comunidade e da contribuição, oferecendo o [Arch User Repository (Português)](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)"), que contém muitas centenas de scripts PKGBUILD mantidos pelos usuários, que podem ser usados pelo programa _makepkg_ para compilar pacotes instaláveis a partir da fonte. Também é possível para os usuários facilmente criar e manter seus próprios repositórios.

## Integridade do Código-Fonte

O Arch Linux provê seu software sem patches ou modificações; os pacotes são criados puramente a partir do upstream, da maneira como o autor originalmente pretendeu que fosse distribuído. Adição de patches ocorre apenas em casos extremamente raros, para prevenir quebras severas no sistema, no caso de desencontro de versões, que podem ocorrer no modelo de _rolling release_.

## Comunidade

A comunidade do Arch é bastante segura, vigorosa e acolhedora: todos os _Archers_ são encorajados a participar e dar sua contribuição para a distribuição, seja ajudando com o desenvolvimento do software núcleo, mantendo pacotes, relatando ou consertando [bugs](https://bugs.archlinux.org/), melhorando a [documentação da ArchWiki](/index.php/Main_Page_(Portugu%C3%AAs) "Main Page (Português)"), ajudando outros usuários a resolver problemas ou apenas discutindo nos [fórums](https://bbs.archlinux.org/), [listas de discussão](https://mailman.archlinux.org/mailman/listinfo/), [Canais de IRC](/index.php/Canais_de_IRC "Canais de IRC"), ou compartilhando seu conhecimento ou mesmo os programas que desenvolveu. O Arch Linux é o sistema operacional escolhido por muitas pessoas no mundo todo, e existem várias [comunidades internacionais](/index.php?title=International_Communities_(Portugu%C3%AAs)&action=edit&redlink=1 "International Communities (Português) (page does not exist)") que oferecem ajuda e documentação em várias línguas diferentes.

Veja a página [Getting Involved (Português)](/index.php/Getting_Involved_(Portugu%C3%AAs) "Getting Involved (Português)") se você deseja tornar-se um membro ativo da comunidade.

## Resumo

Para resumir: o Arch Linux é uma distribuição simples e versátil, projetada para atender às necessidades de usuários competentes do Linux®. Ele é tanto poderoso quanto fácil de manter, tornando-se a distro ideal para servidores e estações de trabalho. Leve-o à direção que você quiser: se você compartilha essa visão sobre o que uma distribuição GNU/Linux deve ser, então você é bem-vindo e encorajado a usá-lo livremente, envolver-se com o projeto, e contribuir com a comunidade. Bem-vindo ao Arch!