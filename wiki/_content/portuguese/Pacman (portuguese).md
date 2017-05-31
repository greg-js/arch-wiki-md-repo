O [gerenciador de pacote](https://en.wikipedia.org/wiki/Package_management_system "wikipedia:Package management system") **[pacman](https://www.archlinux.org/pacman/)** é uma das grandes vantagens do Arch Linux. Combina um simples pacote no formato binário, com um fácil uso de [sistema de compilação](/index.php/Arch_Build_System "Arch Build System"). A meta do pacman é tornar o mais fácil possivel gerenciar pacotes, sejam eles dos [oficiais repositórios Arch](/index.php/Official_repositories "Official repositories") ou das próprias compilações do usuário.

Pacman mantém o sistema atualizado, listas de pacotes de sincronização com o servidor mestre. Este modelo servidor/cliente também permite o usuário baixar/instalar pacotes com um simples comando, completo com todas as dependências requeridas.

Pacman é escrito na linguagem de programação C e usa o formato de pacote `.pkg.tar.xz`.

**Dica:** O oficial pacote [pacman](https://www.archlinux.org/packages/?name=pacman) também contém outras ferramentas úteis, tais como o **makepkg**, **pactree**, **vercmp** e mais: execute `pacman -Ql pacman | grep bin` para ver uma lista completa.

## Contents

*   [1 Configuração](#Configura.C3.A7.C3.A3o)
    *   [1.1 Opções gerais](#Op.C3.A7.C3.B5es_gerais)
        *   [1.1.1 Pular pacotes para não serem atualizados](#Pular_pacotes_para_n.C3.A3o_serem_atualizados)
        *   [1.1.2 Pular um grupos de pacotes para não serem atualizados](#Pular_um_grupos_de_pacotes_para_n.C3.A3o_serem_atualizados)
        *   [1.1.3 Pular arquivos para não serem instalados no sistema](#Pular_arquivos_para_n.C3.A3o_serem_instalados_no_sistema)
    *   [1.2 Repositórios](#Reposit.C3.B3rios)
    *   [1.3 Segurança de pacotes](#Seguran.C3.A7a_de_pacotes)
*   [2 Uso](#Uso)
    *   [2.1 Instalando Pacotes](#Instalando_Pacotes)
        *   [2.1.1 Instalando pacotes específicos](#Instalando_pacotes_espec.C3.ADficos)
        *   [2.1.2 Instalando grupos de pacotes](#Instalando_grupos_de_pacotes)
    *   [2.2 Removendo pacotes](#Removendo_pacotes)
    *   [2.3 Atualizando pacotes](#Atualizando_pacotes)
    *   [2.4 Consultando bancos de dados do pacote](#Consultando_bancos_de_dados_do_pacote)
    *   [2.5 Comandos adicionais](#Comandos_adicionais)
    *   [2.6 Atualizações parciais não são suportadas](#Atualiza.C3.A7.C3.B5es_parciais_n.C3.A3o_s.C3.A3o_suportadas)
*   [3 Solução de problemas](#Solu.C3.A7.C3.A3o_de_problemas)
    *   [3.1 Uma atualização para o pacote XYZ quebrou meu sistema!](#Uma_atualiza.C3.A7.C3.A3o_para_o_pacote_XYZ_quebrou_meu_sistema.21)
    *   [3.2 Eu sei que uma atualização para o pacote ABC foi lançada, mas pacman diz que o meu sistema está atualizado!](#Eu_sei_que_uma_atualiza.C3.A7.C3.A3o_para_o_pacote_ABC_foi_lan.C3.A7ada.2C_mas_pacman_diz_que_o_meu_sistema_est.C3.A1_atualizado.21)
    *   [3.3 Eu recebo um erro durante a atualização: "o arquivo já existe no sistema de arquivos"!](#Eu_recebo_um_erro_durante_a_atualiza.C3.A7.C3.A3o:_.22o_arquivo_j.C3.A1_existe_no_sistema_de_arquivos.22.21)
    *   [3.4 Eu recebo um erro ao instalar um pacote: "não econtrou em sincronia com banco de dados"](#Eu_recebo_um_erro_ao_instalar_um_pacote:_.22n.C3.A3o_econtrou_em_sincronia_com_banco_de_dados.22)
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

## Configuração

Os ajustes do Pacman estão localizados em `/etc/pacman.conf`. Este é o local onde o usuário configura o programa para funcionar da forma desejada. Informações detalhadas sobre o arquivo de configuração pode ser encontrada em [man pacman.conf](https://www.archlinux.org/pacman/pacman.conf.5.html).

### Opções gerais

Opções gerais estão na seção `[options]`. Leia a página de manual ou olhe no padrão `pacman.conf` para obter informações sobre o que pode ser feito aqui.

#### Pular pacotes para não serem atualizados

Para pular a atualização de um pacote específico, faça:

```
IgnorePkg=linux

```

Para vários pacotes use uma lista separada por espaço, ou use adicionais linhas `IgnorePkg`.

#### Pular um grupos de pacotes para não serem atualizados

Tal como acontece com os pacotes, pular um grupo de pacote inteiro também é possível:

```
IgnoreGroup=gnome

```

#### Pular arquivos para não serem instalados no sistema

Para pular sempre a instalação de lista de diretórios sob `NoExtract`. Por exemplo, para evitar a instalação de units [systemd](/index.php/Systemd "Systemd") use:

```
NoExtract=usr/lib/systemd/system/*

```

### Repositórios

A seção define quais [repositórios](/index.php/Official_repositories "Official repositories") usar, como referido no `/etc/pacman.conf`. Podem ser mencionados aqui diretamente ou incluídos de outro arquivo (como `/etc/pacman.d/mirrorlist`), tornando-se assim necessário manter apenas uma lista. Veja [aqui](/index.php/Mirrors "Mirrors") para configuração de espelho.

 `/etc/pacman.conf` 
```
#[testing]
#SigLevel = PackageRequired
#Include = /etc/pacman.d/mirrorlist

[core]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

[extra]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

#[community-testing]
#SigLevel = PackageRequired
#Include = /etc/pacman.d/mirrorlist

[community]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

# If you want to run 32 bit applications on your x86_64 system,
# enable the multilib repositories as required here.

#[multilib-testing]
#SigLevel = PackageRequired
#Include = /etc/pacman.d/mirrorlist

#[multilib]
#SigLevel = PackageRequired
#Include = /etc/pacman.d/mirrorlist

# An example of a custom package repository.  See the pacman manpage for
# tips on creating your own repositories.
#[custom]
#SigLevel = Optional TrustAll
#Server = file:///home/custompkgs
```

Cuidados devem ser tomados ao usar o repositório [testing]. Ele está em desenvolvimento ativo e a atualização pode fazer que alguns pacotes parem de funcionar. As pessoas que usam o repositório [testing] são encorajadas a se increver em [arch-dev-public mailing list](https://mailman.archlinux.org/mailman/listinfo/arch-dev-public) para obter informações atualizadas.}}

### Segurança de pacotes

Pacman suporta 4 assinaturas de pacotes, que adiciona um nível extra de segurança para os pacotes. A configuração padrão, `SigLevel = Required DatabaseOptional`, habilita a verificação de assinaturas para todos os pacotes em um nível global: este pode ser substituido por linhas por repositório `SigLevel`, como mostrado acima. Para mais detalhes sobre pacote de assinatura e verificação de assinatura, dê uma olhada em [pacman-key](/index.php/Pacman-key "Pacman-key").

## Uso

O que se segue é apenas uma pequena amostra das operações que o pacman pode executar. Para ler mais exemplos, consulte [man pacman](https://www.archlinux.org/pacman/pacman.8.html).

### Instalando Pacotes

#### Instalando pacotes específicos

Para instalar um único pacote ou lista de pacotes (incluindo dependências), execute o seguinte comando:

```
# pacman -S *nome_pacote1* *nome_pacote2* ...

```

Às vezes, há várias versões de um pacote nos diferentes repositórios, por exemplo [extra] e [testing]. Para instalar a versão anterior, o repositório deve ser definido na frente:

```
# pacman -S extra/*nome_pacote*

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

**Dica:** Ao instalar os pacotes, *não* atualiza a lista de pacotes sem [atualização](#Upgrading_packages) do sistema (ex. `pacman -Sy *package_name*`), isso pode ocasinar erros de dependêcias. Veja [#Partial upgrades are unsupported](#Partial_upgrades_are_unsupported) e [https://bbs.archlinux.org/viewtopic.php?id=89328](https://bbs.archlinux.org/viewtopic.php?id=89328).

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

**Dica:** Esta operação é recursiva, e deve ser usada com cuidado, pois pode remover muitos pacotes potencialmente necessários.

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

Pacman pode atualizar todos os pacotes no sistema com apenas um comando. Isso pode demorar um pouco dependendo de como anda a atualização do sistema. Este comando pode sincronizar as bases de dados do repositório *e* atualizar os pacotes do sistema (excluindo pacotes "locais" que não estão nos repositórios configurados):

```
# pacman -Syu

```

**Dica:** Em vez de logo que as atualizações estiverem disponíveis, os usuários devem reconhecer que, devido à natureza Arch's rolling release, uma atualização pode ter consequências imprevisíveis. Isso significa que não é prudente atualizar se, por exemplo, tem alguma tarefa importante para fazer. Preferencialmente, atualize durante o tempo livre e esteja preparado para lidar com quaisquer problemas que possam surgir.

Pacman é uma ferramenta de gerenciamento de pacotes poderosa, mas não tenta lidar com todos os casos. Leia [The Arch Way (Português)](/index.php/The_Arch_Way_(Portugu%C3%AAs) "The Arch Way (Português)") se estiver confuso. Os usuários devem estar atentos e ter a responsabilidade pela manutenção do seu próprio sistema. **Ao realizar uma atualização do sistema, é essencial que os usuários leiam todas as saídas de informações do pacman e usem o bom senso.** Se um arquivo de configuração do modificado pelo usuário precisa ser atualizado para uma nova versão de um pacote, um arquivo `.pacnew` será criado para evitar a substituição de configurações alteradas pelo usuário. Pacman pedirá ao usuário para juntá-las. Esses arquivos requerem intervenção manual do usuário e é uma boa prática para lidar com eles logo após cada atualização ou remoção do pacote. Veja [Pacnew e arquivos Pacsave](/index.php?title=Pacnew_e_arquivos_Pacsave&action=edit&redlink=1 "Pacnew e arquivos Pacsave (page does not exist)") para mais informações.

**Dica:** Lembre-se que a saída do pacman é registrada no `/var/log/pacman.log`.

Antes de atualizar, é aconselhável visitar [a página Arch Linux Brasil](https://http://www.archlinux-br.org/) para verificar as últimas notícias (alternativamente assinar o [[1]](http://www.archlinux-br.org/feeds/news/), [arco-announce mailing list](https://mailman.archlinux.org/mailman/listinfo/arch-announce/), ou seguir [@ archlinux](https://twitter.com/archlinux) no Twitter), quando atualizações exigem a intervenção do usuário (mais do que isso pode ser tratada simplesmente seguindo as instruções dadas pelo pacman), uma mensagem de notícias no site será criada.

Se alguém encontrar problemas que não podem ser resolvidos por estas instruções, certifique-se de pesquisar no fórum. É provável que os outros já tenham encontrado o mesmo problema e publicaram as instruções para resolvê-lo.

### Consultando bancos de dados do pacote

Pacman consulta o banco de dados do pacote local com a flag `-Q`, veja:

```
$ pacman -Q --help

```

e consulte o bancos de dados de sincronização com a flag `-S`, veja:

```
$ pacman -S --help

```

Pacman pode pesquisar por pacotes no banco de dados, pesquisando nomes e descrições dos pacotes:

```
$ pacman -Ss *string1* *string2* ...

```

Para procurar os pacotes já instalados:

```
$ pacman -Qs *string1* *string2* ...

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

Para obter uma lista dos arquivos instalados por um pacote

```
$ pacman -Ql *package_name*

```

Para pacotes não instalados, use [pkgfile](/index.php/Pkgfile "Pkgfile").

Pode-se também consultar o banco de dados para saber qual pacote um arquivo no arquivo do sistema pertence:

```
$ pacman -Qo */path/to/file_name*

```

Para listar todos os pacotes não são exigidos como dependências (órfãos):

```
$ pacman -Qdt

```

Para listar a árvore de dependência de um pacote:

```
$ pactree *package_name*

```

Para listar todos os pacotes dependentes de um pacote *instalado*, use `whoneeds` do pacote [pkgtools](/index.php/Pkgtools "Pkgtools"):

```
$ whoneeds *package_name*

```

### Comandos adicionais

Atualizar o sistema e instalar uma lista de pacotes:

```
# pacman -Syu *package_name1* *package_name2* ...

```

Baixe um pacote sem instalá-lo:

```
# pacman -Sw *package_name*

```

Instale um pacote 'local' que não é de um repositório remoto (ex., o pacote é do [Arch User Repository (Português)](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)"):

```
# pacman -U /path/to/package/package_name-version.pkg.tar.xz

```

**Dica:** Para manter uma cópia do pacote local no cache do pacman, use:
```
# pacman -U file://path/to/package/package_name-version.pkg.tar.xz

```

Instalar um pacote 'remoto' (não de um repositório indicado nos arquivos de configuração do pacman):

```
# pacman -U http://www.example.com/repo/example.pkg.tar.xz

```

Limpe o cache de pacotes que não estão instalados (`/var/cache/pacman/pkg`):

**Dica:** Só faça isso se tem certeza que os pacotes instalados são estáveis ​​e que o [downgrade](/index.php/Downgrading_packages "Downgrading packages") não será necessário, já que removerá todas as versões anteriores da pasta cache, deixando apenas as versões dos pacotes que estão instalados atualmente. Tendo versões mais antigas de pacote vem a calhar no caso de uma futura atualização provocar um erro.

```
# pacman -Sc

```

Limpe o cache do pacote inteiro:

**Dica:** Este limpa todo o cache de pacote. Fazer isso é considerado uma má prática, que evita a possibilidade de downgrade de alguma coisa diretamente da pasta cache. Os usuários serão forçados a ter que usar uma fonte alternativa de pacotes obsoletos tais como o [Arch Rollback Machine](/index.php/Downgrading_packages#ARM "Downgrading packages").

```
# pacman -Scc

```

**Dica:** Como alternativa tanto para o `-Sc` e `-Scc`, considere usar `paccache` do [pacman](https://www.archlinux.org/packages/?name=pacman). Isso oferece mais controle sobre o que e quantos pacotes são apagados. Execute `paccache -h` para obter instruções.

### Atualizações parciais não são suportadas

Arch é um rolling release, e novas versões de [bibliotecas](https://en.wikipedia.org/wiki/Library_(computing) serão colocadas nos repositórios. Os desenvolvedores e usuários confiáveis reconstruirão todos os pacotes nos repositórios que precisam ser reconstruídos com as bibliotecas. Se o sistema tem pacotes instalados localmente (tal como pacotes [[Arch User Repository (Português)]), os usuários deverão recontruí-los quando suas dependências receberem uma colisão [soname](https://en.wikipedia.org/wiki/soname "wikipedia:soname").

Isso significa que as atualizações parciais são **não suportadas**. Não use `pacman -Sy package` ou equivalente como `pacman -Sy` e depois `pacman -S package`. Sempre atualize antes de instalar um pacote -- especialmente se o pacman atualizou as sincronização de repositórios. Tenha muito cuidado ao usar `IgnorePkg` e `IgnoreGroup`, pelo mesmo motivo.

Se um cenário de atualização parcial foi criado e os binários estão quebrados porque não conseguem encontrar as bibliotecas que estão ligadas, **não "conserte" o problema simplesmente pelo symlinking**. Bibliotecas recebem colisões [soname](https://en.wikipedia.org/wiki/soname "wikipedia:soname") quando elas **não são compatíveis**. Um simples `pacman -Syu` para um espelho devidamente sincronizado resolverá o problema, desde que pacman não esteja quebrado.

## Solução de problemas

### Uma atualização para o pacote XYZ quebrou meu sistema!

Arch Linux é uma distribuição de ponta rolling-release. Atualizações de pacotes disponíveis assim que são considerados estáveis ​​o suficiente para uso geral. No entanto, as atualizações, por vezes, exigem a intervenção do usuário: arquivos de configuração podem precisar ser atualizados, dependências opcionais podem alterar, etc.

A dica mais importante para se lembrar é não "às cegas" atualizar o sistema Arch. Sempre leia a lista de pacotes a serem atualizados. Note se os pacotes "críticos" vão ser atualizados ([linux](https://www.archlinux.org/packages/?name=linux), [xorg-server](https://www.archlinux.org/packages/?name=xorg-server), e assim por diante). Se assim for, é geralmente uma boa idéia verificar se há alguma notícia no [http://www.archlinux-br.org/](http://www.archlinux-br.org/) e verifique as mensagens mais recentes no fórum para ver se as pessoas estão enfrentando problemas com o resultado de uma atualização.

Se uma atualização do pacote é esperada/conhecida por causar de problemas, empacotadores garantirão que pacman exiba uma mensagem apropriada quando o pacote é atualizado. Se enfrentar problemas após uma atualização, verifique a saída do pacman, veja o log (`/var/log/pacman.log`).

Neste ponto, **só depois de garantir que não há nenhuma informação disponível através de pacman, não há nenhuma notícia relativa em [http://www.archlinux-br.org/](http://www.archlinux-br.org/), e não há mensagem no fórum sobre a atualização**, considere a busca de ajuda no fórum, através [IRC](/index.php/IRC_channel "IRC channel"), ou [downgrade do pacote problemático](/index.php/Downgrading_packages "Downgrading packages").

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

### Eu recebo um erro ao instalar um pacote: "não econtrou em sincronia com banco de dados"

Primeiramente, verifique se o pacote realmente existe (e fique atento para os erros de digitação!). Se o determinado pacote existe sua lista de pacotes pode estar desatualizada ou seus repositórios podem estar configurados incorretamente. Tente executar `pacman-Syy.` para forçar uma atualização de todas as listas de pacotes

### Eu recebo um erro ao instalar um pacote: "alvo não foi encontrado"

Primeiramente, verifique se o pacote realmente existe (e fique atento para os erros de digitação!). Se o determinado pacote existe sua lista de pacotes pode estar desatualizada ou seus repositórios podem estar configurados incorretamente. Tente executar `pacman-Syy` para forçar uma atualização de todas as listas de pacotes.
Pode ser também que o repositório que contém o pacote não está ativado em seu sistema, por exemplo, o pacote poderia estar no repositório *multilib*, mas *multilib* não está habilitado em seu *pacman.conf*.

### Pacman está atualizando várias vezes o mesmo pacote!

É devido a entradas duplicadas em `/var/lib/pacman/local/`, tal como duas instâncias `linux`. `pacman -Qi` emite a versão correta, mas `pacman -Qu` reconhece a versão antiga e, portanto, tentará atualizar.

Solução: eliminar a entrada em `/var/lib/pacman/local/`.

**Nota:** A versão 3.4 do pacman deveria exibir um erro de entradas duplicadas, que deveria deixar esta nota obsoleta.

### Pacman falha durante uma atualização!

No caso de colisão do pacman com um erro de "escrita de banco de dados" equanto remove um pacote, e falha ao reinstalar ou atualizar pacotes:

1.  Inicialize usando a mídia de instalação do Arch
2.  Monte seu sistema de arquivos root.
3.  Atualize o banco de dados do pacman via `pacman -Syy`.
4.  Reinstale o pacote quebrado via `pacman -r /path/to/root -S package`.

### Eu instalei programa usando "make install"; esses arquivos não pertencem a nenhum pacote!

Se receber um erro "arquivos conflitantes", note que o pacman substituirá manualmente o programa instalado se adicionar com o `--force`, por exemplo,(`pacman -S --force`). Veja [Pacman tips#Identify files not owned by any package](/index.php/Pacman_tips#Identify_files_not_owned_by_any_package "Pacman tips") para um script que procura o arquivo de sistema por arquivos *rejeitados*.

**Atenção:** Tome cuidado ao usar a opção `--force`, pois pode causar problemas graves se usada indevidamente. Recomenda-se usar esta opção apenas quando for requisitada em Arch notícias.

### Preciso de um pacote com um arquivo específico. Como faço para saber o que ele dispõe?

Instale [pkgfile](/index.php/Pkgfile "Pkgfile") que usa um banco de dados separado com todos os arquivos e seus pacotes associados.

### Pacman está completamente quebrado! Como faço para reinstalá-lo?

No caso de pacman está quebrado sem possibilidade de reparo, baixe manualmente os pacotes necessários ([openssl](https://www.archlinux.org/packages/?name=openssl), [libarchive](https://www.archlinux.org/packages/?name=libarchive), e [pacman](https://www.archlinux.org/packages/?name=pacman)) e extraia eles no root. O binário pacman será restaurado juntamente com seu arquivo de configuração padrão. Depois disso, reinstale esses pacotes com pacman para manter a integridade do banco de dados do pacote. Informações adicionais e um exemplo de script (desatualizado) que automatiza o processo está disponível nesta [[2]](https://bbs.archlinux.org/viewtopic.php?id=95007) mensagem.

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