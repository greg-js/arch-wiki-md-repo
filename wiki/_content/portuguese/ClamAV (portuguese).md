[Clam AntiVirus](https://www.clamav.net) é uma caixa de ferramentas de antivírus, código aberto (GPL), para UNIX. Ele fornece uma série de utilitários, incluindo um daemon multi-threaded flexível e escalável, um scanner de linha de comando e uma ferramenta avançada para atualizações automáticas de banco de dados. Como o uso principal do ClamAV é em servidores de arquivos/e-mails para desktops Windows, ele principalmente detecta vírus e malwares do Windows com suas assinaturas embutidas.

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
*   [2 Atualizando o banco de dados](#Atualizando_o_banco_de_dados)
*   [3 Iniciando o daemon](#Iniciando_o_daemon)
*   [4 Testando o software](#Testando_o_software)
*   [5 Adicionando mais repositórios de bancos de dados/assinaturas](#Adicionando_mais_reposit.C3.B3rios_de_bancos_de_dados.2Fassinaturas)
    *   [5.1 Configure clamav-unofficial-sigs](#Configure_clamav-unofficial-sigs)
        *   [5.1.1 Banco de dados MalwarePatrol](#Banco_de_dados_MalwarePatrol)
*   [6 Varrendo por vírus](#Varrendo_por_v.C3.ADrus)
*   [7 Usando o milter](#Usando_o_milter)
*   [8 OnAccessScan](#OnAccessScan)
*   [9 Troubleshooting](#Troubleshooting)
    *   [9.1 Erro: Clamd was NOT notified](#Erro:_Clamd_was_NOT_notified)
    *   [9.2 Erro: No supported database files found](#Erro:_No_supported_database_files_found)
    *   [9.3 Erro: Can't create temporary directory](#Erro:_Can.27t_create_temporary_directory)

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [clamav](https://www.archlinux.org/packages/?name=clamav). Também, você pode instalar:

*   [clamtk](https://www.archlinux.org/packages/?name=clamtk) , um front-end gráfico para o clamav.
*   complementos
    *   [clamtk-gnome](https://aur.archlinux.org/packages/clamtk-gnome/) , um plug-ins simples para ClamTk para permitir um scan por meio de item de menu de contexto, clicando com botão direito do mouse sobre arquivos ou pastas no gerenciador de arquivos no Nautilus.
    *   [thunar-sendto-clamtk](https://aur.archlinux.org/packages/thunar-sendto-clamtk/) , um plug-ins simples para permitir um scan por meio de item de menu de contexto, clicando com botão direito do mouse sobre arquivos ou pastas no gerenciador de arquivos no Thunar.

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

O serviço de atualização de definição de vírus é chamado de `clamav-freshclam.service`. Considere iniciá-lo e habilitá-lo para que inicie quando da inicialização do sistema, para que as definições de vírus estejam sempre recentes.

## Iniciando o daemon

Considere atualizar o banco de dados antes de iniciar o serviço pela primeira vez ou você poderá ter problemas/erros que impedirão o ClamAV de iniciar corretamente.

O serviço chamado `clamav-daemon.service`. [Inicie](/index.php/Inicie "Inicie")-o ou [habilite](/index.php/Habilite "Habilite")-o para iniciar quando da inicialização do sistema. Você precisará executar `freshclam` antes de iniciar o serviço.

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

Para adicionar os mais importantes em um único passo, instale [clamav-unofficial-sigs](https://aur.archlinux.org/packages/clamav-unofficial-sigs/) e configure-o em `/etc/clamav-unofficial-sigs/user.conf`.

Isso vai adicionar assinaturas/banco de dados de, por exemplo, MalwarePatrol, SecuriteInfo, Yara, Linux Malware Detect, etc. Para a lista completa de banco de dados, [veja a descrição de seu repositório no GitHub](https://github.com/extremeshok/clamav-unofficial-sigs#description).

### Configure clamav-unofficial-sigs

Primeiro, edite a configuração em `/etc/clamav-unofficial-sigs/user.conf`, e altere a seguinte linha:

```
# Descomente a linha a seguir para habilitar o script
user_configuration_complete="yes"

```

Para habilitar o serviço não oficial de assinaturas (que inclui páginas man, rotação de log e cron job), execute o seguinte:

```
# clamav-unofficial-sigs.sh --install-all

```

Note que você ainda deve estar com o serviço `clamav-daemon` em execução para ter atualizações de assinatura do próprio ClamAV.

Isso vai atualizar as assinaturas dos bancos de dados usados no script clamav-unofficial-sigs e extras conforme configurado em cada arquivo de configuração na pasta `/etc/clamav-unofficial-sigs`. Para atualizar assinaturas desses bancos de dados manualmente, execute o seguinte:

```
# clamav-unofficial-sigs.sh

```

Para parar a execução do cron job, exclua esses arquivo: `/etc/cron.d/clamav-unofficial-sigs`.

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
$ clamscan --recursive --infected /home # ou -r -i
$ clamscan --recursive --infected --exclude-dir='^/sys|^/dev' /

```

Se você quiser que `clamscan` remova o arquivo infectado, adicione ao comando a opção `--remove` ou você pode usar `--move=/dir` para colocá-los em quarentena.

Você também pode se interessar em usar o `clamscan` para varrer arquivos grandes. Neste caso, anexe as opções `--max-filesize=4000M` e `--max-scansize=4000M` ao comando. "4000M" é o maior valor possível e pode ser diminuído conforme necessário.

Usar a opção `-l /caminho/para/arquivo` vai imprimir os logs do `clamscan` para um arquivo texto para localizar infecções relatadas.

## Usando o milter

Milter will scan your sendmail server for email containing virus. Copy `/etc/clamav/clamav-milter.conf.sample` to `/etc/clamav/clamav-milter.conf` and adjust it to your needs. For example:

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

Create `/etc/systemd/system/clamav-milter.service`:

 `/etc/systemd/system/clamav-milter.service` 
```
[Unit]
Description='ClamAV Milter'
After=clamd.service

[Service]
Type=forking
ExecStart=/usr/bin/clamav-milter --config-file /etc/clamav/clamav-milter.conf

[Install]
WantedBy=multi-user.target

```

Enable and start the service.

## OnAccessScan

On-access scanning requires the kernel to be compiled with the *fanotify* kernel module (kernel >= 3.8). Check if *fanotify* has been enabled before enabling on-access scanning.

```
$ cat /proc/config.gz | gunzip | grep FANOTIFY=y

```

On-access scanning will scan the file while reading, writing or executing it.

First, edit the `/etc/clamav/clamd.conf` configuration file by adding the following to the end of the file (you can also change the individual options):

 `/etc/clamav/clamd.conf` 
```
# Enables on-access scan, requires clamd service running
ScanOnAccess true

# Set the mount point where to recursively perform the scan,
# this could be every path or multiple path (one line for path)
OnAccessMountPath /usr
OnAccessMountPath /home/
OnAccessExcludePath /var/log/

# Flag fanotify to block any events on monitored files to perform the scan
OnAccessPrevention false

# Perform scans on newly created, moved, or renamed files
OnAccessExtraScanning true

# Check the UID from the event of fanotify
OnAccessExcludeUID 0

# Specify an action to perform when clamav detects a malicious file
# it is possible to specify an inline command too
VirusEvent /etc/clamav/detected.zsh

# WARNING: clamd should run as root
User root

```

Next, create the file `/etc/clamav/detected.zsh` and add the following. This allows you to change/specify the debug message when a virus has been detected by clamd's on-access scanning service:

 `/etc/clamav/detected.sh` 
```
#!/bin/bash
PATH=/usr/bin

alert="Signature detected: $CLAM_VIRUSEVENT_VIRUSNAME in $CLAM_VIRUSEVENT_FILENAME"

# Send the alert to systemd logger if exist, othewise to /var/log
if [[ -z $(command -v systemd-cat) ]]; then
	echo "$(date) - $alert" >> /var/log/clamav/infected.log
else
	# as "emerg", this could cause your DE to show a visual alert. Happen in Plasma. but the next visual alert is much nicer
	echo "$alert" | /usr/bin/systemd-cat -t clamav -p emerg
fi

#send an alrt to all graphical user
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

If you are using [AppArmor](/index.php/AppArmor "AppArmor"), it is also necessary to allow clamd to run as root:

```
# aa-complain clamd

```

Restart/start the service with `systemctl restart clamd.service`.

Source: [http://blog.clamav.net/2016/03/configuring-on-access-scanning-in-clamav.html](http://blog.clamav.net/2016/03/configuring-on-access-scanning-in-clamav.html)

## Troubleshooting

### Erro: Clamd was NOT notified

If you get the following messages after running freshclam:

```
WARNING: Clamd was NOT notified: Cannot connect to clamd through 
/var/lib/clamav/clamd.sock connect(): No such file or directory

```

Add a sock file for ClamAV:

```
# touch /var/lib/clamav/clamd.sock
# chown clamav:clamav /var/lib/clamav/clamd.sock

```

Then, edit `/etc/clamav/clamd.conf` - uncomment this line:

```
LocalSocket /var/lib/clamav/clamd.sock

```

Save the file and [restart the daemon](/index.php/Daemons "Daemons") with `systemctl restart clamd.service`.

### Erro: No supported database files found

If you get the next error when starting the daemon:

```
LibClamAV Error: cli_loaddb(): No supported database files found
in /var/lib/clamav ERROR: Not supported data format

```

This happens because of mismatch between `/etc/freshclam.conf` setting `DatabaseDirectory` and `/etc/clamd.conf` setting `DatabaseDirectory`. `/etc/freshclam.conf` pointing to `/var/lib/clamav`, but `/etc/clamd.conf` (default directory) pointing to `/usr/share/clamav`, or other directory. Edit in `/etc/clamd.conf` and replace with the same DatabaseDirectory like in `/etc/freshclam.conf`. After that clamav will start up succesfully.

### Erro: Can't create temporary directory

If you get the following error, along with a 'HINT' containing a UID and a GID number:

```
# can't create temporary directory

```

Correct permissions:

```
# chown UID:GID /var/lib/clamav & chmod 755 /var/lib/clamav

```