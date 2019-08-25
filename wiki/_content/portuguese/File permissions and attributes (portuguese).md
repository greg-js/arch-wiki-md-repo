**Status de tradução:** Esse artigo é uma tradução de [File permissions and attributes](/index.php/File_permissions_and_attributes "File permissions and attributes"). Data da última tradução: 2019-08-16\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=File_permissions_and_attributes&diff=0&oldid=579195) na versão em inglês.

Artigos relacionados

*   [Usuários e grupos](/index.php/Usu%C3%A1rios_e_grupos "Usuários e grupos")
*   [umask](/index.php/Umask_(Portugu%C3%AAs) "Umask (Português)")
*   [Listas de Controle de Acesso](/index.php/Access_Control_Lists "Access Control Lists")
*   [Capacidades](/index.php/Capabilities "Capabilities")

[Sistemas de arquivos](/index.php/File_systems "File systems") usam [permissões](https://en.wikipedia.org/wiki/pt:Permiss%C3%B5es_de_sistema_de_arquivos "w:pt:Permissões de sistema de arquivos") e [atributos](https://en.wikipedia.org/wiki/File_attribute "w:File attribute") para regular o nível de interação que processos de sistema podem ter com os arquivos e diretórios.

**Atenção:** Quando usados para fins de segurança, as permissões e atributos só defendem contra ataques iniciados a partir do sistema inicializado. Para proteger os dados armazenados dos invasores com acesso físico à máquina, é preciso também implementar [criptografia de disco](/index.php/Disk_encryption "Disk encryption").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Visualizando permissões](#Visualizando_permissões)
    *   [1.1 Exemplos](#Exemplos)
*   [2 Alterando permissões](#Alterando_permissões)
    *   [2.1 Método de texto](#Método_de_texto)
        *   [2.1.1 Atalhos do método de texto](#Atalhos_do_método_de_texto)
        *   [2.1.2 Permissões de cópia](#Permissões_de_cópia)
    *   [2.2 Método numérico](#Método_numérico)
    *   [2.3 chmod em lote](#chmod_em_lote)
*   [3 Alterando o proprietário](#Alterando_o_proprietário)
*   [4 Listas de Controle de Acesso](#Listas_de_Controle_de_Acesso)
*   [5 Umask](#Umask)
*   [6 Atributos de arquivos](#Atributos_de_arquivos)
    *   [6.1 chattr e lsattr](#chattr_e_lsattr)
*   [7 Atributos estendidos](#Atributos_estendidos)
    *   [7.1 Atributos estendidos de usuário](#Atributos_estendidos_de_usuário)
    *   [7.2 Preservando atributos estendidos](#Preservando_atributos_estendidos)
*   [8 Dicas e truques](#Dicas_e_truques)
    *   [8.1 Preservar root](#Preservar_root)
*   [9 Veja também](#Veja_também)

## Visualizando permissões

Use a opção `-l` do comando [ls](/index.php/Ls_(Portugu%C3%AAs) "Ls (Português)") para visualizar as permissões (ou **modo de arquivo**) definidas para o conteúdo de um diretório, por exemplo:

 `$ ls -l /caminho/para/diretório` 
```
total 128
drwxr-xr-x 2 archie users  4096 Jul  5 21:03 'Área de trabalho'
drwxr-xr-x 6 archie users  4096 Jul  5 17:37  Documentos
drwxr-xr-x 2 archie users  4096 Jul  5 13:45  Downloads
-rw-rw-r-- 1 archie users  5120 Jun 27 08:28  clientes
-rw-r--r-- 1 archie users  3339 Jun 27 08:28  tarefas
-rwxr-xr-x 1 archie users  2048 Jul  6 12:56  meuscript.sh

```

A primeira coluna é o que devemos focar. Tomando um valor de exemplo de `drwxrwxrwx +`, o significado de cada caractere é explicado nas seguintes tabelas:

| `d` | `rwx` | `rwx` | `rwx` | `+` |
| O tipo de arquivo, tecnicamente não sendo parte de suas permissões. Veja `info ls -n "What information is listed"` para uma explicação dos valores possíveis. | As permissões que o proprietário tem sobre o arquivo, explicadas abaixo. | As permissões que o grupo tem sobre o arquivo, explicadas abaixo. | As permissões que outros usuários têm sobre o arquivo, explicadas abaixo. | Um único caractere que especifica se um método de acesso alternativo se aplica ao arquivo. Quando esse caractere é um espaço, não há método de acesso alternativo. Um caractere `.` indica um arquivo com um contexto de segurança, mas nenhum outro método de acesso alternativo. Um arquivo com qualquer outra combinação de métodos de acesso alternativo é marcado com um caractere `+`, por exemplo, no caso de [Listas de Controle de Acesso](/index.php/Access_Control_Lists "Access Control Lists"). |

Cada uma das três tríades de permissão (`rwx` no exemplo acima) pode ser composta dos seguintes caracteres:

 Caractere | Efeito nos arquivos | Efeito em diretórios |
| Permissão de leitura (primeiro caractere) | `-` | O arquivo não pode ser lido. | O conteúdo do diretório não pode ser mostrado. |
| `r` | O arquivo pode ser lido. | O conteúdo do diretório pode ser mostrado. |
| Permissão de escrita (segundo caractere) | `-` | O arquivo não pode ser modificado. | O conteúdo do diretório não pode ser modificado. |
| `w` | O arquivo pode ser modificado. | O conteúdo do diretório pode ser modificado (criar novos arquivos ou pastas; renomear ou excluir arquivos ou pastas existentes); exige que a permissão de execução também esteja definida, do contrário essa permissão não tem efeito. |
| Permissão de execução (terceiro caractere) | `-` | O arquivo não pode ser executado. | O diretório não pode ser acessado com [cd](/index.php/Cd_(Portugu%C3%AAs) "Cd (Português)"). |
| `x` | O arquivo pode ser executado. | O diretório pode ser acessado com [cd](/index.php/Cd_(Portugu%C3%AAs) "Cd (Português)"); essa é o único bit de permissão que, na prática, pode ser considerado como "herdado" dos diretórios anteriores - na verdade, se *qualquer* pasta no caminho não tem o bit `x` definido, o arquivo ou pasta final também não pode ser acessado(a), independentemente de suas permissões; veja [path_resolution(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/path_resolution.7) para mais informações. |
| `s` | O bit [setuid](https://en.wikipedia.org/wiki/pt:setuid "w:pt:setuid") quando encontrar-se na tríade de **u**suário; o bit **setgid** quando encontrar-se na tríade de **g**rupo; ele não é encontrado na tríade de **o**utros; isso também implica que `x` está definido. |
| `S` | Mesmo que `s`, mas `x` não está definido; raro em arquivos comuns e inútil em pastas. |
| `t` | O [sticky](https://en.wikipedia.org/wiki/pt:sticky_bit "w:pt:sticky bit") bit (ou "bit pegajoso"); ele só pode ser encontrado na tríade de **o**utros; isso também implica que `x` está definido. |
| `T` | Mesmo que `t`, mas `x` não está definido; raro em arquivos comuns e inútil em pastas. |

Veja `info Coreutils -n "Mode Structure"` e [chmod(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chmod.1) para mais detalhes.

**Dica:** Você pode ver as permissões de um caminho com `namei -l *caminho*`.

### Exemplos

Vamos ver alguns exemplos para esclarecer:

```
**drwx------** 6 archie users  4096 Jul  5 17:37 Documentos

```

Archie tem acesso total ao diretório Documentos. Ele pode listar, criar arquivos e renomear, excluir qualquer arquivo em Documentos, independentemente das permissões de arquivo. Sua capacidade de acessar um arquivo depende da permissão do arquivo.

```
**dr-x------** 6 archie users  4096 Jul  5 17:37 Documentos

```

Archie tem acesso completo, exceto que ele não pode criar, renomear, excluir qualquer arquivo. Ele pode listar os arquivos e (se a permissão do arquivo permitir) acessar um arquivo existente em Documentos.

```
**d-wx------** 6 archie users  4096 Jul  5 17:37 Documentos

```

Archie não pode fazer 'ls' em Documentos, mas se ele sabe o nome de um arquivo existente, ele pode listar, renomear, deletar ou (se a permissão do arquivo permitir) acessá-lo. Além disso, ele é capaz de criar novos arquivos.

```
**d--x------** 6 archie users  4096 Jul  5 17:37 Documentos

```

Archie só é capaz de (se a permissão do arquivo o autorizar) acessar esses arquivos em Documentos que ele conhece. Ele não pode listar arquivos já existentes ou criar, renomear, excluir qualquer um deles.

Você deve ter em mente que elaboramos permissões de diretório e não tem nada a ver com as permissões de arquivos individuais. Quando você cria um novo arquivo, é o diretório que muda. É por isso que você precisa de permissão de gravação no diretório.

Vejamos outro exemplo, desta vez de um arquivo, não de um diretório:

```
**-rw-r--r--** 1 archie users  5120 Jun 27 08:28 foobar

```

Aqui podemos ver que a primeira letra não é `d` mas `-`. Então sabemos que é um arquivo, não um diretório. Em seguida, as permissões do proprietário são `rw-` para que o proprietário tenha a capacidade de ler e escrever, mas não de executar. Isso pode parecer estranho que o proprietário não tenha todas as três permissões, mas a permissão `x` não é necessária, pois é um arquivo de texto/dados, para ser lido por um editor de texto como Gedit, EMACS ou software como o R, e não um executável por si só (se contivesse algo como código de programação python, então muito bem poderia ser). As permissões do grupo são definidas para `r--`, então o grupo tem a capacidade de ler o arquivo mas não de escrevê-lo/editá-lo de qualquer forma - é essencialmente como configurar algo para somente leitura. Podemos ver que as mesmas permissões se aplicam a todos os outros também.

## Alterando permissões

[chmod](https://en.wikipedia.org/wiki/pt:chmod "wikipedia:pt:chmod") é um comando no Linux e em outros sistemas operacionais parecidos com Unix que permite alterar (*ch*ange) as permissões (ou *mod*o de acesso) de um arquivo ou diretório.

### Método de texto

Para alterar as permissões - ou *modo de acesso* - de um arquivo, use o comando *chmod* em um terminal. Abaixo está a estrutura geral do comando:

```
chmod *quem*=*permissões* *nome_do_arquivo*

```

sendo `*quem*` qualquer intervalo de letras, cada significando a quem está sendo dada a permissão. Eles são o que segue:

*   `u`: o [usuário](/index.php/Usu%C3%A1rio "Usuário") proprietário do arquivo.
*   `g`: o [grupo de usuários](/index.php/Grupo_de_usu%C3%A1rios "Grupo de usuários") ao qual o arquivo pertence.
*   `o`: **o**utros usuários, isto é, todos os demais.
*   `a`: todos (***a**ll*) acima; use isso em vez de digitar `ugo`.

As permissões são as mesmas discutidas em [#Visualizando permissões](#Visualizando_permissões) (`r`, `w` e `x`).

Agora dê uma olhada em alguns exemplos usando este comando. Suponha que você tenha se tornado muito protetor do diretório Documentos e queira negar a todos menos a si mesmo, permissões para ler, escrever e executar (ou, neste caso, pesquisar/procurar) nele:

Antes: `drwxr-xr-x 6 archie users 4096 Jul 5 17:37 Documentos`

```
$ chmod g= Documentos
$ chmod o= Documentos

```

Após: `drwx------ 6 archie users 4096 Jul 6 17:32 Documentos`

Aqui, porque você quer negar permissões, você não coloca nenhuma letra após o `=` onde as permissões seriam inseridas. Agora você pode ver que apenas as permissões do proprietário são `rwx` e todas as outras permissões são `-`.

Isso pode ser revertido com:

Antes: `drwx------ 6 archie users 4096 Jul 6 17:32 Documentos`

```
$ chmod g=rx Documentos
$ chmod o=rx Documentos

```

Após: `drwxr-xr-x 6 archie users 4096 Jul 6 17:32 Documentos`

No próximo exemplo, você deseja conceder permissões de leitura e execução ao grupo e a outros usuários, portanto, coloque as letras das permissões (`r` e `x`) após o `=`, sem espaços.

Você pode simplificar isso para colocar mais de uma letra `*quem*` no mesmo comando, por exemplo:

```
$ chmod go=rx Documentos

```

**Nota:** Não importa em que ordem você coloca as letras `*quem*` ou as letras de permissão em um comando `chmod`: você pode ter `chmod go=rx arquivo` ou `chmod og=xr arquivo`. É tudo a mesma coisa.

Agora, vamos considerar um segundo exemplo, suponha que você queira alterar um arquivo `foobar` para que tenha permissões de leitura e gravação e outros usuários do grupo `users` que possam ser colegas trabalhando em `foobar`, também pode ler e escrever para ele, mas outros usuários só podem lê-lo:

Antes: `-rw-r--r-- 1 archie users 5120 Jun 27 08:28 foobar`

```
$ chmod g=rw foobar

```

Após: `-rw-rw-r-- 1 archie users 5120 Jun 27 08:28 foobar`

Isso é exatamente como no primeiro exemplo, mas com um arquivo, não um diretório, e você concede permissão de gravação (apenas para dar um exemplo de concessão de todas as permissões).

#### Atalhos do método de texto

O comando *chmod* permite adicionar e subtrair permissões de um conjunto existente usando `+` ou `-` em vez de `=`. Isso é diferente dos comandos acima, que essencialmente reescrevem as permissões (por exemplo, para alterar uma permissão de `r--` para `rw-`, você ainda precisa incluir `r` assim como `w` após o `=` na invocação do comando *chmod*. Se você esquecesse `r`, isso retiraria a permissão de `r`, pois estão sendo re-escritas com o `=`. Usar `+` e `-` evita isso adicionando ou afastando do conjunto *atual* de permissões).

Vamos tentar este método `+` e `-` com o exemplo anterior de adicionar permissões de escrita ao grupo:

Antes: `-rw-r--r-- 1 archie users 5120 Jun 27 08:28 foobar`

```
$ chmod g+w foobar

```

Após: `-rw-rw-r-- 1 archie users 5120 Jun 27 08:28 foobar`

Outro exemplo, negando permissões de escrita para todos (**a**):

Antes: `-rw-rw-r-- 1 archie users 5120 Jun 27 08:28 foobar`

```
$ chmod a-w foobar

```

Após: `-r--r--r-- 1 archie users 5120 Jun 27 08:28 foobar`

Um atalho diferente é o modo especial `X`: este não é um modo de arquivo real, mas é frequentemente usado em conjunto com a opção `-R` para definir o bit executável somente para diretórios, e deixe-o inalterado para arquivos regulares, por exemplo:

```
$ chmod -R a+rX ./data/

```

#### Permissões de cópia

É possível dizer ao *chmod* para copiar as permissões de uma classe, digamos o proprietário, e dar as mesmas permissões para grupo ou até mesmo todos. Para fazer isso, ao invés de colocar `r`, `w`, ou `x` depois do `=`, coloque outra letra de *quem*. Por exemplo:

Antes: `-rw-r--r-- 1 archie users 5120 Jun 27 08:28 foobar`

```
$ chmod g=u foobar

```

Após: `-rw-rw-r-- 1 archie users 5120 Jun 27 08:28 foobar`

Este comando essencialmente se traduz a "altere as permissões do grupo (`g=`) para ser a mesma que o usuário proprietário (`=u`). Note que você não pode copiar um conjunto de permissões, bem como conceder novas, por exemplo:

```
$ chmod g=wu foobar

```

Neste caso, *chmod* exibe um erro.

### Método numérico

O *chmod* também pode definir permissões usando números.

Usar números é outro método que permite editar as permissões de todos os três proprietário, grupo e outros ao mesmo tempo, bem como os bits setuid, setgid e sticky. Essa estrutura básica do código é esta:

```
$ chmod *xxx* *nome_do_arquivo*

```

sendo `**xxx**` um número de 3 dígitos onde cada dígito pode ser qualquer coisa de 0 a 7\. O primeiro dígito se aplica a permissões para proprietário, o segundo dígito se aplica a permissões para grupo e o terceiro dígito se aplica a permissões para todos os outros.

Nesta notação numérica, os valores `r`, `w` e `x` possuem seu próprio valor numérico:

```
r=4
w=2
x=1

```

Para criar um número de 3 dígitos, é necessário considerar quais permissões você deseja que proprietário, grupo e usuário tenham e, em seguida, totalizar seus valores. Por exemplo, se você quiser conceder ao proprietário de um diretório permissões de leitura, escrita e execução, e quiser que o grupo e todos os demais tenham apenas permissões de leitura e execução, você obterá os valores numéricos da seguinte forma:

*   Proprietário: `rwx`=4+2+1=7
*   Grupo: `r-x`=4+0+1=5
*   Outro: `r-x`=4+0+1=5

```
$ chmod 755 *nome_do_arquivo*

```

Isso é equivalente a usar o seguinte:

```
$ chmod u=rwx *nome_do_arquivo*
$ chmod go=rx *nome_do_arquivo*

```

Para visualizar as permissões existentes de um arquivo ou diretório no formato numérico, use o comando [stat(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/stat.1):

```
$ stat -c %a *nome_do_arquivo*

```

sendo que a opção %a especifica a saída no formato numérico.

A maioria das pastas e diretórios é configurada para `755` para permitir leitura, escrita e execução para o proprietário, mas nega a escrita para todos os outros, e os arquivos são normalmente `644` para permitir leitura e escrita para o proprietário, mas apenas leitura para todos os outros; consulte a última nota sobre a falta de permissões `x` com arquivos não executáveis: é a mesma coisa aqui.

Para ver isso em ação com exemplos, considere o exemplo anterior que foi usado, mas com este método numérico aplicado:

Antes: `-rw-r--r-- 1 archie users 5120 Jun 27 08:28 foobar`

```
$ chmod 664 foobar

```

Após: `-rw-rw-r-- 1 archie users 5120 Jun 27 08:28 foobar`

Se este fosse um executável, o número seria `774` se você quisesse conceder permissão executável ao proprietário e ao grupo. Alternativamente, se você quiser que todos tenham permissão de leitura, o número será `444`. Tratar `r` como 4, `w` como 2 e `x` como 1 é provavelmente a maneira mais fácil de calcular os valores numéricos para usar `chmod *xxx* *nome_do_arquivo*`, mas há também um método binário, em que cada permissão possui um número binário e, em seguida, isso é convertido em um número. É um pouco mais complicado, mas aqui incluído para ser completo.

Considere esse conjunto de permissões:

```
-rwxr-xr--

```

Se você colocar um 1 em cada permissão concedida e um 0 para cada um não concedido, o resultado seria algo assim:

```
-rwxrwxr-x
 111111101

```

Você pode então converter esses números binários:

```
000=0	    100=4
001=1	    101=5
010=2	    110=6
011=3	    111=7

```

O valor do acima seria, portanto, 775.

Considere que queríamos remover a permissão gravável do grupo:

```
-rwxr-xr-x
 111101101

```

O valor seria, portanto, 755 e você usaria o `chmod 755 *nome_do_arquivo*` para remover a permissão de escrita. Você notará que obtém o mesmo número de três dígitos, independentemente do método usado. O uso de texto ou números dependerá da preferência pessoal e da velocidade de digitação. Quando você deseja restaurar um diretório ou arquivo para as permissões padrão, por exemplo, ler e escrever (e executar) permissão para o proprietário, mas negar permissão de gravação a todos os outros, pode ser mais rápido usar `chmod 755/644 *nome_do_arquivo*`. No entanto, se você estiver alterando as permissões para algo fora da norma, poderá ser mais simples e rápido usar o método de texto, em vez de tentar convertê-lo em números, o que pode levar a um erro. Pode-se argumentar que não há diferença significativa real na velocidade de cada método para um usuário que só precisa usar *chmod* ocasionalmente.

Você também pode usar o método numérico para definir os bits `setuid`, `setgid` e `sticky` usando quatro dígitos.

```
setuid=4
setgid=2
sticky=1

```

Por exemplo, `chmod 2777 *nome_do_arquivo*` vai definir bits de leitura/escrita/execução para todos e também vai habilitar o bit `setgid`.

### chmod em lote

Geralmente, os diretórios e arquivos não devem ter as mesmas permissões. Se for necessário modificar em massa uma árvore de diretórios, use [find](/index.php/Find_(Portugu%C3%AAs) "Find (Português)") para modificar seletivamente um ou o outro.

Para usar *chmod* para modificar permissões apenas de diretórios para 755:

```
$ find *diretório* -type d -exec chmod 755 {} +

```

Para usar *chmod* para modificar permissões apenas de arquivos para 644:

```
$ find *diretório* -type f -exec chmod 644 {} +

```

## Alterando o proprietário

O [chown](https://en.wikipedia.org/wiki/pt:chown "wikipedia:pt:chown") altera o proprietário de um arquivo ou diretório, o que é mais rápido e mais fácil do que alterar as permissões em alguns casos.

Considere o exemplo a seguir, criando uma nova partição com [GParted](/index.php/GParted "GParted") para dados de backup. O Gparted faz isso tudo como root, então tudo pertence à raiz por padrão. Tudo isso é bom, mas quando se trata de escrever dados na partição montada, a permissão é negada para usuários comuns.

```
brw-rw---- 1 root disk 8,    9 Jul  6 16:02 sda9
drwxr-xr-x 5 root root    4096 Jul  6 16:01 Backup

```

Como você pode ver, o dispositivo em `/dev` pertence ao root, assim como o local de montagem (`/media/Backup`). Para alterar o proprietário do local de montagem, é possível fazer o seguinte:

Antes: `drwxr-xr-x 5 root root 4096 Jul 6 16:01 Backup`

```
# chown archie /media/Backup

```

Após: `drwxr-xr-x 5 archie root 4096 Jul 6 16:01 Backup`

Agora a partição pode ter dados gravados pelo novo proprietário, archie, sem alterar as permissões (já que a tríade do proprietário já tinha permissões `rwx`).

**Nota:**

*   `chown` sempre limpa os bits de setuid e setgid.
*   Além root, nenhum usuário pode usar `chown` para "dar" arquivos que lhe pertence para outro usuário.

## Listas de Controle de Acesso

[Access Control Lists](/index.php/Access_Control_Lists "Access Control Lists") fornece um mecanismo de permissão adicional e mais flexível para sistemas de arquivos, permitindo definir permissões para qualquer usuário ou grupo para qualquer arquivo.

## Umask

O utilitário [umask](/index.php/Umask_(Portugu%C3%AAs) "Umask (Português)") é usado para controlar a máscara do modo de criação de arquivo, que determina o valor inicial dos bits de permissão de arquivo para arquivos recém-criados.

## Atributos de arquivos

Além dos bits do modo de arquivo que controlam [usuário e grupo](/index.php/Usu%C3%A1rios_e_grupos "Usuários e grupos") permissões de leitura, gravação e execução, vários [sistemas de arquivos](/index.php/File_systems "File systems") suportam atributos de arquivo que permitem uma personalização adicional das operações de arquivo permitidas. Esta seção descreve alguns desses atributos e como trabalhar com eles.

**Atenção:** Por padrão, atributos de arquivo não são preservados por [cp](/index.php/Cp_(Portugu%C3%AAs) "Cp (Português)"), [rsync](/index.php/Rsync "Rsync") e outros programas similares.

### chattr e lsattr

Para sistemas de arquivos ext2 e [ext3](/index.php/Ext3 "Ext3"), o pacote [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) contém os programas [lsattr](https://en.wikipedia.org/wiki/lsattr "wikipedia:lsattr") e [chattr](https://en.wikipedia.org/wiki/chattr "wikipedia:chattr") que listam e alteram os atributos de um arquivo, respectivamente. Embora alguns não sejam respeitados por todos os sistemas de arquivos, os atributos disponíveis são:

*   `a`: anexar apenas
*   `c`: compactado
*   `d`: sem despejo
*   `e`: formato estendido
*   `i`: imutável
*   `j`: journalling de dados
*   `s`: exclusão segura
*   `t`: sem tail-merging
*   `u`: não excluível
*   `A`: sem atualizações atime
*   `C`: sem cópia ao escrever
*   `D`: atualizações de diretório síncronas
*   `S`: atualizações síncronas
*   `T`: topo da hierarquia de diretório

Por exemplo, se você deseja definir o bit imutável em alguns arquivos, use o seguinte comando:

```
# chattr +i */caminho/para/arquivo*

```

Para remover um atributo em um arquivo, basta alterar `+` para `-`.

## Atributos estendidos

Do [xattr(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xattr.7): "Atributos estendidos são pares nome:valor associados permanentemente a arquivos e diretórios". Existem quatro classes de atributos estendidos: segurança, sistema, confiável e usuário.

**Atenção:** Por padrão, atributos estendidos não são preservados por [cp](/index.php/Cp_(Portugu%C3%AAs) "Cp (Português)"), [rsync](/index.php/Rsync "Rsync") e outros programas similares, veja [#Preservando atributos estendidos](#Preservando_atributos_estendidos).

Atributos estendidos também são usados para definir [Capacidades](/index.php/Capabilities "Capabilities").

### Atributos estendidos de usuário

Os atributos estendidos do usuário podem ser usados para armazenar informações arbitrárias sobre um arquivo. Para criar um:

```
$ setfattr -n user.checksum -v "3baf9ebce4c664ca8d9e5f6314fb47fb" foo.txt

```

Use getfattr para exibir atributos estendidos:

 `$ getfattr -d foo.txt` 
```
# file: foo.txt
user.checksum="3baf9ebce4c664ca8d9e5f6314fb47fb"
```

Finalmente, para remover um atributo estendido:

```
$ setfattr -x user.checksum foo.txt

```

### Preservando atributos estendidos

| Comando | Sinalizador necessário |
| `cp` | `--preserve=mode,ownership,timestamps,xattr` |
| `mv` | preserva, por padrão |
| `tar` | `--xattrs` para criação e extração |
| `bsdtar` | `-p` para extração |
| [rsync](/index.php/Rsync "Rsync") | `--xattrs` |

1.  mv descarta silenciosamente atributos quando o sistema de arquivos alvo não tiver suporte a eles.

Para preservar atributos estendidos com [editores de texto](/index.php/Text_editor "Text editor"), você precisa configurá-los para truncar arquivos ao salvar em vez de usar [rename(2)](https://jlk.fjfi.cvut.cz/arch/manpages/man/rename.2).[[1]](https://unix.stackexchange.com/questions/45407)

## Dicas e truques

### Preservar root

Use o sinalizador `--preserve-root` para impedir que `chmod` atue recursivamente em `/`. Isso pode, por exemplo, impedir que um remova o bit executável em todo o sistema e, assim, quebre o sistema. Para usar esse sinalizador todas as vezes, defina-o em um [alias](/index.php/Alias "Alias"). Veja também [[2]](https://www.reddit.com/r/linux/comments/4ni3xe/tifu_sudo_chmod_644/).

## Veja também

*   [wikipedia:pt:Chattr](https://en.wikipedia.org/wiki/pt:Chattr "wikipedia:pt:Chattr")
*   [Confusão nas Permissões de Arquivos no Linux](http://www.hackinglinuxexposed.com/articles/20030417.html)
*   [Confusão nas Permissões de Arquivos no Linux parte 2](http://www.hackinglinuxexposed.com/articles/20030424.html)
*   [wikipedia:Extended file attributes#Linux](https://en.wikipedia.org/wiki/Extended_file_attributes#Linux "wikipedia:Extended file attributes")
*   [Atributos estendidos: o bom, o não tão bom, o mal.](http://www.lesbonscomptes.com/pages/extattrs.html)
*   [Faça backup e restaure permissões de arquivos no Linux](http://www.concrete5.org/documentation/how-tos/designers/backup-and-restore-file-permissions-in-linux/)
*   [Por que “chmod -R 777 /” é destrutivo?](https://serverfault.com/questions/364677/why-is-chmod-r-777-destructive)