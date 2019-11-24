**Status de tradução:** Esse artigo é uma tradução de [Visual Studio Code](/index.php/Visual_Studio_Code "Visual Studio Code"). Data da última tradução: 2019-11-21\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Visual_Studio_Code&diff=0&oldid=589629) na versão em inglês.

[Visual Studio Code](https://code.visualstudio.com/) é um editor de texto de plataforma cruzada, livre e de código aberto (licenciado sob a licença MIT) desenvolvido pela Microsoft e escrito em JavaScript e TypeScript. Ele é construído sobre a estrutura Electron e é extensível usando extensões, que podem ser navegadas [na web](https://marketplace.visualstudio.com/VSCode) ou de dentro do próprio editor de texto. Enquanto o projeto é de código aberto, uma compilação proprietária (licenciada sob um Contrato de Licença de Usuário Final) também é fornecida pela Microsoft. Para obter uma explicação do licenciamento misto, consulte [este comentário no GitHub](https://github.com/Microsoft/vscode/issues/60#issuecomment-161792005).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Uso](#Uso)
*   [3 Configuração](#Configuração)
    *   [3.1 Terminal Integrado](#Terminal_Integrado)
    *   [3.2 Terminal externo](#Terminal_externo)
*   [4 Solução de problemas](#Solução_de_problemas)
    *   [4.1 O menu global não funciona no KDE/Plasma](#O_menu_global_não_funciona_no_KDE/Plasma)
    *   [4.2 Não foi possível mover itens para a lixeira](#Não_foi_possível_mover_itens_para_a_lixeira)
    *   [4.3 Falha ao depurar C#](#Falha_ao_depurar_C#)
    *   [4.4 Falha ao abrir .csproj com servidor OmniSharp, local inválido de Microsoft.Common.props](#Falha_ao_abrir_.csproj_com_servidor_OmniSharp,_local_inválido_de_Microsoft.Common.props)
    *   [4.5 Erro do OmniSharp que "MSBuild cannot be located"](#Erro_do_OmniSharp_que_"MSBuild_cannot_be_located")
    *   [4.6 Não é possível salvar com "Retry as Sudo"](#Não_é_possível_salvar_com_"Retry_as_Sudo")

## Instalação

Os seguintes pacotes fornecem VSCode:

*   [code](https://www.archlinux.org/packages/?name=code) (lançamento de código aberto)
*   [visual-studio-code-bin](https://aur.archlinux.org/packages/visual-studio-code-bin/) (Lançamento da marca Microsoft)
*   [visual-studio-code-insiders](https://aur.archlinux.org/packages/visual-studio-code-insiders/) (Lançamento da marca Microsoft, atualizado diariamente)
*   [code-git](https://aur.archlinux.org/packages/code-git/) (versão de código aberto em desenvolvimento)
*   [vscodium-bin](https://aur.archlinux.org/packages/vscodium-bin/) (outra versão de código aberto com uma configuração padrão orientada pela comunidade)

Um servidor/módulo da Microsoft [ptvsd](https://github.com/microsoft/ptvsd) (Python Tools for Visual Studio Debug) está disponível em [python-ptvsd](https://aur.archlinux.org/packages/python-ptvsd/).

## Uso

Execute o `code` para iniciar o aplicativo (ou `code-git` ao usar o [code-git](https://aur.archlinux.org/packages/code-git/)).

Se, por qualquer motivo, você desejar iniciar várias instâncias do Visual Studio Code, o sinalizador `-n` poderá ser usado.

## Configuração

[code](https://www.archlinux.org/packages/?name=code) armazena configurações em `~/.config/Code - OSS/User/settings.json`.

[visual-studio-code-bin](https://aur.archlinux.org/packages/visual-studio-code-bin/) armazena configurações em `~/.config/Code/User/settings.json`.

### Terminal Integrado

*View > Integrated Terminal* ou `Ctrl + `` abre um terminal integrado. Por padrão, [Bash](/index.php/Bash "Bash") é usado sem argumentos adicionais, embora isso possa ser alterado. `terminal.integrated.shell.linux` define o shell padrão a ser usado e `terminal.integrated.shellArgs.linux` define os argumentos a serem passados para o shell.

Exemplo:

 `~/.config/Code/User/settings.json` 
```
"terminal.integrated.shell.linux": "/usr/bin/fish",
"terminal.integrated.shellArgs.linux": ["-l","-d 3"]

```

### Terminal externo

Se você estiver usando [Terminator](/index.php/Terminator "Terminator") como terminal padrão para o Arch e tiver um erro no Código do Visual Studio: `Não é possível iniciar o processo do depurador (vsdbg) através do terminal. spawn truecolor ENOENT`, você pode alterar o terminal que será usado pelo Visual Studio para outro terminal (por exemplo,[gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal)).

`"terminal.external.linuxExec": "Yours alternative terminal"` define o terminal padrão a ser usado para depuração da execução.

Exemplo:

 `~/.config/Code/User/settings.json` 
```
"terminal.external.linuxExec": "gnome-terminal"

```

## Solução de problemas

### O menu global não funciona no KDE/Plasma

O Visual Studio Code usa o DBus para passar o menu para o plasma, tente instalar [libdbusmenu-glib](https://www.archlinux.org/packages/?name=libdbusmenu-glib)

### Não foi possível mover itens para a lixeira

Por padrão, [Electron](https://electron.atom.io/) os aplicativos usam `gio` para excluir arquivos. Diferentes implementações de lixo podem ser usadas configurando a [variável de ambiente](/index.php/Vari%C3%A1vel_de_ambiente "Variável de ambiente") `ELECTRON_TRASH`.

Por exemplo, para excluir arquivos no [Plasma](/index.php/Plasma_(Portugu%C3%AAs) "Plasma (Português)"):

```
$ ELECTRON_TRASH=kioclient5 code

```

No momento da redação deste artigo, o Electron possui suporte a `kioclient5`, `kioclient`, `trash-cli`, `gio` (padrão) e `gvfs-trash` (descontinuado). Mais informações estão disponíveis nesta [página de documentação](https://github.com/electron/electron/blob/master/docs/api/environment-variables.md#electron_trash-linux).

### Falha ao depurar C#

Se você deseja depurar o C#[.NET](/index.php/.NET_Core_(Portugu%C3%AAs) ".NET Core (Português)") (usando a [extensão OmniSharp](http://www.omnisharp.net)), será necessário instalar o lançamento com a marca da Microsoft (do AUR). Aparentemente, isso ocorre porque o depurador do .NET Core é licenciado apenas para ser usado com os produtos oficiais da Microsoft - consulte [https://github.com/OmniSharp/omnisharp-vscode/issues/1431#issuecomment-297578930](https://github.com/OmniSharp/omnisharp-vscode/issues/1431#issuecomment-297578930)

Usando o pacote de código aberto, a depuração falha bastante silenciosamente. O console de depuração mostrará apenas a mensagem inicial e nada mais:

```
You may only use the Microsoft .NET Core Debugger (vsdbg) with
Visual Studio Code, Visual Studio or Visual Studio for Mac software
to help you develop and test your applications.
```

Mas de outra maneira, você pode usar [netcoredbg](https://github.com/Samsung/netcoredbg),[netcoredbg](https://aur.archlinux.org/packages/netcoredbg/)

### Falha ao abrir .csproj com servidor OmniSharp, local inválido de Microsoft.Common.props

É necessário alternar dos adereços da versão mono para os adequados da versão SDK:

 `/opt/dotnet/sdk/{VERSION}/Sdks/Microsoft.NET.Sdk/Sdk/Sdk.props` 
```
$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\Microsoft.Common.props

```

Modifique a importação para ficar assim:

 `/opt/dotnet/sdk/{VERSION}/Sdks/Microsoft.NET.Sdk/Sdk/Sdk.props` 
```
/opt/dotnet/sdk/{VERSION}/Current/Microsoft.Common.props

```

### Erro do OmniSharp que "MSBuild cannot be located"

Notou-se na [introdução do OmniSharp](https://github.com/OmniSharp/omnisharp-roslyn#introduction) que os usuários do Arch Linux devem instalar o pacote [msbuild-stable](https://aur.archlinux.org/packages/msbuild-stable/). Sem ele, você pode receber um erro como:

 `OmniSharp Log` 
```
[info]: OmniSharp.MSBuild.Discovery.MSBuildLocator
        Registered MSBuild instance: StandAlone 15.0 - "~/.vscode/extensions/ms-vscode.csharp-1.18.0/.omnisharp/1.32.11/omnisharp/msbuild/15.0/Bin"
            MSBuildExtensionsPath = /usr/lib/mono/xbuild
            BypassFrameworkInstallChecks = true
            CscToolPath = ~/.vscode/extensions/ms-vscode.csharp-1.18.0/.omnisharp/1.32.11/omnisharp/msbuild/15.0/Bin/Roslyn
            CscToolExe = csc.exe
            MSBuildToolsPath = ~/.vscode/extensions/ms-vscode.csharp-1.18.0/.omnisharp/1.32.11/omnisharp/msbuild/15.0/Bin
            TargetFrameworkRootPath = /usr/lib/mono/xbuild-frameworks
System.TypeLoadException: Could not load type of field 'OmniSharp.MSBuild.ProjectManager:_queue' (13) due to: Could not load file or assembly 'System.Threading.Tasks.Dataflow, Version=4.5.24.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a' or one of its dependencies.
...
```

Você pode construir de qualquer maneira (possivelmente dependendo se você tem o [mono](https://www.archlinux.org/packages/?name=mono) instalado)

### Não é possível salvar com "Retry as Sudo"

Esse recurso não funciona no pacote [code](https://www.archlinux.org/packages/?name=code), porque a Microsoft não suporta a maneira como o pacote Arch é empacotado (nativo em vez do Electron incluído). Veja [FS#61516](https://bugs.archlinux.org/task/61516) e o [relatório de erro do upstream](https://github.com/Microsoft/vscode/issues/70403) para obter mais informações.

O lançamento binário [visual-studio-code-bin](https://aur.archlinux.org/packages/visual-studio-code-bin/) não possui esse problema, e o recurso funciona lá.