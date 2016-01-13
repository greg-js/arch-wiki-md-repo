# Makepkg (Português)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Creating packages](/index.php/Creating_packages "Creating packages")
*   [PKGBUILD](/index.php/PKGBUILD "PKGBUILD")
*   [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")
*   [pacman](/index.php/Pacman "Pacman")
*   [Official repositories](/index.php/Official_repositories "Official repositories")
*   [Arch Build System](/index.php/Arch_Build_System "Arch Build System")

Makepkg é usado para compilar e construir um pacote adequado para instalação com o [pacman](/index.php/Pacman "Pacman"), gerenciador de pacotes do Arch Linux. Makepkg é um script automático para a construção do pacote; podendo fazer o download e validar o arquivo, checando as dependências, configurações do tempo de compilação, compilar o código, instalar temporariamente como root, fazer a personalização, gerar informações, e por fim, fazer todo empacotamento.

O Makepkg é fornecido pelos pacotes do [pacman](https://www.archlinux.org/packages/?name=pacman) package.

## Contents

*   [1 Configuração](#Configura.C3.A7.C3.A3o)
    *   [1.1 Arquitetura, compilação flags](#Arquitetura.2C_compila.C3.A7.C3.A3o_flags)
        *   [1.1.1 MAKEFLAGS](#MAKEFLAGS)
    *   [1.2 Saída de pacote](#Sa.C3.ADda_de_pacote)
    *   [1.3 Verificação de assinatura](#Verifica.C3.A7.C3.A3o_de_assinatura)
    *   [1.4 fakeroot](#fakeroot)
*   [2 Uso](#Uso)
*   [3 Dicas e Truques](#Dicas_e_Truques)
    *   [3.1 Gerar novos md5sums](#Gerar_novos_md5sums)
    *   [3.2 Makepkg fonte PKGBUILD duas vezes](#Makepkg_fonte_PKGBUILD_duas_vezes)
    *   [3.3 AVISO: O pacote contém referência para $srcdir](#AVISO:_O_pacote_cont.C3.A9m_refer.C3.AAncia_para_.24srcdir)
*   [4 Veja também](#Veja_tamb.C3.A9m)

## Configuração

`/etc/makepkg.conf` é o principal arquivo de configuração para o makepkg. A maioria dos usuários desejam ajustar as opções de configuração para construção dos pacotes.

### Arquitetura, compilação flags

As opções `MAKEFLAGS`, `CFLAGS`, e `CXXFLAGS` são usadas pelo [make](https://www.archlinux.org/packages/?name=make), [gcc](https://www.archlinux.org/packages/?name=gcc), e `g++` enquanto a compilação de programa é com makepkg. Por padrão, essas opções de gerar pacotes genéricos podem ser instalados em uma ampla variedade de máquinas. Um ganho de desempenho pode ser alcançado por compilação de ajuste para o computador. A desvantagem é que os pacotes compilados especificamente para o processador do computador podem não funcionar em outras máquinas.

**Nota:** Tenha em mente que nem todos os sistemas de compilação de pacote usarão suas variáveis ​​exportadas. Algumas as substituem no makefile original ou [PKGBUILD](/index.php/PKGBUILD "PKGBUILD").

 `/etc/makepkg.conf` 

```
[...]

#########################################################################
# ARCHITECTURE, COMPILE FLAGS
#########################################################################
#
CARCH="x86_64"
CHOST="x86_64-unknown-linux-gnu"

#-- Exclusivo: só vai funcionar em x86_64
# -march (ou -mcpu) constrói exclusivamente para uma arquitetura
# -mtune otimiza para uma arquitetura, mas constrói para toda família de processadores
CPPFLAGS="-D_FORTIFY_SOURCE=2"
CFLAGS="-march=x86-64 -mtune=generic -O2 -pipe -fstack-protector --param=ssp-buffer-size=4"
CXXFLAGS="-march=x86-64 -mtune=generic -O2 -pipe -fstack-protector --param=ssp-buffer-size=4"
LDFLAGS="-Wl,-O1,--sort-common,--as-needed,-z,relro"
#-- Make Flags: mude este para sistemas DistCC/SMP
#MAKEFLAGS="-j2"

[...]

```

O padrão makepkg.conf `CFLAGS` e `CXXFLAGS` são compatíveis com todas as máquinas dentro de suas respectivas arquiteturas.

Em máquinas x86_64, há ganhos raramentes significativos o bastante de desempenho mundial que justifiquem investir o tempo para reconstruir os pacotes oficiais.

A partir da versão 4.3.0, GCC disponibiliza o `-march=native` que permite auto-detecção da CPU e seleciona automaticamente as otimizações suportadas pela máquina local no tempo de execução GCC. Para usá-lo, basta modificar as configurações padrão, alterando as linhas `CFLAGS` e `CXXFLAGS`:

```
# -march=native também define correto o -mtune=
CFLAGS="-march=native -O2 -pipe -fstack-protector --param=ssp-buffer-size=4 -D_FORTIFY_SOURCE=2"
CXXFLAGS="${CFLAGS}"

```

**Dica:** Para ver quais flags o `march=native` define, execute:

```
$ gcc -march=native -E -v - </dev/null 2>&1 | sed -n 's/.* -v - //p'

```

Otimizar ainda mais para o tipo de CPU pode, teoricamente, aumentar o desempenho, pois o `-march=native` permite que todas as instruções disponíveis definem e melhorem o agendamento para uma determinada CPU. Isto é especialmente perceptível na reconstrução de aplicativos (por exemplo: áudio/ferramentas de decodificação de video, aplicações científicas, programas matemáticos pesados, etc.) que podem tiram uma boa vantagem de configurações de instruções mais recentes não habilitadas ao usar opções padrão (ou pacotes) fornecido pelo Arch Linux.

É muito fácil reduzir o desempenho usando o CFLAGS "não-padrão", porque compiladores tendem fortemente passar o tamanho do código com loop, mal vetorização, louco inlining, etc. dependendo do compilador. A menos que possa verificar/benchmark que é mais rápido, há uma chance muito boa nisso!

Veja a página de manual do GCC para uma lista completa de opções disponíveis. O artigo wiki Gentoo [Compilation Optimization Guide](http://www.gentoo.org/doc/en/gcc-optimization.xml) e [Safe CFLAGS](http://wiki.gentoo.org/wiki/Safe_CFLAGS) fornecem informações mais profundas.

#### MAKEFLAGS

A opção `MAKEFLAGS` pode ser usada para especificar opções adicionais a fazer. Usuários com sistemas multi-core/multi-processador podem especificar o número de tarefas para executar simultaneamente. Isto pode ser feito com o uso do `nproc` para determinar o número de processadores disponíveis, e.x. `-j4` _(onde 4 é a saída de `nproc`)_. Alguns especificamente do [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") substituem isso com `-j1`, por causa de corriqueira condições em determinadas versões ou simplesmente porque isso não é suportado, em primeiro lugar. Os pacotes que falham ao construir por causa disso devem ser [reportados](/index.php/Reporting_bug_guidelines "Reporting bug guidelines") no bug tracker depois de ter certeza que o erro é de fato causado por sua MAKEFLAGS.

Consulte `man make` para obter uma lista completa das opções disponíveis.

### Saída de pacote

Em seguida, pode-se configurar onde os arquivos de origem e pacotes deverão ser colocados e identificá-los como empacotadores. Esta etapa é opcional, pacotes serão criados no diretório de trabalho, onde o makepkg é executado por padrão.

 `/etc/makepkg.conf` 

```
[...]

#########################################################################
# PACKAGE OUTPUT
#########################################################################
#
# Default: put built package and cached source in build directory
#
#-- Destination: specify a fixed directory where all packages will be placed
#PKGDEST=/home/packages
#-- Source cache: specify a fixed directory where source files will be cached
#SRCDEST=/home/sources
#-- Source packages: specify a fixed directory where all src packages will be placed
#SRCPKGDEST=/home/srcpackages
#-- Packager: name/email of the person or organization building packages
#PACKAGER="John Doe <john@doe.com>"

[...]

```

Por exemplo, crie o diretório:

```
$ mkdir /home/$USER/packages

```

Então modifique a variável `PKGDEST` em `/etc/makepkg.conf` adequadamente.

A variável `PACKAGER` definirá o valor `packager` dentro dos arquivos de pacotes compilados metadata' `.PKGINFO`. Por padrão, usuários-pacotes compilados exibirão:

 `pacman -Qi package` 

```
[...]
Packager       : Unknown Packager
[...]

```

Depois:

 `pacman -Qi package` 

```
[...]
Packager       : John Doe <john@doe.com>
[...]

```

Será útil se vários usuários copilarem pacotes em um sistema, ou se você for distribuir seus pacotes para outros usuários.

### Verificação de assinatura

O procedimento a seguir não é necessário para compilar com makepkg, para a sua configuração inicial, vá para [#Usage](#Usage). Para desativar temporariamente a verificação de assinatura chame o comando makepkg com a opção `--skippgpcheck`. Se um arquivo de assinatura na forma de .sig faz parte da array de orgigem [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"), makepkg valida a autenticidade dos arquivos de origem. Por exemplo, a assinatura pkgname-pkgver.tar.gz.sig é usada para verificar a integridade do arquivo pkgname-pkgver.tar.gz com o programa gpg. Se desejar, assinaturas de outros desenvolvedores podem ser adicionadas manualmente ao conjunto de chaves gpg. Veja no artigo [GnuPG](/index.php/GnuPG "GnuPG") para mais informação.

**Nota:** A verificação de assinatura implementada no makepkg não usa o conjunto de chaves do pacman. Configure gpg como explicado abaixo para permitir que o makepkg leia o conjunto de chaves do pacman.

As chaves GPG devem ser armazenados no arquivo de usuário `~/.gnupg/pubring.gpg`. No caso de não conter a assinatura determinada, makepkg mostra um aviso.

 `makepkg` 

```
[...]
==> Verifying source file signatures with gpg...
pkgname-pkgver.tar.gz ... FAILED (unknown public key 1234567890)
==> WARNING: Warnings have occurred while verifying the signatures.
    Please make sure you really trust them.
[...]

```

Para mostrar a lista atual de chaves GPG use o comando gpg.

 `gpg --list-keys` 

Se não existe o arquivo pubring.gpg, ele será criado para você imediatamente. Agora você pode prosseguir com a configuração gpg para permitir a compilação de pacotes AUR submetidos pelos desenvolvedores do Arch Linux com verificação com sucesso de assinatura. Adicione a seguinte linha no final do arquivo de configuração gpg para incluir conjunto de chaves pacman no conjunto de chaves pessoal do usuário.

 `~/.gnupg/gpg.conf` 

```
[...]
keyring /etc/pacman.d/gnupg/pubring.gpg

```

Quando for configurado como dito anteriormente, a saída de `gpg --list-keys` contém uma lista de conjunto de chaves e desenvolvedores. Agora makepkg pode compilar pacotes AUR apresentados pelos desenvolvedores Arch Linux com a verificação com sucesso de assinatura.

### `fakeroot`

Fakeroot é a permisão normal do usuário sem a necessidade do root para criar um pacote, sem poder alterar o sistema por completo. Se as tentativas de alterar o processo em construção fora do ambiente de compilação, os erros são abordados e mostra a falha – para verificar a qualidade/segurança/integridade nos PKGBUILDs para a distribuição. Por default, o fakeroot é habilitado no diretório “/etc/make.pkg”; o usuário por opção pode por **!** no BUILDENV para desabilitar.

## Uso

Antes de continuar, verifique se o grupo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) está instalado. Os pacotes que pertencem a este grupo não são requeridos na lista de dependência nos arquivos [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"). A instalação do grupo "base-devel" é como root:

```
# pacman -S base-devel

```

**Nota:** Antes de reclamar sobre a falta (criar) pacotes, lembre-se sobre o grupo “base” que assume a instalação de todo o sistema do Arch Linux. O grupo "base-devel" assume toda a instação durante a construção com o **makepkg**.

A construção do pacote, necessita criar um primeiro [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"), ou Script, com descrição na [Creating packages](/index.php/Creating_packages "Creating packages"), ou obter a partir [ABS tree](/index.php/Arch_Build_System "Arch Build System"), [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"), ou atráves de outras fontes.

**Atenção:** Apenas construção/instalação de pacotes com fontes confiáveis.

Com o `PKGBUILD`, mude para o diretório onde ele se encontra e execute o seguinte comando para construir o pacote descrito pelo `PKGBUILD`:

```
$ makepkg

```

Para que o makepkg limpe arquivos e pastas restantes, tais como arquivos extraídos para o $srcdir, adicione a seguinte opção. É útil para vários construções do mesmo pacote ou ao atualizar a versão do pacote, enquanto usa a mesma pasta de compilação.

```
$ makepkg -c

```

Se está faltando dependências necessárias, makepkg emitirá um aviso antes de falhar. Para construir o pacote e instalar as dependências automaticamente, basta usar o comando:

```
$ makepkg -s

```

Note que essas dependências devem estar disponíveis nos repositórios configurados, consulte [pacman#Repositories](/index.php/Pacman#Repositories "Pacman") para detalhes. Alternativa para instalação manual de dependência antes da construção (`pacman -S --asdeps dep1 dep2`).

Uma vez que todas as dependências estão satisfeita e os pacotes construídos, um arquivo de pacote (`pkgname-pkgver.pkg.tar.xz`) será criado no diretório. Para instalação, como root:

```
# pacman -U pkgname-pkgver.pkg.tar.xz

```

Alternativamente, para instalar, usando o `-i` é um jeito mais fácil de executar `pacman -U pkgname-pkgver.pkg.tar.xz`, como:

```
$ makepkg -i

```

## Dicas e Truques

### Gerar novos md5sums

Desde [pacman 4.1](http://allanmcrae.com/2013/04/pacman-4-1-released/) `makepkg -g >> PKGBUILD` não é mais necessário como pacman-contrib foi [merged](https://projects.archlinux.org/pacman.git/tree/NEWS) juntamente com o script `updpkgsums` capaz de gerar novos checksums e substituí-los no PKGBUILD:

```
$ updpkgsums

```

### Makepkg fonte PKGBUILD duas vezes

Makepkg fontes a PKGBUILD duas vezes (uma quando executado, e a segunda sob fakeroot). Qualquer função não-padrão colocada no PKGBUILD será executada duas vezes também.

### AVISO: O pacote contém referência para $srcdir

De alguma forma, as strings literais `$srcdir` ou `$pkgdir` acabaram em um dos arquivos instalados no seu pacote.

Para identificar quais arquivos, execute o seguinte do diretório de compilação makepkg:

```
$ grep -R "$(pwd)/src" pkg/

```

[Link](http://www.mail-archive.com/arch-general@archlinux.org/msg15561.html) em discussão.

## Veja também

*   [gcccpuopt](https://github.com/pixelb/scripts/blob/master/scripts/gcccpuopt): Um script para mostrar as opções gcc específicas da CPU adaptados para a CPU atual.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Makepkg_(Português)&oldid=415003](https://wiki.archlinux.org/index.php?title=Makepkg_(Português)&oldid=415003)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Package development (Português)](/index.php/Category:Package_development_(Portugu%C3%AAs) "Category:Package development (Português)")
*   [About Arch (Português)](/index.php/Category:About_Arch_(Portugu%C3%AAs) "Category:About Arch (Português)")