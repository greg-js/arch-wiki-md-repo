**Status de tradução:** Esse artigo é uma tradução de [Electron package guidelines](/index.php/Electron_package_guidelines "Electron package guidelines"). Data da última tradução: 2019-06-19\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Electron_package_guidelines&diff=0&oldid=573017) na versão em inglês.

**[Diretrizes de criação de pacotes](/index.php/Padr%C3%B5es_de_empacotamento_do_Arch "Padrões de empacotamento do Arch")**

* * *

[32-bit](/index.php/Diretrizes_de_pacotes_32-bit "Diretrizes de pacotes 32-bit") – [CLR](/index.php/Diretrizes_de_pacotes_CLR "Diretrizes de pacotes CLR") – [Cross](/index.php/Diretrizes_de_pacotes_de_ferramentas_de_compila%C3%A7%C3%A3o_cruzada "Diretrizes de pacotes de ferramentas de compilação cruzada") – [Eclipse](/index.php/Diretrizes_de_pacotes_de_plugin_do_Eclipse "Diretrizes de pacotes de plugin do Eclipse") – [Electron](/index.php/Diretrizes_de_pacotes_Electron "Diretrizes de pacotes Electron") – [Free Pascal](/index.php/Diretrizes_de_pacotes_Free_Pascal "Diretrizes de pacotes Free Pascal") – [GNOME](/index.php/Diretrizes_de_pacotes_GNOME "Diretrizes de pacotes GNOME") – [Go](/index.php/Diretrizes_de_pacotes_Go "Diretrizes de pacotes Go") – [Haskell](/index.php/Diretrizes_de_pacotes_Haskell "Diretrizes de pacotes Haskell") – [Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java") – [KDE](/index.php/Diretrizes_de_pacotes_KDE "Diretrizes de pacotes KDE") – [Kernel](/index.php/Diretrizes_de_pacotes_de_m%C3%B3dulos_de_kernel "Diretrizes de pacotes de módulos de kernel") – [Lisp](/index.php/Diretrizes_de_pacotes_Lisp "Diretrizes de pacotes Lisp") – [MinGW](/index.php/Diretrizes_de_pacotes_MinGW "Diretrizes de pacotes MinGW") – [Node.js](/index.php/Diretrizes_de_pacotes_Node.js "Diretrizes de pacotes Node.js") – [Nonfree](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") – [OCaml](/index.php/Diretrizes_de_pacotes_OCaml "Diretrizes de pacotes OCaml") – [Perl](/index.php/Diretrizes_de_pacotes_Perl "Diretrizes de pacotes Perl") – [PHP](/index.php/Diretrizes_de_pacotes_PHP "Diretrizes de pacotes PHP") – [Python](/index.php/Diretrizes_de_pacotes_Python "Diretrizes de pacotes Python") – [R](/index.php/Diretrizes_de_pacotes_R "Diretrizes de pacotes R") – [Ruby](/index.php/Diretrizes_de_pacotes_Ruby_Gem "Diretrizes de pacotes Ruby Gem") – [Rust](/index.php/Diretrizes_de_pacotes_Rust "Diretrizes de pacotes Rust") – [VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") – [Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web") – [Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine")

Este documento abrange padrões e diretrizes para escrever [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") para [Electron](/index.php/Electron_(Portugu%C3%AAs) "Electron (Português)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Usando o electron do sistema](#Usando_o_electron_do_sistema)
    *   [1.1 Construindo extensões compiladas com o electron do sistema](#Construindo_extensões_compiladas_com_o_electron_do_sistema)
    *   [1.2 Usando electron-builder com electron do sistema](#Usando_electron-builder_com_electron_do_sistema)
*   [2 Arquitetura](#Arquitetura)
*   [3 Estrutura de diretórios](#Estrutura_de_diretórios)

## Usando o electron do sistema

Arch Linux fornece os pacotes globais [electron](https://www.archlinux.org/packages/?name=electron) e [electron2](https://www.archlinux.org/packages/?name=electron2) que podem ser usados para executar um aplicativo electron por meio de um *wrapper* de shellscript:

```
#!/bin/sh

exec electron /caminho/para/*nome_do_app*/ "$@"
```

O diretório `*nome_do_app*/` ou, alternativamente, um pacote de arquivo chamado `*nome_do_app*.asar`, pode ser localizado em um aplicativo electro pré-compilado como a pasta `resources/app/` (ou `resources/app.asar`). Todo resto é apenas uma cópia de *runtime* do electron e pode ser removido no pacote resultante.

### Construindo extensões compiladas com o electron do sistema

Alguns aplicativos de electron compilaram extensões nativas vinculadas ao *runtime* do electron e devem ser compiladas usando a versão correta de electron. Como o npm/yarn sempre será compilado com uma cópia pré-compilada privada de electron, aplique um *patch* na dependência de electron de `package.json` para referenciar a mesma versão da dependência de electron do sistema. O sistema de compilação irá baixar a cópia pré-compilada que precisar, compilará as extensões nativas e empacotará tudo em uma distribuição final, mas isso pode ser removido durante a etapa `package()` como de costume.

Alternativamente, você pode remover a dependência de electron do `package.json` e definir as variáveis de ambiente corretas antes de executar o npm:

```
export npm_config_target=$(tail /usr/lib/electron/version)
export npm_config_arch=x64
export npm_config_target_arch=x64
export npm_config_disturl=[https://atom.io/download/electron](https://atom.io/download/electron)
export npm_config_runtime=electron
export npm_config_build_from_source=true
HOME="$srcdir/.electron-gyp" npm install

```

Configure `HOME` para um caminho dentro do `$srcdir` para que o processo de compilação não coloque nenhum arquivo em seu diretório real `HOME`. Certifique-se de ajustar o caminho para todos os comandos adicionais que fazem uso do cache `.electron-gyp`.

(mais detalhes [aqui](https://electronjs.org/docs/tutorial/using-native-node-modules)).

### Usando electron-builder com electron do sistema

Muitos projetos usam o **electron-builder** para compilar e empacotar o arquivo JavaScript e os binários Electron. Por padrão, o electron-builder baixa toda a versão de electron definida no arquivo de gerenciamento de pacotes (por exemplo, `package.json`). Isso pode não ser desejado se você quiser usar o electron do sistema e economizar a largura de banda, já que você vai jogar fora os binários de electron de qualquer maneira. O electron-builder fornece as configurações `electronDist` e `electronVersion`, para especificar um caminho personalizado de Electron e a versão para a qual o aplicativo é empacotado, respectivamente.

Encontre o arquivo de configuração do electron-builder (por exemplo, `electron-builder.json`) e adicione as seguintes configurações:

*   `electronDist` com `/usr/lib/electron` para [electron](https://www.archlinux.org/packages/?name=electron) ou `/usr/lib/electron2` para [electron2](https://www.archlinux.org/packages/?name=electron2)
*   `electronVersion` com o conteúdo de `/usr/lib/electron/version` sem o `v` no início

Pacotes que aplicam isso: [rocketchat-desktop](https://aur.archlinux.org/packages/rocketchat-desktop/) [ubports-installer-git](https://aur.archlinux.org/packages/ubports-installer-git/)

[Configuração do electron-builder](https://www.electron.build/configuration/configuration)

## Arquitetura

Veja [PKGBUILD (Português)#arch](/index.php/PKGBUILD_(Portugu%C3%AAs)#arch "PKGBUILD (Português)").

Um pacote Electron que contém extensões nativas compiladas depende da arquitetura. Caso contrário, é mais provável que seja independente de arquitetura.

Se o pacote contiver uma cópia pré-compilada do electron, será sempre dependente da arquitetura.

## Estrutura de diretórios

Se o pacote é dependente de arquitetura, instale o diretório `resources/app/` em `/usr/lib/*nome_do_app*/`. Do contrário, use `/usr/share/*nome_do_app*/`.

Se o pacote contém uma cópia pré-compilada de electron, copie toda a distribuição final para `/opt/*nome_do_app*`.