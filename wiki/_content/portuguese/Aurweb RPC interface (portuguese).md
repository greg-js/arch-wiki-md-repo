**Status de tradução:** Esse artigo é uma tradução de [Aurweb RPC interface](/index.php/Aurweb_RPC_interface "Aurweb RPC interface"). Data da última tradução: 2018-11-09\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Aurweb_RPC_interface&diff=0&oldid=553497) na versão em inglês.

Artigos relacionados

*   [Official repositories web interface](/index.php/Official_repositories_web_interface "Official repositories web interface")

A [interface RPC do Aurweb](https://aur.archlinux.org/rpc.php) é uma interface [RPC](https://en.wikipedia.org/wiki/pt:Chamada_de_procedimento_remoto "wikipedia:pt:Chamada de procedimento remoto") leve para o [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)"). Consultas são enviadas como requisições HTTP GET e respostas do servidor com [JSON](http://www.json.org/).

**Nota:** Esse artigo descreve a v5 da API de Interface do RPC, conforme atualizado com o AUR v4.7.0 em 7 de julho de 2018.

## Contents

*   [1 Uso da API](#Uso_da_API)
    *   [1.1 Tipos de consulta](#Tipos_de_consulta)
        *   [1.1.1 search](#search)
        *   [1.1.2 info](#info)
    *   [1.2 Tipos de retorno](#Tipos_de_retorno)
        *   [1.2.1 error](#error)
        *   [1.2.2 search](#search_2)
        *   [1.2.3 info](#info_2)
    *   [1.3 jsonp](#jsonp)
*   [2 Limitações](#Limita.C3.A7.C3.B5es)
*   [3 Clientes de referência](#Clientes_de_refer.C3.AAncia)

## Uso da API

### Tipos de consulta

Há dois tipos de consultas:

*   search
*   info

#### search

Pesquisas por pacote podem ser feitas enviando requisições na forma:

```
/rpc/?v=5&type=search&by=*campo*&arg=*palavras-chave*

```

sendo `*palavras-chave*` o argumento de pesquisa e `*campo*` um dos valores a seguir:

*   `name` (pesquisa pelo nome do pacote apenas)
*   `name-desc` (pesquisa pelo nome e descrição do pacote)
*   `maintainer` (pesquisa pelo mantenedor do pacote)
*   `depends` (pesquisa pacotes que são dependências por palavras-chaves)
*   `makedepends` (pesquisa pacotes que são dependências para compilação por palavras-chaves)
*   `optdepends` (pesquisa pacotes que são dependências opcionais por palavras-chaves)
*   `checkdepends` (pesquisa pacotes que são dependências para verificação por palavras-chaves)

O parâmetro `by` pode ser pulado, tendo como padrão `name-desc`. tipos possíveis de retorno são `search` e `error`.

Se uma pesquisa de mantenedor for realizada e o argumento de pesquisa for deixado vazio, uma lista de pacotes órfãos é retornada.

Exemplos:

Pesquisar por `foobar`:

```
https://aur.archlinux.org/rpc/?v=5&type=search&arg=foobar

```

Pesquisar por pacotes mantidos por `john`:

```
https://aur.archlinux.org/rpc/?v=5&type=search&by=maintainer&arg=john

```

Pesquisar por pacotes que têm `foobar` como `makedepends`:

```
https://aur.archlinux.org/rpc/?v=5&type=search&by=makedepends&arg=foobar

```

Pesquisar com chamadas:

```
https://aur.archlinux.org/rpc/?v=5&type=search&arg=foobar&callback=jsonp1192244621103

```

#### info

Informações de pacote podem ser obtidas enviando requisições na forma:

```
/rpc/?v=5&type=info&arg[]=*pkg1*&arg[]=*pkg2*&…

```

sendo `*pkg1*`, `*pkg2*`, … correspondências exatas de nomes de pacotes para obter detalhes de pacote.

Tipos de retorno possível são `multiinfo` e `error`.

Exemplos:

Informação para um único pacote `foobar`:

```
https://aur.archlinux.org/rpc/?v=5&type=info&arg[]=foobar

```

Informação para múltiplos pacotes `foobar` e `bar`:

```
https://aur.archlinux.org/rpc/?v=5&type=info&arg[]=foo&arg[]=bar

```

### Tipos de retorno

A carga de retorno é de um formato, e atualmente tem três tipos principais. A resposta sempre retornará um tipo para que o usuário possa determinar se o resultado de uma operação foi um erro ou não.

O formato da carga retornada é:

```
{"version":5,"type":*TipoRetornado*,"resultcount":0,"results":*DadosRetornados*}

```

`*TipoRetornado*` é uma string e o valor é um entre:

*   `search`
*   `multiinfo`
*   `error`

O tipo de `*DadosRetornados*` é um vetor de dicionário de objetos para os `*TipoRetornado*` `search` e `multiinfo` e um vetor vazio para `*TipoRetornado*` `error`.

#### error

O tipo `error` possui uma string de resposta de erro como o valor retornado. Uma resposta de erro pode ser retornada de um tipo de consulta `search` ou `info`.

Exemplo de `*TipoRetornado*` `error`:

```
{"version":5,"type":"error","resultcount":0,"results":[],"error":"Incorrect by field specified."}

```

#### search

O tipo `search` é resultado retornado de uma operação de requisição de pesquisa. **Os reais resultados da uma operação de pesquisa serão os mesmos que os de uma requisição de informações para cada resultado. Veja a seção [#info](#info) abaixo.**

Exemplo de `*TipoRetornado*` `search`:

```
{"version":5,"type":"search","resultcount":2,"results":[{"ID":206807,"Name":"cower-git", ...}]}

```

#### info

O tipo `multiinfo` é o resultado de uma operação de requisição de informações.

Exemplo de `*TipoRetornado*` `multiinfo`:

```
 {
    "version":5,
    "type":"multiinfo",
    "resultcount":1,
    "results":[{
        "ID":229417,
        "Name":"cower",
        "PackageBaseID":44921,
        "PackageBase":"cower",
        "Version":"14-2",
        "Description":"A simple AUR agent with a pretentious name",
        "URL":"http:\/\/github.com\/falconindy\/cower",
        "NumVotes":590,
        "Popularity":24.595536,
        "OutOfDate":null,
        "Maintainer":"falconindy",
        "FirstSubmitted":1293676237,
        "LastModified":1441804093,
        "URLPath":"\/cgit\/aur.git\/snapshot\/cower.tar.gz",
        "Depends":[
            "curl",
            "openssl",
            "pacman",
            "yajl"
        ],
        "MakeDepends":[
            "perl"
        ],
        "License":[
            "MIT"
        ],
        "Keywords":[]
    }]
 }

```

### jsonp

Se você está trabalhando com uma página javascript e precisa de um mecanismo de retorno de chamada do JSON, você pode fazê-lo. Você só precisa fornecer uma variável de retorno de chamada adicional. Esse retorno de chamada geralmente é tratado através da biblioteca javascript, mas aqui é um exemplo.

Consulta exemplo:

```
https://aur.archlinux.org/rpc/?v=5&type=search&arg=foobar&callback=jsonp1192244621103

```

Resultado exemplo:

```
/**/jsonp1192244621103({"version":5,"type":"search","resultcount":1,"results":[{"ID":250608,"Name":"foobar2000","PackageBaseID":37068,"PackageBase":"foobar2000","Version":"1.3.9-1","Description":"An advanced freeware audio player (uses Wine).","URL":"http:\/\/www.foobar2000.org\/","NumVotes":39,"Popularity":0.425966,"OutOfDate":null,"Maintainer":"supermario","FirstSubmitted":1273255356,"LastModified":1448326415,"URLPath":"\/cgit\/aur.git\/snapshot\/foobar2000.tar.gz"}]})

```

Isso chamaria automaticamente a função JavaScript `jsonp1192244621103` com o parâmetro definido para os resultados da chamada RPC.

## Limitações

*   Requisições de HTTP GET são limitadas a uma URI com tamanho máximo de 8190 bytes. Porém, a instância oficial do AUR, no servidor nginx com HTTP/2, usa o limite de [tamanho máximo padrão de URI](https://nginx.org/en/docs/http/ngx_http_v2_module.html#http2_max_field_size) de 4443 bytes. Requisições de informações com mais do que 200 pacotes como argumento precisarão ser divididos.
*   A taxa de API está limitada a um máximo de 4000 requisições por dia por IP.

## Clientes de referência

Às vezes, as coisas são mais fáceis de entender com exemplos. Algumas implementações de referência (jQuery, python, ruby) estão disponíveis na seguinte URL: [https://github.com/cactus/random/tree/2b72a1723bfc8ae64eed6a3c40cb154accae3974/aurjson_examples](https://github.com/cactus/random/tree/2b72a1723bfc8ae64eed6a3c40cb154accae3974/aurjson_examples)