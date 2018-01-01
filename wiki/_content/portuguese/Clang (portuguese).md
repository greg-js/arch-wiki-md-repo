[Clang](http://clang.llvm.org/) é um compilador C/C++/Objective C baseado em LLVM. É distribuído sob a licença BSD.

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
*   [2 Compilar pacotes com Clang](#Compilar_pacotes_com_Clang)
*   [3 Usar o analisador estático](#Usar_o_analisador_est.C3.A1tico)
*   [4 Referências](#Refer.C3.AAncias)

## Instalação

Instale [clang](https://www.archlinux.org/packages/?name=clang) dos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais").

## Compilar pacotes com Clang

Adicione `export CC=clang` e (para C++) `export CXX=clang++` ao seu `/etc/makepkg.conf`. Se você está compilando com `debug`, também remova `-fvar-tracking-assignments` de `DEBUG_CFLAGS` ande `DEBUG_CXXFLAGS`, pois não há suporte no clang.

Note que para pacotes que especificam opções de compilação específicas de GCC, pode haver erros que exigem a edição de pacotes fonte, PKGBUILD ou comentar as linhas clang no makepkg.conf.

## Usar o analisador estático

Para analisar um projeto, basta colocar a palavra `scan-build` na frente de seu comando de compilação. Por exemplo:

```
$ scan-build make

```

**Dica:** Se seu projeto já está compilado, `scan-build` não vai recompilar e não vai analisar. Para forçar a recompilação e análise, use a opção `-B`: `$ scan-build make -B` 

Também é possível analisar arquivos específicos:

```
$ scan-build gcc -c t1.c t2.c

```

## Referências

*   [scan-build: executando um analisador a partir da linha de comando](http://clang-analyzer.llvm.org/scan-build.html)