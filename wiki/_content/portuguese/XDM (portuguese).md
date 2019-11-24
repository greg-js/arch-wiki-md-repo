**Status de tradução:** Esse artigo é uma tradução de [XDM](/index.php/XDM "XDM"). Data da última tradução: 2019-11-21\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=XDM&diff=0&oldid=493920) na versão em inglês.

Artigos relacionados

*   [Gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição")

Da [página de manual do XDM](http://www.xfree86.org/current/xdm.1.html):

	*Xdm gerencia uma coleção de telas do X, que podem estar na máquina local ou em servidores remotos. O projeto do xdm foi orientado pelas necessidades dos terminais X, assim como o padrão do The Open Group XDMCP, o Protocolo de Controle do Gerenciador de Tela X. Xdm fornece serviços similares aos fornecidos pelo init getty e login em terminais de caracteres: solicitando o nome de login e senha, autenticando o usuário, e executando uma "sessão"*

XDM fornece um simples e direto solicitador de login gráfico.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Configuração](#Configuração)
    *   [2.1 Definindo a sessão](#Definindo_a_sessão)
    *   [2.2 Tema](#Tema)
        *   [2.2.1 Papel de parede de plano de fundo](#Papel_de_parede_de_plano_de_fundo)
        *   [2.2.2 Fonte](#Fonte)
        *   [2.2.3 Posicionamento de diálogo de login](#Posicionamento_de_diálogo_de_login)
        *   [2.2.4 Removendo a logo](#Removendo_a_logo)
    *   [2.3 Várias sessões X & Login na janela](#Várias_sessões_X_&_Login_na_janela)
    *   [2.4 Login sem senha](#Login_sem_senha)

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm). Então [habilite](/index.php/Habilite "Habilite") `xdm.service`.

Se você quiser usar um tema do Arch Linux para XDM, você pode opcionalmente instalar o pacote [xdm-archlinux](https://www.archlinux.org/packages/?name=xdm-archlinux). Se instalar este último pacote, **não** habilite `xdm.service`, mas, em vez disso, habilite `xdm-archlinux.service`.

## Configuração

### Definindo a sessão

Ao contrário de muitos outros [gerenciadores de exibição](/index.php/Gerenciadores_de_exibi%C3%A7%C3%A3o "Gerenciadores de exibição"), como [GDM](/index.php/GDM_(Portugu%C3%AAs) "GDM (Português)") ou [LightDM](/index.php/LightDM "LightDM"), XDM não carrega sessões disponíveis de arquivos .desktop localizados no diretório `/usr/share/xsessions`. Como tal, XDM não tem um 'menu de sessão.' Instead, XDM vai executar o arquivo `.xsession` no diretório home.

Por exemplo, para iniciar o xfce no login, o `~/.xsession` deve se parecer com isso:

```
startxfce4

```

Certifique-se que o arquivo `.xsession` em seu diretório home é um executável. Para fazer isso, use o seguinte comando:

```
$ chmod 700 ~/.xsession

```

### Tema

Para os significados exatos das opções discutidas abaixo, veja a página de manual do xdm. O arquivo de configuração está localizado em `/etc/X11/xdm/Xresources`, note que se você instalou [xdm-archlinux](https://www.archlinux.org/packages/?name=xdm-archlinux), o arquivo de configuração estará localizado em `/etc/X11/xdm/archlinux/Xresources`.

#### Papel de parede de plano de fundo

Você pode usar um programa como [qiv](https://www.archlinux.org/packages/?name=qiv) para definir o plano de fundo no XDM:

*   Instale [qiv](https://www.archlinux.org/packages/?name=qiv)

*   Crie um diretório para armazenar imagens de plano de fundo, por exemplo, `/root/backgrounds` ou `/usr/local/share/backgrounds`

*   Coloque suas imagens no diretório.

*   Edite `/etc/X11/xdm/Xsetup_0`. Altere o comando `xconsole` para:

```
 /usr/bin/qiv -zr /root/backgrounds/*

```

#### Fonte

*   Edite `/etc/X11/xdm/Xresources`. Adicione/substitua as seguintes definições:

```
 xlogin**greetFont:  -adobe-helvetica-bold-o-normal--20-**-**-**-**-**-iso8859-1
 xlogin**font:       -adobe-helvetica-medium-r-normal--14-**-**-**-**-**-iso8859-1
 xlogin**promptFont: -adobe-helvetica-bold-r-normal--14-**-**-**-**-**-iso8859-1
 xlogin**failFont:   -adobe-helvetica-bold-r-normal--14-**-**-**-**-**-iso8859-1

```

#### Posicionamento de diálogo de login

Essa configuração moverá o diálogo de login para o canto direito inferior da tela.

```
 xlogin*frameWidth: 1
 xlogin*innerFramesWidth: 1
 xlogin*logoPadding: 0
 xlogin*geometry:    300x175-0-0

```

#### Removendo a logo

Comente as definições da logo:

```
 #xlogin*logoFileName: /usr/share/xdm/pixmaps/xorg.xpm
 #xlogin*logoFileName: /usr/share/xdm/pixmaps/xorg-bw.xpm

```

### Várias sessões X & Login na janela

Com o [XDMCP](/index.php/XDMCP "XDMCP") habilitado, você pode facilmente executar várias sessões X simultaneamente na mesma máquina.

```
# X -query *ip_servidor_xdmcp* :2

```

Isso vai iniciar a segunda sessão na janela (você precisará de [xorg-server-xephyr](https://www.archlinux.org/packages/?name=xorg-server-xephyr))

```
# Xephyr -query *ip_dessa_máquina* :2

```

### Login sem senha

Para habilitar login sem senha para XDM, adicione a linha abaixo ao `/etc/X11/xdm/Xresources`:

```
xlogin*allowNullPasswd: true

```