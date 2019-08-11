**Status de tradução:** Esse artigo é uma tradução de [VirtualBox](/index.php/VirtualBox "VirtualBox"). Data da última tradução: 2019-08-02\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=VirtualBox&diff=0&oldid=577754) na versão em inglês.

Artigos relacionados

*   [VirtualBox/Dicas e truques](/index.php/VirtualBox/Tips_and_tricks "VirtualBox/Tips and tricks")
*   [Category:Hypervisors (Português)](/index.php/Category:Hypervisors_(Portugu%C3%AAs) "Category:Hypervisors (Português)")
*   [PhpVirtualBox](/index.php/PhpVirtualBox "PhpVirtualBox")
*   [RemoteBox](/index.php/RemoteBox "RemoteBox")
*   [Movendo uma instalação existente para dentro (ou fora) de uma máquina virtual](/index.php/Movendo_uma_instala%C3%A7%C3%A3o_existente_para_dentro_(ou_fora)_de_uma_m%C3%A1quina_virtual "Movendo uma instalação existente para dentro (ou fora) de uma máquina virtual")

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
    *   [3.7 Clonar um disco virtual e atribuição de um novo UUID a ele](#Clonar_um_disco_virtual_e_atribuição_de_um_novo_UUID_a_ele)
*   [4 Dicas e truques](#Dicas_e_truques)
*   [5 Solução de problemas](#Solução_de_problemas)
    *   [5.1 Teclado e mouse estão travados na máquina virtual](#Teclado_e_mouse_estão_travados_na_máquina_virtual)
    *   [5.2 Nenhuma opção para cliente de SO 64 bits](#Nenhuma_opção_para_cliente_de_SO_64_bits)
    *   [5.3 VirtualBox GUI não corresponde ao tema GTK do hospedeiro](#VirtualBox_GUI_não_corresponde_ao_tema_GTK_do_hospedeiro)
    *   [5.4 Não é possível enviar Ctrl+Alt+Fn para o convidado](#Não_é_possível_enviar_Ctrl+Alt+Fn_para_o_convidado)
    *   [5.5 Subsistema USB não funciona](#Subsistema_USB_não_funciona)
    *   [5.6 Modem USB não funciona no hospedeiro](#Modem_USB_não_funciona_no_hospedeiro)
    *   [5.7 Dispositivo USB trava o convidado](#Dispositivo_USB_trava_o_convidado)
    *   [5.8 Acesso a porta serial pelo convidado](#Acesso_a_porta_serial_pelo_convidado)
    *   [5.9 Convidado trava após iniciar o Xorg](#Convidado_trava_após_iniciar_o_Xorg)
    *   [5.10 Modo tela cheia mostra uma tela branca](#Modo_tela_cheia_mostra_uma_tela_branca)
    *   [5.11 Hospedeiro trava ao iniciar máquina virtual](#Hospedeiro_trava_ao_iniciar_máquina_virtual)
    *   [5.12 Convidados Linux têm áudio lento/distorcido](#Convidados_Linux_têm_áudio_lento/distorcido)
    *   [5.13 Microfone analógico não funciona](#Microfone_analógico_não_funciona)
    *   [5.14 Microfone não funciona após atualização](#Microfone_não_funciona_após_atualização)
    *   [5.15 Problemas com imagens convertidas para ISO](#Problemas_com_imagens_convertidas_para_ISO)
    *   [5.16 Falha ao criar a interface de rede interna](#Falha_ao_criar_a_interface_de_rede_interna)
    *   [5.17 Falha ao inserir módulo](#Falha_ao_inserir_módulo)
    *   [5.18 VBOX_E_INVALID_OBJECT_STATE (0x80BB0007)](#VBOX_E_INVALID_OBJECT_STATE_(0x80BB0007))
    *   [5.19 NS_ERROR_FAILURE e itens de menu em falta](#NS_ERROR_FAILURE_e_itens_de_menu_em_falta)
    *   [5.20 Arch: script pacstrap falhando](#Arch:_script_pacstrap_falhando)
    *   [5.21 OpenBSD inutilizável quando instruções de virtualização estão indisponíveis](#OpenBSD_inutilizável_quando_instruções_de_virtualização_estão_indisponíveis)
    *   [5.22 Hospedeiro Windows: VERR_ACCESS_DENIED](#Hospedeiro_Windows:_VERR_ACCESS_DENIED)
    *   [5.23 Windows: "O caminho especificado não existe. Verifique o caminho e tente novamente."](#Windows:_"O_caminho_especificado_não_existe._Verifique_o_caminho_e_tente_novamente.")
    *   [5.24 Erro no Windows 8.x com código 0x000000C4](#Erro_no_Windows_8.x_com_código_0x000000C4)
    *   [5.25 Windows 8, 8.1 ou 10 falha em instalar, inicializar ou tem erro "ERR_DISK_FULL"](#Windows_8,_8.1_ou_10_falha_em_instalar,_inicializar_ou_tem_erro_"ERR_DISK_FULL")
    *   [5.26 WinXP: Profundidade de bits não pode ser maior que 16](#WinXP:_Profundidade_de_bits_não_pode_ser_maior_que_16)
    *   [5.27 Windows: Oscilação da tela se a aceleração 3D estiver ativada](#Windows:_Oscilação_da_tela_se_a_aceleração_3D_estiver_ativada)
    *   [5.28 Nenhuma aceleração 3D de hardware no convidado Arch Linux](#Nenhuma_aceleração_3D_de_hardware_no_convidado_Arch_Linux)
    *   [5.29 Não é possível iniciar o VirtualBox no Wayland: Falha de segmentação](#Não_é_possível_iniciar_o_VirtualBox_no_Wayland:_Falha_de_segmentação)

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

Uma vez que o sistema e o gerenciador de boot sejam instalados, o VirtualBox tentará primeiro executar `/EFI/BOOT/BOOTX64.EFI` da [ESP](/index.php/ESP_(Portugu%C3%AAs) "ESP (Português)"). Se essa primeira opção falhar, o VirtualBox tentará o script de shell EFI `startup.nsh` da raiz da ESP. Isso significa que, para inicializar o sistema, você tem as seguintes opções:

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

Se a aceleração de hardware não funcionar como esperado, tente alterar a opção *Controladora Gráfica* localizada na aba *Tela* nas opções *Monitor* das configurações da GUI. Parece que, dependendo do tipo de GPU do hospedeiro, nem todos as controladoras emuladas funcionam igualmente bem.

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
# mount -t vboxsf -o gid=vboxsf *nome_da_pasta_compartilhada* *ponto_de_montagem_em_sistema_convidado*

```

sendo que `*nome_da_pasta_compartilhada*` é o *Nome da Pasta* atribuído pelo hipervisor quando o compartilhamento foi criado.

Se o usuário não estiver no grupo *vboxsf*, para dar acesso ao nosso ponto de montagem, podemos especificar as opções [mount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8) `uid=` e `gid=` com os valores correspondentes do usuário. Estes valores podem ser obtidos do comando `id` executado contra este usuário. Por exemplo:

```
# mount -t vboxsf -o uid=1000,gid=1000 home /mnt

```

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

A compactação de discos virtuais só funciona com arquivos *.vdi* e consiste basicamente nas seguintes etapas.

Inicialize sua máquina virtual e remova todo o inchaço manualmente ou usando ferramentas de limpeza como [bleachbit](https://www.archlinux.org/packages/?name=bleachbit) que está [disponível para sistemas Windows também](http://bleachbit.sourceforge.net/download/windows).

A limpeza do espaço livre com zeros pode ser alcançado por meio de várias ferramentas:

*   Se você estava usando Bleachbit anteriormente, marque a caixa de seleção *Sistema > Espaço livre em disco* na GUI, ou use `bleachbit -c system.free_disk_space` na CLI;
*   Em sistemas baseados em UNIX, usando `dd` ou preferencialmente [dcfldd](https://www.archlinux.org/packages/?name=dcfldd) (veja [aqui](http://superuser.com/a/355322) para aprender as diferenças):

	 `# dcfldd if=/dev/zero of=*/arquivo_para_preencher* bs=4M` 

Quando `arquivo_para_preencher` atingir o limite da partição, você receberá uma mensagem como `1280 blocks (5120Mb) written.dcfldd:: No space left on device`. Isso significa que todos os blocos de espaço do usuário e não reservados da partição serão preenchidos com zeros. Usar esse comando como root é importante para garantir que todos os blocos livres tenham sido sobrescritos. De fato, por padrão, ao usar partições com sistema de arquivos ext, uma porcentagem especificada de blocos do sistema de arquivos é reservada para o superusuário (veja o argumento `-m` nas páginas man do `mkfs.ext4` ou use `tune2fs -l` para ver quanto espaço é reservado para aplicativos da raiz).

	Quando o processo supramencionado estiver concluído, você poderá remover o arquivo `*arquivo_para_preencher*` que você criou.

*   No Windows, há duas ferramentas disponíveis:
    *   `sdelete` da [Sysinternals Suite](http://technet.microsoft.com/en-us/sysinternals/bb842062.aspx), digite `sdelete -s -z *c:*`, sendo que você precisa reexecutar o comando para cada unidade existente em sua máquina virtual;
    *   ou, se você gosta de scripts, há uma [solução em PowerShell](http://blog.whatsupduck.net/2012/03/powershell-alternative-to-sdelete.html), mas que ainda precisa ser repetida para todas as unidades.

	 `PS> ./Write-ZeroesToFreeSpace.ps1 -Root *c:\* -PercentFree 0` 

**Nota:** Este script deve ser executado em um ambiente do PowerShell com privilégios de administrador. Por padrão, os scripts não podem ser executados, certifique-se de que a política de execução esteja, pelo menos, em `RemoteSigned` e não em `Restricted`. Isso pode ser verificado com `Get-ExecutionPolicy` e a política necessária pode ser definida com `Set-ExecutionPolicy RemoteSigned`.

Uma vez que o espaço livre em disco tenha sido apagado, desligue sua máquina virtual.

Na próxima vez que você inicializar sua máquina virtual, é recomendável fazer uma verificação do sistema de arquivos.

*   Em sistemas baseados em UNIX, você pode usar `fsck` manualmente;
    *   Nos sistemas GNU/Linux e, portanto, no Arch Linux, você pode forçar uma verificação de disco na inicialização [graças a um parâmetro de inicialização do kernel](/index.php/Fsck#Forcing_the_check "Fsck");
*   Nos sistemas Windows, você pode usar:
    *   `chkdsk *c:* /F` sendo que `*c:*` precisa ser substituído por cada disco que você precisa verificar e corrigir erros;
    *   ou `FsckDskAll` [daqui](http://therightstuff.de/2009/02/14/ChkDskAll-ChkDsk-For-All-Drives.aspx) que é basicamente o mesmo software que `chkdsk`, mas sem a necessidade de repetir o comando para todas as unidades;

Agora, remova os zeros do arquivo *.vdi* com [VBoxManage modifyhd](https://www.virtualbox.org/manual/ch08.html#vboxmanage-modifyvdi):

```
$ VBoxManage modifyhd *seu_disco.vdi* --compact

```

**Nota:** Se sua máquina virtual tiver snapshots, você precisará aplicar o comando acima em cada arquivo `.vdi` que você possui.

### Aumentar discos virtuais

#### Procedimento geral

Se você está ficando sem espaço devido ao pequeno tamanho do disco rígido que você selecionou quando criou sua máquina virtual, a solução recomendada pelo manual do VirtualBox é usar [VBoxManage modifyhd](https://www.virtualbox.org/manual/ch08.html#vboxmanage-modifyvdi). No entanto, esse comando só funciona para discos VDI e VHD e apenas para as variantes alocadas dinamicamente. Se você quiser redimensionar um disco de disco virtual de tamanho fixo também, leia este truque que funciona para uma máquina virtual do Windows ou UNIX.

Primeiro, crie um novo disco virtual próximo ao que você deseja aumentar:

```
$ VBoxManage createhd -filename *novo.vdi* --size *10000*

```

sendo que o tamanho está em MiB, neste exemplo 10000MiB ~= 10GiB e *novo.vdi* é o nome do novo disco rígido a ser criado.

**Nota:** Por padrão, esse comando usa a variante de formato de arquivo *Standard* (correspondente à dinâmica alocada) e, portanto, não usará a mesma variante de formato de arquivo do disco virtual de origem. Se o seu *antigo.vdi* tiver um tamanho fixo e você quiser manter essa variante, adicione o parâmetro `--variant Fixed`.

Em seguida, o disco virtual antigo precisa ser clonado para o novo, o que pode levar algum tempo:

```
$ VBoxManage clonehd *antigo.vdi* *novo.vdi* --existing

```

Desanexe o disco rígido antigo e anexe um novo, substitua todos os argumentos itálicos obrigatórios pelos seus valores apropriados:

```
$ VBoxManage storageattach *nome_VM* --storagectl *SATA* --port *0* --medium none
$ VBoxManage storageattach *nome_VM* --storagectl *SATA* --port *0* --medium *novo.vdi* --type hdd

```

Para obter o nome do controlador de armazenamento e o número da porta, você pode usar o comando `VBoxManage showvminfo *nome_VM*`. Entre os resultados, você obterá esse resultado (o que você está procurando está em itálico):

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

Baixe a [imagem do GParted live](http://gparted.org/download.php) e monte-a como um arquivo de CD/DVD virtual, inicialize sua máquina virtual, aumente/mova suas partições, desmonte o GParted live e reinicie.

**Nota:** Nos discos GPT, aumentar o tamanho do disco resultará no backup do cabeçalho GPT não estar no final do dispositivo. O GParted pedirá para corrigir isso, clique em *Corrigir* nas duas vezes. Nos discos MBR, você não tem esse problema como essa tabela de partições como nenhum trailer no final do disco.

Finalmente, cancele o registro do disco virtual do VirtualBox e remova o arquivo:

```
$ VBoxManage closemedium disk *antigo.vdi*
$ rm *antigo.vdi*

```

#### Aumentando o tamanho de discos VDI

Se o seu disco for um VDI, execute:

```
$ VBoxManage modifyhd *seu_disco_virtual.vdi* --resize *o_novo_tamanho*

```

Em seguida, retorne à etapa Gparted para aumentar o tamanho da partição no disco virtual.

### Substituir um disco virtual manualmente a partir do arquivo .vbox

Se você acha que editar um simples arquivo *XML* é mais conveniente do que brincar com a GUI ou com `VBoxManage` e você deseja substituir (ou adicionar) um disco virtual à sua máquina virtual, no arquivo de configuração *.vbox* correspondente à sua máquina virtual, basta substituir o GUID, o local do arquivo e o formato de acordo com suas necessidades:

 `ArchLinux_vm.vbox`  `<HardDisk uuid="*{670157e5-8bd4-4f7b-8b96-9ee412a712b5}*" location="*ArchLinux_vm.vdi*" format="*VDI*" type="Normal"/>` 

então, na sub-tag `<AttachedDevice>` de `<StorageController>`, substitua o GUID pelo novo.

 `ArchLinux_vm.vbox` 
```
<AttachedDevice type="HardDisk" port="0" device="0">
  <Image uuid="*{670157e5-8bd4-4f7b-8b96-9ee412a712b5}*"/>
</AttachedDevice>
```

**Nota:** Se você não souber o GUID da unidade que deseja adicionar, poderá usar o `VBoxManage showhdinfo *arquivo*`. Se você usou anteriormente o `VBoxManage clonehd` para copiar/converter seu disco virtual, este comando deveria ter gerado o GUID logo após a conclusão da cópia/conversão. O uso de um GUID aleatório não funciona, pois cada UUID [é armazenado dentro de cada imagem de disco](http://www.virtualbox.org/manual/ch05.html#cloningvd).

#### Transferir entre host Linux e outro SO

As informações sobre o caminho para discos rígidos e snapshots são armazenadas entre as tags `<HardDisks> .... </HardDisks>` no arquivo com a extensão *.vbox*. Você pode editá-las manualmente ou usar este script onde você precisará alterar apenas o caminho ou usar os padrões, presumindo que *.vbox* está no mesmo diretório com um disco virtual e a pasta de instantâneos. Ele imprimirá a nova configuração na *stdout*.

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

**Nota:**

*   Se você for preparar a máquina virtual para uso em um host Windows, no final do nome do caminho, use a barra invertida \ em vez de /.
*   O script detecta snapshots procurando `{` no nome do arquivo.
*   Para executá-lo em um novo host, você precisará adicioná-lo primeiro ao registrador clicando em **Máquina -> Adicionar...** ou usando as teclas de atalho Ctrl+A e depois navegue até arquivo *.vbox* que contém configuração ou linha de comando de uso `VBoxManage registervm *nome_de_arquivo*. vbox`

### Clonar um disco virtual e atribuição de um novo UUID a ele

Os UUIDs são amplamente utilizados pelo VirtualBox. Cada máquina virtual e cada disco virtual de uma máquina virtual deve ter um UUID diferente. Quando você inicia uma máquina virtual no VirtualBox, o VirtualBox rastreia todos os UUIDs da sua instância de máquina virtual. Veja a [VBoxManage list](http://www.virtualbox.org/manual/ch08.html#vboxmanage-list) para listar os itens registrados no VirtualBox.

Se clonou um disco virtual manualmente copiando o arquivo de disco virtual, você precisará atribuir um novo UUID à unidade virtual clonada se desejar usar o disco na mesma máquina virtual ou mesmo em outra (se essa já tiver sido aberto, e assim registrado, com o VirtualBox).

Você pode usar este comando para atribuir um novo UUID a um disco virtual:

```
$ VBoxManage internalcommands sethduuid */caminho/para/disco.vdi*

```

**Dica:** Para evitar a cópia do disco virtual e atribuir um novo UUID ao seu arquivo manualmente, você pode usar [VBoxManage clonehd](http://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi).

**Nota:** Os comando acima possuem suporte a todos os [formatos de discos virtuais suportados pelo VirtualBox](#Formatos_suportados_pelo_VirtualBox).

## Dicas e truques

Para configurações avançadas, veja [VirtualBox/Dicas e truques](/index.php/VirtualBox/Tips_and_tricks "VirtualBox/Tips and tricks").

## Solução de problemas

### Teclado e mouse estão travados na máquina virtual

Isso significa que sua máquina virtual capturou a entrada do teclado e do mouse. Simplesmente pressione a tecla `Ctrl` e sua entrada deve controlar seu hospedeiro novamente.

Para controlar de forma transparente sua máquina virtual com o mouse indo e voltando de seu hospedeiro, sem ter que pressionar nenhuma tecla e, assim, ter uma integração perfeita, instale os adicionais para convidados dentro do convidado. Leia a partir do passo [#Instalar os adicionais para convidado](#Instalar_os_adicionais_para_convidado) se o convidado for o Arch Linux, caso contrário leia a ajuda oficial do VirtualBox.

### Nenhuma opção para cliente de SO 64 bits

Ao iniciar um cliente VM e nenhuma opção de 64 bits estiver disponível, verifique se os recursos de virtualização da CPU (geralmente denominados `VT-x`) estão habilitados na BIOS.

Se você estiver usando um hospedeiro do Windows, talvez seja necessário desabilitar o Hyper-V, já que ele impede que o VirtualBox use o VT-x. [[6]](https://www.virtualbox.org/ticket/12350)

### VirtualBox GUI não corresponde ao tema GTK do hospedeiro

Veja [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications") para informações sobre aplicação de temas em aplicativos baseados no Q, como o VirtualBox.

### Não é possível enviar Ctrl+Alt+Fn para o convidado

O sistema operacional do convidado é uma distribuição GNU/Linux e você deseja abrir um novo shell TTY pressionando `Ctrl+Alt+F2` ou sair da sessão atual com `Ctrl+Alt+Backspace`. Se você digitar esses atalhos de teclado sem qualquer adaptação, o convidado não receberá nenhuma entrada e o hospedeiro (se for uma distribuição GNU/Linux também) interceptará essas teclas de atalho. Para enviar `Ctrl+Alt+F2` para o convidado, por exemplo, simplesmente pressione a *Tecla do Hospedeiro* (normalmente a tecla `Ctrl` da direita) e pressione `F2` simultaneamente.

### Subsistema USB não funciona

Seu usuário deve estar no grupo `vboxusers` e você precisa instalar o [pacote de extensões](#Pacote_de_extensões) se quiser suporte a USB 2\. Em seguida, você poderá ativar o USB 2 nas configurações da VM e adicionar um ou vários filtros para os dispositivos que deseja acessar no sistema operacional do convidado.

Se `VBoxManage list usbhost` não mostrar nenhum dispositivo USB, mesmo que seja executado como root, certifique-se de que não há regras antigas do udev (do VirtualBox 4.x) em `/etc/udev/rules.d/`. O VirtualBox 5.0 instala as regras do udev para `/usr/lib/udev/rules.d/`. Você pode usar o comando como `pacman -Qo /usr/lib/udev/rules.d/60-vboxdrv.rules` para determinar se o arquivo de regras do udev está desatualizado.

Às vezes, em hospedeiros Linux antigos, o subsistema USB não é detectado automaticamente, resultando em um erro `Could not load the Host USB Proxy service: VERR_NOT_FOUND` ou em uma unidade USB não visível no hospedeiro, [mesmo quando o usuário está no grupo **vboxusers**](https://bbs.archlinux.org/viewtopic.php?id=121377). Este problema é devido ao fato de que o VirtualBox mudou de *usbfs* para *sysfs* na versão 3.0.8\. Se o hospedeiro não entender essa alteração, você poderá reverter para o comportamento antigo definindo a seguinte variável de ambiente em qualquer arquivo originado pelo seu shell (por exemplo, `~/.bashrc` se estiver usando *bash*):

 `~/.bashrc`  `VBOX_USB=usbfs` 

Em seguida, certifique-se de que o ambiente tenha conhecimento dessa alteração (reconecte, crie o arquivo manualmente, ative uma nova instância do shell ou reinicialize).

Certifique-se também de que seu usuário seja membro do grupo `storage`.

### Modem USB não funciona no hospedeiro

Se você tiver um modem USB que está sendo usado pelo sistema operacional convidado, a eliminação do sistema operacional convidado pode fazer com que o modem fique inutilizável pelo sistema hospedeiro. Matar e reiniciar `VBoxSVC` deve corrigir este problema.

### Dispositivo USB trava o convidado

Se a conexão de um dispositivo USB ao convidado causar uma falha ou qualquer outro comportamento incorreto, tente alternar o controlador USB de USB 2 (EHCI) para USB 3 (xHCI) ou vice-versa.

### Acesso a porta serial pelo convidado

Verifique sua permissão para a porta serial:

 `$ ls -l /dev/ttyS*` 
```
crw-rw---- 1 root uucp 4, 64 Feb  3 09:12 /dev/ttyS0
crw-rw---- 1 root uucp 4, 65 Feb  3 09:12 /dev/ttyS1
crw-rw---- 1 root uucp 4, 66 Feb  3 09:12 /dev/ttyS2
crw-rw---- 1 root uucp 4, 67 Feb  3 09:12 /dev/ttyS3

```

Adicione seu usuário ao [grupo de usuários](/index.php/Grupo_de_usu%C3%A1rios "Grupo de usuários") `uucp`.

### Convidado trava após iniciar o Xorg

Drivers com defeito ou em falta podem fazer com que o convidado congele após iniciar o Xorg, veja por exemplo [[7]](https://bbs.archlinux.org/viewtopic.php?pid=1167838) e [[8]](https://bbs.archlinux.org/viewtopic.php?id=156079). Tente desativar a aceleração 3D em *Configurações > Monitor* e verifique se todos os drivers [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)") estão instalados.

### Modo tela cheia mostra uma tela branca

On some window managers ([i3](/index.php/I3 "I3"), [awesome](/index.php/Awesome "Awesome")), VirtualBox has issues with fullscreen mode properly due to the overlay bar. To work around this issue, disable "Show in Full-screen/Seamless" option in "Guest Settings > User Interface > Mini ToolBar". See the [upstream bug report](https://www.virtualbox.org/ticket/14323) for more information.

### Hospedeiro trava ao iniciar máquina virtual

Possible causes/solutions:

*   SMAP

This is a known incompatiblity with SMAP enabled kernels affecting (mostly) Intel Broadwell chipsets. A solution to this problem is disabling SMAP support in your kernel by appending the `nosmap` option to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

*   Hardware Virtualisation

Disabling hardware virtualisation (VT-x/AMD-V) may solve the problem.

*   Various Kernel bugs
    *   Fuse mounted partitions (like ntfs) [[9]](https://bbs.archlinux.org/viewtopic.php?id=185841), [[10]](https://bugzilla.kernel.org/show_bug.cgi?id=82951#c12)

Generally, such issues are observed after upgrading VirtualBox or linux kernel. Downgrading them to the previous versions of theirs might solve the problem.

### Convidados Linux têm áudio lento/distorcido

The AC97 audio driver within the Linux kernel occasionally guesses the wrong clock settings when running inside Virtual Box, leading to audio that is either too slow or too fast. To fix this, create a file in `/etc/modprobe.d/` with the following line:

```
options snd-intel8x0 ac97_clock=48000

```

### Microfone analógico não funciona

If the audio input from an analog microphone is working correctly on the host, but no sound seems to get through to the guest, despite the microphone device apparently being detected normally, installing a [sound server](/index.php/Sound_system#Sound_servers "Sound system") such as [PulseAudio](/index.php/PulseAudio "PulseAudio") on the host might fix the problem.

If after installing [PulseAudio](/index.php/PulseAudio "PulseAudio") the microphone still refuses to work, setting *Host Audio Driver* (under *VirtualBox > Machine > Settings > Audio*) to *ALSA Audio Driver* might help.

### Microfone não funciona após atualização

There have been issues reported around sound input in 5.1.x versions. [[11]](https://forums.virtualbox.org/viewtopic.php?f=7&t=78797)

[Downgrading](/index.php/Downgrading "Downgrading") may solve the problem. You can use [virtualbox-bin-5.0](https://aur.archlinux.org/packages/virtualbox-bin-5.0/) to ease downgrading.

### Problemas com imagens convertidas para ISO

Some image formats cannot be reliably converted to ISO. For instance, [ccd2iso](https://www.archlinux.org/packages/?name=ccd2iso) ignores .ccd and .sub files, which can result in disk images with broken files.

In this case, you will either have to use [CDemu](/index.php/CDemu "CDemu") for Linux inside VirtualBox or any other utility used to mount disk images.

### Falha ao criar a interface de rede interna

Make sure all required kernel modules are loaded. See [#Load the VirtualBox kernel modules](#Load_the_VirtualBox_kernel_modules).

If all required kernel modules are loaded and you are still unable to create the host-only adapter, navigate to *File > Host Network Manager* and click the *Create* button to add the network interface.

### Falha ao inserir módulo

When you get the following error when trying to load modules:

```
Failed to insert 'vboxdrv': Required key not available

```

[Sign](#Sign_modules) your modules or disable `CONFIG_MODULE_SIG_FORCE` in your kernel config.

### VBOX_E_INVALID_OBJECT_STATE (0x80BB0007)

This can occur if a VM is exited ungracefully. Run the following command:

```
$ VBoxManage controlvm *virtual_machine_name* poweroff

```

### NS_ERROR_FAILURE e itens de menu em falta

This happens sometimes when selecting *QCOW*/*QCOW2*/*QED* disk format when creating a new virtual disk.

If you encounter this message the first time you start the virtual machine:

```
Failed to open a session for the virtual machine debian.
Could not open the medium '/home/.../VirtualBox VMs/debian/debian.qcow'.
QCow: Reading the L1 table for image '/home/.../VirtualBox VMs/debian/debian.qcow' failed (VERR_EOF).
VD: error VERR_EOF opening image file '/home/.../VirtualBox VMs/debian/debian.qcow' (VERR_EOF).

Result Code: 
NS_ERROR_FAILURE (0x80004005)
Component: 
Medium

```

Exit VirtualBox, delete all files of the new machine and from virtualbox config file remove the last line in `MachineRegistry` menu (or the offending machine you are creating):

 `~/.config/VirtualBox/VirtualBox.xml` 
```
...
<MachineRegistry>
  <MachineEntry uuid="{00000000-0000-0000-0000-000000000000}" src="/home/void/VirtualBox VMs/debian/debian.vbox"/>
  <MachineEntry uuid="{00000000-0000-0000-0000-000000000000}" src="/home/void/VirtualBox VMs/ubuntu/ubuntu.vbox"/>
  ~~<MachineEntry uuid="{00000000-0000-0000-0000-000000000000}" src="/home/void/VirtualBox VMs/lastvmcausingproblems/lastvmcausingproblems.qcow"/>~~
</MachineRegistry>
...
```

### Arch: script pacstrap falhando

If you used *pacstrap* in the [#Installation steps for Arch Linux guests](#Installation_steps_for_Arch_Linux_guests) to also [#Install the Guest Additions](#Install_the_Guest_Additions) **before** performing a first boot into the new guest, you will need to `umount -l /mnt/dev` as root before using *pacstrap* again; a failure to do this will render it unusable.

### OpenBSD inutilizável quando instruções de virtualização estão indisponíveis

While OpenBSD is reported to work fine on other hypervisors without virtualisation instructions (VT-x AMD-V) enabled, an OpenBSD virtual machine running on VirtualBox without these instructions will be unusable, manifesting with a bunch of segmentation faults. Starting VirtualBox with the *-norawr0* argument [may solve the problem](https://www.virtualbox.org/ticket/3947). You can do it like this:

```
$ VBoxSDL -norawr0 -vm *name_of_OpenBSD_VM*

```

### Hospedeiro Windows: VERR_ACCESS_DENIED

To access the raw VMDK image on a Windows host, run the VirtualBox GUI as administrator.

### Windows: "O caminho especificado não existe. Verifique o caminho e tente novamente."

This error message may appear when running an `.exe` file which requires administrator privileges from a shared folder in windows guests. [[12]](https://www.virtualbox.org/ticket/5732#comment:39)

As a workaround, copy the file to the virtual drive or use [UNC paths](https://en.wikipedia.org/wiki/Uniform_Naming_Convention "w:Uniform Naming Convention") (`\\vboxsvr`). See [[13]](https://support.microsoft.com/de-de/help/2019185/copying-files-from-a-mapped-drive-to-a-local-directory-fails-with-erro) for more information.

### Erro no Windows 8.x com código 0x000000C4

If you get this error code while booting, even if you choose OS Type Win 8, try to enable the `CMPXCHG16B` CPU instruction:

```
$ vboxmanage setextradata *virtual_machine_name* VBoxInternal/CPUM/CMPXCHG16B 1

```

### Windows 8, 8.1 ou 10 falha em instalar, inicializar ou tem erro "ERR_DISK_FULL"

Update the VM's settings by going to *Settings > Storage > Controller:SATA* and check "Use Host I/O Cache".

### WinXP: Profundidade de bits não pode ser maior que 16

If you are running at 16-bit color depth, then the icons may appear fuzzy/choppy. However, upon attempting to change the color depth to a higher level, the system may restrict you to a lower resolution or simply not enable you to change the depth at all. To fix this, run `regedit` in Windows and add the following key to the Windows XP VM's registry:

```
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services]
"ColorDepth"=dword:00000004

```

Then update the color depth in the "desktop properties" window. If nothing happens, force the screen to redraw through some method (i.e. `Host+f` to redraw/enter full screen).

### Windows: Oscilação da tela se a aceleração 3D estiver ativada

VirtualBox > 4.3.14 has a regression in which Windows guests with 3D acceleration flicker. Since r120678 a patch has been implemented to recognize an [environment variable](/index.php/Environment_variable "Environment variable") setting, launch VirtualBox like this:

```
$ CR_RENDER_FORCE_PRESENT_MAIN_THREAD=0 VirtualBox

```

Make sure no VirtualBox services are still running. See [VirtualBox bug 13653](https://www.virtualbox.org/ticket/13653).

### Nenhuma aceleração 3D de hardware no convidado Arch Linux

[virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils) package as of version 5.2.16-2 does not contain the file `VBoxEGL.so`. This causes the Arch Linux guest does not have proper 3D acceleration. See [FS#49752](https://bugs.archlinux.org/task/49752).

To deal with this problem, apply the patch set at [FS#49752#comment152254](https://bugs.archlinux.org/task/49752#comment152254). Some fix to the patch set is required to make it work for version 5.2.16-2.

### Não é possível iniciar o VirtualBox no Wayland: Falha de segmentação

This problem is usually caused by Qt on Wayland, see [FS#58761](https://bugs.archlinux.org/task/58761).

The best thing, not to affect the rest of Qt applications (which usually work well in Wayland), is to unset the `QT_QPA_PLATFORM` [environment variable](/index.php/Environment_variable "Environment variable") in the VirtualBox's [desktop entry](/index.php/Desktop_entry "Desktop entry"). Follow the instructions in [Desktop entries#Modify environment variables](/index.php/Desktop_entries#Modify_environment_variables "Desktop entries") and change the lines starting with

```
Exec=VirtualBox ...

```

to

```
Exec=env -u QT_QPA_PLATFORM VirtualBox ...

```