**Status de tradução:** Esse artigo é uma tradução de [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling"). Data da última tradução: 2020-01-25\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=CPU_frequency_scaling&diff=0&oldid=588936) na versão em inglês.

Artigos relacionados

*   [Economia de energia](/index.php/Power_saving "Power saving")
*   [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools")
*   [PHC](/index.php/PHC "PHC")

A escala de frequência da CPU permite que o sistema operacional aumente ou diminua a frequência da CPU para economizar energia. Frequências de CPU podem ser escalonadas automaticamente dependendo da carga do sistema, em resposta a eventos ACPI, ou manualmente por programas espaço do usuário.

O escalonamento de frequência da CPU é implementado no kernel do Linux, a infraestrutura é chamada de *cpufreq*. Desde o kernel 3.4, os módulos necessários são carregados automaticamente e o [regulador ondemand](#Escalonando_reguladores) recomendado é ativado por padrão. No entanto, as ferramentas de espaço do usuário, como [cpupower](#cpupower), [acpid](/index.php/Acpid "Acpid"), [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools") ou ferramentas GUI fornecidas para o seu ambiente de área de trabalho, ainda podem ser usadas para configuração avançada.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Ferramentas de espaço do usuário](#Ferramentas_de_espaço_do_usuário)
    *   [1.1 thermald](#thermald)
    *   [1.2 i7z](#i7z)
    *   [1.3 cpupower](#cpupower)
    *   [1.4 cpupower-gui](#cpupower-gui)
*   [2 Drivers de frequência de CPU](#Drivers_de_frequência_de_CPU)
    *   [2.1 Configurando frequências máxima e mínima](#Configurando_frequências_máxima_e_mínima)
    *   [2.2 Desabilitando Turbo Boost](#Desabilitando_Turbo_Boost)
        *   [2.2.1 intel_pstate](#intel_pstate)
        *   [2.2.2 acpi-cpufreq](#acpi-cpufreq)
*   [3 Escalonando reguladores](#Escalonando_reguladores)
    *   [3.1 Ajustando o regulador ondemand](#Ajustando_o_regulador_ondemand)
        *   [3.1.1 Trocando o limite](#Trocando_o_limite)
        *   [3.1.2 Taxa de amostragem](#Taxa_de_amostragem)
        *   [3.1.3 Tornar as alterações permanentes](#Tornar_as_alterações_permanentes)
*   [4 Interação com eventos da ACPI](#Interação_com_eventos_da_ACPI)
*   [5 Concessão de privilégios no GNOME](#Concessão_de_privilégios_no_GNOME)
*   [6 Solução de problemas](#Solução_de_problemas)
    *   [6.1 Limitação de frequências da BIOS](#Limitação_de_frequências_da_BIOS)
*   [7 Veja também](#Veja_também)

## Ferramentas de espaço do usuário

### thermald

[thermald](https://aur.archlinux.org/packages/thermald/) é um daemon do Linux usado para evitar o superaquecimento de plataformas. Esse daemon monitora a temperatura e aplica compensação usando os métodos de resfriamento disponíveis.

Por padrão, ele monitora a temperatura da CPU usando sensores de temperatura digital da CPU disponíveis e mantém a temperatura da CPU sob controle, antes que o hardware execute uma ação de correção agressiva. Se houver um sensor de temperatura da pele em sysfs térmicos, ele tentará manter a temperatura da pele abaixo de 45°C.

A unit de systemd associada é `thermald.service`, que deve ser [iniciada](/index.php/Inicia "Inicia") e [habilitada](/index.php/Habilita "Habilita").

### i7z

[i7z](https://www.archlinux.org/packages/?name=i7z) é uma ferramenta de relatório de CPUs i7 (e agora i3, i5) para o Linux. Pode ser iniciada de um Terminal com o comando `i7z` ou como interface gráfica com `i7z-gui`.

### cpupower

O [cpupower](https://www.archlinux.org/packages/?name=cpupower) é um conjunto de utilitários do espaço de usuário projetado para auxiliar no dimensionamento de frequência da CPU. O pacote não é necessário para usar o escalonamento, mas é altamente recomendado porque ele fornece utilitários de linha de comando úteis e um serviço [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") para alterar o gerenciador na inicialização.

O arquivo de configuração do *cpupower* encontra-se em `/etc/default/cpupower`. Esse arquivo de configuração é lido por um script em bash em `/usr/lib/systemd/scripts/cpupower` que é ativado por *systemd* com `cpupower.service`. Você pode querer [habilitar](/index.php/Habilitar "Habilitar") `cpupower.service` para iniciar na inicialização.

### cpupower-gui

[cpupower-gui](https://aur.archlinux.org/packages/cpupower-gui/) é um utilitário gráfico desenvolvido para auxiliar no dimensionamento da frequência da CPU. A GUI é baseada em [GTK](/index.php/GTK_(Portugu%C3%AAs) "GTK (Português)") e deve fornecer as mesmas opções que *cpupower*. O *cpupower-gui* pode alterar a frequência e o regulador máximo/mínimo da CPU para cada núcleo. O aplicativo manipula a concessão de privilégios por meio do [polkit](/index.php/Polkit "Polkit") e permite que qualquer usuário do [grupo de usuários](/index.php/Grupo_de_usu%C3%A1rios "Grupo de usuários") `wheel` altere a frequência e o regulador.

## Drivers de frequência de CPU

**Nota:**

*   O módulo nativo da CPU é carregado automaticamente.
*   O driver de escala de energia `pstate` é usado automaticamente para CPUs Intel modernas, em vez dos outros drivers abaixo. Este driver tem prioridade sobre outros drivers e é embutido em vez de ser um módulo. Este driver é usado automaticamente para o Sandy Bridge e CPUs mais recentes. Se você encontrar um problema ao usar este driver, adicione `intel_pstate=disable` à sua linha do kernel. Você pode usar os mesmos utilitários de espaço do usuário com este driver, **mas não pode controlá-lo**.
*   Mesmo o comportamento do estado P mencionado acima pode ser influenciado com `/sys/devices/system/cpu/intel_pstate`, por exemplo, o Intel Turbo Boost pode ser desativado com `# echo 1 > /sys/devices/system/cpu/intel_pstate/no_turbo` para manter baixas as temperaturas da CPU.
*   Controle adicional para os modernos processadores da Intel está disponível com o [Linux Thermal Daemon](https://01.org/linux-thermal-daemon) (disponível como [thermald](https://aur.archlinux.org/packages/thermald/)), que proativamente controla a térmica usando estados P, estados T e o driver da clamp de energia da Intel. Thermald também pode ser usado para CPUs Intel mais antigas. Se os drivers mais recentes não estiverem disponíveis, o daemon será revertido para registros específicos do modelo x86 e o "subsistema cpufreq" do Linux para controlar o resfriamento do sistema.

*cpupower* requer módulos para conhecer os limites da CPU nativa:

| Módulo | Descrição |
| intel_pstate | Esse driver implementa um driver de escalonamento com um controlador interno para processadores Intel Core (Sandy Bridge e mais recentes). |
| acpi-cpufreq | Driver CPUFreq que utiliza os estados de desempenho do processador ACPI. Este driver também possui suporte ao Intel Enhanced SpeedStep (anteriormente com suporte pelo módulo speedstep-centrino obsoleto). |
| speedstep-lib | Driver CPUFreq para processadores habilitados para Intel SpeedStep (principalmente Atoms e Pentiums mais antigos (até III)) |
| powernow-k8 | Driver CPUFreq para processadores K8/K10 Athlon 64/Opteron/Phenom. Desde o Linux 3.7, "acpi-cpufreq" será automaticamente usado para CPUs mais modernas desta família. |
| pcc-cpufreq | Este controlador possui suporte a interface de Processing Clocking Control da Hewlett-Packard e Microsoft Corporation, que é útil em alguns servidores ProLiant. |
| p4-clockmod | Driver CPUFreq para processadores Intel Pentium 4/Xeon/Celeron que reduz a temperatura da CPU, ignorando os relógios. (Você provavelmente deseja usar um driver SpeedStep). |

Para ver uma lista completa de módulos disponíveis, execute:

```
$ ls /usr/lib/modules/$(uname -r)/kernel/drivers/cpufreq/

```

Carregue o módulo apropriado (veja [Módulos de kernel](/index.php/Kernel_module_(Portugu%C3%AAs) "Kernel module (Português)") para detalhes). Depois que o driver cpufreq apropriado é carregado, informações detalhadas sobre a(s) CPU(s) podem ser exibidas executando

```
$ cpupower frequency-info

```

### Configurando frequências máxima e mínima

Em alguns casos, pode ser necessário definir manualmente as frequências máxima e mínima.

Para definir a frequência máxima do relógio (`*freq_do_clock*` é uma frequência de relógio com unidades: GHz, MHz):

```
# cpupower frequency-set -u *freq_do_clock*

```

Para definir uma frequência de clock mínima:

```
# cpupower frequency-set -d *freq_do_clock*

```

Para definir a CPU para executar em uma frequência especificada:

```
# cpupower frequency-set -f *freq_do_clock*

```

**Nota:**

*   Para ajustar apenas para um único core de CPU, acrescente `-c *número_do_core*`.
*   As frequências máxima e mínima do regulador podem ser definidas em `/etc/default/cpupower`.

Alternativamente, você pode definir a frequência manualmente:

```
# echo *valor* > /sys/devices/system/cpu/cpu*/cpufreq/scaling_max_freq

```

Os valores disponíveis podem ser definidos em `/sys/devices/system/cpu/cpu*/cpufreq/scaling_available_frequencies` ou similar. [[1]](https://software.intel.com/sites/default/files/comment/1716807/how-to-change-frequency-on-linux-pub.txt)

### Desabilitando Turbo Boost

#### intel_pstate

```
# echo 1 > /sys/devices/system/cpu/intel_pstate/no_turbo

```

#### acpi-cpufreq

1.  echo 0 > /sys/devices/system/cpu/cpufreq/boost

## Escalonando reguladores

Os reguladores (veja a tabela abaixo) são esquemas de energia para a CPU. Apenas um pode estar ativo de cada vez. Para detalhes, veja a [documentação do kernel](https://www.kernel.org/doc/Documentation/cpu-freq/governors.txt) na fonte do kernel.

| Regulador | Descrição |
| performance | Executa a CPU na frequência máxima. |
| powersave | Executa a CPU na frequência mínima. |
| userspace | Execute a CPU nas frequências especificadas pelo usuário. |
| ondemand | Escalona a frequência dinamicamente conforme a carga atual. Pula para a frequência mais alta e então volta conforme o tempo de ociosidade aumenta. |
| conservative | Escalona a frequência dinamicamente conforme a carga atual. Escalona a frequência de forma mais gradual que o "ondemand". |
| schedutil | Seleção de frequência da CPU controlada pelo agendador [[2]](https://lwn.net/Articles/682391/), [[3]](https://lkml.org/lkml/2016/3/17/420). |

Dependendo do driver de escalonamento, um dos reguladores serão carregados por padrão:

*   `ondemand` para CPUs AMD e Intel mais antigos.
*   `powersave` para CPUs Intel mais novas usando o driver `intel_pstate` (Sandy Bridge e mais novas).

**Nota:** O driver `intel_pstate` possui suporte apenas aos reguladores de desempenho e de economia de energia, mas ambos fornecem escalonamento dinâmico. O regulador de desempenho [deve oferecer melhor funcionalidade de economia de energia do que o antigo controlador "ondemand"](http://www.phoronix.com/scan.php?page=news_item&px=MTM3NDQ).

**Atenção:** Use as ferramentas de monitoramento da CPU (para temperaturas, voltagens, etc.) ao alterar o regulador padrão.

Para ativar um regulador em particular, execute:

```
# cpupower frequency-set -g *regulador*

```

**Nota:**

*   Para ajustar apenas para um único core de CPU, acrescente `-c *número_do_core*` ao comando acima.
*   A ativação de um regulador requer que um [módulo de kernel](/index.php/Kernel_module_(Portugu%C3%AAs) "Kernel module (Português)") específico (chamado `cpufreq_*regulador*`) esteja carregado. Desde o kernel 3.4, esses módulos são carregados automaticamente.

Alternativamente, você pode ativar um regulador a cada CPU disponível manualmente com:

```
# echo *regulador* > /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor

```

sendo `*regulador*` o nome do regulador, relacionado na tabela acima, que você deseja ativar.

**Dica:** Para monitorar a velocidade de CPU em tempo real, execute:
```
$ watch grep \"cpu MHz\" /proc/cpuinfo

```

### Ajustando o regulador ondemand

Veja a [documentação do kernel](https://www.kernel.org/doc/Documentation/cpu-freq/governors.txt) para detalhes.

#### Trocando o limite

Para definir o limite *(threshold)* para avançar para outra frequência:

```
# echo -n *percentagem* > /sys/devices/system/cpu/cpufreq/<regulador>/up_threshold

```

Para definir o limite para retroceder para outra frequência:

```
# echo -n *percentagem* > /sys/devices/system/cpu/cpufreq/<regulador>/down_threshold

```

#### Taxa de amostragem

A taxa de amostragem determina com que frequência o controlador verifica a sintonia da CPU. `sampling_down_factor` é um ajuste que multiplica a taxa de amostragem quando a CPU está com a frequência de clock mais alta, atrasando a avaliação da carga e melhorando o desempenho. Os valores permitidos para `sampling_down_factor` são de 1 a 100.000\. Esse ajuste não tem efeito sobre o comportamento em frequências/cargas de CPU mais baixas.

Para ler o valor (padrão = 1), execute:

```
$ cat /sys/devices/system/cpu/cpufreq/ondemand/sampling_down_factor

```

Para definir o valor, execute:

```
# echo -n *valor* > /sys/devices/system/cpu/cpufreq/ondemand/sampling_down_factor

```

#### Tornar as alterações permanentes

Para que o escalonamento desejado seja habilitado na inicialização, [opções de módulo do kernel](/index.php/Kernel_module_(Portugu%C3%AAs)#Usando_arquivos_em_/etc/modprobe.d/ "Kernel module (Português)") e [systemd (Português)#Arquivos temporários](/index.php/Systemd_(Portugu%C3%AAs)#Arquivos_temporários "Systemd (Português)") são métodos regulares.

Por exemplo, alterar o up_threshold para 10:

 `/etc/tmpfiles.d/ondemand.conf`  `w- /sys/devices/system/cpu/cpufreq/ondemand/up_threshold - - - - 10` 

No entanto, em alguns casos, pode haver condições de corrida, conforme observado em [systemd (Português)#Arquivos temporários](/index.php/Systemd_(Portugu%C3%AAs)#Arquivos_temporários "Systemd (Português)"), podem existir e é possível usar o [udev](/index.php/Udev "Udev") para evitá-los.

Por exemplo, para configurar o controlador de escala do núcleo da CPU `0` para desempenho enquanto o driver de escala for `acpi_cpufreq`, crie a seguinte regra de udev:

 `/etc/udev/rules.d/50-scaling-governor.rules`  `SUBSYSTEM=="module", ACTION=="add", KERNEL=="acpi_cpufreq", RUN+="/bin/sh -c 'echo performance > /sys/devices/system/cpu/cpufreq/policy0/scaling_governor'"` 

Para ter a regra já aplicada no *initramfs*, siga o exemplo em [udev#Debug output](/index.php/Udev#Debug_output "Udev").

**Dica:** Alternativamente, configure o utilitário [cpupower](#cpupower) e habilite seu serviço de systemd.

## Interação com eventos da ACPI

Os usuários podem configurar os reguladores de escala para alternar automaticamente com base em diferentes eventos ACPI, como conectar o adaptador AC ou fechar uma tampa do laptop. Um exemplo rápido é dado abaixo, no entanto, pode valer a pena ler o artigo completo sobre [acpid](/index.php/Acpid "Acpid").

Eventos são definidos em `/etc/acpi/handler.sh`. Se o pacote [acpid](https://www.archlinux.org/packages/?name=acpid) estiver instalado, o arquivo já deverá existir e ser executável. Por exemplo, para alterar o regulador de escala de `performance` para `conservative` quando o adaptador de CA for desconectado e alterá-lo de volta, se reconectar:

 `/etc/acpi/handler.sh` 
```
[...]

ac_adapter)
    case "$2" in
        AC*)
            case "$4" in
                00000000)
                    echo "conservative" >/sys/devices/system/cpu/cpu0/cpufreq/scaling_governor
                    echo -n $minspeed >$setspeed
                    #/etc/laptop-mode/laptop-mode start
                ;;
                00000001)
                    echo "performance" >/sys/devices/system/cpu/cpu0/cpufreq/scaling_governor
                    echo -n $maxspeed >$setspeed
                    #/etc/laptop-mode/laptop-mode stop
                ;;
            esac
        ;;
        *) logger "ACPI action undefined: $2" ;;
    esac
;;

[...]

```

## Concessão de privilégios no GNOME

**Nota:** systemd introduziu o logind que lida com ações consolekit e policykit. O código a seguir não funciona. Com logind, basta editar no arquivo `/usr/share/polkit-1/actions/org.gnome.cpufreqselector.policy` os elementos <defaults> conforme a suas necessidades e o manual do polkit [[4]](http://www.freedesktop.org/software/polkit/docs/latest/polkit.8.html).

[GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)") tem um miniaplicativo legal para mudar o regulador na hora. Para usá-lo sem a necessidade de inserir a senha de root, basta criar o seguinte arquivo:

 `/var/lib/polkit-1/localauthority/50-local.d/org.gnome.cpufreqselector.pkla` 
```
[org.gnome.cpufreqselector]
Identity=unix-user:*usuário*
Action=org.gnome.cpufreqselector
ResultAny=no
ResultInactive=no
ResultActive=yes
```

sendo `*usuário*` o nome de usuário interessado.

O pacote [desktop-privileges](https://aur.archlinux.org/packages/desktop-privileges/) no [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)") contém um arquivo `.pkla` para autorizar todos os usuários do [grupo de usuários](/index.php/Grupo_de_usu%C3%A1rios "Grupo de usuários") `power` para alterar o regulador.

## Solução de problemas

*   Alguns aplicativos, como [ntop](/index.php/Ntop "Ntop"), não respondem bem ao escalonamento automático de frequência. No caso de ntop, isso pode resultar em falhas de segmentação e muitas informações perdidas, pois mesmo o regulador `on-demand` não pode alterar a frequência com rapidez suficiente quando muitos pacotes chegam de repente à interface de rede monitorada que não pode ser manipulado pela velocidade atual do processador.

*   Algumas CPUs podem sofrer um desempenho ruim com as configurações padrão do regulador `on-demand` (por exemplo, vídeos em flash que não reproduzem suavemente ou animações instáveis de janelas). Em vez de desativar completamente o escalonamento de frequência para resolver esses problemas, a agressividade do escalonamento de frequência pode ser aumentada diminuindo a variável *up_threshold* do [sysctl](/index.php/Sysctl "Sysctl") para cada CPU. Veja [como alterar o limite do regulador sob demanda](#Trocando_o_limite).

*   Às vezes, o regulador sob demanda pode não acelerar até a frequência máxima, mas um passo abaixo. Isto pode ser resolvido ajustando o valor de max_freq para ligeiramente mais alto que o máximo real. Por exemplo, se a faixa de frequência da CPU for de 2,00 GHz a 3,00 GHz, configurar max_freq para 3,01 GHz pode ser uma boa ideia.

*   Algumas combinações de drivers e chips de som [ALSA](/index.php/ALSA_(Portugu%C3%AAs) "ALSA (Português)") podem causar saltos de áudio enquanto o regulador muda entre as frequências, e a mudança de volta para um regulador que não muda muda a parada do áudio.

### Limitação de frequências da BIOS

Algumas configurações de CPU/BIOS podem ter dificuldades para escalar até a frequência máxima ou escalar para frequências mais altas. Isso é provavelmente causado por eventos do BIOS dizendo ao sistema operacional para limitar a frequência resultando em `/sys/devices/system/cpu/cpu0/cpufreq/bios_limit` definido como um valor mais baixo.

Ou você acabou de fazer uma configuração específica no utilitário de configuração da BIOS (frequência, gerenciamento térmico, etc.), você pode culpar uma BIOS com bugs/desatualizada ou a BIOS pode ter uma razão séria para limitar a CPU por conta própria.

Razões como essa podem ser (supondo que sua máquina seja um notebook) que a bateria está desconectada (ou quase no fim da vida útil), então você está apenas em energia da fonte de alimentação. Neste caso, uma fonte de alimentação fraca pode não fornecer eletricidade suficiente para atender às demandas de pico extremo pelo sistema geral e, como não há bateria para ajudar, isso pode levar à perda de dados, corrupção de dados ou, no pior dos casos, até mesmo danos ao hardware!

Nem todos as BIOS limitam a frequência da CPU neste caso, mas, por exemplo, a maioria dos thinkpads IBM/Lenovo. Consulte thinkwiki para obter mais [informações relacionadas a thinkpad sobre este tópico](http://www.thinkwiki.org/wiki/Problem_with_CPU_frequency_scaling).

Se você verificou que não há apenas uma configuração estranha do BIOS e sabe o que está fazendo, pode fazer com que o Kernel ignore essas limitações do BIOS.

**Atenção:** Certifique-se de ler e entender a seção acima. A limitação de frequência da CPU é um recurso de segurança da sua BIOS e você não deve precisar contorná-la.

Um parâmetro especial deve ser passado para o módulo do processador.

Para tentar isso temporariamente, alerte o valor em `/sys/module/processor/parameters/ignore_ppc` de `0` para `1`.

Para definir permanentemente, [Kernel module (Português)#Opções de configuração de módulos](/index.php/Kernel_module_(Portugu%C3%AAs)#Opções_de_configuração_de_módulos "Kernel module (Português)") descreve alternativas. Por exemplo, você pode adicionar `processor.ignore_ppc=1` à sua linha de inicialização de kernel ou crie

 `/etc/modprobe.d/ignore_ppc.conf` 
```
# Se a frequência de sua máquina for limitada de forma errada pela BIOS, isso deve ajudar
options processor ignore_ppc=1
```

## Veja também

*   [Linux CPUFreq - documentação do kernel](https://www.kernel.org/doc/Documentation/cpu-freq/index.txt)
*   [Explicação compreensiva de pstate](http://www.reddit.com/r/linux/comments/1hdogn/acpi_cpufreq_or_intel_pstates/)
*   [Controle de impulsão de processador](https://www.kernel.org/doc/Documentation/cpu-freq/boost.txt)