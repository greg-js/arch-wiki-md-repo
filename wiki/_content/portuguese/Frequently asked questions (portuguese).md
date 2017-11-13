Artigos relacionados

*   [Arch terminology (Português)](/index.php/Arch_terminology_(Portugu%C3%AAs) "Arch terminology (Português)")
*   [Arch User Repository (Português)#FAQ](/index.php/Arch_User_Repository_(Portugu%C3%AAs)#FAQ "Arch User Repository (Português)")
*   [General troubleshooting](/index.php/General_troubleshooting "General troubleshooting")

## Contents

*   [1 Geral](#Geral)
    *   [1.1 O que é o Arch Linux?](#O_que_.C3.A9_o_Arch_Linux.3F)
    *   [1.2 Por que eu não gostaria de usar o Arch?](#Por_que_eu_n.C3.A3o_gostaria_de_usar_o_Arch.3F)
    *   [1.3 A quais arquiteturas o Arch oferece suporte?](#A_quais_arquiteturas_o_Arch_oferece_suporte.3F)
    *   [1.4 O Arch oferece suporte a CPUs ARM?](#O_Arch_oferece_suporte_a_CPUs_ARM.3F)
    *   [1.5 O Arch segue o FHS?](#O_Arch_segue_o_FHS.3F)
    *   [1.6 Eu sou um completo iniciante no GNU/Linux. Eu deveria usar o Arch?](#Eu_sou_um_completo_iniciante_no_GNU.2FLinux._Eu_deveria_usar_o_Arch.3F)
    *   [1.7 O Arch é projetado para ser usado como um servidor? Um desktop? Uma estação de trabalho?](#O_Arch_.C3.A9_projetado_para_ser_usado_como_um_servidor.3F_Um_desktop.3F_Uma_esta.C3.A7.C3.A3o_de_trabalho.3F)
    *   [1.8 Eu realmente gosto do Arch, exceto que a equipe de desenvolvimento precisa implementar o recurso X](#Eu_realmente_gosto_do_Arch.2C_exceto_que_a_equipe_de_desenvolvimento_precisa_implementar_o_recurso_X)
    *   [1.9 Quando o novo lançamento estará disponível?](#Quando_o_novo_lan.C3.A7amento_estar.C3.A1_dispon.C3.ADvel.3F)
    *   [1.10 O Arch Linux é uma distribuição estável? Vou presenciar frequentes quebras?](#O_Arch_Linux_.C3.A9_uma_distribui.C3.A7.C3.A3o_est.C3.A1vel.3F_Vou_presenciar_frequentes_quebras.3F)
    *   [1.11 O Arch precisa de mais divulgação (i.e. propaganda)](#O_Arch_precisa_de_mais_divulga.C3.A7.C3.A3o_.28i.e._propaganda.29)
    *   [1.12 O Arch precisa de mais desenvolvedores](#O_Arch_precisa_de_mais_desenvolvedores)
    *   [1.13 Por que a minha internet está tão mais lenta em comparação com outros sistemas operacionais?](#Por_que_a_minha_internet_est.C3.A1_t.C3.A3o_mais_lenta_em_compara.C3.A7.C3.A3o_com_outros_sistemas_operacionais.3F)
    *   [1.14 Por que o Arch está usando toda minha RAM?](#Por_que_o_Arch_est.C3.A1_usando_toda_minha_RAM.3F)
    *   [1.15 Para onde foi todo meu espaço livre?](#Para_onde_foi_todo_meu_espa.C3.A7o_livre.3F)
*   [2 Gerenciamento de pacote](#Gerenciamento_de_pacote)
    *   [2.1 Eu encontrei um erro no pacote X. O que eu devo fazer?](#Eu_encontrei_um_erro_no_pacote_X._O_que_eu_devo_fazer.3F)
    *   [2.2 Os pacotes do Arch precisam usar uma nomenclatura única. ".pkg.tar.gz" e "pkg.tar.xz" é muito longo e/ou confuso](#Os_pacotes_do_Arch_precisam_usar_uma_nomenclatura_.C3.BAnica._.22.pkg.tar.gz.22_e_.22pkg.tar.xz.22_.C3.A9_muito_longo_e.2Fou_confuso)
    *   [2.3 O pacman precisa de uma biblioteca para que outros aplicativos possam acessar facilmente informações dos pacotes](#O_pacman_precisa_de_uma_biblioteca_para_que_outros_aplicativos_possam_acessar_facilmente_informa.C3.A7.C3.B5es_dos_pacotes)
    *   [2.4 O pacman precisa do recurso X!](#O_pacman_precisa_do_recurso_X.21)
    *   [2.5 Eu acabei de instalar o Pacote X. Como eu o inicio?](#Eu_acabei_de_instalar_o_Pacote_X._Como_eu_o_inicio.3F)
    *   [2.6 Por que há alguma uma única versão de cada biblioteca compartilhada nos repositórios oficiais?](#Por_que_h.C3.A1_alguma_uma_.C3.BAnica_vers.C3.A3o_de_cada_biblioteca_compartilhada_nos_reposit.C3.B3rios_oficiais.3F)
    *   [2.7 E se eu executar uma atualização completa do sistema e houver uma atualização para uma biblioteca compartilhada, mas não para os aplicativos que dependem dela?](#E_se_eu_executar_uma_atualiza.C3.A7.C3.A3o_completa_do_sistema_e_houver_uma_atualiza.C3.A7.C3.A3o_para_uma_biblioteca_compartilhada.2C_mas_n.C3.A3o_para_os_aplicativos_que_dependem_dela.3F)
    *   [2.8 É possível haver uma atualização de versão maior do kernel no repositório e que alguns dos pacotes de driver não tenham sido atualizados?](#.C3.89_poss.C3.ADvel_haver_uma_atualiza.C3.A7.C3.A3o_de_vers.C3.A3o_maior_do_kernel_no_reposit.C3.B3rio_e_que_alguns_dos_pacotes_de_driver_n.C3.A3o_tenham_sido_atualizados.3F)
    *   [2.9 O que fazer antes de atualizar?](#O_que_fazer_antes_de_atualizar.3F)
    *   [2.10 Uma atualização de pacote foi lançada, mas o pacman diz que o sistema está atualizado](#Uma_atualiza.C3.A7.C3.A3o_de_pacote_foi_lan.C3.A7ada.2C_mas_o_pacman_diz_que_o_sistema_est.C3.A1_atualizado)
    *   [2.11 Upstream do projeto *X* lançou uma nova versão. Quanto tempo vai levar para o pacote do Arch ser atualizado para essa nova versão?](#Upstream_do_projeto_X_lan.C3.A7ou_uma_nova_vers.C3.A3o._Quanto_tempo_vai_levar_para_o_pacote_do_Arch_ser_atualizado_para_essa_nova_vers.C3.A3o.3F)
*   [3 Instalação](#Instala.C3.A7.C3.A3o)
    *   [3.1 O Arch precisa de um instalador. Talvez um instalador gráfico?](#O_Arch_precisa_de_um_instalador._Talvez_um_instalador_gr.C3.A1fico.3F)
    *   [3.2 Eu instalei o Arch e agora eu estou em um shell! O que faço agora?](#Eu_instalei_o_Arch_e_agora_eu_estou_em_um_shell.21_O_que_fa.C3.A7o_agora.3F)
    *   [3.3 Qual ambiente de área de trabalho ou gerenciador de janelas eu devo usar?](#Qual_ambiente_de_.C3.A1rea_de_trabalho_ou_gerenciador_de_janelas_eu_devo_usar.3F)
    *   [3.4 O que faz do Arch único entre outras distribuições "minimalistas"?](#O_que_faz_do_Arch_.C3.BAnico_entre_outras_distribui.C3.A7.C3.B5es_.22minimalistas.22.3F)
*   [4 64 bit](#64_bit)
    *   [4.1 Como eu determino se meu processador é compatível com x86_64?](#Como_eu_determino_se_meu_processador_.C3.A9_compat.C3.ADvel_com_x86_64.3F)
    *   [4.2 Por que 64 bit?](#Por_que_64_bit.3F)
    *   [4.3 Como eu troco de i686 para x86_64 sem reinstalar?](#Como_eu_troco_de_i686_para_x86_64_sem_reinstalar.3F)

## Geral

### O que é o Arch Linux?

Veja o artigo [Arch Linux](/index.php/Arch_Linux_(Portugu%C3%AAs) "Arch Linux (Português)").

### Por que eu não gostaria de usar o Arch?

Você pode **não** querer usar o Arch, se:

*   você não tem habilidade/tempo/desejo para uma distribuição GNU/Linux do tipo *"faça você mesmo"*.
*   você precisa de suporte a uma arquitetura diferente de x86_64.
*   você insiste em usar uma distribuição que só fornece software livre conforme definido pela GNU.
*   você acredita que um sistema operacional deve se autoconfigurar, vir pronto para usar e incluir um conjunto padrão completo de softwares e ambiente de área de trabalho na mídia de instalação.
*   você não deseja uma distribuição GNU/Linux de lançamento contínuo (*rolling release*).
*   você está satisfeito com seu SO atual.

### A quais arquiteturas o Arch oferece suporte?

O Arch só oferece suporte à arquitetura x86_64 (algumas vezes chamada de amd64). Suporte à i686 está sendo desativado e será completamente retirado em Novembro de 2017[[1]](http://www.archlinux-br.org/noticias/260/): se você ainda está usando um sistema 32 bits, você pode se interessar em ler [#Como eu troco de i686 para x86_64 sem reinstalar?](#Como_eu_troco_de_i686_para_x86_64_sem_reinstalar.3F).

### O Arch oferece suporte a CPUs ARM?

Não, mas o projeto [Arch Linux ARM](http://archlinuxarm.org/) fornece um *port* do Arch Linux para várias plataformas ARM. Veja [[2]](http://ix.io/73w/irc).

### O Arch segue o [FHS](http://refspecs.linuxfoundation.org/FHS_3.0/fhs/index.html)?

O Arch Linux segue a *hierarquia de sistema de arquivos* para sistemas de arquivos usando o gerenciador de serviço [systemd](/index.php/Systemd "Systemd"). Veja [file-hierarchy(7)](http://jlk.fjfi.cvut.cz/arch/manpages/man/file-hierarchy.7) para uma explicação de cada diretório junto com suas designações. Em especial, `/bin`, `/sbin` e `/usr/sbin` são links simbólicos para `/usr/bin`, e `/lib` e `/lib64` são links simbólicos para `/usr/lib`.

### Eu sou um completo iniciante no GNU/Linux. Eu deveria usar o Arch?

Se você é um iniciante e deseja usar o Arch, você deve estar disposto a investir tempo para aprender um novo sistema, e aceitar que o Arch é projetado como uma distribuição de "faça você mesmo"; é o usuário que monta o sistema.

Antes de pedir ajuda, faça sua própria pesquisa em mecanismos de pesquisa, em fóruns e nas várias fantásticas documentações fornecidas pelo Arch Wiki. *Há uma razão para que estes recursos tenham sido disponibilizados*. Muitos milhares de *horas de voluntários* foram gastos compilando essas informações excelentes.

Veja também [Terminologia do Arch#RTFM](/index.php/Terminologia_do_Arch#RTFM "Terminologia do Arch") e o [Guia de instalação](/index.php/Guia_de_instala%C3%A7%C3%A3o "Guia de instalação").

### O Arch é projetado para ser usado como um servidor? Um desktop? Uma estação de trabalho?

O Arch não foi projetado para nenhum tipo de uso específico. Em vez disso, ele é projetado para um determinado tipo de *usuário*. O Arch visa usuários competentes que gostam de sua natureza *faça você mesmo* e que a exploram ainda para moldar o sistema para atender às suas necessidades exclusivas. Portanto, nas mãos de sua base de usuários alvo, o Arch pode ser usado praticamente qualquer propósito. Muitos usam o Arch em seus desktops e estações de trabalho. E, claro, o archlinux.org é executado no Arch.

### Eu realmente gosto do Arch, exceto que a equipe de desenvolvimento precisa implementar o recurso X

Envolva-se, contribua seu código/solução para a comunidade. Se for bem aceito pela comunidade e pela equipe de desenvolvimento, talvez seja incorporado. A comunidade do Arch prospera em contribuição e compartilhamento de código e ferramentas.

### Quando o novo lançamento estará disponível?

Os lançamentos do Arch Linux são apenas um ambiente *live* para instalação ou resgate, que inclui o grupo [base](https://www.archlinux.org/groups/x86_64/base/) e alguns [outros pacotes](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.both). Os lançamentos são geralmente emitidos na primeira metade de cada mês.

### O Arch Linux é uma distribuição estável? Vou presenciar frequentes quebras?

*O usuário* é o responsável pela estabilidade de seu próprio sistema de lançamento contínuo. O usuário é quem decide quando atualizar e mesclar alterações necessárias, quando necessário. Se o usuário buscar na comunidade por ajuda, geralmente consegue em pouco tempo. A diferença entre o Arch e outras distribuições está realmente no fato do Arch ser uma distribuição *faça você mesmo*; reclamações sobre quebras e travamentos são equivocadas e contraproducentes, já que alterações no upstream não são responsabilidade dos desenvolvedores do Arch.

Veja o artigo [Manutenção do sistema](/index.php/System_maintenance "System maintenance") para dicas sobre como fazer um sistema Arch o mais estável possível.

### O Arch precisa de mais divulgação (i.e. propaganda)

O Arch já está sendo bastante divulgado. O objetivo do Arch Linux não é ser grande. O objetivo é ser bem feito. Deixe que o crescimento ocorra naturalmente. Tentar forçar este crescimento só causará problemas.

### O Arch precisa de mais desenvolvedores

Possivelmente. Sinta-se livre para ser um voluntário! Visite os [fóruns](https://bbs.archlinux.org/), [canais IRC](/index.php/Canais_IRC "Canais IRC"), [listas de email](https://mailman.archlinux.org/mailman/listinfo/), e veja o que precisa ser feito. Se envolver no subfórum "Community Contributions" é uma boa forma de começar.

### Por que a minha internet está tão mais lenta em comparação com outros sistemas operacionais?

Sua rede está configurada corretamente? Dê uma olhada no artigo [Configuração de rede](/index.php/Configura%C3%A7%C3%A3o_de_rede "Configuração de rede").

Note também que o Arch Linux não vêm com [traffic shaping](https://en.wikipedia.org/wiki/pt:Traffic_shaping "wikipedia:pt:Traffic shaping") (modelagem de tráfego) habilitado. Então, é possível que se um programa de alguma forma utiliza sua conexão de internet por inteiro – independente de ser por conexões P2P ou cliente-servidor clássicas – outros locais vão considerar supersaturados, resultando em severos atrasos e tempos limites esgotados. Um alívio pode ser fornecido por [firewalls](/index.php/Firewalls "Firewalls") como Shorewall ou Vuurmuur; há também scritps estáticos para [iproute2](https://www.archlinux.org/packages/?name=iproute2) (como [esse derivado](http://serendipity.ruwenzori.net/index.php/2008/06/01/modified-wondershaper-for-better-voip-qos) do Wondershaper), que permitem a modelagem na camada de rede.

### Por que o Arch está usando toda minha RAM?

Essencialmente, RAM não usada é RAM desperdiçada.

Muitos novos usuários podem notar como que o kernel do Linux trata memória diferentemente de como era usado antes. Considerando que o acesso a dados da RAM é muito mais rápido do que de uma unidade de armazenamento, o cache do kernel de dados recentemente acessados na memória. Os dados em cache são apagados apenas quando o sistema começa a ficar sem memória disponível e novos dados precisam ser carregados.

Nós poderíamos fazer a distinção pelo comando `free`:

 `$ free -h` 
```
              total        used        free      shared  buff/cache   available
Mem:           2.8G        1.1G        283M        224M        1.4G        1.2G
Swap:          3.0G        881M        2.1G

```

É importante notar a diferença entre memória "free" (livre) e "available" (disponível). No exemplo acima, um laptop com 2.8G de RAM total parece estar usando a maioria dela, com apenas 283M como memória livre. Porém, 1.4G disto é "buff/cache". Há ainda 1.2G disponível para iniciar aplicativos, sem fazer swap. Veja `man free(1)` para detalhes. O resultado de tudo isso? Desempenho!

Veja [esse maravilhoso artigo](http://www.linuxjournal.com/article/2770) se você ficou curioso! Há também um site dedicado a esclarecer essa confusão: [http://www.linuxatemyram.com/](http://www.linuxatemyram.com/)

### Para onde foi todo meu espaço livre?

A resposta para essa questão depende de seu sistema. Há alguns [ótimos utilitários](/index.php/List_of_applications#Disk_usage_display "List of applications") que podem ajudar você a encontrar a resposta.

## Gerenciamento de pacote

Veja as páginas [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)"), [pacman/Tips and tricks](/index.php/Pacman/Tips_and_tricks "Pacman/Tips and tricks") e [Repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais") para mais respostas.

### Eu encontrei um erro no pacote X. O que eu devo fazer?

Primeiramente você precisa descobrir se o erro é algo que a equipe do Arch pode consertar. Algumas vezes não é (aquele travamento no firefox pode ser falha da equipe do Mozilla) - isto é chamado de *upstream error*. Se for um problema do Arch, existe uma série de coisas que você pode fazer:

1.  Procurar informações no fórum. Veja se alguém teve o mesmo problema.
2.  Informar o mantenedor do pacote. Rode um "pacman -Qi <nome do pacote>" para obter esta informação.
3.  Relatar o bug, com informações detalhadas, em [https://bugs.archlinux.org](https://bugs.archlinux.org)
4.  Se desejar, você pode criar um tópico no fórum descrevendo o problema e informando que você já relatou o mesmo. Isto ajuda a prevenir que várias pessoas relatem o mesmo erro.

### Os pacotes do Arch precisam usar uma nomenclatura única. ".pkg.tar.gz" e "pkg.tar.xz" é muito longo e/ou confuso

Isto vem sendo discutido na lista de discussão do Arch. Alguns propuseram uma extensão .pac. Até onde se sabe. não há nenhuma intenção em modificar a extensão dos pacotes. Como Tobias Kieslich, um dos desenvolvedores do Arch, colocou, "Um pacote **é** gzipped tarball!! E ele pode ser aberto, verificado e manipulado por qualquer aplicação tar. Além disso, o mime-type é automaticamente detectado pela maioria das aplicações".

### O pacman precisa de uma biblioteca para que outros aplicativos possam acessar facilmente informações dos pacotes

Já está sendo desenvolvida uma biblioteca para o pacman.

### O pacman precisa do recurso X!

Você leu o [The Arch Way](/index.php/The_Arch_Way "The Arch Way"), o [Arch Linux](/index.php/Arch_Linux "Arch Linux")? A filosofia do Arch é "Keep It Simple". Se você acha que sua ideia tem fundamento, e que ela não viola esta filosofia, então você pode discuti-la no [fórum](https://bbs.archlinux.org/). Você pode, também, verificar [isso](https://bugs.archlinux.org), um lugar onde você pode fazer pedidos, caso você os considere importantes.

### Eu acabei de instalar o Pacote X. Como eu o inicio?

Se você está usando um ambiente desktop como [KDE](/index.php/KDE "KDE") ou [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)"), o programa deve ser automaticamente mostrado em seu menu. Se você está tentando executar o programa de um terminal e não mostrar o nome do binário, use:

```
$ pacman -Qlq *nome-pacote* | grep /usr/bin/

```

### Por que há alguma uma única versão de cada biblioteca compartilhada nos repositórios oficiais?

Several distributions, such as Debian, have different versions of shared libraries packaged as different packages: `libfoo1`, `libfoo2`, `libfoo3` and so on. In this way it is possible to have applications compiled against different versions of `libfoo` installed on the same system.

In case of a distribution like Arch, only the latest stable versions of packages are officially supported. By dropping support for outdated software, package maintainers are able to spend more time ensuring that the newest versions work as expected. As soon as a new version of a shared library becomes available from upstream, it is added to the repositories and affected packages are rebuilt to use the new version.

### E se eu executar uma atualização completa do sistema e houver uma atualização para uma biblioteca compartilhada, mas não para os aplicativos que dependem dela?

This scenario should not happen at all. Assuming an application called `foobaz` is in one of the official repositories and builds successfully against a new version of a shared library called `libbaz`, it will be updated along with `libbaz`. If, however, it doesn't build successfully, `foobaz` package will have a versioned dependency (e.g. *libbaz 1.5*), and will be removed by pacman during `libbaz` upgrade, due to a conflict.

If `foobaz` is a package that you built yourself and installed from AUR, you should try rebuilding `foobaz` against the new version of `libbaz`. If the build fails, report the bug to the `foobaz` developers.

### É possível haver uma atualização de versão maior do kernel no repositório e que alguns dos pacotes de driver não tenham sido atualizados?

No, it is not possible. Major kernel updates (e.g. *linux 3.5.0-1* to *linux 3.6.0-1*) are always accompanied by rebuilds of all supported kernel driver packages. On the other hand, if you have an unsupported driver package installed on your system, such as [catalyst](https://aur.archlinux.org/packages/catalyst/), then a kernel update might break things for you if you do not rebuild it for the new kernel. Users are responsible for updating any unsupported driver packages that they have installed.

### O que fazer antes de atualizar?

Follow the [System maintenance#Upgrading the system](/index.php/System_maintenance#Upgrading_the_system "System maintenance") section.

### Uma atualização de pacote foi lançada, mas o pacman diz que o sistema está atualizado

*pacman* mirrors are not synced immediately. It may take over 24 hours before an update is available to you. The only options are be patient or use another mirror. [MirrorStatus](https://www.archlinux.org/mirrors/status/) can help you identify an up-to-date mirror.

### Upstream do projeto *X* lançou uma nova versão. Quanto tempo vai levar para o pacote do Arch ser atualizado para essa nova versão?

Package updates will be released when they are ready. The specifc amount of time can be as short as a few hours after upstream releases a minor bugfix update to as long as several weeks after a large package group's major update. The amount of time from an upstream's new version to Arch releasing a new package depends on the specific packages and the availability of the package maintainers. Additionally, some packages spend some time in the [testing](/index.php/Testing "Testing") repository, so this can prolong the time before a package is updated. [Package maintainers](/index.php/Package_maintainer "Package maintainer") attempt to work quickly to bring stable updates to the repositories. If you find a package in the official repositories that is out of date, go to that package's page at the [package website](https://www.archlinux.org/packages/) and flag it.

## Instalação

### O Arch precisa de um instalador. Talvez um instalador gráfico?

A discussão sobre um "melhor" instalador é uma opinião subjetiva. A melhor maneira de lidar com isso é colocar o instalador no "jeito arch". Se esta opinião sobre um melhor instalador fosse reforçada com mais argumentos concretos, o desenvolvimento adicional do instalador poderia ser levado em conta. *O Windows usa um instalador baseado em texto*.

### Eu instalei o Arch e agora eu estou em um shell! O que faço agora?

See [General recommendations](/index.php/General_recommendations "General recommendations").

### Qual ambiente de área de trabalho ou gerenciador de janelas eu devo usar?

Since many are available to you, use the one you like the most to fit your needs. Have a look at the [Desktop environment](/index.php/Desktop_environment "Desktop environment") and [Window manager](/index.php/Window_manager "Window manager") articles.

### O que faz do Arch único entre outras distribuições "minimalistas"?

See [Arch compared to other distributions](/index.php/Arch_compared_to_other_distributions "Arch compared to other distributions").

## 64 bit

### Como eu determino se meu processador é compatível com x86_64?

If your processor is [x86_64](https://en.wikipedia.org/wiki/X86-64 "wikipedia:X86-64") compatible, you will have the `lm` flag in `/proc/cpuinfo`. For example,

```
$ grep -w lm /proc/cpuinfo

```

Under Windows, using the freeware [CPU-Z](http://www.cpuid.com/cpuz.php) helps determine whether your CPU is 64-bit compatible. CPUs with AMD's instruction set "AMD64" or Intel's solution "EM64T" should be compatible with the x86_64 releases and binary packages.

### Por que 64 bit?

It is faster under most circumstances and as an added bonus also inherently more secure due to the nature of [Address space layout randomization (ASLR)](https://en.wikipedia.org/wiki/Address_space_layout_randomization "wikipedia:Address space layout randomization") in combination with [Position-independent code (PIC)](https://en.wikipedia.org/wiki/Position-independent_code "wikipedia:Position-independent code") and the [NX Bit](https://en.wikipedia.org/wiki/NX_Bit "wikipedia:NX Bit") which is not available in the stock i686 kernel due to disabled PAE. If your computer has more than 4GB of RAM, only a 64-bit OS will be able to fully utilize it.

Programmers also increasingly tend to care less about 32-bit ("legacy") as "new" x86 CPUs typically support the 64-bit extensions.

There are many more reasons we could list here to tell you to avoid 32-bit, but between the kernel, userspace and individual programs it is simply not viable to list every last thing that 64-bit does much better these days.

### Como eu troco de i686 para x86_64 sem reinstalar?

No. All packages need to be reinstalled for the new architecture and configuration changes may be necessary. However, you do not need to repartition or reformat your hard drives during installation, so it is possible to migrate all of your old data. A forum thread has been created [here](https://bbs.archlinux.org/viewtopic.php?id=64485) which outlines steps taken to migrate an install from 32 to 64 bit without losing any configurations/settings/data using a large external hard drive.

However, you can also start the system with the 64-bit installation ISO, mount the disk, backup anything you may want to keep that is not a 32-bit binary (e.g: `/home` & `/etc`), and install.

You may also want to read about [migrating between architectures](/index.php/Migrating_between_architectures "Migrating between architectures").