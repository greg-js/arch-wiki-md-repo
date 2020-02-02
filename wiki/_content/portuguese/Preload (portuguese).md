**Status de tradução:** Esse artigo é uma tradução de [Preload](/index.php/Preload "Preload"). Data da última tradução: 2020-01-26\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Preload&diff=0&oldid=596276) na versão em inglês.

O pré-carregamento é a ação de colocar e manter os arquivos de destino na RAM. O benefício é que os aplicativos pré-carregados iniciam mais rapidamente porque a leitura na RAM é sempre mais rápida que no disco rígido. No entanto, parte da sua RAM será dedicada a essa tarefa, mas não mais do que se você mantivesse o aplicativo aberto. Portanto, o pré-carregamento é melhor usado com aplicativos grandes e usados com frequência, como Firefox e LibreOffice.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Go-preload](#Go-preload)
    *   [1.1 Configuração](#Configuração)
*   [2 Preload](#Preload)
    *   [2.1 Instalação](#Instalação)
    *   [2.2 Configuração](#Configuração_2)
*   [3 Veja também](#Veja_também)

## Go-preload

[gopreload-git](https://aur.archlinux.org/packages/gopreload-git/) é um pequeno daemon criado no [fórum do Gentoo](https://forums.gentoo.org/viewtopic-t-622085-highlight-preload.html). Para usá-lo, primeiro execute este comando em um terminal para cada programa que você deseja pré-carregar na inicialização:

```
# gopreload-prepare *programa*

```

Para usuários comuns, torne-se o dono de `/usr/share/gopreload/enabled` e `/usr/share/gopreload/disabled`:

```
# chown *usuário*:users /usr/share/gopreload/enabled /usr/share/gopreload/disabled

```

e execute gopreload para cada programa que você deseja pré-carregar:

```
$ gopreload-prepare *programa*

```

Em seguida, conforme as instruções, pressione Enter quando o programa estiver totalmente carregado. Isso adicionará uma lista de arquivos necessários pelo programa em `/usr/share/gopreload/enabled`. Para carregar todas as listas na inicialização, [habilite](/index.php/Habilite "Habilite") o arquivo de serviço do systemd `gopreload.service`.

Para desativar o carregamento de um programa, remova a lista apropriada em `/usr/share/gopreload/enabled` ou mova-a para `/usr/share/gopreload/disabled`.

É recomendável executar o *gopreload-prepare* após as atualizações do sistema para atualizar as listas de arquivos. Para a tarefa, a seguinte ferramenta em lote é útil:

```
# gopreload-batch-refresh.sh

```

Apenas deixe funcionar sem usar o sistema.

### Configuração

O arquivo de configuração está localizado em `/etc/gopreload.conf`

## Preload

*preload* é um programa escrito por Behdad Esfahbod que roda como um [daemon](/index.php/Daemon_(Portugu%C3%AAs) "Daemon (Português)") e registra estatísticas sobre o uso de programas usando cadeias de Markov; os arquivos dos programas mais usados são, durante o tempo livre do computador, carregados na memória. Isso resulta em tempos de inicialização mais rápidos, pois menos dados precisam ser buscados no disco.

### Instalação

[Instale](/index.php/Instale "Instale") o pacote [preload](https://aur.archlinux.org/packages/preload/). Agora [inicie](/index.php/Inicie "Inicie") o serviço systemd `preload`, e/ou [habilite](/index.php/Habilite "Habilite")-o para começar na inicialização.

### Configuração

O arquivo de configuração está localizado em `/etc/preload.conf`, contendo configurações padrão que devem ser adequadas para usuários comuns. A opção `cycle` permite configurar com que frequência executar ping no sistema de pré-carregamento para atualizar seu modelo de quais aplicativos e bibliotecas armazenar em cache.

## Veja também

*   [Wikipedia:pt:Preload](https://en.wikipedia.org/wiki/pt:Preload "wikipedia:pt:Preload")
*   [Melhorando o desempenho da inicialização](/index.php/Improve_boot_performance "Improve boot performance")