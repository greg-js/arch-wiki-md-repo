**Status de tradução:** Esse artigo é uma tradução de [Dm-crypt/Encrypting an entire system](/index.php/Dm-crypt/Encrypting_an_entire_system "Dm-crypt/Encrypting an entire system"). Data da última tradução: 2019-12-17\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Dm-crypt/Encrypting_an_entire_system&diff=0&oldid=591754) na versão em inglês.

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
    *   [7.1 Preparando o disco](#Preparando_o_disco_5)
    *   [7.2 Preparando os volumes lógicos](#Preparando_os_volumes_lógicos_3)
    *   [7.3 Configurando o mkinitcpio](#Configurando_o_mkinitcpio_4)
    *   [7.4 Configurando o GRUB](#Configurando_o_GRUB_2)
    *   [7.5 Evite digitar a senha duas vezes](#Evite_digitar_a_senha_duas_vezes)
*   [8 Subvolumes do Btrfs com swap](#Subvolumes_do_Btrfs_com_swap)
    *   [8.1 Preparando o disco](#Preparando_o_disco_6)
    *   [8.2 Preparando a partição do sistema](#Preparando_a_partição_do_sistema)
        *   [8.2.1 Crie o container LUKS](#Crie_o_container_LUKS)
        *   [8.2.2 Abra o container LUKS](#Abra_o_container_LUKS)
        *   [8.2.3 Formate o dispositivo mapeado](#Formate_o_dispositivo_mapeado)
        *   [8.2.4 Monte o dispositivo mapeado](#Monte_o_dispositivo_mapeado)
    *   [8.3 Criando subvolumes do btrfs](#Criando_subvolumes_do_btrfs)
        *   [8.3.1 Esboço](#Esboço)
        *   [8.3.2 Crie os subvolumes de nível superior](#Crie_os_subvolumes_de_nível_superior)
        *   [8.3.3 Monte os subvolumes de nível superior](#Monte_os_subvolumes_de_nível_superior)
        *   [8.3.4 Crie os subvolumes aninhados](#Crie_os_subvolumes_aninhados)
        *   [8.3.5 Monte a ESP](#Monte_a_ESP)
    *   [8.4 Configurando o mkinitcpio](#Configurando_o_mkinitcpio_5)
        *   [8.4.1 Crie a keyfile](#Crie_a_keyfile)
        *   [8.4.2 Edite o mkinitcpio.conf](#Edite_o_mkinitcpio.conf)
    *   [8.5 Configurando o gerenciador de boot](#Configurando_o_gerenciador_de_boot_5)
    *   [8.6 Configurando a swap](#Configurando_a_swap)

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
*   Ajuda a solucionar [problemas](/index.php/Dm-crypt/Especificidades#Suporte_a_discard/TRIM_para_unidades_de_estado_sólido_(SSD) "Dm-crypt/Especificidades") com SSDs

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
| [#Subvolumes do Btrfs com swap](#Subvolumes_do_Btrfs_com_swap)

Mostra como criptografar um sistema [Btrfs](/index.php/Btrfs "Btrfs"), incluindo o diretório `/boot`, também é possível adicionar uma partição para swap, em um hardware com suporte a UEFI.

 | 

*   similar a [#Partição de boot criptografada (GRUB)](#Partição_de_boot_criptografada_(GRUB))
*   Disponibilidade das funcionalidades do Btrfs

 | 

*   Similar a [#Partição de boot criptografada (GRUB)](#Partição_de_boot_criptografada_(GRUB))

 |

Enquanto todos os cenários acima oferecem maior proteção contra ameaças externas do que somente criptografar sistemas de arquivos não raiz, eles também possuem uma desvantagem comum: qualquer usuário que possui a chave pode abrir todo o disco, e assim, acessar os dados de outro usuário. Se isto é uma preocupação, é possível fazer uma combinação de dispositivo de blocos e sistema de arquivos criptografados empilhados e adquirir as vantagens de ambos. Veja [Criptografia de disco](/index.php/Criptografia_de_disco "Criptografia de disco") para lhe ajudar no planejamento.

Veja [Dm-crypt/Preparando a unidade de armazenamento#Particionamento](/index.php/Dm-crypt/Preparando_a_unidade_de_armazenamento#Particionamento "Dm-crypt/Preparando a unidade de armazenamento") para uma visão geral das estratégias de particionamento usadas nos cenários.

Outra coisa a considerar é se deve usar uma partição swap criptografada e de qual forma. Veja [Dm-crypt/Swap criptografada](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption") para alternativas.

Se você antecipa a proteção de dados do sistema não somente contra roubo físico, como também contra adulteração lógica, veja [Dm-crypt/Especificidades#Protegendo a partição de boot não criptografada](/index.php/Dm-crypt/Especificidades#Securing_the_unencrypted_boot_partition "Dm-crypt/Especificidades") para possibilidades futuras após seguir um dos cenários.

Para [SSDs](/index.php/Solid_state_drive "Solid state drive"), você pode considerar habilitar suporte ao TRIM, mas esteja ciente que, isto tem potenciais problemas de segurança. Veja [Dm-crypt/Especificidades#Suporte a discard/TRIM para unidades de estado sólido (SSD)](/index.php/Dm-crypt/Especificidades#Suporte_a_discard/TRIM_para_unidades_de_estado_sólido_(SSD) "Dm-crypt/Especificidades") para mais informações.

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
|                    |                               |                       |
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

Os comandos a seguir criam e montam a partição raiz criptografada. Eles correspondem ao detalhado procedimento descrito em [dm-crypt/Criptografando um sistema de arquivos não raiz#Partição](/index.php/Dm-crypt/Criptografando_um_sistema_de_arquivos_n%C3%A3o_raiz#Partição "Dm-crypt/Criptografando um sistema de arquivos não raiz") (que, apesar do título, *pode* ser aplicado a partições raiz, contanto que [mkinitcpio](#Configurando_o_mkinitcpio) e o [gerenciador de boot](#Configurando_o_gerenciador_de_boot) sejam corretamente configurados). Se você deseja usar opções de encriptação que não são padrão (exemplo, cifras criptográficas, tamanho da chave), veja as [opções de encriptação](/index.php/Dm-crypt/Encripta%C3%A7%C3%A3o_de_dispositivo#Opções_de_encriptação_para_o_modo_LUKS "Dm-crypt/Encriptação de dispositivo") antes de executar o primeiro comando:

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

Note que cada dispositivo de bloco precisa de sua própria senha. Isto pode ser inconveniente, por ser necessário inserir senhas separadas durante a inicialização. Uma alternativa é usar uma keyfile guardada na partição do sistema para desbloquear a partição separada por meio do `crypttab`. Veja [dm-crypt/Encriptação de dispositivo#Formatando uma partição com LUKS e uma keyfile](/index.php/Dm-crypt/Encripta%C3%A7%C3%A3o_de_dispositivo#Formatando_uma_partição_com_LUKS_e_uma_keyfile "Dm-crypt/Encriptação de dispositivo") para instruções.

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

Dependendo de quais hooks estão sendo usados, a ordem pode ser relevante. Veja [dm-crypt/Configuração do sistema#mkinitcpio](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema#mkinitcpio "Dm-crypt/Configuração do sistema") para detalhes e outros hooks que você pode precisar.

### Configurando o gerenciador de boot

Para desbloquear a partição raiz criptografada na inicialização, os seguintes [parâmetros do kernel](/index.php/Par%C3%A2metros_do_kernel "Parâmetros do kernel") devem ser adicionados ao gerenciador de boot:

```
cryptdevice=UUID=*UUID-da-partição-raiz*:cryptroot root=/dev/mapper/cryptroot

```

Se está usando o hook [sd-encrypt](/index.php/Sd-encrypt "Sd-encrypt"), o seguinte precisa ser definido ao invês:

```
rd.luks.name=*UUID-da-partição-raiz*=cryptroot root=/dev/mapper/cryptroot

```

Veja [dm-crypt/Configuração do sistema#Gerenciador de boot](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema#Gerenciador_de_boot "Dm-crypt/Configuração do sistema") para detalhes.

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

**Nota:** Ao usar o hook `encrypt`, você não poderá utilizar volumes lógicos espalhados em múltiplos discos; use o [sd-encrypt](/index.php/Sd-encrypt "Sd-encrypt") ou veja [dm-crypt/Especificidades#Modificando o hook encrypt para múltiplas partições](/index.php/Dm-crypt/Especificidades#Modifying_the_encrypt_hook_for_multiple_partitions "Dm-crypt/Especificidades").

**Dica:** Duas variações dessa configuração:

*   Instruções em [dm-crypt/Especificidades#Sistema criptografado com cabeçalho do LUKS desanexado](/index.php/Dm-crypt/Especificidades#Encrypted_system_using_a_detached_LUKS_header "Dm-crypt/Especificidades") para usar um cabeçalho do LUKS em um dispositivo USB, e assim conseguindo autentificação de dois fatores com este método.
*   Instruções em [dm-crypt/Especificidades#/boot criptografado e um cabeçalho do LUKS desanexado dentro de um USB](/index.php/Dm-crypt/Especificidades#Encrypted_/boot_and_a_detached_LUKS_header_on_USB "Dm-crypt/Especificidades")]] para usar um cabeçalho do LUKS, partição `/boot` criptografada, e keyfile criptografada tudo em um dispositivo USB.

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

Para mais informações sobre as opções disponíveis do cryptsetup veja as [opções de encriptação](/index.php/Dm-crypt/Encripta%C3%A7%C3%A3o_de_dispositivo#Opções_de_encriptação_para_o_modo_LUKS "Dm-crypt/Encriptação de dispositivo") antes de executar o comando acima.

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

Veja [dm-crypt/Configuração do sistema#mkinitcpio](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema#mkinitcpio "Dm-crypt/Configuração do sistema") para detalhes e outros hooks que você pode precisar.

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

Se quer usar volumes lógicos espalhados por múltiplos discos que já foram configurados, ou expandir o `/home` (ou qualquer outro volume), um dos jeitos de como fazer isto é descrito em [dm-crypt/Especificidades#Expandindo LVM em vários discos](/index.php/Dm-crypt/Especificidades#Expanding_LVM_on_multiple_disks "Dm-crypt/Especificidades"). Vale notar que o container criptografado com LUKS precisa ser redimensionado também.

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

sobrescreva `/dev/sda2` de acordo com [dm-crypt/Preparando a unidade de armazenamento#dm-crypt limpa o disco vazio ou partição](/index.php/Dm-crypt/Preparando_a_unidade_de_armazenamento#dm-crypt_limpa_o_disco_vazio_ou_partição "Dm-crypt/Preparando a unidade de armazenamento").

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

Mais informações sobre opções de encriptação podem ser encontradas em [dm-crypt/Encriptação de dispositivo#Opções de encriptação para o modo LUKS](/index.php/Dm-crypt/Encripta%C3%A7%C3%A3o_de_dispositivo#Opções_de_encriptação_para_o_modo_LUKS "Dm-crypt/Encriptação de dispositivo"). Note que `/home` será criptografada em [#Criptografando o volume lógico /home](#Criptografando_o_volume_lógico_/home).

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

Devido a este cenário usar LVM como mapeador primário e dm-crypt como secundário, cada volume lógico precisa ser criptografado separadamente. Apesar disso, diferente dos sistemas de arquivos temporários que foram configurados acima para serem voláteis, o volume lógico para `/home` vai ser persistente. O seguinte assume que você reiniciou o seu sistema criptografado, se você não fez isto, precisará adaptar os caminhos. Para não digitar uma segunda senha na inicialização, uma [keyfile](/index.php/Dm-crypt/Encripta%C3%A7%C3%A3o_de_dispositivo#Keyfiles "Dm-crypt/Encriptação de dispositivo") é criada:

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

Veja [dm-crypt/Configuração do sistema#Gerenciador de boot](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema#Gerenciador_de_boot "Dm-crypt/Configuração do sistema") e [GRUB#/boot criptografado](/index.php/GRUB_(Portugu%C3%AAs)#/boot_criptografado "GRUB (Português)") para detalhes.

Complete a instalação do GRUB para ambos os SSDs (em realidade, instalando somente em `/dev/sda` irá funcionar).

```
# grub-install --target=i386-pc /dev/sda
# grub-install --target=i386-pc /dev/sdb
# grub-install --target=x86_64-efi --efi-directory=/efi --bootloader-id=GRUB
# grub-mkconfig -o /boot/grub/grub.cfg

```

### Criando as keyfiles

Os próximos passos evitarão que você digite a senha duas vezes quando você inicializar o sistema (uma vez quando o grub pede ela para abrir o dispositivo LUKS1, outra quando o mkinitcpio assume o controle do sistema). Isto é feito ao criar uma [keyfile](/index.php/Dm-crypt/Encripta%C3%A7%C3%A3o_de_dispositivo#Keyfiles "Dm-crypt/Encriptação de dispositivo") e adicionando ela na imagem intramfs, fazendo com que o hook encrypt abra o dispositivo raiz. Veja [dm-crypt/Encriptação de dispositivo#Com uma keyfile no initramfs](/index.php/Dm-crypt/Encripta%C3%A7%C3%A3o_de_dispositivo#Com_uma_keyfile_no_initramfs "Dm-crypt/Encriptação de dispositivo") para detalhes.

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

Veja [dm-crypt/Configuração do sistema#mkinitcpio](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema#mkinitcpio "Dm-crypt/Configuração do sistema") para detalhes.

## Plain dm-crypt

Diferente do LUKS, o modo *plain* do dm-crypt não precisa de um cabeçalho no dispositivo criptografado: Este cenário explora isso para configurar um sistema em uma partição não criptografada, o disco criptografado não será diferenciável de um disco cheio de dados randômicos, isto possibilita a [criptografia negável](https://en.wikipedia.org/wiki/pt:criptografia_neg%C3%A1vel "wikipedia:pt:criptografia negável"). Veja também [wikipedia:Disk encryption#Full disk encryption](https://en.wikipedia.org/wiki/Disk_encryption#Full_disk_encryption "wikipedia:Disk encryption").

Se a encriptação total de disco não é necessária, os métodos usando LUKS descritos nas seções acima são mais recomendados, tanto para a encriptação de sistema quanto partições. Funcionalidades do LUKS como gerenciamento de chaves com múltiplas senhas/keyfiles ou re-criptografar um dispositivo prontamente não estão disponiveis com o modo *plain*.

O modo *plain* pode ser mais resiliente a danos que o LUKS, devido a não depender de um chave mestre de encriptação, que se danificada resulta em falhas. No entanto, usar esse modo requer mais configuração manual de opções de encriptação para se chegar a mesma força criptográfica. Veja também [Criptografia de disco#Metadados criptográficos](/index.php/Criptografia_de_disco#Metadados_criptográficos "Criptografia de disco"). O uso desse modo também pode ser considerado se está preocupado com os problemas explicados em [dm-crypt/Especificidades#Suporte a discard/TRIM para unidades de estado sólido (SSD)](/index.php/Dm-crypt/Especificidades#Suporte_a_discard/TRIM_para_unidades_de_estado_sólido_(SSD) "Dm-crypt/Especificidades").

**Dica:** Se deseja encriptação sem cabeçalho mas não está com certeza sobre a falta de derivação de chaves com o modo *plain*, então duas alternativas:

*   [dm-crypt modo LUKS com um cabeçalho desanexado](/index.php/Dm-crypt/Especificidades#Encrypted_system_using_a_detached_LUKS_header "Dm-crypt/Especificidades"), usando a opção `--header`. Este método não pode ser usado com o hook *encrypt* padrão, mas sim com um modificado.
*   [tcplay](/index.php/Tcplay "Tcplay") que oferece a encriptação sem cabeçalho mas com a função PBKDF2.

O cenário usa dois pendrives USB:

*   um para o dispositivo de boot, que permite guardar as opções necessárias para abrir/desbloquear o dispositivo criptografado com o modo plain nas configurações do gerenciador de boot, desde que digitar eles a cada inicialização deve possivelemente resultar em erros;
*   outro para a keyfile (arquivo chave), assumindo que esta está guardada em bits normais, o atacante desatento pode conseguir o pendrive com ela e pensar que a keyfile é um dado randômico ao invês de ser visível como um arquivo normal. Veja também [Segurança por obscurantismo](https://en.wikipedia.org/wiki/pt:Seguran%C3%A7a_por_obscurantismo "wikipedia:pt:Segurança por obscurantismo"), siga [dm-crypt/Encriptação de dispositivo#Keyfiles](/index.php/Dm-crypt/Encripta%C3%A7%C3%A3o_de_dispositivo#Keyfiles "Dm-crypt/Encriptação de dispositivo") para prepará-la.

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
*   Outra opção é usar uma senha com uma boa [entropia](/index.php/Criptografia_de_disco#Escolhendo_uma_senha_forte "Criptografia de disco").

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

Agora, configure os volumes lógicos do [LVM](/index.php/LVM "LVM") no dispositivo mapeado. Veja [LVM#Installing Arch Linux on LVM](/index.php/LVM#Installing_Arch_Linux_on_LVM "LVM") para maiores detalhes:

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
+--------------------+---------------------+-----------------------+-----------------------+-----------------------+
| Partição de        | Partição de sistema | Volume Lógico 1       | volume lógico 2       | volume lógico 3       |
| inicialização BIOS | EFI                 |                       |                       |                       |
|                    |                     |                       |                       |                       |
|                    | /efi                | /                     | [SWAP]                | /home                 |
|                    |                     |                       |                       |                       |
|                    |                     | /dev/MeuVolGrupo/raiz | /dev/MeuVolGrupo/swap | /dev/MeuVolGrupo/home |
| /dev/sda1          | /dev/sda2           |-----------------------+-----------------------+-----------------------+
| não criptografado  | não criptografado   | /dev/sda3 criptografado usando LVM dentro do LUKS1                    |
+--------------------+---------------------+-----------------------------------------------------------------------+

```

**Dica:**

*   Todos os cenários são exemplos. É possível utilizar os conceitos de distintos cenários na sua instalação, claro adaptando o que for necessário. Veja também uma variação desse cenário em [#LVM dentro do LUKS](#LVM_dentro_do_LUKS).
*   Você pode usar o script `cryptboot` do pacote [cryptboot](https://aur.archlinux.org/packages/cryptboot/) para um gerenciamento simplificado da inicialização com partição de boot criptografada (montar, desmontar, atualizar pacotes) e como uma defesa contra o ataque [Evil Maid](https://www.schneier.com/blog/archives/2009/10/evil_maid_attac.html) com [UEFI Secure Boot](/index.php/Secure_Boot#Using_your_own_keys "Secure Boot"). Para mais detalhes e limitações veja a página do [projeto cryptboot](https://github.com/xmikos/cryptboot).

### Preparando o disco

Antes de criar qualquer partição, você deve saber a importância e métodos de como apagar o disco com segurança, descrito em [dm-crypt/Preparando a unidade de armazenamento](/index.php/Dm-crypt/Preparando_a_unidade_de_armazenamento "Dm-crypt/Preparando a unidade de armazenamento").

Para [sistemas BIOS](/index.php/GRUB_(Portugu%C3%AAs)#Sistemas_BIOS "GRUB (Português)") crie uma [partição de inicialização de BIOS](/index.php/Parti%C3%A7%C3%A3o_de_inicializa%C3%A7%C3%A3o_de_BIOS "Partição de inicialização de BIOS") com o tamanho de 1 MiB para que o GRUB guarde o segundo estágio da inicialização BIOS. não monte a partição.

Para [sistemas UEFI](/index.php/GRUB_(Portugu%C3%AAs)#Sistemas_UEFI "GRUB (Português)") crie uma [partição de sistema EFI](/index.php/Parti%C3%A7%C3%A3o_de_sistema_EFI "Partição de sistema EFI") com tamanho apropriado, será montada em `/efi`.

Crie uma partição do tipo `8309`, que mais tarde conterá o container criptografado para a LVM.

Crie o container criptografado com LUKS:

**Atenção:** GRUB não suporta LUKS2\. Use LUKS1 (`--type luks1`) em partições que o GRUB precisa acessar.

```
# cryptsetup luksFormat --type luks1 /dev/sda3

```

Para mais informações sobre as opções do cryptsetup disponíveis, veja [dm-crypt/Encriptação de dispositivo#Opções de encriptação para o modo LUKS](/index.php/Dm-crypt/Encripta%C3%A7%C3%A3o_de_dispositivo#Opções_de_encriptação_para_o_modo_LUKS "Dm-crypt/Encriptação de dispositivo") antes do comando acima.

Seu particionamento deve ser similar a:

 `# gdisk -l /dev/sda` 
```
...
Number  Start (sector)    End (sector)  Size       Code  Name
   1            2048            4095   1024.0 KiB  EF02  BIOS boot partition
   2            4096         1130495   550.0 MiB   EF00  EFI System
   3         1130496        68239360   32.0 GiB    8309  Linux LUKS

```

Abra o container:

```
# cryptsetup open /dev/sda3 cryptlvm

```

o container aberto agora está disponível em `/dev/mapper/cryptlvm`.

### Preparando os volumes lógicos

Os volumes lógicos do LVM neste exemplo seguem o particionamento acima como o cenário [#LVM dentro do LUKS](#LVM_dentro_do_LUKS). Siga [#Preparando os volumes lógicos](#Preparando_os_volumes_lógicos) acima, ajuste o que desejar e precisar.

Se você planeja inicializar no modo UEFI, crie um ponto de montagem para [partição de sistema EFI](/index.php/Parti%C3%A7%C3%A3o_de_sistema_EFI "Partição de sistema EFI") em `/efi` para compatibilidade com `grub-install` e monte:

```
# mkdir /mnt/efi
# mount /dev/sda2 /mnt/efi

```

Neste ponto, você deve ter as seguintes partições e volumes lógicos dentro de `/mnt`:

 `$ lsblk` 
```
NAME                   MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINT
sda                      8:0    0   200G  0 disk
├─sda1                   8:1    0     1M  0 part
├─sda2                   8:2    0   550M  0 part  /mnt/efi
└─sda3                   8:3    0   100G  0 part
  └─cryptlvm           254:0    0   100G  0 crypt
    ├─MeuVolGrupo-swap 254:1    0     8G  0 lvm   [SWAP]
    ├─MeuVolGrupo-root 254:2    0    32G  0 lvm   /mnt
    └─MeuVolGrupo-home 254:3    0    60G  0 lvm   /mnt/home

```

### Configurando o mkinitcpio

Adicione os hooks `keyboard`, `encrypt` e `lvm2` no [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"):

```
HOOKS=(base **udev** autodetect **keyboard** **keymap** consolefont modconf block **encrypt** **lvm2** filesystems fsck)

```

Se está usando o hook [sd-encrypt](/index.php/Sd-encrypt "Sd-encrypt") com o initramfs baseado no systemd, o seguinte precisa ser definido ao invês:

```
HOOKS=(base **systemd** autodetect **keyboard** **sd-vconsole** modconf block **sd-encrypt** **sd-lvm2** filesystems fsck)

```

Veja [dm-crypt/Configuração do sistema#mkinitcpio](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema#mkinitcpio "Dm-crypt/Configuração do sistema") para detalhes e outros hooks que você pode precisar.

### Configurando o GRUB

Para permitir a inicialização, configure o GRUB para que ele consiga acessar o `/boot` que está dentro de uma partição criptografada com LUKS1:

 `/etc/default/grub`  `GRUB_ENABLE_CRYPTODISK=y` 

Defina os parâmetros do kernel, para que o initramfs possa abrir a partição raiz criptografada. Se for usar o hook `encrypt`:

 `/etc/default/grub`  `GRUB_CMDLINE_LINUX="... cryptdevice=UUID=*UUID-do-dispositivo*:cryptlvm ..."` 

Se for usar o hook [sd-encrypt](/index.php/Sd-encrypt_(Portugu%C3%AAs) "Sd-encrypt (Português)"), o seguinte precisa ser definido:

 `/etc/default/grub`  `GRUB_CMDLINE_LINUX="... rd.luks.name=*UUID-do-dipositivo*=cryptlvm ..."` 

Veja [dm-crypt/Configuração do sistema#Gerenciador de boot](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema#Gerenciador_de_boot "Dm-crypt/Configuração do sistema") e [GRUB#/boot criptografado](/index.php/GRUB_(Portugu%C3%AAs)#/boot_criptografado "GRUB (Português)") for details. `*UUID-do-dispositivo*` faz referência ao UUID do `/dev/sda3` (a partição que tem o sistema de arquivos raiz contido no LVM). Veja [Nomeação persistente de dispositivo de bloco](/index.php/Nomea%C3%A7%C3%A3o_persistente_de_dispositivo_de_bloco "Nomeação persistente de dispositivo de bloco").

[instale o GRUB](/index.php/GRUB_(Portugu%C3%AAs)#Instalação_2 "GRUB (Português)") na ESP montada para inicialização UEFI:

```
# grub-install --target=x86_64-efi --efi-directory=/efi --bootloader-id=GRUB --recheck

```

[instale o GRUB](/index.php/GRUB_(Portugu%C3%AAs)#Instalação "GRUB (Português)") no disco para inicialização BIOS:

```
# grub-install --target=i386-pc --recheck /dev/sda

```

Gere o arquivo de [configuração](/index.php/GRUB_(Portugu%C3%AAs)#Gerar_o_arquivo_de_configuração_principal "GRUB (Português)") do GRUB:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

Se todos os comandos foram executados sem erros, GRUB deve solicitar a senha para abrir a partição `/dev/sda3` na próxima inicialização.

### Evite digitar a senha duas vezes

apesar do GRUB solicitar a senha para abrir a partição criptografada com LUKS1, isso não é passado para o initramfs. Consequentemente, você vai precisa digitar a senha duas vezes: uma vez para o GRUB e outra para o initramfs.

Esta seção lida com uma configuração extra para digitar a senha somente uma vez, no GRUB. Para isso é utilizado [uma keyfile dentro do initramfs](/index.php/Dm-crypt/Encripta%C3%A7%C3%A3o_de_dispositivo#Com_uma_keyfile_no_initramfs "Dm-crypt/Encriptação de dispositivo").

Primeiro crie uma keyfile e a adicione como uma chave do LUKS:

```
# dd bs=512 count=4 if=/dev/random of=/root/cryptlvm.keyfile iflag=fullblock
# chmod 000 /root/cryptlvm.keyfile
# chmod 600 /boot/initramfs-linux*
# cryptsetup -v luksAddKey /dev/sda3 /root/cryptlvm.keyfile

```

Adicione a keyfile para a imagem do initramfs:

 `/etc/mkinitcpio.conf`  `FILES=(/root/cryptlvm.keyfile)` 

Defina o seguinte parâmetro do kernel para abrir a partição criptografada com a keyfile. Se está usando o hook `encrypt`:

```
GRUB_CMDLINE_LINUX="... cryptkey=rootfs:/root/cryptlvm.keyfile"

```

Ou, usando o hook [sd-encrypt](/index.php/Sd-encrypt_(Portugu%C3%AAs) "Sd-encrypt (Português)"):

```
GRUB_CMDLINE_LINUX="... rd.luks.key=*device-UUID*=/root/cryptlvm.keyfile"

```

Se por algum motivo a keyfile falhar, systemd solicitará a senha para abrir e, em caso dela estar correta, continuar a inicialização.

**Dica:** Se quer criptografar a partição `/boot` para proteger contra ameaças de adulteração offline (offline tampering threats), o hook [mkinitcpio-chkcryptoboot](/index.php/Dm-crypt/Especificidades#mkinitcpio-chkcryptoboot "Dm-crypt/Especificidades") têm sido desenvolvido para isso.

## Subvolumes do Btrfs com swap

O seguinte exemplo cria todo um sistema criptografado com LUKS1, [simulando partições](/index.php/Btrfs#Mounting_subvolumes "Btrfs") com subvolumes do [Btrfs](/index.php/Btrfs "Btrfs").

Ao usar UEFI, uma [Partição de sistema EFI](/index.php/Parti%C3%A7%C3%A3o_de_sistema_EFI "Partição de sistema EFI") (ESP) é necessária. `/boot` pode estar em `/` e ser criptografada; no entanto, a ESP não pode ser criptografada. Neste exemplo, a ESP é `/dev/sda1` e está montada em `/efi`. `/boot` está localizada na partição do sistema, `/dev/sda2`.

Desde que `/boot` reside na `/` criptografada com LUKS1, [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)") deve ser usado como o gerenciador de boot porque somente ele pode carregar os módulos para decriptografar `/boot` (exemplo, crypto.mod, cryptodisk.mod e luks.mod).

Também é mostrada uma partição [swap](/index.php/Swap_(Portugu%C3%AAs) "Swap (Português)") criptografada.

**Atenção:** Não use [arquivo swap](/index.php/Arquivo_swap "Arquivo swap") no Btrfs nas versões do kernel Linux anteriores à 5.0, pode resultar em perca de dados. Veja [Btrfs#Swap file](/index.php/Btrfs#Swap_file "Btrfs").

```
+-----------------------+-------------------------+------------------+
| Partição de sistema   | Partição do sistema     | Partição swap    |
| EFI não criptografada | criptografada com LUKS1 | criptografada    |
|                       |                         |                  |
| /efi                  | /                       | [SWAP]           |
| /dev/sda1             | /dev/sda2               | /dev/sda3        |
|-----------------------+-------------------------+------------------+

```

### Preparando o disco

**Nota:** Não é possível utilizar o btrfs como descrito em [Btrfs#Partitionless Btrfs disk](/index.php/Btrfs#Partitionless_Btrfs_disk "Btrfs") ao usar o LUKS. Particionamento tradicional deve ser usado, mesmo se é somente para criar uma partição.

Antes de criar qualquer partição, você deveria saber a importância e também métodos de como apagar o disco com segurança, descritos em [dm-crypt/Preparando a unidade de armazenamento](/index.php/Dm-crypt/Preparando_a_unidade_de_armazenamento "Dm-crypt/Preparando a unidade de armazenamento"). Se você está usando [UEFI](/index.php/UEFI "UEFI") crie uma [partição de sistema EFI](/index.php/Parti%C3%A7%C3%A3o_de_sistema_EFI "Partição de sistema EFI") com o tamanho apropriado. Ela será montada em `/efi`. Se você vai criar uma partição swap criptografada, crie ela, mas *não* marque isso como swap, desde que ela será usada no modo plain do *dm-crypt*.

Crie as partições, ao menos uma para `/` (exemplo, `/dev/sda2`). Veja o artigo [Partitioning](/index.php/Partitioning "Partitioning").

### Preparando a partição do sistema

#### Crie o container LUKS

**Atenção:** GRUB não suporta LUKS2\. Use LUKS1 (`--type luks1`) em partições que ele precisa acessar.

Siga [dm-crypt/Encriptação de dispositivo#Criptografando dispositivos com o modo LUKS](/index.php/Dm-crypt/Encripta%C3%A7%C3%A3o_de_dispositivo#Criptografando_dispositivos_com_o_modo_LUKS "Dm-crypt/Encriptação de dispositivo") para configurar o `/dev/sda2` para LUKS. Veja o [dm-crypt/Encriptação de dispositivo#Opções de encriptação para o modo LUKS](/index.php/Dm-crypt/Encripta%C3%A7%C3%A3o_de_dispositivo#Opções_de_encriptação_para_o_modo_LUKS "Dm-crypt/Encriptação de dispositivo") para uma lista de opções de encriptação.

#### Abra o container LUKS

Siga [dm-crypt/Encriptação de dispositivo#Abrindo/Mapeando containers LUKS com o mapeador de dispositivos](/index.php/Dm-crypt/Encripta%C3%A7%C3%A3o_de_dispositivo#Abrindo/Mapeando_containers_LUKS_com_o_mapeador_de_dispositivos "Dm-crypt/Encriptação de dispositivo") para abrir e mapear o container LUKS.

#### Formate o dispositivo mapeado

Formate o dispositivo mapeado como descrito em [Btrfs#File system on a single device](/index.php/Btrfs#File_system_on_a_single_device "Btrfs"), onde `*/dev/partition*` é o nome do dispositivo mapeado (i.e., `cryptraiz`) e **não** `/dev/sda2`.

#### Monte o dispositivo mapeado

Finalmente, [monte](/index.php/Mount "Mount") o agora formatado dispositivo mapeado (i.e., `/dev/mapper/cryptraiz`) para `/mnt`.

**Dica:** You pode querer usar a opção de montagem `compress=lzo`. Veja [Btrfs#Compression](/index.php/Btrfs#Compression "Btrfs") para mais informações.

### Criando subvolumes do btrfs

#### Esboço

[Subvolumes](/index.php/Btrfs#Subvolumes "Btrfs") serão usados como partições simuladas, mas outros subvolumes (aninhados) serão criados. A seguir uma representação parcial do que este seguinte exemplo vai gerar:

```
subvolid=5 (/dev/sda2)
   |
   ├── @ (montado como /)
   |       |
   |       ├── /bin (diretório)
   |       |
   |       ├── /home (subvolume @home montado)
   |       |
   |       ├── /usr (diretório)
   |       |
   |       ├── /.snapshots (subvolume @snapshots montado)
   |       |
   |       ├── /var/cache/pacman/pkg (subvolume aninhado)
   |       |
   |       ├── ... (outros diretórios e subvolumes aninhados)
   |
   ├── @snapshots (montado como /.snapshots)
   |
   ├── @home (montado como /home)
   |
   └── @... (subvolumes adicionais que você deseja usar como ponto de montagem)

```

Este seção segue [Snapper#Suggested filesystem layout](/index.php/Snapper#Suggested_filesystem_layout "Snapper") que é mais útil quando usado com o [snapper](/index.php/Snapper "Snapper"). Você também deveria consultar [Btrfs Wiki SysadminGuide#Layout](https://btrfs.wiki.kernel.org/index.php/SysadminGuide#Layout).

#### Crie os subvolumes de nível superior

Será utilizada a convenção do prefixo `@` para os nomes do subvolume que serão usados como ponto de montagem, e`@` será o subvolume montado como `/`.

Seguindo o artigo [Btrfs#Creating a subvolume](/index.php/Btrfs#Creating_a_subvolume "Btrfs"), crie os subvolumes em `/mnt/@`, `/mnt/@snapshots`, e `/mnt/@home`.

Crie qualquer subvolume adicional que desejar como ponto de montagem.

#### Monte os subvolumes de nível superior

Desmonte a partição do sistema em `/mnt`.

Agora monte os subvolumes `@` que irão servir como `/` para `/mnt` usando a opção de montagem `subvol=`. Assumindo que o nome do dispositivo mapeado é `cryptraiz`, o comando deve se parecer com:

```
# mount -o compress=lzo,subvol=@ /dev/mapper/cryptraiz /mnt

```

Veja [Btrfs#Mounting subvolumes](/index.php/Btrfs#Mounting_subvolumes "Btrfs") para mais detalhes.

Também monte outros subvolumes para seus respectivos pontos de montagem: `@home` para `/mnt/home` e `@snapshots` para `/mnt/.snapshots`.

#### Crie os subvolumes aninhados

Crie quaisquer subvolumes que você *não* deseja ter snapshots quando tirar uma snapshot do `/`. Por exemplo, você provavelmente não quer tirar snapshots do `/var/cache/pacman/pkg`. estes subvolumes serão aninhados dentro do subvolume `@`, mas facilmente você conseguiria criar no mesmo nível do `@` se for de acordo com sua preferência.

Desde que o subvolume `@` está montado em `/mnt` será necessário [criar um subvolume](/index.php/Create_a_subvolume "Create a subvolume") em `/mnt/var/cache/pacman/pkg` para este exemplo. você pode ser necessário criar diretórios anteriores ao *pkg*.

Outros diretórios que você pode desejar fazer isso são `/var/abs`, `/var/tmp`, e `/srv`.

#### Monte a ESP

Se preparou uma partição de sistema EFI anteriormente, crie seu ponto de montagem e monte-a.

**Nota:** As snapshots do btrfs não irão incluir o `/efi`, desde que este não faz parte de um sistema de arquivos btrfs.

No passo da instalação com o [pacstrap](/index.php/Installation_guide#Install_essential_packages "Installation guide"), [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) deve ser instalado em adição com o [metapacote](/index.php/Metapacote "Metapacote") [base](https://www.archlinux.org/packages/?name=base).

### Configurando o mkinitcpio

#### Crie a keyfile

Para o GRUB abrir a partição LUKS sem que o usuário digite a senha duas vezes, coloque uma keyfile no initramfs. Siga [dm-crypt/Encriptação de dispositivo#Com uma keyfile no initramfs](/index.php/Dm-crypt/Encripta%C3%A7%C3%A3o_de_dispositivo#Com_uma_keyfile_no_initramfs "Dm-crypt/Encriptação de dispositivo"), tenha certeza de adicionar a chave para `/dev/sda2` do passo *luksAddKey*.

#### Edite o mkinitcpio.conf

Depois de criar, adicionar e colocar a chave como descrito acima, adicione o hook `encrypt` no [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf") e também outros hooks que precise. Veja [dm-crypt/Configuração do sistema#mkinitcpio](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema#mkinitcpio "Dm-crypt/Configuração do sistema") para informações detalhadas.

**Dica:** Você pode querer adicionar `BINARIES=(/usr/bin/btrfs)` para sua `mkinitcpio.conf`. Veja o artigo [Btrfs#Corruption recovery](/index.php/Btrfs#Corruption_recovery "Btrfs").

### Configurando o gerenciador de boot

Instale o [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)") em `/dev/sda`. Então, edite `/etc/default/grub` como sugerido em [GRUB#Argumentos adicionais](/index.php/GRUB_(Portugu%C3%AAs)#Argumentos_adicionais "GRUB (Português)") e [GRUB#/boot criptografado](/index.php/GRUB_(Portugu%C3%AAs)#/boot_criptografado "GRUB (Português)"), siga ambas as instruções para o sistema criptografado e a partição de boot. Depois, gere o arquivo de configuração do GRUB.

### Configurando a swap

Se você criou uma partição para ser usada como swap criptografada, siga as instruções em [dm-crypt/Swap criptografada](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption") para configurá-la.