**Status de tradução:** Esse artigo é uma tradução de [dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption"). Data da última tradução: 2020-01-19\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Dm-crypt/Swap_encryption&diff=0&oldid=595522) na versão em inglês.

Dependendo da necessidade, diferentes métodos podem ser usados para criptografar a partição [swap](/index.php/Swap_(Portugu%C3%AAs) "Swap (Português)"). Uma configuração onde a partição swap é criptografada na inicialização oferece maior proteção dos dados, devido a evitar uma situação onde fragmentos de arquivos sensíveis colocados lá, e que não foram sobrescrevidos, estejam alcançáveis. No entanto, criptografar a swap em cada inicialização impossibilita a supensão para o disco.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Sem suporte a suspender para o disco](#Sem_suporte_a_suspender_para_o_disco)
    *   [1.1 UUID e LABEL](#UUID_e_LABEL)
*   [2 Com suporte a suspender para o disco](#Com_suporte_a_suspender_para_o_disco)
    *   [2.1 LVM dentro do LUKS](#LVM_dentro_do_LUKS)
    *   [2.2 Usando uma partição swap](#Usando_uma_partição_swap)
        *   [2.2.1 Hook do mkinitcpio](#Hook_do_mkinitcpio)
    *   [2.3 Usando um arquivo swap](#Usando_um_arquivo_swap)
*   [3 Problemas conhecidos](#Problemas_conhecidos)

## Sem suporte a suspender para o disco

Em sistemas onde suspender para o disco (hibernação) não é desejado, `/etc/crypttab` pode ser usado para abrir a partição swap com uma senha randômica com o modo plain do dm-crypt no tempo de inicialização. Ao desligar o sistema, a senha aleartória é descartada, fazendo os dados criptografados inacessíveis.

Para habilitar esta funcionalidade, simplesmente descomente a linha que começa com `swap` no `/etc/crypttab`. Mude o parâmetro `<dispositivo>` para seu dispositivo swap. Por exemplo, deve parecer com:

 `/etc/crypttab` 
```
# <name>  <device>    <password>     <options>
swap      /dev/sd*X#*   /dev/urandom   swap,cipher=aes-xts-plain64,size=256
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
# <name>  <device>                                                         <password>     <options>
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
# <name> <device>             <password>    <options>
swap     LABEL=*cryptswap*      /dev/urandom  swap,offset=2048,cipher=aes-xts-plain64,size=512
```

Observe o *offset*: são 2048 setores de 512 bytes, então 1 MiB. Desta maneira a swap criptografada não vai afetar o LABEL/UUID do sistema de arquivos, e o alinhamento de dados vai funcionar também.

 `/etc/fstab` 
```
# <filesystem>     <dir>  <type>  <options>  <dump>  <pass>
/dev/mapper/swap   none   swap    defaults   0       0
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

#### Hook do mkinitcpio

**Nota:** Esta seção é somente aplicável quando usar o hook `encrypt`, que pode abrir somente um dispositivo ([FS#23182](https://bugs.archlinux.org/task/23182)). Com o hook `sd-encrypt` múltiplos dispositivos podem ser abertos, veja [dm-crypt/Configuração do sistema#Usando o hook sd-encrypt](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema#Usando_o_hook_sd-encrypt "Dm-crypt/Configuração do sistema").

Se o swap está em um dispositivo diferente do sistema de arquivos da partição raiz, este não vai ser aberto pelo hook `encrypt`, o *resume* vai tomar lugar antes que o `/etc/crypttab` seja lido, por isso é necessário criar um hook e colocá-lo em `/etc/mkinitcpio.conf` para abrir o dispositivo swap criptografado com LUKS antes dessa situação.

Se você deseja usar a partição que é atualmente usada pelo sistema, você vai ter que desativá-la primeiro:

```
# swapoff /dev/<dispositivo>

```

Tenha certeza de remover qualquer linha em `/etc/crypttab` apontando para este dispositivo.

Se você está usando uma [partição](/index.php/Parti%C3%A7%C3%A3o "Partição") swap existente, e esta está numa tabela de partição GPT, você vai precisar usar o [gdisk](/index.php/Gdisk "Gdisk") para definir o [atributo de partição 63 "do not automount"](/index.php/Gdisk#Prevent_GPT_partition_automounting "Gdisk") ("não monte automaticamente") nela. Isto vai prevenir o systemd-gpt-auto-generator de descobrir e habilitar a partição na inicialização.

A seguinte configuração tem a desvantagem de inserir manualmente uma senha adicional para a partição swap toda vez que ligar o sistema.

**Atenção:** Não use esta configuração com uma keyfile se `/boot` não está criptografado. Leia sobre o problema reportado [aqui](https://wiki.archlinux.org/index.php?title=Talk:Dm-crypt&oldid=255742#Suspend_to_disk_instructions_are_insecure) (em inglês). Alternativamente, use uma keyfile criptografada com gnupg, de acordo com [esta página no forum](https://bbs.archlinux.org/viewtopic.php?id=120181isto) (em inglês).

Formate o container criptografado para a partição swap, crie um espaço de chave para uma senha memorizável.

```
# cryptsetup luksFormat /dev/<dispositivo>

```

Abra a partição em `/dev/mapper`:

```
# cryptsetup open /dev/<dispositivo> dispositivoSwap

```

Crie o sistema de arquivos para a swap dentro da partição mapeada:

```
# mkswap /dev/mapper/dispositivoSwap

```

Agora faça um hook para abrir a swap na inicialização. Você pode [instalar](/index.php/Instala "Instala") e configurar o [mkinitcpio-openswap](https://aur.archlinux.org/packages/mkinitcpio-openswap/), ou seguir as seguintes instruções. Crie um arquivo contendo o seguinte comando de abertura:

 `/etc/initcpio/hooks/openswap` 
```
run_hook ()
{
    cryptsetup open /dev/<dispositivo> dispositivoSwap
}

```

**Atenção:** Montar o sistema de arquivos [é perigoso e destrutivo](https://www.kernel.org/doc/Documentation/power/swsusp.txt). A keyfile não deve ser lida de um sistema de arquivos que estava montado quando o sistema foi suspenso.

Para abrir o dispositivo swap ao digitar a senha ou

 `/etc/initcpio/hooks/openswap` 
```
run_hook ()
{
    ## opcional: Para evitar condição de corrida
    x=0;
    while [ ! -b /dev/mapper/<dispositivo-raiz> ] && [ $x -le 10 ]; do
       x=$((x+1))
       sleep .2
    done
    ## Fim do opcional

    mkdir dispositivo_da_chave
    mount /dev/mapper/<dispositivo-raiz> dispositivo_da_chave
    cryptsetup open --key-file dispositivo_da_chave/<caminho-para-a-chave> /dev/<dispositivo> dispositivoSwap
    umount dispositivo_da_chave
}

```

Para abrir o dispositivo swap com uma keyfile do dispositivo raiz criptografado.

Em alguns computadores, condições de corrida podem ocorrer quando o mkinitcpio tenta montar o dispositivo antes dele ser aberto e a enumeração de dispositivos ainda está incompleta. O bloco *opcional* vai atrasar o processo de inicialização em 2 segundos até que o dispositivo raiz esteja pronto para ser montado.

**Nota:** Se a swap está em um SSD e Discard/TRIM é desejado, a opção `--allow-discards` precisa ser adicionada para a linha do cryptsetup no hook openswap acima. Veja [Dm-crypt/Especificidades#Suporte a discard/TRIM para unidades de estado sólido (SSD)](/index.php/Dm-crypt/Especificidades#Suporte_a_discard/TRIM_para_unidades_de_estado_sólido_(SSD) "Dm-crypt/Especificidades") ou [SSD](/index.php/SSD "SSD") para mais informações sobre discard. Também adicione a opção de montagem 'discard' para a entrada do dispositivo swap no fstab.

Crie e edite o arquivo de configuração do hook:

 `/etc/initcpio/install/openswap` 
```
build ()
{
   add_runscript
}
help ()
{
cat<<HELPEOF
  Isto abre a partição swap criptografada /dev/<dispositivo> em /dev/mapper/dispositivoSwap
HELPEOF
}

```

Adicione o hook `openswap` no arranjo `HOOKS` no `/etc/mkinitcpio.conf`, entre `encrypt` e `filesystems`. Não se esqueça de adicionar o hook `resume` depois de `openswap`

```
HOOKS=(... encrypt openswap resume filesystems ...)

```

[Gere novamente o initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").

Coloque a partição mapeada no `/etc/fstab` ao adicionar a seguinte linha:

```
/dev/mapper/dispositivoSwap swap swap defaults 0 0

```

Configure seu sistema para resumir com o `/dev/mapper/dispositivoSwap`. Por exemplo, se você usa [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)") com suporte a hibernação do kernel, adicione o parâmetro do kernel `resume=/dev/mapper/dispositivoSwap` na variável `GRUB_CMDLINE_LINUX_DEFAULT` em `/etc/default/grub`. Uma linha do kernel com a raiz e swap criptografada pode parecer com isso:

```
kernel /vmlinuz-linux cryptdevice=/dev/sda2:raiz root=/dev/mapper/raiz resume=/dev/mapper/dispositivoSwap ro

```

Na inicialização, o hook `openswap` vai abrir a partição swap para que o kernel possa usá-la. Se você usar hooks especiais para resumir da hibernação, tenha certeza de que eles estão **depois** do `openswap` no arranjo `HOOKS`. Note que devido ao initrd abrir a swap, não é necessário ter uma entrada para *dispositivoSwap* em `/etc/crypttab`.

### Usando um arquivo swap

Um arquivo swap pode ser usado para reservar um espaço swap dentro de uma partição existente e isto também pode ser feito dentro de uma partição criptografada.

Siga as instruções para criação do arquivo swap em [Swap#Arquivo swap](/index.php/Swap_(Portugu%C3%AAs)#Arquivo_swap "Swap (Português)") e configure a hibernação de acordo com [Power management/Suspend and hibernate#Hibernation into swap file](/index.php/Power_management/Suspend_and_hibernate#Hibernation_into_swap_file "Power management/Suspend and hibernate").

**Nota:** Quando resumir de um arquivo swap, o parâmetro `resume` deve apontar para o dispositivo aberto/mapeado que contém o sistema de arquivos com o arquivo swap.

## Problemas conhecidos

*   `Stopped (with error) /dev/dm-1` nos logs. Veja a [issue do systemd 1620](https://github.com/systemd/systemd/issues/1620).