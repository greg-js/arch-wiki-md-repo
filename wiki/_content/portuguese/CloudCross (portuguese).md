[CloudCross](Http://cloudcross.mastersoft24.ru) - multi-cliente para a nuvem de sincronização de arquivos locais com vários armazenamento em nuvem, escritos em puro [Qt](/index.php/Qt "Qt"), sem a utilização de bibliotecas de terceiros. atualmente suportado para trabalhar com [Yandex. dRIVE](/index.php?title=Yandex._dRIVE&action=edit&redlink=1 "Yandex. dRIVE (page does not exist)"), [Google drive](/index.php?title=Google_drive&action=edit&redlink=1 "Google drive (page does not exist)") e [Dropbox](/index.php/Dropbox "Dropbox"). CloudCross publicado sob licença [GPL](/index.php?title=GPL&action=edit&redlink=1 "GPL (page does not exist)"). Principais características:

*   Ao trabalhar com o Google Drive - Suporta conversão de duas vias de documentos de formatos de arquivo do Microsoft Office e Abrir / LibreOffice em formato Google Doc, descarga e a transformação inversa ao carregar.
*   Suporte para as chamadas listas negras e brancas de arquivos que estão envolvidos na sincronização.
*   Configuração das preferências de arquivos locais ou remotos com as mudanças, o estado do qual ele será sincronizado.
*   Gerir a criação de novas versões dos arquivos no Google Drive.
*   Possibilidade de download ou upload de arquivos forçados.
*   Capacidade de download direto do arquivo para a nuvem no link para download.

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
*   [2 Escolhendo um provedor](#Escolhendo_um_provedor)
*   [3 Uso](#Uso)
*   [4 Casos de Uso](#Casos_de_Uso)
*   [5 Resolução de Problemas](#Resolu.C3.A7.C3.A3o_de_Problemas)
    *   [5.1 Excluir arquivos em vez de baixá](#Excluir_arquivos_em_vez_de_baix.C3.A1)
    *   [5.2 arquivos do escritório upload / download constantes](#arquivos_do_escrit.C3.B3rio_upload_.2F_download_constantes)
*   [6 Ligações](#Liga.C3.A7.C3.B5es)

## Instalação

Instale o pacote [cloudcross](https://aur.archlinux.org/packages/cloudcross/).

## Escolhendo um provedor

A partir da versão 1.1.0 *'CloudCross'* suporta múltiplos serviços em nuvem. Para selecionar o provedor utilizado opção --provider *nome* . Como um *nome* é usado o nome do fornecedor. O provedor padrão Google Drive.

## Uso

Depois de instalar, definir uma pasta, o conteúdo da qual vai ser sincronizada com a nuvem. Ir para ele e passar a autenticação:

Google Drive para

```
$ ccross -a

```

para Dropbox

```
$ ccross --provider dropbox -a

```

Você será solicitado a copiar o link e cole no seu browser. Seguindo o link proposto, você efetuar logon em sua conta do Google, e permissão para levar aplicações CloudCross solicitado. Depois disso, você será dado um código de confirmação para ser inserido no programa. Depois de passar a autenticação, o programa está pronto para trabalhar.

## Casos de Uso

CloudCross pode ser usado em diferentes situações quando necessário para sincronizar arquivos locais com os arquivos na nuvem. Pode ser, por exemplo, a duplicação de arquivos em um armazenamento remoto, trabalhando em conjunto com o Google Docs ou backup.

## Resolução de Problemas

Ao usar CloudCross pode ter alguns problemas.

### Excluir arquivos em vez de baixá

Quando inicia a sincronização para uma pasta vazia, em vez de baixar arquivos do armazenamento remoto nos arquivos de nuvem são excluídos. Isso ocorre porque o programa está priorizando arquivos locais por padrão. Para evitar isso, use a opção de inicialização --prefer = remoto

```
$ Ccross --prefer = remoto

```

Mas, em qualquer caso, você tem que lembrar que há arquivos locais ou remotos não são excluídos permanentemente. Você sempre pode recuperá-los da Lixeira na nuvem (se for suportado pelo serviço) ou pastas Trash pasta sincronizada.

### arquivos do escritório upload / download constantes

Quando você sincroniza com o Google Drive, se a opção for usada --convert-doc, que converte documentos do Office para o formato do Google Doc e para trás, você pode ver a situação que arquivos de escritório enviados para o servidor e inalterado desde então, durante a próxima sincronização começar a carregar de volta. E mais uma vez enviado para o servidor durante a próxima sincronização. Este não é um erro. Isso acontece porque a conversão altera a soma de verificação de um arquivo sem alterar o conteúdo eo programa tenta sincronizar as mudanças vê-las. Se o arquivo foi modificado desde a última sincronização, a versão mais recente do arquivo sincronizado.

## Ligações

*   [site do projeto](Http://cloudcross.mastersoft24.ru/ru)
*   [Grupo Facebook](Https://www.facebook.com/groups/cloudcross)