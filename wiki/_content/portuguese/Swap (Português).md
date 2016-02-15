Uma livre tradução de [Tudo sobre o espaço de troca do Linux _(All about Linux swap space)_](http://www.linux.com/news/software/applications/8208-all-about-linux-swap-space):

	_O Linux divide sua RAM_ (random access memory) _física em pedaços de memória chamados páginas. A troca_ (swapping) _é o processo no qual uma página de memória é copiada a um espaço pré-configurado no disco rígido, chamado de espaço de troca_ (swap space)_, para liberar aquela página de memória. O tamanho combinado da memória física e do espaço de troca é a quantidade de memória virtual disponível._

O espaço de troca geralmente será uma partição de disco, mas também pode ser um arquivo. Usuários podem criar espaços de troca durante a instalação do Arch Linux ou a qualquer momento no futuro, se a necessidade surgir. O espaço de troca é geralmente recomendado para usuários com menos de 1 GB de RAM e é mais uma questão de preferência pessoal em sistemas com grandes quantidades de RAM física (entretanto, ele é necessário para suporte a suspensão para disco (_suspend-to-disk_).

## Contents

*   [1 Partição _swap_](#Parti.C3.A7.C3.A3o_swap)
*   [2 Arquivo _swap_](#Arquivo_swap)
    *   [2.1 Criação do arquivo _swap_](#Cria.C3.A7.C3.A3o_do_arquivo_swap)
    *   [2.2 Remover o arquivo _swap_](#Remover_o_arquivo_swap)
    *   [2.3 Resumindo uma sessão de um arquivo _swap_](#Resumindo_uma_sess.C3.A3o_de_um_arquivo_swap)

## Partição _swap_

Uma partição _swap_ pode ser criada com a maioria das ferramentas de partição do GNU/Linux (por exemplo o `fdisk` ou `cfdisk`). Partições _swap_ são designadas como tipo **82**.

Para configurar um espaço de troca Linux, o comando `mkswap` é usado. Por exemplo:

```
# mkswap /dev/sda2

```

**Warning:** Todos os dados na partição especificada serão pedidos.

Para ativar o dispositivo para paginação:

```
# swapon /dev/sda2

```

Para ativar essa partição _swap_ durante o _boot_, adicione uma entrada ao [fstab](/index.php/Fstab "Fstab"):

```
/dev/sda2 none swap defaults 0 0

```

## Arquivo _swap_

Uma alternativa à criação de uma partição inteira, o arquivo _swap_ oferece a habilidade de variar seu tamanho dinamicamente, e é de modo geral mais facilmente removível. Isso pode ser especialmente desejável se o espaço em disco for escasso (por exemplo, num SSD de tamanho moderado).

### Criação do arquivo _swap_

Como root use o `fallocate` para criar um arquivo _swap_ do tamanho de sua escolha (M = Megabytes, G = Gigabytes) (o `dd` também pode ser usado, mas irá demorar mais). Por exemplo, para criar um arquivo _swap_ de 512 MB:

```
# fallocate -l 512M /swapfile
# dd if=/dev/zero of=/swapfile bs=1M count=512

```

Configure as permissões corretas (um arquivo _swap_ com permissões de leitura para todo mundo é uma vulnerabilidade local enorme)

```
# chmod 600 /swapfile

```

Depois de criar um arquivo com o tamanho correto, formate-o como _swap_

```
# mkswap /swapfile

```

E ative o arquivo _swap_:

```
# swapon /swapfile

```

Edite `/etc/fstab` e adicione uma entrada para o arquivo _swap_:

```
/swapfile none swap defaults 0 0

```

### Remover o arquivo _swap_

Para remover o arquivo _swap_, ele deve ser primeiro desligado.

Como root:

```
# swapoff -a

```

E remova o arquivo _swap_:

```
# rm -rf /swapfile

```

### Resumindo uma sessão de um arquivo _swap_

Resumir o sistema a partir de um arquivo _swap_ depois de hibernar requer a adição de um parâmetro adicional ao kernel em comparação com resumir a partir de uma partição _swap_. O parâmetro adicional é `resume_offset=<Swap File Offset>`.

O valor de `<Swap File Offset>` pode ser obtido pela saída de `filefrag -v`; a saída é em formado de tabela, e o valor requerido está localizado na coluna `physical`, na primeira linha. Por exemplo:

```
# filefrag -v /swapfile
Filesystem type is: ef53
File size of /swapfile is 4290772992 (1047552 blocks, blocksize 4096)
ext logical  physical  expected  length flags
  0       0     7546880                6144 
  1    6144  7557120  7553023   2048 
  2    8192  7567360  7559167   2048 
...

```

Neste exemplo, o `<Swap File Offset>` é `7546880`.

**Note:** Por favor, note que no parâmetro `resume` do kernel você ainda pode ter que adicionar o caminho da partição (por exemplo, `resume=/dev/sda1`), e não o caminho explícito do arquivo _swap_! O parâmetro `resume_offset` serve para informar o sistema onde o arquivo _swap_ começa no disco rígido.