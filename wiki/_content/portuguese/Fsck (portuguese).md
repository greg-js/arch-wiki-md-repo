**Status de tradução:** Esse artigo é uma tradução de [fsck](/index.php/Fsck "Fsck"). Data da última tradução: 2020-01-18\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Fsck&diff=0&oldid=595322) na versão em inglês.

Artigos relacionados

*   [Ext4](/index.php/Ext4_(Portugu%C3%AAs) "Ext4 (Português)")
*   [Btrfs](/index.php/Btrfs "Btrfs")
*   [fstab](/index.php/Fstab "Fstab")

[fsck](https://en.wikipedia.org/wiki/Fsck "wikipedia:Fsck"), acrônimo do inglês de *"File System Check"*, que significa *"verificação do sistema de arquivos "* é usado para verificar e, opcionalmente, reparar um ou mais sistemas de arquivos Linux. Normalmente, o programa fsck irá tentar manusear sistemas de arquivos em diferentes discos físicos em paralelo para reduzir o tempo total necessário para verificar todos os sistemas de arquivos (veja: [fsck(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fsck.8)).

O [processo de inicialização do Arch Linux](/index.php/Processo_de_inicializa%C3%A7%C3%A3o_do_Arch "Processo de inicialização do Arch") convenientemente cuida dos procedimentos fsck por você e irá verificar todas as partições relevantes em seu(s) dispositivo(s) automaticamente em cada inicialização. Consequentemente, não há necessidade de invocar o programa, a menos em casos estritamente necessários.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Verificação durante inicialização do sistema](#Verificação_durante_inicialização_do_sistema)
    *   [1.1 Mecanismo](#Mecanismo)
    *   [1.2 Forçando a verificação](#Forçando_a_verificação)
*   [2 Dicas e truques](#Dicas_e_truques)
    *   [2.1 Tentar reparar blocos danificados](#Tentar_reparar_blocos_danificados)
    *   [2.2 Reparar blocos danificados interativamente](#Reparar_blocos_danificados_interativamente)
    *   [2.3 Alterando a frequência de verificação](#Alterando_a_frequência_de_verificação)
    *   [2.4 Opções do fstab](#Opções_do_fstab)
*   [3 Solução de problemas](#Solução_de_problemas)
    *   [3.1 Não é possível executar fsck em uma partição /usr separada](#Não_é_possível_executar_fsck_em_uma_partição_/usr_separada)
    *   [3.2 ext2fs : no external journal](#ext2fs_:_no_external_journal)

## Verificação durante inicialização do sistema

### Mecanismo

Há duas opções:

1.  mkinitcpio oferece a opção de executar fsck em seu sistema de arquivos raiz antes de montá-lo pelo hook do fsck. Ao fazer isto, você deverá montar a raiz em modo de escrita pelo apropriado parâmetro do kernel `rw`.[[1]](https://projects.archlinux.org/mkinitcpio.git/commit/?id=449b3e543c)
2.  systemd irá executar fsck em todos os sistemas de arquivos, exceto os que tenham um código execução definido superior a 0 (em `/etc/fstab` ou arquivo init definido pelo usuário). Para o sistema de arquivos raiz, ele também deve ser montado inicialmente em modo somente-leitura com o parâmetro do kernel `ro` para depois ser remontado em modo de escrita pelo [fstab](/index.php/Fstab "Fstab") (note que a opção de montagem `defaults` implica `rw`).

A primeira opção descrita é a padrão, e é a obtida se você seguir o [guia de instalação](/index.php/Guia_de_instala%C3%A7%C3%A3o "Guia de instalação"). Se, ao invés dela, ocorrer a opção 2, você precisará remover o hook do fsck de `mkinitcpio.conf` e usar `ro` na linha de comando do kernel. O parâmetro do kernel `fsck.mode=skip` pode ser usado para certificar-se de que fsck está completamente desativado para ambas as opções.

### Forçando a verificação

Se você usar o hook `base` do [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"), será possível forçar a execução do fsck durante a inicialização passando `fsck.mode=force` como um [parâmetro do kernel](/index.php/Par%C3%A2metro_do_kernel "Parâmetro do kernel"). Isto fará com que ele verifique cada sistema de arquivos existente na máquina.

Alternativamente, systemd fornece [systemd-fsck@.service(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-fsck%40.service.8), que verifica todos os sistemas de arquivos configurados, os quais não foram verificados em initramfs. Contudo, verificar o sistema de arquivos raiz dessa maneira irá causar uma demora no processo de inicialização, já que o sistema de arquivos precisará ser remontado.

**Nota:** Para aqueles acostumados em usar outras distribuições GNU/Linux, os truques antigos que consistiam em escrever um arquivo com o nome `forcefsck` na raiz do sistema de arquivos ou usando o comando `shutdown` com a opção `-F`, somente funcionavam no antigo [SysVinit](/index.php/SysVinit "SysVinit") e em versões anteriores do [Upstart](https://en.wikipedia.org/wiki/Upstart "wikipedia:Upstart"), e não estão mais funcionando com o [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)"). O método descrito acima, portanto, é a única que funciona com Arch Linux.

## Dicas e truques

### Tentar reparar blocos danificados

Para automaticamente reparar setores danificados, execute:

**Atenção:** Isto não irá perguntar se você deseja repará-los, já que a resposta padrão será **Sim** quando você executá-lo.

```
# fsck -a

```

### Reparar blocos danificados interativamente

**Dica:** Isto é útil quando um arquivo na partição de inicialização foi alterado, e o *journal* falhou em atualizá-lo corretamente. Neste caso, desmonte a partição de inicialização, e execute o seguinte código:

Para reparar setores danificados, execute:

```
# fsck -r <drive>

```

### Alterando a frequência de verificação

Por padrão, fsck verifica o sistema de arquivos a cada 30 inicializações (contadas individualmente para cada partição). Para alterar a frequência de verificação, execute:

```
# tune2fs -c 20 /dev/sda1

```

Neste exemplo, `20` é o número de inicializações que ocorrerão entre duas verificações.

Note que `1` fará com que a verificação ocorra em cada inicialização, ao passo que `0` faria com que a varredura deixasse de ocorrer.

**Dica:** Se desejar ver a frequência e a atual contagem de montagens para uma partição específica, use:
```
# dumpe2fs -h /dev/sda1 | grep -i 'mount count'

```

### Opções do fstab

[fstab](/index.php/Fstab "Fstab") é um arquivo de configuração do sistema e é usado para informar ao Linux kernel quais partições (sistemas de arquivos) montar e onde estará a árvore do sistema de arquivos.

Um entrada típica do `/etc/fstab` será algo semelhante a isto:

```
/dev/sda1   /         ext4      defaults       0  **1**
/dev/sda2   /other    ext4      defaults       0  **2**
/dev/sda3   /win      ntfs-3g   defaults       0  **0**

```

A sexta coluna (em negrito) é a opção do fsck.

*   0 = Não verificar.
*   1 = Primeiro sistema de arquivos (partição) passar pela verificação; `/` (partição raiz) deverá ser definida com 1.
*   2 = Todos os outros sistemas de arquivos a serem verificados.

## Solução de problemas

### Não é possível executar fsck em uma partição /usr separada

1.  Certifique-se de que você definiu [hooks](/index.php/Mkinitcpio#.2Fusr_as_a_separate_partition "Mkinitcpio") em `/etc/mkinitcpio.conf` e que você lembrou-se de recriar sua imagem initramfs após editar este arquivo.
2.  Verifique seu [fstab](/index.php/Fstab "Fstab")! Somente a partição raiz precisa de "1" ao final da linha, todos os demais deverão conter "2" ou "0". Cuidadosamente verifique se há quaisquer erros de digitação.

### ext2fs : no external journal

Às vezes (devido à falta de energia), um sistema de arquivos ext(3/4) poderá corromper-se de modo que um reparo normal não será capaz de solucionar. Normalmente, haverá um prompt do fsck indicando que não pôde encontrar um *journal* externo. Neste caso, execute os seguintes comandos:

Desmontar a partição baseada em seu diretório

```
# umount <diretório>

```

Gravar um novo *journal* à partição

```
# tune2fs -j /dev/<partition>

```

Executar fsck para reparar a partição

```
# fsck -p /dev/<partition>

```