**[Diretrizes de criação de pacotes](/index.php/Criando_pacotes "Criando pacotes")**

* * *

[CLR](/index.php/Diretrizes_de_pacotes_CLR "Diretrizes de pacotes CLR") – [Cross](/index.php/Diretrizes_de_pacotes_de_ferramentas_de_compila%C3%A7%C3%A3o_cruzada "Diretrizes de pacotes de ferramentas de compilação cruzada") – [Eclipse](/index.php/Diretrizes_de_pacotes_de_plugin_do_Eclipse "Diretrizes de pacotes de plugin do Eclipse") – [Free Pascal](/index.php/Diretrizes_de_pacotes_Free_Pascal "Diretrizes de pacotes Free Pascal") – [GNOME](/index.php/Diretrizes_de_pacotes_GNOME "Diretrizes de pacotes GNOME") – [Go](/index.php/Diretrizes_de_pacotes_Go "Diretrizes de pacotes Go") – [Haskell](/index.php/Diretrizes_de_pacotes_Haskell "Diretrizes de pacotes Haskell") – [Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java") – [KDE](/index.php/Diretrizes_de_pacotes_KDE "Diretrizes de pacotes KDE") – [Kernel](/index.php/Diretrizes_de_pacotes_de_m%C3%B3dulos_de_kernel "Diretrizes de pacotes de módulos de kernel") – [Lisp](/index.php/Diretrizes_de_pacotes_Lisp "Diretrizes de pacotes Lisp") – [MinGW](/index.php/Diretrizes_de_pacotes_MinGW "Diretrizes de pacotes MinGW") – [Node.js](/index.php/Diretrizes_de_pacotes_Node.js "Diretrizes de pacotes Node.js") – [Nonfree](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") –[OCaml](/index.php/Diretrizes_de_pacotes_OCaml "Diretrizes de pacotes OCaml") – [Perl](/index.php/Diretrizes_de_pacotes_Perl "Diretrizes de pacotes Perl") – [PHP](/index.php/Diretrizes_de_pacotes_PHP "Diretrizes de pacotes PHP") – [Python](/index.php/Diretrizes_de_pacotes_Python "Diretrizes de pacotes Python") – [R](/index.php/Diretrizes_de_pacotes_R "Diretrizes de pacotes R") – [Ruby](/index.php/Diretrizes_de_pacotes_Ruby_Gem "Diretrizes de pacotes Ruby Gem") – [VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") – [Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web") – [Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine")

Para muitos aplicativos (a maioria dos quais são do Windows), não há fontes nem tarballs disponíveis. Muitos desses aplicativos não podem ser distribuídos livremente devido a restrições de licença e/ou falta de meios legais para obter o instalador sem cobrança de taxa. Tal software obviamente não pode ser incluído nos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais") mas devido à natureza do [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)") ainda é possível privadamente [compilar pacotes](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") para ele, gerenciável com [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)").

**Nota:** Todas as informações aqui são agnósticos a pacotes. Para informações específicas para a maioria dos softwares não livres, veja [Diretrizes de pacotes Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine").

## Contents

*   [1 Motivo](#Motivo)
*   [2 Regras comuns](#Regras_comuns)
    *   [2.1 Evite software não livre quando possível](#Evite_software_n.C3.A3o_livre_quando_poss.C3.ADvel)
    *   [2.2 Use variantes de código aberto quando possível](#Use_variantes_de_c.C3.B3digo_aberto_quando_poss.C3.ADvel)
    *   [2.3 Mantenha simples](#Mantenha_simples)
*   [3 Nomenclatura de pacotes](#Nomenclatura_de_pacotes)
*   [4 Colocação de arquivos](#Coloca.C3.A7.C3.A3o_de_arquivos)
*   [5 Arquivos em falta](#Arquivos_em_falta)
*   [6 Tópicos avançados](#T.C3.B3picos_avan.C3.A7ados)
    *   [6.1 DLAGENTS personalizados](#DLAGENTS_personalizados)
    *   [6.2 Desempacotamento](#Desempacotamento)
    *   [6.3 Obtendo ícones para arquivos .desktop](#Obtendo_.C3.ADcones_para_arquivos_.desktop)

## Motivo

Existem vários motivos para empacotar softwares não empacotáveis:

*   Simplificação de processo de instalação/remoção

	Isso é aplicável até mesmo aos aplicativos mais simples, que consistem em um único script a ser instalado em `/usr/bin`. Em vez de executar:

	 `$ chmod +x *nome-de-arquivo*` 

	 `$ chown root:root *nome-de-arquivo*` 

	 `# cp *filename* /usr/bin/` 

	você pode digitar

	 `$ makepkg -i` 

	A maioria dos aplicativos não livres é obviamente muito mais complicada, mas o fardo de baixar um arquivo/instalador de uma página inicial (muitas vezes cheia de propaganda), descompactá-lo/descriptografá-lo, escrever scripts de lançadores estereotipados e realizar outras tarefas semelhantes pode ser efetivamente facilitadas por um script de empacotamento bem escrito.

*   Usando capacidades do *pacman*

	A capacidade de rastrear estado, executar atualizações automáticas de qualquer software instalado, determinar a propriedade de cada arquivo e armazenar pacotes compactados em um cache bem organizado é o que torna as distribuições GNU/Linux tão poderosas.

*   Compartilhamento de código e conhecimento

	É mais simples aplicar ajustes, corrigir bugs e procurar/fornecer ajuda em um único local público, como o AUR, em vez de enviar patches para desenvolvedores proprietários que podem ter interrompido o suporte ou fazer perguntas vagas em fóruns de propósito geral.

## Regras comuns

### Evite software não livre quando possível

Sim, é melhor deixar este guia e passar algum tempo procurando (ou talvez até criando) alternativas para um aplicativo que você queria empacotar porque:

1.  É melhor oferecer suporte a um software que pertence a todos nós do que um software que pertence a uma empresa
2.  É melhor oferecer suporte a um software que é mantido ativamente
3.  É melhor oferecer suporte a um software que pode ser consertado se apenas uma pessoa, em milhões, se importar o suficiente

### Use variantes de código aberto quando possível

Muitos jogos comerciais ([alguns estão listados neste Wiki](/index.php/List_of_Applications/Games "List of Applications/Games")) possuem mecanismos de código aberto e muitos jogos antigos podem ser reproduzidos com emuladores como [ScummVM](https://en.wikipedia.org/wiki/pt:ScummVM "wikipedia:pt:ScummVM"). O uso de mecanismos de software livre junto com os recursos originais do jogo oferece aos usuários acesso a correções de erros e elimina vários problemas causados por pacotes binários.

### Mantenha simples

Se o empacotamento de algum programa exigir mais esforço e hacks do que comprar e usar a versão original - faça a coisa mais simples, isso é Arch!

## Nomenclatura de pacotes

Antes de escolher um nome, pesquise no AUR as versões existentes do software que você deseja empacotar. Tente usar uma conversão de nomenclatura estabelecida (por exemplo, não crie algo como [gish-hb](https://aur.archlinux.org/packages/gish-hb/) quando já houver [aquaria-hib](https://aur.archlinux.org/packages/aquaria-hib/), [penumbra-overture-hib](https://aur.archlinux.org/packages/penumbra-overture-hib/) e [uplink-hib](https://aur.archlinux.org/packages/uplink-hib/)). **Sempre** use o sufixo `-bin`, a menos que você tenha certeza de que nunca haverá um pacote baseado em código-fonte; seu criador terá que perguntar a você (ou no pior caso TUs) ao pacote órfão existente. ele e os dois acabarão com PKGBUILDs cheios de `replaces` e `conflicts` adicionais.

## Colocação de arquivos

Novamente, analise os pacotes existentes (se houver) e decida se deseja ou não entrar em conflito com eles. Não coloque coisas em `/opt`, a menos que você queira usar alguns hacks feios como dar a propriedade `root:games` ao diretório do pacote (para que os usuários do grupo `games` o jogo pode gravar arquivos na própria pasta do jogo).

## Arquivos em falta

Para a maioria dos jogos comerciais, não há como (legalmente) baixar arquivos de jogos, o que é a maneira preferida de obtê-los para pacotes normais. Mesmo quando é possível baixar arquivos após fornecer uma senha (como com todos os jogos do [Humble Indie Bundle](https://en.wikipedia.org/wiki/pt:Humble_Indie_Bundle "wikipedia:pt:Humble Indie Bundle")) solicitando ao usuário essa senha e fazendo o download em alguma parte da função `build`, não é recomendado por várias razões (por exemplo, o usuário pode não ter acesso à Internet, mas ter todos os arquivos baixados e armazenados localmente). As seguintes opções devem ser consideradas:

*   **Há apenas uma forma de obter os arquivos**

*   O software é distribuído em pacote/instalador

	Adicione o arquivo necessário para o vetor `sources`:

	 `sources=(... "*nome-original*::**file://***nome-original*")` 

	Desta forma, o link para o arquivo na interface web do AUR será diferente dos nomes dos arquivos incluídos no tarball de origem.

	Adicione o seguinte comentário na página do pacote:

	 `Need archive/installer to work.` 

	e explicar os detalhes no vetor de fontes do PKGBUILD.

*   O software é distribuído em um disco compacto

	Adicione um script de instalação e um arquivo `.install` ao conteúdo do pacote, como no pacote [tsukihime-en](https://aur.archlinux.org/packages/tsukihime-en/).

*   **Há várias formas de obter arquivos**

Copiar arquivos do disco / fazer o download da Internet / obter do arquivo durante a fase `build` pode parecer uma boa ideia, mas não é recomendado porque limita as possibilidades do usuário e torna a instalação do pacote interativa (o que geralmente é desencorajado e irritante). Novamente, um bom script de instalação e um arquivo `.install` podem funcionar.

Alguns exemplos de várias estratégias para obter arquivos necessários para o pacote:

*   [worldofgoo](https://aur.archlinux.org/packages/worldofgoo/) – dependência em arquivo fornecido por usuário
*   [umineko-en](https://aur.archlinux.org/packages/umineko-en/) – combinando arquivos de patch livremente disponível e disco compacto fornecido por usuário
*   [worldofgoo-demo](https://aur.archlinux.org/packages/worldofgoo-demo/) – obtenção automática de instalação durante a fase de compilação
*   [ut2004-anthology](https://aur.archlinux.org/packages/ut2004-anthology/) – pesquisando por disco via pontos de montagem

## Tópicos avançados

### DLAGENTS personalizados

Alguns autores de software protegem agressivamente seu software contra downloads automáticos: proíbem certas strings "User-Agent", criam links temporários para arquivos, etc. Você ainda pode convenientemente baixar estes arquivos usando a variável `DLAGENTS` no PKGBUILD (veja [makepkg.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/makepkg.conf.5)). Isto é usado por alguns pacotes em [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais"), por exemplo, [ttf-baekmuk](https://www.archlinux.org/packages/?name=ttf-baekmuk).

Por favor, preste atenção, se você quiser ter uma string user-agent personalizada, se esta contiver espaços, parênteses ou barras (ou, na verdade, qualquer coisa que possa interromper a análise), isso não funcionará. Não há solução alternativa, essa é a natureza de vetores no bash e a maneira como o DLAGENTS foi projetado para ser usado no makepkg. O exemplo a seguir, portanto, **não funciona**:

```
DLAGENTS=("http::/usr/bin/curl -A 'Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)' -fLC - --retry 3 --retry-delay 3 -o %o %u")

```

Encurte para o seguinte que está funcionando:

```
DLAGENTS=("http::/usr/bin/curl -A 'Mozilla' -fLC - --retry 3 --retry-delay 3 -o %o %u")

```

E, a seguir, permita extrair link temporário para o arquivo da página de download:

```
DLAGENTS=("http::/usr/bin/wget -r -np -nd -H %u")

```

### Desempacotamento

Muitos programas proprietários são publicados em instaladores desagradáveis que às vezes nem funcionam no Wine. As seguintes ferramentas podem ajudar:

*   [unzip](https://www.archlinux.org/packages/?name=unzip) e [unrar](https://www.archlinux.org/packages/?name=unrar) descompactam arquivos SFX executáveis, baseados nesses formatos
*   [cabextract](https://www.archlinux.org/packages/?name=cabextract) pode descompactar a maioria dos arquivos `.cab` (incluindo aqueles com extensão `.exe`)
*   [unshield](https://www.archlinux.org/packages/?name=unshield) pode extrair arquivos CAB de instaladores do InstallShield
*   [p7zip](https://www.archlinux.org/packages/?name=p7zip) descompacta não apenas muitos formatos de arquivo, mas também [NSIS](https://en.wikipedia.org/wiki/pt:NSIS "wikipedia:pt:NSIS") - instaladores `.exe`
    *   ele pode até mesmo extrair seções únicas de arquivos comuns de PE (`.exe` e `.dll`)!
*   [upx](https://www.archlinux.org/packages/?name=upx) às vezes é usado para compactar os executáveis listados acima e também pode ser usado para descompactá-los
*   [innoextract](https://www.archlinux.org/packages/?name=innoextract) pode descompactar instaladores `.exe` criados com [Inno Setup](https://en.wikipedia.org/wiki/pt:Inno_Setup "wikipedia:pt:Inno Setup") (usado, por exemplo, por jogos GOG.com)

Para determinar o tipo exato de arquivo, execute `file *arquivo_de_tipo_desconhecido*`.

### Obtendo ícones para arquivos .desktop

O software proprietário geralmente não possui arquivos de ícone separados, portanto, não há nada para usar na criação de arquivos [.desktop](/index.php/.desktop ".desktop"). Felizmente, `.ico` arquivos podem ser facilmente extraídos de executáveis com programas do pacote [icoutils](https://www.archlinux.org/packages/?name=icoutils). Você pode até fazer isso durante a fase `build`, por exemplo:

```
$ wrestool -x --output=*icon.ico* -t14 *executable.exe*

```