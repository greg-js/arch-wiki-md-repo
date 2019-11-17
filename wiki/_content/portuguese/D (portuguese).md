De [Wikipedia:D (programming language)](https://en.wikipedia.org/wiki/D_(programming_language) "wikipedia:D (programming language)"):

	"A linguagem de programação D, também conhecida simplesmente como D, é uma linguagem de programação de sistema multiparadigmático, orientada a objetos, de Walter Bright, da Digital Mars. D se originou como uma reengenharia do C++, mas, embora seja predominantemente influenciado por essa linguagem, não é uma variante dela. D redesenhou alguns recursos do C++ e foi influenciado por conceitos usados em outras linguagens de programação, como Java, C# e Eiffel".

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Testando a instalação](#Testando_a_instalação)
*   [3 Considerações](#Considerações)
*   [4 Bibliotecas e bindings úteis](#Bibliotecas_e_bindings_úteis)
*   [5 Veja também](#Veja_também)

## Instalação

Para programar em D, você precisará de duas coisas - um compilador D e uma biblioteca. A maneira mais fácil de começar rapidamente é instalar o grupo de pacotes [dlang-dmd](https://www.archlinux.org/groups/x86_64/dlang-dmd/). Ele fornecerá o compilador oficial ([dmd](https://www.archlinux.org/packages/?name=dmd)), a biblioteca padrão [libphobos](https://www.archlinux.org/packages/?name=libphobos) e o [dtools](https://www.archlinux.org/packages/?name=dtools), uma coleção de pequenas ferramentas de desenvolvimento.

## Testando a instalação

Para garantir que tudo esteja instalado e configurado corretamente, um programa simples de "Olá mundo" deve ser suficiente.

```
import std.stdio;

void main() {
   string seuNome = "archer";
   writefln("Olá, %s!", seuNome);
}

```

Cole o código em um arquivo, nomeie-o como `hello.d` e execute:

```
$ dmd hello.d

```

no mesmo diretório que o arquivo. Você deve ser capaz de executar o programa com:

```
$ ./hello

```

Você também pode executar

```
$ dmd -run hello.d

```

que simplesmente compila e executa sem deixar nenhum arquivo de objeto no diretório.

## Considerações

No entanto, existem opções possíveis em relação ao compilador escolhido. O padrão (referência um) é dmd, mas [gdc](https://www.archlinux.org/packages/?name=gdc) (GNU D Compiler) e [ldc](https://www.archlinux.org/packages/?name=ldc) (LLVM D Compiler) também são populares. Esses também estão na [community].

A partir de abril de 2017 [o back-end do dmd agora é FOSS](https://github.com/dlang/dmd/pull/6680,) (licenciado pelo Boost). Todos os três compiladores compartilham o mesmo código de front-end e, portanto, têm suporte quase idêntico aos recursos da linguagem (assumindo a mesma versão de front-end).

## Bibliotecas e bindings úteis

*   [DDT](https://code.google.com/p/ddt/) - Plugin do Eclipse para projeto e gerenciamento de código em D
*   [Mono-D](http://mono-d.alexanderbothe.com/) - Complemento de [MonoDevelop](http://monodevelop.com/) para programar em D
*   [QtD](https://bitbucket.org/qtd/repo) - Bindings Qt para D
*   [GtkD](http://gtkd.org/) - Uma interface GTK orientada a objeto para D
*   [Derelict](https://github.com/aldacron/Derelict3) - Bindings para bibliotecas de multimídias, com foco em desenvolvimento de jogo
*   [Deimos](https://github.com/D-Programming-Deimos) - Um projeto que engloba vários bindings para diferentes bibliotecas C

## Veja também

*   [Repositório GitHub do Phobos](https://github.com/D-Programming-Language/phobos/)
*   [The D Programming Language](http://dlang.org/) - A página oficial do D
*   [Planet D](http://planet.dsource.org/) - Uma coleção de blogs sobre D