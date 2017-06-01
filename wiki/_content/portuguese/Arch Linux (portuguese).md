O Arch Linux é uma distribuição GNU/Linux x86_64 de uso geral desenvolvida independentemente que se empenha em fornecer as últimas versões estáveis da maioria dos softwares seguindo um modelo *rolling-release*. A instalação padrão é um sistema base mínimo, configurado pelo usuário para adicionar apenas o que é propositalmente necessário.

## Contents

*   [1 Princípios](#Princ.C3.ADpios)
    *   [1.1 Simplicidade](#Simplicidade)
    *   [1.2 Modernidade](#Modernidade)
    *   [1.3 Pragmatismo](#Pragmatismo)
    *   [1.4 Centrado no usuário](#Centrado_no_usu.C3.A1rio)
    *   [1.5 Versatility](#Versatility)
*   [2 História](#Hist.C3.B3ria)
    *   [2.1 Os primeiros anos](#Os_primeiros_anos)
    *   [2.2 Os anos médios](#Os_anos_m.C3.A9dios)
    *   [2.3 Nascimento do ArchWiki](#Nascimento_do_ArchWiki)
    *   [2.4 O alvorecer da era A. Griffin](#O_alvorecer_da_era_A._Griffin)
    *   [2.5 Arch Install Scripts](#Arch_Install_Scripts)
    *   [2.6 A era do systemd](#A_era_do_systemd)
    *   [2.7 Fim do suporte a i686](#Fim_do_suporte_a_i686)

## Princípios

### Simplicidade

O Arch Linux define simplicidade como *sem adições ou modificações desnecessárias*. Ele provê softwares conforme lançado pelos desenvolvedores originais ([upstream](https://en.wikipedia.org/wiki/Upstream_(software_development) "wikipedia:Upstream (software development)")) com alterações mínimas específicas da distribuição (downstream): patches não aceitos pelo upstream são evitados, e patches de downstream do Arch consistem quase totalmente em correções de erros de *backport* que são obsoletos pelo próximo lançamento do projeto.

De uma forma similar, Arch provê os arquivos de configurações fornecidos pelo upstream com alterações limitadas a questões específicas de distribuição, como ajustar caminhos de arquivos de sistema. Ele não adiciona recursos de automação como habilitar um serviço apenas porque o pacote foi instalado. Pacotes só são divididos quando houver vantagens interessantes, tal como economizar espaço em disco em casos em que haja grande desperdício. Utilitários de configuração GUI não são oficialmente fornecidos, incentivando usuários a realizar a maioria da configuração de sistema a partir do shell ou um editor de texto.

### Modernidade

O Arch Linux se empenha em oferecer as últimas versões estáveis de seus pacotes desde que quebra sistemática de pacote possa ser razoavelmente evitado. Ele é baseado em um sistema de [rolling-release](https://en.wikipedia.org/wiki/pt:Rolling_release "wikipedia:pt:Rolling release"), que permite uma única instalação e upgrades contínuos.

O Arch incorpora muitas das mais novas funcionalidades disponíveis para os usuários do GNU/Linux, incluindo o sistema de inicialização [systemd](/index.php/Systemd "Systemd"), [sistemas de arquivos](/index.php/File_systems "File systems") modernos, LVM2, RAID via software, suporte ao udev e initcpio (com [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")), bem como os últimos kernels.

### Pragmatismo

Arch é uma distribuição pragmática, em vez de uma ideológica. Os princípios aqui são apenas diretrizes úteis. Em última análise, decisões de design são feitas caso a caso pelo consenso de desenvolvedores. Análise técnica baseada em evidências e debate são o que importam, não políticas e opinião popular.

O grande número de pacotes e scripts de compilação nos vários repositórios do Arch Linux oferem software livre e de código aberto para aqueles que o preferem, assim como pacotes de software proprietário para aqueles que adotam funcionalidade sobre ideologia.

### Centrado no usuário

Enquanto muitas distribuições GNU/Linux tentam ser mais *user-friendly*, o Arch Linux sempre foi e sempre será *user-centric*. O Arch Linux tem a intenção de preencher as necessidades daqueles contribuindo para ele em vez de tentar agradar a maior quantidade de usuários possível. Ele é direcionado para o usuário GNU/Linux avançado ou a qualquer outro com uma atividade "faça você mesmo" que esteja interessado em ler a documentação e resolver seus próprios problemas.

Todos os usuários são incentivados a [participar](/index.php/Getting_involved_(Portugu%C3%AAs) "Getting involved (Português)") e contribuir com a distribuição. Relatar e ajudar a corrigir [falhas](https://bugs.archlinux.org/) é muito valioso e patches que aprimorem pacotes ou os [projetos](https://projects.archlinux.org/) centrais são muito bem-vindos: desenvolvedores do Arch são voluntários e contribuidores ativos frequentemente se verão se tornando parte da equipe. *Archers* podem contribuir livremente com pacotes para o [Arch User Repository](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)"), melhroar a [documentação do ArchWiki](/index.php/Main_page_(Portugu%C3%AAs) "Main page (Português)"), fornecer assistência técnica para outros ou apenas trocar opiniões nos [fóruns](https://bbs.archlinux.org/), [listas de discussões](https://mailman.archlinux.org/mailman/listinfo/) ou [canais IRC](/index.php/IRC_channels "IRC channels"). Arch Linux é o sistema operacional de escolha para muitos pacotes pelo mundo, e há várias [comunidades internacionais](/index.php/International_communities "International communities") que oferecem ajuda e fornecem documentação em muitos idiomas diferentes.

### Versatility

Arch Linux é uma distribuição de propósito geral. Na instalação, apenas um ambiente de linha de comando é fornecido: em vez de separar pacotes desnecessários e indesejados, ao usuário é oferecido a habilidade de compilar um sistema personalizado escolhendo entre milhares de pacotes de alta qualidade fornecidos nos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais") para a arquitetura [x86-64](https://en.wikipedia.org/wiki/pt:AMD64 "wikipedia:pt:AMD64"). Suporte para [i686](https://en.wikipedia.org/wiki/pt:I686 "wikipedia:pt:I686") será [cessado](http://www.archlinux-br.org/noticias/254/) em Novembro de 2017.

Arch funciona com o [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)"), um gerenciador de pacotes leve, simples e rápido que permite atualizar todo o sistema com apenas um comando. Arch também fornece o [Arch Build System](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)"), um sistema tipo *ports* para facilitar a compilação e instalação de pacotes a partir do fonte, que também pode ser sincronizado com um comando. Além disso, o *Arch User Repository* contém muitos milhares mais de scripts [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") contribuídos pela comunidade para compilar pacotes instaláveis a partir dos fontes usando o aplicativo [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)"). Também é possível para usuários compilar e manter seus próprios repositórios personalizados com facilidade.

## História

### Os primeiros anos

Judd Vinet, um programador canadense e guitarrista ocasional, começou a desenvolver o Arch Linux no começo de 2001\. Seu primeiro lançamento formal, Arch Linux 0.1, foi em 11 de março de 2002\. Inspirado pela elegante simplicidade do [Slackware](http://www.slackware.com/), [BSD](https://en.wikipedia.org/wiki/pt:Berkeley_Software_Distribution "wikipedia:pt:Berkeley Software Distribution"), [PLD Linux](http://www.pld-linux.org/) e [CRUX](http://crux.nu/), mas desapontado com a falta de gerenciamento de pacotes na época; Vinet construiu sua própria distribuição com princípios similares àquelas distros; no entanto, ele também escreveu um gerenciador de programas chamado [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)"), para manipular automaticamente a instalação, remoção e atualizações de pacotes.

### Os anos médios

A comunidade inicial do Arch cresceu firmemente, como evidencia [esse gráfico do número de publicações de fóruns, usuários e relatórios de bugs](https://dev.archlinux.org/~dan/archstats.svg). Além disso, foi desde o começo conhecida como [uma comunidade aberta, amigável e prestativa](http://www.osnews.com/story/4827).

### Nascimento do ArchWiki

Em 2005-07-08 o ArchWiki foi [configurado](/index.php/ArchWiki:About_(Portugu%C3%AAs)#Hist.C3.B3ria "ArchWiki:About (Português)") pela primeira vez no motor do MediaWiki.

### O alvorecer da era A. Griffin

No fim de 2007, Judd Vinet se afastou da participação ativa como desenvolvedor do Arch, e [transferiu sem problemas o reinado para o programador americano Aaron Griffin](https://bbs.archlinux.org/viewtopic.php?id=38024), também conhecido como Phrakture, que continua como líder do desenvolvimento do Arch até hoje.

Com o passar dos anos, a comunidade do Arch continuou a crescer e amadurecer, e recentemente tem recebido uma quantidade incomum de [atenção e análises](/index.php/Arch_Linux_press_coverage "Arch Linux press coverage") para uma distro Linux de seu tamanho.

Os desenvolvedores do Arch continuam a ser voluntários não-pagos e de meio expediente, e não existem expectativas de monetizar o Arch Linux, de modo que ele continuará a ser livre em todos os sentidos da palavra. Aqueles curiosos para ler mais detalhes sobre a história do desenvolvimento do Arch podem navegar na [entrada sobre o Arch na Internet Archive Wayback Machine](http://web.archive.org/web/*/archlinux.org).

### Arch Install Scripts

O lançamento de 2012-07-15 da imagem de instalação tornou [obsoleto](http://www.archlinux-br.org/noticias/192/) o sistema de menus Arch Installation Framework em favor do Arch Install Scripts.

### A era do systemd

Entre 2012 e 2013, o tradicional sistema de inicialização System V foi substituído pelo systemd.[[1]](http://www.archlinux-br.org/noticias/199/)[[2]](http://www.archlinux-br.org/noticias/200/)[[3]](http://www.archlinux-br.org/noticias/204/)[[4]](http://www.archlinux-br.org/noticias/207/)

### Fim do suporte a i686

Em 2017-01-25, foi [anunciado](http://www.archlinux-br.org/noticias/254/) que o suporte à arquitetura i686 seria encerrado em razão da decrescente popularidade dentre os desenvolvedores e da comunidade.