**Status de tradução:** Esse artigo é uma tradução de [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"). Data da última tradução: 2019-01-28\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=PKGBUILD&diff=0&oldid=564976) na versão em inglês.

Artigos relacionados

*   [Padrões de empacotamento do Arch](/index.php/Padr%C3%B5es_de_empacotamento_do_Arch "Padrões de empacotamento do Arch")
*   [Criando pacotes](/index.php/Criando_pacotes "Criando pacotes")
*   [.SRCINFO](/index.php/.SRCINFO_(Portugu%C3%AAs) ".SRCINFO (Português)")
*   [Arch User Repository](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)")
*   [Category:Package development (Português)](/index.php/Category:Package_development_(Portugu%C3%AAs) "Category:Package development (Português)")
*   [Arch Build System](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)")
*   [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)")

Esse artigo discute variáveis definíveis pelo mantenedor em um PKGBUILD. Para informações sobre funções do PKGBUILD e criação de pacotes em geral, veja [Criando pacotes](/index.php/Criando_pacotes "Criando pacotes"). Leia também [PKGBUILD(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/PKGBUILD.5).

Um PKGBUILD é um script shell contendo as informações de compilação necessárias por pacotes do [Arch Linux](/index.php/Arch_Linux_(Portugu%C3%AAs) "Arch Linux (Português)").

Pacotes no Arch Linux são compilados usando o utilitário [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)"). Quando *makepkg* é executado, ele pesquisa por um arquivo `PKGBUILD` no diretório atual e segue as instruções dele para compilar ou obter os arquivos para compilar um pacote (`*pkgname*.pkg.tar.xz`). O pacote resultante contém arquivos binários e instruções de instalação, prontos para serem instalados com [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)").

Variáveis obrigatórias são `pkgname`, `pkgver`, `pkgrel` e `arch`. `license` não é estritamente necessária para compilar um pacote, mas é recomendada para quaisquer PKGBUILDs compartilhados com outras pessoas, já que *makepkg* vai produzir um aviso se não estiver presente.

É uma prática comum definir as variáveis no PKGBUILD da mesma forma dadas aqui. Porém, isso não é obrigatório, desde que a sintaxe [Bash](/index.php/Bash "Bash") correta seja usada.

**Dica:** Use [namcap](/index.php/Namcap_(Portugu%C3%AAs) "Namcap (Português)") para verificar PKGBUILDs por erros comuns de empacotamento.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Nome do pacote](#Nome_do_pacote)
    *   [1.1 pkgbase](#pkgbase)
    *   [1.2 pkgname](#pkgname)
*   [2 Versão](#Versão)
    *   [2.1 pkgver](#pkgver)
    *   [2.2 pkgrel](#pkgrel)
    *   [2.3 epoch](#epoch)
*   [3 Genérica](#Genérica)
    *   [3.1 pkgdesc](#pkgdesc)
    *   [3.2 arch](#arch)
    *   [3.3 url](#url)
    *   [3.4 license](#license)
    *   [3.5 groups](#groups)
*   [4 Dependências](#Dependências)
    *   [4.1 depends](#depends)
    *   [4.2 optdepends](#optdepends)
    *   [4.3 makedepends](#makedepends)
    *   [4.4 checkdepends](#checkdepends)
*   [5 Relações do pacote](#Relações_do_pacote)
    *   [5.1 provides](#provides)
    *   [5.2 conflicts](#conflicts)
    *   [5.3 replaces](#replaces)
*   [6 Outros](#Outros)
    *   [6.1 backup](#backup)
    *   [6.2 options](#options)
    *   [6.3 install](#install)
    *   [6.4 changelog](#changelog)
*   [7 Fontes](#Fontes)
    *   [7.1 source](#source)
    *   [7.2 noextract](#noextract)
    *   [7.3 validpgpkeys](#validpgpkeys)
*   [8 Integridade](#Integridade)
    *   [8.1 md5sums](#md5sums)
    *   [8.2 sha1sums](#sha1sums)
    *   [8.3 sha256sums](#sha256sums)
    *   [8.4 sha224sums, sha384sums, sha512sums](#sha224sums,_sha384sums,_sha512sums)
*   [9 Veja também](#Veja_também)

## Nome do pacote

### pkgbase

Ao compilar pacotes comuns, esta variável não deve ser explicitamente declarada no PKGBUILD: seu valor é padronizado para o do [#pkgname](#pkgname).

Ao criar um [pacote dividido](https://jlk.fjfi.cvut.cz/arch/manpages/man/PKGBUILD.5#PACKAGE_SPLITTING) (*split package*, em inglês), essa variável pode ser usada para especificar explicitamente o nome a ser usado para se referir ao grupo de pacotes na saída de *makepkg* e na nomeação de tarballs somente de origem. O valor não é permitido para começar com um hífen. Se não for especificado, o valor será o padrão para o primeiro elemento no vetor `pkgname`.

Todas opções e diretivas para pacotes divididos têm como padrão os valores globais definidos no PKGBUILD. Mesmo assim, os seguintes podem ser sobrescritos dentro de cada função de empacotameto do pacote dividido: [#pkgdesc](#pkgdesc), [#arch](#arch), [#url](#url), [#license](#license), [#groups](#groups), [#depends](#depends), [#optdepends](#optdepends), [#provides](#provides), [#conflicts](#conflicts), [#replaces](#replaces), [#backup](#backup), [#options](#options), [#install](#install) e [#changelog](#changelog).

### pkgname

O nome do pacote (por exemplo, `pkgname='foo'`) ou, para pacotes divididos, um vetor de nomes (por exemplo, `pkgname=('foo' 'bar')`). Nomes não podem iniciar com hífenes. Por uma questão de consistência, `pkgname` deve corresponder ao nome do tarball fonte do software: por exemplo, se o software está em `foobar-2.5.tar.gz`, use `pkgname=foobar`. O nome do diretório contendo o PKGBUILD também deve corresponder ao `pkgname`.

## Versão

### pkgver

A versão do pacote. Ela deve ser a mesma que a versão publicada pelo autor do software *upstream*. Ela pode conter letras, números, pontos e sublinhados, mas **não** um hífen (`-`). Se o autor do software usa um hífen, substitua-o com um sublinhado (`_`). Se a variável `pkgver` é usada posteriormente no PKGBUILD, então o sublinhado pode ser facilmente substituído por um hífen, ex.: `source=("$pkgname-${pkgver//_/-}.tar.gz")`.

**Nota:** Se o *upstream* usa um versionamento com marca de tempo como `30102014`, certifique-se de usar a data reversa, i.e. `20141030` (formato [ISO 8601](https://en.wikipedia.org/wiki/pt:ISO_8601 "wikipedia:pt:ISO 8601")). Do contrário, ela não aparecerá como uma versão mais nova

**Dica:**

*   A ordem de valores incomuns pode ser testada com [vercmp](https://www.archlinux.org/pacman/vercmp.8.html), que é fornecido pelo pacote [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)").
*   [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") pode [atualizar](http://allanmcrae.com/2013/04/pacman-4-1-released/) automaticamente essa variável definindo uma função `pkgver()` no PKGBUILD. Veja [Diretrizes de pacotes VCS#A função pkgver()](/index.php/Diretrizes_de_pacotes_VCS#A_função_pkgver() "Diretrizes de pacotes VCS") para detalhes.

### pkgrel

O número de lançamento. Geralmente é um número inteiro positivo que permite diferenciar entre compilações consecutivas da mesma versão de um pacote. Na medida em que correções e funcionalidades adicionais são adicionadas ao PKGBUILD que influencie no pacote resultante, `pkgrel` deve ser incrementado em 1\. Quando uma nova versão do software é lançada, esse valor deve ser redefinido para 1\. Em casos excepcionais, outros formatos podem ser encontrados em uso, como em *maior.menor*.

### epoch

**Atenção:** `epoch` só deve ser usado quando absolutamente necessário.

Usado para forçar o pacote a ser visto como mais novo do que uma versão anterior com um *epoch* menor. Esse valor tem que ser um inteiro positivo; o padrão é 0\. É usado quando o esquema de numeração de versão de um pacote muda (ou é alfanumérico), quebrando a lógica de comparação de versão normal. Por exemplo:

```
pkgver=5.13
pkgrel=2
epoch=1
```
 `1:5.13-2` 

Veja [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8) para mais informações sobre comparações de versão.

## Genérica

### pkgdesc

A descrição do pacote. É recomendado no máximo 80 caracteres e não deve incluir o nome do pacote em uma forma autorreferenciativa, a menos que o nome do aplicativo seja diferente do nome do pacote. Por exemplo, use `pkgdesc="Text editor for X11"` em vez de `pkgdesc="Nedit is a text editor for X11"`.

Também é importante usar palavras-chaves com sabedoria para aumentar as chances de aparecer em consultas de pesquisas relevantes.

### arch

Um vetor de arquiteturas nas quais o PKGBUILD deve poder ser compilado e funcionar. Arch oferece suporte oficialmente apenas `x86_64`, mas outros projetos podem oferecer suporte a outras arquiteturas. Por exemplo, [Arch Linux 32](https://archlinux32.org/) fornece suporte a `i686` [Arch Linux ARM](http://archlinuxarm.org/) forence suporte a `arm` (armv5), `armv6h` (armv6 hardfloat), `armv7h` (armv7 hardfloat) e `aarch64` (armv8 64bit).

Há dois tipos de valores que o vetor pode usar:

*   `arch=('any')` é um valor mágico que, usado assim, indica que o pacote pode ser compilado em uma arquitetura e, após compilado, independe da arquitetura em seu estado compilado (shell scripts, fontes, ema, muitos tipos de extensões etc.).

*   `arch=('x86_64')` com uma ou mais arquiteturas indica que o pacote pode ser compilado para qualquer uma das arquiteturas especificadas, mas é específico da arquitetura depois de compilado. Para esses pacotes, especifique todas as arquiteturas as quais o PKGBUILD oficialmente possui suporte. Para repositórios oficiais e pacotes AUR, isso significa *x86_64*. Opcionalmente, os pacotes AUR podem optar por ter suporte adicional a outras arquiteturas que save-se funcionar.

A arquitetura alvo pode ser acessada com a variável `$CARCH` durante uma compilação.

### url

A URL do site oficial do software sendo empacotado.

### license

A licença sob a qual o software é distribuído. O pacote [licenses](https://www.archlinux.org/packages/?name=licenses) (parte do [grupo base](/index.php/Grupo_base "Grupo base")) contém muitas licenças comumente usadas, que são instaladas em `/usr/share/licenses/common`. Se um pacote é licenciado sob uma dessas licenças, o valor deve ser definido para o nome do diretório (ex.: `license=('GPL')`). Se a licença adequada não estiver incluída, diversas coisas devem ser feitas:

1.  Adicione `custom` ao vetor `license`. Opcionalmente, você pode substituir `custom` com `custom:*nome da licença*`. Uma vez que uma licença é usada em dois ou mais pacotes em um repositório oficial (incluindo [repositório community](/index.php/Reposit%C3%B3rio_community "Repositório community")), ela se torna parte do pacote [licenses](https://www.archlinux.org/packages/?name=licenses).
2.  Instale a licença em: `/usr/share/licenses/*pkgname*/` (ex.: `/usr/share/licenses/foobar/LICENSE`). Uma boa forma de fazer isso é usando: `install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"` 
3.  Se a licença é encontrada apenas em um site, então você precisa inclui-la separadamente no pacote.

*   As licenças [BSD](https://en.wikipedia.org/wiki/pt:Licen%C3%A7a_BSD "wikipedia:pt:Licença BSD"), [ISC](https://en.wikipedia.org/wiki/pt:Licen%C3%A7a_ISC "wikipedia:pt:Licença ISC"), [MIT](https://en.wikipedia.org/wiki/pt:Licen%C3%A7a_MIT "wikipedia:pt:Licença MIT"), [zlib/png](https://en.wikipedia.org/wiki/pt:Licen%C3%A7a_zlib "wikipedia:pt:Licença zlib") e [Python](https://en.wikipedia.org/wiki/pt:Python "wikipedia:pt:Python") são casos especiais e não podem ser incluídos no pacote [licenses](https://www.archlinux.org/packages/?name=licenses). Para manter a consistência no vetor `license`, é tratado como licença comum (`license=('BSD')`, `license=('ISC')`, `license=('MIT')`, `license=('ZLIB')` e `license=('Python')`), mas tecnicamente cada uma é uma licença personalizada, porque cada uma possui sua própria linha de copyright. Quaisquer pacotes licenciados sob essas quatro devem ter uma licença única armazenada em `/usr/share/licenses/*pkgname*`.
*   Alguns pacotes podem não estar cobertos por uma única licença. Nestes casos, múltiplas entradas podem ser feitas no vetor `license` como, por exemplo, `license=('GPL' "custom:*nome da licença*")`.
*   (L)GPL possui muitas verões e permutações daquelas versões. Para softwares sob (L)GPL, a convenção é:
    *   (L)GPL — (L)GPLv2 ou qualquer versão posterior
    *   (L)GPL2 — (L)GPL2 apenas
    *   (L)GPL3 — (L)GPL3 ou qualquer versão posterior
*   Se após pesquisar a questão nenhuma licença puder ser determinada, [PKGBUILD.proto](https://projects.archlinux.org/pacman.git/tree/proto/PKGBUILD.proto) sugere `unknown`. Porém, o *upstream* deve ser contatado sobre as condições sob as quais o software está (e não está) disponível.

**Dica:** Alguns autores de software não fornecem arquivo de licença separados e descrevem regras de distribuição em uma seção de `ReadMe.txt` comum. Essa informação pode ser extraída para um arquivo separado durante a `build()` com alguma coisa como `sed -n '/**This software**/,/ **thereof.**/p' ReadMe.txt > LICENSE`

Veja também [Diretrizes de pacotes de aplicativos não livres](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") (*nonfree*).

Informações e perspectivas adicionais sobre licenças de software aberto e livre podem ser encontradas nas seguintes páginas:

*   [Wikipedia:pt:Licença de software livre](https://en.wikipedia.org/wiki/pt:Licen%C3%A7a_de_software_livre "wikipedia:pt:Licença de software livre")
*   [Wikipedia:Comparison of free and open-source software licenses](https://en.wikipedia.org/wiki/Comparison_of_free_and_open-source_software_licenses "wikipedia:Comparison of free and open-source software licenses")
*   [A Legal Issues Primer for Open Source and Free Software Projects](https://www.softwarefreedom.org/resources/2008/foss-primer.html)
*   [Projeto GNU - Várias licenças e comentários sobre elas](https://www.gnu.org/licenses/license-list.html)
*   [Debian - License information](https://www.debian.org/legal/licenses/)
*   [Open Source Initiative - Licenses by Name](http://www.opensource.org/licenses/alphabetical)

### groups

O [grupo](/index.php/Grupo_de_pacotes "Grupo de pacotes") ao qual o pacote pertence. Por exemplo, ao instalar o pacote [kdebase](https://www.archlinux.org/groups/x86_64/kdebase/), ele instala todos os pacotes pertencentes àquele grupo.

## Dependências

**Nota:** Vetores extras específicos por arquitetura podem ser adicionados anexando um sublinhado e o nome da arquitetura. Por exemplo: `optdepends_x86_64=()`.

### depends

Um vetor de pacotes que devem ser instalados para o software compilar **e** executar. Dependências definidas dentro da função `package()` são necessárias apenas para executar o software.

Restrições de versões podem ser especificadas com operadores de comparação, como, por exemplo, `depends=('foobar>=1.8.0')`; se múltiplas restrições forem necessárias, a dependência pode ser repetida para cada uma, como, por exemplo, `depends=('foobar>=1.8.0' 'foobar<2.0.0')`.

Dependências que são fornecidas por outras dependências não precisam ser listadas. Por exemplo, se um pacote *foo* depende de tanto *bar* quanto *baz*, e o pacote *bar* depende de *baz* também, então *baz* não precisa ser incluído no vetor `depends` do *foo*.

Se o nome da dependência parece ser uma biblioteca, como, por exemplo, `depends=('libfoobar.so')`, makepkg vai tentar localizar um binário que depende da biblioteca no pacote compilado e anexar a versão necessária pelo binário. Anexar você mesmo a versão desabilita a detecção automática, como, por exemplo, `depends=('libfoobar.so=2')`.

### optdepends

Um vetor de pacotes que não são necessários pelo software para funcionar, mas fornecem funcionalidades adicionais. Isso pode implicar em nem todos os executáveis fornecidos por um pacote funcionarem sem a respectiva *optdepends*. [[1]](https://lists.archlinux.org/pipermail/arch-general/2014-December/038124.html) Se o software funciona em múltiplas dependências alternativas, todas elas podem ser listadas aqui, em vez de no vetor `depends`.

Uma descrição curta da funcionalidade extra de cada *optdepend* também deve ser anotado:

```
optdepends=('cups: printing support'
            'sane: scanners support'
            'libgphoto2: digital cameras support'
            'alsa-lib: sound support'
            'giflib: GIF images support'
            'libjpeg: JPEG images support'
            'libpng: PNG images support')

```

### makedepends

Um vetor de pacotes que são necessários **apenas** para compilar o software. A versão mínima de dependência pode ser especificada no mesmo formato que no vetor `depends`. Os pacotes no vetor `depends` são implicitamente necessários para compilar o pacote, então eles não devem ser duplicados aqui.

**Dica:** O comando a seguir pode ser usado para verificar se um pacote em particular está no grupo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) ou é obtido por um membro do grupo:
```
$ LC_ALL=C pacman -Si $(pactree -rl ''pacote'') 2>/dev/null | grep -q "^Groups *:.*base-devel"

```

**Nota:** Presume-se que o grupo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) já esteja instalado ao compilar com *makepkg*. Membros deste grupo **não devem** ser incluídos no vetor `makedepends`.

### checkdepends

Um vetor de pacotes dos quais o software depende para executar sua suíte de testes, mas que não são necessários em tempo de execução. Pacotes nesta lista seguem o mesmo formato que `depends`. Essas dependências são consideradas apenas quando a função [check()](/index.php/Criando_pacotes#check() "Criando pacotes") estiver presente e for ser executada pelo makepkg.

**Nota:** Presume-se que o grupo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) já esteja instalado ao compilar com *makepkg*. Membros deste grupo **não devem** ser incluídos no vetor `checkdepends`.

## Relações do pacote

**Nota:** Vetores extras específicos por arquitetura podem ser adicionados anexando um sublinhado e o nome da arquitetura. Por exemplo: `conflicts_x86_64=()`.

### provides

Um vetor de pacotes adicionais dos quais o software fornece as funcionalidades (ou um pacote virtual como o `cron` ou `sh`). Pacotes fornecendo o mesmo item podem ser instalados lado a lado, a menos que um deles use um vetor `conflicts`.

**Nota:** A versão que aquele pacote fornece deve ser mencionada (`pkgver` e potencialmente o `pkgrel`), no caso de pacotes referenciando software que exigem uma. Por exemplo, um pacote modificado do *qt* na versão 3.3.8, chamado *qt-foobar*, deve usar `provides=('qt=3.3.8')`; omitir o número de versão causaria as dependências a exigir uma versão específica do *qt* falharia. Não adicione `pkgname` ao vetor `provides`, pois isso é feito automaticamente.

### conflicts

Um vetor de pacotes que conflitam com, ou causa problemas com o pacote, se instalado. Todos esses pacotes e pacotes fornecendo este item precisarão ser removidos. As propriedades da versão dos pacotes conflitantes também podem ser especificados no mesmo formato que o vetor `depends`.

Isso significa que quando você escreve um pacote para o qual uma versão alternativa está disponível (esteja ela nos pacotes oficiais ou no [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)") e seu pacote conflita com aquela versão, você também precisa colocar as outras versões em seu vetor `conflicts`.

No entanto, há uma exceção a essa regra. Definir pacotes conflitantes em todas as direções nem sempre é aplicável, especialmente se todos esses pacotes forem mantidos por pessoas diferentes. De fato, ter que entrar em contato com todos os mantenedores de pacotes de pacotes em conflito com sua própria versão e pedir que eles incluam o nome do seu pacote em seu vetor `conflicts` é um processo complicado.

É por isso que, neste contexto, se seu pacote fornece `provides` um recurso e outro pacote fornece `provides` o mesmo recurso, você não precisa especificar aquele pacote conflitante em seu vetor `conflicts`. Vejamos um exemplo concreto:

*   [netbeans](https://www.archlinux.org/packages/?name=netbeans) fornece implicitamente `netbeans` como o `pkgname` em si
*   [netbeans-javase](https://aur.archlinux.org/packages/netbeans-javase/) fornece `netbeans` e conflita com `netbeans`
*   [netbeans-php](https://aur.archlinux.org/packages/netbeans-php/) fornece `netbeans` e conflita com `netbeans`, mas não precisa conflitar com [netbeans-javase](https://aur.archlinux.org/packages/netbeans-javase/) já que o pacman é suficientemente inteligente para descobrir que esses pacotes são incompatíveis, já que eles fornecem as mesmas funcionalidades e estão em conflito com isso.

	O mesmo se aplica no inverso: [netbeans-javase](https://aur.archlinux.org/packages/netbeans-javase/) também não precisa conflitar com [netbeans-php](https://aur.archlinux.org/packages/netbeans-php/), porque eles fornecem o mesmo pacote.

### replaces

Um vetor de pacotes obsoletos que são substituídos pelo pacote, como, por exemplo, [wireshark-gtk](https://www.archlinux.org/packages/?name=wireshark-gtk) usa `replaces=('wireshark')`. Ao sincronizar, o *pacman* vai imediatamente substituir um pacote instalado ao encontrar outro pelo `replaces` correspondente nos repositórios. Se estiver fornecendo uma versão alternativa de um pacote já existente ou enviando para o [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)"), use os vetores `conflicts` e `provides`, que são avaliados apenas ao instalar o pacote conflitante.

## Outros

### backup

Um array de arquivos que contêm alterações feitas pelo usuário e, portanto, devem ser preservados durante a atualização ou remoção de um pacote, destinado principalmente para arquivos em `/etc`.

Arquivos neste vetor devem usar caminhos **relativos** sem a barra inicial (`/`) (ex.: `etc/pacman.conf`, em vez de `/etc/pacman.conf`).

Ao atualizar, novas versões podem ser salvadas como `file.pacnew` para evitar sobrescrever um arquivo que já existe e foi previamente modificado pelo usuário. De forma similar, quando o pacote é removido, os arquivos modificados pelo usuário serão preservados como `file.pacsave` a menos que o pacote tenha sido removido com o comando `pacman -Rn`.

Veja também os [arquivos Pacnew e Pacsave](/index.php/Arquivos_Pacnew_e_Pacsave "Arquivos Pacnew e Pacsave").

### options

Esse vetor permite sobrescrever alguns dos comportamentos padrões do *makepkg*, definidos no `/etc/makepkg.conf`. Para definir uma opção, inclua o nome no vetor. Para inverter o comportamento, coloque um **`!`** na frente.

A lista completa das opções disponíveis podem ser localizadas em [PKGBUILD(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/PKGBUILD.5).

### install

O nome do script *.install* a ser incluído no pacote. Este deve ser o mesmo que `pkgname`. *pacman* possui a habilidade de armazenar e executar um script específico por pacote durante a instalação, remoção ou atualização de um pacote. O script contém as seguintes funções que são executadas em momentos diferentes:

*   `pre_install` — O script é executado logo antes dos arquivos serem extraídos. Um argumento é passado: nova versão do pacote.
*   `post_install` — O script é executado logo após os arquivos serem extraídos. Um argumento é passado: nova versão do pacote.
*   `pre_upgrade` — O script é executado logo antes dos arquivos serem extraídos. Dois argumentos são passados na seguinte ordem: nova versão do pacote, versão antiga do pacote.
*   `post_upgrade` — O script é executado logo após os arquivos serem extraídos. Dois argumentos são passados na seguinte ordem: nova versão do pacote, versão antiga do pacote.
*   `pre_remove` — O script é executado logo antes dos arquivos serem removidos. Um argumento é passado: versão antiga do pacote.
*   `post_remove` — O script é executado logo após os arquivos serem removidos. Um argumento é passado: versão antiga do pacote.

Cada função é executada em [chroot](/index.php/Chroot_(Portugu%C3%AAs) "Chroot (Português)") dentro do diretório de instalação do *pacman*. Veja [esse tópico](https://bbs.archlinux.org/viewtopic.php?pid=913891).

**Dica:**

*   Um protótipo de *.install* é fornecido em [/usr/share/pacman/proto.install](https://projects.archlinux.org/pacman.git/plain/proto/proto.install).
*   [Hooks do pacman](/index.php/Pacman_(Portugu%C3%AAs)#Hooks "Pacman (Português)") fornecem funcionalidade similar.

**Nota:** Não termine o script com `exit`. Isso evitaria as funções contidas de serem executadas.

### changelog

O nome do *changelog* do pacote. Para ver os registros de alterações de pacotes instalados (que tenha esse arquivo):

```
$ pacman -Qc *pkgname*

```

## Fontes

### source

Um vetor de arquivos necessários para compilar o pacote. Deve conter a localização do fonte do software, que na maioria dos casos é uma URL HTTP ou FTP completa. As variáveis anteriormente definidas `pkgname` e `pkgver` podem ser usadas efetivamente aqui como, por exemplo, `source=("https://exemplo.com/$pkgname-$pkgver.tar.gz")`.

Os arquivos também podem ser fornecidos no mesmo diretório onde o `PKGBUILD` está localizado, e seus nomes adicionados a este vetor. Antes do processo de compilação iniciar, todos os arquivos referenciados neste vetor serão baixados ou verificados pela existência, e o *makepkg* não dará continuidade, se algum deles estiver faltando.

Arquivos *.install* são reconhecidos automaticamente pelo *makepkg* e não devem ser incluídos no vetor de fontes. Arquivos no vetor de fontes com extensões *.sig*, *.sign* ou *.asc* são reconhecidos pelo *makepkg* como assinaturas PGP e serão usados automaticamente para verificar a integridade do arquivo fonte correspondente.

**Atenção:** Os nomes de arquivos de fontes baixados devem ser globalmente únicos porque o diretório [SRCDEST](/index.php/Makepkg_(Portugu%C3%AAs)#Saída_de_pacote "Makepkg (Português)") pode ser o mesmo para todos pacotes. Por exemplo, usar o número de versão do projeto como um nome de arquivo potencialmente conflita com outros projetos com o mesmo número de versão. Neste caso, o nome de arquivo único alternativo a ser usado é fornecido com a sintaxe `source=('*nome_pacote_único*::*uri-arquivo*')` - por exemplo, `source=("$pkgname-$pkgver.tar.gz::https://github.com/codificador/programa/archive/v$pkgver.tar.gz")`.

**Dica:**

*   Vetores extras específicos por arquitetura podem ser adicionados anexando um sublinhado e o nome da arquitetura, ex.: `x86_64=()`. Deve haver um vetor de integridade correspondente com somas de verificação (*checksums*), ex.: `sha256sums_x86_64=()`.
*   Alguns servidores restringem download filtrando a string "User-Agent" do cliente, a qual pode ser alterada com [DLAGENTS](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres#DLAGENTS_personalizados "Diretrizes de pacotes de aplicativos não livres").

### noextract

Um vetor de arquivos listados sob `source` que não devem ser extraídos de seu formato empacotado pelo *makepkg*. Isso pode ser usado com pacotes que não podem ser tratados pelo `/usr/bin/bsdtar` ou aqueles que precisam ser instalado como estão. Se uma ferramenta alternativa de extração for usada (e.g. [lrzip](https://www.archlinux.org/packages/?name=lrzip)), ela deve ser adicionada no vetor `makedepends` e a primeira linha da função [prepare()](/index.php/Criando_pacotes#prepare() "Criando pacotes") deve extrair manualmente o pacote fonte; por exemplo:

```
prepare() {
  lrzip -d *source*.tar.lrz
}

```

Note que enquanto o vetor `source` aceita URLs, `noextract` é **apenas** a porção de nome do arquivo:

```
source=("http://foo.org/bar/foobar.tar.xz")
noextract=('foobar.tar.xz')

```

Para extrair *nada*, você pode fazer alguma coisa como:

*   Se `source` contém apenas URLs planas sem nomes de arquivos personalizados, remova do vetor de fontes antes da última barra:

	 `noextract=("${source[@]##*/}")` 

*   Se `source` contiver apenas entradas com nomes de arquivos personalizados, remova o vetor de entrada após o separador `::` (retirado do [PKGBUILD do firefox-i18n](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/PKGBUILD?h=packages/firefox-i18n#n123)):

	 `noextract=("${source[@]%%::*}")` 

### validpgpkeys

Um vetor de impressões digitais PGP. Se usado, *makepkg* só aceitará assinaturas das chaves listadas aqui e vai ignorar os valores de confiança do chaveiro. Se o arquivo fonte foi assinado com uma subchave, *makepkg* ainda vai usar a chave primária para comparação.

Apenas impressões digitais completas são aceitas. Elas devem estar em caixa alta e não devem conter caracteres em branco.

**Nota:** Você pode usar `gpg --list-keys --fingerprint <ID-CHAVE>` para localizar a impressão digital da chave apropriada.

Por favor, leia [makepkg (Português)#Verificação de assinatura](/index.php/Makepkg_(Portugu%C3%AAs)#Verificação_de_assinatura "Makepkg (Português)") para mais informações.

## Integridade

Essas variáveis são vetores cujos itens são strings de *checksums* (soma de verificação) que serão usadas para verificar a integridade dos respectivos arquivos no vetor [source](#source). Você também pode inserir `SKIP` para um arquivo em particular e seu *checksum* não será testado.

O tipo e os valores da soma de verificação *(checksum)* devem ser sempre aqueles fornecidos pelo upstream, como nos anúncios de lançamento. Quando vários tipos estão disponíveis, a soma de verificação mais forte deve ser preferida: `sha256` em `sha1` e `sha1` em `md5`. Isso garante a integridade dos arquivos baixados, desde o anúncio do upstream até o desenvolvimento de pacotes.

**Nota:** Além disso, quando o upstream disponibiliza [assinaturas digitais](https://en.wikipedia.org/wiki/pt:Assinatura_digital "w:pt:Assinatura digital"), os arquivos de assinatura devem ser adicionados ao vetor [source](#source) e a impressão digital da chave PGP ao vetor [validpgpkeys](#validpgpkeys). Isso permite a autenticação dos arquivos no momento de compilação.

Os valores para essas variáveis podem ser geradas automaticamente pela opção `-g`/`--geninteg` do [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") e, então, anexado com `makepkg -g >> PKGBUILD`. O comando `updpkgsums` do [pacman-contrib](https://www.archlinux.org/packages/?name=pacman-contrib) é capaz de atualizar as variáveis onde quer que elas estejam no PKGBUILD. Ambas ferramentas usarão a variável que já está definida no PKGBUILD, ou voltarão para `md5sums` se nada estiver definido.

As verificações de integridade de arquivo a serem usadas podem ser configuradas com a opção `INTEGRITY_CHECK` no `/etc/makepkg.conf`. Veja [makepkg.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/makepkg.conf.5).

**Nota:** Vetores adicionais específicos da arquitetura podem ser adicionadas anexando um sublinhado e o nome da arquitetura, p. ex. `sha256sums_x86_64=()`.

### md5sums

Um vetor de *checksums* de [MD5](https://en.wikipedia.org/wiki/pt:MD5 "wikipedia:pt:MD5") de 128 bits dos arquivos listados no vetor `source`.

### sha1sums

Um vetor de *checksums* de [SHA-1](https://en.wikipedia.org/wiki/pt:SHA-1 "wikipedia:pt:SHA-1") de 160 bits dos arquivos listados no vetor `source`.

### sha256sums

Um vetor de *checksums* de [SHA-2](https://en.wikipedia.org/wiki/pt:SHA-2 "wikipedia:pt:SHA-2") com tamanho de *digest* de 256 bits.

### sha224sums, sha384sums, sha512sums

Um vetor de *checksums* de SHA-2 com tamanhos de *digest* 224, 384 e 512 bits, respectivamente. Essas são alternativas mais comuns a `sha256sums`.

## Veja também

*   [PKGBUILD(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/PKGBUILD.5) - página de manual do PKGBUILD
*   [Exemplo de arquivo PKGBUILD](https://projects.archlinux.org/pacman.git/plain/proto/PKGBUILD.proto)