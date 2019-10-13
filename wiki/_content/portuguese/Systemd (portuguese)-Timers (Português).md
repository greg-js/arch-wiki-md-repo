**Status de tradução:** Esse artigo é uma tradução de [Systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers"). Data da última tradução: 2019-10-08\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Systemd/Timers&diff=0&oldid=582921) na versão em inglês.

Artigos relacionados

*   [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)")
*   [systemd/User](/index.php/Systemd/User "Systemd/User")
*   [systemd FAQ](/index.php/Systemd_FAQ "Systemd FAQ")
*   [cron](/index.php/Cron "Cron")

*Timers* são arquivos de unit do [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") cujo nome termina em `.timer` que controla arquivos `.service` ou seus eventos. Timers podem ser usados como uma alternativa ao [cron](/index.php/Cron "Cron") (leia [#Como um substituto do cron](#Como_um_substituto_do_cron)). Os timers têm suporte interno para eventos de tempo do calendário, eventos de tempo monotônicos e podem ser executados de forma assíncrona.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Units de timer](#Units_de_timer)
*   [2 Unit de serviço](#Unit_de_serviço)
*   [3 Gerenciamento](#Gerenciamento)
*   [4 Exemplos](#Exemplos)
    *   [4.1 Timer monotônico](#Timer_monotônico)
    *   [4.2 Timer de tempo real](#Timer_de_tempo_real)
*   [5 Units .timer transientes](#Units_.timer_transientes)
*   [6 Como um substituto do cron](#Como_um_substituto_do_cron)
    *   [6.1 Benefícios](#Benefícios)
    *   [6.2 Ressalvas](#Ressalvas)
    *   [6.3 MAILTO](#MAILTO)
    *   [6.4 Usando um crontab](#Usando_um_crontab)
*   [7 Veja também](#Veja_também)

## Units de timer

Timers são arquivos unit do *systemd* com um sufixo de `.timer`. Timers são como outros [arquivos de configuração units](/index.php/Systemd_(Portugu%C3%AAs)#Escrevendo_arquivos_unit "Systemd (Português)") e são carregados dos mesmos caminhos, mas incluem uma seção `[Timer]` que define quando e como o timer é ativado. Timers são definidos como um dos dois tipos:

*   **Timers de tempo real** (ou *wallclock timers*, relógios de parede) são ativados em um evento de calendário, da mesma forma que os *cronjobs*. A opção `OnCalendar=` é usada para defini-los.
*   **Timers monotônicos** são ativados após um período de tempo relativo a um ponto inicial variável. Eles param se o computador é temporariamente suspenso ou desligado. Há vários timers monotônicos diferentes, mas todos têm a forma: `On*Tipo*Sec=`. Timers monotônicos comuns incluem `OnBootSec` e `OnActiveSec`.

Para uma explicação completa das opções de timers, veja [systemd.timer(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.timer.5). A sintaxe de argumentos para eventos de calendário e períodos de tempo está definida em [systemd.time(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.time.7).

## Unit de serviço

Para cada arquivo `.timer`, um arquivo `.service` correspondente existe (p.ex., `foo.timer` e `foo.service`). O arquivo `.timer` ativa e controla o arquivo `.service`. O `.service` não exige uma seção `[Install]`, pois os units *timer* que são habilitados. Se necessário, é possível controlar uma unit com nome diferente usando a opção `Unit=` na seção `[Timer]` do timer.

## Gerenciamento

Para usar uma unit de *timer*, [habilite](/index.php/Habilite "Habilite") e [inicie](/index.php/Inicie "Inicie")-a como qualquer outra unit unit (lembre-se de adicionar o sufixo `.timer`). Para ver todos os timers iniciados, execute:

 `$ systemctl list-timers` 
```
NEXT                          LEFT        LAST                          PASSED     UNIT                         ACTIVATES
Thu 2014-07-10 19:37:03 CEST  11h left    Wed 2014-07-09 19:37:03 CEST  12h ago    systemd-tmpfiles-clean.timer systemd-tmpfiles-clean.service
Fri 2014-07-11 00:00:00 CEST  15h left    Thu 2014-07-10 00:00:13 CEST  8h ago     logrotate.timer              logrotate.service

```

**Nota:**

*   Para listar todos os timers (incluindo inativos), use `systemctl list-timers --all`.
*   O status de um serviço iniciado por um timer provavelmente ficará inativo, a menos que esteja sendo acionado no momento.
*   Se um timer ficar fora de sincronia, pode ajudar a excluir seu arquivo `stamp-*` em `/var/lib/systemd/timers` (ou `~/.local/share/systemd/` no caso de timers do usuário). Estes são arquivos de comprimento zero que marcam a última vez que cada timer foi executado. Se excluídos, eles serão reconstruídos no próximo início do temporizador.

## Exemplos

Um arquivo unit de serviço pode ser agendado com um temporizador pronto para uso. Os exemplos a seguir agendam o `foo.service` para ser executado com um timer correspondente chamado `foo.timer`.

### Timer monotônico

Um timer que será iniciado 15 minutos após a inicialização e novamente toda semana enquanto o sistema estiver em execução.

 `/etc/systemd/system/foo.timer` 
```
[Unit]
Description=Executa foo semanalmente e na inicialização

[Timer]
OnBootSec=15min
OnUnitActiveSec=1w 

[Install]
WantedBy=timers.target

```

### Timer de tempo real

Um timer que começa uma vez por semana (às 00:00 da segunda-feira). Quando ativado, aciona o serviço imediatamente se perdeu a última hora de início (opção `Persistent=true`), por exemplo, devido ao sistema estar desligado:

 `/etc/systemd/system/foo.timer` 
```
[Unit]
Description=Executa foo semanalmente

[Timer]
OnCalendar=weekly
Persistent=true

[Install]
WantedBy=timers.target
```

Quando datas e horas mais específicas são necessárias, os eventos de `OnCalendar` usam o seguinte formato:

```
`DiaDaSemana Ano-Mês-Dia Hora:Minuto:Segundo`

```

Um asterisco pode ser usado para especificar qualquer valor e vírgulas podem ser usadas para listar possíveis valores. Dois valores separados por `..` indicam um intervalo contíguo.

No exemplo abaixo, o serviço é executado nos primeiros quatro dias de cada mês às 12:00, mas *somente* se esse dia for uma segunda-feira ou uma terça-feira.

```
OnCalendar=Mon,Tue *-*-01..04 12:00:00

```

Para executar um serviço no primeiro sábado de cada mês, use:

```
 OnCalendar=Sat *-*-1..7 18:00:00

```

Ao usar a parte `DiaDaSemana`, pelo menos um dia da semana deve ser especificado. Se você quer que algo seja executado todos os dias às 4h da manhã, use:

```
 OnCalendar=*-*-* 4:00:00

```

Para executar um serviço em momentos diferentes, `OnCalendar` pode ser especificado mais de uma vez. No exemplo abaixo, o serviço funciona às 22:30 durante a semana e às 20:00 nos finais de semana.

```
 OnCalendar=Mon..Fri 22:30
 OnCalendar=Sat,Sun 20:00

```

Mais informações estão disponíveis em [systemd.time(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.time.7).

**Dica:**

*   Especificações de tempo no `OnCalendar` pode ser testado para verificar sua validade e calcular a próxima vez que a condição decorrerá quando usada em um arquivo unit de timer com a opção `calendar` do utilitário *systemd-analyse*. Por exemplo, pode-se usar o `systemd-analyze calendar weekly` ou o `systemd-analyze calendar "Mon,Tue *-*-01..04 12:00:00"`.
*   Expressões de eventos especiais como `daily` e `weekly` referem-se a *horários de início específicos* e, assim, todos os timers que compartilham esses eventos de calendário serão iniciados simultaneamente. Os timers que compartilham eventos iniciais podem causar um desempenho ruim do sistema se os serviços dos timers competirem pelos recursos do sistema. A opção `RandomizedDelaySec` na seção `[Timer]` evita esse problema, escalonando aleatoriamente a hora de início de cada timer. Veja [systemd.timer(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.timer.5).

## Units .timer transientes

Pode-se usar `systemd-run` para criar unidades `.timer` transitórias. Ou seja, é possível definir um comando para ser executado em um horário especificado sem ter um arquivo de serviço. Por exemplo, o seguinte comando toca um arquivo após 30 segundos:

```
# systemd-run --on-active=30 /bin/touch /tmp/foo

```

Também é possível especificar um arquivo de serviço pré-existente que não tenha um arquivo de cronômetro. Por exemplo, o seguinte inicia a unit systemd denominada `*algumaunit*.service` após 12,5 horas:

```
# systemd-run --on-active="12h 30m" --unit *algumaunit*.service

```

Veja [systemd-run(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-run.1) para mais informações e exemplos.

## Como um substituto do cron

Embora o [cron](/index.php/Cron "Cron") seja indiscutivelmente o agendador de tarefas mais conhecido, os temporizadores *systemd* podem ser uma alternativa.

### Benefícios

Os principais benefícios do uso de timers vêm de cada job ter seu próprio serviço *systemd*. Alguns desses benefícios são:

*   Os trabalhos podem ser facilmente iniciados independentemente de seus timers. Isso simplifica a depuração.
*   Cada trabalho pode ser configurado para ser executado em um ambiente específico (consulte [systemd.exec(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.exec.5)).
*   Os trabalhos podem ser anexados a [cgroups](/index.php/Cgroups "Cgroups").
*   Os trabalhos podem ser configurados para depender de outras units *systemd*.
*   Os trabalhos são registrados no diário *systemd* para facilitar a depuração.

### Ressalvas

Algumas coisas que são fáceis de fazer com o cron são difíceis de fazer apenas com units de timers:

*   Criação: para configurar um trabalho com timer com *systemd*, você precisa criar dois arquivos e executar comandos `systemctl`, em comparação com a adição de uma única linha a um crontab.
*   E-mails: não há um equivalente interno ao `MAILTO` do cron para enviar e-mails em caso de falha no trabalho. Veja a próxima seção para um exemplo de configuração de uma funcionalidade similar usando `OnFailure=`.

### MAILTO

Você pode configurar o systemd para enviar um e-mail quando uma unit falhar. Cron envia um e-mail para `MAILTO` se o trabalho é gerado para stdout ou stderr, mas muitos trabalhos são configurados para serem emitidos somente com erro. Primeiro você precisa de dois arquivos: um executável para enviar o e-mail e um *.service* para iniciar o executável. Para este exemplo, o executável é apenas um script de shell usando `sendmail`, que está em pacotes que fornecem `smtp-forwarder`.

 `/usr/local/bin/systemd-email` 
```
#!/bin/sh

/usr/bin/sendmail -t <<ERRMAIL
To: $1
From: systemd <root@$HOSTNAME>
Subject: $2
Content-Transfer-Encoding: 8bit
Content-Type: text/plain; charset=UTF-8

$(systemctl status --full "$2")
ERRMAIL
```

Seja qual for o executável que você usa, ele provavelmente deve ter pelo menos dois argumentos, como o script de shell: o endereço para enviar e o arquivo de unit para obter o status. O *.service* que criamos passará esses argumentos:

 `/etc/systemd/system/status-email-*usuário*@.service` 
```
[Unit]
Description=e-mail de estado de %i para *usuário*

[Service]
Type=oneshot
ExecStart=/usr/local/bin/systemd-email *endereço* %i
User=nobody
Group=systemd-journal
```

sendo `*usuário*` o usuário que está sendo enviado por e-mail e o `*endereço*` o endereço de e-mail desse usuário. Embora o destinatário esteja embutido em código, o arquivo unit a ser relatado é passado como um parâmetro de instância, portanto, esse serviço pode enviar emails para muitas outras units. Neste ponto, você pode [iniciar](/index.php/Inicia "Inicia") `status-email-*usuário*@dbus.service` para verificar se você pode receber os e-mails.

Em seguida, basta [editar](/index.php/Editar "Editar") o serviço para o qual você deseja receber e-mails `OnFailure=status-email-*usuário*@%n.service` para o `[Unit]` seção. `%n` passa o nome da unit para o modelo.

**Nota:**

*   Se você configurar a segurança do SSMTP de acordo com [SSMTP#Security](/index.php/SSMTP#Security "SSMTP"), o usuário `nobody` não terá acesso a `/etc/ssmtp/ssmtp.conf` e o comando `systemctl start status-email-*usuário*@dbus.service` falhará. Uma solução é usar `root` como o usuário da unit `status-email-*usuário*@.service`.
*   Se você tentar usar o `mail -s algunslogs *endereço*` no seu script de e-mail, `mail` fará um *fork* e o systemd eliminará o processo de e-mail quando vir sua saída de script. Certifique-se que o e-mail não faça um "fork" fazendo `mail -Ssendwait -s algunslogs *endereços*`.

### Usando um crontab

Várias das ressalvas podem ser contornadas instalando um pacote que analisa um crontab tradicional para configurar os timers. [systemd-cron-next](https://aur.archlinux.org/packages/systemd-cron-next/) e [systemd-cron](https://aur.archlinux.org/packages/systemd-cron/) são dois desses pacotes. Eles podem fornecer o recurso `MAILTO` ausente.

Além disso, assim como no crontabs, uma visão unificada de todos os trabalhos agendados pode ser obtida com `systemctl`. Veja [#Gerenciamento](#Gerenciamento).

## Veja também

*   [systemd.timer(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.timer.5)
*   [Página wiki do Projeto Fedora](https://fedoraproject.org/wiki/Features/SystemdCalendarTimers) sobre timers de calendário do *systemd*
*   [Seção no wiki do Gentoo](https://wiki.gentoo.org/wiki/Systemd#Timer_services) sobre serviços de timer do *systemd*
*   **systemd-cron-next** — Ferramenta para gerar timers/serviços a partir de arquivos crontab e anacrontab

	[https://github.com/systemd-cron/systemd-cron-next](https://github.com/systemd-cron/systemd-cron-next) || [systemd-cron-next](https://aur.archlinux.org/packages/systemd-cron-next/)

*   **systemd-cron** — Fornece units de systemd para executar scripts do cron; usando *systemd-crontab-generator* para converter crontabs

	[https://github.com/systemd-cron/systemd-cron](https://github.com/systemd-cron/systemd-cron) || [systemd-cron](https://aur.archlinux.org/packages/systemd-cron/)