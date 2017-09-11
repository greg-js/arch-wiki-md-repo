Artigos relacionados

*   [systemd/User](/index.php/Systemd/User "Systemd/User")
*   [systemd FAQ](/index.php/Systemd_FAQ "Systemd FAQ")
*   [init Rosetta](/index.php/Init_Rosetta "Init Rosetta")
*   [Daemons List](/index.php/Daemons_List "Daemons List")
*   [udev](/index.php/Udev "Udev")
*   [Improve Boot Performance](/index.php/Improve_Boot_Performance "Improve Boot Performance")

De [project web page](http://freedesktop.org/wiki/Software/systemd):

	*Systemd* é um sistema e gerenciador de serviços para Linux, compatível com os scripts de inicializações SysV e LS. *Systemd* fornece recursos de paralelização agressivos, usa socket e ativação [D-Bus](/index.php/D-Bus "D-Bus") para iniciar serviços, oferece o início de daemons on-demand, mantém o registro de processos usando [grupos de controle](/index.php/Cgroups "Cgroups") Linux, suporte snapshotting e restauração do estado do sistema, preserva pontos de montagens e automontagens e implementa uma lógica de controle elaborado transacional baseada em dependência de serviço.

**Nota:** Para uma explicação detalhada do porquê Arch migrou para o *systemd*, consulte [esta mensagem do fórum internacional](https://bbs.archlinux.org/viewtopic.php?pid=1149530#p1149530).

## Contents

*   [1 Uso básico systemctl](#Uso_b.C3.A1sico_systemctl)
    *   [1.1 Analisando o estado do sistema](#Analisando_o_estado_do_sistema)
    *   [1.2 Usando units](#Usando_units)
    *   [1.3 O gerenciamento de energia](#O_gerenciamento_de_energia)
*   [2 Executando Gerenciadores de Display no systemd](#Executando_Gerenciadores_de_Display_no_systemd)
    *   [2.1 Usando systemd-logind](#Usando_systemd-logind)
*   [3 Arquivos temporários](#Arquivos_tempor.C3.A1rios)
*   [4 Escrevendo arquivos .service personalizados](#Escrevendo_arquivos_.service_personalizados)
    *   [4.1 Manuseando dependências](#Manuseando_depend.C3.AAncias)
    *   [4.2 Tipo](#Tipo)
    *   [4.3 Edição de arquivos units referidos](#Edi.C3.A7.C3.A3o_de_arquivos_units_referidos)
    *   [4.4 Realce de sintaxe para units dentro do Vim](#Realce_de_sintaxe_para_units_dentro_do_Vim)
*   [5 Targets](#Targets)
    *   [5.1 Obter targets atuais](#Obter_targets_atuais)
    *   [5.2 Criar target personalizada](#Criar_target_personalizada)
    *   [5.3 Tabela de targets](#Tabela_de_targets)
    *   [5.4 Alterar target atual](#Alterar_target_atual)
    *   [5.5 Alterar target padrão para inicializar](#Alterar_target_padr.C3.A3o_para_inicializar)
*   [6 Journal](#Journal)
    *   [6.1 Filtrando saída](#Filtrando_sa.C3.ADda)
    *   [6.2 Tamanho limite do Journal](#Tamanho_limite_do_Journal)
    *   [6.3 Journald em conjunto com o syslog](#Journald_em_conjunto_com_o_syslog)
*   [7 Solução de problemas](#Solu.C3.A7.C3.A3o_de_problemas)
    *   [7.1 Desligar/reiniciar demora um longo tempo](#Desligar.2Freiniciar_demora_um_longo_tempo)
    *   [7.2 Processos de curta duração não parecem registrar qualquer saída](#Processos_de_curta_dura.C3.A7.C3.A3o_n.C3.A3o_parecem_registrar_qualquer_sa.C3.ADda)
    *   [7.3 Diagnosticar problemas de inicialização](#Diagnosticar_problemas_de_inicializa.C3.A7.C3.A3o)
    *   [7.4 Desativando despejos de memória de aplicativos journaling](#Desativando_despejos_de_mem.C3.B3ria_de_aplicativos_journaling)
*   [8 Consulte também](#Consulte_tamb.C3.A9m)

## Uso básico systemctl

O principal comando usado para introspecção e controle *systemd* é **systemctl**. Alguns de seus usos são examinando o estado do sistema e gerenciando o sistema e serviços. Consulte [systemctl(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1) para mais detalhes.

**Dica:** Você pode usar todos os comandos *systemctl* com o `-H *user*@*host*` que muda para controlar uma instância *systemd* em uma máquina remota. Isso usará [SSH](/index.php/SSH "SSH") para conectar-se uma instância remota *systemd*.

**Nota:** *systemadm* é a interface gráfica oficial para *systemctl*. é fornecida pelo pacote [systemd-ui-git](https://aur.archlinux.org/packages/systemd-ui-git/) do [AUR](/index.php/AUR "AUR").

### Analisando o estado do sistema

Lista units executadas:

```
$ systemctl

```

ou:

```
$ systemctl list-units

```

Lista units que falharam::

```
$ systemctl --failed

```

Os arquivos units disponíveis podem ser vistos em `/usr/lib/systemd/system/` e `/etc/systemd/system/` (este último tem precedência). Você pode ver uma lista dos arquivos units instalados com:

```
$ systemctl list-unit-files

```

### Usando units

As units podem ser, por exemplo, serviços (*.service*), pontos de montagem (*.mount*), dispositivos (*.device*) ou sockets (*.socket*).

Quando usa *systemctl*, você geralmente tem que especificar o nome completo do arquivo unit, incluindo o sufixo, por exemplo *sshd.socket*. No entanto, existem algumas formas curtas de especificar a unit nos seguintes comandos *systemctl*:

*   Se você não especificar o sufixo, systemctl assumirá *.service*. Por exemplo, `netcfg` e `netcfg.service` são equivalentes.
*   Os pontos de montagem serão automaticamente convertidos para a unit *.mount* adequada. Por exemplo, especificando `/home` equivale a `home.mount`.
*   Similar aos pontos de montagem, dispositivos são automaticamente convertido para a unit *.device* adequada, portanto, especificando `/dev/sda2` equivale a `dev-sda2.device`.

Consulte [systemd.unit(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.unit.5) para detalhes.

Ativa uma unit imediatamente:

```
# systemctl start *unit*

```

Desativa uma unit imediatamente:

```
# systemctl stop *unit*

```

Reinicia uma unit:

```
# systemctl restart *unit*

```

Peça uma unit para recarregar sua configuração:

```
# systemctl reload *unit*

```

Mostra o estado de uma unit, inclusive se estiver em execução ou não:

```
$ systemctl status *unit*

```

Verifica se a unit já está habilitada ou não:

```
$ systemctl is-enabled *unit*

```

Habilita uma unit para ser iniciada na inicialização:

```
# systemctl enable *unit*

```

**Nota:** Serviços sem uma seção `[Install]` são geralmente chamados por outros serviços automaticamente. Se você precisa instalá-los manualmente, use o seguinte comando, substituindo *foo* com o nome do serviço.
```
# ln -s /usr/lib/systemd/system/*foo*.service /etc/systemd/system/graphical.target.wants/

```

Desativa uma unit para não iniciar durante a inicialização:

```
# systemctl disable *unit*

```

Mostra a página de manual associado a uma unit (tem que ser suportado pelo arquivo da unit):

```
$ systemctl help *unit*

```

Recarrega o *systemd*, scaneando por units novas e modificadas:

```
# systemctl daemon-reload

```

### O gerenciamento de energia

[polkit](/index.php/Polkit "Polkit") é necessário para o gerenciamento de energia. Se você está numa sessão de usuário local *systemd-logind* e nenhuma outra sessão está ativa, os seguintes comandos funcionarão sem privilégios root. Se não (por exemplo, porque outro usuário está conectado em um tty), *systemd* irá automaticamente pedir a senha de root.

Desliga e reinicia o sistema:

```
$ systemctl reboot

```

Desliga e encerra o sistema:

```
$ systemctl poweroff

```

Suspende o sistema:

```
$ systemctl suspend

```

Coloca o sistema em modo de hibernação:

```
$ systemctl hibernate

```

Coloca o sistema em modo de suspensão :

```
$ systemctl hybrid-sleep

```

## Executando Gerenciadores de Display no systemd

Para habilitar a autenticação gráfica, execute o seu daemon de [Display manager](/index.php/Display_manager "Display manager") preferido (ex. [KDM](/index.php/KDM "KDM")). No momento, existem arquivos de serviço para [GDM](/index.php/GDM "GDM"), [KDM](/index.php/KDM "KDM"), [SLiM](/index.php/SLiM "SLiM"), [XDM](/index.php/XDM "XDM"), [LXDM](/index.php/LXDM "LXDM"), [LightDM](/index.php/LightDM "LightDM"), e [sddm](https://www.archlinux.org/packages/?name=sddm).

```
# systemctl enable kdm

```

Isso deve funcionar. Se não, você pode ter que definir o *default.target manualmente* ou de uma velha instalação:

 `# ls -l /etc/systemd/system/default.target`  `/etc/systemd/system/default.target -> /usr/lib/systemd/system/graphical.target` 

Basta apagar o link simbólico e *systemd* usará seu *default.target* (ex. *graphical.target*).

```
# rm /etc/systemd/system/default.target

```

### Usando systemd-logind

A fim de verificar o estado de sua sessão de usuário, você pode usar `loginctl`. Todas ações [PolicyKit](/index.php/PolicyKit "PolicyKit") como suspender o sistema ou montar unidades externas irão funcionar.

```
$ loginctl show-session $XDG_SESSION_ID

```

## Arquivos temporários

**systemd-tmpfiles** usa arquivos de configuração em `/usr/lib/tmpfiles.d/` e `/etc/tmpfiles.d/` para descrever a criação, limpeza e remoção de arquivos e diretórios voláteis e temporários que normalmente residem em diretórios como `/run` ou `/tmp`. Cada arquivo de configuração é chamado no estilo `/etc/tmpfiles.d/*program*.conf`. Isso também irá substituir todos os arquivos em `/usr/lib/tmpfiles.d/` com o mesmo nome.

tmpfiles normalmente são fornecidos em conjunto com arquivos de serviços para criar diretórios que deverão existir por certas daemons. Por exemplo a daemon [Samba](/index.php/Samba "Samba") espera que o diretório `/run/samba` exista e tenha as permissões corretas. Assim, o pacote [samba](https://www.archlinux.org/packages/?name=samba) vem com esta configuração:

 `/usr/lib/tmpfiles.d/samba.conf`  `D /run/samba 0755 root root` 

tmpfiles também pode ser usado para escrever os valores em determinados arquivos na inicialização. Por exemplo, se você usa `/etc/rc.local` para desativar ativação de dispositivos USB com `echo USBE > /proc/acpi/wakeup`, você pode usar o seguinte tmpfile:

 `/etc/tmpfiles.d/disable-usb-wake.conf`  `w /proc/acpi/wakeup - - - - USBE` 

Consulte [tmpfiles.d(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/tmpfiles.d.5) para detalhes.

**Nota:** Este método pode não funcionar para definir as opções em `/sys` uma vez que o serviço *systemd-tmpfiles-setup* pode ser executado antes dos módulos de dispositivo apropriado for carregado. Neste caso, você pode verificar se o módulo tem um parâmetro para a opção que pretende definir com `modinfo *module*` e ajustar essa opção com um [arquivo de configuração em /etc/modprobe.d](/index.php/Modprobe.d#Configuration "Modprobe.d"). Caso contrário, você terá que escrever uma [regra udev](/index.php/Udev#About_udev_rules "Udev") para ajustar o atributo adequado logo que o dispositivo aparecer.

## Escrevendo arquivos .service personalizados

A sintaxe do systemd [arquivos unit](#Using_units) é inspirado pela Especificações de Entrada dos arquivos .desktop XDG Desktop, que são, por sua vez inspirado pelo .ini Microsoft Windows.

### Manuseando dependências

Com *systemd*, dependências podem ser resolvidas através da concepção de arquivos unit corretamente. O caso mais típico é a unit *A* requerer a unit *B* para ser executada antes da *A* ser iniciada. Nesse caso, adicione `Requires=*B*` e `After=*B*` para a seção `[Unit]` de *A*. Se a dependência for opcional, então adicione `Wants=*B*` e `After=*B*`. Nota que `Wants=` e `Requires=` não implicam `After=`, significando que se `After=` não for especificado, as duas units serão iniciada em paralelo.

Dependências são normalmente colocadas em serviços e não em targets. Por exemplo, o *network.target* é puxado por qualquer serviço que configure as interfaces de rede, portanto, ordenando a sua unit personalizada depois disso é o bastante desde que *network.target* é iniciado de qualquer maneira.

### Tipo

Há vários tipos diferentes de arranque a considerar quando se escreve um arquivo de serviço personalizado. Isso é definido com o parâmetro `Type=` na seção `[Service]`. Consulte [systemd.service(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.service.5) para uma explicação mais detalhada.

*   `Type=simple` (padrão): *systemd* considera que o serviço seja iniciado imediatamente. O processo não tem fork. Não use este tipo se outros serviços carecem ser solicitados neste serviço, a menos que seja socket ativado.
*   `Type=forking`: *systemd* considera que o serviço iniciou uma vez que os processos forks e o pai sairam. Para daemons clássicos use este tipo, a menos que você saiba que ele não é necessário. Deve especificar `PIDFile=` tão bem como *systemd* possa acompanhar o processo principal.
*   `Type=oneshot`: este é útil para os scripts que fazem um trabalho único e, em seguida, saem. Você pode querer definir `RemainAfterExit=yes` também para que *systemd* ainda considere o serviço como ativo depois que o processo foi encerrado.
*   `Type=notify`: idêntico ao `Type=simple`, mas com a condição de que o servidor irá enviar um sinal para *systemd* quando estiver pronto. A implementação de referência para essa notificação é fornecido pelo *libsystemd-daemon.so*.
*   `Type=dbus`: o serviço é considerado pronto quando o especificado `BusName` aparece no barramento do sistema do DBus.

### Edição de arquivos units referidos

Para editar um arquivo unit fornecido por um pacote, você pode criar um diretório chamado `/etc/systemd/system/*unit*.d/` por exemplo `/etc/systemd/system/httpd.service.d/` e coloque os arquivos **.conf* lá para substituir ou adicionar novas opções. *Systemd* irá analisar esses arquivos **.conf* e aplicá-los no topo da unit original. Por exemplo, se você simplesmente quiser adicionar uma dependência adicional para a unit, você pode criar o seguinte arquivo:

 `/etc/systemd/system/*unit*.d/customdependency.conf` 
```
[Unit]
Requires=*new dependency*
After=*new dependency*
```

Em seguida, execute os comandos para que as alterações tenham efeito:

```
# systemctl daemon-reload
# systemctl restart *unit*

```

Alternativamente, você pode copiar o antigo arquivo unit de `/usr/lib/systemd/system/` para `/etc/systemd/system/` e fazer suas modificações lá. Um arquivo unit em `/etc/systemd/system/` sempre sobrepõe a mesma unit em `/usr/lib/systemd/system/`. Note que quando a unit original em `/usr/lib/` é alterada devido a uma atualização de pacotes, essas alterações não serão aplicadas automaticamente ao seu arquivo unit personalizado em `/etc/`. Além disso, você vai ter que reativar manualmente a unit com `systemctl reenable *unit*`. Portanto, é recomendável usar o método **.conf* descrito anteriormente.

**Dica:** Você pode usar **systemd-delta** para ver quais arquivos units foram sobrescritos e o que exatamente foi alterado.

Como os arquivos units referidos serão atualizados ao longo do tempo, use *systemd-delta* para a manutenção do sistema.

### Realce de sintaxe para units dentro do Vim

Realce de sintaxe para arquivos unit *systemd* dentro do [Vim](/index.php/Vim "Vim") pode ser habilitado através da instalação do [vim-systemd](https://www.archlinux.org/packages/?name=vim-systemd) dos [repositórios oficiais](/index.php/Official_repositories "Official repositories").

## Targets

*Systemd* usa *targets* que servem a um propósito semelhante, como níveis de execução, mas agem um pouco diferente. Cada *target* é nomeada em vez de numerada e destina-se a servir uma finalidade específica com a possibilidade de ter múltiplos ativos ao mesmo tempo. Algumas *target*s são implementadas por herdar todos os serviços da outra *target* e adicionando serviços adicionais a ela. Há *target*s *systemd* que imitam os níveis de execução SystemVinit comuns para que possa mudar *target*s usando o comando familiar `telinit RUNLEVEL`.

### Obter targets atuais

O comando deve ser no *systemd* em vez de executar `runlevel`:

```
$ systemctl list-units --type=target

```

### Criar target personalizada

Os níveis de execução que são atribuídas uma finalidade específica na instalação vanilla Fedora; 0, 1, 3, 5, e 6; tem um mapeamento 1:1 com uma específica *target* *systemd*. Infelizmente, não há nenhuma boa forma de fazer o mesmo com os níveis de execução definidos pelo usuário, como 2 e 4\. Se você fizer uso deles é sugerido que você faça uma nova nomeação *target* *systemd* como `/etc/systemd/system/*your target*` que tem um dos níveis de execução existentes como base (você pode examinar `/usr/lib/systemd/system/graphical.target` como um exemplo), crie um diretório `/etc/systemd/system/*your target*.wants`, e então symlink o adicional serviço de `/usr/lib/systemd/system/` que você deseja ativar.

### Tabela de targets

| Modo de execução SysV | systemd Target | Notas |
| 0 | runlevel0.target, poweroff.target | Interrrompe o sistema. |
| 1, s, único | runlevel1.target, rescue.target | Modo de usuário único. |
| 2, 4 | runlevel2.target, runlevel4.target, multi-user.target | Níveis de execução User-defined/Site-specific. Por padrão, idêntico ao 3. |
| 3 | runlevel3.target, multi-user.target | Multi-usuário, não-gráfico. Os usuários geralmente podem acessar através de múltiplos consoles ou via rede. |
| 5 | runlevel5.target, graphical.target | Multi-usuário, gráfico. Normalmente tem todos os serviços do nível de execução 3, mais um login gráfico. |
| 6 | runlevel6.target, reboot.target | Reiniciar |
| emergência | emergency.target | Shell de emergência |

### Alterar target atual

No *systemd* targets estão expostas via *target units*. Você pode alterá-las assim:

```
# systemctl isolate graphical.target

```

Isso só vai mudar a target atual, e não tem nenhum efeito na próxima inicialização. É equivalente aos comandos como `telinit 3` ou `telinit 5` no Sysvinit.

### Alterar target padrão para inicializar

A target padrão é *default.target*, que tem alias por padrão para *graphical.target* (que corresponde ao antigo nível de execução 5).Para alterar o destino padrão na hora da inicialização, adicione um dos seguintes [parâmetros kernel](/index.php/Kernel_parameters "Kernel parameters") para o seu gerenciador de boot:

**Dica:** A extensão *.target* pode ser deixada de fora.

*   `systemd.unit=multi-user.target` (que corresponde ao antigo nível de execução 3),
*   `systemd.unit=rescue.target` (que corresponde ao antigo nível de execução 1).

Alternativamente, você pode deixar o gerenciador de boot sozinho e alterar *default.target*. Pode ser feito usando o *systemctl*:

```
# systemctl enable multi-user.target

```

O efeito desse comando é emitido pelo *systemctl*; um symlink para a nova target padrão é feita em `/etc/systemd/system/default.target`. Isso funciona se, e somente se:

```
[Install]
Alias=default.target

```

está no arquivo de configuração da target. Atualmente, *multi-user.target* e *graphical.target* ambos têm isso.

## Journal

*systemd* tem o seu próprio sistema de registro chamado de o journal e, portanto, a execução de uma daemon syslog não é mais necessário. Para ler o registro, utilize:

```
# journalctl

```

Por padrão (quando `Storage=` é definido para `auto` em `/etc/systemd/journald.conf`), o journal escreve para `/var/log/journal/`. O diretório `/var/log/journal/` faz parte do pacote *systemd*. Se você ou algum programa excluir esse diretório, systemd **não** irá recriá-lo automaticamente; no entanto, ele será recriado durante a próxima atualização do pacote systemd. Até então, os registros serão gravados em `/run/systemd/journal`, e os registros se perderão na reinicialização.

**Dica:** Se `/var/log/journal/` reside em um sistema de arquivo [btrfs](/index.php/Btrfs "Btrfs") você deve considerar a desativação [Copy-on-Write](/index.php/Btrfs#Copy-on-Write_.28CoW.29 "Btrfs") do diretório:
```
# chattr +C /var/log/journal

```

### Filtrando saída

*journalctl* permite filtrar a saída por campos específicos.

Exemplos:

Mostra todas as mensagens desta inicialização:

```
# journalctl -b

```

No entanto, muitas vezes alguém está interessado em mensagens não do atual, mas do boot anterior (por exemplo, se uma falha irrecuperável do sistema aconteceu). Atualmente, este recurso não está implementado, embora foi uma discussão em [systemd-devel@lists.freedesktop.org](http://comments.gmane.org/gmane.comp.sysutils.systemd.devel/6608) (Setembro/Outubro 2012).

Como alternativa você pode usar no momento:

```
# journalctl --since=today | tac | sed -n '/-- Reboot --/{n;:r;/-- Reboot --/q;p;n;b r}' | tac

```

desde que a inicialização anterior aconteceu hoje. Esteja ciente que, se houver muitas mensagens para o dia atual, a saída deste comando pode ser atrasada por um tempo.

**Nota:** Isso precisa ser corrigido uma vez que 206 regiões. `journalctl -b` agora assume argumentos como `-0` para a última inicialização ou uma ID de inicialização. Ex. `journalctl -b -3` vai mostrar todas as mensagens da quarta para a última inicialização.

Acompanhe as novas mensagens:

```
# journalctl -f

```

Mostra todas as mensagens por um executável específico:

```
# journalctl /usr/lib/systemd/systemd

```

Mostra todas as mensagens através de um processo específico:

```
# journalctl _PID=1

```

Mostra todas as mensagens de uma unit específica:

```
# journalctl -u netcfg

```

Consulte [journalctl(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/journalctl.1), [systemd.journal-fields(7)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.journal-fields.7), ou [mensagem do blog](http://0pointer.de/blog/projects/journalctl.html) de Lennert para detalhes.

### Tamanho limite do Journal

Se o journal é persistente (não volátil), seu tamanho limite é definido para um valor padrão de 10% do tamanho do respectivo sistema de arquivos. Por exemplo, com o `/var/log/journal` localizado em uma partição root de 50 GiB isso levaria a 5 GiB de dados do journal. O tamanho máximo do journal persistente pode ser controlado pelo `SystemMaxUse` em `/etc/systemd/journald.conf`, então para limitá-lo, por exemplo, a 50 MiB descomente e edite a linha correspondente a:

```
SystemMaxUse=50M

```

Consulte [journald.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/journald.conf.5) para mais informações.

### Journald em conjunto com o syslog

Compatibilidade com implementações do syslog clássico é fornecida através da socket `/run/systemd/journal/syslog`, para o qual todas as mensagens são encaminhadas. Para fazer funcionar a daemon syslog com o journal, tem de vincular a este socket em vez de `/dev/log` ([official announcement](http://lwn.net/Articles/474968/)). O pacote [syslog-ng](https://www.archlinux.org/packages/?name=syslog-ng) nos repositórios fornece automaticamente a configuração necessária.

```
# systemctl enable syslog-ng

```

Um bom tutorial *journalctl* está [aqui](http://0pointer.de/blog/projects/journalctl.html).

## Solução de problemas

### Desligar/reiniciar demora um longo tempo

Se o processo de encerramento tem um tempo muito longo (ou parece congelar) mais provavelmente um serviço que não encerra é o responsável. *Systemd* espera um tempo para cada serviço terminar antes de tentar matá-lo. Para descobrir se você foi afetado, consulte [this article](http://freedesktop.org/wiki/Software/systemd/Debugging#Shutdown_Completes_Eventually).

### Processos de curta duração não parecem registrar qualquer saída

Se `journalctl -u foounit` não mostra nenhuma saída para um serviço de curta duração, veja o PID em vez disso. Por exemplo, se `systemd-modules-load.service` falha, e `systemctl status systemd-modules-load` mostra que executou com PID 123, então você talvez possa ver uma saída no journal por esse PID, ou seja, `journalctl -b _PID=123`. Campos de metadados para o journal como _SYSTEMD_UNIT e _COMM são coletados de forma assíncrona e invocam o diretório `/proc` para o processo existente. A solução deste problema requer fixar o kernel para fornecer esses dados através de uma conexão de socket, semelhante ao SCM_CREDENTIALS.

### Diagnosticar problemas de inicialização

Inicialização desses parâmetros na linha de comando do kernel: `systemd.log_level=debug systemd.log_target=kmsg log_buf_len=1M`

[More Debugging Information](http://freedesktop.org/wiki/Software/systemd/Debugging)

### Desativando despejos de memória de aplicativos journaling

Para voltar os arquivos normais de despejo de memória, edite o seguinte arquivo de forma que sobrescreva os ajustes de `/lib/sysctl.d/`:

 `/etc/sysctl.d/49-coredump.conf` 
```
kernel.core_pattern = core
kernel.core_uses_pid = 0
```

Então execute:

```
# /usr/lib/systemd/systemd-sysctl

```

Como antes, você também precisa o tamanho "unlimit" dos arquivos de núcleo no shell:

```
$ ulimit -c unlimited

```

Consulte [sysctl.d](http://www.freedesktop.org/software/systemd/man/sysctl.d.html) e [a documentação para /proc/sys/kernel](https://www.kernel.org/doc/Documentation/sysctl/kernel.txt) para mais informações.

## Consulte também

*   [Official web site](http://www.freedesktop.org/wiki/Software/systemd)
*   [Wikipedia article](https://en.wikipedia.org/wiki/systemd "wikipedia:systemd")
*   [Manual pages](http://0pointer.de/public/systemd-man/)
*   [systemd optimizations](http://freedesktop.org/wiki/Software/systemd/Optimizations)
*   [FAQ](http://www.freedesktop.org/wiki/Software/systemd/FrequentlyAskedQuestions)
*   [Tips and tricks](http://www.freedesktop.org/wiki/Software/systemd/TipsAndTricks)
*   [systemd for Administrators (PDF)](http://0pointer.de/public/systemd-ebook-psankar.pdf)
*   [About systemd on Fedora Project](http://fedoraproject.org/wiki/Systemd)
*   [How to debug systemd problems](http://fedoraproject.org/wiki/How_to_debug_Systemd_problems)
*   [Two](http://www.h-online.com/open/features/Control-Centre-The-systemd-Linux-init-system-1565543.html) [part](http://www.h-online.com/open/features/Booting-up-Tools-and-tips-for-systemd-1570630.html) introductory article in *The H Open* magazine.
*   [Lennart's blog story](http://0pointer.de/blog/projects/systemd.html)
*   [Status update](http://0pointer.de/blog/projects/systemd-update.html)
*   [Status update2](http://0pointer.de/blog/projects/systemd-update-2.html)
*   [Status update3](http://0pointer.de/blog/projects/systemd-update-3.html)
*   [Most recent summary](http://0pointer.de/blog/projects/why.html)
*   [Fedora's SysVinit to systemd cheatsheet](http://fedoraproject.org/wiki/SysVinit_to_Systemd_Cheatsheet)