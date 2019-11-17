[Visual Studio Code](https://code.visualstudio.com/) é um editor de texto de plataforma cruzada, gratuito e de código aberto (licenciado sob a licença MIT) desenvolvido pela Microsoft e escrito em JavaScript e TypeScript. Ele é construído sobre a estrutura Electron e é extensível usando extensões, que podem ser navegadas [on the web](https://marketplace.visualstudio.com/VSCode) ou de dentro do próprio editor de texto. Enquanto o projeto é de código aberto, uma compilação proprietária (licenciada sob um Contrato de Licença de Usuário Final) também é fornecida pela Microsoft. Para obter uma explicação do licenciamento misto, consulte [this GitHub comment](https://github.com/Microsoft/vscode/issues/60#issuecomment-161792005).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Uso](#Uso)
*   [3 Configuração](#Configuração)
    *   [3.1 Terminal Integrado](#Terminal_Integrado)
    *   [3.2 Terminal externo](#Terminal_externo)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 O menu global não funciona no KDE / Plasma](#O_menu_global_não_funciona_no_KDE_/_Plasma)
    *   [4.2 Não foi possível mover itens para a lixeira](#Não_foi_possível_mover_itens_para_a_lixeira)
    *   [4.3 Unable to debug C#](#Unable_to_debug_C#)
    *   [4.4 Unable to open .csproj with OmniSharp server, invalid Microsoft.Common.props location](#Unable_to_open_.csproj_with_OmniSharp_server,_invalid_Microsoft.Common.props_location)
    *   [4.5 Error from OmniSharp that MSBuild cannot be located](#Error_from_OmniSharp_that_MSBuild_cannot_be_located)
    *   [4.6 Saving with "Retry as Sudo" does not work](#Saving_with_"Retry_as_Sudo"_does_not_work)

## Instalação

Os seguintes pacotes fornecem VSCode:

*   [code](https://www.archlinux.org/packages/?name=code) (open-source release)
*   [visual-studio-code-bin](https://aur.archlinux.org/packages/visual-studio-code-bin/) (Microsoft-branded release)
*   [visual-studio-code-insiders](https://aur.archlinux.org/packages/visual-studio-code-insiders/) (Microsoft-branded release, updated daily)
*   [code-git](https://aur.archlinux.org/packages/code-git/) (in-development open-source version)
*   [vscodium-bin](https://aur.archlinux.org/packages/vscodium-bin/) (another open-source version with a community-driven default configuration)

Um servidor/módulo da Microsoft [ptvsd](https://github.com/microsoft/ptvsd) (Python Tools for Visual Studio Debug) está disponível em [python-ptvsd](https://aur.archlinux.org/packages/python-ptvsd/).

## Uso

Execute o `code` para iniciar o aplicativo (ou `code-git` ao usar o [code-git](https://aur.archlinux.org/packages/code-git/)).

Se, por qualquer motivo, você desejar iniciar várias instâncias do Visual Studio Code, o sinalizador `-n` poderá ser usado.

## Configuração

[code](https://www.archlinux.org/packages/?name=code) armazena configurações em `~/.config/Code - OSS/User/settings.json`.

[visual-studio-code-bin](https://aur.archlinux.org/packages/visual-studio-code-bin/) armazena configurações em `~/.config/Code/User/settings.json`.

### Terminal Integrado

*View > Integrated Terminal* ou `Ctrl + `` abre um terminal integrado. Por padrão, [Bash](/index.php/Bash "Bash") é usado sem argumentos adicionais, embora isso possa ser alterado. `terminal.integrated.shell.linux` define o shell padrão a ser usado e `terminal.integrated.shellArgs.linux` defina os argumentos a serem passados para o shell.

Exemplo:

 `~/.config/Code/User/settings.json` 
```
"terminal.integrated.shell.linux": "/usr/bin/fish",
"terminal.integrated.shellArgs.linux": ["-l","-d 3"]

```

### Terminal externo

Se você estiver usando **Terminator** como terminal padrão para o Arch e tiver um erro no Código do Visual Studio: `Não é possível iniciar o processo do depurador (vsdbg) através do terminal. spawn truecolor ENOENT`, você pode alterar o terminal que será usado pelo Visual Studio para outro terminal (por exemplo, gnome-terminal).

`"terminal.external.linuxExec": "Yours alternative terminal"` define o terminal padrão a ser usado para depuração executiva.

Exemplo:

 `~/.config/Code/User/settings.json` 
```
"terminal.external.linuxExec": "gnome-terminal"

```

## Troubleshooting

### O menu global não funciona no KDE / Plasma

O Visual Studio Code usa o DBus para passar o menu para o plasma, tente instalar [libdbusmenu-glib](https://www.archlinux.org/packages/?name=libdbusmenu-glib)

### Não foi possível mover itens para a lixeira

Por padrão, [Electron](https://electron.atom.io/) os aplicativos usam `gio` para excluir arquivos. Diferentes implementações de lixo podem ser usadas configurando a `ELECTRON_TRASH` [environment variable](/index.php/Environment_variable "Environment variable").

Por exemplo, para excluir arquivos em [Plasma](/index.php/Plasma "Plasma"):

```
$ ELECTRON_TRASH=kioclient5 code

```

At the time of writing, Electron supports `kioclient5`, `kioclient`, `trash-cli`, `gio` (default) and `gvfs-trash` (deprecated). More info is available at this [documentation page](https://github.com/electron/electron/blob/master/docs/api/environment-variables.md#electron_trash-linux).

### Unable to debug C#

If you want to debug C#[.NET](/index.php/.NET_Core ".NET Core") (using the [OmniSharp extension](http://www.omnisharp.net)) then you need to install the Microsoft branded release (from the AUR). This is apparently because the .NET Core debugger is only licensed to be used with official Microsoft products - see [https://github.com/OmniSharp/omnisharp-vscode/issues/1431#issuecomment-297578930](https://github.com/OmniSharp/omnisharp-vscode/issues/1431#issuecomment-297578930)

Using the the open-source package, debugging fails fairly quietly. The debug console will just show the initial message and nothing more:

```
You may only use the Microsoft .NET Core Debugger (vsdbg) with
Visual Studio Code, Visual Studio or Visual Studio for Mac software
to help you develop and test your applications.
```

But in another way, you can use [netcoredbg](https://github.com/Samsung/netcoredbg),[netcoredbg](https://aur.archlinux.org/packages/netcoredbg/)

### Unable to open .csproj with OmniSharp server, invalid Microsoft.Common.props location

You have to switch from mono to proper SDK version props.

 `/opt/dotnet/sdk/{VERSION}/Sdks/Microsoft.NET.Sdk/Sdk/Sdk.props` 
```
$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\Microsoft.Common.props

```

Modify import to look like this:

 `/opt/dotnet/sdk/{VERSION}/Sdks/Microsoft.NET.Sdk/Sdk/Sdk.props` 
```
/opt/dotnet/sdk/{VERSION}/Current/Microsoft.Common.props

```

### Error from OmniSharp that MSBuild cannot be located

It's noted in the [OmniSharp introduction](https://github.com/OmniSharp/omnisharp-roslyn#introduction) that Arch Linux users should install the [msbuild-stable](https://aur.archlinux.org/packages/msbuild-stable/) package. Without it, you might get an error like:

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

You might be able to build anyway (possibly depending whether you have [mono](https://www.archlinux.org/packages/?name=mono) installed too)

### Saving with "Retry as Sudo" does not work

This feature does not work in the [code](https://www.archlinux.org/packages/?name=code) package, because Microsoft does not support the way the Arch package is packaged (native instead of bundled Electron). See [FS#61516](https://bugs.archlinux.org/task/61516) and the [upstream bug report](https://github.com/Microsoft/vscode/issues/70403) for more information.

The binary release [visual-studio-code-bin](https://aur.archlinux.org/packages/visual-studio-code-bin/) does not have this issue, and the feature works there.