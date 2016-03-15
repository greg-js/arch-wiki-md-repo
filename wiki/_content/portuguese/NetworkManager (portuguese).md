## Contents

*   [1 Introdução](#Introdu.C3.A7.C3.A3o)
*   [2 Instalação](#Instala.C3.A7.C3.A3o)
    *   [2.1 Caso **GNOME**:](#Caso_GNOME:)
    *   [2.2 Caso **KDE**:](#Caso_KDE:)
    *   [2.3 Caso **XFCE**:](#Caso_XFCE:)
    *   [2.4 Caso **Fluxbox/Outros WMs**:](#Caso_Fluxbox.2FOutros_WMs:)
*   [3 Configurando](#Configurando)
*   [4 Recursos Adicionais](#Recursos_Adicionais)

# Introdução

O [NetworkManager](http://www.gnome.org/projects/NetworkManager/) é uma ferramenta de rede que possibilita configurar e modificar as conexões com o seu sistema. É uma ferramenta muito útil, principalmente quando se trata de conexões wireless.

# Instalação

Primeiro verifique se o repositório *community* está habilitado na [configuração do pacman](/index.php/Pacman_(Portugu%C3%AAs)#Reposit.C3.B3rios "Pacman (Português)")

Instale o NetworkManager de acordo com o **ambiente desktop** que utiliza:

## Caso **GNOME**:

```
<tt># pacman -S gnome-network-manager wireless_tools dbus hal</tt>

```

## Caso **KDE**:

```
<tt># pacman -S knetworkmanager dbus hal</tt>

```

## Caso **XFCE**:

```
<tt># pacman -S gnome-network-manager dbus hal xfce4-xfapplet-plugin</tt>

```

## Caso **Fluxbox/Outros WMs**:

```
<tt># pacman -S gnome-network-manager dbus hal hicolor-icon-theme</tt>

```

Os usuários deverão pertencer ao grupo *network* para que possam habilitar ou configurar as conexões através do NetworkManager:

```
<tt># gpasswd -a "**logindousuário**" network</tt>

```

# Configurando

Como queremos que o NetworkManager configure a rede, então devemos desabilitar no /etc/rc.conf a autoinicialização das conexões, para isso adicionamos *!* a frente da interface. Mudando a linha de:

```
<tt>INTERFACES=(lo eth0)</tt>

```

Para

```
<tt>INTERFACES=(lo !eth0)</tt>

```

Agora devemos desabilitar o daemon *networks* e habilitar os daemons **dhcdbd** e **networkmanager**:

```
<tt>DAEMONS=(...dbus hal dhcdbd networkmanager...)</tt>

```

***Lembre-se de seguir essa ordem dbus hal dhcdbd networkmanager***. Caso exista o daemon *fam* na sua lista certifique-se que ele apareça **depois** desses citados.

Agora reinicie o computador para reinicializar os daemons e verificar se tudo ocorrerá corretamente. Neste ponto vc ja deve ser capaz de gerenciar suas conexões através do NetworkManager, se você não puder ver um ícone na sua tela para gerenciá-las, é só inicializar:

Para **GNOME/XFCE/Outros**:

```
<tt>$ nm-applet</tt>

```

Para **KDE**:

```
<tt>$ knetworkmanager</tt>

```

# Recursos Adicionais

[Configurando a Rede (English)](/index.php/Network "Network")

[Site oficial do NetworkManager](http://www.gnome.org/projects/NetworkManager/)