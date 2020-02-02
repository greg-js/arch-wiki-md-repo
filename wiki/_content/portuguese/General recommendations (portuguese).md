**Status de tradução:** Esse artigo é uma tradução de [General recommendations](/index.php/General_recommendations "General recommendations"). Data da última tradução: 2019-12-05\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=General_recommendations&diff=0&oldid=589275) na versão em inglês.

Artigos relacionados

*   [Perguntas frequentes](/index.php/Perguntas_frequentes "Perguntas frequentes")
*   [Guia de instalação](/index.php/Guia_de_instala%C3%A7%C3%A3o "Guia de instalação")
*   [Lista de aplicativos](/index.php/List_of_applications "List of applications")

Esse documento é um índice anotado de artigos populares e informações importantes para melhorar e adicionar funcionalidades ao sistema Arch instalado. Presume-se aqui que os leitores leram e seguiram o [Guia de instalação](/index.php/Guia_de_instala%C3%A7%C3%A3o "Guia de instalação") para obter uma instalação básica do Arch Linux. Ter lido e entendido os conceitos explicados em [#Administração do sistema](#Administração_do_sistema) e [#Gerenciamento de pacote](#Gerenciamento_de_pacote) é *obrigatório* para seguir as outras seções desta página e outros artigos no wiki.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Administração do sistema](#Administração_do_sistema)
    *   [1.1 Usuários e grupos](#Usuários_e_grupos)
    *   [1.2 Elevação de privilégios](#Elevação_de_privilégios)
    *   [1.3 Gerenciamento de serviço](#Gerenciamento_de_serviço)
    *   [1.4 Manutenção de sistema](#Manutenção_de_sistema)
*   [2 Gerenciamento de pacote](#Gerenciamento_de_pacote)
    *   [2.1 pacman](#pacman)
    *   [2.2 Repositórios](#Repositórios)
    *   [2.3 Espelhos](#Espelhos)
    *   [2.4 Arch Build System](#Arch_Build_System)
    *   [2.5 Arch User Repository](#Arch_User_Repository)
*   [3 Inicialização](#Inicialização)
    *   [3.1 Autorreconhecimento de hardware](#Autorreconhecimento_de_hardware)
    *   [3.2 Microcódigo](#Microcódigo)
    *   [3.3 Retendo mensagens de inicialização](#Retendo_mensagens_de_inicialização)
    *   [3.4 Ativação de Num Lock](#Ativação_de_Num_Lock)
*   [4 Interface gráfica de usuário](#Interface_gráfica_de_usuário)
    *   [4.1 Servidor de exibição](#Servidor_de_exibição)
    *   [4.2 Drivers de exibição](#Drivers_de_exibição)
    *   [4.3 Ambientes gráficos](#Ambientes_gráficos)
    *   [4.4 Gerenciadores de janela](#Gerenciadores_de_janela)
    *   [4.5 Diretórios de usuário](#Diretórios_de_usuário)
    *   [4.6 Gerenciadores de exibição](#Gerenciadores_de_exibição)
*   [5 Gerenciamento de energia](#Gerenciamento_de_energia)
    *   [5.1 Eventos de ACPI](#Eventos_de_ACPI)
    *   [5.2 Escala de frequência de CPU](#Escala_de_frequência_de_CPU)
    *   [5.3 Laptops](#Laptops)
    *   [5.4 Suspensão e hibernação](#Suspensão_e_hibernação)
*   [6 Multimídia](#Multimídia)
    *   [6.1 Som](#Som)
    *   [6.2 Plugins de navegadores](#Plugins_de_navegadores)
    *   [6.3 Codecs](#Codecs)
*   [7 Conectividade](#Conectividade)
    *   [7.1 Sincronização de relógio](#Sincronização_de_relógio)
    *   [7.2 Segurança de DNS](#Segurança_de_DNS)
    *   [7.3 Configuração de um firewall](#Configuração_de_um_firewall)
    *   [7.4 Compartilhamento de recurso](#Compartilhamento_de_recurso)
*   [8 Dispositivos de entrada](#Dispositivos_de_entrada)
    *   [8.1 Layouts de teclado](#Layouts_de_teclado)
    *   [8.2 Botões de mouse](#Botões_de_mouse)
    *   [8.3 Touchpads de laptop](#Touchpads_de_laptop)
    *   [8.4 TrackPoints](#TrackPoints)
*   [9 Otimizações](#Otimizações)
    *   [9.1 Benchmarking](#Benchmarking)
    *   [9.2 Melhorando o desempenho](#Melhorando_o_desempenho)
    *   [9.3 Solid state drives](#Solid_state_drives)
*   [10 Serviço de sistema](#Serviço_de_sistema)
    *   [10.1 Índice e pesquisa por arquivo](#Índice_e_pesquisa_por_arquivo)
    *   [10.2 Entrega local de correio](#Entrega_local_de_correio)
    *   [10.3 Impressão](#Impressão)
*   [11 Aparência](#Aparência)
    *   [11.1 Fontes](#Fontes)
    *   [11.2 Temas GTK e Qt](#Temas_GTK_e_Qt)
*   [12 Melhorias no console](#Melhorias_no_console)
    *   [12.1 Melhorias na completação por Tab](#Melhorias_na_completação_por_Tab)
    *   [12.2 Aliases](#Aliases)
    *   [12.3 Shells alternativos](#Shells_alternativos)
    *   [12.4 Adições ao Bash](#Adições_ao_Bash)
    *   [12.5 Saída colorida](#Saída_colorida)
    *   [12.6 Arquivos compactados](#Arquivos_compactados)
    *   [12.7 Prompt de console](#Prompt_de_console)
    *   [12.8 Shell do emacs](#Shell_do_emacs)
    *   [12.9 Suporte a mouse](#Suporte_a_mouse)
    *   [12.10 Buffer de scrollback](#Buffer_de_scrollback)
    *   [12.11 Gerenciamento de sessão](#Gerenciamento_de_sessão)

## Administração do sistema

Essa seção lida com tarefas administrativas e gerenciamento do sistema. Para mais, por favor veja [Utilitários principais](/index.php/Utilit%C3%A1rios_principais "Utilitários principais") e [Category:System administration (Português)](/index.php/Category:System_administration_(Portugu%C3%AAs) "Category:System administration (Português)").

### Usuários e grupos

Uma nova instalação deixa você com apenas a conta de [superusuário](https://en.wikipedia.org/wiki/Superuser em um servidor, [é inseguro](https://apple.stackexchange.com/questions/192365/is-it-ok-to-use-the-root-user-as-a-normal-user/192422#192422). Em vez disso, você deve criar e usar uma conta de usuário desprivilegiada para a maioria das tarefas, apenas usando a conta root para administração do sistema. Veja [Usuários e grupos#Gerenciamento de usuário](/index.php/Usu%C3%A1rios_e_grupos#Gerenciamento_de_usuário "Usuários e grupos") para detalhes.

Usuários e grupos são mecanismo para *controle de acesso*; administradores podem ajustar participação e posse de grupos para conceder ou negar a usuários e serviços acesso a recursos do sistema. Leia o artigo [Usuários e grupos](/index.php/Usu%C3%A1rios_e_grupos "Usuários e grupos") para detalhes e riscos de segurança em potencial.

### Elevação de privilégios

Os comandos [su](/index.php/Su "Su") e [sudo](/index.php/Sudo "Sudo") permitem que você execute comandos como outro usuário. Por padrão, *su* inicia um shell interativo como o usuário root e *sudo*, por padrão, temporariamente lhe concede privilégios para um único comando. Veja seus respectivos artigos para diferenças.

### Gerenciamento de serviço

Arch Linux usa [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") como o processo [init](/index.php/Init "Init"), que é um gerenciador de sistema e serviço para Linux. Para dar manutenção em sua instalação do Arch Linux, é uma boa ideia aprender os básicos sobre ele. Interação com o *systemd* é feita com o comando *systemctl*. Leia o [systemd (Português)#Uso básico do systemctl](/index.php/Systemd_(Portugu%C3%AAs)#Uso_básico_do_systemctl "Systemd (Português)") para mais informações.

### Manutenção de sistema

Arch é um sistema *rolling release* e tem uma mudança rápida de pacote, então usuários levam algum tempo para fazer [manutenção do sistema](/index.php/Manuten%C3%A7%C3%A3o_do_sistema "Manutenção do sistema"). Leia [Segurança](/index.php/Security "Security") para recomendações e boas párticas de *hardening* do sistema.

## Gerenciamento de pacote

Essa seção contém informações úteis relacionadas ao gerenciamento de pacote. Para mais, por favor veja [Perguntas frequentes#Gerenciamento de pacote](/index.php/Perguntas_frequentes#Gerenciamento_de_pacote "Perguntas frequentes") e [Category:Package management (Português)](/index.php/Category:Package_management_(Portugu%C3%AAs) "Category:Package management (Português)").

**Nota:** É imprescindível se manter atualizado com as alterações no Arch Linux que exigem intervenção manual *antes* de atualizar seu sistema. Inscreva-se na [lista de discussão arch-announce](https://mailman.archlinux.org/mailman/listinfo/arch-announce/) ou no [feed RSS de notícias recentes](https://www.archlinux.org/feeds/news/). Alternativamente, confira as [notícias do Arch](https://www.archlinux.org/) na página inicial toda vez antes de atualizar.

### pacman

[pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)"), uma abreviação de **pac**kage **man**ager, é o gerenciador de pacotes do Arch Linux: todos os usuários devem se familiarizar com ele antes de ler qualquer outro artigo.

Veja [pacman/Dicas e truques](/index.php/Pacman/Dicas_e_truques "Pacman/Dicas e truques") para sugestões sobre como melhorar sua interação com *pacman* e o gerenciamento de pacotes em geral.

### Repositórios

Veja o artigo [Repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais") para detalhes sobre o propósito de cada repositório oficialmente mantido.

Se você planeja usar aplicativos 32 bits, você vai querer habilitar o repositório [multilib](/index.php/Multilib_(Portugu%C3%AAs) "Multilib (Português)").

O artigo [Repositórios extraoficiais de usuário](/index.php/Unofficial_user_repositories "Unofficial user repositories") lista diversos outros repositórios sem suporte.

Considere instalar o serviço [pkgstats](/index.php/Pkgstats_(Portugu%C3%AAs) "Pkgstats (Português)").

### Espelhos

Por vezes chamados de "espelhos" *(mirrors)*. Visite o artigo [Espelhos](/index.php/Espelhos "Espelhos") para etapas para se beneficiar do uso de espelhos mais rápidos e mais atualizados dos repositórios oficiais. Como explicado no artigo, um conselho particularmente bom é verificar periodicamente a página [Mirror Status](https://www.archlinux.org/mirrors/status/) por uma lista de espelhos que foram sincronizados recentemente.

### Arch Build System

*Ports* é um sistema inicialmente usado pelas distribuições BSD consistindo em scripts de compilação que residem em uma árvore de diretório no sistema local. Basicamente, cada *port* contém um script dentro de um diretório intuitivamente nomeado pelo aplicativo terceiro instalável.

O [Arch Build System](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)") oferece a mesma funcionalidade para fornecer scripts de compilação chamados [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)"), que são populados com informações para uma dada peça de software: *hashes* de integridade, instruções de compilação e licença, versão e URL do projeto. Esses PKGBUILDs são analisados pelo [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)"), o programa atual que gera pacotes que são gerenciáveis de forma limpa pelo *pacman*.

Todo pacote nos repositórios junto com aqueles presentes no AUR estão sujeitos a recompilação com *makepkg*.

### Arch User Repository

Enquanto o Arch Build System permite a capacidade de compilar softwares disponíveis nos repositórios oficiais, o [Arch User Repository](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)") (AUR) é o equivalente a pacotes enviados por usuários. É um repositório sem suporte de scripts de compilação acessíveis por meio da [interface web](https://aur.archlinux.org/) ou pela [interface RPC do Aurweb](/index.php/Interface_RPC_do_Aurweb "Interface RPC do Aurweb").

## Inicialização

Essa seção contém informações pertinentes ao processo de inicialização (*boot*). Uma visão geral do processo de inicialização do Arch pode ser localizado em [Processo de inicialização do Arch](/index.php/Arch_boot_process "Arch boot process"). Para mais, veja [Category:Boot process (Português)](/index.php/Category:Boot_process_(Portugu%C3%AAs) "Category:Boot process (Português)").

### Autorreconhecimento de hardware

Hardware deve ser detectado automaticamente pelo [udev](/index.php/Udev "Udev") durante o processo de inicialização por padrão. Uma melhoria potencial no tempo de inicialização pode ser atingido pela desabilitação de carregamento automático de módulos e especificação manual dos módulos necessários, como descrito em [Módulos de kernel](/index.php/Kernel_module_(Portugu%C3%AAs) "Kernel module (Português)"). Além disso, [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)") deve ser capaz de detectar automaticamente drivers drivers necessários usando `udev`, mas os usuários também têm a opção de configurar o servidor X manualmente.

### Microcódigo

Processadores podem ter [comportamento falho](https://www.anandtech.com/show/8376/intel-disables-tsx-instructions-erratum-found-in-haswell-haswelleep-broadwelly), o que o kernel pode corrigir atualizando o *microcódigo* na inicialização. Veja [Microcódigo](/index.php/Microcode "Microcode") para detalhes.

### Retendo mensagens de inicialização

Uma vez concluído, a tela será apagada e e o prompt de login aparecerá, deixando os usuários incapaz de obter feedback sobre o processo de inicialização. [Desativar o apagamento de mensagens de inicialização](/index.php/Disable_clearing_of_boot_messages "Disable clearing of boot messages") é a solução para passar por cima dessa limitação.

### Ativação de Num Lock

[Num Lock](https://en.wikipedia.org/wiki/pt:Num_Lock "wikipedia:pt:Num Lock") é uma tecla de ativar/desativar localizada na maioria dos teclados. Para ativar a atribuição de tecla numérica do Num Lock durante a inicialização, veja [Ativando numlock na inicialização](/index.php/Ativando_numlock_na_inicializa%C3%A7%C3%A3o "Ativando numlock na inicialização").

## Interface gráfica de usuário

Essa seção fornece orientação para usuários interessados em usar aplicativos gráficos em seu sistema. Veja [Category:Graphical user interfaces (Português)](/index.php/Category:Graphical_user_interfaces_(Portugu%C3%AAs) "Category:Graphical user interfaces (Português)") para recursos adicionais.

### Servidor de exibição

[Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)") é a implementação código aberto e pública do [X Window System](https://en.wikipedia.org/wiki/pt:X_Window_System "wikipedia:pt:X Window System") (mais conhecido como *X11* ou *X*). Ele é necessário para se usar aplicativos com interfaces gráficas de usuário (também conhecidas como *GUI*s) e a maioria dos usuários terão interesse em instalá-los.

[Wayland](/index.php/Wayland_(Portugu%C3%AAs) "Wayland (Português)") é um protocolo alternativo mais novo de servidor de exibição e a implementação referência de Weston está disponível.

### Drivers de exibição

O driver de vídeo *vesa* padrão vai funcionar com a maioria das placas de vídeo, porém o desempenho pode ser drasticamente melhorado e recursos adicionais aproveitados instalando o driver apropriado para produtos [AMD](/index.php/Xorg_(Portugu%C3%AAs)#AMD "Xorg (Português)"), [Intel](/index.php/Intel_(Portugu%C3%AAs) "Intel (Português)") ou [NVIDIA](/index.php/NVIDIA "NVIDIA").

### Ambientes gráficos

Apesar do Xorg fornecer um framework básico para compilação de um ambiente gráfico, componentes adicionais podem ser considerados necessários para uma experiência de usuário completa. [Ambientes de desktop](/index.php/Ambientes_de_desktop "Ambientes de desktop") como o [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)"), [KDE](/index.php/KDE_(Portugu%C3%AAs) "KDE (Português)"), [LXDE](/index.php/LXDE "LXDE") e [Xfce](/index.php/Xfce_(Portugu%C3%AAs) "Xfce (Português)") colecionam uma gama de *clientes X*, tal como um gerenciador de janelas, painel, gerenciador de arquivos, emulador de terminal, editor de texto, ícones e outros utilitários. Usuários com menos experiência podem preferir instalar um ambiente gráfico para ter um ambiente mais familiar. Veja [Category:Desktop environments (Português)](/index.php/Category:Desktop_environments_(Portugu%C3%AAs) "Category:Desktop environments (Português)") para recursos adicionais.

### Gerenciadores de janela

Um ambiente gráfico completo fornece uma interface gráfica de usuário completa e consistente, mas tende a representar um consumo considerável dos recursos do sistema. Usuários buscando maximizar o desempenho ou simplificar seu ambiente, podem optar por instalar um [gerenciador de janela](/index.php/Gerenciador_de_janela "Gerenciador de janela") sozinho e selecionar pessoalmente os extras desejados. A maioria dos ambientes gráficos também permitem o uso de um gerenciador de janela alternativo. Os gerenciadores de janela [dinâmicos](/index.php/Category:Dynamic_WMs "Category:Dynamic WMs"), [empilhamento](/index.php/Category:Stacking_WMs "Category:Stacking WMs") e [tiling](/index.php/Category:Tiling_WMs "Category:Tiling WMs") se diferem na forma de lidar com posicionamento das janelas.

### Diretórios de usuário

Os diretórios de usuário conhecidos, como Downloads ou Música, são criados pelo serviço do usuário `xdg-user-dirs-update.service`, fornecido por [xdg-user-dirs](https://www.archlinux.org/packages/?name=xdg-user-dirs) e ativado por padrão após a instalação. Se o seu ambiente de desktop ou gerenciador de janelas não puxar o pacote, você pode [instalar](/index.php/Instalar "Instalar") e executar `xdg-user-dirs-update` manualmente conforme [Diretórios de usuário XDG#Criando diretórios padrão](/index.php/Diret%C3%B3rios_de_usu%C3%A1rio_XDG#Criando_diretórios_padrão "Diretórios de usuário XDG").

### Gerenciadores de exibição

A maioria dos ambientes gráficos incluem um [gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição") para iniciar automaticamente o ambiente gráfico e gerenciar autenticação de usuário. Usuários sem um ambiente gráfico podem instalar um separadamente. Alternativamente, você pode [iniciar X no login](/index.php/Iniciar_X_no_login "Iniciar X no login") como uma alternativa simples a um gerenciador de exibição.

## Gerenciamento de energia

Essa seção pode ser usada por donos de laptop ou usuários que busquem controles de gerenciamento de energia. Para mais, por favor veja [Category:Power management](/index.php/Category:Power_management "Category:Power management").

Veja [Gerenciamento de energia](/index.php/Power_management "Power management") para uma visão geral.

### Eventos de ACPI

Usuários podem configurar como o sistema reage a eventos de ACPI tal como pressionamento de botão de energia ou fechamento da tampa do laptop. Para novo (recomendado) método usando [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)"), veja [Gerenciamento de energia com systemd](/index.php/Power_management#Power_management_with_systemd "Power management"). Para o método antigo, veja [acpid](/index.php/Acpid "Acpid").

### Escala de frequência de CPU

Processadores modernos pode reduzir sua frequência e voltagem para reduzir a temperatura e consumo de energia. Menos calor leva a um sistema mais silencioso e prolonga a vida útil do hardware. Veja [Escala de frequência do CPU](/index.php/Escala_de_frequ%C3%AAncia_do_CPU "Escala de frequência do CPU") para detalhes.

### Laptops

Para artigos relacionados computação portátil, junto com guias de instalação a modelos específicos, por favor veja [Category:Laptops](/index.php/Category:Laptops "Category:Laptops"). Para uma visão geral de artigos e recomendações relacionadas, veja [Laptop](/index.php/Laptop "Laptop").

### Suspensão e hibernação

Veja o artigo principal: [Power management#Suspend and hibernate](/index.php/Power_management#Suspend_and_hibernate "Power management").

## Multimídia

[Category:Multimedia](/index.php/Category:Multimedia "Category:Multimedia") inclui recursos adicionais.

### Som

[Som](/index.php/Som "Som") é fornecido pelos drivers de som do kernel:

*   [ALSA](/index.php/ALSA_(Portugu%C3%AAs) "ALSA (Português)") é incluído com o kernel e é recomendado porque geralmente ele funciona sem precisar de configuração (só precisa [retirar do mudo](/index.php/Advanced_Linux_Sound_Architecture#Unmuting_the_channels "Advanced Linux Sound Architecture")).

*   [OSS](/index.php/OSS "OSS") é uma alternativa viável no caso de ALSA não funcionar.

Usuários também podem querer instalar e configurar um [servidor de som](/index.php/Som#Servidores_de_som "Som") tal como [PulseAudio](/index.php/PulseAudio_(Portugu%C3%AAs) "PulseAudio (Português)"). Para requisitos de áudio avançados, veja [áudio profissional](/index.php/Professional_audio "Professional audio").

### Plugins de navegadores

Para acesso a certos conteúdos da web, [plugins de navegador](/index.php/Browser_plugins "Browser plugins") tal como Adobe Acrobat Reader, Adobe Flash Player e Java podem ser instalados.

### Codecs

[Codecs](/index.php/Codecs "Codecs") são utilizados por aplicativos de multimídia paracodificar ou decodificar *stremas* de áudio e vídeo. Para reproduzir *streams* codificados, usuários devem se assegurar de que um codec apropriado está instalado.

## Conectividade

Essa seção está confinada a pequenos procedimentos de conectividade. Siga para [Configuração de rede](/index.php/Configura%C3%A7%C3%A3o_de_rede "Configuração de rede") para um guia completo. Para mais, por favor veja [Category:Networking (Português)](/index.php/Category:Networking_(Portugu%C3%AAs) "Category:Networking (Português)").

### Sincronização de relógio

O [Network Time Protocol](https://en.wikipedia.org/wiki/Network_Time_Protocol "wikipedia:Network Time Protocol") (NTP) é um protocolo para sincronizar os relógios de sistemas de computador em redes de dados de latência variável com comutação de pacotes. Veja [Time synchronization](/index.php/Time_synchronization "Time synchronization") para implementações de tal protocolo.

### Segurança de DNS

Para melhor segurança ao navegar na web, jogar na internet, conectar a serviços [SSH](/index.php/SSH_(Portugu%C3%AAs) "SSH (Português)") e tarefas similares, considere usar um [resolvedor de DNS](/index.php/Resolvedor_de_DNS "Resolvedor de DNS") habilitado para [DNSSEC](/index.php/DNSSEC_(Portugu%C3%AAs) "DNSSEC (Português)") que pode validar registros [DNS](https://en.wikipedia.org/wiki/Domain_Name_System e um protocolo criptografado como [DNS sobre TLS](https://en.wikipedia.org/wiki/DNS_over_TLS "wikipedia:DNS over TLS"), [DNS sobre HTTPS](https://en.wikipedia.org/wiki/DNS_over_HTTPS "wikipedia:DNS over HTTPS") ou [DNSCrypt](https://en.wikipedia.org/wiki/DNSCrypt "wikipedia:DNSCrypt"). Veja [Resolução de nome de domínio](/index.php/Resolu%C3%A7%C3%A3o_de_nome_de_dom%C3%ADnio "Resolução de nome de domínio") para detalhes.

### Configuração de um firewall

Um [firewall](/index.php/Firewall "Firewall") pode fornecer uma camada extra de proteção sobre a pilha de rede do Linux. O kernel padrão do Arch é capaz de usar [iptables](/index.php/Iptables "Iptables") do [Netfilter](https://en.wikipedia.org/wiki/Netfilter "wikipedia:Netfilter") e [nftables](/index.php/Nftables "Nftables"), apesar de não estarem habilitados por padrão. É altamente recomendado para configurar alguma forma de firewall. Veja [Category:Firewalls](/index.php/Category:Firewalls "Category:Firewalls") para os guias disponíveis.

### Compartilhamento de recurso

Para compartilhar arquivos entre máquinas em uma rede, siga o artigo [NFS](/index.php/NFS "NFS") ou o [SSHFS](/index.php/SSHFS "SSHFS").

Use [Samba](/index.php/Samba "Samba") para entrar em uma rede Windows. Para configurar a máquina para usar Active Directory para autenticação, leia [Active Directory integration](/index.php/Active_Directory_integration "Active Directory integration").

Veja também [Category:Network sharing](/index.php/Category:Network_sharing "Category:Network sharing").

## Dispositivos de entrada

Esse seção contém dicas de configuração de dispositivo de entrada popular. Para mais, por favor veja [Category:Input devices](/index.php/Category:Input_devices "Category:Input devices").

### Layouts de teclado

Teclados não-americanos ou fora de padrão podem não funcionar como esperado por padrão. Os passos necessários para configurar o mapa de teclas sãos diferentes para console virtual e [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)"), eles são descritos em [Configuração de teclado no console](/index.php/Configura%C3%A7%C3%A3o_de_teclado_no_console "Configuração de teclado no console") e [Configuração de teclado no Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg"), respectivamente.

### Botões de mouse

Proprietários de mouses avançados ou incomuns podem descobrir que nem todos os botões do mouse são reconhecidos por padrão, ou podem querer atribuir ações diferentes para botões extras. Instruções podem ser localizadas em [Todos botões do mouse funcionando](/index.php/All_Mouse_Buttons_Working "All Mouse Buttons Working").

### Touchpads de laptop

Muitos laptops usam dispositivos de ponteiro "touchpad" [Synaptics](https://www.synaptics.com/) ou [ALPS](https://www.alps.com/). Para esses e vários outros modelos de touchpad você pode usar o driver de entrada do Synaptics ou do libinput; veja [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") ou [libinput](/index.php/Libinput "Libinput") para detalhes de instalação e configuração.

### TrackPoints

Veja o artigo [TrackPoint](/index.php/TrackPoint "TrackPoint") para configurar seu dispositivo TrackPoint.

## Otimizações

Essa seção visa resumir ajustes, ferramentas e opções disponíveis úteis para melhorar o desempenho do sistema e de aplicativos.

### Benchmarking

[Benchmarking](/index.php/Benchmarking "Benchmarking") é o ato de medir o desemepho e comparar os resultados ou um padrão amplamente aceito por meio de um procedimento unificado.

### Melhorando o desempenho

O artigo [Melhorando o desempenho](/index.php/Melhorando_o_desempenho "Melhorando o desempenho") junta informações e é resumo básico sobre ganho de desempenho no Arch Linux.

### Solid state drives

O artigo [Solid State Drives](/index.php/Solid_State_Drives "Solid State Drives") cobre muitos aspectos de *solid state drives*, também conhecidos como "unidades de estado sólido", incluindo configurá-los para maximizar seu tempo de vida.

## Serviço de sistema

Essa seção está relacionada a [daemons](/index.php/Daemons_(Portugu%C3%AAs) "Daemons (Português)"). Para mais, consulta [Category:Daemons (Português)](/index.php/Category:Daemons_(Portugu%C3%AAs) "Category:Daemons (Português)").

### Índice e pesquisa por arquivo

A maioria das distribuições possuem um comando `locate` disponível para possibilitar uma pesquisa rápida por arquivos. Para obter essa funcionalidade no Arch Linux, [mlocate](https://www.archlinux.org/packages/?name=mlocate) é a instalação recomendável. Após tê-lo instalado, você deve executar `updatedb` para indexar os sistemas de arquivos.

[Mecanismos de pesquisa](/index.php/List_of_applications/Utilities#File_searching "List of applications/Utilities") fornecem um serviço similar, ao mesmo tempo mais integrado ao [ambiente de desktop](/index.php/Ambiente_de_desktop "Ambiente de desktop").

### Entrega local de correio

Uma instalação padrão não fornece uma forma de sincronizar correios eletrônicos (e-mails). Uma lista de agentes de entrega de correio está disponível no artigo [Servidor de e-mail](/index.php/Servidor_de_e-mail "Servidor de e-mail").

### Impressão

[CUPS](/index.php/CUPS "CUPS") é um sistema de impressão código aberto e baseado em padrões, desenvolvido pela Apple. Veja [Category:Printers](/index.php/Category:Printers "Category:Printers") para artigos específicos de impressoras.

## Aparência

Essa seção contém ajustes cosméticos frequentemente procurados para uma experiência no Arch esteticamente mais agradável. Para mais, por favor veja [Category:Eye candy](/index.php/Category:Eye_candy "Category:Eye candy").

### Fontes

Você pode querer instalar um conjunto de fontes TrueType, já que fontes bitmap não escaláveis são incluídas no sistema Arch. Há várias [famílias de fontes](/index.php/Fonts#Families "Fonts") de propósito geral fornecendo grande cobertura de [Unicode](https://en.wikipedia.org/wiki/Unicode "wikipedia:Unicode") e até mesmo [compatibilidade métrica](/index.php/Metric-compatible_fonts "Metric-compatible fonts") com fontes de outros sistemas operacionais.

Uma abundância de informações sobre o assunto pode ser localizada nos artigos [Fontes](/index.php/Fonts "Fonts") e [Configuração de fonte](/index.php/Font_configuration "Font configuration").

Se for dispender uma quantidade significante de tempo trabalhando pelo console virtual (i.e. fora de um servidor X), usuários podem querer alterar a fonte do console para melhorar a legibilidade; veja [Console do Linux#Fontes](/index.php/Console_do_Linux#Fontes "Console do Linux").

### Temas GTK e Qt

Uma grande parte dos aplicativos com uma interface gráfica para sistemas Linux são baseadas nos *toolkist* [GTK](/index.php/GTK_(Portugu%C3%AAs) "GTK (Português)") ou [Qt](/index.php/Qt "Qt"). Veja estes artigos e [Aparência uniforme para aplicativos Qt e GTK](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications") para ideias de como melhorar a aparência de seus programas instalados e adapte-o ao seu gosto.

## Melhorias no console

Essa seção se aplica a pequenas modificações que melhoram a praticidade de programas de console. Para mais, por favor veja [Category:Command shells (Português)](/index.php/Category:Command_shells_(Portugu%C3%AAs) "Category:Command shells (Português)").

### Melhorias na completação por Tab

É recomendado configurar adequadamente [completação por tab](https://en.wikipedia.org/wiki/Command-line_completion "wikipedia:Command-line completion") estendida imediatamente, conforme instruído no artigo de seu shell escolhido.

### Aliases

Fazer um *alias* de um comando, ou um grupo deles, é uma forma de economizar tempo ao usar o console. Isso é especialmente útil para tarefas repetitivas que não precisam de alterações significativas a seus parâmetros entre execuções. *Aliases* comuns para economia de tempo podem ser encontrados em [Bash#Aliases](/index.php/Bash#Aliases "Bash"), que também é facilmente portável para [zsh](/index.php/Zsh "Zsh").

### Shells alternativos

[Bash](/index.php/Bash "Bash") é o shell que está instalado por padrão em um sistema Arch. A mídia de instalação *live*, porém, usa [zsh](/index.php/Zsh "Zsh") com o pacote complementar [grml-zsh-config](https://www.archlinux.org/packages/?name=grml-zsh-config). Veja [Shell de linha de comando#Lista de shells](/index.php/Shell_de_linha_de_comando#Lista_de_shells "Shell de linha de comando") para mais alternativas.

### Adições ao Bash

Uma lista de configurações Bash diversas, pesquisa de histórico e macros [Readline](/index.php/Readline "Readline") está disponível em [Bash#Tips and tricks](/index.php/Bash#Tips_and_tricks "Bash").

### Saída colorida

Essa seção é coberta por [Saída colorida no console](/index.php/Color_output_in_console "Color output in console").

### Arquivos compactados

Arquivos compactados, ou pacotes, são frequentemente encontrados em um sistema GNU/Linux. [Tar](/index.php/Tar_(Portugu%C3%AAs) "Tar (Português)") é uma das ferramentas de arquivamento mais comumente usadas, e usuários devem estar familiarizados com sua sintaxe (pacotes do Arch Linux, por exemplo, são nada mais do que tarballs compactadas em xz). Veja [Arquivamento e compactação](/index.php/Arquivamento_e_compacta%C3%A7%C3%A3o "Arquivamento e compactação").

### Prompt de console

O prompt de console (`PS1`) pode ser personalizado para uma de diversas formas. Veja [Prompt colorido do Bash](/index.php/Color_Bash_Prompt "Color Bash Prompt") ou [Zsh#Prompts](/index.php/Zsh#Prompts "Zsh") se estiver usando Bash ou Zsh, respectivamente.

### Shell do emacs

Emacs é conhecido por conter opções diversas às tarefas de esperada edição de texto, sendo uma delas uma completa substituição do shell. Consulte [Emacs#Colored output issues](/index.php/Emacs#Colored_output_issues "Emacs") para uma correção sobre caracteres ilegíveis que podem resultar pelo uso de saída colorida.

### Suporte a mouse

Usar um mouse com o console para operações de copiar-colar pode ser preferido em relação ao modo de cópia tradicional do [GNU Screen](/index.php/GNU_Screen "GNU Screen"). Veja o [General purpose mouse](/index.php/General_purpose_mouse_(Portugu%C3%AAs) "General purpose mouse (Português)") para direções compreensivas. Note que você já pode fazer isso em [emuladores de terminal](/index.php/Terminal_emulators "Terminal emulators") com a [área de transferência](/index.php/Clipboard "Clipboard").

### Buffer de scrollback

Para ser capaz de salvar e ver conteúdo antigo que foi deslocado para fora da tela, veja [Buffer de scrollback](/index.php/Scrollback_buffer "Scrollback buffer").

### Gerenciamento de sessão

Com o uso de multiplexadores de terminal como o [tmux](/index.php/Tmux "Tmux") ou [GNU Screen](/index.php/GNU_Screen "GNU Screen"), programas podem ser executados em sessões compostas de ambas e painéis que podem ser desanexados à vontade, de forma que quando o usuário matar o emulador de terminal, terminar o [X](/index.php/X_(Portugu%C3%AAs) "X (Português)") ou encerrar sua sessão, os programas associados permanecerão em execução em segundo plano desde que o servidor multiplexador de terminar esteja ativo. Interação com programas requer reanexar à sessão.