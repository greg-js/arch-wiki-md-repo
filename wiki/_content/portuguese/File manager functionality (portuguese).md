**Status de tradução:** Esse artigo é uma tradução de [File manager functionality](/index.php/File_manager_functionality "File manager functionality"). Data da última tradução: 2019-05-23\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=File_manager_functionality&diff=0&oldid=569937) na versão em inglês.

Artigos relacionados

*   [List of applications/Utilities#File managers](/index.php/List_of_applications/Utilities#File_managers "List of applications/Utilities")
*   [Gerenciador de janela](/index.php/Gerenciador_de_janela "Gerenciador de janela")
*   [Ambiente de desktop](/index.php/Ambiente_de_desktop "Ambiente de desktop")
*   [Udisks](/index.php/Udisks "Udisks")

Este artigo descreve os pacotes de software adicionais necessários para expandir os recursos e a funcionalidade dos gerenciadores de arquivos, especialmente quando se usa um [gerenciador de janela](/index.php/Gerenciador_de_janela "Gerenciador de janela") como o [Openbox](/index.php/Openbox "Openbox"). A capacidade de acessar partições e mídias removíveis sem uma senha - se afetada - também foi fornecida.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Visão geral](#Visão_geral)
*   [2 Recursos adicionais](#Recursos_adicionais)
    *   [2.1 Montando](#Montando)
        *   [2.1.1 Daemon de gerenciador de arquivos](#Daemon_de_gerenciador_de_arquivos)
        *   [2.1.2 Autônomo](#Autônomo)
    *   [2.2 Redes](#Redes)
        *   [2.2.1 Acesso a Windows](#Acesso_a_Windows)
        *   [2.2.2 Acesso a Apple](#Acesso_a_Apple)
    *   [2.3 Visualização de miniaturas](#Visualização_de_miniaturas)
        *   [2.3.1 Gerenciadores de arquivo além do Dolphin e Konqueror](#Gerenciadores_de_arquivo_além_do_Dolphin_e_Konqueror)
        *   [2.3.2 Dolphin e Konqueror (KDE)](#Dolphin_e_Konqueror_(KDE))
    *   [2.4 Arquivos de pacotes](#Arquivos_de_pacotes)
    *   [2.5 Suporte a leitura/escrita de NTFS](#Suporte_a_leitura/escrita_de_NTFS)
    *   [2.6 Notificações de desktop](#Notificações_de_desktop)
    *   [2.7 Habilitar funcionalidade de lixeira em sistemas diferentes (unidades externas)](#Habilitar_funcionalidade_de_lixeira_em_sistemas_diferentes_(unidades_externas))
*   [3 Solução de problemas](#Solução_de_problemas)
    *   [3.1 "Not Authorized" ao tentar montar as unidades](#"Not_Authorized"_ao_tentar_montar_as_unidades)
    *   [3.2 Senhas necessária para acessar partições](#Senhas_necessária_para_acessar_partições)
    *   [3.3 Diretórios não são abertos no gerenciador de arquivos](#Diretórios_não_são_abertos_no_gerenciador_de_arquivos)

## Visão geral

**Nota:** Quando instalados, os pacotes de software listados abaixo serão automaticamente originados por todos os gerenciadores de arquivos instalados e capazes, e em todos os ambientes de área de trabalho e/ou gerenciadores de janelas.

Um gerenciador de arquivos sozinho não fornecerá os recursos e funcionalidades aos quais os usuários de ambientes de desktop completos, como o [Xfce](/index.php/Xfce_(Portugu%C3%AAs) "Xfce (Português)") ou o [KDE](/index.php/KDE_(Portugu%C3%AAs) "KDE (Português)"), estarão acostumados. Isso ocorre porque pacotes de software adicionais serão necessários para permitir que um determinado gerenciador de arquivos:

*   Exibe e acesso outras partições
*   Exibe, monte e acesse mídias removíveis (e.x., pendrives, discos óticos e câmeras digitais)
*   Habilite conectividade/redes compartilhadas com outros sistemas operacionais instalados
*   Habilite miniaturização
*   Arquive e extraia arquivos comprimidos
*   Monte automaticamente mídia removível

Quando um gerenciador de arquivos é instalado como parte de um ambiente de desktop completo, a maioria desses pacotes geralmente é instalada automaticamente. Consequentemente, quando um gerenciador de arquivos foi instalado para um gerenciador de janelas autônomo, como é o caso do próprio gerenciador de janelas, apenas uma base básica será fornecida. O usuário deve determinar a natureza e a extensão dos recursos e funcionalidades a serem adicionados.

## Recursos adicionais

Particularmente, quando usando - ou pretendendo usar - um ambiente leve, deve-se notar que mais recursos e funções do gerenciador de arquivos geralmente significam o uso de mais memória. Veja também [udisks](/index.php/Udisks "Udisks").

### Montando

*   O sistema de arquivos virtual do GNOME ([gvfs](https://www.archlinux.org/packages/?name=gvfs)) fornece funcionalidade de montagem e lixo. O GVFS usa [udisks2](https://www.archlinux.org/packages/?name=udisks2) para funcionalidade de montagem e é a solução recomendada para a maioria dos gerenciadores de arquivos.

Pastas usadas pelo GVFS:

*   `/usr/lib/gvfs/` contém `gvfsd-*` arquivos, sendo que `*` se refere a vários tipos de sistema de arquivos suportados.
*   `/usr/share/gvfs/mounts/` contém regras de montagem para GVFS. Para usar suas próprias regras, crie `~/.gvfs/mounts`.

Pacotes adicionais para instalação geralmente seguem o [padrão gvfs-*](https://www.archlinux.org/packages/?q=gvfs-), por exemplo:

*   [gvfs-mtp](https://www.archlinux.org/packages/?name=gvfs-mtp): reprodutores de mídia e dispositivos móveis que usam [MTP](/index.php/MTP "MTP")
*   [gvfs-gphoto2](https://www.archlinux.org/packages/?name=gvfs-gphoto2): câmeras digitais e dispositivos móveis que usam [PTP](https://en.wikipedia.org/wiki/Picture_Transfer_Protocol "wikipedia:Picture Transfer Protocol")
*   [gvfs-afc](https://www.archlinux.org/packages/?name=gvfs-afc): dispositivos móveis da Apple

#### Daemon de gerenciador de arquivos

A primeira é simplesmente iniciar automaticamente ou executar o gerenciador de arquivos instalado no modo [daemon](/index.php/Daemon_(Portugu%C3%AAs) "Daemon (Português)") (ou seja, como um processo em segundo plano). Por exemplo, quando usando [PCManFM](/index.php/PCManFM "PCManFM") em [Openbox](/index.php/Openbox "Openbox"), o seguinte comando será adicionado ao arquivo `~/.config/openbox/autostart`:

```
pcmanfm -d &

```

Também será necessário configurar o gerenciador de arquivos em relação ao gerenciamento de volume (por exemplo, o que ele fará e quais aplicativos serão lançados quando determinados tipos de arquivo forem detectados na montagem).

**Dica:** A maioria dos ambientes de desktop iniciará o gerenciador de arquivos no modo daemon por padrão, portanto, a intervenção manual não será necessária nesses casos de uso.

#### Autônomo

Outra opção é instalar um [aplicativo de montagem](/index.php/List_of_applications/Utilities#Mount_tools "List of applications/Utilities") separado. As vantagens de usar isso são:

*   Menos memória pode ser necessária para ser executada como um processo de segundo plano [daemon](/index.php/Daemon_(Portugu%C3%AAs) "Daemon (Português)") do que um gerenciador de arquivos
*   Não é específico do gerenciador de arquivos, permitindo que sejam livremente adicionados, removidos e alternados
*   [gvfs](https://www.archlinux.org/packages/?name=gvfs) pode não ter que ser instalado para montar, reduzindo o uso de memória.

### Redes

**Nota:** Também será necessário ativar o [Bluetooth](/index.php/Bluetooth "Bluetooth") e/ou a rede com o [Windows](/index.php/Samba "Samba") para habilitar a funcionalidade relevante do gerenciador de arquivos.

*   [obexfs](https://aur.archlinux.org/packages/obexfs/): Transferências de arquivos e montagem de dispositivos Bluetooth (veja [Bluetooth](/index.php/Bluetooth "Bluetooth"))
*   [gvfs-smb](https://www.archlinux.org/packages/?name=gvfs-smb): Compartilhamento de arquivos e impressoras Windows para ambientes que **não sejam KDE** (veja [Samba](/index.php/Samba "Samba"))
*   [kdenetwork-filesharing](https://www.archlinux.org/packages/?name=kdenetwork-filesharing): Compartilhamento de arquivos e impressoras Windows para [KDE](/index.php/KDE_(Portugu%C3%AAs) "KDE (Português)") (veja [Samba#KDE](/index.php/Samba#KDE "Samba"))
*   [sshfs](https://www.archlinux.org/packages/?name=sshfs): Cliente FUSE baseado no protocolo de transferência de arquivos SSH

#### Acesso a Windows

Se estiver usando [gvfs-smb](https://www.archlinux.org/packages/?name=gvfs-smb), para acessar os compartilhamentos de arquivos do Windows/CIFS/Samba abra primeiro o gerenciador de arquivos e digite o seguinte no nome do caminho, alterando `*nome_do_servidor*` e `*nome_do_compartilhamento*` conforme apropriado:

```
smb://*nome_do_servidor*/*nome_do_compartilhamento*

```

#### Acesso a Apple

Suporte a AFP está incluso no [gvfs](https://www.archlinux.org/packages/?name=gvfs). Para acessar os compartilhamentos de arquivos de AFP abra primeiro o gerenciador de arquivos e digite o seguinte no nome do caminho, alterando `*nome_do_servidor*` e `*nome_do_compartilhamento*` conforme apropriado:

```
afp://*nome_do_servidor*/*nome_do_compartilhamento*

```

### Visualização de miniaturas

Alguns gerenciadores de arquivos podem não suportar miniaturas, mesmo quando os pacotes listados foram instalados. Verifique a documentação do gerenciador de arquivos relevante.

Você não pode ver miniaturas para armazenamento remoto, incluindo [MTP](/index.php/MTP "MTP"). Verifique as configurações do seu gerenciador de arquivos, por exemplo para [Thunar](/index.php/Thunar "Thunar") é preciso definir "Mostrar miniaturas: sempre".

#### Gerenciadores de arquivo além do Dolphin e Konqueror

Esses pacotes se aplicam à maioria dos gerenciadores de arquivos, como [PCManFM](/index.php/PCManFM "PCManFM"), [SpaceFM](/index.php/SpaceFM "SpaceFM"), [Thunar](/index.php/Thunar "Thunar") e [xfe](https://aur.archlinux.org/packages/xfe/). As exceções são Dolphin e Konqueror, usados no ambiente de desktop [KDE](/index.php/KDE_(Portugu%C3%AAs) "KDE (Português)").

*   [tumbler](https://www.archlinux.org/packages/?name=tumbler): Arquivos de imagem. Ele também **<u>deve</u>** deve ser instalado para expandir as capacidades de miniaturas para outros tipos de arquivos
*   [poppler-glib](https://www.archlinux.org/packages/?name=poppler-glib): Arquivos `.pdf` do Adobe
*   [ffmpegthumbnailer](https://www.archlinux.org/packages/?name=ffmpegthumbnailer): Arquivos de vídeo
*   [freetype2](https://www.archlinux.org/packages/?name=freetype2): Arquivos de fonte
*   [libgsf](https://www.archlinux.org/packages/?name=libgsf): Arquivos `.odf`
*   [raw-thumbnailer](https://www.archlinux.org/packages/?name=raw-thumbnailer): Arquivos `.raw`
*   [totem](https://www.archlinux.org/packages/?name=totem): Arquivos de vídeo e arquivos de áudio rotulados ([Arquivos do GNOME](/index.php/GNOME_Files "GNOME Files") e Caja apenas)
*   [evince](https://www.archlinux.org/packages/?name=evince) ou [atril](https://www.archlinux.org/packages/?name=atril): Arquivos `.pdf`

#### Dolphin e Konqueror (KDE)

Veja [Dolphin#File previews](/index.php/Dolphin#File_previews "Dolphin").

### Arquivos de pacotes

Para extrair arquivos compactados, como tarballs (`.tar` e `.tar.gz`) dentro de um gerenciador de arquivos, primeiro será necessário instalar um arquivador GUI, como o [file-roller](https://www.archlinux.org/packages/?name=file-roller). Veja [List of applications/Utilities#Archiving and compression tools](/index.php/List_of_applications/Utilities#Archiving_and_compression_tools "List of applications/Utilities") para mais informações. Um pacote adicional como [unzip](https://www.archlinux.org/packages/?name=unzip) também deve ser instalado para suportar o uso de arquivos zipados (`.zip`). Depois que um arquivador é instalado, os arquivos no gerenciador de arquivos podem, consequentemente, ser clicados com o botão direito do mouse para serem arquivados ou extraídos.

Os empacotadores de arquivos são montados na pasta `/run/user/$(id -u)/gvfs/` com ponto de montagem criado automaticamente que contém caminho completo para o arquivo em seu nome, onde todos `/` são substituídos por `%252F` e `:` substituído por `%253A`, que são [códigos hexa](https://www.owasp.org/index.php/Double_Encoding).

Example de caminho para o pacote montado `/caminho/para/nome/de/arquivo.zip`

```
/run/user/$(id -u)/gvfs/archive:host=file%253A%252F%252F%252F**caminho%252Fpara%252Fnome%252Fde%252Farquivo.zip**

```

### Suporte a leitura/escrita de NTFS

Veja o artigo [NTFS-3G](/index.php/NTFS-3G "NTFS-3G").

### Notificações de desktop

Alguns gerenciadores de arquivos fazem uso de [notificações de desktop](/index.php/Desktop_notifications "Desktop notifications") para confirmar vários eventos e status, como montagem, desmontagem e ejeção de mídia removível.

### Habilitar funcionalidade de lixeira em sistemas diferentes (unidades externas)

Crie [diretórios de lixeira](http://www.ramendik.ru/docs/trashspec.html) `.Trash-*<uid>*` para cada usuário no nível de topo de sistemas de arquivoa:

Por exemplo (ponto de montagem: /media/sdc1, uid: 1000, gid: 1000):

```
# mkdir /media/sdc1/.Trash-1000

```

e execute `chown` neles:

```
# chown 1000:1000 /media/sdc1/.Trash-1000

```

## Solução de problemas

### "Not Authorized" ao tentar montar as unidades

Gerenciadores de arquivos usando [udisks](/index.php/Udisks "Udisks") precisam de um agente de autenticação [polkit](/index.php/Polkit "Polkit"). Veja [polkit#Authentication agents](/index.php/Polkit#Authentication_agents "Polkit").

### Senhas necessária para acessar partições

A necessidade de inserir uma senha para acessar outras partições ou mídia removível montada provavelmente será devido às configurações de permissão padrão de [udisks2](https://www.archlinux.org/packages/?name=udisks2). Mais especificamente, a permissão pode ser definida apenas para a conta raiz, não para a conta do usuário. Veja [Udisks#Configuration](/index.php/Udisks#Configuration "Udisks") para detalhes.

### Diretórios não são abertos no gerenciador de arquivos

Você pode descobrir que um aplicativo que não é um gerenciador de arquivos, [Audacious](/index.php/Audacious "Audacious") por exemplo, está definido como o aplicativo padrão para abrir diretórios - um aplicativo que especifica que ele pode manipular o tipo MIME `inode/directory` em sua entrada de desktop pode se tornar o padrão. Você pode consultar o aplicativo padrão para abrir diretórios com o seguinte comando:

```
$ xdg-mime query default inode/directory

```

Para se certificar que diretórios são abertos no gerenciador de arquivos, execute o seguinte comando:

```
$ xdg-mime default *meu_gerenciador_de_arquivos*.desktop inode/directory

```

sendo que `*meu_gerenciador_de_arquivos*.desktop` é a entrada de desktop para o seu gerenciador de arquivos — `*org.gnome.Nautilus*.desktop`, por exemplo.

**Dica:** Se você quiser que a alteração se aplique a todo sistema, execute o comando acima como root ou crie/edite o arquivo a seguir: `/usr/share/applications/mimeapps.list` 
```
[Default Applications]
inode/directory=*meu_gerenciador_de_arquivos*.desktop
```