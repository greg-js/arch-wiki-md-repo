Veja [systemd (Português)](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") para o artigo principal.

*systemd* tem o seu próprio sistema de registro chamado de o journal e, portanto, a execução de uma daemon `syslog` não é mais necessário. Para ler o registro, utilize:

```
# journalctl

```

No Arch Linux, o diretório `/var/log/journal/` faz parte do pacote *systemd* e o journal (quando `Storage=` está definido para `auto` em `/etc/systemd/journald.conf`) vai escrever para `/var/log/journal/`. Se você ou algum programa excluir esse diretório, systemd **não** vai recriá-lo automaticamente e, em vez disso,vai escrever seus logs em `/run/systemd/journal` em uma forma não persistente. Porém, a pasta será recriada quando você definir `Storage=persistent` e [reiniciar](/index.php/Reiniciar "Reiniciar") `systemd-journald.service` (ou reinicializar o sistema).

O journal do systemd classifica mensagens por [nível de prioridade](#Nível_de_prioridade) e [facilidade](#Facilidade). A classificação de registro de logs corresponde ao clássico protocolo do [Syslog](https://en.wikipedia.org/wiki/pt:Syslog "wikipedia:pt:Syslog") ([RFC 5424](https://tools.ietf.org/html/rfc5424)).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Nível de prioridade](#Nível_de_prioridade)
*   [2 Facilidade](#Facilidade)
*   [3 Filtrando saída](#Filtrando_saída)
*   [4 Limite no tamanho do journal](#Limite_no_tamanho_do_journal)
*   [5 Limpar arquivos de journal manualmente](#Limpar_arquivos_de_journal_manualmente)
*   [6 Journald em conjunto com o syslog](#Journald_em_conjunto_com_o_syslog)
*   [7 Encaminhar journald para /dev/tty12](#Encaminhar_journald_para_/dev/tty12)
*   [8 Especificar um journal diferente para ver](#Especificar_um_journal_diferente_para_ver)

## Nível de prioridade

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

## Facilidade

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

## Filtrando saída

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

**Dica:** Por padrão, *journalctl* trunca linhas maiores que a largura da tela, mas em alguns casos pode ser melhor habilitar *wrapping* em vez de trucamento'. Isso pode ser controlado pela [variável de ambiente](/index.php/Vari%C3%A1vel_de_ambiente "Variável de ambiente") `SYSTEMD_LESS`, que contém opções passadas ao [less](/index.php/Utilit%C3%A1rios_principais#Essenciais "Utilitários principais") (o paginador padrão) e usa como padrão `FRSXMK` (veja [less(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/less.1) e [journalctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journalctl.1) para detalhes).

Ao omitir a opção `S`, a saída estará sob *wrap* em vez de truncamento. Por exemplo, inicie *journalctl* da seguinte forma:

```
$ SYSTEMD_LESS=FRXMK journalctl

```
Se você quiser definir esse comportamento como padrão, [exporte](/index.php/Vari%C3%A1vel_de_ambiente#Por_usuário "Variável de ambiente") a variável a partir de `~/.bashrc` ou `~/.zshrc`.

## Limite no tamanho do journal

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

## Limpar arquivos de journal manualmente

Os arquivos de journal podem ser removidos globalmente de `/var/log/journal/` usando, por exemplo, `rm` ou podem ser aparados de acordo com vários critérios usando `journalctl` . Exemplos:

*   Remova arquivos de journal armazenados até que o espaço em disco que eles usam fique abaixo de 100 MB: `# journalctl --vacuum-size=100M` 
*   Faça com que todos os arquivos de diário não contenham dados com mais de 2 semanas. `# journalctl --vacuum-time=2weeks` 

Veja [journalctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journalctl.1) para mais informações.

## Journald em conjunto com o syslog

Compatibilidade com uma implementação clássica, sem journald, do [syslog](/index.php/Syslog-ng "Syslog-ng") pode ser fornecida deixando o *systemd* encaminhar todas as mensagens pelo soquete `/run/systemd/journal/syslog`. Para fazer funcionar o daemon do syslog com o journal, ele tem que associar a este soquete em vez de `/dev/log` ([anúncio oficial](http://lwn.net/Articles/474968/)).

O `journald.conf` padrão para encaminhar para o soquete é `ForwardToSyslog=no` para evitar sobrecarga de sistema, porque [rsyslog](/index.php/Rsyslog "Rsyslog") ou [syslog-ng](/index.php/Syslog-ng "Syslog-ng") obtêm as mensagens do journal [eles mesmo](https://lists.freedesktop.org/archives/systemd-devel/2014-August/022295.html#journald).

Veja [Syslog-ng#Overview](/index.php/Syslog-ng#Overview "Syslog-ng") e [Syslog-ng#syslog-ng and systemd journal](/index.php/Syslog-ng#syslog-ng_and_systemd_journal "Syslog-ng") e [rsyslog](/index.php/Rsyslog "Rsyslog"), para detalhes sobre a configuração.

## Encaminhar journald para /dev/tty12

Crie um [diretório de *drop-in*](#Editando_units_fornecidas) `/etc/systemd/journald.conf.d` e crie um arquivo `fw-tty12.conf` nele:

 `/etc/systemd/journald.conf.d/fw-tty12.conf` 
```
[Journal]
ForwardToConsole=yes
TTYPath=/dev/tty12
MaxLevelConsole=info
```

Então, [reinicie](/index.php/Reinicie "Reinicie") `systemd-journald.service`.

## Especificar um journal diferente para ver

Pode ser necessário verificar os logs de outro sistema que esteja inativo na água, como a inicialização de um sistema ativo para recuperar um sistema de produção. Nesse caso, pode-se montar o disco em, p. ex., `/mnt` e especificar o caminho do journal via `-D`/`--directory`, assim:

```
$ journalctl -D */mnt*/var/log/journal -xe

```