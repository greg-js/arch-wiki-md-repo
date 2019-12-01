Os exemplos a seguir são cenários comuns de um sistema criptografado com *dm-crypt*. Eles explicam todas as adaptações que serão realizadas do [processo de instalação](/index.php/Guia_de_instala%C3%A7%C3%A3o "Guia de instalação"). Todas as ferramentas necessárias estão disponíveis na [imagem de instalação](https://www.archlinux.org/download/).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Visão geral](#Visão_geral)
*   [2 LUKS dentro de uma partição](#LUKS_dentro_de_uma_partição)
    *   [2.1 Preparando o disco](#Preparando_o_disco)
    *   [2.2 Preparando partições que não são de boot](#Preparando_partições_que_não_são_de_boot)
    *   [2.3 Preparando a partição de boot](#Preparando_a_partição_de_boot)
    *   [2.4 Mountando os dispositivos](#Mountando_os_dispositivos)
    *   [2.5 Configurando o mkinitcpio](#Configurando_o_mkinitcpio)
    *   [2.6 Configurando o gerenciador de boot](#Configurando_o_gerenciador_de_boot)
*   [3 LVM dentro do LUKS](#LVM_dentro_do_LUKS)
    *   [3.1 Preparando o disco](#Preparando_o_disco_2)
    *   [3.2 Preparando os volumes lógicos](#Preparando_os_volumes_lógicos)
    *   [3.3 Preparando a partição de inicialização](#Preparando_a_partição_de_inicialização)
    *   [3.4 Configurando o mkinitcpio](#Configurando_o_mkinitcpio_2)
    *   [3.5 Configurando o gerenciador de boot](#Configurando_o_gerenciador_de_boot_2)
*   [4 LUKS dentro do LVM](#LUKS_dentro_do_LVM)
    *   [4.1 Preparing the disk](#Preparing_the_disk)
    *   [4.2 Preparing the logical volumes](#Preparing_the_logical_volumes)
    *   [4.3 Preparing the boot partition](#Preparing_the_boot_partition)
    *   [4.4 Configuring mkinitcpio](#Configuring_mkinitcpio)
    *   [4.5 Configuring the boot loader](#Configuring_the_boot_loader)
    *   [4.6 Configuring fstab and crypttab](#Configuring_fstab_and_crypttab)
    *   [4.7 Encrypting logical volume /home](#Encrypting_logical_volume_/home)
*   [5 LUKS on software RAID](#LUKS_on_software_RAID)
    *   [5.1 Preparing the disks](#Preparing_the_disks)
    *   [5.2 Building the RAID array](#Building_the_RAID_array)
    *   [5.3 Preparing the block devices](#Preparing_the_block_devices)
    *   [5.4 Configuring GRUB](#Configuring_GRUB)
    *   [5.5 Creating the keyfiles](#Creating_the_keyfiles)
    *   [5.6 Configuring the system](#Configuring_the_system)
*   [6 Plain dm-crypt](#Plain_dm-crypt)
    *   [6.1 Preparing the disk](#Preparing_the_disk_2)
    *   [6.2 Preparing the non-boot partitions](#Preparing_the_non-boot_partitions)
    *   [6.3 Preparing the boot partition](#Preparing_the_boot_partition_2)
    *   [6.4 Configuring mkinitcpio](#Configuring_mkinitcpio_2)
    *   [6.5 Configuring the boot loader](#Configuring_the_boot_loader_2)
    *   [6.6 Post-installation](#Post-installation)
*   [7 Encrypted boot partition (GRUB)](#Encrypted_boot_partition_(GRUB))
    *   [7.1 Preparing the disk](#Preparing_the_disk_3)
    *   [7.2 Preparing the logical volumes](#Preparing_the_logical_volumes_2)
    *   [7.3 Configuring mkinitcpio](#Configuring_mkinitcpio_3)
    *   [7.4 Configuring GRUB](#Configuring_GRUB_2)
    *   [7.5 Avoiding having to enter the passphrase twice](#Avoiding_having_to_enter_the_passphrase_twice)
*   [8 Btrfs subvolumes with swap](#Btrfs_subvolumes_with_swap)
    *   [8.1 Preparing the disk](#Preparing_the_disk_4)
    *   [8.2 Preparing the system partition](#Preparing_the_system_partition)
        *   [8.2.1 Create LUKS container](#Create_LUKS_container)
        *   [8.2.2 Unlock LUKS container](#Unlock_LUKS_container)
        *   [8.2.3 Format mapped device](#Format_mapped_device)
        *   [8.2.4 Mount mapped device](#Mount_mapped_device)
    *   [8.3 Creating btrfs subvolumes](#Creating_btrfs_subvolumes)
        *   [8.3.1 Layout](#Layout)
        *   [8.3.2 Create top-level subvolumes](#Create_top-level_subvolumes)
        *   [8.3.3 Mount top-level subvolumes](#Mount_top-level_subvolumes)
        *   [8.3.4 Create nested subvolumes](#Create_nested_subvolumes)
        *   [8.3.5 Mount ESP](#Mount_ESP)
    *   [8.4 Configuring mkinitcpio](#Configuring_mkinitcpio_4)
        *   [8.4.1 Create keyfile](#Create_keyfile)
        *   [8.4.2 Edit mkinitcpio.conf](#Edit_mkinitcpio.conf)
    *   [8.5 Configuring the boot loader](#Configuring_the_boot_loader_3)
    *   [8.6 Configuring swap](#Configuring_swap)

## Visão geral

*dm-crypt* se destaca, tanto em funcionalidades quanto em velocidade, quando o assunto é proteger o sistema de arquivos principal. Diferente da encriptação seletiva de sistemas de arquivos secundários, a criptografia de todo um sistema pode proteger informações como quais programas estão instalados, os nomes de usuários de todas as contas, e vetores comuns de vazamento de dados tais como [mlocate](/index.php/Mlocate "Mlocate") e `/var/log`. E, é bem mais difícil fazer alterações em um sistema criptografado, exceto o [gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot") e (geralmente) o kernel que nao são criptografados.

Todos os cenários ilustrados a seguir compartilham as vantagens supracitadas, prós e contras que os diferenciam estão resumidos abaixo:

| Cenários | Vantagens | Desvantagens |
| [#LUKS dentro de uma partição](#LUKS_dentro_de_uma_partição)

Mostra uma configuração básica e direta para uma partição principal criptografada com LUKS.

 | 

*   Simples particionamento e configuração

 | 

*   Inflexível; o espaço em disco precisa ser alocado antes de criptografar

 |
| [#LVM dentro do LUKS](#LVM_dentro_do_LUKS)

Consegue flexibilidade no particionamento ao usar LVM dentro de uma partição criptografada com LUKS.

 | 

*   Simples particionamento se sabe como usar LVM
*   Somente uma chave para desbloquear todos os volumes (exemplo, configuração simples de resume-from-disk)
*   design de volumes não é visível quando bloqueado
*   Método mais fácil para [suspensão para o disco](/index.php/Dm-crypt/Swap_encryption#With_suspend-to-disk_support "Dm-crypt/Swap encryption")

 | 

*   LVM adiciona mais uma camada adicional de mapeamento e hook
*   Menos útil, se um volume deve receber uma chave separada

 |
| [#LUKS dentro do LVM](#LUKS_dentro_do_LVM)

usa dm-crypt somente depois de configurar o LVM.

 | 

*   LVM pode ser usado para volumes criptografados em múltiplos discos
*   Fácil de usar com grupos de volumes criptografados ou não

 | 

*   Complexo; para mudar volumes precisa modificar também os mapeadores de encriptação
*   Volumes precisam de chaves individuais
*   design de volumes não é visível quando bloquead

 |
| [#LUKS dentro do RAID de software](#LUKS_dentro_do_RAID_de_software)

usa dm-crypt somente depois de configurar RAID.

 | 

*   Análogo ao LUKS dentro do LVM

 | 

*   Análogo ao LUKS dentro do LVM

 |
| [#Plain dm-crypt](#Plain_dm-crypt)

usa o modo plain dm-crypt, exemplo sem um cabeçalho LUKS e suas opções para múltiplas chaves.
Este cenário também permite que dispositivos USB possam ser usados no `/boot` e como depósito de chaves, que pode ser aplicado para outros cenários.

 | 

*   Melhor em relação aos dados para casos onde um cabeçalho do LUKS é danificado
*   Permite [encriptação total de disco](https://en.wikipedia.org/wiki/Disk_encryption#Full_disk_encryption "wikipedia:Disk encryption")
*   Ajuda a solucionar [problemas](/index.php/Dm-crypt/Specialties#Discard/TRIM_support_for_solid_state_drives_(SSD) "Dm-crypt/Specialties") com SSDs

 | 

*   Necessário grande atenção a todos os parâmetros
*   Encriptação de chave única e sem opção de mudança

 |
| [#Partição de boot criptografada (GRUB)](#Partição_de_boot_criptografada_(GRUB))

Mostra como criptografar a partição de boot usando o gerenciador de boot GRUB.
Este cenário também usa uma partição de sistema EFI, que pode ser aplicado para outros cenários.

 | 

*   Mesmas vantagens do cenário de instalação en que é baseado (LVM dentro do LUKS neste particular exemplo)
*   Menos dados são deixados sem criptografia, exemplo o gerenciador de boot e a partição de sistema EFI, se presente

 | 

*   Mesmas desvantagens do cenário de instalação en que é baseado (LVM dentro do LUKS neste particular exemplo)
*   Configuração mais complicada
*   Não é suportado por outros gerenciadores de boot

 |
| [#Subvolumes do btrfs com swap](#Subvolumes_do_btrfs_com_swap)

Mostra como criptografar um sistema [Btrfs](/index.php/Btrfs "Btrfs"), incluindo o diretório `/boot`, também é possível adicionar uma partição para swap, em um hardware com suporte a UEFI.

 | 

*   similar a [#Partição de boot criptografada (GRUB)](#Partição_de_boot_criptografada_(GRUB))
*   Disponibilidade das funcionalidades do Btrfs

 | 

*   Similar a [#Partição de boot criptografada (GRUB)](#Partição_de_boot_criptografada_(GRUB))

 |

Enquanto todos os cenários acima oferecem maior proteção contra ameaças externas do que somente criptografar sistemas de arquivos não raiz, eles também possuem uma desvantagem comum: qualquer usuário que possui a chave pode abrir todo o disco, e assim, acessar os dados de outro usuário. Se isto é uma preocupação, é possível fazer uma combinação de dispositivo de blocos e sistema de arquivos criptografados empilhados e adquirir as vantagens de ambos. Veja [Encriptação de disco](/index.php/Disk_encryption "Disk encryption") para lhe ajudar no planejamento.

Veja [Dm-crypt/Preparando a unidade de armazenamento#Particionamento](/index.php/Dm-crypt/Preparando_a_unidade_de_armazenamento#Particionamento "Dm-crypt/Preparando a unidade de armazenamento") para uma visão geral das estratégias de particionamento usadas nos cenários.

Outra coisa a considerar é se deve usar uma partição swap criptografada e de qual forma. Veja [Dm-crypt/Swap criptografada](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption") para alternativas.

Se você antecipa a proteção de dados do sistema não somente contra roubo físico, como também contra adulteração lógica, veja [Dm-crypt/Especificidades#Protegendo a partição de boot não criptografada](/index.php/Dm-crypt/Specialties#Securing_the_unencrypted_boot_partition "Dm-crypt/Specialties") para possibilidades futuras após seguir um dos cenários.

Para [SSDs](/index.php/Solid_state_drive "Solid state drive"), você pode considerar habilitar suporte ao TRIM, mas esteja ciente que, isto tem potenciais problemas de segurança. Veja [Dm-crypt/Especificidades#Discard/Suporte ao TRIM para unidades de estado sólido (SSD)](/index.php/Dm-crypt/Specialties#Discard/TRIM_support_for_solid_state_drives_(SSD) "Dm-crypt/Specialties") para mais informações.

**Atenção:**

*   Em qualquer cenário, nunca diretamente repare um volume criptografado com ferramentas de reparação de sistema de arquivos como [fsck](/index.php/Fsck "Fsck"), ou isto destruirá qualquer chance de recuperar a chave usada para abrir seus arquivos. Tais ferramentas devem ser usadas no dispositivo desbloqueado (aberto).
*   para o formato LUKS2:

```
[GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)") não suporta LUKS2.[[1]](https://savannah.gnu.org/bugs/?55093) Use LUKS1 em partições que o GRUB precisa ter acesso.
o formato LUKS2 tem grande uso de RAM por escolha de design, o padrão é 1GB por mapeador criptografado. Máquinas com pouca RAM e/ou múltiplas partições LUKS2 abertas em paralelo podem falhar na inicialização. Veja a opção `--pbkdf-memory` para controlar o uso de memória.[[2]](https://gitlab.com/cryptsetup/cryptsetup/issues/372)

```

## LUKS dentro de uma partição

Este exemplo demonstra um sistema criptografado com *dm-crypt* + LUKS dentro de uma partição:

```
+--------------------+-------------------------------+-----------------------+
| Partição de boot   | Sistema criptogrado com LUKS2 | Espaço livre opcional |
|                    | partição                      | para outras partições |
|                    |                               | ou swap               |
| /boot              | /                             |                       |
|                    |                               |                       |
|                    | /dev/mapper/cryptroot         |                       |
|                    |-------------------------------|                       |
| /dev/sda1          | /dev/sda2                     |                       |
+--------------------+-------------------------------+-----------------------+

```

Os primeiros passos podem ser executados imediatamente após iniciar a imagem de instalação do Arch Linux.

### Preparando o disco

Antes de criar qualquer partição, você deveria saber a importância e também métodos de como apagar o disco com segurança, descritos em [dm-crypt/Preparando a unidade de armazenamento](/index.php/Dm-crypt/Preparando_a_unidade_de_armazenamento "Dm-crypt/Preparando a unidade de armazenamento").

Crie as partições necessárias, ao menos uma para `/` (exemplo `/dev/sda2`) e `/boot` (`/dev/sda1`). Veja [Particionamento](/index.php/Partitioning "Partitioning").

### Preparando partições que não são de boot

Os comandos a seguir criam e montam a partição raiz criptografada. Eles correspondem ao detalhado procedimento descrito em [dm-crypt/Criptografando um sistema de arquivos não raiz#Particionamento](/index.php/Dm-crypt/Criptografando_um_sistema_de_arquivos_n%C3%A3o_raiz#Particionamento "Dm-crypt/Criptografando um sistema de arquivos não raiz") (que, apesar do título, *pode* ser aplicado a partições raiz, contanto que [mkinitcpio](#Configurando_o_mkinitcpio) e o [gerenciador de boot](#Configurando_o_gerenciador_de_boot) sejam corretamente configurados). Se você deseja usar opções de encriptação que não são padrão (exemplo, cifras criptográficas, tamanho da chave), veja as [opções de encriptação](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") antes de executar o primeiro comando:

```
# cryptsetup -y -v luksFormat /dev/sda2
# cryptsetup open /dev/sda2 cryptroot
# mkfs.ext4 /dev/mapper/cryptroot
# mount /dev/mapper/cryptroot /mnt

```

Verifique se o mapeamento funcionou como esperado:

```
# umount /mnt
# cryptsetup close cryptroot
# cryptsetup open /dev/sda2 cryptroot
# mount /dev/mapper/cryptroot /mnt

```

Se você criou partições separadas (exemplo, `/home`), estes passos têm que ser adaptados e repetidos para todos eles, *exceto* para `/boot`. Veja [dm-crypt/Criptografando um sistema de arquivos não raiz#Desbloqueio e montagem automatizados](/index.php/Dm-crypt/Criptografando_um_sistema_de_arquivos_n%C3%A3o_raiz#Desbloqueio_e_montagem_automatizados "Dm-crypt/Criptografando um sistema de arquivos não raiz") para como manusear partições adicionais na inicialização.

Note que cada dispositivo de bloco precisa de sua própria senha. Isto pode ser inconveniente, por ser necessário inserir senhas separadas durante a inicialização. Uma alternativa é usar uma keyfile guardada na partição do sistema para desbloquear a partição separada por meio do `crypttab`. Veja [dm-crypt/Encriptação de dispositivo#Usando LUKS para formatar partições com uma keyfile](/index.php/Dm-crypt/Device_encryption#Using_LUKS_to_format_partitions_with_a_keyfile "Dm-crypt/Device encryption") para instruções.

### Preparando a partição de boot

O que você vai precisar fazer é uma partição para `/boot` não criptografada, que é necessária pelo sistema. Para uma partição ordinária em sistemas BIOS, por exemplo, execute:

```
# mkfs.ext4 /dev/sda1

```

Ou para uma [Partição de sistema EFI](/index.php/Parti%C3%A7%C3%A3o_de_sistema_EFI "Partição de sistema EFI") em sistemas UEFI:

```
# mkfs.fat -F32 /dev/sda1

```

Depois crie o diretório e monte a partição:

```
# mkdir /mnt/boot
# mount /dev/sda1 /mnt/boot

```

### Mountando os dispositivos

no [Guia de instalação#Montar os sistemas de arquivos](/index.php/Guia_de_instala%C3%A7%C3%A3o#Montar_os_sistemas_de_arquivos "Guia de instalação") você vai precisar montar os dispositivos criptografados, não as partições. Claro `/boot`, que não é criptografado, ainda precisará ser montado diretamente.

### Configurando o mkinitcpio

Adicione os hooks `keyboard`, `keymap` e `encrypt` em [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"). Se deseja padrão de teclado US, você pode omitir o hook `keymap`.

```
HOOKS=(base **udev** autodetect **keyboard** **keymap** consolefont modconf block **encrypt** filesystems fsck)

```

Se está usando o hook [sd-encrypt](/index.php/Sd-encrypt "Sd-encrypt") com o initramfs baseado no systemd, o seguinte precisa ser definido ao invês:

```
HOOKS=(base **systemd** autodetect **keyboard** **sd-vconsole** modconf block **sd-encrypt** filesystems fsck)

```

Dependendo de quais hooks estão sendo usados, a ordem pode ser relevante. Veja [dm-crypt/Configuração do sistema#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") para detalhes e outros hooks que você pode precisar.

### Configurando o gerenciador de boot

Para desbloquear a partição raiz criptografada na inicialização, os seguintes [parâmetros do kernel](/index.php/Par%C3%A2metros_do_kernel "Parâmetros do kernel") devem ser adicionados ao gerenciador de boot:

```
cryptdevice=UUID=*UUID-da-partição-raiz*:cryptroot root=/dev/mapper/cryptroot

```

Se está usando o hook [sd-encrypt](/index.php/Sd-encrypt "Sd-encrypt"), o seguinte precisa ser definido ao invês:

```
rd.luks.name=*UUID-da-partição-raiz*=cryptroot root=/dev/mapper/cryptroot

```

Veja [dm-crypt/Configurações do sistema#Gerenciador de boot](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") para detalhes.

o `*UUID-da-partição-raiz*` é para ser substituído pelo UUID da partição raiz, nesse caso `/dev/sda2`. Veja [Nomeação persistente de dispositivo de bloco](/index.php/Nomea%C3%A7%C3%A3o_persistente_de_dispositivo_de_bloco "Nomeação persistente de dispositivo de bloco") para detalhes.

## LVM dentro do LUKS

O método mais direto é configurar o [LVM](/index.php/LVM "LVM") em cima da partição criptografada ao invés do contrário. Tecnicamente o LVM está dentro de um grande dispositivo de bloco criptografado. Em razão disso, o LVM não é transparente até que o dispositivo de bloco seja aberto e o volume estruturado abaixo seja escaneado e montado durante a inicialização.

O design do disco neste exemplo é::

```
+-----------------------------------------------------------------------+ +------------------+
| volume lógico 1       | volume lógico 2       | volume Lógico 3       | | Partição de boot |
|                       |                       |                       | |                  |
| [SWAP]                | /                     | /home                 | | /boot            |
|                       |                       |                       | |                  |
| /dev/MeuGrupoVol/swap | /dev/MeuGrupoVol/raiz | /dev/MeuGrupoVol/home | | (pode ser        |
|_ _ _ _ _ _ _ _ _ _ _ _|_ _ _ _ _ _ _ _ _ _ _ _|_ _ _ _ _ _ _ _ _ _ _ _| | em outro         |
|                                                                       | | dispositivo)     |
|                         Partição criptografada com LUKS2              | |                  |
|                           /dev/sda1                                   | | /dev/sdb1        |
+-----------------------------------------------------------------------+ +------------------+

```

**Nota:** Ao usar o hook `encrypt`, você não poderá utilizar volumes lógicos espalhados em múltiplos discos; use o [sd-encrypt](/index.php/Sd-encrypt "Sd-encrypt") ou veja [dm-crypt/Especificidades#Modificando o hook encrypt para múltiplas partições](/index.php/Dm-crypt/Specialties#Modifying_the_encrypt_hook_for_multiple_partitions "Dm-crypt/Specialties").

**Dica:** Duas variações dessa configuração:

*   Instruções em [dm-crypt/Especificidades#Sistema criptografado com cabeçalho do LUKS desanexado](/index.php/Dm-crypt/Specialties#Encrypted_system_using_a_detached_LUKS_header "Dm-crypt/Specialties") para usar um cabeçalho do LUKS em um dispositivo USB, e assim conseguindo autentificação de dois fatores com este método.
*   Instruções em [dm-crypt/Especificidades#/boot criptografado e um cabeçalho do LUKS desanexado dentro de um USB](/index.php/Dm-crypt/Specialties#Encrypted_/boot_and_a_detached_LUKS_header_on_USB "Dm-crypt/Specialties")]] para usar um cabeçalho do LUKS, partição `/boot` criptografada, e keyfile criptografada tudo em um dispositivo USB.

### Preparando o disco

Antes de criar qualquer partição, você deveria saber a importância e também métodos de como apagar o disco com segurança, descritos em [dm-crypt/Preparando a unidade de armazenamento](/index.php/Dm-crypt/Preparando_a_unidade_de_armazenamento "Dm-crypt/Preparando a unidade de armazenamento").

**Dica:** Se usa o gerenciador de boot [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)") para inicialização com BIOS de um disco [GPT](/index.php/GPT "GPT"), crie uma [Partição de inicialização de BIOS](/index.php/Parti%C3%A7%C3%A3o_de_inicializa%C3%A7%C3%A3o_de_BIOS "Partição de inicialização de BIOS").

Crie uma partição que será montada em `/boot` com o tamanho de 200 MiB ou mais.

**Dica:** sistemas UEFI systems podem usar a [Partição de sistema EFI](/index.php/Parti%C3%A7%C3%A3o_de_sistema_EFI "Partição de sistema EFI") para a `/boot`.

Crie uma partição que depois irá conter o container criptografado.

Crie o container criptografado com LUKS na partição do *sistema*. Enter com a senha escolhida duas vezes.

```
# cryptsetup luksFormat /dev/sda1

```

Para mais informações sobre as opções disponíveis do cryptsetup veja as [opções de encriptação LUKS](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") antes de executar o comando acima.

abra o container:

```
# cryptsetup open /dev/sda1 cryptlvm

```

o container estará disponível em `/dev/mapper/cryptlvm`.

### Preparando os volumes lógicos

Crie um volume físico em cima do container LUKS aberto:

```
# pvcreate /dev/mapper/cryptlvm

```

Crie um grupo de volumes nomeado `MeuGrupoVol` (ou o que você desejar), e adicione ao, anteriormente criado, volume físico:

```
# vgcreate MeuGrupoVol /dev/mapper/cryptlvm

```

Crie todos os seus volumes lógicos no grupo de volumes:

```
# lvcreate -L 8G MeuGrupoVol -n swap
# lvcreate -L 32G MeuGrupoVol -n raiz
# lvcreate -l 100%FREE MeuGrupoVol -n home

```

Formate cada volume lógico para os sistemas de arquivos desejados:

```
# mkfs.ext4 /dev/MeuGrupoVol/raiz
# mkfs.ext4 /dev/MeuGrupoVol/home
# mkswap /dev/MeuGrupoVol/swap

```

Monte eles:

```
# mount /dev/MeuGrupoVol/raiz /mnt
# mkdir /mnt/home
# mount /dev/MeuGrupoVol/home /mnt/home
# swapon /dev/MeuGrupoVol/swap

```

### Preparando a partição de inicialização

O gerenciador de boot carrega o kernel, [initramfs](/index.php/Initramfs "Initramfs"), e seus arquivos de configuração do diretório `/boot`. Qualquer sistema de arquivos em um disco que pode ser lido pelo gerenciador de boot é elegível para uso.

Coloque um [sistema de arquivos](/index.php/Filesystem "Filesystem") na partição escolhida como `/boot`:

```
# mkfs.ext4 /dev/sdb1

```

**Dica:** Se optar por manter o `/boot` em uma [Partição de sistema EFI](/index.php/Parti%C3%A7%C3%A3o_de_sistema_EFI "Partição de sistema EFI") a formatação recomendada é
```
# mkfs.fat -F32 /dev/sdb1

```

Crie o diretório `/mnt/boot`:

```
# mkdir /mnt/boot

```

Monte a partição para `/mnt/boot`:

```
# mount /dev/sdb1 /mnt/boot

```

### Configurando o mkinitcpio

Adicione os hooks `keyboard`, `encrypt` e `lvm2` para o [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"):

```
HOOKS=(base **udev** autodetect **keyboard** **keymap** consolefont modconf block **encrypt** **lvm2** filesystems fsck)

```

Se está usando o hook [sd-encrypt](/index.php/Sd-encrypt "Sd-encrypt") com o initramfs baseado no systemd, o seguinte precisa ser definido ao invês:

```
HOOKS=(base **systemd** autodetect **keyboard** **sd-vconsole** modconf block **sd-encrypt** **sd-lvm2** filesystems fsck)

```

Veja [dm-crypt/Configuração do sistema#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") para detalhes e outros hooks que você pode precisar.

### Configurando o gerenciador de boot

Para desbloquear a partição raiz criptografada na inicialização, os seguintes parâmetros do kernel devem ser adicionados ao gerenciador de boot:

```
cryptdevice=UUID=*UUID-do-dispositivo*:cryptlvm root=/dev/MeuGrupoVol/raiz

```

Se está usando o hook [sd-encrypt](/index.php/Sd-encrypt "Sd-encrypt"), o seguinte precisa ser definido ao invês:

```
rd.luks.name=*UUID-do-dispositivo*=cryptlvm root=/dev/MeuGrupoVol/raiz

```

o `*UUID-do-dispositivo*` é para ser substituído pelo UUID da partição raiz, nesse caso `/dev/sda1`. Veja [Nomeação persistente de dispositivo de bloco](/index.php/Nomea%C3%A7%C3%A3o_persistente_de_dispositivo_de_bloco "Nomeação persistente de dispositivo de bloco") para mais detalhes.

Veja [dm-crypt/Configuração do sistema#Gerenciador de boot](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") para mais informação sobre.

## LUKS dentro do LVM

To use encryption on top of [LVM](/index.php/LVM "LVM"), the LVM volumes are set up first and then used as the base for the encrypted partitions. This way, a mixture of encrypted and non-encrypted volumes/partitions is possible as well.

**Tip:** Unlike [#LVM on LUKS](#LVM_on_LUKS), this method allows normally spanning the logical volumes over multiple disks.

The following short example creates a LUKS on LVM setup and mixes in the use of a key-file for the /home partition and temporary crypt volumes for `/tmp` and `/swap`. The latter is considered desirable from a security perspective, because no potentially sensitive temporary data survives the reboot, when the encryption is re-initialised. If you are experienced with LVM, you will be able to ignore/replace LVM and other specifics according to your plan.

If you want to span a logical volume over multiple disks that have already been set up, or expand the logical volume for `/home` (or any other volume), a procedure to do so is described in [dm-crypt/Specialties#Expanding LVM on multiple disks](/index.php/Dm-crypt/Specialties#Expanding_LVM_on_multiple_disks "Dm-crypt/Specialties"). It is important to note that the LUKS encrypted container has to be resized as well.

### Preparing the disk

Partitioning scheme:

```
+----------------+-------------------------------------------------------------------------------------------------+
| Boot partition | dm-crypt plain encrypted volume | LUKS2 encrypted volume        | LUKS2 encrypted volume        |
|                |                                 |                               |                               |
| /boot          | [SWAP]                          | /                             | /home                         |
|                |                                 |                               |                               |
|                | /dev/mapper/swap                | /dev/mapper/root              | /dev/mapper/home              |
|                |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _|_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _|_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _|
|                | Logical volume 1                | Logical volume 2              | Logical volume 3              |
|                | /dev/MyVolGroup/cryptswap       | /dev/MyVolGroup/cryptroot     | /dev/MyVolGroup/crypthome     |
|                |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _|_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _|_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _|
|                |                                                                                                 |
|   /dev/sda1    |                                   /dev/sda2                                                     |
+----------------+-------------------------------------------------------------------------------------------------+

```

Randomise `/dev/sda2` according to [dm-crypt/Drive preparation#dm-crypt wipe on an empty disk or partition](/index.php/Dm-crypt/Drive_preparation#dm-crypt_wipe_on_an_empty_disk_or_partition "Dm-crypt/Drive preparation").

### Preparing the logical volumes

```
# pvcreate /dev/sda2
# vgcreate MyVolGroup /dev/sda2
# lvcreate -L 32G -n cryptroot MyVolGroup
# lvcreate -L 500M -n cryptswap MyVolGroup
# lvcreate -L 500M -n crypttmp MyVolGroup
# lvcreate -l 100%FREE -n crypthome MyVolGroup

```

```
# cryptsetup luksFormat /dev/MyVolGroup/cryptroot
# cryptsetup open /dev/MyVolGroup/cryptroot root
# mkfs.ext4 /dev/mapper/root
# mount /dev/mapper/root /mnt

```

More information about the encryption options can be found in [dm-crypt/Device encryption#Encryption options for LUKS mode](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption"). Note that `/home` will be encrypted in [#Encrypting logical volume /home](#Encrypting_logical_volume_/home).

**Tip:** If you ever have to access the encrypted root from the Arch-ISO, the above `open` action will allow you to after the [LVM shows up](/index.php/LVM#Logical_Volumes_do_not_show_up "LVM").

### Preparing the boot partition

```
# dd if=/dev/zero of=/dev/sda1 bs=1M status=progress
# mkfs.ext4 /dev/sda1
# mkdir /mnt/boot
# mount /dev/sda1 /mnt/boot

```

### Configuring mkinitcpio

Add the `keyboard`, `lvm2` and `encrypt` hooks to [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"):

```
HOOKS=(base **udev** autodetect **keyboard** **keymap** consolefont modconf block **lvm2** **encrypt** filesystems fsck)

```

If using the [sd-encrypt](/index.php/Sd-encrypt "Sd-encrypt") hook with the systemd-based initramfs, the following needs to be set instead:

```
HOOKS=(base **systemd** autodetect **keyboard** **sd-vconsole** modconf block **sd-encrypt** **sd-lvm2** filesystems fsck)

```

See [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") for details and other hooks that you may need.

### Configuring the boot loader

In order to unlock the encrypted root partition at boot, the following [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") need to be set by the boot loader:

```
cryptdevice=UUID=*device-UUID*:root root=/dev/mapper/root

```

If using the [sd-encrypt](/index.php/Sd-encrypt "Sd-encrypt") hook, the following need to be set instead:

```
rd.luks.name=*device-UUID*=root root=/dev/mapper/root

```

The `*device-UUID*` refers to the UUID of `/dev/MyVolGroup/cryptroot`. See [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") for details.

See [dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") for details.

### Configuring fstab and crypttab

Both [crypttab](/index.php/Crypttab "Crypttab") and [fstab](/index.php/Fstab "Fstab") entries are required to both unlock the device and mount the filesystems, respectively. The following lines will re-encrypt the temporary filesystems on each reboot:

 `/etc/crypttab` 
```
swap	/dev/MyVolGroup/cryptswap	/dev/urandom	swap,cipher=aes-xts-plain64,size=256
tmp	/dev/MyVolGroup/crypttmp	/dev/urandom	tmp,cipher=aes-xts-plain64,size=256
```
 `/etc/fstab` 
```
/dev/mapper/root        /       ext4            defaults        0       1
/dev/sda1               /boot   ext4            defaults        0       2
/dev/mapper/tmp         /tmp    tmpfs           defaults        0       0
/dev/mapper/swap        none    swap            sw              0       0

```

### Encrypting logical volume /home

Since this scenario uses LVM as the primary and dm-crypt as secondary mapper, each encrypted logical volume requires its own encryption. Yet, unlike the temporary filesystems configured with volatile encryption above, the logical volume for `/home` should of course be persistent. The following assumes you have rebooted into the installed system, otherwise you have to adjust paths. To save on entering a second passphrase at boot, a [keyfile](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption") is created:

```
# mkdir -m 700 /etc/luks-keys
# dd if=/dev/random of=/etc/luks-keys/home bs=1 count=256 status=progress

```

The logical volume is encrypted with it:

```
# cryptsetup luksFormat -v /dev/MyVolGroup/crypthome /etc/luks-keys/home
# cryptsetup -d /etc/luks-keys/home open /dev/MyVolGroup/crypthome home
# mkfs.ext4 /dev/mapper/home
# mount /dev/mapper/home /home

```

The encrypted mount is configured in both [crypttab](/index.php/Crypttab "Crypttab") and [fstab](/index.php/Fstab "Fstab"):

 `/etc/crypttab` 
```
home	/dev/MyVolGroup/crypthome   /etc/luks-keys/home

```
 `/etc/fstab` 
```
/dev/mapper/home        /home   ext4        defaults        0       2

```

## LUKS on software RAID

This example is based on a real-world setup for a workstation class laptop equipped with two SSDs of equal size, and an additional HDD for bulk storage. The end result is LUKS1 based full disk encryption (including `/boot`) for all drives, with the SSDs in a [RAID0](/index.php/RAID "RAID") array, and keyfiles used to unlock all encryption after [GRUB](/index.php/GRUB "GRUB") is given a correct passphrase at boot.

This setup utilizes a very simplistic partitioning scheme, with all the available RAID storage being mounted at `/` (no separate `/boot` partition), and the decrypted HDD being mounted at `/data`.

Please note that regular [backups](/index.php/System_backup "System backup") are very important in this setup. If either of the SSDs fail, the data contained in the RAID array will be practically impossible to recover. You may wish to select a different [RAID level](/index.php/RAID#Standard_RAID_levels "RAID") if fault tolerance is important to you.

The encryption is not deniable in this setup.

For the sake of the instructions below, the following block devices are used:

```
/dev/sda = first SSD
/dev/sdb = second SSD
/dev/sdc = HDD

```

```
+---------------------+---------------------------+---------------------------+ +---------------------+---------------------------+---------------------------+ +---------------------------+
| BIOS boot partition | EFI system partition      | LUKS1 encrypted volume    | | BIOS boot partition | EFI system partition      | LUKS1 encrypted volume    | | LUKS2 encrypted volume    |
|                     |                           |                           | |                     |                           |                           | |                           |
|                     | /efi                      | /                         | |                     | /efi                      | /                         | | /data                     |
|                     |                           |                           | |                     |                           |                           | |                           |
|                     |                           | /dev/mapper/cryptroot     | |                     |                           | /dev/mapper/cryptroot     | |                           |
|                     +---------------------------+---------------------------+ |                     +---------------------------+---------------------------+ |                           |
|                     | RAID1 array (part 1 of 2) | RAID0 array (part 1 of 2) | |                     | RAID1 array (part 2 of 2) | RAID0 array (part 2 of 2) | |                           |
|                     |                           |                           | |                     |                           |                           | |                           |
|                     | /dev/md/ESP               | /dev/md/root              | |                     | /dev/md/ESP               | /dev/md/root              | | /dev/mapper/cryptdata     |
|                     +---------------------------+---------------------------+ |                     +---------------------------+---------------------------+ +---------------------------+
| /dev/sda1           | /dev/sda2                 | /dev/sda3                 | | /dev/sdb1           | /dev/sdb2                 | /dev/sdb3                 | | /dev/sdc1                 |
+---------------------+---------------------------+---------------------------+ +---------------------+---------------------------+---------------------------+ +---------------------------+

```

Be sure to substitute them with the appropriate device designations for your setup, as they may be different.

### Preparing the disks

Prior to creating any partitions, you should inform yourself about the importance and methods to securely erase the disk, described in [dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation").

For [BIOS systems](/index.php/GRUB#BIOS_systems "GRUB") with GPT, create a [BIOS boot partition](/index.php/BIOS_boot_partition "BIOS boot partition") with size of 1 MiB for GRUB to store the second stage of BIOS bootloader. Do not mount the partition.

For [UEFI systems](/index.php/GRUB#UEFI_systems "GRUB") create an [EFI system partition](/index.php/EFI_system_partition "EFI system partition") with an appropriate size, it will later be mounted at `/efi`.

In the remaining space on the drive create a partition (`/dev/sda3` in this example) for "Linux RAID". Choose partition type ID `fd` for MBR or partition type GUID `A19D880F-05FC-4D3B-A006-743F0F84911E` for GPT.

Once partitions have been created on `/dev/sda`, the following commands can be used to clone them to `/dev/sdb`.

```
# sfdisk -d /dev/sda > sda.dump
# sfdisk /dev/sdb < sda.dump

```

The HDD is prepared with a single Linux partition covering the whole drive at `/dev/sdc1`.

### Building the RAID array

Create the RAID array for the SSDs.

**Note:**

*   All parts of an EFI system partition RAID array must be individually usable, that means that ESP can only placed in a RAID1 array.
*   The RAID superblock must be placed at the end of the EFI system partition using `--metadata=1.0`, otherwise the firmware will not be able to access the partition.

```
# mdadm --create --verbose --level=1 --metadata=1.0 --raid-devices=2 /dev/md/ESP /dev/sda2 /dev/sdb2

```

This example utilizes RAID0 for root, you may wish to substitute a different level based on your preferences or requirements.

```
# mdadm --create --verbose --level=0 --metadata=1.2 --raid-devices=2 /dev/md/root /dev/sda3 /dev/sdb3

```

### Preparing the block devices

As explained in [dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation"), the devices are wiped with random data utilizing `/dev/zero` and a crypt device with a random key. Alternatively, you could use `dd` with `/dev/random` or `/dev/urandom`, though it will be much slower.

```
# cryptsetup open --type plain /dev/md/root container --key-file /dev/random
# dd if=/dev/zero of=/dev/mapper/container bs=1M status=progress
# cryptsetup close container

```

And repeat above for the HDD (`/dev/sdc1` in this example).

Set up encryption for `/dev/md/root`:

**Warning:** GRUB does not support LUKS2\. Use LUKS1 (`--type luks1`) on partitions that GRUB needs to access.

```
# cryptsetup -y -v luksFormat --type luks1 /dev/md/root
# cryptsetup open /dev/md/root cryptroot
# mkfs.ext4 /dev/mapper/cryptroot
# mount /dev/mapper/cryptroot /mnt

```

And repeat for the HDD:

```
# cryptsetup -y -v luksFormat /dev/sdc1
# cryptsetup open /dev/sdc1 cryptdata
# mkfs.ext4 /dev/mapper/cryptdata
# mkdir /mnt/data
# mount /dev/mapper/cryptdata /mnt/data

```

For UEFI systems, set up the EFI system partition:

```
# mkfs.fat -F32 /dev/md/ESP
# mount /dev/md/ESP /mnt/efi

```

### Configuring GRUB

Configure [GRUB](/index.php/GRUB "GRUB") for the LUKS1 encrypted system by editing `/etc/default/grub` with the following:

```
GRUB_CMDLINE_LINUX="cryptdevice=/dev/md/root:cryptroot"
GRUB_ENABLE_CRYPTODISK=y

```

See [dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") and [GRUB#Encrypted /boot](/index.php/GRUB#Encrypted_/boot "GRUB") for details.

Complete the GRUB install to both SSDs (in reality, installing only to `/dev/sda` will work).

```
# grub-install --target=i386-pc /dev/sda
# grub-install --target=i386-pc /dev/sdb
# grub-install --target=x86_64-efi --efi-directory=/efi --bootloader-id=GRUB
# grub-mkconfig -o /boot/grub/grub.cfg

```

### Creating the keyfiles

The next steps save you from entering your passphrase twice when you boot the system (once so GRUB can unlock the LUKS1 device, and second time once the initramfs assumes control of the system). This is done by creating a [keyfile](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption") for the encryption and adding it to the initramfs image to allow the encrypt hook to unlock the root device. See [dm-crypt/Device encryption#With a keyfile embedded in the initramfs](/index.php/Dm-crypt/Device_encryption#With_a_keyfile_embedded_in_the_initramfs "Dm-crypt/Device encryption") for details.

*   Create the [keyfile](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption") and add the key to `/dev/md/root`.
*   Create another keyfile for the HDD (`/dev/sdc1`) so it can also be unlocked at boot. For convenience, leave the passphrase created above in place as this can make recovery easier if you ever need it. Edit `/etc/crypttab` to decrypt the HDD at boot. See [Dm-crypt/System configuration#Unlocking with a keyfile](/index.php/Dm-crypt/System_configuration#Unlocking_with_a_keyfile "Dm-crypt/System configuration").

### Configuring the system

Edit [fstab](/index.php/Fstab "Fstab") to mount the cryptroot and cryptdata block devices and the ESP:

```
/dev/mapper/cryptroot  /           ext4    rw,noatime  0   1
/dev/mapper/cryptdata  /data       ext4    defaults            0   2
/dev/md/ESP            /efi        vfat    rw,relatime,codepage=437,iocharset=iso8859-1,shortname=mixed,utf8,tz=UTC,errors=remount-ro  0   2

```

Save the RAID configuration:

```
# mdadm --detail --scan >> /etc/mdadm.conf

```

Edit [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf") to include your keyfile and add the proper hooks:

```
FILES=(/crypto_keyfile.bin)
HOOKS=(base udev autodetect **keyboard** **keymap** consolefont modconf block **mdadm_udev** **encrypt** filesystems fsck)

```

See [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") for details.

## Plain dm-crypt

Contrary to LUKS, dm-crypt *plain* mode does not require a header on the encrypted device: this scenario exploits this feature to set up a system on an unpartitioned, encrypted disk that will be indistinguishable from a disk filled with random data, which could allow [deniable encryption](https://en.wikipedia.org/wiki/Deniable_encryption "wikipedia:Deniable encryption"). See also [wikipedia:Disk encryption#Full disk encryption](https://en.wikipedia.org/wiki/Disk_encryption#Full_disk_encryption "wikipedia:Disk encryption").

Note that if full-disk encryption is not required, the methods using LUKS described in the sections above are better options for both system encryption and encrypted partitions. LUKS features like key management with multiple passphrases/key-files or re-encrypting a device in-place are unavailable with *plain* mode.

*Plain* dm-crypt encryption can be more resilient to damage than LUKS, because it does not rely on an encryption master-key which can be a single-point of failure if damaged. However, using *plain* mode also requires more manual configuration of encryption options to achieve the same cryptographic strength. See also [Disk encryption#Cryptographic metadata](/index.php/Disk_encryption#Cryptographic_metadata "Disk encryption"). Using *plain* mode could also be considered if concerned with the problems explained in [dm-crypt/Specialties#Discard/TRIM support for solid state drives (SSD)](/index.php/Dm-crypt/Specialties#Discard/TRIM_support_for_solid_state_drives_(SSD) "Dm-crypt/Specialties").

**Tip:** If headerless encryption is your goal but you are unsure about the lack of key-derivation with *plain* mode, then two alternatives are:

*   [dm-crypt LUKS mode with a detached header](/index.php/Dm-crypt/Specialties#Encrypted_system_using_a_detached_LUKS_header "Dm-crypt/Specialties") by using the *cryptsetup* `--header` option. It cannot be used with the standard *encrypt* hook, but the hook may be modified.
*   [tcplay](/index.php/Tcplay "Tcplay") which offers headerless encryption but with the PBKDF2 function.

The scenario uses two USB sticks:

*   one for the boot device, which also allows storing the options required to open/unlock the plain encrypted device in the boot loader configuration, since typing them on each boot would be error prone;
*   another for the encryption key file, assuming it stored as raw bits so that to the eyes of an unaware attacker who might get the usbkey the encryption key will appear as random data instead of being visible as a normal file. See also [Wikipedia:Security through obscurity](https://en.wikipedia.org/wiki/Security_through_obscurity "wikipedia:Security through obscurity"), follow [dm-crypt/Device encryption#Keyfiles](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption") to prepare the keyfile.

The disk layout is:

```
+----------------------+----------------------+----------------------+ +----------------+ +----------------+
| Logical volume 1     | Logical volume 2     | Logical volume 3     | | Boot device    | | Encryption key |
|                      |                      |                      | |                | | file storage   |
| /                    | [SWAP]               | /home                | | /boot          | | (unpartitioned |
|                      |                      |                      | |                | | in example)    |
| /dev/MyVolGroup/root | /dev/MyVolGroup/swap | /dev/MyVolGroup/home | | /dev/sdb1      | | /dev/sdc       |
|----------------------+----------------------+----------------------| |----------------| |----------------|
| disk drive /dev/sda encrypted using plain mode and LVM             | | USB stick 1    | | USB stick 2    |
+--------------------------------------------------------------------+ +----------------+ +----------------+

```

**Tip:**

*   It is also possible to use a single USB key physical device:
    *   By putting the key on another partition (/dev/sdb2) of the USB storage device (/dev/sdb).
    *   By copying the keyfile to the initramfs directly. An example keyfile `/etc/keyfile` gets copied to the initramfs image by setting `FILES=(/etc/keyfile)` in `/etc/mkinitcpio.conf`. The way to instruct the `encrypt` hook to read the keyfile in the initramfs image is using `rootfs:` prefix before the filename, e.g. `cryptkey=rootfs:/etc/keyfile`.
*   Another option is using a passphrase with good [entropy](/index.php/Disk_encryption#Choosing_a_strong_passphrase "Disk encryption").

### Preparing the disk

It is vital that the mapped device is filled with random data. In particular this applies to the scenario use case we apply here.

See [dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation") and [dm-crypt/Drive preparation#dm-crypt specific methods](/index.php/Dm-crypt/Drive_preparation#dm-crypt_specific_methods "Dm-crypt/Drive preparation")

### Preparing the non-boot partitions

See [dm-crypt/Device encryption#Encryption options for plain mode](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_plain_mode "Dm-crypt/Device encryption") for details.

Using the device `/dev/sda`, with the aes-xts cipher with a 512 bit key size and using a keyfile we have the following options for this scenario:

```
# cryptsetup --cipher=aes-xts-plain64 --offset=0 --key-file=/dev/sdc --key-size=512 open --type plain /dev/sda cryptlvm

```

Unlike encrypting with LUKS, the above command must be executed *in full* whenever the mapping needs to be re-established, so it is important to remember the cipher, and key file details.

We can now check a mapping entry has been made for `/dev/mapper/cryptlvm`:

```
# fdisk -l

```

**Tip:** A simpler alternative to using LVM, advocated in the cryptsetup FAQ for cases where LVM is not necessary, is to just create a filesystem on the entirety of the mapped dm-crypt device.

Next, we setup [LVM](/index.php/LVM "LVM") logical volumes on the mapped device. See [LVM#Installing Arch Linux on LVM](/index.php/LVM#Installing_Arch_Linux_on_LVM "LVM") for further details:

```
# pvcreate /dev/mapper/cryptlvm
# vgcreate MyVolGroup /dev/mapper/cryptlvm
# lvcreate -L 32G MyVolGroup -n root
# lvcreate -L 10G MyVolGroup -n swap
# lvcreate -l 100%FREE MyVolGroup -n home

```

We format and mount them and activate swap. See [File systems#Create a file system](/index.php/File_systems#Create_a_file_system "File systems") for further details:

```
# mkfs.ext4 /dev/MyVolGroup/root
# mkfs.ext4 /dev/MyVolGroup/home
# mount /dev/MyVolGroup/root /mnt
# mkdir /mnt/home
# mount /dev/MyVolGroup/home /mnt/home
# mkswap /dev/MyVolGroup/swap
# swapon /dev/MyVolGroup/swap

```

### Preparing the boot partition

The `/boot` partition can be installed on the standard vfat partition of a USB stick, if required. But if manual partitioning is needed, then a small 200 MiB partition is all that is required. Create the partition using a [partitioning tool](/index.php/Partitioning#Partitioning_tools "Partitioning") of your choice.

Create a [filesystem](/index.php/Filesystem "Filesystem") on the partition intended for `/boot`, if it is not already formatted as vfat:

```
# mkfs.ext4 /dev/sdb1
# mkdir /mnt/boot
# mount /dev/sdb1 /mnt/boot

```

### Configuring mkinitcpio

Add the `keyboard`, `encrypt` and `lvm2` hooks to [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"):

```
HOOKS=(base udev autodetect **keyboard** **keymap** consolefont modconf block **encrypt** **lvm2** filesystems fsck)

```

See [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") for details and other hooks that you may need.

### Configuring the boot loader

In order to boot the encrypted root partition, the following [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") need to be set by the boot loader (note that 64 is the number of bytes in 512 bits):

```
cryptdevice=/dev/disk/by-id/*disk-ID-of-sda*:cryptlvm cryptkey=/dev/disk/by-id/*disk-ID-of-sdc*:0:64 crypto=:aes-xts-plain64:512:0:

```

The `*disk-ID-of-**disk***` refers to the id of the referenced disk. See [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") for details.

See [dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") for details and other parameters that you may need.

**Tip:** If using GRUB, you can install it on the same USB as the `/boot` partition with:
```
# grub-install --recheck /dev/sdb

```

### Post-installation

You may wish to remove the USB sticks after booting. Since the `/boot` partition is not usually needed, the `noauto` option can be added to the relevant line in `/etc/fstab`:

 `/etc/fstab` 
```
# /dev/sdb1
/dev/sdb1 /boot ext4 **noauto**,rw,noatime 0 2

```

However, when an update to anything used in the initramfs, or a kernel, or the bootloader is required; the `/boot` partition must be present and mounted. As the entry in `fstab` already exists, it can be mounted simply with:

```
# mount /boot

```

## Encrypted boot partition (GRUB)

This setup utilizes the same partition layout and configuration as the previous [#LVM on LUKS](#LVM_on_LUKS) section, with the difference that the [GRUB](/index.php/GRUB "GRUB") boot loader is used since it is capable of booting from an LVM logical volume and a LUKS1-encrypted `/boot`. See also [GRUB#Encrypted /boot](/index.php/GRUB#Encrypted_/boot "GRUB").

The disk layout in this example is:

```
+---------------------+----------------------+----------------------+----------------------+----------------------+
| BIOS boot partition | EFI system partition | Logical volume 1     | Logical volume 2     | Logical volume 3     |
|                     |                      |                      |                      |                      |
|                     | /efi                 | /                    | [SWAP]               | /home                |
|                     |                      |                      |                      |                      |
|                     |                      | /dev/MyVolGroup/root | /dev/MyVolGroup/swap | /dev/MyVolGroup/home |
| /dev/sda1           | /dev/sda2            |----------------------+----------------------+----------------------+
| unencrypted         | unencrypted          | /dev/sda3 encrypted using LVM on LUKS1                             |
+---------------------+----------------------+--------------------------------------------------------------------+

```

**Tip:**

*   All scenarios are intended as examples. It is, of course, possible to apply both of the two above distinct installation steps with the other scenarios as well. See also the variants linked in [#LVM on LUKS](#LVM_on_LUKS).
*   You can use `cryptboot` script from [cryptboot](https://aur.archlinux.org/packages/cryptboot/) package for simplified encrypted boot management (mounting, unmounting, upgrading packages) and as a defense against [Evil Maid](https://www.schneier.com/blog/archives/2009/10/evil_maid_attac.html) attacks with [UEFI Secure Boot](/index.php/Secure_Boot#Using_your_own_keys "Secure Boot"). For more information and limitations see [cryptboot project](https://github.com/xmikos/cryptboot) page.

### Preparing the disk

Prior to creating any partitions, you should inform yourself about the importance and methods to securely erase the disk, described in [dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation").

For [BIOS systems](/index.php/GRUB#BIOS_systems "GRUB") create a [BIOS boot partition](/index.php/BIOS_boot_partition "BIOS boot partition") with size of 1 MiB for GRUB to store the second stage of BIOS bootloader. Do not mount the partition.

For [UEFI systems](/index.php/GRUB#UEFI_systems "GRUB") create an [EFI system partition](/index.php/EFI_system_partition "EFI system partition") with an appropriate size, it will later be mounted at `/efi`.

Create a partition of type `8309`, which will later contain the encrypted container for the LVM.

Create the LUKS encrypted container:

**Warning:** GRUB does not support LUKS2\. Use LUKS1 (`--type luks1`) on partitions that GRUB needs to access.

```
# cryptsetup luksFormat --type luks1 /dev/sda3

```

For more information about the available cryptsetup options see the [LUKS encryption options](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") prior to above command.

Your partition layout should look similar to this:

 `# gdisk -l /dev/sda` 
```
...
Number  Start (sector)    End (sector)  Size       Code  Name
   1            2048            4095   1024.0 KiB  EF02  BIOS boot partition
   2            4096         1130495   550.0 MiB   EF00  EFI System
   3         1130496        68239360   32.0 GiB    8309  Linux LUKS

```

Open the container:

```
# cryptsetup open /dev/sda3 cryptlvm

```

The decrypted container is now available at `/dev/mapper/cryptlvm`.

### Preparing the logical volumes

The LVM logical volumes of this example follow the exact layout as the [#LVM on LUKS](#LVM_on_LUKS) scenario. Therefore, please follow [#Preparing the logical volumes](#Preparing_the_logical_volumes) above and adjust as required.

If you plan to boot in UEFI mode, create a mountpoint for the [EFI system partition](/index.php/EFI_system_partition "EFI system partition") at `/efi` for compatibility with `grub-install` and mount it:

```
# mkdir /mnt/efi
# mount /dev/sda2 /mnt/efi

```

At this point, you should have the following partitions and logical volumes inside of `/mnt`:

 `$ lsblk` 
```
NAME                  MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINT
sda                   8:0      0   200G  0 disk
├─sda1                8:1      0     1M  0 part
├─sda2                8:2      0   550M  0 part  /mnt/efi
└─sda3                8:3      0   100G  0 part
  └─cryptlvm          254:0    0   100G  0 crypt
    ├─MyVolGroup-swap 254:1    0     8G  0 lvm   [SWAP]
    ├─MyVolGroup-root 254:2    0    32G  0 lvm   /mnt
    └─MyVolGroup-home 254:3    0    60G  0 lvm   /mnt/home

```

### Configuring mkinitcpio

Add the `keyboard`, `encrypt` and `lvm2` hooks to [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"):

```
HOOKS=(base **udev** autodetect **keyboard** **keymap** consolefont modconf block **encrypt** **lvm2** filesystems fsck)

```

If using the [sd-encrypt](/index.php/Sd-encrypt "Sd-encrypt") hook with the systemd-based initramfs, the following needs to be set instead:

```
HOOKS=(base **systemd** autodetect **keyboard** **sd-vconsole** modconf block **sd-encrypt** **sd-lvm2** filesystems fsck)

```

See [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") for details and other hooks that you may need.

### Configuring GRUB

Configure GRUB to allow booting from `/boot` on a LUKS1 encrypted partition:

 `/etc/default/grub`  `GRUB_ENABLE_CRYPTODISK=y` 

Set the kernel parameters, so that the initramfs can unlock the encrypted root partition. Using the `encrypt` hook:

 `/etc/default/grub`  `GRUB_CMDLINE_LINUX="... cryptdevice=UUID=*device-UUID*:cryptlvm ..."` 

If using the [sd-encrypt](/index.php/Sd-encrypt "Sd-encrypt") hook, the following need to be set instead:

 `/etc/default/grub`  `GRUB_CMDLINE_LINUX="... rd.luks.name=*device-UUID*=cryptlvm ..."` 

See [dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") and [GRUB#Encrypted /boot](/index.php/GRUB#Encrypted_/boot "GRUB") for details. The `*device-UUID*` refers to the UUID of `/dev/sda3` (the partition which holds the lvm containing the root filesystem). See [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming").

[install GRUB](/index.php/GRUB#Installation_2 "GRUB") to the mounted ESP for UEFI booting:

```
# grub-install --target=x86_64-efi --efi-directory=/efi --bootloader-id=GRUB --recheck

```

[install GRUB](/index.php/GRUB#Installation "GRUB") to the disk for BIOS booting:

```
# grub-install --target=i386-pc --recheck /dev/sda

```

Generate GRUB's [configuration](/index.php/GRUB#Generate_the_main_configuration_file "GRUB") file:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

If all commands finished without errors, GRUB should prompt for the passphrase to unlock the `/dev/sda3` partition after the next reboot.

### Avoiding having to enter the passphrase twice

While GRUB asks for a passphrase to unlock the LUKS1 encrypted partition after above instructions, the partition unlock is not passed on to the initramfs. Hence, you have to enter the passphrase twice at boot: once for GRUB and once for the initramfs.

This section deals with extra configuration to let the system boot by only entering the passphrase once, in GRUB. This is accomplished by [with a keyfile embedded in the initramfs](/index.php/Dm-crypt/Device_encryption#With_a_keyfile_embedded_in_the_initramfs "Dm-crypt/Device encryption").

First create a keyfile and add it as LUKS key:

```
# dd bs=512 count=4 if=/dev/random of=/root/cryptlvm.keyfile iflag=fullblock
# chmod 000 /root/cryptlvm.keyfile
# chmod 600 /boot/initramfs-linux*
# cryptsetup -v luksAddKey /dev/sda3 /root/cryptlvm.keyfile

```

Add the keyfile to the initramfs image:

 `/etc/mkinitcpio.conf`  `FILES=(/root/cryptlvm.keyfile)` 

Set the following kernel parameters to unlock the LUKS partition with the keyfile. Using the `encrypt` hook:

```
GRUB_CMDLINE_LINUX="... cryptkey=rootfs:/root/cryptlvm.keyfile"

```

Or, using the [sd-encrypt](/index.php/Sd-encrypt "Sd-encrypt") hook:

```
GRUB_CMDLINE_LINUX="... rd.luks.key=*device-UUID*=/root/cryptlvm.keyfile"

```

If for some reason the keyfile fails to unlock the boot partition, systemd will fallback to ask for a passphrase to unlock and, in case that is correct, continue booting.

**Tip:** If you want to encrypt the `/boot` partition to protect against offline tampering threats, the [mkinitcpio-chkcryptoboot](/index.php/Dm-crypt/Specialties#mkinitcpio-chkcryptoboot "Dm-crypt/Specialties") hook has been contributed to help.

## Btrfs subvolumes with swap

The following example creates a full system encryption with LUKS1 using [Btrfs](/index.php/Btrfs "Btrfs") subvolumes to [simulate partitions](/index.php/Btrfs#Mounting_subvolumes "Btrfs").

If using UEFI, an [EFI system partition](/index.php/EFI_system_partition "EFI system partition") (ESP) is required. `/boot` itself may reside on `/` and be encrypted; however, the ESP itself cannot be encrypted. In this example layout, the ESP is `/dev/sda1` and is mounted at `/efi`. `/boot` itself is located on the system partition, `/dev/sda2`.

Since `/boot` resides on the LUKS1 encrypted `/`, [GRUB](/index.php/GRUB "GRUB") must be used as the bootloader because only GRUB can load modules necessary to decrypt `/boot` (e.g., crypto.mod, cryptodisk.mod and luks.mod).

Additionally an optional plain-encrypted [swap](/index.php/Swap "Swap") partition is shown.

**Warning:** Do not use a [swap file](/index.php/Swap_file "Swap file") instead of a separate partition on Linux kernels before v5.0, because this may result in data loss. See [Btrfs#Swap file](/index.php/Btrfs#Swap_file "Btrfs").

```
+----------------------+----------------------+----------------------+
| EFI system partition | System partition     | Swap partition       |
| unencrypted          | LUKS1-encrypted      | plain-encrypted      |
|                      |                      |                      |
| /efi                 | /                    | [SWAP]               |
| /dev/sda1            | /dev/sda2            | /dev/sda3            |
|----------------------+----------------------+----------------------+

```

### Preparing the disk

**Note:** It is not possible to use btrfs partitioning as described in [Btrfs#Partitionless Btrfs disk](/index.php/Btrfs#Partitionless_Btrfs_disk "Btrfs") when using LUKS. Traditional partitioning must be used, even if it is just to create one partition.

Prior to creating any partitions, you should inform yourself about the importance and methods to securely erase the disk, described in [dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation"). If you are using [UEFI](/index.php/UEFI "UEFI") create an [EFI system partition](/index.php/EFI_system_partition "EFI system partition") with an appropriate size. It will later be mounted at `/efi`. If you are going to create an encrypted swap partition, create the partition for it, but do **not** mark it as swap, since plain *dm-crypt* will be used with the partition.

Create the needed partitions, at least one for `/` (e.g. `/dev/sda2`). See the [Partitioning](/index.php/Partitioning "Partitioning") article.

### Preparing the system partition

#### Create LUKS container

**Warning:** GRUB does not support LUKS2\. Use LUKS1 (`--type luks1`) on partitions that GRUB needs to access.

Follow [dm-crypt/Device encryption#Encrypting devices with LUKS mode](/index.php/Dm-crypt/Device_encryption#Encrypting_devices_with_LUKS_mode "Dm-crypt/Device encryption") to setup `/dev/sda2` for LUKS. See the [dm-crypt/Device encryption#Encryption options for LUKS mode](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") before doing so for a list of encryption options.

#### Unlock LUKS container

Now follow [dm-crypt/Device encryption#Unlocking/Mapping LUKS partitions with the device mapper](/index.php/Dm-crypt/Device_encryption#Unlocking/Mapping_LUKS_partitions_with_the_device_mapper "Dm-crypt/Device encryption") to unlock the LUKS container and map it.

#### Format mapped device

Proceed to format the mapped device as described in [Btrfs#File system on a single device](/index.php/Btrfs#File_system_on_a_single_device "Btrfs"), where `*/dev/partition*` is the name of the mapped device (i.e., `cryptroot`) and **not** `/dev/sda2`.

#### Mount mapped device

Finally, [mount](/index.php/Mount "Mount") the now-formatted mapped device (i.e., `/dev/mapper/cryptroot`) to `/mnt`.

**Tip:** You may want to use the `compress=lzo` mount option. See [Btrfs#Compression](/index.php/Btrfs#Compression "Btrfs") for more information.

### Creating btrfs subvolumes

#### Layout

[Subvolumes](/index.php/Btrfs#Subvolumes "Btrfs") will be used to simulate partitions, but other (nested) subvolumes will also be created. Here is a partial representation of what the following example will generate:

```
subvolid=5 (/dev/sda2)
   |
   ├── @ (mounted as /)
   |       |
   |       ├── /bin (directory)
   |       |
   |       ├── /home (mounted @home subvolume)
   |       |
   |       ├── /usr (directory)
   |       |
   |       ├── /.snapshots (mounted @snapshots subvolume)
   |       |
   |       ├── /var/cache/pacman/pkg (nested subvolume)
   |       |
   |       ├── ... (other directories and nested subvolumes)
   |
   ├── @snapshots (mounted as /.snapshots)
   |
   ├── @home (mounted as /home)
   |
   └── @... (additional subvolumes you wish to use as mount points)

```

This section follows the [Snapper#Suggested filesystem layout](/index.php/Snapper#Suggested_filesystem_layout "Snapper"), which is most useful when used with [Snapper](/index.php/Snapper "Snapper"). You should also consult [Btrfs Wiki SysadminGuide#Layout](https://btrfs.wiki.kernel.org/index.php/SysadminGuide#Layout).

#### Create top-level subvolumes

Here we are using the convention of prefixing `@` to subvolume names that will be used as mount points, and `@` will be the subvolume that is mounted as `/`.

Following the [Btrfs#Creating a subvolume](/index.php/Btrfs#Creating_a_subvolume "Btrfs") article, create subvolumes at `/mnt/@`, `/mnt/@snapshots`, and `/mnt/@home`.

Create any additional subvolumes you wish to use as mount points now.

#### Mount top-level subvolumes

Unmount the system partition at `/mnt`.

Now mount the newly created `@` subvolume which will serve as `/` to `/mnt` using the `subvol=` mount option. Assuming the mapped device is named `cryptroot`, the command would look like:

```
# mount -o compress=lzo,subvol=@ /dev/mapper/cryptroot /mnt

```

See [Btrfs#Mounting subvolumes](/index.php/Btrfs#Mounting_subvolumes "Btrfs") for more details.

Also mount the other subvolumes to their respective mount points: `@home` to `/mnt/home` and `@snapshots` to `/mnt/.snapshots`.

#### Create nested subvolumes

Create any subvolumes you do **not** want to have snapshots of when taking a snapshot of `/`. For example, you probably do not want to take snapshots of `/var/cache/pacman/pkg`. These subvolumes will be nested under the `@` subvolume, but just as easily could have been created earlier at the same level as `@` according to your preference.

Since the `@` subvolume is mounted at `/mnt` you will need to [create a subvolume](/index.php/Create_a_subvolume "Create a subvolume") at `/mnt/var/cache/pacman/pkg` for this example. You may have to create any parent directories first.

Other directories you may wish to do this with are `/var/abs`, `/var/tmp`, and `/srv`.

#### Mount ESP

If you prepared an EFI system partition earlier, create its mount point and mount it now.

**Note:** Btrfs snapshots will exclude `/efi`, since it is not a btrfs file system.

At the [pacstrap](/index.php/Installation_guide#Install_essential_packages "Installation guide") installation step, the [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) must be installed in addition to the [base](https://www.archlinux.org/packages/?name=base) [meta package](/index.php/Meta_package "Meta package").

### Configuring mkinitcpio

#### Create keyfile

In order for GRUB to open the LUKS partition without having the user enter his passphrase twice, we will use a keyfile embedded in the initramfs. Follow [dm-crypt/Device encryption#With a keyfile embedded in the initramfs](/index.php/Dm-crypt/Device_encryption#With_a_keyfile_embedded_in_the_initramfs "Dm-crypt/Device encryption") making sure to add the key to `/dev/sda2` at the *luksAddKey* step.

#### Edit mkinitcpio.conf

After creating, adding, and embedding the key as described above, add the `encrypt` hook to [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf") as well as any other hooks you require. See [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") for detailed information.

**Tip:** You may want to add `BINARIES=(/usr/bin/btrfs)` to your `mkinitcpio.conf`. See the [Btrfs#Corruption recovery](/index.php/Btrfs#Corruption_recovery "Btrfs") article.

### Configuring the boot loader

Install [GRUB](/index.php/GRUB "GRUB") to `/dev/sda`. Then, edit `/etc/default/grub` as instructed in the [GRUB#Additional arguments](/index.php/GRUB#Additional_arguments "GRUB") and [GRUB#Encrypted /boot](/index.php/GRUB#Encrypted_/boot "GRUB"), following both the instructions for an encrypted root and boot partition. Finally, generate the GRUB configuration file.

### Configuring swap

If you created a partition to be used for encrypted swap, now is the time to configure it. Follow the instructions at [dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption").