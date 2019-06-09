**Status de tradução:** Esse artigo é uma tradução de [Makepkg](/index.php/Makepkg "Makepkg"). Data da última tradução: 2019-05-24\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Makepkg&diff=0&oldid=572163) na versão em inglês.

Artigos relacionados

*   [Criando pacotes](/index.php/Criando_pacotes "Criando pacotes")
*   [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)")
*   [Arch User Repository](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)")
*   [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)")
*   [Repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais")
*   [Arch Build System](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)")

[makepkg](https://projects.archlinux.org/pacman.git/tree/scripts/makepkg.sh.in) é um script usado para automatizar a compilação de pacotes. Os requisitos para usar o script são uma plataforma tipo Unix capaz de compilar e um [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)").

O *makepkg* é fornecido pelo pacote [pacman](https://www.archlinux.org/packages/?name=pacman).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Configuração](#Configuração)
    *   [1.1 Informação do empacotador](#Informação_do_empacotador)
    *   [1.2 Saída de pacote](#Saída_de_pacote)
    *   [1.3 Verificação de assinatura](#Verificação_de_assinatura)
*   [2 Uso](#Uso)
*   [3 Dicas e truques](#Dicas_e_truques)
    *   [3.1 Compilando binários otimizados](#Compilando_binários_otimizados)
    *   [3.2 Melhorando os tempos de compilação](#Melhorando_os_tempos_de_compilação)
        *   [3.2.1 Compilação paralela](#Compilação_paralela)
        *   [3.2.2 Compilando de arquivos na memória](#Compilando_de_arquivos_na_memória)
        *   [3.2.3 Usando cache de compilação](#Usando_cache_de_compilação)
    *   [3.3 Gerar novos checksums](#Gerar_novos_checksums)
    *   [3.4 Usar outros algoritmos de compressão](#Usar_outros_algoritmos_de_compressão)
    *   [3.5 Usando vários núcleos na compressão](#Usando_vários_núcleos_na_compressão)
    *   [3.6 Mostrar pacotes com um empacotador específico](#Mostrar_pacotes_com_um_empacotador_específico)
    *   [3.7 Compilar pacotes 32 bits em um sistema 64 bits](#Compilar_pacotes_32_bits_em_um_sistema_64_bits)
*   [4 Solução de problemas](#Solução_de_problemas)
    *   [4.1 Makepkg algumas vezes falha ao assinar um pacote sem perguntar pela palavra-chave de assinatura](#Makepkg_algumas_vezes_falha_ao_assinar_um_pacote_sem_perguntar_pela_palavra-chave_de_assinatura)
    *   [4.2 CFLAGS/CXXFLAGS/LDFLAGS no makepkg.conf não funcionam para pacotes baseados no CMAKE](#CFLAGS/CXXFLAGS/LDFLAGS_no_makepkg.conf_não_funcionam_para_pacotes_baseados_no_CMAKE)
    *   [4.3 CFLAGS/CXXFLAGS/LDFLAGS no makepkg.conf não funcionam para pacotes baseados no QMAKE](#CFLAGS/CXXFLAGS/LDFLAGS_no_makepkg.conf_não_funcionam_para_pacotes_baseados_no_QMAKE)
    *   [4.4 Especificando diretório de instalação para pacotes baseados em QMAKE](#Especificando_diretório_de_instalação_para_pacotes_baseados_em_QMAKE)
    *   [4.5 AVISO: O pacote contém referência para $srcdir](#AVISO:_O_pacote_contém_referência_para_$srcdir)
    *   [4.6 ERRO: Uma ou mais assinaturas PGP não puderam ser verificadas!; o que eu devo fazer?](#ERRO:_Uma_ou_mais_assinaturas_PGP_não_puderam_ser_verificadas!;_o_que_eu_devo_fazer?)
    *   [4.7 Makepkg falha em baixar dependências quando por trás de um proxy](#Makepkg_falha_em_baixar_dependências_quando_por_trás_de_um_proxy)
        *   [4.7.1 Habilitar proxy definindo sua URL no XferCommand](#Habilitar_proxy_definindo_sua_URL_no_XferCommand)
        *   [4.7.2 Habilitar proxy via env_keep do sudoers](#Habilitar_proxy_via_env_keep_do_sudoers)
    *   [4.8 Makepkg falha, mas make obtém sucesso](#Makepkg_falha,_mas_make_obtém_sucesso)
*   [5 Veja também](#Veja_também)

## Configuração

Veja [makepkg.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/makepkg.conf.5) para detalhes sobre as opções de configuração do *makepkg*.

A configuração do sistema está disponível em `/etc/makepkg.conf`, mas alterações específicas para cada usu[ario podem ser feitas em `$XDG_CONFIG_HOME/pacman/makepkg.conf` ou `~/.makepkg.conf`. É recomendado revisar a configuração antes de compilar pacotes.

### Informação do empacotador

Cada pacote é marcado com metadados identificando, entre outros, também o *empacotador*. Por padrão, os pacotes compilados pelo usuário são marcados com `Empacotador desconhecido`. Se vários usuários estiverem compilando pacotes em um sistema, ou de outra forma distribuindo seus pacotes para outros usuários, é conveniente fornecer contato real. Isso pode ser feito configurando a variável `PACKAGER` em `makepkg.conf`.

Para verificar isso em um pacote instalado:

 `$ pacman -Qi *pacote*` 
```
...
Empacotador       : John Doe <john@doe.com>
...

```

Para automaticamente produzir pacotes assinados, defina também a variável `GPGKEY` em `makepkg.conf`.

### Saída de pacote

Por padrão, *makepkg* cria os *tarballs* de pacote no diretório atual de trabalho e baixa os dados fonte diretamente para o diretório `src/`. Caminhos personalizados podem ser configurados, por exemplo, para manter todos os pacotes compilados em `~/build/pacotes/` e todos os fontes em `~/build/fontes/`.

Configure as seguintes variáveis do `makepkg.conf`, se necessário:

*   `PKGDEST` – diretório para armazenar pacotes resultantes
*   `SRCDEST` – diretório para armazenar dados [fonte](/index.php/PKGBUILD_(Portugu%C3%AAs)#source "PKGBUILD (Português)") (links simbólicos serão colocados em `src/` se ele aponta para outro lugar)
*   `SRCPKGDEST` – diretório para armazenar os pacotes fontes (compilado com `makepkg -S`)

**Dica:** O diretório `PKGDEST` pode ser limpado com, p. ex., `paccache -c ~/build/pacotes/` como descrito em [pacman (Português)#Limpando o cache de pacotes](/index.php/Pacman_(Portugu%C3%AAs)#Limpando_o_cache_de_pacotes "Pacman (Português)").

### Verificação de assinatura

**Nota:** A verificação de assinatura implementada no *makepkg* não usa o chaveiro do pacman; em vez disso, depende do chaveiro do usuário.[[1]](http://allanmcrae.com/2015/01/two-pgp-keyrings-for-package-management-in-arch-linux/)

Se um arquivo de assinatura na forma de *.sig* ou *.asc* é parte do vetor fonte do [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)"), o *makepkg* tenta automaticamente [verificá-la](/index.php/GnuPG#Verify_a_signature "GnuPG"). No caso do chaveiro do usuário não contém a chave pública necessária para verificação de assinatura, o *makepkg* vai abortar a instalação com uma mensagem de que a chave PGP não pôde ser verificada.

Se uma chave pública necessária para um pacote está faltando, o [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") muito provavelmente vai conter uma entrada [validpgpkeys](/index.php/PKGBUILD_(Portugu%C3%AAs)#validpgpkeys "PKGBUILD (Português)") com os IDs de chaves necessárias. Você pode [importá-la](/index.php/GnuPG#Import_a_public_key "GnuPG") manualmente ou você pode localizá-la [em um servidor de chaves](/index.php/GnuPG#Use_a_keyserver "GnuPG") e importá-la de lá.

## Uso

Antes de continuar, [instale](/index.php/Instale "Instale") o grupo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/). Os pacotes que pertencem a este grupo **não** são exigidos na lista de dependência de compilação (*makedepends*) nos arquivos [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)"). Além disso, o grupo [base](https://www.archlinux.org/groups/x86_64/base/) é presumido como estando instalado em **todos** os sistemas Arch.

**Nota:** * Certifique-se de que o [sudo](/index.php/Sudo "Sudo") está configurado corretamente para comandos passados para o [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)").

*   Executar *makepkg* em si como root [não é permitido](https://lists.archlinux.org/pipermail/pacman-dev/2014-March/018911.html).[[2]](https://projects.archlinux.org/pacman.git/tree/NEWS) Além disso, como um `PKGBUILD` pode conter comandos arbitrários, compilar como root geralmente é considerado inseguro.[[3]](https://bbs.archlinux.org/viewtopic.php?id=67561) Usuários que não possuem acesso a uma conta de usuário comum devem executar o makepkg como o [usuário *nobody*](http://allanmcrae.com/2015/01/replacing-makepkg-asroot/).

Para compilar um pacote, deve-se primeiro criar um [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)"), ou um script de compilação, como descrito em [Criando pacotes](/index.php/Criando_pacotes "Criando pacotes"). Scripts existentes estão disponíveis na árvore do [Arch Build System](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)") *(ABS)* ou do [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)"). Uma vez em posse de um `PKGBUILD`, altere o diretório no qual está salvo e execute o seguinte comando para compilar o pacote:

```
$ makepkg

```

Se estiverem faltando dependências necessárias, o *makepkg* emitirá um aviso antes de falhar. Para compilar o pacote e instalar as dependências necessárias, adicione a opção `-s/--syncdeps`:

```
$ makepkg --syncdeps

```

Adicionar as opções `-r`/`--rmdeps` faz com que o *makepkg* remova as dependências de compilação logo em seguida, já que não são mais necessárias. Se estiver compilando pacotes constantemente, considere usar [Pacman/Dicas e truques#Removendo pacotes não usados (órfãos)](/index.php/Pacman/Dicas_e_truques#Removendo_pacotes_não_usados_(órfãos) "Pacman/Dicas e truques") de vez em quando.

**Nota:**

*   Essas dependências devem estar disponíveis nos repositórios configurados; veja [pacman (Português)#Repositórios e espelhos](/index.php/Pacman_(Portugu%C3%AAs)#Repositórios_e_espelhos "Pacman (Português)") para detalhes. Alternativamente, pode-se instalar manualmente as dependências antes de compilar (`pacman -S --asdeps *dep1* *dep2*`).
*   Apenas valores globais são usados ao instalar dependências, ou seja, qualquer sobrescrição feita em uma função de empacotamento de pacotes divididos não serão sadas.[[4]](https://patchwork.archlinux.org/patch/2271/)

Uma vez que todas as dependências estejam satisfeitas e os pacotes compilados com sucesso, um arquivo de pacote (`*pkgname*-*pkgver*.pkg.tar.xz`) será criado no diretório. Para instalar, use `-i`/`--install` (o mesmo que `pacman -U *pkgname*-*pkgver*.pkg.tar.xz`):

```
# pacman --install

```

Para limpar arquivos e pastas restantes, tais como arquivos extraídos para $`$srcdir`, adicione a opção `-c`/`--clean`. Isso é útil para várias compilações do mesmo pacote ou ao atualizar a versão do pacote, enquanto usa a mesma pasta de compilação. Isso evita arquivos obsoletos e remanescentes de serem carregados para novas compilações:

```
$ makepkg --clean

```

Para mais informações, veja [makepkg(8)](https://www.archlinux.org/pacman/makepkg.8.html).

## Dicas e truques

### Compilando binários otimizados

Uma melhoria de desempenho do software empacotado pode ser conseguida ao habilitar otimizações do compilador para a máquina host. A desvantagem é que os binários compilados para uma arquitetura de processador específica não serão executados corretamente em outras máquinas. Nas máquinas x86_64, raramente existem ganhos de desempenho reais reais significativos que justificariam investir o tempo para reconstruir pacotes oficiais.

No entanto, é muito fácil reduzir o desempenho usando *flags* de compilação "não padronizadas". Muitas otimizações de compilação só são úteis em certas situações e não devem ser aplicadas indiscriminadamente em cada pacote. A menos que você possa verificar/avaliar que algo é mais rápido, há uma chance muito boa de não ser! O [Guia de Otimização de Compilação](http://www.gentoo.org/doc/en/gcc-optimization.xml) e artigo wiki [CFLAGS Seguras](http://wiki.gentoo.org/wiki/Safe_CFLAGS) do Gentoo (ambos em inglês) fornecem mais informações detalhadas sobre a otimização do compilador.

As opções passadas para um compilador C/C++ (ex.: [gcc](https://www.archlinux.org/packages/?name=gcc) ou [clang](https://www.archlinux.org/packages/?name=clang)) são controladas pelas variáveis de ambiente `CFLAGS`, `CXXFLAGS` e`CPPFLAGS`. Para usar o sistema de compilação do Arch, o *makepkg* expõe essas variáveis de ambiente como opções de configuração no `makepkg.conf`. Os valores padrão são configurados para produzir binários genéricos que podem ser instalados em uma ampla gama de máquinas.

**Nota:** * Tenha em mente que nem todos os sistemas de compilação usam as variáveis configuradas no `makepkg.conf`. Por exemplo, *cmake* ignora a variável de ambiente das opções de pré-processador, `CPPFLAGS`. Consequentemente, muitos [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") contêm soluções alternativas com opções específicas para o sistema de compilação usado pelo software empacotado.

*   A configuração fornecida com o código fonte no `Makefile` ou em um argumento específico na linha de comando de compilação tem a preferência e pode potencialmente sobrescrever aquela no `makepkg.conf`.

O GCC pode detectar e habilitar automaticamente otimizações seguras específicas para cada arquitetura. Para usar esse recurso, primeiro remova os sinalizadores `-march` e `-mtune`, então adicione `-march = native`. Por exemplo:

 `/etc/makepkg.conf` 
```
CFLAGS="**-march=native** -O2 -pipe -fstack-protector-strong -fno-plt"
CXXFLAGS="${CFLAGS}"
```

Para ver quais sinalizadores isso habilita em sua máquina, execute:

```
$ gcc -march=native -v -Q --help=target

```

**Nota:** Se você especificar um valor diferente de `-march=native`, então `-Q --help=target` **não vai** funcionar como esperado.[[5]](https://bbs.archlinux.org/viewtopic.php?pid=1616694#p1616694) Você precisa passar por uma fase de compilação para descobrir quais opções estão realmente habilitadas. Veja [Encontre opções específicas da CPU](https://wiki.gentoo.org/wiki/Safe_CFLAGS#Find_CPU-specific_options) (inglês) no wiki do Gentoo para instruções.

### Melhorando os tempos de compilação

#### Compilação paralela

O sistema de compilação do [make](https://www.archlinux.org/packages/?name=make) usa a [variável de ambiente](/index.php/Vari%C3%A1vel_de_ambiente "Variável de ambiente") `MAKEFLAGS` para especificar opções adicionais para o *make*. A variável também pode ser definida no arquivo `makepkg.conf`.

Os usuários com sistemas multi-core/multiprocessados podem especificar o número de trabalhos a serem executados simultaneamente. Isso pode ser realizado com o uso de *nproc* para determinar o número de processadores disponíveis, ex. `MAKEFLAGS="-j$(nproc)"`. Alguns [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") substituem especificamente isso com `-j1`, devido a condições de corrida em certas versões ou simplesmente porque não é suportado em primeiro lugar. Os pacotes que não conseguem ser compilados devido a isso devem ser [relatados](/index.php/Diretrizes_de_relat%C3%B3rios_de_erro "Diretrizes de relatórios de erro") no rastreador de erros (ou no caso dos pacotes do [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)"), ao mantenedor do pacote) depois de ter certeza de que o erro está sendo realmente causado pelo seu `MAKEFLAGS`.

Veja [make(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/make.1) para uma lista completa de opções disponíveis.

#### Compilando de arquivos na memória

Como a compilação requer muitas operações de E/S e lidar com arquivos pequenos, mover o diretório de trabalhos para um [tmpfs](/index.php/Tmpfs "Tmpfs") pode trazer melhorias em tempos de compilação.

A variável `BUILDDIR` pode ser temporariamente exportada para *makepkg* para definir o diretório de compilação para um tmpfs existente. Por exemplo:

```
$ BUILDDIR=/tmp/makepkg makepkg

```

Uma configuração persistente pode ser feita no `makepkg.conf` descomentando a opção `BUILDDIR`, que é encontrada no fim da seção `BUILD ENVIRONMENT` no arquivo padrão `/etc/makepkg.conf`. Definir esses valores para, por exemplo, `BUILDDIR=/tmp/makepkg` fará uso do sistema de arquivos temporário `/tmp` padrão do Arch.

**Nota:** * Evite compilar pacotes grandes no tmpfs para evitar ficar sem memória.

*   A pasta tmpfs deve ser montada sem a opção `noexec`; do contrário, ela vai impedir que binparios sejam executados.
*   Tenha em mente que pacotes compilados no tmpfs não persistirá após reinicialização. Considere configurar a opção [PKGDEST](#Saída_de_pacote) apropriadamente para mover o pacote compilado automaticamente para um diretório persistente.

#### Usando cache de compilação

O uso de [ccache](/index.php/Ccache_(Portugu%C3%AAs) "Ccache (Português)") pode melhorar os tempos de compilação ao armazenar em cache os resultados de compilações para uso sucessivo.

### Gerar novos checksums

Instale [pacman-contrib](https://www.archlinux.org/packages/?name=pacman-contrib) e execute o seguinte comando no mesmo diretório que o arquivo PKGBUILD para gerar novas somas de verificação (*checksums*):

```
$ updpkgsums

```

As somas de verificação também podem ser obtidos com, por exemplo, `sha256sum` e adicionados ao vetor `sha256sums` manualmente.

### Usar outros algoritmos de compressão

Para acelerar o empacotamento e a instalação, com a consequência de ter arquivos de pacotes maiores, você pode alterar `PKGEXT`. Por exemplo, o seguinte torna o arquivo de pacote descompactado para apenas uma invocação:

```
$ PKGEXT='.pkg.tar' makepkg

```

Um outro exemplo abaixo mostra o uso do algoritmo lzop, com o pacote [lzop](https://www.archlinux.org/packages/?name=lzop) necessário:

```
$ PKGEXT='.pkg.tar.lzo' makepkg

```

Para fazer uma dessas configurações permanentes, configure `PKGEXT` em `/etc/makepkg.conf`.

### Usando vários núcleos na compressão

O [xz](https://www.archlinux.org/packages/?name=xz) oferece suporte a [multiprocessamento simétrico (SMP)](https://en.wikipedia.org/wiki/pt:Multiprocessamento_sim%C3%A9trico "wikipedia:pt:Multiprocessamento simétrico") por meio do sinalizador `--threads` para acelerar a compressão. Por exemplo, para deixar o makepkg usar quantos núcleos de CPU for possível para comprimir os pacotes, edite o vetor `COMPRESSXZ` em `/etc/makepkg.conf`:

```
COMPRESSXZ=(xz -c -z - **--threads=0**)

```

O [pigz](https://www.archlinux.org/packages/?name=pigz) é uma implementação paralela para o [gzip](https://www.archlinux.org/packages/?name=gzip) que, por padrão, usa todos os núcleos disponíveis na CPU (o sinalizador `-p/--processes` pode ser usado para empregar menos núcleos):

```
COMPRESSGZ=(**pigz** -c -f -n)

```

### Mostrar pacotes com um empacotador específico

Isso mostra todos os pacotes instalados no sistema com o empacotador chamado *nome-empacotador*:

```
$ expac "%n %p" | grep "*nome-empacotador*" | column -t

```

Isso mostra todos os pacotes instalados no sistema com o empacotador definido na variável `PACKAGER` do `/etc/makepkg`. Isso mostra apenas pacotes que estão em um repositório definido em `/etc/pacman.conf`.

```
$ . /etc/makepkg.conf; grep -xvFf <(pacman -Qqm) <(expac "%n\t%p" | grep "$PACKAGER$" | cut -f1)

```

### Compilar pacotes 32 bits em um sistema 64 bits

**Atenção:** Erros foram relatados ao usar esse método par compilar o pacote [linux](https://www.archlinux.org/packages/?name=linux).

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

### CFLAGS/CXXFLAGS/LDFLAGS no makepkg.conf não funcionam para pacotes baseados no CMAKE

Para fazer o CMake usar as variáveis definidas no `makepkg.conf`, Basta não especificar `-DCMAKE_BUILD_TYPE` ao configurar um projeto de cmake. [[6]](https://lists.archlinux.org/pipermail/arch-dev-public/2018-March/029181.html)

Isso fará com que o cmake use um tipo de compilação de `None` , o que usa as variáveis de ambiente como `CFLAGS`, `CPPFLAGS`, etc.

### CFLAGS/CXXFLAGS/LDFLAGS no makepkg.conf não funcionam para pacotes baseados no QMAKE

Qmake configura automaticamente a variável `CFLAGS`, `CXXFLAGS` e `LDFLAGS` de acordo com o que você pensa que deveria ser a configuração correta. Para deixar o qmake usar as variáveis definidas no arquivo de configuração do makepkg, você deve editar o PKGBUILD e passar as variáveis [QMAKE_CFLAGS](https://doc.qt.io/qt-5/qmake-variable-reference.html#qmake-cflags), [QMAKE_CXXFLAGS](https://doc.qt.io/qt-5/qmake-variable-reference.html#qmake-cxxflags) e [QMAKE_LFLAGS](https://doc.qt.io/qt-5/qmake-variable-reference.html#qmake-lflags) ao qmake. Por exemplo:

 `PKGBUILD` 
```
...

build() {
  cd "$srcdir/$_pkgname-$pkgver-src"
  qmake-qt5 "$srcdir/$_pkgname-$pkgver-src/$_pkgname.pro" \
    PREFIX=/usr \
    QMAKE_CFLAGS="${CFLAGS}" \
    QMAKE_CXXFLAGS="${CXXFLAGS}" \
    QMAKE_LFLAGS="${LDFLAGS}"

  make
}

...

```

Alternativamente, para uma configuração para todo sistema, você pode criar seu próprio `qmake.conf` e configurar a variável de ambiente [QMAKESPEC](https://doc.qt.io/qt-5/qmake-environment-reference.html#qmakespec).

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

### ERRO: Uma ou mais assinaturas PGP não puderam ser verificadas!; o que eu devo fazer?

É muito provável que você não tenha as chaves públicas necessárias no seu chaveiro pessoal para verificar os arquivos baixados. Se um ou mais arquivos .sig forem baixados durante a criação do pacote, o [makepkg verificará automaticamente o(s) arquivo(s) correspondente(s) com a chave pública de seu signatário](#Verificação_de_assinatura). Se você não tiver a chave necessária no seu chaveiro pessoal, o *makepkg* não fará a verificação.

A maneira recomendada para lidar com este problema é importar a chave pública requerida, ou [manualmente](/index.php/GnuPG#Import_a_public_key "GnuPG") ou [de um servidor de chaves](/index.php/GnuPG#Use_a_keyserver "GnuPG"). Geralmente, você pode simplesmente encontrar a impressão digital das chaves públicas necessárias na seção [validpgpkeys](/index.php/PKGBUILD_(Portugu%C3%AAs)#validpgpkeys "PKGBUILD (Português)") do [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)").

### Makepkg falha em baixar dependências quando por trás de um proxy

Quando o *makepkg* chama dependências, ele chama o pacman para instalar os pacotes, o que requer privilégios administrativos via *sudo*. No entanto, o *sudo* não passa nenhuma [variável de ambiente](/index.php/Vari%C3%A1vel_de_ambiente "Variável de ambiente") para o ambiente privilegiado, e inclui as variáveis relacionadas ao proxy `ftp_proxy`, `http_proxy`, `https_proxy` e `no_proxy`.

Para que ter o *makepkg* funcionando por trás de um proxy, você tem que fazer um dos seguintes métodos.

#### Habilitar proxy definindo sua URL no XferCommand

O XferCommand pode ser definido para usar a URL de proxy desejada no `/etc/pacman.conf`. Adicione ou descomente a linha a seguir em seu `pacman.conf`[[7]](http://www.mail-archive.com/arch-general@archlinux.org/msg15561.html):

 `/etc/pacman.conf` 
```
...
XferCommand = /usr/bin/curl -x http://usuário:senha@proxy.proxyhost.com:80 -L -C - -f -o %o %u
...

```

#### Habilitar proxy via env_keep do sudoers

Alternativamente, pode-se usar a opção `env_keep` do sudoers, a qual permite preservar as variáveis de ambiente dadas no ambiente privilegiado. Veja [Sudo#Environment variables](/index.php/Sudo#Environment_variables "Sudo") para mais informações.

### Makepkg falha, mas make obtém sucesso

Se algo compilar manualmente usando *make*, mas falhar através do *makepkg*, é quase certo que seja porque o `/etc/makepkg.conf` define uma variável de compilação para algo razoável que normalmente funcione, mas que seja incompatível com o que você esteja compilando. Tente adicionar esses sinalizadores ao array `options` do PKGBUILD:

`!buildflags`, para evitar seu `CPPFLAGS`, `CFLAGS`, `CXXFLAGS` e `LDFLAGS` padrão.

`!makeflags`, para evitar seu `MAKEFLAGS` padrão, caso você tenha editado `/etc/makepkg.conf` para habilitar compilações paralelas.

`!debug`, para evitar seu `DEBUG_CFLAGS` e `DEBUG_CXXFLAGS` padrão, no caso de seu pacote ser uma compilação de depuração.

Se qualquer um deles resolver o problema, isso pode indicar que você pode relatar um erro no envio de dados, se você isolar exatamente qual sinalizador está causando o problema.

## Veja também

*   [Página de manual makepkg(8)](https://www.archlinux.org/pacman/makepkg.8.html)
*   [Página de manual makepkg.conf(5)](https://www.archlinux.org/pacman/makepkg.conf.5.html)
*   [Um breve passeio no processo do makepkg](https://gist.github.com/Earnestly/bebad057f40a662b5cc3)
*   [Código fonte do makepkg](https://projects.archlinux.org/pacman.git/tree/scripts/makepkg.sh.in)