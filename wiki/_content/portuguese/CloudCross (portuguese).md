**Status de tradução:** Esse artigo é uma tradução de [CloudCross](/index.php/CloudCross "CloudCross"). Data da última tradução: 2018-10-31\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=CloudCross&diff=0&oldid=552155) na versão em inglês.

De [CloudCross](http://cloudcross.mastersoft24.ru):

	O CloudCross é um projeto de código aberto para uma sincronização entre seus dispositivos e vários armazenamentos em nuvem. [...] CloudCross permite sincronizar todos os seus arquivos locais ou apenas uma parte dos arquivos e pastas locais/remotas usando as listas negra ou branca (arquivos .include e .exclude). Ao mesmo tempo, você tem a oportunidade de escolher quais arquivos têm a vantagem - local ou remota. Assim, você pode manter a relevância de arquivos locais ou arquivos no armazenamento em nuvem.

Está escrito em [Qt](/index.php/Qt "Qt") sem o uso de outra biblioteca de terceiros e atualmente é compatível com o Microsoft OneDrive, o [Google Drive](/index.php/Google_Drive "Google Drive"), o [Dropbox](/index.php/Dropbox "Dropbox"), o [Yandex Disk](/index.php/Yandex_Disk "Yandex Disk") e o Cloud Mail.ru.

Recursos principais:

*   Suporte à conversão bidirecional de documentos ao sincronizar a partir do formato MS/Libre/Open Office para o Google Docs e de volta
*   Suporte às chamadas listas negras e listas brancas de arquivos envolvidos na sincronização.
*   Definição de preferências de arquivos locais ou remotos com as mudanças, o estado do qual será sincronizado.
*   Gerência da criação de novas versões de arquivos no Google Drive.
*   Possibilidade de download forçado ou upload de arquivos.
*   Capacidade de direcionar o download do arquivo para a nuvem no link para download.

O CloudCross pode ser usado em diferentes situações quando necessário para sincronizar arquivos locais com os arquivos na nuvem. Pode ser, por exemplo, a duplicação de arquivos em um armazenamento remoto, trabalhando em conjunto com o Google Docs ou backup.

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
*   [2 Uso](#Uso)
*   [3 Solução de problemas](#Solu.C3.A7.C3.A3o_de_problemas)
    *   [3.1 Excluir arquivos em vez de baixar](#Excluir_arquivos_em_vez_de_baixar)
    *   [3.2 Constante upload/download de arquivos de escritório](#Constante_upload.2Fdownload_de_arquivos_de_escrit.C3.B3rio)
*   [4 Veja também](#Veja_tamb.C3.A9m)

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [cloudcross](https://aur.archlinux.org/packages/cloudcross/).

## Uso

Veja a [página man](/index.php/P%C3%A1gina_man "Página man") ccross(1) ou o [uso online](https://cloudcross.mastersoft24.ru/usage).

Para começar, mude para o diretório que deseja sincronizar e execute:

```
$ ccross --auth --provider *nome_provedor*

```

Você será solicitado a copiar o link e colá-lo em seu navegador. Após o link proposto, você faz login na sua conta do Google e solicita permissão para usar os aplicativos da CloudCross. Depois disso, você receberá um código de confirmação para ser inserido no programa. Depois de passar a autenticação, o programa está pronto para funcionar.

## Solução de problemas

Ao usar o CloudCross pode ter alguns problemas.

### Excluir arquivos em vez de baixar

Quando você inicia a sincronização para uma pasta vazia, em vez de baixar arquivos do armazenamento remoto, os arquivos da nuvem são excluídos. Isso ocorre porque o programa está priorizando arquivos locais por padrão. Para evitar isso, use a opção de inicialização `--prefer remote`.

```
$ ccross --prefer remote

```

Mas, em qualquer caso, é preciso lembrar que nenhum arquivo local ou remoto não é excluído permanentemente. Você sempre pode recuperá-los nas pastas sincronizadas `cloud` (se suportada pelo serviço) ou `.trash`.

### Constante upload/download de arquivos de escritório

Quando você sincroniza com o Google Drive, se a opção `--convert-doc` for usada, você poderá ver os arquivos enviados inalterados sendo sincronizados novamente. Isso não é um erro. Isso acontece porque a conversão de formato de arquivo altera a soma de verificação do arquivo sem alterar seu conteúdo, portanto, *ccross* tenta sincronizá-lo, assumindo que o arquivo foi alterado. Se o arquivo foi modificado desde a última sincronização, *cross* sincronizará a versão mais nova do arquivo.

## Veja também

*   [Site do projeto](Http://cloudcross.mastersoft24.ru)
*   [Grupo no Facebook](Https://www.facebook.com/groups/cloudcross)