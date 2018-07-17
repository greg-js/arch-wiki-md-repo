Artigos relacionados

*   [Terminologia do Arch](/index.php/Terminologia_do_Arch "Terminologia do Arch")
*   [Arch User Repository (Português)#FAQ](/index.php/Arch_User_Repository_(Portugu%C3%AAs)#FAQ "Arch User Repository (Português)")
*   [General troubleshooting](/index.php/General_troubleshooting "General troubleshooting")

## Contents

*   [1 Geral](#Geral)
    *   [1.1 O que é o Arch Linux?](#O_que_.C3.A9_o_Arch_Linux.3F)
    *   [1.2 Por que eu não gostaria de usar o Arch?](#Por_que_eu_n.C3.A3o_gostaria_de_usar_o_Arch.3F)
    *   [1.3 A quais arquiteturas o Arch oferece suporte?](#A_quais_arquiteturas_o_Arch_oferece_suporte.3F)
    *   [1.4 O Arch oferece suporte a CPUs ARM?](#O_Arch_oferece_suporte_a_CPUs_ARM.3F)
    *   [1.5 O Arch segue o Filesystem Hierarchy Standard (FHS) da Linux Foundation?](#O_Arch_segue_o_Filesystem_Hierarchy_Standard_.28FHS.29_da_Linux_Foundation.3F)
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
    *   [2.6 Por que há uma única versão de cada biblioteca compartilhada nos repositórios oficiais?](#Por_que_h.C3.A1_uma_.C3.BAnica_vers.C3.A3o_de_cada_biblioteca_compartilhada_nos_reposit.C3.B3rios_oficiais.3F)
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

O Arch só oferece suporte à arquitetura x86_64 (algumas vezes chamada de amd64). Suporte à i686 foi desativado em Novembro de 2017[[1]](http://www.archlinux-br.org/noticias/260/). Se sua máquina ainda usa a versão i686 do Arch, mas uma CPU x86_64, veja [#Como eu troco de i686 para x86_64 sem reinstalar?](#Como_eu_troco_de_i686_para_x86_64_sem_reinstalar.3F). Se sua máquina não possuir suporte, considere trocar para [Arch Linux 32](https://archlinux32.org/).

### O Arch oferece suporte a CPUs ARM?

Não, mas o projeto [Arch Linux ARM](http://archlinuxarm.org/) fornece um *port* do Arch Linux para várias plataformas ARM. Veja [[2]](http://ix.io/73w/irc).

### O Arch segue o Filesystem Hierarchy Standard (FHS) da Linux Foundation?

O Arch Linux segue FHS (em português, *hierarquia de sistema de arquivos*) para sistemas de arquivos usando o gerenciador de serviço [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)"). Veja [file-hierarchy(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/file-hierarchy.7) para uma explicação de cada diretório junto com suas designações. Em especial, `/bin`, `/sbin` e `/usr/sbin` são links simbólicos para `/usr/bin`, e `/lib` e `/lib64` são links simbólicos para `/usr/lib`.

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

Veja o artigo [Manutenção do sistema](/index.php/Manuten%C3%A7%C3%A3o_do_sistema "Manutenção do sistema") para dicas sobre como fazer um sistema Arch o mais estável possível.

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

Veja as páginas [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)"), [pacman/Dicas e truques](/index.php/Pacman/Dicas_e_truques "Pacman/Dicas e truques") e [Repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais") para mais respostas.

### Eu encontrei um erro no pacote X. O que eu devo fazer?

Primeiro, você precisa descobrir se esse erro é algo que a equipe do Arch possa consertar. Algumas vezes não é (aquele travamento no firefox pode ser falha da equipe do Mozilla); isto é chamado de *upstream error* ("erro do upstream"). Se for um problema do Arch, existe uma série de coisas que você pode fazer:

1.  Procurar informações no fórum. Veja se alguém teve o mesmo problema.
2.  Fazer um [relatório de erro](/index.php/Diretrizes_de_relat%C3%B3rios_de_erro "Diretrizes de relatórios de erro"), com informações detalhadas, em [https://bugs.archlinux.org](https://bugs.archlinux.org)
3.  Se desejar, você pode criar um tópico no fórum descrevendo o problema e informando que você já relatou o mesmo. Isto ajuda a prevenir que várias pessoas relatem o mesmo erro.

### Os pacotes do Arch precisam usar uma nomenclatura única. ".pkg.tar.gz" e "pkg.tar.xz" é muito longo e/ou confuso

Isto foi discutido na lista de discussão do Arch. Alguns propuseram uma extensão de arquivo *.pac*, mas não há nenhum plano para modificar a extensão de pacote. Como Tobias Kieslich, um dos desenvolvedores do Arch, colocou, "Um pacote **é** tarball gzipado em *[xz]*!! E ele pode ser aberto, verificado e manipulado por qualquer aplicação tar. Além disso, o tipo mime é automaticamente detectado pela maioria dos aplicativos".

### O pacman precisa de uma biblioteca para que outros aplicativos possam acessar facilmente informações dos pacotes

Pacman é um front-end para [libalpm](https://www.archlinux.org/pacman/libalpm.3.html), acrônimo para *"Arch Linux Package Management"* ("Gerenciamento de Pacote do Arch Linux"), que permite front-ends alternativos, como um front-end gráfico, serem escritos.

### O pacman precisa do recurso X!

Se você acha que sua ideia tem fundamento, então você pode discuti-la na [pacman-dev](https://lists.archlinux.org/listinfo/pacman-dev/). Verifique também [https://bugs.archlinux.org](https://bugs.archlinux.org) por requisições existentes por recursos.

Porém, a melhor forma de ter um recurso adicionado ao pacman ou Arch Linux é implementá-lo você mesmo. O patch ou código pode ou não ser aceito oficialmente, mas talvez outros vão apreciar, testar e contribuir para seu esforço.

### Eu acabei de instalar o Pacote X. Como eu o inicio?

Se você está usando um ambiente desktop como [KDE](/index.php/KDE "KDE") ou [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)"), o programa deve ser automaticamente mostrado em seu menu. Se você está tentando executar o programa de um terminal e não mostrar o nome do binário, use:

```
$ pacman -Qlq *nome-pacote* | grep /usr/bin/

```

### Por que há uma única versão de cada biblioteca compartilhada nos repositórios oficiais?

Diversas distribuições, como o Debian, possuem diferentes versões de bibliotecas compartilhadas empacotadas como pacotes diferentes: `libfoo1`, `libfoo2`, `libfoo3` e por aí vai. Nesta forma, é possível ter aplicativos compilados com diferentes versões de `libfoo` instaladas no mesmo sistema.

No caso de uma distribuição como o Arch, apenas as últimas versões estáveis recebem suporte oficial. Ao descartar suporte a um software desatualizado, mantenedores de pacote conseguem gastar mais tempo assegurando que as versões mais novas funcionam conforme esperado. Assim que uma nova versão de uma biblioteca compartilhada é disponibilizada pelo upstream, ela é adicionada aos repositórios e pacotes afetados são recompilados para usar a nova versão.

### E se eu executar uma atualização completa do sistema e houver uma atualização para uma biblioteca compartilhada, mas não para os aplicativos que dependem dela?

Esse cenário não deve acontecer. Presumindo que um aplicativo chamado `foobaz` está em um dos repositórios oficiais e compila com sucesso com a nova versão da biblioteca compartilhada chamada `libbaz`, ele será atualizado junto com `libbaz`. Se, porém, ele não compilar com sucesso, o pacote `foobaz` terá uma dependência versionada (p.ex.: *libbaz 1.5*) e será removido pelo pacman durante a atualização de `libbaz`, por causa de um conflito.

Se `foobaz` é um pacote que você mesmo compilou e instalou do AUR, você deve tentar recompilar `foobaz` com a nova versão de `libbaz`. Se a compilação falhar, relate o erro aos desenvolvedores do `foobaz`.

### É possível haver uma atualização de versão maior do kernel no repositório e que alguns dos pacotes de driver não tenham sido atualizados?

Não, não é possível. Atualizações de versões maiores do kernel (p.ex. *linux 3.5.0-1* para *linux 3.6.0-1*) são sempre acompanhadas por recompilações de todos os pacotes de drivers de kernel. Por outro lado, se você tiver um pacote de driver sem suporte em seu sistema, tal como [catalyst](https://aur.archlinux.org/packages/catalyst/), então a atualização de kernel pode quebrar coisas se você não recompilá-lo para o novo kernel. Os usuários são responsáveis por atualizar quaisquer pacotes de driver sem suporte que eles tenham instalado.

### O que fazer antes de atualizar?

Siga a seção [Manutenção do sistema#Atualizando o sistema](/index.php/Manuten%C3%A7%C3%A3o_do_sistema#Atualizando_o_sistema "Manutenção do sistema").

### Uma atualização de pacote foi lançada, mas o pacman diz que o sistema está atualizado

Mirrors do *pacman* não são sincronizados imediatamente. Leva cerca de 24 horas antes que uma atualização esteja disponível para você. As únicas opções são ser paciente ou usar um outro mirror. [MirrorStatus](https://www.archlinux.org/mirrors/status/) pode lhe ajudar a identificar um mirror atualizado.

### Upstream do projeto *X* lançou uma nova versão. Quanto tempo vai levar para o pacote do Arch ser atualizado para essa nova versão?

Atualizações de pacotes serão lançadas quando elas estiverem prontas. A quantidade específica de tempo pode ser tão curta quanto algumas horas após o upstream lançar uma atualização menor de correção de erros e tão longa quanto várias semanas após a atualização de versão maior de um grupo grande de pacotes. A quantidade de tempo de uma nova versão do upstream até o Arch lançar um novo pacote depende dos pacotes específicos e da disponibilidade dos mantenedores de pacote. Adicionalmente, alguns pacotes ficam algum tempo no repositório [testing](/index.php/Testing_(Portugu%C3%AAs) "Testing (Português)"), então isso pode prolongar o tempo antes de um pacote ser atualizado. Cada [mantenedor de pacote](/index.php/Mantenedor_de_pacote "Mantenedor de pacote") tenta trabalhar rapidamente para trazer atualizações estáveis para os repositórios. Se você encontrar um pacote nos repositórios oficiais que está desatualizado, vá até a página do pacote no [site de pacotes](https://www.archlinux.org/packages/) e sinalize-o como tal.

## Instalação

### O Arch precisa de um instalador. Talvez um instalador gráfico?

Já que a instalação não ocorre com frequência (leia o resto deste artigo para saber mais sobre lançamento contínuo - *rolling release*), isso não é uma prioridade alta para os desenvolvedores ou usuários. O [Guia de instalação](/index.php/Guia_de_instala%C3%A7%C3%A3o "Guia de instalação") foi completamente atualizado para usar o método de linha de comando.

### Eu instalei o Arch e agora eu estou em um shell! O que faço agora?

Veja [Recomendações gerais](/index.php/Recomenda%C3%A7%C3%B5es_gerais "Recomendações gerais").

### Qual ambiente de área de trabalho ou gerenciador de janelas eu devo usar?

Já que há muitos disponíveis para você, use o que você preferir para atender suas necessidades. Dê uma olhada nos artigos [Ambiente de desktop](/index.php/Ambiente_de_desktop "Ambiente de desktop") e [Gerenciador de janela](/index.php/Gerenciador_de_janela "Gerenciador de janela").

### O que faz do Arch único entre outras distribuições "minimalistas"?

Veja [Arch em comparação com outras distribuições](/index.php/Arch_em_compara%C3%A7%C3%A3o_com_outras_distribui%C3%A7%C3%B5es "Arch em comparação com outras distribuições").

## 64 bit

### Como eu determino se meu processador é compatível com x86_64?

Se seu processador é compatível com [x86_64](https://en.wikipedia.org/wiki/X86-64 "wikipedia:X86-64"), você terá a flag `lm` ([*l*ong *m*ode](https://en.wikipedia.org/wiki/Long_mode "wikipedia:Long mode")) no `/proc/cpuinfo`. Por exemplo,

```
$ grep -w lm /proc/cpuinfo

```

No Windows, usar o freeware [CPU-Z](http://www.cpuid.com/cpuz.php) ajuda a determinar se seu CPU é compatível com 64-bit. CPUs com conjunto de instruções da AMD "AMD64" ou a solução da Intel "EM64T" devem ser compatíveis com os pacotes binários e lançamentos de x86_64.

### Por que 64 bit?

É mais rápido sob a maioria das circunstâncias e, como um bônus adicional, também mais seguro em razão da natureza de [Aleatorização do layout de espaço do endereço (ASLR)](https://en.wikipedia.org/wiki/Address_space_layout_randomization "wikipedia:Address space layout randomization") em combinação com [Código independente de posição (PIC)](https://en.wikipedia.org/wiki/Position-independent_code "wikipedia:Position-independent code") e [Bit NX](https://en.wikipedia.org/wiki/pt:Bit_NX "wikipedia:pt:Bit NX") que não está disponível em kernels padrão de i686 por causa do PAE desabilitado. Se seu computador tem mais de 4GB de RAM, somente um SO 64 bits será capaz de usá-lo totalmente.

Os programadores também têm se preocupado cada vez menos em relação a 32 bits ("legado"), pois as "novas" CPUs x86 geralmente oferecem suporte às extensões de 64 bits.

Há muitas outras razões que podemos listar aqui para dizer-lhe para evitar 32 bits, mas entre o kernel, o espaço de usuários e os programas individuais, simplesmente não é viável listar todas as últimas coisas que o 64 bits faz muito melhor nos dias de hoje.

### Como eu troco de i686 para x86_64 sem reinstalar?

Não. Todos os pacotes precisam ser reinstalados para uma nova arquitetura e alterações de configuração podem ser necessários. Porém, você não precisa reparticionar seus discos rígidos durante a instalação, de forma que é possível migrar todos os seus dados antigos. Um tópico de fórum foi criado [aqui](https://bbs.archlinux.org/viewtopic.php?id=64485) que delineia os passos feitos para migrar uma instalação de 32 para 64 bits sem perder quaisquer configurações/definições/dados usando um disco rígido grande e externo.

Porém, você também pode iniciar o sistema com a ISO de instalação de 64 bits, montagem do disco, cópia de segurança de qualquer coisa que você deseje manter que não seja um binário de 32 bits (p.ex.: `/home` & `/etc`) e instalar.

Você também pode querer ler sobre [migração entre arquiteturas](/index.php/Migrating_between_architectures "Migrating between architectures").