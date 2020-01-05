**Status de tradução:** Esse artigo é uma tradução de [Dm-crypt/Device encryption](/index.php/Dm-crypt/Device_encryption "Dm-crypt/Device encryption"). Data da última tradução: 2019-12-28\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Dm-crypt/Device_encryption&diff=0&oldid=591797) na versão em inglês.

Esta página mostra como utilizar *dm-crypt* pela linha de comando para criptografar um sistema.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Preparação](#Preparação)
*   [2 Uso do cryptsetup](#Uso_do_cryptsetup)
    *   [2.1 Senhas e chaves do cryptsetup](#Senhas_e_chaves_do_cryptsetup)
*   [3 Opções de encriptação com dm-crypt](#Opções_de_encriptação_com_dm-crypt)
    *   [3.1 Opções de encriptação para o modo LUKS](#Opções_de_encriptação_para_o_modo_LUKS)
    *   [3.2 Opções de encriptação para o modo plain](#Opções_de_encriptação_para_o_modo_plain)
*   [4 Criptografando dispositivos com cryptsetup](#Criptografando_dispositivos_com_cryptsetup)
    *   [4.1 Criptografando dispositivos com o modo LUKS](#Criptografando_dispositivos_com_o_modo_LUKS)
        *   [4.1.1 Formatando partições LUKS](#Formatando_partições_LUKS)
            *   [4.1.1.1 Formatando uma partição com LUKS e uma keyfile](#Formatando_uma_partição_com_LUKS_e_uma_keyfile)
        *   [4.1.2 Abrindo/Mapeando containers LUKS com o mapeador de dispositivos](#Abrindo/Mapeando_containers_LUKS_com_o_mapeador_de_dispositivos)
    *   [4.2 Criptografando dispositivos com o modo plain](#Criptografando_dispositivos_com_o_modo_plain)
*   [5 Ações específicas do cryptsetup para o LUKS](#Ações_específicas_do_cryptsetup_para_o_LUKS)
    *   [5.1 Gerenciamento de chaves](#Gerenciamento_de_chaves)
        *   [5.1.1 Adicionando chaves do LUKS](#Adicionando_chaves_do_LUKS)
        *   [5.1.2 Removendo chaves do LUKS](#Removendo_chaves_do_LUKS)
    *   [5.2 Backup e restauração](#Backup_e_restauração)
        *   [5.2.1 Backup usando o cryptsetup](#Backup_usando_o_cryptsetup)
        *   [5.2.2 Restauração usando o cryptsetup](#Restauração_usando_o_cryptsetup)
        *   [5.2.3 Backup e restauração manual](#Backup_e_restauração_manual)
    *   [5.3 Criptografando dispositivos novamente](#Criptografando_dispositivos_novamente)
        *   [5.3.1 Criptografar um sistema de arquivos](#Criptografar_um_sistema_de_arquivos)
        *   [5.3.2 Criptografando novamente um container LUKS](#Criptografando_novamente_um_container_LUKS)
*   [6 Redimensionando os dispositivos criptografados](#Redimensionando_os_dispositivos_criptografados)
    *   [6.1 Sistema de arquivos de loopback](#Sistema_de_arquivos_de_loopback)
*   [7 Keyfiles](#Keyfiles)
    *   [7.1 Tipos de keyfiles](#Tipos_de_keyfiles)
        *   [7.1.1 Senha](#Senha)
        *   [7.1.2 Texto randômico](#Texto_randômico)
        *   [7.1.3 Binário](#Binário)
    *   [7.2 Criando uma keyfile com caracteres randômicos](#Criando_uma_keyfile_com_caracteres_randômicos)
        *   [7.2.1 Guardando a keyfile em um sistema de arquivos filesystem](#Guardando_a_keyfile_em_um_sistema_de_arquivos_filesystem)
            *   [7.2.1.1 Sobrescrevendo com segurança as keyfiles guardadas](#Sobrescrevendo_com_segurança_as_keyfiles_guardadas)
        *   [7.2.2 Guardando a keyfile no ramfs](#Guardando_a_keyfile_no_ramfs)
    *   [7.3 Configurando o LUKS para utilizar uma/outra keyfile](#Configurando_o_LUKS_para_utilizar_uma/outra_keyfile)
    *   [7.4 Manualmente abrindo uma partição com uma keyfile](#Manualmente_abrindo_uma_partição_com_uma_keyfile)
        *   [7.4.1 Com uma keyfile em um dispositivo externo](#Com_uma_keyfile_em_um_dispositivo_externo)
            *   [7.4.1.1 Configurando o mkinitcpio](#Configurando_o_mkinitcpio)
            *   [7.4.1.2 Configurando os parâmetros do kernel](#Configurando_os_parâmetros_do_kernel)
        *   [7.4.2 Com uma keyfile no initramfs](#Com_uma_keyfile_no_initramfs)

## Preparação

Antes de usar [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup), tenha certeza que o [módulo do kernel](/index.php/Kernel_module "Kernel module") `dm_crypt` está carregado.

## Uso do cryptsetup

*cryptsetup* é uma ferramenta da linha de comando para o *dm-crypt* criar, acessar e gerenciar dispositivos criptografados. Ela foi expandida para suportar diferentes tipos de encriptação que dependem do mapeador de dispositivos e módulos criptografados (**d**evice-**m**apper and the **crypt**ographic modules). A expansão mais notável foi o LUKS (Linux Unified Key Setup), que guarda todas as informações necessárias para o dm-crypt no próprio disco e abstrai a partição e gerenciamento de chaves com o objetivo de facilitar o uso. Dispositivos acessados via o mapeador de dispositivos são chamados de dispositivos de bloco (blockdevices). Para mais informações veja [Criptografia de disco#Encriptação de dispositivo de bloco](/index.php/Criptografia_de_disco#Encriptação_de_dispositivo_de_bloco "Criptografia de disco").

A ferramenta é usada da seguinte forma:

```
# cryptsetup <OPÇÕES> <ação> <opções-específicas-da-ação> <dispositivo> <dmnome>

```

Existem opções e modo de encriptação padrão, que serão usados se nenhuma outra opção for especificada. Veja

```
$ cryptsetup --help 

```

Todos os parâmetros, opções e ações padrão serão listados. A lista completa das opções pode ser encontrada na página man. Parâmetros podem ser opcionais ou não, dependendo do modo de encriptação e ação escolhidas, as seções a seguir possuem mais informação sobre elas. A velocidade é muito importante, portanto deve-se escolher com cuidado o algoritmo que vai utilizar. Mudar a cifra criptográfica de um dispositivo de bloco já criptografado é dificíl, por isso é importante verificar a performance do *dm-crypt* com diferentes parâmetros antes de instalar o sistema:

```
$ cryptsetup benchmark 

```

Lhe ajudará a decidir qual algoritmo e tamanho de chave você quer usar. Se algumas cifras AES se destacarem com uma grande diferença, estas provavelmente devem ter suporte de hardware na CPU.

**Dica:** Pode ser desejado praticar a encriptação em uma [máquina virtual](/index.php/Virtualiza%C3%A7%C3%A3o "Virtualização").

### Senhas e chaves do cryptsetup

Um dispositivo de bloco criptografado é protegido por uma chave. Pode ser:

*   uma senha: veja [Security#Passwords](/index.php/Security#Passwords "Security").
*   uma keyfile, veja [#Keyfiles](#Keyfiles).

Ambos os tipos de chave possuem tamanhos padrões máximos: senhas podem ser até 512 caracteres e keyfiles até 8192KiB.

Uma importante distinção do *LUKS* a se notar é que a chave é usada para desbloquear a chave mestre do dispositivo criptografado com LUKS, e esta pode ser mudada. Outros modos de encriptação não suportam mudança na chave depois de definida, devido a eles não utilizarem uma chave mestre na encriptação. Veja [Criptografia de disco#Encriptação de dispositivo de bloco](/index.php/Criptografia_de_disco#Encriptação_de_dispositivo_de_bloco "Criptografia de disco") para detalhes.

## Opções de encriptação com dm-crypt

*Cryptsetup* suporta o uso de diferentes modos de encriptação com *dm-crypt*:

*   `--type luks` para usar a versão padrão do LUKS (LUKS1 com [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) < 2.1.0, LUKS2 com [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) ≥ 2.1.0),
*   `--type luks1` para usar LUKS1, a versão mais comum do LUKS,
*   `--type luks2` para usar LUKS2, a última versão do LUKS que permite extensões adicionais,
*   `--type plain` para usar o modo plain do dm-crypt,
*   `--type loopaes` para o modo loopaes legacy,
*   `--type tcrypt` para o modo de compatibilidade com [TrueCrypt](/index.php/TrueCrypt "TrueCrypt").

As opções criptográficas básicas para as cifras e hashes disponíveis podem ser usadas para todos os modos e dependem das funcionalidades relacionadas a criptografia presentes no kernel. Todas as que são carregadas e disponíveis para uso como opções podem ser vistas com:

```
$ less /proc/crypto 

```

**Dica:** Se a lista é pequena, execute `$ cryptsetup benchmark` que irá ativar a busca de módulos disponíveis.

As opções de encriptação para os modos `luks`, `luks1`, `luks2` e `plain` serão introduzidas. Note que a tabela lista opções utilizadas em seus respectivos artigos e não todas as disponíveis.

### Opções de encriptação para o modo LUKS

A ação do *cryptsetup* para configurar um novo dispositivo do dm-crypt no modo de encriptação LUKS é *luksFormat*. Diferente do que o nome implica, não formata o dispositivo, mas configura o cabeçalho do dispositivo LUKS e criptografa a chave mestre com as opções criptografadas desejadas.

como LUKS é o modo de encriptação padrão, você pode criar um novo dispositivo LUKS com os parâmetros padrão (`-v` é opcional):

```
# cryptsetup -v luksFormat *dispositivo*

```

Em comparação, você pode querer especificar as opções padrão manualmente também:

```
# cryptsetup -v --type luks --cipher aes-xts-plain64 --key-size 256 --hash sha256 --iter-time 2000 --use-urandom --verify-passphrase luksFormat *dispositivo*

```

As opções padrão são comparadas com um exemplo de especificação criptograficamente maior na tabela abaixo, com comentários:

| Opções | Padrão do cryptsetup 2.1.0 | Exemplo | Comentários |
| --cipher

-c

 | `aes-xts-plain64` | `aes-xts-plain64` | [A versão 1.6.0](https://www.kernel.org/pub/linux/utils/cryptsetup/v1.6/v1.6.0-ReleaseNotes) mudou o padrão para uma [cifra](/index.php/Criptografia_de_disco#Cifras_e_modos_de_operação "Criptografia de disco") do AES no modo [XTS](https://en.wikipedia.org/wiki/Disk_encryption_theory#XEX-based_tweaked-codebook_mode_with_ciphertext_stealing_.28XTS.29 "wikipedia:Disk encryption theory") (veja o item 5.16 [do FAQ](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#5-security-aspects)). Não é recomendado o uso da cifra padrão anterior `--cipher aes-cbc-essiv` devido a seus conhecidos [problemas](https://en.wikipedia.org/wiki/Disk_encryption_theory#Cipher-block_chaining_.28CBC.29 "wikipedia:Disk encryption theory") e [ataques](http://www.jakoblell.com/blog/2013/12/22/practical-malleability-attack-against-cbc-encrypted-luks-partitions/) práticos contra eles. |
| --key-size

-s

 | `256` (`512` for XTS) | `512` | Por padrão uma chave com tamanho de 512 bit é usada para cifras XTS. Note no entanto que [XTS divide a chave no meio](https://en.wikipedia.org/wiki/Disk_encryption_theory#XEX-based_tweaked-codebook_mode_with_ciphertext_stealing_.28XTS.29 "wikipedia:Disk encryption theory"), resultando no uso do AES-256. |
| --hash

-h

 | `sha256` | `sha512` | O algoritmo de Hash usado para [derivação de chave](/index.php/Criptografia_de_disco#Metadados_criptográficos "Criptografia de disco"). A versão 1.7.0 mudou o padrão de `sha1` para `sha256` "*não por segurança [mas] principalmente para previnir problemas de compabilidade em sistemas onde SHA1 já estava [em] desuso* "[[1]](https://www.kernel.org/pub/linux/utils/cryptsetup/v1.7/v1.7.0-ReleaseNotes). O antigo padrão do `sha1` pode ainda ser usado por compatibilidade com versões mais velhas do *cryptsetup* desde que é [considerada segura](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#5-security-aspects) (veja o item 5.20). |
| --iter-time

-i

 | `2000` | `5000` | Número de milisegundos a serem esperados com o processamento da senha PBKDF2\. A versão 1.7.0 mudou o padrão de `1000` para `2000` com o objetivo de "*tentar manter a contagem da interação do PBKDF2 alta o bastante e também ainda aceitável pelos usuários.*"[[2]](https://www.kernel.org/pub/linux/utils/cryptsetup/v1.7/v1.7.0-ReleaseNotes). Esta opção é somente relevante para operações do LUKS que definem ou mudam senhas, tais como *luksFormat* ou *luksAddKey*. Especificando 0 como parâmetro seleciona o padrão compilado. |
| --use-{u,}random | `--use-urandom` | `--use-random` | Seleciona que [gerador de números randômicos](/index.php/Random_number_generator "Random number generator") vai ser utilizado. Traduzindo a página manual do cryptsetup: "Em situações de baixa entropia (exemplo, em um sistema embarcado), ambas as escolhas são problemáticas. Usar /dev/urandom pode resultar em chaves fracas. Usar /dev/random pode demorar muito tempo, potencialmente para sempre, se a entropia coletada pelo kernel não for o bastante." |
| --verify-passphrase

-y

 | Yes | - | Padrão somente para luksFormat e luksAddKey. Não é necessário digitar essa opção no momento. |

As propriedades das funcionalidades e opções do LUKS são descritas nas especificações do [LUKS1](https://gitlab.com/cryptsetup/cryptsetup/wikis/Specification) (pdf) e [LUKS2](https://gitlab.com/cryptsetup/cryptsetup/blob/master/docs/on-disk-format-luks2.pdf) (pdf).

**Dica:** A apresentação dos desenvolvedores do projeto [devconfcz2016](https://mbroz.fedorapeople.org/talks/DevConf2016/devconf2016-luks2.pdf) (pdf) sumariza a motivação para as grandes mudanças do LUKS2.

### Opções de encriptação para o modo plain

No modo *plain* do dm-crypt, não existe chave mestre no dispositivo, consequentemente não é necessário defini-lá. As opções de encriptação são empregadas diretamente para criar a mapeação entre o disco criptografado e um dispositivo nomeado. O mapeamento pode ser criado na partição ou no dispositivo todo. Nesse último caso não é necessário uma tabela de partição.

O mapeamento do modo *plain* com os parâmetros padrão do cryptsetup pode ser feito com:

```
# cryptsetup <opções> open --type plain <dispositivo> <dmnome>

```

Ao executar o comando, será solicitada a senha, que deve possuir uma entropia muito alta. Abaixo uma comparação dos parâmetros padrão com o exemplo em [dm-crypt/Criptografando todo um sistema#Plain dm-crypt](/index.php/Dm-crypt/Criptografando_todo_um_sistema#Plain_dm-crypt "Dm-crypt/Criptografando todo um sistema"):

| Opção | Padrão do cryptsetup 2.1.0 | Exemplo | Comentários |
| --hash

-h

 | `ripemd160` | - | O hash é usado para criar a chave com a senha; não é usado em uma keyfile. |
| --cipher

-c

 | `aes-cbc-essiv:sha256` | `aes-xts-plain64` | As cifras consistem de três pares: geradores cifra-modo_de_opeação-IV. Veja [Criptografia de disco#Cifras e modos de operação](/index.php/Criptografia_de_disco#Cifras_e_modos_de_operação "Criptografia de disco") para uma explicação dessas configurações, e a [documentação do DMCrypt](https://gitlab.com/cryptsetup/cryptsetup/wikis/DMCrypt) para os modos disponíveis. |
| --key-size

-s

 | `256` | `512` | O tamanho da chave (em bits). O tamanho dependerá da cifra e chainmode utilizado. O modo Xts precisa de duas vezes o tamanho da chave do cbc. |
| --size

-b

 | Tamanho real do disco alvo | `2048` (dispositivo mapeado será 512B×2048=1MiB) | Limite o tamanho máximo do dispositivo (em setores de 512-byte). |
| --offset

-o

 | `0` | `0` | O quanto pular do inicio do disco alvo (setores de 512-byte) antes de começar o mapeamento |
| --skip

-p

 | `0` | `2048` (512B×2048=1MiB serão pulados) | O número de setores de 512-byte de dados criptografados a pular no começo. |
| --key-file

-d

 | A senha será usada por padrão | `/dev/sd*Z*` (ou, por exemplo, `/boot/keyfile.enc`) | O dispositivo ou arquivo a ser usado como chave. Veja [#Keyfiles](#Keyfiles) para mais detalhes. |
| --keyfile-offset | `0` | `0` | Distância do início do arquivo onde a chave começa (em bytes). Esta opção é suportada a partir da versão 1.6.7 do *cryptsetup*. |
| --keyfile-size

-l

 | `8192kB` | - (será utilizado o padrão) | Limita os bytes lidos da keyfile. Esta opção é suportada a partir da versão 1.6.7 do *cryptsetup*. |

Se usar o dispositivo `/dev/sd*X*`, o exemplo da columa acima da direita resulta em:

```
# cryptsetup --cipher=aes-xts-plain64 --offset=0 --key-file=/dev/sd*Z* --key-size=512 open --type=plain /dev/sdX enc

```

Diferente de criptografar com LUKS, o comando acima deve ser executado *totalmente*, independente se o mapeamento precisa ser re-estabelecido ou não, é importante lembrar da cifra, hash e keyfile. Agora podemos checar se o mapeamento foi feito:

```
# fdisk -l

```

O dispositivo mapeado deve aparecer como `/dev/mapper/enc`.

## Criptografando dispositivos com cryptsetup

Esta seção mostra como empregar as opções para criar novos dispositivos de bloco criptografados e acessá-los manualmente.

**Atenção:** GRUB não suporta cabeçalhos do LUKS2; veja [GRUB bug #55093](https://savannah.gnu.org/bugs/?55093). Então, se você planeja [abrir uma partição de boot criptografada com o GRUB](/index.php/GRUB_(Portugu%C3%AAs)#/boot_criptografado "GRUB (Português)"), especifique `--type luks1` nos dispositivos criptografados que o GRUB precisa acessar.

### Criptografando dispositivos com o modo LUKS

#### Formatando partições LUKS

Para configurar uma partição criptografada LUKS, execute:

```
# cryptsetup luksFormat *dispositivo*

```

Lhe será solicitado uma senha e também a verificação desta.

Veja [#Opções de encriptação para o modo LUKS](#Opções_de_encriptação_para_o_modo_LUKS) para opções da linha de comando.

Você pode checar os resultados com:

```
# cryptsetup luksDump *dispositivo*

```

Note que a saída vai mostrar a informação do cabeçalho da cifra criptográfica, como também as chaves em uso da partição LUKS.

O seguinte exemplo criará uma partição raiz criptografada no `/dev/sda1` usando a cifra AES padrão no modo XTS com uma efetiva encriptação de 256-bit

```
# cryptsetup -s 512 luksFormat /dev/sda1

```

##### Formatando uma partição com LUKS e uma keyfile

Na criação de uma partição criptografada LUKS, uma keyfile pode ser associada usando:

```
# cryptsetup luksFormat *dispositivo* */caminho/para/keyfile*

```

Veja [#Keyfiles](#Keyfiles) para instruções em como gerar e gerenciar keyfiles.

#### Abrindo/Mapeando containers LUKS com o mapeador de dispositivos

Uma vez que os containers LUKS foram criados, eles podem ser abertos.

Para abrir um container LUKS voce precisa definir o nome do novo dispositivo mapeado. Isto alerta o kernel que `*dispositivo*` está criptografado e deve ser acessado através do LUKS usando o `/dev/mapper/*dm_nome*` para nao sobrescrever os dados criptografados. Para se proteger deste tipo de acidente, leia sobre como fazer [backup do cabeçalho criptografado](#Backup_e_restauração) depois de terminar a configuração.

Para abrir um container LUKS criptografado execute:

```
# cryptsetup open *dispositivo* *dm_nome*

```

Será solicitada a senha para abrir o container. Normalmente o nome do dispositivo mapeado é uma breve descrição da função do container mapeado. Por exemplo, o comando a seguir abre o container LUKS `/dev/sda1` e mapeia ele para `cryptraiz`:

```
# cryptsetup open /dev/sda1 cryptraiz

```

Uma vez aberto, o container criptografado deve ser acessado pelo caminho `/dev/mapper/cryptraiz` ao invés do container diretamente (exemplo `/dev/sda1`).

Para configurar um grupo de volumes do LVM em cima da camada criptografada, o nome do dispositivo mapeado deve ser (nesse caso) algo parecido com `/dev/mapper/cryptraiz`, e não `/dev/sda1`. LVM vai dar nomes adicionais para todos os volumes lógicos criados, exemplo, `/dev/lvmpool/raiz` e `/dev/lvmpool/swap`.

Para escrever dados criptografados no container você deve acessá-lo pelo nome do dispositivo mapeado. O primeiro passo tipicamente será [colocar um sistema de arquivos](/index.php/File_systems#Create_a_file_system "File systems") . Por exemplo:

```
# mkfs -t ext4 /dev/mapper/cryptraiz

```

O dispositivo `/dev/mapper/cryptraiz` pode ser então [montado](/index.php/Mount "Mount") como qualquer partição.

Para fechar o container LUKS, desmonte a partição e execute:

```
# cryptsetup close cryptraiz

```

### Criptografando dispositivos com o modo plain

A criação e acesso subsequente do container no modo plain do *dm-crypt* precisam somente dos [parâmetros](#Opções_de_encriptação_para_o_modo_plain) corretos com a ação `open`. A seguir é mostrado dois dispositivos não raiz, com o segundo criado em cima do primeiro. Obviamente, empilhar a criptografia dobra uso de recursos. Este exemplo é utilizado para mostrar o uso de cifras criptográficas.

O primeiro mapeamento é criado com as opções padrão do modo plain do*cryptsetup*, como descrito em uma das tabelas acima

 `# cryptsetup --type plain -v open /dev/sdaX plain1` 
```
Enter passphrase:
Command successful.

```

No segundo dispositivo de bloco, vão ser utilizados parâmetros diferentes e um (opcional) início (offset), colocar um sistema de arquivos e montá-lo.

 `# cryptsetup --type plain --cipher=serpent-xts-plain64 --hash=sha256 --key-size=256 --offset=10  open /dev/mapper/plain1 plain2`  `Enter passphrase:`  `# lsblk -p` 
```
 NAME
 /dev/sda
 ├─/dev/sdaX
 │ └─/dev/mapper/plain1
 │   └─/dev/mapper/plain2
 ...

```

```
# mkfs -t ext2 /dev/mapper/plain2
# mount -t ext2 /dev/mapper/plain2 /mnt
# echo "Este é o empilhado. Uma senha por pé para atirar" > /mnt/stacked.txt

```

Feche o dispositivo para checar se o acesso funciona

```
# cryptsetup close plain2
# cryptsetup close plain1

```

Primerio, tente abrir o sistema de arquivos diretamente:

```
# cryptsetup --type plain --cipher=serpent-xts-plain64 --hash=sha256 --key-size=256 --offset=10 open /dev/sdaX plain2

```
 `# mount -t ext2 /dev/mapper/plain2 /mnt` 
```
mount: wrong fs type, bad option, bad superblock on /dev/mapper/plain2,
      missing codepage or helper program, or other error

```

Por que não deu certo? como o "plain2" que começa no bloco (`10`) está criptografado com a cifra do "plain1". Ele só pode ser acessado através do dispositivo mapeado empilhado. O erro é arbitário, tentar a senha ou opções erradas vai resultar no mesmo. Para o modo plain do *dm-crypt*, a ação `open` não apresentará erros.

Tentando novamente mas agora na ordem correta:

```
# cryptsetup close plain2    # dispositivo mapeado disfuncional da tentativa anterior

```
 `# cryptsetup --type plain open /dev/sdaX plain1` 
```
Enter passphrase:

```
 `# cryptsetup --type plain --cipher=serpent-xts-plain64 --hash=sha256 --key-size=256 --offset=10 open /dev/mapper/plain1 plain2`  `Enter passphrase:`  `# mount /dev/mapper/plain2 /mnt && cat /mnt/stacked.txt` 
```
Este é o empilhado. Uma senha por pé para atirar

```

*dm-crypt* irá cuidar da criptografia empilhada com alguns modos misturados também. Por exemplo o modo LUKS poderia ser empilhado no dispositivo mapeado "plain1". Seu cabeçalho deve estar criptografado dentro do "plain1".

A opção `--shared` está somente disponível para o modo plain. Com esta um dispositivo pode ser segmentado em diferentes dispositivos mapeados sem sobreposição. Isto será exemplificado a seguir, usando um modo de cifra compatível com *loopaes* para o "plain2":

 `# cryptsetup --type plain --offset 0 --size 1000 open /dev/sdaX plain1`  `Enter passphrase:`  `# cryptsetup --type plain --offset 1000 --size 1000 --shared --cipher=aes-cbc-lmk --hash=sha256 open /dev/sdaX plain2`  `Enter passphrase:`  `# lsblk -p` 
```
NAME
dev/sdaX
├─/dev/sdaX
│ ├─/dev/mapper/plain1
│ └─/dev/mapper/plain2
...

```

Como a árvore de dispositivos mostra, ambos residem no mesmo nível, elas não estão empilhadas e "plain2" pode ser aberto individualmente.

## Ações específicas do cryptsetup para o LUKS

### Gerenciamento de chaves

É possível definir até 8 chaves diferentes por container LUKS. Permitindo a criação do acesso a chaves para salvar dados de backup: Na prática conhecida como key escrow, uma chave é usada para utilização diária, outra guardada para ganhar acesso ao container caso a senha seja esquecida ou a keyfile foi perdida/danificada. Também, um diferente espaço de chave pode ser usado para garantir acesso de um container para um usuário ao adicionar uma segunda chave e mais tarde removê-la.

Uma vez que o container criptografado foi criado, o espaço de chave (key slot) 0 é criado (se nenhum outro foi definido manualmente). Espaços de chave adicionais são numerados de 1 a 7\. Os espaços de chave utilizados podem ser vistos com:

 `# cryptsetup luksDump /dev/<dispositivo> | grep BLED` 
```
Key Slot 0: ENABLED
Key Slot 1: ENABLED
Key Slot 2: ENABLED
Key Slot 3: DISABLED
Key Slot 4: DISABLED
Key Slot 5: DISABLED
Key Slot 6: DISABLED
Key Slot 7: DISABLED

```

Onde <dispositivo> é o volume que contém o cabeçalho do LUKS. Este e todos os seguintes comandos nesta seção funcionam em backups de cabeçalho também.

#### Adicionando chaves do LUKS

Para adicionar uma nova chave, use a ação do cryptsetup `luksAddKey`. Por segurança, sempre será solicitada uma chave existente válida ("any passphrase"), também para dispositivos já abertos, antes que a nova senha seja solicitada:

 `# cryptsetup luksAddKey /dev/<dispositivo> (/caminho/para/<keyfile_adicional>)` 
```
Enter any passphrase:
Enter new passphrase for key slot:
Verify passphrase: 

```

Se `/caminho/para/<keyfile_adicional>` for dado, cryptsetup adicionará a <keyfile_adicional>. Se não, uma nova senha será solicitada duas vezes. É possível usar uma existente *keyfile* para autorizar a ação, use a opção `--key-file` ou `-d` seguida pela "antiga" <keyfile>:

```
# cryptsetup luksAddKey /dev/<dispositivo> (/caminho/para/<keyfile_adicional>) -d /caminho/para/<keyfile>

```

Se é desejado usar múltiplas chaves e mudar ou remover elas, a opção `--key-slot` ou `-S` pode ser usada para especificar o slot:

 `# cryptsetup luksAddKey /dev/<dispositivo> -S 6` 
```
Enter any passphrase: 
Enter new passphrase for key slot: 
Verify passphrase:

```
 `# cryptsetup luksDump /dev/sda8 | grep 'Slot 6'` 
```
Key Slot 6: ENABLED

```

Para mostrar uma ação associada neste exemplo, foi decidido mudar a chave acima mostrada:

 `# cryptsetup luksChangeKey /dev/<dispositivo> -S 6` 
```
Enter LUKS passphrase to be changed: 
Enter new LUKS passphrase:

```

Antes de removê-la.

#### Removendo chaves do LUKS

Existem três diferentes ações para remover chaves do cabeçalho:

*   `luksRemoveKey` é usado para remover uma chave por especificar sua senha/kefile.
*   `luksKillSlot` pode ser usado para remover uma chave específica (usando outra chave). Isto é extremamente útil se você esqueceu uma senha, perdeu uma keyfile ou não tem acesso a ela.
*   `luksErase` é usado para rapidamente remover **todas** as chaves ativas.

**Atenção:**

*   Todas as ações acima podem ser usadas apagar a última chave ativa de um dispositivo criptografado!
*   O comando `luksErase` foi adicionado na versão 1.6.4 para rapidamente retirar o acesso ao dispositivo. Esta ação **não irá** solicitar senha! Isto não irá [apagar o cabeçalho do LUKS](/index.php/Dm-crypt/Preparando_a_unidade_de_armazenamento#Apagar_o_cabeçalho_do_LUKS "Dm-crypt/Preparando a unidade de armazenamento"), mas todos os espaços de chave de uma vez só, então você não ganhará acesso a menos que você tenha um backup válido do cabeçalho do LUKS.

É útil saber se a chave que desejamos **manter** é válida. Uma forma fácil de checar é abrir o dispositivo com a opção `-v`, o espaço que ela ocupa será mostrado:

 `# cryptsetup -v open /dev/<dispositivo> testcrypt` 
```
Enter passphrase for /dev/<dispositivo>: 
Key slot 1 unlocked.
Command successful.

```

Agora será removida a chave adicionada na subseção anterior, usando sua senha:

 `# cryptsetup luksRemoveKey /dev/<dispositivo>` 
```
Enter LUKS passphrase to be deleted:

```

Se for usada a mesma senha para dois espaços, a primeira ocorrência de espaço que tiver a senha vai ser apagado. Somente executando novamente a segunda vai ser apagada.

Alternativamente, é possível especificar o espaço de chave:

 `# cryptsetup luksKillSlot /dev/<dispositivo> 6` 
```
Enter any remaining LUKS passphrase:

```

Note que em ambos os casos, nenhuma confirmação é necessária.

 `# cryptsetup luksDump /dev/sda8 | grep 'Slot 6'` 
```
Key Slot 6: DISABLED

```

Reiterando o que foi falado acima: Se a mesma senha foi usada para o espaço 1 e 6, ambos devem ter sidos apagados agora.

### Backup e restauração

Se o cabeçalho de um container criptografado com LUKS é destruído, você não vai conseguir decriptografar seus dados. Tão problemático quanto esquecer a senha ou modificar/perder a keyfile. Danos podem acontecer por sua própria responsabilidade ao particionar novamente o disco depois ou por programas de terceiros que interpretam errado a tabela de partições. Então, ter um backup do cabeçalho e guardá-lo em outro lugar pode ser uma boa ideia.

**Nota:** Se uma das senhas das partições criptografadas com LUKS for revelada, você deve retirá-la em *todas* as cópias do cabeçalho, até mesmo estes que você fez o backup. De outro modo, uma cópia do cabeçalho criptografado que a usa pode ser utilizado para determinar a chave mestre que pode ser usada para abrir o container relacionado (até mesmo o seu atual, não somente o do backup). Se a chave mestre for descoberta, você vai ter que re-criptografar todo seu container. Veja o [PAQ do LUKS](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#6-backup-and-data-recovery) para mais detalhes.

#### Backup usando o cryptsetup

A ação `luksHeaderBackup` do cryptsetup faz o backup do cabeçalho LUKS e os espaços de chave:

```
# cryptsetup luksHeaderBackup /dev/<dispositivo> --header-backup-file /mnt/<backup>/<arquivo>.img

```

Onde <dispositivo> é a partição que contém o volume LUKS.

**Dica:** Você pode também fazer o backup do cabeçalho no ramfs e criptografá-lo com o gpg antes de escrevê-lo em um local persistente ao executar os seguintes comandos.

```
# mkdir /root/<tmp>/
# mount ramfs /root/<tmp>/ -t ramfs
# cryptsetup luksHeaderBackup /dev/<dispositivo> --header-backup-file /root/<tmp>/<arquivo>.img
# gpg2 --recipient <User ID> --encrypt /root/<tmp>/<arquivo>.img 
# cp /root/<tmp>/<arquivo>.img.gpg /mnt/<backup>/
# umount /root/<tmp>

```

**Atenção:** Tmpfs pode trocar para o disco se tem pouca memória disponível, então isto não é recomendado aqui.

#### Restauração usando o cryptsetup

**Atenção:** Restaurar o cabeçalho errado ou restaurar para uma partição não criptografada pode resultar em perda de dados! A ação não pode fazer uma verificação se o cabeçalho é o *correto* para dado dispositivo.

Para evitar a restauração de um cabeçalho errado, você pode fazer a verificação ao usá-lo como um cabeçalho remoto com a opção `--header`:

 `# cryptsetup -v --header /mnt/<backup>/<arquivo>.img open /dev/<dispositivo> test` 
```
Key slot 0 unlocked.
Command successful.

```

```
# mount /dev/mapper/test /mnt/test && ls /mnt/test 
# umount /mnt/test 
# cryptsetup close test 

```

Se não ocorreram erros, a restauração pode ser feita:

```
# cryptsetup luksHeaderRestore /dev/<dispositivo> --header-backup-file ./mnt/<backup>/<arquivo>.img

```

Agora todos os espaços de chave foram sobrescrevidos; somente os espaços de chave ativos do backup devem estar disponíveis.

#### Backup e restauração manual

O cabeçalho sempre vai residir no início do dispositivo e um backup pode ser feito sem acesso ao *cryptsetup* também. Primeiro você têm que descobrir o payload offset da partição criptografada:

 `# cryptsetup luksDump /dev/<dispositivo> | grep "Payload offset"` 
```
Payload offset:	4040

```

Depois, cheque o tamanho dos setores na unidade de armazenamento

 `# fdisk -l /dev/<dispositivo> | grep "Sector size"` 
```
Sector size (logical/physical): 512 bytes / 512 bytes

```

Agora que você sabe os valores, você pode fazer o backup do cabeçalho com o [dd](/index.php/Dd "Dd"):

```
# dd if=/dev/<dispositivo> of=/caminho/para/<arquivo>.img bs=512 count=4040

```

Guarde-o com segurança.

Uma restauração pode ser feita usando os mesmos valores, com exceção do `if` e `of` que serão invertidos:

```
# dd if=/caminho/para/<arquivo>.img of=/dev/<dispositivo> bs=512 count=4040

```

### Criptografando dispositivos novamente

O pacote [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) possui a ferramenta *cryptsetup-reencrypt*. Esta pode ser usada para converter um sistema de arquivos existente para um criptografado com LUKS (opção `--new`) e permanentemente removê-lo (opção `--decrypt`) de um dispositivo. Como o nome sugere também pode ser usado para criptografar novamente um container LUKS, apesar que isto não é possível com o cabeçalho desanexado ou outros modos de encriptação (exemplo, modo plain). É possível mudar as [#Opções de encriptação para o modo LUKS](#Opções_de_encriptação_para_o_modo_LUKS). Ações do *cryptsetup-reencrypt* podem somente ser executadas em dispositivos desmontados. Veja [cryptsetup-reencrypt(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cryptsetup-reencrypt.8) para mais informações.

Criptografar novamente um container pode ser útil para assegurar os dados depois que uma senha ou [keyfile](#Keyfiles) foi compromisada *e* não tem certeza que alguma cópia do cabeçalho foi obtida. Por exemplo, se somente uma senha foi vista mas nenhum acesso físico/lógico ocorreu, deve ser o bastante mudar a respectiva senha/chave ([#Gerenciamento de chaves](#Gerenciamento_de_chaves)).

**Atenção:** Sempre tenha um **backup confiável** disponível e verifique duas vezes as opções especificadas antes de usar a ferramenta!

Exemplo, uma partição é criptografada com LUKS e então criptografada novamente.

#### Criptografar um sistema de arquivos

O cabeçalho do LUKS sempre é armazenado no início do dispositivo. Já que usualmente um sistema de arquivos existente usa todos os setores da partição, o primeiro passo é diminuir o espaço alocado para o cabeçalho do LUKS.

O cabeçalho [padrão](#Opções_de_encriptação_para_o_modo_LUKS) do LUKS2 precisa de 16MiB. O sistema de arquivos `ext4` existente no `/dev/sdaX` será verificado e depois redimensionado para seu mínimo espaço possível:

```
# umount /mnt

```
 `# e2fsck -f /dev/sdaX` 
```
e2fsck 1.43-WIP (18-May-2015)
Pass 1: Checking inodes, blocks, and sizes
...
/dev/sdaX: 12/166320 files (0.0% non-contiguous), 28783/665062 blocks

```
 `# resize2fs -M /dev/sdaX` 
```
resize2fs 1.43-WIP (18-May-2015)
Resizing the filesystem on /dev/sdaX to 26347 (4k) blocks.
The filesystem on /dev/sdaX is now 26347 (4k) blocks long.

```

A cifra padrão de encriptação vai ser utilizada, então não há necessidade de especificá-la:

 `# cryptsetup-reencrypt /dev/sdaX --new  --reduce-device-size 16M` 
```
Enter new passphrase:
Verify passphrase:
Finished, time 00:05.126,  952 MiB written, speed 185,7 MiB/s

```

Depois que acabar, a encriptação vai ter sido feita para toda a partição, não somente o espaço que o sistema de arquivos foi diminuído (`sdaX` tem `2.6GiB` e a CPU usada no exemplo não tem instruções AES presentes no hardware). Por fim, extenda o sistema de arquivos para ocupar o espaço disponível novamente:

 `# cryptsetup open /dev/sdaX recrypt` 
```
Enter passphrase for /dev/sdaX:
...

```
 `# resize2fs /dev/mapper/recrypt` 
```
resize2fs 1.43-WIP (18-May-2015)
Resizing the filesystem on /dev/mapper/recrypt to 664807 (4k) blocks.
The filesystem on /dev/mapper/recrypt is now 664807 (4k) blocks long.

```

```
# mount /dev/mapper/recrypt /mnt

```

E pronto.

#### Criptografando novamente um container LUKS

Neste exemplo um container LUKS é criptografado novamente.

**Atenção:** Tenha certeza de especificar as opções de encriptação corretas para *cryptsetup-reencrypt* e *nunca* faça isso sem um **backup confiável**!

Para criptografar novamente o dispositivo com suas opções de encriptação atuais, você não precisa especificá-las:

 `# cryptsetup-reencrypt /dev/sdaX` 
```
Enter passphrase for key slot 0:
Progress: 100,0%, ETA 00:00, 2596 MiB written, speed  36,5 MiB/s

```

Um possível uso é criptografar dispositivos LUKS que não tem opções de encriptação modernas. A habilidade de modificar o cabeçalho pode ser limitada pelo seu tamanho. Exemplo, se um dispositivo inicialmente foi criptografado com a cifra CBC e tamanho de chave de 128 bit, o cabeçalho deste vai ter metade do tamanho mencionado acima (`4096` setores):

 `# cryptsetup luksDump /dev/sdaX |grep -e "mode" -e "Payload" -e "MK bits"` 
```
Cipher mode:   	cbc-essiv:sha256
Payload offset:	**2048**
MK bits:       	128

```

Apesar de ser possível atualizar a criptografia de tal dispositivo, isto é praticável somente se feito em dois passos. Primeiro, use as mesmas opções de encriptação, mas use a opção `--reduce-device-size` para disponibilizar espaço para um cabeçalho maior. Segundo, agora utilize as opções de encriptação que desejar. Por esta razão e o fato que um backup deve ser feito, criar um novo dispositivo criptografado para o restaurar é uma opção mais rápida.

## Redimensionando os dispositivos criptografados

Se um dispositivo de armazenamento criptografado com dm-crypt está sendo clonado (com uma ferramenta como o [dd](/index.php/Dd "Dd")) para outro dispositivo maior, este último deve ser redimensionado para utilizar todo o seu espaço.

Neste exemplo, o dispositivo destino é /dev/sdX2, todo o espaço adicional da partição vai ser utilizado:

```
# cryptsetup luksOpen /dev/sdX2 sdX2
# cryptsetup resize sdX2

```

O sistema de arquivos deste deve ser redimensionado também.

### Sistema de arquivos de loopback

Assuma que um sistema de arquivos de loopback criptografado está no arquivo `grande_segredo`, ligado ao `/dev/loop0`, mapeado como `segredo` e montado em `/mnt/segredo`, como no exemplo presente em [dm-crypt/Criptografando um sistema de arquivos não raiz#Dispositivo de loop](/index.php/Dm-crypt/Criptografando_um_sistema_de_arquivos_n%C3%A3o_raiz#Dispositivo_de_loop "Dm-crypt/Criptografando um sistema de arquivos não raiz").

Se o container está mapeado e/ou montado, o desmonte e/ou feche:

```
# umount /mnt/segredo
# cryptsetup close segredo
# losetup -d /dev/loop0

```

Depois, expanda o container com o tamanho do arquivo que você quer adicionar. Neste exemplo, o arquivo será expandido com 1M * 1024, que é 1G.

**Atenção:** Tenha certeza de usar **dois** `>`, ao invês de um, ou você irá sobrescrever o arquivo e não adicionar no final dele. Fazer um backup antes desse passo é fortemente recomendado.

```
# dd if=/dev/urandom bs=1M count=1024 | cat - >> grande_segredo

```

Agora mapeie o container para o dispositivo de loop:

```
# losetup /dev/loop0 grande_segredo
# cryptsetup open /dev/loop0 segredo

```

Depois disso, redimensione a parte criptografada do container para o novo tamanho máximo do arquivo container:

```
# cryptsetup resize segredo

```

Finalmente, cheque o sistema de arquivos e, se está ok, o redimensione (exemplo para ext2/3/4):

```
# e2fsck -f /dev/mapper/segredo
# resize2fs /dev/mapper/segredo

```

Você pode montar o container novamente:

```
# mount /dev/mapper/segredo /mnt/segredo

```

## Keyfiles

**Nota:** Esta seção descreve o uso de keyfile em texto puro. Se desejar criptografar a keyfile para conseguir autentificação de dois fatores veja [Usando keyfiles criptografadas com GPG ou OpenSSL](/index.php/Dm-crypt/Specialties#Using_GPG,_LUKS,_or_OpenSSL_Encrypted_Keyfiles "Dm-crypt/Specialties") para detalhes, mas ainda leia esta seção.

**O que é uma keyfile?**

Também conhecida como arquivo chave ou arquivo-chave, uma keyfile é um arquivo cujo dados são usados como senha para abrir um volume criptografado. Isto significa que se tal arquivo é perdido ou modificado, abrir o volume pode não ser mais possível.

**Dica:** Adicione uma senha além da keyfile para evitar a situação citada acima.

**Porque usar uma keyfile?**

Existem muitos tipos de keyfiles. Cada tipo possui suas vantagens e desvantagens, resumidos abaixo:

### Tipos de keyfiles

#### Senha

Contém a senha. A vantagem deste tipo é que se o arquivo perde os dados, o proprietário do volume criptografado pode se lembrar do conteudo. No entanto a desvantagem é que isto não trás nenhuma segurança extra comparado com digitar a senha na inicialização.

Exemplo: `1234`

**Nota:** A keyfile que contém a senha não deve ter quebra de linha (newline) dentro dela. Uma opção é criá-la usando:
```
# echo -n 'sua_senha' > /caminho/para/<keyfile>
# chown root:root /caminho/para/<keyfile>; chmod 400 /caminho/para/<keyfile>

```

#### Texto randômico

Este tipo de keyfile contém um bloco de caracteres randômicos. É muito mais resistente ao ataques de dicionários que uma simples senha. Possui também como vantagem o tamanho dos dados utilizados. Desde que este tipo não é para ser memorizado por uma pessoa, é possível criar um arquivo com milhares de caracteres e colocá-lo como uma chave. A desvantagem é que se o arquivo é perdido ou modificado, não deve ser possível recuperar o acesso ao volume criptografado sem outra chave.

Exemplo: `fjqweifj830149-57 819y4my1-38t1934yt8-91m 34co3;t8y;9p3y-`

#### Binário

É um arquivo binário que foi definido como keyfile. Quando identificar candidatos para uma keyfile, é recomendado que escolha fotos relativamente estáticas como fotos, músicas, vídeos. A vantagem, esses arquivos tem outras funções que dificultam a sua identificação como keyfile. Ao invês de ter um arquivo de texto com uma grande quantidade de texto randômico, a keyfile vai ser considerada como um arquivo de mídia normal. A desvantagem, se o arquivo for perdido ou mudado, provavelmente não será mais possível acessar o volume criptografado sem outra chave. Adicionalmente, existe teoricamente uma perda de aleatoriedade se comparado com um arquivo de texto randômico. Isto é devido ao fato que imagens, vídeos e músicas tem uma relação intríseca entre bits de dados vizinhos que não existe num texto randômico. No entanto isto é controverso e nunca foi publicamente explorado.

Exemplo: imagens, texto, video ...

### Criando uma keyfile com caracteres randômicos

#### Guardando a keyfile em um sistema de arquivos filesystem

Uma keyfile pode ser de conteudo e tamanho arbitrários.

É utilizado o `dd` para gerar uma keyfile de 2048 bytes randômicos, os colocando no arquivo `/etc/minha_keyfile`:

```
# dd bs=512 count=4 if=/dev/random of=/etc/minha_keyfile iflag=fullblock

```

Se você planeja guardar a keyile em um dispositivo externo, você pode simplesmente mudar a saída para o diretório correspondente:

```
# dd bs=512 count=4 if=/dev/random of=/media/pendrive/minha_keyfile iflag=fullblock

```

Para negar o acesso de qualquer usuário exceto o `root`:

```
# chmod 600 /etc/minha_keyfile

```

##### Sobrescrevendo com segurança as keyfiles guardadas

Se você guardar sua keyfile temporária em uma unidade de armazenamento, e quer deletá-la, use algo parecido com isso

```
# shred --remove --zero minha_keyfile

```

para sobrescrever com segurança. Para sistemas de arquivos antigos como FAT ou ext2 isto deve bastar, enquanto que no caso de sistemas de arquivos com journaling, hardware de memória flash e outros casos é recomendado a [apagar todo o disco](/index.php/Securely_wipe_disk "Securely wipe disk").

#### Guardando a keyfile no ramfs

Alternativamente você pode montar uma ramfs para guardar a keyfile temporariamente:

```
# mkdir /root/minha_ramfs
# mount ramfs /root/minha_ramfs/ -t ramfs
# cd /root/minha_ramfs

```

A vantagem é que ela reside na RAM e não em um disco fisíco, então não pode ser recuperada depois de desmontar o ramfs. Depois de copiar a keyfile para outro seguro e persistente sistema de arquivos, desmonte o ramfs com

```
# umount /root/minha_ramfs

```

### Configurando o LUKS para utilizar uma/outra keyfile

Adicione um espaço de chave para a keyfile no cabeçalho do LUKS:

 `# cryptsetup luksAddKey /dev/sda2 /etc/minha_keyfile` 
```
Enter any LUKS passphrase:
key slot 0 unlocked.
Command successful.

```

### Manualmente abrindo uma partição com uma keyfile

Use a opção `--key-file` quando for abrir um dispositivo LUKS:

```
# cryptsetup open /dev/sda2 *dm_nome* --key-file /etc/minha_keyfile

```

#### Com uma keyfile em um dispositivo externo

##### Configurando o mkinitcpio

Você pode adicionar um módulo em sua `/etc/mkinitcpio.conf` para o sistema de arquivos da sua unidade de armazenamento, no exemplo abaixo o módulo (`vfat`):

```
MODULES=(vfat)

```

Neste exemplo é assumido que você vai usar um pendrive formatado em FAT (módulo `vfat`). Mude este módulo para outro caso forusar outro sistema de arquivos (exemplo, `ext2`). Se receber uma mensagem reclamando de "bad superblock" e "bad codepage" na inicialização, é necessário carregar uma codepage extra. Você pode precisar do módulo `nls_iso8859-1` para a codepage `iso8859-1`.

Se você usa um teclado não-US, pode ser útil carregá-lo antes que seja solicitada a senha para abrir a partição raiz na inicialização. Para isto, você precisa do hook `keyboard` antes do `encrypt`.

[Gere novamente o initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").

##### Configurando os parâmetros do kernel

Adicione as seguintes opções nos [parâmetros do kernel](/index.php/Par%C3%A2metros_do_kernel "Parâmetros do kernel") se está usando o hook `encrypt`. Se está usando o `sd-encrypt` veja [dm-crypt/Configuração do sistema#Usando o hook sd-encrypt](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema#Usando_o_hook_sd-encrypt "Dm-crypt/Configuração do sistema").

```
cryptdevice=/dev/*<partição1>*:raiz cryptkey=/dev/*<partição2>*:<tipo_do_sistema_de_arquivos>:<caminho>

```

Por exemplo:

```
cryptdevice=/dev/sda3:raiz cryptkey=/dev/sdb1:vfat:/chaves/chavesecreta

```

Escolher um arquivo com nome normal dá um pouco de 'segurança por obscurantismo', mas esteja ciente que a linha de comando do kernel é gravada no log do kernel (*dmesg*). A keyfile não pode ser um arquivo escondido, isto significa que o nome do arquivo não deve começar com um ponto, ou o hook `encrypt` não vai conseguir encontrar o arquivo durante o processo de inicialização. Alternativamente, você pode essconder a keyfile entre partições e usar:

```
cryptkey=/dev/sdb1:início:tamanho

```

Como vantagem, é mais difícil acidentalmente deletar a chave.

Não existe garantia que nomes de dispositivos como `/dev/sdb1` irão permanecer os mesmos entre inicializações. É mais confiável acessar o dispositivo com a [nomeação persistente de dispositivo de bloco](/index.php/Nomea%C3%A7%C3%A3o_persistente_de_dispositivo_de_bloco "Nomeação persistente de dispositivo de bloco") do udev. Use isto para ter certeza que o hook `encrypt` vai encontrar sua keyfile quando lê-la de um dispositivo externo.

#### Com uma keyfile no initramfs

**Atenção:** Use uma keyfile dentro do initramfs **somente** se você proteger a keyfile suficientemente por:

*   Usar alguma forma de autentificação prévia no processo de inicialização. De outro modo, o dispositivo vai ser aberto automaticamente, acabando com a proposta de criptografar o dispositivo de bloco.
*   `/boot` é criptografado. De outro modo, a raiz de outra instalação (incluindo o [ambiente live](/index.php/Guia_de_instala%C3%A7%C3%A3o#Inicializar_o_ambiente_live "Guia de instalação")) pode extrair sua chave do initramfs, e decriptografar o dispositivo sem qualquer meio de autentificação.

Este método permite o uso de um nome especial para a keyfile que vai ser colocada no [initramfs](/index.php/Initramfs "Initramfs") e lida pelo [hook](/index.php/Mkinitcpio#HOOKS "Mkinitcpio") `encrypt` para abrir o sistema de arquivos raiz (`cryptdevice`) automaticamente. Pode ser útil quando deseja que o [/boot criptografado](/index.php/GRUB_(Portugu%C3%AAs)#/boot_criptografado "GRUB (Português)"), evitando entrar duas senhas durante a inicialização.

O hook `encrypt` permite que o usuário especificar uma keyfile com o parâmetro do kernel `cryptkey`: no caso do initramfs, a sintaxe é `rootfs:*caminho*`. Veja [dm-crypt/Configuração do sistema#cryptkey](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema#cryptkey "Dm-crypt/Configuração do sistema"). Apesar que, este parâmetro do kernel se não definido vai usar por padrão `/crypto_keyfile.bin`, e se o initramfs contém uma chave válida com este nome, o container será aberto sem a necessidade de definir o parâmetro `cryptkey`.

Se está usando o `sd-encrypt`, especifique a localização da keyfile com o parâmetro do kernel `rd.luks.key`. Veja [dm-crypt/Configuração do sistema#rd.luks.key](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema#rd.luks.key "Dm-crypt/Configuração do sistema").

[Gere uma keyfile](#Criando_uma_keyfile_com_caracteres_randômicos), defina permissões apropriadas e [a adicione como uma chave do LUKS](#Adicionando_chaves_do_LUKS):

```
# dd bs=512 count=4 if=/dev/random of=/crypto_keyfile.bin iflag=fullblock
# chmod 600 /crypto_keyfile.bin
# chmod 600 /boot/initramfs-linux*
# cryptsetup luksAddKey /dev/sdX# /crypto_keyfile.bin

```

**Atenção:** Quando as permissões do initramfs estão definidas para 644 (por padrão), então todos os usuários poderão despejar a keyfile. Tenha certeza de que as permissões ainda são 600 depois de atualizar ou instalar um kernel.

Inclua a chave no [arranjo de arquivos do mkinitcpio](/index.php/Mkinitcpio#BINARIES_and_FILES "Mkinitcpio"):

 `/etc/mkinitcpio.conf`  `FILES=(/crypto_keyfile.bin)` 

Finalmente [gere novamente o initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").

Na próxima inicialização você deve precisar somente entrar com a senha do container criptografado uma vez.

([fonte](http://www.pavelkogan.com/2014/05/23/luks-full-disk-encryption/#bonus-login-once))