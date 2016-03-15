Primeiramente leia o [O Jeito Arch](/index.php/The_Arch_Way_(Portugu%C3%AAs) "The Arch Way (Português)"), o [Arch Linux](/index.php/Arch_Linux_(Portugu%C3%AAs) "Arch Linux (Português)"). Todos os três documentos são uma ótima fonte de informação sobre o Arch Linux.

## Contents

*   [1 P) Eu sou um completo iniciante no Linux. Eu deveria usar o Arch?](#P.29_Eu_sou_um_completo_iniciante_no_Linux._Eu_deveria_usar_o_Arch.3F)
*   [2 P) Eu encontrei um erro no pacote X, o que eu devo fazer?](#P.29_Eu_encontrei_um_erro_no_pacote_X.2C_o_que_eu_devo_fazer.3F)
*   [3 P) O Arch terá uma base de dados para o pacman?](#P.29_O_Arch_ter.C3.A1_uma_base_de_dados_para_o_pacman.3F)
*   [4 P) O pacman está lento! Como o tempo de inicialização pode ser melhorado?](#P.29_O_pacman_est.C3.A1_lento.21_Como_o_tempo_de_inicializa.C3.A7.C3.A3o_pode_ser_melhorado.3F)
*   [5 P) Os pacotes do Arch precisam usar uma nomenclatura única. .pkg.tar.gz é muito longo e/ou confuso.](#P.29_Os_pacotes_do_Arch_precisam_usar_uma_nomenclatura_.C3.BAnica._.pkg.tar.gz_.C3.A9_muito_longo_e.2Fou_confuso.)
*   [6 P) O pacman precisa de uma biblioteca para que outras aplicações possam acessar facilmente informações dos pacotes.](#P.29_O_pacman_precisa_de_uma_biblioteca_para_que_outras_aplica.C3.A7.C3.B5es_possam_acessar_facilmente_informa.C3.A7.C3.B5es_dos_pacotes.)
*   [7 P) O pacman precisa de um front-end](#P.29_O_pacman_precisa_de_um_front-end)
*   [8 P) O pacman precisa do recurso X!](#P.29_O_pacman_precisa_do_recurso_X.21)
*   [9 P) O Arch precisa de um instalador melhor. Talvez um instalador gráfico.](#P.29_O_Arch_precisa_de_um_instalador_melhor._Talvez_um_instalador_gr.C3.A1fico.)
*   [10 P) O Arch precisa de mais divulgação (leia: propaganda)](#P.29_O_Arch_precisa_de_mais_divulga.C3.A7.C3.A3o_.28leia:_propaganda.29)
*   [11 P) O Arch precisa de menos divulgação](#P.29_O_Arch_precisa_de_menos_divulga.C3.A7.C3.A3o)
*   [12 P) O Arch precisa de mais desenvolvedores](#P.29_O_Arch_precisa_de_mais_desenvolvedores)
*   [13 P) O Arch precisa de um repositório de pacotes estáveis](#P.29_O_Arch_precisa_de_um_reposit.C3.B3rio_de_pacotes_est.C3.A1veis)
*   [14 P) O Arch precisa de mais documentação](#P.29_O_Arch_precisa_de_mais_documenta.C3.A7.C3.A3o)
*   [15 P) O Arch precisa ser mais amigável para os "novatos"](#P.29_O_Arch_precisa_ser_mais_amig.C3.A1vel_para_os_.22novatos.22)
*   [16 P) Novatos são irritantes. Faça eles irem embora.](#P.29_Novatos_s.C3.A3o_irritantes._Fa.C3.A7a_eles_irem_embora.)
*   [17 P) O Arch precisa de uma entidade de apoio](#P.29_O_Arch_precisa_de_uma_entidade_de_apoio)

## P) Eu sou um completo iniciante no Linux. Eu deveria usar o Arch?

**R)** Esta é uma questão que já foi bastante discutida. O Arch é uma distribuição voltada para usuários Linux mais avançados, porém muitas pessoas acham que o "Arch é um bom local para começar". Se você é um iniciante e deseja usar o Arch, saiba que você DEVE estar disposto a aprender. Antes de fazer sua pergunta, pesquise no google, no wiki e no fórum. Fazendo isso, você não terá problemas. Saiba, também, que muitas pessoas não querem responder as mesmas perguntas várias vezes, e você estará se expondo a este tipo de coisa. Há uma razão para que estes recursos tenham sido disponibilizados para você. Você pode consultar o [Guia para Iniciantes](/index.php/Guia_para_Iniciantes "Guia para Iniciantes").

* * *

## P) Eu encontrei um erro no pacote X, o que eu devo fazer?

**R)** Primeiramente você precisa descobrir se o erro é algo que a equipe do Arch pode consertar. Algumas vezes não é (aquele travamento no firefox pode ser falha da equipe do Mozilla) - isto é chamado de *upstream error*. Se for um problema do Arch, existe uma série de coisas que você pode fazer:

1.  Procurar informações no fórum. Veja se alguém teve o mesmo problema.
2.  Informar o mantenedor do pacote. Rode um "pacman -Qi <nome do pacote>" para obter esta informação.
3.  Relatar o bug, com informações detalhadas, em [https://bugs.archlinux.org](https://bugs.archlinux.org)
4.  Se desejar, você pode criar um tópico no forum descrevendo o problema e informando que você já relatou o mesmo. Isto ajuda a prevenir que várias pessoas relatem o mesmo erro.

* * *

## P) O Arch terá uma base de dados para o pacman?

**R)** Possivelmente. Já existe uma discussão sobre o assunto. [https://bbs.archlinux.org/viewtopic.php?t=11193](https://bbs.archlinux.org/viewtopic.php?t=11193) [https://bbs.archlinux.org/viewtopic.php?t=10898](https://bbs.archlinux.org/viewtopic.php?t=10898)

* * *

## P) O pacman está lento! Como o tempo de inicialização pode ser melhorado?

**R)** O pacman pode ser lento apenas na primeira vez que o mesmo roda após o boot. Depois disso, as coisas são geralmente armazenadas no cache. Entretanto, o tempo de inicialização do pacman ainda é um problema para algumas pessoas. Existe uma discussão sobre isso. Se você está usando ReiserFS, existem alguns problemas com fragmentação que diminuem a velocidade do pacman mais do que necessário. Para ajuda, veja este tópico: [https://bbs.archlinux.org/viewtopic.php?t=11840](https://bbs.archlinux.org/viewtopic.php?t=11840)

Desde a versão 2.9.6, o pacman acompanha um script chamado <tt>pacman-optimize</tt> que deve ajudar qualquer pessoa que esteja tendo problemas com o tempo de inicialização do mesmo.

* * *

## P) Os pacotes do Arch precisam usar uma nomenclatura única. .pkg.tar.gz é muito longo e/ou confuso.

**R)** Isto vem sendo discutido na lista de discussão do Arch. Alguns propuseram uma extensão .pac. Até onde se sabe. não há nenhuma intenção em modificar a extensão dos pacotes. Como Tobias Kieslich, um dos desenvolvedores do Arch, colocou, "Um pacote **é** gzipped tarball!! E ele pode ser aberto, verificado e manipulado por qualquer aplicação tar. Além disso, o mime-type é automaticamente detectado pela maioria das aplicações".

* * *

## P) O pacman precisa de uma biblioteca para que outras aplicações possam acessar facilmente informações dos pacotes.

**R)** Já está sendo desenvolvida uma biblioteca para o pacman.

* * *

## P) O pacman precisa de um front-end

**R)** Você leu o [The Arch Way](/index.php/The_Arch_Way "The Arch Way"), o [Arch Linux](/index.php/Arch_Linux "Arch Linux")? A resposta é que basicamente o time de desenvolvedores do Arch não estará fornecendo um front-end. Sinta-se a vontade para usar um dos fornecidos pelos usuários. Existe uma ótima lista deles na [Getting involved](/index.php/Getting_involved "Getting involved"). Assim que a biblioteca para o pacman estiver pronta, será bem mais fácil para os vários fontends interagirem com os pacotes do Arch.

Além do mais, isso não é uma pergunta e sim uma afirmação; ;-)

* * *

## P) O pacman precisa do recurso X!

**R)** Você leu o [The Arch Way](/index.php/The_Arch_Way "The Arch Way"), o [Arch Linux](/index.php/Arch_Linux "Arch Linux")? A filosofia do Arch é "Keep It Simple". Se você acha que sua idéia tem fundamento, e que ela não viola esta filosofia, então você pode discuti-la no [forum](https://bbs.archlinux.org/). Você pode, também, verificar [isso](https://bugs.archlinux.org), um lugar onde você pode fazer pedidos, caso você os considere importantes.

* * *

## P) O Arch precisa de um instalador melhor. Talvez um instalador gráfico.

**R)** A discussão sobre um "melhor" instalador é uma opinião subjetiva. A melhor maneira de lidar com isso é colocar o instalador no "jeito arch". Se esta opinião sobre um melhor instalador fosse reforçada com mais argumentos concretos, o desenvolvimento adicional do instalador poderia ser levado em conta. *O Windows usa um instalador baseado em texto*.

* * *

## P) O Arch precisa de mais divulgação (leia: propaganda)

**R)** O Arch já está sendo bastante divulgado. O objetivo do Arch Linux não é ser grande. O objetivo é ser bem feito. Deixe que o crescimento ocorra naturalmente. Tentar forçar este crescimento só causará problemas.

* * *

## P) O Arch precisa de menos divulgação

**R)** De maneira parecida com o que foi dito acima, não tente desacelerar o crescimento natural. Mais usuários podem significar mais desenvolvedores trabalhando no Arch Linux. Isto pode causar alguns problemas de organização no "topo", mas estes serão tratados quando aparecerem.

* * *

## P) O Arch precisa de mais desenvolvedores

**R)** Possivelmente. Sinta-se livre para ser um voluntário! Visite os fóruns, irc, listas de email, e veja o que precisa ser feito. Documentação é algo que é sempre necessário. Veja [DocumentRequests](/index.php/DocumentRequests "DocumentRequests") para qualquer coisa pendente.

* * *

## P) O Arch precisa de um repositório de pacotes estáveis

**R)** COMENTÁRIO: "Para mim, o Arch é maturo o suficiente"

RESPOSTA: Isso depende do tipo de trabalho para o qual a máquina é usada. Por exemplo, em um escritório nós não queremos que nossa impressora pare de trabalhar. Em trabalhos de multimedia nosso gravador de cd deve funcionar. Desenvolvedores web precisam de clientes de ftp funcionais. Atualmente estou irritado com o kde-3.4 porque perdi todos os meus favoritos no kbear (ftp). Novos favoritos não podem ser salvos.

SOLUÇÃO: Existe um **repositório** **release** que é estável, apesar de não estar suportando todos os pacotes. Há a intenção de incluir todos os pacotes principais (kde, gnome, etc).
[ftp://ftp.archlinux.org/release/os/i686/](ftp://ftp.archlinux.org/release/os/i686/)

Leia mais em:
[https://bbs.archlinux.org/viewtopic.php?t=11288](https://bbs.archlinux.org/viewtopic.php?t=11288)

* * *

## P) O Arch precisa de mais documentação

**R)** Se após procurar nos fóruns, e no wiki, você não conseguir encontrar a documentação que deseja, tente criá-la. Comece uma página no wiki, e crie um tópico no fórum comentando sobre a mesma. Provavelmente você encontrará algumas pessoas com experiência no assunto, ou que ao menos estão dispostas a ajudar. Se ninguém o fizer, não desanime. Quando você terminar sua documentação, há uma grande chance de outras pessoas descobrirem nela uma ótima fonte de informação. Documentação é algo que é sempre necessário. Veja [DocumentRequests](/index.php/DocumentRequests "DocumentRequests") para qualquer coisa pendente.

* * *

## P) O Arch precisa ser mais amigável para os "novatos"

**R)** Antes de começarmos uma discussão sobre isso, precisamos definir o que é "amigável para os novatos". Por favor, consulte a questão sobre um melhor instalador.

* * *

## P) Novatos são irritantes. Faça eles irem embora.

**R)** <Discussão filosófica> Parte de ser humano é aceitar que outros sejam humanos também. </Discussão filosófica>

A melhor maneira de lidar com novatos é não julgá-los de antemão. Algumas pessoas podem estar com um problema comum, mesmo se elas leram as documentações. Todos erram algumas vezes. Criticá-los não ajudará. Use seu melhor comportamento e ignore pessoas de que você não gosta, ao invés de começar uma briga.

Novatos são melhor ajudados ao serem guiados para que encontrem a informação correta. Especialmente os novatos que estão vindo do Windows, podem ter problemas ao tentar encontrar informações; nem sempre elas estão no lugar que eles esperam. Compare isso com encontrar a palavra correta para o trabalho correto: você pode pedir para que seu professor encontre uma certa palavra para você, mas você sempre esquecerá o significado da mesma. Entretanto, se você mesmo procurar a palavra no dicionário, você não a esquecerá durante o resto da sua vida.

* * *

## P) O Arch precisa de uma entidade de apoio

**R)** Por quê? Outros projetos, como o Gentoo, sobrevivem sem uma e o Arch também pode.