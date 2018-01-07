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
| man | Mostra página de manual para um comando | [man(7)](http://jlk.fjfi.cvut.cz/arch/manpages/man/man.7) | man ed |
| cd | Muda o diretório (comando embutido no shell) | [cd(1p)](http://jlk.fjfi.cvut.cz/arch/manpages/man/cd.1p) | cd /etc/pacman.d |
| mkdir | Cria um diretório | [mkdir(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/mkdir.1) | mkdir ~/novapasta |
| rmdir | Remove diretório vazio | [rmdir(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/rmdir.1) | rmdir ~/pastavazia |
| rm | Remove um arquivo | [rm(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/rm.1) | rm ~/file.txt |
| rm -r | Remove diretório e seu conteúdo | rm -r ~/.cache |
| ls | Lista arquivos | [ls(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/ls.1) | ls *.mkv |
| ls -a | Lista arquivos ocultos | ls -a /home/archie |
| ls -al | Lista arquivos ocultos e propriedades de arquivos |
| mv | Move um arquivo | [mv(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/mv.1) | mv ~/comprimido.zip ~/archive/comprimido2.zip |
| cp | Copia uma arquivo | [cp(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/cp.1) | cp ~/.bashrc ~/.bashrc.bak |
| chmod +x | Torna um arquivo [executável](/index.php/Execut%C3%A1vel "Executável") | [chmod(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/chmod.1) | chmod +x ~/.local/bin/meuscript.sh |
| cat | Mostrar conteúdo de arquivo | [cat(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/cat.1) | cat /etc/hostname |
| strings | Mostra caracteres imprimíveis em arquivos binários | [strings(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/strings.1) | strings /usr/bin/free |
| find | Pesquisa por um arquivo | [find(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/find.1) | find ~ -name meuarquivo |
| mount | Monta uma partição | [mount(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8) | mount /dev/sdc1 /media/usb |
| df -h | Mostra o espaço restante em todas as partições | [df(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/df.1) |
| ps -A | Mostra todos os processos em execução | [ps(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/ps.1) |
| killall | Mata todas as instâncias em execução de um processo | [killall(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/killall.1) |
| ss -at | Exibe uma lista de sockets TCP abertos | [ss(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/ss.8) |

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

**Dica:** Por padrão, *dd* emite nada até a tarefa está finalizada. Para monitorar o progresso da operação, adicione a opção `status=progress` ao comando. Ela não está disponível em versões antigas (antes 8.24) do [coreutils](https://www.archlinux.org/packages/?name=coreutils).

Para mais informações, veja [dd(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/dd.1) ou da [documentação completa](https://www.gnu.org/software/coreutils/dd).

## grep

[grep](https://en.wikipedia.org/wiki/pt:grep "w:pt:grep") (de *g/re/p*, *global/regular expression/print*, do [ed](https://en.wikipedia.org/wiki/pt:Ed_(software) "w:pt:Ed (software)")) é um utilitário de pesquisa de texto de linha de comando originalmente escrito para Unix. O comando *grep* pesquisa arquivos ou entrada padrão para linhas correspondendo a uma expressão regular dada, e imprime essas linhas para a saída padrão do programa.

*   Lembre-se que *grep* trata de arquivos, então um construto como `cat *arquivo* | grep *padrão*` pode ser substituído com `grep *padrão* *arquivo*`
*   Há alternativas ao *grep* otimizadas para código fonte em VCS, tal como [the_silver_searcher](https://www.archlinux.org/packages/?name=the_silver_searcher) e [ack](https://www.archlinux.org/packages/?name=ack).
*   Para incluir números de linha de arquivo na saída, use a opção `-n`.

**Nota:** Alguns comandos enviam suas saídas para [stderr(3)](http://jlk.fjfi.cvut.cz/arch/manpages/man/stderr.3) e o grep não tem aparente efeito. Neste caso, redirecione *stderr* para *stdout* com `*comando* 2>&1 | grep *args*` ou (par Bash 4) `*comando* |& grep *args*`. Veja também [Redirecionamento de E/S](http://www.tldp.org/LDP/abs/html/io-redirection.html) (inglês).

Para suporte a cores, veja [Color output in console#grep](/index.php/Color_output_in_console#grep "Color output in console").

## find

*find* é parte do pacote [findutils](https://www.archlinux.org/packages/?name=findutils), que pertence ao grupo de pacotes [base](https://www.archlinux.org/groups/x86_64/base/).

Provavelmente se esperaria que um comando *find* levasse como argumento um nome de arquivo e pesquisasse no sistema de arquivos para arquivos que correspondessem a esse nome. Para um programa que faz exatamente isso, veja [#locate](#locate) abaixo.

Em vez disso, find leva um conjunto de diretórios e combina cada arquivo abaixo deles contra um conjunto de expressões. Este design permite alguns "one-liners" muito poderosos que não seriam possíveis usando o design "intuitivo" descrito acima. Veja [UsingFind](http://mywiki.wooledge.org/UsingFind) para detalhes de uso.

## iconv

*iconv* converte uma codificação de caracteres de um *codeset* para outro.

O seguinte comando vai converter o arquivo `*foo*` de ISO-8859-15 para UTF-8, salvando-o em `*foo*.utf`:

```
$ iconv -f ISO-8859-15 -t UTF-8 *foo* > *foo*.utf

```

Veja [iconv(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/iconv.1) para mais detalhes.

### Converter um arquivo no lugar

**Dica:** Você pode usar [recode](https://www.archlinux.org/packages/?name=recode) em vez do iconv se você não deseja tocar no mtime.

Ao contrário do [sed](#sed), *iconv* não fornece uma opção para converter um arquivo no lugar onde se encontra. Porém, `sponge` do pacote [moreutils](https://www.archlinux.org/packages/?name=moreutils) pode ajudar:

```
$ iconv -f WINDOWS-1251 -t UTF-8 *foobar*.txt | sponge *foobar*.txt

```

Veja [sponge(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/sponge.1) para detalhes.

## ip

[ip](https://en.wikipedia.org/wiki/Iproute2 "wikipedia:Iproute2") allows you to show information about network devices, IP addresses, routing tables, and other objects in the Linux [IP](https://en.wikipedia.org/wiki/Internet_Protocol "wikipedia:Internet Protocol") software stack. By appending various commands, you can also manipulate or configure most of these objects.

**Note:** The *ip* utility is provided by the [iproute2](https://www.archlinux.org/packages/?name=iproute2) package, which is included in the [base](https://www.archlinux.org/groups/x86_64/base/) group.

| Object | Purpose | Manual page |
| ip addr | protocol address management | [ip-address(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/ip-address.8) |
| ip addrlabel | protocol address label management | [ip-addrlabel(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/ip-addrlabel.8) |
| ip l2tp | tunnel Ethernet over IP (L2TPv3) | [ip-l2tp(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/ip-l2tp.8) |
| ip link | network device configuration | [ip-link(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/ip-link.8) |
| ip maddr | multicast addresses management | [ip-maddress(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/ip-maddress.8) |
| ip monitor | watch for netlink messages | [ip-monitor(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/ip-monitor.8) |
| ip mroute | multicast routing cache management | [ip-mroute(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/ip-mroute.8) |
| ip mrule | rule in multicast routing policy db |
| ip neigh | neighbour/ARP tables management | [ip-neighbour(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/ip-neighbour.8) |
| ip netns | process network namespace management | [ip-netns(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/ip-netns.8) |
| ip ntable | neighbour table configuration | [ip-ntable(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/ip-ntable.8) |
| ip route | routing table management | [ip-route(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/ip-route.8) |
| ip rule | routing policy database management | [ip-rule(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/ip-rule.8) |
| ip tcp_metrics | management for TCP Metrics | [ip-tcp_metrics(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/ip-tcp_metrics.8) |
| ip tunnel | tunnel configuration | [ip-tunnel(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/ip-tunnel.8) |
| ip tuntap | manage TUN/TAP devices |
| ip xfrm | manage IPsec policies | [ip-xfrm(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/ip-xfrm.8) |

The `help` command is available for all objects. For example, typing `ip addr help` will show you the command syntax available for the address object. For advanced usage see the [iproute2 documentation](http://www.policyrouting.org/iproute2.doc.html).

The [Network configuration](/index.php/Network_configuration "Network configuration") article shows how the *ip* command is used in practice for various common tasks.

**Note:** You might be familiar with the [ifconfig](https://en.wikipedia.org/wiki/ifconfig "wikipedia:ifconfig") command, which was used in older versions of Linux for interface configuration. It is now deprecated in Arch Linux; you should use *ip* instead.

## locate

[Install](/index.php/Install "Install") the [mlocate](https://www.archlinux.org/packages/?name=mlocate) package. The package contains an `updatedb.timer` unit, which invokes a database update each day. The timer is enabled right after installation, [start](/index.php/Start "Start") it manually if you want to use it before reboot. You can also manually run *updatedb* as root at any time. By default, paths such as `/media` and `/mnt` are ignored, so *locate* may not discover files on external devices. See [updatedb(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/updatedb.8) for details.

The *locate* command is a common Unix tool for quickly finding files by name. It offers speed improvements over the [find](https://en.wikipedia.org/wiki/Find "wikipedia:Find") tool by searching a pre-constructed database file, rather than the filesystem directly. The downside of this approach is that changes made since the construction of the database file cannot be detected by *locate*.

Before *locate* can be used, the database will need to be created. To do this, execute `updatedb` as root.

See also [How locate works and rewrite it in one minute](http://jvns.ca/blog/2015/03/05/how-the-locate-command-works-and-lets-rewrite-it-in-one-minute/).

## less

[less](https://en.wikipedia.org/wiki/less_(Unix) is a terminal pager program used to view the contents of a text file one screen at a time. Whilst similar to other pagers such as [more](https://en.wikipedia.org/wiki/more_(command) and [pg](https://en.wikipedia.org/wiki/pg_(Unix) "wikipedia:pg (Unix)"), *less* offers a more advanced interface and complete [feature-set](http://www.greenwoodsoftware.com/less/faq.html).

See [List of applications#Terminal pagers](/index.php/List_of_applications#Terminal_pagers "List of applications") for alternatives.

### Vim como alternativa de paginador

[Vim](/index.php/Vim "Vim") includes a script to view the content of text files, compressed files, binaries and directories. Add the following line to your shell configuration file to use it as a pager:

 `~/.bashrc`  `alias less='/usr/share/vim/vim80/macros/less.sh'` 

There is also an alternative to the *less.sh* macro, which may work as the `PAGER` environment variable. Install [vimpager](https://www.archlinux.org/packages/?name=vimpager) and add the following to your shell configuration file:

 `~/.bashrc` 
```
export PAGER='vimpager'
alias less=$PAGER
```

Now programs that use the `PAGER` environment variable, like [git](/index.php/Git "Git"), will use *vim* as pager.

## ls

[ls](https://en.wikipedia.org/wiki/ls "wikipedia:ls") lists directory contents.

See `info ls` or [the online manual](https://www.gnu.org/software/coreutils/manual/html_node/ls-invocation.html#ls-invocation) for more information.

### Formato longo

The `-l` option displays some metadata, for example:

 `$ ls -l */path/to/directory*` 
```
total 128
drwxr-xr-x 2 archie users  4096 Jul  5 21:03 Desktop
drwxr-xr-x 6 archie users  4096 Jul  5 17:37 Documents
drwxr-xr-x 2 archie users  4096 Jul  5 13:45 Downloads
-rw-rw-r-- 1 archie users  5120 Jun 27 08:28 customers.ods
-rw-r--r-- 1 archie users  3339 Jun 27 08:28 todo
-rwxr-xr-x 1 archie users  2048 Jul  6 12:56 myscript.sh

```

The `total` value represents the total disk allocation for the files in the directory, by default in number of blocks.

Below, each file and subdirectory is represented by a line divided into 7 metadata fields, in the following order:

*   type and permissions:
    *   the first character is the entry type, see `info ls -n "What information is listed"` for an explanation of all the possible types; for example:
        *   `-` denotes a normal file;
        *   `d` denotes a directory, i.e. a folder containing other files or folders;
        *   `p` denotes a named pipe (aka FIFO);
        *   `l` denotes a symbolic link;
    *   the remaining characters are the entry's [permissions](/index.php/Permissions "Permissions");
*   number of [hard links](https://en.wikipedia.org/wiki/Hard_link "wikipedia:Hard link") for the entity; files will have at least 1, i.e. the showed reference itself; folders will have at least 2: the showed reference, the self-referencing `.` entry, and then a `..` entry in each of its subfolders;
*   owner [user](/index.php/User "User") name;
*   [group](/index.php/Group "Group") name;
*   size;
*   last modification timestamp;
*   entity name.

### Nomes de arquivos contendo espaços envoltos por aspas

By default, file and directory names that contain spaces are displayed surrounded by single quotes. To change this behavior use the `-N` or `--quoting-style=literal` options. Alternatively, set the `QUOTING_STYLE` [environment variable](/index.php/Environment_variable "Environment variable") to `literal`. [[1]](https://unix.stackexchange.com/questions/258679/why-is-ls-suddenly-surrounding-items-with-spaces-in-single-quotes)

## lsblk

[lsblk(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/lsblk.8) will show all available [block devices](https://en.wikipedia.org/wiki/Device_file#Block_devices "w:Device file") along with their partitioning schemes, for example:

 `$ lsblk -f` 
```
NAME   FSTYPE   LABEL       UUID                                 MOUNTPOINT
sda
├─sda1 vfat                 C4DA-2C4D                            /boot
├─sda2 swap                 5b1564b2-2e2c-452c-bcfa-d1f572ae99f2 [SWAP]
└─sda3 ext4                 56adc99b-a61e-46af-aab7-a6d07e504652 /

```

The beginning of the device name specifies the type of block device. Most modern storage devices (e.g. hard disks, [SSDs](/index.php/SSD "SSD") and USB flash drives) are recognised as SCSI disks (`sd`). The type is followed by a lower-case letter starting from `a` for the first device (`sda`), `b` for the second device (`sdb`), and so on. *Existing* partitions on each device will be listed with a number starting from `1` for the first partition (`sda1`), `2` for the second (`sda2`), and so on. In the example above, only one device is available (`sda`), and that device has three partitions (`sda1` to `sda3`), each with a different [file system](/index.php/File_system "File system").

Other common block device types include for example `mmcblk` for memory cards and `nvme` for [NVMe](/index.php/NVMe "NVMe") devices. Unknown types can be searched in the [kernel documentation](https://www.kernel.org/doc/Documentation/devices.txt).

## mkdir

[mkdir](https://en.wikipedia.org/wiki/mkdir "wikipedia:mkdir") makes directories.

To create a directory and its whole hierarchy, the `-p` switch is used, otherwise an error is printed. As users are supposed to know what they want, `-p` switch may be used as a default:

```
alias mkdir='mkdir -p -v'

```

The `-v` switch make it verbose.

Changing mode of a just created directory using *chmod* is not necessary as the `-m` option lets you define the access permissions.

**Tip:** If you just want a temporary directory, a better alternative may be [mktemp](https://en.wikipedia.org/wiki/Temporary_file "wikipedia:Temporary file"): `mktemp -p`.

## mv

[mv](https://en.wikipedia.org/wiki/mv "wikipedia:mv") moves and renames files and directories.

To limit potential damage caused by the command, use an alias:

```
alias mv='timeout 8 mv -iv'

```

This alias suspends *mv* after eight seconds, asks for confirmation before overwriting any existing files, lists the operations in progress and does not store itself in the shell history file if the shell is configured to ignore space starting commands.

## od

The [od](https://en.wikipedia.org/wiki/od_(Unix) (*o*ctal *d*ump) command is useful for visualizing data that is not in a human-readable format, like the executable code of a program, or the contents of an unformatted device. See the [manual](https://www.gnu.org/software/coreutils/manual/html_node/od-invocation.html#od-invocation) for more information.

## pv

You can use [pv](https://www.archlinux.org/packages/?name=pv) (*pipe viewer*) to monitor the progress of data through a pipeline, for example:

```
# dd if=*/source/filestream* | pv -*monitor_options* -s *size_of_file* | dd of=*/destination/filestream*

```

In most cases `pv` functions as a drop-in replacement for `cat`.

## rm

[rm](https://en.wikipedia.org/wiki/rm_(Unix) removes files or directories.

To limit potential damage caused by the command, use an alias:

```
alias rm='timeout 3 rm -Iv --one-file-system'

```

This alias suspends *rm* after three seconds, asks confirmation to delete three or more files, lists the operations in progress, does not involve more than one file systems and does not store itself in the shell history file if the shell is configured to ignore space starting commands. Substitute `-I` with `-i` if you prefer to confirm even for one file.

Zsh users may want to put `noglob` before `timeout` to avoid implicit expansions.

To remove directories believed to be empty, use *rmdir* as it fails if there are files inside the target.

## sed

[sed](https://en.wikipedia.org/wiki/sed "wikipedia:sed") is stream editor for filtering and transforming text.

Here is a handy [list](http://sed.sourceforge.net/sed1line.txt) of *sed* one-liners examples.

**Tip:** More powerful alternatives are [AWK](https://en.wikipedia.org/wiki/AWK "wikipedia:AWK") and the [Perl](https://en.wikipedia.org/wiki/Perl "wikipedia:Perl") language.

## seq

*seq* prints a sequence of numbers. Shell built-in alternatives are available, so it is good practice to use them as explained on [Wikipedia](https://en.wikipedia.org/wiki/Seq_(Unix) "wikipedia:Seq (Unix)").

## ss

*ss* is a utility to investigate network ports and is part of the [iproute2](https://www.archlinux.org/packages/?name=iproute2) package in the [base](https://www.archlinux.org/groups/x86_64/base/) group. It has a similar functionality to the [deprecated](https://www.archlinux.org/news/deprecation-of-net-tools/) netstat utility.

Common usage includes:

Display all TCP Sockets with service names:

```
$ ss -at

```

Display all TCP Sockets with port numbers:

```
$ ss -atn

```

Display all UDP Sockets:

```
$ ss -au

```

For more information see [ss(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/ss.8) or `ss.html` from the [iproute2](https://www.archlinux.org/packages/?name=iproute2) package.

## tar

As an early Unix archiving format, .tar files—known as "tarballs"—are widely used for packaging in Unix-like operating systems. Both [pacman](/index.php/Pacman "Pacman") and [AUR](/index.php/AUR "AUR") packages are compressed tarballs, and Arch uses [GNU's](/index.php/GNU_Project "GNU Project") *tar* program by default.

For .tar archives, *tar* by default will extract the file according to its extension:

```
$ tar xvf *file.EXTENSION*

```

Forcing a given format:

| File Type | Extraction Command |
| `*file*.tar` | `tar xvf *file*.tar` |
| `*file*.tgz` | `tar xvzf *file*.tgz` |
| `*file*.tar.gz` | `tar xvzf *file*.tar.gz` |
| `*file*.tar.bz` | `bzip -cd *file*.bz | tar xvf -` |
| `*file*.tar.bz2` | `tar xvjf *file*.tar.bz2`
`bzip2 -cd *file*.bz2 | tar xvf -` |
| `*file*.tar.xz` | `tar xvJf *file*.tar.xz`
`xz -cd *file*.xz | tar xvf -` |

The construction of some of these *tar* arguments may be considered legacy, but they are still useful when performing specific operations. See [tar(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/tar.1) for details.

## which

[which](https://en.wikipedia.org/wiki/Which_(Unix) shows the full path of shell commands. In the following example the full path of `ssh` is used as an argument for `journalctl`:

```
# journalctl $(which sshd)

```

## wipefs

*wipefs* can list or erase [file system](/index.php/File_system "File system"), [RAID](/index.php/RAID "RAID") or [partition-table](/index.php/Partition "Partition") signatures (magic strings) from the specified device. It does not erase the file systems themselves nor any other data from the device.

See [wipefs(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/wipefs.8) for more information.

For example, to erase all signatures from the device `/dev/sdb` and create a signature backup `~/wipefs-sdb-*offset*.bak` file for each signature:

```
# wipefs --all --backup /dev/sdb

```

## Veja também

*   [A sampling of coreutils](http://www.reddit.com/r/commandline/comments/19garq/a_sampling_of_coreutils_120/) [, part 2](http://www.reddit.com/r/commandline/comments/19ge6v/a_sampling_of_coreutils_2040/) [, part 3](http://www.reddit.com/r/commandline/comments/19j1w3/a_sampling_of_coreutils_4060/) - Overview of commands in coreutils
*   [GNU Coreutils online documentation](https://www.gnu.org/software/coreutils/manual/coreutils.html)
*   [Learn the DD command](https://www.linuxquestions.org/questions/linux-newbie-8/learn-the-dd-command-362506/)