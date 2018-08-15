**Status de tradução:** Esse artigo é uma versão localizada de [Xprofile](/index.php/Xprofile "Xprofile"). Data da última tradução: 2018-08-14\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Xprofile&diff=0&oldid=526059) na versão em inglês.

Artigos relacionados

*   [xinitrc](/index.php/Xinitrc_(Portugu%C3%AAs) "Xinitrc (Português)")

Um arquivo xprofile, `~/.xprofile` e `/etc/xprofile`, permite que você execute comandos no início da sessão do usuário X - antes que o [gerenciador de janela](/index.php/Gerenciador_de_janela "Gerenciador de janela") seja iniciado.

O arquivo xprofile é similar em estilo ao [xinitrc](/index.php/Xinitrc_(Portugu%C3%AAs) "Xinitrc (Português)").

## Compatibilidade

Os arquivos xprofile são nativamente carregados pelos gerenciadores de exibição a seguir:

*   [GDM](/index.php/GDM_(Portugu%C3%AAs) "GDM (Português)") - `/etc/gdm/Xsession`
*   KDM - `/usr/share/config/kdm/Xsession`
*   [LightDM](/index.php/LightDM "LightDM") - `/etc/lightdm/Xsession`
*   [LXDM](/index.php/LXDM "LXDM") - `/etc/lxdm/Xsession`
*   [SDDM](/index.php/SDDM "SDDM") - `/usr/share/sddm/scripts/Xsession`

### Carregando xprofile de uma sessão iniciada com xinit

É possível obter xprofile a partir de uma sessão iniciada com um dos seguintes programas:

*   `startx`
*   `xinit`
*   [XDM](/index.php/XDM "XDM")
*   [SLiM](/index.php/SLiM "SLiM")
*   Qualquer outro [Gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição") que usa `~/.xsession` ou `~/.xinitrc`

Todos eles executam, direta ou indiretamente, `~/.xinitrc` ou `/etc/X11/xinit/xinitrc` se ele não existir. É por isso que o xprofile deve ser originado desses arquivos.

 `~/.xinitrc and /etc/X11/xinit/xinitrc` 
```
#!/bin/sh

# Certifique-se que isso esteja antes do comando 'exec' ou não será carregado.
[ -f /etc/xprofile ] && . /etc/xprofile
[ -f ~/.xprofile ] && . ~/.xprofile

...

```

## Configuração

Em primeiro lugar, crie o arquivo `~/.xprofile`, se ele ainda não existir. Em seguida, basta adicionar os comandos para os programas que você deseja iniciar com a sessão. Ver abaixo:

 `~/.xprofile` 
```
tint2 &
nm-applet &

```