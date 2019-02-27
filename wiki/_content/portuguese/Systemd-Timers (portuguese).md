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

One can use `systemd-run` to create transient `.timer` units. That is, one can set a command to run at a specified time without having a service file. For example the following command touches a file after 30 seconds:

```
# systemd-run --on-active=30 /bin/touch /tmp/foo

```

One can also specify a pre-existing service file that does not have a timer file. For example, the following starts the systemd unit named `*someunit*.service` after 12.5 hours have elapsed:

```
# systemd-run --on-active="12h 30m" --unit *someunit*.service

```

See [systemd-run(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-run.1) for more information and examples.

## Como um substituto do cron

Although [cron](/index.php/Cron "Cron") is arguably the most well-known job scheduler, *systemd* timers can be an alternative.

### Benefícios

The main benefits of using timers come from each job having its own *systemd* service. Some of these benefits are:

*   Jobs can be easily started independently of their timers. This simplifies debugging.
*   Each job can be configured to run in a specific environment (see [systemd.exec(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.exec.5)).
*   Jobs can be attached to [cgroups](/index.php/Cgroups "Cgroups").
*   Jobs can be set up to depend on other *systemd* units.
*   Jobs are logged in the *systemd* journal for easy debugging.

### Ressalvas

Some things that are easy to do with cron are difficult to do with timer units alone:

*   Creation: to set up a timed job with *systemd* you need to create two files and run `systemctl` commands, compared to adding a single line to a crontab.
*   Emails: there is no built-in equivalent to cron's `MAILTO` for sending emails on job failure. See the next section for an example of setting up a similar functionality using `OnFailure=`.

### MAILTO

You can set up systemd to send an e-mail when a unit fails. Cron sends mail to `MAILTO` if the job outputs to stdout or stderr, but many jobs are setup to only output on error. First you need two files: an executable for sending the mail and a *.service* for starting the executable. For this example, the executable is just a shell script using `sendmail`, which is in packages that provide `smtp-forwarder`.

 `/usr/local/bin/systemd-email` 
```
#!/bin/bash

/usr/bin/sendmail -t <<ERRMAIL
To: $1
From: systemd <root@$HOSTNAME>
Subject: $2
Content-Transfer-Encoding: 8bit
Content-Type: text/plain; charset=UTF-8

$(systemctl status --full "$2")
ERRMAIL
```

Whatever executable you use, it should probably take at least two arguments as this shell script does: the address to send to and the unit file to get the status of. The *.service* we create will pass these arguments:

 `/etc/systemd/system/status-email-*user*@.service` 
```
[Unit]
Description=status email for %i to *user*

[Service]
Type=oneshot
ExecStart=/usr/local/bin/systemd-email *address* %i
User=nobody
Group=systemd-journal
```

Where `*user*` is the user being emailed and `*address*` is that user's email address. Although the recipient is hard-coded, the unit file to report on is passed as an instance parameter, so this one service can send email for many other units. At this point you can [start](/index.php/Start "Start") `status-email-*user*@dbus.service` to verify that you can receive the emails.

Then simply [edit](/index.php/Edit "Edit") the service you want emails for and add `OnFailure=status-email-*user*@%n.service` to the `[Unit]` section. `%n` passes the unit's name to the template.

**Note:**

*   If you set up SSMTP security according to [SSMTP#Security](/index.php/SSMTP#Security "SSMTP") the user `nobody` will not have access to `/etc/ssmtp/ssmtp.conf`, and the `systemctl start status-email-*user*@dbus.service` command will fail. One solution is to use `root` as the User in the `status-email-*user*@.service` unit.
*   If you try to use `mail -s somelogs *address*` in your email script, `mail` will fork and systemd will kill the mail process when it sees your script exit. Make the mail non-forking by doing `mail -Ssendwait -s somelogs *address*`.

### Usando um crontab

Several of the caveats can be worked around by installing a package that parses a traditional crontab to configure the timers. [systemd-cron-next](https://aur.archlinux.org/packages/systemd-cron-next/) and [systemd-cron](https://aur.archlinux.org/packages/systemd-cron/) are two such packages. These can provide the missing `MAILTO` feature.

Also, like with crontabs, a unified view of all scheduled jobs can be obtained with `systemctl`. See [#Management](#Management).

## Veja também

*   [systemd.timer(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.timer.5)
*   [Fedora Project wiki page](https://fedoraproject.org/wiki/Features/SystemdCalendarTimers) on *systemd* calendar timers
*   [Gentoo wiki section](https://wiki.gentoo.org/wiki/Systemd#Timer_services) on *systemd* timer services
*   **systemd-cron-next** — tool to generate timers/services from crontab and anacrontab files

	[https://github.com/systemd-cron/systemd-cron-next](https://github.com/systemd-cron/systemd-cron-next) || [systemd-cron-next](https://aur.archlinux.org/packages/systemd-cron-next/)

*   **systemd-cron** — provides systemd units to run cron scripts; using *systemd-crontab-generator* to convert crontabs

	[https://github.com/systemd-cron/systemd-cron](https://github.com/systemd-cron/systemd-cron) || [systemd-cron](https://aur.archlinux.org/packages/systemd-cron/)