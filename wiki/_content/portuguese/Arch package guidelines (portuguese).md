**Status de tradução:** Esse artigo é uma tradução de [Arch package guidelines](/index.php/Arch_package_guidelines "Arch package guidelines"). Data da última tradução: 2019-11-24\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Arch_package_guidelines&diff=0&oldid=589951) na versão em inglês.

Artigos relacionados

*   [Criando pacotes](/index.php/Criando_pacotes "Criando pacotes")
*   [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)")
*   [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)")
*   [Arch Build System](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)")
*   [Arch User Repository](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)")
*   [Diretrizes de segurança para pacotes](/index.php/Diretrizes_de_seguran%C3%A7a_para_pacotes "Diretrizes de segurança para pacotes")

Ao compilar pacotes para o Arch Linux, **siga as diretrizes de empacotamento** abaixo, especialmente se a intenção é **contribuir** com um novo pacote para o Arch Linux. Você também deve ler as páginas de manual do [PKGBUILD(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/PKGBUILD.5) e do [makepkg(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/makepkg.8).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Protótipo de PKGBUILD](#Protótipo_de_PKGBUILD)
*   [2 Etiqueta de pacotes](#Etiqueta_de_pacotes)
*   [3 Nomenclatura de pacotes](#Nomenclatura_de_pacotes)
*   [4 Versionamento de pacotes](#Versionamento_de_pacotes)
*   [5 Dependências de pacotes](#Dependências_de_pacotes)
*   [6 Relações de pacotes](#Relações_de_pacotes)
*   [7 Fontes de pacotes](#Fontes_de_pacotes)
*   [8 Trabalhando com upstream](#Trabalhando_com_upstream)
*   [9 Diretórios](#Diretórios)
*   [10 Tarefas do Makepkg](#Tarefas_do_Makepkg)
*   [11 Arquiteturas](#Arquiteturas)
*   [12 Licenças](#Licenças)
*   [13 Diretrizes adicionais](#Diretrizes_adicionais)

## Protótipo de PKGBUILD

```
# Maintainer: Seu nome <seu-email@domínio.com>
pkgname=NOME
pkgver=VERSÃO
pkgrel=1
pkgdesc=""
arch=()
url=""
license=('GPL')
groups=()
depends=()
makedepends=()
optdepends=()
provides=()
conflicts=()
replaces=()
backup=()
options=()
install=
changelog=
source=($pkgname-$pkgver.tar.gz)
noextract=()
md5sums=() #gerado com updpkgsums

build() {
  cd "$pkgname-$pkgver"

  ./configure --prefix=/usr
  make
}

package() {
  cd "$pkgname-$pkgver"

  make DESTDIR="$pkgdir/" install
}
```

Outros protótipos podem ser encontrados em `/usr/share/pacman/` dos pacotes pacman e abs.

## Etiqueta de pacotes

*   Os pacotes **jamais** devem ser instalados em `/usr/local/`
*   **Não introduza novas variáveis ou funções** em scripts de compilação `PKGBUILD`, a menos que o pacote não possa ser compilado sem elas, pois elas podem **conflitar** com variáveis ou funções usadas pelo próprio makepkg.
*   Se uma nova variável ou uma nova função for absolutamente necessária, **prefixe seu nome com um caractere de sublinhado** (`_`), ex: `_variavelpersonalizada=` 
*   O campo `packager` do meta-arquivo do pacote pode ser **personalizado** pelo compilador do pacote, modificando a opção apropriada no arquivo `/etc/makepkg.conf` ou, alternativamente, sobrescrevendo-o com a criação de um ~/.makepkg.conf
*   Todas as mensagens importantes devem ser exibidas durante a instalação usando um **arquivo .install**. Por exemplo, se um pacote precisa de configurações extras para funcionar, as direções devem ser incluídas neste arquivo.
*   **Dependências** são os erros mais comuns de empacotamento. Por favor, invista um tempo em verificá-las cuidadosamente, por exemplo executando `ldd` em executáveis dinâmicos, verificando ferramentas necessárias por scripts ou olhando documentação do software. O utilitário [namcap](/index.php/Namcap_(Portugu%C3%AAs) "Namcap (Português)") pode lhe ajudar neste assunto. Essa ferramenta pode analisar ambos PKGBUILD e o tarball de pacote resultante e vai avisar você sobre permissões erradas, dependências em falta, dependências redundantes e outros erros comuns.
*   Quaisquer **dependências opcionais** que não são necessárias para executar o pacote ou que faça-o funcionar, não devem ser incluídas no vetor **depends**; em vez disso, a informação deve ser adicionada ao vetor **optdepends**:

```
optdepends=('cups: printing support'
            'sane: scanners support'
            'libgphoto2: digital cameras support'
            'alsa-lib: sound support'
            'giflib: GIF images support'
            'libjpeg: JPEG images support'
            'libpng: PNG images support')

```

	O exemplo acima foi tirado do pacote **wine** do `extra`. A informação do optdepends é automaticamente exibida na instalação/atualização, de forma que tal informação **não** deve-se manter esse tipo de informação em arquivos `.install`.

*   Ao criar a **descrição de pacote** para um pacote, não inclua o nome do pacote, em uma forma autorreferenciativa. Por exemplo, "Nedit is a text editor for X11" poderia ser simplificado em "A text editor for X11". Também tente manter as descrições abaixo de 80 caracteres.
*   Tente manter o **tamanho da linha** do PKGBUILD abaixo de 100 caracteres.
*   Onde for possível, **remova linhas vazias** do `PKGBUILD` (`provides`, `replaces`, etc.)
*   É uma prática comum **preservar a ordem** dos campos do `PKGBUILD` informada acima. Porém, isso não é obrigatório, sendo o único requisito neste contexto a **correção da sintaxe bash**.
*   **Envolva com aspas** as variáveis que podem conter espaços, tal como `"$pkgdir"` e `"$srcdir"`.
*   Para garantir a **integridade** de pacotes, certifique-se que as [variáveis de integridade](/index.php/PKGBUILD_(Portugu%C3%AAs)#Integridade "PKGBUILD (Português)") contêm os valores corretos. Essas podem ser atualizadas usando a ferramenta `updpkgsums`.

## Nomenclatura de pacotes

*   Nomes de pacotes pode conter apenas caracteres alfanuméricos e algum entre `@`, `.`, `_`, `+`, `-`. Nomes não podem iniciar com hífenes ou pontos. Todas as letras devem ser **minúsculas**.
*   Nomes de pacotes NÃO devem ser sufixados com o número de versão principal de lançamento do upstream (ex.: não queremos libfoo2 se upstream chama-o de libfoo v2.3.4) no caso da biblioteca e suas dependências esperadas para serem capazes de manter o uso da maioria das versões recentes de biblioteca com cada lançamento do upstream. Porém, para alguns softwares ou dependências, isso não pode ser presumido. No passado, isso foi especialmente verdadeiro para kits de ferramentas de widget, tal como GTK ou Qt. Softwares que depende em tais kits de ferramentas geralmente podem não ser trivialmente portadas para uma nova versão maior. Como tal, em casos em que softwares podem, trivialmente, se manter funcionando junto com suas dependências, nomes de pacotes devem carregar o sufixo da versão maior (ex.: gtk2, gtk3, qt4, qt5). Para casos em que a maioria das dependências podem se manter funcionando junto com lançamentos mais novos, mas alguns não podem (por exemplo, código fechado que precisa de libpng12 ou similar), uma versão obsoleta daquele pacote pode ser chamado de libfoo1 enquanto a versão atual é apenas libfoo.

## Versionamento de pacotes

*   Versões de pacotes (p.ex., [PKGBUILD (Português)#pkgver](/index.php/PKGBUILD_(Portugu%C3%AAs)#pkgver "PKGBUILD (Português)")) **devem ser as mesmas que a versão lançada pelo autor**. Versões podem incluir letras, se for necessário (ex: a versão do nmap é 2.54BETA32). **Tags de versão não podem incluir hífens!** Letras, números e pontos, somente.
*   **Pacotes estáveis empacotam lançamentos estáveis**: Candidatos a lançamento (p.ex., `1.0.0-rc1`), alfa (p.ex., `1.0.0-alpha1`) e beta (p.ex., `1.0.0-beta1`) não são permitidos e são apenas para ser usado sob as seguintes circunstâncias:
    *   O lançamentos não estável contém correções de segurança **urgentes** (e *backporting* não é trivial).
    *   O lançamento não estável permite que o pacote seja compilado (p.ex., problemas introduzidos por causa de dependências atualizadas) e essas alterações não poderiam, do contrário, ser backportado facilmente.
    *   O lançamento não estável permite a distribuição descartar um componente EOL (p.ex., qt4, python2).
*   Lançamentos de pacotes (p.ex., [PKGBUILD (Português)#pkgrel](/index.php/PKGBUILD_(Portugu%C3%AAs)#pkgrel "PKGBUILD (Português)")) são **específicos de pacotes do Arch Linux**. Eles permitem a usuários diferenciar entre compilações de pacotes mais novas das mais antigas. Quando uma nova versão de software do pacote é lançada, o **contador de lançamento recomeça em 1**. Então, na medida em que correções e otimizações forem feitas, o pacote será **relançado** para o público do Arch Linux e o **número de lançamento será incrementado**. Quando uma nova versão for lançada, o contador de lançamento será reiniciado para 1\. As tags de lançamento do pacote seguem as **mesmas restrições de nomenclatura que tags de versão**.

## Dependências de pacotes

*   **Não confie em [dependências transitivas](https://en.wikipedia.org/wiki/Transitive_dependency "wikipedia:Transitive dependency")** em qualquer uma das [PKGBUILD (Português)#Dependencias](/index.php/PKGBUILD_(Portugu%C3%AAs)#Dependencias "PKGBUILD (Português)"), pois elas podem quebrar, se uma das dependências for atualizada.
*   Liste todas as dependências diretas da biblioteca. Para identificá-las, [find-libdeps(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/find-libdeps.1) (parte de [devtools](https://www.archlinux.org/packages/?name=devtools)) pode ser usado.

## Relações de pacotes

*   Não adicione `$pkgname` a [PKGBUILD (Português)#provides](/index.php/PKGBUILD_(Portugu%C3%AAs)#provides "PKGBUILD (Português)"), pois ele é sempre fornecido implicitamente pelo pacote.
*   Liste todas as bibliotecas compartilhadas externas de um pacote em [PKGBUILD (Português)#provides](/index.php/PKGBUILD_(Portugu%C3%AAs)#provides "PKGBUILD (Português)") (por exemplo, `'libalgumacoisa.so'`). Para identificá-los, [find-libprovides(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/find-libprovides.1) (parte de [devtools](https://www.archlinux.org/packages/?name=devtools)) pode ser usado.

## Fontes de pacotes

*   Os fontes HTTPS (`https://` para tarballs, `git+https://` para fontes git) devem ser usados sempre que possível
*   Os fontes devem ser verificados usando assinaturas PGP sempre que possível (isso pode envolver a criação de uma tag git em vez de um tarball de origem, se os sinais upstream confirmarem e marcarem, mas não os tarballs)
*   **Não diminua a segurança ou a validade de um pacote** (por exemplo, removendo uma verificação de soma de verificação ou removendo a verificação de assinatura PGP) porque uma versão anterior foi interrompida ou de repente carece de um determinado recurso (por exemplo, falta de assinatura PGP para um novo lançamento)
*   Os fontes precisam ser exclusivos em `srcdir` (isso pode exigir que você os renomeie durante o download, por exemplo, `"${pkgname}-${pkgver}.tar.gz::https://${pkgname}.tld/download/${pkgver}.tar.gz"`)
*   Evite usar espelhos específicos (por exemplo, no sourceforge) para fazer o download, pois eles podem ficar indisponíveis

## Trabalhando com upstream

É uma boa prática trabalhar em estreita colaboração com a upstream, sempre que possível. Isso implica relatar problemas sobre a compilação e o teste de um pacote.

*   Relate problemas imediatamente ao upstream.
*   Patches do upstream sempre que possível.
*   Adicione comentários com links para relatórios de erros relevantes (do upstream) no [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") (isso é particularmente importante, pois garante, que outros empacotadores possam entender as alterações e também trabalhar com um pacote).

## Diretórios

*   **Arquivos de configuração** devem ser mantidos dentro do diretório `/etc`. Se há mais de um arquivo de configuração, é costumeiro **usar um subdiretório** para manter a área do `/etc` o mais limpo possível. Use `/etc/{pkgname}/`, sendo `{pkgname}` o nome do pacote (ou uma alternativa adequada, p.ex., o apache usa `/etc/httpd/`).
*   Arquivos de pacotes devem seguir essas **diretrizes gerais de diretórios**:

| `/etc` | Arquivos de configuração **essenciais para o sistema** |
| `/usr/bin` | Binários |
| `/usr/lib` | Bibliotecas |
| `/usr/include` | Arquivos cabeçalhos (*headers*) |
| `/usr/lib/{pkg}` | Módulos, plug-ins, etc. |
| `/usr/share/doc/{pkg}` | Documentação de aplicativo |
| `/usr/share/info` | Arquivos de sistema do GNU Info |
| `/usr/share/man` | Páginas de manual (*man*) |
| `/usr/share/{pkg}` | Dados de aplicativo |
| `/var/lib/{pkg}` | Armazenamento persistente de aplicativo |
| `/etc/{pkg}` | Arquivos de configuração de `{pkg}` |
| `/opt/{pkg}` | Pacotes grandes contendo todos os seus arquivos |

*   Pacotes não devem conter os diretórios abaixo:
    *   `/bin`
    *   `/sbin`
    *   `/dev`
    *   `/home`
    *   `/srv`
    *   `/media`
    *   `/mnt`
    *   `/proc`
    *   `/root`
    *   `/selinux`
    *   `/sys`
    *   `/tmp`
    *   `/var/tmp`
    *   `/run`

## Tarefas do Makepkg

Quando [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") é usado para compilar um pacote, ele automaticamente faz o seguinte:

1.  Verifica se as dependências (**depends**) e dependências em tempo de compilação (**makedepends**) do pacote estão instaladas
2.  **Baixa os arquivos fontes** dos servidores
3.  **Verifica a integridade** de arquivos fonte
4.  **Descompacta** os arquivos fonte
5.  Realiza qualquer **patching** necessário
6.  **Compila** o software e instala-o em um *fakeroot*
7.  Remove (**strips**) símbolos de binários
8.  Remove (**strips**) símbolos de depuração de bibliotecas
9.  **Compacta** páginas de manual e/ou info
10.  Gera o **meta-arquivo de pacote**, o qual é incluído em cada pacote
11.  **Compacta** o *fakeroot* no arquivo de pacote
12.  **Armazena** o arquivo de pacote no diretório de destino configurado (por padrão, cwd)

## Arquiteturas

O vetor `arch` deve conter `'x86_64'` se o pacote compilado é específico para a arquitetura. Do contrário, use `'any'` para pacotes que independem de arquitetura.

## Licenças

Veja [PKGBUILD#license](/index.php/PKGBUILD_(Portugu%C3%AAs)#license "PKGBUILD (Português)").

## Diretrizes adicionais

Certifique-se de ler primeiro as diretrizes acima - pontos importantes são listados nesta página e que não serão repetidos nas páginas de diretrizes a seguir. As diretrizes específicas abaixo têm a intenção de ser um adicionar aos padrões listados nesta.

**[Diretrizes de criação de pacotes](/index.php/Padr%C3%B5es_de_empacotamento_do_Arch "Padrões de empacotamento do Arch")**

* * *

[32-bit](/index.php/Diretrizes_de_pacotes_32-bit "Diretrizes de pacotes 32-bit") – [CLR](/index.php/Diretrizes_de_pacotes_CLR "Diretrizes de pacotes CLR") – [Cross](/index.php/Diretrizes_de_pacotes_de_ferramentas_de_compila%C3%A7%C3%A3o_cruzada "Diretrizes de pacotes de ferramentas de compilação cruzada") – [Eclipse](/index.php/Diretrizes_de_pacotes_de_plugin_do_Eclipse "Diretrizes de pacotes de plugin do Eclipse") – [Electron](/index.php/Diretrizes_de_pacotes_Electron "Diretrizes de pacotes Electron") – [Free Pascal](/index.php/Diretrizes_de_pacotes_Free_Pascal "Diretrizes de pacotes Free Pascal") – [GNOME](/index.php/Diretrizes_de_pacotes_GNOME "Diretrizes de pacotes GNOME") – [Go](/index.php/Diretrizes_de_pacotes_Go "Diretrizes de pacotes Go") – [Haskell](/index.php/Diretrizes_de_pacotes_Haskell "Diretrizes de pacotes Haskell") – [Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java") – [KDE](/index.php/Diretrizes_de_pacotes_KDE "Diretrizes de pacotes KDE") – [Kernel](/index.php/Diretrizes_de_pacotes_de_m%C3%B3dulos_de_kernel "Diretrizes de pacotes de módulos de kernel") – [Lisp](/index.php/Diretrizes_de_pacotes_Lisp "Diretrizes de pacotes Lisp") – [MinGW](/index.php/Diretrizes_de_pacotes_MinGW "Diretrizes de pacotes MinGW") – [Node.js](/index.php/Diretrizes_de_pacotes_Node.js "Diretrizes de pacotes Node.js") – [Nonfree](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") – [OCaml](/index.php/Diretrizes_de_pacotes_OCaml "Diretrizes de pacotes OCaml") – [Perl](/index.php/Diretrizes_de_pacotes_Perl "Diretrizes de pacotes Perl") – [PHP](/index.php/Diretrizes_de_pacotes_PHP "Diretrizes de pacotes PHP") – [Python](/index.php/Diretrizes_de_pacotes_Python "Diretrizes de pacotes Python") – [R](/index.php/Diretrizes_de_pacotes_R "Diretrizes de pacotes R") – [Ruby](/index.php/Diretrizes_de_pacotes_Ruby_Gem "Diretrizes de pacotes Ruby Gem") – [Rust](/index.php/Diretrizes_de_pacotes_Rust "Diretrizes de pacotes Rust") – [VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") – [Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web") – [Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine")

Pacotes enviados ao AUR também devem estar em conformidade com as [diretrizes de envio ao AUR](/index.php/Diretrizes_de_envio_ao_AUR "Diretrizes de envio ao AUR").