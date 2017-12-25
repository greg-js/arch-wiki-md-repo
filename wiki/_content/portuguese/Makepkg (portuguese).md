Artigos relacionados

*   [Criando pacotes](/index.php/Criando_pacotes "Criando pacotes")
*   [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)")
*   [Arch User Repository](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)")
*   [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)")
*   [Repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais")
*   [Arch Build System](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)")

Makepkg é usado para compilar e construir um pacote adequado para instalação com o [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)"), gerenciador de pacotes do Arch Linux. Makepkg é um script automático para a construção do pacote; podendo fazer o download e validar o arquivo, checando as dependências, configurações do tempo de compilação, compilar o código, instalar temporariamente como root, fazer a personalização, gerar informações, e por fim, fazer todo empacotamento.

O Makepkg é fornecido pelos pacotes do [pacman](https://www.archlinux.org/packages/?name=pacman) package.

## Contents

*   [1 Configuração](#Configura.C3.A7.C3.A3o)
    *   [1.1 Informação do empacotador](#Informa.C3.A7.C3.A3o_do_empacotador)
    *   [1.2 Saída de pacote](#Sa.C3.ADda_de_pacote)
    *   [1.3 Verificação de assinatura](#Verifica.C3.A7.C3.A3o_de_assinatura)
*   [2 Uso](#Uso)
*   [3 Dicas e Truques](#Dicas_e_Truques)
    *   [3.1 Criando pacotes otimizados](#Criando_pacotes_otimizados)
        *   [3.1.1 MAKEFLAGS](#MAKEFLAGS)
    *   [3.2 Mostrar pacotes com um empacote específico](#Mostrar_pacotes_com_um_empacote_espec.C3.ADfico)
    *   [3.3 Melhorando os tempos de compilação](#Melhorando_os_tempos_de_compila.C3.A7.C3.A3o)
        *   [3.3.1 tmpfs](#tmpfs)
        *   [3.3.2 ccache](#ccache)
    *   [3.4 Gerar novos checksums](#Gerar_novos_checksums)
    *   [3.5 Usar outros algoritmos de compressão](#Usar_outros_algoritmos_de_compress.C3.A3o)
    *   [3.6 Usando núcleos na compressão](#Usando_n.C3.BAcleos_na_compress.C3.A3o)
    *   [3.7 Compilar pacotes 32 bits em um sistema 64 bits](#Compilar_pacotes_32_bits_em_um_sistema_64_bits)
*   [4 Solução de problemas](#Solu.C3.A7.C3.A3o_de_problemas)
    *   [4.1 Makepkg algumas vezes falha ao assinar um pacote sem perguntar pela palavra-chave de assinatura](#Makepkg_algumas_vezes_falha_ao_assinar_um_pacote_sem_perguntar_pela_palavra-chave_de_assinatura)
    *   [4.2 CFLAGS/CXXFLAGS/CPPFLAGS no makepkg.conf não funciona para pacotes baseados no QMAKE](#CFLAGS.2FCXXFLAGS.2FCPPFLAGS_no_makepkg.conf_n.C3.A3o_funciona_para_pacotes_baseados_no_QMAKE)
    *   [4.3 Especificando diretório de instalação para pacotes baseados em QMAKE](#Especificando_diret.C3.B3rio_de_instala.C3.A7.C3.A3o_para_pacotes_baseados_em_QMAKE)
    *   [4.4 AVISO: O pacote contém referência para $srcdir](#AVISO:_O_pacote_cont.C3.A9m_refer.C3.AAncia_para_.24srcdir)
*   [5 Veja também](#Veja_tamb.C3.A9m)

## Configuração

Veja [makepkg.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/makepkg.conf.5) para detalhes sobre as opções de configuração do makepkg.

A configuração do sistema está disponível em `/etc/makepkg.conf`, mas alterações específicas para cada usu[ario podem ser feitas em `$XDG_CONFIG_HOME/pacman/makepkg.conf` ou `~/.makepkg.conf`. É recomendado revisar a configuração antes de compilar pacotes.

### Informação do empacotador

Cada pacote é marcado com metadados identificando, entre outros, também o *empacotador*. Por padrão, os pacotes compilados pelo usuário são marcados com `Empacotador desconhecido`. Se vários usuários estiverem compilando pacotes em um sistema, ou de outra forma distribuindo seus pacotes para outros usuários, é conveniente fornecer contato real. Isso pode ser feito configurando a variável `PACKAGER` em `makepkg.conf`.

Para verificar isso em um pacote instalado:

 `$ pacman -Qi *pacote*` 
```
[...]
Empacotador       : John Doe <john@doe.com>
[...]

```

Para automaticamente produzir pacotes assinados, defina também a variável `GPGKEY` em `makepkg.conf`.

### Saída de pacote

Por padrão, *makepkg* cria os *tarballs* de pacote no diretório atual de trabalho e baixa os dados fonte diretamente para o diretório `src/`. Caminhos personalizados podem ser configurados, por exemplo, para manter todos os pacotes compilados em `~/build/pacotes/` e todos os fontes em `~/build/fontes/`.

Configure as seguintes variáveis do `makepkg.conf`, se necessário:

*   `PKGDEST` – diretório para armazenar pacotes resultantes
*   `SRCDEST` – diretório para armazenar dados [fonte](/index.php/PKGBUILD_(Portugu%C3%AAs)#source "PKGBUILD (Português)") (links simbólicos serão colocados em `src/` se ele aponta para outro lugar)
*   `SRCPKGDEST` – diretório para armazenar os pacotes fontes (compilado com `makepkg -S`)

### Verificação de assinatura

**Nota:** A verificação de assinatura implementada no *makepkg* não usa o chaveiro do pacman; em vez disso, depende do chaveiro do usuário.

Se um arquivo de assinatura na forma de `.sig` ou `.asc` é parte do vetor fonte do [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)"), o *makepkg* tenta automaticamente [verificá-la](/index.php/GnuPG#Verify_a_signature "GnuPG"). No caso do chaveiro do usuário não contém a chave pública necessária para verificação de assinatura, o *makepkg* vai abortar a instalação com uma mensagem de que a chave PGP não pôde ser verificada.

Se uma chave pública necessária para um pacote está faltando, o [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") muito provavelmente vai conter uma entrada [validpgpkeys](/index.php/PKGBUILD_(Portugu%C3%AAs)#validpgpkeys "PKGBUILD (Português)") com os IDs de chaves necessárias. Você pode [importá-la](/index.php/GnuPG#Import_a_public_key "GnuPG") manualmente ou você pode localizá-la [em um servidor de chaves](/index.php/GnuPG#Use_a_keyserver "GnuPG") e importá-la de lá.

## Uso

Antes de continuar, verifique se o grupo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) está instalado. Os pacotes que pertencem a este grupo não são requeridos na lista de dependência nos arquivos [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)"). A instalação do grupo "base-devel" é como root:

```
# pacman -S base-devel

```

**Nota:** Antes de reclamar sobre a falta (criar) pacotes, lembre-se sobre o grupo “base” que assume a instalação de todo o sistema do Arch Linux. O grupo "base-devel" assume toda a instação durante a construção com o **makepkg**.

A construção do pacote, necessita criar um primeiro [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)"), ou Script, com descrição na [Criando pacotes](/index.php/Criando_pacotes "Criando pacotes"), ou obter a partir [árvore do ABS](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)"), [Arch User Repository](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)"), ou através de outras fontes.

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

Note que essas dependências devem estar disponíveis nos repositórios configurados, consulte [pacman (Português)#Repositórios e espelhos](/index.php/Pacman_(Portugu%C3%AAs)#Reposit.C3.B3rios_e_espelhos "Pacman (Português)") para detalhes. Alternativa para instalação manual de dependência antes da construção (`pacman -S --asdeps dep1 dep2`).

Uma vez que todas as dependências estão satisfeita e os pacotes construídos, um arquivo de pacote (`pkgname-pkgver.pkg.tar.xz`) será criado no diretório. Para instalação, como root:

```
# pacman -U pkgname-pkgver.pkg.tar.xz

```

Alternativamente, para instalar, usando o `-i` é um jeito mais fácil de executar `pacman -U pkgname-pkgver.pkg.tar.xz`, como:

```
$ makepkg -i

```

## Dicas e Truques

### Criando pacotes otimizados

Uma melhoria de desempenho do software empacotado pode ser conseguida ao permitir otimizações do compilador para a máquina host. A desvantagem é que os pacotes compilados para uma arquitetura de processador específica não serão executados corretamente em outras máquinas. Nas máquinas x86_64, raramente existem ganhos de desempenho reais reais significativos que justificariam investir o tempo para reconstruir pacotes oficiais.

No entanto, é muito fácil reduzir o desempenho usando *flags* de compilação "não padronizadas". Muitas otimizações de compilação só são úteis em certas situações e não devem ser aplicadas indiscriminadamente em cada pacote. A menos que você possa verificar/avaliar que algo é mais rápido, há uma chance muito boa de não ser! O [Guia de Otimização de Compilação](http://www.gentoo.org/doc/en/gcc-optimization.xml) e artigo wiki [CFLAGS Seguras](http://wiki.gentoo.org/wiki/Safe_CFLAGS) do Gentoo (ambos em inglês) fornecem mais informações detalhadas sobre a otimização do compilador.

As opções passadas para um compilador C/C++ (ex.: [gcc](https://www.archlinux.org/packages/?name=gcc) ou [clang](https://www.archlinux.org/packages/?name=clang)) são controladas pelas variáveis de ambiente `CFLAGS`, `CXXFLAGS` e`CPPFLAGS`. Da mesma forma, o sistema de compilação [make](https://www.archlinux.org/packages/?name=make) usa `MAKEFLAGS`. Para usar o sistema de compilação do Arch, o *makepkg* expõe essas variáveis de ambiente como opções de configuração no `makepkg.conf`. Os valores padrão são configurados para produzir pacotes genéricos que podem ser instalados em uma ampla gama de máquinas.

**Nota:** Tenha em mente que nem todos os sistemas de compilação usam as variáveis configuradas no `makepkg.conf`. Por exemplo, *cmake* ignora a variável de ambiente das opções de pré-processador, `CPPFLAGS`. Consequentemente, muitos [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") contêm soluções alternativas com opções específicas para o sistema de compilação usado pelo software empacotado.

O GCC pode detectar e habilitar automaticamente otimizações seguras específicas para cada arquitetura. Para usar esse recurso, primeiro remova os sinalizadores `-march` e `-mtune`, então adicione `-march = native`. Por exemplo,

```
CFLAGS="-march=native -O2 -pipe -fstack-protector-strong -fno-plt"
CXXFLAGS="${CFLAGS}"

```

Para ver quais sinalizadores isso habilita em sua máquina, execute:

```
$ gcc -march=native -v -Q --help=target

```

**Nota:** Se você especificar um valor diferente de `-march=native`, então `-Q --help=target` **não vai** funcionar como esperado.[[1]](https://bbs.archlinux.org/viewtopic.php?pid=1616694#p1616694) Você precisa passar por uma fase de compilação para descobrir quais opções estão realmente habilitadas. Veja [Encontre opções específicas da CPU](https://wiki.gentoo.org/wiki/Safe_CFLAGS#Find_CPU-specific_options) (inglês) no wiki do Gentoo para instruções.

#### MAKEFLAGS

A opção `MAKEFLAGS` pode ser usada para especificar opções adicionais para fazer. Os usuários com sistemas multi-core/multiprocessador podem especificar o número de tarefas a serem executadas simultaneamente. Isso pode ser realizado com o uso de *nproc* para determinar o número de processadores disponíveis, ex.: `MAKEFLAGS="-j$(nproc)"`. Alguns [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") substituem especificamente isso com `-j1`, devido a condições de corrida em certas versões ou simplesmente porque não há suporte em primeiro lugar. Os pacotes que não conseguem ser compilados por causa disso devem ser [relatados](/index.php/Reporting_bug_guidelines "Reporting bug guidelines") no rastreador de erros (ou no caso dos pacotes [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)"), para o mantenedor do pacote) depois de ter certeza de que o erro está realmente sendo causado pelo seu `MAKEFLAGS`.

Veja [make(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/make.1) para uma lista completa de opções disponíveis.

### Mostrar pacotes com um empacote específico

Isso mostra todos os pacotes instalados no sistema com o empacotador chamado *nome-empacotador*:

```
$ expac "%n %p" | grep "*nome-empacotador*" | column -t

```

Isso mostra todos os pacotes instalados no sistema com o empacotador definido na variável `PACKAGER` do `/etc/makepkg`. Isso mostra apenas pacotes que estão em um repositório definido em `/etc/pacman.conf`.

```
$ . /etc/makepkg.conf; grep -xvFf <(pacman -Qqm) <(expac "%n\t%p" | grep "$PACKAGER$" | cut -f1)

```

### Melhorando os tempos de compilação

#### tmpfs

Como a compilação requer muitas operações de E/S e lidar com arquivos pequenos, mover o diretório de trabalhos para um [tmpfs](/index.php/Tmpfs "Tmpfs") pode trazer melhorias em tempos de compilação.

A variável `BUILDDIR` pode ser temporariamente exportada para *makepkg* para definir o diretório de compilação para um tmpfs existente. Por exemplo:

```
$ BUILDDIR=/tmp/makepkg makepkg

```

**Atenção:** Evite compilar pacotes grandes no tmpfs para evitar ficar sem memória.

Configuração persistente pode ser feita no `makepkg.conf` descomentando a opção `BUILDDIR`, que é encontrada no fim da seção `BUILD ENVIRONMENT` no arquivo padrão `/etc/makepkg.conf`. Definir esses valores para, por exemplo, `BUILDDIR=/tmp/makepkg` fará uso do `/tmp` [tmpfs](/index.php/Tmpfs "Tmpfs") padrão do Arch.

**Nota:**

*   A pasta [tmpfs](/index.php/Tmpfs "Tmpfs") deve ser montada sem a opção `noexec`; do contrário, ela vai evitar que scripts de compilação ou utilitários sejam executados.
*   Tenha em mente que qualquer pacote compilado no [tmpfs](/index.php/Tmpfs "Tmpfs") não persistirá após reinicialização. Considere configurar a opção [PKGDEST](#Sa.C3.ADda_de_pacote) apropriadamente para mover o pacote compilado automaticamente para outro diretório (persistente).

#### ccache

O uso de [ccache](/index.php/Ccache "Ccache") pode melhorar os tempos de compilação ao armazenar em cache os resultados de compilações.

### Gerar novos checksums

Execute o seguinte comando no mesmo diretório que o arquivo PKGBUILD para gerar novas somas de verificação (*checksums*):

```
$ updpkgsums

```

### Usar outros algoritmos de compressão

Para acelerar o empacotamento e a instalação, com a consequência de ter arquivos de pacotes maiores, você pode alterar `PKGEXT`. Por exemplo, o seguinte torna o arquivo de pacote descompactado para apenas uma invocação:

```
$ PKGEXT='.pkg.tar' makepkg

```

Um outro exemplo abaixo mostra o uso do algoritmo lzop, com o pacote [lzo](https://www.archlinux.org/packages/?name=lzo) necessário:

```
$ PKGEXT='.pkg.tar.lzo' makepkg

```

Para fazer uma dessas configurações permanentes, configure `PKGEXT` em `/etc/makepkg.conf`.

### Usando núcleos na compressão

O [xz](https://www.archlinux.org/packages/?name=xz) oferece suporte a [multiprocessamento simétrico (SMP)](https://en.wikipedia.org/wiki/pt:Multiprocessamento_sim%C3%A9trico "wikipedia:pt:Multiprocessamento simétrico") por meio do sinalizador `--threads` para acelerar a compressão. Por exemplo, para deixar o makepkg usar quantos núcleos de CPU for possível para comprimir os pacotes, edite o vetor `COMPRESSXZ` em `/etc/makepkg.conf`:

```
COMPRESSXZ=(xz -c -z - **--threads=0**)

```

O [pigz](https://www.archlinux.org/packages/?name=pigz) é uma implementação paralela para o [gzip](https://www.archlinux.org/packages/?name=gzip) que, por padrão, usa todos os núcleos disponíveis na CPU (o sinalizador `-p/--processes` pode ser usado para empregar menos núcleos):

```
COMPRESSGZ=(**pigz** -c -f -n)

```

### Compilar pacotes 32 bits em um sistema 64 bits

**Atenção:** Erros foram relatados ao usar esse método par compilar o pacote [linux](https://www.archlinux.org/packages/?name=linux). O [método de instalação](/index.php/Install_bundled_32-bit_system_in_64-bit_system "Install bundled 32-bit system in 64-bit system") é preferível e verificou-se que funciona para compilar os pacotes do kernel.

Primeiro, habilite o repositório [multilib](/index.php/Multilib_(Portugu%C3%AAs) "Multilib (Português)") e [instale](/index.php/Instale "Instale") [multilib-devel](https://www.archlinux.org/groups/x86_64/multilib-devel/).

Então, crie um arquivo de configuração 32 bits

 `~/.makepkg.i686.conf` 
```
CARCH="i686"
CHOST="i686-unknown-linux-gnu"
CFLAGS="-m32 -march=i686 -mtune=generic -O2 -pipe -fstack-protector-strong"
CXXFLAGS="${CFLAGS}"
LDFLAGS="-m32 -Wl,-O1,--sort-common,--as-needed,-z,relro"
```

e chame o makepkg assim

```
$ linux32 makepkg --config ~/.makepkg.i686.conf

```

## Solução de problemas

### Makepkg algumas vezes falha ao assinar um pacote sem perguntar pela palavra-chave de assinatura

Com o [gnupg 2.1](https://www.gnupg.org/faq/whats-new-in-2.1.html), gpg-agent agora é iniciado automaticamente pelo gpg. O problema surge no estágio do pacote de `makepkg --sign`. Para permitir os privilégios corretos, [fakeroot](https://www.archlinux.org/packages/?name=fakeroot) executa a função `package()` iniciando o gpg-agent dentro do mesmo ambiente *fakeroot*. Na saída, o *fakeroot* limpa os semáforos fazendo com que a "escrita" termine o *pipe* para fechar para aquela instância do gpg-agent que resultará em um erro de *pipe* quebrado. Se o mesmo gpg-agent estiver em execução quando `makepkg --sign` estiver próximo de executado, então o gpg-agent retorna código de saída 2; então a seguinte saída ocorre:

```
==> Assinando pacote...
==> ATENÇÃO: Falha em assinar arquivo de pacote.

```

Esse erro está atualmente sendo rastreado: [FS#49946](https://bugs.archlinux.org/task/49946). Uma solução temporária de contorno para esse problema é executar `killall gpg-agent && makepkg --sign`. Esse problema está resolvido no [pacman-git](https://aur.archlinux.org/packages/pacman-git/), especificamento no hash de commit `c6b04c04653ba9933fe978829148312e412a9ea7`

### CFLAGS/CXXFLAGS/CPPFLAGS no makepkg.conf não funciona para pacotes baseados no QMAKE

Qmake configura automaticamente a variável `CFLAGS` e `CXXFLAGS` de acordo com o que você pensa que deveria ser a configuração correta. Para deixar o qmake usar as variáveis definidas no arquivo de configuração do makepkg, você deve editar o PKGBUILD e passar as variáveis [QMAKE_CFLAGS_RELEASE](http://doc.qt.io/qt-5/qmake-variable-reference.html#qmake-cflags-release) e [QMAKE_CXXFLAGS_RELEASE](http://doc.qt.io/qt-5/qmake-variable-reference.html#qmake-cxxflags-release) ao qmake. Por exemplo:

 `PKGBUILD` 
```
...

build() {
  cd "$srcdir/$_pkgname-$pkgver-src"
  qmake-qt4 "$srcdir/$_pkgname-$pkgver-src/$_pkgname.pro" \
    PREFIX=/usr \
    QMAKE_CFLAGS_RELEASE="${CFLAGS}"\
    QMAKE_CXXFLAGS_RELEASE="${CXXFLAGS}"

  make
}

...

```

Alternativamente, para uma configuração para todo sistema, você pode criar seu próprio `qmake.conf` e configurar a variável de ambiente [QMAKESPEC](http://doc.qt.io/qt-5/qmake-environment-reference.html#qmakespec).

### Especificando diretório de instalação para pacotes baseados em QMAKE

O makefile gerado pelo qmake usa a variável de ambiente INSTALL_ROOT para especificar onde o programa deve ser instalado. Então, essa função *package* deve funcionar:

 `PKGBUILD` 
```
...

package() {
	cd "$srcdir/${pkgname%-git}"
	make INSTALL_ROOT="$pkgdir" install
}

...

```

Note que o qmake também tem que ser configurado adequadamente. Por exemplo, coloque isso em seu arquivo .pro:

 `SeuProjeto.pro` 
```
...

target.path = /usr/local/bin
INSTALLS += target

...

```

### AVISO: O pacote contém referência para $srcdir

De alguma forma, as strings literais `$srcdir` ou `$pkgdir` acabaram em um dos arquivos instalados no seu pacote.

Para identificar quais arquivos, execute o seguinte do diretório de compilação makepkg:

```
$ grep -R "$(pwd)/src" pkg/

```

[Link](http://www.mail-archive.com/arch-general@archlinux.org/msg15561.html) em discussão.

## Veja também

*   [Página de manual makepkg(8)](https://www.archlinux.org/pacman/makepkg.8.html)
*   [Página de manual makepkg.conf(5)](https://www.archlinux.org/pacman/makepkg.conf.5.html)
*   [Um breve passeio no processo do makepkg](https://gist.github.com/Earnestly/bebad057f40a662b5cc3)
*   [Código fonte do makepkg](https://projects.archlinux.org/pacman.git/tree/scripts/makepkg.sh.in)