**Status de tradução:** Esse artigo é uma tradução de [chroot](/index.php/Chroot "Chroot"). Data da última tradução: 2019-11-11\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Chroot&diff=0&oldid=587612) na versão em inglês.

Artigos relacionados

*   [PRoot](/index.php/PRoot_(Portugu%C3%AAs) "PRoot (Português)")
*   [Linux Containers](/index.php/Linux_Containers_(Portugu%C3%AAs) "Linux Containers (Português)")
*   [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn")

[chroot](https://en.wikipedia.org/wiki/pt:Chroot "wikipedia:pt:Chroot") é uma operação que altera o diretório raiz aparente para o processo atual de execução e seus filhos. Um programa que é executado em tal ambiente modificado não consegue acessar os arquivos e comandos fora dessa árvore de diretórios ambiental. Esse ambiente modificado é chamado de um *prisão chroot* (ou *chroot jail*).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Motivação](#Motivação)
*   [2 Requisitos](#Requisitos)
*   [3 Uso](#Uso)
    *   [3.1 Usando arch-chroot](#Usando_arch-chroot)
        *   [3.1.1 Entrar em um chroot](#Entrar_em_um_chroot)
        *   [3.1.2 Executar um único comando e sair](#Executar_um_único_comando_e_sair)
    *   [3.2 Usando chroot](#Usando_chroot)
*   [4 Executar aplicativos gráficos a partir do chroot](#Executar_aplicativos_gráficos_a_partir_do_chroot)
*   [5 Sem privilégios de root](#Sem_privilégios_de_root)
    *   [5.1 PRoot](#PRoot)
    *   [5.2 Fakechroot](#Fakechroot)
*   [6 Veja também](#Veja_também)

## Motivação

Alterar a raiz geralmente é feito para executar a manutenção do sistema em sistemas onde a inicialização e/ou a autenticação não são mais possíveis. Exemplos comuns são:

*   Reinstalação do [gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot").
*   Reconstrução da [imagem de initramfs](/index.php/Mkinitcpio "Mkinitcpio").
*   Atualizar ou [fazer downgrade de pacotes](/index.php/Fazer_downgrade_de_pacote "Fazer downgrade de pacote").
*   Redefinir uma [senha esquecida](/index.php/Recupera%C3%A7%C3%A3o_de_senha "Recuperação de senha").
*   Compilar pacotes em um *chroot* limpo, veja [DeveloperWiki:Building in a clean chroot](/index.php/DeveloperWiki:Building_in_a_clean_chroot "DeveloperWiki:Building in a clean chroot").

Veja também [Wikipedia:Chroot#Limitations](https://en.wikipedia.org/wiki/Chroot#Limitations "wikipedia:Chroot").

## Requisitos

*   Privilégio de *root*.
*   Outro ambiente Linux, como um LiveCD ou mídia flash USB (ex.: pendrive), ou outra distribuição Linux.
*   Ambientes com igual arquitetura; i.e. o chroot de e chroot para. A arquitetura do ambiente atual pode ser descoberta com: `uname -m` (ex.: i686 ou x86_64).
*   Módulos de kernel carregados que são necessários no ambiente chroot.
*   [Swap](/index.php/Swap_(Portugu%C3%AAs) "Swap (Português)") habilitado se necessário: `# swapon /dev/sd*xY*` 
*   Conexão com a Internet estabelecida, se necessário.

## Uso

**Nota:**

*   Algumas ferramentas do [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)"), tal como *hostnamectl*, *localectl* e *timedatectl*, não podem ser usados dentro de um chroot, pois eles exigem uma conexão [dbus](/index.php/Dbus "Dbus") ativa. [[1]](https://github.com/systemd/systemd/issues/798#issuecomment-126568596)
*   O sistema de arquivos que vai servir como uma nova raiz (`/`) de seu chroot deve estar acessível (i.e., descriptografado, montado).

Há duas opções principais para usar chroot, descritas abaixo.

### Usando arch-chroot

O script bash `arch-chroot` é parte do pacote [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts). Antes que ele execute `/usr/bin/chroot`, o script monta sistemas de arquivos de api como `/proc` e torna o `/etc/resolv.conf` disponível no chroot.

#### Entrar em um chroot

Execute *arch-chroot* com o novo diretório raiz como o primeiro argumento:

```
# arch-chroot */local/da/nova/raiz*

```

Por exemplo, no [guia de instalação](/index.php/Guia_de_instala%C3%A7%C3%A3o "Guia de instalação") esse diretório seria o `/mnt`:

```
# arch-chroot /mnt

```

Para sair do chroot, basta usar:

```
# exit

```

#### Executar um único comando e sair

Para executar um comando a partir do chroot e sair novamente, anexe o comando ao final da linha:

```
# arch-chroot */local/da/nova/raiz* *meucomando*

```

Por exemplo, para executar `mkinitcpio -p linux` para um chroot localizado em `/mnt/arch` faça:

```
# arch-chroot /mnt/arch mkinitcpio -p linux

```

### Usando chroot

**Atenção:** Ao usar `--rbind`, alguns subdiretório de `dev/` e `sys/` não serão desmontáveis. Tentar desmontar com `umount -l` nesta situação vai quebrar a sua sessão, exigindo um *reboot*. Se possível, use `-o bind`.

No exemplo a seguir, `/local/da/nova/raiz` é o diretório no qual a nova raiz reside.

Primeiro, monte os sistemas de arquivos de API temporários:

```
# cd */local/da/nova/raiz*
# mount -t proc /proc proc/
# mount --rbind /sys sys/
# mount --rbind /dev dev/

```

E opcionalmente:

```
# mount --rbind /run run/

```

Em seguida, para usar uma conexão com a internet no ambiente *chroot* copie os detalhes do DNS:

```
# cp /etc/resolv.conf etc/resolv.conf

```

Finalmente, para alterar a raiz para `/local/da/nova/raiz` usando um shell do bash:

```
# chroot */local/da/nova/raiz* /bin/bash

```

**Nota:** Se você vir o erro:

*   `chroot: não foi possível executar o comando '/usr/bin/bash': Erro no formato exec`, é provável que as arquiteturas do ambiente hospedeiro e do ambiente *chroot* não sejam iguais.
*   `chroot: '/usr/bin/bash': permissão negada`, remote com a permissão de execução: `mount -o remount,exec */local/da/nova/raiz*`.

Após fazer o *chroot* pode ser necessário carregar a configuração local do bash:

```
# source /etc/profile
# source ~/.bashrc

```

**Dica:** Opcionalmente, crie um prompt único ser possível diferenciar seu ambiente *chroot*: `# export PS1="(chroot) $PS1"` 

Ao finalizar com o *chroot*, você pode sair dele via:

```
# exit

```

Então, desmonte os sistemas de arquivos temporários:

```
# cd /
# umount --recursive */local/da/nova/raiz*

```

**Nota:** Se houver um erro mencionando algo como: `umount: /caminho: dispositivo está ocupado` isso geralmente significa que: um programa (até mesmo um shell) foi mantido em execução no chroot ou que uma submontagem ainda existe. Saia do programa e use `findmnt -R /local/da/nova/raiz` para localizar e então desmontar (com `umount`) as submontagens. Pode ser complicado desmontar algumas coisas e pode-se ter sorte com o `umount --force`. Como um último recurso, use `umount --lazy` para apenas liberá-los. Em ambos casos, para ter segurança, reinicialize (com `reboot`) assim que possível se essas coisas ficarem não resolvidas para evitar possíveis conflitos futuros.

## Executar aplicativos gráficos a partir do chroot

Se você tiver um [servidor X](/index.php/Servidor_X "Servidor X") funcionando em seu sistema, você pode iniciar aplicativos gráficos a partir do ambiente chroot.

Para permitir que o ambiente *chroot* se conecte a um servidor X, abra um terminal virtual dentro do servidor X (i.e. dentro do computador do usuário que está atualmente autenticado), então execute o comando [xhost](/index.php/Xhost_(Portugu%C3%AAs) "Xhost (Português)"), que dá a permissão para qualquer um se conectar ao servidor X do usuário (veja também [Xhost](/index.php/Xhost_(Portugu%C3%AAs) "Xhost (Português)")):

```
$ xhost +local:

```

Então, para direcionar os aplicativos para o servidor X do *chroot*, defina a variável de ambiente DISPLAY dentro do *chroot* para corresponder a variável DISPLAY do usuário que possui o servidor X. Então, por exemplo, execute

```
$ echo $DISPLAY

```

como o usuário que possui o servidor X para ver o valor de DISPLAY. Se o valor for ": 0" (por exemplo), em seguida, no ambiente *chroot* é executado

```
# export DISPLAY=:0

```

## Sem privilégios de root

O *chroot* requer privilégios de root, o que pode não ser desejável ou possível para o usuário obter em determinadas situações. Há, no entanto, várias maneiras de simular o comportamento de *chroot* com implementações alternativas.

### PRoot

[PRoot](/index.php/PRoot_(Portugu%C3%AAs) "PRoot (Português)") pode ser usado para alterar o diretório raiz aparente e usar `mount --bind` sem privilégios de root. Isso é útil para confinar aplicativos para um único diretório ou executar programas criados para uma arquitetura de CPU diferente, mas tem limitações devido ao fato de que todos os arquivos são de propriedade do usuário no sistema hospedeiro. O PRoot fornece um argumento `--root-id` que pode ser usado como uma solução alternativa para algumas dessas limitações de maneira semelhante (embora mais limitada) para *fakeroot*.

### Fakechroot

[fakechroot](https://www.archlinux.org/packages/?name=fakechroot) é uma camada de biblioteca que intercepta a chamada do *chroot* e falsifica os resultados. Ele pode ser usado em conjunto com [fakeroot](https://www.archlinux.org/packages/?name=fakeroot) para simular um *chroot* como usuário comum.

```
# fakechroot fakeroot chroot ~/meu-chroot bash

```

## Veja também

*   [Básico de chroot](https://help.ubuntu.com/community/BasicChroot)