Artigos relacionados

*   [xdg-menu](/index.php/Xdg-menu "Xdg-menu")
*   [Aplicativos padrão](/index.php/Default_applications "Default applications")
*   [Suporte a XDG Base Directory](/index.php/XDG_Base_Directory_support "XDG Base Directory support")

Do [freedesktop.org](https://www.freedesktop.org/wiki/Software/xdg-user-dirs/):

	xdg-user-dirs é uma ferramenta para ajudar a gerenciar diretórios de usuário "bem conhecidos", como a pasta de área de trabalho e a pasta de música. Também lida com localização (isto é, tradução) dos nomes de arquivo.

	A maneira como funciona é que o [xdg-user-dirs-update(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdg-user-dirs-update.1) é executado muito cedo na fase de login. Este programa lê um arquivo de configuração e um conjunto de diretórios padrão. Em seguida, ele cria versões localizadas desses diretórios no diretório inicial dos usuários e configura um arquivo de configuração em `$XDG_CONFIG_HOME/user-dirs.dirs` (XDG_CONFIG_HOME tem como padrão ~/.config) que os aplicativos podem ler para localizar esses diretórios.

A maioria dos [gerenciadores de arquivo](/index.php/File_manager "File manager") indicam diretórios de usuário XDG com ícones especiais.

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