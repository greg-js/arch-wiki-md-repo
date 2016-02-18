**Dica:** Esta é parte de um artigo multi-páginas do "The Beginners' Guide" ("O Guia para Iniciantes"). **[Clique aqui](/index.php/Beginners%27_Guide_(Portugu%C3%AAs) "Beginners' Guide (Português)")** se preferir ler o artigo completo.

## Contents

*   [1 Extra](#Extra)
    *   [1.1 Gerenciamento de pacotes](#Gerenciamento_de_pacotes)
    *   [1.2 Gerenciamento de serviços](#Gerenciamento_de_servi.C3.A7os)
    *   [1.3 Som](#Som)
    *   [1.4 Ambiente Gráfico](#Ambiente_Gr.C3.A1fico)
        *   [1.4.1 Instalação do X](#Instala.C3.A7.C3.A3o_do_X)
        *   [1.4.2 Instalação de driver de vídeo](#Instala.C3.A7.C3.A3o_de_driver_de_v.C3.ADdeo)
        *   [1.4.3 Instalação de dispositivos de entrada](#Instala.C3.A7.C3.A3o_de_dispositivos_de_entrada)
        *   [1.4.4 Configuração do X](#Configura.C3.A7.C3.A3o_do_X)
            *   [1.4.4.1 Teclado](#Teclado)
        *   [1.4.5 Teste do X](#Teste_do_X)
            *   [1.4.5.1 Troubleshooting](#Troubleshooting)
        *   [1.4.6 Fonts](#Fonts)
        *   [1.4.7 Escolha e instale uma interface gráfica](#Escolha_e_instale_uma_interface_gr.C3.A1fica)
*   [2 Apêndice](#Ap.C3.AAndice)

## Extra

**Parabéns, e bem vindo ao seu sistema Arch Linux**

Seu novo sistema Arch Linux é agora um sistema GNU/Linux funcional e pronto para ser customizado. A partir daqui, você pode fazer o que quiser com este elegante conjunto de ferramentas, definindo o propósito que desejar. A maioria das pessoas se interessa por sistemas desktop, com opções de som e vídeo completas: Esta parte tem como proposta guiar e dar uma geral nos procedimentos para adquirir funcionalidades extras.

Vá em frente e logue com sua conta de usuário.

### Gerenciamento de pacotes

Veja [pacman](/index.php/Pacman "Pacman") e [gerenciamento de pacotes](/index.php/FAQ#Package_Management "FAQ") para respostas sobre instalação, atualização e gerenciamento de pacotes.

### Gerenciamento de serviços

O Arch Linux utiliza o [systemd](/index.php/Systemd "Systemd") como init, que é um sistema para gerenciamento de serviços no Linux. Para configurar sua instalação de Arch Linux, é uma boa idéia aprender o básico desta tecnologia. A interação com o systemd é feita através do comando `systemctl`. Leia [systemd#Basic aplicação do systemd](/index.php/Systemd#Basic_aplica.C3.A7.C3.A3o_do_systemd "Systemd") para maiores informações.

### Som

O [ALSA](/index.php/ALSA "ALSA") geralmente funciona fora da caixa. Só precisa tirar do mudo. Instale o pacote [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) (que possui o software `alsamixer`) e siga [estas](/index.php/Advanced_Linux_Sound_Architecture#Unmuting_the_channels "Advanced Linux Sound Architecture") instruções.

O ALSA está dentro do próprio kernel, portanto, recomendado de primeira. Contudo, se não funcionar, ou você não estiver satisfeito com a qualidade, o [OSS](/index.php/OSS "OSS") é uma alternativa viável. Se você possui algum requisito avançado de áudio, procure por mais informações no artigo [Sound system](/index.php/Sound_system "Sound system").

### Ambiente Gráfico

#### Instalação do X

O [X Window System](https://en.wikipedia.org/wiki/X_Window_System "wikipedia:X Window System") (mais conhecido como **X11** ou **X**) é um protocolo de rede e display que prove o mapeamento de janelas em sistemas bitmap. Também é um toolkit padrão e protocolo para a construção de interfaces gráficas de usuário(GUIs).

Para instalar os pacotes do [Xorg](/index.php/Xorg "Xorg"):

```
# pacman -S xorg-server xorg-xinit xorg-server-utils

```

Instale o [mesa](https://en.wikipedia.org/wiki/Mesa_(computer_graphics) para suporte a gráficos 3D:

```
# pacman -S mesa

```

#### Instalação de driver de vídeo

**Nota:** Se você instalou o Arch em um sistema convidado no VirtualBox, você não precisa instalar driver de vídeo. Veja [Arch Linux guests](/index.php/VirtualBox#Arch_Linux_guests "VirtualBox") para a instalação e configuração do "Guest additions" e pule para a parte [#Configuração do X](#Configura.C3.A7.C3.A3o_do_X).

Caso você não saiba qual o chipset de seu computador, rode:

```
$ lspci | grep VGA

```

Para a lista completa de drivers de vídeo open-source, procure da seguinte forma no banco de dados de pacotes:

```
$ pacman -Ss xf86-video | less

```

O driver `vesa` é um driver mode-setting genérico que funcionará quase todas as GPUs, porém sem aceleração 2D ou 3D satisfatória. Se um driver melhor não puder ser encontrado ou falhar durante a carga, o Xorg irá utilizar o vesa como solução de contorno. Para instalar:

```
# pacman -S xf86-video-vesa

```

Para que a aceleração de vídeo funcione, um driver de dispositivo adequado deve ser instalado:

| Marca | Tipo | Driver | Pacote [Multilib](/index.php/Multilib "Multilib")
(para aplicações 32-bit no Arch x86_64) | Documentação |
| **AMD/ATI** | Open source | [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) | [lib32-ati-dri](https://www.archlinux.org/packages/?name=lib32-ati-dri) | [ATI](/index.php/ATI "ATI") |
| Proprietário | [catalyst-dkms](https://aur.archlinux.org/packages/catalyst-dkms/) | [lib32-catalyst-utils](https://aur.archlinux.org/packages/lib32-catalyst-utils/) | [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst") |
| **Intel** | Open source | [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) | [lib32-intel-dri](https://www.archlinux.org/packages/?name=lib32-intel-dri) | [Intel graphics](/index.php/Intel_graphics "Intel graphics") |
| [xf86-video-i740](https://www.archlinux.org/packages/?name=xf86-video-i740) | – | (driver legado) |
| **Nvidia** | Open source | [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau)
(+ [nouveau-dri](https://www.archlinux.org/packages/?name=nouveau-dri) for 3D support) | [lib32-nouveau-dri](https://www.archlinux.org/packages/?name=lib32-nouveau-dri) | [Nouveau](/index.php/Nouveau "Nouveau") |
| [xf86-video-nv](https://www.archlinux.org/packages/?name=xf86-video-nv) | – | (driver legado) |
| Proprietário | [nvidia](https://www.archlinux.org/packages/?name=nvidia) | [lib32-nvidia-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-utils) | [NVIDIA](/index.php/NVIDIA "NVIDIA") |
| **SiS** | Open source | [xf86-video-sis](https://www.archlinux.org/packages/?name=xf86-video-sis)
[xf86-video-sisimedia](https://aur.archlinux.org/packages/xf86-video-sisimedia/)
[xf86-video-sisusb](https://www.archlinux.org/packages/?name=xf86-video-sisusb) | – | [SiS](/index.php/SiS "SiS") |

#### Instalação de dispositivos de entrada

O Udev será bom o suficiente para detectar seu hardware sem maiores problemas. O driver `evdev`([xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev)) é um driver moderno de dispositivo de entrada, hotplug, e que funciona com a maioria dos dispositivos não sendo necessária a instalação de drivers. Neste ponto o `evdev` já deve estar instalado por ser dependência do pacote [xorg-server](https://www.archlinux.org/packages/?name=xorg-server).

Usuários de laptop(ou de telas táteis) podem precisar do pacote [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) para touchpads/touchscreens funcionárem:

```
# pacman -S xf86-input-synaptics

```

Para instruções adicionais de resolução de problemas, dê uma olhada no artigo [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics").

#### Configuração do X

**Warning:** Drivers proprietários podem precisar de um reboot logo após a instalação. Veja [NVIDIA](/index.php/NVIDIA "NVIDIA") e [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst") para maiores detalhes.

As funcionalidades do Xorg de auto detecção podem funcionar sem um arquivo `xorg.conf`. Se você ainda deseja configurar manualmente o Servidor X, veja a pagina [Xorg](/index.php/Xorg "Xorg") nesta wiki.

##### Teclado

Para que seu teclado **br-abnt2** funcione no ambiente **X** é preciso editar o arquivo `/etc/X11/xorg.conf.d/10-evdev.conf` e acrescentar a seguinte linha:

 `# nano /etc/X11/xorg.conf.d/10-evdev.conf` 
```
Section "InputClass"
        Identifier "evdev keyboard catchall"
        MatchIsKeyboard "on"
        MatchDevicePath "/dev/input/event*"
        Driver "evdev"
                **Option  "XkbLayout"     "br"**
EndSection

```

Caso o arquivo `/etc/X11/xorg.conf.d/10-evdev.conf` não exista, crie um arquivo chamado **01-keyboard-layout.conf** em `/etc/X11/xorg.conf.d/`:

 `# nano /etc/X11/xorg.conf.d/01-keyboard-layout.conf` 
```
Section "InputClass"
   Identifier       "Keyboard Defaults"
   MatchIsKeyboard  "yes"
   Option           "XkbLayout" "br"
EndSection

```

ou você ainda pode utilizar o comando abaixo:

```
# localectl set-x11-keymap br abnt2

```

Feito isso, reinicie o X.

#### Teste do X

**Dica:** Estes passos são opcionais. Teste apenas se você estiver instalando o Arch Linux pela primeira vez, ou caso esteja instalando o Arch em um hardware que não é familiar a você.

**Nota:** Caso seus dispositivos de entrada não funcionem durante este teste, instale o driver necessário que está no grupo [xorg-drivers](https://www.archlinux.org/groups/x86_64/xorg-drivers/) e tente novamente. Para uma lista completa dos drivers de dispositivos disponíveis, executuma busca no pacman (pressione `Q` para sair):
```
$ pacman -Ss xf86-input | less

```
Você apenas precisara dos pacotes [xf86-input-keyboard](https://www.archlinux.org/packages/?name=xf86-input-keyboard) ou [xf86-input-mouse](https://www.archlinux.org/packages/?name=xf86-input-mouse) se você planeja desabilitar o hot-plugging, senão, mantenha o `evdev` que atuará como dispositivo de entrada(recomendado).

Instale o ambiente padrão:

```
# pacman -S xorg-twm xorg-xclock xterm

```

Se o Xorg for instalado antes da criação do usuário não-root, haverá um arquivo de template `.xinitrc` no diretório home do usuário que deverá ser deletado ou comentado por completo. Apenas deletando forçará o *X* a executar no ambiente padrão instalado acima.

```
$ rm ~/.xinitrc

```

**Nota:** O servidor X deve sempre rodar na mesma tty de onde o login ocorreu, para preservar a sessão logind. Esta configuração é manuseada pelo arquivo padrão `/etc/X11/xinit/xserverrc`.

Para iniciar(e testar) o Xorg, execute:

```
$ startx

```

Algumas janelas flutuantes serão mostradas e o mouse deverá funcionar. Assim que você estiver satisfeito que a instalação do **X** funcionou, saia dele digitando o comando `exit` em todos os prompts de comando até que você retorne para o console.

```
$ exit

```

Se a tela ficar preta, tente alterar a console virtual (exemplo: `Ctrl+Alt+F2`), e tente logar como root nas escuras. Digite "root" (pressione `Enter`) digite a senha (pressione `Enter`).

Você pode tentar também matar o **X** através do comando:

```
# pkill X

```

Caso não funcione, reinicie as escuras:

```
# reboot

```

##### Troubleshooting

Caso você encontre problemas, dê uma olhada no arquivo `Xorg.0.log`. As linhas que começam com `(EE)` representam erros, e as que começam com `(WW)` avisos, que podem ajudar na constatação de problemas.

```
$ grep EE /var/log/Xorg.0.log

```

Se ainda sim os problemas persistirem após consultar o artigo [Xorg](/index.php/Xorg "Xorg") e você precisar de auxílio extra através dos fóruns e canal do IRC, certifique-se de ter o pacote [wgetpaste](https://www.archlinux.org/packages/?name=wgetpaste) instalado para poder fornecer toda a informação necessária:

```
# pacman -S wgetpaste
$ wgetpaste ~/.xinitrc
$ wgetpaste /etc/X11/xorg.conf
$ wgetpaste /var/log/Xorg.0.log

```

**Nota:** Tente sempre prover toda informação pertinente(hardware, driver, versão de software, etc) quando buscar assistência.

#### Fonts

Agora, seu desejo deve ser o de instalar fontes TrueType, e apenas fontes bitmap não escaláveis são incluídas por padrão. O DejaVu é um conjunto de fontes de alta qualidade, de propósito geral e com boa cobertura do [Unicode](https://en.wikipedia.org/wiki/Unicode "wikipedia:Unicode"):

```
# pacman -S ttf-dejavu

```

Veja mais em [configuração de fontes](/index.php/Font_configuration "Font configuration") para saber como configurar a renderização das fontes, e obter maiores detalhes sobre instalação e sugestão de fontes.

#### Escolha e instale uma interface gráfica

O sistema X(X Window System) prove um framework básico para a construção de interfaces gráficas de usuário(GUI).

**Nota:** A escolha de um gerenciador de janelas é muito subjetiva/pessoal. Escolha o ambiente que melhor se encaixe as *suas* necessidaes. Você pode até mesmo construir o seu ambiente de desktop com apenas um gerenciador de janelas, e aplicativos selecionados "a dedo" por você.

*   [Gerenciadores de Janelas](/index.php/Window_manager "Window manager") (WM) controlam a localização e aparencia das janelas de aplicativos, juntamente com o X.

*   [Ambientes de Desktop](/index.php/Desktop_environment "Desktop environment") (DE) trabalham uma camada acima e em conjunção com o X, para criar um ambiente GUI completo e dinâmico. As principais funcionalidades que um ambiente de desktop (DE) provê são: Gerenciamento de janelas, ícones, applets, janelas, barras de tarefas, diretórios, papéis de parede e um conjunto de aplicativos e habilidades como a de arrastar e soltar(drag'n drop).

Ao invés de iniciar o X manualmente com o comando `xorg-xinit`, veja [gerenciador de login](/index.php/Display_manager "Display manager") para maiores instruções, ou ainda [Start X at login](/index.php/Start_X_at_login "Start X at login") para detalhes de como utilizar um terminal virtual como um equivalente ao gerenciador de Login

## Apêndice

Para uma lista de aplicativos que podem ser de seu interesse, veja [a lista de aplicativos](/index.php/List_of_applications "List of applications").

Dê uma olhada também em [recomendações gerais](/index.php/General_recommendations "General recommendations") para tarefas pós-instalação como configuração de um touchpad ou renderização de fontes.

**[Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide")**

* * *

[Prefácio](/index.php/Beginners%27_Guide/Preface_(Portugu%C3%AAs) "Beginners' Guide/Preface (Português)") >> [Preparar a Instalação](/index.php/Beginners%27_Guide/Preparation_(Portugu%C3%AAs) "Beginners' Guide/Preparation (Português)") >> [Instalar o sistema base](/index.php/Beginners%27_Guide/Installation_(Portugu%C3%AAs) "Beginners' Guide/Installation (Português)") >> **Extras**