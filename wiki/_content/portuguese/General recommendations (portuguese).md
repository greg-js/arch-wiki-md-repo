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

Essa seção lida com tarefas administrativas e gerenciamento do sistema. Para mais, por favor veja [Utilitários centrais](/index.php/Core_utilities "Core utilities") e [Category:System administration](/index.php/Category:System_administration "Category:System administration").

### Usuários e grupos

Uma nova instalação deixa você com apenas a conta de superusuário, mais conhecida como "root". Se autenticar como root por períodos prolongados de tempo, possivelmente expondo-o via [SSH](/index.php/SSH "SSH") em um servidor, [é inseguro](https://apple.stackexchange.com/questions/192365/is-it-ok-to-use-the-root-user-as-a-normal-user/192422#192422). Em vez disso, você deve criar e usar uma conta de usuário desprivilegiada para a maioria das tarefas, apenas usando a conta root para administração do sistema. Veja [Users and groups#User management](/index.php/Users_and_groups#User_management "Users and groups") para detalhes.

Usuários e grupos são mecanismo para *controle de acesso*; administradores podem ajustar participação e posse de grupos para conceder ou negar a usuários e serviços acesso a recursos do sistema. Leia o artigo [Usuários e grupos](/index.php/Users_and_groups "Users and groups") para detalhes e riscos de segurança em potencial.

### Escalação de privilégios

O comano [su](/index.php/Su "Su") (abreviação de *substitute user* ou "substituto de usuário") permite que você assuma a identidade de um outro usuário no sistema (geralmente o root) de um conta existente, enquanto o comando [sudo](/index.php/Sudo "Sudo") (abreviação para *substitute user do* ou "substituto de usuário faça") concede escalação de privilégio temporário para um comando específico.

### Gerenciamento de serviço

Arch Linux usa [systemd](/index.php/Systemd "Systemd") como o processo [init](/index.php/Init "Init"), que é um gerenciador de sistema e serviço para Linux. Para dar manutenção em sua instalação do Arch Linux, é uma boa ideia aprender os básicos sobre ele. Interação com o *systemd* é feita com o comando *systemctl*. Leia o [systemd#Basic systemctl uso](/index.php/Systemd#Basic_systemctl_uso "Systemd") para mais informações.

### Manutenção de sistema

Arch é um sistema *rolling release* e tem uma mudança rápida de pacote, então usuários levam algum tempo para fazer [manutenção do sistema](/index.php/System_maintenance "System maintenance"). Leia [Segurança](/index.php/Security "Security") para recomendações e boas párticas de *hardening* do sistema.

## Gerenciamento de pacote

Essa seção contém informações úteis relacionadas ao gerenciamento de pacote. Para mais, por favor veja [FAQ#Package management](/index.php/FAQ#Package_management "FAQ") e [Category:Package management (Português)](/index.php/Category:Package_management_(Portugu%C3%AAs) "Category:Package management (Português)").

**Note:** É imprescindível se manter atualizado com as alterações no Arch Linux que exigem intervenção manual *antes* de atualizar seu sistema. Inscreva-se na [lista de discussão arch-announce](https://mailman.archlinux.org/mailman/listinfo/arch-announce/) ou confira a página inicial pelas [últimas notícias do Arch](https://www.archlinux.org/) toda vez antes de atualizar. Alternativamente, você pode achar útil se inscrever [neste feed RSS](https://www.archlinux.org/feeds/news/) ou seguir [@archlinux](https://twitter.com/archlinux) no Twitter.

### pacman

[pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)"), uma abreviação de **pac**kage **man**ager, é o gerenciador de pacotes do Arch Linux: todos os usuários devem se familiarizar com ele antes de ler qualquer outro artigo.

Veja [Pacman/Dicas e truques](/index.php/Pacman/Tips_and_tricks "Pacman/Tips and tricks") para sugestões sobre como melhorar sua interação com *pacman* e o gerenciamento de pacotes em geral.

### Repositórios

Veja [Repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais") para detalhes sobre o propósito de cada repositório oficialmente mantido.

Se você instalou o Arch Linux x86_64 e planeja usar aplicativos 32 bits, você vai querer habilitar o repositório [multilib](/index.php/Multilib "Multilib").

[Repositórios extraoficiais de usuário](/index.php/Unofficial_user_repositories "Unofficial user repositories") lista diversos outros repositórios sem suporte.

Considere instalar o serviço [pkgstats](/index.php/Pkgstats "Pkgstats").

### Mirrors

Por vezes chamados de "espelhos". Visite [Mirrors](/index.php/Mirrors "Mirrors") para etapas para se beneficiar do uso de mirrors mais rápidos e mais atualizados dos repositórios oficiais. Como explicado no artigo, um conselho particularmente bom é verificar periodicamente a página [Mirror Status](https://www.archlinux.org/mirrors/status/) por uma lista de mirrors que foram sincronizados recentemente.

### Arch Build System

*Ports* é um sistema inicialmente usado pelas distribuições BSD consistindo em scripts de compilação que residem em uma árvore de diretório no sistema local. Basicamente, cada *port* contém um script dentro de um diretório intuitivamente nomeado pelo aplicativo terceiro instalável.

O [Arch Build System](/index.php/Arch_Build_System "Arch Build System") oferece a mesma funcionalidade para fornecer scripts de compilação chamados [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD"), que são populados com informações para uma dada peça de software; *hashes* de integridade, instruções de compilação e licença, versão e URL do projeto. Esses PKGBUILDs são posteriormente analisados pelo [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)"), o programa atual que de forma limpa gera pacotes gerenciáveis pelo *pacman*.

Todo pacote nos repositórios junto com aqueles presentes no AUR estão sujeitos a recompilação com *makepkg*.

### Arch User Repository

Enquanto o Arch Build System permite a capacidade de compilar softwares disponíveis nos repositórios oficiais, o [Arch User Repository](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)") (AUR) é o equivalente a pacotes enviados por usuários. É um repositório sem suporte de scripts de compilação acessíveis por meio da [interface web](https://aur.archlinux.org/) ou pelo [AurJson](/index.php/AurJson "AurJson").

## Inicialização

Essa seção contém informações pertinentes ao processo de inicialização (*boot*). Uma visão geral do processo de inicialização do Arch pode ser localizado em [Processo de inicialização do Arch](/index.php/Arch_boot_process "Arch boot process"). Para mais, veja [Category:Boot process](/index.php/Category:Boot_process "Category:Boot process").

### Autorreconhecimento de hardware

Hardware deve ser detectado automaticamente pelo [udev](/index.php/Udev "Udev") durante o processo de inicialização por padrão. Uma melhoria potencial no tempo de inicialização pode ser atingido pela desabilitação de carregamento automático de módulos e especificação manual dos módulos necessários, como descrito em [Módulos de kernel](/index.php/Kernel_modules "Kernel modules"). Além disso, [Xorg](/index.php/Xorg "Xorg") deve ser capaz de detectar automaticamente drivers drivers necessários usando `udev`, mas os usuários também têm a opção de configurar o servidor X manualmente.

### Microcódigo

Processadores podem ter [comportamento falho](http://www.anandtech.com/show/8376/intel-disables-tsx-instructions-erratum-found-in-haswell-haswelleep-broadwelly), o que o kernel pode corrigir atualizando o *microcódigo* na inicialização. Processadores Intel exigem um pacote separado para esse efeito. Veja [Microcódigo](/index.php/Microcode "Microcode") para detalhes.

### Retendo mensagens de inicialização

Uma vez concluído, a tela será apagada e e o prompt de login aparecerá, deixando os usuários incapaz de obter feedback sobre o processo de inicialização. [Desativar o apagamento de mensagens de inicialização](/index.php/Disable_clearing_of_boot_messages "Disable clearing of boot messages") é a solução para passar por cima dessa limitação.

### Ativação de Num Lock

Num Lock é uma tecla de ativar/desativar localizada na maioria dos teclados. Para ativar a atribuição de tecla numérica do Num Lock durante a inicialização, veja [Ativando Numlock na inicialização](/index.php/Activating_Numlock_on_Bootup "Activating Numlock on Bootup").

## Interface gráfica de usuário

Essa seção fornece orientação para usuários interessados em usar aplicativos gráficos em seu sistema. Veja [Category:X server](/index.php/Category:X_server "Category:X server") para recursos adicionais.

### Servidor de exibição

[Xorg](/index.php/Xorg "Xorg") é a implementação código aberto e pública do [X Window System](https://en.wikipedia.org/wiki/X_Window_System "wikipedia:X Window System") (mais conhecido como *X11* ou *X*). Ele é necessário para se usar aplicativos com interfaces gráficas de usuário (também conhecidas como *GUI*s) e a maioria dos usuários terão interesse em instalá-los.

[Wayland](/index.php/Wayland "Wayland") é um protocolo alternativo mais novo de servidor de exibição e a implementação referência de Weston está disponível.

### Drivers de exibição

O driver de vídeo *vesa* padrão vai funcionar com a maioria das placas de vídeo, porém o desempenho pode ser drasticamente melhorado e recursos adicionais aproveitados instalando o driver apropriado para produtos [ATI](/index.php/ATI "ATI"), [Intel](/index.php/Intel "Intel") ou [NVIDIA](/index.php/NVIDIA "NVIDIA").

### Ambientes gráficos

Apesar do Xorg fornecer um framework básico para compilação de um ambiente gráfico, componentes adicionais podem ser considerados necessários para uma experiência de usuário completa. [Ambientes gráficos](/index.php/Desktop_environment "Desktop environment") como o [GNOME](/index.php/GNOME "GNOME"), [KDE](/index.php/KDE "KDE"), [LXDE](/index.php/LXDE "LXDE") e [Xfce](/index.php/Xfce "Xfce") colecionam uma gama de *clientes X*, tal como um gerenciador de janelas, painel, gerenciador de arquivos, emulador de terminal, editor de texto, ícones e outros utilitários. Usuários com menos experiência podem preferir instalar um ambiente gráfico para ter um ambiente mais familiar. Veja [Category:Desktop environments](/index.php/Category:Desktop_environments "Category:Desktop environments") para recursos adicionais.

### Gerenciadores de janela

Um ambiente gráfico completo fornece uma interface gráfica de usuário completa e consistente, mas tende a representar um consumo considerável dos recursos do sistema. Usuários buscando maximizar o desempenho ou simplificar seu ambiente, podem optar por instalar um [gerenciador de janela](/index.php/Window_manager "Window manager") sozinho e selecionar pessoalmente os extras desejados. A maioria dos ambientes gráficos também permitem o uso de um gerenciador de janela alternativo. Os gerenciadores de janela [Dynamic](/index.php/Category:Dynamic_WMs "Category:Dynamic WMs"), [stacking](/index.php/Category:Stacking_WMs "Category:Stacking WMs") e [tiling](/index.php/Category:Tiling_WMs "Category:Tiling WMs") se diferem na forma de lidar com posicionamento das janelas.

### Gerenciadores de exibição

A maioria dos ambientes gráficos incluem um [gerenciador de exibição](/index.php/Display_manager "Display manager") para iniciar automaticamente o ambiente gráfico e gerenciar autenticação de usuário. Usuários sem um ambiente gráfico podem instalar um separadamente. Alternativamente, você pode [iniciar X no login](/index.php/Start_X_at_login "Start X at login") como uma alternativa simples a um gerenciador de exibição.

## Gerenciamento de energia

Essa seção pode ser usada por donos de laptop ou usuários que busquem controles de gerenciamento de energia. Para mais, por favor veja [Category:Power management](/index.php/Category:Power_management "Category:Power management").

Veja [Gerenciamento de energia](/index.php/Power_management "Power management") para uma visão geral.

### Eventos de ACPI

Usuários podem configurar como o sistema reage a eventos de ACPI tal como pressionamento de botão de energia ou fechamento da tampa do laptop. Para novo (recomendado) método usando [systemd](/index.php/Systemd "Systemd"), veja [Gerenciamento de energia com systemd](/index.php/Power_management#Power_management_with_systemd "Power management"). Para o método antigo, veja [acpid](/index.php/Acpid "Acpid").

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

*   [ALSA](/index.php/ALSA "ALSA") é incluído com o kernel e é recomendado porque geralmente ele funciona sem precisar de configuração (só precisa [retirar do mudo](/index.php/Advanced_Linux_Sound_Architecture#Unmuting_the_channels "Advanced Linux Sound Architecture")).

*   [OSS](/index.php/OSS "OSS") é uma alternativa viável no caso de ALSA não funcionar.

Usuários também podem querer instalar e configurar um [servidor de som](/index.php/Sound#Sound_servers "Sound") tal como [PulseAudio](/index.php/PulseAudio_(Portugu%C3%AAs) "PulseAudio (Português)"). Para requisitos de áudio avançados, veja [áudio profissional](/index.php/Professional_audio "Professional audio").

### Plugins de navegadores

Para acesso a certos conteúdos da web, [plugins de navegador](/index.php/Browser_plugins "Browser plugins") tal como Adobe Acrobat Reader, Adobe Flash Player e Java podem ser instalados.

### Codecs

[Codecs](/index.php/Codecs "Codecs") são utilizados por aplicativos de multimídia paracodificar ou decodificar *stremas* de áudio e vídeo. Para reproduzir *streams* codificados, usuários devem se assegurar de que um codec apropriado está instalado.

## Conectividade

This section is confined to small networking procedures. Head over to [Network configuration](/index.php/Network_configuration "Network configuration") for a full guide. For more, please see [Category:Networking](/index.php/Category:Networking "Category:Networking").

### Sincronização de relógio

The [Network Time Protocol](https://en.wikipedia.org/wiki/Network_Time_Protocol "wikipedia:Network Time Protocol") (NTP) is a protocol for synchronizing the clocks of computer systems over packet-switched, variable-latency data networks. See [Time#Time synchronization](/index.php/Time#Time_synchronization "Time") for implementations of such protocol.

### Segurança de DNS

For better security while browsing web, paying online, connecting to [SSH](/index.php/SSH "SSH") services and similar tasks consider using [DNSSEC](/index.php/DNSSEC "DNSSEC")-enabled client software which can validate signed [DNS](https://en.wikipedia.org/wiki/Domain_Name_System "wikipedia:Domain Name System") records, and [DNSCrypt](/index.php/DNSCrypt "DNSCrypt") to encrypt DNS traffic.

### Configuração de um firewall

A [firewall](/index.php/Firewall "Firewall") can provide an extra layer of protection on top of the Linux networking stack. While the stock Arch kernel is capable of using [Netfilter](https://en.wikipedia.org/wiki/Netfilter "wikipedia:Netfilter")'s [iptables](/index.php/Iptables "Iptables"), it is not enabled by default. It is highly recommended to set up some form of firewall. See [Firewalls](/index.php/Firewalls "Firewalls") for the available guides.

### Compartilhamento de recurso

To share files among the machines in a network, follow the [NFS](/index.php/NFS "NFS") or the [SSHFS](/index.php/SSHFS "SSHFS") article.

Use [Samba](/index.php/Samba "Samba") to join a Windows network. To configure the machine to use Active Directory for authentication, read [Active Directory Integration](/index.php/Active_Directory_Integration "Active Directory Integration").

See also [Category:Network sharing](/index.php/Category:Network_sharing "Category:Network sharing").

## Dispositivos de entrada

This section contains popular input device configuration tips. For more, please see [Category:Input devices](/index.php/Category:Input_devices "Category:Input devices").

### Layouts de teclado

Non-English or otherwise non-standard keyboards may not function as expected by default. The necessary steps to configure the keymap are different for virtual console and [Xorg](/index.php/Xorg "Xorg"), they are described in [Keyboard configuration in console](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") and [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg") respectively.

### Botões de mouse

Owners of advanced or unusual mice may find that not all mouse buttons are recognized by default, or may wish to assign different actions for extra buttons. Instructions can be found in [All Mouse Buttons Working](/index.php/All_Mouse_Buttons_Working "All Mouse Buttons Working").

### Touchpads de laptop

Many laptops use [Synaptics](http://www.synaptics.com/) or [ALPS](http://www.alps.com/) "touchpad" pointing devices. These, and several other touchpad models, use the Synaptics input driver; see [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") for installation and configuration details.

### TrackPoints

See the [TrackPoint](/index.php/TrackPoint "TrackPoint") article to configure your TrackPoint device.

## Otimizações

This section aims to summarize tweaks, tools and available options useful to improve system and application performance.

### Benchmarking

[Benchmarking](/index.php/Benchmarking "Benchmarking") is the act of measuring performance and comparing the results to another system's results or a widely accepted standard through a unified procedure.

### Melhorando o desempenho

The [Improving performance](/index.php/Improving_performance "Improving performance") article gathers information and is a basic rundown about gaining performance in Arch Linux.

### Solid state drives

The [Solid State Drives](/index.php/Solid_State_Drives "Solid State Drives") article covers many aspects of solid state drives, including configuring them to maximize their lifetimes.

## Serviço de sistema

This section relates to [daemons](/index.php/Daemons "Daemons"). For more, please see [Category:Daemons and system services](/index.php/Category:Daemons_and_system_services "Category:Daemons and system services").

### Índice e pesquisa por arquivo

Most distributions have a `locate` command available to be able to quickly search for files. To get this functionality in Arch Linux, [mlocate](https://www.archlinux.org/packages/?name=mlocate) is the recommended install. After the install you should run `updatedb` to index the filesystems.

[Desktop search engines](/index.php/List_of_applications/Utilities#Desktop_search_engines "List of applications/Utilities") provide a similar service, while better integrated into [desktop environments](/index.php/Desktop_environments "Desktop environments").

### Entrega local de correio

A default setup does not provide a way to sync mail. To configure *Postfix* for simple local mailbox delivery, see [Postfix](/index.php/Postfix "Postfix"). Other options are [SSMTP](/index.php/SSMTP "SSMTP"), [msmtp](/index.php/Msmtp "Msmtp") and [fdm](/index.php/Fdm "Fdm").

### Impressão

[CUPS](/index.php/CUPS "CUPS") is a standards-based, open source printing system developed by Apple. See [Category:Printers](/index.php/Category:Printers "Category:Printers") for printer-specific articles.

## Aparência

This section contains frequently-sought "eye candy" tweaks for an aesthetically pleasing Arch experience. For more, please see [Category:Eye candy](/index.php/Category:Eye_candy "Category:Eye candy").

### Fontes

You may wish to install a set of TrueType fonts, as only unscalable bitmap fonts are included in a basic Arch system. The [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) package provides a set of high quality, general-purpose fonts with good [Unicode](https://en.wikipedia.org/wiki/Unicode "wikipedia:Unicode") coverage.

A plethora of information on the subject can be found in the [Fonts](/index.php/Fonts "Fonts") and [Font configuration](/index.php/Font_configuration "Font configuration") articles.

If spending a significant amount of time working from the virtual console (i.e. outside an X server), users may wish to change the console font to improve readability; see [Fonts#Console fonts](/index.php/Fonts#Console_fonts "Fonts").

### Temas GTK+ e Qt

A big part of the applications with a graphical interface for Linux systems are based on the [GTK+](/index.php/GTK%2B "GTK+") or the [Qt](/index.php/Qt "Qt") toolkits. See those articles and [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications") for ideas to improve the appearance of your installed programs and adapt it to your liking.

## Melhorias no console

This section applies to small modifications that better console programs' practicality. For more, please see [Category:Command shells](/index.php/Category:Command_shells "Category:Command shells").

### Aliases

Aliasing a command, or a group thereof, is a way of saving time when using the console. This is specially helpful for repetitive tasks that do not need significant alteration to their parameters between executions. Common time-saving aliases can be found in [Bash#Aliases](/index.php/Bash#Aliases "Bash"), which are easily portable to [zsh](/index.php/Zsh "Zsh") as well.

### Shells alternativos

[Bash](/index.php/Bash "Bash") is the shell that is installed by default in an Arch system. The live installation media, however, uses [zsh](/index.php/Zsh "Zsh") with the [grml-zsh-config](https://www.archlinux.org/packages/?name=grml-zsh-config) addon package. See [Command-line shell#List of shells](/index.php/Command-line_shell#List_of_shells "Command-line shell") for more alternatives.

### Adições ao Bash

A list of miscellaneous Bash settings, including completion enhancements, history search and [Readline](/index.php/Readline "Readline") macros is available in [Bash#Tips and tricks](/index.php/Bash#Tips_and_tricks "Bash").

### Saída colorida

This section is covered in [Color output in console](/index.php/Color_output_in_console "Color output in console").

### Arquivos compactados

Compressed files, or archives, are frequently encountered on a GNU/Linux system. [Tar](/index.php/Tar "Tar") is one of the most commonly used archiving tools, and users should be familiar with its syntax (Arch Linux packages, for example, are simply xzipped tarballs). See [Bash/Functions](/index.php/Bash/Functions "Bash/Functions") for other helpful commands.

### Prompt de console

The console prompt (PS1) can be customized to a great extent. See [Color Bash Prompt](/index.php/Color_Bash_Prompt "Color Bash Prompt") or [Zsh#Prompts](/index.php/Zsh#Prompts "Zsh") if using Bash or Zsh, respectively.

### Shell do emacs

Emacs is known for featuring options beyond the duties of regular text editing, one of these being a full shell replacement. Consult [Emacs#Colored output issues](/index.php/Emacs#Colored_output_issues "Emacs") for a fix regarding garbled characters that may result from enabling colored output.

### Suporte a mouse

Using a mouse with the console for copy-paste operations can be preferred over [GNU Screen](/index.php/GNU_Screen "GNU Screen")'s traditional copy mode. Refer to [Console mouse support](/index.php/Console_mouse_support "Console mouse support") for comprehensive directions. Note that you can already do this in [terminal emulators](/index.php/Terminal_emulators "Terminal emulators") with the [clipboard](/index.php/Clipboard "Clipboard").

### Buffer de scrollback

To be able to save and view text which has scrolled off the screen, refer to [Scrollback buffer](/index.php/Scrollback_buffer "Scrollback buffer").

### Gerenciamento de sessão

Using terminal multiplexers like [tmux](/index.php/Tmux "Tmux") or [GNU Screen](/index.php/GNU_Screen "GNU Screen"), programs may be run under sessions composed of tabs and panes that can be detached at will, so when the user either kills the terminal emulator, terminates [X](/index.php/X "X"), or logs off, the programs associated with the session will continue to run in the background as long as the terminal multiplexer server is active. Interacting with the programs requires reattaching to the session.