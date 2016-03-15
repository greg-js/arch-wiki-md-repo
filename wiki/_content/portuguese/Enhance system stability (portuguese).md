O objetivo deste artigo é dar dicas de como tornar seu sistema Arch Linux o mais estável possível. Mesmo com os desenvolvedores do Arch e seus usuários confiáveis(Trusted Users) trabalhando para produzir pacotes de grande qualidade, devido a natureza rolling release do Arch Linux e evolução rápida dos pacotes, esta distribuição pode não ser a mais adequada para ambientes de missão crítica e comerciais.

Contudo, o Arch internalizou a estabilidade devido a sua simplicidade de configuração, junto com um ciclo de criação e resolução de bugs bastante rápido e o uso de códigos-fonte sem muita aplicação de patches. E, seguindo as instruções abaixo de configuração e manutenção do Arch, o usuário desfrutará de um sistema bastante estável. Como adicional, também serão passadas dicas que tornarão mais fáceis os reparos futuros devido a um mal funcionamento do sistema.

O quão estável o Arch Linux pode ser? Existem diversos relatórios nos fóruns do Arch de Administradores habilidosos com bastante sucesso ao utilizá-lo em servidores de produção. Archlinux.org é um destes exemplos. No desktop, um sistema bem configurado e mantido pode oferecer excelente estabilidade.

## Contents

*   [1 Configurando o Arch](#Configurando_o_Arch)
    *   [1.1 Dicas específicas do Arch](#Dicas_espec.C3.ADficas_do_Arch)
        *   [1.1.1 Mantendo pacotes antigos em uma partição /var grande](#Mantendo_pacotes_antigos_em_uma_parti.C3.A7.C3.A3o_.2Fvar_grande)
        *   [1.1.2 Utilize as configurações recomendadas](#Utilize_as_configura.C3.A7.C3.B5es_recomendadas)
        *   [1.1.3 Seja cuidadoso com pacotes não-oficiais e menos testados](#Seja_cuidadoso_com_pacotes_n.C3.A3o-oficiais_e_menos_testados)
        *   [1.1.4 Utilize espelhos atualizados](#Utilize_espelhos_atualizados)
        *   [1.1.5 Evite pacotes de desenvolvimento](#Evite_pacotes_de_desenvolvimento)
        *   [1.1.6 Instale o pacote linux-lts](#Instale_o_pacote_linux-lts)
    *   [1.2 Melhores práticas genéricas](#Melhores_pr.C3.A1ticas_gen.C3.A9ricas)
        *   [1.2.1 Utilize o gerenciador de pacotes para instalar software](#Utilize_o_gerenciador_de_pacotes_para_instalar_software)
        *   [1.2.2 Utilize pacotes mainstream e comprovados](#Utilize_pacotes_mainstream_e_comprovados)
        *   [1.2.3 Escolha drivers de código aberto](#Escolha_drivers_de_c.C3.B3digo_aberto)
*   [2 Dando manutenção ao Arch](#Dando_manuten.C3.A7.C3.A3o_ao_Arch)
    *   [2.1 Dicas específicas do Arch](#Dicas_espec.C3.ADficas_do_Arch_2)
        *   [2.1.1 Atualize todo o sistema com frequência](#Atualize_todo_o_sistema_com_frequ.C3.AAncia)
        *   [2.1.2 Leia antes de atualizar o sistema](#Leia_antes_de_atualizar_o_sistema)
        *   [2.1.3 Tome ações em alertas durante uma atualização](#Tome_a.C3.A7.C3.B5es_em_alertas_durante_uma_atualiza.C3.A7.C3.A3o)
        *   [2.1.4 Gerencie antecipatamente arquivos .pacnew, .pacsave e .pacorig](#Gerencie_antecipatamente_arquivos_.pacnew.2C_.pacsave_e_.pacorig)
        *   [2.1.5 Considere a utilização do pacmatic](#Considere_a_utiliza.C3.A7.C3.A3o_do_pacmatic)
        *   [2.1.6 Evite certos comandos do pacman](#Evite_certos_comandos_do_pacman)
        *   [2.1.7 Revertendo pacotes que causaram instabilidade](#Revertendo_pacotes_que_causaram_instabilidade)
        *   [2.1.8 Faça backups periódicos da lista de pacotes instalados](#Fa.C3.A7a_backups_peri.C3.B3dicos_da_lista_de_pacotes_instalados)
        *   [2.1.9 Faça backups periódicos do banco de dados de pacotes](#Fa.C3.A7a_backups_peri.C3.B3dicos_do_banco_de_dados_de_pacotes)
            *   [2.1.9.1 Automação no systemd](#Automa.C3.A7.C3.A3o_no_systemd)
    *   [2.2 Melhores práticas genéricas](#Melhores_pr.C3.A1ticas_gen.C3.A9ricas_2)
        *   [2.2.1 Inscreva-se nas listas NVD/CVE e apenas atualize em alertas de segurança](#Inscreva-se_nas_listas_NVD.2FCVE_e_apenas_atualize_em_alertas_de_seguran.C3.A7a)
        *   [2.2.2 Teste as atualizações em sistemas não-críticos](#Teste_as_atualiza.C3.A7.C3.B5es_em_sistemas_n.C3.A3o-cr.C3.ADticos)
        *   [2.2.3 Sempre execute backup de arquivos de configuração antes de editar](#Sempre_execute_backup_de_arquivos_de_configura.C3.A7.C3.A3o_antes_de_editar)
        *   [2.2.4 Faça backups períodicos dos diretórios /etc, /home, /srv, e /var](#Fa.C3.A7a_backups_per.C3.ADodicos_dos_diret.C3.B3rios_.2Fetc.2C_.2Fhome.2C_.2Fsrv.2C_e_.2Fvar)

## Configurando o Arch

Quando efetuamos a instalação e configuração do Arch Linux, existe uma variedade de opções de configuração que devemos fazer, de software ou drivers. Todas estas escolhas impactam diretamente na estabilidade do sistema.

### Dicas específicas do Arch

#### Mantendo pacotes antigos em uma partição /var grande

O Pacman mantém todos os pacotes previamente instalados no caminho `/var/cache/pacman/pkg`, que pode crescer para alguns GB em tamanho. Se você irá configurar partições separadas durante a instalação, tenha a certeza de alocar bastante espaço no /var. De 4 a 8 GB poderá ser suficiente, contudo um espaço maior pode ser necessário para servidores. Manter estes pacotes é útil em um caso onde uma atualização pode causar instabilidade, requerendo um downgrade para uma versão antiga do pacote problemático. Veja a seção [#Revertendo pacotes que causaram instabilidade](#Revertendo_pacotes_que_causaram_instabilidade)

#### Utilize as configurações recomendadas

O documento de instalação detalhada do Arch Linux geralmente exibe mais de uma forma de configurar uma característica específica do sistema. Sempre utilize a configuração padrão recomendada quando configurar seu sistema. Esta configuração sempre reflete as melhores práticas, escolhidas para um sistema de maior estabilidade e de mais fácil reparo.

#### Seja cuidadoso com pacotes não-oficiais e menos testados

Evite utilizar qualquer repositório de testes, ou pacotes vindo destes. Estes pacotes experimentais são para tais fins(testes e desenvolvimento) e não são adequados para um sistema estável

Seja precavido ao utilizar pacotes vindos do AUR. A maioria destes pacotes são disponibilizados por usuários e pode não possuir a mesma qualidade de empacotamento dos repositórios oficiais. Sempre verifique o PKGBUILD do AUR buscando qualquer erro ou código malicioso antes de criar e instalar tais pacotes.

Seja também cuidadoso com os [AUR helpers](/index.php/AUR_helpers "AUR helpers") que simplificam bastante a instalação de pacotes vindos do AUR e podem induzir a criação e instalação de pacotes mal formatados ou com PKGBUILD de conteúdo malicioso. **Sempre** verifique a sanidade de um PKGBUILD antes de criar e/ou instalar um pacote.

Por último, é bastante imprudente utilizar um [AUR helpers](/index.php/AUR_helpers "AUR helpers") ou o comando [makepkg](/index.php/Makepkg "Makepkg") como root.

Apenas utilize repositórios de terceiros se for absolutamente necessário e se você sabe o que está fazendo. Sempre busque fontes confiáveis sobre tais repositórios.

#### Utilize espelhos atualizados

Utilize espelhos que são atualizados com mais frequência para os pacotes do FTP principal do Arh Linux. Verifique o site [status do espelho](https://www.archlinux.org/mirrors/status/) para verificar se o escolhido por você está atualizado. Utilizando espelhos que possuem um rsync recente garante que seu sistema poderá obter os pacotes mais recentes bem como bancos de dados de pacotes disponíveis mais rapidamente, tendo-os já sincronizados em caso de uma manutenção.

E se você se sentir confortável, edite a lista de espelhos em `/etc/pacman.d` colocando os locais(que estão na sua região/seu país) no topo da lista. Veja a página [habilitando seu espelho favorito](/index.php/Mirrors#Enabling_your_favorite_mirror "Mirrors") para maiores detalhes, incluindo a instalação do script [rankmirrors](/index.php/Mirrors#List_by_speed "Mirrors") que avaliará os espelhos mais rápidos. Estes passos grantem que você utilizará os espelhos mais rápidos e confiáveis.

Após alterar um repositório, atualize seu sistema através de um pacman -Syu.

#### Evite pacotes de desenvolvimento

Para evitar problemas sérios ao sistema, não instale pacotes de desenvolvimento, que são geralmente encontrados no AUR e ocasionalmente, no community. Estes pacotes são obtidos diretamente de seus repositórios de desenvolvimento, e possuem alguma palavra relacionada a desenvolvimento como sufixo dos nomes: dev, devel, svn, cvs, git, hg, bzr, ou darcs.

Especialmente, evite instalar versões de desenvolvimento de pacotes cruciais ao sistema como kernel ou glibc.

Se estiver criando um pacote personalizado utilizando o makepkg, esteja certo de seguir os [Arch packaging standards](/index.php/Arch_packaging_standards "Arch packaging standards"), ao montar um PKGBUILD. Utilize o namcap para verificar o .tar.gz ou PKGBUILD

#### Instale o pacote linux-lts

O pacote [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) é uma alternativa de kernel para o Arch baseado no Linux 3.0 e está disponível no repositório [core]. Esta versão do kernel em particular possui a sigla LTS(**l**ong-**t**erm **s**upport) que possui atualizações de códigos-fonte relacionados a segurança, e backports de funcionalidades de kernels mais novos para esta versão, sendo especialmente útil a usuários do Arch buscando por um kernel para servidor, e que não desejam utilizar o fallback caso uma nova versão de kernel dê problemas.

Para disponibilizar esta opção no boot, você necessitará atualizar a configuração do seu bootloader. Por exemplo, se você utiliza o [Syslinux](/index.php/Syslinux "Syslinux"), deverá editar o `/boot/syslinux/syslinux.cfg` e duplicar as entradas exceto pela alteração da imagem em initramfs para `vmlinuz-linux-lts` e `initramfs-linux-lts.img`. Para o [GRUB](/index.php/GRUB "GRUB"), o método recomendado é [gerar um novo .cfg](/index.php/GRUB#Generate_GRUB2_BIOS_Config_file "GRUB") automaticamente.

Alguns preferem instalar o pacote [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) como um adicional ao pacote [linux](https://www.archlinux.org/packages/?name=linux), e apontar a entrada "Fallback" de bootloader para o kernel LTS.

### Melhores práticas genéricas

#### Utilize o gerenciador de pacotes para instalar software

O gerenciador de pacotes (no Arch: [pacman](/index.php/Pacman "Pacman")) faz o serviço melhor que você de rastrear e manter arquivos. Se você instalar software manualmente logo você *irá* esquecer o que fez, e cedo ou tarde instalará mais software que conflitará e desorganizará tudo.

Do ponto de vista da estabilidade, você deve tentar evitar pacotes não suportados e software customizado, mas se você realmente precisa destes softwares o ideal é criar um pacote ao invés de compilar e instalar manualmente.

Desabilite o comando make install(que geralmente é o início dos problemas) dentro de /root/.bashrc

```
 make() {
   [ "$1" == 'install' ] &&
     echo -e "AVISO:
NÃO INSTALE SOFTWARE MANUALMENTE
NÃO USE unset make PARA SOBRESCREVER" &&
     echo "Dica: É fácil criar seus próprios pacotes. Veja: man PKGBUILD makepkg" &&
     return 1;
   /usr/bin/make $@;
 }

```

#### Utilize pacotes mainstream e comprovados

Instale softwares mainstream e de maturidade comprovada. Além de evitar softwares cutting edge que tendem a possuir mais bugs, evite as versões "ponto zero", aka x.y.0 de uma determinada versão de software. Por exemplo, ao instalar o software foobar 2.5.0 espere pela versão 2.5.1\. Não padronize e utilize software novo sem que comprovada sua estabilidade e confiabilidade através de testes. Por exemplo, as primeiras versões do PulseAudio tendem a ser problemáticas. Usuários interessados em maior estabilidade devem utilizar o sistema de som ALSA. Por último, busque por softwares que possuem uma comunidade ampla e desenvolvimento ativo.

#### Escolha drivers de código aberto

Sempre que possível, utilize drivers de código aberto(open source). Evite drivers proprietários. Na maioria dos casos, os drivers abertos são mais estáveis e confiáveis que os proprietários. Drivers abertos tem seus bugs corrigidos de forma mais fácil e rápida. Enquanto drivers proprietários pode oferecer mais funcionalidades e capacidades, este pode ser o custo da estabilidade. Para evitar tal dilema, escolha componentes de hardware que possuem drivers abertos maduros e com suporte a maioria ou todas as funcionalidades. Informações sobre hardware com drivers abertos podem ser encontradas em [linux-drivers.org](http://www.linux-drivers.org/).

## Dando manutenção ao Arch

Adicionalmente a configuração do Arch focada em estabilidade, estes são alguns passos durante a manutenção que vão aumentar a estabilidade. Preste atenção nas dicas de alguns Administradores de Sistemas que irão ajudar a manter a confiabilidade contínua do sistema.

### Dicas específicas do Arch

#### Atualize todo o sistema com frequência

Muitos usuários do Arch atualizam frequentemente, até mesmo diariamente a atualização de sistemas através do comando `pacman -Syu`. Enquanto atualizar de forma tão frequente não é necessário, é uma boa forma de obter as últimas atualizações relativas a correção de bugs e segurança. Atualizações semanais e bissemanais são uma boa idéia.

Se seu sistema possui pacotes do AUR, cuidadosamente atualize todos os pacotes do AUR.

#### Leia antes de atualizar o sistema

Antes de atualizar o Arch, sempre leia as últimas notícias no [Arch News](https://www.archlinux.org/news/) para verificar se há alguma grande alteração de software ou de configuração nos últimos pacotes, necessitando até mesmo intervenção manual. Antes de atualizar qualquer software crítico, como o kernel, xorg, glibc, dê uma olhada no [fórum](https://bbs.archlinux.org/) apropriado e veja se não há problemas reportados por outros usuários.

#### Tome ações em alertas durante uma atualização

Quando atualizar o sistema, preste atenção nos alertas providos pelo pacman. Se quaisquer ações adicionais forem necessárias pelo usuário, tome o cuidado de fazê-las da forma certa. Se um alerta do pacman for confuso, busque nos fóruns por postagens recentes de instruções mais detalhadas.

#### Gerencie antecipatamente arquivos .pacnew, .pacsave e .pacorig

Quando o pacman remove um pacote que possui arquivo de configuração, ele normalmente cria um backup deste arquivo e adiciona o sufixo .pacsave ao nome do original. Da mesma forma, quando o pacman atualiza um pacote que inclui um novo arquivo de configuração criado por um mantenedor, e que possua diferenças do arquivo atual, o sufixo .pacnew é adicionado a um novo arquivo. Ocasionalmente, em circunstâncias especiais, o arquivo .pacorig é criado. O pacman sempre avisa da existência ou escrita destes arquivos.

Os usuários devem lidar com estes arquivo assim que o pacman criá-los, para garantir a estabilidade do sistema. A matéria [Pacnew and Pacsave files](/index.php/Pacnew_and_Pacsave_files "Pacnew and Pacsave files") possui instruções detalhadas sobre estes arquivos.

#### Considere a utilização do pacmatic

O [Pacmatic](http://kmkeen.com/pacmatic/index.html) é um wrapper do pacman que automatiza o processo de verificação das notícias do Arch antes de uma atualização. O pacmatic também garante que o banco de dados local do pacman está corretamente sincronizado com os repositórios online, evitando problemas potenciais com bancos de dados do pacman mal sincronizados. Por último, ele traz uma série de avisos detalhados sobre atualização ou arquivos de configuração obsoletos. O pacman pode ser transformado em um apelido(alias) para o pacmatic, e vários [AUR helpers](/index.php/AUR_helpers "AUR helpers") também podem ser configurados para utilizar o pacmatic como substituto do pacman.

#### Evite certos comandos do pacman

Devido a natureza rolling release do Arch, pode ser perigoso atualizar o banco de dados sem efetuar uma atualização do sistema em seguida. Evite utilizar `pacman -Sy package` para instalar um pacote, e sempre use o comando `pacman -S package`. E atualize seu sistema regularmente com `pacman -Syu`.

Evite utilizar a opção `-f` do comando pacman **especialmente** em comandos como `pacman -Syuf` envolvendo a manipulação de vários pacotes. A opção `--force` ignora conflitos de arquivos mas pode até mesmo causar a perda de arquivos que forem realocados entre pacotes diferentes! Em um sistema que é mantido da forma correta, tal opção nunca é necessária.

Não use o `pacman -Rdd package`. Utilizando a opção -d ignora a verificação de dependências durante a remoção de um pacote. Como resultado, um pacote que serve de dependência crítica pode ser removido, resultando num sistema com problemas severos.

Nunca execute `pacman -Scc` a não ser que você possua uma necessidade desesperadora de liberação de espaço em disco, e não possui a necessidade de armazenar pacotes antigos. É seguro manter versões antigas de pacotes no cache em eventos onde a atualização pode causar problemas, necessitando uma desatualização de um pacote. Ao invés disto, utilize o `pacman -Sc` para remover pacotes arquivados no cache do pacman e que foram previamente removidos do banco de dados do pacman.

Certifique-se de utilizar este comando apenas se não houver intenção de reinstalar pacotes removidos recentemente. Se tais pacotes forem reinstalados após este comando ser executado, não haverá versões mais antigas arquivadas no cache de pacotes do pacman.

Em um evento onde houver falta de espaço no /var, mova **todos** os pacotes arquivados para o diretório home do usuário em questão utilizando o script [fduparch.sh](http://www.3111skyline.com/download/Archlinux/scripts/). Utilize o script [fduppkg](http://www.3111skyline.com/download/Archlinux/scripts/fduppkg) para mover tais pacotes para /home exceto os utilizados na última versão armazenada no cache de arquivamento.

#### Revertendo pacotes que causaram instabilidade

Em um evento onde a atualização de um pacote em particular resulta em instabilidade, instale a última versão estável conhecida de um pacote no cache local do pacman com o seguinte comando:

```
pacman -U /var/cache/pacman/pkg/Package-Name.pkg.tar.gz

```

Para maiores detalhes e informações do assunto reverter versão de pacotes, consulte a página [Downgrading packages](/index.php/Downgrading_packages "Downgrading packages").

Uma vez que um pacote é revertido, adicione temporariamente a lista de pacotes que devem ter atualização ignorada [na seção IgnorePkg do pacman.conf](/index.php/Pacman#Skip_package_from_being_upgraded "Pacman") até que a dificultade na atalização seja resolvida. Consulte a wiki e/ou fóruns para orientações, e preencha um bug se necessário.

#### Faça backups periódicos da lista de pacotes instalados

Em intervalos regulares, crie uma lista dos pacotes instalados e armazene em alguma mídia offline como um pendrive, hd externo ou CD-R. Utilize o seguinte comando para criar tal lista:

```
pacman -Qqne > /path/to/chosen/directory/pkg.list

```

Em um evento de falha severa do sistema que requeira a reinstalação, estes pacotes podem ser facilmente reinstalados com o seguinte comando:

pacman -S --needed $(< /path/to/chosen/directory/pkg.list )

#### Faça backups periódicos do banco de dados de pacotes

O comando seguinte pode ser utilizado para efetuar o backup do banco de dados local do pacman, e dele, uma rotina na cron pode ser criada:

```
tar -cjf /path/to/chosen/directory/pacman-database.tar.bz2 /var/lib/pacman/local

```

Armazene o backup do banco de dados de pacotes em alguma mídia offline como um pendrive, hd externo ou CD-R.

Restaure tal backup do banco de dados do pacman movendo o arquivo pacman-database.tar.bz2 para a raíz do sistema / e execute o seguinte comando:

```
tar -xjvf pacman-database.tar.bz2

```

Caso os bancos de dados estejam corrimpidos, e não há backup disponível, existe a possibilidade da reconstrução do banco de dados. Consulte a página:[Como restaurar o banco de dados local do pacman](/index.php/Pacman_tips#Restore_pacman.27s_local_database "Pacman tips").

##### Automação no systemd

Você pode configurar o [systemd](/index.php/Systemd "Systemd") para fazer backups do banco de dados do pacman a cada novo pacote instalado, ou a cada atualização do sistema, através dos scripts que podem ser encontrados [aqui](/index.php/Pacman_tips#Backing_up_Local_database_with_systemd "Pacman tips").

### Melhores práticas genéricas

#### Inscreva-se nas listas NVD/CVE e apenas atualize em alertas de segurança

Inscreva-se na Common Vulnerabilities e Exposure Security Alert, disponível através da National Vulnerability Database encontrada [NVD aqui](http://nvd.nist.gov/download.cfm). Apenas atualize seu sistema Arch quando um alerta de segurança for lançado para um pacote em particular instalado neste sistema.

Esta é uma alternativa ao método de atualizar o sistema frequentemente. Garante que os problemas de segurança em vários pacotes foram resolvidos pró-ativamente, enquanto o resto dos pacotes fica congelado em uma configuração estável e conhecida. Contudo, verificar na CVE por alertas em todos os pacotes instalados e aplicá-los de tempos em tempos pode ser uma tarefa entediante e que leva tempo.

#### Teste as atualizações em sistemas não-críticos

Se possível, teste alterações em configuração e atualizações de pacotes em um sistema não-crítico que seja cópia do sistema original. Se nenhum problema ocorrer, atualize seu sistema de produção.

#### Sempre execute backup de arquivos de configuração antes de editar

Antes de editar qualquer arquivo de configuração, faça um backup da última versão funcional deste arquivo. Em um evento onde mudanças no arquivo de configuração podem acarretar em problemas, você pode reverter para a versão anterior e estável do arquivo. Faça isto salvando o arquivo logo que o abrir no seu editor, ou executando uma cópia antes de editar assim:

```
cp config config.bak

```

Utilizando a extensão *.bak* garantirá por dedução lógica que tal backup foi efetuado por um humano, diferentemente de arquivos como .pacnew, .pacsave, ou .pacorig.

[etckeeper](https://www.archlinux.org/packages/?name=etckeeper) pode ajudar nesta tarefa de lidar com arquivos de configuração. Ele mantém o diretório /etc inteiro dentro de um sistema de versionamento.

#### Faça backups períodicos dos diretórios /etc, /home, /srv, e /var

Por conta dos diretórios /etc, /home, /srv e /var conter informações importantes ao sistema e configurações, é recomendável que se guarde backup destes diretórios em um intervalo regular. Como fazer isto em um passo simples:

*   **/etc:** Efetuar backups do /etc através de uma rotina na cron:

```
tar -cjf /path/to/chosen/directory/etc-backup.tar.bz2 /etc

```

Armazene o backup do /etc em alguma mídia offline como um pendrive, hd externo ou CD-R. Ocasionalmente, verifique a integridade do backup comparando os arquivos originais com as cópias.

Restaure os arquivos corrompidos do /etc descompatcando o etc-backup.tar.bz2 em um diretório temporário e copiando os arquivos e diretórios individualmente quando necessário. Para restaurar o diretório /etc por completo mova o arquivo etc-backup.tar.bz2 para o diretório raíz / e execute o seguinte comando:

```
tar -xvjf etc-backup.tar.bz2

```

*   **/home:** At regular intervals, backup the /home directory to an external hard drive, Network Attached Server, or online backup service. Occasionally verify the integrity of the backup process by comparing original files and directories with their backups.

*   **/srv:** Server installations should have the /srv directory regularly backed up.

*   **/var:** Additional directories in /var, such a /var/spool/mail or /var/lib, which also require backup and occasional verification.

If you want to backup much faster (using parallel compression, SMP), you should use pbzip2 (Parallel bzip2). The steps are slightly different, but not by much.

First we will backup the files to a plain tarball with no compression:

```
tar -cvf /path/to/chosen/directory/etc-backup.tar /etc

```

Then we will use pbzip2 to compress it in parallel (Make sure you install it with **pacman -S pbzip2**)

```
pbzip2 /path/to/chosen/directory/etc-backup.tar.bz2

```

and that's it. Your files should be backing up using all of your cores.