au

**Status de tradução:** Esse artigo é uma tradução de [EFI system partition](/index.php/EFI_system_partition "EFI system partition"). Data da última tradução: 2019-11-24\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=EFI_system_partition&diff=0&oldid=589005) na versão em inglês.

Artigos relacionados

*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface")
*   [Gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot")

A [partição de sistema EFI](https://en.wikipedia.org/wiki/EFI_system_partition "wikipedia:EFI system partition") (em inglês *EFI system partition*, abreviado como ESP) é uma partição independente do sistema operacional que atua como o local de armazenamento para os gerenciadores de boot, aplicativos e drivers EFI a serem lançados pelo firmware UEFI. É obrigatório para a inicialização do UEFI.

A especificação UEFI determina o suporte para os sistemas de arquivos FAT12, FAT16 e FAT32 (consulte a [especificação UEFI versão 2.7, seção 13.3.1.1](https://www.uefi.org/sites/default/files/resources/UEFI%20Spec%202_7_A%20Sept%206.pdf#G17.1019485)), mas qualquer fornecedor em conformidade pode, opcionalmente, adicionar suporte para sistemas de arquivos adicionais; por exemplo, o firmware em [Macs](/index.php/Mac "Mac") da Apple possui suporte ao sistema de arquivos HFS+.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Verificar uma partição existente](#Verificar_uma_partição_existente)
*   [2 Criar a partição](#Criar_a_partição)
    *   [2.1 Discos particionados em GPT](#Discos_particionados_em_GPT)
    *   [2.2 Discos particionados em MBR](#Discos_particionados_em_MBR)
*   [3 Formatar a partição](#Formatar_a_partição)
*   [4 Montar a partição](#Montar_a_partição)
    *   [4.1 Pontos de montagem comuns](#Pontos_de_montagem_comuns)
    *   [4.2 Pontos de montagem alternativos](#Pontos_de_montagem_alternativos)
        *   [4.2.1 Usando montagem com bind](#Usando_montagem_com_bind)
        *   [4.2.2 Usando systemd](#Usando_systemd)
        *   [4.2.3 Usando eventos do sistema de arquivos](#Usando_eventos_do_sistema_de_arquivos)
        *   [4.2.4 Usando hook do mkinitcpio](#Usando_hook_do_mkinitcpio)
        *   [4.2.5 Usando predefinição de mkinitcpio](#Usando_predefinição_de_mkinitcpio)
            *   [4.2.5.1 Substituindo o hook do mkinitcpio acima](#Substituindo_o_hook_do_mkinitcpio_acima)
            *   [4.2.5.2 Outro exemplo](#Outro_exemplo)
        *   [4.2.6 Usando hook do pacman](#Usando_hook_do_pacman)
*   [5 Problemas conhecidos](#Problemas_conhecidos)
    *   [5.1 ESP no RAID](#ESP_no_RAID)
*   [6 Veja também](#Veja_também)

## Verificar uma partição existente

Se você estiver instalando o Arch Linux em um computador compatível com UEFI com um sistema operacional instalado, como [Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows") 10 por exemplo, é muito provável que você já tenha uma partição do sistema EFI.

Para descobrir o esquema de partição de disco e a partição do sistema, use [fdisk](/index.php/Fdisk "Fdisk") como root no disco que você quer inicializar:

```
# fdisk -l /dev/sd*x*

```

O comando retorna:

*   A tabela de partições do disco: indica `Tipo de rótulo do disco: gpt` se a tabela de partições for [GPT](/index.php/GPT "GPT") ou `Tipo de rótulo do disco: dos` se for [MBR](/index.php/MBR "MBR").
*   A lista de partições no disco: Procure a partição do sistema EFI na lista, é uma partição pequena (normalmente cerca de 100–550 MiB) com um tipo `Sistema EFI` ou `EFI (FAT-12/16/32)`. Para confirmar isso é a ESP, [monte](/index.php/Mount "Mount") e verifique se ela contém um diretório chamado `EFI`, se contiver é definitivamente a ESP.

**Dica:** Para descobrir se é um sistema de arquivos FAT12, FAT16 ou FAT32, use `minfo` a partir de [mtools](https://www.archlinux.org/packages/?name=mtools).
```
# minfo -i /dev/sd*xY* :: | grep 'disk type'

```

**Atenção:** Ao usar *dual-boot*, evite reformatar a ESP, pois ela pode conter arquivos necessários para inicializar outros sistemas operacionais.

Se você encontrou uma partição do sistema EFI existente, simplesmente prossiga para [#Montar a partição](#Montar_a_partição). Se você não encontrou uma, você precisará criá-la, vá para [#Criar a partição](#Criar_a_partição).

## Criar a partição

As duas seções a seguir mostram como criar uma partição do sistema EFI (ESP).

**Atenção:** A partição do sistema EFI deve ser uma partição física na tabela de partição principal do disco, não sob LVM ou software RAID, etc.

**Nota:** Recomenda-se o uso de [GPT](/index.php/GPT "GPT"), pois alguns firmwares podem não suportar a inicialização via UEFI/MBR por não serem suportados pelo [Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows"). Veja também [Partitioning#Choosing between GPT and MBR](/index.php/Partitioning#Choosing_between_GPT_and_MBR "Partitioning") para as vantagens da GPT em geral.

Para fornecer espaço adequado para armazenar gerenciadores de boot e outros arquivos necessários para inicialização e para evitar problemas de interoperabilidade com outros sistemas operacionais[[1]](https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/configure-uefigpt-based-hard-drive-partitions#diskpartitionrules)[[2]](https://superuser.com/questions/1310927/what-is-the-absolute-minimum-size-a-uefi-partition-can-be/1310938) a partição deve ter pelo menos 260 MiB. Para implementações de UEFI precoces e/ou com bugs, o tamanho de pelo menos 512 MiB pode ser necessário.[[3]](https://www.rodsbooks.com/efi-bootloaders/principles.html)

### Discos particionados em GPT

Partição de sistema EFI em uma [Tabela de Partição GUID](/index.php/GUID_Partition_Table "GUID Partition Table") é identificada pelo [GUID de tipo de partição](https://en.wikipedia.org/wiki/pt:Tabela_de_Parti%C3%A7%C3%A3o_GUID#Tipos_de_parti.C3.A7.C3.A3o_GUID "wikipedia:pt:Tabela de Partição GUID") `C12A7328-F81F-11D2-BA4B-00A0C93EC93B`.

**Escolha um** dos métodos a seguir para criar uma ESP para um disco particionado em GPT:

*   [fdisk](/index.php/Fdisk "Fdisk"): Crie uma partição com o tipo de partição `EFI System`.
*   [gdisk](/index.php/Gdisk "Gdisk"): Crie uma partição com o tipo de partição `EF00`.
*   [GNU Parted](/index.php/GNU_Parted "GNU Parted"): Crie uma partição com `fat32` como o tipo de sistema de arquivos e defina a opção `esp` nela.

Continue com a seção [#Formatar a partição](#Formatar_a_partição) abaixo.

### Discos particionados em MBR

A partição do sistema EFI em uma tabela de partição [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record") é identificada pelo [ID de tipo de partição](https://en.wikipedia.org/wiki/pt:Tipo_de_parti%C3%A7%C3%A3o "wikipedia:pt:Tipo de partição") `EF`.

**Escolha um** dos métodos a seguir para criar uma ESP para um disco particionado em MBR:

*   [fdisk](/index.php/Fdisk "Fdisk"): Crie uma partição primária com o tipo de partição `EFI (FAT-12/16/32)`.
*   [GNU Parted](/index.php/GNU_Parted "GNU Parted"): Crie uma partição primária com `fat32` como o tipo de sistema de arquivos e defina a opção `esp` nela.

Continue com a seção [#Formatar a partição](#Formatar_a_partição) abaixo.

## Formatar a partição

A especificação UEFI determina o suporte para os sistemas de arquivos FAT12, FAT16 e FAT32[[4]](https://www.uefi.org/sites/default/files/resources/UEFI%20Spec%202_7_A%20Sept%206.pdf#G17.1019485). Para evitar possíveis problemas com outros sistemas operacionais e também porque a especificação UEFI apenas exige suporte a FAT16 e FAT12 em mídia removível[[5]](https://uefi.org/sites/default/files/resources/UEFI%20Spec%202_7_A%20Sept%206.pdf#G17.1345080), recomenda-se usar o FAT32.

Após criar a partição, [formate](/index.php/Format "Format")-a como [FAT32](/index.php/FAT32 "FAT32"). Para usar o utilitário `mkfs.fat`, [instale](/index.php/Instale "Instale") [dosfstools](https://www.archlinux.org/packages/?name=dosfstools).

```
# mkfs.fat -F32 /dev/sd*xY*

```

Se você receber a mensagem `WARNING: Not enough clusters for a 32 bit FAT!`, reduza o tamanho do cluster com `mkfs.fat -s2 -F32 ...` ou `-s1`; caso contrário, a partição pode ser ilegível pelo UEFI. Veja [mkfs.fat(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.fat.8) para os tamanhos de cluster suportados.

## Montar a partição

Os kernels, os arquivos initramfs e, na maioria dos casos, o [microcódigo](/index.php/Microcode "Microcode") do processador, precisam ser acessados pelo [gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot") ou pelo próprio UEFI para inicializar com sucesso o sistema. Portanto, se você quiser manter a configuração simples, sua opção de gerenciador de boot limita os pontos de montagem disponíveis para a partição do sistema EFI.

### Pontos de montagem comuns

Os cenários mais simples para montar uma partição de sistema EFI são:

*   [montar](/index.php/Mount "Mount") a ESP em `/efi` e usar um [gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot") que tem um driver para seu sistema de arquivos raiz (p.ex., [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)"), [rEFInd](/index.php/REFInd "REFInd")).
*   [montar](/index.php/Mount "Mount") a ESP em `/boot`. Esse é o método preferível ao inicializar diretamente um kernel de [EFISTUB](/index.php/EFISTUB_(Portugu%C3%AAs) "EFISTUB (Português)") do UEFI.

**Dica:**

*   `/efi` é um substituto[[6]](https://github.com/systemd/systemd/pull/3757#issuecomment-234290236) para o anterior e popular (e possivelmente ainda usado por outras distribuições) ponto de montagem ESP `/boot/efi`.
*   O diretório `/efi` não está disponível por padrão, de forma que você precisará primeiro criá-lo com [mkdir(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkdir.1) antes de montar a ESP nele.

### Pontos de montagem alternativos

Se você não usar um dos métodos simples de [#Montar a partição](#Montar_a_partição), você precisará copiar seus arquivos de inicialização para a ESP (referida daqui em diante como `*esp*`).

```
# mkdir -p *esp*/EFI/arch
# cp -a /boot/vmlinuz-linux *esp*/EFI/arch/
# cp -a /boot/initramfs-linux.img *esp*/EFI/arch/
# cp -a /boot/initramfs-linux-fallback.img *esp*/EFI/arch/

```

**Nota:** Você também pode precisar copiar o [microcódigo](/index.php/Microcode "Microcode") para o local da entrada de inicialização.

Além disso, você precisará manter os arquivos na ESP em dia com as atualizações posteriores do kernel. Não fazer isso pode resultar em um sistema não inicializável. As seções a seguir discutem vários mecanismos para automatizá-la.

**Nota:** Se a ESP não estiver montada em `/boot`, certifique-se de não confiar no [mecanismo de automontagem do systemd](/index.php/Fstab#Automount_with_systemd "Fstab") (incluindo o de [systemd-gpt-auto-generator(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-gpt-auto-generator.8)). Sempre monte-a manualmente antes de atualizar o sistema ou o kernel, caso contrário você pode não conseguir montá-la após a atualização, lhe travando no kernel em execução no momento sem a capacidade de atualizar a cópia do kernel na ESP.

Alternativamente, [carregue antecipadamente os módulos de kernel necessários na inicialização](/index.php/Kernel_module#Automatic_module_loading_with_systemd "Kernel module"), p.ex.:

 `/etc/modules-load.d/vfat.conf` 
```
vfat
nls_cp437
nls_iso8859-1

```

#### Usando montagem com bind

Em vez de montar o próprio ESP para `/boot`, você pode montar um diretório do ESP para `/boot` usando uma [montagem](/index.php/Mount "Mount") "bind" (consulte [mount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8)). Isto permite que [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") atualize o kernel diretamente enquanto mantém a ESP organizada ao seu gosto.

**Nota:**

*   Isso requer um [kernel](/index.php/FAT#Kernel_configuration "FAT") e [gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot") compatível com o FAT32\. Este não é um problema para uma instalação comum do Arch, mas pode ser problemático para outras distribuições (ou seja, aquelas que exigem links simbólicos em `/boot/`). Veja a postagem no fórum [arquivo](https://bbs.archlinux.org/viewtopic.php?pid=1331867#p1331867).
*   Você *deve* usar o [parâmetro do kernel](/index.php/Par%C3%A2metros_do_kernel#Lista_de_parâmetros "Parâmetros do kernel") `root=` para inicializar usando este método.

Assim como em [#Pontos de montagem alternativos](#Pontos_de_montagem_alternativos), copie todos os arquivos de inicialização para um diretório em sua ESP, mas monte a ESP **fora** do `/boot`. Em seguida, associe o diretório:

```
# mount --bind *esp*/EFI/arch /boot

```

Após confirmar o sucesso, edite seu [Fstab](/index.php/Fstab "Fstab") para tornar as alterações persistentes:

 `/etc/fstab` 
```
*esp*/EFI/arch /boot none defaults,bind 0 0

```

#### Usando systemd

O [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") apresenta tarefas acionadas por eventos. Nesse caso específico, a capacidade de detectar uma alteração no caminho é usada para sincronizar os arquivos kernel EFISTUB e initramfs quando eles são atualizados em `/boot/`. O arquivo assistido por alterações é o `initramfs-linux-fallback.img`, pois este é o último arquivo construído pelo mkinitcpio, para garantir que todos os arquivos tenham sido construídos antes de iniciar a cópia. Os arquivos de caminho e serviço *systemd* a serem criados são:

 `/etc/systemd/system/efistub-update.path` 
```
[Unit]
Description=Copy EFISTUB Kernel to EFI system partition

[Path]
PathChanged=/boot/initramfs-linux-fallback.img

[Install]
WantedBy=multi-user.target
WantedBy=system-update.target
```
 `/etc/systemd/system/efistub-update.service` 
```
[Unit]
Description=Copy EFISTUB Kernel to EFI system partition

[Service]
Type=oneshot
ExecStart=/usr/bin/cp -af /boot/vmlinuz-linux *esp*/EFI/arch/
ExecStart=/usr/bin/cp -af /boot/initramfs-linux.img *esp*/EFI/arch/
ExecStart=/usr/bin/cp -af /boot/initramfs-linux-fallback.img *esp*/EFI/arch/
```

Então, [habilite](/index.php/Habilite "Habilite") e [inicie](/index.php/Inicie "Inicie") `efistub-update.path`.

**Dica:** Para [Secure Boot](/index.php/Secure_Boot "Secure Boot") com suas próprias chaves, você pode configurar o serviço para também assinar a imagem usando [sbsigntools](https://www.archlinux.org/packages/?name=sbsigntools): `ExecStart=/usr/bin/sbsign --key */caminho/para/bd.key* --cert */caminho/para/bd.crt* --output *esp*/EFI/arch/vmlinuz-linux /boot/vmlinuz-linux` 

#### Usando eventos do sistema de arquivos

[Eventos de sistemas de arquivos](/index.php/Inicializa%C3%A7%C3%A3o_autom%C3%A1tica#Em_eventos_de_sistemas_de_arquivos "Inicialização automática") podem ser usados para executar um script sincronizando o kernel EFISTUB após atualizações do kernel. Um exemplo com [incron](/index.php/Incron_(Portugu%C3%AAs) "Incron (Português)") a seguir:

 `/usr/local/bin/efistub-update` 
```
#!/bin/sh
cp -af /boot/vmlinuz-linux *esp*/EFI/arch/
cp -af /boot/initramfs-linux.img *esp*/EFI/arch/
cp -af /boot/initramfs-linux-fallback.img *esp*/EFI/arch/

```

**Nota:** O primeiro parâmetro `/boot/initramfs-linux-fallback.img` é o arquivo a ser observado. O segundo parâmetro `IN_CLOSE_WRITE` é a ação a ser observada. O terceiro parâmetro `/usr/local/bin/efistub-update` é o script a ser executado.
 `/etc/incron.d/efistub-update.conf` 
```
/boot/initramfs-linux-fallback.img IN_CLOSE_WRITE /usr/local/bin/efistub-update

```

Para usar este método, [habilite](/index.php/Habilite "Habilite") o `incrond.service`.

#### Usando hook do mkinitcpio

Mkinitcpio pode gerar um hook que não precisa de um daemon de nível de sistema para funcionar. Ele gera um processo de segundo plano que aguarda a geração de `vmlinuz`, `initramfs-linux.img` e `initramfs-linux-fallback.img` antes de copiar os arquivos.

Adicione `efistub-update` à lista de hooks em `/etc/mkinitcpio.conf`.

 `/etc/initcpio/install/efistub-update` 
```
#!/usr/bin/env bash
build() {
	/usr/local/bin/efistub-copy $$ &
}

help() {
	cat <<HELPEOF
This hook waits for mkinitcpio to finish and copies the finished ramdisk and kernel to the ESP
HELPEOF
}

```
 `/usr/local/bin/efistub-copy` 
```
#!/usr/bin/env bash

if [[ $1 -gt 0 ]]
then
	while [ -e /proc/$1 ]
	do
		sleep .5
	done
fi

rsync -a /boot/ *esp*/

echo "Synced /boot with ESP"

```

#### Usando predefinição de mkinitcpio

Como as predefinições em `/etc/mkinitcpio.d/` possuem suporte a script shell, o kernel e initramfs podem ser copiados apenas editando as predefinições.

##### Substituindo o hook do mkinitcpio acima

Edite o arquivo `/etc/mkinitcpio.d/linux.preset`:

 `/etc/mkinitcpio.d/linux.preset` 
```
# mkinitcpio preset file for the 'linux' package

# Directory to copy the kernel, the initramfs...
ESP_DIR="''esp''/EFI/arch"

ALL_config="/etc/mkinitcpio.conf"
ALL_kver="${ESP_DIR}/vmlinuz-linux"
cp -af /boot/vmlinuz-linux "${ESP_DIR}/"
[[ -e /boot/intel-ucode.img ]] && cp -af /boot/intel-ucode.img "${ESP_DIR}/"
[[ -e /boot/amd-ucode.img ]] && cp -af /boot/amd-ucode.img "${ESP_DIR}/"

PRESETS=('default' 'fallback')

#default_config="/etc/mkinitcpio.conf"
default_image="${ESP_DIR}/initramfs-linux.img"
default_options="-A esp-update-linux"

#fallback_config="/etc/mkinitcpio.conf"
fallback_image="${ESP_DIR}/initramfs-linux-fallback.img"
fallback_options="-S autodetect"

```

Para testar isso, basta executar:

```
# rm /boot/initramfs-linux-fallback.img
# rm /boot/initramfs-linux.img
# mkinitcpio -p linux

```

##### Outro exemplo

 `/etc/mkinitcpio.d/0.preset` 
```
ESP_DIR="*esp*/EFI/arch"
cp -af "/boot/vmlinuz-linux${suffix}" "$ESP_DIR/"
ALL_config="/etc/mkinitcpio.conf"
ALL_kver="$ESP_DIR/vmlinuz-linux${suffix}"
PRESETS=('default')
default_config="/etc/mkinitcpio.conf"
default_image="$ESP_DIR/initramfs-linux${suffix}.img"
```
 `/etc/mkinitcpio.d/linux.preset` 
```
source /etc/mkinitcpio.d/0.preset

```
 `/etc/mkinitcpio.d/linux-zen.preset` 
```
suffix='-zen'
source /etc/mkinitcpio.d/0.preset
```

#### Usando hook do pacman

Uma última opção depende dos [hooks do pacman](/index.php/Hooks_do_pacman "Hooks do pacman") que são executados no final da transação.

O primeiro arquivo é um hook que monitora os arquivos relevantes e é executado se eles foram modificados na transação anterior.

 `/etc/pacman.d/hooks/999-kernel-efi-copy.hook` 
```
[Trigger]
Type = File
Operation = Install
Operation = Upgrade
Target = usr/lib/modules/*/vmlinuz
Target = usr/lib/initcpio/*
Target = boot/*-ucode.img

[Action]
Description = Copying linux and initramfs to EFI directory...
When = PostTransaction
Exec = /usr/local/bin/kernel-efi-copy.sh

```

O segundo arquivo é o próprio script. Crie o arquivo e torne-o [executável](/index.php/Execut%C3%A1vel "Executável"):

 `/usr/local/bin/kernel-efi-copy.sh` 
```
#!/usr/bin/env bash
#
# Copy kernel and initramfs images to EFI directory
#

ESP_DIR="*esp*/EFI/arch"

for file in /boot/vmlinuz*
do
        cp -af "$file" "$ESP_DIR/$(basename "$file").efi"
        [[ $? -ne 0 ]] && exit 1
done

for file in /boot/initramfs*
do
        cp -af "$file" "$ESP_DIR/"
        [[ $? -ne 0 ]] && exit 1
done

[[ -e /boot/intel-ucode.img ]] && cp -af /boot/intel-ucode.img "$ESP_DIR/"
[[ -e /boot/amd-ucode.img ]] && cp -af /boot/amd-ucode.img "$ESP_DIR/"

exit 0

```

## Problemas conhecidos

### ESP no RAID

É possível tornar a ESP parte de uma matriz RAID1, mas isso traz o risco de corrupção de dados, e outras considerações precisam ser feitas ao criar a ESP. Veja [[7]](https://bbs.archlinux.org/viewtopic.php?pid=1398710#p1398710) e [[8]](https://bbs.archlinux.org/viewtopic.php?pid=1390741#p1390741) para detalhes.

Veja [Inicialização com UEFI e RAID1](https://outflux.net/blog/archives/2018/04/19/uefi-booting-and-raid1/) (em inglês) para um guia mais aprofundado.

A parte principal é usar `--metadata 1.0` para manter os metadados RAID no final da partição, caso contrário o firmware não poderá acessá-los:

```
# mdadm --create --verbose --level=1 **--metadata=1.0** --raid-devices=2 /dev/md/ESP /dev/sda*X* /dev/sdb*Y*

```

## Veja também

*   [A partição de sistema EFI e o comportamento de inicialização padrão](https://blog.uncooperative.org/blog/2014/02/06/the-efi-system-partition/)