**Status de tradução:** Esse artigo é uma tradução de [Pacman/Tips and tricks](/index.php/Pacman/Tips_and_tricks "Pacman/Tips and tricks"). Data da última tradução: 2019-02-02\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Pacman/Tips_and_tricks&diff=0&oldid=565058) na versão em inglês.

Artigos relacionados

*   [Espelhos](/index.php/Espelhos "Espelhos")
*   [Criando pacotes](/index.php/Criando_pacotes "Criando pacotes")

Para métodos gerais para melhorar a flexibilidade das dicas fornecidas ou do *pacman* em si, veja [Utilitários principais](/index.php/Utilit%C3%A1rios_principais "Utilitários principais") e [Bash](/index.php/Bash "Bash").

## Contents

*   [1 Manutenção](#Manutenção)
    *   [1.1 Listando pacotes](#Listando_pacotes)
        *   [1.1.1 Com tamanho](#Com_tamanho)
            *   [1.1.1.1 Pacotes individuais](#Pacotes_individuais)
            *   [1.1.1.2 Pacotes e dependências](#Pacotes_e_dependências)
        *   [1.1.2 Por data](#Por_data)
        *   [1.1.3 Que não estejam em um grupo ou repositório especificado](#Que_não_estejam_em_um_grupo_ou_repositório_especificado)
        *   [1.1.4 Pacotes de desenvolvimento](#Pacotes_de_desenvolvimento)
    *   [1.2 Navegando por pacotes](#Navegando_por_pacotes)
    *   [1.3 Listando arquivos pertencentes a um pacote com tamanho](#Listando_arquivos_pertencentes_a_um_pacote_com_tamanho)
    *   [1.4 Identificar arquivos que pertençam a nenhum pacote](#Identificar_arquivos_que_pertençam_a_nenhum_pacote)
    *   [1.5 Rastreando arquivos sem donos criados criados por pacotes](#Rastreando_arquivos_sem_donos_criados_criados_por_pacotes)
    *   [1.6 Removendo pacotes não usados (órfãos)](#Removendo_pacotes_não_usados_(órfãos))
    *   [1.7 Removendo tudo exceto o grupo base](#Removendo_tudo_exceto_o_grupo_base)
    *   [1.8 Obtendo a lista de dependências de vários pacotes](#Obtendo_a_lista_de_dependências_de_vários_pacotes)
    *   [1.9 Listando arquivos backup modificados](#Listando_arquivos_backup_modificados)
    *   [1.10 Fazer backup da base de dados do pacman](#Fazer_backup_da_base_de_dados_do_pacman)
    *   [1.11 Verificar changelogs facilmente](#Verificar_changelogs_facilmente)
*   [2 Instalação e recuperação](#Instalação_e_recuperação)
    *   [2.1 Instalando pacotes a partir de um CD/DVD ou pendrive](#Instalando_pacotes_a_partir_de_um_CD/DVD_ou_pendrive)
    *   [2.2 Repositório local personalizado](#Repositório_local_personalizado)
    *   [2.3 Cache do pacman compartilhado na rede](#Cache_do_pacman_compartilhado_na_rede)
        *   [2.3.1 Cache de somente leitura](#Cache_de_somente_leitura)
        *   [2.3.2 Cache somente leitura distribuído](#Cache_somente_leitura_distribuído)
        *   [2.3.3 Cache de leitura-escrita](#Cache_de_leitura-escrita)
        *   [2.3.4 Duas vias com rsync](#Duas_vias_com_rsync)
        *   [2.3.5 Cache dinâmico de proxy reverso usando nginx](#Cache_dinâmico_de_proxy_reverso_usando_nginx)
        *   [2.3.6 Sincronizar cache de pacotes do pacman usando programas de sincronização](#Sincronizar_cache_de_pacotes_do_pacman_usando_programas_de_sincronização)
        *   [2.3.7 Prevenção de purgas de cache indesejadas](#Prevenção_de_purgas_de_cache_indesejadas)
    *   [2.4 Recriar um pacote do sistema de arquivos](#Recriar_um_pacote_do_sistema_de_arquivos)
    *   [2.5 Lista de pacotes instalados](#Lista_de_pacotes_instalados)
    *   [2.6 Instalar pacotes de uma lista](#Instalar_pacotes_de_uma_lista)
    *   [2.7 Listando todos os arquivos alterados de pacotes](#Listando_todos_os_arquivos_alterados_de_pacotes)
    *   [2.8 Reinstalando todos pacotes](#Reinstalando_todos_pacotes)
    *   [2.9 Restaurar a base de dados local do pacman](#Restaurar_a_base_de_dados_local_do_pacman)
    *   [2.10 Recuperando um pendrive a partir de uma instalação existente](#Recuperando_um_pendrive_a_partir_de_uma_instalação_existente)
    *   [2.11 Vendo um único arquivo dentro de um arquivo .pkg](#Vendo_um_único_arquivo_dentro_de_um_arquivo_.pkg)
    *   [2.12 Localizar aplicativos que usam bibliotecas de pacotes mais antigos](#Localizar_aplicativos_que_usam_bibliotecas_de_pacotes_mais_antigos)
    *   [2.13 Instalando apenas conteúdo nos idiomas necessários](#Instalando_apenas_conteúdo_nos_idiomas_necessários)
*   [3 Desempenho](#Desempenho)
    *   [3.1 Velocidades de download](#Velocidades_de_download)
        *   [3.1.1 Powerpill](#Powerpill)
        *   [3.1.2 wget](#wget)
        *   [3.1.3 aria2](#aria2)
        *   [3.1.4 Outros aplicativos](#Outros_aplicativos)
*   [4 Utilitários](#Utilitários)
    *   [4.1 Gráficos](#Gráficos)

## Manutenção

**Nota:** Em vez de usar *comm* (que requer entradas ordenadas com *sort*) na seção abaixo, você também pode usar `grep -Fxf` ou `grep -Fxvf`.

Veja também [Manutenção do sistema](/index.php/Manuten%C3%A7%C3%A3o_do_sistema "Manutenção do sistema").

### Listando pacotes

Você pode querer obter a lista de pacotes instalados com sua versão, o que é útil ao relatar erros ou discutir pacotes instalados.

*   Listar todos os pacotes instalados explicitamente: `pacman -Qe`.
*   Listar todos os pacotes no grupo de nome `grupo`: `pacman -Sg grupo`
*   Listar todos pacotes nativos (ou seja, presente na base de dados de sincronização) instalados explicitamente que não são dependências diretas ou opcional: `pacman -Qent`.
*   Listar todos os pacotes externos (geralmente baixados e instalados manualmente ou removidos do repositório): `pacman -Qm`.
*   Listar todos os pacotes nativos (instalados a partir de base(s) de dados de sincronização): `pacman -Qn`.
*   Listar pacotes por expressão regular: `pacman -Qs *regex*`.
*   Listar pacotes por expressão regular com formato de saída personalizada: `expac -s "%-30n %v" *regex*` (precisa de [expac](https://www.archlinux.org/packages/?name=expac)).

#### Com tamanho

Descobrir quais pacotes são maiores pode ser útil ao tentar liberar espaço em seu disco rígido. Existem duas opções aqui: obter o tamanho de pacotes individuais ou obter o tamanho dos pacotes e suas dependências.

##### Pacotes individuais

O comando a seguir listará todos os pacotes instalados e seus tamanhos individuais:

```
$ pacman -Qi | awk '/^Name/{name=$3} /^Installed Size/{print $4$5, name}' | sort -h

```

##### Pacotes e dependências

Para listar tamanhos com suas dependências,

*   Instale [expac](https://www.archlinux.org/packages/?name=expac) e execute `expac -H M '%m\t%n' | sort -h`.
*   Execute [pacgraph](https://www.archlinux.org/packages/?name=pacgraph) com a opção `-c`.

Para listas o tamanho baixado de vários pacotes (deixe `*pacotes*` em branco para listar todos os pacotes):

```
$ expac -S -H M '%k\t%n' *pacotes*

```

Para listar pacotes instalados explicitamente que não estejam em [base](https://www.archlinux.org/groups/x86_64/base/) nem [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) com tamanho e descrição:

```
$ expac -H M "%011m\t%-20n\t%10d" $(comm -23 <(pacman -Qqen | sort) <(pacman -Qqg base base-devel | sort)) | sort -n

```

Para listar os pacotes marcados para atualização com seu tamanho de download

```
$ pacman -Quq|xargs expac -S -H M '%k\t%n' | sort -sh

```

#### Por data

Para listar os últimos 20 pacotes instalados com [expac](https://www.archlinux.org/packages/?name=expac), execute:

```
$ expac --timefmt='%Y-%m-%d %T' '%l\t%n' | sort | tail -n 20

```

ou com segundos desde o *epoch* (1970-01-01 UTC):

```
$ expac --timefmt=%s '%l\t%n' | sort -n | tail -n 20

```

#### Que não estejam em um grupo ou repositório especificado

**Nota:** Para obter uma lista de pacotes instalados como dependências, mas não mais exigidos para qualquer pacote instalado, veja [#Removendo pacotes não usados (órfãos)](#Removendo_pacotes_não_usados_(órfãos)).

Listar explicitamente os pacotes instalados explicitamente que não estejam no grupo [base](https://www.archlinux.org/groups/x86_64/base/) nem no [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/):

```
$ comm -23 <(pacman -Qeq | sort) <(pacman -Qgq base base-devel | sort)

```

Listar todos os pacotes instalados não necessários para outros pacotes, e que não estejam no grupo [base](https://www.archlinux.org/groups/x86_64/base/) nem no [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/):

```
$ comm -23 <(pacman -Qqt | sort) <(pacman -Sqg base base-devel | sort)

```

Mesmo que o acima, mas com descrições:

```
$ expac -HM '%-20n\t%10d' $(comm -23 <(pacman -Qqt | sort) <(pacman -Qqg base base-devel | sort))

```

Listar todos os pacotes instalados que *não* estão no repositório especificado *nome_repo*

```
$ comm -23 <(pacman -Qq | sort) <(pacman -Slq *nome_repo* | sort)

```

Listar todos os pacotes instalados que estão no repositório *nome_repo*:

```
$ comm -12 <(pacman -Qq | sort) <(pacman -Slq *nome_repo* | sort)

```

Listar todos os pacotes na ISO do Arch Linux que não estão no grupo base:

```
$ comm -23 <(curl https://git.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) <(pacman -Qqg base | sort)

```

#### Pacotes de desenvolvimento

Para listar todos os pacotes de desenvolvimento/instáveis, execute:

```
 $ pacman -Qq | grep -Ee '-(bzr|cvs|darcs|git|hg|svn)$'

```

### Navegando por pacotes

Para navegador por todos os pacotes instalados com uma visualização instantânea de cada pacote:

```
 $ pacman -Qq | fzf --preview 'pacman -Qil {}' --layout=reverse --bind 'enter:execute(pacman -Qil {} | less)'

```

Isso usa [fzf](/index.php/Fzf "Fzf") para apresentar uma visão de dois painéis listando todos os pacotes com informações de pacotes mostradas na direita.

Insira letras para filtrar a lista de pacotes; use teclas de setas (ou `Ctrl-j`/`Ctrl-k`) para navegar; pressione `Enter` para ver informações de pacote sob *less*.

### Listando arquivos pertencentes a um pacote com tamanho

Este pode ser útil se você descobriu que um pacote específico usa uma enorme quantidade de espaço e você quer descobrir quais arquivos usam mais desse espaço.

```
$ pacman -Qlq *pacote* | grep -v '/$' | xargs du -h | sort -h

```

### Identificar arquivos que pertençam a nenhum pacote

Se seu arquivo possui arquivos não pertencentes a qualquer pacote (um caso comum se você não [usa o gerenciador de pacotes para instalar softwares](/index.php/Manuten%C3%A7%C3%A3o_do_sistema#Use_o_gerenciador_de_pacotes_para_instalar_softwares "Manutenção do sistema")), você pode querer descobrir quais são esses arquivos para limpá-los. O processo geral para fazer isso:

Um método é usar `# pacreport --unowned-files` do [pacutils](https://www.archlinux.org/packages/?name=pacutils), o qual vai listar arquivos sem dono entre outros detalhes.

Outro é listar todos os arquivos de seu interesse e verificá-los com o pacman:

```
# find /etc /usr /opt /var | LC_ALL=C pacman -Qqo - 2>&1 > /dev/null | cut -d ' ' -f 5-

```

**Dica:** O script [lostfiles](https://www.archlinux.org/packages/?name=lostfiles) realizar etapas similares, mas também inclui uma lista negra extensa para remover falso-positivos comuns da saída. [aconfmgr](https://github.com/CyberShadow/aconfmgr) ([aconfmgr-git](https://aur.archlinux.org/packages/aconfmgr-git/)) permite rastrear arquivos órfãos usando um script de configuração.

### Rastreando arquivos sem donos criados criados por pacotes

A maioria dos sistemas vão aos poucos coletando diversos arquivos [fantasmas](http://ftp.rpm.org/max-rpm/s1-rpm-inside-files-list-directives.html#S3-RPM-INSIDE-FLIST-GHOST-DIRECTIVE) tal como arquivos de estado, logs, índices, etc. pelo curso de operação comum.

`pacreport` do [pacutils](https://www.archlinux.org/packages/?name=pacutils) pode ser usado para rastrear esses arquivos e suas associações via `/etc/pacreport.conf` (veja [pacreport(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacreport.1#FILES)).

Um exemplo pode se parecer com algo como isso (resumido):

 `/etc/pacreport.conf` 
```
[Options]
IgnoreUnowned = usr/share/applications/mimeinfo.cache

[PkgIgnoreUnowned]
alsa-utils = var/lib/alsa/asound.state
bluez = var/lib/bluetooth
ca-certificates = etc/ca-certificates/trust-source/*
dbus = var/lib/dbus/machine-id
glibc = etc/ld.so.cache
grub = boot/grub/*
linux = boot/initramfs-linux.img
pacman = var/lib/pacman/local
update-mime-database = usr/share/mime/magic

```

Então, ao usar `# pacreport --unowned-files`, todos os arquivos sem dono serão listados se o pacote associado não estiver mais instalado (ou se algum arquivo novo tiver sido criado).

Adicionalmente, [aconfmgr](https://github.com/CyberShadow/aconfmgr) ([aconfmgr-git](https://aur.archlinux.org/packages/aconfmgr-git/)) permite rastrear arquivos modificados e órfãos usando um script de configuração.

### Removendo pacotes não usados (órfãos)

Para remover recursivamente ófãos e seus arquivos de configuração:

```
# pacman -Rns $(pacman -Qtdq)

```

Se nenhum órfão for encontrado, o *pacman* emite `erro: nenhum alvo especificado`. É esperado que nenhum tenha sido passado para `pacman -Rns`.

**Nota:** Os argumentos `-Qt` listam somente verdadeiros órfãos. Para incluir pacotes que são *opcionalmente* exigidos por outro pacote, passe a opção `-t` duas vezes, ou seja, `-Qtt`.

### Removendo tudo exceto o grupo base

Se for necessário remover todos os pacotes, exceto o grupo base, experimente esta linha (exige [pacman-contrib](https://www.archlinux.org/packages/?name=pacman-contrib)):

```
# pacman -R $(comm -23 <(pacman -Qq | sort) <((for i in $(pacman -Qqg base); do pactree -ul "$i"; done) | sort -u))

```

Essa linha foi originalmente aconselhada [nesta discussão](https://bbs.archlinux.org/viewtopic.php?id=130176) e posteriormente melhorada neste artigo.

### Obtendo a lista de dependências de vários pacotes

As dependências são ordenadas alfabeticamente e as duplas são removidas.

**Nota:** Para só mostrar a árvore de pacotes instalados, use `pacman -Qi`.

```
$ pacman -Si *pacotes* | awk -F'[:<=>]' '/^Depends/ {print $2}' | xargs -n1 | sort -u

```

Alternativamente, com [expac](https://www.archlinux.org/packages/?name=expac):

```
$ expac -l '
' %E -S *pacotes* | sort -u

```

### Listando arquivos backup modificados

Se você quiser fazer backup dos arquivos de configuração do seu sistema, você pode copiar todos os arquivos em `/etc/`, mas normalmente você só estaria interessado nos arquivos que você alterou. Os [arquivos backup](/index.php/Arquivos_Pacnew_e_Pacsave#Arquivos_backup_do_pacote "Arquivos Pacnew e Pacsave") modificados podem ser vistos com o seguinte comando:

```
# pacman -Qii | awk '/^MODIFIED/ {print $2}'

```

Executar esse comando com permissões de *root* vai garantir que os arquivos legíveis apenas pelo *root* (como o `/etc/sudoers`) sejam incluídos na saída.

**Dica:** Veja [#Listando todos os arquivos alterados de pacotes](#Listando_todos_os_arquivos_alterados_de_pacotes) para listar os arquivos alterados que o *pacman* conhece, e não apenas arquivos backup.

### Fazer backup da base de dados do pacman

O seguinte comando pode ser usado para fazer backup da base de dados local do *pacman*:

```
$ tar -cjf pacman_database.tar.bz2 /var/lib/pacman/local

```

Armazene o arquivo de base de dados backup do *pacman* em uma ou mais mídias offline, tal como um pendrive, disco rígido externo ou um CD-R.

A base de dados pode ser restaurada movendo o arquivo `pacman_database.tar.bz2` para o diretório `/` e execução o comando a seguir:

```
# tar -xjvf pacman_database.tar.bz2

```

**Nota:** Se os arquivos de base de dados do *pacman* estiverem corrompidos e não houver um arquivo backup disponível, há alguma esperança de recompilar a base de dados do *pacman*. Consulte [#Restaurar a base de dados local do pacman](#Restaurar_a_base_de_dados_local_do_pacman).

**Dica:** O pacote [pakbak-git](https://aur.archlinux.org/packages/pakbak-git/) fornece um script e um serviço [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") para automatizar a tarefa. A configuração é possível em `/etc/pakbak.conf`.

### Verificar changelogs facilmente

Quando os mantenedores atualizam os pacotes, os commits geralmente são comentados de forma útil. Os usuários podem verificá-los rapidamente a partir da linha de comando instalando [pacolog](https://aur.archlinux.org/packages/pacolog/). Este utilitário lista mensagens de commit recentes para pacotes dos repositórios oficiais ou do AUR, usando `pacolog <pacote>`.

## Instalação e recuperação

Meios alternativos de obter e restaurar pacotes.

### Instalando pacotes a partir de um CD/DVD ou pendrive

Para baixar pacotes ou grupos de pacotes:

```
# cd ~/Packages
# pacman -Syw base base-devel grub-bios xorg gimp --cachedir .
# repo-add ./custom.db.tar.gz ./*

```

Então, você pode gravar a pasta "Packages" para um CD/DVD ou transferi-la para um pendrive, HDD externo, etc.

Para instalar:

**1.** Monte a mídia:

```
# mkdir /mnt/repo
# mount /dev/sr0 /mnt/repo    #Para um CD/DVD.
# mount /dev/sdxY /mnt/repo   #Para um pendrive.

```

**2.** Edite `pacman.conf` e adicione esse repositório *antes* dos outros (ex.: extra, core, etc.). Isso é importante. Não apenas descomente aquele na parte de baixo. Essa forma garante que os arquivos do CD/DVD/pendrive tenham precedência sobre aqueles nos repositórios padrões:

 `/etc/pacman.conf` 
```
[custom]
SigLevel = PackageRequired
Server = file:///mnt/repo/Packages
```

**3.** Finalmente, sincronize a base de dados do *pacman* para habilitar o uso do novo repositório:

```
# pacman -Syu

```

### Repositório local personalizado

Use o script *repo-add*, incluído no *pacman*, para gerar uma base de dados para um repositório pessoal. Use `repo-add --help` para obter mais detalhes sobre seu uso. Para adicionar um novo pacote à base de dados, ou para substituir a versão antiga de um pacote existente na base de dados, execute:

```
$ repo-add */caminho/para/repo.db.tar.gz /caminho/para/pacote-1.0-1-x86_64.pkg.tar.xz*

```

**Nota:** Uma base de dados de pacote é um arquivo tar, opcionalmente comprimida. Extensões válidas são *.db* ou *.files* seguido por uma extensão de arquivamento de *.tar*, *.tar.gz*, *.tar.bz2*, *.tar.xz* ou*.tar.Z*. O arquivo não precisa existir, mas todos os diretórios pais devem existir.

A base de dados e os pacotes não precisam estar no diretório ao usar *repo-add*, mas tenha em mente que ao usar *pacman* com aquela base de dados, eles devem estar juntos. Armazenar todos os pacotes compilados para serem incluídos no repositório em um diretório também permite usar a expansão shell glob para adicionar ou atualizar vários pacotes ao mesmo tempo.

```
$ repo-add */caminho/para/repo.db.tar.gz /caminho/para/*.pkg.tar.xz*

```

**Atenção:** *repo-add* adiciona as entradas na base de dados na mesma ordem que foi passada na linha de comando. Se várias versões do mesmo pacote estiverem envolvidas, deve-se ter cuidado para garantir que a versão correta seja adicionada por último. Em particular, observe que a ordem lexical usada pelo shell depende do locale e difere do pedido de [vercmp](https://www.archlinux.org/pacman/vercmp.8.html) usado pelo *pacman*.

*repo-remove* é usado para remover pacotes da base de dados de pacotes, exceto que somente nomes de pacotes são especificados na linha de comando.

```
$ repo-remove */caminho/para/repo.db.tar.gz pkgname*

```

Uma vez que a base de dados local do repositório tenha sido criado, adicione o repositório a `pacman.conf` para cada sistema que seja para usar o repositório. Um exemplo de um repositório personalizado está em `pacman.conf`. O nome do repositório é o nome do arquivo da base de dados com a extensão do arquivo omitida. No caso do exemplo acima, o nome do repositório simplesmente seria *repo*. Consulte a localização do repositório usando um URL `file://`, ou via FTP usando o diretório [ftp://localhost/caminho/para/diretório](ftp://localhost/caminho/para/diretório).

Se quiser, adicione um repositório personalizado à [lista de repositórios de usuário não oficiais](/index.php/Unofficial_user_repositories "Unofficial user repositories"), de forma que a comunidade possa se beneficiar dele.

### Cache do pacman compartilhado na rede

Se você tiver várias máquinas com Arch na sua rede local, você pode compartilhar pacotes para que você possa diminuir significativamente os tempos de download. Tenha em mente que você não deve compartilhar entre arquiteturas diferentes (isto é, i686 e x86_64) ou você terá problemas.

#### Cache de somente leitura

Se você está procurando uma solução rápida, você pode simplesmente executar um servidor web autônomo que outros computadores possam usar como um primeiro espelho:

```
# ln -s /var/lib/pacman/sync/*.db /var/cache/pacman/pkg
$ sudo -u http darkhttpd /var/cache/pacman/pkg --no-server-id

```

Você também poderia executar darkhttpd como um serviço systemd por conveniência. Basta adicionar esse servidor no topo de seu `/etc/pacman.d/mirrorlist` em máquinas clientes com `Server = http://meuespelho:8080`. Certifique-se de manter seu espelho atualizado.

Se você já está executando um servidor web para alguma outra finalidade, você pode querer reutilizá-lo como seu servidor de repo local em vez de darkhttpd. Por exemplo, digamos que você já atende um site com [nginx](/index.php/Nginx "Nginx"), você pode adicionar um bloco de servidor nginx na porta 8080:

 `/etc/nginx/nginx.conf` 
```
http {
    # ... outras configs de servidor nginx aqui

    server {
        listen 8080;
        root /var/cache/pacman/pkg;
        server_name myarchrepo.localdomain;
        try_files $uri $uri/;
    }
}

```

Lembre-se de reiniciar o nginx após fazer essa alteração.

Seja qual for o servidor web que você usa, lembre-se de abrir a porta 8080 para o tráfego local (e provavelmente você quer negar qualquer coisa que não seja local), então adicione uma regra como a seguinte para [iptables](/index.php/Iptables "Iptables"):

 `/etc/iptables/iptables.rules` 
```
-A TCP -s 192.168.0.0/16 -p tcp -m tcp --dport 8080 -j ACCEPT

```

Lembre-se de reiniciar o iptables após fazer essa alteração.

#### Cache somente leitura distribuído

Existem ferramentas específicas do Arch para descobrir automaticamente outros computadores em sua rede oferecendo um cache de pacote. Tente [pacredir](https://www.archlinux.org/packages/?name=pacredir), [pacserve](/index.php/Pacserve_(Portugu%C3%AAs) "Pacserve (Português)"), [pkgdistcache](https://aur.archlinux.org/packages/pkgdistcache/) ou [paclan](https://aur.archlinux.org/packages/paclan/). O pkgdistcache usa Avahi em vez de UDP simples, que pode funcionar melhor em determinadas redes domésticas que roteiam em vez de ponte entre WiFi e Ethernet.

Historicamente, havia [PkgD](https://bbs.archlinux.org/viewtopic.php?id=64391) e [multipkg](https://github.com/toofishes/multipkg), mas eles não são mais mantidos.

#### Cache de leitura-escrita

Para compartilhar pacotes entre vários computadores, simplesmente compartilhe `/var/cache/pacman/` usando qualquer protocolo de montagem em rede. Esta seção mostra como usar [shfs](/index.php/Shfs "Shfs") ou [SSHFS](/index.php/SSHFS "SSHFS") para compartilhar um cache de pacotes mais os diretórios de biblioteca relacionados entre vários computadores na mesma rede local. Tenha em mente que um cache compartilhado em rede pode ser lento dependendo da escolha do sistema de arquivos, entre outros fatores.

Primeiro, instale qualquer sistema de arquivos que tenha suporte a rede: [shfs-utils](https://www.archlinux.org/packages/?name=shfs-utils), [sshfs](https://www.archlinux.org/packages/?name=sshfs), [curlftpfs](https://www.archlinux.org/packages/?name=curlftpfs), [samba](https://www.archlinux.org/packages/?name=samba) ou [nfs-utils](https://www.archlinux.org/packages/?name=nfs-utils).

**Dica:**

*   Para usar *sshfs* ou *shfs*, considere ler [Using SSH Keys](/index.php/Using_SSH_Keys "Using SSH Keys").
*   Por padrão, *smbfs* não fornece nomes de arquivos que contenham dois pontos, o que resulta no cliente baixar o pacote problemática novamente. Para evitar isso, use a opção de montagem `mapchars` no cliente.

Então, para compartilhar os pacotes, monte `/var/cache/pacman/pkg` do servidor em `/var/cache/pacman/pkg` para toda máquina cliente.

**Atenção:** Não torne `/var/cache/pacman/pkg` ou qualquer um de seus antecessores (ex., `/var`) um link simbólico. *Pacman* espera que esses sejam diretórios. Quando o *pacman* reinstala ou atualiza a si próprio, ele vai remover os links simbólicos e vai criar diretórios vazios no lugar. Porém, durante a transação, o *pacman* depende de alguns pacotes estarem lá, resultando em quebrar o processo de atualização. Veja [FS#50298](https://bugs.archlinux.org/task/50298) para mais detalhes.

#### Duas vias com rsync

Outra abordagem em um ambiente local é [rsync](/index.php/Rsync "Rsync"). Escolha um servidor para armazenamento em cache e ative o [Rsync#rsync daemon](/index.php/Rsync#rsync_daemon "Rsync"). Nos clientes, sincronize em duas vias com este compartilhamento via protocolo rsync. Os nomes dos arquivos que contêm dois pontos não são um problema para o protocolo rsync.

Um exemplo de rascunho para um cliente, usando `uname -m` dentro de nome de compartilhamento garante uma sincronização dependente da arquitetura:

```
 # rsync rsync://servidor/share_$(uname -m)/ /var/cache/pacman/pkg/ ...
 # pacman ...
 # paccache ...
 # rsync /var/cache/pacman/pkg/ rsync://servidor/share_$(uname -m)/  ...

```

#### Cache dinâmico de proxy reverso usando nginx

[nginx](/index.php/Nginx "Nginx") pode ser usado para solicitações de proxy para espelhos oficiais de *upstream* e armazenar em cache os resultados para o disco local. Todas as solicitações subsequentes para esse arquivo serão atendidas diretamente do cache local, minimizando a quantidade de tráfego de internet necessária para atualizar um grande número de servidores com um esforço mínimo.

**Atenção:** Este método tem uma limitação. Você deve usar espelhos que usam o mesmo caminho relativo para o pacote de arquivos e você deve configurar seu cache para usar esse mesmo caminho. Neste exemplo, estamos usando espelhos que usam o caminho relativo `/archlinux/$repo/os/$arch` e a definição `Server` do nosso cache no `mirrorlist` está configurada similarmente.

Neste exemplo, vamos executar o servidor de cache em `http://cache.domain.example:8080/` e armazenar os pacotes em `/srv/http/pacman-cache/`.

Crie o diretório para o cache e ajuste as permissões de forma que o nginx possa escrever os arquivos para ele:

```
 # mkdir /srv/http/pacman-cache
 # chown http:http /srv/http/pacman-cache

```

Em seguida, configure o nginx como o [cache dinâmico](https://gist.github.com/anonymous/97ec4148f643de925e433bed3dc7ee7d) (leia os comentários para uma explicação dos comandos).

Finalmente, atualize seus outros servidores Arch Linux para usar esse novo cache adicionando a seguinte linha ao arquivo `mirrorlist`:

 `/etc/pacman.d/mirrorlist` 
```
Server = http://cache.domain.example:8080/archlinux/$repo/os/$arch
...

```

**Nota:** Você precisará criar um método para limpar pacotes antigos, pois esse diretório continuará a crescer ao longo do tempo. `paccache` (que é fornecido por [pacman-contrib](https://www.archlinux.org/packages/?name=pacman-contrib)) pode ser usado para automatizar isso usando os critérios de retenção de sua escolha. Por exemplo, `find /srv/http/pacman-cache/ -type d -exec paccache -v -r -k 2 -c {} \;` manterá as últimas 2 versões de pacotes no seu diretório de cache.

#### Sincronizar cache de pacotes do pacman usando programas de sincronização

Use [Syncthing](/index.php/Syncthing "Syncthing") ou [Resilio Sync](/index.php/Resilio_Sync "Resilio Sync") para sincronizar as pastas de cache do *pacman* (ou seja, `/var/cache/pacman/pkg`).

#### Prevenção de purgas de cache indesejadas

Por padrão, `pacman -Sc` remove tarballs de pacotes do cache que correspondem a pacotes que não estão instalados na máquina em que o comando foi emitido. Porque o *pacman* não pode prever quais pacotes estão instalados em todas as máquinas que compartilham o cache, ele acabará excluindo arquivos que não deveriam ser excluídos.

Para limpar o cache de forma que apenas tarballs *desatualizados* seja excluídos, adicione essa entrada na seção `[options]` do `/etc/pacman.conf`:

```
CleanMethod = KeepCurrent

```

### Recriar um pacote do sistema de arquivos

Para recriar um pacote do sistema de arquivos, use [fakepkg](https://aur.archlinux.org/packages/fakepkg/). Os arquivos do sistema são aceitos como estão, portanto, quaisquer modificações estarão presentes no pacote montado. Distribuir o pacote recriado é, portanto, desencorajado; veja [ABS](/index.php/ABS_(Portugu%C3%AAs) "ABS (Português)") e [Arch Linux Archive (Português)](/index.php/Arch_Linux_Archive_(Portugu%C3%AAs) "Arch Linux Archive (Português)") para obter alternativas.

### Lista de pacotes instalados

Manter uma lista de todos os pacotes instalados explicitamente pode ser útil para, por exemplo, servidor de backup de um sistema ou acelerar a instalação em um novo sistema:

```
$ pacman -Qqe > pkglist.txt

```

**Nota:**

*   Com a opção `-t`, os pacotes já necessários para outros pacotes explicitamente instalados não são mencionados. Se estiver reinstalando a partir desta lista, eles serão instalados, mas apenas como dependências.
*   Com uma opção `-n`, pacotes externos (p. ex., do [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)")) são omitidos da lista.
*   Use `comm -13 <(pacman -Qqdt | sort) <(pacman -Qqdtt | sort) > optdeplist.txt` para também criar uma lista das dependências opcionais instaladas que pode ser reinstalada com `--asdeps`.
*   Use `pacman -Qqem > foreignpkglist.txt` para criar a lista de AUR e outros pacotes externos que foram explicitamente instalados.

Para manter uma lista atualizada de pacotes explicitamente instalados (p. ex., em combinação com um `/etc/` versionado), você pode configurar um [hook](/index.php/Pacman_(Portugu%C3%AAs)#Hooks "Pacman (Português)"). Exemplo:

```
[Trigger]
Operation = Install
Operation = Remove
Type = Package
Target = *

[Action]
When = PostTransaction
Exec = /bin/sh -c '/usr/bin/pacman -Qqe > /etc/pkglist.txt'

```

### Instalar pacotes de uma lista

Para instalar pacotes de uma lista salva anteriormente de pacotes, sem reinstalar pacotes já instalados que já estão atualizados, execute:

```
# pacman -S --needed - < pkglist.txt

```

No entanto, é provável que pacotes externos, como os do AUR ou instalados localmente, estejam presentes na lista. Para filtrar da lista os pacotes externos, a linha de comandos anterior pode ser enriquecida da seguinte forma:

```
 # pacman -S --needed $(comm -12 <(pacman -Slq | sort) <(sort pkglist.txt))

```

Eventualmente, para garantir que os pacotes instalados do seu sistema correspondam à lista e remova todos os pacotes que não são mencionados nela:

```
# pacman -Rsu $(comm -23 <(pacman -Qq | sort) <(sort pkglist.txt))

```

**Dica:** Essas tarefas podem ser automatizadas. Veja [bacpac](https://aur.archlinux.org/packages/bacpac/), [packup](https://aur.archlinux.org/packages/packup/), [pacmanity](https://aur.archlinux.org/packages/pacmanity/) e [pug](https://aur.archlinux.org/packages/pug/) para exemplos.

### Listando todos os arquivos alterados de pacotes

Se você suspeitar de corrompimento de arquivos (por exemplo, por falha de software/hardware), mas não tem certeza se os arquivos foram corrompidos, você pode querer comparar com as somas de hash nos pacotes. Isso pode ser feito com [pacutils](https://www.archlinux.org/packages/?name=pacutils):

```
# paccheck --md5sum --quiet

```

Para recuperação da base de dados, veja [#Restaurar a base de dados local do pacman](#Restaurar_a_base_de_dados_local_do_pacman). Os arquivos `mtree` também pode ser [extraído como `.MTREE` a partir dos respectivos arquivos de pacote](#Vendo_um_único_arquivo_dentro_de_um_arquivo_.pkg).

**Nota:** Isso **não** deve ser usado assim quando se suspeita de mudanças maliciosas! Neste caso, são recomendadas precauções de segurança, como o uso de uma mídia *Live* e uma fonte independente para as somas de hash.

### Reinstalando todos pacotes

Para reinstalar todos os pacotes nativos, use:

```
# pacman -Qqn | pacman -S -

```

Pacotes externos (do AUR) devem ser reinstalados separadamente; você pode listá-los com `pacman -Qqm`.

*Pacman* preserva o [motivo de instalação](/index.php/Motivo_de_instala%C3%A7%C3%A3o "Motivo de instalação") por padrão.

### Restaurar a base de dados local do pacman

Veja [Pacman/Restaurar base de dados local](/index.php/Pacman/Restaurar_base_de_dados_local "Pacman/Restaurar base de dados local").

### Recuperando um pendrive a partir de uma instalação existente

Se você possui o Arch instalado em um pendrive e conseguir arruiná-lo (por exemplo, removê-lo enquanto ainda está sendo gravado), é possível reinstalar todos os pacotes e, com esperança, recuperá-lo e trabalhar novamente (presumindo que o pendrive esteja montado em `/novoarch`)

```
# pacman -S $(pacman -Qq --dbpath /novoarch/var/lib/pacman) --root /novoarch --dbpath /novoarch/var/lib/pacman

```

### Vendo um único arquivo dentro de um arquivo .pkg

Por exemplo, se você deseja ver o conteúdo de `/etc/systemd/logind.conf` fornecido no pacote [systemd](https://www.archlinux.org/packages/?name=systemd):

```
$ bsdtar -xOf /var/cache/pacman/pkg/systemd-204-3-x86_64.pkg.tar.xz etc/systemd/logind.conf

```

Ou você pode usar [vim](https://www.archlinux.org/packages/?name=vim) para navegar no pacote:

```
$ vim /var/cache/pacman/pkg/systemd-204-3-x86_64.pkg.tar.xz

```

### Localizar aplicativos que usam bibliotecas de pacotes mais antigos

Mesmo se você instalou um pacote, os programas existentes de longa duração (como daemons e servidores) continuam usando código de bibliotecas de pacotes antigos. E é uma má ideia deixar esses programas em execução se a biblioteca antiga contiver um erro de segurança.

Aqui está uma maneira de encontrar todos os programas que usam código de pacotes antigo:

```
# lsof +c 0 | grep -w DEL | awk '1 { print $1 ": " $NF }' | sort -u

```

Ele imprimirá o nome do programa em execução e a biblioteca antiga que foi removida ou substituída por conteúdo mais novo.

### Instalando apenas conteúdo nos idiomas necessários

Muitos pacotes tentam instalar documentação e traduções em vários idiomas. Alguns programas são projetados para remover esses arquivos desnecessários, como [localepurge](https://aur.archlinux.org/packages/localepurge/), que é executado após a instalação de um pacote para excluir os arquivos de localidade desnecessários. Uma abordagem mais direta é fornecida através da diretiva `NoExtract` em `pacman.conf`, que impede que esses arquivos sejam instalados. O exemplo abaixo instala arquivos em inglês (EUA) ou nenhum:

 `/etc/pacman.conf` 
```
NoExtract = usr/share/help/* !usr/share/help/en*
NoExtract = usr/share/gtk-doc/html/*
NoExtract = usr/share/locale/* usr/share/X11/locale/* usr/share/i18n/* opt/google/chrome/locales/*
NoExtract = !*locale*/en*/* !usr/share/i18n/charmaps/UTF-8.gz !usr/share/*locale*/locale.*
NoExtract = !usr/share/*locales/en_?? !usr/share/*locales/i18n !usr/share/*locales/iso*
NoExtract = !usr/share/*locales/trans*
NoExtract = usr/share/qt4/translations/*
NoExtract = usr/share/man/* !usr/share/man/man*
NoExtract = usr/share/vim/vim*/lang/*
NoExtract = usr/lib/libreoffice/help/en-US/*
```

Alguns usuários notaram que remover localidades resultou em [consequências não planejadas](https://wiki.archlinux.org/index.php?title=Talk:Pacman&oldid=460285#Dangerous_NoExtract_example).

## Desempenho

### Velocidades de download

**Nota:** Se suas velocidades de download foram reduzidas a uma lesma, certifique-se de usar um dos muitos [espelhos](/index.php/Espelhos "Espelhos") e não o ftp.archlinux.org, cuja [velocidade é limitada desde março de 2007](https://www.archlinux.org/news/302/).

Ao baixar pacotes, o *pacman* usa os espelhos na ordem em que estão no `/etc/pacman.d/mirrorlist`. O espelho que está no topo da lista por padrão, no entanto, pode não ser o mais rápido para você. Para selecionar um espelho mais rápido, veja [Espelhos](/index.php/Espelhos "Espelhos").

A velocidade do *pacman* ao baixar pacotes também pode ser melhorada usando um aplicativo diferente para baixar pacotes, em vez baixador de arquivos embutido do *pacman*.

Em todos os casos, certifique-se de ter o *pacman* mais recente antes de fazer quaisquer modificações.

```
# pacman -Syu

```

#### Powerpill

[Powerpill](/index.php/Powerpill_(Portugu%C3%AAs) "Powerpill (Português)") é um wrapper do *pacman* que faz uso de download paralelo e segmentado para tentar acelerar os downloads para o *pacman*.

#### wget

Esse também é muito útil se você precisar de configurações de proxy mais poderosas que as capacidades incorporadas no *pacman*.

Para usar o `wget`, primeiro [instale](/index.php/Instale "Instale") o pacote [wget](https://www.archlinux.org/packages/?name=wget) e, após, modifique o `/etc/pacman.conf` descomentando a seguinte linha na seção `[options]`:

```
XferCommand = /usr/bin/wget --passive-ftp -c -O %o %u

```

Em vez de descomentar os parâmetros de `wget` no `/etc/pacman.conf`, você também pode modificar o arquivo de configuração do `wget` diretamente (o arquivo de todo o sistema é `/etc/wgetrc`, enquanto arquivos por usuário são `$HOME/.wgetrc`.

#### aria2

O [aria2](/index.php/Aria2 "Aria2") é um utilitário de download leve com suporte a downloads resumíveis e segmentados via HTTP/HTTPS e FTP. O aria2 permite conexões múltiplas e simultâneas de HTTP/HTTPS e FTP para um espelho do Arch, o que deve resultar em um aumento na velocidade de download para a obtenção de arquivos e pacotes.

**Nota:** O uso do aria2c no XferCommand do *pacman* **não** vai resultar em downloads paralelos de múltiplos pacotes. O *pacman* chama o XferCommand com um único pacote por vez e aguarda por ele concluir antes de chamar o próximo. Para baixar múltiplos pacotes em paralelo, veja [Powerpill](/index.php/Powerpill_(Portugu%C3%AAs) "Powerpill (Português)").

Instale o [aria2](https://www.archlinux.org/packages/?name=aria2) e, após, edite o `/etc/pacman.conf` adicionando a seguinte linha à seção `[options]`:

```
XferCommand = /usr/bin/aria2c --allow-overwrite=true --continue=true --file-allocation=none --log-level=error --max-tries=2 --max-connection-per-server=2 --max-file-not-found=5 --min-split-size=5M --no-conf --remote-time=true --summary-interval=60 --timeout=5 --dir=/ --out %o %u

```

**Dica:** [Essa configuração alternativa para usar o *pacman* com aria2](https://bbs.archlinux.org/viewtopic.php?pid=1491879#p1491879) tenta simplificar a configuração e adiciona mais opções de configuração.

Veja [OPTIONS](http://aria2.sourceforge.net/manual/en/html/aria2c.html#options) em [aria2c(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/aria2c.1) para opções do aria2c usadas.

*   `-d, --dir`: O diretório para armazenar o arquivos baixados, conforme especificado pelo *pacman*.
*   `-o, --out`: Os nomes de arquivo dos arquivos baixados.
*   `%o`: A variável que representa os nomes de arquivos locais, conforme especificado pelo *pacman*.
*   `%u`: A variável que representa a URL de download, conforme especificado pelo *pacman*.

#### Outros aplicativos

Existem outros aplicativos de download que você pode usar com *pacman*. Aqui estão, e as configurações associadas de XferCommand:

*   `snarf`: `XferCommand = /usr/bin/snarf -N %u`
*   `lftp`: `XferCommand = /usr/bin/lftp -c pget %u`
*   `axel`: `XferCommand = /usr/bin/axel -n 2 -v -a -o %o %u`
*   `hget`: `XferCommand = /usr/bin/hget %u -n 2 -skip-tls false` (por favor, leia a [documentação na página de projeto no Github](https://github.com/huydx/hget) para mais informações)

## Utilitários

*   **Lostfiles** — Script que identifica arquivos que não pertencem a nenhum pacote.

	[https://github.com/graysky2/lostfiles](https://github.com/graysky2/lostfiles) || [lostfiles](https://www.archlinux.org/packages/?name=lostfiles)

*   **Pacmatic** — Wrapper do *pacman* para verificar o Arch News antes de atualizar, evitar atualizações parciais e avisar sobre alterações de arquivo de configuração.

	[http://kmkeen.com/pacmatic](http://kmkeen.com/pacmatic) || [pacmatic](https://www.archlinux.org/packages/?name=pacmatic)

*   **pacutils** — Biblioteca auxiliar para programas baseados no libalpm.

	[https://github.com/andrewgregory/pacutils](https://github.com/andrewgregory/pacutils) || [pacutils](https://www.archlinux.org/packages/?name=pacutils)

*   **[pkgfile](/index.php/Pkgfile_(Portugu%C3%AAs) "Pkgfile (Português)")** — Ferramenta que descobre qual pacote é dono de um arquivo.

	[http://github.com/falconindy/pkgfile](http://github.com/falconindy/pkgfile) || [pkgfile](https://www.archlinux.org/packages/?name=pkgfile)

*   **pkgtools** — Coleção de scripts para pacotes do Arch Linux.

	[https://github.com/Daenyth/pkgtools](https://github.com/Daenyth/pkgtools) || [pkgtools](https://aur.archlinux.org/packages/pkgtools/)

*   **[Powerpill](/index.php/Powerpill_(Portugu%C3%AAs) "Powerpill (Português)")** — Usa download paralelo e segmentado por meio do [aria2](/index.php/Aria2 "Aria2") e do [Reflector](/index.php/Reflector "Reflector") para tentar acelerar downloads para o *pacman*.

	[https://xyne.archlinux.ca/projects/powerpill/](https://xyne.archlinux.ca/projects/powerpill/) || [powerpill](https://aur.archlinux.org/packages/powerpill/)

*   **repoctl** — Ferramenta para ajudar a gerenciar repositórios locais.

	[https://github.com/cassava/repoctl](https://github.com/cassava/repoctl) || [repoctl](https://aur.archlinux.org/packages/repoctl/)

*   **repose** — Uma ferramenta para construção de repositório do Arch Linux.

	[https://github.com/vodik/repose](https://github.com/vodik/repose) || [repose](https://www.archlinux.org/packages/?name=repose)

*   **[snap-pac](/index.php/Snapper#Wrapping_pacman_transactions_in_snapshots "Snapper")** — Faz o *pacman* usar automaticamente o snapper para criar snapshots pré/pós como o YaST do openSUSE.

	[https://github.com/wesbarnett/snap-pac](https://github.com/wesbarnett/snap-pac) || [snap-pac](https://www.archlinux.org/packages/?name=snap-pac)

*   **vrms-arch** — Um Richard M. Stallman virtual para lhe dizer quis pacotes não livres estão instalados.

	[https://github.com/orospakr/vrms-arch](https://github.com/orospakr/vrms-arch) || [vrms-arch](https://aur.archlinux.org/packages/vrms-arch/)

### Gráficos

**Atenção:** PackageKit abre permissões do sistema por padrão e, do contrário, não é recomendado para uso geral. Veja [FS#50459](https://bugs.archlinux.org/task/50459) e [FS#57943](https://bugs.archlinux.org/task/57943).

*   **Apper** — Aplicativo Qt 5 e gerenciador de pacotes usando o PackageKit escrito em C++. Tem suporte a [metadados de AppStream](https://www.freedesktop.org/wiki/Distributions/AppStream/).

	[https://userbase.kde.org/Apper](https://userbase.kde.org/Apper) || [apper](https://www.archlinux.org/packages/?name=apper)

*   **Discover** — Gerenciador de aplicativos do Qt 5 usando o PackageKit escrito em C++/QML. Tem suporte a [metadados de AppStream](https://www.freedesktop.org/wiki/Distributions/AppStream/), [Flatpak](/index.php/Flatpak "Flatpak") e [atualizações de firmware](/index.php/Fwupd "Fwupd").

	[https://userbase.kde.org/Discover](https://userbase.kde.org/Discover) || [discover](https://www.archlinux.org/packages/?name=discover)

*   **GNOME PackageKit** — Gerenciador de pacotes GTK + 3 usando o PackageKit escrito em C.

	[https://freedesktop.org/software/PackageKit/](https://freedesktop.org/software/PackageKit/) || [gnome-packagekit](https://www.archlinux.org/packages/?name=gnome-packagekit)

*   **GNOME Software** — Gerenciador de aplicativos GTK + 3 usando PackageKit escrito em C. Tem suporte a [metadados de AppStream](https://www.freedesktop.org/wiki/Distributions/AppStream/), [Flatpak](/index.php/Flatpak "Flatpak") e [atualizações de firmware](/index.php/Fwupd "Fwupd").

	[https://wiki.gnome.org/Apps/Software](https://wiki.gnome.org/Apps/Software) || [gnome-software](https://www.archlinux.org/packages/?name=gnome-software)

*   **pcurses** — Wrapper TUI curses para o pacman escrito em C++.

	[https://github.com/schuay/pcurses](https://github.com/schuay/pcurses) || [pcurses](https://www.archlinux.org/packages/?name=pcurses)

*   **tkPacman** — Wrapper Tk para o pacman escrito em Tcl.

	[https://sourceforge.net/projects/tkpacman](https://sourceforge.net/projects/tkpacman) || [tkpacman](https://aur.archlinux.org/packages/tkpacman/)