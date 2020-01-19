**Status de tradução:** Esse artigo é uma tradução de [Reflector](/index.php/Reflector "Reflector"). Data da última tradução: 2020-01-18\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Reflector&diff=0&oldid=595449) na versão em inglês.

Artigos relacionados

*   [Espelhos](/index.php/Espelhos "Espelhos")
*   [Pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)")

[Reflector](http://xyne.archlinux.ca/projects/reflector/) é um script que pode recuperar a lista de espelhos mais recente da página [MirrorStatus](https://www.archlinux.org/mirrors/status/), filtrar os espelhos mais atualizados, classificá-los por velocidade e substituir o arquivo `/etc/pacman.d/mirrorlist`.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Uso](#Uso)
    *   [2.1 Exemplos](#Exemplos)
*   [3 Automação](#Automação)
    *   [3.1 Hook do pacman](#Hook_do_pacman)
    *   [3.2 Serviço de systemd](#Serviço_de_systemd)
    *   [3.3 Timer de systemd](#Timer_de_systemd)
    *   [3.4 Pacote reflector-timer](#Pacote_reflector-timer)
    *   [3.5 Tarefa do cron](#Tarefa_do_cron)

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [reflector](https://www.archlinux.org/packages/?name=reflector).

## Uso

**Atenção:**

*   Nos exemplos a seguir, `/etc/pacman.d/mirrorlist` vai ser sobrescrito. Faça um backup antes de proceder.
*   Certifique-se de que o `/etc/pacman.d/mirrorlist` resultante não contenha entradas que você considere não confiáveis antes de sincronizar ou atualizar com [Pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)").

Para ver todos os comandos disponíveis, execute o seguinte comando:

```
# reflector --help

```

### Exemplos

Classifica e ordena de forma detalhada os cinco espelhos sincronizados mais recentemente pela velocidade do download e sobrescreve o arquivo `/etc/pacman.d/mirrorlist`:

```
# reflector --verbose --latest 5 --sort rate --save /etc/pacman.d/mirrorlist

```

Seleciona os 200 espelhos HTTP ou HTTPS sincronizado mais recentemente, ordena-os pela velocidade de download e sobrescreve o arquivo `/etc/pacman.d/mirrorlist`:

```
# reflector --latest 200 --protocol http --protocol https --sort rate --save /etc/pacman.d/mirrorlist

```

Seleciona os espelhos HTTPS sincronizados dentro das últimas 12 horas e localizados na França ou Alemanha, ordena-os pela velocidade de download e sobrescreve o arquivo `/etc/pacman.d/mirrorlist`:

```
# reflector --country France --country Germany --age 12 --protocol https --sort rate --save /etc/pacman.d/mirrorlist

```

## Automação

### Hook do pacman

Você pode criar um [hook do pacman](/index.php/Hook_do_pacman "Hook do pacman") que executará *reflector* e removerá o arquivo *.pacnew* criado toda vez que [pacman-mirrorlist](https://www.archlinux.org/packages/?name=pacman-mirrorlist) recebe uma atualização.

 `/etc/pacman.d/hooks/mirrorupgrade.hook` 
```
[Trigger]
Operation = Upgrade
Type = Package
Target = pacman-mirrorlist

[Action]
Description = Updating pacman-mirrorlist with reflector and removing pacnew...
When = PostTransaction
Depends = reflector
Exec = /bin/sh -c "reflector --country 'United States' --latest 200 --age 24 --sort rate --save /etc/pacman.d/mirrorlist; rm -f /etc/pacman.d/mirrorlist.pacnew"

```

Certifique-se de substituir nos argumentos desejados para o *refletor*.

### Serviço de systemd

Este é um exemplo de uma unit de serviço que espera que a rede esteja ativa e online antes de executar o refletor:

 `/etc/systemd/system/reflector.service` 
```
[Unit]
Description=Pacman mirrorlist update
Wants=network-online.target
After=network-online.target

[Service]
Type=oneshot
ExecStart=/usr/bin/reflector --protocol https --latest 30 --number 20 --sort rate --save /etc/pacman.d/mirrorlist

[Install]
RequiredBy=multi-user.target
```

Ao [iniciar](/index.php/Inicia "Inicia") `reflector.service`, a lista de espelhos será atualizada. Para atualizar a lista de espelhos sempre que o computador inicializar, [habilite](/index.php/Habilite "Habilite") o serviço.

**Nota:** Para obter mais informações sobre a implementação da dependência de rede, consulte [Systemd (Português)#Executando serviços após a rede estar ativa](/index.php/Systemd_(Portugu%C3%AAs)#Executando_serviços_após_a_rede_estar_ativa "Systemd (Português)").

### Timer de systemd

Se você deseja executar `reflector.service` semanalmente, crie um *.timer* associado. Por exemplo:

 `/etc/systemd/system/reflector.timer` 
```
[Unit]
Description=Run reflector weekly

[Timer]
OnCalendar=Mon *-*-* 7:00:00
RandomizedDelaySec=15h
Persistent=true

[Install]
WantedBy=timers.target
```

E basta [iniciar](/index.php/Inicia "Inicia") o `reflector.timer`.

### Pacote reflector-timer

[Instale](/index.php/Instale "Instale") [reflector-timer](https://aur.archlinux.org/packages/reflector-timer/) para executar o *reflector* semanalmente.

A configuração padrão, que pode ser editada para atender necessidades específicas de cada um, é:

 `/usr/share/reflector-timer/reflector.conf` 
```
AGE=6
COUNTRY=Germany
LATEST=30
NUMBER=20
SORT=rate
### remova uma entrada, se você não deseja-o como um protocolo disponível
PROTOCOL1='-p http'
PROTOCOL2='-p https'
PROTOCOL3='-p ftp'
```

Certifique-se de [habilitar](/index.php/Habilita "Habilita") o `reflector.timer`.

### Tarefa do cron

Para atualizar o mirrorlist diariamente, considere o seguinte:

 `/etc/cron.daily/mirrorlist` 
```
#!/bin/bash

# Obtém a lista por país
/usr/bin/reflector -c "India" -p http --sort rate > /etc/pacman.d/mirrorlist

# Trabalha com as alternativas
/usr/bin/reflector -p http  --latest 20 -p https -p ftp --sort rate >> /etc/pacman.d/mirrorlist
```