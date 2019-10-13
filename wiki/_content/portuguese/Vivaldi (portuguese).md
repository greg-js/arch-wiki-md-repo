**Status de tradução:** Esse artigo é uma tradução de [Vivaldi](/index.php/Vivaldi "Vivaldi"). Data da última tradução: 2019-07-08\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Vivaldi&diff=0&oldid=576866) na versão em inglês.

[Vivaldi](http://vivaldi.com/) é um novo navegador da web do ex-fundador do [Opera](/index.php/Opera_(Portugu%C3%AAs) "Opera (Português)") e membros da equipe, com base no [Chromium](/index.php/Chromium "Chromium") e focado em aspectos de personalização.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Extensões](#Extensões)
*   [3 Reprodução de mídia](#Reprodução_de_mídia)
*   [4 Solução de problemas](#Solução_de_problemas)
    *   [4.1 Não é possível definir o Vivaldi como navegador padrão](#Não_é_possível_definir_o_Vivaldi_como_navegador_padrão)

## Instalação

Vivaldi pode ser instalado com [vivaldi](https://aur.archlinux.org/packages/vivaldi/) ou [vivaldi-snapshot](https://aur.archlinux.org/packages/vivaldi-snapshot/). Pacotes pré-construídos podem, alternativamente, ser encontrados no repositório não-oficial [herecura](/index.php/Unofficial_user_repositories#herecura "Unofficial user repositories").

Para usar [Qt](/index.php/Qt "Qt") em vez de [GTK](/index.php/GTK_(Portugu%C3%AAs) "GTK (Português)") nos diálogos de seleção de arquivo, apenas instale [kdialog](https://www.archlinux.org/packages/?name=kdialog).

## Extensões

O Vivaldi é compatível com a maioria das extensões do Chrome. Estes podem ser instalados diretamente na [Chrome Web Store](https://chrome.google.com/webstore/category/extensions). Para ver quais extensões estão instaladas/habilitadas, pesquise `vivaldi:// extensions` ou apenas `extensions`.

Veja também [Wikipedia:Google Chrome Extension](https://en.wikipedia.org/wiki/Google_Chrome_Extension "wikipedia:Google Chrome Extension").

## Reprodução de mídia

Para suporte adicional relacionado à reprodução de áudio e vídeo, instale o pacote correspondente para sua versão escolhida: [vivaldi-ffmpeg-codecs](https://aur.archlinux.org/packages/vivaldi-ffmpeg-codecs/), [vivaldi-snapshot-ffmpeg-codecs](https://aur.archlinux.org/packages/vivaldi-snapshot-ffmpeg-codecs/).

Você pode instalar o [pepper-flash](https://www.archlinux.org/packages/?name=pepper-flash) para reproduzir mídia flash.

## Solução de problemas

### Não é possível definir o Vivaldi como navegador padrão

Você tem que editar as [aplicações padrão](/index.php/Default_applications "Default applications") manualmente. Vivaldi não é capaz de reconhecer como fazê-lo sozinho.