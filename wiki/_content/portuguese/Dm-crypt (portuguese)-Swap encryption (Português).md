Dependendo da necessidade, diferentes métodos podem ser usados para criptografar a partição [swap](/index.php/Swap_(Portugu%C3%AAs) "Swap (Português)"). Uma configuração onde a partição swap é criptografada na inicialização oferece maior proteção dos dados, devido a evitar uma situação onde fragmentos de arquivos sensíveis colocados lá, e que não foram sobrescrevidos, estejam alcançáveis. No entanto, criptografar a swap em cada inicialização impossibilita a supensão para o disco.

**Nota:** Os termos comentados no arquivo `/etc/crypttab`, e em outros locais convenientes, foram traduzidos para melhor didádica. No seu sistema estes devem aparecer em inglês.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Sem suporte a suspender para o disco](#Sem_suporte_a_suspender_para_o_disco)
    *   [1.1 UUID e LABEL](#UUID_e_LABEL)
*   [2 Com suporte a suspender para o disco](#Com_suporte_a_suspender_para_o_disco)
    *   [2.1 LVM dentro do LUKS](#LVM_dentro_do_LUKS)
    *   [2.2 Usando uma partição swap](#Usando_uma_partição_swap)
        *   [2.2.1 mkinitcpio hook](#mkinitcpio_hook)
    *   [2.3 Usando um arquivo swap](#Usando_um_arquivo_swap)
*   [3 Problemas conhecidos](#Problemas_conhecidos)

## Sem suporte a suspender para o disco

Em sistemas onde suspender para o disco (hibernação) não é desejado, `/etc/crypttab` pode ser usado para abrir a partição swap com uma senha randômica com o modo plain do dm-crypt no tempo de inicialização. Ao desligar o sistema, a senha aleartória é descartada, fazendo os dados criptografados inacessíveis.

Para habilitar esta funcionalidade, simplesmente descomente a linha que começa com `swap` no `/etc/crypttab`. Mude o parâmetro `<dispositivo>` para seu dispositivo swap. Por exemplo, deve parecer com:

 `/etc/crypttab` 
```
# <nome>  <dispositivo>    <senha>        <opções>
swap      /dev/sd*X#*        /dev/urandom   swap,cipher=aes-xts-plain64,size=256
```

Isto vai mapear `/dev/sd*X#*` para `/dev/mapper/swap` e assim esta pode ser adicionada em `/etc/fstab` como uma swap normal. Se você tinha uma partição swap não criptografada antes, não se esqueça de desabilitá-la - ou reutilizar sua entrada do [fstab](/index.php/Fstab "Fstab") ao mudar o dispositivo para `/dev/mapper/swap`. As opções padrão devem ser o suficiente para a maioria dos usuários. Para outras opções e uma explicação de cada coluna, veja [crypttab(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/crypttab.5) e também [2.3 do FAQ do cryptsetup](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#2-setup).

**Atenção:** Tudo que estiver dentro do dispositivo nomeado vai ser permanentemente **deletado**. É perigoso usar a nomeação simples do kernel para o dispositivo swap, desde que a ordem pode mudar a cada inicialização (*exemplo*, `/dev/sda`, `/dev/sdb`). Opções são:

*   Usar caminhos do `by-id` e `by-path`. No entanto, estes dois são sucetíveis a mudanças no hardware. Veja [nomeação persistente de dispositivo de bloco#by-id e by-path](/index.php/Nomea%C3%A7%C3%A3o_persistente_de_dispositivo_de_bloco#by-id_e_by-path "Nomeação persistente de dispositivo de bloco").
*   Usar um nome do volume lógico do [LVM](/index.php/LVM_(Portugu%C3%AAs) "LVM (Português)").
*   Usar o método descrito em [#UUID e LABEL](#UUID_e_LABEL). Labels e [UUIDS](/index.php/Nomea%C3%A7%C3%A3o_persistente_de_dispositivo_de_bloco#by-uuid "Nomeação persistente de dispositivo de bloco") **não podem** ser usados diretamente devido a criação e encriptação do dispositivo swap a cada inicialização com `mkswap`, veja o [FAQ do cryptsetup](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#2-setup).

**Nota:** A configuração da partição swap pode algumas vezes falhar, veja a [issue do systemd 10179](https://github.com/systemd/systemd/issues/10179).

Para usar o nomeação persistente `by-id`, primeiro identifique o dispositivo swap:

 `# find -L /dev/disk -samefile /dev/*sdX#*` 
```
/dev/disk/by-id/ata-WDC_WD2500BEVT-22ZCT0_WD-WXE908VF0470-part*X*
/dev/disk/by-id/wwn-0x60015ee0000b237f-part*X*

```

Então o use como uma referência persistente para a partição (se dois resultados são retornados como acima, use qualquer um deles):

 `/etc/crypttab` 
```
# <nome>  <dispositivo>                                                    <senha>        <opções>
swap      /dev/disk/by-id/ata-WDC_WD2500BEVT-22ZCT0_WD-WXE908VF0470-partX  /dev/urandom   swap,cipher=aes-cbc-essiv:sha256,size=256
```

Depois de inicializar para ativar a swap criptografada, você vai notar que ao rodar `swapon -s` vai ser mostrado uma entrada arbitária para o dispositivo mapeado (exemplo, `/dev/dm-1`), enquanto o comando `lsblk` mostra **crypt** na coluna `FSTYPE`. Devido a cada inicialização ser criptografada novamente, o UUID de `/dev/mapper/swap` vai mudar toda vez.

**Nota:** Se a partição escolhida para swap foi antes uma partição LUKS, crypttab não vai sobrescrever esta partição. Isto é uma medida de segurança para prevenir perda de dados por acidental má-identificação da partição swap no crypttab. Para usar a partição o [cabeçalho do LUKS deve ser sobrescrito](/index.php/Dm-crypt/Preparando_a_unidade_de_armazenamento#Apagar_o_cabeçalho_do_LUKS "Dm-crypt/Preparando a unidade de armazenamento") uma vez.

### UUID e LABEL

É perigoso usar a nomeação simples de dispositivos do kernel, como `/dev/sdX#` e `/dev/disk/by-id/ata-SERIAL-partX`, para criptografar a swap com o crypttab. Uma pequena mudança no nome dos dispositivos ou particionamento pode acarretar na perda de seus dados na próxima inicialização. O mesmo se você usar o PARTUUID e então usar esta partição para alguma outra coisa e se esquecer de remover a respectiva entrada do crypttab.

É mais confiável identificar a partição correta ao dar um genuíno UUID ou LABEL. Por padrão isto não funciona devido ao dm-crypt e `mkswap` sobrescreverem qualquer coisa presente na partição, incluindo o UUID e LABEL. No entanto é possível especificar o início (offset) da swap. Isto permite criar um minúsculo e vazio sistema de arquivos com o objetivo de prover um UUID ou LABEL persistente para a encriptação da swap.

Crie um [sistema de arquivos](/index.php/Sistema_de_arquivos "Sistema de arquivos"), com uma LABEL de sua escolha:

```
# mkfs.ext2 -L *cryptswap* /dev/sd*X#* 1M

```

O parâmetro não usual depois do nome do dispositivo limita o tamanho do sistema de arquivos para 1 MiB, deixando espaço para a swap criptografada.

 `# blkid /dev/sdX#`  `/dev/sdX#: LABEL="cryptswap" UUID="b72c384e-bd3c-49aa-b7a7-a28ea81a2605" TYPE="ext2"` 

Com isso, `/dev/sdX#` agora pode facilmente ser identificada por ambos UUID ou LABEL, independente do nome do dispositivo ou até mesmo o número da partição que podem mudar no futuro. Modifique as entradas do `/etc/crypttab` e `/etc/fstab`:

 `/etc/crypttab` 
```
# <nome> <dispositivo>        <senha>       <opções>
swap     LABEL=*cryptswap*      /dev/urandom  swap,offset=2048,cipher=aes-xts-plain64,size=512
```

Observe o *offset*: são 2048 setores de 512 bytes, então 1 MiB. Desta maneira a swap criptografada não vai afetar o LABEL/UUID do sistema de arquivos, e o alinhamento de dados vai funcionar também.

 `/etc/fstab` 
```
# <sistema de arquivos>    <diretório>  <tipo>  <opções>  <dump>  <pass>
/dev/mapper/swap           none         swap    defaults   0       0
```

Ao usar esta configuração, o *cryptswap* vai somente usar a partição com o LABEL correspondente, independente do que o nome do dispositivo pode ser. Se você decidir formatar e usar a partição para outra coisa, o LABEL vai ser perdido, logo, na próxima inicialização nada deve ser sobrescrito.

## Com suporte a suspender para o disco

Para resumir depois de suspender o computador para o disco (hibernar), é necessário manter o espaço swap intacto. Por isso, tenha uma partição ou arquivo swap criptografada com LUKS, que pode ser guardada no disco ou colocada na inicialização.

Os três seguintes métodos são alternativas que possibilitam suspender para o disco. Se você aplicar qualquer uma delas, entenda que dados críticos podem ter sido colocados na swap e potencialmente permanecer por um longo período de tempo (até que sejam sobrescritos). Para reduzir o risco, considere montar um sistema que criptografa a swap novamente, por exemplo, a cada vez que o sistema é desligado normalmente, junto com o método de sua escolha.

### LVM dentro do LUKS

Se o swap está no grupo de volumes lógicos que é ativado no initramfs, simplesmente siga as instruções em [Power management/Suspend and hibernate#Hibernation](/index.php/Power_management/Suspend_and_hibernate#Hibernation "Power management/Suspend and hibernate").

### Usando uma partição swap

Para resumir de uma partição swap criptografada, esta deve ser aberta durante o initramfs.

*   Quando usar o initramfs padrão baseado no busybox com o hook [encrypt](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema#Usando_o_hook_encrypt "Dm-crypt/Configuração do sistema"), siga as instruções em [#Hook do mkinitcpio](#Hook_do_mkinitcpio).
*   Quando usar o initramfs baseado no systemd com o hook [sd-encrypt](/index.php/Sd-encrypt_(Portugu%C3%AAs) "Sd-encrypt (Português)"), adicione os parâmetros adicionais do `rd.luks` para abrir a partição swap.

#### mkinitcpio hook

**Note:** This section is only applicable when using the `encrypt` hook, which can only unlock a single device ([FS#23182](https://bugs.archlinux.org/task/23182)). With `sd-encrypt` multiple devices may be unlocked, see [dm-crypt/System configuration#Using sd-encrypt hook](/index.php/Dm-crypt/System_configuration#Using_sd-encrypt_hook "Dm-crypt/System configuration").

If the swap device is on a different device from that of the root file system, it will not be opened by the `encrypt` hook, i.e. the resume will take place before `/etc/crypttab` can be used, therefore it is required to create a hook in `/etc/mkinitcpio.conf` to open the swap LUKS device before resuming.

If you want to use a partition which is currently used by the system, you have to disable it first:

```
# swapoff /dev/<device>

```

Also make sure you remove any line in `/etc/crypttab` pointing to this device.

If you are reusing an existing swap [partition](/index.php/Partition "Partition"), and if the partition is on a GPT partition table, you will need use [gdisk](/index.php/Gdisk "Gdisk") to set the [partition attribute 63 "do not automount"](/index.php/Gdisk#Prevent_GPT_partition_automounting "Gdisk") on it. This will prevent systemd-gpt-auto-generator from discovering and enabling the partition at boot.

The following setup has the disadvantage of having to insert an additional passphrase for the swap partition manually on every boot.

**Warning:** Do not use this setup with a key file if `/boot` is unencrypted. Please read about the issue reported [here](https://wiki.archlinux.org/index.php?title=Talk:Dm-crypt&oldid=255742#Suspend_to_disk_instructions_are_insecure). Alternatively, use a gnupg-encrypted keyfile as per [https://bbs.archlinux.org/viewtopic.php?id=120181](https://bbs.archlinux.org/viewtopic.php?id=120181)

To format the encrypted container for the swap partition, create a keyslot for a user-memorizable passphrase.

```
# cryptsetup luksFormat /dev/<device>

```

Open the partition in `/dev/mapper`:

```
# cryptsetup open /dev/<device> swapDevice

```

Create a swap filesystem inside the mapped partition:

```
# mkswap /dev/mapper/swapDevice

```

Now you have to create a hook to open the swap at boot time. You can either [install](/index.php/Install "Install") and configure [mkinitcpio-openswap](https://aur.archlinux.org/packages/mkinitcpio-openswap/), or follow the following instructions. Create a hook file containing the open command:

 `/etc/initcpio/hooks/openswap` 
```
run_hook ()
{
    cryptsetup open /dev/<device> swapDevice
}

```

**Warning:** Mounting the file system [is dangerous and destructive](https://www.kernel.org/doc/Documentation/power/swsusp.txt). The keyfile should not be read from a file system that was mounted when the system was suspended.

for opening the swap device by typing your password or

 `/etc/initcpio/hooks/openswap` 
```
run_hook ()
{
    ## Optional: To avoid race conditions
    x=0;
    while [ ! -b /dev/mapper/<root-device> ] && [ $x -le 10 ]; do
       x=$((x+1))
       sleep .2
    done
    ## End of optional

    mkdir crypto_key_device
    mount /dev/mapper/<root-device> crypto_key_device
    cryptsetup open --key-file crypto_key_device/<path-to-the-key> /dev/<device> swapDevice
    umount crypto_key_device
}

```

for opening the swap device by loading a keyfile from a crypted root device.

On some computers race conditions may occur when mkinitcpio tries to mount the device before the decryption process and device enumeration is completed. The commented *Optional* block will delay the boot process up to 2 seconds until the root device is ready to mount.

**Note:** If swap is on a Solid State Disk (SSD) and Discard/TRIM is desired the option `--allow-discards` has to get added to the cryptsetup line in the openswap hook above. See [Dm-crypt/Specialties#Discard/TRIM support for solid state drives (SSD)](/index.php/Dm-crypt/Specialties#Discard/TRIM_support_for_solid_state_drives_(SSD) "Dm-crypt/Specialties") or [SSD](/index.php/SSD "SSD") for more information on discard. Additionally you have to add the mount option 'discard' to your fstab entry for the swap device.

Then create and edit the hook setup file:

 `/etc/initcpio/install/openswap` 
```
build ()
{
   add_runscript
}
help ()
{
cat<<HELPEOF
  This opens the swap encrypted partition /dev/<device> in /dev/mapper/swapDevice
HELPEOF
}

```

Add the hook `openswap` in the `HOOKS` array in `/etc/mkinitcpio.conf`, before `filesystem` but after `encrypt`. Do not forget to add the `resume` hook after `openswap`.

```
HOOKS=(... encrypt openswap resume filesystems ...)

```

[Regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").

Add the mapped partition to `/etc/fstab` by adding the following line:

```
/dev/mapper/swapDevice swap swap defaults 0 0

```

Set up your system to resume from `/dev/mapper/swapDevice`. For example, if you use [GRUB](/index.php/GRUB "GRUB") with kernel hibernation support, add the kernel parameter `resume=/dev/mapper/swapDevice` to GRUB by appending it to the `GRUB_CMDLINE_LINUX_DEFAULT` variable in `/etc/default/grub`. A kernel line with encrypted root and swap partitions can look like this:

```
kernel /vmlinuz-linux cryptdevice=/dev/sda2:rootDevice root=/dev/mapper/rootDevice resume=/dev/mapper/swapDevice ro

```

At boot time, the `openswap` hook will open the swap partition so the kernel resume may use it. If you use special hooks for resuming from hibernation, make sure they are placed **after** `openswap` in the `HOOKS` array. Please note that because of initrd opening swap, there is no entry for swapDevice in `/etc/crypttab` needed in this case.

### Usando um arquivo swap

Um arquivo swap pode ser usado para reservar um espaço swap dentro de uma partição existente e isto também pode ser feito dentro de uma partição criptografada.

Siga as instruções para criação do arquivo swap em [Swap#Arquivo swap](/index.php/Swap_(Portugu%C3%AAs)#Arquivo_swap "Swap (Português)") e configure a hibernação de acordo com [Power management/Suspend and hibernate#Hibernation into swap file](/index.php/Power_management/Suspend_and_hibernate#Hibernation_into_swap_file "Power management/Suspend and hibernate").

**Nota:** Quando resumir de um arquivo swap, o parâmetro `resume` deve apontar para o dispositivo aberto/mapeado que contém o sistema de arquivos com o arquivo swap.

## Problemas conhecidos

*   `Stopped (with error) /dev/dm-1` nos logs. Veja a [issue do systemd 1620](https://github.com/systemd/systemd/issues/1620).