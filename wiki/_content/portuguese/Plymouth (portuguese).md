[Plymouth](http://www.freedesktop.org/wiki/Software/Plymouth) é um projecto da Fedora que consistem em proporcionar um processo de arranque gráfico sem cintilação. Baseia-se no [modo de configuração do kernel](/index.php/Kernel_mode_setting "Kernel mode setting") (KMS) para definir uma resolução nativa do ecrã assim que possível, fornecendo então um ecrã de boas vindas atractivo, até ao gestor de inicio de sessão.

## Contents

*   [1 Preparação](#Prepara.C3.A7.C3.A3o)
*   [2 Instalação](#Instala.C3.A7.C3.A3o)
    *   [2.1 Plymouth Hook](#Plymouth_Hook)
    *   [2.2 Hook alternativo Plymouth (systemd)](#Hook_alternativo_Plymouth_.28systemd.29)
    *   [2.3 Linha de comandos do kernel](#Linha_de_comandos_do_kernel)
*   [3 Configuração](#Configura.C3.A7.C3.A3o)
    *   [3.1 Transição suave](#Transi.C3.A7.C3.A3o_suave)
    *   [3.2 Atraso na apresentação](#Atraso_na_apresenta.C3.A7.C3.A3o)
    *   [3.3 Mudar o tema](#Mudar_o_tema)
*   [4 Truques e dicas](#Truques_e_dicas)
    *   [4.1 Mostrar mensagens do kernel](#Mostrar_mensagens_do_kernel)
    *   [4.2 Substituir o logo Arch e criar temas próprios](#Substituir_o_logo_Arch_e_criar_temas_pr.C3.B3prios)
*   [5 Ver também](#Ver_tamb.C3.A9m)

## Preparação

Plymouth usa principalmente [KMS](/index.php/KMS "KMS") (Modo de Configuração do Kernel) para apresentar imagens. Se não pode usar KMS (por ex. porque está a usar um driver proprietário) terá então de usar [framebuffer](/index.php/Framebuffer#Framebuffer_Resolution "Framebuffer"). Nos sistemas EFI/UEFI, Plymouth pode utilizar o framebuffer EFI, de outra forma [Uvesafb](/index.php/Uvesafb "Uvesafb") é recomendado pois pode funcionar com resoluções widescreen.

Se não tem KMS nem um framebuffer, Plymouth entrará em contigência e usará o modo de texto.

## Instalação

Plymouth está disponível através da [AUR](/index.php/AUR "AUR"): o pacote estável é [plymouth](https://aur.archlinux.org/packages/plymouth/) e a versão de desenvolvimento é [plymouth-git](https://aur.archlinux.org/packages/plymouth-git/).

Se também usa [GDM](/index.php/GDM "GDM"), deverá também instalar o [gdm-plymouth](https://aur.archlinux.org/packages/gdm-plymouth/), que compila gdm juntamente com o suporte plymouth.

Estes pacotes também se encontram disponíveis nos repositórios [nullptr_t](/index.php/Unofficial_user_repositories#nullptr_t "Unofficial user repositories") não oficiais.

### Plymouth Hook

Adicione `plymouth` ao conjunto de HOOKS em [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"). **Tem** de ser adicionado **após** `base` e `udev` a fim de funcionar:

 `/etc/mkinitcpio.conf`  `HOOKS="base udev plymouth [...] "` 
**Atenção:**

*   Se usa [Encriptação no disco rigido](/index.php/System_Encryption_with_LUKS_for_dm-crypt "System Encryption with LUKS for dm-crypt") com o hook `encrypt` , **tem de** substituir o hook `encrypt` com `plymouth-encrypt` a fim de introduzir a password quando solicitado pelo TTY.
*   Usando o parâmetro PARTUUID ou PARTLABEL em `cryptdevice=` **não** funciona com o hook `plymouth-encrypt`.

Após adicionar o hook `plymouth-encrypt`, se a entrada for para o background em mode de texto em vez de ir para a solicitação de password, necessita de adicionar o driver gráfico (kernel) ao seu initramfs. Por exemplo, se utilizar intel:

 `/etc/mkinitcpio.conf`  `MODULES="i915 [...]"` 

### Hook alternativo Plymouth (systemd)

Se o seu [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf") inclui o hook `systemd`, então substitua `plymouth` por `sd-plymouth`. Se utilizar encriptação nos seus discos utilize `sd-encrypt` em vez de `encrypt` ou de `plymouth-encrypt`

 `/etc/mkinitcpio.conf`  `HOOKS="base systemd sd-plymouth [...] sd-encrypt [...]"` 

Neste caso poderá ser necessário utilizar [plymouth-git](https://aur.archlinux.org/packages/plymouth-git/) em vez de [plymouth](https://aur.archlinux.org/packages/plymouth/).

### Linha de comandos do kernel

Neste momento precisa de adicionar o parâmetro `quiet splash` na sua linha de comandos do kernel. Veja [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") para mais informação.

Refaça a sua imagem initrd (veja o artigo [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") para mais detalhes, por exemplo:

```
# mkinitcpio -p linux

```

## Configuração

### Transição suave

Para activar a *transição suave* (se a mesma for suportada) tem de:

1.  Desactivar o seu [Display manager](/index.php/Display_manager "Display manager"), por ex. `systemctl disable gdm.service`
2.  Activar o respectivo serviço plymouth-DM (GDM, LXDM, SLiM, LightDM, SDDM serviços incluidos) por ex. `systemctl enable gdm-plymouth.service`

### Atraso na apresentação

Plymouth tem uma opção de configuração para atrasar o ecrã de boas vindas:

 `/etc/plymouth/plymouthd.conf` 
```
[Daemon]
Theme=spinner
ShowDelay=5
```

Em sistemas que iniciem depressa, poderá apenas ver uma tremulação do seu ecrã de boas vindas, antes do seu DM ou ecrã de login estar pronto. Pode definir ShowDelay para um intervalo (em segundos) maior que o tempo de iniciação do vosso sistema, a fim de prevenir essa tremulação e apresentar um ecrã branco. Por defeito é 5 segundos, mas pode definir para um valor mais baixo para poder ver a sua tela de abertura durante o boot.

### Mudar o tema

Plymouth vem com uma vasta selecção de temas:

1.  **Fade-in**: "Tema simples com uma transição gradual com estrelas brilhantes"
2.  **Glow**: "Tema corporativo com um gráfico que apresenta o progresso do boot, seguido de um brilhante logo"
3.  **Script**: "Plugin com um script de exemplo" (Apesar da descrição, parece ser um bom tema com o logo do Arch)
4.  **Solar**: "Tema do espaço com uma estrela azul rodeada de efeitos"
5.  **Spinner**: "Temas simples com uma roda de progresso"
6.  **Spinfinity**: "Tema simples que apresenta um simbolo rodando infinitamente no centro do ecrã"
7.  *(**Text**: "Tema com uma barra tricolor apresentando o progresso através de texto")*
8.  *(**Details**: "Tema em mode texto de fallback")*

Adicionalmente poderá instalar outros temas através do [AUR](/index.php/AUR "AUR"). Esteja atento ao "Required by" em [plymouth](https://aur.archlinux.org/packages/plymouth/)

Todos os temas actualmente instalados podem ser vistos através do comando:

```
$ plymouth-set-default-theme -l

```

ou:

 `$ ls /usr/share/plymouth/themes` 
```
details  glow    solar       spinner  tribar
fade-in  script  spinfinity  text

```

Por defeito, o tema **spinner** está seleccionado. Este tema pode ser mudado editando `/etc/plymouth/plymouthd.conf` por exemplo:

 `/etc/plymouth/plymouthd.conf` 
```
[Daemon]
Theme=spinner
ShowDelay=5
```

Os temas podem ser previstos sem reconstrução, pressione `Ctrl+Alt+F2` para alterar para a consola, faça login como root e escreva:

```
# plymouthd
# plymouth --show-splash

```

Para sair do ecrã de previsão carregue `Ctrl+Alt+F2` e escreva:

```
# plymouth --quit

```

Cada vez que um tema é alterado a imagem do kernel terá de ser reconstruída:

```
# plymouth-set-default-theme -R <theme>

```

Reinicie para aplicar as alterações.

## Truques e dicas

#### Mostrar mensagens do kernel

Durante o boot pode alterar para as mensagens do kernel pressionando a tecla "Home" (ou "Escape").

### Substituir o logo Arch e criar temas próprios

Os seguintes temas usam o logo Arch Linux fornecido por Plymouth em `/usr/share/plymouth/arch-logo.png`: fade-in, script, solar, spinfinity. Se quiser usar outro logo, pode usar um deles ou um dos outros temas em [AUR](/index.php/AUR "AUR"), editar o ficheiro `*.plymouth` (se calhar `*.script`, também) e substituir esta imagem com uma da sua escolha. Deverá criar um pacote do seu tema criado, porque alterações em `/usr/share/plymouth` poderão não ser persistentes através de actualizações de pacotes.

Depois de instalado e seleccionado o seu tema, deverá faze rebuild à imgem initrd e usar o novo spalsh.

## Ver também

*   [Original Spec](http://fedoraproject.org/wiki/Releases/FeatureBetterStartup)
*   [Related forum thread](https://bbs.archlinux.org/viewtopic.php?id=81406)