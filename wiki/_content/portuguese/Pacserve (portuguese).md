[Pacserve](http://xyne.archlinux.ca/projects/pacserve/) permite compartilhar facilmente pacotes do *pacman* entre computadores. Isso é muito útil se você tiver uma conexão lenta com a Internet, com várias máquinas funcionando com o Arch Linux.

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
*   [2 Configuração](#Configura.C3.A7.C3.A3o)
    *   [2.1 IPv6](#IPv6)
    *   [2.2 Avahi](#Avahi)
*   [3 Uso autônomo](#Uso_aut.C3.B4nomo)
*   [4 Configurar o Pacman para usar Pacserve](#Configurar_o_Pacman_para_usar_Pacserve)
*   [5 Solução de problemas](#Solu.C3.A7.C3.A3o_de_problemas)
    *   [5.1 Problemas se usar baixadores externos no pacman.conf](#Problemas_se_usar_baixadores_externos_no_pacman.conf)
*   [6 Veja também](#Veja_tamb.C3.A9m)

## Instalação

[Instale](/index.php/Instale "Instale") [pacserve](https://aur.archlinux.org/packages/pacserve/).

**Dica:** O pacote também está disponível no repositório não oficial [xyne-x86_64](/index.php/Unofficial_user_repositories#xyne-x86_64 "Unofficial user repositories").

Finalmente, [inicie/habilite](/index.php/Inicie/habilite "Inicie/habilite") `pacserve.service`.

No caso de você usar [iptables](/index.php/Iptables "Iptables"), você provavelmente terá que inciar `pacserve-ports.service` também. Para outros [firewalls](/index.php/Firewalls "Firewalls"), abra as portas TCP e UDP `15678`. A porta UDP pode ser limitada a tráfego multicast apenas.

## Configuração

O `pacserve.service` pode ser configurado editando `PACSERVE_ARGS` em `/etc/pacserve/pacserve.service.conf`. Execute `pacserve --help` para ver as opções disponíveis.

### IPv6

Para habilitar suporte a [IPv6](/index.php/IPv6 "IPv6"), adicione a opção `--ipv6` a `PACSERVE_ARGS` em `/etc/pacserve/pacserve.service.conf`.

### Avahi

Para anunciar ou descobrir o Pacserve usando [mDNS](/index.php/MDNS "MDNS"), adicione a opção `--avahi` a `PACSERVE_ARGS` em `/etc/pacserve/pacserve.service.conf`.

## Uso autônomo

Em vez de pacman, use o wrapper *pacsrv* para executar uma atualização, instalar pacotes e assim por diante. Ele irá baixar automaticamente todos os pacotes da LAN, se alguém os hospedar com o pacserve lá. Caso contrário, basta baixá-los dos espelhos da internet, como geralmente. Por exemplo:

```
# pacsrv -Syu
# pacsrv -S openssh

```

## Configurar o Pacman para usar Pacserve

Se você estiver executando o daemon do pacserve e deseja que o pacman use o wrapper, insira a seguinte linha (antes de quaisquer outras linhas `Include`) em **cada** repositório no `/etc/pacman.conf`.

```
Include = /etc/pacman.d/pacserve

```

Aqui está um exemplo para o repositório do Xyne:

 `/etc/pacman.conf` 
```
...
[xyne-x86_64]
SigLevel = Required
**Include  = /etc/pacman.d/pacserve**
Server   = http://xyne.archlinux.ca/repos/xyne
...
```

Alternativamente (para somente espelhos oficiais), você pode inserir a linha `Include` em cima do arquivo *mirrorlist* do Pacman ou deixar o *pacman.conf-insert_pacserve* gerar um arquivo `pacman.conf` para você.

## Solução de problemas

### Problemas se usar baixadores externos no pacman.conf

Se você estiver usando um baixador externo, como o [wget](/index.php/Wget "Wget"), *pacsrv* pode retornar erros ao baixar. Para contornar esses erros, basta colocar entre aspas simples as strings de url e de formatação de saída (`%u` e `%o`):

```
XferCommand = /usr/bin/wget --timeout=6 --passive-ftp -c -O '%o' '%u'

```

## Veja também

*   [tópico do pacserve no fórum do Arch Linux](https://bbs.archlinux.org/viewtopic.php?id=117094)