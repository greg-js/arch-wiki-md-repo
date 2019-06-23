**Status de tradução:** Esse artigo é uma tradução de [Badblocks](/index.php/Badblocks "Badblocks"). Data da última tradução: 2019-06-19\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Badblocks&diff=0&oldid=575919) na versão em inglês.

*badblocks* é um programa para testar dispositivos de armazenamento para blocos defeituosos (em inglês, *bad blocks*).

No caso de um HDD, todo o setor deve ser aposentado. Um setor é uma subdivisão de uma faixa em um dispositivo de armazenamento e setores que se tornaram ruins não podem ser usados porque ficaram danificados permanentemente (um setor defeituoso pode ter efeitos adversos variando de alterar uma letra em um arquivo de texto para causar um programa binário tem uma falha de segmentação).

[S.M.A.R.T.](/index.php/S.M.A.R.T. "S.M.A.R.T.") *(Self-Monitoring, Analysis, and Reporting Technology)* é um recurso de hardware presente em quase todos os HDD ainda em uso hoje em dia e em alguns casos pode automaticamente "aposentar" defeituosos setores de HDD. De qualquer forma, S.M.A.R.T. espera apenas passivamente por erros, enquanto os blocos defeituosos escrevem padrões simples para cada bloco de um dispositivo e, em seguida, os lê e verifica procurando por áreas danificadas. (Assim como o memtest86* faz com a RAM.)

Isso pode ser feito em um modo de gravação *(write-mode)* destrutivo que efetivamente [apaga](/index.php/Securely_wipe_disk "Securely wipe disk") o dispositivo (faça backup!) ou em modos não-destrutivos de leitura-gravação (backup aconselhável também!) e somente leitura.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Fidelidade do dispositivo de armazenamento](#Fidelidade_do_dispositivo_de_armazenamento)
*   [3 Comparações com outros programas](#Comparações_com_outros_programas)
*   [4 Testando por setores ruins](#Testando_por_setores_ruins)
    *   [4.1 Teste de leitura-gravação (aviso:destrutivo)](#Teste_de_leitura-gravação_(aviso:destrutivo))
        *   [4.1.1 Defina padrão de teste específico](#Defina_padrão_de_teste_específico)
            *   [4.1.1.1 Padrão aleatório](#Padrão_aleatório)
    *   [4.2 Teste de leitura-gravação (não-destrutivo)](#Teste_de_leitura-gravação_(não-destrutivo))
*   [5 Faça o sistema de arquivos incorporar setores ruins](#Faça_o_sistema_de_arquivos_incorporar_setores_ruins)
    *   [5.1 Durante a verificação de sistema de arquivos](#Durante_a_verificação_de_sistema_de_arquivos)
    *   [5.2 Antes da criação do sistema de arquivos](#Antes_da_criação_do_sistema_de_arquivos)
        *   [5.2.1 Ext4](#Ext4)
        *   [5.2.2 Tamanho do bloco](#Tamanho_do_bloco)
*   [6 Veja também](#Veja_também)

## Instalação

O pacote [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) é parte do [grupo base](/index.php/Grupo_de_pacotes "Grupo de pacotes"). Veja [badblocks(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/badblocks.8) para o uso.

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

	`-b *número*`: especifica o tamanho do bloco do disco rígido que pode melhorar significativamente o tempo de teste. (`# tune2fs -l *partição*`)

	`-w`: faz um teste de gravação destrutivo

	`-s`: mostra a barra de progresso

	`-v`: torna a saída "verbosa" e emite setores defeituosos detectados para a *stdout*

Opções adicionais que você pode considerar:

	`-p *número*`: executa *número* testes extensos de passagens de iterações sequenciais

	`-o */caminho/do/arquivo-de-saída*`: emite setores defeituosos para *arquivo-de-saída* em vez da stdout

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

Este teste foi projetado para dispositivos com dados já existentes. Um teste de leitura-gravação não destrutivo faz um backup do conteúdo original de um setor antes de testar com um único padrão aleatório e, em seguida, restaura o conteúdo do backup. Este é um teste de passagem única e é útil como um teste de manutenção geral.

 `# badblocks -nsv /dev/*dispositivo*` 
```
Checking for bad blocks in non-destructive read-write mode
From block 0 to 488386583
Checking for bad blocks (non-destructive read-write test)
Testing with **random pattern**: done
Pass completed, 0 bad blocks found. (0/0/0 errors)
```

A opção `-n` significa um teste de leitura-gravação não destrutivo.

## Faça o sistema de arquivos incorporar setores ruins

Para não usar setores defeituosos, eles devem ser conhecidos pelo sistema de arquivos.

### Durante a verificação de sistema de arquivos

A incorporação de setores defeituosos pode ser feita usando o utilitário de verificação do sistema de arquivos (`fsck`). Pode-se dizer ao `fsck` para usar *badblocks* durante um teste. Para fazer um teste **leitura-gravação** (não destrutivo) e ter os setores defeituosos tornados conhecidos para o sistema de arquivos:

```
# fsck -vcck /dev/*dispositivo-PARTIÇÃO*

```

A opção `-cc` fala para executar `fsck` no modo de teste **não-destrutivo**, o `-v` diz ao `fsck` para mostre sua saída, e a opção `-k` preserva setores defeituosos antigos que foram detectados.

Para fazer um teste **somente leitura** (não recomendado):

```
# fsck -vck /dev/*dispositivo-PARTIÇÃO*

```

### Antes da criação do sistema de arquivos

Como alternativa, isso pode ser feito antes da criação do sistema de arquivos.

Se *badblocks* for executado sem a opção `-o`, os setores defeituosos serão impressos apenas no stdout.

Exemplo de saída para erros de leitura no começo do disco:

 `# badblocks -wsv /dev/*dispositivo*` 
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

Para passar confortavelmente a saída de erro de *badblocks* para o sistema de arquivos, deve-se gravar em um arquivo.

 `# badblocks -wsv **-o** /root/*badblocks.txt* /dev/*dispositivo*` 
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

Então, (re)crie o sistema de arquivos com a informação:

```
# mkfs.*tipo-sistema-de-arquivos* **-l** /root/*badblocks.txt* /dev/*dispositivo*

```

**Nota:** O sentido de erros `0/0/527405` é *número_de_erros_de_leitura* / *número_de_erros_de_escrita* / *número_de_erros_de_corrupção*.

#### Ext4

Da página de manual [mke2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mke2fs.8):

	Note que os números de bloco na lista de blocos defeituosos devem ser gerados usando o mesmo tamanho de bloco usado por *mke2fs*. Como resultado, a opção `-c` para *mke2fs* é um método muito mais simples e menos propenso a erros de verificar um disco em busca de blocos defeituosos antes de formatá-lo.

Então, o método recomendado é usar:

```
# mkfs.ext4 -c /dev/*dispositivo*

```

Use `-cc` para fazer um teste de leitura-gravação de blocos defeituosos.

#### Tamanho do bloco

Primeiramente, encontre o **tamanho de bloco** do sistema de arquivos. Por exemplo, para sistemas de arquivos ext#:

```
# dumpe2fs /dev/*dispositivo-PARTIÇÃO* | grep 'Block size'

```

Alimente isso ao *badblocks*:

```
# badblocks -b *tamanho de bloco*

```

## Veja também

*   [Meu disco rígido tem setores defeituosos ou está desenvolvendo setores defeituosos ao longo do tempo](http://www.pcguide.com/ts/x/comp/hdd/errorsBadSectors-c.html) (em inglês)