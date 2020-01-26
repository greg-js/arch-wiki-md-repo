**Status de tradução:** Esse artigo é uma tradução de [Icons](/index.php/Icons "Icons"). Data da última tradução: 2020-01-25\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Icons&diff=0&oldid=589861) na versão em inglês.

Artigos relacionados

*   [Temas de cursor](/index.php/Temas_de_cursor "Temas de cursor")
*   [Xfce](/index.php/Xfce_(Portugu%C3%AAs) "Xfce (Português)")

O projeto freedesktop fornece a [Icon Theme Specification](https://specifications.freedesktop.org/icon-theme-spec/latest/), que se aplica à maioria dos ambientes de desktop linux e tenta unificar a aparência de vários ícones em um *icon-theme* (tema de ícones). O Freedesktop também fornece a [Icon Naming Specification](https://specifications.freedesktop.org/icon-naming-spec/latest/), que define um esquema de nomeação padrão para ícones que se acredita serem instalados em qualquer sistema. O tema padrão *hicolor* deve incluir todos eles.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
    *   [1.1 Ícones e emblemas](#Ícones_e_emblemas)
    *   [1.2 Ícones de tipo MIME](#Ícones_de_tipo_MIME)
    *   [1.3 Temas de ícones](#Temas_de_ícones)
        *   [1.3.1 De um pacote](#De_um_pacote)
        *   [1.3.2 Manualmente](#Manualmente)
*   [2 fstab / gvfs](#fstab_/_gvfs)

## Instalação

### Ícones e emblemas

Para anexar um ícone personalizado a um tema de ícones existente, `xdg-icon-resource` pode ser usado. Isso redimensionará e copiará o ícone para `$HOME/.local/share/icons/`. Com esse método, emblemas personalizados também podem ser adicionados. Exemplos:

```
$ xdg-icon-resource install --size 128 --context emblems archuser-exemplo.png # adicionar como emblema
$ xdg-icon-resource install --size 128 archuser-exemplo.png # adicionar como um ícone normal

```

### Ícones de tipo MIME

Os gerenciadores de arquivos atuais não dependem do tipo tradicional de MIME que `file --mime` gera. Em vez disso, são utilizadas definições de `/usr/share/mime/`. Chamar um ícone de acordo com a definição encontrada lá e copiá-lo para `~/.local/share/icons` fará com que o gerenciador de arquivos exiba o ícone do tipo MIME personalizado. Este comando ilustra o método:

 `Cria um ícone personalizado para arquivos de banco de dados do keepass (*.kdb)` 
```
# grep kdb /usr/share/mime/globs | egrep -o '.+\/[^:]+' | tr '/' '-'
application-x-keepass ;# renomeie seu ícones de acordo com essa saída
xdg-icon-resource install --size 128 --context mimetypes application-x-keepass.png

```

### Temas de ícones

**Dica:** É recomendável instalar o pacote [hicolor-icon-theme](https://www.archlinux.org/packages/?name=hicolor-icon-theme), pois muitos programas depositam seus ícones em `/usr/share/icons/hicolor` e a maioria dos outros temas de ícones herdará ícones do tema de ícones hicolor.

#### De um pacote

*   [Repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais") — [pesquisa por "icon-theme"](https://www.archlinux.org/packages/?sort=&q=icon-theme&maintainer=&last_update=&flagged=&limit=50).
*   [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)") — [pesquisa por "icon-theme"](https://aur.archlinux.org/packages.php?O=0&L=0&C=17&K=icon-theme&SeB=nd&SB=n&SO=a&PP=50&do_Search=Go).

#### Manualmente

Se você não conseguir encontrar um pacote para o tema do ícone que está procurando, será necessário instalá-lo manualmente.

*   Primeiro, encontre e baixe o pacote de ícones desejado. Muitos temas de ícones diferentes podem ser baixados dos seguintes sites: [Customize.org](http://www.customize.org), [Opendesktop.org](http://opendesktop.org) e [Xfce-look.org](http://xfce-look.org/).

*   Em seguida, navegue até o diretório que contém o pacote de ícones e extraia-o. Por exemplo, `tar -xzf /home/user/downloads/icon-pack.tar.gz`.

*   Mova a pasta extraída que contém os ícones para `~/.icons` ou `~/.local/share/icons` (apenas usuário) ou para `/usr/share/icons` (em todo o sistema).

*   Opcional: execute `gtk-update-icon-cache -f -t ~/.icons/<nome_tema>` para atualizar o cache do ícone.

*   Selecione o tema do ícone usando a ferramenta de configuração apropriada para seu [ambiente de desktop](/index.php/Ambiente_de_desktop "Ambiente de desktop") ou [gerenciador de janela](/index.php/Gerenciador_de_janela "Gerenciador de janela").

## fstab / gvfs

De acordo com este [documento](https://github.com/GNOME/gvfs/blob/mainline/monitor/udisks2/what-is-shown.txt), gerenciadores de arquivos que usam [GVFS](/index.php/GVFS_(Portugu%C3%AAs) "GVFS (Português)") (como [GNOME Arquivos](/index.php/GNOME_Files "GNOME Files") ou [Thunar](/index.php/Thunar "Thunar")) podem exibir ícones para locais personalizados, como compartilhamentos [NFS](/index.php/NFS "NFS"). Tudo o que você precisa são algumas opções de montagem estendidas dentro do `/etc/fstab` com nomes de ícones suportados pelo tema do ícone selecionado:

 `/etc/fstab` 
```
hostname:/ /mnt/ nfs4 defaults,_netdev,user,rw,exec,comment=x-gvfs-show,x-gvfs-name=Network%20Attached%20Storage,x-gvfs-icon=network-server,x-gvfs-symbolic-icon=network-server,timeo=14,noatime 0 0

```