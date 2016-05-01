O objetivo deste guia é permitir a utilização de um arranjo RAID criado através de uma controladora RAID on-board e assim permitir o dual-boot do GNU/L*i*nux com o Windows a partir de partições dentro do conjunto RAID usando o GRUB. Ao utilizar os chamados "Fake RAID"ou "Host RAID", os arranjos RAID serão atingidos a partir de `/dev/mapper/chipsetName_randomName` e não `/dev/sdX`.

## Contents

*   [1 O que é "Fake RAID"](#O_que_.C3.A9_.22Fake_RAID.22)
*   [2 Instalação](#Instala.C3.A7.C3.A3o)
    *   [2.1 Prepare a instalação](#Prepare_a_instala.C3.A7.C3.A3o)
        *   [2.1.1 Configure os arranjos RAID](#Configure_os_arranjos_RAID)
    *   [2.2 Inicie com o CD do Arch](#Inicie_com_o_CD_do_Arch)
    *   [2.3 Inicie o dmraid](#Inicie_o_dmraid)
    *   [2.4 Continue com a instalação normal](#Continue_com_a_instala.C3.A7.C3.A3o_normal)
        *   [2.4.1 Particionamento do arranjo RAID](#Particionamento_do_arranjo_RAID)
        *   [2.4.2 Monte o sistema de arquivos](#Monte_o_sistema_de_arquivos)
        *   [2.4.3 Instale e configure o Arch](#Instale_e_configure_o_Arch)
        *   [2.4.4 Instalação do GRUB](#Instala.C3.A7.C3.A3o_do_GRUB)
        *   [2.4.5 Toques finais e término da instalação](#Toques_finais_e_t.C3.A9rmino_da_instala.C3.A7.C3.A3o)
*   [3 Resolução de problemas](#Resolu.C3.A7.C3.A3o_de_problemas)
    *   [3.1 Iniciando com um arranjo corrompido](#Iniciando_com_um_arranjo_corrompido)
*   [4 Resources](#Resources)

## O que é "Fake RAID"

Segundo a [Wikipedia](https://pt.wikipedia.org/):

	*A implementação via software geralmente não possui uma facil configuração. Já na implementação via hardware as controladoras tem um preço muito elevado. Então foi criada uma "controladora barata" que em vez de um chip controlador RAID voce utiliza uma combinação de funções especiais na BIOS da placa e drivers instalados no sistema operacional .*[[1]](https://pt.wikipedia.org/wiki/Raid#Fake_RAID)

Veja [Wikipedia:pt:RAID](https://en.wikipedia.org/wiki/pt:RAID "wikipedia:pt:RAID") ou [Guia do Hardware:RAID](http://www.hardware.com.br/livros/hardware/raid.html)para mais informações.

Apesar da terminologia, "Fake RAID" via dmraid é uma implementação RAID via software robusta que oferece um solido sistema de mirror ou stripe para multiplos discos com sobrecarga insignificante para qualquer sistema moderno. O dmraid é comparável a mdraid (software RAID puro para GNU/L*i*nux) com a vantagem de ser capaz de reconstruir completamente um arranjo.

## Instalação

Antes de tudo:

*   Tenha em mãos os guias que precisará (além deste guia podem ser necessários o [Beginners' guide (Português)](/index.php/Beginners%27_guide_(Portugu%C3%AAs) "Beginners' guide (Português)") ou [Installation guide](/index.php/Installation_guide "Installation guide")) abertos em outra máquina ou impressos.
*   Baixe a imagem e queime o disco da última versão do disco de instalação do Arch.
*   Faça o Backup de seus dados importantes.

### Prepare a instalação

#### Configure os arranjos RAID

**Atenção:** Se seus HDs não estão configurados como RAID e o MS-Windows já está instalado, a mudança para "RAID" poderá causar danos.
[[2]](http://support.microsoft.com/kb/316401/)

*   Entre no **setup do BIOS** de sua placa-mãe e habilite o **Controlador RAID**, aproveite e também configure para que o PC inicie pelo drive de CD.
*   Salve e saia do **setup do BIOS**. Durante o boot, entre no utilitário de configuração da sua controladora RAID.
*   No utilitário crie o arranjo que precisará (mirror/stripe).

**Dica:** Consulte o manual de sua placa-mãe para maiores detalhes.

Com os arranjos RAID definidos no BIOS da placa-mãe inicie o CD do Arch L*i*nux.

### Inicie com o CD do Arch

Veja [Installation guide#Pre-installation](/index.php/Installation_guide#Pre-installation "Installation guide") para maiores detalhes.

**Dica:** Altere a resolução da tela para visualizar mais informações na tela conforme seu sistema. Precione a tecla **Tab** e adicione `vga=xxx` para escolher sua resolução (por exemplo `vga=792` para 1024x786), e aperte **Enter** para iniciar com a resolução escolhida.

Loge como **root** sem senha para começar o procedimento.

### Inicie o dmraid

Inicie o "device-mapper" e procure os arranjos RAID:

```
# modprobe dm_mod
# dmraid -ay
# ls -la /dev/mapper/

```

Exemplo de saída:

```
/dev/mapper/control            <- Criado pelo device-mapper
/dev/mapper/sil_aiageicechah   <- O arranjo RAID na controladora Silicon Image
/dev/mapper/sil_aiageicechah1  <- Primeira partição nesse arranjo RAID

```

Se houver apenas um arquivo (`/dev/mapper/control`), verifique se o módulo do seu chipset está carregado com `lsmod`. Se estiver carregado, então o dmraid não suporta essa controladora, ou não existem arranjos RAID no sistema (verifique a BIOS RAID novamente). Se tudo estiver correto, então você será forçado a utilizar [Software RAID](/index.php/Installing_with_Software_RAID_or_LVM "Installing with Software RAID or LVM") (não será possível fazer Dual Boot com essa controladora).

Se o módulo do seu chipset não foi carregado, faça-o agora. Como no exemplo:

```
# modprobe sata_sil

```

Veja `/lib/modules/`uname -r`/kernel/drivers/ata/` para os drivers disponíveis.

Para testar os arranjos raid:

```
# dmraid -tay

```

### Continue com a instalação normal

Mude para o **tty2** e inicie o instalador:

```
# /arch/setup

```

#### Particionamento do arranjo RAID

*   Em **Prepare Hard Drive** escolha **Manually partition hard drives** já que a opção **Auto-prepare** não encontrará seus arranjos RAID.
*   Escolha **OTHER** e digite o caminho completo para seu arranjo RAID (exemplo `/dev/mapper/sil-aiageicechah`). Mude para **tty1** para verificar a ortografia correta.
*   Crie suas partições normalmente

**Dica:** Agora seria um bom momento para instalar o "outro" SO para utilizar em dual-boot. Se for instalar o Windows XP em "C:", então todas as partições antes da partição do Windows devem ser alteradas para o tipo [1B] (FAT32 oculta) para escondê-las durante a instalação do Windows. Quando isso for feito, mude-as novamente para o tipo [83] (GNU/L*i*nux). Logicamente isso exigirá um reinício e alguns dos passos acima deverão ser repetidos.

#### Monte o sistema de arquivos

Se, provavelmente é o caso, você não conseguir encontrar as partições recém criadas em **Manually configure block devices, filesystems and mountpoings**:

*   Mude para o **tty1**.
*   Desative todos os device-mapper:

```
# dmsetup remove_all

```

*   Reative as partições RAID recém criadas:

```
# dmraid -ay
# ls -la /dev/mapper

```

*   Mude para **tty2**, saia e entre novamente em **Manually configure block devices, filesystems and mountpoints** e as partições estarão disponíveis.

#### Instale e configure o Arch

**Dica:** Utilize três consoles: um para a **GUI de instalação**, outro para chroot e instalação do **GRUB** e outro para abrir o **cfdisk** e ter uma referência sobre as partições. Siga esse formato:

*   **tty1**: chroot e instalação do grub.
*   **tty2**: /arch/setup.
*   **tty3**: cfdisk para referência.

Execute a instalação conforme indica o [Beginners' guide (Português)](/index.php/Beginners%27_guide_(Portugu%C3%AAs) "Beginners' guide (Português)") com essas alterações:

*   Select Packages
    *   Marque **dmraid** para instalação
*   Configure System
    *   Adicione **dm_mod** na linha **MODULES** no `mkinitcpio.conf`. E se você utiliza arranjo mirror adicione também **dm_mirror**. Adicione **chipset_module_driver** na linha **Modules** caso seja necessário.
    *   Adicione **dmraid** na linha **HOOKS** também em `mkinitcpio.conf` preferencialmente antes de **sata** e depois de **filesystems**

Prossiga com a instalação até o ponto **Install Bootloader**.

#### Instalação do GRUB

Veja [GRUB](/index.php/GRUB "GRUB") para maiores informações sobre a instalação e configuração do GRUB. A instalação do GRUB será iniciada ao selecionar **Install Bootloader** no instalador do Arch.

**Nota:** Por alguma razão o `menu.lst` padrão provavelmente será incorretamente preenchido ao instalar via "Fake RAID" Verifique as linhas de **root** (root (hd0,0)). Além disso, se você não criou uma partição separada para `/boot`, certifique-se que o caminho do kernel/initrd estão corretos (`/vmlinuz` e `/kernel26.img` para `/boot/vmlinuz` e `/boot/kernel26.img`).

Se você criou várias partições lógicas elas serão mapeadas de forma semelhante a isso:

```
  /dev/mapper     | GNU/Linux    Número da partição
                  | Partição        no GRUB
nvidia_difdjida   | 
nvidia_difdjida1  |     /               0
nvidia_difdjida2  |     /boot		1
nvidia_difdjida3  |	/home		2

```

Nesse exemplo a correta partição **root** seria **(hd0,1)**.

**Nota:** Se você utiliza mais de um arranjo RAID ou várias distribuições GNU/L*i*nux instaladas em diferentes arranjos (por exemplo 2 discos em nvidia_fdaacfde e 2 discos em nvidia_ffadgic), você precisará designar corretamente a partição e o arranjo RAID a ser utilizado. Por exemplo se você está utilizando o segundo arranjo e a segunda partição sua linha **root** seria assim **root(1,1)**

Após salvar o arquivo de configuraçã, o instalador do GRUB irá **Falhar**. Mas ele copiará os arquivos para o /boot. **Não desista e reinicie** simplesmente siga as instruções:

*   Mude para **tty1** e entre como [chroot](/index.php/Chroot "Chroot"):

```
# mount -o bind /dev /mnt/dev
# mount -t proc none /mnt/proc
# mount -t sysfs none /mnt/sys
# chroot /mnt /bin/bash

```

*   Mude para o **tty3** veja a geometria do seu arranjo RAID. Utilize o cfdisk para verificar corretamente as informações C H S. Você apenas precisará iniciar o cfdisc com os argumentos corretos (exemplo `cfdisk /dev/mapper/nvidia_ffadgic`):
    *   Os números de **C**ylinders, **H**eads e **S**ectors do arranjo são mostrados no topo da tela do cfdisk. **Importante**: o cfdik mostrará as informações na seguinte ordem **H S C** mas o grub precisa dessas informações na ordem **C H S**.

Exemplo: 18079 255 63 para um arranjo RAID stripe com dois discos Raptor de 74GB. Exemplo: 38914 255 63 para um arranjo RAID stripe com dois discos de laptop com 160GB.

*   O GRUB deixará de ler corretamente a unidade. Será necessário utilizar o comando **geometry** direto no GRUB:
    *   Mude para **tty1**, que estará em **chroot**.
    *   Instale o GRUB em `/dev/mapper/raidSet`:

```
# dmsetup mknodes
# grub --device-map=/dev/null
grub> device (hd0) /dev/mapper/raidSet
grub> geometry (hd0) C H S

```

Mude **raidSet** para o nome apropriado do seu arranjo e **C H S** para os números corretos mostrados no cfdisk.

Se a geometria for inserida corretamente, o GRUB irá listar as partições encontradas nesse arranjo RAID. Você pode confirmar isso utilizando o comando **find**. Se você criou uma partição separada para o `/boot` você deve procurar como `/grub/stage1` caso contrário deverá procurar como `/boot/grub/stage1`. Exemplos:

```
grub> find /grub/stage1       # se você tem uma partição separada para o boot
grub> find /boot/grub/stage1  # se você não tem uma partição separada para o boot

```

O grub irá relatar a partição apropriada para ser o **root** (ou seja (hd0,0),(hd(0,2), etc...). Continue a instalação na MBR alterando de "hd0" para "hd1" se necessário.

```
grub> root (hd0,0)
grub> setup (hd0)
grub> quit

```

**Nota:** Utilizando o dmraid 1.0.0rc15-8 ou superiores ar partições serão rotuladas como "raidSet**p1**, raidSet**p2**, etc. E não "raidSet**1**, raidSet**2**, etc. Se o comando **setup** falhar com "error22: No such partition", será necessário a criação de **symlinks**.

O problema é que o GRUB utiliza um algoritmo antigo para a detecção das partições, ele procurará por `/dev/mapper/raidSet1` e não `/dev/mapper/raidSetp1` A solução seria a criação de symlinks de `/dev/mapper/raidSetp1` para `/dev/mapper/raidSet1` (mudando o número da partição confirme necessário). Seguindo esse procedimento:

```
# cd /dev/mapper
# for i in raidSetp*; do ln -s $i ${i/p/}; done

```

#### Toques finais e término da instalação

Para finalizar, se você tiver multiplas controladoras através do dmraid e ou múltiplos arranjos (como nvidia-fdaacfde e nvidia_ffadgic), você deverá criar o arquivo `/boot/grub/device.map` para ajudar a manter a sanidade do GRUB enquanto trabalha com múltiplos arranjos. Usando os dispositivos dmraid exemplificados seu `device.map` será parecido com isso:

```
(hd0) /dev/mapper/nvidia_fdaacfde
(hd1) /dev/mapper/nvidia_fffadgic

```

Agora o procedimento está totalmente concluido, termine o utilitário de instalação e reinicie sua nova instalação do Arch L*i*nux com raid.

```
# reboot

```

## Resolução de problemas

### Iniciando com um arranjo corrompido

Uma desvantagem do uso de Fake RAID no GNU/L*i*nux é que o **dmraid** é, atualmente, incapaz de lidar com arranjos degradados e se recusa a ativar. Nesse cenário, é preciso resolver o problema através de outro sistema operacional (por exemplo o Windows) ou através do utilitário do chipset RAID.

Alternativamente, se você estiver utilizando um arranjo de espelhamento (mirror ou RAID 1), você pode desabilitar temporariamente o dmraid e efetuar o boot através de um único drive:

1.  Edite a linhe **kernel** no menu do [GRUB](/index.php/GRUB "GRUB")
    1.  Remova as referencias aos dispositivos dmriad (exemplo mude `/dev/mapper/raidSet1` para `/dev/sda1`)
    2.  Acrescente `disablehooks=dmraid` para prevenir um **kernel panic** se o dmraid descobrir o arranjo degradado
2.  Inicie o sistema

## Resources

*   [Related forum thread](https://bbs.archlinux.org/viewtopic.php?id=22038)