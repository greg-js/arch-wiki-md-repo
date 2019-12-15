Os exemplos a seguir são cenários comuns de um sistema criptografado com *dm-crypt*. Eles explicam todas as adaptações que serão realizadas do [processo de instalação](/index.php/Guia_de_instala%C3%A7%C3%A3o "Guia de instalação"). Todas as ferramentas necessárias estão disponíveis na [imagem de instalação](https://www.archlinux.org/download/).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Visão geral](#Visão_geral)
*   [2 LUKS em uma partição](#LUKS_em_uma_partição)
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
    *   [4.1 Preparando o disco](#Preparando_o_disco_3)
    *   [4.2 Preparando os volumes lógicos](#Preparando_os_volumes_lógicos_2)
    *   [4.3 Preparando a partição de boot](#Preparando_a_partição_de_boot_2)
    *   [4.4 Configurando o mkinitcpio](#Configurando_o_mkinitcpio_3)
    *   [4.5 Configurando o gerenciador de boot](#Configurando_o_gerenciador_de_boot_3)
    *   [4.6 Configurando o fstab e crypttab](#Configurando_o_fstab_e_crypttab)
    *   [4.7 Criptografando o volume lógico /home](#Criptografando_o_volume_lógico_/home)
*   [5 LUKS dentro do RAID de software](#LUKS_dentro_do_RAID_de_software)
    *   [5.1 Preparando os discos](#Preparando_os_discos)
    *   [5.2 Fazendo o arranjo RAID](#Fazendo_o_arranjo_RAID)
    *   [5.3 Preparando os dispositivos de bloco](#Preparando_os_dispositivos_de_bloco)
    *   [5.4 Configurando o GRUB](#Configurando_o_GRUB)
    *   [5.5 Criando as keyfiles](#Criando_as_keyfiles)
    *   [5.6 Configurando o sistema](#Configurando_o_sistema)
*   [6 Plain dm-crypt](#Plain_dm-crypt)
    *   [6.1 Preparando o disco](#Preparando_o_disco_4)
    *   [6.2 Preparando a partição que não é de boot](#Preparando_a_partição_que_não_é_de_boot)
    *   [6.3 Preparando a partição de boot](#Preparando_a_partição_de_boot_3)
    *   [6.4 Configurando mkinitcpio](#Configurando_mkinitcpio)
    *   [6.5 Configurando o gerenciador de boot](#Configurando_o_gerenciador_de_boot_4)
    *   [6.6 Pós-instalação](#Pós-instalação)
*   [7 Partição de boot criptografada (GRUB)](#Partição_de_boot_criptografada_(GRUB))
    *   [7.1 Preparing the disk](#Preparing_the_disk)
    *   [7.2 Preparing the logical volumes](#Preparing_the_logical_volumes)
    *   [7.3 Configuring mkinitcpio](#Configuring_mkinitcpio)
    *   [7.4 Configuring GRUB](#Configuring_GRUB)
    *   [7.5 Avoiding having to enter the passphrase twice](#Avoiding_having_to_enter_the_passphrase_twice)
*   [8 Btrfs subvolumes with swap](#Btrfs_subvolumes_with_swap)
    *   [8.1 Preparing the disk](#Preparing_the_disk_2)
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
    *   [8.4 Configuring mkinitcpio](#Configuring_mkinitcpio_2)
        *   [8.4.1 Create keyfile](#Create_keyfile)
        *   [8.4.2 Edit mkinitcpio.conf](#Edit_mkinitcpio.conf)
    *   [8.5 Configuring the boot loader](#Configuring_the_boot_loader)
    *   [8.6 Configuring swap](#Configuring_swap)

## Visão geral

*dm-crypt* se destaca, tanto em funcionalidades quanto em velocidade, quando o assunto é proteger o sistema de arquivos principal. Diferente da encriptação seletiva de sistemas de arquivos secundários, a criptografia de todo um sistema pode proteger informações como quais programas estão instalados, os nomes de usuários de todas as contas, e vetores comuns de vazamento de dados tais como [mlocate](/index.php/Mlocate "Mlocate") e `/var/log`. E, é bem mais difícil fazer alterações em um sistema criptografado, exceto o [gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot") e (geralmente) o kernel que nao são criptografados.

Todos os cenários ilustrados a seguir compartilham as vantagens supracitadas, prós e contras que os diferenciam estão resumidos abaixo:

| Cenários | Vantagens | Desvantagens |
| [#LUKS em uma partição](#LUKS_em_uma_partição)

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

## LUKS em uma partição

Este exemplo demonstra um sistema criptografado com *dm-crypt* + LUKS em uma partição:

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

Adicione os hooks `keyboard`, `encrypt` e `lvm2` em [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"):

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

o `*UUID-do-dispositivo*` precisa ser substituído pelo UUID da partição raiz, nesse caso `/dev/sda1`. Veja [Nomeação persistente de dispositivo de bloco](/index.php/Nomea%C3%A7%C3%A3o_persistente_de_dispositivo_de_bloco "Nomeação persistente de dispositivo de bloco") para mais detalhes.

Veja [dm-crypt/Configuração do sistema#Gerenciador de boot](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema#Gerenciador_de_boot "Dm-crypt/Configuração do sistema") para mais informação sobre.

## LUKS dentro do LVM

Você deve configurar os volumes do [LVM](/index.php/LVM "LVM") primeiro antes de usá-los como base para as partições criptografadas. Desta maneira, é possível fazer uma mistura de volumes/partições que são criptografadas ou não.

**Dica:** Diferente do [#LVM dentro do LUKS](#LVM_dentro_do_LUKS), este método permite usar volumes lógicos espalhados em múltiplos discos.

O texto a seguir exemplifica uma configuração do LUKS dentro do LVM que também faz uso de uma keyfile para o volume lógico /home e volumes temporários criptografados para `/tmp` e `/swap`. O último é desejável caso se preocupe com segurança, devido a evitar que dados temporários sensíveis sobrevivam durante a inicialização do sistema. Se tem experiência com LVM, você vai ser capaz de ignorar/trocar alguns dos passos relacionados com ele e outras coisas específicas de acordo com sua vontade.

Se quer usar volumes lógicos espalhados por múltiplos discos que já foram configurados, ou expandir o `/home` (ou qualquer outro volume), um dos jeitos de como fazer isto é descrito em [dm-crypt/Especificidades#Expandindo LVM em vários discos](/index.php/Dm-crypt/Specialties#Expanding_LVM_on_multiple_disks "Dm-crypt/Specialties"). Vale notar que o container criptografado com LUKS precisa ser redimensionado também.

### Preparando o disco

Esquema de particionamento:

```
+------------------+------------------------------------------------------------------------------------------------+
| Partição de boot | Volume criptografado com o   | Volume criptografado com LUKS2 | Volume criptografado com LUKS2 |
|                  | modo plain do dm-crypt       |                                |                                |
|                  |                              |                                |                                |
| /boot            | [SWAP]                       | /                              | /home                          |
|                  |                              |                                |                                |
|                  | /dev/mapper/swap             | /dev/mapper/raiz               | /dev/mapper/home               |
|                  |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |
|                  | Volume lógico 1              | Volume lógico 2                | Volume lógico 3                |
|                  | /dev/MeuGrupoVol/cryptswap   | /dev/MeuGrupoVol/cryptraiz     | /dev/MeuGrupoVol/crypthome     |
|                  |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |
|   /dev/sda1      |                                   /dev/sda2                                                    |
+------------------+------------------------------------------------------------------------------------------------+

```

sobrescreva `/dev/sda2` de acordo com [dm-crypt/Preparando a unidade de armazenamento#dm-crypt limpa o disco vazio ou partição](/index.php/Dm-crypt/Drive_preparation#dm-crypt_wipe_on_an_empty_disk_or_partition "Dm-crypt/Drive preparation").

### Preparando os volumes lógicos

```
# pvcreate /dev/sda2
# vgcreate MeuGrupoVol /dev/sda2
# lvcreate -L 32G -n raiz MeuGrupoVol
# lvcreate -L 500M -n cryptswap MeuGrupoVol
# lvcreate -L 500M -n crypttmp MeuGrupoVol
# lvcreate -l 100%FREE -n crypthome MeuGrupoVol

```

```
# cryptsetup luksFormat /dev/MeuGrupoVol/cryptraiz
# cryptsetup open /dev/MeuGrupoVol/cryptraiz raiz
# mkfs.ext4 /dev/mapper/raiz
# mount /dev/mapper/raiz /mnt

```

Mais informações sobre opções de encriptação podem ser encontradas em [dm-crypt/Encriptação de dispositivo#opções de encriptação para o modo LUKS](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption"). Note que `/home` será criptografada em [#Criptografando o volume lógico /home](#Criptografando_o_volume_lógico_/home).

**Dica:** Se você precisar acessar a raiz criptografada pelo archiso, a ação `open` vai possibilitar a execução de comandos para [mostrar volumes do LVM](/index.php/LVM#Logical_Volumes_do_not_show_up "LVM").

### Preparando a partição de boot

```
# dd if=/dev/zero of=/dev/sda1 bs=1M status=progress
# mkfs.ext4 /dev/sda1
# mkdir /mnt/boot
# mount /dev/sda1 /mnt/boot

```

### Configurando o mkinitcpio

Adicione os hooks `keyboard`, `lvm2` e `encrypt` em [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"):

```
HOOKS=(base **udev** autodetect **keyboard** **keymap** consolefont modconf block **lvm2** **encrypt** filesystems fsck)

```

Se está usando o hook [sd-encrypt](/index.php/Sd-encrypt "Sd-encrypt") com o initramfs baseado no systemd, o seguinte precisa ser definido ao invês:

```
HOOKS=(base **systemd** autodetect **keyboard** **sd-vconsole** modconf block **sd-encrypt** **sd-lvm2** filesystems fsck)

```

Veja [dm-crypt/Configuração do sistema#mkinitcpio](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema#mkinitcpio "Dm-crypt/Configuração do sistema") para detalhes e outros hooks que você pode precisar.

### Configurando o gerenciador de boot

Para abrir a partição raiz criptografada na inicialização, os seguintes [parâmetros do kernel](/index.php/Par%C3%A2metros_do_kernel "Parâmetros do kernel") precisam ser adicionados ao gerenciador de boot:

```
cryptdevice=UUID=*UUID-do-dispositivo*:raiz root=/dev/mapper/raiz

```

Se está usando o hook [sd-encrypt](/index.php/Sd-encrypt "Sd-encrypt"), o seguinte precisa ser definido ao invés:

```
rd.luks.name=*UUID-do-dispositivo*=raiz root=/dev/mapper/raiz

```

O `*UUID-do-dispositivo*` precisa ser substituído pelo UUID do `/dev/MeuGrupoVol/cryptraiz`. Veja [Nomeação persistente de dispositivo de bloco](/index.php/Nomea%C3%A7%C3%A3o_persistente_de_dispositivo_de_bloco "Nomeação persistente de dispositivo de bloco") para detalhes.

Veja [dm-crypt/Configuração do sistema#Gerenciador de boot](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema#Gerenciador_de_boot "Dm-crypt/Configuração do sistema") para mais informação sobre.

### Configurando o fstab e crypttab

Ambas as entradas do [crypttab](/index.php/Crypttab "Crypttab") e [fstab](/index.php/Fstab "Fstab") são necessárias para abrir o dispositivo e montar os sistemas de arquivos, respectivamente. As seguintes linhas irão criptografar os sistemas de arquivos temporários a cada inicialização:

 `/etc/crypttab` 
```
swap	/dev/MeuGrupoVol/cryptswap	/dev/urandom	swap,cipher=aes-xts-plain64,size=256
tmp	    /dev/MeuGrupoVol/crypttmp	/dev/urandom	tmp,cipher=aes-xts-plain64,size=256
```
 `/etc/fstab` 
```
/dev/mapper/raiz        /       ext4            defaults        0       1
/dev/sda1               /boot   ext4            defaults        0       2
/dev/mapper/tmp         /tmp    tmpfs           defaults        0       0
/dev/mapper/swap        none    swap            sw              0       0

```

### Criptografando o volume lógico /home

Devido a este cenário usar LVM como mapeador primário e dm-crypt como secundário, cada volume lógico precisa ser criptografado separadamente. Apesar disso, diferente dos sistemas de arquivos temporários que foram configurados acima para serem voláteis, o volume lógico para `/home` vai ser persistente. O seguinte assume que você reiniciou o seu sistema criptografado, se você não fez isto, precisará adaptar os caminhos. Para não digitar uma segunda senha na inicialização, uma [keyfile](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption") é criada:

```
# mkdir -m 700 /etc/luks-keys
# dd if=/dev/random of=/etc/luks-keys/home bs=1 count=256 status=progress

```

O volume lógico é criptografado com:

```
# cryptsetup luksFormat -v /dev/MeuGrupoVol/crypthome /etc/luks-keys/home
# cryptsetup -d /etc/luks-keys/home open /dev/MeuGrupoVol/crypthome home
# mkfs.ext4 /dev/mapper/home
# mount /dev/mapper/home /home

```

A montagem dos volumes criptografados é feita tanto no [crypttab](/index.php/Crypttab "Crypttab") como no [fstab](/index.php/Fstab "Fstab"):

 `/etc/crypttab` 
```
home	/dev/MeuGrupoVol/crypthome   /etc/luks-keys/home

```
 `/etc/fstab` 
```
/dev/mapper/home        /home   ext4        defaults        0       2

```

## LUKS dentro do RAID de software

Este exemplo é baseado em uma configuração real para um notebook empresarial equipado com dois SSDs de tamanho igual, e um HDD adicional para guardar dados. O resultado é uma encriptação total de disco com LUKS1 (incluindo `/boot`) para todos as unidades de armazenamento, Os SSDs em um arranjo [RAID0](/index.php/RAID "RAID"), e são usadas keyfiles para abrir todos os dispositivos criptografados, depois que o [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)") recebe a senha correta na inicialização.

Esta configuração usa um esquema de partições muito simples, com as unidades de armazenamento RAID sendo montadas em `/` (sem partição `/boot` separada), e o HDD montado em `/data`.

Por favor note que [backups](/index.php/Backup_do_sistema "Backup do sistema") regulares são muito importantes. Se qualquer um dos SSDs falharem, os dados contidos no arranjo RAID serão praticamente impossíveis de recuperar. Você pode querer um diferente [nível de RAID](/index.php/RAID#Standard_RAID_levels "RAID") se a tolerância a falhas é considerada importante.

A encriptação não é negável nesta configuração.

Os seguintes dispositivos de bloco são usados:

```
/dev/sda = primeiro SSD
/dev/sdb = segundo SSD
/dev/sdc = HDD

```

```
+---------------+----------------+-----------------------+ +---------------+----------------+-----------------------+ +---------------------+
| Partição de   | Partição de    | Volume LUKS1          | | Partição de   | Partição de    | Volume LUKS1          | | volume LUKS2        |
| inicialização | sistema EFI    | criptografado         | | inicialização | sistema EFI    | criptografado         | | criptografado       |
| de BIOS       |                |                       | | de BIOS       |                |                       | |                     |
|               |                |                       | |               |                |                       | |                     |
|               | /efi           | /                     | |               | /efi           | /                     | | /data               |
|               |                |                       | |               |                |                       | |                     |
|               |                | /dev/mapper/cryptraiz | |               |                | /dev/mapper/cryptraiz | |                     |
|               +----------------+-----------------------+ |               +----------------+-----------------------+ |                     |
|               | arranjo RAID1  | arranjo RAID0         | |               | arranjo RAID1  | arranjo RAID0         | |                     |
|               | (parte 1 de 2) | (parte 1 de 2)        | |               | (parte 2 de 2) | (parte 2 de 2)        | |                     |
|               |                |                       | |               |                |                       | |                     |
|               | /dev/md/ESP    | /dev/md/raiz          | |               | /dev/md/ESP    | /dev/md/raiz          | |/dev/mapper/cryptdata|
|               +----------------+-----------------------+ |               |+---------------+-----------------------+ +---------------------+
| /dev/sda1     | /dev/sda2      | /dev/sda3             | | /dev/sdb1     | /dev/sdb2      | /dev/sdb3             | | /dev/sdc1           |
+---------------+----------------+-----------------------+ +---------------+----------------+-----------------------+ +---------------------+

```

Tenha certeza de substituir eles com os dispositivos apropriados para sua situação, eles podem ser diferentes.

### Preparando os discos

Antes de criar qualquer partição, você deve se informar sobre a importância e também métodos de como apagar o disco com segurança, descritos em [dm-crypt/Preparando a unidade de armazenamento](/index.php/Dm-crypt/Preparando_a_unidade_de_armazenamento "Dm-crypt/Preparando a unidade de armazenamento").

Para [sistemas BIOS](/index.php/GRUB_(Portugu%C3%AAs)#Sistemas_BIOS "GRUB (Português)") com GPT, crie uma [Partição de inicialização de BIOS](/index.php/Parti%C3%A7%C3%A3o_de_inicializa%C3%A7%C3%A3o_de_BIOS "Partição de inicialização de BIOS") com o tamanho de 1 MiB para o GRUB poder utilizá-lo no segundo estágio da inicialização da BIOS. Não monte a partição.

Para [sistemas UEFI](/index.php/GRUB_(Portugu%C3%AAs)#Sistemas_UEFI "GRUB (Português)") crie uma [Partição de sistema EFI](/index.php/Parti%C3%A7%C3%A3o_de_sistema_EFI "Partição de sistema EFI") com um tamanho apropriado, ela mais tarde será montada em `/efi`.

No restante do espaço disponível no dispositivo, crie uma partição (`/dev/sda3` neste exemplo) "Linux RAID". Coloque o ID do tipo da partição: `fd` para MBR ou GUID `A19D880F-05FC-4D3B-A006-743F0F84911E` para GPT.

Uma vez que as partições forem criadas em `/dev/sda`, os seguintes comandos podem ser usados para clonar elas para `/dev/sdb`.

```
# sfdisk -d /dev/sda > sda.dump
# sfdisk /dev/sdb < sda.dump

```

O HDD é preparado com um única partição Linux (`/dev/sdc1`) para todo o disco.

### Fazendo o arranjo RAID

Crie o arranjo RAID para os SSDs.

**Nota:**

*   Todas as partes de uma partição de sistema EFI de arranjo RAID devem ser individualmente usáveis, isto significa que ela pode ser somente colocada em um arranjo RAID1.
*   O superbloco RAID deve ser colocado no fim da partição de sistema EFI usando `--metadata=1.0`, de outro modo, o firmware não conseguirá acessar a partição.

```
# mdadm --create --verbose --level=1 --metadata=1.0 --raid-devices=2 /dev/md/ESP /dev/sda2 /dev/sdb2

```

Este exemplo utiliza RAID0 para a raiz, você pode desejar substituir para um nível diferente baseado em suas preferências ou necessidades.

```
# mdadm --create --verbose --level=0 --metadata=1.2 --raid-devices=2 /dev/md/raiz /dev/sda3 /dev/sdb3

```

### Preparando os dispositivos de bloco

Como explicado em [dm-crypt/Preparando a unidade de armazenamento](/index.php/Dm-crypt/Preparando_a_unidade_de_armazenamento "Dm-crypt/Preparando a unidade de armazenamento"), os dispositivos são apagados com dados randômicos utilizando `/dev/zero` e um dispositivo criptografado com uma chave randômica. Alternativamente, você pode usar `dd` com `/dev/random` ou `/dev/urandom`, apesar que será muito mais lento.

```
# cryptsetup open --type plain /dev/md/raiz container --key-file /dev/random
# dd if=/dev/zero of=/dev/mapper/container bs=1M status=progress
# cryptsetup close container

```

e faça o mesmo para o HDD (`/dev/sdc1` neste exemplo).

Encripte `/dev/md/raiz`:

**Atenção:** GRUB não suporta LUKS2\. Use LUKS1 (`--type luks1`) nas partições que o GRUB precisa acessar.

```
# cryptsetup -y -v luksFormat --type luks1 /dev/md/raiz
# cryptsetup open /dev/md/raiz cryptraiz
# mkfs.ext4 /dev/mapper/cryptraiz
# mount /dev/mapper/cryptraiz /mnt

```

e faça o mesmo para o HDD:

```
# cryptsetup -y -v luksFormat /dev/sdc1
# cryptsetup open /dev/sdc1 cryptdata
# mkfs.ext4 /dev/mapper/cryptdata
# mkdir /mnt/data
# mount /dev/mapper/cryptdata /mnt/data

```

Para sistemas UEFI, defina a ESP (partição de sistema EFI):

```
# mkfs.fat -F32 /dev/md/ESP
# mount /dev/md/ESP /mnt/efi

```

### Configurando o GRUB

Configure [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)") para o sistema criptogrado com LUKS1, editando `/etc/default/grub` com o seguinte:

```
GRUB_CMDLINE_LINUX="cryptdevice=/dev/md/raiz:cryptraiz"
GRUB_ENABLE_CRYPTODISK=y

```

Veja [dm-crypt/Configuração do sistema#Gerenciador de boot](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema#Gerenciador_de_boot "Dm-crypt/Configuração do sistema") e [GRUB#/boot criptografado](/index.php/GRUB_(Portugu%C3%AAs)#/boot_Criptografada "GRUB (Português)") para detalhes.

Complete a instalação do GRUB para ambos os SSDs (em realidade, instalando somente em `/dev/sda` irá funcionar).

```
# grub-install --target=i386-pc /dev/sda
# grub-install --target=i386-pc /dev/sdb
# grub-install --target=x86_64-efi --efi-directory=/efi --bootloader-id=GRUB
# grub-mkconfig -o /boot/grub/grub.cfg

```

### Criando as keyfiles

Os próximos passos evitarão que você digite a senha duas vezes quando você inicializar o sistema (uma vez quando o grub pede ela para abrir o dispositivo LUKS1, outra quando o mkiniticpio assume o controle do sistema). Isto é feito ao criar uma [keyfile](/index.php/Dm-crypt/Encripta%C3%A7%C3%A3o_de_dispositivo#Keyfiles "Dm-crypt/Encriptação de dispositivo") e adicionando ela na imagem intramfs, fazendo com que o hook encrypt abra o dispositivo raiz. Veja [dm-crypt/Encriptação de dispositivo#Com uma keyfile no initramfs](/index.php/Dm-crypt/Encripta%C3%A7%C3%A3o_de_dispositivo#With_a_keyfile_embedded_in_the_initramfs "Dm-crypt/Encriptação de dispositivo") para detalhes.

*   Crie a [keyfile](/index.php/Dm-crypt/Encripta%C3%A7%C3%A3o_de_dispositivo#Keyfiles "Dm-crypt/Encriptação de dispositivo") e adicione a chave para `/dev/md/raiz`.
*   Crie outra keyfile para o HDD (`/dev/sdc1`) para que ele seja decriptografado na inicialização. Para conveniência, deixe a senha criada acima em um lugar onde você consiga recuperar facilmente se precisar. Edite o `/etc/crypttab` para decriptografar o HDD na inicialização. Veja [Dm-crypt/Configuração do sistema#Desbloqueando com uma keyfile](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema#Desbloqueando_com_uma_keyfile "Dm-crypt/Configuração do sistema").

### Configurando o sistema

Edite o [fstab](/index.php/Fstab "Fstab") para montar os dispositivos de bloco *cryptraiz* e *cryptdata* e o ESP:

```
/dev/mapper/cryptraiz  /           ext4    rw,noatime  0   1
/dev/mapper/cryptdata  /data       ext4    defaults            0   2
/dev/md/ESP            /efi        vfat    rw,relatime,codepage=437,iocharset=iso8859-1,shortname=mixed,utf8,tz=UTC,errors=remount-ro  0   2

```

Save a configuração do RAID:

```
# mdadm --detail --scan >> /etc/mdadm.conf

```

Edite o [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf") e inclua sua keyfile, também coloque os hooks apropriados:

```
FILES=(/crypto_keyfile.bin)
HOOKS=(base udev autodetect **keyboard** **keymap** consolefont modconf block **mdadm_udev** **encrypt** filesystems fsck)

```

Veja [dm-crypt/Configuração do sistema#Mkinitcpio](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema#Mkinitcpio "Dm-crypt/Configuração do sistema") para detalhes.

## Plain dm-crypt

Diferente do LUKS, o modo *plain* do dm-crypt não precisa de um cabeçalho no dispositivo criptografado: Este cenário explora isso para configurar um sistema em uma partição não criptografada, o disco criptografado não será diferenciável de um disco cheio de dados randômicos, isto possibilita a [criptografia negável](https://en.wikipedia.org/wiki/pt:criptografia_neg%C3%A1vel "wikipedia:pt:criptografia negável"). Veja também [wikipedia:Disk encryption#Full disk encryption](https://en.wikipedia.org/wiki/Disk_encryption#Full_disk_encryption "wikipedia:Disk encryption").

Se a encriptação total de disco não é necessária, os métodos usando LUKS descritos nas seções acima são mais recomendados, tanto para a encriptação de sistema quanto partições. Funcionalidades do LUKS como gerenciamento de chaves com múltiplas senhas/keyfiles ou re-criptografar um dispositivo prontamente não estão disponiveis com o modo *plain*.

O modo *Plain* pode ser mais resiliente a danos que o LUKS, devido a não depender de um chave mestre de encriptação, que se danificada resulta em falhas. No entanto, usar esse modo requer mais configuração manual de opções de encriptação para se chegar a mesma força criptográfica. Veja também [Criptografia de disco#Metadata criptográfica](/index.php/Disk_encryption#Cryptographic_metadata "Disk encryption"). O uso desse modo também pode ser considerado se está preocupado com os problemas explicados em [dm-crypt/Especificidades#Discard/TRIM para discos de estado sólido (SSD)](/index.php/Dm-crypt/Specialties#Discard/TRIM_support_for_solid_state_drives_(SSD) "Dm-crypt/Specialties").

**Dica:** Se deseja encriptação sem cabeçalho mas não está com certeza sobre a falta de derivação de chaves com o modo *plain*, então duas alternativas:

*   [dm-crypt modo LUKS com um cabeçalho desanexado](/index.php/Dm-crypt/Specialties#Encrypted_system_using_a_detached_LUKS_header "Dm-crypt/Specialties"), usando a opção `--header`. Este método não pode ser usado com o hook *encrypt* padrão, mas sim com um modificado.
*   [tcplay](/index.php/Tcplay "Tcplay") que oferece a encriptação sem cabeçalho mas com a função PBKDF2.

O cenário usa dois pendrives USB:

*   um para o dispositivo de boot, que permite guardar as opções necessárias para abrir/desbloquear o dispositivo criptografado com o modo plain nas configurações do gerenciador de boot, desde que digitar eles a cada inicialização deve possivelemente resultar em erros;
*   outro para o arquivo chave (keyfile) da encriptação, assumindo que este está guardado em bits normais, o atacante desatento pode conseguir o pendrive com o arquivo chave e pensar que ele é um dado randômico ao invês de ser visível como um arquivo normal. Veja também [Segurança por obscurantismo](https://en.wikipedia.org/wiki/pt:Seguran%C3%A7a_por_obscurantismo "wikipedia:pt:Segurança por obscurantismo"), siga [dm-crypt/Encriptação de dispositivo#Keyfiles](/index.php/Dm-crypt/Encripta%C3%A7%C3%A3o_de_dispositivo#Keyfiles "Dm-crypt/Encriptação de dispositivo") para prepará-la.

O exemplo de particionamento é:

```
+-----------------------+-----------------------+-----------------------+ +----------------+ +---------------+
| Volume lógico 1       | Volume lógico 2       | Volume lógico 3       | | Dispositivo de | | Lugar onde a  |
|                       |                       |                       | | boot           | | keyfile será  |
|                       |                       |                       | |                | | guardada (não |
| /                     | [SWAP]                | /home                 | | /boot          | | particionada  |
|                       |                       |                       | |                | | no exemplo)   |
|                       |                       |                       | |                | |               |
| /dev/MeuVolGrupo/raiz | /dev/MeuVolGrupo/swap | /dev/MeuVolGrupo/home | | /dev/sdb1      | | /dev/sdc      |
|-------------------------+----------------------+----------------------| |----------------| |---------------|
| O disco /dev/sda é criptografado com o modo plain e usa LVM           | | Pendrive 1     | | Pendrive 2    |
+-----------------------------------------------------------------------+ +----------------+ +---------------+

```

**Dica:**

*   É possível usar somente um pendrive:
    *   Ao colocar a chave em outra partição (por exemplo, /dev/sdb2).
    *   Ao copiar a keyfile para o initramfs diretamente. Por exemplo, uma keyfile é copiada para a imagem initramfs ao colocar `FILES=(/etc/keyfile)` em `/etc/mkinitcpio.conf`. Para fazer o hook `encrypt` ler a keyfile na imagem initramfs, use o prefixo `rootfs:` antes do nome do arquivo, exemplo `cryptkey=rootfs:/etc/keyfile`.
*   Outra opção é usar uma senha com uma boa [entropia](/index.php/Disk_encryption#Choosing_a_strong_passphrase "Disk encryption").

### Preparando o disco

É vital que o dispositivo mapeado tenha dados randômicos. Em particular nesse cenário.

Veja [dm-crypt/Preparando a unidade de armazenamento](/index.php/Dm-crypt/Preparando_a_unidade_de_armazenamento "Dm-crypt/Preparando a unidade de armazenamento") e [dm-crypt/Preparando a unidade de armazenamento#Métodos específicos do dm-crypt](/index.php/Dm-crypt/Preparando_a_unidade_de_armazenamento#Métodos_específicos_do_dm-crypt "Dm-crypt/Preparando a unidade de armazenamento")

### Preparando a partição que não é de boot

Veja [dm-crypt/Encriptação de dispositivo#Opções de encriptação para o modo plain](/index.php/Dm-crypt/Encripta%C3%A7%C3%A3o_de_dispositivo#Opções_de_encriptação_para_o_modo_plain "Dm-crypt/Encriptação de dispositivo") para detalhes.

Usando o dispositivo `/dev/sda`, com a cifra aes-xts, tamanho de chave de 512 bit e uma keyfile, temos as seguintes opções para esse cenário:

```
# cryptsetup --cipher=aes-xts-plain64 --offset=0 --key-file=/dev/sdc --key-size=512 open --type plain /dev/sda cryptlvm

```

Diferente da encriptação com LUKS, o comando acima deve ser executado *completamente* toda vez que o mapeamento precisa ser restabelecido, então é importante lembrar da cifra e detalhes da keyfile.

Podemos agora checar se a entrada de mapeamento foi feita para `/dev/mapper/cryptlvm`:

```
# fdisk -l

```

**Dica:** Uma alternativa simples para o LVM, em casos do FAQ do cryptsetup onde ele não é necessário, é somente criar um sistema de arquivos com todo o dispositivo mapeado.

Agora, configurare os volumes lógicos do [LVM](/index.php/LVM "LVM") no dispositivo mapeado. Veja [LVM#Installing Arch Linux on LVM](/index.php/LVM#Installing_Arch_Linux_on_LVM "LVM") para maiores detalhes:

```
# pvcreate /dev/mapper/cryptlvm
# vgcreate MeuVolGrupo /dev/mapper/cryptlvm
# lvcreate -L 32G MeuVolGrupo -n raiz
# lvcreate -L 10G MeuVolGrupo -n swap
# lvcreate -l 100%FREE MeuVolGrupo -n home

```

Formate e monte eles além de ativar a swap. Veja [File systems#Create a file system](/index.php/File_systems#Create_a_file_system "File systems") para mais detalhes:

```
# mkfs.ext4 /dev/MeuVolGrupo/raiz
# mkfs.ext4 /dev/MeuVolGrupo/home
# mount /dev/MeuVolGrupo/raiz /mnt
# mkdir /mnt/home
# mount /dev/MeuVolGrupo/home /mnt/home
# mkswap /dev/MeuVolGrupo/swap
# swapon /dev/MeuVolGrupo/swap

```

### Preparando a partição de boot

A partição `/boot` pode ser instalada na partição vfat de um pendrive, se necessário. Mas se o particionamento manual é desejado, criar uma partição de 200 MiB é necessário. Crie a partição usando uma [ferramenta de particionamento](/index.php/Partitioning#Partitioning_tools "Partitioning") de sua escolha.

Coloque um [sistema de arquivos](/index.php/Filesystem "Filesystem") na partição `/boot`:

```
# mkfs.ext4 /dev/sdb1
# mkdir /mnt/boot
# mount /dev/sdb1 /mnt/boot

```

### Configurando mkinitcpio

Adicione os hooks `keyboard`, `encrypt` e `lvm2` no [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"):

```
HOOKS=(base udev autodetect **keyboard** **keymap** consolefont modconf block **encrypt** **lvm2** filesystems fsck)

```

Veja [dm-crypt/Configuração do sistema#mkinitcpio](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema#mkinitcpio "Dm-crypt/Configuração do sistema") para detalhes e outros hooks que você pode precisar.

### Configurando o gerenciador de boot

Para inicializar a partição raiz criptografada, os seguintes [parâmetros do kernel](/index.php/Par%C3%A2metros_do_kernel "Parâmetros do kernel") precisma ser definidos no gerenciador de boot (note que 64 é o número de bytes em 512 bits):

```
cryptdevice=/dev/disk/by-id/*ID-do-sda*:cryptlvm cryptkey=/dev/disk/by-id/*ID-do-sdc*:0:64 crypto=:aes-xts-plain64:512:0:

```

`*ID-do-**disco***` significa o id do disco referenciado. Veja [Nomeação persistente de dispositivo de bloco](/index.php/Nomea%C3%A7%C3%A3o_persistente_de_dispositivo_de_bloco "Nomeação persistente de dispositivo de bloco") para detalhes.

Veja [dm-crypt/Configuração do sistema#Gerenciador de boot](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema#Gerenciador_de_boot "Dm-crypt/Configuração do sistema") para mais detalhes e outros parâmetros que você pode precisar.

**Dica:** Se está usando o GRUB, você pode instalar no mesmo pendrive da partição /boot com:
```
# grub-install --recheck /dev/sdb

```

### Pós-instalação

Você pode remover os pendrives depois da inicialização. Já que a partição `/boot` não é normalmente necessária, a opção `noauto` pode ser adicionada na linha relevante em `/etc/fstab`:

 `/etc/fstab` 
```
# /dev/sdb1
/dev/sdb1 /boot ext4 **noauto**,rw,noatime 0 2

```

No entanto, quando uma atualização é feita para o initramfs, kernel ou gerenciador de boot é necessário que ela esteja montada. Como uma entrada no `fstab` já existe, ela pode ser montada simplesmente com:

```
# mount /boot

```

## Partição de boot criptografada (GRUB)

Esta configuração utiliza o mesmo particionamento que a seção [#LVM dentro do LUKS](#LVM_dentro_do_LUKS), com diferença que o [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)") é usado por ser capaz de inicializar de um volume lógico LVM e um `/boot` criptografado com LUKS1\. Veja também [GRUB#/boot criptografado](/index.php/GRUB_(Portugu%C3%AAs)#/boot_criptografado "GRUB (Português)").

O Particionamento deste exemplo é:

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