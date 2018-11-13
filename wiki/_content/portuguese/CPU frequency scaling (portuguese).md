## Contents

*   [1 Sumário](#Sumário)
*   [2 Instalação](#Instalação)
*   [3 Configuração](#Configuração)
    *   [3.1 Controlador da Frequência do CPU](#Controlador_da_Frequência_do_CPU)
    *   [3.2 Reguladores de Escalonamento](#Reguladores_de_Escalonamento)
    *   [3.3 Modo daemon](#Modo_daemon)

## Sumário

[cpufrequtils](https://www.archlinux.org/packages/?name=cpufrequtils) trata-se de um conjunto de utilitários projectados para assistir ao escalonamento da frequência do processador, tecnologia usada principalmente nos portáteis para permitir ao sistema operativo reduzir ou aumentar a frequência do processador consoante a necessidade actual, tornando o consumo energético mais eficiente.

## Instalação

O pacote [cpufrequtils](https://www.archlinux.org/packages/?name=cpufrequtils) está disponível no repositório. [Official repositories (Português)](/index.php/Official_repositories_(Portugu%C3%AAs) "Official repositories (Português)")

## Configuração

A configuração do escalonamento do CPU é um processo de 3 passos:

1.  Carregar o controlador apropriado para o CPU
2.  Carregar o regulador de frequência desejado
3.  Configurar e carregar o daemon de escalonamento de frequência (opcional)

### Controlador da Frequência do CPU

Para que o escalonamento de frequência funcione, o sistema operativo precisa de saber os limites do(s) teu(s) CPU(s). Para isso, temos de carregar um módulo do kernel que permita ler e gerir as espeficicações do(s) teu(s) CPU(s).

Os portáteis e desktops mais modernos podem simplesmente usar o driver `acpi-cpufreq`, apesar de existirem outras opções: `p4-clockmod`, `powernow-k6`, `powernow-k7`, `powernow-k8` e `speedstep-centrino`.

Para carregar o módulo do kernel manualmente:

```
# modprobe acpi-cpufreq

```

Para carregar automaticamente no arranque do sistema, adiciona o o driver respectivo ao array `MODULES` no ficheiro `/etc/rc.conf`. Por exemplo:

```
MODULES=( ***acpi-cpufreq*** vboxdrv fuse fglrx iwl3945 ... )

```

Uma vez carregado do driver apropriado, podes ver informação detalhado do(s) teu(s) CPU(s) executando:

```
$ cpufreq-info

```

Exemplo de output de `cpufreq-info` de um Intel Core 2 Duo T7200:

```
cpufrequtils 002: cpufreq-info (C) Dominik Brodowski 2004-2006
Report errors and bugs to linux@brodo.de, please.
analyzing CPU 0:
 driver: acpi-cpufreq
 CPUs which need to switch frequency at the same time: 0 1
 hardware limits: 996 MHz - 1.99 GHz
 available frequency steps: 1.99 GHz, 1.66 GHz, 1.33 GHz, 996 MHz
 available cpufreq governors: ondemand, performance
 current policy: frequency should be within 996 MHz and 1.99 GHz.
                 The governor "ondemand" may decide which speed to use
                 within this range.
 current CPU frequency is 996 MHz.
analyzing CPU 1:
 driver: acpi-cpufreq
 CPUs which need to switch frequency at the same time: 0 1
 hardware limits: 996 MHz - 1.99 GHz
 available frequency steps: 1.99 GHz, 1.66 GHz, 1.33 GHz, 996 MHz
 available cpufreq governors: ondemand, performance
 current policy: frequency should be within 996 MHz and 1.99 GHz.
                 The governor "ondemand" may decide which speed to use
                 within this range.
 current CPU frequency is 996 MHz.

```

### Reguladores de Escalonamento

Os reguladores podem ser vistos como definições pré-configuradas de energia para o CPU. Estes reguladores têm de ser carregados como módulos do kernel para serem vistos por programas como o kpoewrsave ou o gnome-power-manager. Podes carregar tantos quantos quiseres, mas não pode haver mais do que um activos em simultâneo.

Reguladores disponíveis:

	performance **(omissão)**

	O regulador performance está embutido no kernel e corre o(s) CPU(s) à frequẽncia máxima.

	cpufreq_ondemand *(recomendado)*

	Aumenta/diminui, de forma dinâmica, a velocidade do(s) CPU(s) baseado na necessidade do sistema.

	cpufreq_conservative

	Semelhante a 'ondemand', mas mais conservador (as mudanças de frequência não são tão repentinas, mas mais baseadas em médias de utilização).

	cpufreq_powersave

	Corre o(s) CPU(s) à velocidade mais baixa.

	cpufreq_userspace

	Velocidades definidas pelo utilizador.

Adiciona os reguladores desejados ao array MODULES no ficheiro `/etc/rc.conf`:

```
MODULES=(acpi-cpufreq ***cpufreq_ondemand cpufreq_powersave*** vboxdrv fuse fglrx iwl3945 ... )

```

Em alternativa, podes definir manualmente o regulador executando (como root) o comando `cpufreq-set`, mas o estado não será salvo quando o sistema for reiniciado. Por exemplo:

```
# cpufreq-set -g ondemand

```

Executa **`cpufreq-set --help`** ou **`man cpufreq-set`** para mais informação.

### Modo daemon

O `cpufrequtils` também instala um daemon que te permite definir o regulador desejado para velocidades mínimas/máximas no arranque sem a necessidade de ferramentas como kpowersave. Esta solução e perfeita para quem corre ambientes de trabalho leves, como Openbox.

Antes de iniciar o daemon, edita o ficheiro `/etc/conf.d/cpufreq` como root, seleccionando o regulador e definindo a velocidade mínima/máxima para o(s) teu(s) CPU(s), por exemplo:

```
#configuration for cpufreq control
# valid governors:
#  ondemand, performance, powersave,
#  conservative, userspace
governor="ondemand"

# valid suffixes: Hz, kHz (default), MHz, GHz, THz
min_freq="800MHz"
max_freq="2GHz"

```

**Nota:** Os valores min/max exactos para o(s) teu(s) CPU(s) podem ser verificados executando `cpufreq-info` depois de carregado o módulo referido no início (e.g. `modprobe acpi-cpufreq`). Contudo, estes valores são opcionais. Podes omiti-los completamente eliminando ou comentando as linhas respectivas, que tudo funcionará automaticamente, uma vez que o kernel consegue detectar os valores necessários.

Com o ficheiro de configuração tratado, podes agora iniciar o daemon com o seguinte comando:

```
# /etc/rc.d/cpufreq start

```

Para iniciar o daemon automaticamente no arranque, adiciona `cpufreq` ao array `DAEMONS` no ficheiro `/etc/rc.conf`, por exemplo:

```
DAEMONS=(syslog-ng hal ***cpufreq*** network netfs @alsa @crond @cupsd @fam @ntpd @sshd)

```