**Status de tradução:** Esse artigo é uma tradução de [mlocate](/index.php/Mlocate "Mlocate"). Data da última tradução: 2018-10-24\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Mlocate&diff=0&oldid=544335) na versão em inglês.

Artigos relacionados

*   [find](/index.php/Find_(Portugu%C3%AAs) "Find (Português)")
*   [Utilitários principais](/index.php/Utilit%C3%A1rios_principais "Utilitários principais")
*   [List of applications/Utilities#File searching](/index.php/List_of_applications/Utilities#File_searching "List of applications/Utilities")

[mlocate](https://pagure.io/mlocate) *(Merging Locate)* é uma versão mais segura do utilitário [locate](https://en.wikipedia.org/wiki/pt:locate_(Unix) "wikipedia:pt:locate (Unix)"), que mostra apenas arquivos acessíveis ao usuário.

`locate` é uma ferramenta Unix comum para encontrar rapidamente arquivos pelo nome. Ele oferece melhorias de velocidade em relação à ferramenta [find](/index.php/Find_(Portugu%C3%AAs) "Find (Português)"), pesquisando um arquivo de banco de dados pré-compilado, em vez do [sistema de arquivos](/index.php/File_system "File system") diretamente. A desvantagem dessa abordagem é que as alterações feitas desde a construção do arquivo de banco de dados não podem ser detectadas pelo `locate`. Esse problema pode ser minimizado por atualizações de banco de dados agendadas.

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [mlocate](https://www.archlinux.org/packages/?name=mlocate).

Enquanto o [GNU findutils](https://www.gnu.org/software/findutils/) também uma implementação do *locate*, o pacote [findutils](https://www.archlinux.org/packages/?name=findutils) do Arch não inclui.

## Uso

Antes que [locate(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locate.1) possa ser usado, o banco de dados precisará ser criado, isso é feito com o comando [updatedb(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/updatedb.8), que (como o nome sugere) atualiza o banco de dados.

O pacote contém uma unidade `updatedb.timer`, que invoca uma atualização do banco de dados todos os dias. O timer é ativado logo após a instalação, [inicie](/index.php/Inicie "Inicie") manualmente se você quiser usá-lo antes de reinicializar. Você também pode executar manualmente *updatedb* como root a qualquer momento.

Para economizar tempo, *updatedb* pode ser (e por padrão é) configurado para ignorar certos sistemas de arquivos e caminhos editando `/etc/updatedb.conf`. [updatedb.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/updatedb.conf.5) descreve a semântica deste arquivo. Vale a pena notar que entre os caminhos ignorados na configuração padrão (`PRUNEPATHS`) estão `/media` e `/mnt`, então *locate* pode não descobrir arquivos em dispositivos externos.

## Veja também

*   [Como locate funciona e rescreva-o em um minuto](http://jvns.ca/blog/2015/03/05/how-the-locate-command-works-and-lets-rewrite-it-in-one-minute/)