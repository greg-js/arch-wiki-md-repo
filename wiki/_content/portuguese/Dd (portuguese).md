**Status de tradução:** Esse artigo é uma tradução de [dd](/index.php/Dd "Dd"). Data da última tradução: 2019-07-27\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Dd&diff=0&oldid=578145) na versão em inglês.

Artigos relacionados

*   [Clonagem de disco](/index.php/Clonagem_de_disco "Clonagem de disco")
*   [Mídia de instalação em flash USB#Usando dd](/index.php/M%C3%ADdia_de_instala%C3%A7%C3%A3o_em_flash_USB#Usando_dd "Mídia de instalação em flash USB")
*   [Benchmarking#dd](/index.php/Benchmarking#dd "Benchmarking")

[dd](https://en.wikipedia.org/wiki/dd_(Unix) é um dos [utilitários principais](/index.php/Utilit%C3%A1rios_principais "Utilitários principais") cujo propósito primário é converter e copiar um arquivo.

Similarmente ao *cp*, o *dd* faz, por padrão, uma cópia bit a bit do arquivo, mas com recursos de controle de fluxo de E/S de nível inferior.

Para mais informações, consulte [dd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dd.1) ou a [documentação completa](https://www.gnu.org/software/coreutils/dd).

**Dica:** Por padrão, *dd* não produz nada até que a tarefa seja finalizada. Para monitorar o progresso da operação, adicione a opção `status=progress` ao comando.

**Atenção:** Deve-se ter extrema cautela ao usar o *dd*, como em qualquer comando desse tipo, ele pode destruir dados irreversivelmente.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Clonagem e restauração de disco](#Clonagem_e_restauração_de_disco)
    *   [2.1 Clonando uma partição](#Clonando_uma_partição)
    *   [2.2 Clonando todo um disco rígido](#Clonando_todo_um_disco_rígido)
    *   [2.3 Fazer backup da tabela de partição](#Fazer_backup_da_tabela_de_partição)
    *   [2.4 Criar imagem de disco](#Criar_imagem_de_disco)
    *   [2.5 Restaurar o sistema](#Restaurar_o_sistema)
*   [3 Aplicação de patch em arquivo binário](#Aplicação_de_patch_em_arquivo_binário)
*   [4 Fazer backup e restaurar MBR](#Fazer_backup_e_restaurar_MBR)
    *   [4.1 Remover o gerenciador de boot](#Remover_o_gerenciador_de_boot)

## Instalação

*dd* é parte do GNU [coreutils](https://www.archlinux.org/packages/?name=coreutils). Para outros utilitários no pacote, por favor, confira [Utilitários principais](/index.php/Utilit%C3%A1rios_principais "Utilitários principais").

## Clonagem e restauração de disco

O comando *dd* é uma ferramenta simples, mas versátil e poderosa. Ele pode ser usado para copiar da origem para o destino, bloco por bloco, independentemente de seus tipos de sistema de arquivos ou sistemas operacionais. Um método conveniente é usar *dd* em um ambiente *live*, como em um Live CD.

**Atenção:** Assim como com qualquer comando desse tipo, você deve ter muita cautela ao usá-lo; pode destruir dados. Lembre-se da ordem do arquivo de entrada (`if=`) e do arquivo de saída (`of=`) e não os inverta! Certifique-se sempre de que a unidade ou partição de destino (`of=`) seja de tamanho igual ou maior que a origem (`if=`).

### Clonando uma partição

Do disco físico `/dev/sda`, partição 1, para disco físico `/dev/sdb`, partição 1:

```
# dd if=/dev/sda1 of=/dev/sdb1 bs=64K conv=noerror,sync status=progress

```

**Nota:** Tenha cuidado se a partição de saída `of` (`sdb1` no exemplo) não existir, *dd* criará um arquivo com este nome e começará a encher seu sistema de arquivos raiz.

### Clonando todo um disco rígido

Do disco físico `/dev/sda` para um disco físico `/dev/sdb`:

```
# dd if=/dev/sda of=/dev/sdb bs=64K conv=noerror,sync status=progress

```

Isso irá clonar a unidade inteira, incluindo o MBR (e, portanto, o gerenciador de boot), todas as partições, UUIDs e dados.

*   `bs=` define o tamanho do bloco. O padrão é 512 bytes, que é o tamanho de bloco "clássico" para discos rígidos desde o início dos anos 80, mas não é o mais conveniente. Use um valor maior, 64K ou 128K. Além disso, leia o aviso abaixo, porque há mais do que apenas "tamanhos de bloco" - também influencia a maneira como os erros de leitura se propagam. Veja [[1]](http://www.mail-archive.com/eug-lug@efn.org/msg12073.html) e [[2]](http://blog.tdg5.com/tuning-dd-block-size/) para detalhes e para descobrir o melhor valor de bs para o seu caso de uso.
*   `noerror` instrui o *dd* a continuar a operação, ignorando todos os erros de leitura. O comportamento padrão para *dd* é parar em qualquer erro.
*   `sync` preenche os blocos de entrada com zeros se houver algum erro de leitura, para que os deslocamentos de dados permaneçam em sincronia.
*   `status=progress` mostra estatísticas de transferência periódicas que podem ser usadas para estimar quando a operação pode estar completa.

**Nota:** O tamanho do bloco que você especifica influencia como os erros de leitura são manipulados. Leia abaixo. Para recuperação de dados, use [ddrescue](/index.php/Clonagem_de_disco#Usando_ddrescue "Clonagem de disco").

O utilitário *dd* tecnicamente possui um "tamanho de bloco de entrada" (IBS) e um "tamanho de bloco de saída" (OBS). Quando você define `bs`, você efetivamente define IBS e OBS. Normalmente, se o tamanho do bloco for, digamos, 1 MiB, o *dd* lerá 1024×1024 bytes e gravará essa mesma quantidade de bytes. Mas se ocorrer um erro de leitura, as coisas vão dar errado. Muitas pessoas parecem pensar que o *dd* irá "preencher erros de leitura com zeros" se você usar as opções `noerror, sync`, mas isto não é o que acontece. O *dd* irá, segundo a documentação, preencher o OBS para o tamanho IBS *depois de completar sua leitura*, o que significa adicionar zeros no *fim* do bloco. Isso significa, para um disco, que efetivamente todo o 1 MiB seria confuso por causa de um único erro de leitura de 512 bytes no início da leitura: 12ERROR89 se tornaria 128900000 em vez de 120000089.

Se você está certo de que o seu disco não contém erros, você pode continuar usando um tamanho de bloco maior, o que aumentará a velocidade da cópia várias vezes. Por exemplo, a alteração de bs de 512 para 64K alterou a velocidade de cópia de 35 MB/s para 120 MB/s em um sistema Celeron de 2,7 GHz. Mas lembre-se de que os erros de leitura no disco de origem terminarão como *erros de bloco* no disco de destino, ou seja, um único erro de leitura de 512 bytes estragará todo o bloco de saída de 64 KiB.

**Dica:** Se você quiser ver o progresso de *dd*, use a opção `status=progress`. Veja [dd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dd.1) para detalhes.

**Nota:**

*   Para obter UUIDs únicos de um sistema de arquivos *ext2/3/4*, use `tune2fs/dev/sd*XY* -U random` em cada partição. Para partições de swap, use `mkswap/dev/sd*XY*`.
*   Mudanças na tabela de partição com o *dd* não são registradas pelo kernel. Para notificar as alterações sem reinicializar, use um utilitário como *partprobe* (parte do [GNU Parted](/index.php/GNU_Parted "GNU Parted")).

### Fazer backup da tabela de partição

Veja [fdisk#Backup and restore partition table](/index.php/Fdisk#Backup_and_restore_partition_table "Fdisk") ou [gdisk#Backup and restore partition table](/index.php/Gdisk#Backup_and_restore_partition_table "Gdisk").

### Criar imagem de disco

Inicialize a partir de uma mídia ao vivo e certifique-se de que nenhuma partição seja montada a partir do disco rígido de origem.

Em seguida, monte o disco rígido externo e faça o backup da unidade:

```
# dd if=/dev/sda conv=sync,noerror bs=64K | gzip -c  > */caminho/para/backup.img.gz*

```

Se necessário (por exemplo, quando o formato do HD externo é FAT32), divida a imagem do disco em volumes (veja também [split(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/split.1)):

```
# dd if=/dev/sda conv=sync,noerror bs=64K | gzip -c | split -a3 -b2G - */caminho/para/backup.img.gz*

```

Se não houver espaço em disco suficiente localmente, você poderá enviar a imagem por meio de *ssh*:

```
# dd if=/dev/sda conv=sync,noerror bs=64K | gzip -c | ssh usuario@local dd of=backup.img.gz

```

Finalmente, salve informações extras sobre a geometria da unidade necessária para interpretar a tabela de partição armazenada na imagem. O mais importante dos quais é o tamanho do cilindro.

```
# fdisk -l /dev/sda > */caminho/para/lista_fdisk.info*

```

**Nota:** Você pode querer usar um tamanho de bloco (`bs=`) que seja igual à quantidade de cache no HD que você está fazendo backup. Por exemplo, `bs=8192K` funciona para um cache de 8 MiB. O 64 KiB mencionado neste artigo é melhor que o padrão `bs=512` bytes, mas pode ser mais rápido se executado com um `bs=` maior.

### Restaurar o sistema

Para restaurar seu sistema:

```
# gunzip -c */caminho/para/backup.img.gz* | dd of=/dev/sda

```

Quando a imagem tiver sido dividida com *split*, use o seguinte:

```
# cat */caminho/para/backup.img.gz** | gunzip -c | dd of=/dev/sda

```

## Aplicação de patch em arquivo binário

Caso queira substituir a posição `0x123AB` de um arquivo com a sequência hexadecimal `FF C0 14`, isso pode ser feito com a linha de comando: `# printf '\xff\xc0\x14' | dd seek=$((0x123AB)) conv=notrunc bs=1 of=*/path/to/file*` 

## Fazer backup e restaurar MBR

Antes de fazer alterações em um disco, você pode querer fazer backup da tabela de partição e do esquema de partição da unidade. Você também pode usar um backup para copiar o mesmo layout de partição para várias unidades.

O MBR é armazenado nos primeiros 512 bytes do disco. Consiste em 4 partes:

1.  Os primeiros 440 bytes contêm o código de *bootstrap* (gerenciador de boot).
2.  Os próximos 6 bytes contêm a assinatura do disco.
3.  Os próximos 64 bytes contêm a tabela de partição (4 entradas de 16 bytes cada, uma entrada para cada partição primária).
4.  Os últimos 2 bytes contêm uma assinatura de inicialização.

Para salvar o MBR como `arquivo_mbr.img`:

```
# dd if=/dev/sd*X* of=*/caminho/para/arquivo_mbr.img* bs=512 count=1

```

Você também pode extrair o MBR de uma imagem completa do disco dd:

```
# dd if=*/caminho/para/disco.img* of=*/caminho/para/arquivo_mbr.img* bs=512 count=1

```

Para restaurar (cuidado, isso destrói a tabela de partição existente e, com ela, o acesso a todos os dados no disco):

```
# dd if=/*caminho/para/arquivo_mbr.img* of=/dev/sd*X* bs=512 count=1

```

**Atenção:** Restaurar o MBR com uma tabela de partição incompatível tornará seus dados ilegíveis e quase impossíveis de recuperar. Se você simplesmente precisar reinstalar o gerenciador de boot, consulte suas respectivas páginas, pois elos também empregam a [região de compatibilidade do DOS](http://www.pixelbeat.org/docs/disk/): [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)") ou [Syslinux](/index.php/Syslinux "Syslinux").

Se você deseja restaurar apenas o gerenciador de boot, mas não as entradas da tabela de partição primária, basta restaurar os primeiros 440 bytes do MBR:

```
# dd if=*/caminho/para/arquivo_mbr.img* of=/dev/sd*X* bs=440 count=1

```

Para restaurar apenas a tabela de partição, você deve usar:

```
# dd if=*/caminho/para/arquivo_mbr.img* of=/dev/sd*X* bs=1 skip=446 count=64

```

### Remover o gerenciador de boot

Para apagar o código de bootstrap do MBR (pode ser útil se você tiver que fazer uma reinstalação completa de outro sistema operacional) apenas os primeiros 440 bytes precisam ser zerados:

```
# dd if=/dev/zero of=/dev/sd*X* bs=440 count=1

```