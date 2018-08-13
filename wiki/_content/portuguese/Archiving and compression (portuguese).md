As ferramentas tradicionais de arquivamento e compactação (ou compressão) Unix são separadas de acordo com a [filosofia Unix](https://en.wikipedia.org/wiki/pt:Filosofia_Unix "wikipedia:pt:Filosofia Unix"):

*   Um [arquivador ou empacotador de arquivo](https://en.wikipedia.org/wiki/File_archiver "wikipedia:File archiver") combina vários arquivos em um arquivo de pacote (p.ex., *tar*).
*   Uma ferramenta [compressão](https://en.wikipedia.org/wiki/pt:Compress%C3%A3o_de_dados "wikipedia:pt:Compressão de dados") compacta ou descompacta dados.

Essas ferramentas geralmente são usadas em sequência, criando primeiro um arquivo e, em seguida, compactando-o.

Claro que também existem [ferramentas que fazem ambos](#Arquivamento_e_compress.C3.A3o), que tendem a oferecer adicionalmente criptografia, detecção de erro e recuperação.

## Contents

*   [1 Arquivamento apenas](#Arquivamento_apenas)
*   [2 Ferramentas de compressão](#Ferramentas_de_compress.C3.A3o)
    *   [2.1 Compressão apenas](#Compress.C3.A3o_apenas)
    *   [2.2 Arquivamento e compressão](#Arquivamento_e_compress.C3.A3o)
    *   [2.3 Comparação de recursos](#Compara.C3.A7.C3.A3o_de_recursos)
        *   [2.3.1 Descompressão](#Descompress.C3.A3o)
*   [3 Comparação de uso](#Compara.C3.A7.C3.A3o_de_uso)
    *   [3.1 Arquivamento apenas](#Arquivamento_apenas_2)
    *   [3.2 Compressão apenas](#Compress.C3.A3o_apenas_2)
    *   [3.3 Arquivamento e compressão](#Arquivamento_e_compress.C3.A3o_2)
*   [4 Ferramentas de conveniência](#Ferramentas_de_conveni.C3.AAncia)
*   [5 Determinando o formato do pacote](#Determinando_o_formato_do_pacote)
*   [6 Ferramentas esotéricas, raras e obsoletas](#Ferramentas_esot.C3.A9ricas.2C_raras_e_obsoletas)
*   [7 Bibliotecas de compressão](#Bibliotecas_de_compress.C3.A3o)
*   [8 Veja também](#Veja_tamb.C3.A9m)

## Arquivamento apenas

| Nome | Pacotes | Manuais | Descrição |
| [ar](https://en.wikipedia.org/wiki/ar_(Unix) | [binutils](https://www.archlinux.org/packages/?name=binutils) | [ar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ar.1) | Arquivador legado do Unix antes do *tar*. Hoje usado apenas para criar arquivos de [biblioteca estática](https://en.wikipedia.org/wiki/pt:Biblioteca_est%C3%A1tica "wikipedia:pt:Biblioteca estática"). |
| [cpio](https://en.wikipedia.org/wiki/pt:cpio "wikipedia:pt:cpio") | [cpio](https://www.archlinux.org/packages/?name=cpio) | [cpio(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cpio.1) | Arquivador de arquivos via stdin/stdout, oferece suporte a formatos cpio e tar. |
| [DAR](http://dar.linux.free.fr/) | [dar](https://aur.archlinux.org/packages/dar/) | [dar(1)](http://dar.linux.free.fr/doc/man/dar.html) | Arquivador para fazer backup de sistemas de arquivos *live* grandes, lida com links absolutos, [atributos estendidos](/index.php/Extended_attributes "Extended attributes"), arquivos esparsos e tipos de nó-I. |
| GNU [tar](https://en.wikipedia.org/wiki/pt:tar_(computa%C3%A7%C3%A3o) | [coreutils](https://www.archlinux.org/packages/?name=coreutils) | [tar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tar.1) | Utilitário do GNU para manipulação de pacotes tar (tarballs) onipresente, veja [tar](/index.php/Tar_(Portugu%C3%AAs) "Tar (Português)") para exemplos de uso. |
| [libarchive](http://libarchive.org/) | [libarchive](https://www.archlinux.org/packages/?name=libarchive) | [bsdtar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/bsdtar.1)
[bsdcpio(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/bsdcpio.1) | Implementação de *tar* e *cpio* que também oferece uma biblioteca. Usado pelo [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") e [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"). |

**Dica:** O GNU tar e o BSD tar fazem automaticamente a delegação de descompactação para arquivos comprimidos bzip2, compress, gzip, lzip, lzma e xz. Ao criar arquivos, ambos oferecem suporte à opção `-a` para filtrar automaticamente o arquivo criado através do programa de compactação correto, com base na extensão do arquivo. Enquanto o BSD reconhece os formatos de compressão baseados no formato, o GNU tar adivinha apenas baseado na extensão do arquivo.

## Ferramentas de compressão

### Compressão apenas

Esses programas de compactação implementam seu próprio formato de arquivo.

| Nome | Pacotes | Manual | Ext | ext do Tar | Descrição | Implementações paralelas |
| [bzip2](https://en.wikipedia.org/wiki/pt:bzip2 "wikipedia:pt:bzip2") | [bzip2](https://www.archlinux.org/packages/?name=bzip2) | [bzip2(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/bzip2.1) | .bz2, .bz | .tbz2, .tbz | Usa o [algoritmo Burrows–Wheeler](https://en.wikipedia.org/wiki/pt:M%C3%A9todo_de_Burrows-Wheeler "wikipedia:pt:Método de Burrows-Wheeler"). | [lbzip2](https://www.archlinux.org/packages/?name=lbzip2), [pbzip2](https://www.archlinux.org/packages/?name=pbzip2) |
| [gzip](https://en.wikipedia.org/wiki/pt:gzip "wikipedia:pt:gzip") | [gzip](https://www.archlinux.org/packages/?name=gzip) | [gzip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gzip.1) | .gz, .z | .tgz, .taz | GNU zip, baseado no algoritmo [DEFLATE](https://en.wikipedia.org/wiki/pt:DEFLATE "wikipedia:pt:DEFLATE"). | [pigz](https://www.archlinux.org/packages/?name=pigz) |
| [lrzip](/index.php/Lrzip "Lrzip") | [lrzip](https://www.archlinux.org/packages/?name=lrzip) | [lrzip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lrzip.1) | .lrz | Versão melhorada do [rzip](https://en.wikipedia.org/wiki/rzip "wikipedia:rzip"), usa múltiplos algoritmos. | é multithreaded |
| [LZ4](https://en.wikipedia.org/wiki/pt:LZ4_(algoritmo_de_compress%C3%A3o) | [lz4](https://www.archlinux.org/packages/?name=lz4) | [lz4(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lz4.1) | .lz4 | Escrito em C, com foco na velocidade de compressão e descompressão. | é multithreaded |
| [lzip](https://en.wikipedia.org/wiki/lzip "wikipedia:lzip") | [lzip](https://www.archlinux.org/packages/?name=lzip) | [lzip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lzip.1) | .lz | Usa [LZMA](https://en.wikipedia.org/wiki/pt:LZMA "wikipedia:pt:LZMA"). | [plzip](https://aur.archlinux.org/packages/plzip/) |
| [lzop](https://en.wikipedia.org/wiki/lzop "wikipedia:lzop") | [lzop](https://www.archlinux.org/packages/?name=lzop) | [lzop(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lzop.1) | .lzop | .tzo | Usa a biblioteca [LZO](https://en.wikipedia.org/wiki/Lempel%E2%80%93Ziv%E2%80%93Oberhumer "wikipedia:Lempel–Ziv–Oberhumer") ([lzo](https://www.archlinux.org/packages/?name=lzo)). |
| [xz](https://en.wikipedia.org/wiki/pt:xz "wikipedia:pt:xz") | [xz](https://www.archlinux.org/packages/?name=xz) | [xz(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xz.1) | .xz, .lzma | .txz, .tlz | Usa [LZMA](https://en.wikipedia.org/wiki/pt:LZMA "wikipedia:pt:LZMA"), padrão para arquivos de pacotes de GNU [coreutils](https://www.archlinux.org/packages/?name=coreutils) e de kernel. | [pixz](https://www.archlinux.org/packages/?name=pixz), [pxz](https://aur.archlinux.org/packages/pxz/) |

*   Implementações paralelas oferecem velocidades aprimoradas usando vários núcleos de CPU.
*   Extensões de tar fazem referências a arquivos compactados em que o `tar` e a ferramenta de compactação são usados (p.ex., {ic|.tzo}} é `.tar.lzo`.

### Arquivamento e compressão

| Nome | Pacotes | Manual | Ext | Descrição |
| [7z](https://en.wikipedia.org/wiki/pt:7z "wikipedia:pt:7z") | [p7zip](https://www.archlinux.org/packages/?name=p7zip) | [7z(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/7z.1) | .7z | Porte POSIX da linha de comando do 7-zip. Veja [p7zip](/index.php/P7zip "P7zip"). |
| [RAR](https://en.wikipedia.org/wiki/pt:RAR "wikipedia:pt:RAR") | [rar](https://aur.archlinux.org/packages/rar/), [unrar](https://www.archlinux.org/packages/?name=unrar) | rar(1) | .rar | Ambos formato e utilitário [rar](/index.php/Rar "Rar") são proprietário. |
| [ZIP](https://en.wikipedia.org/wiki/pt:ZIP "wikipedia:pt:ZIP") | [zip](https://www.archlinux.org/packages/?name=zip), [unzip](https://www.archlinux.org/packages/?name=unzip) | [zip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/zip.1), [unzip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/unzip.1) | .zip | Amplamente usado fora do mundo do Linux. |
| [Unarchiver](https://theunarchiver.com/) | [unarchiver](https://www.archlinux.org/packages/?name=unarchiver) | [unar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/unar.1), [lsar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lsar.1) | *many* | Ferramenta de linha de comando de um aplicativo Mac, suporta mais de 40 formatos de pacote. |
| [ZPAQ](https://en.wikipedia.org/wiki/ZPAQ "wikipedia:ZPAQ") | [zpaq](https://aur.archlinux.org/packages/zpaq/) | [zpaq(1)](http://mattmahoney.net/dc/zpaqdoc.html) | .zpaq | Um arquivador de alta taxa de compactação escrito em C++, usa vários algoritmos. |

### Comparação de recursos

#### Descompressão

| Nome | gzip | bzip2 | ZIP | compress | pack | CAB | ARJ |
| [gzip](https://www.archlinux.org/packages/?name=gzip) | Sim | Não | Sim | Sim | Sim | Não | Não |
| [p7zip](https://www.archlinux.org/packages/?name=p7zip) | Sim | Sim | Sim | Não | Sim | Sim | Sim |
| [unarchiver](https://www.archlinux.org/packages/?name=unarchiver) | Sim | Sim | Sim | Sim | Não | Sim | Parcial |

## Comparação de uso

### Arquivamento apenas

| Nome | Criação de pacote | Extração de pacote | Listagem de conteúdo |
| [tar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tar.1) | `tar cfv pacote.tar arquivo1 arquivo2` | `tar xfv pacote.tar` | `tar -tvf pacote.tar` |
| [cpio(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cpio.1) | `ls arquivo1 arquivo2 | cpio -o > pacote.cpio` | `cpio -i -vd < pacote.cpio` | `cpio -t < pacote.cpio` |

### Compressão apenas

| Nome | Compressão | Descompressão | Descompressão para stdout |
| [bzip2(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/bzip2.1) | `bzip2 arquivo` | `bzip2 -d arquivo.bz2` | `bzcat arquivo.bz2` |
| [gzip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gzip.1) | `gzip arquivo` | `gzip -d arquivo.gz` | `zcat arquivo.gz` |
| [lrzip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lrzip.1) | `lrzip arquivo`
`lrztar pasta` | `lrzip -d arquivo.lrz`
`lrztar -d pasta.tar.lrz` | `lrzcat arquivo.lrz` |
| [xz(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xz.1) | `xz arquivo` | `xz -d arquivo.xz` | `xzcat arquivo.xz` |

### Arquivamento e compressão

| Name | Compress | Decompress | Decompress to stdout | List content |
| [7z(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/7z.1) | `7z a archive.7z file1 file2` | `7z x archive.7z` | `7z e -so archive.7z file1` | `7z l archive.7z` |
| rar(1) & unrar | `rar a archive.rar file1 file2` | `rar x archive.rar` | `rar p -inul archive.rar file1` | `rar l archive.rar` |
| [zip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/zip.1), [unzip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/unzip.1) | `zip archive.zip file1 file2` | `unzip archive.zip` | `unzip -p archive.zip file1` | `unzip -l archive.zip` |

## Ferramentas de conveniência

*   **atool** — Script for managing file archives of various types.

	[https://www.nongnu.org/atool/](https://www.nongnu.org/atool/) || [atool](https://www.archlinux.org/packages/?name=atool)

*   **dtrx** — An intelligent archive extraction tool.

	[https://brettcsmith.org/2007/dtrx/](https://brettcsmith.org/2007/dtrx/) || [dtrx](https://aur.archlinux.org/packages/dtrx/)

*   **unp** — Command line tool that can unpack archives easily.

	[https://github.com/mitsuhiko/unp](https://github.com/mitsuhiko/unp) || [python-unp](https://aur.archlinux.org/packages/python-unp/)

*   **unpack** — Wrapper script for handling multiple archive formats.

	[https://github.com/githaff/unpack](https://github.com/githaff/unpack) || [unpack-git](https://aur.archlinux.org/packages/unpack-git/)

*   [Bash/Functions#Extract](/index.php/Bash/Functions#Extract "Bash/Functions")

## Determinando o formato do pacote

To extract an archive, its file format needs to be determined. If the file is properly named you can deduce its format from the file extension.

Otherwise you can use the [file](https://www.archlinux.org/packages/?name=file) tool, see [file(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/file.1).

## Ferramentas esotéricas, raras e obsoletas

| Name | Packages | Ext | Description |
| [ARC](https://en.wikipedia.org/wiki/ARC_(file_format) | [arc](https://aur.archlinux.org/packages/arc/) | .arc, .ark | Was very popular during the early days of the dial-up BBS. Superseded by ZIP. |
| [ARJ](https://en.wikipedia.org/wiki/ARJ "wikipedia:ARJ") | [arj](https://www.archlinux.org/packages/?name=arj) | .arj | An archiver used on DOS/Windows in mid-1990s. This is an open source clone. |
| [compress](https://en.wikipedia.org/wiki/compress "wikipedia:compress") | [ncompress](https://aur.archlinux.org/packages/ncompress/) | .Z | The classic unix compression utility which can handle the ancient .Z archive. |
| [LHA](https://en.wikipedia.org/wiki/LHA_(file_format) | [lha](https://aur.archlinux.org/packages/lha/) | .lzh, .lha | Format popular in Japan, archiver to create LH-7 format archives. 32-bit only (requires [multilib](/index.php/Multilib "Multilib")). |
| [PAR2](https://en.wikipedia.org/wiki/Parchive "wikipedia:Parchive") | [par2cmdline](https://www.archlinux.org/packages/?name=par2cmdline) | .par2 | Parity archiver for increased data integrity. See also [Parchive](/index.php/Parchive "Parchive"). |
| [shar](https://en.wikipedia.org/wiki/shar "wikipedia:shar") | [sharutils](https://www.archlinux.org/packages/?name=sharutils) | .shar | Creates self-extracting archives that are valid shell scripts. |
| [Zoo](https://en.wikipedia.org/wiki/Zoo_(file_format) | [zoo](https://aur.archlinux.org/packages/zoo/) | .zoo | Was mostly popular on the [OpenVMS](https://en.wikipedia.org/wiki/OpenVMS "wikipedia:OpenVMS") operating system before PKZIP became popular. |

## Bibliotecas de compressão

*   **[zlib](https://en.wikipedia.org/wiki/zlib "wikipedia:zlib")** — Compression library implementing the deflate compression method found in gzip and PKZIP.

	[https://www.zlib.net/](https://www.zlib.net/) || [zlib](https://www.archlinux.org/packages/?name=zlib)

*   **[Zopfli](https://en.wikipedia.org/wiki/Zopfli "wikipedia:Zopfli")** — High compress ratio file compressor from Google, using a deflate-compatible algorithm called zopfli.

	[https://github.com/google/zopfli](https://github.com/google/zopfli) || [zopfli-git](https://aur.archlinux.org/packages/zopfli-git/)

## Veja também

*   [List of applications/Utilities#Archive managers](/index.php/List_of_applications/Utilities#Archive_managers "List of applications/Utilities")
*   [List of applications/Multimedia#Image compression](/index.php/List_of_applications/Multimedia#Image_compression "List of applications/Multimedia")
*   [Wikipedia:Comparison of file archivers](https://en.wikipedia.org/wiki/Comparison_of_file_archivers "wikipedia:Comparison of file archivers")
*   [Wikipedia:List of archive formats](https://en.wikipedia.org/wiki/List_of_archive_formats "wikipedia:List of archive formats")
*   [Wikipedia:Comparison of archive formats](https://en.wikipedia.org/wiki/Comparison_of_archive_formats "wikipedia:Comparison of archive formats")