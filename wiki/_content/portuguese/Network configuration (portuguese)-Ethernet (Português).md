Esse artigo descreve especificidades sobre [Ethernet](https://en.wikipedia.org/wiki/pt:Ethernet "wikipedia:pt:Ethernet"). Configuração de rede em geral está coberto em [Configuração de rede](/index.php/Configura%C3%A7%C3%A3o_de_rede "Configuração de rede").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Driver de dispositivo](#Driver_de_dispositivo)
    *   [1.1 Verificando o estado](#Verificando_o_estado)
    *   [1.2 Carregando o módulo](#Carregando_o_módulo)
*   [2 Dicas e truques](#Dicas_e_truques)
    *   [2.1 ifplugd para laptops](#ifplugd_para_laptops)
*   [3 Solução de problemas](#Solução_de_problemas)
    *   [3.1 Trocando computadores no modem a cabo](#Trocando_computadores_no_modem_a_cabo)
    *   [3.2 Notificação de Congestionamento Explícito](#Notificação_de_Congestionamento_Explícito)
    *   [3.3 Realtek sem link / Problema com WOL](#Realtek_sem_link_/_Problema_com_WOL)
        *   [3.3.1 Habilitando a NIC diretamente no Linux](#Habilitando_a_NIC_diretamente_no_Linux)
        *   [3.3.2 Revertendo/alterando driver do Windows](#Revertendo/alterando_driver_do_Windows)
        *   [3.3.3 Habilitando WOL no driver do Windows](#Habilitando_WOL_no_driver_do_Windows)
        *   [3.3.4 Driver Realtek mais novo para Linux](#Driver_Realtek_mais_novo_para_Linux)
        *   [3.3.5 Ativando LAN Boot ROM na BIOS/CMOS](#Ativando_LAN_Boot_ROM_na_BIOS/CMOS)
    *   [3.4 No interface with Atheros chipsets](#No_interface_with_Atheros_chipsets)
    *   [3.5 Broadcom BCM57780](#Broadcom_BCM57780)
    *   [3.6 Realtek RTL8111/8168B](#Realtek_RTL8111/8168B)
    *   [3.7 Placa-mãe Gigabyte com Realtek 8111/8168/8411](#Placa-mãe_Gigabyte_com_Realtek_8111/8168/8411)

## Driver de dispositivo

### Verificando o estado

O [udev](/index.php/Udev "Udev") deve detectar sua [interface de rede](https://en.wikipedia.org/wiki/pt:Placa_de_rede necessário na inicialização. Verifique pela entrada "Ethernet controller" (ou similar) no resultado do comando `lspci -v`. Este comando dirá qual módulo do kernel é necessário para o funcionamento do dispositivo. Por exemplo:

 `$ lspci -v` 
```
02:00.0 Ethernet controller: Attansic Technology Corp. L1 Gigabit Ethernet Adapter (rev b0)
     ...
     Kernel driver in use: atl1
     Kernel modules: atl1

```

Após, veja se o driver foi carregado usando `dmesg | grep *nome_módulo*`. Exemplo:

 `$ dmesg | grep atl1` 
```
...
atl1 0000:02:00.0: eth0 link is up 100 Mbps full duplex

```

Pule para a próxima sessão caso o driver tenha sido carregado com sucesso. Caso contrário, você precisará descobrir qual é o módulo necessário para o seu modelo de interface de rede em específico.

### Carregando o módulo

Pesquise na internet pelo modelo/driver para o seu chipset. Algumas módulos comuns são `8139too` para as placas com um chipset da Realtek, ou `sis900` para placas com um chipset da SiS. Assim que descobrir qual módulo deve usar, tente [carregar o módulo manualmente](/index.php/Kernel_module_(Portugu%C3%AAs)#Manuseio_manual_de_módulos_de_kernel "Kernel module (Português)"). Caso você esbarre com algum erro dizendo que o módulo não foi encontrado, é possível que o driver não foi incluído no kernel do Arch Linux. Tente procurar no [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)") pelo nome do módulo.

Caso o udev não detecte ou não carregue o módulo de forma apropriada e automaticamente durante o boot, veja [Kernel module (Português)#Carregamento automático de módulos com systemd](/index.php/Kernel_module_(Portugu%C3%AAs)#Carregamento_automático_de_módulos_com_systemd "Kernel module (Português)").

## Dicas e truques

### ifplugd para laptops

**Dica:** [dhcpcd](/index.php/Dhcpcd "Dhcpcd") fornece o mesmo recurso pronto para uso.

O [ifplugd](https://www.archlinux.org/packages/?name=ifplugd) é um daemon que configura automaticamente seu dispositivo Ethernet quando um cabo é conectado e desconfigura automaticamente quando desconectado. É útil para laptops com adaptadores de rede *onboards*, pois configurará a interface quando um cabo realmente for conectado. Outro uso é quando você deseja reiniciar as configurações de rede mas não deseja reiniciar o computador ou deseja fazer isto via linha de comando.

Por padrão, ele é configurado para funcionar para o dispositivo `eth0`. Estas e outras configurações como tempo de espera podem ser alterados no arquivo `/etc/ifplugd/ifplugd.conf`.

**Nota:** O pacote [netctl](/index.php/Netctl "Netctl") inclui `netctl-ifplugd@.service`, do contrário você pode usar `ifplugd@.service` do pacote [ifplugd](https://www.archlinux.org/packages/?name=ifplugd). Por exemplo, [habilite](/index.php/Habilite "Habilite") `ifplugd@eth0.service`.

## Solução de problemas

### Trocando computadores no modem a cabo

Alguns ISP por cabo têm o modem a cabo configurado para reconhecer apenas um PC cliente, pelo endereço MAC da sua interface de rede. Uma vez que o modem a cabo aprendeu o endereço MAC do primeiro PC ou equipamento que fala com ele, ele não responderá de outro modo a outro endereço MAC. Assim, se você trocar um PC por outro (ou por um roteador), o novo PC (ou roteador) não funcionará com o modem a cabo, porque o novo PC (ou roteador) possui um endereço MAC diferente do antigo. Para reiniciar o modem a cabo para que reconheça o novo PC, você deve desligar e ligar o modem a cabo. Uma vez que o modem a cabo foi reiniciado e voltou totalmente on-line novamente (as luzes indicadoras foram instaladas), reinicie o PC recém-conectado para que ele faça uma solicitação DHCP ou faça com que ele solicite um novo *lease* (concessão) DHCP.

Caso este método não funcione, você deverá clonar o endereço MAC do computador original. Veja também [MAC address spoofing](/index.php/MAC_address_spoofing "MAC address spoofing").

### Notificação de Congestionamento Explícito

[Explicit Congestion Notification](https://en.wikipedia.org/wiki/Explicit_Congestion_Notification "wikipedia:Explicit Congestion Notification") (ECN), Notificação de Congestionamento Explícito, pode causar problemas de tráfego com roteadores antigos/ruins [[1]](https://bbs.archlinux.org/viewtopic.php?id=239892). Desde o [systemd 239](https://github.com/systemd/systemd/issues/9748), está habilitado para tráfego de entrada e de saída.

Para habilitar apenas ECN quando requisitado pelas conexões de entrada (padrão do kernel razoavelmente seguro):

```
# sysctl net.ipv4.tcp_ecn=2

```

Para desabilitar ECN completamente (para, por exemplo, testar se ECN estava causando problemas):

```
# sysctl net.ipv4.tcp_ecn=0

```

Veja também a [documentação do kernel](https://www.kernel.org/doc/Documentation/networking/ip-sysctl.txt).

### Realtek sem link / Problema com WOL

Os usuários com o Realtek 8168 8169 8101 8111(C) baseados em NIC (placas e *on-board*) podem notar um problema onde a NIC parece estar desativada na inicialização e não tem nenhuma luz no Link. Isso geralmente pode ser encontrado em um sistema de *dual boot*, onde o Windows também está instalado. Parece que o uso dos drivers oficiais do Realtek (datado de qualquer coisa após maio de 2007) no Windows é a causa. Esses drivers mais recentes desativam o recurso Wake-On-LAN desabilitando a NIC no tempo de desligamento do Windows, onde ele permanecerá desabilitado até a próxima vez que o Windows for inicializado. Você poderá notar se esse problema está afetando você se a luz do Link estiver desligada até que o Windows seja iniciado; durante o desligamento do Windows, a luz do link será desligada. A operação normal deve ser que a luz do link esteja sempre ativada enquanto o sistema estiver ligado, mesmo durante o POST. Este problema também afetará outros sistemas operacionais sem drivers mais recentes (por exemplo, Live CDs). Aqui estão algumas correções para este problema.

#### Habilitando a NIC diretamente no Linux

Siga [#Habilitando e desabilitando interfaces de rede](#Habilitando_e_desabilitando_interfaces_de_rede) para habilitar a interface.

#### Revertendo/alterando driver do Windows

Você pode reverter o driver de NIC do Windows para o fornecido pela Microsoft (se disponível), ou reverter/instalar um driver Realtek oficial pré-datado de maio de 2007 (pode estar no CD que acompanhou o hardware).

#### Habilitando WOL no driver do Windows

Provavelmente a melhor e mais correção é mudar essa configuração no driver do Windows. Desta forma, ele deve ser corrigido em todo o sistema e não apenas em Arch (ex.:, Live CDs, outros sistemas operacionais). No Windows, no Gerenciamento de dispositivos, encontre seu adaptador de rede Realtek e clique duas vezes nele. Na guia "Avançado", altere "Wake-on-LAN após o desligamento" para "Ativar".

No Windows XP (exemplo):

```
 Realize duple clique no meu computador e escolha "Propriedades"
 --> Aba "Hardware"
  --> Gerenciamento de dispositivo
    --> Adaptadores de rede
      --> "duplo clique" Realtek ...
        --> Aba "Avançada"
          --> Wake-On-Lan após o desligamento
            --> Habilitar

```

**Nota:** Novos drivers Windows do Realtek (testados com *Realtek 8111/8169 LAN Driver v5.708.1030.2008*, datado de 2009/01/22, disponível da GIGABYTE) podem se referir a esta opção de forma ligeiramente diferente, como *Desligar Wake-On-LAN > Ativar*. Parece que mudar para `Desativar` não tem efeito (você notará que a luz do link ainda está desligada no desligamento do Windows). Uma solução de contorno ruim é inicializar no Windows e apenas reiniciar o sistema (executar um reinício/desligamento desagradável), portanto, não dar ao driver do Windows a chance de desabilitar a LAN. A luz de link permanecerá ativada e o adaptador de LAN permanecerá acessível após o POST - isto é, até reiniciar o Windows e desligá-lo corretamente novamente.

#### Driver Realtek mais novo para Linux

Qualquer driver mais recente para estas placas Realtek pode ser encontrado para o Linux no site da Realtek (não testado, mas acredita que também resolve o problema).

#### Ativando LAN Boot ROM na BIOS/CMOS

Parece que a configuração *Periféricos integrados > Onboard LAN Boot ROM > Ativado* na BIOS/CMOS reativa o chip de LAN da Realtek na inicialização do sistema, apesar do driver do Windows desabilitando no desligamento do sistema operacional.

**Nota:** Isso foi testado várias vezes em uma placa-mãe GIGABYTE GA-G31M-ES2L, BIOS versão F8 lançada em 2009/02/05.

### No interface with Atheros chipsets

Os usuários de alguns chips de Ethernet da Atheros estão relatando que não funciona pronto para uso (com mídia de instalação de fevereiro de 2014). A solução de trabalho para isso é instalar [backports-patched](https://aur.archlinux.org/packages/backports-patched/).

### Broadcom BCM57780

Este chipset Broadcom às vezes não se comporta bem, a menos que você especifique a ordem dos módulos a serem carregados. Os módulos são `broadcom` e `tg3`, o primeiro que precisa ser carregado primeiro.

Essas etapas devem ajudar se o seu computador tiver esse chipset:

*   Localize sua NIC na saída do *lspci*:

 `$ lspci | grep Ethernet` 
```
02:00.0 Ethernet controller: Broadcom Corporation NetLink BCM57780 Gigabit Ethernet PCIe (rev 01)

```

*   Se sua rede com fio não estiver funcionando de alguma maneira, desconecte seu cabo e, em seguida, faça o seguinte:

```
# modprobe -r tg3
# modprobe broadcom
# modprobe tg3

```

*   Conecte seu cabo de rede de volta e verifique se o módulo foi carregado com sucesso com:

```
$ dmesg | greg tg3

```

*   Se esse procedimento resolveu o problema, você pode torná-lo permanente adicionando `broadcom` e `tg3` (nesta ordem) para o vetor `MODULES`:

 `/etc/mkinitcpio.conf`  `MODULES=(.. broadcom tg3 ..)` 

*   [Gere novamente o initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs")
*   Alternativamente, você pode criar um `/etc/modprobe.d/broadcom.conf`:

```
softdep tg3 pre: broadcom

```

**Nota:** Esses métodos podem funcionar para outros chipsets, tal como BCM57760.

### Realtek RTL8111/8168B

 `# lspci | grep Ethernet` 
```
03:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168B PCI Express Gigabit Ethernet controller (rev 02)

```

O adaptador deve ser reconhecido pelo módulo `r8169`. No entanto, com algumas revisões de chips, a conexão pode cair e voltar o tempo todo. A alternativa [r8168](https://www.archlinux.org/packages/?name=r8168) deve ser usada para uma conexão confiável neste caso. [Lista negra](/index.php/Kernel_module_(Portugu%C3%AAs)#Adicionar_um_módulo_em_uma_lista-negra_(Blacklisting) "Kernel module (Português)") `r8169`, se [r8168](https://www.archlinux.org/packages/?name=r8168) não for carregado automaticamente pelo [udev](/index.php/Udev "Udev"), veja [Kernel module (Português)#Carregamento automático de módulos com systemd](/index.php/Kernel_module_(Portugu%C3%AAs)#Carregamento_automático_de_módulos_com_systemd "Kernel module (Português)").

Outra falha nos drivers para algumas revisões deste adaptador é um suporte fraco de IPv6\. [IPv6 (Português)#Desabilitar funcionalidade](/index.php/IPv6_(Portugu%C3%AAs)#Desabilitar_funcionalidade "IPv6 (Português)") pode ser útil se você encontrar problemas como pendurar páginas da web e velocidades lentas.

### Placa-mãe Gigabyte com Realtek 8111/8168/8411

Com placas-mãe como o *Gigabyte GA-990FXA-UD3*, inicializar com [IOMMU](/index.php/PCI_passthrough_via_OVMF#Setting_up_IOMMU "PCI passthrough via OVMF") desligado (o que pode ser o padrão) fará com que a interface de rede não seja confiável, muitas vezes não conseguindo se conectar, ou até conectar mas não permitindo a transferência. Isso se aplicará à NIC *on-board* e para qualquer outra NIC pci na máquina porque a configuração IOMMU afeta toda a interface de rede na placa. Habilitar o IOMMU e inicializar com a mídia de instalação lançará as falhas da página AMD I-10/xhci por um segundo, mas depois inicializará normalmente, resultando em uma NIC *onboard* totalmente funcional (mesmo com o módulo r8169).

Ao configurar o processo de inicialização para sua instalação, adicione `iommu=soft` como um [parâmetro do kernel](/index.php/Par%C3%A2metro_do_kernel "Parâmetro do kernel") para eliminar as mensagens de erro na inicialização e restaurar a funcionalidade USB3.0.