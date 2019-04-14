**Status de tradução:** Esse artigo é uma tradução de [Ext4](/index.php/Ext4 "Ext4"). Data da última tradução: 2019-04-08\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Ext4&diff=0&oldid=565570) na versão em inglês.

Artigos relacionados

*   [Sistemas de arquivos](/index.php/File_systems "File systems")
*   [Ext3](/index.php/Ext3 "Ext3")

De [Ext4 - Linux Kernel Newbies](http://kernelnewbies.org/Ext4) (traduzido):

	Ext4 é a evolução do sistema de arquivos mais usado no Linux, o Ext3\. De diversas formas, o Ext4 é uma melhoria mais profunda sobre Ext3 do que o Ext3 foi sobre Ext2\. O Ext3 foi principalmente sobre adicionar *journaling* ao Ext2, mas o Ext4 modifica estruturas de dados importantes do sistema de arquivos como aqueles projetados para armazenar os dados de arquivos. O resultado é um sistema de arquivos com um desenho melhorado, melhor desempenho, confiabilidade e recursos.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Criando um novo sistema de arquivos ext4](#Criando_um_novo_sistema_de_arquivos_ext4)
    *   [1.1 Proporção de bytes por nó-i](#Proporção_de_bytes_por_nó-i)
    *   [1.2 Blocos reservados](#Blocos_reservados)
*   [2 Migrando de ext2/ext3 para ext4](#Migrando_de_ext2/ext3_para_ext4)
    *   [2.1 Montando partições ext2/ext3 como ext4 sem conversão](#Montando_partições_ext2/ext3_como_ext4_sem_conversão)
        *   [2.1.1 Motivo](#Motivo)
        *   [2.1.2 Procedimento](#Procedimento)
    *   [2.2 Convertendo partições ext2/ext3 para ext4](#Convertendo_partições_ext2/ext3_para_ext4)
        *   [2.2.1 Motivo](#Motivo_2)
        *   [2.2.2 Procedimento](#Procedimento_2)
*   [3 Melhorando o desempenho](#Melhorando_o_desempenho)
    *   [3.1 E4rat](#E4rat)
    *   [3.2 Desabilitando atualização de tempo de acesso](#Desabilitando_atualização_de_tempo_de_acesso)
    *   [3.3 Aumentando o intervalo de commit](#Aumentando_o_intervalo_de_commit)
    *   [3.4 Desligando barreiras](#Desligando_barreiras)
    *   [3.5 Desabilitando journaling](#Desabilitando_journaling)
    *   [3.6 Use journal externo para otimizar o desempenho](#Use_journal_externo_para_otimizar_o_desempenho)
*   [4 Dicas e truques](#Dicas_e_truques)
    *   [4.1 Usando criptografia baseada em arquivos](#Usando_criptografia_baseada_em_arquivos)
        *   [4.1.1 Habilitar em um sistema de arquivos existente](#Habilitar_em_um_sistema_de_arquivos_existente)
        *   [4.1.2 Uso](#Uso)
    *   [4.2 Habilitando somas de verificação de metadados](#Habilitando_somas_de_verificação_de_metadados)
        *   [4.2.1 Novo sistema de arquivos](#Novo_sistema_de_arquivos)
        *   [4.2.2 Converter arquivo de sistema existente](#Converter_arquivo_de_sistema_existente)
*   [5 Veja também](#Veja_também)

## Criando um novo sistema de arquivos ext4

Para formatar uma partição, faça:

```
# mkfs.ext4 /dev/*partição*

```

**Dica:**

*   Veja [mke2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mke2fs.8) para mais opções; edite `/etc/mke2fs.conf` para ver/configurar as opções padrões.
*   Se houver suporte, você pode querer habilitar suporte a 64-bits e [metadados de somas de verificação](#Habilitando_somas_de_verificação_de_metadados) (também conhecidos como *checksums*).

### Proporção de bytes por nó-i

Traduzido de [mke2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mke2fs.8):

	***mke2fs** cria um nó-i para todos os* bytes por nó-i *de espaço no disco. Quanto maior proporção de* bytes por nó-i*, menos nós-i serão criados.*

A criação de um novo arquivo, diretório, link simbólico etc. exige pelo menos um [nó-i](https://en.wikipedia.org/wiki/pt:N%C3%B3-i "wikipedia:pt:Nó-i") livre. Se a contagem de nós-i for pequena demais, nenhum arquivo pode ser criado no sistema de arquivos mesmo se ainda houver espaço restante nele.

Porque não é possível alterar a proporção de bytes por nó-i ou a contagem de nós-i após o sistema de arquivos ser criado, o `mkfs.ext4` usa, por padrão, uma proporção relativamente baixa de um nó-i a cada 16384 bytes (16 KB) para evitar essa situação.

Porém, para partições com tamanho em centenas ou milhares de GB e tamanho de arquivo médio na faixa de megabytes, isso geralmente resulta em um número muito grande de nós-i porque o número de arquivos criados nunca alcança o número de nós-i.

Isso resulta em um desperdício de espaço em disco, porque todos arquivos nós-i não usados ocupam até 256 bytes no sistema de arquivos (isso também é definido em `/etc/mke2fs.conf`, mas não deve ser alterado). 256 * vários milhões = alguns poucos gigabytes desperdiçados em nós-i não usados.

Essa situação pode ser avaliada comparando as figuras `{I}Uso%` fornecidas pelo `df` e `df -i`:

 `$ df -h /home` 
```
Sist. Arq.              Tam.   Usado   Dispo.  **Uso%**  Montado em
/dev/mapper/lvm-home    115G    56G    59G     **49%**   /home

```
 `$ df -hi /home` 
```
Sist. Arq.              Inodes IUsado ILivre **IUso%**   Montado em
/dev/mapper/lvm-home    1.8M    1.1K   1.8M   **1%**     /home

```

Para especificar uma proporção de bytes por nó-i diferente, você pode usar a opção `-T *tipo-de-uso*` que sugere o uso esperado do sistema de arquivos usando tipos definidos em `/etc/mke2fs.conf`. Além daqueles tipos estão os `largefile` e `largefile4` maiores, que oferecem proporções mais relevantes de um nó-i a cada 1 MB e 4 MB, respectivamente. Pode-se usar da seguinte forma:

```
# mkfs.ext4 -T largefile /dev/*dispositivo*

```

A proporção de bytes por nó-i também pode ser definida diretamente via a opção `-i`: *p.ex.:* use `-i 2097152` para uma proporção 2 MB e `-i 6291456` para uma proporção 6 MB.

**Dica:** Por outro lado, se você está configurando uma partição dedicada a hospedar milhões de arquivos pequenos, como e-mails e itens de newsgroups, você pode usar valores menores de *tipo-de-uso* como `news` (um nó-i para cada 4096 bytes) ou `small` (idem, somado a tamanhos de bloco e nó-i menores).

**Atenção:** Se você faz uso intenso de links simbólicos, certifique-se de manter a contagem de nós-i alta o suficiente com uma proporção baixa de bytes por nó-i, porque, apesar de não usar muito espaço, todo novo link simbólico consume um novo nó-i e, portanto, o sistema de arquivos pode esgotá-los rapidamente.

### Blocos reservados

Por padrão, 5% dos blocos de sistema de arquivos serão reservados para o superusuário, para evitar fragmentação e "*permitir daemons do root continuarem a funcionar corretamente após processos sem privilégios serem impedidos de escrever no sistema de arquivos*" (traduzido de [mke2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mke2fs.8)).

Para discos modernos de alta capacidade, isso é mais alto do que necessário se a partição for usada como um arquivo de longo prazo ou não crucial para operações do sistema (como `/home`). Veja [esse e-mail](http://www.redhat.com/archives/ext3-users/2009-January/msg00026.html) para a opinião do desenvolvedor do ext4 Ted Ts'o sobre blocos reservados.

Geralmente é seguro reduzir a percentagem de blocos reservados para liberar espaço de disco quando a partição é:

*   Grande demais (por exemplo > 50G); ou
*   Usado como arquivo de longo prazo, isto é, onde arquivos não serão excluídos e criados com muita frequência

A opção `-m` de utilitários relacionados ao ext4 permitem especificar a percentagem de blocos reservados.

Para impedir totalmente de reservar blocos na criação do sistema de arquivos, use:

```
# mkfs.ext4 -m 0 /dev/*dispositivo*

```

Para reduzi-lo para 1% posteriormente, use:

```
# tune2fs -m 1 /dev/*dispositivo*

```

Você pode usar [findmnt(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/findmnt.8) para localizar o nome do dispositivo:

```
$ findmnt */o/ponto/de/montagem*

```

## Migrando de ext2/ext3 para ext4

### Montando partições ext2/ext3 como ext4 sem conversão

#### Motivo

Um compromisso entre a conversão total para ext4 e simplesmente permanecer com ext2/ext3 é montar as partições como ext4.

**Vantagens:**

*   Compatibilidade (o sistema de arquivos pode continuar sendo montado como ext3) – Isso permite que os usuários ainda leiam o sistema de arquivos de outros sistemas operacionais sem suporte a ext4 (por exemplo, o Windows com drivers ext2/ext3)
*   Melhor desempenho (embora não tanto como uma partição ext4 totalmente convertida).[[1]](http://kernelnewbies.org/Ext4) [[2]](http://events.linuxfoundation.org/slides/2010/linuxcon_japan/linuxcon_jp2010_fujita.pdf)

**Desvantagens:**

*   Menos recursos do ext4 são usados (apenas aqueles que não alteram o formato do disco, como a alocação de múltiplos blocos e a alocação atrasada)

**Nota:** Exceto pela novidade relativa do ext4 (que pode ser visto como um risco), **não há nenhuma desvantagem importante para esta técnica**.

#### Procedimento

1.  Edite `/etc/fstab` e altere o 'type' de ext2/ext3 para ext4 para quaisquer partições você gostaria de montar como ext4.
2.  Monte novamente as partições afetadas.

### Convertendo partições ext2/ext3 para ext4

#### Motivo

Para experimentar os benefícios do ext4, um processo de conversão irreversível deve ser concluído.

**Vantagens:**

*   Desempenho melhorado e novos recursos.[[3]](http://kernelnewbies.org/Ext4) [[4]](http://events.linuxfoundation.org/slides/2010/linuxcon_japan/linuxcon_jp2010_fujita.pdf)

**Desvantagens:**

*   As partições que contêm principalmente arquivos estáticos, como uma partição `/boot`, podem não se beneficiar dos novos recursos. Além disso, adicionar um journal (que está implícito ao mover uma partição ext2 para ext3/4) sempre incorre em despesas extras ao custo de desempenho.
*   Irreversível (as partições ext4 não podem ser "rebaixadas" para ext2/ext3\. No entanto, é compatível com versões anteriores até que a extensão e outras opções exclusivas estejam habilitadas)

#### Procedimento

Essas instruções foram adaptadas da [documentação do Kernel](http://ext4.wiki.kernel.org/index.php/Ext4_Howto) e um [tópico do BBS](https://bbs.archlinux.org/viewtopic.php?id=61602).

**Atenção:**

*   Se você converter o sistema de arquivos raiz do sistema, certifique-se de que o initramfs reserva ('fallback') está disponível na reinicialização. Alternativamente, adicione `ext4` de acordo com [Mkinitcpio#MODULES](/index.php/Mkinitcpio#MODULES "Mkinitcpio") e [gere novamente o initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs") antes de iniciar.
*   Se você decidir converter uma partição `/boot` separada, certifique-se que o [gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot") oferece inicialização do ext4.

Nas etapas a seguir, `/dev/sdxX` denota o caminho para a partição a ser convertida, tal como `/dev/sda1`.

1.  **[Faça backup](/index.php/Backup_programs "Backup programs")** de todos os dados em quaisquer partições ext3 que serão convertidas para ext4\. Um pacote útil, especialmente para partições raiz, é o [clonezilla](https://www.archlinux.org/packages/?name=clonezilla).
2.  Edite `/etc/fstab` e altere o 'type' de ext3 para ext4 para quaisquer partições que serão convertidos para ext4.
3.  Inicialize uma mídia *Live* (se necessário). O processo de conversão com [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) deve ser feito quando a unidade não está montada. Se estiver convertendo uma partição raiz, a forma mais simples de alcançar isso é inicializar de alguma outra mídia *Live*.
4.  Certifique-se que a partição *não* está montada.
5.  Se você quiser converter uma partição ext2, a primeira etapa de conversão é adicionar um [journal](/index.php/File_systems#Journaling "File systems") executando `tune2fs -j /dev/sdxX` como root; fazendo dela uma partição ext3.
6.  Execute `tune2fs -O extent,uninit_bg,dir_index /dev/sdxX` como root. Esse comando converte o sistema de arquivos ext3 para ext4 (irreversivelmente).
7.  Execute `fsck -f /dev/sdxX` como root.
    *   Esta etapa é necessário, do contrário o sistema de arquivos **ficará ilegível**. A execução de *fsck* é necessária para retornar o sistema de arquivos para um estado consistente. Ele vai encontrar erros de soma de verificação nos descritores de grupo - isso é esperado. A opção `-f` pede que o *fsck* verifique mesmo se o sistema de arquivos parecer limpo. A opção `-p` pode ser usada sobre a "reparação automática" (do contrário, o usuário será solicitado inserir para cada erro).
8.  Recomendado: monte a partição e execute `e4defrag -c -v /dev/sdxX` como root.
    *   Mesmo que o sistema de arquivos agora esteja convertido em ext4, todos os arquivos que foram escritos antes da conversão ainda não aproveitam a opção de extensão do ext4, que melhorará o desempenho de arquivos grandes e reduzirá a fragmentação e o tempo de verificação do sistema de arquivos. Para aproveitar plenamente o ext4, todos os arquivos teriam que ser reescritos no disco. Use *e4defrag* para cuidar desse problema.
9.  Reinicie

## Melhorando o desempenho

### E4rat

[E4rat](/index.php/E4rat "E4rat") é um aplicativo de pré-carregamento projetado para o sistema de arquivos ext4\. Ele monitora os arquivos abertos durante a inicialização, otimiza seu posicionamento na partição para melhorar o tempo de acesso e os pré-carrega no começo do processo de inicialização. *E4rat* não oferece melhorias com [SSDs](/index.php/SSD "SSD"), cujo tempo de acesso é insignificante em comparação com discos rígidos.

### Desabilitando atualização de tempo de acesso

O sistema de arquivos *ext4* registra informações sobre quando um arquivo foi acessado pela última vez e há um custo associado ao registro dele. Com a opção `noatime`, os timestamps de acesso no sistema de arquivos não são atualizados.

 `/etc/fstab` 
```
/dev/sda5    /    ext4    defaults,**noatime**    0    1

```

Fazer isso quebra aplicativos que dependem do tempo de acesso, veja [fstab#atime options](/index.php/Fstab#atime_options "Fstab") para soluções possíveis.

### Aumentando o intervalo de commit

O intervalo de sincronização para dados e metadados pode ser aumentado, proporcionando um maior atraso de tempo para a opção `commit`.

O 5 segundos padrão significa que, se a energia for perdida, será perdido tanto quanto os últimos 5 segundos de trabalho. Isso força uma sincronia completa de todos os dados/journals para mídia física a cada 5 segundos. O sistema de arquivos não será danificado, graças ao registro no journaling. O seguinte [fstab](/index.php/Fstab "Fstab") ilustra o uso de `commit`:

 `/etc/fstab`  `/dev/sda5    /    ext4   defaults,noatime,**commit=60**    0    1` 

### Desligando barreiras

**Atenção:** Desabilitar as barreiras para discos sem cache com respaldo de bateria não é recomendado e pode levar à corrupção severa do sistema de arquivos e perda de dados.

*Ext4* permite barreiras de gravação por padrão. Isso garante que os metadados do sistema de arquivos sejam corretamente escritos e ordenados no disco, mesmo quando os caches de gravação perdem energia. Isso ocorre com um custo de desempenho especialmente para aplicativos que usam *fsync* intensamente ou criam e excluem muitos pequenos arquivos. Para discos que tenham um cache de gravação com respaldo de bateria de uma forma ou de outra, desabilitar as barreiras pode melhorar o desempenho com segurança.

Para desligar as barreiras, adicione a opção `barrier=0` ao sistema de arquivos desejado. Por exemplo:

 `/etc/fstab`  `/dev/sda5    /    ext4    noatime,**barrier=0**   0    1` 

### Desabilitando journaling

**Atenção:** Usar um sistema de arquivos sem o journal pode resultar em perda de dados em caso de desmontagem repentina, como falha de energia ou bloqueio do kernel.

Desabilitar o journal do *ext4* pode ser feito com o seguinte comando em um disco desmontado:

```
# tune2fs -O "^has_journal" /dev/sdXN

```

### Use journal externo para otimizar o desempenho

Para aqueles com preocupações sobre integridade e desempenho de dados, o registro no jornal pode ser significativamente acelerado com a opção de montagem `journal_async_commit`. Note que [não funciona](https://patchwork.ozlabs.org/patch/414750/) com o padrão balanceado de `data=ordered`, então isso é recomendado apenas quando o sistema de arquivos já estiver usando `data=journal` cautelosamente.

Você pode formatar um dispositivo dedicado para o journal com `mke2fs -O journal_dev /dev/journal_device`. Use `tune2fs -J device=/dev/journal_device /dev/ext4_fs` para atribuir o journal a um dispositivo existente ou substitua `tune2fs` por `mkfs.ext4` se você estiver criando um novo sistema de arquivos.

## Dicas e truques

### Usando criptografia baseada em arquivos

**Nota:** O ext4 proíbe criptografar o diretório raiz (`/`) e vai produzir um erro no [kernel](/index.php/Kernel "Kernel") 4.13 o posterior [[5]](https://patchwork.kernel.org/patch/9787619/) [[6]](https://www.phoronix.com/scan.php?page=news_item&px=EXT4-Linux-4.13-Work).

O ext4 oferece suporte a criptografia baseada em arquivos. Em uma árvore de diretórios marcada para criptografia, o conteúdo de arquivo, nomes de arquivos e alvos de links simbólicos são criptografados. As chaves de criptografia são armazenadas no chaveiro do kernel. Veja também a entrada do [blog do Quarkslab](http://blog.quarkslab.com/a-glimpse-of-ext4-filesystem-level-encryption.html) com um registro do recurso, uma visão geral do estado de implementação e resultados de testes práticos com o kernel 4.1.

A criptografia depende da opção do kernel `CONFIG_EXT4_ENCRYPTION`, que está habilitada por padrão, bem como o comando *e4crypt* do pacote [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs).

Uma condição prévia é que o sistema de arquivos esteja usando um tamanho de bloco suportado para criptografia:

 `# tune2fs -l /dev/*dispositivo* | grep 'Block size'` 
```
Block size:               4096

```
 `# getconf PAGE_SIZE` 
```
4096

```

Se esses valores não forem os mesmos, o sistema de arquivos não terá suporte à criptografia e você **não deve continuar**.

**Atenção:** Assim que a opção de recurso de criptografia estiver ativado, os kernels anteriores a 4.1 não conseguirão montar o sistema de arquivos.

#### Habilitar em um sistema de arquivos existente

Para habilitar a opção do recurso de criptografia em seu sistema de arquivos:

```
# tune2fs -O encrypt /dev/*dispositivo*

```

**Dica:** A operação pode ser revertida com `debugfs -w -R "feature -encrypt" /dev/*dispositivo*`. Execute [fsck](/index.php/Fsck "Fsck") antes e depois para garantir a integridade do sistema de arquivos.

#### Uso

Para fazer um diretório criptografado:

```
$ mkdir *cofre*

```

**Nota:**

*   A criptografia só pode ser aplicada a um diretório vazio. Novos arquivos e subdiretórios dentro de um diretório criptografado herdam sua política de criptografia. A criptografia de arquivos já existentes ainda não é suportada.
*   Aplicativos que precisam de acesso a um diretório criptografado que está bloqueado (p.ex., na inicialização) podem falhar.

Gere e adicione uma nova chave ao chaveiro dos usuários. Este passo deve ser repetido toda vez que você descarrega o seu chaveiro (p.ex., ao encerrar a sessão ou reiniciar):

 `$ e4crypt add_key` 
```
Enter passphrase (echo disabled): 
Added key with descriptor [f88747555a6115f5]

```

**Dica:** Por padrão, a chave é armazenada no [session-keyring](http://man7.org/linux/man-pages/man7/session-keyring.7.html), veja [e4crypt(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/e4crypt.8#COMMANDS). No entanto, é possível especificar um chaveiro diferente usando `-k`. Alternativas úteis podem incluir [user-keyring](http://man7.org/linux/man-pages/man7/user-keyring.7.html) e [user-session-keyring](http://man7.org/linux/man-pages/man7/user-session-keyring.7.html), por exemplo para usar o user-keyring:
```
$ e4crypt add_key -k @u

```

**Atenção:** Se você esqueceu sua senha, não haverá outra maneira de descriptografar seus arquivos. Também não é possível alterar uma senha depois de ter sido configurada.

**Nota:** Para ajudar a evitar [ataques de dicionário](https://en.wikipedia.org/wiki/Dictionary_attack aleatório é gerado automaticamente e armazenado no superbloco de sistema de arquivos ext4\. A senha *e* o sal são usados para derivar a chave de criptografia real. Como consequência disso, se você tiver vários sistemas de arquivos ext4 com criptografia habilitada montados, então `e4crypt add_key` adicionará várias chaves, uma por sistema de arquivos. Embora qualquer chave possa ser usada em qualquer sistema de arquivos, seria sábio usar apenas, em um determinado sistema de arquivos, chaves usando o sal do sistema de arquivos. Caso contrário, você corre o risco de não conseguir descriptografar arquivos no sistema de arquivos A se o sistema de arquivos B estiver desmontado. Alternativamente, você pode usar a opção `-S` para `e4crypt add_key` para especificar um sal você mesmo.

Certifique-se que o descritor de chave está no chaveiro de sessão:

 `$ keyctl show` 
```
Session Keyring
1021618178 --alswrv   1000  1000  keyring: _ses
 176349519 --alsw-v   1000  1000   \_ logon: ext4:**f88747555a6115f5**

```

Atribua uma chave de descritor para uma política de criptografia no diretório:

```
$ e4crypt set_policy *f88747555a6115f5* *cofre*

```

O diretório *cofre* deve agora ser acessível e legível para o usuário atual desde que a chave esteja no chaveiro do usuário.

Se alguém tentar acessar *cofre* sem adicionar a chave primeiro no chaveiro do usuário, os nomes de arquivos e seus conteúdos serão vistos como mensagens sem criptografia.

Para obter (novamente) acesso ao diretório, basta adicionar a chave ao chaveiro do usuário:

 `$ e4crypt add_key` 
```
Enter passphrase (echo disabled): *senha_fornecida*
Added key with descriptor [f88747555a6115f5]

```

**Atenção:** O início de sessão efetua o desbloqueio automático de diretórios de usuário criptografados por esse método ao usar o login do GDM ou do console.

**Nota:** Por motivos de segurança, arquivos não criptografados não podem existir em um diretório criptografado. Como tal, tentar mover (`mv`) arquivos não criptografados para um diretório criptografado vai

*   falhar, se ambos os diretórios estiverem no mesmo ponto de montagem do sistema de arquivos. Isso acontece porque *mv* só atualizará o índice de diretórios para apontar para o novo diretório, mas não os nós-i de dados do arquivo (que contém a referência criptográfica).
*   ter sucesso, se ambos os diretórios estiverem em diferentes pontos de montagem do sistema de arquivos (novos nós-i de dados são criados).

Em ambos os casos, é melhor copiar os arquivos (`cp`), porque isso deixa a opção para excluir com segurança o original não criptografado com *shred* ou uma ferramenta similar.

### Habilitando somas de verificação de metadados

Quando um sistema de arquivos foi criado com o [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) 1.44 ou posterior, as somas de verificação de metadados já devem estar ativadas por padrão. Os sistemas de arquivos existentes podem ser convertidos para permitir o suporte à soma de verificação de metadados.

Se o seu CPU tem suporte a SSE 4.2, certifique-se que o [módulo do kernel](/index.php/Kernel_module "Kernel module") `crc32c_intel` esteja carregado para habilitar o algoritmo CRC32C acelerado por hardware [[7]](https://ext4.wiki.kernel.org/index.php/Ext4_Metadata_Checksums#Benchmarking). Caso contrário, você precisará carregar o módulo `crc32c_generic`.

Para ler mais sobre metadados de somas de verificação, veja o [wiki do ext4](https://ext4.wiki.kernel.org/index.php/Ext4_Metadata_Checksums).

**Dica:** Use `dump2fs` para verificar os recursos que estão habilitados no sistema de arquivos:
```
# dumpe2fs */dev/caminho/para/disco*

```

#### Novo sistema de arquivos

Para habilitar o suporte a somas de verificação de metadados ext4 ao criar um novo sistema de arquivos.

```
# mkfs.ext4 -O metadata_csum */dev/caminho/para/disco*

```

#### Converter arquivo de sistema existente

**Nota:** Um sistema de arquivos não deve estar montado.

Primeiro, a partição precisa ser verificada e otimizada usando `e2fsck`:

```
# e2fsck -Df */dev/caminho/para/disco*

```

Converta o sistema de arquivos para 64 bits:

```
# resize2fs -b */dev/caminho/para/disco*

```

Finalmente, habilite suporte a somas de verificação:

```
# tune2fs -O metadata_csum */dev/caminho/para/disco*

```

## Veja também

*   [Wiki oficial do Ext4](https://ext4.wiki.kernel.org/)
*   [Layout de disco com Ext4](https://ext4.wiki.kernel.org/index.php/Ext4_Disk_Layout) descrito no seu wiki
*   [Criptografia no Ext4](http://lwn.net/Articles/639427/) - artigo do LWN
*   Commits do kernel para criptografia no ext4 [[8]](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=6162e4b0bedeb3dac2ba0a5e1b1f56db107d97ec) [[9]](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=8663da2c0919896788321cd8a0016af08588c656)
*   [Changelog do e2fsprogs](http://e2fsprogs.sourceforge.net/e2fsprogs-release.html)
*   [Somas de verificação de metadados do Ext4](https://ext4.wiki.kernel.org/index.php/Ext4_Metadata_Checksums)