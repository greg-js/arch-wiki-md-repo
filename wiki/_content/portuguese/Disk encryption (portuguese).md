Related articles

*   [dm-crypt (Português)](/index.php/Dm-crypt_(Portugu%C3%AAs) "Dm-crypt (Português)")
*   [TrueCrypt](/index.php/TrueCrypt "TrueCrypt")
*   [eCryptfs](/index.php/ECryptfs "ECryptfs")
*   [EncFS](/index.php/EncFS "EncFS")
*   [gocryptfs](/index.php/Gocryptfs "Gocryptfs")
*   [fscrypt](/index.php/Fscrypt "Fscrypt")
*   [Tomb](/index.php/Tomb "Tomb")
*   [tcplay](/index.php/Tcplay "Tcplay")
*   [GnuPG](/index.php/GnuPG "GnuPG")
*   [Self-Encrypting Drives](/index.php/Self-Encrypting_Drives "Self-Encrypting Drives")

**Status de tradução:** Esse artigo é uma tradução de [Disk encryption](/index.php/Disk_encryption "Disk encryption"). Data da última tradução: 2020-01-02\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Disk_encryption&diff=0&oldid=593622) na versão em inglês.

Este artigo discute sobre software de [Criptografia de disco](https://en.wikipedia.org/wiki/disk_encryption "wikipedia:disk encryption"), que des-/criptografa dados escritos / lidos de um [dispositivo de bloco](/index.php/Dispositivo_de_bloco "Dispositivo de bloco"), [partição de disco](/index.php/Parti%C3%A7%C3%A3o_de_disco "Partição de disco") ou diretório. Exemplos de dispositivos de blocos são discos rígidos, unidade flash e DVDs.

Encriptação de disco deve ser somente vista como um complemento para mecanismos de segurança já existentes do sistema operacional - focado em prevenir acesso físico, enquanto confia em *outras* partes do sistema que proveem coisas como segurança de rede e acesso baseado no usuário.

Para encriptação total de disco (full-disk encryption, FDE), veja [dm-crypt/Criptografando todo um sistema](/index.php/Dm-crypt/Criptografando_todo_um_sistema "Dm-crypt/Criptografando todo um sistema").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Porque criptografar?](#Porque_criptografar?)
*   [2 Criptografia de dados do sistema](#Criptografia_de_dados_do_sistema)
*   [3 Métodos disponíveis](#Métodos_disponíveis)
    *   [3.1 Encriptação empilhada no sistema de arquivos](#Encriptação_empilhada_no_sistema_de_arquivos)
        *   [3.1.1 Armazenamento na nuvem optimizado](#Armazenamento_na_nuvem_optimizado)
    *   [3.2 Encriptação de dispositivo de bloco](#Encriptação_de_dispositivo_de_bloco)
    *   [3.3 Encriptação de dispositivo de bloco vs encriptação empilhada no sistema de arquivos](#Encriptação_de_dispositivo_de_bloco_vs_encriptação_empilhada_no_sistema_de_arquivos)
    *   [3.4 Tabela de comparação](#Tabela_de_comparação)
*   [4 Preparação](#Preparação)
    *   [4.1 Escolhendo uma configuração](#Escolhendo_uma_configuração)
    *   [4.2 Exemplos](#Exemplos)
    *   [4.3 Escolhendo uma senha forte](#Escolhendo_uma_senha_forte)
    *   [4.4 Preparando o disco](#Preparando_o_disco)
*   [5 Como a criptografia funciona](#Como_a_criptografia_funciona)
    *   [5.1 Princípio básico](#Princípio_básico)
    *   [5.2 Chaves, keyfiles e senhas](#Chaves,_keyfiles_e_senhas)
    *   [5.3 Metadados criptográficos](#Metadados_criptográficos)
    *   [5.4 Cifras e modos de operação](#Cifras_e_modos_de_operação)
    *   [5.5 Negação plausível](#Negação_plausível)

## Porque criptografar?

Encriptação de disco assegura que os arquivos são sempre guardados na forma criptografada. Os arquivos somente se tornam disponíveis para o sistema operacional e programas em forma legível enquanto o sistema está rodando e aberto por um usuário confiável. Uma pessoa não autorizada olhando para o conteúdo do disco diretamente vai somente achar dados ilegíveis que parecem randômicos.

Por exemplo, isto barra a visualização não autorizada de dados quando o computador ou disco é/está:

*   em um local com pessoas não confiáveis que podem tentar acessá-lo quando você não está por perto
*   perdido ou roubado, como ocorre com notebooks ou discos externos
*   na loja de conserto
*   descartado depois do fim de sua vida útil

Em adição, encriptação de disco pode também ser usada para adicionar alguma segurança contra tentativas não autorizadas de adulteração do sistema operacional - por exemplo, a instalação de keyloggers ou cavalos Trojan por atacantes que podem ganhar acesso físico ao sistema operacional enquanto você está fora.

**Atenção:** Criptografia de disco **não** protege seus dados de todas as ameaças.

Você ainda vai ser vulnerável a:

*   Atacantes podem entrar no seu sistema (exemplo, pela internet) depois que você já abriu e montou as partes criptografadas do disco.
*   Atacantes que conseguem acesso físico ao computador enquanto este está ligado (até mesmo se você usar um bloqueador de tela), ou um pouco *depois* que ele está ligado, se eles têm recursos para fazer um [cold boot attack](https://en.wikipedia.org/wiki/Cold_boot_attack "wikipedia:Cold boot attack").
*   Uma entidade governamental, que não somente tem recursos para facilmente fazer as coisas citadas acima como também pode simplesmente forçar você a desistir de suas chaves/senhas usando várias técnicas de [coerção](https://en.wikipedia.org/wiki/pt:Coer%C3%A7%C3%A3o "wikipedia:pt:Coerção"). Na maioria dos países não democráticos, como também no EUA e Reino Unido, pode ser legal para agências que aplicam a lei fazer isso se eles suspeitam que você pode estar escondendo algo de interesse deles.
*   [Rubber-hose cryptanalysis](https://en.wikipedia.org/wiki/Rubber-hose_cryptanalysis "wikipedia:Rubber-hose cryptanalysis"). Veja também [XKCD #538](https://xkcd.com/538/)

Uma configuração de encriptação de disco muito forte (exemplo, encriptação total de disco com autentificação e partição de boot criptografada) é necessária se deseja ter uma chance contra atacantes profissionais que podem adulterar seu sistema *antes* de você usá-lo. No entanto, não é possível prevenir todos os tipos de adulteração (exemplo, keyloggers no hardware). O melhor remédio pode ser [encriptação total de disco baseada no hardware](/index.php/Hardware-based_full-disk_encryption "Hardware-based full-disk encryption") e [Computação confiável](https://en.wikipedia.org/wiki/Trusted_Computing "wikipedia:Trusted Computing").

**Atenção:** Criptografia de disco também não vai lhe proteger contra a [limpeza de disco](/index.php/Securely_wipe_disk "Securely wipe disk"). [Backups regulares](/index.php/Backup_programs "Backup programs") são recomendados para manter seus dados seguros.

## Criptografia de dados do sistema

Apesar de que criptografar somente os dados dos usuários (normalmente dentro do diretório home, ou em uma mídia removível como DVD), ser o mais simples e menos intrusivo método, existem pontos a ponderar. Em sistemas de operacionais modernos, muitos processos podem fazer cache e guardar informações sobre dados do usuário ou partes desses dados em areas não criptografadas, como:

*   partições swap
    *   (soluções potenciais: desabilitar a troca rápida, swapping, ou usar [swap criptografada](/index.php/Encrypted_swap "Encrypted swap"))
*   `/tmp` (arquivos temporários criados pelos programas do usuário)
    *   (soluções potenciais: evite tais programas; monte `/tmp` dentro de um [ramdisk](/index.php/Ramdisk "Ramdisk"))
*   `/var` (arquivos de log e bancos de dados e semelhantes; por exemplo, [mlocate](/index.php/Mlocate_(Portugu%C3%AAs) "Mlocate (Português)") guarda um índice de todos os arquivos em `/var/lib/mlocate/mlocate.db`)

A solução é criptografar ambos o sistema e dados do usuário, prevenindo acesso físico não autorizado de dados privados. No entanto, isto vem com a desvantagem de abrir partes criptografadas do disco durante a inicialização. Outro benefício é que isto complica a instalação de malware como [keyloggers](https://en.wikipedia.org/wiki/Keystroke_logging "wikipedia:Keystroke logging") ou rootkits para alguém com acesso físico.

## Métodos disponíveis

Todos os métodos de encriptação de disco operam de tal maneira que apesar do disco ter os dados criptografados, o sistema operacional e programas "veem" isto como os dados normais correspondentes enquanto o container criptografado (exemplo, a parte lógica do disco que possui os dados criptografados) estiver "aberto" e montado.

Para isto acontecer, alguma "informação secreta" (normalmente em forma de uma keyfile e/ou senha) precisa ser dada pelo usuário, pela qual a chave de encriptação pode ser derivada (e guardada no chaveiro do kernel durante a sessão).

Se você não é familiar com este tipo de operação, leia a seção [#Como a criptografia funciona](#Como_a_criptografia_funciona) abaixo.

Os métodos de encriptação de disco podem ser separados em dois tipos, por sua camada de operação:

### Encriptação empilhada no sistema de arquivos

Soluções de encriptação empilhada no sistema de arquivos são implementadas como uma camada que se empilha em cima de um sistema de arquivos existente, causando a todos os arquivos de dado diretório sejam criptografados antes o sistema de arquivos os grave no disco. Desta maneira, os arquivos são guardados em sua forma criptografada pelo sistema de arquivos (significando que seu conteúdo, e normalmente nomes de arquivos e diretórios, são trocados por dados aparentemente randômicos de aproximadamente o mesmo tamanho), mas se não fosse por isso, eles ainda existiriam no sistema de arquivos como eles deveriam sem encriptação, como arquivos / symlinks / hardlinks / etc.

Da maneira que é implementado, o diretório que guarda os arquivos criptografados no sistema de arquivos ("diretório inferior") é aberto e montado (usando um especial pseudo sistema de arquivos empilhado) nele mesmo ou opcionalmente em outro diretório ("diretório superior"), onde os mesmos arquivos então aparecem em forma legível - até ser desmontado ou o sistema seja desligado.

Soluções disponíveis nesta categoria são [eCryptfs](/index.php/ECryptfs "ECryptfs") e [EncFS](/index.php/EncFS "EncFS").

#### Armazenamento na nuvem optimizado

Se você está fazendo encriptação empilhada no sistema de arquivos para conseguir sincronização com conhecimento-zero em locais controlados por terceiros como serviços de armazenamento na nuvem, você pode considerar alternativas ao eCryptfs e EncFS, desde que estes não são otimizados para a transmissão de arquivos pela internet. Algumas soluções que tem essa proposta são:

*   [gocryptfs](/index.php/Gocryptfs "Gocryptfs")
*   [cryptomator](https://aur.archlinux.org/packages/cryptomator/) (multiplataforma)
*   [cryfs](https://www.archlinux.org/packages/?name=cryfs)

Note que alguns serviços de armazenamento em nuvem oferecem criptografia de conhecimento-zero através de suas [aplicações cliente](/index.php/List_of_applications/Internet#Cloud_synchronization_clients "List of applications/Internet").

### Encriptação de dispositivo de bloco

Métodos de encriptação de dispositivo de bloco operam *abaixo* da camada do sistema de arquivos e garantem que tudo escrito para certo dispositivo de bloco (exemplo, todo o disco, uma partição ou um arquivo agindo como [dispositivo de loop](https://en.wikipedia.org/wiki/loop_device "wikipedia:loop device")) é criptografado. Isto significa que enquanto o dispositivo de bloco não está sendo usado, todo seu conteúdo parece com um aglomerado de dados randômicos, sem forma de determinar que tipo de sistema de arquivos e dados ele contém. O acesso dos dados é feito quando o container criptografado (nesse caso um dispositivo de bloco) está montado em uma localização arbitrária de uma maneira especial.

As seguintes soluções de "encriptação de dispositivo de bloco" estão disponíveis no Arch Linux:

	loop-AES

	loop-AES é um descendente do cryptoloop e é uma solução segura e rápida para encriptação de sistema. No entanto, loop-AES é considerado menos amigável que outras opções já que necessita de um suporte não padrão do kernel.

	dm-crypt

	[dm-crypt](/index.php/Dm-crypt_(Portugu%C3%AAs) "Dm-crypt (Português)") é o mapeador de dispositivo da funcionalidade de encriptação padrão do kernel Linux. Pode ser usado diretamente por estes que gostam de ter total controle sobre todos os aspectos da partição e chave. O gerenciamento do dm-crypt é feito com o utilitário do userspace [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup). Pode ser usado para os seguintes tipos de encriptação de dispositivo de bloco: *LUKS* (padrão), *plain*, e tem funcionalidades limitadas para dispositivos *loopAES* e *Truecrypt*.

*   LUKS, usada por padrão, é uma camada adicional de conveniência que guarda todas as informações necessárias para a configuração do dm-crypt no disco e abstrai o gerenciamento de chave e partição na tentativa de facilitar o uso e segurança da criptografia.
*   modo plain do dm-crypt, sendo uma funcionalidade original do kernel, não emprega uma camada de conveniência. É mais difícil aplicar a mesma força criptográfica a ele. Quando feito, chaves (senhas ou keyfiles) mais longas são o resultado. No entanto tem outras vantagens, como descrito em [#Encriptação de dispositivo de bloco vs encriptação empilhada no sistema de arquivos](#Encriptação_de_dispositivo_de_bloco_vs_encriptação_empilhada_no_sistema_de_arquivos).

	TrueCrypt/VeraCrypt

	Um formato portável, suporta a encriptação de todo um disco/partição ou containers de arquivos, com compatibilidade em todos os sistemas operacionais mais populares. [TrueCrypt](/index.php/TrueCrypt "TrueCrypt") foi descontinuado por seus desenvolvedores em Maio de 2014\. O fork VeraCrypt foi auditado em 2016.

Para implicações práticas da camada de operação escolhida, veja [#Encriptação de dispositivo de bloco vs encriptação empilhada no sistema de arquivos](#Encriptação_de_dispositivo_de_bloco_vs_encriptação_empilhada_no_sistema_de_arquivos) abaixo, também o artigo do [eCryptfs](https://www.systutorials.com/docs/linux/packages/ecryptfs-utils-111/ecryptfs-faq.html#compare). Veja [:Categoria:Encriptação](/index.php/Category:Encryption "Category:Encryption") para conteúdos disponíveis do métodos abaixo, como também outras ferramentas não incluídas na tabela.

### Encriptação de dispositivo de bloco vs encriptação empilhada no sistema de arquivos

| Aspecto | Encriptação de dispositivo de bloco | Encriptação empilhada no sistema de arquivos |
| Criptografa | Todo dispositivo de bloco | Arquivos |
| Container para os dados criptografados pode ser... | Uma partição ou disco / um arquivo agindo como partição virtual | Um diretório em um sistema de arquivos existente |
| Relação com sistema de arquivos | Opera abaixo da camada do sistema de arquivos: não importa se o conteúdo do dispositivo de bloco é um sistema de arquivos, uma tabela de partição, uma configuração do LVM, ou qualquer outra coisa | Adiciona uma camada adicional para um sistema de arquivos existente, para automaticamente des-/criptografar arquivos quando eles são escritos/lidos |
| Metadados do arquivo (número de arquivos, estrutura do diretório, tamanhos do arquivo, permissões, mtimes, etc.) é criptografada | ✔ | ✘
(nomes de arquivos e diretórios podem ser criptografados) |
| Pode ser usado para customizar a encriptação de todo o disco (incluindo tabelas de partições) | ✔ | ✘ |
| Pode ser usado para criptografar espaço de troca (swap) | ✔ | ✘ |
| Pode ser usado sem pré-alocar uma quantidade fixada de espaço para o container de dados criptografados | ✘ | ✔ |
| Pode ser usado para proteger sistemas de arquivos existentes sem acesso ao dispositivo de bloco, exemplo BFS ou compartilhamento do Samba, armazenamento da nuvem, etc. | ✘ | ✔ |
| Permite backups de dados criptografados baseado em arquivos | ✘ | ✔ |

### Tabela de comparação

A coluna "dm-crypt +/- LUKS" denota funcionalidades do dm-crypt para os modos de encriptação LUKS ("+") e plain ("-"). Se uma funcionalidade específica precisa do LUKS, é indicado por "(com LUKS)". De mesmo modo "(sem LUKS)" indica que o uso do LUKS é contraprodutivo para a funcionalidade e o modo plain deve ser usado.

| Sumário | Loop-AES | [dm-crypt](/index.php/Dm-crypt_(Portugu%C3%AAs) "Dm-crypt (Português)") +/- LUKS | [TrueCrypt](/index.php/TrueCrypt "TrueCrypt") | VeraCrypt | [eCryptfs](/index.php/ECryptfs "ECryptfs") | [EncFS](/index.php/EncFS "EncFS") | [gocryptfs](/index.php/Gocryptfs "Gocryptfs") | [fscrypt](/index.php/Fscrypt "Fscrypt") |
| Tipo de encriptação | dispositivo de bloco | dispositivo de bloco | dispositivo de bloco | dispositivo de bloco | empilhado no sistema de arquivos | empilhado no sistema de arquivos | empilhado no sistema de arquivos | nativo do sistema de arquivos |
| Nota | mais antigo; possivelmente o mais rápido; funciona em sistemas antigos | padrão para encriptação de dispositivo de bloco; muito flexível | muito portável, bem feito mas abandonado | fork do TrueCrypt mantido pela comunidade | um pouco mais rápido que EncFS; arquivos criptografados individuais portáveis entre sistemas | mais fácil de usar; suporta administração sem necessidade de superusuário | aspirante sucessor do EncFS | padrão para Chrome OS e Android |
| disponibilidade no Arch Linux | precisa de um kernel customizado, manualmente compilado | *módulos do kernel:* já vem com o kernel padrão; *ferramentas:* [device-mapper](https://www.archlinux.org/packages/?name=device-mapper), [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) | [truecrypt](https://www.archlinux.org/packages/?name=truecrypt) | [veracrypt](https://www.archlinux.org/packages/?name=veracrypt) | *módulos do kernel:* já vem com o kernel padrão; *ferramentas:* [ecryptfs-utils](https://www.archlinux.org/packages/?name=ecryptfs-utils) | [encfs](https://www.archlinux.org/packages/?name=encfs) | [gocryptfs](https://www.archlinux.org/packages/?name=gocryptfs) | *módulos do kernel:* já vem com o kernel padrão; *ferramentas:* [fscrypt-git](https://aur.archlinux.org/packages/fscrypt-git/) |
| Licença | GPL | GPL | TrueCrypt License 3.1 | Apache License 2.0, partes sujeitas a TrueCrypt License v3.0 | GPL | GPL | MIT | GPL (kernel), Apache 2.0 (ferramenta no userspace) |
| Encriptação implementada em... | kernelspace | kernelspace | kernelspace | kernelspace | kernelspace | userspace ([FUSE](/index.php/FUSE "FUSE")) | userspace ([FUSE](/index.php/FUSE "FUSE")) | kernelspace |
| Metadados criptográficos são guardados no... | ? | com LUKS: cabeçalho do LUKS | começo/fim do dispositivo (descriptografado) ([especificação do formato](http://www.truecrypt.org/docs/volume-format-specification)) | começo/fim do dispositivo (descriptografado) ([especificação do formato](https://www.veracrypt.fr/en/VeraCrypt%20Volume%20Format%20Specification.html)) | cabeçalho de cada arquivo criptografado | arquivo de controle no topo de cada container EncFs | ? | diretório `.fscrypt` na raiz de cada sistema de arquivos |
| Chave de encriptação criptografada é guardada no... | ? | com LUKS: cabeçalho do LUKS | começo/fim do dispositivo (descriptografado) ([format spec](http://www.truecrypt.org/docs/volume-format-specification)) | começo/fim do dispositivo (descriptografado) ([format spec](https://www.veracrypt.fr/en/VeraCrypt%20Volume%20Format%20Specification.html)) | arquivo chave pode ser guardado em qualquer lugar | arquivo chave pode ser guardado em qualquer lugar

[[1]](https://github.com/rfjakob/encfs/blob/next/encfs/encfs.pod#environment-variables)[[2]](https://github.com/vgough/encfs/issues/48#issuecomment-69301831)

 | ? | diretório `.fscrypt` na raiz de cada sistema de arquivos |
| Recursos de usabilidade | Loop-AES | dm-crypt +/- LUKS | TrueCrypt | VeraCrypt | eCryptfs | EncFs | gocryptfs | fscrypt |
| Usuários normais podem criar/destruir containers de dados criptografados | ✘ | ✘ | ✘ | ✘ | limitado | ✔ | ✔ | ✔ |
| Provê uma interface de usuário gráfica (GUI) | ✘ | ✘ | ✔ | ✔ | ✘ | ✔

[opcional](/index.php/EncFS#Gnome_Encfs_Manager "EncFS")

 | ✘ | ✘ |
| Suporte a montagem automática no login | ? | ✔ | ✔

com [systemd e /etc/crypttab](/index.php/TrueCrypt#Automounting_using_.2Fetc.2Fcrypttab "TrueCrypt")

 | ✔

com [systemd e /etc/crypttab](/index.php/TrueCrypt#Automounting_using_.2Fetc.2Fcrypttab "TrueCrypt")

 | ✔ | ✔ | ✔ | ✔ |
| Suporte a desmontagem automática em caso de inatividade | ? | ? | ? | ? | ? | ✔ | ? | ✘ |
| Funcionalidades relacionadas a segurança | Loop-AES | dm-crypt +/- LUKS | TrueCrypt | VeraCrypt | eCryptfs | EncFs | gocryptfs | fscrypt |
| Cifras suportadas | AES | AES, Anubis, CAST5/6, Twofish, Serpent, Camellia, Blowfish,… (toda cifra que a API do kernel oferece) | AES, Twofish, Serpent | AES, Twofish, Serpernt, Camellia, Kuznyechik | AES, Blowfish, Twofish... | AES, Blowfish, Twofish, e quaisquer outras cifras disponíveis no sistema | AES | AES, ChaCha12 |
| Integridade | nenhuma | opcional no LUKS2 | nenhuma | nenhuma | nenhuma | nenhuma (modo normal)
HMAC (modo paranoia) | GCM | nenhuma |
| Suporte a salting | ? | ✔
(com LUKS) | ✔ | ✔ | ✔ | ? | ✔ | ✔ |
| Suporte a múltiplas cifras encadeadas | ? | não em um dispositivo, mas dispositivos de bloco podem ser | ✔

AES-Twofish, AES-Twofish-Serpent, Serpent-AES, Serpent-Twofish-AES, Twofish-Serpent

 | ✔

AES-Twofish, AES-Twofish-Serpent, Serpent-AES, Serpent-Twofish-AES, Twofish-Serpent

 | ? | ✘ | ✘ | ✘ |
| Suporte a difusão de espaço de chave | ? | ✔
(com LUKS) | ? | ? | ? | ? | ? | ✘ |
| Proteção contra leitura de teclas | ✔ | ✔
(sem LUKS) | ? | ? | ? | ? | ? | ✘ |
| Suporte a múltiplas chaves (independentemente revogáveis) para os mesmos dados criptografados | ? | ✔
(com LUKS) | ? | ? | ? | ✘ | ? | ✔ |
| Funcionalidades relacionadas com performance | Loop-AES | dm-crypt +/- LUKS | TrueCrypt | VeraCrypt | eCryptfs | EncFs | gocryptfs | fscrypt |
| Suporte a multithreading | ? | ✔
[[3]](http://kernelnewbies.org/Linux_2_6_38#head-49f5f735853f8cc7c4d89e5c266fe07316b49f4c) | ✔ | ✔ | ? | ? | ✔ | ✔ |
| Encriptação com suporte no hardware | ✔ | ✔ | ✔ | ✔ | ✔ | ✔
[[4]](https://github.com/vgough/encfs/issues/118) | ✔ | ✔ |
| Específico para Encriptação de dispositivo de bloco | Loop-AES | dm-crypt +/- LUKS | TrueCrypt | VeraCrypt |
| Suporte para redimensionamento (manual) do dispositivo de bloco criptografado sem desmontá-lo | ? | ✔ | ✘ | ✘ |
| Específico para encriptação empilhada no sistema de arquivos | eCryptfs | EncFs | gocryptfs | fscrypt |
| Suportado pelo sistemas de arquivos | ext3, ext4, xfs (com ressalvas), jfs, nfs... | ext3, ext4, xfs (com ressalvas), jfs, nfs, cifs...

[[5]](https://github.com/vgough/encfs)

 | qualquer | ext4, F2FS, UBIFS |
| Habilidade para criptografar nomes de arquivos | ✔ | ✔ | ✔ | ✔ |
| Habilidade para *não* criptografar nomes de arquivos | ✔ | ✔ | ✘ | ✘ |
| Manuseio otimizado de arquivos espalhados | ✘ | ✔ | ✔ | ✔ |
| Compatibilidade & prevalência | Loop-AES | dm-crypt +/- LUKS | TrueCrypt | VeraCrypt | eCryptfs | EncFs | gocryptfs | fscrypt |
| Suporta versões recentes do kernel Linux | 2.0 ou mais novo | CBC-mode desde 2.6.4, ESSIV 2.6.10, LRW 2.6.20, XTS 2.6.24 | ? | ? | ? | 2.4 ou mais novo | ? | 4.1 ou mais novo |
| Dados criptografados podem ser acessados pelo Windows | ? | ? | ✔ | ✔ | ? | ✔
[[6]](https://github.com/vgough/encfs/wiki/Windows) | ✔ (porte cppcryptfs) | ✘ |
| Dados criptografados podem ser acessados pelo Mac OS X | ? | ? | ✔ | ✔ | ? | ✔
[[7]](https://sites.google.com/a/arg0.net/www/encfs-mac-build) | ✔ (em beta) | ✘ |
| Dados criptografados podem ser acessados pelo FreeBSD | ? | ? | ✔

(com VeraCrypt)

 | ✔
 | ? | ✔
[[8]](http://www.freshports.org/sysutils/fusefs-encfs/) | ? | ✘ |
| Usado por | ? | instalador do Debian/Ubuntu (encriptação de sistema)
Instalador do Fedora | ? | ? | ? | ? | ? | Android, Chrome OS |

1.  Um único arquivo pode ser usado como um container (dispositivo virtual de loop-back!) mas então não estaria mais usando o sistema de arquivos (e suas funcionalidades)

## Preparação

### Escolhendo uma configuração

Que configuração de encriptação de disco é apropriada para você vai depender de seus objetivos (leia [#Porque criptografar?](#Porque_criptografar?)) e parâmetros do sistema.

Entre outras coisas, você vai precisar responder as seguintes perguntas:

	Que tipo de "atacante" você quer se proteger?

*   Usuário casual bisbilhotando seu disco quando o sistema está desligado / foi roubado / etc.
*   Um profissional que pode ter acesso de leitura/escrita repetidamente antes ou depois de você usar o seu sistema
*   Qualquer coisa entre os dois

	O que você quer criptografar?

*   Somente dados do usuário
*   Dados do usuário e do sistema
*   Algo entre os dois

	Como swap, `/tmp`, etc. deveriam ser tratadas?

*   Ignore, e espere que nenhum dado seja vazado
*   Desabilite ou monte como ramdisk
*   Criptografar *(como parte de uma encriptação total de disco, ou separadamente)*

	Como deveriam as partes criptografadas do disco serem abertas?

*   Senhas *(como senha de login, ou separada)*
*   Keyfile *(exemplo, em um pendrive, que você mantém num local seguro ou carrega consigo)*
*   Ambas

	*Quando* deveriam as partes criptografadas do disco serem abertas?

*   Antes do processo de inicialização
*   Durante o processo de inicialização
*   No login
*   Manualmente, em demanda *(depois do login)*

	Como múltiplos usuários deveriam ser acomodados?

*   De forma alguma
*   Usando senha/chave compartilhada
*   Senhas/chaves independentes e revogáveis para a mesma parte criptografada do disco
*   Partes criptografadas do disco separadas para diferentes usuários

E então você pode fazer as escolhas técnicas necessárias (veja [#Métodos disponíveis](#Métodos_disponíveis) acima, e [#Como a criptografia funciona](#Como_a_criptografia_funciona) abaixo), de acordo com:

*   encriptação de dispositivo de bloco vs encriptação empilhada no sistema de arquivos
*   gerenciamento de chaves
*   cifra e modo de operação
*   armazenamento de metadados
*   localização do "diretório inferior" (em caso da encriptação empilhada no sistema de arquivos)

### Exemplos

Na prática, pode se tornar algo assim:

	Exemplo 1

	Encriptação simples dos dados do usuário (disco interno de armazenamento) com [EncFS](/index.php/EncFS "EncFS"), usando o diretório virtual `~/Privado` no diretório home do usuário

*   versão criptografada dos arquivos guardados no disco em `~/.Privado`
*   aberto em demanda com senha dedicada

	Exemplo 2

	Encriptação parcial do sistema no diretório home de cada usuário com [ECryptfs](/index.php/ECryptfs "ECryptfs")

*   aberto no login do respectivo usuário, usando a senha do login
*   as partições `swap` e `/tmp` são criptografadas com [Dm-crypt com LUKS](/index.php/Dm-crypt_com_LUKS "Dm-crypt com LUKS"), usando uma chave descartável gerada para a sessão automaticamente
*   indexação/cache do conteúdo do `/home` pelo *slocate* (e programas similares) desabilitada.

	Exemplo 3

	Encriptação do sistema - todo o disco rígido exceto a partição `/boot` (no entanto, `/boot` pode ser criptografada e lida pelo [GRUB](/index.php/Dm-crypt/Criptografando_todo_um_sistema#Partição_de_boot_criptografada_(GRUB) "Dm-crypt/Criptografando todo um sistema")) usando [Dm-crypt com LUKS](/index.php/Dm-crypt_com_LUKS "Dm-crypt com LUKS")

*   aberto durante a inicialização, usando senhas ou pendrive com keyfiles
*   talvez diferentes senhas/chaves por usuário - independentemente revocáveis
*   talvez criptografia em múltiplas unidades de armazenamento ou design de partições flexíveis com [LUKS dentro do LVM](/index.php/Dm-crypt/Criptografando_todo_um_sistema#LUKS_dentro_do_LVM "Dm-crypt/Criptografando todo um sistema")

	Exemplo 4

	Encriptação oculta/simples do sistema - todo o disco rígido é criptografado com [dm-crypt](/index.php/Dm-crypt_(Portugu%C3%AAs) "Dm-crypt (Português)")

*   inicialização com pelo USB, usando senha dedicada e pendrive com keyfile
*   integridade de dados checada antes de montar
*   partição de `/boot` no já mencionado pendrive

Muitas outras combinações são possíveis. Você deve escolher cuidadosamente que tipo de configuração será apropriada para seu sistema.

### Escolhendo uma senha forte

Veja [Security#Passwords](/index.php/Security#Passwords "Security").

### Preparando o disco

Antes de fazer a encriptação de disco (ou de parte dele), considere limpá-lo primeiro. Isto consiste de sobreescrever toda a unidade de armazenamento ou partição com bytes zero ou randômicos, isto é feito por uma das seguintes razões:

	Prevenir a recuperação de dados guardados anteriormente

Encriptação de disco não muda o fato de que setores são somente sobrescritos em demanda, quando o sistema de arquivos cria ou modifica os dados que estes setores guardam (veja [#Como a criptografia funciona](#Como_a_criptografia_funciona) abaixo). Setores que o sistema de arquivos considera "atualmente não usados" não são tocados, e podem ainda conter dados remanecentes. A única forma de ter certeza que todos os dados que você previamente guardou na unidade de armazenamento não podem ser recuperados [recuperados](https://en.wikipedia.org/wiki/Data_recovery "wikipedia:Data recovery"), é manualmente apagá-los. Para isso não importa se são usados bytes zero ou randômicos (apesar que a limpeza com bytes zero vai ser muito mais rápida).

	Prevenir a descoberta de padrões usados na unidade de armazenamento

Idealisticamente, toda a parte criptografada do disco não deve ser discernível de dados randômicos uniformes. Desta maneira, nenhuma pessoa não autorizada pode saber quais e quantos setores contém dados criptografados - que pode ser um objetivo desejável por si só (como parte de verdadeira confiabilidade), e também serve como uma barreira adicional contra os atacantes que tentarem quebrar a sua encriptação. Para satisfazer esse objetivo, limpar o disco com bytes randômicos de alta qualidade é crucial.

O segundo objetivo somente faz sentido em combinação com encriptação de dispositivo de bloco, no caso da encriptação empilhada no sistema de arquivos, os dados criptografados podem ser facilmente localizados (em forma de arquivos distintos no sistema de arquivos). Note também que nesse caso mesmo se você deseja criptografar um diretório específico, você vai ter que apagar toda a partição se quiser eliminar o que foi previamente guardado naquele particular diretório (devido a [fragmentação de disco](https://en.wikipedia.org/wiki/File_system_fragmentation "wikipedia:File system fragmentation")). Se tem outros diretórios na mesma partição, você vai ter de fazer o backup deles e depois mové-los de volta.

Uma vez que você decidiu que tipo de limpeza de disco deseja, veja o artigo [Securely wipe disk](/index.php/Securely_wipe_disk "Securely wipe disk") para instruções técnicas.

**Dica:** Na decisão de que método usar para apagar o disco com segurança, se lembre que isto vai ser feito somente uma vez enquanto a unidade de armazenamento estiver criptografada.

## Como a criptografia funciona

Esta seção tem como objetivo uma introdução de alto nível sobre conceitos e processos que são o coração da encriptação de disco normal.

Não vão ter detalhes matemáticos ou técnicos (consulte materiais apropriados para isso), mas deve prover a um administrador de sistemas um entendimento básico de como diferentes escolhas de configuração (especialmente sobre gerenciamento de chaves) podem afetar a usabilidade e segurança.

### Princípio básico

Para propostas da encriptação de disco, cada dispositivo de bloco (ou arquivo individual no caso de encriptação empilhada no sistema de arquivos) é dividido em **setores** de igual comprimento, por exemplo 512 bytes (4,096 bits). A encriptação/desencriptação então é feita por setores, então o nº setor do dispositivo de bloco ou arquivo no disco vai guardar a versão criptografada do nº setor dos dados originais.

Quando o sistema operacional ou um programa pede um certo fragmento de dados do dispositivo de bloco/arquivo, todos os setores (ou setor) que possuem os dados serão lidos do disco, descriptografados, e temporariamente guardados na memória:

```
           ╔═══════╗
  setor 1  ║"???.."║
           ╠═══════╣         ╭┈┈┈┈┈╮
  setor 2  ║"???.."║         ┊chave┊
           ╠═══════╣         ╰┈┈┬┈┈╯
           :       :            │
           ╠═══════╣            ▼                 ┣┉┉┉┉┉┉┉┫
  setor n  ║"???.."║━━━━━━━(descriptografar)━━━━▶┋"abc.."┋ setor n
           ╠═══════╣                              ┣┉┉┉┉┉┉┉┫
           :       :
           ╚═══════╝

           arquivo ou dispositivo de               dados não criptografados
    	   bloco criptografado no disco            na RAM

```

Similarmente, em cada operação de escrita, todos os setores que são afetados devem ser criptografados completamente de novo (enquanto o resto dos setores não são modificados).

Para ser possível de/criptografar dados, o sistema de encriptação de disco precisa saber o segredo único associado ("chave"). Quando o dispositivo de bloco ou diretório em questão é montado, sua chave correspondente (a partir de agora chamada de "chave mestre") deve ser fornecida.

A entropia da chave é de extrema importância para a segurança da encriptação. Uma string de bytes randômicamente gerada de certo comprimento, por exemplo 32 bytes (256 bits), tem propriedades desejadas mas não é praticável se lembrar e colocá-la manualmente durante a montagem.

Por este motivo, duas técnicas são usadas como auxiliares. A primeira é o programa de criptografia aumentar a propriedade de entropia da chave mestre, normalmente envolvendo uma senha separada amigável para humanos. Para diferentes tipos de criptografia a [#Tabela de comparação](#Tabela_de_comparação) lista as respectivas funcionalidades. O segundo método é criar uma keyfile com grande entropia e guardá-la num dispositivo separado do disco a ser criptografado.

Veja também [Wikipedia:Authenticated encryption](https://en.wikipedia.org/wiki/Authenticated_encryption "wikipedia:Authenticated encryption").

### Chaves, keyfiles e senhas

Os exemplos a seguir são sobre como guardar e assegurar criptograficamente uma chave mestre com uma keyfile:

	Guardada em uma keyfile de texto puro

Simplesmente guardar a chave mestre num arquivo (em forma legível) é a opção mais simples. O arquivo - chamado de "keyfile" - pode ser colocada em um pendrive que você pode manter num local seguro e somente conectá-lo no computador quando você quer montar as partes criptografadas do disco (exemplo, durante a inicialização ou login).

	Guardada e protegida por senha em uma keyfile ou no próprio disco

A chave mestre (e assim os dados criptografados) pode ser protegida com uma senha secreta, que você vai se lembrar e digitar toda vez que quiser montar o dispositivo de bloco ou diretório. Veja [#Metadados criptográficos](#Metadados_criptográficos) abaixo para detalhes.

	Randômicamente gerada para cada sessão

Em alguns casos, exemplo swap criptografada ou uma partição `/tmp`, não é necessário manter uma chave mestre persistente. Uma nova chave descartável pode ser gerada para cada sessão, sem precisar de qualquer interação do usuário. Isto significa que uma vez desmontada, todos os arquivos escritos para a partição em questão nunca podem ser descriptografados novamente por *qualquer um* - que nesse uso é perfeitamente aceitável.

### Metadados criptográficos

Normalmente, técnicas de encriptação usam funções criptográficas para aumentar a segurança da chave mestre. Na montagem do dispositivo criptografado, a senha ou keyfile é passada por estas e somente o resultado pode abrir a chave mestre para descriptografar os dados.

Uma configuração comum é aplicar a chamada "key stretching"(alongamento de chave) para a senha (com a "key derivation function"), e usar a chave resultante para descriptografar a chave mestre (que previamente foi guardada em forma criptografada):

```
 ╭┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╮                                ╭┈┈┈┈┈┈┈┈┈┈┈╮
 ┊senha de montagem ┊━━━━━⎛função de derivação ⎞━━━▶┊   chave   ┊
 ╰┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╯ ,───⎝ de chave           ⎠     ╰┈┈┈┈┈┬┈┈┈┈┈╯
 ╭──────╮            ╱                                     │
 │ salt │───────────´                                      │
 ╰──────╯                                                  │
 ╭────────────────────────────╮                            ▼         ╭┈┈┈┈┈┈┈┈┈┈┈┈┈┈╮
 │ chave mestre criptografada │━━━━━━━━━━━━━(descriptografar)━━━━━━▶┊ chave mestre ┊
 ╰────────────────────────────╯                                      ╰┈┈┈┈┈┈┈┈┈┈┈┈┈┈╯

```

A **função de derivação de chave** ("key derivation function", exemplo: PBKDF2 ou scrypt) é deliberamente lenta (aplica várias iterações de uma função hash, por exemplo: 1000 iterações do HMAC-SHA-512), fazendo ataques de força bruta não viáveis. Para o uso normal de um usuário autorizado, vai ser somente necessário calculá-la uma vez por sessão, então uma pequena espera não é um problema. Também é utilizado o aglomerado de dados, chamado "**salt**", como um argumento - este é gerado randômicamente uma vez durante a configuração da encriptação do disco e guardada (sem ser criptografada) como parte dos metadados criptográficos. Devido a ter diferentes valores por configuração, não é viável para atacantes fazer uso de tabelas pré-computadas para a função de derivação de chave.

A **chave mestre criptografada** ("encrypted master key") pode ser guardada no disco junto com os dados criptografados. Desta maneira, a confiabilidade dos dados criptografados depende da senha secreta.

Segurança adicional pode ser alcançada ao guardar a chave mestre criptografada em uma keyfile em, por exemplo, um pendrive. Isto provê **autentificação de dois fatores**: Para acessar dados criptografados é necessário algo que somente você *sabe* (a senha), e algo que somente você *tem* (a keyfile).

Outra maneira de conseguir autentificação de dois fatores é aumentar o esquema de recuperação de chave acima para "combinar" matematicamente a senha com os bytes lidos dos dados de um ou mais arquivos externos (localizado em um pendrive ou similar), antes de passá-lo para a função de derivação de chave. Os arquivos em questão podem ser qualquer coisa, exemplo, imagens JPEG normais, que podem ser benéficas para [#Negação plausível](#Negação_plausível). Apesar deles ainda serem chamados de "keyfiles" neste contexto.

Depois de derivada, a chave mestre é guardada com segurança na memória (exemplo, no chaveiro do kernel), enquanto o dispositivo de bloco ou diretório criptografado é montado.

Apesar que normalmente não é usada para des-/criptografar os dados do disco diretamente. Por exemplo, no caso da encriptação empilhada no sistema de arquivos, cada arquivo pode ser automaticamente atribuído para sua própria chave de encriptação. Quando o arquivo é lido/modificado, esta primeiro precisa ser descriptografada usando a chave mestre, antes que esta possa ser usada para de-/criptografar o conteúdo do arquivo:

```
                                     ╭┈┈┈┈┈┈┈┈┈┈┈┈╮
                                     ┊chave mestre┊
   arquivo no disco:                 ╰┈┈┈┈┈┬┈┈┈┈┈┈╯
  ┌ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┐              │
  ╎╭───────────────────────╮╎              ▼            ╭┈┈┈┈┈┈┈┈┈┈╮
  ╎│ chave do arquivo      │━━━━━━(descriptografar)━━━▶┊ chave do ┊
  ╎│ criptografada         │╎                           ┊ arquivo  ┊
  ╎╰───────────────────────╯╎                           ╰┈┈┈┈┬┈┈┈┈┈╯
  ╎┌───────────────────────┐╎                                ▼            ┌┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┐
  ╎│ conteúdo criptografado│◀━━━━━━━━━━━━━━━━(des-/criptografar)━━━━━━━▶┊ conteúdo légivel ┊
  ╎│ do arquivo            │╎                                             ┊ do arquivo       ┊
  ╎└───────────────────────┘╎                                             └┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┘
  └ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┘

```

De maneira similar, uma chave separada (exemplo, uma por diretório) pode ser usada para a encriptação de nomes de arquivos no caso de encriptação empilhada no sistema de arquivos.

No caso da encriptação do dispositivo de bloco uma chave mestre é usada por dispositivo e, consequentemente, todos os dados. Alguns métodos oferecem funcionalidades para atribuir múltiplas senhas/keyfiles para o mesmo dispositivo e outros não. Alguns usam funções mencionadas acima para aumentar a segurança da chave mestre e outros dão todo o controle da segurança da chave para o usuário. Dois exemplos são explicados pelos parâmetros criptográficos usados pelo [dm-crypt](/index.php/Dm-crypt_(Portugu%C3%AAs) "Dm-crypt (Português)") nos modos plain ou LUKS.

Ao comparar os parâmetros usados por ambos os modos, é possível observar que o modo plain tem parâmetros relacionados a localização da keyfile (exemplo, `--keyfile-size`, `--keyfile-offset`). O LUKS não precisa disso, porquê cada dispositivo de bloco contém um cabeçalho com os metadados criptográficos no início. O cabeçalho inclui a cifra usada, a chave mestre criptografada e parâmetros necessários para sua função de derivação de chave. Os últimos parâmetros resultam de opções usadas durante a encriptação inicial da chave mestre (exemplo, `--iter-time`, `--use-random`).

Para as vantagens e desvantagens, veja a [#Tabela de comparação](#Tabela_de_comparação) ou navegue páginas específicas.

Veja também:

*   [Wikipedia:Passphrase](https://en.wikipedia.org/wiki/Passphrase "wikipedia:Passphrase")
*   [Wikipedia:Key (cryptography)](https://en.wikipedia.org/wiki/Key_(cryptography) "wikipedia:Key (cryptography)")
*   [Wikipedia:Key management](https://en.wikipedia.org/wiki/Key_management "wikipedia:Key management")
*   [Wikipedia:Key derivation function](https://en.wikipedia.org/wiki/Key_derivation_function "wikipedia:Key derivation function")

### Cifras e modos de operação

O algoritmo usado para traduzir pedaços de dados criptografados e os não (chamados de "ciphertext" e "plaintext", respectivamente), que correspondem entre si de acordo com dada chave de encriptação, é chamado de "**cifra**".

Encriptação de disco emprega "cifras de bloco", que operam em um tamanho definido de bloco de dados, exemplo 16 bytes (128 bits). No tempo que este artigo foi escrito, os predominentemente usados são:

 tamanho do bloco | tamanho da chave | comentário |
| [AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard "wikipedia:Advanced Encryption Standard") | 128 bits | 128, 192 ou 256 bits | aprovado pela NSA por porteger informações do governo do EUA classificadas como "SECRET" e "TOP SECRET" (quando o tamanho de chave usado foi 192 e 256 bits) |
| [Blowfish](https://en.wikipedia.org/wiki/Blowfish_(cipher) | 64 bits | 32–448 bits | uma das primeiras cifras seguras sem patente que se tornou publicamente disponível, muito bem estabelecida no Linux |
| [Twofish](https://en.wikipedia.org/wiki/Twofish "wikipedia:Twofish") | 128 bits | 128, 192 ou 256 bits | desenvolvida como sucessora do Blowfish, mas não conseguiu tanta popularidade |
| [Serpent](https://en.wikipedia.org/wiki/Serpent_(cipher) | 128 bits | 128, 192 ou 256 bits | Considerado o finalista mais seguro de cinco competições do AES[[9]](http://csrc.nist.gov/archive/aes/round2/r2report.pdf)[[10]](https://www.cl.cam.ac.uk/~rja14/Papers/serpentcase.pdf)[[11]](https://www.cl.cam.ac.uk/~rja14/Papers/serpent.pdf). |

Criptografar (ou descriptografar) um setor ([veja acima](#Princípio_básico)) é alcançado ao dividi-lo em pequenos blocos de tamanho igual ao bloco da cifra, e seguindo um conjunto de regras (chamado de "**modo de operação**") de como consecutivamente aplicar a cifra aos blocos individuais.

Simplesmente aplicar isto para cada bloco separadamente sem modificações (apelidado como modo "*electronic codebook (ECB)*") seria inseguro, se os mesmos 16 bytes de plaintext sempre produzem os mesmos 16 bytes de ciphertext, um atacante poderia facilmente reconhecer os padrões guardados no disco.

O modo de operação mais básico (e comum) usado em prática é o "*cipher-block chaining (CBC)*". Antes da encriptação de um setor com este modo, cada bloco de dados plaintext é combinado em uma forma matemática com o ciphertext do bloco anterior. Para o primeiro bloco, já que este não tem um ciphertext anterior, um especial bloco de dados pré-gerado guardado junto com os metadados criptográficos, e chamado de "**initialization vector (IV)**"(vetor de inicialização), é usado:

```
                                   ╭──────────────╮
                                   │vetor de      │
                                   │inicialização │
                                   ╰────────┬─────╯
           ╭  ╠══════════╣        ╭─chave   │      ┣┉┉┉┉┉┉┉┉┉┉┫        
           │  ║          ║        ▼         ▼      ┋          ┋         . COMEÇO
           ┴  ║"????????"║◀━━━━(cifra)━━━━(+)━━━━━┋"Hello, W"┋ bloco  ╱╰────┐
   setor n do ║          ║                         ┋          ┋ 1      ╲╭────┘
   arquivo ou ║          ║──────────────────╮      ┋          ┋         ' 
   dispositivo╟──────────╢        ╭─chave   │      ┠┈┈┈┈┈┈┈┈┈┈┨
           ┬  ║          ║        ▼         ▼      ┋          ┋
           │  ║"????????"║◀━━━━(cifra)━━━━(+)━━━━━┋"orld !!!"┋ bloco
           │  ║          ║                         ┋          ┋ 2
           │  ║          ║──────────────────╮      ┋          ┋
           │  ╟──────────╢                  │      ┠┈┈┈┈┈┈┈┈┈┈┨
           │  ║          ║                  ▼      ┋          ┋
           :  :   ...    :        ...      ...     :   ...    : ...

              texto cifrado                         texto puro
                no disco                              na RAM

```

Para descriptografar o procedimento é o revertido analogamente.

Uma coisa legal de se notar é a geração do único vetor de inicialização para cada setor. A escolha mais simples é calcular isto em um jeito preditivo de um valor prontamente disponível como o número do setor. No entanto, isso permite que um atacante com repetidos acessos ao sistema faça o chamado [watermarking attack](https://en.wikipedia.org/wiki/Watermarking_attack "wikipedia:Watermarking attack"). Para prevenir isto, um método chamado "Encrypted salt-sector initialization vector (**ESSIV**)" pode ser usado para gerar os vetores de inicialização de uma maneira que o faz parecer completamente randômica para um atacante em potencial.

Existem outros, mais complicados, modos de operação disponíveis para a encriptação de disco, que já oferecem nativamente segurança contra tais ataques (e não precisam do ESSIV). Alguns também podem garantir autentificação dos dados criptografados (exemplo, confirmar que não foi modificado/corrompido por alguém que não tem acesso a chave).

Veja também:

*   [Wikipedia:Disk encryption theory](https://en.wikipedia.org/wiki/Disk_encryption_theory "wikipedia:Disk encryption theory")
*   [Wikipedia:Block cipher](https://en.wikipedia.org/wiki/Block_cipher "wikipedia:Block cipher")
*   [Wikipedia:Block cipher modes of operation](https://en.wikipedia.org/wiki/Block_cipher_modes_of_operation "wikipedia:Block cipher modes of operation")

### Negação plausível

Veja [Wikipedia:Plausible deniability](https://en.wikipedia.org/wiki/Plausible_deniability "wikipedia:Plausible deniability").