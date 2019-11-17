**Status de tradução:** Esse artigo é uma tradução de [Kernel](/index.php/Kernel "Kernel"). Data da última tradução: 2019-11-10\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Kernel&diff=0&oldid=587067) na versão em inglês.

Artigos relacionados

*   [Módulos de kernel](/index.php/Kernel_modules "Kernel modules")
*   [Compilar módulo de kernel](/index.php/Compile_kernel_module "Compile kernel module")
*   [Kernel Panics](/index.php/Kernel_Panics "Kernel Panics")
*   [sysctl](/index.php/Sysctl "Sysctl")

De acordo com o Wikipédia:

	O [kernel Linux](https://en.wikipedia.org/wiki/pt:Linux_(n%C3%BAcleo) (ou núcleo Linux) é um [kernel para sistemas operacionais](https://en.wikipedia.org/wiki/pt:N%C3%BAcleo_(sistema_operacional) tipo UNIX, monolítico e de código aberto.

[Arch Linux](/index.php/Arch_Linux_(Portugu%C3%AAs) "Arch Linux (Português)") é baseado no kernel do Linux. Existem vários kernels Linux disponíveis para o Arch Linux, além do kernel estável mais recente. Este artigo lista algumas das opções disponíveis nos repositórios com uma breve descrição de cada uma. Há também uma descrição dos patches que podem ser aplicados ao kernel do sistema. O artigo termina com uma visão geral da compilação personalizada do kernel com links para vários métodos.

Os pacotes de kernel são [instalados](/index.php/Instala "Instala") no sistema de arquivos em `/boot/`. Para poder inicializar no kernels, o [gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot") deve ser configurado adequadamente.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Kernels com suporte oficial](#Kernels_com_suporte_oficial)
*   [2 Compilação](#Compilação)
*   [3 Kernels do kernel.org](#Kernels_do_kernel.org)
*   [4 Patches e patchsets](#Patches_e_patchsets)
    *   [4.1 Patchsets principais](#Patchsets_principais)
    *   [4.2 Outros patchsets](#Outros_patchsets)
*   [5 Veja também](#Veja_também)

## Kernels com suporte oficial

*   **Stable** — Kernel e módulos Vanilla Linux, com alguns patches aplicados.

	[https://www.kernel.org/](https://www.kernel.org/) || [linux](https://www.archlinux.org/packages/?name=linux)

*   **Hardened** — Um kernel Linux focado na segurança que aplica um conjunto de patches rígidos para mitigar as explorações do kernel e do espaço do usuário. Ele também permite mais recursos de fortalecimento do kernel upstream do que [linux](https://www.archlinux.org/packages/?name=linux).

	[https://github.com/anthraxx/linux-hardened](https://github.com/anthraxx/linux-hardened) || [linux-hardened](https://www.archlinux.org/packages/?name=linux-hardened)

*   **Longterm** — Kernel e módulos Linux de suporte a longo prazo (LTS).

	[https://www.kernel.org/](https://www.kernel.org/) || [linux-lts](https://www.archlinux.org/packages/?name=linux-lts)

*   **Zen Kernel** — Resultado de um esforço colaborativo de hackers do kernel para fornecer o melhor kernel Linux possível para os sistemas do dia a dia. Mais detalhes podem ser encontrados em [https://liquorix.net](https://liquorix.net) (que fornece binários de kernel baseados no Zen for Debian).

	[https://github.com/zen-kernel/zen-kernel](https://github.com/zen-kernel/zen-kernel) || [linux-zen](https://www.archlinux.org/packages/?name=linux-zen)

## Compilação

O Arch Linux fornece dois métodos para compilar seu próprio kernel.

	[/Arch Build System](/index.php/Kernel/Arch_Build_System "Kernel/Arch Build System")

	Aproveita a alta qualidade do [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") existente do [linux](https://www.archlinux.org/packages/?name=linux) e os benefícios de [gerenciamento de pacote](https://en.wikipedia.org/wiki/pt:Sistema_gestor_de_pacotes "wikipedia:pt:Sistema gestor de pacotes").

	[/Compilação tradicional](/index.php/Kernel/Traditional_compilation "Kernel/Traditional compilation")

	Envolve o download manual de um tarball de origem e a compilação no diretório inicial como um usuário normal.

## Kernels do kernel.org

*   **Git** — Kernel e módulos Linux compilados usando fontes do repositório Git de Linus Torvalds

	[https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git) || [linux-git](https://aur.archlinux.org/packages/linux-git/)

*   **Mainline** — Kernels onde todos os novos recursos são introduzidos, lançados a cada 2-3 meses.

	[https://www.kernel.org/](https://www.kernel.org/) || [linux-mainline](https://aur.archlinux.org/packages/linux-mainline/)

*   **Next** — Kernels mais recentes com recursos pendentes para serem mesclados na próxima versão da linha principal.

	[https://www.kernel.org/doc/man-pages/linux-next.html](https://www.kernel.org/doc/man-pages/linux-next.html) || [linux-next-git](https://aur.archlinux.org/packages/linux-next-git/)

*   **Longterm 3.16** — Kernel e módulos Linux 3.16 de suporte a longo prazo (LTS).

	[https://www.kernel.org/](https://www.kernel.org/) || [linux-lts316](https://aur.archlinux.org/packages/linux-lts316/)

*   **Longterm 4.4** — Kernel e módulos Linux 4.4 de suporte a longo prazo (LTS).

	[https://www.kernel.org/](https://www.kernel.org/) || [linux-lts44](https://aur.archlinux.org/packages/linux-lts44/)

*   **Longterm 4.9** — Kernel e módulos Linux 4.9 de suporte a longo prazo (LTS).

	[https://www.kernel.org/](https://www.kernel.org/) || [linux-lts49](https://aur.archlinux.org/packages/linux-lts49/)

*   **Longterm 4.14** — Kernel e módulos Linux 4.14 de suporte a longo prazo (LTS).

	[https://www.kernel.org/](https://www.kernel.org/) || [linux-lts414](https://aur.archlinux.org/packages/linux-lts414/)

## Patches e patchsets

Existem muitas razões para corrigir o seu kernel, as principais são para desempenho ou suporte a recursos que não são da linha principal, como o suporte ao sistema de arquivos [reiser4](/index.php/Reiser4 "Reiser4"). Outras razões podem incluir diversão e ver como isso é feito e quais são as melhorias.

No entanto, é importante notar que a melhor maneira de aumentar a velocidade do seu sistema é primeiro adaptar o kernel ao seu sistema, especialmente a arquitetura e o tipo de processador. Por esse motivo, o uso de versões pré-empacotadas de kernels personalizados com configurações genéricas de arquitetura não é recomendado nem realmente vale a pena. Um benefício adicional é que você pode reduzir o tamanho do seu kernel (e, portanto, tempo de compilação), não incluindo suporte para itens que você não possui ou usa. Por exemplo, você pode começar com a configuração do kernel padrão quando uma nova versão do kernel for lançada e remover o suporte a itens como Bluetooth, video4linux, Ethernet de 1000 Mbit etc., funcionalidades que você sabe que não precisará para sua máquina específica. Embora esta página não seja para personalizar a configuração do seu kernel, ela é recomendada como um primeiro passo - antes de passar a usar um conjunto de patches depois de entender os fundamentos envolvidos.

Os arquivos de configuração para os pacotes do kernel do Arch podem ser usados como ponto de partida. Eles estão nos arquivos de origem do pacote Arch, por exemplo [[1]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/linux) vinculados a partir de [linux](https://www.archlinux.org/packages/?name=linux). O arquivo de configuração do seu kernel atualmente em execução também pode estar disponível no seu sistema de arquivos em `/proc/config.gz` se a opção do kernel `CONFIG_IKCONFIG_PROC` estiver ativada.

Se você realmente não corrigiu ou personalizou um kernel antes, não é tão difícil e existem muitos PKGBUILDs no fórum para conjuntos de patches individuais. No entanto, é aconselhável começar do zero com um pouco de pesquisa sobre os benefícios de cada conjunto de patches, em vez de escolher apenas um. Dessa forma, você aprenderá muito mais sobre o que está fazendo, em vez de apenas escolher um kernel na inicialização e ficar imaginando o que ele realmente faz.

**Atenção:** Os patchesets são desenvolvidos por uma variedade de pessoas. Algumas dessas pessoas estão realmente envolvidas na produção do kernel Linux e outras são entusiastas, o que pode refletir seu nível de confiabilidade e estabilidade.

### Patchsets principais

*   **[Linux-ck](/index.php/Linux-ck "Linux-ck")** — Contém os patches da Con Kolivas projetados para melhorar a capacidade de resposta do sistema, com ênfase específica na área de trabalho, mas adequados a qualquer carga de trabalho.

	[http://ck.kolivas.org/](http://ck.kolivas.org/) || [linux-ck](https://aur.archlinux.org/packages/linux-ck/)

*   **pf-kernel** — Fornece um punhado de recursos impressionantes não mesclados na linha principal. Ele não se baseia no fork ou no patchset do Linux existente, embora alguns ports não oficiais possam ser usadas se os patches necessários não tiverem sido lançados oficialmente. Os patches mais proeminentes do linux-pf são o agendador de CPU PDS e UKSM.

	[https://gitlab.com/post-factum/pf-kernel/wikis/README](https://gitlab.com/post-factum/pf-kernel/wikis/README) || Pacotes:

*   [Repositório](/index.php/Unofficial_user_repositories#post-factum_kernels "Unofficial user repositories") do desenvolvedor do pf-kernel, [post-factum](https://aur.archlinux.org/account/post-factum)
*   [Repositório](/index.php/Unofficial_user_repositories#home-thaodan "Unofficial user repositories"), [linux-pf](https://aur.archlinux.org/packages/linux-pf/), [linux-pf-preset-default](https://aur.archlinux.org/packages/linux-pf-preset-default/), [linux-pf-lts](https://aur.archlinux.org/packages/linux-pf-lts/) do desenvolvedor do fork do pf-kernel, [Thaodan](https://aur.archlinux.org/account/Thaodan)

*   **[Realtime kernel](/index.php/Realtime_kernel "Realtime kernel")** — Mantido por um pequeno grupo de desenvolvedores principais, liderado por Ingo Molnar. Esse patch permite que quase todo o kernel seja antecipado, com exceção de algumas regiões muito pequenas de código ("regiões críticas de raw_spinlock"). Isso é feito substituindo a maioria dos spinlocks do kernel por mutexes que suportam a herança de prioridade, além de mover todas as interrupções e interrupções do software para os threads do kernel.

	[https://wiki.linuxfoundation.org/realtime/start](https://wiki.linuxfoundation.org/realtime/start) || [linux-rt](https://aur.archlinux.org/packages/linux-rt/), [linux-rt-lts](https://aur.archlinux.org/packages/linux-rt-lts/)

### Outros patchsets

Alguns dos pacotes listados também podem estar disponíveis como pacotes binários via [Repositórios não oficiais de usuários](/index.php/Unofficial_user_repositories "Unofficial user repositories").

*   **[AppArmor](/index.php/AppArmor "AppArmor")** — O sistema do [Mandatory Access Control](https://en.wikipedia.org/wiki/Mandatory_access_control "wikipedia:Mandatory access control") (MAC), implementado no [Linux Security Modules](https://en.wikipedia.org/wiki/Linux_Security_Modules "wikipedia:Linux Security Modules") (LSM). Enquanto o [linux](https://www.archlinux.org/packages/?name=linux) suporta o apparmor, este kernel tem os [parâmetros do kernel](/index.php/Par%C3%A2metros_do_kernel "Parâmetros do kernel") necessários habilitados por padrão.

	[https://gitlab.com/apparmor/apparmor/wikis/About](https://gitlab.com/apparmor/apparmor/wikis/About) || [linux-apparmor](https://aur.archlinux.org/packages/linux-apparmor/)

*   **Aufs** — O kernel e os módulos do linux compatíveis com aufs, úteis ao usar o [docker](/index.php/Docker "Docker").

	[http://aufs.sourceforge.net/](http://aufs.sourceforge.net/) || [linux-aufs](https://aur.archlinux.org/packages/linux-aufs/)

*   **Clear** — Patches do projeto Clear Linux da Intel. Fornece otimizações de desempenho e segurança; Módulo [WireGuard](/index.php/WireGuard "WireGuard").

	[https://github.com/clearlinux-pkgs/linux](https://github.com/clearlinux-pkgs/linux) || [linux-clear](https://aur.archlinux.org/packages/linux-clear/)

*   **Libre** — Os kernels do Linux sem "blobs binários".

	[https://www.fsfla.org/ikiwiki/selibre/linux-libre/](https://www.fsfla.org/ikiwiki/selibre/linux-libre/) || [linux-libre](https://aur.archlinux.org/packages/linux-libre/)

*   **Liquorix** — Substituição do kernel criada usando a configuração direcionada ao Debian e as fontes do kernel Zen. Projetado para cargas de trabalho de desktop, multimídia e jogos, é frequentemente usado como um kernel de substituição de desempenho Debian Linux. Damentz, o mantenedor do patchset Liquorix, também é desenvolvedor do patchset Zen.

	[https://liquorix.net](https://liquorix.net) || [linux-lqx](https://aur.archlinux.org/packages/linux-lqx/)

*   **MultiPath TCP** — O kernel do Linux e os módulos com suporte a Multipath TCP.

	[https://multipath-tcp.org/](https://multipath-tcp.org/) || [linux-mptcp](https://aur.archlinux.org/packages/linux-mptcp/)

*   **[Reiser4](/index.php/Reiser4 "Reiser4")** — Sistema de arquivos sucessor do ReiserFS, desenvolvido do zero por Namesys e Hans Reiser.

	[https://sourceforge.net/projects/reiser4/files/](https://sourceforge.net/projects/reiser4/files/) || [linux-ck-reiser4](https://aur.archlinux.org/packages/linux-ck-reiser4/)

*   **VFIO** — O kernel do Linux e alguns patches escritos por Alex Williamson (substituição de ACS e i915) para permitir a capacidade de passagem do PCI com o KVM em algumas máquinas.

	[https://lwn.net/Articles/499240/](https://lwn.net/Articles/499240/) || [linux-vfio](https://aur.archlinux.org/packages/linux-vfio/), [linux-vfio-lts](https://aur.archlinux.org/packages/linux-vfio-lts/)

*   **XanMod** — Com o objetivo de aproveitar ao máximo as estações de trabalho de alto desempenho, os desktops de jogos, os centros de mídia e outros, criados para oferecer uma experiência de desktop mais sólida, responsiva e suave. Este kernel usa o agendador BFS, o agendador de E/S BFQ, a deduplicação de dados da memória em tempo real do UKSM, o controle de congestionamento YeAH TCP, o suporte avançado ao conjunto de instruções x86_64 e outras alterações padrão.

	[https://xanmod.org/](https://xanmod.org/) || [linux-xanmod](https://aur.archlinux.org/packages/linux-xanmod/)

## Veja também

*   [O'Reilly - Linux Kernel in a Nutshell](http://www.kroah.com/lkn/) (free ebook)
*   [What stable kernel should I use?](http://kroah.com/log/blog/2018/08/24/what-stable-kernel-should-i-use/) by Greg Kroah-Hartman