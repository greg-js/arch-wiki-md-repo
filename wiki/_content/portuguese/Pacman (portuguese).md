Artigos relacionados

*   [Criando pacotes](/index.php/Criando_pacotes "Criando pacotes")
*   [Fazendo downgrade de pacotes](/index.php/Fazendo_downgrade_de_pacotes "Fazendo downgrade de pacotes")
*   [pacman/Package signing](/index.php/Pacman/Package_signing "Pacman/Package signing")
*   [pacman/Pacnew e Pacsave](/index.php/Pacman/Pacnew_e_Pacsave "Pacman/Pacnew e Pacsave")
*   [pacman/Restore local database](/index.php/Pacman/Restore_local_database "Pacman/Restore local database")
*   [pacman/Rosetta](/index.php/Pacman/Rosetta "Pacman/Rosetta")
*   [pacman/Tips and tricks](/index.php/Pacman/Tips_and_tricks "Pacman/Tips and tricks")
*   [FAQ (Português)#Gerenciamento de pacote](/index.php/FAQ_(Portugu%C3%AAs)#Gerenciamento_de_pacote "FAQ (Português)")
*   [Manutenção do sistema](/index.php/Manuten%C3%A7%C3%A3o_do_sistema "Manutenção do sistema")
*   [Arch Build System](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)")
*   [Repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais")
*   [Arch User Repository](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)")

O [gerenciador de pacote](https://en.wikipedia.org/wiki/Package_management_system "wikipedia:Package management system") **[pacman](https://www.archlinux.org/pacman/)** é uma das grandes vantagens do Arch Linux. Combina um simples pacote no formato binário, com um fácil uso de [sistema de compilação](/index.php/Arch_Build_System "Arch Build System"). A meta do pacman é tornar o mais fácil possivel gerenciar pacotes, sejam eles dos [oficiais repositórios Arch](/index.php/Official_repositories "Official repositories") ou das próprias compilações do usuário.

Pacman mantém o sistema atualizado, listas de pacotes de sincronização com o servidor mestre. Este modelo servidor/cliente também permite o usuário baixar/instalar pacotes com um simples comando, completo com todas as dependências requeridas.

Pacman é escrito na linguagem de programação C e usa o formato de pacote `.pkg.tar.xz`.

**Dica:** O oficial pacote [pacman](https://www.archlinux.org/packages/?name=pacman) também contém outras ferramentas úteis, tais como o **makepkg**, **pactree**, **vercmp** e mais: execute `pacman -Ql pacman | grep bin` para ver uma lista completa.

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
    *   [3.1 Uma atualização para o pacote XYZ quebrou meu sistema!](#Uma_atualiza.C3.A7.C3.A3o_para_o_pacote_XYZ_quebrou_meu_sistema.21)
    *   [3.2 Eu sei que uma atualização para o pacote ABC foi lançada, mas pacman diz que o meu sistema está atualizado!](#Eu_sei_que_uma_atualiza.C3.A7.C3.A3o_para_o_pacote_ABC_foi_lan.C3.A7ada.2C_mas_pacman_diz_que_o_meu_sistema_est.C3.A1_atualizado.21)
    *   [3.3 Eu recebo um erro durante a atualização: "o arquivo já existe no sistema de arquivos"!](#Eu_recebo_um_erro_durante_a_atualiza.C3.A7.C3.A3o:_.22o_arquivo_j.C3.A1_existe_no_sistema_de_arquivos.22.21)
    *   [3.4 Eu recebo um erro ao instalar um pacote: "não encontrou em sincronia com base de dados"](#Eu_recebo_um_erro_ao_instalar_um_pacote:_.22n.C3.A3o_encontrou_em_sincronia_com_base_de_dados.22)
    *   [3.5 Eu recebo um erro ao instalar um pacote: "alvo não foi encontrado"](#Eu_recebo_um_erro_ao_instalar_um_pacote:_.22alvo_n.C3.A3o_foi_encontrado.22)
    *   [3.6 Pacman está atualizando várias vezes o mesmo pacote!](#Pacman_est.C3.A1_atualizando_v.C3.A1rias_vezes_o_mesmo_pacote.21)
    *   [3.7 Pacman falha durante uma atualização!](#Pacman_falha_durante_uma_atualiza.C3.A7.C3.A3o.21)
    *   [3.8 Eu instalei programa usando "make install"; esses arquivos não pertencem a nenhum pacote!](#Eu_instalei_programa_usando_.22make_install.22.3B_esses_arquivos_n.C3.A3o_pertencem_a_nenhum_pacote.21)
    *   [3.9 Preciso de um pacote com um arquivo específico. Como faço para saber o que ele dispõe?](#Preciso_de_um_pacote_com_um_arquivo_espec.C3.ADfico._Como_fa.C3.A7o_para_saber_o_que_ele_disp.C3.B5e.3F)
    *   [3.10 Pacman está completamente quebrado! Como faço para reinstalá-lo?](#Pacman_est.C3.A1_completamente_quebrado.21_Como_fa.C3.A7o_para_reinstal.C3.A1-lo.3F)
    *   [3.11 Depois de atualizar meu sistema, eu recebo um erro "não é possível encontrar o dispositivo root" depois de reiniciar e o meu sistema não mais inicializará.](#Depois_de_atualizar_meu_sistema.2C_eu_recebo_um_erro_.22n.C3.A3o_.C3.A9_poss.C3.ADvel_encontrar_o_dispositivo_root.22_depois_de_reiniciar_e_o_meu_sistema_n.C3.A3o_mais_inicializar.C3.A1.)
    *   [3.12 Assinatura de "Usuário <email@gmail.com>" e de confiança desconhecida, falha na instalação](#Assinatura_de_.22Usu.C3.A1rio_.3Cemail.40gmail.com.3E.22_e_de_confian.C3.A7a_desconhecida.2C_falha_na_instala.C3.A7.C3.A3o)
    *   [3.13 Recebo "PackageName: assinatura do "User <email@archlinux.org>" é inválida"](#Recebo_.22PackageName:_assinatura_do_.22User_.3Cemail.40archlinux.org.3E.22_.C3.A9_inv.C3.A1lida.22)
    *   [3.14 Recebo um erro "falha ao confirmar a transação (pacote inválido ou corrompido)"](#Recebo_um_erro_.22falha_ao_confirmar_a_transa.C3.A7.C3.A3o_.28pacote_inv.C3.A1lido_ou_corrompido.29.22)
    *   [3.15 Recebo erro toda vez que uso pacman dizendo 'aviso: locale atual é inválida; usando padrão locale "C"'. O que eu faço?](#Recebo_erro_toda_vez_que_uso_pacman_dizendo_.27aviso:_locale_atual_.C3.A9_inv.C3.A1lida.3B_usando_padr.C3.A3o_locale_.22C.22.27._O_que_eu_fa.C3.A7o.3F)
    *   [3.16 Como posso ter Pacman para minhas configurações de proxy?](#Como_posso_ter_Pacman_para_minhas_configura.C3.A7.C3.B5es_de_proxy.3F)
    *   [3.17 Como faço para reinstalar todos os pacotes, mantendo informações sobre se algo foi explicitamente instalado ou como uma dependência?](#Como_fa.C3.A7o_para_reinstalar_todos_os_pacotes.2C_mantendo_informa.C3.A7.C3.B5es_sobre_se_algo_foi_explicitamente_instalado_ou_como_uma_depend.C3.AAncia.3F)
*   [4 Veja também](#Veja_tamb.C3.A9m)

## Uso

O que se segue é apenas uma pequena amostra das operações que o pacman pode executar. Para ler mais exemplos, consulte [pacman(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8).

**Dica:** Para usuários que utilizaram outras distribuições linux antes, ver o artigo [Pacman Rosetta](/index.php/Pacman_Rosetta "Pacman Rosetta") será útil.

### Instalando pacotes

**Nota:** Alguns pacotes muitas vezes têm uma série de [dependências opcionais](/index.php/PKGBUILD_(Portugu%C3%AAs)#optdepends "PKGBUILD (Português)") de pacotes que fornecem funcionalidades adicionais para a aplicação, embora não seja estritamente necessário para executá-lo. Ao instalar um pacote, o *pacman* irá listar suas dependências opcionais entre as mensagens de saída, porém elas não serão encontrados no arquivo `pacman.log`: utilize o comando [pacman -Si](#Consultando_base_de_dados_do_pacote) para visualizar as dependências opcionais de um pacote, juntamente com uma breve descrição das funcionalidades de cada um.

**Atenção:** Ao instalar pacotes no Arch, evite atualizar a lista de pacotes sem [atualizar o sistema](#Atualizando_pacotes) (por exemplo, quando um [pacote não é encontrado](#Eu_recebo_um_erro_ao_instalar_um_pacote:_.22n.C3.A3o_encontrou_em_sincronia_com_base_de_dados.22) nos repositórios oficiais). Na prática, execute o comando `pacman -Sy *nome_pacote*` em vez de `pacman -Sy**u** *nome_pacote*`, pois isso pode levar a problemas de dependências. Veja [Manutenção do sistema#Sem suporte a atualizações parciais](/index.php/Manuten%C3%A7%C3%A3o_do_sistema#Sem_suporte_a_atualiza.C3.A7.C3.B5es_parciais "Manutenção do sistema")

#### Instalando pacotes específicos

Para instalar um único pacote ou lista de pacotes (incluindo dependências), execute o seguinte comando:

```
# pacman -S *nome_pacote1* *nome_pacote2* ...

```

Às vezes, há várias versões de um pacote nos diferentes repositórios, por exemplo [extra] e [testing]. Para instalar a versão anterior, o repositório deve ser definido na frente:

```
# pacman -S extra/*nome_pacote*

```

Para instalar um grupo de pacotes que compartilham padrões em sua nomenclatura, mas sem instalar o grupo inteiro, por exemplo, se for instalar o [plasma](https://www.archlinux.org/groups/x86_64/plasma/), mas apenas alguns pacotes como o plasma-desktop e o plasma-mediacenter, pode se utilizar o comando:

```
# pacman -S *plasma-{desktop,mediacenter}*

```

O comando acima também pode ser usado em subniveis como:

```
# pacman -S *plasma-{workspace{,-wallpapers},pa}*

```

#### Instalando grupos de pacotes

Alguns pacotes pertencem a um grupo de pacotes que podem ser instalados simultaneamente. Por exemplo, o comando:

```
# pacman -S gnome

```

este comando solicitará que você selecione os pacotes do grupo [gnome](https://www.archlinux.org/groups/x86_64/gnome/) que você deseja instalar.

Às vezes, um grupo de pacote conterá uma grande quantidade de pacotes, e pode haver só alguns que você quer ou não instalar. Em vez de digitar todos os números, exceto aqueles que você não quer, pode ser mais conveniente selecionar ou excluir pacotes ou intervalos de pacotes com a seguinte sintaxe:

```
Digite uma seleção (padrão=todos): 1-10 15

```

irá selecionar pacotes 1 até 10 e 15 para a instalação, ou:

```
Digite uma seleção (padrão=todos):: ^5-8 ^2

```

irá selecionar todos os pacotes, exceto 5 até 8 e 2 para a instalação.

Para ver quais pacotes pertencem ao grupo gnome, execute:

```
# pacman -Sg gnome

```

Também visite [https://www.archlinux.org/groups/](https://www.archlinux.org/groups/) para saber quais os grupos de pacotes disponíveis.

**Nota:** Se um pacote na lista já está instalado no sistema, ele será reinstalado mesmo se já estiver atualizado. Este comportamento pode ser substituído com a opção `--needed`.

**Dica:** Ao instalar os pacotes, *não* atualizar a lista de pacotes sem [atualizar o sistema](#Atualizando_pacotes) (ex. `pacman -Sy *package_name*`), isso pode ocasinar erros de dependêcias. Veja [#Atualizações parciais não são suportadas](#Atualiza.C3.A7.C3.B5es_parciais_n.C3.A3o_s.C3.A3o_suportadas) e [https://bbs.archlinux.org/viewtopic.php?id=89328](https://bbs.archlinux.org/viewtopic.php?id=89328).

### Removendo pacotes

Para remover um único pacote, deixando todas as suas dependências instaladas:

```
# pacman -R *package_name*

```

Para remover um pacote e suas dependências que não são exigidas por qualquer outro pacote instalado:

```
# pacman -Rs *package_name*

```

Para remover um pacote, suas dependências e todos os pacotes que dependem deste pacote:

**Atenção:** Esta operação é recursiva, e deve ser usada com cuidado, pois pode remover muitos pacotes potencialmente necessários.

```
# pacman -Rsc *package_name*

```

Para remover um pacote, o qual é exigido por outro pacote, sem remover o pacote dependente:

```
# pacman -Rdd *package_name*

```

O pacman salva arquivos de configuração importantes ao remover certos aplicativos e os nomes com a extensão: `.pacsave`. Para prevenir a criação desses arquivos de backup use a opção `-n`:

```
# pacman -Rn *package_name*

```

**Nota:** Pacman não removerá as configurações que o próprio aplicativo cria (por exemplo, "dotfiles" na pasta home).

### Atualizando pacotes

**Atenção:**

*   Os usuários devem seguir as orientações em [System maintenance (Português)#Atualizando o sistema](/index.php/System_maintenance_(Portugu%C3%AAs)#Atualizando_o_sistema "System maintenance (Português)") para atualizar os seus sistemas regularmente e nao executar o seguinte comando as cegas.
*   Arch suporta apenas atualizações completa de sistema. Veja [System maintenance (Português)#Sem suporte a atualizações parciais](/index.php/System_maintenance_(Portugu%C3%AAs)#Sem_suporte_a_atualiza.C3.A7.C3.B5es_parciais "System maintenance (Português)") e [#Instalando Pacotes](#Instalando_Pacotes) para mais detalhes.

*Pacman* pode atualizar todos os pacotes no sistema com apenas um comando. Isso pode demorar um pouco dependendo de como anda a atualização do sistema. Este comando pode sincronizar as bases de dados do repositório *e* atualizar os pacotes do sistema (excluindo pacotes "locais" que não estão nos repositórios configurados):

```
# pacman -Syu

```

**Dica:** Em vez de logo que as atualizações estiverem disponíveis, os usuários devem reconhecer que, devido à natureza Arch's rolling release, uma atualização pode ter consequências imprevisíveis. Isso significa que não é prudente atualizar se, por exemplo, tem alguma tarefa importante para fazer. Preferencialmente, atualize durante o tempo livre e esteja preparado para lidar com quaisquer problemas que possam surgir.

O Pacman é uma ferramenta de gerenciamento de pacotes poderosa, ao atualizar o sistema, os usuários devem estar atentos e ter a responsabilidade pela manutenção do seu próprio sistema. **Ao realizar uma atualização do sistema, é essencial que os usuários leiam todas as saídas de informações do pacman e usem o bom senso.** Se um arquivo de configuração que foi modificado pelo usuário precisar ser atualizado para uma nova versão de um pacote, um arquivo `.pacnew` será criado para evitar a substituição de configurações alteradas pelo usuário, então, o Pacman pedirá ao usuário para juntá-las. Esses arquivos requerem intervenção manual do usuário e é uma boa prática para lidar com eles logo após cada atualização ou remoção do pacote.

**Dica:** Lembre-se que a saída do pacman é registrada no `/var/log/pacman.log`.

Antes de atualizar, é aconselhável visitar [a página Arch Linux Brasil](https://www.archlinux-br.org/) para verificar as últimas notícias (alternativamente assinar o [[1]](http://www.archlinux-br.org/feeds/news/), [arco-announce mailing list](https://mailman.archlinux.org/mailman/listinfo/arch-announce/), ou seguir [@archlinux](https://twitter.com/archlinux) no Twitter), quando atualizações exigem a intervenção do usuário (mais do que isso pode ser tratada simplesmente seguindo as instruções dadas pelo pacman), uma mensagem de notícias no site será criada.

Se alguém encontrar problemas que não podem ser resolvidos por estas instruções, certifique-se de pesquisar no fórum. É provável que os outros já tenham encontrado o mesmo problema e publicaram as instruções para resolvê-lo.

### Consultando base de dados de pacotes

Pacman consulta a base de dados do pacote local com a flag `-Q`, veja:

```
$ pacman -Q --help

```

e consulte a base de dados de sincronização com a flag `-S`, veja:

```
$ pacman -S --help

```

Pacman pode pesquisar por pacotes na base de dados, pesquisando nomes e descrições dos pacotes:

```
$ pacman -Ss *string1* *string2* ...

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
$ pacman -Si *package_name*

```

Para os pacotes instalados localmente:

```
$ pacman -Qi *package_name*

```

Inserindo duas flags `-i` também exibirá a lista de arquivos de backup e seus estados de alterações:

```
$ pacman -Qii *package_name*

```

Para obter uma lista dos arquivos instalados por um pacote:

```
$ pacman -Ql *package_name*

```

Para pacotes não instalados, use [pkgfile](/index.php/Pkgfile_(Portugu%C3%AAs) "Pkgfile (Português)").

Para obter uma lista dos arquivos instalados por um pacote remoto:

```
$ pacman -Fl *package_name*

```

Para verificar a presença dos arquivos instalados por um pacote:

```
$ pacman -Qk *package_name*

```

Usando duas flags `k`, irá ser realizado uma verificação mais aprofundada.

Pode-se também consultar a base de dados para saber qual pacote um arquivo no arquivo do sistema pertence:

```
$ pacman -Qo */path/to/file_name*

```

Para consultar o banco de dados para saber de qual pacote remoto um arquivo pertence:

```
$ pacman -Fo /path/to/file_name

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
$ pactree *package_name*

```

Para listar todos os pacotes dependentes de um pacote *instalado*, use `whoneeds` do pacote [pkgtools](/index.php/Pkgtools "Pkgtools"):

```
$ whoneeds *package_name*

```

Ou a flag inversa para *pactree*:

```
$ pactree -r *package_name*

```

veja [pacman tips](/index.php/Pacman_tips "Pacman tips") para mais exemplos.

#### Estrutura da base de dados

As bases de dados do pacman estão normalmente localizadas em `/var/lib/pacman/sync`. Para cada repositório especificado em `/etc/pacman.conf` haverá um arquivo de base de dados correspondente localizado lá. Os arquivos das bases de dados são arquivos tar-gzipped contendo um diretório para cada pacote, por exemplo, para o pacote [which](https://www.archlinux.org/packages/?name=which):

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

*   Apenas faça isso quando estiver certeza de que as versões anteriores dos pacotes não são mais necessárias, por exemplo, para um [downgrade](/index.php/Downgrade_(Portugu%C3%AAs) "Downgrade (Português)") posterior. `pacman -Sc` deixa as versões dos pacotes atualmente instalados, as versões antigas teriam que ser recuperadas por outros meios, como o [Archive](/index.php/Archive "Archive") (*Arch Linux Archive*).
*   É possível esvaziar completamente a pasta cache com `pacman -Scc`. Além disso, isso também impede a reinstalação de um pacote diretamente da pasta de cache em caso de necessidade, exigindo um novo download. Isso deve ser evitado a menos que seja necessário ter espaço em disco imediatamente.

Devido às limitações acima, considere uma alternativa para ter mais controle sobre quais pacotes e quantos são excluídos do cache:

O script *paccache*, fornecido pelo próprio pacote [pacman](https://www.archlinux.org/packages/?name=pacman), exclui todas as versões em cache de cada pacote independentemente de estarem instalados ou não, exceto os 3 mais recentes, por padrão:

```
# paccache -r

```

**Dica:**
**Template error:** are you trying to use the = sign? Visit [Help:Template#Escape template-breaking characters](/index.php/Help:Template#Escape_template-breaking_characters "Help:Template") for workarounds.

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
# pacman -Sw *package_name*

```

Instale um pacote local que não seja de um repositório remoto (ex., o pacote é do [Arch User Repository (Português)](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)"):

```
# pacman -U */path/to/package/package_name-version.pkg.tar.xz*

```

Para manter uma cópia do pacote local no cache do pacman, use:

```
# pacman -U *file:///path/to/package/package_name-version.pkg.tar.xz*

```

Instalar um pacote 'remoto' (não de um repositório indicado nos arquivos de configuração do pacman):

```
# pacman -U *http://www.example.com/repo/example.pkg.tar.xz*

```

Para inibir as ações `-S`, `-U` e `-R`, `-p` pode ser usado.

O *pacman* sempre lista os pacotes a serem instalados ou removidos e pede permissão antes de executar.

### Motivo de instalação

A base de dados do *pacman* distingue os pacotes instalados em dois grupos de acordo com o motivo pelo qual eles foram instalados:

*   **Instalados explicitamente**: Os pacotes que foram literalmente instalados com os comandos *pacman* `-S` ou `-U`;
*   **Dependências**: Os pacotes que, apesar de nunca (em geral) terem sido instalados explicitamente através de um comando de instalação do *pacman*, foram instalados implicitamente porque é [exigido](/index.php/Dependency "Dependency") por outro pacote que foi explicitamente instalado.

Ao instalar um pacote, é possível forçar o motivo da instalação da *dependência* com:

```
# pacman -S --asdeps *package_name*

```

Quando reinstalar um pacote, o motivo dessa instalação atual é preservado por padrão.

A lista de pacotes instalados explicitamente pode ser vista com `pacman -Qe`, enquanto a lista de dependências instaladas pode ser vista com `pacman -Qd`.

Para alterar o motivo da instalação de um pacote já instalado, execute:

```
# pacman -D -asdeps *package_name*

```

Use `--asexplicit` para a operação oposta.

**Dica:** A instalação de dependências opcionais com o `--asdeps` o causará de tal forma que, se você remover pacotes órfãos, o pacman também removerá as dependências opcionais.

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

Os ajustes do Pacman estão localizados em `/etc/pacman.conf`. Este é o local onde o usuário configura o programa para funcionar da forma desejada. Informações detalhadas sobre o arquivo de configuração pode ser encontrada em [man pacman.conf](https://www.archlinux.org/pacman/pacman.conf.5.html).

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

O *pacman* oferece suporte a assinaturas de pacotes, que adiciona uma camada extra de segurança para os pacotes. A configuração padrão, `SigLevel = Required DatabaseOptional`, habilita verificação de assinatura para todos os pacotes em um nível global: isso pode ser sobrescrito por linhas `SigLevel` para cada repositório. Para mais detalhes sobre assinatura de pacote e verificação de assinatura, dê uma olhada em [pacman-key](/index.php/Pacman-key "Pacman-key").

## Solução de problemas

### Uma atualização para o pacote XYZ quebrou meu sistema!

Arch Linux é uma distribuição de ponta rolling-release. Atualizações de pacotes disponíveis assim que são considerados estáveis ​​o suficiente para uso geral. No entanto, as atualizações, por vezes, exigem a intervenção do usuário: arquivos de configuração podem precisar ser atualizados, dependências opcionais podem alterar, etc.

A dica mais importante para se lembrar é não "às cegas" atualizar o sistema Arch. Sempre leia a lista de pacotes a serem atualizados. Note se os pacotes "críticos" vão ser atualizados ([linux](https://www.archlinux.org/packages/?name=linux), [xorg-server](https://www.archlinux.org/packages/?name=xorg-server), e assim por diante). Se assim for, é geralmente uma boa idéia verificar se há alguma notícia no [http://www.archlinux-br.org/](http://www.archlinux-br.org/) e verifique as mensagens mais recentes no fórum para ver se as pessoas estão enfrentando problemas com o resultado de uma atualização.

Se uma atualização do pacote é esperada/conhecida por causar de problemas, empacotadores garantirão que pacman exiba uma mensagem apropriada quando o pacote é atualizado. Se enfrentar problemas após uma atualização, verifique a saída do pacman, veja o log (`/var/log/pacman.log`).

Neste ponto, **só depois de garantir que não há nenhuma informação disponível através de pacman, não há nenhuma notícia relativa em [http://www.archlinux-br.org/](http://www.archlinux-br.org/), e não há mensagem no fórum sobre a atualização**, considere a busca de ajuda no fórum, através do [IRC](/index.php/IRC_channel "IRC channel"), ou [fazendo downgrade do pacote problemático](/index.php/Downgrading_packages_(Portugu%C3%AAs) "Downgrading packages (Português)").

### Eu sei que uma atualização para o pacote ABC foi lançada, mas pacman diz que o meu sistema está atualizado!

Espelhos do Pacman não são sincronizados imediatamente. Pode demorar mais de 24 horas antes que uma atualização esteja disponível para você. As únicas opções é ser paciente ou usar outro espelho. [MirrorStatus](https://www.archlinux.org/mirrors/status/) pode ajudar a identificar um espelho atualizado.

### Eu recebo um erro durante a atualização: "o arquivo já existe no sistema de arquivos"!

ASIDE: *Tirado de [https://bbs.archlinux.org/viewtopic.php?id=56373](https://bbs.archlinux.org/viewtopic.php?id=56373) by Misfit138.*

```
error: could not prepare transaction
error: failed to commit transaction (conflicting files)
package: /path/to/file exists in filesystem
Errors occurred, no packages were upgraded.

```

Por que isso está acontecendo: pacman detectou um conflito de arquivo, e pelo projeto, não vai substituir os arquivos para você. Esta é uma característica do projeto, e não um defeito.

O problema é usualmente simples de se resolver. Uma maneira segura é primeiro verificar se outro pacote possui o arquivo (`pacman -Qo /path/to/file`). Se o arquivo é de propriedade de outro pacote, [enviar relatório de bug](/index.php/Reporting_bug_guidelines "Reporting bug guidelines"). Se o arquivo não é propriedade de outro pacote, renomeie o 'existente no sistema de arquivo' e re-execute o comando atualizar. Se tudo correr bem, o arquivo pode então ser removido.

Se você tinha instalado um programa manualmente, sem usar pacman ou interface, você tem que removê-lo e todos os seus arquivos e reinstalar corretamente usando pacman.

Cada pacote instalado fornece arquivo `/var/lib/pacman/local/$package-$version/files` que contém metadata sobre este pacote. Se este arquivo for corrompido - é vazio ou ausente - que resulta no erro "o arquivo existe no sistema de arquivos" durante a atualização do pacote. Esse erro geralmente só diz respeito a um único pacote e, em vez de renomear manualmente e depois remover todos os arquivos que pertencem ao pacote em questão, você pode executar `pacman -S --force $package` para forçar o pacman substituir estes arquivos

**Não** execute `pacman -Syu --force`.

### Eu recebo um erro ao instalar um pacote: "não encontrou em sincronia com base de dados"

Primeiramente, verifique se o pacote realmente existe (e fique atento para os erros de digitação!). Se o determinado pacote existe sua lista de pacotes pode estar desatualizada ou seus repositórios podem estar configurados incorretamente. Tente executar `pacman-Syy.` para forçar uma atualização de todas as listas de pacotes

### Eu recebo um erro ao instalar um pacote: "alvo não foi encontrado"

Primeiramente, verifique se o pacote realmente existe (e fique atento para os erros de digitação!). Se o determinado pacote existe sua lista de pacotes pode estar desatualizada ou seus repositórios podem estar configurados incorretamente. Tente executar `pacman-Syy` para forçar uma atualização de todas as listas de pacotes.
Pode ser também que o repositório que contém o pacote não está ativado em seu sistema, por exemplo, o pacote poderia estar no repositório *multilib*, mas *multilib* não está habilitado em seu *pacman.conf*.

### Pacman está atualizando várias vezes o mesmo pacote!

É devido a entradas duplicadas em `/var/lib/pacman/local/`, tal como duas instâncias `linux`. `pacman -Qi` emite a versão correta, mas `pacman -Qu` reconhece a versão antiga e, portanto, tentará atualizar.

Solução: eliminar a entrada em `/var/lib/pacman/local/`.

**Nota:** A versão 3.4 do pacman deveria exibir um erro de entradas duplicadas, que deveria deixar esta nota obsoleta.

### Pacman falha durante uma atualização!

No caso de colisão do pacman com um erro de "escrita de base de dados" enquanto remove um pacote, e falha ao reinstalar ou atualizar pacotes:

1.  Inicialize usando a mídia de instalação do Arch
2.  Monte seu sistema de arquivos root.
3.  Atualize a base de dados do pacman via `pacman -Syy`.
4.  Reinstale o pacote quebrado via `pacman -r /path/to/root -S package`.

### Eu instalei programa usando "make install"; esses arquivos não pertencem a nenhum pacote!

Se receber um erro "arquivos conflitantes", note que o pacman substituirá manualmente o programa instalado se adicionar com o `--force`, por exemplo,(`pacman -S --force`). Veja [Pacman tips#Identify files not owned by any package](/index.php/Pacman_tips#Identify_files_not_owned_by_any_package "Pacman tips") para um script que procura o arquivo de sistema por arquivos *rejeitados*.

**Atenção:** Tome cuidado ao usar a opção `--force`, pois pode causar problemas graves se usada indevidamente. Recomenda-se usar esta opção apenas quando for requisitada em Arch notícias.

### Preciso de um pacote com um arquivo específico. Como faço para saber o que ele dispõe?

Instale [pkgfile](/index.php/Pkgfile_(Portugu%C3%AAs) "Pkgfile (Português)") que usa um banco de dados separado com todos os arquivos e seus pacotes associados.

### Pacman está completamente quebrado! Como faço para reinstalá-lo?

No caso de pacman está quebrado sem possibilidade de reparo, baixe manualmente os pacotes necessários ([openssl](https://www.archlinux.org/packages/?name=openssl), [libarchive](https://www.archlinux.org/packages/?name=libarchive), e [pacman](https://www.archlinux.org/packages/?name=pacman) e extraia eles no root. O binário pacman será restaurado juntamente com seu arquivo de configuração padrão. Depois disso, reinstale esses pacotes com pacman para manter a integridade do banco de dados do pacote. Informações adicionais e um exemplo de script (desatualizado) que automatiza o processo está disponível nesta [[2]](https://bbs.archlinux.org/viewtopic.php?id=95007) mensagem.

### Depois de atualizar meu sistema, eu recebo um erro "não é possível encontrar o dispositivo root" depois de reiniciar e o meu sistema não mais inicializará.

Muito provavelmente seus initramfs quebrou durante uma atualização do kernel (uso indevido da opção do pacman `--force` pode ser uma causa). Você tem duas opções:

**1.** Tente a entrada *Fallback*.

**Dica:** No caso de você ter removido esta entrada por alguma razão, você pode sempre pressionar a tecla `Tab` quando o gerenciador de boot aparecer (para Syslinux) ou `e` (para GRUB), renomear `initramfs-linux-fallback.img` e pressione `Enter` ou `b` (dependendo do seu gerenciador de boot) para inicializar com os novos parâmetros.

	Quando o sistema iniciar, execute este comando (para amarzenar no Kernel [linux](https://www.archlinux.org/packages/?name=linux)) através do console ou de um terminal para reconstruir a imagem initramfs:

	 `# mkinitcpio -p linux` 

**2.** Se não funcionar, de um lançamento 2012 Arch (CD/DVD ou USB), execute:

**Nota:** Se você não tem uma versão de 2012 ou se tem apenas alguma outra distribuição Linux "live" que possa aplicar [chroot](/index.php/Chroot "Chroot") usando o jeito antigo. Obviamente, não será mais simples que digitando o script `arch-chroot`.

```
# mount /dev/sdxY /mnt         #Sua partição root.
# mount /dev/sdxZ /mnt/boot    #Se usa uma partição /boot separada.
# arch-chroot /mnt
# pacman -Syu mkinitcpio systemd linux
```

	Reinstalando o Kernel (o pacote [linux](https://www.archlinux.org/packages/?name=linux)) irá gerar automaticamente a imagem com `mkinitcpio -p linux`. Não precisa fazer separamente.

	Depois, recomenda-se que você execute `exit`, `umount /mnt/{boot,}` e `reboot`.

**Nota:** Se você não pode entrar no ambiente arch-chroot ou chroot, mas precisa reintalar os pacotes você pode usar o comando `pacman -r /mnt -Syu foo bar` para utilizar pacman em sua partição root.

### Assinatura de "Usuário <email@gmail.com>" e de confiança desconhecida, falha na instalação

Siga [pacman-key#Resetting all the keys](/index.php/Pacman-key#Resetting_all_the_keys "Pacman-key"). Ou pode tentar atualizar manualmente [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) primeiro o pacote, ex. `pacman -S archlinux-keyring`.

### Recebo "PackageName: assinatura do "User <email@archlinux.org>" é inválida"

```
error: PackageName: assinatura do "User <email@archlinux.org>" é inválida
error: falha ao confirmar a transação (pacote inválido ou corrompido (PGP signature))
Erros ocorreram, nenhum pacote foi atualizado. 

```
Isso acontece quando o relógio do sistema está errado. Ajuste a [hora](/index.php/Time "Time") e execute: `# hwclock -w` antes de tentar instalar/atualizar um pacote novamente.}}

### Recebo um erro "falha ao confirmar a transação (pacote inválido ou corrompido)"

Procure por arquivos `*.part` (pacotes baixados parcialmente) em `/var/cache/pacman/pkg` e remove eles (muitas vezes causado pelo uso da opção `XferCommand` em `pacman.conf`).

### Recebo erro toda vez que uso pacman dizendo 'aviso: locale atual é inválida; usando padrão locale "C"'. O que eu faço?

Como a própria mensagem de erro diz, sua locale está configurada incorretamente. Consulte [Locale](/index.php/Locale "Locale").

### Como posso ter Pacman para minhas configurações de proxy?

Certifique-se que as variáveis de ambiente relevantes (`$http_proxy`, `$ftp_proxy` etc.) estão configuradas. Se você usa Pacman com [sudo](/index.php/Sudo "Sudo"), você precisa configurar o sudo para [passar essas variáveis ​​de ambiente para o Pacman](/index.php/Sudo#Environment_variables "Sudo").

### Como faço para reinstalar todos os pacotes, mantendo informações sobre se algo foi explicitamente instalado ou como uma dependência?

Para reinstalar todos os pacotes nativos: `pacman -S $(pacman -Qnq)` (a opção `-S` preserva a razão de instalação por padrão).
Então você terá que reinstalar todos os pacotes externos, que podem ser listados com `pacman -Qmq`.

## Veja também

*   [Common Applications/Utilities#Package management](/index.php/Common_Applications/Utilities#Package_management "Common Applications/Utilities")