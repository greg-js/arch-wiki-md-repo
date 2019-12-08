**Status de tradução:** Esse artigo é uma tradução de [Flatpak](/index.php/Flatpak "Flatpak"). Data da última tradução: 2019-08-09\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Flatpak&diff=0&oldid=23769) na versão em inglês.

Artigos relacionados

*   [Snapd](/index.php/Snapd "Snapd")
*   [bubblewrap](/index.php/Bubblewrap "Bubblewrap")

Do [README](https://github.com/flatpak/flatpak/blob/master/README.md) do projeto: "*[Flatpak](http://flatpak.org) é um sistema para construção, distribuição e execução de aplicações desktop sandboxed no Linux.*"

De [flatpak(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/flatpak.1):

	*Flatpak é uma ferramenta para gerenciar aplicações e os runtimes que elas usam. No modelo Flatpak, aplicações podem ser construídas e distribuídas independentemente do sistema hospedeiro em que elas estão usando, e elas são isoladas do sistema hospedeiro (‘sandboxed’) em algum grau, no runtime.*

	*Flatpak usa [OSTree](https://ostree.readthedocs.io/en/latest/) para distribuir e implantar dados. Os repositórios que ele usa são repositórios OSTree e podem ser manipulados com a ferramenta ostree. Runtimes instalados e aplicações são checkouts do OSTree.*

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Gerenciar repositórios](#Gerenciar_repositórios)
    *   [2.1 Adicionar um repositório](#Adicionar_um_repositório)
    *   [2.2 Deletar repositórios](#Deletar_repositórios)
    *   [2.3 Listar repositórios](#Listar_repositórios)
*   [3 Gerenciar runtimes e aplicações](#Gerenciar_runtimes_e_aplicações)
    *   [3.1 Procurar por um runtime ou aplicação](#Procurar_por_um_runtime_ou_aplicação)
    *   [3.2 Listar todos os runtime ou aplicações disponíveis](#Listar_todos_os_runtime_ou_aplicações_disponíveis)
    *   [3.3 Instalar um runtine ou aplicação](#Instalar_um_runtine_ou_aplicação)
    *   [3.4 Listar os runtimes e aplicações instalados](#Listar_os_runtimes_e_aplicações_instalados)
    *   [3.5 Rodar aplicações](#Rodar_aplicações)
    *   [3.6 Atualizar um runtime ou aplicação](#Atualizar_um_runtime_ou_aplicação)
    *   [3.7 Desinstalar um runtime ou aplicação](#Desinstalar_um_runtime_ou_aplicação)
    *   [3.8 Adicionando arquivos .desktop Flatpak ao seu menu](#Adicionando_arquivos_.desktop_Flatpak_ao_seu_menu)
    *   [3.9 Vendo as permissões sandbox da aplicação](#Vendo_as_permissões_sandbox_da_aplicação)
    *   [3.10 Sobrescrevendo permissões sandbox de aplicações](#Sobrescrevendo_permissões_sandbox_de_aplicações)
*   [4 Criar uma base de runtime customizada](#Criar_uma_base_de_runtime_customizada)
    *   [4.1 Criar aplicativos com o pacman](#Criar_aplicativos_com_o_pacman)
*   [5 Veja também](#Veja_também)

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [flatpak](https://www.archlinux.org/packages/?name=flatpak).

**Nota:** Se você quer construir flatpaks com o `flatpak-builder`, você precisará instalar as dependências opcionais [elfutils](https://www.archlinux.org/packages/?name=elfutils) e [patch](https://www.archlinux.org/packages/?name=patch).

## Gerenciar repositórios

### Adicionar um repositório

Para adicionar um repositório flatpak remoto faça:

```
$ flatpak remote-add *nome* *localização*

```

onde *nome* é o nome do novo remoto e *localização* é o caminho ou a URL do repositório.

Por exemplo, para adicionar o [repositório oficial Flathub](https://flathub.org/):

```
$ flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo

```

### Deletar repositórios

Para deletar um repositório flatpak remoto faça:

```
$ flatpak remote-delete *nome*

```

onde *nome* é o nome do repositório remoto a ser deletado.

### Listar repositórios

Para listar todos os repositórios adicionados faça:

```
$ flatpak remotes

```

## Gerenciar runtimes e aplicações

### Procurar por um runtime ou aplicação

Antes de estar pronto para procurar por um runtime ou aplicação em um novo repositório remoto adicionado, nós precisamos recuperar os dados appstream. Para isso:

 `$ flatpak update` 
```
Procurando por atualizações...
Atualizando dados appstream para remote *nome*

```

Então nós podemos proceder para procurar por um pacote com `flatpak search *nomedopacote*`, *e.g.* para procurar pelo pacote `libreoffice` com o `flathub` remoto configurado:

 `$ flatpak search libreoffice` 
```
ID de aplicativo              Versão Ramo Remotos Descrição                       
org.libreoffice.LibreOffice         stable flathub The LibreOffice productivity suite

```

### Listar todos os runtime ou aplicações disponíveis

Para listar todos os runtimes e aplicações disponíveis em um repositório remoto nomeado como *remoto* faça:

```
$ flatpak remote-ls *remoto*

```

### Instalar um runtine ou aplicação

Para instalar umruntime ou aplicação faça:

```
$ flatpak install *remoto* *nome*

```

onde *remoto* é o nome do repositório remoto e *nome* é o nome da aplicação ou runtime a ser instalado.

**Dica:** Você pode usar identificadores parciais `flatpak install *nome-parcial*` (por exemplo `flatpak install libreoffice`).

### Listar os runtimes e aplicações instalados

Para listar os runtimes e aplicações instaladas faça:

```
$ flatpak list

```

### Rodar aplicações

Aplicações Flatpak também podem ser executadas por linha de comando:

```
$ flatpak run *nome*

```

### Atualizar um runtime ou aplicação

Para atualizar um runtime ou aplicação nomeada como *nome* faça:

```
$ flatpak update *name*

```

### Desinstalar um runtime ou aplicação

Para desinstalar um runtime ou aplicação nomeado(a) como nome faça:

```
$ flatpak uninstall *name*

```

**Dica:** Você pode desinstalar flatpak “refs” não utilizado (também conhecido como orfãos sem aplicação/runtime) com `flatpak unsinstall --unused`.

### Adicionando arquivos .desktop Flatpak ao seu menu

Flatpak espera que o gerenciador de janelas respeite a variável de ambiente XDG_DATA_DIRS para descobrir aplicações. Isso pode requerer que a sessão seja reiniciada ou o lançador pode não suportar isso. Nesse caso, onde você pode editar a lista de diretórios escaneados, adicionar isso a ela:

```
~/.local/share/flatpak/exports/share/applications
/var/lib/flatpak/exports/share/applications

```

Isso é sabidamente necessário no Awesome.

### Vendo as permissões sandbox da aplicação

Aplicações Flatpak vêm com regras sandbox pré-definidas que definem quais os recursos e os caminhos do sistema de arquivos a aplicação tem permissão para acessar. Para ver as permissões de uma aplicação específica faça:

```
$ flatpak info --show-permissions *name*

```

A referência para os nomes das permissões sandbox podem ser encontradas na [documentação oficial do Flatpak.](https://docs.flatpak.org/en/latest/sandbox-permissions-reference.html/)

### Sobrescrevendo permissões sandbox de aplicações

Se você acha que as permissões pré-definidas da aplicação é muito permissiva ou muito restritiva, você pode mudar para qualquer uma que quiser usando o comando `flatpak override`. Por exemplo:

```
$ flatpak override --nofilesystem=home *name*

```

Isso irá prevenir que a aplicação acesse a sua pasta home.

Todo tipo de permissão como dispositivo, sistema de arquivo ou soquete tem um uma linha de comando que permite aquela permissão em particular e uma opção separada que nega. Por exemplo, no caso de acesso ao dispositivo `--device=device_*nome*` permite o acesso, `--no-device=device_*nome*` nega a permissão para acessar o dispositivo.

Para todos os tipos de comandos de permissão consulte a página de manual: [flatpak-override(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/flatpak-override.1).

Substituições de permissão podem ser redefinidas para o padrão com o comando:

```
$ flatpak override --reset *nome*

```

## Criar uma base de runtime customizada

**Atenção:** Se você quer lançar o seu software para o público como Flatpak, um runtime com base no Arch é inadequado. Nesse caso, você precisará seguir a [documentação oficial](http://docs.flatpak.org/) para integrar seu software ao ecossistema adequado do Flatpak usando os [runtimes comuns](http://flatpak.org/runtimes.html/).

**Nota:** Você pode querer usar uma conta não confiável e desprivilegiadas para construir software não confiável porque o software não é sandboxed durante a criação do aplicativo e do runtime.

**Nota:** Quando distribuindo pacotes para outros, você pode ser legalmente obrigado a fornecer o código fonte de alguns dos softwares empacotados mediante solicitação. Vocẽ ode querer usar [ABS](/index.php/ABS_(Portugu%C3%AAs) "ABS (Português)") para construir tais pacotes a partir da fonte.

Você pode criar uma runtime base e uma SDK base customizada com base no Arch para Flatpak usando o pacman. Você pode, então, usá-las para criação e empacotamento de aplicações. Isso é uma alternativa para uso pessoal para o padrão `org.freedesktop.BasePlatform` e `org.freedesktop.BaseSdk runtimes`.

Em adição ao [flatpak](https://www.archlinux.org/packages/?name=flatpak), você precisa ter instalado [fakeroot](https://www.archlinux.org/packages/?name=fakeroot) e [fakechroot](https://www.archlinux.org/packages/?name=fakechroot), para suportar o pacman hooks.

Primeiro, comece criando um diretório para criação do runtime e, possivelmente, aplicações.

```
$ mkdir *minhapastadecriacaoflatpak*
$ cd *minhapastadecriacaoflatpak*

```

Você pode, então, preparar o diretório para a criação da plataforma base do runtime. Os arquivos do subdiretório irão conter o que depois será o diretório `/usr` no sandbox. Portanto, você precisará criar links simbólicos para o padrão `/etc/share` etc. do Arch ainda possa ser acessado no caminho usual.

```
$ mkdir -p *meuruntime*/files/var/lib/pacman
$ touch *meuruntime*/files/.ref
$ ln -s /usr/usr/share *meuruntime*/files/share
$ ln -s /usr/usr/include *meuruntime*/files/include
$ ln -s /usr/usr/local *meuruntime*/files/local

```

Certifique-se que as fontes disponíveis pelo seu sistema operacional host para o runtime do Arch:

```
$ mkdir -p *meuruntime*/files/usr/share/fonts
$ ln -s /run/host/fonts *meuruntime*/files/usr/share/fonts/flatpakhostfonts

```

Você precisa e talvez queira adaptar o seu `pacman.conf` antes de instalar pacotes no runtime. Copie o `/etc/pacman.conf` para o seu diretório de criação e então faça as seguintes mudanças:

*   Remova a opção `CheckSpace` e então o pacman não reclamará sobre erros ao encontrar a raiz do sistema de arquivo para checar o espaço de disco.
*   Remova quaisquer repositórios customizados indesejados e as configurações `IgnorePkg`, `IgnoreGroup`, `NoUpgrade` e `NoExtract`, que são necessárias somente para o sistema hospedeiro.

Agora instale os pacotes para o runtime.

```
$ fakechroot fakeroot pacman -Syu --root *meuruntime*/files --dbpath *meuruntime*/files/var/lib/pacman --config pacman.conf base
$ mv pacman.conf *meuruntime*/files/etc/pacman.conf

```

Configure os [locales](/index.php/Locale_(Portugu%C3%AAs) "Locale (Português)") a serem usados editando `*meuruntime*/files/etc/locale.gen`. Então, gere novamente os locales do runtime.

```
$ fakechroot chroot *meuruntime*/files locale-gen

```

A SDK base pode ser criada a partir da base runtime com adição de aplicações necessárias para a criação de pacotes e executar o pacman.

```
$ cp -r *meuruntime* mysdk
$ fakechroot fakeroot pacman -S --root mysdk/files --dbpath mysdk/files/var/lib/pacman --config meusdk/files/etc/pacman.conf base-devel fakeroot fakechroot --needed

```

Insira metadados sobre runtime e SDK.

 `*meuruntime*/metadados` 
```
[Runtime]
name=org.meudominio.BasePlatform
runtime=org.meudominio.BasePlatform/x86_64/2016-06-26
sdk=org.meudominio.BaseSdk/x86_64/2016-06-26
```
 `meusdk/metadados` 
```
[Runtime]
name=org.meudominio.BaseSdk
runtime=org.meudominio.BasePlatform/x86_64/2016-06-26
sdk=org.meudominio.BaseSdk/x86_64/2016-06-26
```

Adicione as bases runtime e SDK para um repositório local no diretório atual. Você pode querer dar para eles mensagens commit apropriadas como, por exemplo, “Minha runtime base Arch” e “Minha SDK base Arch”.

```
$ ostree init --mode archive-z2 --repo=.
$ EDITOR="nano -w" ostree commit -b runtime/org.meudominio.BasePlatform/x86_64/2016-06-26 --tree=dir=*meuruntime*
$ EDITOR="nano -w" ostree commit -b runtime/org.meudominio.BaseSdk/x86_64/2016-06-26 --tree=dir=meusdk
$ ostree summary -u

```

Instale o runtime e o SDK.

```
$ flatpak remote-add --user --no-gpg-verify myarchos file://$(pwd)
$ flatpak install --user myarchos org.meudominio.BasePlatform 2016-06-26
$ flatpak install --user myarchos org.meudominio.BaseSdk 2016-06-26

```

### Criar aplicativos com o pacman

Como uma alternativa para a criação de aplicação da [forma comum](http://flatpak.org/developer.html), nós podemos usar o pacman para criar uma versão em contêiner dos pacotes comuns do Arch. Note que `/usr` é somente-leitura quando criando aplicativos, então nós não podemos usar os pacotes do Arch quando da criação de um app. Para criar um aplicativo real com o pacman, nós podemos também:

*   Usar o pacman para criar um runtime contendo todas as dependências
*   e compilar os aplicativos [como de costume](http://flatpak.org/developer.html) ou talvez usando o pacman para criar um [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") customizado e adaptado ao Flatpak, o qual usa `--prefix=/app` para o script `configure`,

ou nós podemos

*   usar o pacman para criar o runtime contendo o aplicativo instalado com o pacman
*   e criar um aplicativo dummy para executá-lo.

Por último, primeiro crie um runtime usando o pacman como esse para o [gedit](https://www.archlinux.org/packages/?name=gedit). O runtime é primeiramente inicializado e preparado para uso com o pacman.

```
$ flatpak build-init -w geditruntime org.meudominio.geditruntime org.meudominio.BaseSdk org.meudominio.BasePlatform 2016-06-26
$ flatpak build geditruntime sed -i "s/^#Server/Server/g" /etc/pacman.d/mirrorlist
$ flatpak build geditruntime ln -s /usr/var/lib /var/lib
$ flatpak build geditruntime fakeroot pacman-key --init
$ flatpak build geditruntime fakeroot pacman-key --populate archlinux

```

Então o pacote está instalado. A conexão da rede hospedeira deve estar disponível para o pacman.

```
$ flatpak build --share=network geditruntime fakechroot fakeroot pacman --root /usr -S gedit

```

Você pode testar a aplicação antes de finalizar o runtime (sem o sandboxing apropriado).

```
$ flatpak build --socket=x11 geditruntime gedit

```

Agora termine criando o runtime e exporte-o para um novo repositório local. As chaves GnuPG do pacman têm permissões que podem interferir e precisam ser removidas primeiro.

```
$ flatpak build geditruntime rm -r /etc/pacman.d/gnupg
$ flatpak build-finish geditruntime
$ sed -i "s/\[Application\]/\[Runtime\]/;s/runtime=org.meudominio.BasePlatform/runtime=org.meudominio.geditruntime/" geditruntime/metadata
$ flatpak build-export -r geditrepo geditruntime

```

Então crie o aplicativo dummy.

```
$ flatpak build-init geditapp org.gnome.gedit org.meudominio.BaseSdk org.meudominio.geditruntime

```

Agora termine criando o aplicativo dummy. Você pode ajustar as permissões de acesso quando sandboxed dando opções adicionais ao terminar de criar. Para possíveis opções veja a [documentação do Flatpak](#Veja_também) e os [arquivos de manifesto do GNOME](https://gitlab.gnome.org/GNOME/gnome-apps-nightly/tree/master/). Alternativamente, adapte `geditapp/metadata` para as suas necessidades após terminar de criar, mas antes de exportar. Quando os arquivos de metadados estiver concluído, exporte o app para o repositório.

```
$ flatpak build-finish geditapp --socket=x11 *[possivelmente outras opções]* --command=gedit
$ flatpak build-export geditrepo geditapp

```

Instale-o junto com o runtime.

```
$ flatpak --user remote-add --no-gpg-verify geditrepo geditrepo
$ flatpak install --user geditrepo org.meudominio.geditruntime
$ flatpak install --user geditrepo org.gnome.gedit
$ flatpak run org.gnome.gedit

```

## Veja também

*   [Site oficial](http://flatpak.org)
*   [Wiki oficial no GitHub](https://github.com/flatpak/flatpak/wiki)
*   [Página no Wikipédia](https://en.wikipedia.org/wiki/pt:Flatpak "wikipedia:pt:Flatpak")
*   [SandboxedApps no GNOME Wiki](https://wiki.gnome.org/Projects/SandboxedApps)
*   [Runtime e aplicativos de teste do KDE](https://community.kde.org/Guidelines_and_HOWTOs/Flatpak)