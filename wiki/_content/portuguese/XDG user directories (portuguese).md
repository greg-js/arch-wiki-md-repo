Artigos relacionados

*   [xdg-menu](/index.php/Xdg-menu "Xdg-menu")
*   [Aplicativos padrão](/index.php/Default_applications "Default applications")
*   [Suporte a XDG Base Directory](/index.php/XDG_Base_Directory_support "XDG Base Directory support")

*User directories* (diretórios de usuários) são um conjunto de diretórios comuns de usuário localizados dentro do diretório `$HOME`, incluindo `Documents`, `Downloads`, `Music` e `Desktop`. Em português, esses diretórios são chamados de `Documentos`, `Downloads`, `Música` e `Área de trabalho`, respectivamente. Identificados por ícones únicos de um gerenciador de arquivos, eles normalmente serão carregados automaticamente por vários programas e aplicativos. [xdg-user-dirs](https://www.archlinux.org/packages/?name=xdg-user-dirs) é um programa que vão gerar automaticamente esses diretórios. Veja o site do [freedesktop.org](https://www.freedesktop.org/wiki/Software/xdg-user-dirs) para informação adicional.

**Dica:** Esse programa será especialmente útil para aqueles que desejam usar um gerenciador de arquivos para gerenciar seu desktop para um [Gerenciador de janela](/index.php/Gerenciador_de_janela "Gerenciador de janela") como o [Openbox](/index.php/Openbox "Openbox"), pois ele também vai criar automaticamente um diretório `~/Desktop` ou, em português, `~/'Área de trabalho'`.

## Criando diretórios padrão

A criação de um conjunto completo de diretórios de usuários padrão localizados dentro do diretório `$HOME` pode ser feito automaticamente usando [xdg-user-dirs](https://www.archlinux.org/packages/?name=xdg-user-dirs) e executando:

```
$ xdg-user-dirs-update

```

**Dica:** Para forçar a criação de diretórios com nome em inglês, `LC_ALL=C xdg-user-dirs-update` pode ser usado.

Quando executado, ele também vai automaticamente:

*   Criar um arquivo de configuração local `~/.config/user-dirs.dirs`: usado por aplicativos para localizar e usar diretórios *home* específicos para uma conta.
*   Criar um arquivo de configuração local `~/.config/user-dirs.locale`: usado para definir o idioma conforme o *locale* em uso.

## Criando diretórios personalizados

Ambos os arquivos de configuração local `~/.config/user-dirs.dirs` e o global `/etc/xdg/user-dirs.defaults` usam o seguinte formato de variável de ambiente para apontar para diretórios de usuário: `XDG_DIRNAME_DIR="$HOME/nome_do_diretório"`. Um arquivo de configuração vai/pode se parecer com esse exemplo abaixo (esses são diretórios modelo):

 `~/.config/user-dirs.dirs` 
```
XDG_DESKTOP_DIR="$HOME/Área de trabalho"
XDG_DOWNLOAD_DIR="$HOME/Downloads"
XDG_TEMPLATES_DIR="$HOME/Modelos"
XDG_PUBLICSHARE_DIR="$HOME/Público"
XDG_DOCUMENTS_DIR="$HOME/Documentos"
XDG_MUSIC_DIR="$HOME/Música"
XDG_PICTURES_DIR="$HOME/Imagens"
XDG_VIDEOS_DIR="$HOME/Vídeos"
```

Como [xdg-user-dirs](https://www.archlinux.org/packages/?name=xdg-user-dirs) vai carregar o arquivo de configuração local para apontar para os diretórios de usuário apropriados, é então possível especificar pastas personalizadas. Por exemplo, se uma pasta personalizada para a variável `XDG_DOWNLOAD_DIR` tiver sido nomeada `$HOME/Internet` no `~/.config/user-dirs.dirs`, qualquer aplicativo que usa essa variável vai usar esse diretório.

**Nota:** Como com muitos arquivos de configuração, as configurações locais substituem as configurações globais. Também será necessário criar novos diretórios personalizados.

Alternativamente, também é possível especificar pastas personalizadas usando a linha de comando. Por exemplo, o seguinte comando produzirá os mesmos resultados que a edição do arquivo de configuração acima:

```
$ xdg-user-dirs-update --set DOWNLOAD ~/Internet

```

## Consultando diretórios configurados

Uma vez definido, qualquer diretório de usuário pode ser visto com [xdg-user-dirs](https://www.archlinux.org/packages/?name=xdg-user-dirs). Por exemplo, o comando a seguir vai mostrar a localização do diretório `Templates` (em português, `Modelos`), que, é claro, corresponde à variável `XDG_TEMPLATES_DIR` no arquivo de configuração local:

```
$ xdg-user-dir TEMPLATES

```