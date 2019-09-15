**Status de tradução:** Esse artigo é uma tradução de [System maintenance](/index.php/System_maintenance "System maintenance"). Data da última tradução: 2019-05-23\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=System_maintenance&diff=0&oldid=572894) na versão em inglês.

Artigos relacionados

*   [Recomendações gerais](/index.php/Recomenda%C3%A7%C3%B5es_gerais "Recomendações gerais")

Manutenção de sistema regular é necessário para o correto funcionamento do Arch por um período de tempo. Manutenção periódica é uma prática a que muitos usuários se acostumam.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Verifique por erros](#Verifique_por_erros)
    *   [1.1 Falha em serviços de systemd](#Falha_em_serviços_de_systemd)
    *   [1.2 Arquivos de log](#Arquivos_de_log)
*   [2 Backup](#Backup)
    *   [2.1 Arquivos de configuração](#Arquivos_de_configuração)
    *   [2.2 Lista de pacotes instalados](#Lista_de_pacotes_instalados)
    *   [2.3 Banco de dados do pacman](#Banco_de_dados_do_pacman)
    *   [2.4 Cabeçalhos LUKS](#Cabeçalhos_LUKS)
    *   [2.5 Dados de sistema e de usuário](#Dados_de_sistema_e_de_usuário)
*   [3 Atualizando o sistema](#Atualizando_o_sistema)
    *   [3.1 Leia antes de atualizar o sistema](#Leia_antes_de_atualizar_o_sistema)
    *   [3.2 Evite certos comandos do pacman](#Evite_certos_comandos_do_pacman)
    *   [3.3 Sem suporte a atualizações parciais](#Sem_suporte_a_atualizações_parciais)
    *   [3.4 Aja em alertas durante uma atualização](#Aja_em_alertas_durante_uma_atualização)
    *   [3.5 Lide prontamente com os novos arquivos de configuração](#Lide_prontamente_com_os_novos_arquivos_de_configuração)
    *   [3.6 Reverta atualizações quebradas](#Reverta_atualizações_quebradas)
    *   [3.7 Verifique por pacotes órfãos ou abandonados](#Verifique_por_pacotes_órfãos_ou_abandonados)
*   [4 Use o gerenciador de pacotes para instalar softwares](#Use_o_gerenciador_de_pacotes_para_instalar_softwares)
    *   [4.1 Escolha drivers código aberto](#Escolha_drivers_código_aberto)
    *   [4.2 Tenha cuidado com pacotes não oficiais](#Tenha_cuidado_com_pacotes_não_oficiais)
    *   [4.3 Atualize o mirrorlist](#Atualize_o_mirrorlist)
*   [5 Limpe o sistema de arquivos](#Limpe_o_sistema_de_arquivos)
    *   [5.1 Cache de pacotes](#Cache_de_pacotes)
    *   [5.2 Pacotes não usados (órfãos)](#Pacotes_não_usados_(órfãos))
    *   [5.3 Arquivos de configuração antigos](#Arquivos_de_configuração_antigos)
    *   [5.4 Links simbólicos quebrados](#Links_simbólicos_quebrados)
*   [6 Dicas e truques](#Dicas_e_truques)
    *   [6.1 Use pacotes de software aprovados](#Use_pacotes_de_software_aprovados)
    *   [6.2 Instale o pacote linux-lts](#Instale_o_pacote_linux-lts)
*   [7 Veja também](#Veja_também)

## Verifique por erros

### Falha em serviços de systemd

Verifique se algum serviço do systemd entrou em um estado de falha:

```
$ systemctl --failed

```

Veja [Systemd (Português)#Analisando o estado do sistema](/index.php/Systemd_(Portugu%C3%AAs)#Analisando_o_estado_do_sistema "Systemd (Português)") para mais informações.

### Arquivos de log

Procure por erros nos arquivos de log localizados em `/var/log`, bem como erros de alta prioridade no journal do systemd:

```
# journalctl -p 3 -xb

```

Veja [systemd/Journal](/index.php/Systemd/Journal_(Portugu%C3%AAs) "Systemd/Journal (Português)") para mais informações.

Veja [Xorg (Português)#Troubleshooting](/index.php/Xorg_(Portugu%C3%AAs)#Troubleshooting "Xorg (Português)") para informações sobre onde e como o [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)") registra os erros.

## Backup

Crie backups de dados importante em intervalos regulares. Veja [Programas de sincronização e backup](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs") para muitas alternativas de aplicativos que podem se adequar ao seu caso. Veja [Category:System recovery (Português)](/index.php/Category:System_recovery_(Portugu%C3%AAs) "Category:System recovery (Português)") para outros artigos de internet.

Os backups podem ser automatizados com [systemd/Timers (Português)](/index.php/Systemd/Timers_(Portugu%C3%AAs) "Systemd/Timers (Português)").

### Arquivos de configuração

Antes de editar quaisquer arquivos de configuração, crie um backup de forma que você possa reverter para uma versão funcional no caso de haver problemas. Editores como [vim](/index.php/Vim "Vim") e [emacs](/index.php/Emacs "Emacs") pode fazer isso automaticamente, assim como ferramentas como [etckeeper](/index.php/Etckeeper "Etckeeper") que mantêm `/etc` em um [sistema de controle de versão](/index.php/Version_control_system "Version control system") (VCS); veja [dotfiles (Português)#Rastreando dotfiles diretamente com Git](/index.php/Dotfiles_(Portugu%C3%AAs)#Rastreando_dotfiles_diretamente_com_Git "Dotfiles (Português)") para mais.

### Lista de pacotes instalados

Mantenha uma lista de todos os pacotes instalados de forma que, se uma reinstalação completa for inevitável, seja mais fácil recriar o ambiente original.

Veja [pacman/Dicas e truques#Lista de pacotes instalados](/index.php/Pacman/Dicas_e_truques#Lista_de_pacotes_instalados "Pacman/Dicas e truques") para detalhes.

### Banco de dados do pacman

Veja [pacman/Dicas e truques#Fazer backup da base de dados do pacman](/index.php/Pacman/Dicas_e_truques#Fazer_backup_da_base_de_dados_do_pacman "Pacman/Dicas e truques").

### Cabeçalhos LUKS

Pode fazer sentido verificar e sincronizar periodicamente os backups de cabeçalhos de partições criptografadas com LUKS, especialmente se palavras-chaves tiverem sido revogadas. Veja [Dm-crypt/Device encryption#Backup and restore](/index.php/Dm-crypt/Device_encryption#Backup_and_restore "Dm-crypt/Device encryption").

### Dados de sistema e de usuário

Veja [Backup do sistema](/index.php/Backup_do_sistema "Backup do sistema").

## Atualizando o sistema

É recomendado realizar atualizações completas do sistema regularmente via [Pacman (Português)#Atualizando pacotes](/index.php/Pacman_(Portugu%C3%AAs)#Atualizando_pacotes "Pacman (Português)"), para aproveitar as últimas correções de erros e atualizações de segurança, além de evitar de ter que lidar com muitas atualizações de pacotes que exigem intervenção manual de uma só vez. Ao solicitar suporte da comunidade, é geralmente presumido que o sistema esteja atualizado.

Certifique-se de que a mídia de instalação do Arch ou outro CD/USB "live" de Linux esteja disponível, de forma que você possa facilmente recuperar seu sistema se houver um problema após a atualização. Se você está usando o Arch em um ambiente de produção, ou não puder se dar o luxo de tê-lo indisponível por algum motivo, teste alterações aos arquivos de configurações, bem como atualizações de pacotes de software, em um sistema duplicata não crítico (i.e sistema de homologação) primeiro. Então, se tudo funcionar corretamente, aplique as alterações no sistema de produção.

Se o sistema possui pacotes do [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)"), atualize todos eles com muito cuidado.

*pacman* é uma ferramenta de gerenciamento de pacotes poderosa, mas ela não tenta resolver todos problemas possíveis. Os usuários devem estar vigilantes e ter responsabilidade pela manutenção de seu próprio sistema.

### Leia antes de atualizar o sistema

Antes de atualizar, espera-se que os usuários visitem a [página inicial do Arch Linux](https://www.archlinux.org/) (ou até o [Arch Linux Brasil](http://www.archlinux-br.org/)) para verificar as últimas notícias ou, alternativamente, estejam inscritos no [feed RSS](https://www.archlinux.org/feeds/news/) ou na [lista de discussão arch-announce](https://mailman.archlinux.org/mailman/listinfo/arch-announce/). Quando atualizações exigirem intervenção fora do normal do usuário (mais do que pode ser tratado simplesmente seguindo as instruções fornecidas pelo *pacman*), uma notícia apropriada será publicada.

Antes de atualizar softwares fundamentais (como o [kernel](/index.php/Kernel "Kernel"), [xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)"), [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") ou [glibc](https://www.archlinux.org/packages/?name=glibc)) para uma nova versão, procure pelo [fórum](https://bbs.archlinux.org/) apropriado por algum relato de problema.

Da mesma forma, usuários devem estar cientes de que atualizar pacotes pode trazer problemas **inesperados** que podem precisar de intervenção imediata; portanto, é desencorajado atualizar um sistema estável logo antes dele ser necessário para realizar uma tarefa importante. Em vez disso, é sábio esperar ter tempo suficiente para poder lidar com possíveis problemas pós-atualização.

### Evite certos comandos do pacman

Evite fazer [atualizações parciais](#Sem_suporte_a_atualizações_parciais). Em outras palavras, nunca execute `pacman -Sy`; em vez disso, sempre use `pacman -Syu`.

Geralmente evite usar a opção `--overwrite` com o pacman. A opção `--overwrite` leva um argumento contendo um glob. Quando usado, o pacman ignorará as verificações de conflitos de arquivos em busca de arquivos que correspondam ao glob. Em um sistema adequadamente mantido, ele deve ser usado somente quando explicitamente recomendado pelos desenvolvedores do Arch. Veja a seção [#Leia antes de atualizar o sistema](#Leia_antes_de_atualizar_o_sistema).

Evite usar a opção `-d` com o pacman. `pacman -Rdd *pacote*` ignora verificações de dependência durante a remoção de pacote. Como resultado, um pacote fornecendo uma dependência crítica pode ser removido, resultando em um sistema quebrado.

### Sem suporte a atualizações parciais

Arch Linux é uma distribuição de *[rolling release](https://en.wikipedia.org/wiki/pt:rolling_release são enviadas para os repositórios, os [desenvolvedores](https://www.archlinux.org/people/developers/) e [Trusted Users](/index.php/Trusted_Users_(Portugu%C3%AAs) "Trusted Users (Português)") recompilam todos os pacotes nos repositórios que precisam ser recompilados com as bibliotecas. Por exemplo, se dois pacotes dependem da mesma biblioteca, atualizar apenas um pacote pode também atualizar a biblioteca (como uma dependência), o que pode então quebrar o outro pacote que depende de uma versão antiga da biblioteca.

É por esse motivo que *não há suporte* a atualizações parciais. Não use `pacman -Sy *pacote*` ou qualquer comando equivalente, como `pacman -Sy` seguido por `pacman -S *pacote*`. **Sempre** atualize (com `pacman -Syu`) antes de instalar um pacote. Tenha muito cuidado ao usar `IgnorePkg` e `IgnoreGroup` pelo mesmo motivo. Se o sistema possui pacotes compilados localmente (tal como pacote do [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)")), os usuários precisarão recompilá-los quando suas dependências receberem uma mudança no [soname](https://en.wikipedia.org/wiki/pt:soname "wikipedia:pt:soname").

Se um cenário de atualização parcial for criado, e os binários forem quebrados porque eles não conseguem localizar as bibliotecas às quais eles estão vinculados, **não "corrija" o problema usando apenas fazendo um link simbólico**. Bibliotecas recebem mudanças [soname](https://en.wikipedia.org/wiki/pt:soname "wikipedia:pt:soname") quando elas **não possuem compatível com a versão anterior**. Um simples `pacman -Syu` com um espelho sincronizado corretamente irá corrigir o problema, desde que o *pacman* não esteja quebrado.

O script bash *checkupdates*, incluído no pacote [pacman-contrib](https://www.archlinux.org/packages/?name=pacman-contrib), fornece uma forma segura de verificar por atualizações para pacotes instalados sem executar uma atualização do sistema ao mesmo tempo.

### Aja em alertas durante uma atualização

Ao atualizar o sistema, certifique-se de prestar atenção aos avisos de alerta fornecidos pelo [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)"). Se quaisquer ações adicionais do usuário forem exigidas, assegure-se de resolvê-las imediatamente. Se um alerta do pacman estiver confuso, pesquise no fórum e notícias recentes para mais instruções detalhadas.

### Lide prontamente com os novos arquivos de configuração

Quando o pacman é chamado, arquivos `.pacnew` e `.pacsave` podem ser criados. Pacman fornece aviso quando isso acontece e usuários devem lidar com esses arquivos imediatamente. Veja a página wiki [pacman/Pacnew e Pacsave](/index.php/Pacman/Pacnew_e_Pacsave "Pacman/Pacnew e Pacsave") para instruções detalhadas.

Também, pense em outros arquivos de configuração que você pode ter copiado ou criado. Se um pacote possuir um exemplo de configuração que você copiou para seu diretório home, verifique se um novo foi criado.

### Reverta atualizações quebradas

Se uma atualização de pacote é esperada/sabido causar problemas, empacotadores vão se certificar de exibir uma mensagem apropriada quando o pacote é atualizado. Se você presenciar um problema após uma atualização, confira a saída do pacman olhando no `/var/log/pacman.log`.

**Dica:** Você pode usar um visualização de log como o [wat-git](https://aur.archlinux.org/packages/wat-git/) para pesquisar por logs do pacman.

A esse ponto, somente após garantir que não haja informações disponíveis pelo pacman, que não há notícia relacionada no [https://www.archlinux.org/](https://www.archlinux.org/) e que não haja tópicos no fórum sobre a atualização, considere pedir ajuda no [fórum](https://bbs.archlinux.org), pelo [IRC](/index.php/IRC_(Portugu%C3%AAs) "IRC (Português)") ou [fazendo downgrade](/index.php/Fazendo_downgrade "Fazendo downgrade") da versão do pacote danoso.

### Verifique por pacotes órfãos ou abandonados

Após a atualização, você pode agora ter pacotes que não são mais necessários ou que não estão mais nos repositórios oficiais.

Use `pacman -Qtd` para verificar se os pacotes foram instalados como uma dependência, mas agora, nenhum outro pacote depende deles. Se um pacote órfão ainda for necessário, é recomendável alterar o [motivo de instalação](/index.php/Motivo_de_instala%C3%A7%C3%A3o "Motivo de instalação") para explícito. Caso contrário, se o pacote não for mais necessário, ele pode ser removido.

Além disso, alguns pacotes podem não estar nos repositórios remotos, mas eles ainda podem estar no seu sistema local. Para listar todos os pacotes externos use `pacman -Qm`. Observe que esta lista incluirá pacotes que foram instalados manualmente (p. ex., a partir do [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)")). Para excluir pacotes que (ainda) estão disponíveis no AUR, use a ferramenta [ancient-packages](https://aur.archlinux.org/packages/ancient-packages/).

## Use o gerenciador de pacotes para instalar softwares

O [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") faz um trabalho bem melhor do que você em manter rastro dos arquivos. Se você instalar coisas manualmente você *vai*, cedo ou tarde, esquecer o que você fez, esquecer onde você instalou, instalar softwares conflitantes, instalar as localizações erradas, etc.

*   Instale pacotes dos repositórios oficiais usando o método na seção [Pacman (Português)#Instalando pacotes](/index.php/Pacman_(Portugu%C3%AAs)#Instalando_pacotes "Pacman (Português)").
*   Se o programa que você deseja não estiver disponível, verifique se alguém criou um pacote no [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)"). Siga o método naquele artigo para instalação.
*   Por último, se o programa que você deseja não se encontra nos repositórios oficiais ou no AUR, aprenda como [criar um pacote](/index.php/Criar_um_pacote "Criar um pacote") para ele.

Para limpar arquivos instalados inadequadamente, Veja [Pacman/Dicas e truques#Identificar arquivos que pertençam a nenhum pacote](/index.php/Pacman/Dicas_e_truques#Identificar_arquivos_que_pertençam_a_nenhum_pacote "Pacman/Dicas e truques").

### Escolha drivers código aberto

Sempre tente usar drivers de código aberto antes de recorrer a drivers proprietários. Na maioria das vezes, drivers de código aberto são mais estáveis e confiáveis do que drivers proprietários. Bugs de drivers de código aberto são corrigidos com mais facilidade e rapidez. Apesar de drivers proprietários poderem oferecer mais recursos e capacidades, isso pode vir com o custo da perda de estabilidade. Para evitar esse dilema, tente escolher componentes de hardware conhecidos para ter um suporte maduro a driver de código aberto com todos os recursos. Informações sobre hardware com drivers Linux de código aberto estão disponíveis em [linux-drivers.org](http://www.linux-drivers.org/).

### Tenha cuidado com pacotes não oficiais

Seja cauteloso ao usar pacotes do [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)") ou um [repositório não oficial de usuários](/index.php/Unofficial_user_repository "Unofficial user repository"). A maioria é fornecida pelos usuários e, portanto, pode não ter os mesmos padrões que aqueles nos repositórios oficiais. Evite [auxiliares do AUR](/index.php/Auxiliares_do_AUR "Auxiliares do AUR") que automatizam a instalação de pacotes do AUR. **Sempre** verifique PKGBUILDs por sanidade e sinais de erro ou código malicioso antes de compilar a/ou instalar o pacote.

Para simplificar a manutenção, limite a quantidade de pacotes não oficiais usados. Faça verificações periódicas de quais estão em uso e remova (ou substitua por suas contrapartes oficiais) quaisquer outros. Veja [pacman/Dicas e truques#Manutenção](/index.php/Pacman/Dicas_e_truques#Manutenção "Pacman/Dicas e truques") para comandos úteis.

### Atualize o mirrorlist

Atualize a lista de espelhos (*mirrorlist*) do pacman, pois a qualidade dos espelhos podem variar ao longo do tempo e alguns podem ficar inacessíveis ou sua taxa de download pode estar ruim.

Veja [Espelhos](/index.php/Espelhos "Espelhos") para detalhes.

## Limpe o sistema de arquivos

Ao procurar por arquivos para remover, é importante localizar os arquivos que mais ocupam espaço do disco. Programas que ajudam nisso são localizados em:

*   [List of applications#Disk usage display](/index.php/List_of_applications#Disk_usage_display "List of applications").
*   [List of applications#Disk cleaning](/index.php/List_of_applications#Disk_cleaning "List of applications").

### Cache de pacotes

Remova arquivos `.pkg` indesejados de `/var/cache/pacman/pkg/` para liberar espaço em disco.

Veja [Pacman (Português)#Limpando o cache de pacotes](/index.php/Pacman_(Portugu%C3%AAs)#Limpando_o_cache_de_pacotes "Pacman (Português)") para mais informações.

### Pacotes não usados (órfãos)

Remova pacotes não usados do sistema para liberar espaço em disco e simplificar a manutenção

See [Pacman/Dicas e truques#Removendo pacotes não usados (órfãos)](/index.php/Pacman/Dicas_e_truques#Removendo_pacotes_não_usados_(órfãos) "Pacman/Dicas e truques") for details.

### Arquivos de configuração antigos

Arquivos de configuração antigos podem conflitar com versões novas dos softwares ou se corromperem ao longo do tempo. Remova configurações desnecessárias periodicamente, em especial em sua pasta home e `~/.config`. Por motivos similares, tenha cuidado ao compartilhar pastas home entre instalações.

Procure pelas seguintes pastas:

*   `~/.config/` -- onde aplicativos armazenam suas configurações
*   `~/.cache/` -- cache de alguns programas podem crescer em tamanho
*   `~/.local/share/` -- arquivos antigos podem estar parados lá

Veja [XDG Base Directory support](/index.php/XDG_Base_Directory_support "XDG Base Directory support") para mais informações.

Para manter o diretório home limpe de arquivos temporários criados no lugar errado, é uma boa ideia gerenciar uma lista de arquivos indesejados e removê-los regularmente, por exemplo, com [rmshit.py](https://github.com/lahwaacz/Scripts/blob/master/rmshit.py).

[rmlint](https://www.archlinux.org/packages/?name=rmlint) pode ser usado para localizar e, opcionalmente, remover arquivos duplicados, arquivos vazios, diretórios vazios recursivamente e links simbólicos quebrados.

### Links simbólicos quebrados

Links simbólicos antigos e quebrados podem estar soltos no seu sistema; você deve removê-los. Pode-se encontrar exemplos sobre como conseguir isso [aqui](https://unix.stackexchange.com/questions/34248/how-can-i-find-broken-symlinks) e [aqui](http://www.commandlinefu.com/commands/view/8260/find-broken-symlinks).

Para listar rapidamente todos os links simbólicos em seu sistema, use:

```
# find / -xtype l -print

```

Então, inspecione e remova todas as entradas desnecessárias desta lista.

## Dicas e truques

As seguintes dicas geralmente não são necessários, mas certos usuários podem achá-los úteis.

### Use pacotes de software aprovados

O estilo *rolling release* do Arch pode ser benéfico para usuários que desejam tentar os últimos recursos ou obter atualizações do upstream o mais cedo possível, mas eles também podem dificultar a manutenção do sistema. Para simplificar a manutenção e melhorar a estabilidade, tente evitar softwares demasiadamente novos e instale apenas softwares aprovados e maduros. Tais pacotes têm menos chance de receber atualizações difíceis, como grandes alterações nas configurações ou remoções de recursos. Prefira um software que possua uma comunidade de desenvolvimento forte e ativa, bem como um alto número de usuários competentes, para simplificar suporte na eventualidade de ocorrer um problema.

Evite qualquer uso do repositório de teste, até mesmo pacotes individuais de teste. Esses pacotes são experimentais e não são adequados para um sistema estável. Da mesma forma, evite pacotes que são compilados diretamente dos fontes de desenvolvimento do upstream. Esses geralmente são encontrados no [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)"), com nomes incluindo coisas como: "dev", "devel", "svn", "cvs", "git", etc.

### Instale o pacote linux-lts

O pacote [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) é uma pacote alternativo de kernel do Arch e está disponível no repositório [core](/index.php/Core_(Portugu%C3%AAs) "Core (Português)"). Essa versão de kernel em particular possui suporte de longo prazo (LTS) do upstream, incluindo correções de segurança e alguns *backports* de recursos. É útil caso você prefira a estabilidade de atualizações menos frequentes de kernel ou caso você deseje um kernel *fallback* na eventualidade de um novo kernel causar problemas.

Para disponibilizá-lo como uma opção de boot, você precisará atualizar as configurações de seu [gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot") para usar o kernel LTS e disco de ram: `vmlinuz-linux-lts` and `initramfs-linux-lts.img`.

## Veja também

*   [Arch News Bash Script](https://bbs.archlinux.org/viewtopic.php?id=146850)
*   [Automatic Arch System Maintenance](https://bbs.archlinux.org/viewtopic.php?pid=1791008)