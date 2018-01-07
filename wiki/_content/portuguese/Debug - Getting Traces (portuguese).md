Artigos relacionados

*   [General troubleshooting](/index.php/General_troubleshooting "General troubleshooting")
*   [Diretrizes de relatórios de erro](/index.php/Diretrizes_de_relat%C3%B3rios_de_erro "Diretrizes de relatórios de erro")
*   [Step-by-step debugging guide](/index.php/Step-by-step_debugging_guide "Step-by-step debugging guide")

Esse artigo visa ajudar na criação de um pacote de depuração do Arch e usá-lo para fornecer informações de rastro e depuração para relatar bugs de software para desenvolvedores.

## Contents

*   [1 Nomes de pacotes](#Nomes_de_pacotes)
*   [2 PKGBUILD](#PKGBUILD)
*   [3 Configurações de compilação](#Configura.C3.A7.C3.B5es_de_compila.C3.A7.C3.A3o)
    *   [3.1 Geral](#Geral)
    *   [3.2 Qt4](#Qt4)
    *   [3.3 Qt5](#Qt5)
    *   [3.4 Aplicativos CMAKE (KDE)](#Aplicativos_CMAKE_.28KDE.29)
*   [4 Compilando e instalando o pacote](#Compilando_e_instalando_o_pacote)
*   [5 Obtendo o rastro](#Obtendo_o_rastro)
*   [6 Conclusão](#Conclus.C3.A3o)
*   [7 Veja também](#Veja_tamb.C3.A9m)

## Nomes de pacotes

Ao procurar por mensagens de depuração, tal como:

```
[...]
Backtrace was generated from '/usr/bin/epiphany'

**(no debugging symbols found)**
Using host libthread_db library "/lib/libthread_db.so.1".
**(no debugging symbols found)**
[Thread debugging using libthread_db enabled]
[New Thread -1241265952 (LWP 12630)]
(no debugging symbols found)
0xb7f25410 in __kernel_vsyscall ()
#0  0xb7f25410 in __kernel_vsyscall ()
#1  0xb741b45b in **??** () from /lib/libpthread.so.0
[...]

```

`??` mostra onde a informação de depuração está faltando, assim como o nome da biblioteca ou executável que chamou a função. Similarmente, quando `(no debugging symbols found)` aparece, você deve procurar pelos nomes de arquivos mencionados. Por exemplo, com [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)"):

```
$ pacman -Qo /lib/libthread_db.so.1
/lib/libthread_db.so.1 pertence a *glibc* 2.5-8

```

O pacote é chamado [glibc](https://www.archlinux.org/packages/?name=glibc) na versão 2.5-8\. Repita essa etapa para todo pacote que precisa de depuração.

## PKGBUILD

Para compilar um pacote a partir do fonte, o arquivo PKGBUILD file é necessário. Veja [ABS (Português)](/index.php/ABS_(Portugu%C3%AAs) "ABS (Português)") para pacotes nos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais"), e [AUR (Português)#Obtendo arquivos de compilação](/index.php/AUR_(Portugu%C3%AAs)#Obtendo_arquivos_de_compila.C3.A7.C3.A3o "AUR (Português)") para pacotes no [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)").

## Configurações de compilação

Neste estágio, você pode modificar o arquivo de configuração global do `makepkg` se você for usá-lo apenas para propósito de depuração. Nos demais casos, você deve modificar o arquivo PKGBUILD do pacote apenas para cada pacote que você gostaria de recompilar.

### Geral

Desde o pacman 4.1, `/etc/makepkg.conf` possui flags de depuração de compilação em `DEBUG_CFLAGS` e `DEBUG_CXXFLAGS`. Para usá-las, habilite a opção do makepkg `debug` e desabilite `strip`.

```
OPTIONS+=(debug !strip)

```

Essas configurações vão forçar a compilação com informações de depuração e vai desabilitar a remoção de símbolos de executáveis. Para aplicar essa configuração a um único pacote, modifique o PKGBUILD:

```
options=(debug !strip)

```

Alternativamente, você pode colocar as informações de depuração em um pacote separado habilitando `debug` e `strip`, informações de depuração serão então removidos do pacote principal e colocados em um pacote separado `*foo*-debug`.

**Nota:** Não é suficiente só instalar o pacote de depuração de recentemente compilado, porque o depurador vai conferir se o arquivo contendo os símbolos de depuração é o da mesma compilação que a biblioteca e executável associados. Você deve instalar os pacotes recompilados. No Arch, os arquivos de símbolos de depuração são instalados sob `/usr/lib/debug`. Veja a [documentação do GDB](https://sourceware.org/gdb/onlinedocs/gdb/Separate-Debug-Files.html) para mais informações sobre os pacotes de depuração.

Note que certos pacotes como *glibc* são removidos. Verifique o PKGBUILD para seções como:

```
strip $STRIP_BINARIES usr/bin/{gencat,getconf,getent,iconv,iconvconfig} \
                      usr/bin/{ldconfig,locale,localedef,nscd,makedb} \
                      usr/bin/{pcprofiledump,pldd,rpcgen,sln,sprof} \
                      usr/lib/getconf/*

strip $STRIP_STATIC usr/lib/*.a

strip $STRIP_SHARED usr/lib/{libanl,libBrokenLocale,libcidn,libcrypt}-*.so \
                    usr/lib/libnss_{compat,db,dns,files,hesiod,nis,nisplus}-*.so \
                    usr/lib/{libdl,libm,libnsl,libresolv,librt,libutil}-*.so \
                    usr/lib/{libmemusage,libpcprofile,libSegFault}.so \
                    usr/lib/{audit,gconv}/*.so

```

E, então, remova onde apropriado.

### Qt4

Além das configurações gerais anteriores, passe a opção `-developer-build` para o script `configure` no `PKGBUILD`. Por padrão, `-developer-build` passa `-Werror` para o compilador, o que pode fazer com que a compilação falhe. Para evitar erros de compilação, você pode precisar passar `-no-warnings-are-errors` também.

### Qt5

O repositório [qt-debug](/index.php/Unofficial_user_repositories#qt-debug "Unofficial user repositories") contém pacotes Qt/PyQt pré-compilados com símbolos de depuração. Veja também as instruções do [upstream](http://doc.qt.io/qt-5/debug.html).

### Aplicativos CMAKE (KDE)

[KDE](/index.php/KDE "KDE") e programas relacionados geralmente usam [cmake](https://www.archlinux.org/packages/?name=cmake). Para habilitar informações de depuração e desabilitar otimização, altere `-DCMAKE_BUILD_TYPE` para `Debug`. Para habilitar informações de depuração enquanto mantém as otimizações habilitadas, altere `-DCMAKE_BUILD_TYPE` para `RelWithDebInfo`.

## Compilando e instalando o pacote

Compile o pacote a partir do fonte usando `makepkg` no diretório do PKGBUILD. Isso pode levar algum tempo:

```
$ makepkg

```

Então, instale o pacote compilado:

```
# pacman -U glibc-2.26-1-x86_64.pkg.tar.gz

```

## Obtendo o rastro

O backtrace real (ou rastro de pilha) pode agora ser obtido por meio de, p.ex. [gdb](https://www.archlinux.org/packages/?name=gdb), o GNU Debugger. Execute-o através de:

```
# gdb /caminho/para/arquivo

```

ou:

```
# gdb
(gdb) exec /caminho/para/arquivo

```

O caminho é opcional, se já definido na variável `$PATH`.

Então, dentro do `gdb`, digite `run` seguido por quaisquer argumentos que você deseje que o programa inicie com, p.ex.:

```
(gdb) run --no-daemon --verbose

```

para iniciar a execução do arquivo. Faça o que for necessário para evocar o erro. Para registrar log, digite as linhas:

```
(gdb) set logging file rastro.log
(gdb) set logging on

```

e então:

```
(gdb) thread apply all bt full

```

para emitir o rastro para `rastro.log` no diretório no qual `gdb` foi iniciado. Para sair, digite:

```
(gdb) set logging off
(gdb) quit

```

**Dica:** Para depurar um aplicativo escrito em python:
```
# gdb /usr/bin/python
(gdb) run <aplicativo em python>

```

Você também pode depurar um aplicativo em execução, p.ex.:

```
 # gdb --pid=$(pidof firefox)
 (gdb) continue

```

Para depurar um aplicativo que já travou, você vai querer usar o gdb [despejo de núcleo](/index.php/Core_dump#Examining_a_core_dump "Core dump").

## Conclusão

Use o rastro de pilha completo para informar os desenvolvedores de um erro que você descobriu. Isso será muito apreciado por eles e ajudará a melhorar o seu programa favorito

## Veja também

*   [Gentoo Wiki - Backtraces with Gentoo](https://wiki.gentoo.org/wiki/Project:Quality_Assurance/Backtraces)
*   [Fedora - StackTraces](http://fedoraproject.org/wiki/StackTraces)
*   [GNOME - Getting Stack Traces](https://wiki.gnome.org/Community/GettingInTouch/Bugzilla/GettingTraces/Details#obtain-a-stacktrace)
*   [mini-introdução ao gdb](http://linux.bytesex.org/gdb.html)