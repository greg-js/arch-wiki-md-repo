**Status de tradução:** Esse artigo é uma tradução de [Install Arch Linux on LVM](/index.php/Install_Arch_Linux_on_LVM "Install Arch Linux on LVM"). Data da última tradução: 2020-01-18\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Install_Arch_Linux_on_LVM&diff=0&oldid=595716) na versão em inglês.

Você deve criar seus volumes LVM entre as etapas de [particionamento](/index.php/Particionamento "Particionamento") e [formatação](/index.php/Sistemas_de_arquivos#Criar_um_sistema_de_arquivos "Sistemas de arquivos") do [procedimento de instalação](/index.php/Guia_de_instala%C3%A7%C3%A3o "Guia de instalação"). Ao invés de diretamente formatar uma partição para que ela seja a raiz de seu sistema de arquivos, o sistema de arquivos deverá ser criado dentro de um volume lógico (LV).

Resumo:

Visão geral:

*   Instalar os pacotes necessários. (consulte [LVM (Português)#Introdução](/index.php/LVM_(Portugu%C3%AAs)#Introdução "LVM (Português)"))
*   Criar [partições](/index.php/Parti%C3%A7%C3%B5es "Partições") onde seu PV(s) irá residir;
*   Criar seus volumes físicos (PVs). Se você tiver um disco é melhor apenas criar um PV em uma partição grande. Se você tiver múltiplos discos, você pode criar partições em cada um deles e criar um PV em cada partição;
*   Criar seu grupo de volumes (VG) e adicionar todos os PVs a ele;
*   Criar volumes lógicos (LVs) dentro deste VG;
*   Continuar com a [formatação das partições](/index.php/Guia_de_instala%C3%A7%C3%A3o#Formatar_as_partições "Guia de instalação");
*   Ao chegar na etapa “Initramfs” do guia de instalação, adicione o hook `lvm2` ao `/etc/mkinitcpio.conf` (veja abaixo para detalhes).

**Atenção:** `/boot` não pode residir em um LVM quando seu gerenciador de boot não suportar LVM; você deverá criar uma partição `/boot` separada e formatá-la diretamente. Somente [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)") é conhecido por oferecer suporte ao LVM.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
    *   [1.1 Criar partições](#Criar_partições)
    *   [1.2 Criar volumes físicos](#Criar_volumes_físicos)
    *   [1.3 Criar um grupo de volumes](#Criar_um_grupo_de_volumes)
        *   [1.3.1 Criação combinada de volumes físicos e grupos de volumes](#Criação_combinada_de_volumes_físicos_e_grupos_de_volumes)
    *   [1.4 Criar volumes lógicos](#Criar_volumes_lógicos)
    *   [1.5 Criar sistemas de arquivos e montar volumes lógicos](#Criar_sistemas_de_arquivos_e_montar_volumes_lógicos)
*   [2 Configuração do sistema](#Configuração_do_sistema)
    *   [2.1 Adicionando hooks do mkinitcpio](#Adicionando_hooks_do_mkinitcpio)
    *   [2.2 Opções de carregamento do kernel](#Opções_de_carregamento_do_kernel)

## Instalação

Consulte primeiro "introdução".

### Criar partições

Primeiro, [particione](/index.php/Particionamento "Particionamento") o dispositivo conforme necessário antes de configurar o LVM.

Criar as partições:

*   Se estiver usando uma tabela de partições do tipo MBR, defina o [ID do tipo de partição](https://en.wikipedia.org/wiki/pt:Tipo_de_parti%C3%A7%C3%A3o "wikipedia:pt:Tipo de partição") para `8e` (partição do tipo `Linux LVM` no *fdisk*).
*   Se estiver usando GPT, defina o [GUID do tipo de partição](https://en.wikipedia.org/wiki/pt:Tabela_de_Parti%C3%A7%C3%A3o_GUID#Tipos_de_parti.C3.A7.C3.A3o_GUIDs "wikipedia:pt:Tabela de Partição GUID") para `E6D6D379-F507-44C2-A23C-238F2A3DF928` (partição do tipo `Linux LVM` no *fdisk* e `8e00` no *gdisk*).

### Criar volumes físicos

Para listar todos os seus dispositivos capazes de serem usados como volume físico:

```
# lvmdiskscan

```

**Atenção:** Certifique-se de que o seu alvo é o dispositivo correto, ou os comandos a seguir irão resultar em perda de dados!

Crie um volume físico neles:

```
# pvcreate *DISPOSITIVO*

```

Este comando cria um cabeçalho em cada dispositivo que poderá ser usado pelo LVM. Conforme definido em [#Construção em blocos do LVM](#Construção_em_blocos_do_LVM), *DISPOSITIVO* pode ser qualquer [dispositivo de bloco](/index.php/Dispositivo_de_bloco "Dispositivo de bloco"), ou seja, um disco `/dev/sda`, uma partição `/dev/sda2` ou um dispositivo de [loopback](https://en.wikipedia.org/wiki/loopback "wikipedia:loopback"). Por exemplo:

```
# pvcreate /dev/sda2

```

Você pode verificar os volumes físicos criados com:

```
# pvdisplay

```

Você também pode obter um resumo de informações em volumes físicos com:

```
# pvscan

```

**Dica:** Se você tiver problemas com uma assinatura de disco já existente, você poderá removê-la usando [wipefs](/index.php/Device_file_(Portugu%C3%AAs) "Device file (Português)").

**Nota:** Se estiver usando um SSD sem particioná-lo primeiro, use `pvcreate --dataalignment 1m /dev/sda` (para tamanho de bloco de remoção < 1 MiB), veja exemplo [aqui](http://serverfault.com/questions/356534/ssd-erase-block-size-lvm-pv-on-raw-device-alignment)

### Criar um grupo de volumes

O próximo passo é criar um grupo de volumes neste volume físico.

Primeiro, você precisa criar um grupo de volumes em um dos volumes físicos:

```
# vgcreate <*grupo_de_volumes*> <*volume_fisico*>

```

Veja [lvm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvm.8) para uma lista de caracteres válidos para nomes de grupos de volumes.

Por exemplo:

```
# vgcreate GrupoVolume00 /dev/sda2

```

Então estenda-o para todos os volumes físicos que você desejar que pertençam a ele:

```
# vgextend <*grupo_de_volumes*> <*volume_fisico*>
# vgextend <*grupo_de_volumes*> <*outro_volume_fisico*>
# ...

```

Por exemplo:

```
# vgextend GrupoVolume00 /dev/sdb1
# vgextend GrupoVolume00 /dev/sdc

```

Você pode ver como o seu grupo de volumes aumenta, usando:

```
# vgdisplay

```

Isto é o que você também faria se desejasse adicionar um disco a um RAID ou grupo de espelhamento com discos em falha.

**Nota:** Você pode criar mais do que um grupo de volumes se necessário, mas nesse caso não terá todo o seu armazenamento apresentado como um único disco.

#### Criação combinada de volumes físicos e grupos de volumes

O LVM permite combinar a criação de grupo de volumes e de volume físico em um simples passo. Por exemplo, para criar o grupo de volumes *GrupoVol00* com três dispositivos mencionados acima, você pode executar:

```
# vgcreate GrupoVol00 /dev/sda2 /dev/sdb1 /dev/sdc

```

Este comando irá primeiro configurar três partições como volumes físicos (se necessário) e então irá criar o grupo de volumes com os três volumes. O comando irá avisá-lo se detectar um sistema de arquivos existente em qualquer um dos dispositivos.

### Criar volumes lógicos

**Dica:** Se desejar usar snapshots, cache de volume lógico, volumes lógicos provisionados ou RAID, veja [#Tipos de volume lógico](#Tipos_de_volume_lógico).

Agora será necessário criar volumes lógicos neste grupo de volumes. Você cria um volume lógico com o comando a seguir fornecendo o nome de um novo volume lógico, seu tamanho, e o grupo de volumes ao qual ele pertencerá:

```
# lvcreate -L <*tamanho*> <*grupo_de_volumes*> -n <*volume_logico*>

```

Por exemplo:

```
# lvcreate -L 10G GrupoVol00 -n lvolhome

```

Isto irá criar um volume lógico que você poderá acessar posteriormente com `/dev/GrupoVol00/lvolhome`. Assim como grupos de volumes, você pode usar qualquer nome que desejar para seu volume lógico quando estiver criando-o, com exceção de algumas restrições listadas em [lvm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvm.8#VALID_NAMES).

Você também pode especificar um ou mais volumes físicos para restringir onde o LVM irá alocar os dados. Por exemplo, você pode criar um volume lógico para a raiz do sistema de arquivos em seu SSD pequeno, e seu volume /home em um disco rígido mecânico mais lento. Simplesmente adicione os dispositivos de volume físicos à linha de comando, por exemplo:

```
# lvcreate -L 10G GrupoVol00 -n lvolhome /dev/sdc1

```

Se você desejar preencher todo o espaço livre no restante do grupo de volumes, use o seguinte comando:

```
# lvcreate -l 100%FREE  <*grupo_de_volumes*> -n <*volume_logico*>

```

Você pode verificar os volumes lógicos criados com:

```
# lvdisplay

```

**Nota:** Você pode precisar carregar o módulo do kernel *device-mapper* (`modprobe dm_mod`) para que os comandos acima funcionem.

**Dica:** Você pode iniciar com volumes lógicos relativamente pequenos e expandí-los posteriormente se necessário. Por simplicidade, deixe algum espaço livre no grupo de volumes para que haja espaço para expansões futuras.

### Criar sistemas de arquivos e montar volumes lógicos

Seus volumes lógicos deverão agora estar localizados em `/dev/*NomeDoSeuGrupoDeVolumes*/`. Se você não puder localizá-lo, use os comandos a seguir para carregar o módulo para criação de *nodes* de dispositivo e para tornar os grupos de volumes disponíveis:

```
# modprobe dm_mod
# vgscan
# vgchange -ay

```

Agora você pode criar sistemas de arquivos em volumes lógicos e montá-los como partições normais (se estiver instalando Arch linux, consulte [montando partições](/index.php/File_systems_(Portugu%C3%AAs)#Montar_um_sistema_de_arquivos "File systems (Português)") para detalhes adicionais):

```
# mkfs.<*tipo_de_sistema_de_arquivos*> /dev/<*grupo_de_volumes*>/<*volume_logico*>
# mount /dev/<*grupo_de_volumes*>/<*volume_logico*> /<*ponto_de_montagem*>

```

Por exemplo:

```
# mkfs.ext4 /dev/GrupoVol00/lvolhome
# mount /dev/GrupoVol00/lvolhome /home

```

**Atenção:** Ao escolher montos de montagem, selecione seu recém-criados volumes lógicos (use: `/dev/GrupoVol00/lvolhome`). **Não** selecione as atuais partições onde os volumes lógicos foram criados (não use: `/dev/sda2`).

## Configuração do sistema

### Adicionando hooks do mkinitcpio

No caso da raiz do sistema de arquivos estar em um LVM, você irá precisar ativar os hooks apropriados do [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"), caso contrário seu sistema não irá inicializar. Ative:

*   `udev` e `lvm2` para um initramfs baseado no busybox
*   `systemd` e `sd-lvm2` para um initramfs baseado no systemd

`udev` estará lá por padrão. Edite o arquivo e insira `lvm2` entre `block` e `filesystems`, como por exemplo:

 `/etc/mkinitcpio.conf`  `HOOKS=(base **udev** ... block **lvm2** filesystems)` 

Para initramfs baseados no systemd:

 `/etc/mkinitcpio.conf`  `HOOKS=(base **systemd** ... block **sd-lvm2** filesystems)` 

Depois, você pode continuar com as instruções normais de instalação com a etapa [criar uma ramdisk inicial](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio").

**Dica:**

*   Os hooks `lvm2` e `sd-lvm2` são instalados por [lvm2](https://www.archlinux.org/packages/?name=lvm2), não [mkinitcpio](https://www.archlinux.org/packages/?name=mkinitcpio). Se estiver executando *mkinitcpio* em *arch-chroot* para uma nova instalação, [lvm2](https://www.archlinux.org/packages/?name=lvm2) deve ser instalado dentro do *arch-chroot* para *mkinitcpio* para encontrar os hooks `lvm2` ou `sd-lvm2`. Se [lvm2](https://www.archlinux.org/packages/?name=lvm2) existir apenas fora de *arch-chroot*, *mkinitcpio* irá dar a saída `Error: Hook 'lvm2' cannot be found`.
*   Se a raiz de seu sistema de arquivos está em LVM RAID, veja [#Configurar mkinitcpio para RAID](#Configurar_mkinitcpio_para_RAID).

### Opções de carregamento do kernel

Se a raiz do sistema de arquivos estiver em um volume lógico, o [parâmetro do kernel](/index.php/Par%C3%A2metro_do_kernel "Parâmetro do kernel") `root=` deve ser apontado para o dispositivo mapeado, por exemplo `/dev/*nome-do-vg*/*nome-do-lv*`.