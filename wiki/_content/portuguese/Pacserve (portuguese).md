[Pacserve](http://xyne.archlinux.ca/projects/pacserve/) permite compartilhar facilmente pacotes do *pacman* entre computadores. Isso é muito útil se você tiver uma conexão lenta com a Internet, com várias máquinas funcionando com o Arch Linux.

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
*   [2 Uso autônomo](#Uso_aut.C3.B4nomo)
*   [3 Configurar o Pacman para usar Pacserve](#Configurar_o_Pacman_para_usar_Pacserve)
*   [4 Solução de problemas](#Solu.C3.A7.C3.A3o_de_problemas)
    *   [4.1 Problemas se usar baixadores externos no pacman.conf](#Problemas_se_usar_baixadores_externos_no_pacman.conf)

## Instalação

Você pode instalar o [pacserve](https://aur.archlinux.org/packages/pacserve/) manualmente do [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)") ou de um dos repositórios não oficiais [xyne-any](/index.php/Unofficial_user_repositories#xyne-any "Unofficial user repositories") ou [xyne-x86_64](/index.php/Unofficial_user_repositories#xyne-x86_64 "Unofficial user repositories").

Finalmente, [inicie/habilite](/index.php/Inicie/habilite "Inicie/habilite") `pacserve.service`.

No caso de você usar [iptables](/index.php/Iptables "Iptables"), você provavelmente terá que inciar `pacserve-ports.service` também.

## Uso autônomo

Em vez de pacman, use o wrapper *pacsrv* para executar uma atualização, instalar pacotes e assim por diante. Ele irá baixar automaticamente todos os pacotes da LAN, se alguém os hospedar com o pacserve lá. Caso contrário, basta baixá-los dos espelhos da internet, como geralmente. Por exemplo:

```
# pacsrv -Syu
# pacsrv -S openssh

```

## Configurar o Pacman para usar Pacserve

Se você estiver executando o daemon do pacserve e deseja que o pacman use o wrapper, insira a seguinte linha (antes de quaisquer outras linhas `Include`) em **cada** repositório no /etc/pacman.conf.

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

Alternativamente (para somente espelhos oficiais), você pode inserir a linha `Include` em cima do arquivo *mirrorlist* do Pacman ou deixar o *pacman.conf-insert_pacserve* gerar um arquivo *pacman.conf* para você.

## Solução de problemas

### Problemas se usar baixadores externos no pacman.conf

Se você estiver usando um baixador externo, como o [wget](/index.php/Wget "Wget"), *pacsrv* pode retornar erros ao baixar. Para contornar esses erros, basta colocar entre aspas simples as strings de url e de formatação de saída (`%u` e `%o`):

```
XferCommand = /usr/bin/wget --timeout=6 --passive-ftp -c -O '%o' '%u'

```