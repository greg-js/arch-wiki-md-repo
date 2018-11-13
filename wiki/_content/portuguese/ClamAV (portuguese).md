**Status de tradução:** Esse artigo é uma tradução de [ClamAV](/index.php/ClamAV "ClamAV"). Data da última tradução: 2018-09-18\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=ClamAV&diff=0&oldid=539450) na versão em inglês.

[Clam AntiVirus](https://www.clamav.net) é uma caixa de ferramentas de antivírus, código aberto (GPL), para UNIX. Ele fornece uma série de utilitários, incluindo um daemon multi-threaded flexível e escalável, um scanner de linha de comando e uma ferramenta avançada para atualizações automáticas de banco de dados. Como o uso principal do ClamAV é em servidores de arquivos/e-mails para desktops Windows, ele principalmente detecta vírus e malwares do Windows com suas assinaturas embutidas.

## Contents

*   [1 Instalação](#Instalação)
*   [2 Atualizando o banco de dados](#Atualizando_o_banco_de_dados)
*   [3 Iniciando o daemon](#Iniciando_o_daemon)
*   [4 Testando o software](#Testando_o_software)
*   [5 Adicionando mais repositórios de bancos de dados/assinaturas](#Adicionando_mais_repositórios_de_bancos_de_dados/assinaturas)
    *   [5.1 Configure clamav-unofficial-sigs](#Configure_clamav-unofficial-sigs)
        *   [5.1.1 Banco de dados MalwarePatrol](#Banco_de_dados_MalwarePatrol)
*   [6 Varrendo por vírus](#Varrendo_por_vírus)
*   [7 Usando o milter](#Usando_o_milter)
*   [8 OnAccessScan](#OnAccessScan)
*   [9 Solução de programas](#Solução_de_programas)
    *   [9.1 Erro: Clamd was NOT notified](#Erro:_Clamd_was_NOT_notified)
    *   [9.2 Erro: No supported database files found](#Erro:_No_supported_database_files_found)
    *   [9.3 Erro: Can't create temporary directory](#Erro:_Can't_create_temporary_directory)
*   [10 Dicas e truques](#Dicas_e_truques)
    *   [10.1 Executar em múltiplas threads](#Executar_em_múltiplas_threads)
*   [11 Veja também](#Veja_também)

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [clamav](https://www.archlinux.org/packages/?name=clamav).

## Atualizando o banco de dados

Atualize as definições de vírus com:

```
# freshclam

```

Os arquivos de banco de dados são salvos em:

```
/var/lib/clamav/daily.cvd
/var/lib/clamav/main.cvd
/var/lib/clamav/bytecode.cvd

```

[Inicie/habilite](/index.php/Inicie/habilite "Inicie/habilite") `clamav-freshclam.service` para que as definições de vírus estejam sempre recentes.

## Iniciando o daemon

**Nota:** Você precisa executar `freshclam` antes de iniciar o serviço pela primeira vez ou você poderá ter problemas/erros que impedirão o ClamAV de iniciar corretamente.

O serviço chamado `clamav-daemon.service`. [Inicie](/index.php/Inicie "Inicie")-o e [habilite](/index.php/Habilite "Habilite")-o para iniciar quando da inicialização do sistema.

## Testando o software

Para ter certeza que o ClamAV e as definições estão instaladas corretamente, execute um scan no [arquivo de teste EICAR](https://www.eicar.org/86-0-Intended-use.html) (uma assinatura inofensiva com nenhum código de vírus) com clamscan.

```
$ curl [https://www.eicar.org/download/eicar.com.txt](https://www.eicar.org/download/eicar.com.txt) | clamscan -

```

A saída **deve** incluir:

```
stdin: Eicar-Test-Signature FOUND

```

Do contrário, leia a parte Solução de Problemas ou peça por ajuda nos [Fóruns do Arch](https://bbs.archlinux.org/).

## Adicionando mais repositórios de bancos de dados/assinaturas

ClamAV pode usar banco de dados/assinaturas de outros repositórios ou fornecedores de segurança.

Para adicionar os mais importantes em um único passo, instale [clamav-unofficial-sigs](https://aur.archlinux.org/packages/clamav-unofficial-sigs/).

Isso vai adicionar assinaturas/banco de dados de, por exemplo, MalwarePatrol, SecuriteInfo, Yara, Linux Malware Detect, etc. Para a lista completa de banco de dados, [veja a descrição de seu repositório no GitHub](https://github.com/extremeshok/clamav-unofficial-sigs#description).

### Configure clamav-unofficial-sigs

[Habilite](/index.php/Habilite "Habilite") o `clamav-unofficial-sigs.timer`.

Isso vai atualizar regularmente as assinaturas não oficiais baseadas nos arquivos de configuração no diretório `/etc/clamav-unofficial-sigs`.

Para atualizar as assinaturas manualmente, execute o seguinte comando:

```
# clamav-unofficial-sigs.sh

```

Para alterar as configurações padrão, acesse e modifique `/etc/clamav-unofficial-sigs/user.conf`.

**Nota:** Você ainda deve estar com o `clamav-freshclam.service` [iniciado](/index.php/Iniciado "Iniciado") para ter atualizações de assinaturas oficiais dos espelhos do ClamAV.

#### Banco de dados MalwarePatrol

Se você quiser de usar o banco de dados do MalwarePatrol, crie uma conta em [https://www.malwarepatrol.net/](https://www.malwarepatrol.net/).

Em `/etc/clamav-unofficial-sigs/user.conf`, altere o seguinte para habilitar essa funcionalidade:

```
malwarepatrol_receipt_code="SEU-NÚMERO-RECIBO" # Insira seu número de recibo aqui
malwarepatrol_product_code="8" # Use 8 se você tiver uma conta Free ou 15 se você for um cliente Premium.
malwarepatrol_list="clamav_basic" # *clamav_basic* ou *clamav_ext*
malwarepatrol_free="yes" # Defina para *yes* se você tiver uma conta Free ou *no* see você tiver uma conta Premium.

```

Fonte: [https://www.malwarepatrol.net/clamav-configuration-guide/](https://www.malwarepatrol.net/clamav-configuration-guide/)

## Varrendo por vírus

`clamscan` pode ser usado para varrer *(scan)* certos arquivos, diretórios home, um sistema inteiro:

```
$ clamscan meuarquivo
$ clamscan --recursive --infected /home
$ clamscan --recursive --infected --exclude-dir='^/sys|^/dev' /

```

Se você quiser que `clamscan` remova o arquivo infectado, adicione ao comando a opção `--remove` ou você pode usar `--move=/dir` para colocá-los em quarentena.

Você também pode se interessar em usar o `clamscan` para varrer arquivos grandes. Neste caso, anexe as opções `--max-filesize=4000M` e `--max-scansize=4000M` ao comando. "4000M" é o maior valor possível e pode ser diminuído conforme necessário.

Usar a opção `-l /caminho/para/arquivo` vai imprimir os logs do `clamscan` para um arquivo texto para localizar infecções relatadas.

## Usando o milter

Milter vai realizar um scan em seu servidor sendmail por e-mail contendo vírus. Copie `/etc/clamav/clamav-milter.conf.sample` para `/etc/clamav/clamav-milter.conf` e ajuste-o às suas necessidades. Por exemplo:

 `/etc/clamav/clamav-milter.conf` 
```
MilterSocket /run/clamav/clamav-milter.sock
MilterSocketMode 660
FixStaleSocket yes
User clamav
PidFile /run/clamav/clamav-milter.pid
TemporaryDirectory /tmp
ClamdSocket unix:/var/lib/clamav/clamd.sock
LogSyslog yes
LogInfected Basic
```

Crie `/etc/systemd/system/clamav-milter.service`:

 `/etc/systemd/system/clamav-milter.service` 
```
[Unit]
Description='ClamAV Milter'
After=clamav-daemon.service

[Service]
Type=forking
ExecStart=/usr/bin/clamav-milter --config-file /etc/clamav/clamav-milter.conf

[Install]
WantedBy=multi-user.target
```

[Habilite](/index.php/Habilite "Habilite") e [inicie](/index.php/Inicie "Inicie") `clamav-milter.service`.

## OnAccessScan

A varredura no acesso (*on-access scan*) requer que o kernel seja compilado com o módulo kernel *fanotify* (kernel >= 3.8). Verifique se *fanotify* foi ativado antes de ativar a varredura no acesso.

```
 $ zgrep FANOTIFY /proc/config.gz

```

A varredura no acesso digitalizará o arquivo ao ler, escrever ou executá-lo.

Primeiro, edite o arquivo de configuração `/etc/clamav/clamd.conf`, adicionando o seguinte ao final do arquivo (você também pode alterar as opções individuais):

 `/etc/clamav/clamd.conf` 
```
# Ativa varredura no acesso, exige que clamav-daemon.service esteja em execução
ScanOnAccess true

# Define o ponto de montagem onde deve-se realizar recursivamente a varredura,
# isso poderia ser todo caminho ou vários caminho (uma linha por caminho)
OnAccessMountPath /usr
OnAccessMountPath /home/
OnAccessExcludePath /var/log/

# Sinaliza fanotify para bloquear quaisquer eventos em arquivos monitorados para realizar a varredura
OnAccessPrevention false

# Realiza a varredura em arquivos recém-criados, movidos ou renomeados
OnAccessExtraScanning true

# Verifica o UID do evento do fanotify
OnAccessExcludeUID 0

# Especifica uma ação para realizar quando o clamav detecta um arquivo malicioso
# é possível especificar um comando em linha também
VirusEvent /etc/clamav/detected.sh

# AVISO: clamd deve ser executado como root
User root

```

Em seguida, crie o arquivo `/etc/clamav/detected.sh` e adicione o conteúdo a seguir. Isso permite que você altere/especifique a mensagem de depuração quando um vírus tiver sido detectado pelo dispositivo de varredura no acesso do clamd:

 `/etc/clamav/detected.sh` 
```
#!/bin/bash
PATH=/usr/bin

alert="Signature detected: $CLAM_VIRUSEVENT_VIRUSNAME in $CLAM_VIRUSEVENT_FILENAME"

# Envia o alerta para o systemd logger se existir, do contrário para /var/log
if [[ -z $(command -v systemd-cat) ]]; then
	echo "$(date) - $alert" >> /var/log/clamav/infected.log
else
	# como "emerg", isso poderia fazer com que seu DE mostre um alerta virtual. Acontece no plasma, mas o próximo alerta visual é muito melhor
	echo "$alert" | /usr/bin/systemd-cat -t clamav -p emerg
fi

# Envia um alerta para todos os usuários gráficos
XUSERS=($(who|awk '{print $1$NF}'|sort -u))

for XUSER in $XUSERS; do
    NAME=(${XUSER/(/ })
    DISPLAY=${NAME[1]/)/}
    DBUS_ADDRESS=unix:path=/run/user/$(id -u ${NAME[0]})/bus
    echo "run $NAME - $DISPLAY - $DBUS_ADDRESS -" >> /tmp/testlog 
    /usr/bin/sudo -u ${NAME[0]} DISPLAY=${DISPLAY} \
                       DBUS_SESSION_BUS_ADDRESS=${DBUS_ADDRESS} \
                       PATH=${PATH} \
                       /usr/bin/notify-send -i dialog-warning "clamAV" "$alert"
done

```

Se você está usando [AppArmor](/index.php/AppArmor "AppArmor"), também é necessário permitir que o clamd execute como root:

```
# aa-complain clamd

```

[Reinicie](/index.php/Reinicie "Reinicie") o `clamav-daemon.service`.

Fonte: [http://blog.clamav.net/2016/03/configuring-on-access-scanning-in-clamav.html](http://blog.clamav.net/2016/03/configuring-on-access-scanning-in-clamav.html)

## Solução de programas

### Erro: Clamd was NOT notified

Se você receber as seguintes mensagens após executar freshclam:

```
WARNING: Clamd was NOT notified: Cannot connect to clamd through 
/var/lib/clamav/clamd.sock connect(): No such file or directory

```

Adicione um arquivo sock ao ClamAV:

```
# touch /var/lib/clamav/clamd.sock
# chown clamav:clamav /var/lib/clamav/clamd.sock

```

Então, edite `/etc/clamav/clamd.conf` - descomente essa linha:

```
LocalSocket /var/lib/clamav/clamd.sock

```

Salve o arquivo e [reinicie](/index.php/Reinicie "Reinicie") `clamav-daemon.service`.

### Erro: No supported database files found

Se você receber o erro abaixo quando iniciar o daemon:

```
LibClamAV Error: cli_loaddb(): No supported database files found
in /var/lib/clamav ERROR: Not supported data format

```

Isso acontece por causa de incompatibilidade entre a configuração `DatabaseDirectory` do `/etc/clamav/freshclam.conf` e `DatabaseDirectory` do `/etc/clamav/clamd.conf`. `/etc/clamav/freshclam.conf` apontando para `/var/lib/clamav`, mas `/etc/clamav/clamd.conf` (diretório padrão) apontando para `/usr/share/clamav`, ou outro diretório. Edite `/etc/clamav/clamd.conf` e substituta com o mesmo DatabaseDirectory como no `/etc/clamav/freshclam.conf`. Após isso, clamav vai iniciar com sucesso.

### Erro: Can't create temporary directory

Se você obtiver o erro a seguir, junto com um 'HINT' contendo um número de UID e um de GID:

```
# can't create temporary directory

```

Corrija as permissões:

```
# chown *UID*:*GID* /var/lib/clamav & chmod 755 /var/lib/clamav

```

sendo *UID* e *GID* o informado na dica acima

## Dicas e truques

### Executar em múltiplas threads

Ao varrer um arquivo ou diretório a partir da linha de comando usando `clamscan` ou `clamdscan`, apenas uma única thread de CPU é usada para varrer os arquivos um a um. Isso pode servir nos casos em que você não quer que o seu computador fique lento enquanto a verificação está em andamento, mas se você quiser digitalizar rapidamente uma pasta grande ou uma unidade USB, você pode querer usar todas as CPUs disponíveis para acelerar o processo.

`clamscan` é projetado para funcionar em uma única thread, então você precisaria usar alguma coisa como `xargs` para executar a varredura em paralelo:

```
$ find /home/archie -type f -print | xargs -P 2 clamscan

```

Neste exemplo, o parâmetro `-P` para `xargs` executa `clamscan` em até 2 processos por vez. Se você tiver mais CPUs disponíveis, ajuste esse parâmetro de acordo. As opções `--max-lines` e `--max-args` permitirão um controle ainda melhor do envio em lote da carga de trabalho entre as threads.

Use a seguinte versão se os nomes de arquivos puderem conter espaços ou outros caracteres especiais (como fazem frequentemente as unidades USB e ex-Windows):

```
$ find /home/archie -type f -print0 | xargs -0 -P 2 clamscan

```

`clamdscan` usa o daemon `clamd` para realizar a varredura. Você precisa iniciar o daemon `clamd` primeiro (veja [#Iniciando o daemon](#Iniciando_o_daemon)) e então executar o seguinte comando:

```
$ clamdscan --multiscan --fdpass /home/archie

```

Aqui, o parâmetro `--multiscan` permite que o `clamd` verifique o conteúdo do diretório em paralelo usando as threads disponíveis. O parâmetro `--fdpass` é necessário para passar as permissões do descritor de arquivo para `clamd`, pois o daemon está sendo executado sob o usuário e grupo `clamav`.

O número de threads disponíveis para `clamdscan` é determinado em `/etc/clamav/clamd.conf` através do parâmetro `MaxThreads` [clamd.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/clamd.conf.5). Mesmo que você possa ver que o número de `MaxThreads` especificado é mais de um (o padrão atual é 10), quando você inicia a varredura usando `clamdscan` na linha de comando e não especifica a opção `--multiscan`, apenas uma thread eficaz da CPU será usado para a varredura.

## Veja também

*   [Wikipedia:ClamAV](https://en.wikipedia.org/wiki/ClamAV "wikipedia:ClamAV")
*   [ClamSMTP](/index.php/ClamSMTP_(Portugu%C3%AAs) "ClamSMTP (Português)")