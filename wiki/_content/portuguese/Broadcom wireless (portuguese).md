**Status de tradução:** Esse artigo é uma tradução de [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless"). Data da última tradução: 2019-06-23\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Broadcom_wireless&diff=0&oldid=575582) na versão em inglês.

Artigos relacionados

*   [Wireless](/index.php/Wireless_(Portugu%C3%AAs) "Wireless (Português)")

Este artigo detalha como instalar e configurar um dispositivo de rede sem fio Broadcom.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Histórico](#Histórico)
*   [2 Seleção de drivers](#Seleção_de_drivers)
*   [3 Instalação](#Instalação)
    *   [3.1 brcm80211](#brcm80211)
    *   [3.2 b43](#b43)
    *   [3.3 broadcom-wl](#broadcom-wl)
        *   [3.3.1 Instalação offline](#Instalação_offline)
        *   [3.3.2 Manualmente](#Manualmente)
*   [4 Solução de problemas](#Solução_de_problemas)
    *   [4.1 Configurando broadcom-wl no modo monitor](#Configurando_broadcom-wl_no_modo_monitor)
    *   [4.2 Dispositivo inacessível após atualização do kernel](#Dispositivo_inacessível_após_atualização_do_kernel)
    *   [4.3 Dispositivo com driver broadcom-wl são funcionando ou não sendo mostrado](#Dispositivo_com_driver_broadcom-wl_são_funcionando_ou_não_sendo_mostrado)
    *   [4.4 Interfaces trocadas com broadcom-wl](#Interfaces_trocadas_com_broadcom-wl)
    *   [4.5 Interface está sendo mostrada, mas não permite conexões](#Interface_está_sendo_mostrada,_mas_não_permite_conexões)
    *   [4.6 Suprimindo mensagens de console](#Suprimindo_mensagens_de_console)
    *   [4.7 Dispositivo BCM43241 não detectado](#Dispositivo_BCM43241_não_detectado)
    *   [4.8 Conexão está instável com alguns roteadores](#Conexão_está_instável_com_alguns_roteadores)
    *   [4.9 Nenhum 5GHz para dispositivos BCM4360 (14e4:43a0) / BCM43602 (14e4:43ba)](#Nenhum_5GHz_para_dispositivos_BCM4360_(14e4:43a0)_/_BCM43602_(14e4:43ba))
    *   [4.10 Dispositivo funciona de forma intermitente](#Dispositivo_funciona_de_forma_intermitente)

## Histórico

A Broadcom tem um histórico notável com seu suporte a dispositivos Wi-Fi relacionados ao GNU/Linux. Durante boa parte do seu histórico inicial, os dispositivos da Broadcom eram totalmente incompatíveis ou exigiam que o usuário mexesse no firmware. O conjunto limitado de dispositivos sem fio que eram suportados era feito por um driver de engenharia reversa. O driver `b43` de engenharia reversa foi introduzido no kernel 2.6.24.

Em agosto de 2008, a Broadcom lançou o [driver 802.11 Linux STA](http://www.broadcom.com/support/802.11/linux_sta.php) com suporte oficial a dispositivos sem fio da Broadcom no GNU/Linux. Este é um driver licenciado restritivamente e não funciona com ESSIDs ocultos, mas a Broadcom prometeu trabalhar para uma abordagem mais aberta no futuro.

Em setembro de 2010, a Broadcom [lançou](http://thread.gmane.org/gmane.linux.kernel.wireless.general/55418) um driver totalmente código aberto. O driver [brcm80211](http://wireless.kernel.org/en/users/Drivers/brcm80211) foi introduzido no kernel 2.6.37 e no kernel 2.6.39 foi subdividido nos drivers `brcmsmac` e `brcmfmac`.

Os tipos de drivers disponíveis são:

| Driver | Descrição |
| brcm80211 | Versão de driver de kernel principal (recomendada) |
| b43 | Versão de driver de kernel por engenharia reversa |
| broadcom-wl | Driver da Broadcom com licença restrita |

## Seleção de drivers

Para saber quais drivers podem ser operados no dispositivo de rede sem fio Broadcom do computador, será preciso detectar o [ID do dispositivo](https://en.wikipedia.org/wiki/PCI_configuration_space "wikipedia:PCI configuration space") e o nome do chipset. Cruze-os com a lista de dispositivos suportados pelos de drivers [brcm80211](https://wireless.wiki.kernel.org/en/users/Drivers/brcm80211#supported_chips) e [b43](https://wireless.wiki.kernel.org/en/users/Drivers/b43#list_of_hardware).

```
$ lspci -vnn -d 14e4:

```

## Instalação

### brcm80211

O kernel contém dois drivers código abertos embutidos: **brcmfmac** para FullMAC nativo e **brcmsmac** para SoftMAC baseado em mac80211\. Eles devem ser carregados automaticamente ao inicializar.

**Nota:**

*   **brcmfmac** possui suporte a chipsets mais novos, e possui suporte a modo AP, modo P2P ou criptografia de hardware.
*   **brcmsmac** possui suporte apenas a chipsets antigos como BCM4313, BCM43224, BCM43225.

### b43

Dois drivers de código aberto de engenharia reversa são integrados ao kernel: **b43** e **b43legacy**. O b43 possui suporte aos chipsets Broadcom mais recentes, enquanto o driver b43legacy possui suporte apenas aos primeiros chipsets BCM4301 e BCM4306 rev.2\. Para evitar a detecção errônea do chipset da sua placa WiFi, coloque na [lista negra](/index.php/Blacklist "Blacklist") o driver não utilizado.

Ambos os drivers exigem que o firmware não livre funcione. Instale [b43-firmware](https://aur.archlinux.org/packages/b43-firmware/) ou [b43-firmware-classic](https://aur.archlinux.org/packages/b43-firmware-classic/).

**Note:**

*   BCM4306 rev.3, BCM4311, BCM4312 and BCM4318 rev.2 foram relatados como tendo problemas com **b43-firmware**. Use [b43-firmware-classic](https://aur.archlinux.org/packages/b43-firmware-classic/) para essas placas.
*   BCM4331 foi relatado como tendo problemas com **b43-firmware-classic**. Use [b43-firmware](https://aur.archlinux.org/packages/b43-firmware/) para essa placa.

### broadcom-wl

Existem duas variantes do driver licenciado restrito:

*   a variante comum: [broadcom-wl](https://www.archlinux.org/packages/?name=broadcom-wl)
*   a variante [DKMS](/index.php/DKMS "DKMS"): [broadcom-wl-dkms](https://www.archlinux.org/packages/?name=broadcom-wl-dkms)

**Dica:** A variante DKMS [broadcom-wl-dkms](https://www.archlinux.org/packages/?name=broadcom-wl-dkms)

*   é agnóstico a kernel. Significa que ela possui suporte a diferentes kernels que você possa usar (e.g. [linux-ck](https://aur.archlinux.org/packages/linux-ck/)).
*   é agnóstica a lançamento de kernel também. Ela será recompilada automaticamente após cada atualização de kernel ou nova instalação. Se você usa [broadcom-wl](https://www.archlinux.org/packages/?name=broadcom-wl) ou outra variante dependente de lançamento de kernel (p.ex., [broadcom-wl-ck](https://aur.archlinux.org/packages/broadcom-wl-ck/)), pode acontecer de atualizações do kernel atrapalharem o funcionamento da rede sem fim de tempo em tempo até que o pacote seja sincronizado novamente.

#### Instalação offline

Uma conexão com a Internet é a maneira ideal de instalar o driver **broadcom-wl**; muitos laptops mais novos com placas Broadcom dispensam portas Ethernet, portanto, um adaptador Ethernet USB ou [Android tethering](/index.php/Android_tethering "Android tethering") pode ser útil. Se você não tiver nenhum dos dois, será necessário primeiro instalar o grupo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) durante a instalação. Em seguida, use outro computador conectado à Internet para fazer o download do [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) e o tarball do driver do AUR e instale-os nessa ordem.

#### Manualmente

**Atenção:** Este método não é recomendado. Os drivers não rastreados podem se tornar problemáticos ou não funcionar nas atualizações do sistema.

Instale o driver apropriado para sua arquitetura de sistema no [site da Broadcom](https://www.broadcom.com/support/?gid=1). Depois disso, para evitar colisões de driver/módulo com módulos semelhantes e disponibilizar o driver, faça:

```
# rmmod b43
# rmmod ssb
# modprobe wl

```

O módulo *wl* deve carregar automaticamente *lib80211* ou *lib80211_crypt_tkip*; do contrário, eles terão que ser carregados manualmente.

Se o driver não funcionar neste momento, talvez seja necessário atualizar as dependências:

```
# depmod -a

```

Para fazer com que o módulo seja carregado na inicialização, consulte [Módulos de kernel](/index.php/Kernel_modules "Kernel modules"). É recomendando que você coloque em [lista negra](/index.php/Blacklist "Blacklist") os módulos conflitantes.

## Solução de problemas

### Configurando broadcom-wl no modo monitor

Para definir broadcom-wl no modo de monitor, você deve definir 1 para `/proc/brcm_monitor0)`:

```
# echo 1 > /proc/brcm_monitor0

```

Ele irá criar uma nova interface de rede chamada `prism0`.

Para trabalhar no modo monitor, use essa interface de rede recém-criada.

### Dispositivo inacessível após atualização do kernel

Desde o kernel 3.3.1, o módulo **bcma** foi introduzido. Se estiver usando um driver **brcm80211**, certifique-se de que ele não esteja em [lista negra](/index.php/Kernel_modules#Blacklisting "Kernel modules"). Deve ser negado se usar um driver **b43**.

Se você estiver usando [broadcom-wl](https://www.archlinux.org/packages/?name=broadcom-wl), desinstale e reinstale-o após atualizar seu kernel, ou alterne para o pacote [broadcom-wl-dkms](https://www.archlinux.org/packages/?name=broadcom-wl-dkms).

### Dispositivo com driver broadcom-wl são funcionando ou não sendo mostrado

Certifique-se de que os módulos corretos estão na lista negra e, ocasionalmente, pode ser necessário colocar os drivers **brcm80211** na lista negra, caso tenham sido acidentalmente detectados antes de o driver **wl** ser carregado. Além disso, atualize as dependências dos módulos com `depmod -a`, verifique a interface sem fio com `ip addr`, os upgrades de kernel exigirão uma atualização do pacote não-[DKMS](/index.php/DKMS "DKMS").

### Interfaces trocadas com broadcom-wl

Os usuários do driver broadcom-wl podem achar que suas interfaces Ethernet e Wi-Fi foram trocadas. Consulte [Configuração de rede#Interfaces de rede](/index.php/Configura%C3%A7%C3%A3o_de_rede#Interfaces_de_rede "Configuração de rede") para uma resposta.

### Interface está sendo mostrada, mas não permite conexões

Acrescente ao final o seguinte [parâmetro de kernel](/index.php/Kernel_parameter "Kernel parameter"):

```
b43.allhwsupport=1

```

### Suprimindo mensagens de console

Você pode continuamente obter algumas mensagens verbosas e irritantes durante a inicialização, semelhante a

```
phy0: brcms_ops_bss_info_changed: arp filtering: enabled true, count 0 (implement)
phy0: brcms_ops_bss_info_changed: qos enabled: false (implement)
phy0: brcms_ops_bss_info_changed: arp filtering: enabled true, count 1 (implement)
enabled, active

```

Para desabilitar essas mensagens, aumente o nível de log das mensagens impressas que chegam ao console - consulte [Silent boot (Português)#sysctl](/index.php/Silent_boot_(Portugu%C3%AAs)#sysctl "Silent boot (Português)").

### Dispositivo BCM43241 não detectado

Este dispositivo não será exibido com `lspci` nem `lsusb`; ainda não há solução conhecida. Por favor, remova esta seção quando for resolvido.

### Conexão está instável com alguns roteadores

Se nenhum outra abordagem ajudar, instale [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) ou use uma [versão anterior](/index.php/Fazendo_downgrade_de_pacotes "Fazendo downgrade de pacotes").

### Nenhum 5GHz para dispositivos BCM4360 (14e4:43a0) / BCM43602 (14e4:43ba)

O problema parece estar vinculado a um [problema de canal](https://askubuntu.com/questions/749420/wireless-lost-ability-to-use-5ghz-pce-ac68), pelo menos nos Estados Unidos. Alterar o canal sem fio para um número de canal inferior (como 40) parece permitir a conexão a bandas de 5GHz.

### Dispositivo funciona de forma intermitente

Em alguns casos (p.ex., usando BCM4331 e [b43-firmware](https://aur.archlinux.org/packages/b43-firmware/)), a conexão Wi-Fi funciona de forma intermitente. Uma forma de corrigir isso é verificar se a placa está *hard-blocked* ou *soft-blocked* pelo kernel e, se estiver, desbloqueá-la com [rfkill](/index.php/Rfkill "Rfkill").