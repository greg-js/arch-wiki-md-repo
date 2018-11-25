**Status de tradução:** Esse artigo é uma tradução de [Archiving and compression](/index.php/Archiving_and_compression "Archiving and compression"). Data da última tradução: 2018-11-24\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Archiving_and_compression&diff=0&oldid=555712) na versão em inglês.

As ferramentas tradicionais de arquivamento e compactação (ou compressão) Unix são separadas de acordo com a [filosofia Unix](https://en.wikipedia.org/wiki/pt:Filosofia_Unix "wikipedia:pt:Filosofia Unix"):

*   Um [arquivador ou empacotador de arquivo](https://en.wikipedia.org/wiki/File_archiver "wikipedia:File archiver") combina vários arquivos em um arquivo de pacote (p.ex., *tar*).
*   Uma ferramenta [compressão](https://en.wikipedia.org/wiki/pt:Compress%C3%A3o_de_dados "wikipedia:pt:Compressão de dados") compacta ou descompacta dados (p.ex., *gzip*).

Essas ferramentas geralmente são usadas em sequência, criando primeiro um arquivo e, em seguida, compactando-o.

Claro que também existem [ferramentas que fazem ambos](#Arquivamento_e_compressão), que tendem a oferecer adicionalmente criptografia, detecção de erro e recuperação.

## Contents

*   [1 Arquivamento apenas](#Arquivamento_apenas)
*   [2 Ferramentas de compressão](#Ferramentas_de_compressão)
    *   [2.1 Compressão apenas](#Compressão_apenas)
    *   [2.2 Arquivamento e compressão](#Arquivamento_e_compressão)
    *   [2.3 Comparação de recursos](#Comparação_de_recursos)
        *   [2.3.1 Descompressão](#Descompressão)
*   [3 Comparação de uso](#Comparação_de_uso)
    *   [3.1 Uso para arquivamento apenas](#Uso_para_arquivamento_apenas)
    *   [3.2 Uso para compressão apenas](#Uso_para_compressão_apenas)
    *   [3.3 Uso para arquivamento e compressão](#Uso_para_arquivamento_e_compressão)
*   [4 Ferramentas de conveniência](#Ferramentas_de_conveniência)
*   [5 Determinando o formato do pacote](#Determinando_o_formato_do_pacote)
*   [6 Ferramentas esotéricas, raras e obsoletas](#Ferramentas_esotéricas,_raras_e_obsoletas)
*   [7 Bibliotecas de compressão](#Bibliotecas_de_compressão)
*   [8 Veja também](#Veja_também)

## Arquivamento apenas

| Nome | Pacote | Manuais | Descrição |
| GNU [tar](https://en.wikipedia.org/wiki/pt:tar_(computa%C3%A7%C3%A3o) | [tar](https://www.archlinux.org/packages/?name=tar) | [tar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tar.1), [info](https://www.gnu.org/software/tar/manual/html_chapter/index.html) | [Utilitário principal](/index.php/Utilit%C3%A1rio_principal "Utilitário principal") de manipulação de pacotes tar (tarballs) onipresentes, que são usados pelo [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") e pelo [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)"). |
| [libarchive](http://libarchive.org/) | [libarchive](https://www.archlinux.org/packages/?name=libarchive) | [bsdtar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/bsdtar.1)
[bsdcpio(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/bsdcpio.1) | Implementação de *tar* e *cpio* que também oferece uma biblioteca. Usado pelo [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") e [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"). |
| [ar](https://en.wikipedia.org/wiki/ar_(Unix) | [binutils](https://www.archlinux.org/packages/?name=binutils) | [ar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ar.1) | Arquivador legado do Unix antes do *tar*. Hoje usado apenas para criar arquivos de [biblioteca estática](https://en.wikipedia.org/wiki/pt:Biblioteca_est%C3%A1tica "wikipedia:pt:Biblioteca estática"). |
| [cpio](https://en.wikipedia.org/wiki/pt:cpio "wikipedia:pt:cpio") | [cpio](https://www.archlinux.org/packages/?name=cpio) | [cpio(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cpio.1) | Arquivador de arquivos via stdin/stdout, oferece suporte a formatos cpio e tar. |
| [DAR](http://dar.linux.free.fr/) | [dar](https://aur.archlinux.org/packages/dar/) | [dar(1)](http://dar.linux.free.fr/doc/man/dar.html) | Arquivador para fazer backup de sistemas de arquivos *live* grandes, lida com links absolutos, [atributos estendidos](/index.php/Atributos_estendidos "Atributos estendidos"), arquivos esparsos e tipos de nó-I. |

**Dica:** O GNU tar e o BSD tar fazem automaticamente a delegação de descompactação para arquivos comprimidos bzip2, compress, gzip, lzip, lzma e xz. Ao criar arquivos, ambos oferecem suporte à opção `-a` para filtrar automaticamente o arquivo criado através do programa de compactação correto, com base na extensão do arquivo. Enquanto o BSD reconhece os formatos de compressão baseados no formato, o GNU tar adivinha apenas baseado na extensão do arquivo.

Veja [#Uso para arquivamento apenas](#Uso_para_arquivamento_apenas).

## Ferramentas de compressão

### Compressão apenas

Esses programas de compactação implementam seu próprio formato de arquivo.

| Nome | Pacote | Manual | Ext | ext do Tar | Descrição | Implementações paralelas |
| [bzip2](https://en.wikipedia.org/wiki/pt:bzip2 "wikipedia:pt:bzip2") | [bzip2](https://www.archlinux.org/packages/?name=bzip2) | [bzip2(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/bzip2.1) | .bz2, .bz | .tbz2, .tbz | Usa o [algoritmo Burrows–Wheeler](https://en.wikipedia.org/wiki/pt:M%C3%A9todo_de_Burrows-Wheeler "wikipedia:pt:Método de Burrows-Wheeler"). | [lbzip2](https://www.archlinux.org/packages/?name=lbzip2), [pbzip2](https://www.archlinux.org/packages/?name=pbzip2) |
| [gzip](https://en.wikipedia.org/wiki/pt:gzip "wikipedia:pt:gzip") | [gzip](https://www.archlinux.org/packages/?name=gzip) | [gzip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gzip.1) | .gz, .z | .tgz, .taz | GNU zip, baseado no algoritmo [DEFLATE](https://en.wikipedia.org/wiki/pt:DEFLATE "wikipedia:pt:DEFLATE"). | [pigz](https://www.archlinux.org/packages/?name=pigz) |
| [lrzip](/index.php/Lrzip "Lrzip") | [lrzip](https://www.archlinux.org/packages/?name=lrzip) | [lrzip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lrzip.1) | .lrz | Versão melhorada do [rzip](https://en.wikipedia.org/wiki/rzip "wikipedia:rzip"), usa múltiplos algoritmos. | é multithreaded |
| [LZ4](https://en.wikipedia.org/wiki/pt:LZ4_(algoritmo_de_compress%C3%A3o) | [lz4](https://www.archlinux.org/packages/?name=lz4) | [lz4(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lz4.1) | .lz4 | Escrito em C, com foco na velocidade de compressão e descompressão. | é multithreaded |
| [lzip](https://en.wikipedia.org/wiki/lzip "wikipedia:lzip") | [lzip](https://www.archlinux.org/packages/?name=lzip) | [lzip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lzip.1) | .lz | Usa [LZMA](https://en.wikipedia.org/wiki/pt:LZMA "wikipedia:pt:LZMA"). | [plzip](https://aur.archlinux.org/packages/plzip/) |
| [lzop](https://en.wikipedia.org/wiki/lzop "wikipedia:lzop") | [lzop](https://www.archlinux.org/packages/?name=lzop) | [lzop(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lzop.1) | .lzop | .tzo | Usa a biblioteca [LZO](https://en.wikipedia.org/wiki/Lempel%E2%80%93Ziv%E2%80%93Oberhumer "wikipedia:Lempel–Ziv–Oberhumer") ([lzo](https://www.archlinux.org/packages/?name=lzo)). |
| [xz](https://en.wikipedia.org/wiki/pt:xz "wikipedia:pt:xz") | [xz](https://www.archlinux.org/packages/?name=xz) | [xz(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xz.1) | .xz, .lzma | .txz, .tlz | Usa [LZMA](https://en.wikipedia.org/wiki/pt:LZMA "wikipedia:pt:LZMA"), padrão para arquivos de pacotes de GNU [coreutils](https://www.archlinux.org/packages/?name=coreutils) e de kernel. | [pixz](https://www.archlinux.org/packages/?name=pixz), [pxz](https://aur.archlinux.org/packages/pxz/) |

*   Implementações paralelas oferecem velocidades aprimoradas usando vários núcleos de CPU.
*   Extensões de tar fazem referências a arquivos compactados em que o `tar` e a ferramenta de compactação são usados (p.ex., {ic|.tzo}} é `.tar.lzo`.
*   Veja também [#Uso para compressão apenas](#Uso_para_compressão_apenas).

### Arquivamento e compressão

| Nome | Pacotes | Manuais | Ext | Descrição |
| [7z](https://en.wikipedia.org/wiki/pt:7z "wikipedia:pt:7z") | [p7zip](https://www.archlinux.org/packages/?name=p7zip) | [7z(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/7z.1) | .7z | Porte POSIX da linha de comando do 7-zip. Veja [p7zip](/index.php/P7zip "P7zip"). |
| [RAR](https://en.wikipedia.org/wiki/pt:RAR "wikipedia:pt:RAR") | [rar](https://aur.archlinux.org/packages/rar/), [unrar](https://www.archlinux.org/packages/?name=unrar) | rar(1) | .rar | Ambos formato e utilitário [rar](/index.php/Rar "Rar") são proprietário. |
| [ZIP](https://en.wikipedia.org/wiki/pt:ZIP "wikipedia:pt:ZIP") | [zip](https://www.archlinux.org/packages/?name=zip), [unzip](https://www.archlinux.org/packages/?name=unzip) | [zip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/zip.1), [unzip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/unzip.1) | .zip | Amplamente usado fora do mundo do Linux. |
| [Unarchiver](https://theunarchiver.com/) | [unarchiver](https://www.archlinux.org/packages/?name=unarchiver) | [unar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/unar.1), [lsar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lsar.1) | *many* | Ferramenta de linha de comando de um aplicativo Mac, suporta mais de 40 formatos de pacote. |
| [ZPAQ](https://en.wikipedia.org/wiki/ZPAQ "wikipedia:ZPAQ") | [zpaq](https://aur.archlinux.org/packages/zpaq/) | [zpaq(1)](http://mattmahoney.net/dc/zpaqdoc.html) | .zpaq | Um arquivador de alta taxa de compactação escrito em C++, usa vários algoritmos. |

Veja também [#Uso para arquivamento e compressão](#Uso_para_arquivamento_e_compressão).

### Comparação de recursos

#### Descompressão

| Nome | gzip | bzip2 | ZIP | compress | pack | CAB | ARJ |
| [gzip](https://www.archlinux.org/packages/?name=gzip) | Sim | Não | Sim | Sim | Sim | Não | Não |
| [p7zip](https://www.archlinux.org/packages/?name=p7zip) | Sim | Sim | Sim | Não | Sim | Sim | Sim |
| [unarchiver](https://www.archlinux.org/packages/?name=unarchiver) | Sim | Sim | Sim | Sim | Não | Sim | Parcial |

## Comparação de uso

### Uso para arquivamento apenas

| Nome | Criação de pacote | Extração de pacote | Listagem de conteúdo |
| [tar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tar.1) | `tar cfv pacote.tar arquivo1 arquivo2` | `tar xfv pacote.tar` | `tar -tvf pacote.tar` |
| [cpio(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cpio.1) | `ls arquivo1 arquivo2 | cpio -o > pacote.cpio` | `cpio -i -vd < pacote.cpio` | `cpio -t < pacote.cpio` |

### Uso para compressão apenas

| Nome | Compressão | Descompressão | Descompressão para stdout |
| [bzip2(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/bzip2.1) | `bzip2 arquivo` | `bzip2 -d arquivo.bz2` | `bzcat arquivo.bz2` |
| [gzip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gzip.1) | `gzip arquivo` | `gzip -d arquivo.gz` | `zcat arquivo.gz` |
| [lrzip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lrzip.1) | `lrzip arquivo`
`lrztar pasta` | `lrzip -d arquivo.lrz`
`lrztar -d pasta.tar.lrz` | `lrzcat arquivo.lrz` |
| [xz(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xz.1) | `xz arquivo` | `xz -d arquivo.xz` | `xzcat arquivo.xz` |

### Uso para arquivamento e compressão

| Nome | Compressão | Descompressão | Descompressão para stdout | Listagem de conteúdo |
| [7z(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/7z.1) | `7z a pacote.7z arquivo1 arquivo2` | `7z x pacote.7z` | `7z e -so pacote.7z arquivo1` | `7z l pacote.7z` |
| rar(1) & unrar | `rar a pacote.rar arquivo1 arquivo2` | `rar x pacote.rar` | `rar p -inul pacote.rar arquivo1` | `rar l pacote.rar` |
| [zip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/zip.1), [unzip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/unzip.1) | `zip pacote.zip arquivo1 arquivo2` | `unzip pacote.zip` | `unzip -p pacote.zip arquivo1` | `unzip -l pacote.zip` |

## Ferramentas de conveniência

*   **atool** — Script para gerenciar pacotes de vários tipos.

	[https://www.nongnu.org/atool/](https://www.nongnu.org/atool/) || [atool](https://www.archlinux.org/packages/?name=atool)

*   **dtrx** — Uma ferramenta inteligente de extração de pacotes.

	[https://brettcsmith.org/2007/dtrx/](https://brettcsmith.org/2007/dtrx/) || [dtrx](https://aur.archlinux.org/packages/dtrx/)

*   **unp** — Ferramenta de linha de comando que pode extrair pacotes facilmente.

	[https://github.com/mitsuhiko/unp](https://github.com/mitsuhiko/unp) || [python-unp](https://aur.archlinux.org/packages/python-unp/)

*   **unpack** — Script wrapper para lidar com diversos formatos de pacotes.

	[https://github.com/githaff/unpack](https://github.com/githaff/unpack) || [unpack-git](https://aur.archlinux.org/packages/unpack-git/)

*   [Bash/Functions#Extract](/index.php/Bash/Functions#Extract "Bash/Functions")

## Determinando o formato do pacote

Para extrair um pacote, seu formato de arquivo precisa ser determinado. Se o arquivo tiver o nome correto, você poderá deduzir seu formato a partir da extensão do arquivo.

Do contrário, você pode usar a ferramenta [file](https://www.archlinux.org/packages/?name=file), veja [file(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/file.1).

## Ferramentas esotéricas, raras e obsoletas

| Nome | Pacotes | Ext | Descrição |
| [ARC](https://en.wikipedia.org/wiki/ARC_(file_format) | [arc](https://aur.archlinux.org/packages/arc/) | .arc, .ark | Foi muito popular durante os primeiros dias do BBS em conexão discada. Substituído pelo ZIP. |
| [ARJ](https://en.wikipedia.org/wiki/pt:ARJ "wikipedia:pt:ARJ") | [arj](https://www.archlinux.org/packages/?name=arj) | .arj | Um arquivador usado no DOS/Windows em meados dos anos 90\. Este é um clone de código aberto. |
| [compress](https://en.wikipedia.org/wiki/compress "wikipedia:compress") | [ncompress](https://aur.archlinux.org/packages/ncompress/) | .Z | O utilitário clássico de compressão unix que pode lidar com o antigo arquivo .Z. |
| [LHA](https://en.wikipedia.org/wiki/LHA_(file_format) | [lha](https://aur.archlinux.org/packages/lha/) | .lzh, .lha | Formato popular no Japão, archiver para criar arquivos no formato LH-7\. Apenas 32 bits (requer [multilib](/index.php/Multilib_(Portugu%C3%AAs) "Multilib (Português)")). |
| [PAR2](https://en.wikipedia.org/wiki/Parchive "wikipedia:Parchive") | [par2cmdline](https://www.archlinux.org/packages/?name=par2cmdline) | .par2 | Arquivador de paridade para maior integridade de dados. Veja também [Parchive](/index.php/Parchive "Parchive"). |
| [shar](https://en.wikipedia.org/wiki/shar "wikipedia:shar") | [sharutils](https://www.archlinux.org/packages/?name=sharutils) | .shar | Cria arquivos de extração automática que são scripts de shell válidos. |
| [Zoo](https://en.wikipedia.org/wiki/Zoo_(file_format) | [zoo](https://aur.archlinux.org/packages/zoo/) | .zoo | Era mais popular no sistema operacional [OpenVMS](https://en.wikipedia.org/wiki/pt:OpenVMS "wikipedia:pt:OpenVMS") antes de o PKZIP se tornar popular. |

## Bibliotecas de compressão

*   **[Brotli](https://en.wikipedia.org/wiki/Brotli "wikipedia:Brotli")** — Algoritmo de compressão para fluxos de dados usando o algoritmo LZ77, codificação de Huffman e modelagem de contexto de segunda ordem.

	[https://github.com/google/brotli](https://github.com/google/brotli) || [brotli](https://www.archlinux.org/packages/?name=brotli)

*   **[zlib](https://en.wikipedia.org/wiki/pt:zlib "wikipedia:pt:zlib")** — Biblioteca de compressão implementando o método de compactação deflate encontrado no gzip e no PKZIP.

	[https://www.zlib.net/](https://www.zlib.net/) || [zlib](https://www.archlinux.org/packages/?name=zlib)

*   **[Zopfli](https://en.wikipedia.org/wiki/Zopfli "wikipedia:Zopfli")** — Compressor de arquivos de alta taxa de compressão do Google, usando um algoritmo compatível com deflação chamado zopfli.

	[https://github.com/google/zopfli](https://github.com/google/zopfli) || [zopfli-git](https://aur.archlinux.org/packages/zopfli-git/)

## Veja também

*   [List of applications/Utilities#Archive managers](/index.php/List_of_applications/Utilities#Archive_managers "List of applications/Utilities")
*   [List of applications/Multimedia#Image compression](/index.php/List_of_applications/Multimedia#Image_compression "List of applications/Multimedia")
*   [Wikipedia:Comparison of file archivers](https://en.wikipedia.org/wiki/Comparison_of_file_archivers "wikipedia:Comparison of file archivers")
*   [Wikipedia:List of archive formats](https://en.wikipedia.org/wiki/List_of_archive_formats "wikipedia:List of archive formats")
*   [Wikipedia:Comparison of archive formats](https://en.wikipedia.org/wiki/Comparison_of_archive_formats "wikipedia:Comparison of archive formats")