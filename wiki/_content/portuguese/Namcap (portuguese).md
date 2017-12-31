Namcap é uma ferramenta para verificar pacotes binários e PKGBUILDs fonte para erros comuns de empacotamento, que também pode ser habilitado automaticamente. Ele foi criado por [Jason Chu](https://www.archlinux.org/people/developer-fellows/#jason).

**Alterações**: O arquivo [NEWS](https://git.archlinux.org/namcap.git/tree/NEWS) no repositório Git contém as alterações em relação versões anteriores de forma concisa.

**Ramo de desenvolvimento**: [https://git.archlinux.org/namcap.git](https://git.archlinux.org/namcap.git)

Para fazer um **relato de erro** ou **requisição de recurso** para o namcap, preencha um relatório na seção *Packages:Extra* do [rastreador de erros](https://bugs.archlinux.org) do Arch Linux e defina a importância conforme o caso. Se você está relatando um erro, por favor forneça exemplos concretos de pacotes nos quais o problema ocorra e lembre-se de inserir o número de versão.

Se você tem um *patch* (corrigindo um erro ou adicionando um novo módulo para o namcap), você pode enviá-lo para a lista de discussão [arch-projects](mailto:arch-projects@archlinux.org). O desenvolvimento do namcap é gerenciado com git, então patches formatados em git são preferíveis.

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
*   [2 Como usá-lo](#Como_us.C3.A1-lo)
*   [3 Entendendo a saída](#Entendendo_a_sa.C3.ADda)
*   [4 Tags](#Tags)
    *   [4.1 Links simbólicos](#Links_simb.C3.B3licos)
    *   [4.2 Depedências](#Deped.C3.AAncias)
    *   [4.3 Licenças](#Licen.C3.A7as)
    *   [4.4 Arquivos](#Arquivos)
    *   [4.5 Diversos](#Diversos)
    *   [4.6 PKGBUILDs](#PKGBUILDs)
    *   [4.7 Não lançadas](#N.C3.A3o_lan.C3.A7adas)
*   [5 Fazendo um módulo de namcap](#Fazendo_um_m.C3.B3dulo_de_namcap)
*   [6 Relatórios do namcap](#Relat.C3.B3rios_do_namcap)

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [namcap](https://www.archlinux.org/packages/?name=namcap).

## Como usá-lo

Para executar o namcap em um arquivo, sendo *nome_de_arquivo* o `PKGBUILD` ou o nome de um binário `pkg.tar.xz`:

```
$ namcap *nome_de_arquivo*

```

Se você deseja ver mensagens informacionais extras, chame o namcap com a opção `-i`:

```
$ namcap -i *nome_de_arquivo*

```

Para mais informações sobre uso, veja a página man [namcap(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/namcap.1).

## Entendendo a saída

O namcap usa um sistema de **tags** para classificar a saída. Atualmente, as tags são de três tipos, *erros* (denotados por E), *avisos* (denotados por W) e *informativo* (denotado por I). Um erro é importante e deve ser corrigido imediatamente; principalmente se eles referem a segurança insuficiente, falta de licença ou problemas de permissão.

Normalmente, o namcap imprime uma explicação legível por humanos (às vezes com sugestões sobre como solucionar o problema). Se quiser saída que pode ser facilmente analisada por um programa, passe a opção -m (*legível para máquina*) para o namcap (esse recurso está atualmente no ramo de desenvolvimento).

## Tags

### Links simbólicos

*   **symlink-found** (*informacional*) Relata quaisquer **links simbólicos** presentes no pacote.
*   **hardlink-found** (*informacional*) Relata quaisquer **links abosolutos** presentes no pacote.
*   **dangling-symlink** (*erro*) Relata ocorrências de links simbólicos que apontam para um arquivo que não está presente no pacote.
*   **dangling-hardlink** (*erro*) Relata ocorrências de links absolutos que apontam para um arquivo que não está presente no pacote.

### Depedências

*   **link-level-dependence** (*informacional*) Informa sobre uma biblioteca à qual um pacote está dinamicamente vinculado.
*   **dependency-is-testing-release** (*aviso*) A dependência do pacote listada está no repositório [testing]. Enquanto os pacotes estão sendo criados para os repositórios oficiais do Arch Linux (core, extra e community), eles **não devem ser compilados** contra pacotes do [testing]. Para os pacotes do [core] e [extra], os pacotes comilados contra [testing] devem ser colocados no repositório [testing].
*   **dependency-covered-by-link-dependence** (*informacional*) Dependência coberta por dependências da dependência de links. Portanto, esta é uma dependência redundante.
*   **dependency-detected-not-included** (*erro*) O arquivo referido tem uma dependência que não está listada no vetor depends. Ignore este erro se a dependência mencionada estiver listada na matriz optdepends.

*   **dependency-already-satisfied** (*aviso*) A dependência já está satisfeita (como a dependência de algum pacote já listado como uma dependência, por exemplo) e, portanto, é redundante. Você pode usar a ferramenta `pactree` de [pacman](https://www.archlinux.org/packages/?name=pacman) para ver a árvore de dependências do seu pacote.
*   **dependency-not-needed** (*aviso*) Essa dependência não é necessária por nenhum arquivo presente no programa (até onde o namcap pode deduzir). Isso ainda não funciona corretamente para scripts (como pacotes Python ou perl); lá, você terá que descobrir as dependências por conta própria.
*   **depends-by-namcap-sight** (*informacional*) Uma lista de dependências de acordo com o namcap.

### Licenças

*   **missing-license** (*error*) This package is missing a license. Licenses should be put in the `license=()` array of the PKGBUILD. See the [Arch packaging standards](/index.php/Arch_packaging_standards "Arch packaging standards") for more information. It is **very important** to fix this error as soon as possible, since not including a license is a copyright violation in many cases.
*   **missing-custom-license-dir** (*error*) The license specified is *custom* but no license directory was found under */usr/share/licenses/* as specified in the packaging guidelines.
*   **missing-custom-license-file** (*error*) The license specified is *custom* but no license file was found in */usr/share/licenses/$pkgname*.
*   **not-a-common-license** (*error*) The license specified is **not** *custom* but it is not present in the common [licenses](https://www.archlinux.org/packages/?name=licenses) package shipped in the Arch Linux distribution.

### Arquivos

This section describes the tags which relate to incorrect permissions of files or files not being installed in accordance with the FHS guidelines.

*   **script-link-detected** (*informational*) The following file is a script.
*   **file-in-non-standard-dir** (*warning*) The following file is in a non-standard directory as defined by the [FHS guidelines](http://proton.pathname.com/fhs/pub/fhs-2.3.html). The allowed directories are: *bin/*, *etc/*, *usr/bin/*, *usr/sbin/*, *usr/lib*, *usr/include/*, *usr/share/*, *opt/*, *lib/*, *sbin/*, *srv/*, *var/lib/*, *var/opt/*, *var/spool/*, *var/lock/*, *var/state/*, *var/run/*, *var/log/*.
*   **elffile-not-in-allowed-dirs** (*error*) ELF files should only be in these directories: */lib*, */bin*, */sbin*, */usr/bin*, */usr/sbin*, */lib*, */usr/lib*, */opt/$pkgname/*.
*   **empty-directory** (*warning*) The following directory in the package is empty.
*   **non-fhs-man-page** (*error*) The package installs manual pages into a location other than */usr/share/man* which is the directory for manual pages according to the [FHS guidelines](http://www.pathname.com/fhs/pub/fhs-2.3.html#USRSHAREMANMANUALPAGES).
*   **potential-non-fhs-man-page** (*warning*) This file seems to be a manual page which is not installed in */usr/share/man* but namcap is not too sure about it.
*   **non-fhs-info-page** (*error*) The package installs info pages into a location other than */usr/share/info* which is where architecture independent data should be installed according to the [FHS guidelines](http://www.pathname.com/fhs/pub/fhs-2.3.html#USRSHAREARCHITECTUREINDEPENDENTDATA)
*   **potential-non-fhs-info-page** (*warning*) This file seems to be a info page which is not installed in */usr/share/info* but namcap is not too sure about it.
*   **incorrect-permissions** (*error*) This file has incorrect ownership. The ownership of files in binary packages should be `root/root`.
*   **file-not-world-readable** (*warning*) The file is not readable by everyone; usually this should not be the case.
*   **file-world-writable** (*warning*) Anyone can write to this file; again not a typical case.
*   **directory-not-world-executable** (*warning*) The directory does not have the world executable bit set. This disallows access to the directory for programs running under user privileges.
*   **incorrect-library-permissions** (*warning*) The static library file (.a) does not have permission 644 (readable and writable by root, readable by anyone else).
*   **libtool-file-present** (*warning*) This file is a libtool (.la) file and should not be normally present. One can use the `!libtool` option in the *options* array of the PKGBUILD to remove these files automatically.
*   **perllocal-pod-present** (*error*) The file perllocal.pod should not be present in a perl package; see the [Perl package guidelines](/index.php/Perl_package_guidelines "Perl package guidelines") for more information.
*   **scrollkeeper-dir-exists** (*error*) A scrollkeeper directory was found in the package. scrollkeeper should not be run till post_{install,upgrade,remove}.
*   **info-dir-file-present** (*error*) The info directory file */usr/share/info/dir* was found in the package. This file should not be present.
*   **gnome-mime-file** (*error*) The file is an autogenerated GNOME mime file and should not be present in the package.

### Diversos

*   **insecure-rpath** (*error*) An RPATH (for an executable) is outside */usr/lib*. An RPATH to an insecure location is a potential security issue. See [FS#14049](https://bugs.archlinux.org/task/14049) for discussion.

### PKGBUILDs

These are the tags related to the PKGBUILDs. Some of these might also apply for binary packages.

*   **variable-not-array** (*warning*) The variable should be a bash array instead of a string. These are the variables which should be written as arrays: *arch*, *license*, *depends*, *makedepends*, *optdepends*, *provides*, *conflicts*, *replaces*, *backup*, *source*, *noextract*, *md5sums*
*   **backups-preceding-slashes** (*error*) The file mentioned in the backup array begins with a slash ('/').
*   **package-name-in-uppercase** (*error*) There should not be any upper case letters in package names.
*   **specific-host-type-used** (*warning*) Instead of using a specific host type (like i686 or x86_64) use the generic $CARCH variable.
*   **extra-var-begins-without-underscore** (*warning*) The variable is not one of the standard variables defined in the PKGBUILD manual, yet it does not begin with an underscore.
*   **file-referred-in-startdir** (*error*) A file was referenced in *$startdir* outside of *$startdir/pkg* and *$startdir/src*.
*   **missing-md5sums** (*error*) MD5sums corresponding to the source files are missing. These can be added to the PKGBUILD using `updpkgsums`.
*   **not-enough-md5sums** (*error*) There are more source files than MD5sums provided in the PKGBUILD.
*   **too-many-md5sums** (*error*) There are more MD5sums than source files in the PKGBUILD.
*   **improper-md5sum** (*error*) An improper MD5sum was found. MD5sums are of 32 characters in length.
*   **specific-sourceforge-mirror** (*warning*) The PKGBUILD uses a specific sourceforge mirror. [http://downloads.sourceforge.net](http://downloads.sourceforge.net) should be used instead.
*   **using-dl-sourceforge** (*warning*) The deprecated [http://dl.sourceforge.net](http://dl.sourceforge.net) domain is being used in the source array. [http://downloads.sourceforge.net](http://downloads.sourceforge.net) should be used instead.
*   **missing-contributor** (*warning*) The contributor tag is missing.
*   **missing-maintainer** (*warning*) The maintainer tag is missing.
*   **missing-url** (*error*) The package does not have an upstream homepage set. Use the `url` variable for this.
*   **pkgname-in-description** (*warning*) Description should not contain the package name.
*   **recommend-use-pkgdir** (*informational*) *$startdir/pkg* is deprecated, use *$pkgdir* instead.
*   **recommend-use-srcdir** (*informational*) *$startdir/src* is deprecated, use *$srcdir* instead.

### Não lançadas

There are currently no new tags in the development version.

## Fazendo um módulo de namcap

This section documents the innards of namcap and specifies how to create a new namcap module.

The main namcap program namcap.py takes as parameters the filename of a package or a PKGBUILD and makes a pkginfo object, which it passes to a list of rules defined in `__tarball__` and `__pkgbuild__`.

*   *__tarball__* defines the rules which process binary packages.
*   *__pkgbuild__* defines the rules which process PKGBUILDs

Once your module is finalized, remember to add it to the appropriate array (*__tarball__* or *__pkgbuild__*) defined in *Namcap/__init__.py*

A sample namcap module is like this:

 `namcap/url.py` 
```
  import pacman

  class package:
  	def short_name(self):
		return "url"
	def long_name(self):
		return "Verifies url is included in a PKGBUILD"
	def prereq(self):
		return ""
	def analyze(self, pkginfo, tar):
		ret = [[],[],[]]
		if not hasattr(pkginfo, 'url'):
			ret[0].append(("missing-url", ()))
		return ret
	def type(self):
		return "pkgbuild"

```

Mostly, the code is self-explanatory. The following are the list of the methods that each namcap module must have:

*   **short_name**(self) Returns a string containing a short name of the module. Usually, this is the same as the basename of the module file.
*   **long_name**(self) Returns a string containing a concise description of the module. This description is used when listing all the rules using `namcap -r list`.
*   **prereq**(self) Return a string containing the prerequisites needed for the module to operate properly. Usually "" for modules processing PKGBUILDs and "tar" for modules processing package files. "extract" should be specified if the package contents should be extracted to a temporary directory before further processing.
*   **analyze**(self, pkginfo, tar) Should return a list comprising in turn of three lists: of error tags, warning tags and information tags respectively. Each member of these tag lists should be a tuple consisting of two components: **the short, hyphenated form** of the tag with the appropriate format specifiers (%s, etc.) The first word of this string must be the tag name. The human readable form of the tag should be put in the tags file. The format of the tags file is described below; and **the parameters** which should replace the format specifier tokens in the final output.
*   **type**(self) "pkgbuild" for a module processing PKGBUILDs, "tarball" for a module processing a binary package file.

The tags file consists of lines specifying the human readable form of the hyphenated tags used in the namcap code. A line beginning with a '#' is treated as a comment. Otherwise the format of the file is:

```
 machine-parseable-tag %s :: This is machine parseable tag %s

```

Note that a double colon (::) is used to separate the hyphenated tag from the human readable description.

## Relatórios do namcap

**namcap-reports** is an automatically generated report obtained after running namcap against the core, extra and community trees.

How it works:

*   namcap is run against the entire [ABS](/index.php/ABS "ABS") tree to make `namcap.log`.
*   The packages in core, extra and community are put in files named core, extra and community respectively (using `pacman -Slq`).
*   `namcap-report.py` takes the code and prepares the report and RSS feeds, which is then copied to the webserver.