Artigos relacionados

*   [systemd/User](/index.php/Systemd/User "Systemd/User")
*   [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers")
*   [systemd FAQ](/index.php/Systemd_FAQ "Systemd FAQ")
*   [init](/index.php/Init "Init")
*   [Daemons](/index.php/Daemons_(Portugu%C3%AAs) "Daemons (Português)")
*   [udev](/index.php/Udev "Udev")
*   [Melhorar desempenho/Processo de inicialização](/index.php/Improving_performance/Boot_process "Improving performance/Boot process")
*   [Permitir desligamento por usuários](/index.php/Allow_users_to_shutdown "Allow users to shutdown")

De [página web do projeto](http://freedesktop.org/wiki/Software/systemd):

	*Systemd* é um sistema e gerenciador de serviços para Linux, compatível com os scripts de inicializações SysV e LS. *Systemd* fornece recursos de paralelização agressivos, usa socket e ativação [D-Bus](/index.php/D-Bus "D-Bus") para iniciar serviços, oferece o início de daemons on-demand, mantém o registro de processos usando [grupos de controle](/index.php/Cgroups "Cgroups") Linux, suporte snapshotting e restauração do estado do sistema, preserva pontos de montagens e automontagens e implementa uma lógica de controle elaborado transacional baseada em dependência de serviço. O *systemd* oferece suporte scripts de init SysV e LSB e funciona como um substituto para o sysvinit. Outras partes incluem um daemon de registro, utilitários para controlar a configuração básica do sistema como o nome do host, data, local, manter uma lista de usuários logados e executar contêineres e máquinas virtuais, contas do sistema, diretórios e configurações de tempo de execução e daemons para gerenciar configuração de redes simples, sincronização de tempo de rede, encaminhamento de log e resolução de nomes.

**Nota:** Para uma explicação detalhada do porquê Arch migrou para o *systemd*, consulte [esta mensagem do fórum internacional](https://bbs.archlinux.org/viewtopic.php?pid=1149530#p1149530).

## Contents

*   [1 Uso básico systemctl](#Uso_b.C3.A1sico_systemctl)
    *   [1.1 Analisando o estado do sistema](#Analisando_o_estado_do_sistema)
    *   [1.2 Usando units](#Usando_units)
    *   [1.3 Gerenciamento de energia](#Gerenciamento_de_energia)
*   [2 Escrevendo arquivos unit](#Escrevendo_arquivos_unit)
    *   [2.1 Manuseando dependências](#Manuseando_depend.C3.AAncias)
    *   [2.2 Tipos de serviços](#Tipos_de_servi.C3.A7os)
    *   [2.3 Editando units fornecidas](#Editando_units_fornecidas)
        *   [2.3.1 Arquivos unit de substituição](#Arquivos_unit_de_substitui.C3.A7.C3.A3o)
        *   [2.3.2 Arquivos drop-in](#Arquivos_drop-in)
        *   [2.3.3 Reverter para versão do vendor](#Reverter_para_vers.C3.A3o_do_vendor)
        *   [2.3.4 Exemplos](#Exemplos)
*   [3 Targets](#Targets)
    *   [3.1 Obter targets atuais](#Obter_targets_atuais)
    *   [3.2 Criar target personalizado](#Criar_target_personalizado)
    *   [3.3 Mapeamento entre níveis do SysV e targets do systemd](#Mapeamento_entre_n.C3.ADveis_do_SysV_e_targets_do_systemd)
    *   [3.4 Alterar target atual](#Alterar_target_atual)
    *   [3.5 Alterar target padrão para inicializar](#Alterar_target_padr.C3.A3o_para_inicializar)
    *   [3.6 Ordem de target padrão](#Ordem_de_target_padr.C3.A3o)
*   [4 Arquivos temporários](#Arquivos_tempor.C3.A1rios)
*   [5 Timers](#Timers)
*   [6 Montagem](#Montagem)
*   [7 Journal](#Journal)
    *   [7.1 Nível de prioridade](#N.C3.ADvel_de_prioridade)
    *   [7.2 Facilidade](#Facilidade)
    *   [7.3 Filtrando saída](#Filtrando_sa.C3.ADda)
    *   [7.4 Limite no tamanho do journal](#Limite_no_tamanho_do_journal)
    *   [7.5 Limpar arquivos de journal manualmente](#Limpar_arquivos_de_journal_manualmente)
    *   [7.6 Journald em conjunto com o syslog](#Journald_em_conjunto_com_o_syslog)
    *   [7.7 Encaminhar journald para /dev/tty12](#Encaminhar_journald_para_.2Fdev.2Ftty12)
    *   [7.8 Especificar um journal diferente para ver](#Especificar_um_journal_diferente_para_ver)
*   [8 Dicas e truques](#Dicas_e_truques)
    *   [8.1 Executando serviços após a rede estar ativa](#Executando_servi.C3.A7os_ap.C3.B3s_a_rede_estar_ativa)
    *   [8.2 Habilitar units instaladas por padrão](#Habilitar_units_instaladas_por_padr.C3.A3o)
    *   [8.3 Usando ambientes de aplicativos em *sandbox*](#Usando_ambientes_de_aplicativos_em_sandbox)
*   [9 Solução de problemas](#Solu.C3.A7.C3.A3o_de_problemas)
    *   [9.1 Investigar erros no systemd](#Investigar_erros_no_systemd)
    *   [9.2 Diagnosticar problemas de inicialização](#Diagnosticar_problemas_de_inicializa.C3.A7.C3.A3o)
    *   [9.3 Diagnosticar um serviço](#Diagnosticar_um_servi.C3.A7o)
    *   [9.4 Desligamento/reinicialização demora demais](#Desligamento.2Freinicializa.C3.A7.C3.A3o_demora_demais)
    *   [9.5 Processos de curta duração não parecem registrar qualquer saída](#Processos_de_curta_dura.C3.A7.C3.A3o_n.C3.A3o_parecem_registrar_qualquer_sa.C3.ADda)
    *   [9.6 Tempo de inicialização aumentando com o tempo](#Tempo_de_inicializa.C3.A7.C3.A3o_aumentando_com_o_tempo)
    *   [9.7 systemd-tmpfiles-setup.service não inicia na inicialização do sistema](#systemd-tmpfiles-setup.service_n.C3.A3o_inicia_na_inicializa.C3.A7.C3.A3o_do_sistema)
    *   [9.8 A versão impressa do systemd na inicialização não é a mesma da versão do pacote instalado](#A_vers.C3.A3o_impressa_do_systemd_na_inicializa.C3.A7.C3.A3o_n.C3.A3o_.C3.A9_a_mesma_da_vers.C3.A3o_do_pacote_instalado)
    *   [9.9 Desabilitar modo de emergência em máquina remota](#Desabilitar_modo_de_emerg.C3.AAncia_em_m.C3.A1quina_remota)
*   [10 Veja também](#Veja_tamb.C3.A9m)

## Uso básico systemctl

O principal comando usado para introspecção e controle *systemd* é *systemctl*. Alguns de seus usos são examinando o estado do sistema e gerenciando o sistema e serviços. Consulte [systemctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1) para mais detalhes.

**Dica:**

*   Você pode usar todos os comandos de *systemctl* abaixo com a opção `-H *usuário*@*host*` para controlar uma instância de *systemd* em uma máquina remota. Isso usará [SSH](/index.php/SSH "SSH") para se conectar uma instância remota *systemd*.
*   Usuários de [Plasma](/index.php/Plasma "Plasma") podem instalar [systemd-kcm](https://aur.archlinux.org/packages/systemd-kcm/) como um frontend gráfico para *systemctl*. Após a instalação, o módulo será adicionar sob *Administração de sistema*.

### Analisando o estado do sistema

Mostre **status do sustema** usando:

```
$ systemctl status

```

Liste units **em execução**:

```
$ systemctl

```

ou:

```
$ systemctl list-units

```

Liste units **que falharam**:

```
$ systemctl --failed

```

Os arquivos units disponíveis podem ser vistos em `/usr/lib/systemd/system/` e `/etc/systemd/system/` (este último tem precedência). Liste os arquivos unit **instalados** com:

```
$ systemctl list-unit-files

```

### Usando units

As units podem ser, por exemplo, serviços (*.service*), pontos de montagem (*.mount*), dispositivos (*.device*) ou soquetes (*.socket*).

Quando usa *systemctl*, você geralmente tem que especificar o nome completo do arquivo unit, incluindo o sufixo, por exemplo `sshd.socket`. No entanto, existem algumas formas curtas de especificar a unit nos seguintes comandos *systemctl*:

*   Se você não especificar o sufixo, systemctl presumirá *.service*. Por exemplo, `netctl` e `netctl.service` são equivalentes.
*   Os pontos de montagem serão automaticamente convertidos para a unit *.mount* adequada. Por exemplo, especificar `/home` equivale a `home.mount`.
*   Similar aos pontos de montagem, dispositivos são automaticamente convertidos para a unit *.device* adequada, portanto, especificar `/dev/sda2` equivale a `dev-sda2.device`.

Veja [systemd.unit(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.unit.5) para detalhes.

**Nota:** Alguns nomes de unit contêm um sinal `@` (por exemplo, `nome@*string*.service`): isso significa que eles são [instâncias](http://0pointer.de/blog/projects/instances.html) de uma unit *modelo* (em inglês, *template*), cujo nome real do arquivo não contém a parte `*string*` (por exemplo, `nome@.service`). `*string*` é chamado de *identificador de instância* (em inglês, *instance identifier*) e é semelhante a um argumento que é passado para a unit modelo quando chamado com o comando *systemctl*: no arquivo unit, ele irá substituir o especificador `%i`.

Para ser mais preciso, *antes* de tentar instanciar a unit modelo `nome@.suffix`, o *systemd* vai, na verdade, procurar por uma unit com o nome de arquivo exato `nome@string.sufixo`, embora por convenção tal "conflito" ocorra raramente, ou seja, a maioria dos arquivos unit contendo um sinal `@` são destinados a serem um modelo. Além disso, se uma unit modelo for chamada sem um identificador de instância, ela falhará, pois o especificador `%i` não conseguirá ser substituído.

**Dica:**

*   A maioria dos comandos a seguir também funciona se várias units forem especificadas; veja [systemctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1) para obter mais informações.
*   A opção `--now` pode ser usada em conjunto com `enable`, `disable` e `mask` para iniciar, parar ou mascarar, respectivamente, imediatamente a unit em vez de após na próxima inicialização.
*   Um pacote pode oferecer units para diferentes finalidades. Se você acabou de instalar um pacote, `pacman -Qql *pacote* | grep -Fe .service -e .socket` pode ser usado para verificar e localizá-las.

**Inicia** uma unit imediatamente:

```
# systemctl start *unit*

```

**Para** uma unit imediatamente:

```
# systemctl stop *unit*

```

**Reinicia** uma unit:

```
# systemctl restart *unit*

```

Pede a uma unit para **recarregar** sua configuração:

```
# systemctl reload *unit*

```

Mostra o **status** de uma unit, inclusive se estiver em execução ou não:

```
$ systemctl status *unit*

```

**Verifica** se a unit já está habilitada ou não:

```
$ systemctl is-enabled *unit*

```

**Habilita** uma unit para ser iniciada na **inicialização**:

```
# systemctl enable *unit*

```

**Habilita** uma unit para ser iniciada na **inicialização** e **inicia-a** imediatamente:

```
# systemctl enable --now *unit*

```

**Desabilita** uma unit para não ser iniciada durante a inicialização:

```
# systemctl disable *unit*

```

**Mascara** uma unit para tornar impossível iniciá-la (Tanto manualmente quanto como uma dependência, o que torna mascaragem perigoso):

```
# systemctl mask *unit*

```

**Desmascara** uma unit:

```
# systemctl unmask *unit*

```

Mostra a **página de manual** associado a uma unit (tem que haver suporte no arquivo da unit):

```
$ systemctl help *unit*

```

Recarrega o *systemd*, procurando por **units novas e modificadas**:

```
# systemctl daemon-reload

```

### Gerenciamento de energia

[polkit](/index.php/Polkit "Polkit") é necessário para o gerenciamento de energia como um usuário sem privilégios. Se você está em uma sessão de usuário local *systemd-logind* e nenhuma outra sessão está ativa, os seguintes comandos funcionarão sem privilégios de root. Se não (por exemplo, porque outro usuário está conectado em um tty), *systemd* vai automaticamente pedir a senha de root.

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

Coloca o sistema em modo de suspensão híbrida:

```
$ systemctl hybrid-sleep

```

## Escrevendo arquivos unit

A sintaxe de [arquivos unit](http://www.freedesktop.org/software/systemd/man/systemd.unit.html) do *systemd* é inspirada nos arquivos *.desktop* da XDG Desktop Entry Specification, que por sua vez são inspirados nos arquivos *.ini* do Microsoft Windows. Os arquivos unit são carregados de vários localizações (para ver a lista completa, execute `systemctl show --property=UnitPath`), mas os principais são (listados da menor para a mais alta precedência):

*   `/usr/lib/systemd/system/`: units fornecidas por pacotes instalados
*   `/etc/systemd/system/`: units instaladas pelo administrador do sistema

**Nota:**

*   Os caminhos de carregamento são completamente diferentes quando se está executando *systemd* em [modo usuário](/index.php/Systemd/User#How_it_works "Systemd/User").
*   Nomes de unit do systemd só podem conter caracteres alfanuméricos, sublinhados e pontos. Todos outros caracteres devem ser substituídos por escapes no estilo C "\x2d" ou deve-se empregar suas semânticas predefinidas ('@', '-'). Veja [systemd.unit(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.unit.5) e [systemd-escape(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-escape.1) para mais informações.

Veja as units instaladas por seus pacotes para exemplos, bem como a [seção de exemplos comentados](http://www.freedesktop.org/software/systemd/man/systemd.service.html#Examples) de [systemd.service(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.service.5).

**Dica:** Comentários prefixados com `#` também podem ser usados em arquivos units, mas apenas em novas linhas. Não use comentários em fim de linha após parâmetros do *systemd* ou a unidade não conseguirá ativar.

### Manuseando dependências

Com o *systemd*, dependências podem ser resolvidas através da concepção de arquivos unit corretamente. O caso mais típico é a unit *A* requerer a unit *B* para ser executada antes da *A* ser iniciada. Nesse caso, adicione `Requires=*B*` e `After=*B*` para a seção `[Unit]` de *A*. Se a dependência for opcional, então adicione `Wants=*B*` e `After=*B*`. Nota que `Wants=` e `Requires=` não implicam `After=`, significando que se `After=` não for especificado, as duas units serão iniciada em paralelo.

Dependências são normalmente colocadas em serviços e não em [#Targets](#Targets). Por exemplo, o `network.target` é puxado por qualquer serviço que configure as interfaces de rede, portanto, ordenando a sua unit personalizada depois disso é o bastante desde que `network.target` é iniciado de qualquer maneira.

### Tipos de serviços

Há vários tipos de execução diferentes a considerar quando se escreve um arquivo de serviço personalizado. Isso é definido com o parâmetro `Type=` na seção `[Service]`:

*   `Type=simple` (padrão): *systemd* considera que o serviço seja iniciado imediatamente. O processo não deve fazer *fork*. Não use este tipo se outros serviços precisarem ser ordenados neste serviço, a menos que seja socket ativado.
*   `Type=forking`: *systemd* considera que o serviço iniciou uma vez que o processo fez *fork* e o pai encerrou. Para daemons clássicos, use este tipo a menos que você saiba que ele não é necessário. Você deve especificar `PIDFile=` também, de forma que o *systemd* possa acompanhar o processo principal.
*   `Type=oneshot`: este é útil para os scripts que fazem um trabalho único e, em seguida, saem. Você pode querer definir `RemainAfterExit=yes` também para que *systemd* ainda considere o serviço como ativo depois que o processo foi encerrado.
*   `Type=notify`: idêntico ao `Type=simple`, mas com a condição de que o servidor enviará um sinal para *systemd* quando estiver pronto. A implementação de referência para essa notificação é fornecida por *libsystemd-daemon.so*.
*   `Type=dbus`: o serviço é considerado pronto quando o `BusName` especificado aparece no barramento do sistema do DBus.
*   `Type=idle`: *systemd*vai atrasar a execução do binário do serviço até todos os trabalhos serem despachados. Além desse comportamento, é muito similar a `Type=simple`.

Veja a página man [systemd.service(5)](http://www.freedesktop.org/software/systemd/man/systemd.service.html#Type=) para uma explicação mais detalhada dos valores de `Type`.

### Editando units fornecidas

Para evitar conflitos com o pacman, arquivos unit fornecidos por pacotes não devem ser editados diretamente. Há duas formas seguras de modificar um unit sem tocar no arquivo original: crie um novo arquivo unit que [se sobreponha ao unit original](#Arquivos_unit_de_substitui.C3.A7.C3.A3o) ou crie [trechos drop-in](#Arquivos_drop-in) que são aplicados sobre o unit original. Para ambos métodos, você deve recarregar o unit em seguida para aplicar suas alterações. Isso pode ser feito editando o unit com `systemctl edit` (que recarrega o unit automaticamente) ou recarregando todos os units com:

```
# systemctl daemon-reload

```

**Dica:**

*   Você pode usar *systemd-delta* para ver quais arquivos units foram sobrepostos ou estendidos e o que exatamente foi alterado.
*   Use `systemctl cat *unit*` para ver o conteúdo de um arquivo unit e todos os trechos *drop-in* associados.
*   O realce de sintaxe padrão para arquivos unit do *systemd* no [Vim](/index.php/Vim "Vim") é o mesmo para [arquivos INI](https://en.wikipedia.org/wiki/pt:Arquivo_INI "wikipedia:pt:Arquivo INI"). Porém, se você quiser algo mais específico do systemd, instale [vim-systemd](https://www.archlinux.org/packages/?name=vim-systemd).

#### Arquivos unit de substituição

Para substituir o arquivo unit `/usr/lib/systemd/system/*unit*`, crie o arquivo `/etc/systemd/system/*unit*` e reabilite o unit para atualizar os links simbólicos:

```
# systemctl reenable *unit*

```

Alternativamente, execute:

```
# systemctl edit --full *unit*

```

Isso abre `/etc/systemd/system/*unit*` em seu editor (copiando a versão instalada se ela não existir ainda) e automaticamente a recarrega quando você finaliza a edição.

**Nota:** As units de substituição continuarão sendo usadas mesmo que o Pacman atualize as units originais no futuro. Esse método dificulta a manutenção do sistema e, portanto, a próxima abordagem é a preferível.

#### Arquivos drop-in

Para criar arquivos *drop-in* para o arquivo de unidade `/usr/lib/systemd/system/*unit*`, crie o diretório `/etc/systemd/system/*unit*.d/` e coloque arquivos *.conf* para substituir ou adicionar novas opções. *systemd* analisará e aplicará esses arquivos sobre a unit original.

A forma mais fácil de fazer isso é executar:

```
# systemctl edit *unit*

```

Isso abre o arquivo `/etc/systemd/system/*unit*.d/override.conf` em seu editor de texto (criando-o, se necessário) e recarrega automaticamente a unit quando você finalizar a edição.

**Nota:** Nem todas as chaves podem ser substituídas por arquivos drop-in. Por exemplo, para alterar `Conflicts=` um arquivo de substituição [é necessário](https://lists.freedesktop.org/archives/systemd-devel/2017-June/038976.html).

#### Reverter para versão do vendor

Para reverter quaisquer alterações a uma unit feita usando `systemctl edit` faça:

```
# systemctl revert *unit*

```

#### Exemplos

Por exemplo, se você só quiser adicionar uma dependência adicional a uma unit, basta criar o seguinte arquivo:

 `/etc/systemd/system/*unit*.d/dependenciapesonalizada.conf` 
```
[Unit]
Requires=*nova dependência*
After=*nova dependência*
```

Como outro exemplo, para substituir a diretiva `ExecStart` para uma unit que não é do tipo `oneshot`, crie o seguinte arquivo:

 `/etc/systemd/system/*unit*.d/execpersonalizado` 
```
[Service]
ExecStart=
ExecStart=*novo comando*
```

Note como `ExecStart` deve ser limpado antes de reatribuir [[1]](https://bugzilla.redhat.com/show_bug.cgi?id=756787#c9). O mesmo ocorre para todo item que pode ser especificado várias vezes, como `OnCalendar` para *timers*.

Mais um exemplo para reiniciar automaticamente um serviço:

 `/etc/systemd/system/*unit*.d/reiniciar.conf` 
```
[Service]
Restart=always
RestartSec=30
```

## Targets

O *systemd* usa *targets* que servem a um propósito semelhante, como [níveis de execução](https://en.wikipedia.org/wiki/pt:N%C3%ADvel_de_execu%C3%A7%C3%A3o "wikipedia:pt:Nível de execução"), mas agem um pouco diferente. Cada *target* é nomeado em vez de numerado e destina-se a servir uma finalidade específica com a possibilidade de ter múltiplos ativos ao mesmo tempo. Alguns *target*s são implementados herdando todos os serviços de outro *target* e adicionando serviços adicionais a ele. Há *target*s do *systemd* que imitam os níveis de execução SystemVinit comuns para que possa mudar *target*s usando o comando familiar `telinit RUNLEVEL`.

### Obter targets atuais

O comando deve ser no *systemd* em vez de executar `runlevel`:

```
$ systemctl list-units --type=target

```

### Criar target personalizado

Os níveis de execução que tinham um significado definido no sysvinit (ex.: 0, 1, 3, 5 e 6) têm um mapeamento 1:1 com um *target* de *systemd* específico. Infelizmente, não há nenhuma boa forma de fazer o mesmo com os níveis de execução definidos pelo usuário, como 2 e 4\. Se você fizer uso deles é sugerido que você faça um *target* de *systemd* com um novo nome como `/etc/systemd/system/*seu target*` que leva um dos níveis de execução existentes como base (você pode examinar `/usr/lib/systemd/system/graphical.target` como um exemplo), crie um diretório `/etc/systemd/system/*seu target*.wants`, e então faça um link simbólico dos serviços adicionais de `/usr/lib/systemd/system/` que você deseja ativar.

### Mapeamento entre níveis do SysV e targets do systemd

| Nível de execução do SysV | Target do systemd | Notas |
| 0 | runlevel0.target, poweroff.target | Interrrompe o sistema. |
| 1, s, único | runlevel1.target, rescue.target | Modo de usuário único. |
| 2, 4 | runlevel2.target, runlevel4.target, multi-user.target | Níveis de execução User-defined/Site-specific. Por padrão, idêntico ao 3. |
| 3 | runlevel3.target, multi-user.target | Multi-usuário, não-gráfico. Os usuários geralmente podem acessar através de múltiplos consoles ou via rede. |
| 5 | runlevel5.target, graphical.target | Multi-usuário, gráfico. Normalmente tem todos os serviços do nível de execução 3, mais um login gráfico. |
| 6 | runlevel6.target, reboot.target | Reiniciar |
| emergência | emergency.target | Shell de emergência |

### Alterar target atual

No *systemd*, targets são expostos via *units de targets*. Você pode alterá-los assim:

```
# systemctl isolate graphical.target

```

Isso só vai mudar o target atual, e não tem nenhum efeito na próxima inicialização. É equivalente aos comandos como `telinit 3` ou `telinit 5` no Sysvinit.

### Alterar target padrão para inicializar

O target padrão é `default.target`, que é um link simbólico para `graphical.target`. Basicamente, ele corresponde ao antigo nível de execução 5.

Para verificar o target atual com *systemctl*:

```
# systemctl get-default

```

Para alterar o target padrão a ser inicializado, altere o link simbólico `default.target`. Com *systemctl*:

 `$ systemctl set-default multi-user.target` 
```
Removed /etc/systemd/system/default.target.
Created symlink /etc/systemd/system/default.target -> /usr/lib/systemd/system/graphical.target.
```

Alternativamente, acrescente um dos seguintes [parâmetros de kernel](/index.php/Kernel_parameters "Kernel parameters") a seu gerenciador de boot:

*   `systemd.unit=multi-user.target` (que basicamente corresponde ao antigo nível de execução 3),
*   `systemd.unit=rescue.target` (que basicamente corresponde ao antigo nível de execução 1).

### Ordem de target padrão

O systemd escolher o `default.target` conforme a ordem a seguir:

1.  Parâmetro de kernel mostrado acima
2.  Link simbólico de `/etc/systemd/system/default.target`
3.  Link simbólico de `/usr/lib/systemd/system/default.target`

## Arquivos temporários

"O *systemd-tmpfiles* cria, exclui e limpa arquivos e diretórios voláteis e temporários". Ele lê arquivos de configuração em `/etc/tmpfiles.d/` e `/usr/lib/tmpfiles.d/` para descobrir que ações devem ser realizadas. Os arquivos de configuração no primeiro diretório têm precedência sobre o segundo.

Os arquivos de configuração são geralmente fornecidos junto com arquivos de serviço e são nomeados no estilo de `/usr/lib/tmpfiles.d/*programa*.conf`. Por exemplo, o daemon do [Samba](/index.php/Samba "Samba") espera que o diretório `/run/samba` exista e tenha as permissões corretas. Portanto, o pacote [samba](https://www.archlinux.org/packages/?name=samba) vem com essa configuração:

 `/usr/lib/tmpfiles.d/samba.conf`  `D /run/samba 0755 root root` 

Os arquivos de configuração também podem ser usados para escrever valores em determinados arquivos na inicialização. Por exemplo, se você usa `/etc/rc.local` para desativar ativação de dispositivos USB com `echo USBE > /proc/acpi/wakeup`, você pode usar o seguinte *tmpfile*:

 `/etc/tmpfiles.d/disable-usb-wake.conf`  `w /proc/acpi/wakeup - - - - USBE` 

Veja as páginas man [systemd-tmpfiles(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-tmpfiles.8) e [tmpfiles.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tmpfiles.d.5) para detalhes.

**Nota:** Este método pode não funcionar para definir as opções em `/sys` uma vez que o serviço *systemd-tmpfiles-setup* pode ser executado antes dos módulos de dispositivo apropriados serem carregados. Neste caso, você pode verificar se o módulo tem um parâmetro para a opção que pretende definir com `modinfo *módulo*` e definir essa opção com um [arquivo de configuração em /etc/modprobe.d](/index.php/Kernel_modules#Setting_module_options "Kernel modules"). Caso contrário, você terá que escrever uma [regra de udev](/index.php/Udev#About_udev_rules "Udev") para defeinir o atributo adequado logo que o dispositivo aparecer.

## Timers

Um *timer* (em português, temporizador) é um arquivo de configuração de unit cujo nome termina com *.timer* e codifica informações sobre um temporizador controlado e supervisionado por *systemd*, para ativação baseada em temporizador. Veja [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers").

**Nota:** *Timers* podem substitui a funcionalidade do [cron](/index.php/Cron "Cron") muito bem. Veja [systemd/Timers#As a cron replacement](/index.php/Systemd/Timers#As_a_cron_replacement "Systemd/Timers").

## Montagem

O *systemd* é responsável pela montagem das partições e sistemas de arquivos especificados em `/etc/fstab`. O [systemd-fstab-generator(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-fstab-generator.8) converte todas as entradas do `/etc/fstab` em units de systemd, isso é executado no momento da inicialização e sempre que a configuração do gerenciador do sistema é recarregada.

O *systemd* estende os recursos habituais do [fstab](/index.php/Fstab "Fstab") e oferece opções adicionais de montagem. Eles afetam as dependências da unit de montagem, elas podem, por exemplo, garantir que uma montagem seja executada somente quando a rede estiver ativa ou apenas quando outra partição for montada. A lista completa de opções específicas de montagem *systemd*, tipicamente prefixadas com `x-systemd.`, é detalhada em [systemd.mount(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.mount.5#FSTAB).

Um exemplo dessas opções de montagem no contexto de *automontagem*, que significa montar somente quando o recurso é necessário, e não automaticamente no momento da inicialização, é fornecido em [fstab#Automount with systemd](/index.php/Fstab#Automount_with_systemd "Fstab").

## Journal

*systemd* tem o seu próprio sistema de registro chamado de o journal e, portanto, a execução de uma daemon `syslog` não é mais necessário. Para ler o registro, utilize:

```
# journalctl

```

No Arch Linux, o diretório `/var/log/journal/` faz parte do pacote *systemd* e o journal (quando `Storage=` está definido para `auto` em `/etc/systemd/journald.conf`) vai escrever para `/var/log/journal/`. Se você ou algum programa excluir esse diretório, systemd **não** vai recriá-lo automaticamente e, em vez disso,vai escrever seus logs em `/run/systemd/journal` em uma forma não persistente. Porém, a pasta será recriada quando você definir `Storage=persistent` e [reiniciar](/index.php/Reiniciar "Reiniciar") `systemd-journald.service` (ou reinicializar o sistema).

O journal do systemd classifica mensagens por [nível de prioridade](#N.C3.ADvel_de_prioridade) e [facilidade](#Facilidade). A classificação de registro de logs corresponde ao clássico protocolo do [Syslog](https://en.wikipedia.org/wiki/pt:Syslog "wikipedia:pt:Syslog") ([RFC 5424](https://tools.ietf.org/html/rfc5424)).

### Nível de prioridade

Um código de severidade do syslog (em systemd chamado de prioridade) é usado para marcar a importância de uma mensagem [RFC 5424 Seção 6.2.1](https://tools.ietf.org/html/rfc5424#section-6.2.1).

| Valor | Severidade | Palavra-chave | Descrição | Exemplos |
| 0 | Emergência | emerg | Sistema não está usável | BUG de kernel severo, núcleo do systemd despejado.
Esse nível não deve ser usado por aplicativos. |
| 1 | Alerta | alert | Deve ser corrigido imediatamente | Subsistema vital parou de funcionar. Perda de dados.
`kernel: BUG: unable to handle kernel paging request at ffffc90403238ffc`. |
| 2 | Crítico | crit | Condições críticas | Travamentos, despejos de núcleo. Como flash familiar:
`systemd-coredump[25319]: Process 25310 (plugin-containe) of user 1000 dumped core`
Falha no aplicativo de sistema principal, como o X11. |
| 3 | Erro | err | Condições de erro | Erro não severo relatado:
`kernel: usb 1-3: 3:1: cannot get freq at ep 0x84`,
`systemd[1]: Failed unmounting /var.`,
`libvirtd[1720]: internal error: Failed to initialize a valid firewall backend`. |
| 4 | Aviso | warning | Pode indicar que um erro vai ocorrer se uma ação não for tomada. | Um sistema de arquivos não raiz tem apenas 1GB livre.
`org.freedesktop. Notifications[1860]: (process:5999): Gtk-WARNING **: Locale not supported by C library. Using the fallback 'C' locale`. |
| 5 | Nota | notice | Eventos que são incomuns, mas não condições de erro. | `systemd[1]: var.mount: Directory /var to mount over is not empty, mounting anyway`. `gcr-prompter[4997]: Gtk: GtkDialog mapped without a transient parent. This is discouraged`. |
| 6 | Informacional | info | Mensagens de operação normais que exigem nenhuma ação. | `lvm[585]: 7 logical volume(s) in volume group "archvg" now active`. |
| 7 | Depuração | debug | Informações úteis para desenvolvedores para depurar o aplicativo. | `kdeinit5[1900]: powerdevil: Scheduling inhibition from ":1.14" "firefox" with cookie 13 and reason "screen"`. |

Se você não encontrar uma mensagem no nível de prioridade esperado, pesquise também alguns níveis acima e abaixo: essas regras são recomendações, e o desenvolvedor do aplicativo afetado pode ter uma percepção diferente da importância do problema.

### Facilidade

Um código de facilidade syslog é usado para especificar o tipo de programa que está registrando a mensagem [RFC 5424 Seção 6.2.1](https://tools.ietf.org/html/rfc5424#section-6.2.1).

| Código de facilidade | Palavra-chave | Descrição | Informação |
| 0 | kern | mensagens de kernel |
| 1 | user | mensagens de nível de usuário |
| 2 | mail | sistema de correio | O POSIX arcaico ainda tem suporte e é por vezes usado (para mais [mail(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mail.1)) |
| 3 | daemon | daemons de sistemas | Todos os daemons, incluindo systemd e seus subsistemas |
| 4 | auth | mensagens de segurança/autorização | Também monitora a facilidade 10 |
| 5 | syslog | mensagens geradas internamente pelo syslogd | Padronizado para syslog, não sendo usado pelo systemd (veja facilidade 3) |
| 6 | lpr | subsistema de impressora de linha (subsistema arcaico) |
| 7 | news | subsistema de notícias de rede (subsistema arcaico) |
| 8 | uucp | subsistema UUCP (subsistema arcaico) |
| 9 | daemon de relógio | systemd-timesyncd |
| 10 | authpriv | mensagens de segurança/autorização | Também monitora a facilidade 4 |
| 11 | ftp | daemon FTP |
| 12 | - | subsistema NTP |
| 13 | - | auditoria de log |
| 14 | - | alerta de log |
| 15 | cron | daemon de agendamento |
| 16 | local0 | uso local 0 (local0) |
| 17 | local1 | uso local 1 (local1) |
| 18 | local2 | uso local 2 (local2) |
| 19 | local3 | uso local 3 (local3) |
| 20 | local4 | uso local 4 (local4) |
| 21 | local5 | uso local 5 (local5) |
| 22 | local6 | uso local 6 (local6) |
| 23 | local7 | uso local 7 (local7) |

Então, facilidades que é útil monitorar: 0,1,3,4,9,10,15.

### Filtrando saída

*journalctl* permite filtrar a saída por campos específicos. Esteja ciente de que, se houver muitas mensagens para exibir ou filtrar um grande intervalo de tempo, a saída desse comando poderá ser atrasada por algum tempo.

**Dica:** Sendo o journal armazenado em um formato binário, o conteúdo das mensagens armazenadas não é modificado. Isso significa que ele é visível com *strings*, por exemplo, para recuperação em um ambiente que não tenha *systemd* instalado. Exemplo de comando: `$ strings /mnt/arch/var/log/journal/af4967d77fba44c6b093d0e9862f6ddd/system.journal | grep -i *mensagem*` 

Exemplos:

*   Mostrar todas mensagens desta inicialização: `# journalctl -b` No entanto, muitas vezes, alguém está interessado em mensagens que não são da atual, mas da inicialização anterior (por exemplo, se uma falha irrecuperável de sistema ocorrer). Isso é possível através do parâmetro de deslocamento opcional da opção `-b`: `journalctl -b -0` mostra mensagens da inicialização atual, `journalctl -b -1` da inicialização anterior, `journalctl -b -2` da segunda anterior e por aí vai – você pode ver a lista de inicializações com seus números usando `journalctl --list-boots`. Veja [journalctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journalctl.1) para descrição completa, a semântica é muito mais poderosa.
*   Mostrar todas as mensagens da data (e hora opcional): `# journalctl --since="2012-10-30 18:17:16"` 
*   Mostrar todas as mensagens desde 20 minutos atrás: `# journalctl --since "20 min ago"` 
*   Seguir novas mensagens: `# journalctl -f` 
*   Mostrar novas mensagens por um executável específico: `# journalctl /usr/lib/systemd/systemd` 
*   Mostrar todas as mensagens por um processo específico: `# journalctl _PID=1` 
*   Mostrar todas as mensagens por uma unit específica: `# journalctl -u man-db.service` 
*   Mostrar o *ring buffer* do kernel: `# journalctl -k` 
*   Mostrar apenas mensagens de prioridade de erro, crítico e alerta `# journalctl -p err..alert` Números também podem ser usados, `journalctl -p 3..1`. Se somente um número/uma palavra-chave usado(a), `journalctl -p 3` - todos os níveis de prioridade maiores também são incluídos.
*   Mostrar equivalente a auth.log filtrando na facilidade do syslog: `# journalctl SYSLOG_FACILITY=10` 
*   Se o diretório do journal (por padrão, localizado sob `/var/log/journal`) contém quantidade imensa de dados de log, então `journalctl` pode levar vários minutos filtrando a saída. Você pode acelerar significativamente usando a opção `--file` para forçar o `journalctl` a procurar apenas no journal mais recente: `# journalctl --file /var/log/journal/*/system.journal -f` 

Veja [journalctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journalctl.1), [systemd.journal-fields(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.journal-fields.7) ou a [publicação de blogue](http://0pointer.de/blog/projects/journalctl.html) do Lennart para detalhes.

**Dica:** Por padrão, *journalctl* trunca linhas maiores que a largura da tela, mas em alguns casos pode ser melhor habilitar *wrapping* em vez de trucamento'. Isso pode ser controlado pela [variável de ambiente](/index.php/Environment_variable "Environment variable") `SYSTEMD_LESS`, que contém opções passadas ao [less](/index.php/Utilit%C3%A1rios_principais#less "Utilitários principais") (o paginador padrão) e usa como padrão `FRSXMK` (veja [less(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/less.1) e [journalctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journalctl.1) para detalhes).

Ao omitir a opção `S`, a saída estará sob *wrap* em vez de truncamento. Por exemplo, inicie *journalctl* da seguinte forma:

```
$ SYSTEMD_LESS=FRXMK journalctl

```
Se você quiser definir esse comportamento como padrão, [exporte](/index.php/Environment_variables#Per_user "Environment variables") a variável a partir de `~/.bashrc` ou `~/.zshrc`.

### Limite no tamanho do journal

Se o journal é persistente (não volátil), seu tamanho limite é definido para um valor padrão de 10% do tamanho do respectivo sistema de arquivos, mas limitado a 4 GB. Por exemplo, com o `/var/log/journal` localizado em uma partição de 20 GB, o journal pode usar até 2 GB. Em uma partição de 50 GB, ela usaria no máximo até 4 GB.

O tamanho máximo do journal persistente pode ser controlado removendo o comentário e alterando o seguinte:

 `/etc/systemd/journald.conf`  `SystemMaxUse=50M` 

Também é possível usar o mecanismo de substituição de configuração de snippets de *drop-in*, em vez de editar o arquivo de configuração global. Neste caso, não esqueça de colocar as sobrescrições no cabeçalho `[Journal]`:

 `/etc/systemd/journald.conf.d/00-journal-size.conf` 
```
[Journal]
SystemMaxUse=50M
```

[Reinicie](/index.php/Reinicie "Reinicie") o `systemd-journald.service` após alterar essa configuração para aplicar imediatamente o novo limite.

Veja [journald.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journald.conf.5) para mais informações.

### Limpar arquivos de journal manualmente

Os arquivos de journal podem ser removidos globalmente de `/var/log/journal/` usando, por exemplo, `rm` ou podem ser aparados de acordo com vários critérios usando `journalctl` . Exemplos:

*   Remova arquivos de journal armazenados até que o espaço em disco que eles usam fique abaixo de 100 MB: `# journalctl --vacuum-size=100M` 
*   Faça com que todos os arquivos de diário não contenham dados com mais de 2 semanas. `# journalctl --vacuum-time=2weeks` 

Veja [journalctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journalctl.1) para mais informações.

### Journald em conjunto com o syslog

Compatibilidade com uma implementação clássica, sem journald, do [syslog](/index.php/Syslog-ng "Syslog-ng") pode ser fornecida deixando o *systemd* encaminhar todas as mensagens pelo soquete `/run/systemd/journal/syslog`. Para fazer funcionar o daemon do syslog com o journal, ele tem que associar a este soquete em vez de `/dev/log` ([anúncio oficial](http://lwn.net/Articles/474968/)).

O `journald.conf` padrão para encaminhar para o soquete é `ForwardToSyslog=no` para evitar sobrecarga de sistema, porque [rsyslog](/index.php/Rsyslog "Rsyslog") ou [syslog-ng](/index.php/Syslog-ng "Syslog-ng") obtêm as mensagens do journal [eles mesmo](http://lists.freedesktop.org/archives/systemd-devel/2014-August/022295.html#journald).

Veja [Syslog-ng#Overview](/index.php/Syslog-ng#Overview "Syslog-ng") e [Syslog-ng#syslog-ng and systemd journal](/index.php/Syslog-ng#syslog-ng_and_systemd_journal "Syslog-ng") e [rsyslog](/index.php/Rsyslog "Rsyslog"), para detalhes sobre a configuração.

### Encaminhar journald para /dev/tty12

Crie um [diretório de *drop-in*](#Editando_units_fornecidas) `/etc/systemd/journald.conf.d` e crie um arquivo `fw-tty12.conf` nele:

 `/etc/systemd/journald.conf.d/fw-tty12.conf` 
```
[Journal]
ForwardToConsole=yes
TTYPath=/dev/tty12
MaxLevelConsole=info
```

Então, [reinicie](/index.php/Reinicie "Reinicie") `systemd-journald.service`.

### Especificar um journal diferente para ver

Pode ser necessário verificar os logs de outro sistema que esteja inativo na água, como a inicialização de um sistema ativo para recuperar um sistema de produção. Nesse caso, pode-se montar o disco em, p. ex., `/mnt` e especificar o caminho do journal via `-D`/`--directory`, assim:

```
$ journalctl -D */mnt*/var/log/journal -xe

```

## Dicas e truques

### Executando serviços após a rede estar ativa

Para atrasar um serviço depois que a rede está ativa, inclua as seguintes dependências no arquivo *.service*:

 `/etc/systemd/system/*foo*.service` 
```
[Unit]
...
**Wants=network-online.target**
**After=network-online.target**
...
```

O serviço de espera de rede do aplicativo específico que gerencia a rede também deve ser ativado para que `network-online.target` reflita adequadamente o status da rede.

*   Para os que estão usando [NetworkManager](/index.php/NetworkManager_(Portugu%C3%AAs) "NetworkManager (Português)"), [habilite](/index.php/Habilite "Habilite") `NetworkManager-wait-online.service`.
*   Se estiver usando [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd"), `systemd-networkd-wait-online.service` é, por padrão, habilitado automaticamente sempre que `systemd-networkd.service` foi habilitado; caso obtenha sucesso na verificação como `systemctl is-enabled systemd-networkd-wait-online.service`, nenhuma outra ação é necessária.

Para explicações mais detalhadas, veja [Running services after the network is up](https://www.freedesktop.org/wiki/Software/systemd/NetworkTarget/) no wiki do systemd.

### Habilitar units instaladas por padrão

O Arch Linux vem com `/usr/lib/systemd/system-preset/99-default.preset` contendo `disable *`. Isso faz com que o *systemctl preset* desabilite todas as unidades por padrão, de forma que quando um novo pacote é instalado, o usuário deve habilitar manualmente a unit.

Se este comportamento não for desejado, basta criar um link simbólico de `/etc/systemd/system-preset/99-default.preset` para `/dev/null` para sobrescrever o arquivo de configuração. Isso fará com que o *systemctl preset* habilite todas as units que forem instaladas – independentemente do tipo de unit – a menos que especificado em outro arquivo em um dos diretórios de configuração do *systemctl preset*. Units de usuário não são afetadas. Veja [systemd.preset(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.preset.5) para mais informações.

**Nota:** Habilitar todas as units por padrão pode causar problemas com pacotes que contêm duas ou mais unidades mutuamente exclusivas. O *systemctl preset* é projetado para ser usado por distribuições ou administradores de sistema. No caso em que duas units conflitantes seriam habilitadas, você deve especificar explicitamente qual delas deve ser desabilitada em um arquivo de configuração predefinido, conforme especificado na página man de `systemd.preset`.

### Usando ambientes de aplicativos em *sandbox*

Um arquivo de unit pode ser criado como uma *sandbox* para isolar aplicativos e seus processos em um ambiente virtual reforçado. O systemd alavanca [espaços de nomes](https://en.wikipedia.org/wiki/Linux_namespaces "wikipedia:Linux namespaces"), listas brancas/negras de [Capacidades](/index.php/Capabilities "Capabilities") e [grupos de controle](/index.php/Control_groups "Control groups") ("cgroups") para processos contêineres através de uma extensa [configuração do ambiente de execução](https://www.freedesktop.org/software/systemd/man/systemd.exec.html).

O aprimoramento de um arquivo existente de unit do systemd com um aplicativo de *sandboxing* normalmente requer testes de tentativa e erro acompanhados pelo uso generoso de [strace](https://www.archlinux.org/packages/?name=strace), [stderr](https://en.wikipedia.org/wiki/pt:Fluxos_padr%C3%A3o#Erro_padr.C3.A3o_.28stderr.29 "wikipedia:pt:Fluxos padrão") e facilidades de saída e registro de erro do [journalctl](https://www.freedesktop.org/software/systemd/man/journalctl.html). Você pode querer pesquisar primeiro a documentação original para testes já feitos para basear os testes.

Alguns exemplos sobre como fazer *sandboxing* como systemd pode ser implementado:

*   `CapabilityBoundingSet` define uma lista branca definida de capacidades permitidas, mas também pode ser usado para inserir em lista negra uma capacidade específica para uma unit.
    *   A capacidade `CAP_SYS_ADM`, por exemplo, que deve ser um dos [objetivos de um sandbox seguro](https://lwn.net/Articles/486306/): `CapabilityBoundingSet=~ CAP_SYS_ADM`

## Solução de problemas

### Investigar erros no systemd

Como um exemplo, vamos investigar um erro como o serviço `systemd-modules-load`:

**1.** Vamos procurar os serviços *systemd* que falham em iniciar em tempo de inicialização:

 `$ systemctl --state=failed`  `systemd-modules-load.service   loaded **failed failed**  Load Kernel Modules` 

Outra forma é mensagens de log ao vivo do *systemd*:

```
$ journalctl -fp err

```

**2.** Beleza, localizamos um problema com o serviço `systemd-modules-load`. Queremos saber mais:

 `$ systemctl status systemd-modules-load` 
```
systemd-modules-load.service - Load Kernel Modules
   Loaded: loaded (/usr/lib/systemd/system/systemd-modules-load.service; static)
   Active: **failed** (Result: exit-code) since So 2013-08-25 11:48:13 CEST; 32s ago
     Docs: man:systemd-modules-load.service(8).
           man:modules-load.d(5)
  Process: **15630** ExecStart=/usr/lib/systemd/systemd-modules-load (**code=exited, status=1/FAILURE**)
```

Se o `Process ID` não estiver listado, basta reiniciar o serviço que falhou usando `systemctl restart systemd-modules-load`.

**3.** Agora temos o id de processo (PID) para investigar esse erro em profundidade. Digite o comando a seguir com o `Process ID` atual (aqui: 15630):

 `$ journalctl _PID=15630` 
```
-- Logs begin at Sa 2013-05-25 10:31:12 CEST, end at So 2013-08-25 11:51:17 CEST. --
Aug 25 11:48:13 mypc systemd-modules-load[15630]: **Failed to find module 'blacklist usblp'**
Aug 25 11:48:13 mypc systemd-modules-load[15630]: **Failed to find module 'install usblp /bin/false'**
```

**4.** Vemos que algumas configurações de módulo do kernel estão com configurações erradas. Portanto, vamos dar uma olhada nessas configurações em `/etc/modules-load.d/`:

 `$ ls -Al /etc/modules-load.d/` 
```
...
-rw-r--r--   1 root root    79  1\. Dez 2012  blacklist.conf
-rw-r--r--   1 root root     1  2\. Mär 14:30 encrypt.conf
-rw-r--r--   1 root root     3  5\. Dez 2012  printing.conf
-rw-r--r--   1 root root     6 14\. Jul 11:01 realtek.conf
-rw-r--r--   1 root root    65  2\. Jun 23:01 virtualbox.conf
...

```

**5.** A mensagem de erro `Failed to find module 'blacklist usblp'` pode estar relacionada a uma configuração errada dentro de `blacklist.conf`. Vamos desativá-lo inserindo um **#** antes de cada opção que encontramos na etapa 3:

 `/etc/modules-load.d/blacklist.conf` 
```
**#** blacklist usblp
**#** install usblp /bin/false

```

**6.** Agora, tentar iniciar `systemd-modules-load`:

```
$ systemctl start systemd-modules-load

```

Se for bem sucedido, nada deve ser emitido. Se você vir algum erro, volte para a etapa 3 e use o novo PID para resolver os erros deixados.

Se tudo estiver correto, você pode verificar se o serviço foi iniciado com sucesso com:

 `$ systemctl status systemd-modules-load` 
```
systemd-modules-load.service - Load Kernel Modules
   Loaded: **loaded** (/usr/lib/systemd/system/systemd-modules-load.service; static)
   Active: **active (exited)** since So 2013-08-25 12:22:31 CEST; 34s ago
     Docs: man:systemd-modules-load.service(8)
           man:modules-load.d(5)
 Process: 19005 ExecStart=/usr/lib/systemd/systemd-modules-load (code=exited, status=0/SUCCESS)
Aug 25 12:22:31 mypc systemd[1]: **Started Load Kernel Modules**.
```

### Diagnosticar problemas de inicialização

O *systemd* tem várias opções para diagnosticar problemas com o processo de inicialização. Veja [Depuração de inicialização](/index.php/Boot_debugging "Boot debugging") para instruções mais gerais e opções para capturar mensagens de inicialização antes que o *systemd* assuma o [processo de inicialização](/index.php/Processo_de_inicializa%C3%A7%C3%A3o "Processo de inicialização"). Veja também a [documentação de depuração do systemd](http://freedesktop.org/wiki/Software/systemd/Debugging/).

### Diagnosticar um serviço

Se algum serviço do *systemd* se comportar mal ou você quiser obter mais informações sobre o que está acontecendo, defina a [variável de ambiente](/index.php/Environment_variable "Environment variable") `SYSTEMD_LOG_LEVEL` com `debug`. Por exemplo, para executar o daemon *systemd-networkd* no modo de depuração:

Adicione um [arquivo *drop-in*](#Arquivos_drop-in) para o serviço adicionando as duas linhas:

```
[Service]
Environment=SYSTEMD_LOG_LEVEL=debug

```

Ou, de forma equivalente, defina a variável de ambiente manualmente:

```
# SYSTEMD_LOG_LEVEL=debug /lib/systemd/systemd-networkd

```

então, [reinicie](/index.php/Reinicie "Reinicie") *systemd-networkd* e monitore o journal para o serviço com a opção `--follow`.

### Desligamento/reinicialização demora demais

Se o processo de desligamento leva um tempo muito longo (ou parece estar congelado) muito provavelmente um serviço que não se encerra é o responsável. O *systemd* espera um tempo para cada serviço encerrar antes de tentar matá-lo. Para descobrir se você foi afetado, veja [esse artigo](http://freedesktop.org/wiki/Software/systemd/Debugging#Shutdown_Completes_Eventually).

### Processos de curta duração não parecem registrar qualquer saída

Se `journalctl -u foounit` não mostra nenhuma saída para um serviço de curta duração, veja o PID em vez disso. Por exemplo, se `systemd-modules-load.service` falha, e `systemctl status systemd-modules-load` mostra que executou com PID 123, então você talvez possa ver uma saída no journal por esse PID, ou seja, `journalctl -b _PID=123`. Campos de metadados para o journal como `_SYSTEMD_UNIT` e `_COMM` são coletados de forma assíncrona e invocam o diretório `/proc` para o processo existente. A solução deste problema requer fixar o kernel para fornecer esses dados através de uma conexão de socket, semelhante ao `SCM_CREDENTIALS`.

### Tempo de inicialização aumentando com o tempo

Depois de usar o `systemd-analyze`, vários usuários notaram que o tempo de inicialização aumentou significativamente em comparação com o que costumava ser. Depois de usar `systemd-analyse blame`, o [NetworkManager](/index.php/NetworkManager_(Portugu%C3%AAs) "NetworkManager (Português)") está sendo relatado como tendo uma quantidade anormalmente grande de tempo para iniciar.

O problema para alguns usuários foi devido a `/var/log/journal` se tornar muito grande. Isso pode ter outros impactos no desempenho, como `systemctl status` ou `journalctl`. Como tal, a solução é remover todos os arquivos dentro da pasta (idealmente fazendo um backup em algum lugar, pelo menos temporariamente) e, em seguida, definindo um limite de tamanho de arquivo de diário conforme descrito em [#Limite no tamanho do journal](#Limite_no_tamanho_do_journal).

### systemd-tmpfiles-setup.service não inicia na inicialização do sistema

A partir do systemd 219, `/usr/lib/tmpfiles.d/systemd.conf` especifica os atributos da ACL para os diretórios sob `/var/log/journal` e, portanto, requer que o suporte da ACL seja ativada para o sistema de arquivos em que o journal reside.

Veja [Access Control Lists#Enabling ACL](/index.php/Access_Control_Lists#Enabling_ACL "Access Control Lists") para instruções sobre como habilitar ACL no sistema de arquivos que hospeda `/var/log/journal`.

### A versão impressa do systemd na inicialização não é a mesma da versão do pacote instalado

Você precisa [regenerar seu initramfs](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio") e as versões deve corresponder.

**Dica:** Um hook do pacman pode ser usado para regenerar automaticamente o initramfs toda vez que o [systemd](https://www.archlinux.org/packages/?name=systemd) é atualizado. Veja [esse tópico no fórum](https://bbs.archlinux.org/viewtopic.php?id=215411) e [Pacman (Português)#Hooks](/index.php/Pacman_(Portugu%C3%AAs)#Hooks "Pacman (Português)").

### Desabilitar modo de emergência em máquina remota

Você pode desabilitar o modo de emergência em uma máquina remota, por exemplo, uma máquina virtual hospedada no Azure ou no Google Cloud. É porque se o modo de emergência for acionado, a máquina será bloqueada de se conectar à rede.

```
# systemctl mask emergency.service
# systemctl mask emergency.target

```

## Veja também

*   [Artigo do Wikipédia](https://en.wikipedia.org/wiki/pt:systemd "wikipedia:pt:systemd")
*   [Site oficial do systemd](http://www.freedesktop.org/wiki/Software/systemd)
*   [Otimizações do systemd](http://www.freedesktop.org/wiki/Software/systemd/Optimizations)
*   [FAQ do systemd](http://www.freedesktop.org/wiki/Software/systemd/FrequentlyAskedQuestions)
*   [Dicas e truques do systemd](http://www.freedesktop.org/wiki/Software/systemd/TipsAndTricks)
*   [Página sobre systemd do Gentoo Wiki](http://wiki.gentoo.org/wiki/Systemd)
*   [Projeto Fedora - Sobre o systemd](http://fedoraproject.org/wiki/Systemd)
*   [Projeto Fedora - Como depurar problemas no systemd](http://fedoraproject.org/wiki/How_to_debug_Systemd_problems)
*   [Projeto Fedora - Folha de dicas de SysVinit para systemd](http://fedoraproject.org/wiki/SysVinit_to_Systemd_Cheatsheet)
*   [Página sobre systemd do Debian Wiki](https://wiki.debian.org/systemd "debian:systemd")
*   [Páginas de manual](http://0pointer.de/public/systemd-man/)
*   [História do blogue do Lennart](http://0pointer.de/blog/projects/systemd.html), [atualização 1](http://0pointer.de/blog/projects/systemd-update.html), [atualização 2](http://0pointer.de/blog/projects/systemd-update-2.html), [atualização 3](http://0pointer.de/blog/projects/systemd-update-3.html), [resumo](http://0pointer.de/blog/projects/why.html)
*   [systemd para administradores (PDF)](http://0pointer.de/public/systemd-ebook-psankar.pdf)
*   [Como usar o systemctl para gerenciar serviços e units do systemd](https://www.digitalocean.com/community/tutorials/how-to-use-systemctl-to-manage-systemd-services-and-units)
*   [gerenciamento de sessão com systemd-logind](https://dvdhrm.wordpress.com/2013/08/24/session-management-on-linux/)
*   [Realce de sintaxe do Emacs para arquivos do systemd](/index.php/Emacs#Syntax_highlighting_for_systemd_Files "Emacs")
*   Artigo introdutório em [duas](http://www.h-online.com/open/features/Control-Centre-The-systemd-Linux-init-system-1565543.html) [partes](http://www.h-online.com/open/features/Booting-up-Tools-and-tips-for-systemd-1570630.html) na revista *The H Open*.