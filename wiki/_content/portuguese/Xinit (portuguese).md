**Status de tradução:** Esse artigo é uma tradução de [Xinit](/index.php/Xinit "Xinit"). Data da última tradução: 2018-12-31\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Xinit&diff=0&oldid=560963) na versão em inglês.

Artigos relacionados

*   [Gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição")
*   [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)")
*   [xprofile](/index.php/Xprofile_(Portugu%C3%AAs) "Xprofile (Português)")
*   [Xresources](/index.php/Xresources "Xresources")

Do [Wikipédia](https://en.wikipedia.org/wiki/xinit "wikipedia:xinit"):

	O programa **xinit** permite que um usuário inicie manualmente um servidor de exibição [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)"). O script [startx(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/startx.1) é um front-end para [xinit(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xinit.1).

*xinit* é normalmente usado para iniciar os [gerenciadores de janela](/index.php/Gerenciadores_de_janela "Gerenciadores de janela") ou [ambientes de desktop](/index.php/Ambientes_de_desktop "Ambientes de desktop"). Embora você também possa usar o *xinit* para executar aplicativos GUI sem um gerenciador de janelas, muitos aplicativos gráficos esperam um gerenciador de janelas compatível com [EWMH](https://en.wikipedia.org/wiki/Extended_Window_Manager_Hints para você e geralmente obtém o [xprofile](/index.php/Xprofile_(Portugu%C3%AAs) "Xprofile (Português)").

## Contents

*   [1 Instalação](#Instalação)
*   [2 Configuração](#Configuração)
    *   [2.1 xinitrc](#xinitrc)
    *   [2.2 xserverrc](#xserverrc)
*   [3 Uso](#Uso)
*   [4 Dicas e truques](#Dicas_e_truques)
    *   [4.1 Sobrescrever xinitrc](#Sobrescrever_xinitrc)
    *   [4.2 Inicializar automaticamente o X no login](#Inicializar_automaticamente_o_X_no_login)
    *   [4.3 Alternando entre ambientes de desktop/gerenciadores de janela](#Alternando_entre_ambientes_de_desktop/gerenciadores_de_janela)
    *   [4.4 Inicializando aplicativos sem um gerenciador de janela](#Inicializando_aplicativos_sem_um_gerenciador_de_janela)
    *   [4.5 Faça redirecionamento usando startx](#Faça_redirecionamento_usando_startx)

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [xorg-xinit](https://www.archlinux.org/packages/?name=xorg-xinit).

## Configuração

*xinit* e *startx* aceitam um argumento opcional do programa cliente, veja [#Sobrescrever xinitrc](#Sobrescrever_xinitrc). Se você não fornecer um, eles procurarão `~/.xinitrc` para executar como um script de shell para inicializar os programas clientes.

### xinitrc

```
O `~/.xinitrc` é útil para executar programas dependendo do X e definir variáveis de ambiente na inicialização do servidor X. Se ele estiver presente no diretório home de um usuário, *startx* e *xinit* o executa. Do contrário, *startx* executará o `/etc/X11/xinit/xinitrc` padrão.

```

**Nota:** *Xinit* possui seu próprio comportamento padrão em vez de executar o arquivo. Veja [xinit(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xinit.1) para detalhes.

Este xinitrc padrão iniciará um ambiente básico com [Twm](/index.php/Twm "Twm"), [xorg-xclock](https://www.archlinux.org/packages/?name=xorg-xclock) e [Xterm](/index.php/Xterm "Xterm") (supondo que os pacotes necessários estejam instalados). Portanto, para iniciar um gerenciador de janelas ou ambiente de desktop diferente, primeiro crie uma cópia do `xinitrc` padrão em seu diretório inicial:

```
$ cp /etc/X11/xinit/xinitrc ~/.xinitrc

```

Então, [edite](/index.php/Help:Reading_(Portugu%C3%AAs)#Acrescentar,_adicionar,_criar,_editar "Help:Reading (Português)") o arquivo e substitua os programas padrão pelos comandos desejados. Lembre-se que as linhas que seguem um comando usando `exec` serão ignoradas. Por exemplo, para iniciar `xscreensaver` em segundo plano e, em seguida, iniciar [openbox](/index.php/Openbox#Standalone "Openbox"), use o seguinte:

 `~/.xinitrc` 
```
...
xscreensaver &
exec openbox-session
```

**Nota:** No mínimo, certifique-se de que o último bloco if em `/etc/X11/xinit/xinitrc` esteja presente em seu arquivo `~/.xinitrc` para garantir que os scripts em `/etc/X11/xinit/xinitrc.d` são originados.

Programas de execução longa iniciados antes do gerenciador de janelas, como um aplicativo de proteção de tela e de papel de parede, devem ser separados ou executados em segundo plano anexando um sinal de `&`. Caso contrário, o script pararia e aguardaria a saída de cada programa antes de executar o gerenciador de janelas ou o ambiente de área de trabalho. Note que alguns programas não devem ser bifurcados *(fork)*, para evitar bugs de corrida, como é o caso do [xrdb](/index.php/Xrdb "Xrdb"). Acrescentar `exec` antes do comando substituirá o processo do script pelo processo do gerenciador de janelas, de modo que o X não saia mesmo que esse processo se bifurque ao segundo plano.

### xserverrc

O arquivo `xserverrc` é um script de shell responsável por inicializar o servidor X. Ambos *startx* e *xinit* executam `~/.xserverrc` se ele existir; caso contrário, *startx* usará `/etc/X11/xinit/xserverrc`.

Para manter um [sessão autenticada](/index.php/General_troubleshooting#Session_permissions "General troubleshooting") com `logind` e para evitar contornar o bloqueio de tela alternando os terminais, o [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)") deve ser iniciado no mesmo terminal virtual onde ocorreu o login [[1]](http://blog.falconindy.com/articles/back-to-basics-with-x-and-systemd.html). Portanto, é recomendado especificar `vt$XDG_VTNR` no arquivo `~/.xserverrc`:

 `~/.xserverrc` 
```
#!/bin/sh

exec /usr/bin/Xorg -nolisten tcp "$@" vt$XDG_VTNR

```

Veja [Xserver(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/Xserver.1) para uma lista de todas as opções de linha de comando.

**Dica:** `-nolisten local` pode ser adicionado após `-nolisten tcp` para desabilitar soquetes abstratos de X11 para ajudar com isolação. Há uma [rápida história por trás](https://tstarling.com/blog/2016/06/x11-security-isolation/) sobre como isso potencialmente afeta a segurança do X11.

Alternativamente, se você deseja que o X seja exibido em um console separado daquele onde o servidor é invocado, você pode fazê-lo usando o wrapper do servidor X fornecido por `/usr/lib/systemd/systemd-multi-seat-x`. Por conveniência, *xinit* e *startx* podem ser configurados para usar este wrapper modificando seu `~/.xserverrc`.

**Nota:** Para habilitar novamente o redirecionamento da saída da sessão X para o arquivo de log do Xorg, adicione a opção `-keeptty`. Veja [Xorg#Broken redirection](/index.php/Xorg#Broken_redirection "Xorg") para detalhes.

## Uso

Para executar o Xorg como um usuário comum, use:

```
$ startx

```

ou se [#xserverrc](#xserverrc) estiver configurado:

```
$ xinit -- :1

```

**Nota:** O *xinit* não oferece suporte a múltiplos *displays* quando outro servidor X já está iniciado. Para isso você deve especificar o *display* anexando `-- :*número_display*`, onde `*número_display*` é `1` ou mais.

Seu gerenciador de janela (ou ambiente de desktop) deve ser iniciado corretamente agora.

Para sair do X, execute a função de saída do seu gerenciador de janela (supondo que ele tenha uma). Se não tiver essa funcionalidade, execute:

```
$ pkill -15 Xorg

```

**Nota:** *pkill* vai matar todas as instâncias X em execução. Para matar especificamente o gerenciador de janela no terminal virtual atual, execute:
```
$ pkill -15 -t tty"$XDG_VTNR" Xorg

```

Veja também [signal(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/signal.7).

## Dicas e truques

### Sobrescrever xinitrc

Se você tem um `~/.xinitrc` funcionando, mas quer apenas tentar outro gerenciador de janela ou ambiente de desktop, você pode executá-lo emitindo *startx* seguido pelo caminho para o gerenciador de janela, por exemplo:

```
$ startx /usr/bin/i3

```

Se o binário recebe argumentos, eles precisam ser citados para serem reconhecidos como parte do primeiro parâmetro de *startx*:

```
$ startx "/usr/bin/*aplicativo* --*chave valor*"

```

Note que o caminho completo é **obrigatório**. Você também pode especificar opções personalizadas para o script [#xserverrc](#xserverrc) anexando-as após o sinal de traço duplo `--`:

```
$ startx /usr/bin/enlightenment -- -br +bs -dpi 96

```

Veja também [startx(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/startx.1).

**Nota:** Display precisa se especificado (pois o carregamento `/etc/X11/xinit/xinitrc.d/` é ignorado) para algumas operações para funcionar (por exemplo, para daemons de notificação). [[2]](https://bbs.archlinux.org/viewtopic.php?id=202812)

**Dica:** Isso pode ser usado para iniciar programas de interface gráfica comum, mas sem qualquer recurso básico de gerenciador de janela. Veja também [#Inicializando aplicativos sem um gerenciador de janela](#Inicializando_aplicativos_sem_um_gerenciador_de_janela) e [Executando um programa em uma tela X separada](/index.php/Running_program_in_separate_X_display "Running program in separate X display").

### Inicializar automaticamente o X no login

Certifique-se de que *startx* esteja apropriadamente [configurado](#Configuração).

Para o [Bash](/index.php/Bash "Bash"), adicione o seguinte ao final do `~/.bash_profile`. Se o arquivo não existir, copie uma versão esqueleto de `/etc/skel/.bash_profile`. Para [Zsh](/index.php/Zsh "Zsh"), adicione-o a `~/.zprofile`.

```
if [[ ! $DISPLAY && $XDG_VTNR -eq 1 ]]; then
  exec startx
fi

```

Você pode substituir a comparação `-eq` por uma como `-le 3` (de vt1 a vt3) se quiser usar logins gráficos em mais de um terminal virtual.

Condições alternativas para detectar o terminal virtual incluem `"$(tty)" = "/dev/tty1"`, que não permite comparação com `-le`, e `"$(fgconsole 2>/dev/null || echo -1)" -eq 1`, que não funciona em [consoles seriais](/index.php/Serial_console "Serial console").

Se você quiser de permanecer autenticado quando a sessão X terminar, remova `exec`.

Veja também [Fish#Start X at login](/index.php/Fish#Start_X_at_login "Fish") e [Systemd/User#Automatic login into Xorg without display manager](/index.php/Systemd/User#Automatic_login_into_Xorg_without_display_manager "Systemd/User").

**Dica:** Esse método pode ser combinado com [login automático a um console virtual](/index.php/Automatic_login_to_virtual_console "Automatic login to virtual console").

### Alternando entre ambientes de desktop/gerenciadores de janela

Se você estiver alternando com frequência entre diferentes ambientes de desktop ou gerenciadores de janela, é conveniente usar um [gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição") ou expandir `~/.xinitrc` para tornar a troca possível.

O seguinte exemplo mostra como iniciar um determinado ambiente de desktop ou gerenciador de janela com um argumento:

 `~/.xinitrc` 
```
...

# Aqui o Xfce é mantido como padrão
session=${1:-xfce}

case $session in
    i3|i3wm           ) exec i3;;
    kde               ) exec startkde;;
    xfce|xfce4        ) exec startxfce4;;
    # Nenhuma sessão conhecida, tenta como comando
    *                 ) exec $1;;
esac

```

Para passar o argumento *sessão*:

```
$ xinit *sessão*

```

ou

```
$ startx ~/.xinitrc *sessão*

```

### Inicializando aplicativos sem um gerenciador de janela

É possível iniciar apenas aplicativos específicos sem um gerenciador de janela, embora provavelmente isso seja útil apenas com um único aplicativo mostrado no modo de tela cheia. Por exemplo:

 `~/.xinitrc` 
```
...

exec chromium

```

Alternativamente, o binário pode ser chamado diretamente a partir do prompt de comando, conforme descrito em [#Sobrescrever xinitrc](#Sobrescrever_xinitrc).

Com esse método, você precisa definir a geometria de cada janela do aplicativo por meio de seus próprios arquivos de configuração (se possível).

**Dica:** Isso pode ser útil para lançar jogos gráficos, nos quais a sobrecarga de um compositor pode ajudar a melhorar o desempenho da execução do jogo.

Veja também also [Gerenciador de exibição#Iniciando aplicativos sem um gerenciador de janela](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o#Iniciando_aplicativos_sem_um_gerenciador_de_janela "Gerenciador de exibição").

### Faça redirecionamento usando startx

Veja [Xorg#Broken redirection](/index.php/Xorg#Broken_redirection "Xorg") para detalhes.