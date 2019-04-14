**Status de tradução:** Esse artigo é uma tradução de [Arch IRC channels](/index.php/Arch_IRC_channels "Arch IRC channels"). Data da última tradução: 2019-04-14\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Arch_IRC_channels&diff=0&oldid=566394) na versão em inglês.

Artigos relacionados

*   [ArchWiki:IRC (Português)](/index.php/ArchWiki:IRC_(Portugu%C3%AAs) "ArchWiki:IRC (Português)")
*   [Comunidades internacionais](/index.php/Comunidades_internacionais "Comunidades internacionais")
*   [phrik](/index.php/Phrik "Phrik")

**Nota:** Não edite a [página em inglês](/index.php/IRC_channel "IRC channel") a menos que você seja um operador de canal no #archlinux. Você é bem-vindo para usar a [página de discussão](/index.php/Talk:IRC_channel "Talk:IRC channel").

Para usar [Internet Relay Chat](https://en.wikipedia.org/wiki/pt:Internet_Relay_Chat "wikipedia:pt:Internet Relay Chat") (IRC), você precisa de um [cliente IRC](/index.php/IRC_client "IRC client"). O [ambiente de instalação live](/index.php/Guia_de_instala%C3%A7%C3%A3o "Guia de instalação") inclui o cliente [Irssi](/index.php/Irssi "Irssi").

Espera-se que você esteja familiarizado com nosso [Código de conduta](/index.php/C%C3%B3digo_de_conduta "Código de conduta") e o [Código de conduta#IRC](/index.php/C%C3%B3digo_de_conduta#IRC "Código de conduta") antes de entrar em qualquer um dos canais oficiais. Para uma lista da s abreviações comumente usadas, veja [Terminologia do Arch](/index.php/Terminologia_do_Arch "Terminologia do Arch") e [Jargão do IRC](http://www.ircbeginner.com/ircinfo/abbreviations.html).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Canais principais](#Canais_principais)
    *   [1.1 Registro](#Registro)
    *   [1.2 Operadores do canal](#Operadores_do_canal)
*   [2 Outros canais](#Outros_canais)
    *   [2.1 Canais IRC internacionais](#Canais_IRC_internacionais)

## Canais principais

**Nota:**

*   Devido ao abuso, vários gateways e clientes web podem ser banidos às vezes. Se você tiver problemas, use um cliente de IRC "*adequado*" IRC ou peça a algum dos operadores por uma exceção de banimento (`+e`).
*   Estatísticas de canal são registrados para [#archlinux-offtopic](https://alyp.tk/stats/aotstats.html). Fale com "jp/alyptik" se você gostaria de se retirar permanentemente.

Essa seção é sobre [#archlinux](ircs://chat.freenode.net/archlinux), o canal [IRC](https://en.wikipedia.org/wiki/pt:Internet_Relay_Chat "wikipedia:pt:Internet Relay Chat") principal do Arch Linux, e [#archlinux-offtopic](ircs://chat.freenode.net/archlinux-offtopic), o canal social principal do Arch Linux, ambos disponíveis na rede [Freenode](https://freenode.net/).

O tópico central de **#archlinux** é suporte e discussão geral sobre o Arch Linux.

### Registro

Para reduzir o spam, **#archlinux** e **#archlinux-offtopic** agora têm o modo de canal definido para `+r` e `+q $~a`. Isso significa que agora você precisa estar identificado via `NickServ` para ser capaz de ingressar nesses canais e enviar mensagens, respectivamente. Se você não estiver registrado e identificado, você será encaminhado para **#archlinux-unregistered**.

Para registrar com NickServ, siga o [FAQ do freenode](https://freenode.net/kb/answer/registration), bem como `NickServ help` quando conectado ao *chat.freenode.net*:

```
/query NickServ HELP REGISTER
/query NickServ HELP IDENTIFY

```

**Nota:**

*   Se `/query` acabar por não funcionar em seu cliente, você pode tentar usar `/quote NickServ <comando>` ou `/msg NickServ <comando>`.
*   Alguns clientes IRC têm uma condição de corrida na qual eles tentam ingressar automaticamente em canais antes de você ser identificado com NickServ e, para resolver isso, você precisa habilitar SASL. Olhe a documentação do seu cliente IRC ou olhe a [página SASL](https://freenode.net/kb/answer/sasl) do freenode para encontrar instruções sobre como habilitá-lo.
*   Você pode obter uma lsita de pessoas que podem lhe ajudar digitando `/msg ChanServ ACCESS #archlinux LIST` ou ingressando no **#freenode** e perguntando lá.

### Operadores do canal

Operadores do Arch são operadores em ambos **#archlinux** e **#archlinux-offtopic**. Veja abaixo a lista ou execute `/msg phrik listops` no freenode.

Se você, por algum motivo, precisar de ajuda de um operador, não seja tímido para nos `/query` ou `/msg`. Aqui está a lista de operadores até 1º de novembro de 2018:

*   alad
*   amcrae
*   falconindy
*   gehidore / man
*   grawity
*   heftig
*   jelle
*   MrElendig / Mion
*   Namarrgon
*   pid1
*   tigrmesh / tigr
*   vodik
*   wonder / ioni

## Outros canais

O tamanho de nossa comunidade levou à criação de múltiplos canais IRC. Para obter uma lista de todos os canais em **[chat.freenode.net](ircs://chat.freenode.net)** que contêm `archlinux` em seu nome, use o comando `/query alis list *archlinux*`.

| Canal | Descrição |
| [#archlinux64](ircs://chat.freenode.net/archlinux64) | Canal de discussão específica para x86_64, principalmente em inglês |
| [#archlinux-aur](ircs://chat.freenode.net/archlinux-aur) | Discussão geral do [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)") |
| [#archlinux-aurweb](ircs://chat.freenode.net/archlinux-aurweb) | Discussão sobre o desenvolvimento do [aurweb](https://projects.archlinux.org/aurweb.git/) |
| [#archlinux-bugs](ircs://chat.freenode.net/archlinux-bugs) | Discussão centrada em bugs |
| [#archlinux-classroom](ircs://chat.freenode.net/archlinux-classroom) | Um projeto que desenvolve e hospeda classes para a comunidade do Arch Linux. |
| [#archlinux-devops](ircs://chat.freenode.net/archlinux-devops) | Discussões sobre infraestrutura interna e devops do Arch Linux. |
| [#archlinux-multilib](ircs://chat.freenode.net/archlinux-multilib) | Discussão e empacotamento do Projeto Multilib do Arch Linux |
| [#archlinux-newbie](ircs://chat.freenode.net/archlinux-newbie) | Um espaço para aprender, tentar novas coisas e pedir ajuda sem medo do ridículo. |
| [#archlinux-pacman](ircs://chat.freenode.net/archlinux-pacman) | Desenvolvimento e discussão sobre o [Pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") |
| [#archlinux-projects](ircs://chat.freenode.net/archlinux-projects) | Desenvolvimento e discussão sobre projetos (mkinitcpio, abs, dbscripts, devtools, ...) |
| [#archlinux-reproducible](ircs://chat.freenode.net/archlinux-reproducible) | Canal de discussão para atingir compilações reproduzíveis. |
| [#archlinux-security](ircs://chat.freenode.net/archlinux-security) | Discussão sobre questões de segurança em pacotes do Arch. |
| [#archlinux-testing](ircs://chat.freenode.net/archlinux-testing) | Canal de discussão a cerca dos repositórios de teste. |
| [#archlinux-wiki](ircs://chat.freenode.net/archlinux-wiki) | Discussão sobre [ArchWiki](/index.php/ArchWiki_(Portugu%C3%AAs) "ArchWiki (Português)"), seus artigos e os [Fóruns do Arch Linux](https://bbs.archlinux.org/). |
| [#archlinux-women](ircs://chat.freenode.net/archlinux-women) | Discutindo gênero e igualdade, principalmente em inglês. |
| [#archlinux-proaudio](ircs://chat.freenode.net/archlinux-proaudio) | Discussão de [Arch Linux Pro Audio](/index.php/Professional_audio "Professional audio"). Usuários também no #archaudio não oficial |

### Canais IRC internacionais

Discussões internacionais estão disponíveis nos seguintes canais, também localizados na rede IRC **[chat.freenode.net](ircs://chat.freenode.net)** , a menos que seja afirmado o contrário.

| Canal | Descrição |
| [#archlinux-za](ircs://chat.freenode.net/archlinux-za) | Discussão (Africâner, Inglês) |
| [#archlinux-br](ircs://chat.freenode.net/archlinux-br) | Discussão (Brasileiro) |
| [#archlinux-cn](ircs://chat.freenode.net/archlinux-cn) | Discussão (Chinês), também em **[irc.oftc.net#arch-cn](ircs://irc.oftc.net/arch-cn)** |
| [#archlinux-cr](ircs://chat.freenode.net/archlinux-cr) | Discussão (Costa Rica) |
| [#archlinux.cz](ircs://chat.freenode.net/archlinux.cz) | Discussão (Tcheco) |
| [#archlinux.dk](ircs://chat.freenode.net/archlinux.dk) | Discussão (Dinamarquês) |
| [#archlinux.fi](ircs://chat.freenode.net/archlinux.fi) | Discussão (Finlandês) |
| [#archlinux-fr](ircs://chat.freenode.net/archlinux-fr) | Discussão (Francês) |
| [#archlinux-gaelic](ircs://chat.freenode.net/archlinux-gaelic) | Discussão (Hebreu) |
| [#archlinux.hu](ircs://chat.freenode.net/archlinux.hu) | Discussão (Húngaro) |
| [#archlinux-it](ircs://chat.freenode.net/archlinux-it) | Discussão (Italiano); também em **[irc.azzurra.org#archlinux](irc://irc.azzurra.org/archlinux)** |
| [#archlinux-nordics](ircs://chat.freenode.net/archlinux-nordics) | Discussão (os nórdicos: Dinamarquês, Finlandês, Norueguês e Sueco) |
| [#archlinux-kr](ircs://chat.freenode.net/archlinux-kr) | Discussão (Coreano) |
| [#archlinux-ir](ircs://chat.freenode.net/archlinux-ir) | Discussão (Persa) |
| [#archlinux.org.pl](ircs://chat.freenode.net/archlinux.org.pl) | Discussão (Polonês) |
| [#archlinux-pt](ircs://chat.freenode.net/archlinux-pt) | Discussão (Português) |
| [#archlinux.ro](ircs://chat.freenode.net/archlinux.ro) | Discussão (Romano) |
| [#archlinux-tg](ircs://chat.freenode.net/archlinux-tg) | Discussão (russo); ponte entre o IRC e grupo Telegram [Arch Linux RU](https://t.me/ArchLinuxChatRU) |
| [#archlinux-ru](ircs://chat.freenode.net/archlinux-ru) | Discussão (Russo); também em **[irc.mibbit.net#archlinux-ru](irc://irc.mibbit.net/archlinux-ru)** |
| [#archlinux-rs](ircs://chat.freenode.net/archlinux-rs) | Discussão (Sérbio) |
| [#archlinux-es](ircs://chat.freenode.net/archlinux-es) | Discussão (Espanhol) |
| [#archlinux.se](ircs://chat.freenode.net/archlinux.se) | Discussão (Sueco) |
| [#archlinux-tr](ircs://chat.freenode.net/archlinux-tr) | Discussão (Turco) |
| [#archlinux-ve](ircs://chat.freenode.net/archlinux-ve) | Discussão (Venezuela) |
| [#archlinuxvn](ircs://chat.freenode.net/archlinuxvn) | Discussão (Vietnamita, Tiếng Việt) |