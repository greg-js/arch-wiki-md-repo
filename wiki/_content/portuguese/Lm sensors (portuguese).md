**Status de tradução:** Esse artigo é uma tradução de [lm_sensors](/index.php/Lm_sensors "Lm sensors"). Data da última tradução: 2019-05-24\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Lm_sensors&diff=0&oldid=573846) na versão em inglês.

Artigos relacionados

*   [Controle da velocidade do cooler](/index.php/Fan_speed_control "Fan speed control")
*   [hddtemp](/index.php/Hddtemp "Hddtemp")
*   [monitorix](/index.php/Monitorix "Monitorix")

[lm_sensors](http://lm-sensors.org/) (*Linux monitoring sensors*) é um aplicativo livre e de código aberto que fornece ferramentas e drivers para monitorar temperaturas, tensão e ventiladores. Este documento explica como instalar, configurar e usar o *lm_sensors*.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Configuração](#Configuração)
*   [3 Execução de sensors](#Execução_de_sensors)
    *   [3.1 Lendo valores SPD de módulos de memória (opcional)](#Lendo_valores_SPD_de_módulos_de_memória_(opcional))
*   [4 Usando dados de sensores](#Usando_dados_de_sensores)
    *   [4.1 Front-ends gráficos](#Front-ends_gráficos)
    *   [4.2 sensord](#sensord)
*   [5 Dicas e truques](#Dicas_e_truques)
    *   [5.1 Ajustando valores](#Ajustando_valores)
        *   [5.1.1 Exemplo 1\. Ajustante posições de temperatura](#Exemplo_1._Ajustante_posições_de_temperatura)
        *   [5.1.2 Exemplo 2\. Renomeando rótulos](#Exemplo_2._Renomeando_rótulos)
        *   [5.1.3 Exemplo 3\. Renumerando núcleos para sistemas com várias CPUs](#Exemplo_3._Renumerando_núcleos_para_sistemas_com_várias_CPUs)
    *   [5.2 Implantação automática de lm_sensors](#Implantação_automática_de_lm_sensors)
*   [6 Solução de problemas](#Solução_de_problemas)
    *   [6.1 Módulo K10Temp](#Módulo_K10Temp)
    *   [6.2 Placas-mãe Asus Z97/Z170](#Placas-mãe_Asus_Z97/Z170)
    *   [6.3 Placas-mãe Gigabyte B250](#Placas-mãe_Gigabyte_B250)
    *   [6.4 Gigabyte GA-J1900N-D3V](#Gigabyte_GA-J1900N-D3V)
    *   [6.5 Problemas na tela do laptop após a execução de sensors-detect](#Problemas_na_tela_do_laptop_após_a_execução_de_sensors-detect)

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [lm_sensors](https://www.archlinux.org/packages/?name=lm_sensors).

**Nota:** Mais documentação está no [repositório GitHub](https://github.com/groeck/lm-sensors/tree/master/doc). No futuro, esses podem ser instalados, veja [FS#48354](https://bugs.archlinux.org/task/48354).

## Configuração

Use *sensors-detect* como root para detectar e gere uma lista de módulos de kernel:

**Atenção:** Não uso nada além das opções padrão (só pressionando `Enter`), a menos que você saiba exatamente o que você está fazendo. Veja [#Problemas na tela do laptop após a execução de sensors-detect](#Problemas_na_tela_do_laptop_após_a_execução_de_sensors-detect).

```
# sensors-detect

```

Ele pedirá para sondar vários hardwares. As respostas "seguras" são os padrões, então apenas pressionar `Enter` para todas as perguntas geralmente não causará nenhum problema. Isso criará o arquivo de configuração `/etc/conf.d/lm_sensors` que é usado por `lm_sensors.service` para carregar automaticamente os módulos do kernel na inicialização.

Quando a detecção é concluída, um resumo das sondas é apresentado.

Exemplo:

 `# sensors-detect` 
```
This program will help you determine which kernel modules you need
to load to use lm_sensors most effectively. It is generally safe
and recommended to accept the default answers to all questions,
unless you know what you're doing.

Some south bridges, CPUs or memory controllers contain embedded sensors.
Do you want to scan for them? This is totally safe. (YES/no): 
Module cpuid loaded successfully.
Silicon Integrated Systems SIS5595...                       No
VIA VT82C686 Integrated Sensors...                          No
VIA VT8231 Integrated Sensors...                            No
AMD K8 thermal sensors...                                   No
AMD Family 10h thermal sensors...                           No

...

Now follows a summary of the probes I have just done.
Just press ENTER to continue: 

Driver `coretemp':
  * Chip `Intel digital thermal sensor' (confidence: 9)

Driver `lm90':
  * Bus `SMBus nForce2 adapter at 4d00'
    Busdriver `i2c_nforce2', I2C address 0x4c
    Chip `Winbond W83L771AWG/ASG' (confidence: 6)

Do you want to overwrite /etc/conf.d/lm_sensors? (YES/no): 
ln -s '/usr/lib/systemd/system/lm_sensors.service' '/etc/systemd/system/multi-user.target.wants/lm_sensors.service'
Unloading i2c-dev... OK
Unloading cpuid... OK

```

**Nota:** Um serviço systemd é ativado automaticamente se os usuários responderem **YES** quando perguntados sobre a geração de `/etc/conf.d/lm_sensors`. Respondendo **SIM** também inicia automaticamente o serviço.

## Execução de sensors

Exemplo de execução do `sensors`:

 `$ sensors` 
```
coretemp-isa-0000
Adapter: ISA adapter
Core 0:       +35.0°C  (crit = +105.0°C)
Core 1:       +32.0°C  (crit = +105.0°C)

w83l771-i2c-0-4c
Adapter: SMBus nForce2 adapter at 4d00
temp1:        +28.0°C  (low  = -40.0°C, high = +70.0°C)
                       (crit = +85.0°C, hyst = +75.0°C)
temp2:        +37.4°C  (low  = -40.0°C, high = +70.0°C)
                       (crit = +110.0°C, hyst = +100.0°C)

```

### Lendo valores SPD de módulos de memória (opcional)

Para ler os valores de tempo de SPD de módulos de memória, instale o pacote [i2c-tools](https://www.archlinux.org/packages/?name=i2c-tools). Uma vez instalado, carregue [módulo de kernel](/index.php/Kernel_module "Kernel module") `eeprom`.

```
# modprobe eeprom

```

Finalmente, veja informações de memória com `decode-dimms`.

Aqui está uma saída parcial de uma máquina:

 `# decode-dimms` 
```
Memory Serial Presence Detect Decoder
By Philip Edelbrock, Christian Zuckschwerdt, Burkart Lingner,
Jean Delvare, Trent Piepho and others

Decoding EEPROM: /sys/bus/i2c/drivers/eeprom/0-0050
Guessing DIMM is in                             bank 1

---=== SPD EEPROM Information ===---
EEPROM CRC of bytes 0-116                       OK (0x583F)
# of bytes written to SDRAM EEPROM              176
Total number of bytes in EEPROM                 512
Fundamental Memory type                         DDR3 SDRAM
Module Type                                     UDIMM

---=== Memory Characteristics ===---
Fine time base                                  2.500 ps
Medium time base                                0.125 ns
Maximum module speed                            1066MHz (PC3-8533)
Size                                            2048 MB
Banks x Rows x Columns x Bits                   8 x 14 x 10 x 64
Ranks                                           2
SDRAM Device Width                              8 bits
tCL-tRCD-tRP-tRAS                               7-7-7-33
Supported CAS Latencies (tCL)                   8T, 7T, 6T, 5T

---=== Timing Parameters ===---
Minimum Write Recovery time (tWR)               15.000 ns
Minimum Row Active to Row Active Delay (tRRD)   7.500 ns
Minimum Active to Auto-Refresh Delay (tRC)      49.500 ns
Minimum Recovery Delay (tRFC)                   110.000 ns
Minimum Write to Read CMD Delay (tWTR)          7.500 ns
Minimum Read to Pre-charge CMD Delay (tRTP)     7.500 ns
Minimum Four Activate Window Delay (tFAW)       30.000 ns

---=== Optional Features ===---
Operable voltages                               1.5V
RZQ/6 supported?                                Yes
RZQ/7 supported?                                Yes
DLL-Off Mode supported?                         No
Operating temperature range                     0-85C
Refresh Rate in extended temp range             1X
Auto Self-Refresh?                              Yes
On-Die Thermal Sensor readout?                  No
Partial Array Self-Refresh?                     No
Thermal Sensor Accuracy                         Not implemented
SDRAM Device Type                               Standard Monolithic

---=== Physical Characteristics ===---
Module Height (mm)                              15
Module Thickness (mm)                           1 front, 1 back
Module Width (mm)                               133.5
Module Reference Card                           B

---=== Manufacturer Data ===---
Module Manufacturer                             Invalid
Manufacturing Location Code                     0x02
Part Number                                     OCZ3G1600LV2G     

...

```

## Usando dados de sensores

### Front-ends gráficos

Há uma variedade de front-ends para dados de sensores.

*   **psensor** — Aplicativo GTK+ para monitorar sensores de hardware, incluindo temperaturas e velocidades do cooler. Monitora placa-mãe e CPU (usando lm-sensors), Nvidia GPUs (usando XNVCtrl) e harddisks (usando [hddtemp](/index.php/Hddtemp "Hddtemp") ou libatasmart).

	[https://wpitchoune.net/psensor/](https://wpitchoune.net/psensor/) || [psensor](https://www.archlinux.org/packages/?name=psensor)

*   **xsensors** — Interface X11 para o lm_sensors.

	[http://linuxhardware.org/xsensors/](http://linuxhardware.org/xsensors/) || [xsensors](https://www.archlinux.org/packages/?name=xsensors)

Para [Ambientes de desktop](/index.php/Ambientes_de_desktop "Ambientes de desktop") específicos:

*   **Freon (Extensão do GNOME Shell)** — Extensão para exibir temperatura de CPU, temperatura do disco, temperatura da placa de vídeo, voltagem e RPM do cooler no [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)") Shell.

	[https://github.com/UshakovVasilii/gnome-shell-extension-freon](https://github.com/UshakovVasilii/gnome-shell-extension-freon) || [gnome-shell-extension-freon](https://aur.archlinux.org/packages/gnome-shell-extension-freon/)

*   **GNOME Sensors Applet** — Miniaplicativo para o painel do [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)") para exibir leituras dos sensores do hardware, incluindo leituras de temperatura de CPU, velocidades de coolers e voltagem.

	[http://sensors-applet.sourceforge.net/](http://sensors-applet.sourceforge.net/) || [sensors-applet](https://www.archlinux.org/packages/?name=sensors-applet)

*   **lm-sensors (plugin de LXPanel)** — Monitora temperatura/voltagens/velocidades de cooler no [LXDE](/index.php/LXDE "LXDE") por meio de lm-sensors.

	[http://danamlund.dk/sensors_lxpanel_plugin/](http://danamlund.dk/sensors_lxpanel_plugin/) || [sensors-lxpanel-plugin](https://aur.archlinux.org/packages/sensors-lxpanel-plugin/)

*   **MATE Sensors Applet** — Exibe leituras de sensores de hardware no seu painel do [MATE](/index.php/MATE "MATE").

	[https://github.com/mate-desktop/mate-sensors-applet](https://github.com/mate-desktop/mate-sensors-applet) || [mate-sensors-applet](https://www.archlinux.org/packages/?name=mate-sensors-applet)

*   **Sensors (Plugin do painel do Xfce4)** — Plugin de sensores de hardware para o painel do [Xfce](/index.php/Xfce "Xfce").

	[http://goodies.xfce.org/projects/panel-plugins/xfce4-sensors-plugin](http://goodies.xfce.org/projects/panel-plugins/xfce4-sensors-plugin) || [xfce4-sensors-plugin](https://www.archlinux.org/packages/?name=xfce4-sensors-plugin)

*   **Thermal Monitor (Miniaplicativo do Plasma 5)** — Miniaplicativo do Plasma para [KDE](/index.php/KDE "KDE") para monitoramento de CPU, GPU e outros sensores de temperatura disponíveis.

	[https://github.com/kotelnik/plasma-applet-thermal-monitor](https://github.com/kotelnik/plasma-applet-thermal-monitor) || [plasma5-applets-thermal-monitor-git](https://aur.archlinux.org/packages/plasma5-applets-thermal-monitor-git/)

### sensord

Existe um daemon opcional chamado *sensord* (incluído no pacote [lm_sensors](https://www.archlinux.org/packages/?name=lm_sensors)) que pode registrar dados em um banco de dados round robin (rrd) e depois visualizar graficamente. Veja a página man [sensord(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sensord.8) para detalhes.

## Dicas e truques

### Ajustando valores

Em alguns casos, os dados exibidos podem estar incorretos ou os usuários podem desejar renomear a saída. Casos de uso incluem:

*   Valores incorretos de temperatura devido a um deslocamento incorreto (isto é, os tempos são relatados 20°C mais altos do que os reais).
*   Usuários desejam renomear a saída de alguns sensores.
*   Os *cores* podem ser exibidos em uma ordem incorreta.

Todos os itens acima (e mais) podem ser ajustados sobrepondo as configurações do pacote em `/etc/sensors3.conf` criando `/etc/sensors.d/*foo*` em que qualquer número de os ajustes substituirão os valores padrão. Recomenda-se renomear 'foo' para a marca e modelo da placa-mãe, mas esta nomenclatura de nomenclatura é opcional.

**Nota:** Não edite `/etc/sensors3.conf` diretamente, já que atualizações de pacotes vão sobrescrever quaisquer alterações, consequentemente perdendo-as.

#### Exemplo 1\. Ajustante posições de temperatura

Este é um exemplo real de uma placa-mãe Zotac ION-ITX-A-U. Os valores de coretemp estão desativados em 20°C (muito alto) e são ajustados de acordo com as especificações da Intel.

 `$ sensors` 
```
coretemp-isa-0000
Adapter: ISA adapter
Core 0:       +57.0°C  (crit = +125.0°C)
Core 1:       +55.0°C  (crit = +125.0°C)
...

```

Execute `sensors` com a opção `-u` para ver quais opções estão disponíveis para cada chip físico (modo "raw"):

 `$ sensors -u` 
```
coretemp-isa-0000
Adapter: ISA adapter
Core 0:
  temp2_input: 57.000
  temp2_crit: 125.000
  temp2_crit_alarm: 0.000
Core 1:
  temp3_input: 55.000
  temp3_crit: 125.000
  temp3_crit_alarm: 0.000
...

```

Crie o seguinte arquivo substituindo os valores padrão:

 `/etc/sensors.d/Zotac-IONITX-A-U` 
```
chip "coretemp-isa-0000"
  label temp2 "Core 0"
  compute temp2 @-20,@-20

  label temp3 "Core 1"
  compute temp3 @-20,@-20

```

Agora, chamar `sensors` mostra os valores ajustados:

 `$ sensors` 
```
coretemp-isa-0000
Adapter: ISA adapter
Core 0:       +37.0°C  (crit = +105.0°C)
Core 1:       +35.0°C  (crit = +105.0°C)
...

```

#### Exemplo 2\. Renomeando rótulos

Este é um exemplo real em um Asus A7M266\. O usuário deseja nomes mais detalhados para os rótulos de temperatura "temp1" e "temp2":

 `$ sensors` 
```
as99127f-i2c-0-2d
Adapter: SMBus Via Pro adapter at e800
...
temp1:        +35.0°C  (high =  +0.0°C, hyst = -128.0°C)
temp2:        +47.5°C  (high = +100.0°C, hyst = +75.0°C)
...

```

Crie o seguinte arquivo para substituir os valores padrão:

 `/etc/sensors.d/Asus_A7M266` 
```
chip "as99127f-*"
  label temp1 "Mobo Temp"
  label temp2 "CPU0 Temp"

```

Agora, chamar `sensors` mostra os valores ajustados:

 `$ sensors` 
```
as99127f-i2c-0-2d
Adapter: SMBus Via Pro adapter at e800
...
Mobo Temp:        +35.0°C  (high =  +0.0°C, hyst = -128.0°C)
CPU0 Temp:        +47.5°C  (high = +100.0°C, hyst = +75.0°C)
...

```

#### Exemplo 3\. Renumerando núcleos para sistemas com várias CPUs

Este é um exemplo real de uma estação de trabalho HP Z600 com Xeons duplos. A numeração real dos núcleos físicos está incorreta: numerada 0, 1, 9, 10, que é repetida na segunda CPU. A maioria dos usuários espera que as temperaturas do núcleo relatem em ordem sequencial, ou seja, 0,1,2,3,4,5,6,7.

 `$ sensors` 
```
coretemp-isa-0000
Adapter: ISA adapter
Core 0:       +65.0°C  (high = +85.0°C, crit = +95.0°C)
Core 1:       +65.0°C  (high = +85.0°C, crit = +95.0°C)
Core 9:       +66.0°C  (high = +85.0°C, crit = +95.0°C)
Core 10:      +66.0°C  (high = +85.0°C, crit = +95.0°C)

coretemp-isa-0004
Adapter: ISA adapter
Core 0:       +54.0°C  (high = +85.0°C, crit = +95.0°C)
Core 1:       +56.0°C  (high = +85.0°C, crit = +95.0°C)
Core 9:       +60.0°C  (high = +85.0°C, crit = +95.0°C)
Core 10:      +61.0°C  (high = +85.0°C, crit = +95.0°C)
...

```

Agora, execute `sensors` com a opção `-u` para ver quais opções estão disponíveis para cada chip físico:

 `$ sensors -u coretemp-isa-0000` 
```
coretemp-isa-0000
Adapter: ISA adapter
Core 0:
  temp2_input: 61.000
  temp2_max: 85.000
  temp2_crit: 95.000
  temp2_crit_alarm: 0.000
Core 1:
  temp3_input: 61.000
  temp3_max: 85.000
  temp3_crit: 95.000
  temp3_crit_alarm: 0.000
Core 9:
  temp11_input: 62.000
  temp11_max: 85.000
  temp11_crit: 95.000
Core 10:
  temp12_input: 63.000
  temp12_max: 85.000
  temp12_crit: 95.000

```
 `$ sensors -u coretemp-isa-0004` 
```
coretemp-isa-0004
Adapter: ISA adapter
Core 0:
  temp2_input: 53.000
  temp2_max: 85.000
  temp2_crit: 95.000
  temp2_crit_alarm: 0.000
Core 1:
  temp3_input: 54.000
  temp3_max: 85.000
  temp3_crit: 95.000
  temp3_crit_alarm: 0.000
Core 9:
  temp11_input: 59.000
  temp11_max: 85.000
  temp11_crit: 95.000
Core 10:
  temp12_input: 59.000
  temp12_max: 85.000
  temp12_crit: 95.000
...

```

Crie o seguinte arquivo substituindo os valores padrão:

 `/etc/sensors.d/HP_Z600` 
```
chip "coretemp-isa-0000"
  label temp2 "Core 0"
  label temp3 "Core 1"
  label temp11 "Core 2"
  label temp12 "Core 3"

chip "coretemp-isa-0004"
  label temp2 "Core 4"
  label temp3 "Core 5"
  label temp11 "Core 6"
  label temp12 "Core 7"
```

Agora, chamar `sensors` mostra os valores ajustados:

 `$ sensors` 
```
coretemp-isa-0000
Adapter: ISA adapter
Core0:        +64.0°C  (high = +85.0°C, crit = +95.0°C)
Core1:        +63.0°C  (high = +85.0°C, crit = +95.0°C)
Core2:        +65.0°C  (high = +85.0°C, crit = +95.0°C)
Core3:        +66.0°C  (high = +85.0°C, crit = +95.0°C)

coretemp-isa-0004
Adapter: ISA adapter
Core4:        +53.0°C  (high = +85.0°C, crit = +95.0°C)
Core5:        +54.0°C  (high = +85.0°C, crit = +95.0°C)
Core6:        +59.0°C  (high = +85.0°C, crit = +95.0°C)
Core7:        +60.0°C  (high = +85.0°C, crit = +95.0°C)
...

```

### Implantação automática de lm_sensors

Os usuários que desejam implantar lm_sensors em várias máquinas podem usar o seguinte para aceitar os valores padrão para todas as perguntas:

```
# sensors-detect --auto

```

## Solução de problemas

### Módulo K10Temp

Alguns processadores K10 têm problemas com seu sensor de temperatura. Da documentação do kernel (`linux-<version>/Documentation/hwmon/k10temp`):

	*Todos esses processadores possuem um sensor, mas para o soquete F ou AM2+, o sensor pode retornar valores inconsistentes (errata 319). O driver se recusará a carregar nessas revisões, a menos que os usuários especifiquem o parâmetro do módulo `force=1`.*

	*Devido a razões técnicas, o driver pode detectar apenas o tipo de soquete da placa-mãe, não os recursos reais do processador. Portanto, os usuários de um processador AM3 em uma placa-mãe AM2+ podem usar com segurança o parâmetro `force=1`.*

Em máquinas afetadas, o módulo relatará "unreliable CPU thermal sensor; monitoring disabled". Usuários que desejam forçá-lo podem:

```
# rmmod k10temp
# modprobe k10temp force=1

```

Confirme se o sensor é de fato válido e confiável. Se estiver, pode editar `/etc/modprobe.d/k10temp.conf` e adicionar:

```
options k10temp force=1

```

Isso vai permitir o módulo para carregar na inicialização.

### Placas-mãe Asus Z97/Z170

Com algumas placas-mãe recentes da Asus, o acesso ao ventilador e ao sensor de tensão pode exigir o módulo NCT6775:

```
 # modprobe nct6775

```

e adicione-o aos parâmetros do kernel de inicialização:

```
 acpi_enforce_resources=lax

```

### Placas-mãe Gigabyte B250

Algumas placa-mãe da Gigabyte usam o chip ITE IT8686E, ao qual o driver it87 do kernel não dá suporte, até maio de 2019 [[1]](https://www.kernel.org/doc/Documentation/hwmon/it87).

Porém, há suporte na versão do upstream do driver de kernel [[2]](https://github.com/bbqlinux/it87/blob/master/it87.c#L24).

A variante dkms está contida em [it87-dkms-git](https://aur.archlinux.org/packages/it87-dkms-git/).

### Gigabyte GA-J1900N-D3V

Essa placa-mãe usa o chip ITE IT8620E (útil também para ler voltagens, temperatura da placa principal, velocidade do cooler). Até outubro de 2014, lm_sensors não tem suporte de driver para o chip ITE IT8620E [[3]](https://hwmon.wiki.kernel.org/device_support_status_g_i) [[4]](http://comments.gmane.org/gmane.linux.drivers.sensors/35168). Os desenvolvedores do lm_sensors tinham um relatório de que o chip é um pouco compatível com o IT8728F para a parte de monitoramento de hardware. No entanto, a partir de agosto de 2016, [[5]](https://www.kernel.org/doc/Documentation/hwmon/it87) lista o IT8620E como suportado.

Você pode carregar o módulo em tempo de execução com modprobe:

```
$ modprobe it87 force_id=0x8728

```

Ou você pode [carregar os módulos](/index.php/Kernel_modules "Kernel modules") durante o processo de inicialização criando os seguintes arquivos:

 `/etc/modules-load.d/it87.conf`  `it87`  `/etc/modprobe.d/it87.conf`  `options it87 force_id=0x8603` 

Quando o módulo estiver carregado, você pode usar a ferramenta *sensores* para testar o chip.

Você também pode usar [fancontrol](/index.php/Fancontrol "Fancontrol") para controlar os "speedsteps" de do cooler do gabinete.

### Problemas na tela do laptop após a execução de sensors-detect

Isso é causado por lm_sensors mexendo nos valores Vcom da tela enquanto sondam sensores. Já foi discutido e resolvido nos fóruns: [https://bbs.archlinux.org/viewtopic.php?id=193048](https://bbs.archlinux.org/viewtopic.php?id=193048) No entanto, certifique-se de ler o tópico cuidadosamente antes de executar qualquer um dos comandos sugeridos.