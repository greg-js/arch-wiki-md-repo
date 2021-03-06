Artigos relacionados

*   [Compiz/Configuration](/index.php/Compiz/Configuration "Compiz/Configuration")
*   [Gerenciador de janela](/index.php/Gerenciador_de_janela "Gerenciador de janela")
*   [Ambiente de desktop](/index.php/Ambiente_de_desktop "Ambiente de desktop")
*   [Xfce](/index.php/Xfce_(Portugu%C3%AAs) "Xfce (Português)")
*   [MATE](/index.php/MATE "MATE")

Segundo a [Wikipedia](https://en.wikipedia.org/wiki/Compiz "wikipedia:Compiz"):

	O Compiz é um gerenciador de janela de composição para o [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)"), que utiliza aceleração 3D para criar efeitos compostos rápidos de desktop para o gerenciador de janelas. Efeitos como minimizar e maximizar ou a área de trabalho em cubo são implementados como plugins carregáveis.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
    *   [1.1 Através do Repositório Community](#Através_do_Repositório_Community)
        *   [1.1.1 Todos os Pacotes](#Todos_os_Pacotes)
        *   [1.1.2 Pacotes GTK](#Pacotes_GTK)
        *   [1.1.3 Pacotes KDE](#Pacotes_KDE)
    *   [1.2 Iniciando O Compiz Fusion](#Iniciando_O_Compiz_Fusion)
        *   [1.2.1 Com o Compiz Fusion Icon](#Com_o_Compiz_Fusion_Icon)
        *   [1.2.2 KDE](#KDE)
            *   [1.2.2.1 Manual Sem O Fusion-Icon](#Manual_Sem_O_Fusion-Icon)
            *   [1.2.2.2 Automaticamente](#Automaticamente)
                *   [1.2.2.2.1 Método 1 = Fusion-Icon](#Método_1_=_Fusion-Icon)
                *   [1.2.2.2.2 Método 2 = Manualmente criar um arquivo de inicialização automática](#Método_2_=_Manualmente_criar_um_arquivo_de_inicialização_automática)
    *   [1.3 Links Úteis](#Links_Úteis)

# Instalação

A instalação pode ser feita usando os repositórios community. Uma outra forma seria utilizando os pacotes git no artigo [Compiz Fusion Git](/index.php?title=Compiz_Fusion_Git&action=edit&redlink=1 "Compiz Fusion Git (page does not exist)").

## Através do Repositório Community

Após [habilitar o repositório no arquivo /etc/pacman.conf](/index.php/Pacman_(Portugu%C3%AAs)#Repositórios_e_espelhos "Pacman (Português)"), pode-se instalar o compiz com o comando:

### Todos os Pacotes

```
<tt># pacman -S **compiz-fusion**</tt>

```

### Pacotes GTK

```
<tt># pacman -S compiz-fusion-***gtk***</tt>

```

### Pacotes KDE

```
<tt># pacman -S compiz-fusion-***kde***</tt>

```

Agora adicione os pacotes com os **efeitos** fusion:

```
<tt># pacman -S compiz-fusion-plugins-**{main,extra}**</tt>

```

## Iniciando O Compiz Fusion

### Com o Compiz Fusion Icon

```
<tt>$ fusion-icon</tt>

```

Agora clique com o botão direito no ícone da bandeja e 'selecione gerenciador de janelas'. Escolha "Compiz" (se já não estiver selecionado). Se falhar você pode iniciar manualmente com os seguintes comandos:

```
<tt>$ fusion-icon
$ emerald --replace
$ compiz-manager</tt>

```

### KDE

#### Manual Sem O Fusion-Icon

Inicie o Compiz com o seguinte comando:

```
<tt>$ compiz --replace cpp&</tt>

```

Inicie o gerenciador de configurações e configure os efeitos desejados:

```
<tt>$ ccsm&</tt>

```

Inicie o decorador de janelas:

```
<tt>$ kde-window-decorator --replace</tt>

```

#### Automaticamente

##### Método 1 = Fusion-Icon

Crie um link do fusion-icon na pasta $HOME/.kde/Autostart:

```
<tt>$  ln -s /usr/bin/fusion-icon ~/.kde/Autostart/fusion-icon</tt>

```

##### Método 2 = Manualmente criar um arquivo de inicialização automática

```
<tt>$ kate $HOME/.kde/Autostart/compiz.desktop *OU* $ nano $HOME/.kde/Autostart/compiz.desktop
[Desktop Entry]
Encoding=UTF-8
Exec=compiz --replace ccp
StartupNotify=false
Terminal=false
Type=Application
X-KDE-autostart-after=kdesktop</tt>

```

## Links Úteis

[Compiz](/index.php/Compiz "Compiz")

[Xcompmgr](/index.php/Xcompmgr "Xcompmgr")

Wikipedia: [Gerenciador de Janelas Compositores(English)](https://en.wikipedia.org/wiki/Compositing_window_manager "wikipedia:Compositing window manager")