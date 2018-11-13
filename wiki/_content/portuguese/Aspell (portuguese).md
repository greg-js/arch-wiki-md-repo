**Status de tradução:** Esse artigo é uma tradução de [Aspell](/index.php/Aspell "Aspell"). Data da última tradução: 2018-11-12\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Aspell&diff=0&oldid=554857) na versão em inglês.

Do [site oficial](http://aspell.net/): "O GNU Aspell é um verificador ortográfico livre e de código aberto projetado para substituir [Ispell](https://en.wikipedia.org/wiki/Ispell "wikipedia:Ispell"). Ele pode ser usado como uma biblioteca ou como um verificador ortográfico independente."

## Contents

*   [1 Instalação](#Instalação)
*   [2 Uso](#Uso)
*   [3 Solução de problemas](#Solução_de_problemas)
    *   [3.1 Todo texto está marcado como incorreto](#Todo_texto_está_marcado_como_incorreto)
*   [4 Veja também](#Veja_também)

## Instalação

[Instale](/index.php/Instale "Instale") o [dicionário aspell](https://www.archlinux.org/packages/?sort=&q=aspell-) para o idioma que você deseja. Fazer isso vai também baixar o pacote [aspell](https://www.archlinux.org/packages/?name=aspell) como uma dependência.

## Uso

Muitos programas usam o *aspell* automaticamente e não precisam de configuração adicional. Além disso, pode-se usar o *aspell* manualmente. Aqui estão alguns usos básicos. Veja [aspell(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/aspell.1) para mais.

Para verificar a ortografia de um único arquivo:

```
$ aspell check *um_arquivo*

```

Você será então colocado em um prompt com o texto do arquivo exibido. A partir daí, você pode selecionar *aspell* para fazer correções em cada palavra escrita incorretamente, ou pode optar por ignorar suas sugestões. As correções que você fizer serão salvas no arquivo.

Para lista palavras com erro de escrita a partir da entrada padrão:

```
$ aspell list < *um_arquivo*

```

## Solução de problemas

### Todo texto está marcado como incorreto

Certifique-se de ter o dicionário correto instalado. Se a instalação dos arquivos de dicionário não resolver o problema, é mais provável que ocorra um problema com o `enchant`. Verifique os arquivos de dicionário conhecidos:

 `$ aspell dicts` 
```
pt_BR
pt_PT
pt_PT-preao
...etc
```

Se o dicionário do respectivo idioma está listado, adicione-o ao `/usr/share/enchant/enchant.ordering`. Pelo exemplo acima, ele seria:

```
pt_BR:aspell

```

## Veja também

*   [Documento info do aspell](http://aspell.net/man-html/index.html)
*   [Wikipedia:GNU Aspell](https://en.wikipedia.org/wiki/GNU_Aspell "wikipedia:GNU Aspell")