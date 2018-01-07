Artigos relacionados

*   [Criando pacotes](/index.php/Criando_pacotes "Criando pacotes")
*   [Fazendo downgrade de pacotes](/index.php/Fazendo_downgrade_de_pacotes "Fazendo downgrade de pacotes")
*   [pacman/Assinatura de pacote](/index.php/Pacman/Assinatura_de_pacote "Pacman/Assinatura de pacote")
*   [pacman/Pacnew e Pacsave](/index.php/Pacman/Pacnew_e_Pacsave "Pacman/Pacnew e Pacsave")
*   [pacman/Restaurar base de dados local](/index.php/Pacman/Restaurar_base_de_dados_local "Pacman/Restaurar base de dados local")
*   [pacman/Rosetta](/index.php/Pacman/Rosetta "Pacman/Rosetta")
*   [pacman/Dicas e truques](/index.php/Pacman/Dicas_e_truques "Pacman/Dicas e truques")
*   [FAQ (Português)#Gerenciamento de pacote](/index.php/FAQ_(Portugu%C3%AAs)#Gerenciamento_de_pacote "FAQ (Português)")
*   [Manutenção do sistema](/index.php/Manuten%C3%A7%C3%A3o_do_sistema "Manutenção do sistema")
*   [Arch Build System](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)")
*   [Repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais")
*   [Arch User Repository](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)")

O [gerenciador de pacote](https://en.wikipedia.org/wiki/Package_management_system "wikipedia:Package management system") **[pacman](https://www.archlinux.org/pacman/)** é uma das grandes vantagens do Arch Linux. Combina um simples pacote no formato binário, com um fácil uso de [sistema de compilação](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)"). A meta do pacman é tornar o mais fácil possível gerenciar pacotes, sejam eles dos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais") ou das próprias compilações do usuário.

O *pacman* mantém o sistema atualizado, listas de pacotes de sincronização com o servidor mestre. Este modelo servidor/cliente também permite o usuário baixar/instalar pacotes com um simples comando, completo com todas as dependências requeridas.

O *pacman* é escrito na linguagem de programação C e usa o formato [tar](https://en.wikipedia.org/wiki/pt:TAR "w:pt:TAR") para empacotamento.

**Dica:** O pacote [pacman](https://www.archlinux.org/packages/?name=pacman) também contém outras ferramentas úteis, tal como o [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)"), **pactree**, **vercmp** e [checkupdates](/index.php/Checkupdates_(Portugu%C3%AAs) "Checkupdates (Português)"). Execute `pacman -Qlq pacman | grep bin` para ver uma lista completa.

## Contents

*   [1 Uso](#Uso)
    *   [1.1 Instalando pacotes](#Instalando_pacotes)
        *   [1.1.1 Instalando pacotes específicos](#Instalando_pacotes_espec.C3.ADficos)
        *   [1.1.2 Instalando grupos de pacotes](#Instalando_grupos_de_pacotes)
    *   [1.2 Removendo pacotes](#Removendo_pacotes)
    *   [1.3 Atualizando pacotes](#Atualizando_pacotes)
    *   [1.4 Consultando base de dados de pacotes](#Consultando_base_de_dados_de_pacotes)
        *   [1.4.1 Estrutura da base de dados](#Estrutura_da_base_de_dados)
    *   [1.5 Limpando o cache de pacotes](#Limpando_o_cache_de_pacotes)
    *   [1.6 Comandos adicionais](#Comandos_adicionais)
    *   [1.7 Motivo de instalação](#Motivo_de_instala.C3.A7.C3.A3o)
    *   [1.8 Pesquisar por um pacote que contenha um arquivo específico](#Pesquisar_por_um_pacote_que_contenha_um_arquivo_espec.C3.ADfico)
*   [2 Configuração](#Configura.C3.A7.C3.A3o)
    *   [2.1 Opções gerais](#Op.C3.A7.C3.B5es_gerais)
        *   [2.1.1 Comparando versões antes de atualizar](#Comparando_vers.C3.B5es_antes_de_atualizar)
        *   [2.1.2 Pular pacotes para não serem atualizados](#Pular_pacotes_para_n.C3.A3o_serem_atualizados)
        *   [2.1.3 Pular um grupos de pacotes para não serem atualizados](#Pular_um_grupos_de_pacotes_para_n.C3.A3o_serem_atualizados)
        *   [2.1.4 Pular arquivos para não serem instalados no sistema](#Pular_arquivos_para_n.C3.A3o_serem_instalados_no_sistema)
        *   [2.1.5 Manter vários arquivos de configuração](#Manter_v.C3.A1rios_arquivos_de_configura.C3.A7.C3.A3o)
        *   [2.1.6 Hooks](#Hooks)
    *   [2.2 Repositórios e espelhos](#Reposit.C3.B3rios_e_espelhos)
        *   [2.2.1 Segurança de pacote](#Seguran.C3.A7a_de_pacote)
*   [3 Solução de problemas](#Solu.C3.A7.C3.A3o_de_problemas)
    *   [3.1 Erro "falha em submeter a transação (arquivos conflitantes)"](#Erro_.22falha_em_submeter_a_transa.C3.A7.C3.A3o_.28arquivos_conflitantes.29.22)
    *   [3.2 Erro "falha em submeter a transação (pacote inválido ou corrompido)"](#Erro_.22falha_em_submeter_a_transa.C3.A7.C3.A3o_.28pacote_inv.C3.A1lido_ou_corrompido.29.22)
    *   [3.3 Erro "falha ao iniciar a transação (não foi possível travar a base de dados)"](#Erro_.22falha_ao_iniciar_a_transa.C3.A7.C3.A3o_.28n.C3.A3o_foi_poss.C3.ADvel_travar_a_base_de_dados.29.22)
    *   [3.4 Pacotes não podem ser obtidos na instalação](#Pacotes_n.C3.A3o_podem_ser_obtidos_na_instala.C3.A7.C3.A3o)
    *   [3.5 Reinstalação manual do pacman](#Reinstala.C3.A7.C3.A3o_manual_do_pacman)
    *   [3.6 pacman trava durante uma atualização](#pacman_trava_durante_uma_atualiza.C3.A7.C3.A3o)
    *   [3.7 Erro "Unable to find root device" após a reinicialização](#Erro_.22Unable_to_find_root_device.22_ap.C3.B3s_a_reinicializa.C3.A7.C3.A3o)
    *   [3.8 Assinatura de "<email@exemplo.org>" tem confiança desconhecida, falha na instalação](#Assinatura_de_.22.3Cemail.40exemplo.org.3E.22_tem_confian.C3.A7a_desconhecida.2C_falha_na_instala.C3.A7.C3.A3o)
    *   [3.9 Solicitação de importação de chaves PGP](#Solicita.C3.A7.C3.A3o_de_importa.C3.A7.C3.A3o_de_chaves_PGP)
    *   [3.10 Erro: chave "0123456789ABCDEF" não pôde ser procurado remotamente](#Erro:_chave_.220123456789ABCDEF.22_n.C3.A3o_p.C3.B4de_ser_procurado_remotamente)
    *   [3.11 Assinatura de "Usuário <email@archlinux.org>" é inválida, falha na instalação](#Assinatura_de_.22Usu.C3.A1rio_.3Cemail.40archlinux.org.3E.22_.C3.A9_inv.C3.A1lida.2C_falha_na_instala.C3.A7.C3.A3o)
    *   [3.12 Erro 'aviso: locale atual é inválida; usando locale padrão "C"'](#Erro_.27aviso:_locale_atual_.C3.A9_inv.C3.A1lida.3B_usando_locale_padr.C3.A3o_.22C.22.27)
    *   [3.13 pacman não respeita as configurações de proxy](#pacman_n.C3.A3o_respeita_as_configura.C3.A7.C3.B5es_de_proxy)
    *   [3.14 Como faço para reinstalar todos os pacotes, mantendo informações sobre se algo foi explicitamente instalado ou como uma dependência?](#Como_fa.C3.A7o_para_reinstalar_todos_os_pacotes.2C_mantendo_informa.C3.A7.C3.B5es_sobre_se_algo_foi_explicitamente_instalado_ou_como_uma_depend.C3.AAncia.3F)
    *   [3.15 Erro "cannot open shared object file"](#Erro_.22cannot_open_shared_object_file.22)
    *   [3.16 Congelamento de downloads de pacote](#Congelamento_de_downloads_de_pacote)
    *   [3.17 Falha ao obter arquivo 'core.db' do espelho](#Falha_ao_obter_arquivo_.27core.db.27_do_espelho)
*   [4 Veja também](#Veja_tamb.C3.A9m)

## Uso

O que se segue é apenas uma pequena amostra das operações que o *pacman* pode executar. Para ler mais exemplos, consulte [pacman(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8).

**Dica:** Para usuários que utilizaram outras distribuições linux antes, ver o artigo [Pacman Rosetta](/index.php/Pacman_Rosetta "Pacman Rosetta") será útil.

### Instalando pacotes

**Nota:** Alguns pacotes muitas vezes têm uma série de [dependências opcionais](/index.php/PKGBUILD_(Portugu%C3%AAs)#optdepends "PKGBUILD (Português)") de pacotes que fornecem funcionalidades adicionais para a aplicação, embora não seja estritamente necessário para executá-lo. Ao instalar um pacote, o *pacman* irá listar suas dependências opcionais entre as mensagens de saída, porém elas não serão encontrados no arquivo `pacman.log`: utilize o comando [pacman -Si](#Consultando_base_de_dados_de_pacotes) para visualizar as dependências opcionais de um pacote, juntamente com uma breve descrição das funcionalidades de cada um.

**Atenção:** Ao instalar pacotes no Arch, evite atualizar a lista de pacotes sem [atualizar o sistema](#Atualizando_pacotes) (por exemplo, quando um [pacote não é encontrado](#Pacotes_n.C3.A3o_podem_ser_obtidos_na_instala.C3.A7.C3.A3o) nos repositórios oficiais). Na prática, **não** execute o comando `pacman -Sy *nome_pacote*`, pois isso poderia levar para problemas de dependências. Veja [Manutenção do sistema#Sem suporte a atualizações parciais](/index.php/Manuten%C3%A7%C3%A3o_do_sistema#Sem_suporte_a_atualiza.C3.A7.C3.B5es_parciais "Manutenção do sistema") e [BBS#89328](https://bbs.archlinux.org/viewtopic.php?id=89328).

#### Instalando pacotes específicos

Para instalar um único pacote ou lista de pacotes (incluindo dependências), execute o seguinte comando:

```
# pacman -S *nome_pacote1* *nome_pacote2* ...

```

Para instalar uma lista de pacotes com expressão regular (veja [esse tópico do fórum](https://bbs.archlinux.org/viewtopic.php?id=7179)):

```
# pacman -S $(pacman -Ssq *regexp_pacote*)

```

Às vezes, há várias versões de um pacote nos diferentes repositórios, por exemplo *extra* e *testing*. Para instalar a versão anterior, o repositório deve ser definido na frente:

```
# pacman -S extra/*nome_pacote*

```

Para instalar um número de pacotes que compartilham padrões em sua nomenclatura -- não todo um grupo nem todos pacotes correspondentes; por exemplo [plasma](https://www.archlinux.org/groups/x86_64/plasma/):

```
# pacman -S plasma-{desktop,mediacenter,nm}

```

É claro, que não é limitado e pode ser expandido para quaisquer níveis sejam necessários:

```
# pacman -S plasma-{workspace{,-wallpapers},pa}

```

#### Instalando grupos de pacotes

Alguns pacotes pertencem a um [grupo de pacotes](/index.php/Criando_pacotes#Pacotes_meta_e_grupos "Criando pacotes") que podem ser instalados simultaneamente. Por exemplo, o comando:

```
# pacman -S gnome

```

solicitará que você selecione os pacotes do grupo [gnome](https://www.archlinux.org/groups/x86_64/gnome/) que você deseja instalar.

Às vezes, um grupo de pacote conterá uma grande quantidade de pacotes, e pode haver só alguns que você quer ou não instalar. Em vez de digitar todos os números, exceto aqueles que você não quer, pode ser mais conveniente selecionar ou excluir pacotes ou intervalos de pacotes com a seguinte sintaxe:

```
Digite uma seleção (padrão=todos): 1-10 15

```

que vai selecionar pacotes 1 até 10 e 15 para a instalação, ou:

```
Digite uma seleção (padrão=todos):: ^5-8 ^2

```

vai selecionar todos os pacotes, exceto 5 até 8 e 2 para a instalação.

Para ver quais pacotes pertencem ao grupo gnome, execute:

```
# pacman -Sg gnome

```

Também visite [https://www.archlinux.org/groups/](https://www.archlinux.org/groups/) para saber quais os grupos de pacotes disponíveis.

**Nota:** Se um pacote na lista já está instalado no sistema, ele será reinstalado mesmo se já estiver atualizado. Este comportamento pode ser substituído com a opção `--needed`.

### Removendo pacotes

Para remover um único pacote, deixando todas as suas dependências instaladas:

```
# pacman -R *nome_pacote*

```

Para remover um pacote e suas dependências que não são exigidas por qualquer outro pacote instalado:

```
# pacman -Rs *nome_pacote*

```

Para remover um pacote, suas dependências e todos os pacotes que dependem deste pacote:

**Atenção:** Esta operação é recursiva, e deve ser usada com cuidado, pois pode remover muitos pacotes potencialmente necessários.

```
# pacman -Rsc *nome_pacote*

```

Para remover um pacote, o qual é exigido por outro pacote, sem remover o pacote dependente:

```
# pacman -Rdd *nome_pacote*

```

O *pacman* salva arquivos de configuração importantes ao remover certos aplicativos e os nomes com a extensão: *.pacsave*. Para prevenir a criação desses arquivos de backup use a opção `-n`:

```
# pacman -Rn *nome_pacote*

```

**Nota:** O *pacman* não removerá as configurações que o próprio aplicativo cria (por exemplo, "dotfiles" na pasta home).

### Atualizando pacotes

**Atenção:**

*   Os usuários devem seguir as orientações em [Manutenção do sistema#Atualizando o sistema](/index.php/Manuten%C3%A7%C3%A3o_do_sistema#Atualizando_o_sistema "Manutenção do sistema") para atualizar os seus sistemas regularmente e nao executar o seguinte comando as cegas.
*   Arch suporta apenas atualizações completa de sistema. Veja [Manutenção do sistema#Sem suporte a atualizações parciais](/index.php/Manuten%C3%A7%C3%A3o_do_sistema#Sem_suporte_a_atualiza.C3.A7.C3.B5es_parciais "Manutenção do sistema") e [#Instalando pacotes](#Instalando_pacotes) para mais detalhes.

O *pacman* pode atualizar todos os pacotes no sistema com apenas um comando. Isso pode demorar um pouco dependendo de como anda a atualização do sistema. Este comando pode sincronizar as bases de dados do repositório *e* atualizar os pacotes do sistema (excluindo pacotes "locais" que não estão nos repositórios configurados):

```
# pacman -Syu

```

### Consultando base de dados de pacotes

O *pacman* consulta a base de dados do pacote local com a opção `-Q`, a base de dados de sincronização com a opção `-S` e a base de dados de arquivos com a opção `-F`. Veja `pacman -Q --help`, `pacman -S --help` e `pacman -F --help` para as respectivas subopções de cada opção.

O *pacman* pode pesquisar por pacotes na base de dados, pesquisando nomes e descrições dos pacotes:

```
$ pacman -Ss *string1* *string2* ...

```

Algumas vezes, ERE (Extended Regular Expressions) incorporadas no `-s` podem causar muitos dos resultados indesejados, então têm que ser limitadas a corresponder ao nome de pacote apenas; não a descrição nem qualquer outro campo:

```
$ pacman -Ss '^vim-'

```

Para procurar os pacotes já instalados:

```
$ pacman -Qs *string1* *string2* ...

```

Para procurar nomes de pacotes em pacotes remotos:

```
$ pacman -Fs *string1* *string2* ...

```

Para exibir informações detalhadas sobre um determinado pacote:

```
$ pacman -Si *nome_pacote*

```

Para os pacotes instalados localmente:

```
$ pacman -Qi *nome_pacote*

```

Inserindo duas opções `-i` também exibirá a lista de arquivos de backup e seus estados de alterações:

```
$ pacman -Qii *nome_pacote*

```

Para obter uma lista dos arquivos instalados por um pacote:

```
$ pacman -Ql *nome_pacote*

```

Para obter uma lista dos arquivos instalados por um pacote remoto:

```
$ pacman -Fl *nome_pacote*

```

Para verificar a presença dos arquivos instalados por um pacote:

```
$ pacman -Qk *nome_pacote*

```

Passando a opção `k` duas vezes, irá ser realizado uma verificação mais aprofundada.

Pode-se também consultar a base de dados para saber qual pacote um arquivo no arquivo do sistema pertence:

```
$ pacman -Qo */caminho/para/nome_de_arquivo*

```

Para consultar o banco de dados para saber de qual pacote remoto um arquivo pertence:

```
$ pacman -Fo */caminho/para/nome_de_arquivo*

```

Para listar todos os pacotes que não são exigidos como dependências (órfãos):

```
$ pacman -Qdt

```

Para listar todos os pacotes explicitamente instalados e que não são necessários como dependências:

```
$ pacman -Qet

```

Para listar a árvore de dependência de um pacote:

```
$ pactree *nome_pacote*

```

Para listar todos os pacotes dependentes de um pacote *instalado*, use *whoneeds* do pacote [pkgtools](https://aur.archlinux.org/packages/pkgtools/):

```
$ whoneeds *nome_pacote*

```

Ou a opção inversa para *pactree*:

```
$ pactree -r *nome_pacote*

```

Veja [Pacman/Dicas e truques](/index.php/Pacman/Dicas_e_truques "Pacman/Dicas e truques") para mais exemplos.

#### Estrutura da base de dados

As bases de dados do *pacman* estão normalmente localizadas em `/var/lib/pacman/sync`. Para cada repositório especificado em `/etc/pacman.conf` haverá um arquivo de base de dados correspondente localizado lá. Os arquivos das bases de dados são arquivos tar-gzipped contendo um diretório para cada pacote, por exemplo, para o pacote [which](https://www.archlinux.org/packages/?name=which):

```
% tree which-2.20-6 
which-2.20-6
|-- depends
`-- desc

```

O arquivo `depends` lista os pacotes que este pacote depende, enquanto a `desc` possui uma descrição do pacote, como o tamanho do arquivo e o hash do MD5.

### Limpando o cache de pacotes

O *pacman* armazena seus pacotes baixados em `/var/cache/pacman/pkg/` e não remove as versões antigas ou desinstaladas automaticamente, portanto, é necessário limpar deliberadamente essa pasta periodicamente para impedir que essa pasta cresça indefinidamente em tamanho.

A opção interna para remover todos os pacotes em cache que não estão instalados atualmente é:

```
# pacman -Sc

```

**Atenção:**

*   Apenas faça isso quando estiver certeza de que as versões anteriores dos pacotes não são mais necessárias, por exemplo, para um [downgrade](/index.php/Downgrade_(Portugu%C3%AAs) "Downgrade (Português)") posterior. `pacman -Sc` deixa as versões dos pacotes atualmente instalados, as versões antigas teriam que ser recuperadas por outros meios, como o [Arch Linux Archive](/index.php/Arch_Linux_Archive_(Portugu%C3%AAs) "Arch Linux Archive (Português)").
*   É possível esvaziar completamente a pasta cache com `pacman -Scc`. Além disso, isso também impede a reinstalação de um pacote diretamente da pasta de cache em caso de necessidade, exigindo um novo download. Isso deve ser evitado a menos que seja necessário ter espaço em disco imediatamente.

Devido às limitações acima, considere uma alternativa para ter mais controle sobre quais pacotes e quantos são excluídos do cache:

O script *paccache*, fornecido pelo próprio pacote [pacman](https://www.archlinux.org/packages/?name=pacman), exclui todas as versões em cache de cada pacote independentemente de estarem instalados ou não, exceto os 3 mais recentes, por padrão:

```
# paccache -r

```

**Dica:** Você pode criar [pacman hooks](/index.php/Pacman_hooks "Pacman hooks") para executar isso automaticamente após cada transação do pacman. Veja [este tópico](https://bbs.archlinux.org/viewtopic.php?pid=1694743#p1694743) para obter exemplos.

Você pode definir quantas versões recentes deseja manter:

```
# paccache -rk 1

```

Para remover todas as versões em cache de pacotes desinstalados, execute novamente *paccache* com:

```
# paccache -ruk0

```

Veja `paccache -h` para mais opções.

[pkgcacheclean](https://aur.archlinux.org/packages/pkgcacheclean/) e [pacleaner](https://aur.archlinux.org/packages/pacleaner/) são duas alternativas.

### Comandos adicionais

Faça o download de um pacote sem instalá-lo:

```
# pacman -Sw *nome_pacote*

```

Instale um pacote "local" que não seja de um repositório remoto (ex., o pacote é do [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)")):

```
# pacman -U */caminho/para/pacote/nome_pacote-versão.pkg.tar.xz*

```

Para manter uma cópia do pacote local no cache do *pacman*, use:

```
# pacman -U file:///*caminho/para/pacote/nome_pacote-versão.pkg.tar.xz*

```

Instale um pacote "remoto" (não de um repositório indicado nos arquivos de configuração do pacman):

```
# pacman -U *http://www.exemplo.com/repo/exemplo.pkg.tar.xz*

```

Para inibir as ações `-S`, `-U` e `-R`, a opção `-p` pode ser usada.

O *pacman* sempre lista os pacotes a serem instalados ou removidos e pede permissão antes de executar.

### Motivo de instalação

A base de dados do *pacman* distingue os pacotes instalados em dois grupos de acordo com o motivo pelo qual eles foram instalados:

*   **instalados explicitamente**: os pacotes foram passados literalmente para um comando genérico *pacman* `-S` ou `-U`;
*   **dependências**: os pacotes que, apesar de nunca (em geral) terem sido passados para um comando de instalação do *pacman*, foram instalados implicitamente porque é [exigido](/index.php/Depend%C3%AAncia "Dependência") por outro pacote que foi instalado explicitamente.

Ao instalar um pacote, é possível forçar o motivo da instalação da *dependência* com:

```
# pacman -S --asdeps *nome_pacote*

```

Ao **re**instalar um pacote, o motivo dessa instalação atual é preservado por padrão.

A lista de pacotes instalados explicitamente pode ser vista com `pacman -Qe`, enquanto a lista de dependências instaladas pode ser vista com `pacman -Qd`.

Para alterar o motivo da instalação de um pacote já instalado, execute:

```
# pacman -D -asdeps *nome_pacote*

```

Use `--asexplicit` para a operação oposta.

**Dica:** A instalação de dependências opcionais com o `--asdeps` o causará de tal forma que, se você [remover pacotes órfãos](/index.php/Pacman/Dicas_e_truques#Removendo_pacotes_n.C3.A3o_usados_.28.C3.B3rf.C3.A3os.29 "Pacman/Dicas e truques"), o *pacman* também removerá as dependências opcionais.

### Pesquisar por um pacote que contenha um arquivo específico

Sincronize a base de dados de arquivos:

```
# pacman -Fy

```

Pesquise por um pacote contendo um arquivo, p.ex.:

```
# pacman -Fs pacman
core/pacman 5.0.1-4
    usr/bin/pacman
    usr/share/bash-completion/completions/pacman
extra/xscreensaver 5.36-1
    usr/lib/xscreensaver/pacman

```

**Dica:** Você pode definir um trabalho cron ou um temporizador do systemd para sincronizar a base de dados de arquivos regularmente.

Para funcionalidade avançada, instale o [pkgfile](/index.php/Pkgfile_(Portugu%C3%AAs) "Pkgfile (Português)"), que usa uma base de dados separada com todos os arquivos e seus pacotes associados.

## Configuração

As configurações do *pacman* estão localizados em `/etc/pacman.conf`: este é o local onde o usuário configura o programa para funcionar da forma desejada. Informações detalhadas sobre o arquivo de configuração pode ser encontrada em [pacman.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.conf.5).

### Opções gerais

Opções gerais estão na seção `[options]`. Leia [pacman(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8) ou olhe no `pacman.conf` padrão para obter informações sobre o que pode ser feito aqui.

#### Comparando versões antes de atualizar

Para ver versões antigas e novas dos pacotes disponíveis, descomente a linha "VerbosePkgLists" em `/etc/pacman.conf`. A saída de `pacman -Syu` será algo como:

```
Pacote (6)            Versão antiga  Versão nova    Alteração   Tamanho de download

extra/libmariadbclient  10.1.9-4     10.1.10-1      0.03 MiB       4.35 MiB
extra/libpng            1.6.19-1     1.6.20-1       0.00 MiB       0.23 MiB
extra/mariadb           10.1.9-4     10.1.10-1      0.26 MiB      13.80 MiB

```

#### Pular pacotes para não serem atualizados

**Atenção:** Tenha cuidado ao pular pacotes, já que não há suporte a [atualizações parciais](/index.php/Atualiza%C3%A7%C3%B5es_parciais "Atualizações parciais").

Para pular a atualização de um pacote específico quando estiver [atualizando](#Atualizando_pacotes) o sistema, faça:

```
IgnorePkg=linux

```

Para vários pacotes use uma lista separada por espaço, ou use adicionais linhas `IgnorePkg`. Além disso, padrões de *glob* podem ser usados. Se você deseja pular pacotes apenas uma vez, você também pode usar a opção `--ignore` na linha de comando - dessa vez com uma lista separada por vírgula.

Ainda será possível atualizar pacotes ignorados usando `pacman -S`: neste caso, *pacman* lhe lembrará de que os pacotes têm incluídos em uma declaração de `IgnorePkg`.

#### Pular um grupos de pacotes para não serem atualizados

**Atenção:** Tenha cuidado ao pular grupos de pacotes, já que não há suporte a [atualizações parciais](/index.php/Atualiza%C3%A7%C3%B5es_parciais "Atualizações parciais").

Tal como acontece com os pacotes, pular um grupo de pacote inteiro também é possível:

```
IgnoreGroup=gnome

```

#### Pular arquivos para não serem instalados no sistema

Para pular sempre a instalação de lista de diretórios sob `NoExtract`. Por exemplo, para evitar a instalação de units de [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") use:

```
NoExtract=usr/lib/systemd/system/*

```

Regras posteriores sobrescrevem as anteriores e podem negar uma regra adicionando antes `!`.

**Dica:** O *pacman* emite mensagens de avisos sobre locales faltando ao atualizar um pacote para os quais os locales foram limpados com *localepurge* ou *bleachbit*. Comentando a opção `CheckSpace` em `pacman.conf` suprime aviso, mas considera que a funcionalidade de verificação de espaço será desabilitada para todos os pacotes.

#### Manter vários arquivos de configuração

Se você tiver vários arquivos de configuração (ex.: configuração principal e configuração com repositório [testing](/index.php/Testing_(Portugu%C3%AAs) "Testing (Português)") habilitado) e você gostaria de compartilhar opções entre configurações, você pode usar a opção `Include` declarada nos arquivos de configuração, ex.:

```
Include = */caminho/para/configurações/comuns*

```

sendo que arquivo `*/caminho/para/configurações/comuns*` contém as mesmas opções para ambas configurações.

#### Hooks

*pacman* pode executar hooks de pré- e pós-transação do diretório `/usr/share/libalpm/hooks/`; mais diretórios podem ser especificados com a opção `HookDir` no `pacman.conf`, que tem como padrão `/etc/pacman.d/hooks`. Nomes de arquivo hook devem ser sufixados com *.hook*.

Para mais informações sobre hooks do alpm, veja [alpm-hooks(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/alpm-hooks.5).

### Repositórios e espelhos

Além da seção especial [[options]](#Op.C3.A7.C3.B5es_gerais), cada outra `[section]` no `pacman.conf` define um repositório de pacote a ser usado. Um *repositório* é uma coleção *lógica* de pacotes, que são armazenados *fisicamente* em um ou mais servidores: por esse motivo, cada servidor é chamado de um *espelho* para o repositório.

Repositórios são distinguidos entre [oficial](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais") e [não oficiais](/index.php/Unofficial_user_repositories "Unofficial user repositories"). A ordem de repositórios no arquivo de configuração importa; repositórios listados primeiro terão precedências sobre os listados posteriormente quando pacotes nos dois repositórios tiverem nomes idênticos, independentemente do número da versão. Para usar um repositório após adicioná-lo, você precisará [atualizar](#Atualizando_pacotes) todo o sistema primeiro.

Cada seção de repositório permite definir a lista de seus espelhos diretamente ou em um arquivo externo por meio da diretiva `Include`: por exemplo, os espelhos para os repositórios oficiais são incluídos no `/etc/pacman.d/mirrorlist`. Veja o artigo [Mirrors](/index.php/Mirrors "Mirrors") para configuração de espelho.

#### Segurança de pacote

O *pacman* oferece suporte a assinaturas de pacotes, que adiciona uma camada extra de segurança para os pacotes. A configuração padrão, `SigLevel = Required DatabaseOptional`, habilita verificação de assinatura para todos os pacotes em um nível global: isso pode ser sobrescrito por linhas `SigLevel` para cada repositório. Para mais detalhes sobre assinatura de pacote e verificação de assinatura, dê uma olhada em [pacman-key](/index.php/Pacman-key_(Portugu%C3%AAs) "Pacman-key (Português)").

## Solução de problemas

### Erro "falha em submeter a transação (arquivos conflitantes)"

Se você vir o erro: [[1]](https://bbs.archlinux.org/viewtopic.php?id=56373)

```
erro: não foi possível preparar transação
erro: falha ao submeter transação (arquivos conflitantes)
*pacote*: */caminho/para/arquivo* existe no sistema de arquivos
Ocorreram erros e, portanto, nenhum pacote foi atualizado.

```

Por que isso aconteceu: o *pacman* detectou um conflito de arquivo e, por design, não vai sobrescrever arquivos para você. Este é um recurso de design, não uma falha.

O problema geralmente é trivial de resolver. Uma maneira segura é primeiro verificar se outro pacote possui o arquivo (`pacman -Qo */caminho/para/arquivo*`). Se o arquivo for de propriedade de outro pacote, [preencha um relatório de erro](/index.php/Diretrizes_de_relat%C3%B3rios_de_erro "Diretrizes de relatórios de erro"). Se o arquivo não for de outro pacote, renomeie o arquivo que "existe no sistema de arquivos" e execute novamente o comando de atualização. Se tudo correr bem, o arquivo pode então ser removido.

Se você instalou um programa manualmente sem usar o *pacman* ou um frontend dele (p.ex.: por meio de `make install`), você tem que removê-lo e todos os seus arquivos para, depois, reinstalar adequadamente usando o *pacman*. Veja também [Pacman/Dicas e truques#Identificar arquivos que pertençam a nenhum pacote](/index.php/Pacman/Dicas_e_truques#Identificar_arquivos_que_perten.C3.A7am_a_nenhum_pacote "Pacman/Dicas e truques").

Todo pacote instalado fornece um arquivo `/var/lib/pacman/local/*$pacote-$versão*/files` que contém metadados sobre esse pacote. Se o arquivo ficar corrompido, vazio ou desaparecer, ele resulta em erros de `existe no sistema de arquivos` ao tentar atualizar o pacote. Tal erro geralmente está relacionado a um pacote. Em vez de renomear manualmente e posteriormente remover todos os arquivos que pertencem ao pacote em questão, você pode tentar excepcionalmente executar `pacman -S --force $pacote` para forçar o *pacman* a sobrescrever esses arquivos.

**Atenção:** Tenha cuidado ao usar a opção `--force` (por exemplo, `pacman -Syu --force`), pois ela pode causar grandes problemas se usada inadequadamente. É altamente recomendado usar essa opção apenas quando as notícias do Arch instruem o usuário a fazê-lo.

### Erro "falha em submeter a transação (pacote inválido ou corrompido)"

Procure por arquivos *.part* (pacotes baixados parcialmente) em `/var/cache/pacman/pkg` e remove-os (muitas vezes causado pelo uso da opção `XferCommand` em `pacman.conf`).

```
# find /var/cache/pacman/pkg/ -iname "*.part" -exec rm {} \;

```

### Erro "falha ao iniciar a transação (não foi possível travar a base de dados)"

Quando o *pacman* vai alterar a base de dados de pacotes, por exemplo instalar um pacote, ele cria um arquivo de trava em `/var/lib/pacman/db.lck`. Isso evita que uma outra instância do *pacman* tente alterar a base de dados de pacotes ao mesmo tempo.

Se o *pacman* for interrompido enquanto altera a base de dados, esse arquivo de trava obsoleto pode permanecer. Se você tem certeza que nenhuma outra instância do *pacman* está em execução, então exclua o arquivo de trava:

```
# rm /var/lib/pacman/db.lck

```

### Pacotes não podem ser obtidos na instalação

Esse erro se manifesta como `não encontrado na base de dados de sincronização`, `alvo não encontrado` ou `falha ao obter o arquivo`.

Primeiramente, assegure-se de que o pacote realmente existe (e cuidado para erros de escrita!). Se você tem certeza que o pacote existe, sua lista de pacote pode estar desatualizada ou seus repositórios podem estar configurados incorretamente. Tente execute `pacman -Syyu` para forçar uma atualização de todas as listas de pacote e atualize.

Pode ser também que aquele repositório contendo o pacote não está habilidade no seu sistema. Por exemplo, o pacote pode estar no repositório *multilib*, mas o *multilib* não está habilitado em seu `pacman.conf`.

Veja também [FAQ (Português)#Por que há alguma uma única versão de cada biblioteca compartilhada nos repositórios oficiais?](/index.php/FAQ_(Portugu%C3%AAs)#Por_que_h.C3.A1_alguma_uma_.C3.BAnica_vers.C3.A3o_de_cada_biblioteca_compartilhada_nos_reposit.C3.B3rios_oficiais.3F "FAQ (Português)").

### Reinstalação manual do pacman

**Atenção:** É extremamente fácil quebrar seu sistema ainda mais, usando essa abordagem. Use isso apenas como um último recurso se o método do [#pacman trava durante uma atualização](#pacman_trava_durante_uma_atualiza.C3.A7.C3.A3o) não for uma opção.

Mesmo se o *pacman* estiver terrivelmente quebrado, você pode corrigi-lo manualmente baixando os últimos pacotes e extraindo-os para os locais corretos. Os passos difíceis a se executar são

1.  Determinar dependências para instalar
2.  Baixar cada pacote de um espelho de sua escolha
3.  Extrair cada pacote para a raiz
4.  Reinstalar esses pacotes com `pacman -Sf` para atualizar a base de dados de pacote
5.  Fazer uma atualização completa do sistema

Se você tem um sistema do Arch saudável disponível, você pode ver a lista completa de dependências com

```
$ pacman -Q $(pactree -u pacman)

```

mas você pode precisar atualizar algumas delas, dependendo do seu problema. Um exemplo de extração de um pacote é

```
# tar -xvpwf *pacote.tar.xz* -C / --exclude .PKGINFO --exclude .INSTALL

```

Note que o uso da opção `w` para modo interativo. Executar não interativamente é muito arriscado já que você pode acabar sobrescrevendo um arquivo importante. Também tenha cuidado ao extrair pacotes na ordem correta (i.e. dependências primeiro). [Essa publicação no fórum](https://bbs.archlinux.org/viewtopic.php?id=95007) contém um exemplo deste processo no qual apenas duas dependências do *pacman* estava quebradas.

### pacman trava durante uma atualização

No caso do *pacman* travar com um erro de "escrita da base de dados" enquanto remove pacotes, e a reinstalação ou atualização de pacotes falha a partir daí, faça o seguinte:

1.  Inicialize usando a mídia de instalação do Arch. Preferivelmente use uma mídia recente, para que a versão do *pacman* seja igual ou mais nova do que a do sistema.
2.  Monte o sistema de arquivos raiz do sistema (ex.: `mount /dev/sdaX /mnt`) como root e verifique se a montagem tem espaço suficiente com `df -h`
3.  Monte os sistemas de arquivos proc e sysfs também: `mount -t {proc,sysfs} /dev/sdaX {/mnt/proc, /mnt/sys}`
4.  Se o sistema usa locais padrão de base de dados e diretório, você pode agora atualizar a base de dados do *pacman* do sistema e atualizá-lo via `pacman --root=/mnt --cachedir=/mnt/var/cache/pacman/pkg -Syyu` como root.
5.  Após a atualização, uma forma de verificar se pacotes não atualizados, mas ainda quebrados: `find /mnt/usr/lib -size 0`
6.  Seguido pela reinstalação de qualquer pacote ainda quebrado via `pacman --root /mnt --cachedir=/mnt/var/cache/pacman/pkg -S *pacote*`.

### Erro "Unable to find root device" após a reinicialização

Muito provavelmente seus initramfs quebrou durante uma atualização do kernel (uso indevido da opção `--force` do *pacman* pode ser uma causa). Você tem duas opções; primeiro, tente a entrada *Fallback*.

**Dica:** No caso de você ter removido o *Fallback*, você pode sempre pressionar a tecla `Tab` quando o gerenciador de boot aparecer (para Syslinux) ou `e` (para GRUB), renomear `initramfs-linux-fallback.img` e pressione `Enter` ou `b` (dependendo do seu gerenciador de boot) para inicializar com os novos parâmetros.

Quando o sistema iniciar, execute este comando (para o Kernel [linux](https://www.archlinux.org/packages/?name=linux) padrão) através do console ou de um terminal para reconstruir a imagem initramfs:

```
# mkinitcpio -p linux

```

Se isso não funcionar, de uma versão atual do Arch (CD/DVD ou pendrive USB), [monte](/index.php/Mount "Mount") as partições *root* e *boot*. Então, faça um [chroot](/index.php/Chroot_(Portugu%C3%AAs) "Chroot (Português)") usando o *arch-chroot*:

```
# arch-chroot /mnt
# pacman -Syu mkinitcpio systemd linux

```

**Nota:**

*   Se você não tem uma versão atual ou se tem apenas alguma outra distribuição Linux "live", você pode fazer [chroot](/index.php/Chroot_(Portugu%C3%AAs) "Chroot (Português)") usando o jeito antigo. Obviamente, terá que digitar mais do que simplesmente executar o script `arch-chroot`.
*   Se *pacman* falhar com `não foi possível resolver máquina`, por favor [verifique sua conexão com a Internet](/index.php/Configura%C3%A7%C3%A3o_de_rede#Verificando_a_conex.C3.A3o "Configuração de rede").
*   Se você não conseguir entrar no ambiente do arch-chroot ou chroot, mas precisa reinstalar os pacotes, você pode usar o comando `pacman -r /mnt -Syu foo bar` para usar o *pacman* em sua partição raiz.

A reinstalação do kernel (o pacote [linux](https://www.archlinux.org/packages/?name=linux)) vai gerar automaticamente a imagem com `mkinitcpio -p linux`. Não precisa fazer separadamente.

Após, recomenda-se que você execute `exit`, `umount /mnt/{boot,}` e `reboot`.

### Assinatura de "<email@exemplo.org>" tem confiança desconhecida, falha na instalação

Você pode tentar:

*   atualizar as chaves conhecidas, executando `pacman-key --refresh-keys`
*   atualizar manualmente o pacote [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) primeiro, i.e. `pacman -Sy archlinux-keyring && pacman -Su`
*   siga [pacman-key (Português)#Redefinindo todas as chaves](/index.php/Pacman-key_(Portugu%C3%AAs)#Redefinindo_todas_as_chaves "Pacman-key (Português)")

### Solicitação de importação de chaves PGP

Se estiver [instalando](/index.php/Guia_de_instala%C3%A7%C3%A3o "Guia de instalação") o Arch com uma ISO desatualizado, você provavelmente terá que importar chaves PGP. Concorde com baixar a chave para proceder. Se você não consegue adicionar a chave PGP com sucesso, atualizar o chaveiro ou atualizar [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) (veja [acima](#Assinatura_de_.22.3Cemail.40exemplo.org.3E.22_tem_confian.C3.A7a_desconhecida.2C_falha_na_instala.C3.A7.C3.A3o)).

### Erro: chave "0123456789ABCDEF" não pôde ser procurado remotamente

Se pacotes forem assinados com novas chaves, que foram adicionadas apenas recentemente ao [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring), essas chaves não estão disponível localmente durante a atualização (problema [ovo ou galinha](https://en.wikipedia.org/wiki/pt:o_ovo_ou_a_galinha "w:pt:o ovo ou a galinha")). O [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) instalado não contém a chave até estar atualizado. Pacman tenta contornar isso procurando em um servidor de chaves, o que pode não ser possível, por exemplo, atrás de proxys ou firewall e resulta no erro informado. Atualize o [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) primeiro como mostrado [acima](#Assinatura_de_.22.3Cemail.40exemplo.org.3E.22_tem_confian.C3.A7a_desconhecida.2C_falha_na_instala.C3.A7.C3.A3o).

### Assinatura de "Usuário <email@archlinux.org>" é inválida, falha na instalação

Quando a hora do sistema está errado, as chaves de assinatura são considerados como expiradas (ou inválidas) e verificações de assinatura em pacotes vão falhar com o erro a seguir:

```
erro: *pacote*: assinatura de "Usuário <email@archlinux.org>" é inválida
erro: falha ao submeter transação (pacote inválido ou corrompido (assinatura PGP))
Ocorreram erros e, portanto, nenhum pacote foi atualizado.

```

Certifique-se de corrigir o [tempo](/index.php/Time "Time"), por exemplo com `ntpd -qg` executado como root, e execute `hwclock -w` como root antes de instalações ou atualizações subsequentes.

### Erro 'aviso: locale atual é inválida; usando locale padrão "C"'

Como a própria mensagem de erro diz, sua locale está configurada incorretamente. Consulte [Locale](/index.php/Locale_(Portugu%C3%AAs) "Locale (Português)").

### pacman não respeita as configurações de proxy

Certifique-se que as variáveis de ambiente relevantes (`$http_proxy`, `$ftp_proxy` etc.) estão configuradas. Se você usa o *pacman* com [sudo](/index.php/Sudo "Sudo"), você precisa configurar o sudo para [passar essas variáveis ​​de ambiente para o pacman](/index.php/Sudo#Environment_variables "Sudo").

### Como faço para reinstalar todos os pacotes, mantendo informações sobre se algo foi explicitamente instalado ou como uma dependência?

Para reinstalar todos os pacotes nativos: `pacman -Qnq | pacman -S -` (a opção `-S` preserva a razão de instalação por padrão).

Então você terá que reinstalar todos os pacotes externos, que podem ser listados com `pacman -Qmq`.

### Erro "cannot open shared object file"

Parece que uma transição anterior do *pacman* removeu ou corrompeu as bibliotecas compartilhadas necessárias para o *pacman* em si.

Para recuperar dessa situação, você precisa desempacotar manualmente as bibliotecas necessárias para seu sistema. Primeiro descubra qual pacote contém a biblioteca em falta e, então, localize-o no cache do *pacman* (`/var/cache/pacman/pkg/`). Desempacote a biblioteca compartilhada necessária no sistema de arquivos. Isso vai permitir executar o *pacman*.

Agora, você precisa [reinstalar](#Instalando_pacotes_espec.C3.ADficos) o pacote quebrado. Note que você precisa usar a opção `--force`, pois você acabou de desempacotar arquivos de sistema e o*pacman* não tem conhecimento deles. O *pacman* vai substituir corretamente nosso arquivo de biblioteca compartilhada com o do pacote.

É isso. Atualize o resto do sistema.

### Congelamento de downloads de pacote

Houve alguns relatos a cerca de problemas de rede que impedem o *pacman* de atualizar/sincronizar repositórios. [[2]](https://bbs.archlinux.org/viewtopic.php?id=68944) [[3]](https://bbs.archlinux.org/viewtopic.php?id=65728) Ao instalar o Arch Linux nativamente, essas questões foram resolvidas substituindo o gerenciador de download de arquivos padrão do *pacman* com um alternativo (veja [Melhorar desempenho do pacman](/index.php/Melhorar_desempenho_do_pacman "Melhorar desempenho do pacman") para mais detalhes). Ao instalar o Arch Linux como um SO hospedeiro no [Virtualbox](/index.php/VirtualBox_(Portugu%C3%AAs) "VirtualBox (Português)"), essa questão também foi resolvido usando *Host interface* em vez de *NAT* nas propriedades da máquina.

### Falha ao obter arquivo 'core.db' do espelho

Se você receber essa mensagem de erro com os [espelhos](/index.php/Mirrors "Mirrors") (*mirrors*) corretos, tente configurar um [servidor de nomes](/index.php/Resolv.conf "Resolv.conf") diferente.

## Veja também

*   [Página inicial do pacman](https://www.archlinux.org/pacman/)
*   [libalpm(3)](http://jlk.fjfi.cvut.cz/arch/manpages/man/libalpm.3)
*   [pacman(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8)
*   [pacman.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.conf.5)
*   [repo-add(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/repo-add.8)