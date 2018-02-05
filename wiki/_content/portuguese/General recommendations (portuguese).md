Artigos relacionados

*   [FAQ](/index.php/FAQ_(Portugu%C3%AAs) "FAQ (Português)")
*   [Guia de instalação](/index.php/Guia_de_instala%C3%A7%C3%A3o "Guia de instalação")
*   [Lista de aplicativos](/index.php/List_of_applications "List of applications")

Esse documento é um índice anotado de artigos populares e informações importantes para melhorar e adicionar funcionalidades ao sistema Arch instalado. Presume-se aqui que os leitores leram e seguiram o [Guia de instalação](/index.php/Guia_de_instala%C3%A7%C3%A3o "Guia de instalação") para obter uma instalação básica do Arch Linux. Ter lido e entendido os conceitos explicados em [#Administração do sistema](#Administra.C3.A7.C3.A3o_do_sistema) e [#Gerenciamento de pacote](#Gerenciamento_de_pacote) é *obrigatório* para seguir as outras seções desta página e outros artigos no wiki.

## Contents

*   [1 Administração do sistema](#Administra.C3.A7.C3.A3o_do_sistema)
    *   [1.1 Usuários e grupos](#Usu.C3.A1rios_e_grupos)
    *   [1.2 Escalação de privilégios](#Escala.C3.A7.C3.A3o_de_privil.C3.A9gios)
    *   [1.3 Gerenciamento de serviço](#Gerenciamento_de_servi.C3.A7o)
    *   [1.4 Manutenção de sistema](#Manuten.C3.A7.C3.A3o_de_sistema)
*   [2 Gerenciamento de pacote](#Gerenciamento_de_pacote)
    *   [2.1 pacman](#pacman)
    *   [2.2 Repositórios](#Reposit.C3.B3rios)
    *   [2.3 Mirrors](#Mirrors)
    *   [2.4 Arch Build System](#Arch_Build_System)
    *   [2.5 Arch User Repository](#Arch_User_Repository)
*   [3 Inicialização](#Inicializa.C3.A7.C3.A3o)
    *   [3.1 Autorreconhecimento de hardware](#Autorreconhecimento_de_hardware)
    *   [3.2 Microcódigo](#Microc.C3.B3digo)
    *   [3.3 Retendo mensagens de inicialização](#Retendo_mensagens_de_inicializa.C3.A7.C3.A3o)
    *   [3.4 Ativação de Num Lock](#Ativa.C3.A7.C3.A3o_de_Num_Lock)
*   [4 Interface gráfica de usuário](#Interface_gr.C3.A1fica_de_usu.C3.A1rio)
    *   [4.1 Servidor de exibição](#Servidor_de_exibi.C3.A7.C3.A3o)
    *   [4.2 Drivers de exibição](#Drivers_de_exibi.C3.A7.C3.A3o)
    *   [4.3 Ambientes gráficos](#Ambientes_gr.C3.A1ficos)
    *   [4.4 Gerenciadores de janela](#Gerenciadores_de_janela)
    *   [4.5 Gerenciadores de exibição](#Gerenciadores_de_exibi.C3.A7.C3.A3o)
*   [5 Gerenciamento de energia](#Gerenciamento_de_energia)
    *   [5.1 Eventos de ACPI](#Eventos_de_ACPI)
    *   [5.2 Escala de frequência de CPU](#Escala_de_frequ.C3.AAncia_de_CPU)
    *   [5.3 Laptops](#Laptops)
    *   [5.4 Suspensão e hibernação](#Suspens.C3.A3o_e_hiberna.C3.A7.C3.A3o)
*   [6 Multimídia](#Multim.C3.ADdia)
    *   [6.1 Som](#Som)
    *   [6.2 Plugins de navegadores](#Plugins_de_navegadores)
    *   [6.3 Codecs](#Codecs)
*   [7 Conectividade](#Conectividade)
    *   [7.1 Sincronização de relógio](#Sincroniza.C3.A7.C3.A3o_de_rel.C3.B3gio)
    *   [7.2 Segurança de DNS](#Seguran.C3.A7a_de_DNS)
    *   [7.3 Configuração de um firewall](#Configura.C3.A7.C3.A3o_de_um_firewall)
    *   [7.4 Compartilhamento de recurso](#Compartilhamento_de_recurso)
*   [8 Dispositivos de entrada](#Dispositivos_de_entrada)
    *   [8.1 Layouts de teclado](#Layouts_de_teclado)
    *   [8.2 Botões de mouse](#Bot.C3.B5es_de_mouse)
    *   [8.3 Touchpads de laptop](#Touchpads_de_laptop)
    *   [8.4 TrackPoints](#TrackPoints)
*   [9 Otimizações](#Otimiza.C3.A7.C3.B5es)
    *   [9.1 Benchmarking](#Benchmarking)
    *   [9.2 Melhorando o desempenho](#Melhorando_o_desempenho)
    *   [9.3 Solid state drives](#Solid_state_drives)
*   [10 Serviço de sistema](#Servi.C3.A7o_de_sistema)
    *   [10.1 Índice e pesquisa por arquivo](#.C3.8Dndice_e_pesquisa_por_arquivo)
    *   [10.2 Entrega local de correio](#Entrega_local_de_correio)
    *   [10.3 Impressão](#Impress.C3.A3o)
*   [11 Aparência](#Apar.C3.AAncia)
    *   [11.1 Fontes](#Fontes)
    *   [11.2 Temas GTK+ e Qt](#Temas_GTK.2B_e_Qt)
*   [12 Melhorias no console](#Melhorias_no_console)
    *   [12.1 Aliases](#Aliases)
    *   [12.2 Shells alternativos](#Shells_alternativos)
    *   [12.3 Adições ao Bash](#Adi.C3.A7.C3.B5es_ao_Bash)
    *   [12.4 Saída colorida](#Sa.C3.ADda_colorida)
    *   [12.5 Arquivos compactados](#Arquivos_compactados)
    *   [12.6 Prompt de console](#Prompt_de_console)
    *   [12.7 Shell do emacs](#Shell_do_emacs)
    *   [12.8 Suporte a mouse](#Suporte_a_mouse)
    *   [12.9 Buffer de scrollback](#Buffer_de_scrollback)
    *   [12.10 Gerenciamento de sessão](#Gerenciamento_de_sess.C3.A3o)

## Administração do sistema

Essa seção lida com tarefas administrativas e gerenciamento do sistema. Para mais, por favor veja [Utilitários centrais](/index.php/Core_utilities "Core utilities") e [Category:System administration (Português)](/index.php/Category:System_administration_(Portugu%C3%AAs) "Category:System administration (Português)").

### Usuários e grupos

Uma nova instalação deixa você com apenas a conta de superusuário, mais conhecida como "root". Se autenticar como root por períodos prolongados de tempo, possivelmente expondo-o via [SSH](/index.php/SSH "SSH") em um servidor, [é inseguro](https://apple.stackexchange.com/questions/192365/is-it-ok-to-use-the-root-user-as-a-normal-user/192422#192422). Em vez disso, você deve criar e usar uma conta de usuário desprivilegiada para a maioria das tarefas, apenas usando a conta root para administração do sistema. Veja [Usuários e grupos#Gerenciamento de usuário](/index.php/Usu%C3%A1rios_e_grupos#Gerenciamento_de_usu.C3.A1rio "Usuários e grupos") para detalhes.

Usuários e grupos são mecanismo para *controle de acesso*; administradores podem ajustar participação e posse de grupos para conceder ou negar a usuários e serviços acesso a recursos do sistema. Leia o artigo [Usuários e grupos](/index.php/Usu%C3%A1rios_e_grupos "Usuários e grupos") para detalhes e riscos de segurança em potencial.

### Escalação de privilégios

Os comandos [su](/index.php/Su "Su") e [sudo](/index.php/Sudo "Sudo") permitem que você execute comandos como outro usuário. Por padrão, *su* lhe fornece um shell de login como o usuário root e *sudo*, por padrão, temporariamente lhe concede privilégios para um único comando. Veja seus respectivos artigos para diferenças.

### Gerenciamento de serviço

Arch Linux usa [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") como o processo [init](/index.php/Init "Init"), que é um gerenciador de sistema e serviço para Linux. Para dar manutenção em sua instalação do Arch Linux, é uma boa ideia aprender os básicos sobre ele. Interação com o *systemd* é feita com o comando *systemctl*. Leia o [systemd (Português)#Uso básico systemctl](/index.php/Systemd_(Portugu%C3%AAs)#Uso_b.C3.A1sico_systemctl "Systemd (Português)") para mais informações.

### Manutenção de sistema

Arch é um sistema *rolling release* e tem uma mudança rápida de pacote, então usuários levam algum tempo para fazer [manutenção do sistema](/index.php/Manuten%C3%A7%C3%A3o_do_sistema "Manutenção do sistema"). Leia [Segurança](/index.php/Security "Security") para recomendações e boas párticas de *hardening* do sistema.

## Gerenciamento de pacote

Essa seção contém informações úteis relacionadas ao gerenciamento de pacote. Para mais, por favor veja [FAQ (Português)#Gerenciamento de pacote](/index.php/FAQ_(Portugu%C3%AAs)#Gerenciamento_de_pacote "FAQ (Português)") e [Category:Package management (Português)](/index.php/Category:Package_management_(Portugu%C3%AAs) "Category:Package management (Português)").

**Nota:** É imprescindível se manter atualizado com as alterações no Arch Linux que exigem intervenção manual *antes* de atualizar seu sistema. Inscreva-se na [lista de discussão arch-announce](https://mailman.archlinux.org/mailman/listinfo/arch-announce/) ou confira a página inicial pelas [últimas notícias do Arch](https://www.archlinux.org/) toda vez antes de atualizar. Alternativamente, você pode achar útil se inscrever [neste feed RSS](https://www.archlinux.org/feeds/news/) ou seguir [@archlinux](https://twitter.com/archlinux) no Twitter.

### pacman

[pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)"), uma abreviação de **pac**kage **man**ager, é o gerenciador de pacotes do Arch Linux: todos os usuários devem se familiarizar com ele antes de ler qualquer outro artigo.

Veja [pacman/Dicas e truques](/index.php/Pacman/Dicas_e_truques "Pacman/Dicas e truques") para sugestões sobre como melhorar sua interação com *pacman* e o gerenciamento de pacotes em geral.

### Repositórios

Veja [Repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais") para detalhes sobre o propósito de cada repositório oficialmente mantido.

Se você planeja usar aplicativos 32 bits, você vai querer habilitar o repositório [multilib](/index.php/Multilib_(Portugu%C3%AAs) "Multilib (Português)").

[Repositórios extraoficiais de usuário](/index.php/Unofficial_user_repositories "Unofficial user repositories") lista diversos outros repositórios sem suporte.

Considere instalar o serviço [pkgstats](/index.php/Pkgstats_(Portugu%C3%AAs) "Pkgstats (Português)").

### Mirrors

Por vezes chamados de "espelhos". Visite [Mirrors](/index.php/Mirrors "Mirrors") para etapas para se beneficiar do uso de mirrors mais rápidos e mais atualizados dos repositórios oficiais. Como explicado no artigo, um conselho particularmente bom é verificar periodicamente a página [Mirror Status](https://www.archlinux.org/mirrors/status/) por uma lista de mirrors que foram sincronizados recentemente.

### Arch Build System

*Ports* é um sistema inicialmente usado pelas distribuições BSD consistindo em scripts de compilação que residem em uma árvore de diretório no sistema local. Basicamente, cada *port* contém um script dentro de um diretório intuitivamente nomeado pelo aplicativo terceiro instalável.

O [Arch Build System](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)") oferece a mesma funcionalidade para fornecer scripts de compilação chamados [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)"), que são populados com informações para uma dada peça de software; *hashes* de integridade, instruções de compilação e licença, versão e URL do projeto. Esses PKGBUILDs são posteriormente analisados pelo [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)"), o programa atual que de forma limpa gera pacotes gerenciáveis pelo *pacman*.

Todo pacote nos repositórios junto com aqueles presentes no AUR estão sujeitos a recompilação com *makepkg*.

### Arch User Repository

Enquanto o Arch Build System permite a capacidade de compilar softwares disponíveis nos repositórios oficiais, o [Arch User Repository](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)") (AUR) é o equivalente a pacotes enviados por usuários. É um repositório sem suporte de scripts de compilação acessíveis por meio da [interface web](https://aur.archlinux.org/) ou pelo [AurJson](/index.php/AurJson_(Portugu%C3%AAs) "AurJson (Português)").

## Inicialização

Essa seção contém informações pertinentes ao processo de inicialização (*boot*). Uma visão geral do processo de inicialização do Arch pode ser localizado em [Processo de inicialização do Arch](/index.php/Arch_boot_process "Arch boot process"). Para mais, veja [Category:Boot process (Português)](/index.php/Category:Boot_process_(Portugu%C3%AAs) "Category:Boot process (Português)").

### Autorreconhecimento de hardware

Hardware deve ser detectado automaticamente pelo [udev](/index.php/Udev "Udev") durante o processo de inicialização por padrão. Uma melhoria potencial no tempo de inicialização pode ser atingido pela desabilitação de carregamento automático de módulos e especificação manual dos módulos necessários, como descrito em [Módulos de kernel](/index.php/Kernel_modules "Kernel modules"). Além disso, [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)") deve ser capaz de detectar automaticamente drivers drivers necessários usando `udev`, mas os usuários também têm a opção de configurar o servidor X manualmente.

### Microcódigo

Processadores podem ter [comportamento falho](http://www.anandtech.com/show/8376/intel-disables-tsx-instructions-erratum-found-in-haswell-haswelleep-broadwelly), o que o kernel pode corrigir atualizando o *microcódigo* na inicialização. Processadores Intel exigem um pacote separado para esse efeito. Veja [Microcódigo](/index.php/Microcode "Microcode") para detalhes.

### Retendo mensagens de inicialização

Uma vez concluído, a tela será apagada e e o prompt de login aparecerá, deixando os usuários incapaz de obter feedback sobre o processo de inicialização. [Desativar o apagamento de mensagens de inicialização](/index.php/Disable_clearing_of_boot_messages "Disable clearing of boot messages") é a solução para passar por cima dessa limitação.

### Ativação de Num Lock

Num Lock é uma tecla de ativar/desativar localizada na maioria dos teclados. Para ativar a atribuição de tecla numérica do Num Lock durante a inicialização, veja [Ativando Numlock na inicialização](/index.php/Activating_Numlock_on_Bootup "Activating Numlock on Bootup").

## Interface gráfica de usuário

Essa seção fornece orientação para usuários interessados em usar aplicativos gráficos em seu sistema. Veja [Category:X server](/index.php/Category:X_server "Category:X server") para recursos adicionais.

### Servidor de exibição

[Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)") é a implementação código aberto e pública do [X Window System](https://en.wikipedia.org/wiki/pt:X_Window_System "wikipedia:pt:X Window System") (mais conhecido como *X11* ou *X*). Ele é necessário para se usar aplicativos com interfaces gráficas de usuário (também conhecidas como *GUI*s) e a maioria dos usuários terão interesse em instalá-los.

[Wayland](/index.php/Wayland "Wayland") é um protocolo alternativo mais novo de servidor de exibição e a implementação referência de Weston está disponível.

### Drivers de exibição

O driver de vídeo *vesa* padrão vai funcionar com a maioria das placas de vídeo, porém o desempenho pode ser drasticamente melhorado e recursos adicionais aproveitados instalando o driver apropriado para produtos [ATI](/index.php/ATI "ATI"), [Intel](/index.php/Intel_(Portugu%C3%AAs) "Intel (Português)") ou [NVIDIA](/index.php/NVIDIA "NVIDIA").

### Ambientes gráficos

Apesar do Xorg fornecer um framework básico para compilação de um ambiente gráfico, componentes adicionais podem ser considerados necessários para uma experiência de usuário completa. [Ambientes gráficos](/index.php/Desktop_environment "Desktop environment") como o [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)"), [KDE](/index.php/KDE "KDE"), [LXDE](/index.php/LXDE "LXDE") e [Xfce](/index.php/Xfce "Xfce") colecionam uma gama de *clientes X*, tal como um gerenciador de janelas, painel, gerenciador de arquivos, emulador de terminal, editor de texto, ícones e outros utilitários. Usuários com menos experiência podem preferir instalar um ambiente gráfico para ter um ambiente mais familiar. Veja [Category:Desktop environments](/index.php/Category:Desktop_environments "Category:Desktop environments") para recursos adicionais.

### Gerenciadores de janela

Um ambiente gráfico completo fornece uma interface gráfica de usuário completa e consistente, mas tende a representar um consumo considerável dos recursos do sistema. Usuários buscando maximizar o desempenho ou simplificar seu ambiente, podem optar por instalar um [gerenciador de janela](/index.php/Gerenciador_de_janela "Gerenciador de janela") sozinho e selecionar pessoalmente os extras desejados. A maioria dos ambientes gráficos também permitem o uso de um gerenciador de janela alternativo. Os gerenciadores de janela [dinâmicos](/index.php/Category:Dynamic_WMs "Category:Dynamic WMs"), [empilhamento](/index.php/Category:Stacking_WMs "Category:Stacking WMs") e [tiling](/index.php/Category:Tiling_WMs "Category:Tiling WMs") se diferem na forma de lidar com posicionamento das janelas.

### Gerenciadores de exibição

A maioria dos ambientes gráficos incluem um [gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição") para iniciar automaticamente o ambiente gráfico e gerenciar autenticação de usuário. Usuários sem um ambiente gráfico podem instalar um separadamente. Alternativamente, você pode [iniciar X no login](/index.php/Start_X_at_login "Start X at login") como uma alternativa simples a um gerenciador de exibição.

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

Veja o artigo principal: [Suspensão e hibernação](/index.php/Suspend_and_hibernate "Suspend and hibernate").

## Multimídia

[Category:Multimedia](/index.php/Category:Multimedia "Category:Multimedia") inclui recursos adicionais.

### Som

[Som](/index.php/Sound "Sound") é fornecido pelos drivers de som do kernel:

*   [ALSA](/index.php/ALSA_(Portugu%C3%AAs) "ALSA (Português)") é incluído com o kernel e é recomendado porque geralmente ele funciona sem precisar de configuração (só precisa [retirar do mudo](/index.php/Advanced_Linux_Sound_Architecture#Unmuting_the_channels "Advanced Linux Sound Architecture")).

*   [OSS](/index.php/OSS "OSS") é uma alternativa viável no caso de ALSA não funcionar.

Usuários também podem querer instalar e configurar um [servidor de som](/index.php/Sound#Sound_servers "Sound") tal como [PulseAudio](/index.php/PulseAudio_(Portugu%C3%AAs) "PulseAudio (Português)"). Para requisitos de áudio avançados, veja [áudio profissional](/index.php/Professional_audio "Professional audio").

### Plugins de navegadores

Para acesso a certos conteúdos da web, [plugins de navegador](/index.php/Browser_plugins "Browser plugins") tal como Adobe Acrobat Reader, Adobe Flash Player e Java podem ser instalados.

### Codecs

[Codecs](/index.php/Codecs "Codecs") são utilizados por aplicativos de multimídia paracodificar ou decodificar *stremas* de áudio e vídeo. Para reproduzir *streams* codificados, usuários devem se assegurar de que um codec apropriado está instalado.

## Conectividade

Essa seção está confinada a pequenos procedimentos de conectividade. Siga para [Configuração de rede](/index.php/Configura%C3%A7%C3%A3o_de_rede "Configuração de rede") para um guia completo. Para mais, por favor veja [Category:Networking (Português)](/index.php/Category:Networking_(Portugu%C3%AAs) "Category:Networking (Português)").

### Sincronização de relógio

O [Network Time Protocol](https://en.wikipedia.org/wiki/Network_Time_Protocol "wikipedia:Network Time Protocol") (NTP) é um protocolo para sincronizar os relógios de sistemas de computador em redes de dados de latência variável com comutação de pacotes. Veja [Time#Time synchronization](/index.php/Time#Time_synchronization "Time") para implementações de tal protocolo.

### Segurança de DNS

Para melhor segurança ao navegar na web, jogar na internet, conectar a serviços [SSH](/index.php/SSH "SSH") e tarefas similares, considere usar software cliente habilitado para [DNSSEC](/index.php/DNSSEC "DNSSEC") que pode validar registros [DNS](https://en.wikipedia.org/wiki/Domain_Name_System "wikipedia:Domain Name System") assinados e [DNSCrypt](/index.php/DNSCrypt "DNSCrypt") para criptografar tráfego DNS.

### Configuração de um firewall

Um [firewall](/index.php/Firewall "Firewall") pode fornecer uma camada extra de proteção sobre a pilha de rede do Linux. O kernel padrão do Arch é capaz de usar [iptables](/index.php/Iptables "Iptables") do [Netfilter](https://en.wikipedia.org/wiki/Netfilter "wikipedia:Netfilter") e [nftables](/index.php/Nftables "Nftables"), apesar de não estarem habilitados por padrão. É altamente recomendado para configurar alguma forma de firewall. Veja [Category:Firewalls](/index.php/Category:Firewalls "Category:Firewalls") para os guias disponíveis.

### Compartilhamento de recurso

Para compartilhar arquivos entre máquinas em uma rede, siga o artigo [NFS](/index.php/NFS "NFS") ou o [SSHFS](/index.php/SSHFS "SSHFS").

Use [Samba](/index.php/Samba "Samba") para entrar em uma rede Windows. Para configurar a máquina para usar Active Directory para autenticação, leia [Active Directory Integration](/index.php/Active_Directory_Integration "Active Directory Integration").

Veja também [Category:Network sharing](/index.php/Category:Network_sharing "Category:Network sharing").

## Dispositivos de entrada

Esse seção contém dicas de configuração de dispositivo de entrada popular. Para mais, por favor veja [Category:Input devices](/index.php/Category:Input_devices "Category:Input devices").

### Layouts de teclado

Teclados não-americanos ou fora de padrão podem não funcionar como esperado por padrão. Os passos necessários para configurar o mapa de teclas sãos diferentes para console virtual e [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)"), eles são descritos [Configuração de teclado no console](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") e [Configuração de teclado no Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg"), respectivamente.

### Botões de mouse

Proprietários de mouses avançados ou incomuns podem descobrir que nem todos os botões do mouse são reconhecidos por padrão, ou podem querer atribuir ações diferentes para botões extras. Instruções podem ser localizadas em [Todos botões do mouse funcionando](/index.php/All_Mouse_Buttons_Working "All Mouse Buttons Working").

### Touchpads de laptop

Muitos laptops usam dispositivos de ponteiro "touchpad" [Synaptics](https://www.synaptics.com/) ou [ALPS](http://www.alps.com/). Para esses e vários outros modelos de touchpad você pode usar o driver de entrada do Synaptics ou do libinput; veja [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") ou [libinput](/index.php/Libinput "Libinput") para detalhes de instalação e configuração.

### TrackPoints

Veja o artigo [TrackPoint](/index.php/TrackPoint "TrackPoint") para configurar seu dispositivo TrackPoint.

## Otimizações

Essa seção visa resumir ajustes, ferramentas e opções disponíveis úteis para melhorar o desempenho do sistema e de aplicativos.

### Benchmarking

[Benchmarking](/index.php/Benchmarking "Benchmarking") é o ato de medir o desemepho e comparar os resultados ou um padrão amplamente aceito por meio de um procedimento unificado.

### Melhorando o desempenho

O artigo [Melhorando o desempenho](/index.php/Improving_performance "Improving performance") junta informações e é resumo básico sobre ganho de desempenho no Arch Linux.

### Solid state drives

O artigo [Solid State Drives](/index.php/Solid_State_Drives "Solid State Drives") cobre muitos aspectos de *solid state drives*, também conhecidos como "unidades de estado sólido", incluindo configurá-los para maximizar seu tempo de vida.

## Serviço de sistema

Essa seção está relacionada a [daemons](/index.php/Daemons_(Portugu%C3%AAs) "Daemons (Português)"). Para mais, por favor veja [Category:Daemons and system services (Português)](/index.php/Category:Daemons_and_system_services_(Portugu%C3%AAs) "Category:Daemons and system services (Português)").

### Índice e pesquisa por arquivo

A maioria das distribuições possuem um comando `locate` disponível para possibilitar uma pesquisa rápida por arquivos. Para obter essa funcionalidade no Arch Linux, [mlocate](https://www.archlinux.org/packages/?name=mlocate) é a instalação recomendável. Após tê-lo instalado, você deve executar `updatedb` para indexar os sistemas de arquivos.

[Mecanismos de pesquisa](/index.php/List_of_applications/Utilities#Desktop_search_engines "List of applications/Utilities") fornecem um serviço similar, ao mesmo tempo mais integrado ao [ambiente gráfico](/index.php/Desktop_environments "Desktop environments").

### Entrega local de correio

Uma instalação padrão não forence uma forma de sincronizar correios eletrônicos (e-mails). Para configurar *Postfix* para uma simples entrega para caixa de correio local, veja [Postfix](/index.php/Postfix "Postfix"). Outras opções são [SSMTP](/index.php/SSMTP "SSMTP"), [msmtp](/index.php/Msmtp "Msmtp") e [fdm](/index.php/Fdm "Fdm").

### Impressão

[CUPS](/index.php/CUPS "CUPS") é um sistema de impressão código aberto e baseado em padrões, desenvolvido pela Apple. Veja [Category:Printers](/index.php/Category:Printers "Category:Printers") para artigos específicos de impressoras.

## Aparência

Essa seção contém ajustes cosméticos frequentemente procurados para uma experiência no Arch esteticamente mais agradável. Para mais, por favor veja [Category:Eye candy](/index.php/Category:Eye_candy "Category:Eye candy").

### Fontes

Você pode querer instalar um conjunto de fontes TrueType, já que fontes bitmap não escaláveis são incluídas no sistema Arch. O pacote [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) fornece um conjunto de alta qualidade, fontes de propósito geral com boa cobertura de [Unicode](https://en.wikipedia.org/wiki/Unicode "wikipedia:Unicode").

Uma abundância de informações sobre o assunto pode ser localizada nos artigos [Fontes](/index.php/Fonts "Fonts") e [Configuração de fonte](/index.php/Font_configuration "Font configuration").

Se for dispender uma quantidade significante de tempo trabalhando pelo console virtual (i.e. fora de um servidor X), usuários podem querer alterar a fonte do console para melhorar a legibilidade; veja [Fonts#Console fonts](/index.php/Fonts#Console_fonts "Fonts").

### Temas GTK+ e Qt

Uma grande parte dos aplicativos com uma interface gráfica para sistemas Linux são baseadas nos *toolkist* [GTK+](/index.php/GTK%2B "GTK+") ou [Qt](/index.php/Qt "Qt"). Veja estes artigos e [Aparência uniforme para aplicativos Qt e GTK](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications") para ideias de como melhorar a aparência de seus programas instalados e adapte-o ao seu gosto.

## Melhorias no console

Essa seção se aplica a pequenas modificações que melhoram a praticidade de programas de console. Para mais, por favor veja [Category:Command shells (Português)](/index.php/Category:Command_shells_(Portugu%C3%AAs) "Category:Command shells (Português)").

### Aliases

Fazer um *alias* de um comando, ou um grupo deles, é uma forma de economizar tempo ao usar o console. Isso é especialmente útil para tarefas repetitivas que não precisam de alterações significativas a seus parâmetros entre execuções. *Aliases* comuns para economia de tempo podem ser encontrados em [Bash#Aliases](/index.php/Bash#Aliases "Bash"), que também é facilmente portável para [zsh](/index.php/Zsh "Zsh").

### Shells alternativos

[Bash](/index.php/Bash "Bash") é o shell que está instalado por padrão em um sistema Arch. A mídia de instalação *live*, porém, usa [zsh](/index.php/Zsh "Zsh") com o pacote complementar [grml-zsh-config](https://www.archlinux.org/packages/?name=grml-zsh-config). Veja [Command-line shell (Português)#Lista de shells](/index.php/Command-line_shell_(Portugu%C3%AAs)#Lista_de_shells "Command-line shell (Português)") para mais alternativas.

### Adições ao Bash

Uma lista de configurações Bash diversas, incluindo melhorias de *completion* (completação, conclusão), pesquisa de histórico e macros [Readline](/index.php/Readline "Readline") está disponível em [Bash#Tips and tricks](/index.php/Bash#Tips_and_tricks "Bash").

### Saída colorida

Essa seção é coberta por [Saída colorida no console](/index.php/Color_output_in_console "Color output in console").

### Arquivos compactados

Arquivos compactados, ou pacotes, são frequentemente encontrados em um sistema GNU/Linux. [Tar](/index.php/Tar "Tar") é uma das ferramentas de arquivamento mais comumente usadas, e usuários devem estar familiarizados com sua sintaxe (pacotes do Arch Linux, por exemplo, são nada mais do que tarballs compactadas em xz). Veja [Bash/Functions](/index.php/Bash/Functions "Bash/Functions") para outros comandos úteis.

### Prompt de console

O prompt de console (PS1) pode ser personalizado para uma de diversas formas. Veja [Prompt colorido do Bash](/index.php/Color_Bash_Prompt "Color Bash Prompt") ou [Zsh#Prompts](/index.php/Zsh#Prompts "Zsh") se estiver usando Bash ou Zsh, respectivamente.

### Shell do emacs

Emacs é conhecido por conter opções diversas às tarefas de esperada edição de texto, sendo uma delas uma completa substituição do shell. Consulte [Emacs#Colored output issues](/index.php/Emacs#Colored_output_issues "Emacs") para uma correção sobre caracteres ilegíveis que podem resultar pelo uso de saída colorida.

### Suporte a mouse

Usar um mouse com o console para operações de copiar-colar pode ser preferido em relação ao modo de cópia tradicional do [GNU Screen](/index.php/GNU_Screen "GNU Screen"). Veja o [Suporte a mouse no console](/index.php/Console_mouse_support "Console mouse support") para direções compreensivas. Note que você já pode fazer isso em [emuladores de terminal](/index.php/Terminal_emulators "Terminal emulators") com a [área de transferência](/index.php/Clipboard "Clipboard").

### Buffer de scrollback

Para ser capaz de salvar e ver conteúdo antigo que foi deslocado para fora da tela, veja [Buffer de scrollback](/index.php/Scrollback_buffer "Scrollback buffer").

### Gerenciamento de sessão

Com o uso de multiplexadores de terminal como o [tmux](/index.php/Tmux "Tmux") ou [GNU Screen](/index.php/GNU_Screen "GNU Screen"), programas podem ser executados em sessões compostas de ambas e painéis que podem ser desanexados à vontade, de forma que quando o usuário matar o emulador de terminal, terminar o [X](/index.php/X_(Portugu%C3%AAs) "X (Português)") ou encerrar sua sessão, os programas associados permanecerão em execução em segundo plano desde que o servidor multiplexador de terminar esteja ativo. Interação com programas requer reanexar à sessão.