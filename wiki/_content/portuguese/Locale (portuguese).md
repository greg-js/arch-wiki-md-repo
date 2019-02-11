**Status de tradução:** Esse artigo é uma tradução de [Locale](/index.php/Locale "Locale"). Data da última tradução: 2019-01-01\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Locale&diff=0&oldid=560668) na versão em inglês.

Artigos relacionados

*   [Variáveis de ambiente](/index.php/Vari%C3%A1veis_de_ambiente "Variáveis de ambiente")

[Locales](https://en.wikipedia.org/wiki/Locale_(computer_software) "wikipedia:Locale (computer software)"), por vezes chamados em português de *localidades*, são usados pelo [glibc](https://www.archlinux.org/packages/?name=glibc) e outros programas ou bibliotecas conscientes de locales para renderizar texto, exibindo corretamente valores monetários regionais, formatos de hora e data, idiossincrasias alfabéticas e outros padrões específicas para locales.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Gerando locales](#Gerando_locales)
*   [2 Configurando o locale](#Configurando_o_locale)
    *   [2.1 Configurando o locale do sistema](#Configurando_o_locale_do_sistema)
    *   [2.2 Sobrepondo locale do sistema por sessão de usuário](#Sobrepondo_locale_do_sistema_por_sessão_de_usuário)
    *   [2.3 Fazer alterações de locale imediatas](#Fazer_alterações_de_locale_imediatas)
    *   [2.4 Outros usos](#Outros_usos)
*   [3 Variáveis](#Variáveis)
    *   [3.1 LANG: locale padrão](#LANG:_locale_padrão)
    *   [3.2 LANGUAGE: locales reservas](#LANGUAGE:_locales_reservas)
    *   [3.3 LC_TIME: formato de data e hora](#LC_TIME:_formato_de_data_e_hora)
    *   [3.4 LC_COLLATE: colação](#LC_COLLATE:_colação)
    *   [3.5 LC_ALL: solução de problemas](#LC_ALL:_solução_de_problemas)
*   [4 Solução de problemas](#Solução_de_problemas)
    *   [4.1 Meu terminal não possui suporte a UTF-8](#Meu_terminal_não_possui_suporte_a_UTF-8)
        *   [4.1.1 Gnome-terminal ou rxvt-unicode](#Gnome-terminal_ou_rxvt-unicode)
    *   [4.2 Meu sistema ainda está usando o idioma errado](#Meu_sistema_ainda_está_usando_o_idioma_errado)
*   [5 Veja também](#Veja_também)

## Gerando locales

Nomes de locales geralmente possuem a forma `idioma[território][.código][@modificador]`, sendo *idioma* um [código de idiomas da ISO 639](https://en.wikipedia.org/wiki/pt:ISO_639 "w:pt:ISO 639"), *território* um [código de países da ISO 3166](https://en.wikipedia.org/wiki/pt:ISO_3166-1#Current_codes "w:pt:ISO 3166-1") e *.código* uma [codificação de caracteres](https://en.wikipedia.org/wiki/pt:Codifica%C3%A7%C3%A3o_de_caracteres "w:pt:Codificação de caracteres") ou identificador de codificação como [ISO-8859-1](https://en.wikipedia.org/wiki/pt:ISO/IEC_8859-1 "w:pt:ISO/IEC 8859-1") ou [UTF-8](https://en.wikipedia.org/wiki/pt:UTF-8 "w:pt:UTF-8"). Veja [setlocale(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setlocale.3).

Para uma lista de locales habilitados, execute:

```
$ locale -a

```

Antes que um locale possa ser habilitado no sistema, ele deve ser gerado. Isso pode ser alcançado descomentando as entradas corretas em `/etc/locale.gen` e executando *locale-gen*. Da mesma forma, comentar entradas desabilita seus respectivos locales. Ao fazer alterações, considere quaisquer localizações necessárias para outros usuários no sistema, bem como [#Variáveis](#Variáveis) específicas.

Por exemplo, descomente `pt_BR.UTF-8 UTF-8` para português brasileiro:

 `/etc/locale.gen` 
```
...
#ps_AF UTF-8  
pt_BR.UTF-8 UTF-8  
#pt_BR ISO-8859-1
...

```

Salve o arquivo e gere o locale:

```
# locale-gen

```

**Nota:**

*   `locale-gen` também é executado em toda atualização de [glibc](https://www.archlinux.org/packages/?name=glibc). [[1]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/glibc.install?h=packages/glibc#n5)
*   `UTF-8` é recomendado sobre outras codificações de caracteres. [[2]](http://utf8everywhere.org/)

## Configurando o locale

Para exibir o locale atualmente configurado e suas configurações ambientais relacionadas, digite:

```
$ locale

```

O locale a ser usado, escolhido dentre os previamente gerados, é configurado em arquivos `locale.conf`. Cada um desses arquivos deve conter uma lista, separada por nova linha, de atribuições de [variáveis de ambiente](/index.php/Vari%C3%A1veis_de_ambiente "Variáveis de ambiente"), tendo o mesmo formato que a saída de *locale*.

Para listar os locales disponíveis que foram gerados previamente, execute:

```
$ localedef --list-archive

```

Alternativamente, use [localectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/localectl.1):

```
$ localectl list-locales

```

### Configurando o locale do sistema

Para configurar o locale do sistema, escreva variável `LANG` no `/etc/locale.conf`, sendo que `*pt_BR.UTF-8*` pertence à **primeira coluna** de uma entrada não comentada em `/etc/locale.gen`:

 `/etc/locale.conf`  `LANG=*pt_BR.UTF-8*` 

Alternativamente, execute:

```
# localectl set-locale LANG=*pt_BR.UTF-8*

```

Veja [#Variáveis](#Variáveis) e [locale.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.conf.5) para detalhes.

### Sobrepondo locale do sistema por sessão de usuário

O locale para todo sistema pode ser sobrescrito em cada sessão de usuário criando ou editando `~/.config/locale.conf` (ou, em geral, `$XDG_CONFIG_HOME/locale.conf` ou `$HOME/.config/locale.conf`).

A precedência desses arquivos `locale.conf` é configurada em `/etc/profile.d/locale.sh`.

**Dica:**

*   Isso também pode permitir manter os logs em `/var/log` em inglês enquanto usa o idioma local na variável do usuário.
*   Você pode criar um arquivo `/etc/skel/.config/locale.conf` para que qualquer novos usuários adicionados usando *useradd* e a opção `-m` vai ter `~/.config/locale.conf` gerado automaticamente.

### Fazer alterações de locale imediatas

Uma vez que os arquivos `locale.conf` de sistema e de usuários terem sido criados ou editados, seus novos valores terão efeito para novas sessões na autenticação. Para fazer o ambiente atual usar as novas configurações, desconfigure `LANG` e carregue `/etc/profile.d/locale.sh`:

```
$ unset LANG
$ source /etc/profile.d/locale.sh

```

**Nota:** A variável `LANG` tem que ser desconfigurada primeiro, do contrário `locale.sh` não vai atualizar os valores de `locale.conf`. Apenas variáveis novas e alteradas serão atualizadas; variáveis removidas de `locale.conf` ainda estão configuradas na sessão.

### Outros usos

As variáveis de locale também podem ser definidas com os métodos padrão como explicado em [Variáveis de ambiente](/index.php/Vari%C3%A1veis_de_ambiente "Variáveis de ambiente").

Por exemplo, para testar ou depurar um aplicativo em particular durante o desenvolvimento, ele poderia ser iniciado com alguma coisa como:

```
$ LANG=C ./meu_aplicativo.sh

```

Da mesma forma, para definir o locale para todos os processo executados pela shell atual (por exemplo, durante a instalação do sistema):

```
$ export LANG=C

```

## Variáveis

Os arquivos `locale.conf` oferecem suporte às seguintes variáveis de ambiente:

*   [LANG](#LANG:_locale_padrão)
*   [LANGUAGE](#LANGUAGE:_locales_reservas)
*   `LC_ADDRESS`
*   [LC_COLLATE](#LC_COLLATE:_colação)
*   `LC_CTYPE`
*   `LC_IDENTIFICATION`
*   `LC_MEASUREMENT`
*   `LC_MESSAGES`
*   `LC_MONETARY`
*   `LC_NAME`
*   `LC_NUMERIC`
*   `LC_PAPER`
*   `LC_TELEPHONE`
*   [LC_TIME](#LC_TIME:_formato_de_data_e_hora)

O significado completo das variáveis `LC_*` acima pode ser localizado na página man [locale(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.7), enquanto os detalhes de suas definições estão descritas em [locale(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.5).

### LANG: locale padrão

O locale configurado para essa variável será usado para todas as variáveis `LC_*` que não forem configuradas explicitamente.

### LANGUAGE: locales reservas

Os programas que usam [gettext](https://www.archlinux.org/packages/?name=gettext) para traduções respeitam a opção `LANGUAGE` além das variáveis usuais. Isso permite que usuários para especificar uma [lista](http://www.gnu.org/software/gettext/manual/gettext.html#The-LANGUAGE-variable) de locales que serão usados naquela ordem. Se uma tradução para o locale preferido não está disponível, outro de um locale similar será usado em vez do padrão. Por exemplo, um usuário australiano pode querer usar a ortografia britânica em vez da americana:

 `locale.conf` 
```
LANG=en_AU.UTF-8
LANGUAGE=en_AU:en_GB:en
```

### LC_TIME: formato de data e hora

Se `LC_TIME` estiver configurado para `en_US.UTF-8`, por exemplo, o formato de data será "MM/DD/AAAA". Caso prefira usar o formato de data da ISO 8601 de "AAAA-MM-DD", use:

 `locale.conf`  `LC_TIME=en_DK.UTF-8` 
**Nota:** Os programas não necessariamente respeitam essa variável para formatar a data. Por exemplo, [date(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/date.1) usa seus próprios parâmetros para fazê-lo.

### LC_COLLATE: colação

Essa variável governa as regras de colação usadas para ordenação e expressões regulares.

Configurar o valor para `C` pode, por exemplo, fazer o comando *ls* ordenar arquivos iniciados com ponto primeiro, seguidos por nomes de arquivos em maiúsculo e minúsculo:

 `locale.conf`  `LC_COLLATE=C` 

Veja também [[3]](http://superuser.com/a/448294/175967).

Para evitar problemas potenciais, o Arch costumava definir `LC_COLLATE=C` em `/etc/profile`, mas esse método está agora obsoleto.

### LC_ALL: solução de problemas

O locale configurado para essa variável sempre sobrescreverá `LANG` e todas outras variáveis `LC_*`, independentemente de estarem definidas ou não.

`LC_ALL` é a única variável `LC_*` que **não pode** ser definida em arquivos `locale.conf`: ela é feita para ser usada apenas para propósito de testar ou solucionar problemas, por exemplo, em `/etc/profile`.

## Solução de problemas

### Meu terminal não possui suporte a UTF-8

A lista a seguir mostra alguns (não todos) terminais que oferecem suporte a UTF-8:

*   gnustep-terminal
*   konsole
*   [mlterm](/index.php/Mlterm "Mlterm")
*   [rxvt-unicode](/index.php/Rxvt-unicode "Rxvt-unicode")
*   [st](/index.php/St "St")
*   [termite](/index.php/Termite "Termite")
*   [VTE-based terminals](/index.php/List_of_applications/Utilities#VTE-based "List of applications/Utilities")
*   [xterm](/index.php/Xterm "Xterm") - Execute com o argumento `-u8` ou configure o recurso `xterm*utf8: 2`.

#### Gnome-terminal ou rxvt-unicode

Você precisa iniciar esses aplicativos a partir de um locale UTF-8 ou eles não terão suporte a UTF-8\. Habilite o locale `pt_BR.UTF-8` (ou sua alternativa UTF-8 local) com as instruções acima e configure-o como o locale padrão, então reinicie.

### Meu sistema ainda está usando o idioma errado

É possível que as variáveis de ambiente sejam redefinidas em outros arquivos além de `locale.conf`, por exemplo `~/.pam_environment`. Veja [Variáveis de ambiente#Definindo variáveis](/index.php/Vari%C3%A1veis_de_ambiente#Definindo_variáveis "Variáveis de ambiente") para detalhes.

Se você está usando um ambiente gráfico, como o [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)"), suas configurações de idioma podem estar sobrescrevendo as configurações em `locale.conf`.

[KDE](/index.php/KDE "KDE") Plasma também permite alterar o idioma da interface de usuário por meio de configurações do sistema. Se o ambiente gráfico ainda está usando o idioma padrão após a modificação, [excluir o arquivo em](https://bbs.archlinux.org/viewtopic.php?pid=1435219#p1435219) `~/.config/plasma-localerc` (anteriormente: `~/.config/plasma-locale-settings.sh`) deve resolver o problema.

## Veja também

*   [Gentoo:Localization/Guide](https://wiki.gentoo.org/wiki/Localization/Guide "gentoo:Localization/Guide")
*   [Artigo wiki do Gentoo supostamente de 2008, ou anterior](http://wikigentoo.ksiezyc.pl/Locales.htm)
*   [Teste de colação interativa da ICU](http://demo.icu-project.org/icu-bin/locexp?_=en_US&x=col)
*   [Free Standards Group Open Internationalisation Initiative](http://www.openi18n.org/)
*   [*The Single UNIX Specification* definição de Locale](http://pubs.opengroup.org/onlinepubs/007908799/xbd/locale.html) por The Open Group
*   [Variáveis de ambiente de local](https://help.ubuntu.com/community/EnvironmentVariables#Locale_setting_variables)