**Status de tradução:** Esse artigo é uma tradução de [Pacman/Pacnew and Pacsave](/index.php/Pacman/Pacnew_and_Pacsave "Pacman/Pacnew and Pacsave"). Data da última tradução: 2019-10-13\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Pacman/Pacnew_and_Pacsave&diff=0&oldid=582907) na versão em inglês.

Quando o *pacman* remove um pacote que tem um arquivo de configuração, ele normalmente cria uma cópia backup daquele arquivo de configuração e anexa *.pacsave* ao nome do arquivo. Da mesma forma, quando o *pacman* atualiza um pacote que inclui um novo arquivo de configuração pelo mantenedor, comparando-o com a configuração atualmente instalada, ele salva um arquivo *.pacnew* com a nova configuração. O *pacman* fornece um aviso quando esses arquivos são escritos.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Por que esses arquivos são criados](#Por_que_esses_arquivos_são_criados)
*   [2 Arquivos backup do pacote](#Arquivos_backup_do_pacote)
*   [3 Tipos explicados](#Tipos_explicados)
    *   [3.1 .pacnew](#.pacnew)
    *   [3.2 .pacsave](#.pacsave)
*   [4 Localizando arquivos .pac*](#Localizando_arquivos_.pac*)
*   [5 Gerenciando arquivos .pac*](#Gerenciando_arquivos_.pac*)
    *   [5.1 pacdiff](#pacdiff)
    *   [5.2 Utilitários de terceiros](#Utilitários_de_terceiros)
*   [6 Veja também](#Veja_também)

## Por que esses arquivos são criados

Um arquivo *.pacnew* pode ser criado durante uma atualização de pacote (`pacman -Syu`, `pacman -Su` ou `pacman -U`) para evitar sobrescrever um arquivo que já existe e foi previamente modificado pelo usuário. Quando isso acontecer, uma mensagem como a seguir aparecerá na saída do *pacman*:

```
atenção: /etc/pam.d/usermod instalado como /etc/pam.d/usermod.pacnew

```

Um arquivo *.pacsave* pode ser criado durante a remoção de um pacote (`pacman -R`) ou na atualização de um pacote (o pacote deve ser removido primeiro). Quando a base de dados do pacman possuir registro de que deve-se fazer backup de um certo arquivo de um pacote, ele vai criar um arquivo *.pacsave*. Quando isso acontece, o pacman emite uma mensagem como a seguir:

```
atenção: /etc/pam.d/usermod salvo como /etc/pam.d/usermod.pacsave

```

Esses arquivos exigem intervenção manual do usuário e é uma boa prática tratar deles imediatamente a cada atualização ou remoção de pacote. Se não for tratado, configurações inadequadas podem resultar em função inadequada do software ou o software sendo incapaz de funcionar por completo.

## Arquivos backup do pacote

Um arquivo `PKGBUILD` do pacote especifica quais arquivos devem ser preservados ou cujo backup deve ser armazenado quando o pacote é atualizado ou removido. Por exemplo, o `PKGBUILD` do `pulseaudio` contém a seguinte linha:

```
backup=('etc/pulse/client.conf' 'etc/pulse/daemon.conf' 'etc/pulse/default.pa')

```

Para evitar que um pacote sobrescreva um certo arquivo, veja [Pacman (Português)#Pular pacotes para não serem atualizados](/index.php/Pacman_(Portugu%C3%AAs)#Pular_pacotes_para_não_serem_atualizados "Pacman (Português)").

## Tipos explicados

### .pacnew

Para cada um dos [#Arquivos backup do pacote](#Arquivos_backup_do_pacote) sendo atualizado, o pacman compara três [md5sums](https://en.wikipedia.org/wiki/pt:Md5sum "wikipedia:pt:Md5sum") gerados do conteúdo do arquivo: uma soma para a versão originalmente instalada pelo pacote, um para a versão atualmente no sistema de arquivo e uma para a versão no novo pacote. Se a versão do arquivo atualmente no sistema de arquivos foi modificada da versão originalmente instalada pelo pacote, o pacman não consegue saber como mesclar essas alterações com a nova versão do arquivo. Portanto, em vez de escrever no arquivo modificado ao atualizar, o pacman salva a nova versão com uma extensão *.pacnew* e deixa a versão modificada sem alterá-la.

Entrando nos detalhes, os resultados da comparação de soma do MD5 em três vias é um dos seguintes:

	original = *X*, atual = *X*, novo = *X* 

	Todas as três versões do arquivo possuem conteúdo idêntico, então sobrescrever não é um problema. Sobrescreve a versão atual com a nova versão e não notifica o usuário (apesar do conteúdo do arquivo ser o mesmo, isso vai sobrescrever as informações do sistema de arquivos a cerca dos tempos de instalação, modificação e acesso do arquivo, bem como garante que qualquer alteração de permissão do arquivo seja aplicada).

	original = *X*, atual = *X*, novo = *Y* 

	O conteúdo da versão atual é idêntico ao da original, mas a nova versão é diferente. Já que o usuário não modificou a versão atual e a nova versão pode conter melhorias ou correções de erros, sobrescreve a versão atual com a nova versão e não notifica o usuário. Esse é a única automesclagem de novas alterações que o pacman é capaz de realizar.

	original = *X*, atual = *Y*, novo = *X* 

	O pacote original e o novo pacote contêm exatamente a mesma versão do arquivo, mas a versão atualmente no sistema foi modificada. Deixa a versão atual no lugar e descarta a nova versão sem notificar o usuário.

	original = *X*, atual = *Y*, novo = *Y* 

	A nova versão é idêntica à versão atual. Sobrescreve a versão atual com a nova versão e não notifica o usuário (apesar do conteúdo do arquivo ser o mesmo, isso vai sobrescrever as informações do sistema de arquivos a cerca dos tempos de instalação, modificação e acesso do arquivo, bem como garante que qualquer alteração de permissão do arquivo seja aplicada).

	original = *X*, atual = *Y*, nova = *Z* 

	Todas as três versões são diferentes, então deixa a versão atual no lugar, instala a nova versão com uma extensão *.pacnew* e avisa o usuário sobre a nova versão. Espera-se que o usuário mescle manualmente quaisquer alterações necessárias da nova versão na versão atual.

Raramente, quando um pacote atualizado inclui um arquivo backup que a versão anterior não incluía, a situação é corretamente lidada como X/Y/Y ou X/Y/Z, com X sendo um valor não existente.

### .pacsave

Se o usuário modificou um dos arquivos especificados em `backup`, então aquele arquivo será renomeado com a extensão *.pacsave* e vai permanecer no sistema de arquivos após o resto do pacote ser removido.

**Nota:** O uso da opção `-n` com `pacman -R` vai resultar na remoção completa de *todos* os arquivos no pacote especificado, então nenhum arquivo *.pacsave* será criado.

## Localizando arquivos .pac*

O pacman não lida com arquivos *.pacnew* automaticamente: você deve mantê-los você mesmo. Algumas poucas ferramentas são apresentadas na próxima seção. Para fazer isso manualmente, você primeiro terá que localizá-los. Ao atualizar ou remover um grande número de pacotes, arquivos *.pac** atualizados serão perdidos. Para descobrir se algum arquivo *.pac** foi instalado, use um entre os seguintes:

*   Para procurar no `/etc`, onde a maioria das configurações globais estão armazenadas: `$ find /etc -regextype posix-extended -regex ".+\.pac(new|save)" 2> /dev/null` ou pesquisar em todo o disco substituindo `/etc` por `/` no comando anterior.
*   Se instalado, [locate](/index.php/Locate_(Portugu%C3%AAs) "Locate (Português)") também pode ser usado. Primeiro reindexe a base de dados: `# updatedb` . Então, execute: `$ locate --existing --regex "\.pac(new|save)$"` 
*   Use o log do pacman para localizá-los: `$ grep --extended-regexp "\.pac(new|save)" /var/log/pacman.log` Note que o log não mantém rastro dos arquivos atualmente no sistema de arquivos nem daqueles que já foram removidos; o comando acima vai listar todos os arquivos *.pac** que já existiram em seu sistema. Para apenas obter os 10 mais recentes arquivos *.pac**, faça um *pipe* do resultado para `tail`.

## Gerenciando arquivos .pac*

### pacdiff

[pacman-contrib](https://www.archlinux.org/packages/?name=pacman-contrib) fornece *pacdiff*, uma ferramenta simples para gerenciar arquivos pac*. Com isso, pode-se vai pesquisar por todos os arquivos *.pacnew* e *.pacsave* e pedir por quaisquer ações neles. Ele usa [vimdiff](/index.php/Vim#Merging_files "Vim") por padrão, mas você pode especificar uma ferramenta diferente com `DIFFPROG=*seu_editor* pacdiff`. Veja [List of applications/Utilities#Comparison, diff, merge](/index.php/List_of_applications/Utilities#Comparison,_diff,_merge "List of applications/Utilities") para outras ferramentas de comparação comum.

### Utilitários de terceiros

Alguns poucos utilitários de terceiros fornecendo vários níveis de automação para essas ferramentas estão disponíveis no [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)").

Você pode usar uma das seguintes ferramentas:

*   **dotpac** — Script interativo básico com interface de texto baseada no ncurses e um passo a passo útil. Nenhum recurso de mesclagem ou automesclagem.

	[https://github.com/AladW/dotpac](https://github.com/AladW/dotpac) || [dotpac](https://aur.archlinux.org/packages/dotpac/)

*   **etc-update** — Utilitário do *Gentoo* compatível com outras distribuições, incluindo o Arch. Ele fornece uma CLI simples para ver, mesclar e editar interativamente alterações. Alterações triviais, como comentários, podem ser mescladas automaticamente.

	[https://wiki.gentoo.org/wiki/Handbook:Parts/Portage/Tools#etc-update](https://wiki.gentoo.org/wiki/Handbook:Parts/Portage/Tools#etc-update) || [etc-update](https://aur.archlinux.org/packages/etc-update/)

*   **pacnew-auto** — Mesclagem automática de `pacnew` usando *rebase* do [git](https://www.archlinux.org/packages/?name=git).

	[https://github.com/joanrieu/pacnew-auto](https://github.com/joanrieu/pacnew-auto) || [pacnew-auto-git](https://aur.archlinux.org/packages/pacnew-auto-git/)

*   **pacnews-git** — Um script simples visando localizar todos os arquivos *.pacnew*, para então editá-los com [vimdiff](/index.php/Vim#Merging_files "Vim").

	[https://github.com/pbrisbin/scripts/blob/master/pacnews](https://github.com/pbrisbin/scripts/blob/master/pacnews) || [pacnews-git](https://aur.archlinux.org/packages/pacnews-git/)

*   **pacfiles-mode** — Um pacote para [Emacs](/index.php/Emacs "Emacs") para gerenciar e mesclar arquivos *.pacnew*, disponível em [melpa](https://melpa.org/#/pacfiles-mode).

	[https://github.com/UndeadKernel/pacfiles-mode](https://github.com/UndeadKernel/pacfiles-mode) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

## Veja também

*   Fórum do Arch Linux: [Dealing with .pacnew files](https://bbs.archlinux.org/viewtopic.php?id=53532) ("Lidando com arquivos .pacnew")