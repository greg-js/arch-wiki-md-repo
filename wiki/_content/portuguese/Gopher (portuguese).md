**Status de tradução:** Esse artigo é uma tradução de [Gopher](/index.php/Gopher "Gopher"). Data da última tradução: 2019-01-18\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Gopher&diff=0&oldid=563786) na versão em inglês.

[Gopher](https://en.wikipedia.org/wiki/Gopher_(protocol) é um protocolo para transferência de informações pela Internet que era muito popular antes do HTTP assumir como o protocolo dominante, mas ainda há uma comunidade de usuários gopher que prefere a simplicidade do protocolo em relação aos protocolos mais complexos e grandes mais frequentemente encontrados. Note que nem todos os navegadores possuem suporte ao gopher, ou têm suporte incompleto.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Servidor GoFish](#Servidor_GoFish)
    *   [1.1 Instalação](#Instalação)
    *   [1.2 Configuração](#Configuração)
    *   [1.3 .cache](#.cache)
*   [2 Gopher Browser](#Gopher_Browser)
*   [3 Overbite para Firefox](#Overbite_para_Firefox)
*   [4 Acesso HTTP via proxy Gopher](#Acesso_HTTP_via_proxy_Gopher)
*   [5 Veja também](#Veja_também)

## Servidor GoFish

[GoFish](http://gofish.sourceforge.net/) é um servidor gopher básico que permite que você execute seu próprio *gopherspace*. A configuração é semelhante a outros servidores, mas geralmente requer menos recursos para funcionar.

### Instalação

[Instale](/index.php/Instale "Instale") o pacote [gofish](https://aur.archlinux.org/packages/gofish/).

### Configuração

Existem algumas configurações básicas para o servidor que você pode alterar no arquivo `/etc/gofish.conf`, mas os padrões funcionarão. Se você não alterar nenhuma configuração, a raiz do servidor gopher será `/var/gopher` e será executada na porta 70\. (Observe que o Firefox só pode usar o protocolo gopher na porta 70, então mudar isso significará que seus usuários devem usar algum outro cliente.)

Para rodar o servidor, [inicie](/index.php/Inicie "Inicie") `gofish.service`.

Você pode conectar ao seu servidor e ver o que você tem navegando em [gopher://127.0.0.1](gopher://127.0.0.1)

### .cache

Ao contrário do FTP, que mostra automaticamente todos os arquivos, o gopher depende de um arquivo chamado `.cache` em cada diretório para determinar como a página será mostrada ao usuário final. Embora o GoFish venha com a página man dotcache(5) para os arquivos `.cache`, pode ser um pouco confuso. O GoFish também vem com um programa para autogerar os arquivos `.cache` para todos os diretórios e arquivos na raiz do seu servidor.

```
mkcache -r

```

Isto irá criar todos os arquivos `.cache` necessários de forma recursiva, mas você pode querer editar alguns nomes. Um exemplo de arquivo `.cache` se parece com isto:

```
iHello         none            example.com     70
0ReadMe	0/ReadMe.txt	example.com	70
1Ebooks	1/ebooks	example.com	70

```

O protocolo gopher usa prefixos numéricos para descrever o tipo de arquivo. `0` é um arquivo de texto simples, `1` é um diretório e `9` é um arquivo binário. O `i` indica uma imagem e, se estiver vinculada a `none`, ela será mostrada como texto simples. Isso é bom para apresentar seu site. Veja a página do manual dotcache(5) para mais informações sobre os prefixos. Após o prefixo, o nome será exibido no cliente e não precisará ser o mesmo que o arquivo ao qual ele está vinculado. Na segunda seção, vemos o "caminho" para o arquivo. Não existe um diretório chamado `0` ou `1` no sistema de arquivos, ele é adicionado apenas no URI para permitir que o servidor gopher e o usuário final saibam que tipo de arquivo ele é. A terceira seção é qualquer nome de domínio do site e o quarto é a porta em que está, o padrão é 70\. O espaço entre cada uma das quatro seções deve ser uma guia, não um espaço ou não será analisado corretamente.

Agora vamos examinar o arquivo `.cache` no diretório de e-books.

```
9Book 1	9/ebooks/Book1.chm	example.com	70
9Book 2	9/ebooks/Book2.pdf	example.com	70

```

Observe que o URI é `9/ebooks/Book1.chm`, e não `1/ebooks/9Book1.chm`. Há sempre apenas um número de prefixo para o último item no URI. Observe também que um arquivo chm ou um arquivo pdf não são exatamente binários, mas ainda recebem o prefixo `9`. No servidor GoFish, qualquer arquivo que não seja um arquivo de texto ou um diretório recebe o prefixo binário. Lembre-se que, se houver arquivos na raiz do seu servidor, as pessoas podem baixá-los ou visualizá-los, mesmo que eles não estejam no seu arquivo `.cache`, portanto, tenha cuidado.

## Gopher Browser

Para navegar no *gopherspace* como era originalmente destinado a ser navegado, você pode instalar o navegador gopher da Universidade de Minnesota com o pacote [gopher](https://aur.archlinux.org/packages/gopher/).

## Overbite para Firefox

[The Overbite Project](https://gopher.floodgap.com/overbite/) adiciona capacidade de *gopherspace* em alguns navegadores e dispositivos, incluindo o Mozilla Firefox. Verifique os complementos [firefox-extension-overbitenx](https://aur.archlinux.org/packages/firefox-extension-overbitenx/) ou [overbitewx](https://addons.mozilla.org/en-US/firefox/addon/overbitewx/).

**Nota:** OverbiteNX e OverbiteWX são sucessores do complemento anterior OverbiteFF, conforme registrado nos sites dessas extensões.

## Acesso HTTP via proxy Gopher

Você pode usar [http://gopher.floodgap.com/gopher/gw](http://gopher.floodgap.com/gopher/gw) para navegar na rede Gopher via HTTP, por exemplo, usando um navegador sem suporte a Gopher.

## Veja também

*   [Site do GoFish](http://gofish.sourceforge.net/)
*   [Exemplos de sites Gopher](http://gopher.floodgap.com/gopher/gw?gopher/1/new)