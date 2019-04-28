**Status de tradução:** Esse artigo é uma tradução de [Cmus](/index.php/Cmus "Cmus"). Data da última tradução: 2019-04-22\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Cmus&diff=0&oldid=571864) na versão em inglês.

[cmus](https://cmus.github.io/) *(C* MUsic Player)* é um reprodutor de áudio de console pequeno, rápido e poderoso que suporta a maioria dos principais formatos de áudio. Vários recursos incluem reprodução contínua, suporte a ReplayGain, streaming de MP3 e Ogg, filtragem ao vivo, inicialização instantânea, atalhos de teclado personalizáveis e vinculações de teclas padrão no estilo vi.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
    *   [1.1 Usando o cmus com ALSA](#Usando_o_cmus_com_ALSA)
*   [2 Uso](#Uso)
*   [3 Configuração](#Configuração)
    *   [3.1 Controle Remoto](#Controle_Remoto)
*   [4 Veja Também](#Veja_Também)

## Instalação

Instale o pacote [cmus](https://www.archlinux.org/packages/?name=cmus) ou [cmus-git](https://aur.archlinux.org/packages/cmus-git/) para a versão de desenvolvimento.

Veja as dependências opcionais para codecs disponíveis e plugins de saída (instalados podem ser listados com `cmus --plugins`).

### Usando o cmus com ALSA

Instale o pacote [alsa-lib](https://www.archlinux.org/packages/?name=alsa-lib).

Ao usar cmus com [ALSA](/index.php/ALSA "ALSA"), a configuração padrão não permite reproduzir música. O que você pode encontrar ao tentar iniciar o cmus é uma linha terminal em branco, sem saída alguma. Para corrigi-lo, crie um novo arquivo de configuração e defina as seguintes variáveis

 `~/.config/cmus/rc` 
```
set output_plugin=alsa
set dsp.alsa.device=default
set mixer.alsa.device=default
set mixer.alsa.channel=Master
```

## Uso

Veja [cmus(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cmus.1), [cmus-tutorial(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cmus-tutorial.7) e [cmus-remote(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cmus-remote.1).

## Configuração

Para configurar o cmus, inicie-o e mude para a guia de configuração pressionando `7`.Agora você pode ver uma lista de atalhos de teclado padrão. Selecione um campo na lista com as teclas de seta e pressione`Enter` para editar os valores. Você também pode remover ligações com `D` ou `del`. Para editar comandos independentes e variáveis de opção, role para baixo na lista até a seção relevante. As variáveis também podem ser alternadas em vez de editadas com `space`. O Cmus permite alterar a cor de quase todos os elementos da interface. Você pode prefixar cores com "light" para torná-las mais claras e definir atributos para alguns elementos de texto.

### Controle Remoto

Cmus pode ser controlado externamente através de um unix-socket com `cmus-remote`. Isso facilita o controle da reprodução por meio de um aplicativo externo ou vinculação de teclas.

Um tal uso deste recurso é controlar a reprodução no Cmus com os eventos do teclado XF86\. O script a seguir quando executado iniciará o Cmus em um terminal xterm se ele não estiver em execução, caso contrário, ele alternará entre reproduzir / pausar:

```
#!/bin/sh

if ! pgrep -x cmus ; then
  xterm -e cmus
else
  cmus-remote -u
fi
```

Copie o código acima em um arquivo `~/bin/cplay` e faça-o executável.

Para usar o cmus-remote em [Openbox](/index.php/Openbox "Openbox"), edite `~/.config/openbox/rc.xml` e altere os seguintes atalhos de teclado para ficar assim:

**Nota:** Tenha certeza de que não hajam conflitos com os atalhos de teclado em `rc.xml`
 `~/.config/openbox/rc.xml` 
```
  <keyboard>
    <keybind key="XF86AudioPlay">
      <action name="Execute">
        <command>cmus-remote -u</command>
      </action>
    </keybind>
    <keybind key="XF86AudioNext">
      <action name="Execute">
        <command>cmus-remote -n</command>
      </action>
    </keybind>
    <keybind key="XF86AudioPrev">
      <action name="Execute">
        <command>cmus-remote -r</command>
      </action>
    </keybind>
  </keyboard>

```

Agora use a tecla `XF86AudioPlay` em seu teclado, cmus irá abrir. Se ele já estiver aberto, comecará a tocar. Usando as teclas `XF86AudioNext` e `XF86AudioPrev` irá mudar as faixas.

## Veja Também

*   [Git Repository](https://github.com/cmus/cmus)
*   [Website](https://cmus.github.io/)
*   [User submitted scripts](https://github.com/cmus/cmus/wiki)