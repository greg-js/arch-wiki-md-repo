**Status de tradução:** Esse artigo é uma tradução de [Dm-crypt/Encrypting a non-root file system](/index.php/Dm-crypt/Encrypting_a_non-root_file_system "Dm-crypt/Encrypting a non-root file system"). Data da última tradução: 2019-12-28\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Dm-crypt/Encrypting_a_non-root_file_system&diff=0&oldid=592783) na versão em inglês.

Os seguintes exemplos são para criptografar um sistema de arquivos secundário, não raiz, com dm-crypt.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Visão geral](#Visão_geral)
*   [2 Partição](#Partição)
    *   [2.1 Montando e desmontando manualmente](#Montando_e_desmontando_manualmente)
    *   [2.2 Desbloqueio e montagem automatizados](#Desbloqueio_e_montagem_automatizados)
        *   [2.2.1 Na inicialização do sistema](#Na_inicialização_do_sistema)
        *   [2.2.2 No login do usuário](#No_login_do_usuário)
*   [3 Dispositivo de loop](#Dispositivo_de_loop)
    *   [3.1 Sem losetup](#Sem_losetup)
    *   [3.2 Com losetup](#Com_losetup)
        *   [3.2.1 Montando e desmontando manualmente](#Montando_e_desmontando_manualmente_2)

## Visão geral

Criptografar um sistema de arquivos secundário normalmente protege somente dados sensíveis, enquanto deixa o sistema operacional e programas sem encriptação. Isto é somente útil para dispositivos removíveis, como um USB, para então este ser usado em outros computadores com segurança. Também, é possível criptografar conjuntos separados de dados de acordo com quem possui acesso.

Devido ao dm-crypt ser uma camada de encriptação a [nível de blocos](/index.php/Disk_encryption#Block_device_encryption "Disk encryption"), ele somente criptografa os dispositivos, [partições](#Partição) e [dispositivos de loop](#Dispositivo_de_loop). Para criptografar arquivos indíviduais é necessário uma camada de encriptação a nível de sistema de arquivos, como [eCryptfs](/index.php/ECryptfs "ECryptfs") or [EncFS](/index.php/EncFS "EncFS"). Veja [Encriptação de disco](/index.php/Disk_encryption "Disk encryption") para informações gerais sobre como proteger dados privados.

## Partição

Este exemplo detalha a encriptação da partição `/home`, mas pode ser aplicado para qualquer outra partição similar, não raiz, que contém dados do usuário.

**Dica:** Você pode ter o diretório `/home`, em uma partição, único para um usuário, ou criar uma partição `/home` compartilhada para todos os diretórios dos usuários.

Primeiro tenha certeza que a partição está vazia (sem sistema de arquivos). Delete a partição e crie uma nova se ela possui um sistema de arquivos. Então apague com segurança, veja [apagando o disco com segurança](/index.php/Dm-crypt/Preparando_a_unidade_de_armazenamento#Apagando_o_disco_com_segurança "Dm-crypt/Preparando a unidade de armazenamento").

Crie a partição que vai conter o container criptografado.

Então configure o cabeçalho LUKS com:

```
# cryptsetup *opções* luksFormat *dispositivo*

```

Mude `*dispositivo*` para a nova partição. Veja [Opções de encriptação para o modo LUKS](/index.php/Dm-crypt/Encripta%C3%A7%C3%A3o_de_dispositivo#Opções_de_encriptação_para_o_modo_LUKS "Dm-crypt/Encriptação de dispositivo") para detalhes tais como as `*opções*` disponíveis.

Para acessar a partição criptografada, desbloqueie ela com o mapeador de dispositivos, usando:

```
# cryptsetup open *dispositivo* *nome*

```

Depois de desbloquear a partição, ela estará disponível em `/dev/mapper/*nome*`. Agora crie um [sistema de arquivos](/index.php/File_system "File system") de sua escolha com:

```
# mkfs.*tipo_do_sistema_de_arquivos* /dev/mapper/*nome*

```

Monte o sistema de arquivos em `/home`, ou se deve ser somente acessível a um usuário em `/home/*nome do usuário*`, veja [#Montando e desmontando manualmente](#Montando_e_desmontando_manualmente).

**Dica:** Desmonte e monte uma vez para verificar se o mapeamento está funcionando como desejado.

### Montando e desmontando manualmente

Para montar a partição:

```
# cryptsetup open *dispositivo* *nome*
# mount -t *tipo_do_sistema_de_arquivos* /dev/mapper/*nome* /mnt/home

```

Para desmontar:

```
# umount /mnt/home
# cryptsetup close *nome*

```

**Dica:** [GVFS](/index.php/GVFS "GVFS") tambem pode montar partições criptografadas. Você pode usar um gerenciador de arquivos com suporte ao gvfs (exemplo [Thunar](/index.php/Thunar "Thunar")) para montar a partição, e a caixa de diálogo pedindo a senha aparecerá. Para outros desktops, [zulucrypt](https://aur.archlinux.org/packages/zulucrypt/) também oferece uma GUI.

### Desbloqueio e montagem automatizados

Existem três diferentes soluções para automaticamente desbloquear a partição e montar seu sistema de arquivos.

#### Na inicialização do sistema

Usando o arquivo de configuração `/etc/crypttab`, o desbloqueio ocorre no momento de inicialização fazendo uso do parsing automático do systemd. Esta é a solução recomendada se você deseja usar uma partição home comum para os diretórios de todos os usuários ou automaticamente montar outro dispositivo de bloco encriptado.

Veja [Dm-crypt/Configuração do sistema#crypttab](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema#crypttab "Dm-crypt/Configuração do sistema") para referências e [Montando na inicialização do sistema](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema#Montando_na_inicialização "Dm-crypt/Configuração do sistema") para um exemplo prático.

#### No login do usuário

Usando *pam_exec* é possível desbloquear (*cryptsetup open*) a partição no login do usuário: esta é a solução recomendada se deseja um diretório home de somente um usuário em uma partição. Veja [dm-crypt/Montagem no login](/index.php/Dm-crypt/Mounting_at_login "Dm-crypt/Mounting at login").

O desbloqueio no login do usuário também é possível com [pam_mount](/index.php/Pam_mount "Pam mount").

## Dispositivo de loop

Existem dois métodos para usar um dispositivo de loop como um container criptografado, um usando `losetup` diretamente e outro não.

### Sem losetup

Usar diretamente o losetup pode ser evitado completamente ao fazer o seguinte[[1]](https://wiki.gentoo.org/wiki/Custom_Initramfs#Encrypted_keyfile):

```
$ dd if=/dev/urandom of=grande_segredo.img bs=100M count=1 iflag=fullblock
$ cryptsetup luksFormat grande_segredo.img

```

Tenha certeza de não omitir a opção `iflag=fullblock`, de outro modo *dd* pode retornar uma leitura parcial. Veja [dd#Partial read](/index.php/Dd#Partial_read "Dd") para detalhes.

Antes de executar `cryptsetup`, veja [Opções de encriptação para o modo LUKS](/index.php/Dm-crypt/Encripta%C3%A7%C3%A3o_de_dispositivo#Opções_de_encriptação_para_o_modo_LUKS "Dm-crypt/Encriptação de dispositivo") e [cifras criptográficas e modos de operação](/index.php/Disk_encryption#Ciphers_and_modes_of_operation "Disk encryption") primeiro para selecionar configurações adicionais do seu interesse.

As instruções para abrir o dispositivo e criar o [sistema de arquivos](/index.php/File_system "File system") são do mesmo jeito que em [#Partição](#Partição).

**Nota:** Se criar um arquivo menor que o cabeçalho do LUKS (16 MiB) vai receber um erro `Requested offset is beyond real size of device grande_segredo.img` quando tentar abrir o dispositivo.

O procedimento de montagem e desmontagem manual é igual a [#Montando e desmontando manualmente](#Montando_e_desmontando_manualmente).

### Com losetup

Um dispositivo de loop permite mapear um dispositivo de bloco para um arquivo com a ferramenta padrão do util-linux `losetup`. O arquivo pode então conter um sistema de arquivos, que pode ser usado como qualquer outro. Vários usuários conhecem [TrueCrypt](/index.php/TrueCrypt "TrueCrypt") como uma ferramenta para criar containers criptografados. É possível conseguir essa mesma funcionalidade com um sistema de arquivos de looback criptografado com LUKS, como é mostrado no exemplo a seguir.

Primeiro, crie um container criptografado com [dd](/index.php/Dd "Dd"), usando um [gerador de números aleatórios](/index.php/Random_number_generator "Random number generator") apropriado:

```
# dd if=/dev/urandom of=grande_segredo.img bs=100M count=1 iflag=fullblock

```

O arquivo `grande_segredo.img` vai ser criado com o tamanho de 100 mebibytes.

**Nota:** Evite [redimensionar](/index.php/Dm-crypt/Encripta%C3%A7%C3%A3o_de_dispositivo#Sistema_de_arquivos_de_loopback "Dm-crypt/Encriptação de dispositivo") o container, crie ele maior do que a soma do tamanho de todos os arquivos que serão criptografados, de modo que consiga hospedar a metadata associada utilizada pelo sistema de arquivos interno. Se pretende usar o modo LUKS, o cabeçalho de metadata dele sozinho vai ocupar mais de 16 mebibytes.

Depois, crie um dispositivo de nó, agora podemos montar/usar nosso container:

```
# losetup /dev/loop0 grande_segredo.img

```

**Nota:** Se você receber um erro `/dev/loop0: No such file or directory`, você precisa carregar o módulo do kernel `modprobe loop` comoo superusuário. Nestes dias (kernel 3.2) dispositivos de loop são criados em demanda. Solicite um novo com `losetup -f` como superusuário.

A partir de agora, o procedimento é o mesmo que o especificado em [#Partição](#Partição), exceto pelo fato que o container já está com dados aleatórios e não será necessário apagar com segurança.

**Dica:** Containers com *dm-crypt* podem ser muito flexíveis. Veja as funcionalidades e documentação de [Tomb](/index.php/Tomb "Tomb"). Ele oferece um script para um manuseio rápido e flexível do *dm-crypt*.

#### Montando e desmontando manualmente

Para desmontar o container:

```
# umount /mnt/segredo
# cryptsetup close segredo
# losetup -d /dev/loop0

```

Para montar o container novamente:

```
# losetup /dev/loop0 grande_segredo.img
# cryptsetup open /dev/loop0 segredo
# mount -t ext4 /dev/mapper/segredo /mnt/segredo

```