**Status de tradução:** Esse artigo é uma tradução de [Patching packages](/index.php/Patching_packages "Patching packages"). Data da última tradução: 2019-04-13\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Patching_packages&diff=0&oldid=571094) na versão em inglês.

Artigos relacionados

*   [ABS](/index.php/ABS_(Portugu%C3%AAs) "ABS (Português)")

Esse artigo cobre como criar e como aplicar *patches* (correções, remendos) em pacotes no [Arch Build System (Português)](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)") (ABS).

Um [patch](https://en.wikipedia.org/wiki/Patch_(computa%C3%A7%C3%A3o) descreve um conjunto de alterações a linha para um ou mais arquivos. Patches são geralmente usados para automatizar as alterações ao código-fonte.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Criando patches](#Criando_patches)
*   [2 Aplicando patches](#Aplicando_patches)
*   [3 Usando quilt](#Usando_quilt)
*   [4 Veja também](#Veja_também)

## Criando patches

**Nota:** Se você precisar alterar apenas uma ou duas linhas, convém usar o [sed](/index.php/Sed "Sed").

A ferramenta *diff* compara arquivos linha por linha. Se você salvar sua saída, você terá um patch, por exemplo `diff --unified --recursive --text foo bar > patch`. Se você informar diretórios, *diff* vai comparar os arquivos que eles contêm.

1.  Exclua o diretório `src` se você já tiver construído o pacote.
2.  Execute `makepkg --nobuild`, o qual baixará e extrairá os arquivos fonte, especificados em `PKGBUILD`, mas não os compilará.
3.  Crie duas cópias do diretório extraído no diretório `src`, uma como uma cópia original e outra para sua versão alterada. Nós os chamaremos de `pacote.orig` e `pacote.new`.
4.  Faça suas alterações no diretório `pacote.new`.
5.  Execute `diff --unified --recursive --text pacote.orig pacote.new --color` e verifique se o patch está correto.
6.  Execute `diff --unified --recursive --text pacote.orig pacote.new > pacote.patch` para criar o patch.
7.  Entre no diretório `pacote.orig` e aplique o patch usando `patch --strip=1 < ../pacote.patch`. Verifique se o patch está funcionando na compilação e instalação do pacote modificado com `makepkg --noextract --install`.

**Nota:** Você também pode criar patches com [Git](/index.php/Git "Git") usando `git diff` ou `git format-patch` [[1]](https://stackoverflow.com/questions/6658313/generate-a-git-patch-for-a-specific-commit).

Veja [diff(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/diff.1) e [git-diff(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-diff.1) para mais informações.

## Aplicando patches

Esta seção descreve como aplicar patches criados ou baixados da Internet a partir da função `PKGBUILD` `prepare()`. Siga esses passos:

1.  Adicione uma entrada ao array `source` do `PKGBUILD` para o arquivo de patch, separado do URL fonte original por um espaço. Se o arquivo estiver disponível online, você pode fornecer a URL completa e ela será automaticamente baixada e colocada no diretório `src`. Se for um patch criado por você mesmo ou não estiver disponível, você deverá colocar o arquivo de patch no mesmo diretório que o arquivo `PKGBUILD` e apenas adicionar o nome do arquivo ao array de fontes para que ele é copiado para o diretório `src`. Se você redistribuir o `PKGBUILD`, você deve, claro, incluir o patch com o `PKGBUILD`.
2.  Então, use *updpkgsums* (do [pacman-contrib](https://www.archlinux.org/packages/?name=pacman-contrib)) para atualizar o array `md5sums`. Ou adicione manualmente uma entrada à matriz `md5sums`; você pode gerar a soma do seu patch usando a ferramenta *md5sum*.
3.  Crie a função `prepare()` no `PKGBUILD` se ainda não houver uma.
4.  O primeiro passo é mudar para o diretório que precisa ser corrigido (na função `prepare()`, não no seu terminal! Você quer automatizar o processo de aplicação do patch). Você pode fazer isso com algo como `cd "$srcdir/$pkgname-$pkgver"` ou algo semelhante. O `$pkgname-$pkgver` é geralmente o nome de um diretório criado pela descompactação de um arquivo de origem baixado, mas não em todos os casos.
5.  Agora você só precisa aplicar o patch dentro desse diretório. Isto é feito simplesmente adicionando `patch --strip=1 --input=*pkgname*.patch` à sua função `prepare()`, alterando `*pkgname*.patch` para o nome do arquivo que contém o diff (o arquivo que foi copiado automaticamente em seu diretório `src` porque estava no array `source` do arquivo `PKGBUILD`).

Um exemplo de função "prepare":

```
prepare() {
    cd $pkgname-$pkgver
    patch --forward --strip=1 --input="${srcdir}/eject.patch"
}
```

Execute `makepkg` (a partir do terminal agora). Se tudo correr bem, o patch será aplicado automaticamente e o novo pacote conterá as alterações incluídas no patch. Se não, você pode ter que tentar com a opção `--strip` do patch. Enquanto estiver tentado, você pode achar as opções `--dry-run`, `--reverse` ou `--verbose` utilizáveis. Leia [patch(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/patch.1) para mais informações.

Basicamente, funciona da seguinte forma. Se o arquivo diff foi criado para aplicar patches a arquivos em `minhaversão/`, os arquivos diff serão aplicados a `minhaversão/arquivo`. Você está executando-o de dentro do diretório `suaversão/` (porque você mudar o diretório para dentro daquele diretório no `PKGBUILD`), então quando o patch é aplicado ao arquivo, você vai querer aplicá-lo ao arquivo `arquivo`, retirando a parte `minhaversão/`. `--strip=1` faz isso, removendo um diretório do caminho. Porém, se o desenvolvedor aplicou patch em `meusarquivos/minhaversão`, você precisa remover dois diretórios, usando `--strip=2`.

Se você não aplicar uma opção `--strip`, ela tirará toda a estrutura do diretório. Tudo bem se todos os arquivos estiverem no diretório base, mas se o patch foi criado em `minhaversão/` e um dos arquivos editados for `minhaversão/src/arquivo`, e você executar o patch sem uma opção `--strip` de `suaversão`, ele tentará corrigir um arquivo chamado `suaversão/arquivo`.

A maioria dos desenvolvedores cria patches a partir do diretório pai do diretório que está sendo corrigido, então `--strip=1` geralmente estará correto.

## Usando quilt

Uma maneira mais simples de criar patches é usar o [quilt](https://www.archlinux.org/packages/?name=quilt), que tem um trabalho melhor para gerenciar vários patches, como aplicar patches, atualizar patches e reverter arquivos com patches para o estado original. O [quilt](https://www.archlinux.org/packages/?name=quilt) é usado no [Debian](https://wiki.debian.org/UsingQuilt "debian:UsingQuilt") para gerenciar seus patches. Consulte [Using Quilt](http://www.shakthimaan.com/downloads/glv/quilt-tutorial/quilt-doc.pdf) para obter informações básicas sobre o uso de quilt básico para gerar, aplicar patches e reverter arquivos corrigidos.

## Veja também

*   [http://www.kegel.com/academy/opensource.html](http://www.kegel.com/academy/opensource.html) — Informações úteis sobre fazer patching de arquivos