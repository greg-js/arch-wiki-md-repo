**Status de tradução:** Esse artigo é uma tradução de [VirtualBox](/index.php/VirtualBox "VirtualBox"). Data da última tradução: 2019-07-08\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=VirtualBox&diff=0&oldid=576206) na versão em inglês.

Artigos relacionados

*   [VirtualBox/Dicas e truques](/index.php/VirtualBox/Tips_and_tricks "VirtualBox/Tips and tricks")
*   [Category:Hypervisors (Português)](/index.php/Category:Hypervisors_(Portugu%C3%AAs) "Category:Hypervisors (Português)")
*   [PhpVirtualBox](/index.php/PhpVirtualBox "PhpVirtualBox")
*   [RemoteBox](/index.php/RemoteBox "RemoteBox")
*   [Movendo uma instalação existente para dentro (ou fora) de uma máquina virtual](/index.php/Moving_an_existing_install_into_(or_out_of)_a_virtual_machine "Moving an existing install into (or out of) a virtual machine")

[VirtualBox](https://www.virtualbox.org) é um [hipervisor](https://en.wikipedia.org/wiki/pt:Hipervisor para gerenciar e executar máquinas virtuais.

A fim de integrar funções do sistema host aos convidados, incluindo pastas compartilhadas e área de transferência, aceleração de vídeo e um modo de integração de janela transparente, os "adicionais para convidado" (*guest additions*) são fornecidos para alguns sistemas operacionais convidados.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Etapas de instalação para hosts Arch Linux](#Etapas_de_instalação_para_hosts_Arch_Linux)
    *   [1.1 Instalar os pacotes principais](#Instalar_os_pacotes_principais)
    *   [1.2 Assinar módulos](#Assinar_módulos)
    *   [1.3 Carregar os módulos de kernel do VirtualBox](#Carregar_os_módulos_de_kernel_do_VirtualBox)
    *   [1.4 Acessando dispositivos USB do host no convidado](#Acessando_dispositivos_USB_do_host_no_convidado)
    *   [1.5 Disco de adicionais para convidado](#Disco_de_adicionais_para_convidado)
    *   [1.6 Pacote de extensões](#Pacote_de_extensões)
    *   [1.7 Front-ends](#Front-ends)
*   [2 Etapas de instalação para convidados Arch Linux](#Etapas_de_instalação_para_convidados_Arch_Linux)
    *   [2.1 Instalação no modo EFI](#Instalação_no_modo_EFI)
    *   [2.2 Instalar os adicionais para convidado](#Instalar_os_adicionais_para_convidado)
    *   [2.3 Definir a melhor resolução de framebuffer](#Definir_a_melhor_resolução_de_framebuffer)
    *   [2.4 Carregar os módulos de kernel do VirtualBox](#Carregar_os_módulos_de_kernel_do_VirtualBox_2)
    *   [2.5 Iniciar os serviços de convidados do VirtualBox](#Iniciar_os_serviços_de_convidados_do_VirtualBox)
    *   [2.6 Aceleração de hardware](#Aceleração_de_hardware)
    *   [2.7 Habilitar pastas compartilhadas](#Habilitar_pastas_compartilhadas)
        *   [2.7.1 Montagem manual](#Montagem_manual)
        *   [2.7.2 Montagem automática](#Montagem_automática)
        *   [2.7.3 Montar na inicialização](#Montar_na_inicialização)
    *   [2.8 SSH do host para o convidado](#SSH_do_host_para_o_convidado)
        *   [2.8.1 SSHFS como alternativa à pasta compartilhada](#SSHFS_como_alternativa_à_pasta_compartilhada)
*   [3 Gerenciamento de discos virtuais](#Gerenciamento_de_discos_virtuais)
    *   [3.1 Formatos suportados pelo VirtualBox](#Formatos_suportados_pelo_VirtualBox)
    *   [3.2 Conversão de formato de imagem de disco](#Conversão_de_formato_de_imagem_de_disco)
        *   [3.2.1 QCOW](#QCOW)
    *   [3.3 Montar discos virtuais](#Montar_discos_virtuais)
        *   [3.3.1 VDI](#VDI)
        *   [3.3.2 VHD](#VHD)
    *   [3.4 Compactar discos virtuais](#Compactar_discos_virtuais)
    *   [3.5 Aumentar discos virtuais](#Aumentar_discos_virtuais)
        *   [3.5.1 Procedimento geral](#Procedimento_geral)
        *   [3.5.2 Aumentando o tamanho de discos VDI](#Aumentando_o_tamanho_de_discos_VDI)
    *   [3.6 Substituir um disco virtual manualmente a partir do arquivo .vbox](#Substituir_um_disco_virtual_manualmente_a_partir_do_arquivo_.vbox)
        *   [3.6.1 Transferir entre host Linux e outro SO](#Transferir_entre_host_Linux_e_outro_SO)
    *   [3.7 Clonar um disco virtual e atribuição d eum novo UUID a ele](#Clonar_um_disco_virtual_e_atribuição_d_eum_novo_UUID_a_ele)
*   [4 Dicas e truques](#Dicas_e_truques)
*   [5 Solução de problemas](#Solução_de_problemas)
    *   [5.1 Teclado e mouse estão travados na máquina virtual](#Teclado_e_mouse_estão_travados_na_máquina_virtual)

## Etapas de instalação para hosts Arch Linux

Para iniciar as máquinas virtuais do VirtualBox na sua caixa Arch Linux, siga estas etapas de instalação.

### Instalar os pacotes principais

[Instale](/index.php/Instale "Instale") o pacote [virtualbox](https://www.archlinux.org/packages/?name=virtualbox). Você precisará escolher um pacote para fornecer os módulos de host:

*   para o kernel [linux](https://www.archlinux.org/packages/?name=linux), escolha [virtualbox-host-modules-arch](https://www.archlinux.org/packages/?name=virtualbox-host-modules-arch)
*   para outros [kernels](/index.php/Kernels "Kernels"), escolha [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms)

Para compilar os módulos do VirtualBox fornecidos pelo [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms), também será necessário instalar o(s) pacote(s) apropriado(s) para o(s) seu(s) kernel(s) instalado(s) (p.ex., [linux-lts-headers](https://www.archlinux.org/packages/?name=linux-lts-headers) para [linux-lts](https://www.archlinux.org/packages/?name=linux-lts)). [[1]](https://lists.archlinux.org/pipermail/arch-dev-public/2016-March/027808.html) Quando o VirtualBox ou o kernel é atualizado, os módulos do kernel serão recompilados automaticamente graças ao hook do pacman de [DKMS](/index.php/DKMS "DKMS").

### Assinar módulos

Ao usar um kernel personalizado com a opção `CONFIG_MODULE_SIG_FORCE` ativada, você deve assinar seus módulos com uma chave gerada durante a compilação do kernel.

Navegue até a pasta da árvore do kernel e execute o seguinte comando:

```
# for module in `ls /lib/modules/$(uname -r)/kernel/misc/{vboxdrv.ko,vboxnetadp.ko,vboxnetflt.ko,vboxpci.ko}` ; do ./scripts/sign-file sha1 certs/signing_key.pem certs/signing_key.x509 $module ; done

```

**Nota:** O algoritmo de hashing não precisa corresponder ao configurado, mas deve ser integrado ao kernel.

### Carregar os módulos de kernel do VirtualBox

[virtualbox-host-modules-arch](https://www.archlinux.org/packages/?name=virtualbox-host-modules-arch) e [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) usam `systemd-modules-load.service` para carregar todos os quatro módulos do VirtualBox automaticamente no momento da inicialização. Para que os módulos sejam carregados após a instalação, reinicie ou carregue os módulos uma vez manualmente.

**Nota:** Se você não quer que os módulos do VirtualBox sejam carregados automaticamente no momento da inicialização, você tem que usar [mask](/index.php/Mask_(Portugu%C3%AAs) "Mask (Português)") para mascarar o padrão `/usr/lib/modules-load.d/virtualbox-host-modules-arch.conf` (ou `/usr/lib/modules-load.d/virtualbox-host-dkms.conf`) criando um arquivo vazio (ou um link simbólico para `/dev/null`) com o mesmo nome em `/etc/modules-load.d/`.

Entre os [módulos de kernel](/index.php/Kernel_module "Kernel module") que o VirtualBox usa, existe um módulo obrigatório chamado `vboxdrv`, que deve ser carregado antes que qualquer máquina virtual possa ser executada.

Para carregar o módulo manualmente, executar:

```
# modprobe vboxdrv

```

Os seguintes módulos são necessários somente em configurações avançadas:

*   `vboxnetadp` e `vboxnetflt` são necessários quando você pretende usar os recursos de [conexão em modo Bridge](https://www.virtualbox.org/manual/ch06.html#network_bridged) ou [Rede Interna](https://www.virtualbox.org/manual/ch06.html#network_hostonly). Mais precisamente, o `vboxnetadp` é necessário para criar a interface do host nas preferências globais do VirtualBox, e `vboxnetflt` é necessário para iniciar uma máquina virtual usando essa interface de rede.
*   `vboxpci` é necessário quando sua máquina virtual precisa passar por um dispositivo PCI em seu host.

**Nota:** Se os módulos do kernel do VirtualBox foram carregados no kernel enquanto você atualizou os módulos, você precisa recarregá-los manualmente para usar a nova versão atualizada. Para fazer isso, execute `vboxreload` como root.

### Acessando dispositivos USB do host no convidado

Para usar as portas USB de sua máquina host em suas máquinas virtuais, adicione usuários que serão autorizados a usar esse recurso para o [grupo de usuários](/index.php/Grupo_de_usu%C3%A1rios "Grupo de usuários") `vboxusers`.

### Disco de adicionais para convidado

Também é recomendado instalar o pacote [virtualbox-guest-iso](https://www.archlinux.org/packages/?name=virtualbox-guest-iso) no host executando o VirtualBox. Este pacote funcionará como uma imagem de disco que pode ser usada para instalar os adicionais para convidado em sistemas convidados que não sejam o Arch Linux. O arquivo *.iso* estará localizado em `/usr/lib/virtualbox/additions/VBoxGuestAdditions.iso`, e pode ter que ser montado manualmente dentro da máquina virtual. Uma vez montado, você pode executar o instalador de adicionais para convidado dentro da máquina convidado.

### Pacote de extensões

O Oracle Extension Pack fornece [funcionalidades adicionais](https://www.virtualbox.org/manual/ch01.html#intro-installing) e é lançado sob uma licença não-livre **disponível apenas para uso pessoal**. Para instalá-lo, o pacote [virtualbox-ext-oracle](https://aur.archlinux.org/packages/virtualbox-ext-oracle/) está disponível, e uma versão pré-compilada pode ser encontrada no repositório [seblu](/index.php/Unofficial_user_repositories#seblu "Unofficial user repositories").

Se você preferir usar o modo tradicional e manual: baixe a extensão manualmente e instale-a através da GUI (*Arquivo > Preferências > Extensões*) ou via `VBoxManage extpack install <.vbox-extpack>`, verifique se você tem um kit de ferramentas como [Polkit](/index.php/Polkit "Polkit") para conceder acesso privilegiado ao VirtualBox. A instalação desta extensão [requer acesso de root](https://www.virtualbox.org/ticket/8473).

### Front-ends

VirtualBox vem com três front-ends:

*   Se você quiser usar o VirtualBox com a GUI regular, use `VirtualBox`.
*   Se você deseja iniciar e gerenciar suas máquinas virtuais a partir da linha de comando, use o comando `VBoxSDL`, que fornece apenas uma janela simples para a máquina virtual, sem nenhuma sobreposição.
*   Se você quiser usar o VirtualBox sem executar qualquer GUI (por exemplo, em um servidor), use o comando `VBoxHeadless`. Com a extensão VRDP, você ainda pode acessar remotamente as exibições de suas máquinas virtuais.

Finalmente, você também pode usar [phpVirtualBox](/index.php/PhpVirtualBox "PhpVirtualBox") para administrar suas máquinas virtuais via uma interface web.

Confira o [manual do VirtualBox](https://www.virtualbox.org/manual) para aprender como criar máquinas virtuais.

**Atenção:** Se você pretende armazenar imagens de disco virtuais em um sistema de arquivos [Btrfs](/index.php/Btrfs "Btrfs"), antes de criar quaisquer imagens, considere a possibilidade de desabilitar [copy-on-write](/index.php/Btrfs#Copy-on-Write_(CoW) "Btrfs") (também conhecido como "cópia em gravação") para o destino diretório dessas imagens.

## Etapas de instalação para convidados Arch Linux

Inicialize a mídia de instalação do Arch por meio de uma das unidades virtuais da máquina virtual. Em seguida, conclua a instalação de um sistema Arch básico, conforme explicado no [Guia de instalação](/index.php/Guia_de_instala%C3%A7%C3%A3o "Guia de instalação").

### Instalação no modo EFI

Se você deseja instalar o Arch Linux no modo EFI dentro do VirtualBox, nas configurações da máquina virtual, escolha o item *Sistema* no painel à esquerda e a aba *Placa-mãe* no painel direito, e marque a caixa de seleção *Habilitar EFI (sistemas especiais apenas)*. Depois de selecionar o kernel no menu da mídia de instalação do Arch Linux, a mídia irá travar por um minuto ou dois e continuará a inicializar o kernel normalmente depois. Seja paciente.

Uma vez que o sistema e o gerenciador de boot sejam instalados, o VirtualBox tentará primeiro executar `/EFI/BOOT/BOOTX64.EFI` da [ESP](/index.php/ESP "ESP"). Se essa primeira opção falhar, o VirtualBox tentará o script de shell EFI `startup.nsh` da raiz da ESP. Isso significa que, para inicializar o sistema, você tem as seguintes opções:

*   [Iniciar o gerenciador de boot manualmente](/index.php/Unified_Extensible_Firmware_Interface#UEFI_Shell "Unified Extensible Firmware Interface") do shell EFI toda vez;
*   Mover o gerenciador de boot para o caminho padrão `/EFI/BOOT/BOOTX64.EFI`;
*   Criar um script chamado `startup.nsh` na raiz da ESP contendo o caminho para o aplicativo do gerenciador de boot, p.ex., `\EFI\grub\grubx64.efi`.
*   Inicializar diretamente da partição ESP usando um [script startup.nsh](/index.php/EFISTUB#Using_a_startup.nsh_script "EFISTUB").

Nem se incomode em usar o gerenciador de boot do VirtualBox (acessível com `F2` na inicialização), pois ele é cheio de bugs e está incompleto. Ele não armazena efivars configurados interativamente. Portanto, entradas EFI adicionadas a ele manualmente no firmware (acessado com `F12` no momento da inicialização) ou com [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) persistirão após a reinicialização, [mas são perdidas quando a VM é desligada](https://www.virtualbox.org/ticket/11177).

Veja também [UEFI Virtualbox installation boot problems](https://bbs.archlinux.org/viewtopic.php?id=158003).

### Instalar os adicionais para convidado

As [Adicionais para Convidado](https://www.virtualbox.org/manual/ch04.html) (*Guest Additions*) do VirtualBox fornecem drivers e aplicativos que otimizam o sistema operacional convidado, incluindo resolução de imagem aprimorada e melhor controle do mouse. Dentro do sistema convidado instalado, instale:

*   [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils) para utilitários de convidados do VirtualBox com suporte a X
*   [virtualbox-guest-utils-nox](https://www.archlinux.org/packages/?name=virtualbox-guest-utils-nox) para utilitários de convidados do VirtualBox sem suporte a X

Ambos os pacotes farão você escolher um pacote para fornecer módulos de convidados:

*   para o padrão kernel [linux](https://www.archlinux.org/packages/?name=linux) padrão, escolha [virtualbox-guest-modules-arch](https://www.archlinux.org/packages/?name=virtualbox-guest-modules-arch)
*   para outros [kernels](/index.php/Kernels "Kernels"), escolha [virtualbox-guest-dkms](https://www.archlinux.org/packages/?name=virtualbox-guest-dkms)

Para compilar os módulos do VirtualBox fornecidos pelo [virtualbox-guest-dkms](https://www.archlinux.org/packages/?name=virtualbox-guest-dkms), também será necessário instalar o(s) pacote(s) de headers apropriado(s) para o(s) seu(s) kernel(s) instalado(s) (p.ex., [linux-lts-headers](https://www.archlinux.org/packages/?name=linux-lts-headers) para [linux-lts](https://www.archlinux.org/packages/?name=linux-lts)). [[2]](https://lists.archlinux.org/pipermail/arch-dev-public/2016-March/027808.html) Quando o VirtualBox ou o kernel é atualizado, os módulos do kernel serão recompilados automaticamente graças ao hook do pacman de [DKMS](/index.php/DKMS "DKMS").

**Nota:**

*   Você pode alternativamente instalar os adicionais para convidado com o ISO do pacote [virtualbox-guest-iso](https://www.archlinux.org/packages/?name=virtualbox-guest-iso), desde que você o tenha instalado no sistema host. Para fazer isso, vá para o menu do dispositivo e clique em *Inserir imagem de CD dos Adicionais para Convidado*.
*   Para recompilar os módulos de kernel do vbox, execute `rcvboxdrv` como root.

Os adicionais para convidado em execução no seu convidado e o aplicativo VirtualBox em execução no seu host devem ter versões correspondentes, caso contrário, os adicionais para convidado (como a área de transferência compartilhada) podem parar de funcionar. Se você atualizar seu convidado (por exemplo, `pacman -Syu`), verifique se o aplicativo do VirtualBox neste host também é a versão mais recente. "Verificar por atualizações" na GUI do VirtualBox às vezes não é suficiente; verifique o site [VirtualBox.org](https://www.virtualbox.org/).

### Definir a melhor resolução de framebuffer

Normalmente, após a instalação dos Adicionais para Convidado, um convidado Arch em tela cheia executando o X será definido para a melhor resolução para o seu monitor; no entanto, o framebuffer do console virtual será configurado para uma resolução padrão, geralmente menor, detectada pelo driver VESA personalizado do VirtualBox.

Para usar os consoles virtuais na resolução ideal, o Arch precisa reconhecer essa resolução como válida, o que, por sua vez, exige que o VirtualBox passe essas informações para o sistema operacional convidado.

Primeiro, verifique se sua resolução desejada já não é reconhecida executando o comando:

```
hwinfo --framebuffer

```

Se a resolução ideal não aparecer, você precisará executar a ferramenta `VBoxManage` na máquina host e adicionar "resoluções extras" à sua máquina virtual (em um host Windows, vá para o diretório de instalação do VirtualBox para encontrar `VBoxManage.exe`). Por exemplo:

```
$ VBoxManage setextradata "Arch Linux" "CustomVideoMode1" "1360x768x24"

```

Os parâmetros "Arch Linux" e "1360x768x24" no exemplo acima devem ser substituídos pelo nome da sua VM e pela resolução desejada do framebuffer. Aliás, este comando permite definir até 16 resoluções extras ("CustomVideoMode1" a "CustomVideoMode16").

Depois, reinicie a máquina virtual e execute `hwinfo --framebuffer` mais uma vez para verificar se as novas resoluções foram reconhecidas pelo sistema convidado (o que não garante que todas elas funcionem, dependendo das limitações de hardware).

**Nota:** A partir do VirtualBox 5.2, `hwinfo --framebuffer` pode não mostrar qualquer saída, mas você ainda deve ser capaz de definir uma resolução personalizada seguindo este procedimento.

Finalmente, adicione um [parâmetro de kernel](/index.php/Kernel_parameter "Kernel parameter") `video=*resolução*` para definir o framebuffer para uma nova resolução, por exemplo:

```
video=1360x768

```

Além disso, você pode querer configurar seu [gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot") para usar a mesma resolução. Se você usa GRUB, veja [GRUB/Tips and tricks#Setting the framebuffer resolution](/index.php/GRUB/Tips_and_tricks#Setting_the_framebuffer_resolution "GRUB/Tips and tricks").

**Nota:** Nem o parâmetro do kernel `vga` nem as configurações de resolução do gerenciador de boot (p.ex., `GRUB_GFXPAYLOAD_LINUX` do GRUB) irão corrigir o framebuffer, uma vez que eles são substituídos pelo Kernel Mode Setting. A resolução do framebuffer deve ser definida pelo parâmetro do kernel `video` como descrito acima.

### Carregar os módulos de kernel do VirtualBox

Para carregar os módulos automaticamente, [habilite](/index.php/Habilite "Habilite") `vboxservice.service` que carrega os módulos e sincroniza a hora do sistema do convidado com o host.

Para carregar os módulos manualmente, digite:

```
# modprobe -a vboxguest vboxsf vboxvideo

```

[virtualbox-guest-dkms](https://www.archlinux.org/packages/?name=virtualbox-guest-dkms) usa `systemd-modules-load.service` para carregar seus módulos quando da inicialização.

**Nota:** Se você não quer que os módulos do VirtualBox sejam carregados no momento da inicialização, você tem que usar [mask](/index.php/Mask_(Portugu%C3%AAs) "Mask (Português)") para mascarar o padrão `/usr/lib/modules-load.d/virtualbox-guest-dkms.conf` criando um arquivo vazio (ou um link simbólico para `/dev/null`) com o mesmo nome em `/etc/modules-load.d/`.

### Iniciar os serviços de convidados do VirtualBox

Após o passo de instalação bastante grande lidando com módulos de kernel do VirtualBox, agora você precisa iniciar os serviços de convidado. Os serviços de convidado são na verdade apenas um executável binário chamado `VBoxClient` que irá interagir com o seu Sistema de Janelas X. O `VBoxClient` gerencia os seguintes recursos:

*   área de transferência compartilhada e arrastar e soltar entre o host e o convidado;
*   modo de janela *seamless*;
*   a exibição de convidado é automaticamente redimensionada de acordo com o tamanho da janela do convidado;
*   verificação da versão do host VirtualBox

Todos esses recursos podem ser ativados independentemente com seus flags dedicados:

```
$ VBoxClient --clipboard
$ VBoxClient --draganddrop
$ VBoxClient --seamless
$ VBoxClient --display
$ VBoxClient --checkhostversion
$ VBoxClient --vmsvga-x11

```

Observe que `VBoxClient` só pode ser chamado com um sinalizador por vez, cada chamada gerando um processo de serviço dedicado. Como um atalho, o script `VBoxClient-all` permite todos esses recursos.

[virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils) instala `/etc/xdg/autostart/vboxclient.desktop` que inicia `VBoxClient-all` ao iniciar a sessão. Se o seu [ambiente de desktop](/index.php/Ambiente_de_desktop "Ambiente de desktop") ou [gerenciador de janela](/index.php/Gerenciador_de_janela "Gerenciador de janela") não tiver suporte a [XDG Autostart](/index.php/XDG_Autostart_(Portugu%C3%AAs) "XDG Autostart (Português)"), você precisará configurar a inicialização automática -- veja [Autostarting#On desktop environment startup](/index.php/Autostarting#On_desktop_environment_startup "Autostarting") e [Autostarting#On window manager startup](/index.php/Autostarting#On_window_manager_startup "Autostarting") para mais detalhes.

O VirtualBox também pode sincronizar o tempo entre o host e o convidado, para isso, [inicie/habilite](/index.php/Inicie/habilite "Inicie/habilite") o `vboxservice.service`.

Agora, você deve ter um convidado Arch Linux. Observe que recursos como compartilhamento de área de transferência estão desabilitados por padrão no VirtualBox, e você precisará desabilitá-los nas configurações por VM se realmente quiser usá-los (p.ex., *Configurações > Geral > Avançado > Área de Transferência Compartilhada*).

### Aceleração de hardware

A aceleração de hardware pode ser ativada nas opções do VirtualBox. O gerenciador de exibição [GDM](/index.php/GDM "GDM") 3.16+ é conhecido por quebrar o suporte de aceleração de hardware. [[3]](https://bugzilla.gnome.org/show_bug.cgi?id=749390) Então, se você tiver problemas com a aceleração de hardware, experimente outro gerenciador de exibição (o lightdm parece funcionar bem). [[4]](https://bbs.archlinux.org/viewtopic.php?id=200025) [[5]](https://bbs.archlinux.org/viewtopic.php?pid=1607593#p1607593)

### Habilitar pastas compartilhadas

Pastas compartilhadas são gerenciadas no host, nas configurações da máquina virtual acessível através da GUI do VirtualBox, na aba *Pastas Compartilhadas*. Lá, *Caminho da pasta*, o nome do ponto de montagem identificado por *Nome da pasta* e opções como *Apenas para Leitura*, *Montar Automaticamente* e *Tornar Permanente* podem ser especificados. Esses parâmetros podem ser definidos com o utilitário de linha de comando `VBoxManage`. Consulte [para mais detalhes](https://www.virtualbox.org/manual/ch04.html#sharedfolders).

Não importa qual método você usará para montar sua pasta, todos os métodos requerem algumas etapas primeiro.

Para evitar este problema, `/sbin/mount.vboxsf: mounting failed with the error: No such device`, certifique-se de que o módulo do kernel `vboxsf` esteja carregado corretamente. Deveria ser, já que ativamos todos os módulos do kernel do convidado anteriormente.

Duas etapas adicionais são necessárias para que o ponto de montagem seja acessível a partir de usuários que não sejam root:

*   o pacote [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils) criou um grupo `vboxsf` (feito em uma etapa anterior);
*   seu usuário deve estar no [grupo de usuários](/index.php/Grupo_de_usu%C3%A1rios "Grupo de usuários") `vboxsf`.

#### Montagem manual

Use o seguinte comando para montar sua pasta em seu convidado Arch Linux:

```
# mount -t vboxsf *nome_da_pasta_compartilhada* *ponto_de_montagem_em_sistema_convidado*

```

sendo que `*nome_da_pasta_compartilhada*` é o *Nome da Pasta* atribuído pelo hipervisor quando o compartilhamento foi criado.

O sistema de arquivos vboxsf oferece outras opções que podem ser exibidas com esse comando:

```
# mount.vboxsf

```

Por exemplo, se o usuário não estava no grupo *vboxsf*, nós poderíamos ter usado este comando para lhe dar acesso ou ponto de montagem:

```
# mount -t vboxsf -o uid=1000,gid=1000 home /mnt

```

sendo que `*uid*` e `*gid*` são valores correspondentes para os usuários aos quais queremos dar acesso. Esses valores são obtidos a partir do comando `id` executado com este usuário.

#### Montagem automática

**Note:** A montagem automática requer que o `vboxservice.service` esteja [habilitado](/index.php/Habilita "Habilita")/[iniciado](/index.php/Inicia "Inicia").

Para que o recurso de montagem automática funcione, você deve marcar a caixa de seleção de *Montagem Automática* na GUI ou usar o argumento opcional `--automount` com o comando `VBoxManage sharedfolder`.

A pasta compartilhada agora deve aparecer em `/media/sf_*nome_da_pasta_compartilhada*`. Se os usuários em `media` não puderem acessar as pastas compartilhadas, verifique se `media` tem permissões `755` ou se tem propriedade de grupo `vboxsf` se estiver usando permissão `750`. Atualmente, esse não é o padrão se a mídia for criada instalando o [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils).

Você pode usar links simbólicos para ter um acesso mais conveniente e evitar de navegar naquele diretório, p.ex.:

```
$ ln -s /media/sf_*nome_da_pasta_compartilhada* ~/*meus_documentos*

```

#### Montar na inicialização

Você pode montar seu diretório com [fstab](/index.php/Fstab "Fstab"). No entanto, para evitar problemas de inicialização com o systemd, `noauto,x-systemd.automount` deve ser adicionado ao `/etc/fstab`. Dessa forma, as pastas compartilhadas são montadas somente quando esses pontos de montagem são acessados e não durante a inicialização. Isso pode evitar alguns problemas, especialmente se os adicionais para convidados não forem carregados ainda quando o systemd ler fstab e montar as partições.

```
*nomePastaCompartilhada*  */caminho/para/PontoMontagemNaMáquinaConvidado*  vboxsf  uid=*usuário*,gid=*grupo*,rw,dmode=700,fmode=600,noauto,x-systemd.automount

```

*   `*nomePastaCompartilhada*`: o valor do menu *Configurações > Pastas Compartilhadas > Editar > Nome da Pasta* da máquina virtual. Esse valor pode ser diferente do nome do nome real da pasta na máquina host. Para ver as *Configurações* da máquina virtual, vá para o aplicativo VirtualBox do sistema host, selecione a máquina virtual correspondente e clique em *Configurações*.
*   `*/caminho/para/PontoMontagemNaMáquinaConvidado*`: se não existir, esse diretório deve ser criado manualmente (por exemplo, usando [mkdir](/index.php/Utilit%C3%A1rios_principais#Essenciais "Utilitários principais")).
*   `dmode`/`fmode` são permissões de diretório/arquivo para diretórios/arquivos dentro `*/caminho/para/PontoMontagemNaMáquinaConvidado*`.

Até 2012-08-02, mount.vboxsf não possui suporte à opção `nofail`:

```
*desktop*  */media/desktop*  vboxsf  uid=*user*,gid=*group*,rw,dmode=700,fmode=600,nofail  0  0

```

### SSH do host para o convidado

A aba de rede das configurações da máquina virtual contém, em *Avançado*, uma ferramenta para criar o encaminhamento de porta. É possível usá-lo para encaminhar a porta ssh do convidado `22` para uma porta do host, por exemplo, `3022`:

```
user@host$ ssh -p 3022 $USER@localhost

```

vai estabelecer uma conexão entre host e o convidado.

#### SSHFS como alternativa à pasta compartilhada

Usando este encaminhamento de porta e o sshfs, é simples montar o sistema de arquivos do convidado no do host:

```
user@host$ sshfs -p 3022 $USER@localhost:$HOME ~/pasta_compartilhada

```

e transferir arquivos entre ambos.

## Gerenciamento de discos virtuais

Veja também [VirtualBox/Tips and tricks#Import/export VirtualBox virtual machines from/to other hypervisors](/index.php/VirtualBox/Tips_and_tricks#Import/export_VirtualBox_virtual_machines_from/to_other_hypervisors "VirtualBox/Tips and tricks").

### Formatos suportados pelo VirtualBox

VirtualBox possui suporte aos seguintes formatos de disco virtual:

*   **VDI**: O Virtual Disk Image é o próprio contêiner aberto do VirtualBox usado por padrão quando você cria uma máquina virtual com o VirtualBox.
*   **VMDK**: O Virtual Machine Disk foi inicialmente desenvolvido pela VMware para seus produtos. A especificação foi inicialmente de código fechado, mas tornou-se agora um formato aberto que é totalmente suportado pelo VirtualBox. Este formato oferece a possibilidade de ser dividido em vários arquivos de 2GB. Esse recurso é especialmente útil se você quiser armazenar a máquina virtual em máquinas que não suportam arquivos muito grandes. Outros formatos, excluindo o formato HDD da Parallels, não fornecem esse recurso equivalente.
*   **VHD**: O Virtual Hard Disk é o formato usado pela Microsoft no Windows Virtual PC e no Hyper-V. Se você pretende usar qualquer um desses produtos da Microsoft, terá que escolher esse formato.

**Dica:** Desde o Windows 7, esse formato pode ser montado diretamente sem qualquer aplicativo adicional.

*   **VHDX** (somente leitura): Esta é a versão estendida ("e**X**tended") do formato Virtual Hard Disk desenvolvido pela Microsoft, que foi lançado em 2012-09-04 com o Hyper-V 3.0 vindo com o Windows Server 2012\. Esta nova versão do formato de disco oferece desempenho aprimorado (melhor bloco alinhamento), tamanho de blocos maiores e suporte a journal, o que resulta em resiliência de falha de energia. O VirtualBox [deve ter suporte este formato somente leitura](https://www.virtualbox.org/manual/ch15.html#idp63002176).
*   **HDD** (versão 2): O formato HDD é desenvolvido pela Parallels Inc e usado em suas soluções de hipervisor, como o Parallels Desktop for Mac. Versões mais recentes deste formato (ou seja, 3 e 4) não são suportadas devido à falta de documentação para este formato proprietário.
    **Nota:** Há atualmente uma controvérsia a cerca do suporte à versão 2 do formato. Enquanto o manual oficial do VirtualBox [só relata ter suporte à segunda versão do formato de arquivo HDD](https://www.virtualbox.org/manual/ch05.html#vdidetails), contribuidores do Wikipédia [relatam que a primeira versão pode funcionar também](https://en.wikipedia.org/wiki/Comparison_of_platform_virtual_machines#Image_type_compatibility "wikipedia:Comparison of platform virtual machines"). Ajuda é bem-vinda se você puder realizar alguns testes com a primeira versão do formato HDD.

*   **QED**: O formato de disco aprimorado do QEMU é um formato de arquivo antigo para o QEMU, outro hipervisor de código aberto e software livre. Este formato foi projetado a partir de 2010 de forma a fornecer uma alternativa superior ao QCOW2 e outros. Esse formato apresenta um caminho de E/S totalmente assíncrono, integridade de dados forte, arquivos de apoio e arquivos esparsos. Há suprote ao formato QED apenas para compatibilidade com máquinas virtuais criadas com versões antigas do QEMU.
*   **QCOW**: O formato QEMU Copy On Write é o formato atual do QEMU. O formato QCOW possui suporte a compressão e criptografia transparentes baseadas em zlib (o último é falho e não é recomendado). O QCOW está disponível em duas versões: QCOW e QCOW2\. QCOW2 tende a substituir o primeiro. O QCOW possui [atualmente total suporte pelo VirtualBox](https://www.virtualbox.org/manual/ch15.html#idp63002176). O QCOW2 vem em duas revisões: QCOW2 0.10 e QCOW2 1.1 (que é o padrão quando você cria um disco virtual com o QEMU). O VirtualBox não posssui suporte a QCOW2.
*   **OVF**: O Open Virtualization Format é um formato aberto que foi projetado para interoperabilidade e distribuição de máquinas virtuais entre diferentes hipervisores. O VirtualBox possui suporte a todas as revisões deste formato através do [recurso de importação/exportação do VBoxManage](https://www.virtualbox.org/manual/ch08.html#idp55423424), mas com [limitações conhecidas](https://www.virtualbox.org/manual/ch14.html#KnownProblems).
*   **RAW**: Esse é o modo quando o disco virtual é exposto diretamente ao disco sem estar contido em um contêiner de formato de arquivo específico. O VirtualBox possui suporte a esse recurso de várias maneiras: convertendo disco RAW [para um formato específico](https://www.virtualbox.org/manual/ch08.html#idp59139136) ou [clonando um disco para RAW](https://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi) ou usando diretamente um arquivo VMDK [que aponta para um disco físico ou um arquivo simples](https://www.virtualbox.org/manual/ch09.html#idp57804112).

### Conversão de formato de imagem de disco

[VBoxManage clonehd](https://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi) pode ser usado para converter entre VDI, VMDK, VHD e RAW.

```
$ VBoxManage clonehd *arquivo_entrada* *arquivo_saída* --format *formato_saída*

```

Por exemplo, para converter VDI em VMDK:

```
$ VBoxManage clonehd *origem.vdi* *destino.vmdk* --format VMDK

```

#### QCOW

O VirtualBox não possui suporte ao formato de imagem de disco QCOW2 do [QEMU](/index.php/QEMU "QEMU"). Para usar uma imagem de disco QCOW2 com o VirtualBox, você precisa convertê-la, o que você pode fazer com o comando [qemu](https://www.archlinux.org/packages/?name=qemu) do `qemu-img`. `qemu-img` pode converter QCOW para/de VDI, VMDK, VHDX, RAW e vários outros formatos (que você pode ver executando `qemu-img --help`).

```
$ qemu-img convert -O *formato_saída* *arquivo_entrada* *arquivo_saída*

```

Por exemplo, para converter QCOW2 em VDI:

```
$ qemu-img convert -O vdi *origem.qcow2* *destino.vdi*

```

**Dica:** O parâmetro `-p` é usado para obter o progresso da tarefa de conversão.

Há duas revisões do QCOW2: 0.10 e 1.1\. Você pode especificar a revisão a ser usada com `-o compat=*revisão*`.

### Montar discos virtuais

#### VDI

A montagem de imagens VDI só funciona com imagens de tamanho fixo (também imagens estáticas); imagens dinâmicas (alocação dinâmica de tamanho) não são facilmente montáveis.

O deslocamento da partição (dentro da VDI) é necessário, em seguida, adicione o valor de `offData` a `32256` (por exemplo, 69632 + 32256 = 101888):

```
$ VBoxManage internalcommands dumphdinfo <armazenamento.vdi> | grep "offData"

```

O armazenamento pode agora ser montado com:

```
# mount -t ext4 -o rw,noatime,noexec,loop,offset=101888 <armazenamento.vdi> /mntpoint/

```

Você também pode usar o script [mount.vdi](https://github.com/pld-linux/VirtualBox/blob/master/mount.vdi), o qual você pode usar como (instale o script em `/usr/bin/`):

```
# mount -t vdi -o fstype=ext4,rw,noatime,noexec *local_arquivo_vdi* */mnt/*

```

Alternativamente, você pode usar o módulo de kernel do [qemu](https://www.archlinux.org/packages/?name=qemu) que pode fazer essa [atribuição](http://bethesignal.org/blog/2011/01/05/how-to-mount-virtualbox-vdi-image/):

```
# modprobe nbd max_part=16
# qemu-nbd -c /dev/nbd0 <armazenamento.vdi>
# mount /dev/nbd0p1 /mnt/dir/
# # to unmount:
# umount /mnt/dir/
# qemu-nbd -d /dev/nbd0

```

Se os nós da partição não forem propagados, tente usar `partprobe/dev/nbd0`; caso contrário, uma partição VDI pode ser mapeada diretamente para um nó por: `qemu-nbd -P 1 -c /dev/nbd0 <armazenamento.vdi>`.

#### VHD

Como em VDI, imagens VHD podem ser montadas com o módulo nbd do [QEMU](/index.php/QEMU "QEMU"):

```
# modprobe nbd
# qemu-nbd -c /dev/nbd0 *armazenamento*.vhd
# mount /dev/nbd0p1 /mnt

```

Para desmontar:

```
# umount /mnt
# qemu-nbd -d /dev/nbd0

```

### Compactar discos virtuais

Compacting virtual disks only works with *.vdi* files and basically consists of the following steps.

Boot your virtual machine and remove all bloat manually or by using cleaning tools like [bleachbit](https://www.archlinux.org/packages/?name=bleachbit) which is [available for Windows systems too](http://bleachbit.sourceforge.net/download/windows).

Wiping free space with zeroes can be achieved with several tools:

*   If you were previously using Bleachbit, check the checkbox *System > Free disk space* in the GUI, or use `bleachbit -c system.free_disk_space` in CLI;
*   On UNIX-based systems, by using `dd` or preferably [dcfldd](https://www.archlinux.org/packages/?name=dcfldd) (see [here](http://superuser.com/a/355322) to learn the differences):

	 `# dcfldd if=/dev/zero of=*/fillfile* bs=4M` 

	When `fillfile` reaches the limit of the partition, you will get a message like `1280 blocks (5120Mb) written.dcfldd:: No space left on device`. This means that all of the user-space and non-reserved blocks of the partition will be filled with zeros. Using this command as root is important to make sure all free blocks have been overwritten. Indeed, by default, when using partitions with ext filesystem, a specified percentage of filesystem blocks is reserved for the super-user (see the `-m` argument in the `mkfs.ext4` man pages or use `tune2fs -l` to see how much space is reserved for root applications).

	When the aforementioned process has completed, you can remove the file `*fillfile*` you created.

*   On Windows, there are two tools available:
    *   `sdelete` from the [Sysinternals Suite](http://technet.microsoft.com/en-us/sysinternals/bb842062.aspx), type `sdelete -s -z *c:*`, where you need to reexecute the command for each drive you have in your virtual machine;
    *   or, if you love scripts, there is a [PowerShell solution](http://blog.whatsupduck.net/2012/03/powershell-alternative-to-sdelete.html), but which still needs to be repeated for all drives.

	 `PS> ./Write-ZeroesToFreeSpace.ps1 -Root *c:\* -PercentFree 0` 

**Note:** This script must be run in a PowerShell environment with administrator privileges. By default, scripts cannot be run, ensure the execution policy is at least on `RemoteSigned` and not on `Restricted`. This can be checked with `Get-ExecutionPolicy` and the required policy can be set with `Set-ExecutionPolicy RemoteSigned`.

Once the free disk space have been wiped, shut down your virtual machine.

The next time you boot your virtual machine, it is recommended to do a filesystem check.

*   On UNIX-based systems, you can use `fsck` manually;
    *   On GNU/Linux systems, and thus on Arch Linux, you can force a disk check at boot [thanks to a kernel boot parameter](/index.php/Fsck#Forcing_the_check "Fsck");
*   On Windows systems, you can use:
    *   either `chkdsk *c:* /F` where `*c:*` needs to be replaced by each disk you need to scan and fix errors;
    *   or `FsckDskAll` [from here](http://therightstuff.de/2009/02/14/ChkDskAll-ChkDsk-For-All-Drives.aspx) which is basically the same software as `chkdsk`, but without the need to repeat the command for all drives;

Now, remove the zeros from the *.vdi* file with [VBoxManage modifyhd](https://www.virtualbox.org/manual/ch08.html#vboxmanage-modifyvdi):

```
$ VBoxManage modifyhd *your_disk.vdi* --compact

```

**Note:** If your virtual machine has snapshots, you need to apply the above command on each `.vdi` files you have.

### Aumentar discos virtuais

#### Procedimento geral

If you are running out of space due to the small hard drive size you selected when you created your virtual machine, the solution adviced by the VirtualBox manual is to use [VBoxManage modifyhd](https://www.virtualbox.org/manual/ch08.html#vboxmanage-modifyvdi). However this command only works for VDI and VHD disks and only for the dynamically allocated variants. If you want to resize a fixed size virtual disk disk too, read on this trick which works either for a Windows or UNIX-like virtual machine.

First, create a new virtual disk next to the one you want to increase:

```
$ VBoxManage createhd -filename *new.vdi* --size *10000*

```

where size is in MiB, in this example 10000MiB ~= 10GiB, and *new.vdi* is name of new hard drive to be created.

**Note:** By default, this command uses the *Standard* (corresponding to dynamic allocated) file format variant and thus will not use the same file format variant as your source virtual disk. If your *old.vdi* has a fixed size and you want to keep this variant, add the parameter `--variant Fixed`.

Next, the old virtual disk needs to be cloned to the new one which this may take some time:

```
$ VBoxManage clonehd *old.vdi* *new.vdi* --existing

```

Detach the old hard drive and attach new one, replace all mandatory italic arguments by your own:

```
$ VBoxManage storageattach *VM_name* --storagectl *SATA* --port *0* --medium none
$ VBoxManage storageattach *VM_name* --storagectl *SATA* --port *0* --medium *new.vdi* --type hdd

```

To get the storage controller name and the port number, you can use the command `VBoxManage showvminfo *VM_name*`. Among the output you will get such a result (what you are looking for is in italic):

```
[...]
Storage Controller Name (0):            IDE
Storage Controller Type (0):            PIIX4
Storage Controller Instance Number (0): 0
Storage Controller Max Port Count (0):  2
Storage Controller Port Count (0):      2
Storage Controller Bootable (0):        on
Storage Controller Name (1):            SATA
Storage Controller Type (1):            IntelAhci
Storage Controller Instance Number (1): 0
Storage Controller Max Port Count (1):  30
Storage Controller Port Count (1):      1
Storage Controller Bootable (1):        on
IDE (1, 0): Empty
*SATA* (*0*, 0): /home/wget/IT/Virtual_machines/GNU_Linux_distributions/ArchLinux_x64_EFI/Snapshots/{6bb17af7-e8a2-4bbf-baac-fbba05ebd704}.vdi (UUID: 6bb17af7-e8a2-4bbf-baac-fbba05ebd704)
[...]

```

Download [GParted live image](http://gparted.org/download.php) and mount it as a virtual CD/DVD disk file, boot your virtual machine, increase/move your partitions, umount GParted live and reboot.

**Note:** On GPT disks, increasing the size of the disk will result in the backup GPT header not being at the end of the device. GParted will ask to fix this, click on *Fix* both times. On MBR disks, you do not have such a problem as this partition table as no trailer at the end of the disk.

Finally, unregister the virtual disk from VirtualBox and remove the file:

```
$ VBoxManage closemedium disk *old.vdi*
$ rm *old.vdi*

```

#### Aumentando o tamanho de discos VDI

If your disk is a VDI one, run:

```
$ VBoxManage modifyhd *your_virtual_disk.vdi* --resize *the_new_size*

```

Then jump back to the Gparted step, to increase the size of the partition on the virtual disk.

### Substituir um disco virtual manualmente a partir do arquivo .vbox

If you think that editing a simple *XML* file is more convenient than playing with the GUI or with `VBoxManage` and you want to replace (or add) a virtual disk to your virtual machine, in the *.vbox* configuration file corresponding to your virtual machine, simply replace the GUID, the file location and the format to your needs:

 `ArchLinux_vm.vbox`  `<HardDisk uuid="*{670157e5-8bd4-4f7b-8b96-9ee412a712b5}*" location="*ArchLinux_vm.vdi*" format="*VDI*" type="Normal"/>` 

then in the `<AttachedDevice>` sub-tag of `<StorageController>`, replace the GUID by the new one.

 `ArchLinux_vm.vbox` 
```
<AttachedDevice type="HardDisk" port="0" device="0">
  <Image uuid="*{670157e5-8bd4-4f7b-8b96-9ee412a712b5}*"/>
</AttachedDevice>
```

**Note:** If you do not know the GUID of the drive you want to add, you can use the `VBoxManage showhdinfo *file*`. If you previously used `VBoxManage clonehd` to copy/convert your virtual disk, this command should have outputted the GUID just after the copy/conversion completed. Using a random GUID does not work, as each [UUID is stored inside each disk image](http://www.virtualbox.org/manual/ch05.html#cloningvdis).

#### Transferir entre host Linux e outro SO

The information about path to harddisks and the snapshots is stored between `<HardDisks> .... </HardDisks>` tags in the file with the *.vbox* extension. You can edit them manually or use this script where you will need change only the path or use defaults, assumed that *.vbox* is in the same directory with a virtual harddisk and the snapshots folder. It will print out new configuration to stdout.

```
#!/bin/bash
NewPath="${PWD}/"
Snapshots="Snapshots/"
Filename="$1"

 awk -v SetPath="$NewPath" -v SnapPath="$Snapshots" '{if(index($0,"<HardDisk uuid=") != 0){A=$3;split(A,B,"=");
L=B[2];
 gsub(/\"/,"",L);
  sub(/^.*\//,"",L);
  sub(/^.*\\/,"",L);
 if(index($3,"{") != 0){SnapS=SnapPath}else{SnapS=""};
  print $1" "$2" location="\"SetPath SnapS L"\" "$4" "$5}
else print $0}' "$Filename"
```

**Note:**

*   If you will prepare virtual machine for use in Windows host then in the path name end you should use backslash \ instead of / .
*   The script detects snapshots by looking for `{` in the file name.
*   To make it run on a new host you will need to add it first to the register by clicking on **Machine -> Add...** or use hotkeys Ctrl+A and then browse to *.vbox* file that contains configuration or use command line `VBoxManage registervm *filename*.vbox`

### Clonar um disco virtual e atribuição d eum novo UUID a ele

UUIDs are widely used by VirtualBox. Each virtual machines and each virtual disk of a virtual machine must have a different UUID. When you launch a virtual machine in VirtualBox, VirtualBox will keep track of all UUIDs of your virtual machine instance. See the [VBoxManage list](http://www.virtualbox.org/manual/ch08.html#vboxmanage-list) to list the items registered with VirtualBox.

If you cloned a virtual disk manually by copying the virtual disk file, you will need to assign a new UUID to the cloned virtual drive if you want to use the disk in the same virtual machine or even in another (if that one has already been opened, and thus registered, with VirtualBox).

You can use this command to assign a new UUID to a virtual disk:

```
$ VBoxManage internalcommands sethduuid */path/to/disk.vdi*

```

**Tip:** To avoid copying the virtual disk and assigning a new UUID to your file manually you can use [VBoxManage clonehd](http://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi).

**Note:** The commands above support all [virtual disk formats supported by VirtualBox](#Formats_supported_by_VirtualBox).

## Dicas e truques

For advanced configuration, see [VirtualBox/Tips and tricks](/index.php/VirtualBox/Tips_and_tricks "VirtualBox/Tips and tricks").

## Solução de problemas

### Teclado e mouse estão travados na máquina virtual

This means your virtual machine has captured the input of your keyboard and your mouse. Simply press the right `Ctrl` key and your input should control your host again.

To control transparently your virtual machine with your mouse going back and forth your host, without having to press any key, and thus have a seamless integration, install the guest additions inside the guest. Read from the [[