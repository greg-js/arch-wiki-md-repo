Artigos relacionados

*   [Bash](/index.php/Bash "Bash")
*   [Zsh](/index.php/Zsh "Zsh")
*   [Recomendações gerais](/index.php/Recomenda%C3%A7%C3%B5es_gerais "Recomendações gerais")
*   [Projeto GNU](/index.php/Projeto_GNU "Projeto GNU")
*   [sudo](/index.php/Sudo "Sudo")
*   [cron](/index.php/Cron "Cron")
*   [Página man](/index.php/P%C3%A1gina_man "Página man")
*   [Securely wipe disk#shred](/index.php/Securely_wipe_disk#shred "Securely wipe disk")
*   [File permissions and attributes](/index.php/File_permissions_and_attributes "File permissions and attributes")
*   [Color output in console](/index.php/Color_output_in_console "Color output in console")

Este artigo trata dos utilitários chamados *core* ("principais") em um sistema GNU/Linux, como *less*, *ls* e *grep*. O escopo deste artigo inclui, mas não está limitado a, os utilitários incluídos no pacote GNU [coreutils](https://www.archlinux.org/packages/?name=coreutils). O que se segue são várias dicas e truques e outras informações úteis relacionadas a esses utilitários.

## Contents

*   [1 Comandos básicos](#Comandos_b.C3.A1sicos)
*   [2 cat](#cat)
*   [3 dd](#dd)
*   [4 grep](#grep)
*   [5 find](#find)
*   [6 iconv](#iconv)
    *   [6.1 Converter um arquivo no lugar](#Converter_um_arquivo_no_lugar)
*   [7 ip](#ip)
*   [8 locate](#locate)
*   [9 less](#less)
    *   [9.1 Vim como alternativa de paginador](#Vim_como_alternativa_de_paginador)
*   [10 ls](#ls)
    *   [10.1 Formato longo](#Formato_longo)
    *   [10.2 Nomes de arquivos contendo espaços envoltos por aspas](#Nomes_de_arquivos_contendo_espa.C3.A7os_envoltos_por_aspas)
*   [11 lsblk](#lsblk)
*   [12 mkdir](#mkdir)
*   [13 mv](#mv)
*   [14 od](#od)
*   [15 pv](#pv)
*   [16 rm](#rm)
*   [17 sed](#sed)
*   [18 seq](#seq)
*   [19 ss](#ss)
*   [20 tar](#tar)
*   [21 which](#which)
*   [22 wipefs](#wipefs)
*   [23 Veja também](#Veja_tamb.C3.A9m)

## Comandos básicos

A tabela a seguir lista os comandos básicos do shell, cada usuário Linux deve estar familiarizado. Veja as seções abaixo e "Artigos relacionados" para obter detalhes.

| Comando | Descrição | Página de manual | Exemplo |
| man | Mostra página de manual para um comando | [man(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/man.7) | man ed |
| cd | Muda o diretório (comando embutido no shell) | [cd(1p)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cd.1p) | cd /etc/pacman.d |
| mkdir | Cria um diretório | [mkdir(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkdir.1) | mkdir ~/novapasta |
| rmdir | Remove diretório vazio | [rmdir(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/rmdir.1) | rmdir ~/pastavazia |
| rm | Remove um arquivo | [rm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/rm.1) | rm ~/file.txt |
| rm -r | Remove diretório e seu conteúdo | rm -r ~/.cache |
| ls | Lista arquivos | [ls(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ls.1) | ls *.mkv |
| ls -a | Lista arquivos ocultos | ls -a /home/archie |
| ls -al | Lista arquivos ocultos e propriedades de arquivos |
| mv | Move um arquivo | [mv(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mv.1) | mv ~/comprimido.zip ~/archive/comprimido2.zip |
| cp | Copia uma arquivo | [cp(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cp.1) | cp ~/.bashrc ~/.bashrc.bak |
| chmod +x | Torna um arquivo [executável](/index.php/Execut%C3%A1vel "Executável") | [chmod(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chmod.1) | chmod +x ~/.local/bin/meuscript.sh |
| cat | Mostrar conteúdo de arquivo | [cat(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cat.1) | cat /etc/hostname |
| strings | Mostra caracteres imprimíveis em arquivos binários | [strings(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/strings.1) | strings /usr/bin/free |
| find | Pesquisa por um arquivo | [find(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/find.1) | find ~ -name meuarquivo |
| mount | Monta uma partição | [mount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8) | mount /dev/sdc1 /media/usb |
| df -h | Mostra o espaço restante em todas as partições | [df(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/df.1) |
| ps -A | Mostra todos os processos em execução | [ps(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ps.1) |
| killall | Mata todas as instâncias em execução de um processo | [killall(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/killall.1) |
| ss -at | Exibe uma lista de sockets TCP abertos | [ss(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ss.8) |

## cat

[cat](https://en.wikipedia.org/wiki/pt:cat_(Unix) "w:pt:cat (Unix)") é um utilitário padrão do Unix que concatena e lista arquivos.

*   Porque o *cat* não é embutido no shell, em muitas ocasiões você pode achar mais conveniente usar um [redirecionamento](https://en.wikipedia.org/wiki/Redirection_(computing) "wikipedia:Redirection (computing)"), por exemplo em scripts, ou se você se preocupa muito com desempenho. De fato, `< *arquivo*` faz o mesmo que `cat *arquivo*`.

*   *cat* é capaz de trabalhar com várias linhas:

```
$ cat << EOF >> *caminho/arquivo*
*primeira linha*
...
*última linha*
EOF

```

Alternativamente, usando `printf`:

```
$ printf '%s
' 'primeira linha' ... 'última linha'

```

*   Se você precisa listar linhas na ordem reversa, há um utilitários chamado [tac](https://en.wikipedia.org/wiki/tac_(Unix) (*cat* inverso).

## dd

[dd](https://en.wikipedia.org/wiki/pt:dd_(Unix) "w:pt:dd (Unix)") é um utilitário para o Unix e sistemas operacionais similares Unix, cujo principal objetivo é converter e copiar um arquivo.

Similarmente ao *cp*, por padrão o *dd* faz cópia bit a bit do arquivo, mas com recursos de controle de fluxo de E/S de baixo nível.

**Dica:** Por padrão, *dd* emite nada até a tarefa está finalizada. Para monitorar o progresso da operação, adicione a opção `status=progress` ao comando.

Para mais informações, veja [dd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dd.1) ou da [documentação completa](https://www.gnu.org/software/coreutils/dd).

## grep

[grep](https://en.wikipedia.org/wiki/pt:grep "w:pt:grep") (de *g/re/p*, *global/regular expression/print*, do [ed](https://en.wikipedia.org/wiki/pt:Ed_(software) "w:pt:Ed (software)")) é um utilitário de pesquisa de texto de linha de comando originalmente escrito para Unix. O comando *grep* pesquisa arquivos ou entrada padrão para linhas correspondendo a uma expressão regular dada, e imprime essas linhas para a saída padrão do programa.

*   Lembre-se que *grep* trata de arquivos, então um construto como `cat *arquivo* | grep *padrão*` pode ser substituído com `grep *padrão* *arquivo*`
*   Há alternativas ao *grep* otimizadas para código fonte em VCS, tal como [the_silver_searcher](https://www.archlinux.org/packages/?name=the_silver_searcher) e [ack](https://www.archlinux.org/packages/?name=ack).
*   Para incluir números de linha de arquivo na saída, use a opção `-n`.

**Nota:** Alguns comandos enviam suas saídas para [stderr(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/stderr.3) e o grep não tem aparente efeito. Neste caso, redirecione *stderr* para *stdout* com `*comando* 2>&1 | grep *args*` ou (par Bash 4) `*comando* |& grep *args*`. Veja também [Redirecionamento de E/S](http://www.tldp.org/LDP/abs/html/io-redirection.html) (inglês).

Para suporte a cores, veja [Color output in console#grep](/index.php/Color_output_in_console#grep "Color output in console").

## find

*find* é parte do pacote [findutils](https://www.archlinux.org/packages/?name=findutils), que pertence ao grupo de pacotes [base](https://www.archlinux.org/groups/x86_64/base/).

Dica: [fd](https://github.com/sharkdp/fd) é uma alternativa moderna e amigável para usuário para `find`, que tenta melhorar desempenho e oferece padrões mais amigáveis. Por exemplo, `fd PADRÃO` em vez de `find -iname '*PADRÃO*'`. Possui saída colorida (semelhante ao `ls`), pesquisa de casos inteligentes por padrão, ignorar arquivos ocultos e muito mais. [fd](https://www.archlinux.org/packages/?name=fd)

Provavelmente se esperaria que um comando *find* levasse como argumento um nome de arquivo e pesquisasse no sistema de arquivos para arquivos que correspondessem a esse nome. Para um programa que faz exatamente isso, veja [#locate](#locate) abaixo.

Em vez disso, find leva um conjunto de diretórios e combina cada arquivo abaixo deles contra um conjunto de expressões. Este design permite alguns "one-liners" muito poderosos que não seriam possíveis usando o design "intuitivo" descrito acima. Veja [UsingFind](http://mywiki.wooledge.org/UsingFind) para detalhes de uso.

## iconv

*iconv* converte uma codificação de caracteres de um *codeset* para outro.

O seguinte comando vai converter o arquivo `*foo*` de ISO-8859-15 para UTF-8, salvando-o em `*foo*.utf`:

```
$ iconv -f ISO-8859-15 -t UTF-8 *foo* > *foo*.utf

```

Veja [iconv(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/iconv.1) para mais detalhes.

### Converter um arquivo no lugar

**Dica:** Você pode usar [recode](https://www.archlinux.org/packages/?name=recode) em vez do iconv se você não deseja tocar no mtime.

Ao contrário do [sed](#sed), *iconv* não fornece uma opção para converter um arquivo no lugar onde se encontra. Porém, `sponge` do pacote [moreutils](https://www.archlinux.org/packages/?name=moreutils) pode ajudar:

```
$ iconv -f WINDOWS-1251 -t UTF-8 *foobar*.txt | sponge *foobar*.txt

```

Veja [sponge(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sponge.1) para detalhes.

## ip

[ip](https://en.wikipedia.org/wiki/Iproute2 "wikipedia:Iproute2") permite que você mostre informações sobre dispositivos de rede, endereços IP, tabelas de roteamento e outros objetos no Linux. Software de [IP](https://en.wikipedia.org/wiki/pt:Protocolo_de_Internet "w:pt:Protocolo de Internet"). Ao anexar vários comandos, você também pode manipular ou configurar a maioria desses objetos.

**Nota:** O utilitário *ip* é fornecido pelo pacote [iproute2](https://www.archlinux.org/packages/?name=iproute2), que está incluído no grupo [base](https://www.archlinux.org/groups/x86_64/base/).

| Objeto | Propósito | Página de manual |
| ip addr | gerenciamento de endereço de protocolo | [ip-address(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-address.8) |
| ip addrlabel | gerenciamento de rótulo de endereço de protocolo | [ip-addrlabel(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-addrlabel.8) |
| ip l2tp | tunelamento de Ethernet over IP (L2TPv3) | [ip-l2tp(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-l2tp.8) |
| ip link | configuração de dispositivo de rede | [ip-link(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-link.8) |
| ip maddr | gerenciamento de endereços de multicast | [ip-maddress(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-maddress.8) |
| ip monitor | monitore por mensagens de netlink | [ip-monitor(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-monitor.8) |
| ip mroute | gerenciamento de cache de roteamento de multicast | [ip-mroute(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-mroute.8) |
| ip mrule | regra no banco de dados de política de roteamento multicast |
| ip neigh | gerenciamento de tabelas de vizinhança/ARP | [ip-neighbour(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-neighbour.8) |
| ip netns | gerenciamento de espaço de nome de rede de processo | [ip-netns(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-netns.8) |
| ip ntable | configuração de tabela de vizinhança | [ip-ntable(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-ntable.8) |
| ip route | gerenciamento de tabela de roteamento | [ip-route(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-route.8) |
| ip rule | gerenciamento de banco de dados de políticas de roteamento | [ip-rule(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-rule.8) |
| ip tcp_metrics | gerenciamento para Métricas de TCP | [ip-tcp_metrics(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-tcp_metrics.8) |
| ip tunnel | configuração de tunel | [ip-tunnel(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-tunnel.8) |
| ip tuntap | gerencia dispositivos TUN/TAP |
| ip xfrm | gerencia políticas IPsec | [ip-xfrm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-xfrm.8) |

O comando `help` está disponível para todos os objetos. Por exemplo, digitar `ip addr help` mostrará a você a sintaxe de comando disponível para o objeto do endereço. Para uso avançado, veja o [documentação do iproute2](http://www.policyrouting.org/iproute2.doc.html).

O artigo [Configuração de rede](/index.php/Configura%C3%A7%C3%A3o_de_rede "Configuração de rede") mostra como o comando *ip* é usado na prática para várias tarefas comuns.

**Nota:** Você pode estar familiarizado com o comando [ifconfig](https://en.wikipedia.org/wiki/ifconfig "wikipedia:ifconfig"), que era usado em versões antigas do Linux para configuração de interface. Ele está obsoleto no Arch Linux; em vez dele, você deve usar o *ip*.

## locate

[Instale](/index.php/Instale "Instale") o pacote [mlocate](https://www.archlinux.org/packages/?name=mlocate). O pacote contém uma unidade `updatedb.timer`, que invoca uma atualização do banco de dados a cada dia. O temporizador é ativado logo após a instalação, [inicie](/index.php/Inicie "Inicie") manualmente se você quiser usá-lo antes de reiniciar. Você também pode executar manualmente *updatedb* como root a qualquer momento. Por padrão, os caminhos como `/media` e `/mnt` são ignorados, portanto, *locate* pode não descobrir arquivos em dispositivos externos. Veja a [updatedb(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/updatedb.8) para obter detalhes.

O comando *locate* é uma ferramenta Unix comum para encontrar rapidamente arquivos pelo nome. Ele oferece melhorias de velocidade ao longo da ferramenta [find](https://en.wikipedia.org/wiki/pt:Find "w:pt:Find") pesquisando um arquivo de banco de dados pré-construído, em vez do sistema de arquivos diretamente. A desvantagem dessa abordagem é que as mudanças feitas desde a construção do arquivo de banco de dados não podem ser detectadas pelo *locate*.

Antes que o *locate* possa ser usado, o banco de dados precisará ser criado. Para fazer isso, execute `updatedb` como root.

Veja também [How locate works and rewrite it in one minute](http://jvns.ca/blog/2015/03/05/how-the-locate-command-works-and-lets-rewrite-it-in-one-minute/) ("Como locate funciona e rescreva-o em um minuto").

## less

[less](https://en.wikipedia.org/wiki/pt:less "w:pt:less") é um programa paginador de terminal usado para visualizar os conteúdos de um arquivo texto uma tela por vez. Embora parecido com outros paginadores, como o [more](https://en.wikipedia.org/wiki/pt:more_(comando) "w:pt:more (comando)") e [pg](https://en.wikipedia.org/wiki/pg_(Unix) "wikipedia:pg (Unix)"), *less* oferece uma interface mais avançada e um [conjunto de recursos](http://www.greenwoodsoftware.com/less/faq.html) mais completo.

Veja [List of applications#Terminal pagers](/index.php/List_of_applications#Terminal_pagers "List of applications") para alternativas.

### Vim como alternativa de paginador

[Vim](/index.php/Vim "Vim") inclui um script para visualizar o conteúdo de arquivos texto, arquivos comprimidos, binários e diretórios. Adicione a seguinte linha para o arquivo de configuração do seu shell para usá-lo como paginador:

 `~/.bashrc`  `alias less='/usr/share/vim/vim80/macros/less.sh'` 

Há também uma alternativa para a macro *less.sh*, que pode funcionar como a variável de ambiente `PAGER`. Instale [vimpager](https://www.archlinux.org/packages/?name=vimpager) e adicione o seguinte para o arquivo de configuração do seu shell:

 `~/.bashrc` 
```
export PAGER='vimpager'
alias less=$PAGER
```

Agora, programas que usam a variável de ambiente `PAGER`, como o [git](/index.php/Git "Git"), vão usar *vim* como paginador.

## ls

[ls](https://en.wikipedia.org/wiki/pt:ls "w:pt:ls") lista conteúdos de diretório.

Veja `info ls` ou [o manual online](https://www.gnu.org/software/coreutils/manual/html_node/ls-invocation.html#ls-invocation) para mais informações.

[exa](https://the.exa.website) é uma alternativa moderna e mais amigável para o `ls` e `tree`, que possui mais recursos, tal como exibir modificações [Git](/index.php/Git "Git") junto com nomes de arquivos, colorizando diferentemente cada coluna no modo `--long`, ou exibindo no modo `--long` metadados junto com uma visão `tree`. [exa](https://www.archlinux.org/packages/?name=exa)

### Formato longo

A opção `-l` exibe alguns metadados, por exemplo:

 `$ ls -l */caminho/para/diretório*` 
```
total 128
drwxr-xr-x 2 archie users  4096 Jul  5 21:03 'Área de trabalho'
drwxr-xr-x 6 archie users  4096 Jul  5 17:37 Documentos
drwxr-xr-x 2 archie users  4096 Jul  5 13:45 Downloads
-rw-rw-r-- 1 archie users  5120 Jun 27 08:28 clientes.ods
-rw-r--r-- 1 archie users  3339 Jun 27 08:28 'a fazer'
-rwxr-xr-x 1 archie users  2048 Jul  6 12:56 meuscript.sh

```

O valor `total` representa a alocação de disco total para os arquivos no diretório, por padrão em número de blocos.

Abaixo, cada arquivo e subdiretório está representado por uma linha dividida em 7 campos de metadados, na ordem a seguir:

*   tipo e permissões:
    *   o primeiro caractere é o tipo de entrada, veja `info ls -n "What information is listed"` para uma explicação de todos os tipos possíveis; por exemplo:
        *   `-` denota um arquivo normal;
        *   `d` denota um diretório, isto é, uma pasta contendo outros arquivos ou pastas;
        *   `p` denota um pipe dado (também conhecido como FIFO);
        *   `l` denota um link simbólico;
    *   os caracteres restantes são [permissões](/index.php/Permissions "Permissions") da entrada;
*   número de [links absolutos](https://en.wikipedia.org/wiki/Hard_link "wikipedia:Hard link") para a entidade; arquivos serão pelo menos 1, isto é, a própria referência mostrada; as pastas terão pelo menos 2: a referência mostrada, entrada `.` autorreferenciada, e então uma entrada `..` em cada uma dessas subpastas;
*   nome do [usuário](/index.php/Usu%C3%A1rio "Usuário") dono;
*   nome do [grupo](/index.php/Grupo "Grupo");
*   tamanho;
*   marca de tempo da última modificação;
*   nome da entidade.

### Nomes de arquivos contendo espaços envoltos por aspas

Por padrão, nomes de arquivos e diretórios que contêm espaços são exibidos envoltos por aspas simples. Para alterar esse comportamento, use as opções `-N` ou `--quoting-style=literal`. Alternativamente, defina a [variável de ambiente](/index.php/Vari%C3%A1vel_de_ambiente "Variável de ambiente") `QUOTING_STYLE` para `literal`. [[1]](https://unix.stackexchange.com/questions/258679/why-is-ls-suddenly-surrounding-items-with-spaces-in-single-quotes)

## lsblk

[lsblk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lsblk.8) vai mostrar todos os [dispositivos de blocos](https://en.wikipedia.org/wiki/pt:Arquivo_de_dispositivo#Dispositivos_de_bloco "w:pt:Arquivo de dispositivo") disponíveis junto com seus esquemas de particionamento, por exemplo:

 `$ lsblk -f` 
```
NAME   FSTYPE   LABEL       UUID                                 MOUNTPOINT
sda
├─sda1 vfat                 C4DA-2C4D                            /boot
├─sda2 swap                 5b1564b2-2e2c-452c-bcfa-d1f572ae99f2 [SWAP]
└─sda3 ext4                 56adc99b-a61e-46af-aab7-a6d07e504652 /

```

O início do nome do dispositivo especifica o tipo de dispositivo de bloco. A maioria dos dispositivos de armazenamento modernos (por exemplo, discos rígidos, [SSDs](/index.php/SSD "SSD") e unidades flash USB) é reconhecida como disco SCSI (`sd`). O tipo é seguido por uma letra minúscula a partir de `a` para o primeiro dispositivo (`sda`), `b` para o segundo dispositivo (`sdb`), e assim por diante. As partições "existentes" em cada dispositivo serão listadas com um número a partir de `1` para a primeira partição (`sda1`), `2` para a segunda (`sda2`), e assim por diante. No exemplo acima, apenas um dispositivo está disponível (`sda`) e esse dispositivo possui três partições (`sda1` para `sda3`), cada uma com um [sistema de arquivo](/index.php/File_system "File system").

Outros tipos comuns de dispositivos de blocos incluem, por exemplo, `mmcblk` para cartões de memória e `nvme` para dispositivos [NVMe](/index.php/NVMe "NVMe"). Tipos desconhecidos podem ser pesquisados na [documentação do kernel](https://web.archive.org/web/20161221203124/https://www.kernel.org/doc/Documentation/devices.txt).

## mkdir

[mkdir](https://en.wikipedia.org/wiki/pt:mkdir "w:pt:mkdir") cria diretórios.

Para criar um diretório e toda sua hierarquia, a opção `-p` é usada; do contrário, um erro é impresso. Como os usuários devem saber o que eles querem, a opção `-p` pode ser usada como padrão:

```
alias mkdir='mkdir -p -v'

```

A opção `-v` o torna verboso.

Alterar o modo de um diretório recém-criado usando *chmod* não é necessário como a opção `-m` permite que você defina as permissões de acesso.

**Dica:** Se você já quer um diretório temporário, uma alternativa melhor pode ser o [mktemp](https://en.wikipedia.org/wiki/Temporary_file "wikipedia:Temporary file"): `mktemp -p`.

## mv

[mv](https://en.wikipedia.org/wiki/pt:mv_(Unix) "w:pt:mv (Unix)") move e renomeia arquivos e diretórios.

Para limitar dano potencial causado pelo comando, use um alias:

```
alias mv='timeout 8 mv -iv'

```

Esse alias suspende *mv* após 8 segundos, pede confirmação antes de sobrescrever quaisquer arquivos existentes, lista as operações em progresso e não armazena ele mesmo no arquivo de histórico do shell se o shell estiver configurado para ignorar comandos iniciando com espaço.

## od

O comando [od](https://en.wikipedia.org/wiki/od_(Unix) (*o*ctal *d*ump) é útil para visualizar dados que não estejam em um formato legível por humanos, como o código executável de um programa, ou o conteúdo de um dispositivo não formatado. Veja o [manual](https://www.gnu.org/software/coreutils/manual/html_node/od-invocation.html#od-invocation) para mais informações.

## pv

Você pode usar [pv](https://www.archlinux.org/packages/?name=pv) (*pipe viewer*) para monitorar o progresso de dados por meio de um *pipeline*, por exemplo:

```
# dd if=*/origem/fluxo_arquivo* | pv -*opções_monitoramento* -s *tam_de_arquivo* | dd of=*/destino/fluxo_arquivo*

```

Na maioria dos casos, `pv` funciona como um substituto para `cat`.

## rm

[rm](https://en.wikipedia.org/wiki/pt:rm_(Unix) "w:pt:rm (Unix)") remove arquivos ou diretórios.

Para limitar danos potenciais causados pelo comando, use um alias:

```
alias rm='timeout 3 rm -Iv --one-file-system'

```

Este alias suspende *rm* após três segundos, solicita confirmação para excluir três ou mais arquivos, lista as operações em andamento, não envolve mais de um sistema de arquivos e não se armazena no arquivo de histórico de shell se o shell estiver configurado para ignorar os comandos iniciais do espaço. Substitua `-I` por `-i` se preferir confirmar mesmo para um arquivo.

Usuários do zsh podem querer colocar `noglob` antes de `timeout` para evitar expansões implícitas.

Para remover diretórios que se acredita estarem vazios, use *rmdir*, pois ele falha se houver arquivos dentro do alvo.

## sed

[sed](https://en.wikipedia.org/wiki/pt:sed "w:pt:sed") é um editor do fluxo para filtrar e transformar texto.

Aqui está uma [lista](http://sed.sourceforge.net/sed1line.txt) útil de exemplos de um só linha com *sed*.

**Dica:** Alternativas mais poderosa são [AWK](https://en.wikipedia.org/wiki/pt:AWK "w:pt:AWK") e o idioma [Perl](https://en.wikipedia.org/wiki/pt:Perl "w:pt:Perl").

## seq

*seq* imprime uma sequência de números. Alternativas embutidas em shell estão disponíveis, então é de boa prática usá-las como explicado no [wikipédia](https://en.wikipedia.org/wiki/Seq_(Unix) "wikipedia:Seq (Unix)").

## ss

*ss* é um utilitário par investigar portas de rede e é parte do pacote [iproute2](https://www.archlinux.org/packages/?name=iproute2) no grupo [base](https://www.archlinux.org/groups/x86_64/base/). Tem uma funcionalidade similar ao utilitário [obsoleto](http://www.archlinux-br.org/noticias/155/) netstat.

Uso comum inclui:

Exiba todos os soquetes TCP com nomes de serviços:

```
$ ss -at

```

Exiba todos os soquetes TCP com números de portas:

```
$ ss -atn

```

Exiba todos os soquetes UDP:

```
$ ss -au

```

Para mais informações, veja [ss(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ss.8) ou `ss.html` do pacote [iproute2](https://www.archlinux.org/packages/?name=iproute2).

## tar

Como um formato de arquivamento antigo do Unix, arquivos .tar – conhecidos como "tarballs" – são amplamente usados para empacotamento nos sistema operacionais tipo Unix. Os pacotes de tanto o [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") quanto [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)") são comprimidos em tarballs, e o Arch usa o programa *tar* do [Projeto GNU](/index.php/Projeto_GNU "Projeto GNU") por padrão.

Para pacotes .tar, *tar* por padrão vai extrair o arquivo conforme sua extensão:

```
$ tar xvf *arquivo.EXTENSÃO*

```

Forçando um formato dado:

| Tipo de arquivo | Comando de extração |
| `*arquivo*.tar` | `tar xvf *arquivo*.tar` |
| `*arquivo*.tgz` | `tar xvzf *arquivo*.tgz` |
| `*arquivo*.tar.gz` | `tar xvzf *arquivo*.tar.gz` |
| `*arquivo*.tar.bz` | `bzip -cd *arquivo*.bz | tar xvf -` |
| `*arquivo*.tar.bz2` | `tar xvjf *arquivo*.tar.bz2`
`bzip2 -cd *arquivo*.bz2 | tar xvf -` |
| `*arquivo*.tar.xz` | `tar xvJf *arquivo*.tar.xz`
`xz -cd *arquivo*.xz | tar xvf -` |

A construção de alguns dos argumentos do *tar* podem ser considerado legado, mas eles ainda são úteis ao realizar operações específicas. Veja [tar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tar.1) para detalhes.

## which

[which](https://en.wikipedia.org/wiki/Which_(Unix) mostra o caminho completo de comandos shells. No exemplo a seguir, o caminho completo de `ssh` é usado como argumento para `journalctl`:

```
# journalctl $(which sshd)

```

## wipefs

*wipefs* pode listar ou apagar assinaturas de [sistema de arquivos](/index.php/File_system "File system"), [RAID](/index.php/RAID "RAID") ou [tabela de partições](/index.php/Partition "Partition") (strings mágicas) do dispositivo específico. Ela não apaga os sistemas de arquivos em si nem quaisquer outros dados do dispositivo.

Veja [wipefs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wipefs.8) para mais informações.

Por exemplo, para apagar todas as assinaturas do dispositivo `/dev/sdb` e criar uma arquivo backup de assinatura `~/wipefs-sdb-*deslocamento*.bak` para cada assinatura:

```
# wipefs --all --backup /dev/sdb

```

## Veja também

*   [Uma amostra do coreutils](http://www.reddit.com/r/commandline/comments/19garq/a_sampling_of_coreutils_120/) [, parte 2](http://www.reddit.com/r/commandline/comments/19ge6v/a_sampling_of_coreutils_2040/) [, parte 3](http://www.reddit.com/r/commandline/comments/19j1w3/a_sampling_of_coreutils_4060/) - Visão geral de comandos no coreutils
*   [Documentação online do GNU Coreutils](https://www.gnu.org/software/coreutils/manual/coreutils.html)
*   [Aprenda o comando DD](https://www.linuxquestions.org/questions/linux-newbie-8/learn-the-dd-command-362506/)