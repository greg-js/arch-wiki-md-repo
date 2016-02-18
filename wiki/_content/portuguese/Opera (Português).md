[Opera](http://www.opera.com) é um navegador da web livre e gratuito desenvolvido desde de 1994 pela empresa norueguesa [Opera Software](http://pt.wikipedia.org/wiki/Opera_Software). Ele é conhecido por ser o primeiro a trazer novos recursos de navegação para o mundo que se tornaram comuns em todos os navegadores da Web, como navegação por abas e construído em pesquisa.

Opera continua a inovar com o seu cliente de email integrado, de um clique bookmarking, pilhas guia (uma forma de organizar suas abas) e suporte muito bom para recursos [HTML5](http://pt.wikipedia.org/wiki/HTML5).

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
*   [2 Plugins](#Plugins)
    *   [2.1 Adobe Flash](#Adobe_Flash)
    *   [2.2 Suporte ao Java](#Suporte_ao_Java)
    *   [2.3 Adblock](#Adblock)
*   [3 Ajustes de performance](#Ajustes_de_performance)
    *   [3.1 Desabilitando características e serviços](#Desabilitando_caracter.C3.ADsticas_e_servi.C3.A7os)
        *   [3.1.1 Desativar o cliente de E-mail](#Desativar_o_cliente_de_E-mail)
        *   [3.1.2 Desativar ARGB, LIRC e links de Email mailto](#Desativar_ARGB.2C_LIRC_e_links_de_Email_mailto)
    *   [3.2 Melhorar o desempenho do Flash](#Melhorar_o_desempenho_do_Flash)
        *   [3.2.1 Exemplo no .xinitrc](#Exemplo_no_.xinitrc)
        *   [3.2.2 Exemplo para linha de comando](#Exemplo_para_linha_de_comando)
    *   [3.3 Perfil na tmpfs](#Perfil_na_tmpfs)
*   [4 Aparência](#Apar.C3.AAncia)
    *   [4.1 Temas](#Temas)
    *   [4.2 Modos das Guias](#Modos_das_Guias)
    *   [4.3 Fontes de texto](#Fontes_de_texto)
*   [5 Guias privadas](#Guias_privadas)
*   [6 Dicas de acessibilidade](#Dicas_de_acessibilidade)
    *   [6.1 Desativar seleção de texto](#Desativar_sele.C3.A7.C3.A3o_de_texto)
    *   [6.2 Modo agarramento e modo de rolagem](#Modo_agarramento_e_modo_de_rolagem)
    *   [6.3 Manter pressionado um link para abrir em uma aba de fundo (extensão)](#Manter_pressionado_um_link_para_abrir_em_uma_aba_de_fundo_.28extens.C3.A3o.29)
    *   [6.4 Teclado virtual na tela (extensão)](#Teclado_virtual_na_tela_.28extens.C3.A3o.29)
*   [7 Solução de problemas](#Solu.C3.A7.C3.A3o_de_problemas)
    *   [7.1 Deslocamento lento em placas NVIDIA](#Deslocamento_lento_em_placas_NVIDIA)
    *   [7.2 Roda de rolagem horizontal do mouse](#Roda_de_rolagem_horizontal_do_mouse)
    *   [7.3 Lançar um navegador externo](#Lan.C3.A7ar_um_navegador_externo)
    *   [7.4 Opera trava ao iniciar ou fechar com GTK+ 2.24.7+](#Opera_trava_ao_iniciar_ou_fechar_com_GTK.2B_2.24.7.2B)
    *   [7.5 Ilegíveis campos de texto e barra de endereços com temas escuros GTK+](#Ileg.C3.ADveis_campos_de_texto_e_barra_de_endere.C3.A7os_com_temas_escuros_GTK.2B)
*   [8 Veja mais](#Veja_mais)

## Instalação

O navegador Opera pode ser [instalado](/index.php/Pacman "Pacman") através do pacote [opera](https://www.archlinux.org/packages/?name=opera), disponível nos [repositórios oficiais](https://wiki.archlinux.org/index.php/Official_Repositories_(Português)).

Versões em desenvolvimento podem ser encontradas no [AUR](/index.php/AUR "AUR"):

*   [opera-beta](https://aur.archlinux.org/packages/opera-beta/) - Uma versão beta.
*   [opera-next](https://aur.archlinux.org/packages/opera-next/) - Uma versão alfa/em desenvolvimento.

## Plugins

O navegador Opera pode usar plugins baseados em Netscape que são suportados pela maioria dos principais navegadores, como o Firefox e Chromium. Para obter detalhes sobre plugins diferentes e instruções de instalação veja: [Browser plugins](/index.php/Browser_plugins "Browser plugins"). No Opera, o caminho dos plugins pode ser especificado em *Configurações > Preferências... > Avançado > Conteúdo > Opções de plug-in...*.

### Adobe Flash

Veja o principal artigo: [Browser plugins#Flash Player](/index.php/Browser_plugins#Flash_Player "Browser plugins").

### Suporte ao Java

Veja o principal artigo: [Browser plugins#Java (IcedTea)](/index.php/Browser_plugins#Java_.28IcedTea.29 "Browser plugins").

### Adblock

O suporte ao Adblock pode ser instalado usando o pacote [opera-adblock-complete](https://aur.archlinux.org/packages/opera-adblock-complete/) disponível no [AUR](/index.php/AUR "AUR").

## Ajustes de performance

Apesar do Opera ser bastante rápido em hardware modernos, ele pode ser otimizado ainda mais. Para mais informações, consulte a [Página wiki do Opera](http://operawiki.info/operaperformance) sobre performance.

### Desabilitando características e serviços

Uma das chaves para a maximização de desempenho do aplicativo é desativar características indesejáveis e serviços habilitadas por padrão em [opera:config Editor de Preferências.](http://www.opera.com/browser/tutorials/personalize/behavior/)

Alguns recursos normalmente desativados são:

*   **Ícone na área de notificação**: desmarque ***Show Tray Icon*** em **opera:config#ShowTrayIcon**.
*   **BitTorrent**: desmarque ***Enable*** em **opera:config#BitTorrent|Enable**.
*   **Geolocalização**: desmarque ***Enable geolocation'*** em **opera:config#Geolocation|Enablegeolocation**.
*   **Multimedia**: desmarque as opções indesejadas em **opera:config#Multimedia**.
*   **Servidor Web**: desmarque ***Enable*** em **opera:config#WebServer|Enable**.

Para maior facilidade em localizar essas opções, apenas escreva o caminho respectivo (sem espaços) na barra de endereços, por exemplo `opera:config#UserPrefs|ShowTrayIcon` ou use a pesquisa embutida.

#### Desativar o cliente de E-mail

Linhas de comando adicionais são as opções disponíveis para um melhor controle sobre os recursos do navegador e serviços. Para iniciar o Opera sem o cliente padrão de e-mail interno:

```
$ opera -nomail

```

Alternativamente, se voce quer desabilitar permanentemente o cliente de e-mail interno voce pode desmarcar a opção *Show E-mail Client* em **opera:config#UserPrefs**.

#### Desativar ARGB, LIRC e links de Email mailto

Para iniciar o Opera sem visuais [ARGB](https://en.wikipedia.org/wiki/ARGB "wikipedia:ARGB") (32-bit) , suporte [LIRC](http://www.lirc.org/) ao controlador de infravermelho e com links `mailto:` desativados:

```
$ opera -noargb -nolirc -nomaillinks

```

### Melhorar o desempenho do Flash

Para melhorar o desempenho do Flash você pode definir as seguintes variáveis de ambiente antes de iniciar o Opera, ou exportar as entradas do [xinitrc](/index.php/Xinitrc "Xinitrc"), ou [~/.bash_profile](/index.php?title=Startup_Files&action=edit&redlink=1 "Startup Files (page does not exist)"), ou completamente no sistema, em `/etc/profile`:

```
 OPERAPLUGINWRAPPER_PRIORITY=0
 OPERA_KEEP_BLOCKED_PLUGIN=1

```

Outra variável de ambiente que pode ajudar a resolver problemas de flash:

```
GDK_NATIVE_WINDOWS=1

```

Veja o artigo de um blog sobre [Problemas com o flash no linux](http://pelenegra.blogspot.com/2007/12/problemas-com-flash-no-opera-e-no.html) para informações adicionais.

#### Exemplo no .xinitrc

 `~/.xinitrc` 
```
...
export OPERAPLUGINWRAPPER_PRIORITY=0
export OPERA_KEEP_BLOCKED_PLUGIN=0
...

```

#### Exemplo para linha de comando

Para usar as variáveis com o Opera pela linha de comando chame com:

```
$ OPERAPLUGINWRAPPER_PRIORITY=0 OPERA_KEEP_BLOCKED_PLUGIN=1 opera &

```

### Perfil na tmpfs

Realocar o perfil do navegador para um sistema de arquivos [tmpfs](/index.php/Fstab#_tmpfs "Fstab") , incluindo `/tmp` causa melhorias na resposta da aplicação com o perfil inteiro armazenado na memória RAM. Outra vantagem é a redução da leitura do disco e das operações de gravação, de que beneficia o mais SSDs.

Atualmente existem duas maneiras de fazer isso:

*   usando o [Profile-sync-daemon](/index.php/Profile-sync-daemon "Profile-sync-daemon"), que automaticamente detecta e transfere o perfil do Opera para tmpfs.
*   usando o comando `-pd` decide onde o Opera irá manter os dados do perfil:

```
$ opera -pd /tmp/opera

```

## Aparência

### Temas

Já que o Opera é multi-plataforma, ele pode integrar muito bem em vários ambientes de desktop Linux.

	Qt

	Para fazer os menus visualmente integrados com , instale um tema em Qt de sua preferência e aplique usando `qtconfig`.

	KDE

	Para fazer o Opera usar icones do [KDE](/index.php/KDE "KDE"), você pode instalar uns temas [como estes](http://my.opera.com/community/customize/skins/info/?id=8141).

	GTK+

	Um bom tema baseado em GTK+ que usa o tema de ícones Tango pode ser encontrado [aqui](http://my.opera.com/community/customize/skins/info/?id=3465).

### Modos das Guias

Opera tem suporte nativo para guias em modo cascata e lado a lado. Botões apropriados podem ser encontrados ativando a barra de ferramentas "Principal" ou arrastando e soltando os botões em qualquer lugar desejado, encontrado em *Menu > Aparência > Botões > Navegação*.

### Fontes de texto

Fontes de texto pode ser configuradas em *Configurações > Preferências... > Avançado > Fontes*.

Se o pacote [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) foi instalado antes de executar o Opera pela primeira vez, por padrão o Opera irá usar estas fontes de texto, independentemente do que é especificado nas opções locais do GTK+ pelo gerenciamento de fontes do [GNOME](/index.php/GNOME "GNOME") ou do [KDE](/index.php/KDE "KDE"). Para fazer com que as instalações existentes do Opera usem as opções definidas pelo seu sistema:

*   Feche todas as instancias do Opera.
*   Des-instale o pacote [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/).
*   Mover uma pasta de perfil existente: `mv -i ~/.opera ~/.opera.bak`
*   Executar uma instancia do Opera e verificar se o gerenciamento de fontes aplicou as configurações corretamente.
*   Restaurar marcadores e arquivos desejados no filtro de `~/.opera.bak` para `~/.opera` exceto o arquivo `operaprefs.ini`.
*   Re-instale o pacote [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) , se quiser.

## Guias privadas

Para navegar sem deixar vestígios visíveis dos sites que você visitou, você pode usar uma guia privada. Quando você fechar uma aba privada, os seguintes dados relativos à guia são excluídos:

*   Cache
*   Cookies
*   Histórico
*   Logins

Isto é semelhante a [opção --incognito (Página em inglês)](http://www.google.com/support/chrome/bin/answer.py?hl=en&answer=95464) do Chrome/[Chromium](/index.php/Chromium "Chromium") e [Navegação Privada (Página em inglês)](https://wiki.mozilla.org/PrivateBrowsing) do [Firefox](/index.php/Firefox "Firefox").

Para abrir uma guia privada através da linha de comando use:

```
$ opera -newprivatetab

```

Para assegurar que apenas as guias particulares são utilizados ao longo da duração da sessão de navegação:

*   Selecione *Configurações > Preferencias... > Geral > Iniciar > Iniciar com a página inicial OU Iniciar com Speed Dial*.
*   Limpar as entradas em *Configurações > Preferencias... > Geral > opção Página inicial*.
*   Habilitar *Configurações > Preferencias... > Avançado > Guias > Opções adicionais de guia... > Permitir janelas sem guias*.

Para abrir uma nova janela de navegação privada quando o Opera já estiver em execução, você pode apenas pressionar `Ctrl+Shift+N` ou ativar em *Menu > Guias e janelas > Nova janela privada*. Todos os separadores abertos subsequentes vão ser separados com as guias privadas numa nova janela.

## Dicas de acessibilidade

### Desativar seleção de texto

É possível desativar a seleção de texto no Opera. No entanto, a seleção de texto através de JavaScript continuará a funcionar (por exemplo, em formulários, etc). Para chegar à definição siga o link abaixo:

```
opera:config#System|DisableTextSelect

```

### Modo agarramento e modo de rolagem

Além de definir a seleção de texto fora, modo agarramento e de rolagem faz uma rolagem de página possível com o arrastar do mouse. É muito útil, especialmente quando você tem um ecrã táctil. Copie e cole o link abaixo para obter a definição mencionada.

```
opera:config#UserPrefs|ScrollIsPan

```

Também é possível alterar essa configuração em tempo real, arrastando e soltando o apropriado botão Opera na barra de ferramentas. O botão pode ser encontrado em *Menu > Aparência > Botões > Exibição na nav (navegação)...*.

### Manter pressionado um link para abrir em uma aba de fundo (extensão)

É possível abrir qualquer link clicado a um certo tempo em uma aba nova do fundo através da instalação [dessa](https://addons.opera.com/en/addons/extensions/details/open-in-background-with-long-press/) extensão.

### Teclado virtual na tela (extensão)

Existe uma extensão que permite a utilização de um teclado virtual na tela. Mais detalhes e link de instalação pode ser encontrado [aqui](https://addons.opera.com/en/addons/extensions/details/virtual-keyboard/).

## Solução de problemas

### Deslocamento lento em placas NVIDIA

Tente executar o seguinte comando:

```
$ nvidia-settings -a InitialPixmapPlacement=2

```

Em alguns computadores, [http://helion.pl](http://helion.pl) funciona muito lento sem este meio, tornando-se um local perfeito para testes.

### Roda de rolagem horizontal do mouse

Cheque *Configurações > Preferencias... > Avançado > Atalhos > Mouse > Opções de botão central... > Habilitar panorama horizontal*.

ou

*   Selecione *Configurações > Preferencias... > Avançado > Atalhos > Mouse > Opera Standard*.
*   Duplicar *Configurações > Preferencias... > Avançado > Atalhos > Mouse > Opera Standard*.
*   Editar... *Configurações > Preferencias... > Avançado > Atalhos > Mouse > Copia de Opera Standard*.
*   Procure nos contextos de texto e edite os Atalhos botão apropriado para `Avançado`, `Voltar`, `Vá para a esquerda` e `Vá para a direita`.
*   Renomear *Configurações > Preferencias... > Avançado > Atalhos > Mouse > Copia de Opera Standard* como desejado.

### Lançar um navegador externo

Se o Opera não exibir um site bem, uma solução alternativa é lançar a página exibida em um navegador externo.

**Note:** O seguinte método parece ser substituído a favor do menu interno `Abrir Com` acessado via botão esquerdo do mouse.

*   Aplique a seguinte linha de comando `[Site Navigation Toolbar.content]` em `$HOME/.opera/toolbar/standard_toolbar.ini`:

```
Button0, "Chromium"="Executar programa, "chromium, "%u", , "Chromium""

```

*   Se Firefox for o seu preferido, ou o desejado:

```
Button0, "Firefox"="Executar programa, "firefox", "%u", , "Firefox""

```

*   Qualquer número de opção da linha de comando pode ser incluído na cadeia:

```
Button0, "Chromium"="Executar programa, "chromium --block-nonsandboxed-plugins --disable-java --incognito --safe-plugins --start-maximized --user-data-dir=/tmp/.chromium", "%u", , "Chromium""

```

### Opera trava ao iniciar ou fechar com GTK+ 2.24.7+

Se esse erro acontecer, voce pode contornar o problema mudando a opção *DialogToolkit* para a opção 4:

```
opera:config#FileSelector|DialogToolkit

```

Isto irá desativar o suporte do estilo GTK+ e, consequentemente, evitar o problema.

### Ilegíveis campos de texto e barra de endereços com temas escuros GTK+

Ao usar um tema GTK escuro, pode-se encontrar a barra de endereços do Opera e páginas da Internet com textos e campos de texto ilegíveis (por exemplo, o site do Amazon pode ter texto em preto sobre fundo preto do campo de texto). Isso pode acontecer porque o site define apenas fundo de texto, ou cor do texto, e o Opera se baseia nas outras cores a partir do tema do sistema.

Usando um tema claro instalado e um comando ajudará a contornar o problema: `env GTK2_RC_FILES=/usr/share/themes/<nome-do-tema-claro>/gtk-2.0/gtkrc opera`

para defini-lo como padrão, use um editor de texto preferencial e edite o arquivo `/usr/bin/opera`.

```
ex: com o Opera 12.14:

```

```
sudo gedit /usr/bin/opera
...
#!/bin/sh
export OPERA_DIR=${OPERA_DIR:-/usr/share/opera}
export OPERA_PERSONALDIR=${OPERA_PERSONALDIR:-$HOME/.opera}
exec /usr/lib/opera/opera "$@"

```

edite o arquivo e siga o exemplo mudando para:

```
/usr/bin/opera
...
#!/bin/sh
export OPERA_DIR=${OPERA_DIR:-/usr/share/opera}
export OPERA_PERSONALDIR=${OPERA_PERSONALDIR:-$HOME/.opera}
env GTK2_RC_FILES=/usr/share/themes/Clearlooks/gtk-2.0/gtkrc /usr/lib/opera/opera "$@"

```

isso fará com que o navegador use um tema claro que você definir no arquivo `/usr/bin/opera` que foi usado no exemplo acima, o tema "Clearlooks" e os problemas serão resolvidos.

## Veja mais

*   [Forum do Opera para UNIX](http://my.opera.com/community/forums/forum.dml?id=3)
*   [Documentação do Opera](http://www.opera.com/pt/docs/)
*   [Ajuda do Opera](http://www.opera.com/pt/help)