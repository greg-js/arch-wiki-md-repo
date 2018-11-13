**Status de tradução:** Esse artigo é uma tradução de [Clang](/index.php/Clang "Clang"). Data da última tradução: 2018-11-05\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Clang&diff=0&oldid=551753) na versão em inglês.

[Clang](http://clang.llvm.org/) é um compilador [C](/index.php/C "C")/C++/Objective C//[CUDA](/index.php/CUDA "CUDA") baseado em [LLVM](/index.php/LLVM "LLVM"). É distribuído sob a licença BSD.

## Contents

*   [1 Instalação](#Instalação)
*   [2 Compilar pacotes com Clang](#Compilar_pacotes_com_Clang)
*   [3 Usar o analisador estático](#Usar_o_analisador_estático)
*   [4 Veja também](#Veja_também)

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [clang](https://www.archlinux.org/packages/?name=clang).

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

## Veja também

*   [Wikipedia:pt:Clang](https://en.wikipedia.org/wiki/pt:Clang "wikipedia:pt:Clang")
*   [scan-build: executando um analisador a partir da linha de comando](http://clang-analyzer.llvm.org/scan-build.html)
*   [Compilando CUDA com clang](http://llvm.org/docs/CompileCudaWithLLVM.html)