**Status de tradução:** Esse artigo é uma tradução de [Badblocks](/index.php/Badblocks "Badblocks"). Data da última tradução: 2018-08-20\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Badblocks&diff=0&oldid=536453) na versão em inglês.

*badblocks* é um programa para testar dispositivos de armazenamento para blocos defeituosos (em inglês, *bad blocks*).

No caso de um HDD, todo o setor deve ser aposentado. Um setor é uma subdivisão de uma faixa em um dispositivo de armazenamento e setores que se tornaram ruins não podem ser usados porque ficaram danificados permanentemente (um setor defeituoso pode ter efeitos adversos variando de alterar uma letra em um arquivo de texto para causar um programa binário tem uma falha de segmentação).

[S.M.A.R.T.](/index.php/S.M.A.R.T. "S.M.A.R.T.") *(Self-Monitoring, Analysis, and Reporting Technology)* é um recurso de hardware presente em quase todos os HDD ainda em uso hoje em dia e em alguns casos pode automaticamente "aposentar" defeituosos setores de HDD. De qualquer forma, S.M.A.R.T. espera apenas passivamente por erros, enquanto os blocos defeituosos escrevem padrões simples para cada bloco de um dispositivo e, em seguida, os lê e verifica procurando por áreas danificadas. (Assim como o memtest86* faz com a RAM.)

Isso pode ser feito em um modo de gravação *(write-mode)* destrutivo que efetivamente [apaga](/index.php/Securely_wipe_disk "Securely wipe disk") o dispositivo (faça backup!) ou em modos não-destrutivos de leitura-gravação (backup aconselhável também!) e somente leitura.

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
*   [2 Fidelidade do dispositivo de armazenamento](#Fidelidade_do_dispositivo_de_armazenamento)
*   [3 Comparações com outros programas](#Compara.C3.A7.C3.B5es_com_outros_programas)
*   [4 Testando por setores ruins](#Testando_por_setores_ruins)
    *   [4.1 Teste de leitura-gravação (aviso:destrutivo)](#Teste_de_leitura-grava.C3.A7.C3.A3o_.28aviso:destrutivo.29)
        *   [4.1.1 Defina padrão de teste específico](#Defina_padr.C3.A3o_de_teste_espec.C3.ADfico)
            *   [4.1.1.1 Padrão aleatório](#Padr.C3.A3o_aleat.C3.B3rio)
    *   [4.2 Teste de leitura-gravação (não-destrutivo)](#Teste_de_leitura-grava.C3.A7.C3.A3o_.28n.C3.A3o-destrutivo.29)
*   [5 Faça o sistema de arquivos incorporar setores ruins](#Fa.C3.A7a_o_sistema_de_arquivos_incorporar_setores_ruins)
    *   [5.1 Durante a verificação de sistema de arquivos](#Durante_a_verifica.C3.A7.C3.A3o_de_sistema_de_arquivos)
    *   [5.2 Antes da criação do sistema de arquivos](#Antes_da_cria.C3.A7.C3.A3o_do_sistema_de_arquivos)
        *   [5.2.1 Ext4](#Ext4)
        *   [5.2.2 Tamanho do bloco](#Tamanho_do_bloco)
*   [6 Veja também](#Veja_tamb.C3.A9m)

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs). Veja [badblocks(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/badblocks.8) para o uso.

## Fidelidade do dispositivo de armazenamento

Embora não exista uma regra firme, é comum pensar que uma nova unidade deve ter zero setores defeituosos. Com o passar do tempo, setores defeituosos se desenvolverão e, embora possam ser definidos para o sistema de arquivos para que sejam evitados, o uso contínuo da unidade geralmente resultará na formação de setores defeituosos adicionais e normalmente é o prenúncio de sua eventual morte. A substituição do dispositivo é recomendada.

## Comparações com outros programas

Prática recomendada típica para testar um dispositivo de armazenamento para setores defeituosos é usar o programa de teste do fabricante. A maioria dos fabricantes possui programas que fazem isso. O principal motivo para isso é que os fabricantes geralmente têm seus padrões embutidos nos programas de teste que lhe dirão se a unidade precisa ser substituída ou não. A ressalva aqui é que alguns programas de teste de fabricantes não imprimem resultados de teste completos e permitem que um certo número de setores defeituosos diga apenas se eles passam ou não. Os programas de fabricantes, no entanto, são geralmente mais rápidos do que os *badblocks*, por vezes, uma quantidade razoável.

## Testando por setores ruins

Para testar setores defeituosos no Linux, o programa *badblocks* é normalmente usado. *badblocks* tem vários modos diferentes para detectar setores defeituosos.

### Teste de leitura-gravação (aviso:destrutivo)

Este teste é principalmente para testar novas unidades e é um teste de leitura/gravação. À medida que o padrão é gravado em todos os blocos acessíveis, o dispositivo obtém efetivamente [apagado](/index.php/Securely_wipe_disk "Securely wipe disk"). O padrão é um teste extensivo com quatro passagens usando quatro padrões diferentes: 0xaa (10101010), 0x55 (01010101), 0xff (11111111) e 0x00 (00000000). Para alguns dispositivos, isso levará alguns dias para ser concluído.

 `# badblocks -wsv /dev/*dispositivo*` 
```
Checking for bad blocks in read-write mode
From block 0 to 488386583
Testing with pattern **0xaa**: done
Reading and comparing: done
Testing with pattern **0x55**: done
Reading and comparing: done
Testing with pattern **0xff**: 22.93% done, 4:09:55 elapsed. (0/0/0 errors)
[...]
Testing with pattern **0x00**: done
Reading and comparing: done
Pass completed, 0 bad blocks found. (0/0/0 errors)

```

Opções:

	`-w`: faz um teste de gravação destrutivo

	`-s`: mostra a barra de progresso

	`-v`: torna a saída "verbosa" e emite setores defeituosos detectados para a *stdout*

Opções adicionais que você pode considerar:

	`-p *número*`: executa *número* testes extensos de passagens de iterações sequenciais

	`-o */caminho/do/arquivo-de-saída*`: emite setores defeituosos para <arquivo-de-saída> em vez da *stdout*

	`-t *padrão_de_teste*`: especifica um padrão. Veja abaixo.

#### Defina padrão de teste específico

**Da página man:** "O *padrão_de_teste* pode ser um valor numérico entre 0 e um ULONG_MAX-1 inclusive [...]."

##### Padrão aleatório

Pode-se fazer com que blocos defeituosos sejam repetidamente gravados com um único "padrão aleatório" com a opção `-t random`.

 `# badblocks -wsv -t random /dev/*dispositivo*` 
```
Checking for bad blocks in read-write mode
From block 0 to 488386583
Testing with **random pattern**: done
Reading and comparing: done
Pass completed, 0 bad blocks found. (0/0/0 errors)
```

**Atenção:** Isso não é seguro para fins criptográficos. Um "padrão aleatório" é uma contradição em si. Como *badblocks* não (como [/dev/urandom](https://en.wikipedia.org/wiki/pt:/dev/random "wikipedia:pt:/dev/random")) aplica procedimentos sofisticados para reutilizar a entropia, mas simplesmente repete um "padrão aleatório", ele não deve ser usado onde dados aleatórios seriam necessários, por exemplo, para [criptografia de dispositivos de bloco](/index.php/Securely_wipe_disk#Preparations_for_block_device_encryption "Securely wipe disk").

### Teste de leitura-gravação (não-destrutivo)

This test is designed for devices with data already on them. A non-destructive read-write test makes a backup of the original content of a sector before testing with a single random pattern and then restoring the content from the backup. This is a single pass test and is useful as a general maintenance test.

 `# badblocks -nsv /dev/<device>` 
```
Checking for bad blocks in non-destructive read-write mode
From block 0 to 488386583
Checking for bad blocks (non-destructive read-write test)
Testing with **random pattern**: done                                                 
Pass completed, 0 bad blocks found. (0/0/0 errors)
```

The `-n` option signifies a non-destructive read-write test.

## Faça o sistema de arquivos incorporar setores ruins

To not use bad sectors they have to be known by the filesystem.

### Durante a verificação de sistema de arquivos

Incorporating bad sectors can be done using the filesystem check utility (`fsck`). `fsck` can be told to use *badblocks* during a check. To do a **read-write** (non-destructive) test and have the bad sectors made known to the filesystem run:

```
# fsck -vcck /dev/<device-PARTITION>

```

The `-cc` option tells run `fsck` in **non-destructive** test mode, the `-v` tells `fsck` to show its output, and the `-k` option preserves old bad sectors that were detected.

To do a **read-only** test (not recommended):

```
# fsck -vck /dev/<device-PARTITION>

```

### Antes da criação do sistema de arquivos

Alternately, this can be done before filesystem creation.

If badblocks is run without the `-o` option bad sectors will only be printed to stdout.

Example output for read errors in the beginning of the disk:

 `# badblocks -wsv /dev/<drive>` 
```
[...]
Testing with pattern **0xff**: done                                                 
Reading and comparing:
[...]
37584
37585 0.84% done, 7:31:08 elapsed. (0/0/527405 errors)
37586
[...]
done
Testing with pattern **0x00**:
Reading and comparing:
[...]
37584
37585
[...]
done
Pass completed, 527405 bad blocks found. (0/0/527405 errors)
```

For comfortably passing badblocks error output to the filesystem it has to be written to a file.

 `# badblocks -wsv **-o** /root/<badblocks.txt> /dev/<device>` 
```
Checking for bad blocks in read-write mode
From block 0 to 488386583
Testing with pattern **0xaa**: done
Reading and comparing:   6.36% done, 0:51 elapsed. (0/0/14713 errors)
[...]
Testing with pattern **0x00**: done
Reading and comparing: done
Pass completed, 527405 bad blocks found. (0/0/527405 errors)
```

Then (re-)create the file system with the information:

```
# mkfs.<filesystem-type> **-l** /root/<badblocks.txt> /dev/<device>

```

**Note:** The meaning of `0/0/527405` errors is <number of read errors>/<number of write errors>/<number of corruption errors>.

#### Ext4

From the [mke2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mke2fs.8) manual page:

	Note that the block numbers in the bad block list must be generated using the same block size as used by *mke2fs*. As a result, the `-c` option to *mke2fs* is a much simpler and less error-prone method of checking a disk for bad blocks before formatting it.

So the recommended method is to use:

```
# mkfs.ext4 -c /dev/<device>

```

Use `-cc` to do a read-write badblock test.

#### Tamanho do bloco

First find the file systems **block size**. For example for ext# filesystems:

```
# dumpe2fs /dev/<device-PARTITION> | grep 'Block size'

```

Feed this to *badblocks*:

```
# badblocks -b <block size>

```

## Veja também

*   [My hard disk has bad sectors or is developing bad sectors over time](http://www.pcguide.com/ts/x/comp/hdd/errorsBadSectors-c.html)