**Faction** é uma biblioteca para desenvolvimento de software movido a testes.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Uso](#Uso)
*   [3 Exemplo](#Exemplo)
*   [4 Modos](#Modos)
    *   [4.1 Recursos de modo estendido](#Recursos_de_modo_estendido)
*   [5 Veja também](#Veja_também)

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [libfaction](https://aur.archlinux.org/packages/libfaction/).

## Uso

A biblioteca fornece várias macros C para acelerar os testes de gravação.

*   FI representa "Faction Initialization"
*   FT indica um "Faction Test"
*   FC representa "Faction Close"

Usando a macro FT, três campos são obrigatórios.

*   AUTHORS() pega uma lista separada por vírgula de nomes de autores entre aspas duplas
*   SPEC() recebe uma única descrição de especificação de teste entre aspas duplas
*   Uma expressão booleana C (como ao usar macros de declaração C)

A convenção determina que os testes de Faction devem ser escritos na parte inferior do arquivo fonte que contém o código que será testado. Os testes devem ser cercados por uma proteção macro FACTION (veja o exemplo abaixo) para que possam ser ativados/desativados no tempo de compilação. Compiladores C, como o GNU C Compiler (GCC), oferecem uma maneira de ativar macros na linha de comando (ou seja, o sinalizador `-D`)

## Exemplo

```
/* Essa é a função a ser testada */
int
increment(int input)
{
   return (input + 1);
}

#ifdef FACTION
#include <faction.h>
#include <limits.h>
FI

  FT(
    AUTHORS( "timetoplatypus" ),
    SPEC( "increment() returns 1 when given 0" ),
    increment(0) == 1
  );

  FT(
    AUTHORS( "timetoplatypus" ),
    SPEC( "increment() returns 0 when given the largest integer value" ),
    increment(INT_MAX) == 0
  );

FC
#endif

```

Isso pode ser compilado usando `gcc *nome-de-arquivo.c* -D FACTION`

## Modos

Existem dois modos nos quais o Faction pode compilar: o modo *minimal* e o modo 'extended'.

O exemplo acima compila Faction no modo mínimo. Uma compilação mínima possui exatamente três dependências de biblioteca: stdlib, stdio e getopt. Uma compilação estendida possui dependências adicionais, incluindo algumas funções que estão disponíveis apenas através da macro de teste do recurso GNU.

Portanto, para compilar no modo estendido, basta definir a macro de teste do recurso GNU na parte superior do arquivo. Por exemplo, o exemplo anterior modificado para ser compilado no modo estendido ficaria assim:

```
#ifdef FACTION
#define _GNU_SOURCE
#endif
```

```
/* Essa é a saída a ser testada */
increment(int input)
{
  return (input + 1);
}

#ifdef FACTION
#include <faction.h>
#include <limits.h>
FI

  FT(
    AUTHORS( "timetoplatypus" ),
    SPEC( "increment() returns 1 when given 0" ),
    increment(0) == 1
  );

  FT(
    AUTHORS( "timetoplatypus" ),
    SPEC( "increment() returns 0 when given the largest integer value" ),
    increment(INT_MAX) == 0
  );

FC
#endif
```

### Recursos de modo estendido

No modo estendido,

*   a saída pode ser opcionalmente espelhada para um arquivo de log especificado pelo usuário usando o sinalizador `-l` no tempo de execução.
*   a tabela de resultados será redimensionada dinamicamente para a largura do terminal que está sendo usado. Caso contrário, o padrão será uma largura de 78 caracteres.

## Veja também

*   [Site do Faction](https://timetoplatypus.com/static/faction/index.html)
*   [Projeto exemplo do Faction](https://git.timetoplatypus.com/timetoplatypus/three_b)