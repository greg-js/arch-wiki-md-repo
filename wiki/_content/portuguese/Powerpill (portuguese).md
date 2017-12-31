O [Powerpill](https://xyne.archlinux.ca/projects/powerpill/) é um wrapper do [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") que usa downloads paralelos e segmentados para tentar acelerar downloads para o pacman. Internamente, usa [Aria2](/index.php/Aria2 "Aria2") e [Reflector](/index.php/Reflector "Reflector") para conseguir isso. O Powerpill também pode usar [rsync](/index.php/Rsync "Rsync") para espelhos oficiais que oferecem suporte a ele. Isso pode ser eficiente para usuários que já usam largura de banda total ao fazer o download a partir de um único espelho. Também há suporte ao [Pacserve](/index.php/Pacserve_(Portugu%C3%AAs) "Pacserve (Português)") através do arquivo de configuração e será usado antes de baixar de espelhos externos. Exemplo: deseja-se atualizar e executa-se *pacman -Syu*, o qual retorna uma lista de 20 pacotes que estão disponíveis para atualização total de 200 mega. Se o usuário os baixar via pacman, eles serão baixados um após o outro. Se o usuário os baixar através do powerpill, eles serão baixados simultaneamente em muitos casos várias vezes mais rápido (dependendo da velocidade da conexão, da disponibilidade de pacotes nos servidores e da velocidade do servidor/carga, etc.)

Um teste de pacman vs. powerpill em um sistema revelou uma aceleração de 4x no cenário acimia, sendo que o pacman baixa em uma média de 300 kB/s e o powerpill baixa na média de 1.2 MB/s.

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
*   [2 Configuração](#Configura.C3.A7.C3.A3o)
*   [3 Usando Reflector](#Usando_Reflector)
*   [4 Usando rsync](#Usando_rsync)
*   [5 Uso básico](#Uso_b.C3.A1sico)
    *   [5.1 Atualizando o sistema](#Atualizando_o_sistema)
    *   [5.2 Instalação de pacotes](#Instala.C3.A7.C3.A3o_de_pacotes)
*   [6 Solução de problemas](#Solu.C3.A7.C3.A3o_de_problemas)
*   [7 Veja também](#Veja_tamb.C3.A9m)

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [powerpill](https://aur.archlinux.org/packages/powerpill/).

## Configuração

Powerpill tem um único arquivo de configuração `/etc/powerpill/powerpill.json` que você pode editar como quiser. Veja a página man [powerpill.json(1)](https://xyne.archlinux.ca/projects/powerpill/#powerpill.json1) para detalhes.

## Usando Reflector

Por padrão, o Powerpill está configurado para usar [Reflector](/index.php/Reflector "Reflector") para obter a lista atual de espelhos da API Web do servidor do Arch Linux e usá-los para downloads paralelos. Isto é para se certificar de que existem servidores suficientes na lista para melhorias de velocidade significativas.

## Usando rsync

O suporte a [Rsync](/index.php/Rsync "Rsync") está disponível para alguns espelhos. Quando ativado, as sincronizações de base de dados (`pacman -Sy`) e outras operações podem ser muito mais rápidas porque uma única conexão é usada. O próprio protocolo rsync também acelera as verificações de atualização e, às vezes, as transferências de arquivos.

Para localizar um espelho adequado com suporte a rsync, use o `reflector`:

```
$ reflector -p rsync

```

Alternativamente, você pode localizar os `*n*` servidores mais rápidos com a opção `-f *n*` e os `*m*` servidores mais recentemente sincronizados com a opção `-l *m*`:

```
$ reflector -p rsync -f *n* -l *m*

```

Selecione o(s) espelho(s) que você deseja usar. A opção `-c` também pode ser usada para filtrar por sua nacionalidade (`reflector --list-countries` para ver uma lista completa, usando aspas em volta do nome, e há diferenciação de maiúsculo e minúsculo!). Uma vez feito, edite `/etc/powerpill/powerpill.json`, role para baixo para a seção `rsync` e adicione quantos servidores você quiser ao campo de servidor.

Após isso, toda a base de dados e pacotes oficiais será baixada do servidor rsync quando possível.

## Uso básico

Para a maioria das operações, o *powerpill* funciona da mesma forma que o pacman, já que é um script *wrapper* para o *pacman*.

### Atualizando o sistema

Para atualizar seu sistema (sincronizar e atualizar pacotes instalados) usando o, basta passar as opções `-Syu` como você faria com o *pacman*:

```
# powerpill -Syu

```

### Instalação de pacotes

Para instalar um pacote e suas dependências, basta usar o powerpill com a opção `-S` como você faria com o *pacman*:

```
# powerpill -S *pacote*

```

Você também pode instalar múltiplos pacotes com ele como você faria com o *pacman*:

```
# powerpill -S *pacote1* *pacote2* *pacote3*

```

## Solução de problemas

No caso de você obter um [err] para arquivos <repo>.db.sig:

```
   b5d7d7|ERR |       0B/s|/var/lib/pacman/sync/extra.db.sig
   899e91|ERR |       0B/s|/var/lib/pacman/sync/multilib.db.sig
   8fcc32|ERR |       0B/s|/var/lib/pacman/sync/core.db.sig
   85eb3d|ERR |       0B/s|/var/lib/pacman/sync/community.db.sig

```
É porque os arquivos de assinatura estão faltando para aquele repo e você não definiu `SigLevel = PackageRequired` explicitamente no `/etc/pacman.conf`, conforme explicado nesta publicação do [fórum do Arch](https://bbs.archlinux.org/viewtopic.php?pid=1254940#p1254940)

## Veja também

*   [Powerpill](http://xyne.archlinux.ca/projects/powerpill/) - página oficial do projeto
*   [powerpill reborn](https://bbs.archlinux.org/viewtopic.php?id=153818) - powerpill está de volta :)