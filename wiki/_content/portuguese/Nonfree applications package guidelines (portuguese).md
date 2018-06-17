**[Diretrizes de criação de pacotes](/index.php/Criando_pacotes "Criando pacotes")**

* * *

[CLR](/index.php/Diretrizes_de_pacotes_CLR "Diretrizes de pacotes CLR") – [Cross](/index.php/Diretrizes_de_pacotes_de_ferramentas_de_compila%C3%A7%C3%A3o_cruzada "Diretrizes de pacotes de ferramentas de compilação cruzada") – [Eclipse](/index.php/Diretrizes_de_pacotes_de_plugin_do_Eclipse "Diretrizes de pacotes de plugin do Eclipse") – [Free Pascal](/index.php/Diretrizes_de_pacotes_Free_Pascal "Diretrizes de pacotes Free Pascal") – [GNOME](/index.php/Diretrizes_de_pacotes_GNOME "Diretrizes de pacotes GNOME") – [Go](/index.php/Diretrizes_de_pacotes_Go "Diretrizes de pacotes Go") – [Haskell](/index.php/Diretrizes_de_pacotes_Haskell "Diretrizes de pacotes Haskell") – [Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java") – [KDE](/index.php/Diretrizes_de_pacotes_KDE "Diretrizes de pacotes KDE") – [Kernel](/index.php/Diretrizes_de_pacotes_de_m%C3%B3dulos_de_kernel "Diretrizes de pacotes de módulos de kernel") – [Lisp](/index.php/Diretrizes_de_pacotes_Lisp "Diretrizes de pacotes Lisp") – [MinGW](/index.php/Diretrizes_de_pacotes_MinGW "Diretrizes de pacotes MinGW") – [Node.js](/index.php/Diretrizes_de_pacotes_Node.js "Diretrizes de pacotes Node.js") – [Nonfree](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") –[OCaml](/index.php/Diretrizes_de_pacotes_OCaml "Diretrizes de pacotes OCaml") – [Perl](/index.php/Diretrizes_de_pacotes_Perl "Diretrizes de pacotes Perl") – [PHP](/index.php/Diretrizes_de_pacotes_PHP "Diretrizes de pacotes PHP") – [Python](/index.php/Diretrizes_de_pacotes_Python "Diretrizes de pacotes Python") – [Ruby](/index.php/Diretrizes_de_pacotes_Ruby_Gem "Diretrizes de pacotes Ruby Gem") – [VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") – [Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web") – [Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine")

Para muitos aplicativos (a maioria dos quais são do Windows), não há fontes nem tarballs disponíveis. Muitos desses aplicativos não podem ser distribuídos livremente devido a restrições de licença e/ou falta de meios legais para obter o instalador sem cobrança de taxa. Tal software obviamente não pode ser incluído nos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais") mas devido à natureza do [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)") ainda é possível privadamente [compilar pacotes](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") para ele, gerenciável com [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)").

**Nota:** Todas as informações aqui são agnósticos a pacotes. Para informações específicas para a maioria dos softwares não livres, veja [Diretrizes de pacotes Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine").

## Contents

*   [1 Motivo](#Motivo)
*   [2 Regras comuns](#Regras_comuns)
    *   [2.1 Evite software não livre quando possível](#Evite_software_n.C3.A3o_livre_quando_poss.C3.ADvel)
    *   [2.2 Use variantes de código aberto quando possível](#Use_variantes_de_c.C3.B3digo_aberto_quando_poss.C3.ADvel)
    *   [2.3 Mantenha simples](#Mantenha_simples)
*   [3 Nomenclatura de pacotes](#Nomenclatura_de_pacotes)
*   [4 Colocação de arquivos](#Coloca.C3.A7.C3.A3o_de_arquivos)
*   [5 Arquivos em falta](#Arquivos_em_falta)
*   [6 Tópicos avançados](#T.C3.B3picos_avan.C3.A7ados)
    *   [6.1 DLAGENTS personalizados](#DLAGENTS_personalizados)
    *   [6.2 Desempacotamento](#Desempacotamento)
    *   [6.3 Obtendo ícones para arquivos .desktop](#Obtendo_.C3.ADcones_para_arquivos_.desktop)

## Motivo

There are multiple reasons for packaging even non-packageable software:

*   Simplification of installation/removal process

	This is applicable even to the simplest of apps, which consist of a single script to be installed into `/usr/bin`. Instead of issuing:

	 `$ chmod +x *filename*` 

	 `$ chown root:root *filename*` 

	 `# cp *filename* /usr/bin/` 

	you can type just

	 `$ makepkg -i` 

	Most non-free applications are obviously much more complicated, but the burden of downloading an archive/installer from a homepage (often full of advertising), unpacking/decrypting it, hand-writing stereotypical launcher scripts and doing other similar tasks can be effectively lightened by a well-written packaging script.

*   Utilizing pacman capabilities

	The ability to track state, perform automatic updates of any installed piece of software, determine ownership of every single file, and store compressed packages in a well-organized cache is what makes GNU/Linux distributions so powerful.

*   Sharing code and knowledge

	It is simpler to apply tweaks, fix bugs and seek/provide help in a single public place like AUR versus submitting patches to proprietary developers who may have ceased support or asking vague questions on general purpose forums.

## Regras comuns

### Evite software não livre quando possível

Yes, it's better to leave this guide and spend some time searching (or maybe even creating) alternatives to an application you wanted to package because:

1.  It is better to support software that is owned by us all than software that is owned by a company
2.  It is better to support software that is actively maintained
3.  It is better to support software that can be fixed if just one person out of millions cares enough

### Use variantes de código aberto quando possível

Many commercial games ([some are listed in this Wiki](/index.php/List_of_Applications/Games "List of Applications/Games")) have open source engines and many old games can be played with emulators such as [ScummVM](https://en.wikipedia.org/wiki/ScummVM "wikipedia:ScummVM"). Using open source engines together with the original game assets gives users access to bug fixes and eliminates several issues caused by binary packages.

### Mantenha simples

If the packaging of some program requires more effort and hacks than buying and using the original version - do the simplest thing, it is Arch!

## Nomenclatura de pacotes

Before choosing a name on your own, search in AUR for existing versions of the software you want to package. Try to use established naming conversion (e.g. do not create something like [gish-hb](https://aur.archlinux.org/packages/gish-hb/) when there are already [aquaria-hib](https://aur.archlinux.org/packages/aquaria-hib/), [penumbra-overture-hib](https://aur.archlinux.org/packages/penumbra-overture-hib/) and [uplink-hib](https://aur.archlinux.org/packages/uplink-hib/)). Use suffix `-bin` **always** unless you are sure there will never be a source-based package—its creator would have to ask you (or in worst case TUs) to orphan existing package for him and you both will end up with PKGBUILDs cluttered with additional `replaces` and `conflicts`.

## Colocação de arquivos

Again, analyze existing packages (if present) and decide whether or not you want to conflict with them. Do not place things under `/opt` unless you want to use some ugly hacks like giving ownership `root:games` to the package directory (so users in group `games` running the game can write files in the game's own folder).

## Arquivos em falta

For most commercial games there is no way to (legally) download game files, which is the preferable way to get them for normal packages. Even when it is possible to download files after providing a password (like with all [Humble Indie Bundle](https://en.wikipedia.org/wiki/Humble_Indie_Bundle "wikipedia:Humble Indie Bundle") games) asking user for this password and downloading somewhere in `build` function is not recommended for a variety of reasons (for example, the user may have no Internet access but have all files downloaded and stored locally). The following options should be considered:

*   **There is only one way to obtain files**

*   Software is distributed in archive/installer

	Add the required file to `sources` array:

	 `sources=(... "*originalname*::**file://***originalname*")` 

	This way the link to file in AUR web interface will look different from names of files included in source tarball.

	Add following comment on package page:

	 `Need archive/installer to work.` 

	and explain the details in PKGBUILD source.

*   Software is distributed on compact-disk

	Add installer script and `.install` file to package contents, like in package [tsukihime-en](https://aur.archlinux.org/packages/tsukihime-en/).

*   **There are several ways to obtain files**

Copying files from disk / downloading from Net / getting from archive during `build` phase may look like a good idea but it is not recommended because it limits the user's possibilities and makes package installation interactive (which is generally discouraged and just annoying). Again, a good installer script and `.install` file can work instead.

Few examples of various strategies for obtaining files required for package:

*   [worldofgoo](https://aur.archlinux.org/packages/worldofgoo/) – dependency on user-provided file
*   [umineko-en](https://aur.archlinux.org/packages/umineko-en/) – combining files from freely available patch and user-provided compact-disk
*   [worldofgoo-demo](https://aur.archlinux.org/packages/worldofgoo-demo/) – autonomic fetching installer during build phase
*   [ut2004-anthology](https://aur.archlinux.org/packages/ut2004-anthology/) – searching for disk via mountpoints

## Tópicos avançados

### DLAGENTS personalizados

Some software authors aggressively protect their software from automatic downloading: ban certain "User-Agent" strings, create temporary links to files etc. You can still conveniently download this files by using `DLAGENTS` variable in PKGBUILD (see [makepkg.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/makepkg.conf.5)). This is used by some packages in [official repositories](/index.php/Official_repositories "Official repositories"), for example [ttf-baekmuk](https://www.archlinux.org/packages/?name=ttf-baekmuk).

Please pay attention, if you want to have a customized user-agent string, if the latter contains spaces, parentheses, or slashes in it (or actually anything that can break parsing), this will not work. There's no workaround, this is the nature of arrays in bash and the way DLAGENTS was designed to be consumed in makepkg. The following example will thus **not work**:

```
DLAGENTS=("http::/usr/bin/curl -A 'Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)' -fLC - --retry 3 --retry-delay 3 -o %o %u")

```

Shorten it to the following which is working:

```
DLAGENTS=("http::/usr/bin/curl -A 'Mozilla' -fLC - --retry 3 --retry-delay 3 -o %o %u")

```

And following allows to extract temporary link to file from download page:

```
DLAGENTS=("http::/usr/bin/wget -r -np -nd -H %u")

```

### Desempacotamento

Many proprietary programs are shipped in nasty installers which sometimes do not even run in Wine. Following tools may be of some help:

*   [unzip](https://www.archlinux.org/packages/?name=unzip) and [unrar](https://www.archlinux.org/packages/?name=unrar) unpack executable SFX archives, based on this formats
*   [cabextract](https://www.archlinux.org/packages/?name=cabextract) can unpack most `.cab` files (including ones with `.exe` extension)
*   [unshield](https://www.archlinux.org/packages/?name=unshield) can extract CAB files from InstallShield installers
*   [p7zip](https://www.archlinux.org/packages/?name=p7zip) unpacks not only many archive formats but also [NSIS](https://en.wikipedia.org/wiki/NSIS "wikipedia:NSIS")-based `.exe` installers
    *   it even can extract single sections from common PE (`.exe` & `.dll`) files!
*   [upx](https://www.archlinux.org/packages/?name=upx) is sometimes used to encrypt above-listed executables and can be used for decryption as well
*   [innoextract](https://www.archlinux.org/packages/?name=innoextract) can unpack `.exe` installers created with [Inno Setup](https://en.wikipedia.org/wiki/Inno_Setup "wikipedia:Inno Setup") (used for example by GOG.com games)

In order to determine exact type of file run `file *file_of_unknown_type*`.

### Obtendo ícones para arquivos .desktop

Proprietary software often have no separate icon files, so there is nothing to use in [.desktop](/index.php/.desktop ".desktop") file creation. Happily `.ico` files can be easily extracted from executables with programs from [icoutils](https://www.archlinux.org/packages/?name=icoutils) package. You can even do it on fly during `build` phase, for example:

```
$ wrestool -x --output=*icon.ico* -t14 *executable.exe*

```