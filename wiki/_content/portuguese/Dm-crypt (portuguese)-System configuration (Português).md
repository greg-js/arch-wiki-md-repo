**Status de tradução:** Esse artigo é uma tradução de [Dm-crypt/System configuration](/index.php/Dm-crypt/System_configuration "Dm-crypt/System configuration"). Data da última tradução: 2019-12-03\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Dm-crypt/System_configuration&diff=0&oldid=590453) na versão em inglês.

**Dica:**

*   Se precisa desbloquear remotamente o sistema de arquivos da partição raiz ou de outras partições na inicialização (máquinas sem monitor, servidores distantes...), siga instruções específicas em [dm-crypt/Especificidades#Desbloqueio remoto da partição raiz (ou outra)](/index.php/Dm-crypt/Especificidades#Desbloqueio_remoto_da_partição_raiz_(ou_outra) "Dm-crypt/Especificidades").
*   Você pode querer instalar e usar [GNU Screen](/index.php/GNU_Screen "GNU Screen") depois de entrar no ambiente chroot para copiar e colar UUIDs mais facilmente.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 mkinitcpio](#mkinitcpio)
    *   [1.1 Exemplos](#Exemplos)
*   [2 Gerenciador de boot](#Gerenciador_de_boot)
    *   [2.1 Parâmetros do Kernel](#Parâmetros_do_Kernel)
        *   [2.1.1 root](#root)
        *   [2.1.2 resume](#resume)
    *   [2.2 Usando o hook encrypt](#Usando_o_hook_encrypt)
        *   [2.2.1 cryptdevice](#cryptdevice)
        *   [2.2.2 cryptkey](#cryptkey)
        *   [2.2.3 crypto](#crypto)
    *   [2.3 Usando o hook sd-encrypt](#Usando_o_hook_sd-encrypt)
        *   [2.3.1 rd.luks.uuid](#rd.luks.uuid)
        *   [2.3.2 rd.luks.name](#rd.luks.name)
        *   [2.3.3 rd.luks.options](#rd.luks.options)
        *   [2.3.4 rd.luks.key](#rd.luks.key)
        *   [2.3.5 Timeout](#Timeout)
*   [3 crypttab](#crypttab)
    *   [3.1 Montando na inicialização](#Montando_na_inicialização)
        *   [3.1.1 Desbloqueando com uma keyfile](#Desbloqueando_com_uma_keyfile)
        *   [3.1.2 Montando um dispositivo de bloco empilhado](#Montando_um_dispositivo_de_bloco_empilhado)
    *   [3.2 Montando em demanda](#Montando_em_demanda)
*   [4 Solução de problemas](#Solução_de_problemas)
    *   [4.1 Sistema travado no prompt de inicialização/senha não aparece](#Sistema_travado_no_prompt_de_inicialização/senha_não_aparece)

## mkinitcpio

Em alguns cenários, um subconjunto dos seguintes hooks do [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") terão que ser habilitados:

| busybox | systemd | Caso de uso |
| `encrypt` | `sd-encrypt` | Sempre necessário quando a partição raiz, ou outra partição que precisa ser montada *antes* dela, é criptografada. Não é necessário em todos os casos, scripts de inicialização de sistema como `crypttab` cuidam do desbloqueio de outras partições criptografadas. Deve ser colocado depois do hook `udev` ou `systemd`. |
| `keyboard` | Necessário para o funcionamento do teclado no estágio inicial do espaço do usuário. |
| `keymap` | `sd-vconsole` | Trás suporte a teclados que não são do padrão US; deve ser colocado *antes* do hook `encrypt`. Defina seu padrão do seu teclado em `/etc/vconsole.conf`, veja [Configuração de teclado no console#Configuração persistente](/index.php/Configura%C3%A7%C3%A3o_de_teclado_no_console#Configuração_persistente "Configuração de teclado no console"). |
| `consolefont` | Carrega uma fonte alternativa para o console no estágio inicial do espaço do usuário. Defina sua fonte em `/etc/vconsole.conf`, veja [Console do Linux#Configuração persistente](/index.php/Console_do_Linux#Configuração_persistente "Console do Linux"). |

[Outros hooks](/index.php/Mkinitcpio#Common_hooks "Mkinitcpio") necessários devem ser claramente especificados durante a instalação do sistema.

Se lembre de [gerar novamente o initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs") depois de salvar as mudanças.

### Exemplos

Uma configuração típica em `/etc/mkinitcpio.conf` quando se usa o hook `encrypt` é:

 `/etc/mkinitcpio.conf` 
```
...
HOOKS=(base udev autodetect keyboard keymap consolefont modconf block encrypt lvm2 filesystems fsck)
...
```

Já uma configuração com o initramfs baseado no systemd, fazendo uso do hook `sd-encrypt`, seria semelhante a:

 `/etc/mkinitcpio.conf` 
```
...
HOOKS=(base systemd autodetect keyboard sd-vconsole modconf block sd-encrypt sd-lvm2 filesystems fsck)
...
```

## Gerenciador de boot

Para habilitar a inicialização em uma partição raiz criptografada, um subconjunto dos seguintes parâmetros do kernel terão que ser configurados. Veja [Parâmetros do kernel](/index.php/Par%C3%A2metros_do_kernel "Parâmetros do kernel") para instruções específicas para seu [Gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot").

Por exemplo, se está usando o [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)"), os parâmetros relevantes são adicionados no `/etc/default/grub`, antes de [gerar o arquivo de configuração principal](/index.php/GRUB_(Portugu%C3%AAs)#Gerar_o_arquivo_de_configuração_principal "GRUB (Português)"). Veja também [GRUB#Aviso ao instalar em chroot](/index.php/GRUB_(Portugu%C3%AAs)#Aviso_ao_instalar_em_chroot "GRUB (Português)") como outro ponto a se atentar.

Os parâmetros do kernel irão variar de acordo com qual hook (`encrypt` ou `sd-encrypt`) você vai usar.

### Parâmetros do Kernel

[Parâmetros do kernel](/index.php/Par%C3%A2metros_do_kernel "Parâmetros do kernel") como `root` e `resume` são especificados da mesma forma para os hooks `encrypt` e `sd-encrypt`.

#### root

O parâmetro `root=` especifica o `*dispositivo*` do sistema de arquivos raiz (descriptografado):

```
root=*dispositivo*

```

*   Se o sistema de arquivos foi colocado diretamente no dispositivo descriptografado, o caminho será `/dev/mapper/*dmnome*`.
*   Se LVM vai ser ativado primeiro e contém um [volume lógico raiz criptografado](/index.php/Volume_l%C3%B3gico_raiz_criptografado "Volume lógico raiz criptografado"), a forma acima também é aplicável.
*   Se o sistema de arquivos raiz está no volume lógico de uma [LVM criptografada](/index.php/LVM_criptografada "LVM criptografada"), o mapeador de dispositivos vai estar em sua forma genérica `root=/dev/*grupoDoVolume*/*volumeLógico*`.

**Dica:** Se usa o [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)") e está gerando o arquivo `grub.cfg` com *grub-mkconfig*, este parâmetro não precisa se especificado manualmente. *grub-mkconfig* determinará o UUID correto do sistema de arquivos raiz e automaticamente vai colocá-lo no `grub.cfg`.

#### resume

```
resume=*dispositivo*

```

*   `*dispositivo*` nesse caso é a swap decriptografada, este parâmetro é utilizado com o objetivo de [suspender para o disco](/index.php/Power_management/Suspend_and_hibernate#Hibernation "Power management/Suspend and hibernate"). Se a swap está em uma partição separada, ela estará na forma de `/dev/mapper/partição_swap`. Veja também [dm-crypt/Swap criptografada](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption").

### Usando o hook encrypt

**Nota:** Comparado com o hook [sd-encrypt](/index.php/Sd-encrypt "Sd-encrypt"), o hook `encrypt` tem algumas limitações. não suporta:

*   Abrir [múltiplos discos criptografados](/index.php/Dm-crypt/Especificidades#O_hook_encrypt_e_múltiplos_discos "Dm-crypt/Especificidades") ([FS#23182](https://bugs.archlinux.org/task/23182)). Somente **um** dispositivo pode ser aberto no initramfs.
*   Usar um [cabeçalho LUKS desanexado](/index.php/Dm-crypt/Especificidades#Sistema_criptografado_usando_um_cabeçalho_LUKS_desanexado "Dm-crypt/Especificidades") ([FS#42851](https://bugs.archlinux.org/task/42851)).

#### cryptdevice

Este parâmetro fará o sistema solicitar a senha para abrir o dispositivo contendo a raiz criptografada na primeira inicialização (cold boot). Ele é utilizado para o hook `encrypt` identificar o dispositivo que contém o sistema criptografado:

```
cryptdevice=*dispositivo*:*nomedm*

```

*   `*dispositivo*` é o caminho para o container criptografado que contém o sistema. É recomendado o uso da [Nomeação persistente de dispositivo de bloco](/index.php/Nomea%C3%A7%C3%A3o_persistente_de_dispositivo_de_bloco "Nomeação persistente de dispositivo de bloco").
*   `*nomedm*` é o nome do **d**ispositivo **m**apeado que será dado ao container descriptografado, que estará disponível como `/dev/mapper/nomedm`.
*   Se possui um [volume lógico raiz criptografado](/index.php/Volume_l%C3%B3gico_raiz_criptografado "Volume lógico raiz criptografado"), LVM vai ser ativado primeiro, o grupo de volumes e o volume lógico raiz serão o *dispositivo*. Coloque da seguinte forma `cryptdevice=*/dev/grupo_de_volumes/volume_lógico_raiz*:*nomedm*`.

**Dica:** Você pode querer [habilitar suporte ao Discard/TRIM](/index.php/Dm-crypt/Especificidades#Suporte_a_discard/TRIM_para_unidades_de_estado_sólido_(SSD) "Dm-crypt/Especificidades") para unidades de estado sólido (SSD).

#### cryptkey

Este parâmetro especifica a localização de uma keyfile e é necessário o hook `*encrypt*` para ler e abrir o `*cryptdevice*` (a menos que a chave está em um caminho padrão, veja abaixo). Três parâmetros podem ser definidos, dependendo de como a keyfile existe, pode ser um arquivo no dispositivo, uma bitstream que começa em uma localização específica ou um arquivo incluido no initramfs.

Para um arquivo no dispositivo o formato é:

```
cryptkey=*dispositivo*:*tipo_do_sistema_de_arquivos*:*caminho*

```

*   `*dispositivo*` é o dispositivo de bloco onde a keyfile se encontra.
*   `*tipo_do_sistema_de_arquivos*` é o tipo do sistema de arquivos do `*dispositivo*` (ou auto).
*   `*caminho*` é o caminho absoluto da keyfile dentro do dispositivo.

Exemplo: `cryptkey=/dev/sdb1:vfat:/chave_secreta`

Para uma bitstream no dispositivo, a localização é especificada com:

```
cryptkey=*dispositivo*:*início*:*tamanho* 

```

Onde início e tamanho estão em bytes. Exemplo: `cryptkey=/dev/sdZ:0:512` lê uma keyfile de 512 byte no começo do dispositivo.

**Dica:** Se o caminho do dispositivo que você quer acessar contém o caracter `:`, terá que escapar isto com `\`. Neste caso o parâmetro cryptkey deve ser semelhante a: `cryptkey=/dev/disk/by-id/usb-123456-0\:0:0:512`, este exemplo é de um pendrive com o id `usb-123456-0:0`.

Para um arquivo [incluído](/index.php/Mkinitcpio#BINARIES_and_FILES "Mkinitcpio") no initramfs o formato é:[[1]](https://git.archlinux.org/svntogit/packages.git/tree/trunk/hooks-encrypt?h=packages/cryptsetup#n14)

```
cryptkey=rootfs:*caminho*

```

Exemplo: `cryptkey=rootfs:/chave_secreta`

Também note que se `cryptkey` não é especificada, o padrão `/crypto_keyfile.bin` (arquivo incluído no initramfs) será utilizado.[[2]](https://git.archlinux.org/svntogit/packages.git/tree/trunk/hooks-encrypt?h=packages/cryptsetup#n8)

Veja também [dm-crypt/Encriptação de dispositivo#Keyfiles](/index.php/Dm-crypt/Encripta%C3%A7%C3%A3o_de_dispositivo#Keyfiles "Dm-crypt/Encriptação de dispositivo").

#### crypto

Este parâmetro é especifíco para passar opções do modo plain do *dm-crypt* para o hook *encrypt*.

Sua forma é:

```
crypto=<hash>:<cifra>:<tamanho_da_chave>:<início>:<pule>

```

Os argumentos são relacionados diretamente a opções do *cryptsetup*. Veja [dm-crypt/Encriptação de dispositivo#Opções de encriptação para o modo plain](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_plain_mode "Dm-crypt/Device encryption").

Para um disco criptografado com somente as opções padrão do modo *plain*, o argumento `crypto` deve ser especificado, mas cada entrada pode ser vazia:

```
crypto=::::

```

Um exemplo especifíco é:

```
crypto=sha512:twofish-xts-plain64:512:0:

```

### Usando o hook sd-encrypt

Todos os seguintes `rd.luks` podem ser trocados por `luks`. Os parâmetros `rd.luks` são somente reconhecidos pelo initrd, enquanto `luks` são reconhecidos tanto pelo sistema quanto pelo initrd. A menos que você queira controlar os dispositivos com argumentos dados ao kernel enquanto o sistema é inicializado, use `rd.luks`. Veja [systemd-cryptsetup-generator(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-cryptsetup-generator.8) para mais informações e detalhes.

**Dica:**

*   Se o arquivo `/etc/crypttab.initramfs` existe, [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") o adicionará ao initramfs como `/etc/crypttab`, você pode especificar nele dispositivos que precisam ser desbloqueados durante a inicialização. Sintaxe é documentada em [#crypttab](#crypttab) e [crypttab(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/crypttab.5).
*   `/etc/crypttab.initramfs` não é limitado somente ao uso do UUID como o `rd.luks`. Você pode usar qualquer um dos [métodos de nomeação persistente de dispositivo de bloco](/index.php/Persistent_block_device_naming#Persistent_naming_methods "Persistent block device naming").

**Nota:**

*   Se você entrou no shell de emergência durante a inicialização com a versão 239.300-2 ou superior do systemd, veja [FS#60907](https://bugs.archlinux.org/task/60907).
*   Todos os parâmetros do `rd.luks` podem ser especificados múltiplas vezes para múltiplos volumes criptografados LUKS.
*   Os parâmetros do `rd.luks` somente suportam dispositivos LUKS detectáveis. Para abrir um dispositivo dm-crypt plain ou com cabeçalho do LUKS desanexado, você deve especificá-lo em `/etc/crypttab.initramfs`. Veja [#crypttab](#crypttab) para a sintaxe.

**Atenção:** Se você está usando o `/etc/crypttab` ou `/etc/crypttab.initramfs` junto com os parâmetros `luks.*` ou `rd.luks.*`, somente os dispositivos especificados na linha de comando do kernel serão ativados e você verá `Not creating device 'devicename' because it was not specified on the kernel command line.`. Para ativar todos os dispositivos em `/etc/crypttab` não especifique nenhum parâmetro `luks.*` e use `rd.luks.*`. Para ativar todos os dispositivos em `/etc/crypttab.initramfs` não especifique nenhum parâmetro `luks.*` or `rd.luks.*`.

#### rd.luks.uuid

**Dica:** `rd.luks.uuid` pode ser omitido ao usar `rd.luks.name`.

```
rd.luks.uuid=*XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX*

```

Especifique o [UUID](/index.php/Persistent_block_device_naming_(Portugu%C3%AAs)#by-uuid "Persistent block device naming (Português)") do dispositivo a ser aberto na inicialização com este parâmetro. Se o UUID está em `/etc/crypttab.initramfs`, as opções listadas lá serão utilizadas. Para opções do `luks.uuid`, o `/etc/crypttab.initramfs` ou `/etc/crypttab` será usado.

Por padrão o dispositivo mapeado estará localizado en `/dev/mapper/luks-*XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX*` onde *XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX* é o UUID da partição LUKS.

#### rd.luks.name

**Dica:** Ao usar este parâmetro, você pode omitir `rd.luks.uuid`.

```
rd.luks.name=*XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX*=*nome*

```

Especifique o nome do dispositivo mapeado depois que a partição LUKS é aberta, onde *XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX* é o UUID dela. É equivalente ao segundo parâmetro do `encrypt`, `cryptdevice`.

Exemplo, especificar `rd.luks.name=12345678-9ABC-DEF0-1234-56789ABCDEF0=cryptraiz` faz o dispositivo LUKS aberto do UUID `12345678-9ABC-DEF0-1234-56789ABCDEF0` estar localizado em `/dev/mapper/cryptroot`.

#### rd.luks.options

```
rd.luks.options=*XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX*=*opções*

```

ou

```
rd.luks.options=*opções*

```

Defina as opções para um dispositivo especificado com o UUID ou, se não especificado, para todos os UUIDs especificados em outro lugar (e.g., crypttab).

É relativamente equivalente ao terceiro parâmetro do `encrypt`, `cryptdevice`.

Segue um formato similar às opções usadas no crypttab - opções são separadas por vírgulas, opções com valores são especificados com `*opção*=*valor*`.

Exemplo:

```
rd.luks.options=timeout=10s,swap,cipher=aes-cbc-essiv:sha256,size=256

```

#### rd.luks.key

Especifique a localização da keyfile que será utilizada para abrir o dispositivo especificado com o UUID. Não há uma localização padrão para a keyfile, como existe com o parâmetro do hook `encrypt`, `cryptkey`.

Se a keyfile está [incluída](/index.php/Mkinitcpio#BINARIES_and_FILES "Mkinitcpio") no initramfs:

```
rd.luks.key=*XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX*=*/caminho/para/keyfile*

```

ou

```
rd.luks.key=*/caminho/para/keyfile*

```

Se a keyfile está em outro dispositivo:

```
rd.luks.key=*XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX*=*/caminho/para/keyfile*:UUID=*ZZZZZZZZ-ZZZZ-ZZZZ-ZZZZ-ZZZZZZZZZZZZ*

```

Substitua `UUID=*ZZZZZZZZ-ZZZZ-ZZZZ-ZZZZ-ZZZZZZZZZZZZ*` com o identificador do dispositivo que a keyfile está localizada. Se o sistema de arquivos utilizado não é o mesmo do sistema raiz, você deve [incluir o módulo dele no initramfs](/index.php/Mkinitcpio#MODULES "Mkinitcpio").

**Atenção:** `rd.luks.key` com uma keyfile em outro dispositivo por padrão não vai pedir a senha caso este não estiver disponível. Para solicitar a senha, especifique a opção `keyfile-timeout=` no `rd.luks.options`. Exemplo, para uma espera de 10 secondos: `rd.luks.options=*XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX*=keyfile-timeout=10s` 

#### Timeout

Existem duas opções que irão afetar o tempo de espera até a senha ser solicitada durante a inicialização:

*   `rd.luks.options=timeout=*tempo_limite*` especifica o tempo máximo para achar a senha
*   `rootflags=x-systemd.device-timeout=*tempo_limite*` especifica o quanto systemd deve esperar pelo dispositivo até desistir (padrão 90 segundos)

Se deseja desabilitar os tempos de espera, então defina ambos para zero:

```
rd.luks.options=timeout=0 rootflags=x-systemd.device-timeout=0

```

## crypttab

O arquivo `/etc/crypttab` (tabela de dispositivos criptografados) é similar ao arquivo [fstab](/index.php/Fstab "Fstab") e contém uma lista de dispositivos criptografados que serão abertos durante a inicialização. Este arquivo pode ser usado para montar automaticamente dispositivos swap ou sistemas de arquivos não raiz.

`crypttab` é lido *antes* do `fstab`, então os containers do dm-crypt podem ser abertos antes que o sistema de arquivos seja montado. Note que `crypttab` é lido *depois* que o sistema inicia, logo não é um substituto para abrir partições criptografadas com os hooks do [mkinitcpio](#mkinitcpio) e [opções do gerenciador de boot](#Gerenciador_de_boot) como no caso de [criptografar a partição raiz](/index.php/Dm-crypt/Criptografando_todo_um_sistema "Dm-crypt/Criptografando todo um sistema"). A leitura do `crypttab` é feita na inicialização pelo `systemd-cryptsetup-generator` automaticamente.

Veja [crypttab(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/crypttab.5) para detalhes, veja abaixo alguns exemplos, e a seção [#Montando na inicialização](#Montando_na_inicialização) para instruções de como usar UUIDs para montar um dispositivo criptografado.

**Nota:** Se usa o [systemd-boot](/index.php/Systemd-boot "Systemd-boot") e o hook `sd-encrypt`, se a senha de uma partição não raiz é igual a da raiz, não há necessidade de colocar a partição não raiz no crypttab devido ao cache da senha. Veja [esta conversa no fórum](https://bbs.archlinux.org/viewtopic.php?id=219859) para mais informações.

**Atenção:**

*   Se a opção *nofail* é especificada, a tela de entrada da senha pode desaparecer enquanto digita. *nofail* deve então somente ser usada junto com keyfiles.
*   Existem problemas no [systemd](/index.php/Systemd "Systemd") quando ele processa entradas do `crypttab` para o [modo plain](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_plain_mode "Dm-crypt/Device encryption") (`--type plain`) do *dm-crypt*:
    *   Para dispositivos `--type plain` com uma keyfile, é necessário adicionar a opção `hash=plain` para o crypttab devido a uma [incompatibilidade do systemd](https://bugs.freedesktop.org/show_bug.cgi?id=52630). **Não** use `systemd-cryptsetup` manualmente para a criação do dispositivo como medida provisória.
    *   Pode ser necessário adicionar a opção `plain` explicitamente para forçar `systemd-cryptsetup` a reconhecer o dispositivo (`--type plain`) na inicialização. Veja [issue do systemd 442](https://github.com/systemd/systemd/issues/442).

 `/etc/crypttab` 
```
# Exemplo de um arquivo crypttab. campos são: nome, dispositivo criptografado, senha, opções do cryptsetup.

# Monte /dev/lvm/swap criptografando-a com uma nova chave a cada inicialização.
 swap	/dev/lvm/swap	/dev/urandom	swap,cipher=aes-xts-plain64,size=256

# Monte /dev/lvm/tmp como /dev/mapper/tmp usando o modo plain do dm-crypt com uma senha randômica, fazendo seu conteúdo não recuperável depois de desmontada.
tmp	/dev/lvm/tmp	/dev/urandom	tmp,cipher=aes-xts-plain64,size=256 

# Monte /dev/lvm/home como /dev/mapper/home usando LUKS, solicite a senha durante a inicialização.
home   /dev/lvm/home

# Monte /dev/sdb1 como /dev/mapper/backup usando LUKS, com uma senha guardada em um arquivo.
backup /dev/sdb1       /home/alice/backup.key
```

### Montando na inicialização

Se você quer montar uma unidade de armazenamento criptografada na inicialização, você pode colocar o UUID do dispositivo em `/etc/crypttab`. Para descobrir o UUID (da partição) pode usar o comando `lsblk -f` e adicioná-lo ao `crypttab` desse jeito:

 `/etc/crypttab`  `disco_externo         UUID=XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX        none    luks,timeout=180` 

O primeiro parâmetro é o nome que o dispositivo criptografado vai receber quando aberto(que fica a sua preferência). A opção `none` fará a senha ser solicitada durante a inicialização. A opção `timeout` define um tempo de espera máximo em segundos para entrar com a senha.

**Nota:** Tenha em mente que a opção `timeout` em `crypttab` somente determina a quantidade de tempo permitida para *entrar com a senha*. Adicionalmente, [systemd](/index.php/Systemd "Systemd") também tem um tempo de espera máximo para o *dispositivo estar disponível* (90 segundos por padrão), que é independente do temporarizador da senha. Consequentemente, até quando a opção `timeout` em `crypttab` é definida para um valor maior que 90 segundos (ou está no seu valor padrão 0, sem limite de tempo), *systemd* esperará no máximo 90 segundos para o dispositivo ser aberto. Para mudar isso, a opção `x-systemd.device-timeout` (veja [systemd.mount(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.mount.5)) pode ser definida no [fstab](/index.php/Fstab "Fstab") para tal dispositivo. Provavelmente é desejado que a quantidade de tempo da opção `timeout` no `crypttab` é igual a presente na opção `x-systemd.device-timeout` no `fstab` para cada dispositivo montado na inicialização.

#### Desbloqueando com uma keyfile

Se a [keyfile](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption") para um sistema de arquivos não raiz está guardada dentro do sistema criptografado, ela está segura quando o sistema está desligado e pode ser automaticamente aberto durante a inicialização via [crypttab](/index.php/Crypttab "Crypttab"). Por exemplo, abrir um dispositivo especificado com [UUID](/index.php/Nomea%C3%A7%C3%A3o_persistente_de_dispositivo_de_bloco#by-uuid "Nomeação persistente de dispositivo de bloco"):

 `/etc/crypttab` 
```
home    UUID=<identificador UUID>    /etc/mykeyfile

```

**Dica:** Se você prefere usar o modo `--plain`, as opções de encriptação necessárias para abrir o dispositivo deverão ser especificadas no `/etc/crypttab`. Tome cuidado ao fazer a medida provisória mencionada no [crypttab](#crypttab).

Use o nome do dispositivo mapeado (definido no `/etc/crypttab`) para fazer a entrada no `/etc/fstab`:

 `/etc/fstab` 
```
/dev/mapper/home        /home   ext4        defaults        0       2

```

Desde que `/dev/mapper/home` já é uma mapeação única, não existe a necessidade de especificar o UUID dele. Em qualquer caso, o sistema de arquivos mapeado vai ter um UUID diferente da partição criptografada.

#### Montando um dispositivo de bloco empilhado

Os geradores do systemd também processam automaticamente os dispositivos de bloco empilhados na inicialização.

Por exemplo, você pode usar o cryptsetup numa configuração do [RAID](/index.php/RAID "RAID") e criar um volume lógico [LVM](/index.php/LVM_(Portugu%C3%AAs) "LVM (Português)") com o sistema de arquivos dentro de um dispositivo de bloco criptografado. Resultando em:

 `$ lsblk -f` 
```
─sdXX                  linux_raid_member    
│ └─md0                 crypto_LUKS   
│   └─cryptedbackup     LVM2_member 
│     └─vgraid-lvraid   ext4              /mnt/backup
└─sdYY                  linux_raid_member    
  └─md0                 crypto_LUKS       
    └─cryptedbackup     LVM2_member 
      └─vgraid-lvraid   ext4              /mnt/backup

```

A senha será solicitada e ele será montado na inicialização.

Ao especificar corretamente as entradas do crypttab (exemplo, UUID para o dispositivo `crypto_LUKS`) e fstab (`/dev/vgraid/lvraid`), não há necessidade para configurações/hooks adicionais no mkinitcpio, devido ao processamento do `/etc/crypttab` aplicado às partições não raiz somente. Existe uma exceção, quando o hook `mdadm_udev` *já* é usado (exemplo, o dispositivo raiz). Neste caso é necessário atualizar o `/etc/madadm.conf` e o initramfs para que a raid raiz correta seja selecionada.

### Montando em demanda

Você pode dar [start](/index.php/Systemd_(Portugu%C3%AAs)#Usando_units "Systemd (Português)") no `systemd-cryptsetup@disco_externo.service`, ao invés de usar:

```
# cryptsetup luksOpen UUID=... disco_externo

```

Quando você tem uma entrada como a seguir em seu `/etc/crypttab`:

 `/etc/crypttab`  `disco_externo UUID=... none noauto` 

Desta maneira você não precisa se lembrar exatamente das opções do crypttab. A senha será solicitada se necessário.

O arquivo correspondente unit é gerada automaticamente pelo [systemd-cryptsetup-generator(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-cryptsetup-generator.8). Você pode listar todos os arquivos unit gerados usando:

```
$ systemctl list-unit-files | grep systemd-cryptsetup

```

## Solução de problemas

### Sistema travado no prompt de inicialização/senha não aparece

Se você está usando [Plymouth](/index.php/Plymouth_(Portugu%C3%AAs) "Plymouth (Português)"), tenha certeza de usar os módulos corretos (veja [Plymouth#O hook do plymouth](/index.php/Plymouth_(Portugu%C3%AAs)#O_hook_do_plymouth "Plymouth (Português)")) ou desabilite isso. De outra forma, Plymouth irá atrapalhar o prompt de senha, impedindo o sistema de inicializar.