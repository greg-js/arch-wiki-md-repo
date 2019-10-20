**Status de tradução:** Esse artigo é uma tradução de [Plymouth](/index.php/Plymouth "Plymouth"). Data da última tradução: 2019-10-13\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Plymouth&diff=0&oldid=582475) na versão em inglês.

Artigos relacionados

*   [Inicialização silenciosa](/index.php/Silent_boot "Silent boot")

[Plymouth](http://www.freedesktop.org/wiki/Software/Plymouth) é um projeto da Fedora e agora listado entre os [recursos oficiais do freedesktop.org](https://www.freedesktop.org/wiki/Software/#graphicsdriverswindowsystemsandsupportinglibraries) que fornece um processo de inicialização gráfico sem cintilação. Baseia-se no [modo de configuração do kernel](/index.php/Kernel_mode_setting "Kernel mode setting") (KMS) para definir uma resolução nativa da tela assim que possível, fornecendo então uma tela de boas vindas atrativa, até chegar no gerenciador de login.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Preparação](#Preparação)
*   [2 Instalação](#Instalação)
    *   [2.1 O hook do plymouth](#O_hook_do_plymouth)
    *   [2.2 Hook alternativo Plymouth (systemd)](#Hook_alternativo_Plymouth_(systemd))
    *   [2.3 Linha de comando do kernel](#Linha_de_comando_do_kernel)
*   [3 Configuração](#Configuração)
    *   [3.1 Transição suave](#Transição_suave)
    *   [3.2 Atraso na apresentação](#Atraso_na_apresentação)
    *   [3.3 Mudar o tema](#Mudar_o_tema)
*   [4 Truques e dicas](#Truques_e_dicas)
    *   [4.1 Mostrar mensagens do kernel](#Mostrar_mensagens_do_kernel)
    *   [4.2 Adicionar o Arch Logo para temas BGRT e spinner](#Adicionar_o_Arch_Logo_para_temas_BGRT_e_spinner)
    *   [4.3 Substituir o logo Arch e criar temas próprios](#Substituir_o_logo_Arch_e_criar_temas_próprios)
*   [5 Veja também](#Veja_também)

## Preparação

*Plymouth* usa principalmente [KMS](/index.php/KMS "KMS") *(Kernel Mode Setting)* para exibir imagens. Em sistemas EFI/UEFI, *plymouth* pode utilizar o framebuffer EFI. Se você não puder usar KMS (p.ex., porque está usando um driver proprietário) ou se você não quiser usar um framebuffer EFI, considere usar [Uvesafb](/index.php/Uvesafb "Uvesafb"), pois ele funciona com resoluções *widescreen*.

Caso não tenha KMS nem framebuffer, *plymouth* entrará recorrerá ao modo de texto.

## Instalação

Plymouth está disponível através do [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)"): o pacote estável é [plymouth](https://aur.archlinux.org/packages/plymouth/) e a versão de desenvolvimento é [plymouth-git](https://aur.archlinux.org/packages/plymouth-git/).

Se também usa o [GDM](/index.php/GDM_(Portugu%C3%AAs) "GDM (Português)"), você deve também instalar o [gdm-plymouth](https://aur.archlinux.org/packages/gdm-plymouth/), que compila gdm juntamente com o suporte a *plymouth*.

### O hook do plymouth

Adicione `plymouth` ao vetor `HOOKS` em [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"). **Tem** que ser adicionado **após** `base` e `udev` para funcionar:

 `/etc/mkinitcpio.conf`  `HOOKS=(base udev plymouth [...])` 
**Atenção:**

*   Se usa [criptografia no disco rígido](/index.php/System_Encryption_with_LUKS_for_dm-crypt "System Encryption with LUKS for dm-crypt") com o hook `encrypt`, você **deve** substituir o hook `encrypt` com `plymouth-encrypt` e adicioná-lo após o hook `plymouth` para conseguir inserir senhas quando solicitado pelo TTY.
*   O uso dos parâmetros `PARTUUID` ou `PARTLABEL` em `cryptdevice=` **não** funciona com o hook `plymouth-encrypt`.
*   Para uma [raiz ZFS criptografada](/index.php/Installing_Arch_Linux_on_ZFS#Native_encryption "Installing Arch Linux on ZFS"), você **deve** instalar [plymouth-zfs](https://aur.archlinux.org/packages/plymouth-zfs/) e substituir o hook `zfs` com `plymouth-zfs`

Após adicionar o hook `plymouth-encrypt`, se a entrada for para plano de fundo em modo de texto em vez de ir para a solicitação de senha, é necessário adicionar o driver gráfico (kernel) ao seu initramfs. Por exemplo, se estiver usando intel:

 `/etc/mkinitcpio.conf`  `MODULES=(i915 [...])` 

### Hook alternativo Plymouth (systemd)

Se o seu [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf") inclui o hook `systemd`, então substitua `plymouth` por `sd-plymouth`. Além disso, se utilizar criptografia nos discos rígidos, utilize `sd-encrypt` em vez de `encrypt` ou de `plymouth-encrypt`

 `/etc/mkinitcpio.conf`  `HOOKS=(base systemd sd-plymouth [...] sd-encrypt [...])` 

Neste caso poderá ser necessário utilizar [plymouth-git](https://aur.archlinux.org/packages/plymouth-git/) em vez de [plymouth](https://aur.archlinux.org/packages/plymouth/).

### Linha de comando do kernel

Neste momento precisa de adicionar os [parâmetros do kernel](/index.php/Par%C3%A2metros_do_kernel "Parâmetros do kernel") `quiet splash loglevel=3 rd.udev.log_priority=3 vt.global_cursor_default=0`. Veja [Inicialização silenciosa](/index.php/Inicializa%C3%A7%C3%A3o_silenciosa "Inicialização silenciosa") para outros parâmetros para limitar a saída para o console.

Recompile a sua imagem initrd (veja o artigo [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") para mais detalhes), por exemplo:

```
# mkinitcpio -p linux

```

## Configuração

### Transição suave

Para ativar a "transição suave" (em inglês, *smooth transition*), se houver suporte a ela, basta:

1.  [Desabilitar](/index.php/Desabilitar "Desabilitar") seu [gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição") (p.ex., gdm.service)
2.  [Habilitar](/index.php/Habilitar "Habilitar") a respectiva unit de plymouth-DM (units GDM, LXDM, SLiM, LightDM, SDDM incluídos) (p.ex., gdm-plymouth.service)

### Atraso na apresentação

Plymouth tem uma opção de configuração para atrasar a tela de apresentação:

 `/etc/plymouth/plymouthd.conf` 
```
[Daemon]
Theme=spinner
ShowDelay=5
```

Em sistemas que iniciem muito rápido, pode apenas ser possível ver uma tremulação de seu tema de apresentação antes do seu gerenciador de exibição ou seu prompt de login estar pronto. Pode-se definir `ShowDelay` para um intervalo (em segundos) maior que seu tempo de inicialização para evitar essa tremulação e apresentar uma tela branca. Por padrão é 5 segundos, mas pode definir para um valor mais baixo para poder ver a sua tela de apresentação durante a inicialização.

### Mudar o tema

Plymouth vem com uma vasta seleção de temas:

1.  **Fade-in**: "Tema simples com uma transição gradual com estrelas brilhantes"
2.  **Glow**: "Tema corporativo com um gráfico que apresenta o progresso da inicialização, seguido de um brilhante logo"
3.  **Script**: "Plugin com um script de exemplo" (Apesar da descrição, parece ser um bom tema com o logo do Arch)
4.  **Solar**: "Tema do espaço com uma estrela azul rodeada de efeitos"
5.  **Spinner**: "Temas simples com uma roda de progresso"
6.  **Spinfinity**: "Tema simples que apresenta um símbolo rodando infinitamente no centro da tela"
7.  *(**Text**: "Tema com uma barra tricolor apresentando o progresso através de texto")*
8.  *(**Details**: "Tema em modo texto reserva")*

A versão de desenvolvimento do Plymouth ([plymouth-git](https://aur.archlinux.org/packages/plymouth-git/)) também vem com o tema **BGRT**, que é uma variação do Spinner que mantém o logo OEM se disponível.

Adicionalmente, pode-se instalar outros temas do [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)"), bastando olhar no vetor "Necessário para" em [plymouth](https://aur.archlinux.org/packages/plymouth/)

Todos os temas atualmente instalados podem ser vistos através do comando:

```
$ plymouth-set-default-theme -l

```

ou:

 `$ ls /usr/share/plymouth/themes` 
```
details  glow    solar       spinner  tribar
fade-in  script  spinfinity  text

```

Por padrão, o tema **spinner** está selecionado. Este tema pode ser mudado editando `/etc/plymouth/plymouthd.conf`, por exemplo:

 `/etc/plymouth/plymouthd.conf` 
```
[Daemon]
Theme=spinner
ShowDelay=5
```

Os temas podem ser pré-visualizados sem recompilação, pressione `Ctrl+Alt+F2` para alterar para o console, faça login como root e escreva:

```
# plymouthd
# plymouth --show-splash

```

Para sair da tela de pré-visualização, pressione `Ctrl+Alt+F2` e digite:

```
# plymouth --quit

```

Cada vez que um tema é alterado, a imagem do kernel terá de ser recompilada:

```
# plymouth-set-default-theme -R <tema>

```

Reinicie para aplicar as alterações.

## Truques e dicas

#### Mostrar mensagens do kernel

Durante a inicialização, é possível alterar para as mensagens do kernel pressionando a tecla "Home" (ou "Escape").

### Adicionar o Arch Logo para temas BGRT e spinner

Para adicionar o Arch Logo aos temas *spinner* e *BGRT* copie o logo Arch o diretório de tema do spinner com nome `watermark.png`:

```
# cp /usr/share/plymouth/arch-logo.png /usr/share/plymouth/themes/spinner/watermark.png

```

### Substituir o logo Arch e criar temas próprios

Os seguintes temas usam o logo Arch Linux fornecido por Plymouth em `/usr/share/plymouth/arch-logo.png`: fade-in, script, solar, spinfinity. Se quiser usar outro logo, pode usar um deles ou um dos outros temas em [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)"), editar o arquivo `*.plymouth` (talvez `*.script`, também) e substituir esta imagem com uma da sua escolha. Deverá criar um pacote do seu tema criado, porque alterações em `/usr/share/plymouth` poderão não ser persistentes através de atualizações de pacotes.

Depois de instalado e seleccionado o seu tema, deverá faze rebuild à imgem initrd e usar o novo spalsh.

## Veja também

*   [Especificação original](http://fedoraproject.org/wiki/Releases/FeatureBetterStartup)
*   [Tópico relacionado mp fórum](https://bbs.archlinux.org/viewtopic.php?id=81406)