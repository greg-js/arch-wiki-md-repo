## Contents

*   [1 Especificações](#Especifica.C3.A7.C3.B5es)
*   [2 Instalação/Configuração](#Instala.C3.A7.C3.A3o.2FConfigura.C3.A7.C3.A3o)
    *   [2.1 Kernel](#Kernel)
    *   [2.2 Wireless](#Wireless)
    *   [2.3 Áudio](#.C3.81udio)
    *   [2.4 Vídeo](#V.C3.ADdeo)
    *   [2.5 Touchpad](#Touchpad)
    *   [2.6 Webcam](#Webcam)
    *   [2.7 Hotkeys](#Hotkeys)
    *   [2.8 Bluetooth](#Bluetooth)
    *   [2.9 Leitor de Cartão](#Leitor_de_Cart.C3.A3o)
*   [3 Veja também](#Veja_tamb.C3.A9m)

## Especificações

| Modelo | HP Mini 210-1040br |
| Processador | Intel Atom N450 (1.66 GHz, 512 KB L2 cache, 667 MHz FSB) [(Intel Atom in Wikipedia)](https://en.wikipedia.org/wiki/List_of_Intel_Atom_microprocessors#.22Pineview.22_.2845_nm.29 "wikipedia:List of Intel Atom microprocessors") |
| Arquitetura | x86_64 |
| Tela | LED HD 10.1" (1024x600) |
| RAM | 2GB 667 |
| HDD | 250GB 7200RPM HDD (Seagate SATA II) [(Seagate)](http://www.seagate.com/ww/v/index.jsp?name=st9250410as-momentus-7200.4-sata-250-gb-hd&vgnextoid=e9f188b2ea9dd110VgnVCM100000f5ee0a0aRCRD&locale=en-US) |
| Bateria | 6 células, aproximadamente 6 horas de duração utilizando rede sem fio |
| Drive Óptico | Nenhum |
| Gráfico | Intel Graphics Media Accelerator HD (3150) (Integrado ao processador) [(Intel GMA in Wikipedia)](https://en.wikipedia.org/wiki/Intel_GMA#Specifications "wikipedia:Intel GMA") |
| LAN | Realtek Semiconductor Co., Ltd. RTL8101E/RTL8102E |
| Wireless/Bluetooth | Broadcom Corporation BCM4312 802.11b/g |
| Webcam | 0.3 Megapixel |
| Leitor de Cartão | Secure Digital, MultiMedia, Memory Stick, Memory Stick Pro, ou xD-Picture cards |
| Conexões | 3 USB 2.0, 1 VGA, 1 porta Ethernet |

## Instalação/Configuração

**ISO**: 2010-05 (64 bits) netinstall.

### Kernel

Kernel padrão do arch (x86_64), não apresentou problemas no boot, não precisando de parâmetros adicionais.

### Wireless

Siga as instruções contidas em [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless"), sendo necessário ter [instalados](/index.php/Instala "Instala") os pacotes [b43-firmware](https://aur.archlinux.org/packages/b43-firmware/) e [b43-fwcutter](https://www.archlinux.org/packages/?name=b43-fwcutter) ou o driver proprietário [broadcom-wl](https://www.archlinux.org/packages/?name=broadcom-wl).

Com ele, seu atalho para rede wireless do teclado funcionará normalmente.

### Áudio

[Instale](/index.php/Instale "Instale") [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) e execute *alsaconf*. Então, inicie *alsamixer* e mute o *Beep*, do contrário sairá um beep estranho ao desligar/reiniciar. Salve as configurações com `alsactl store`.

### Vídeo

Funcionando com [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) (não testei outros) sem configurações adicionais. Não testada saída VGA.

### Touchpad

Funcionando, 3 botões. Canto superior direito (middle-button), inferior direito (right-button), rolagem vertical (borda direita) e horizontal (borda inferior). [Instale](/index.php/Instale "Instale") [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) para o driver do synaptics.

Configurações do arquivo `/etc/X11/xorg.conf.d/10-synaptics.conf`:

 `/etc/X11/xorg.conf.d/10-synaptics.conf` 
```
Section "InputClass"
    Identifier "touchpad catchall"
    Driver "synaptics"
    MatchIsTouchpad "on"
        Option "TapButton1" "1"
        Option "TapButton2" "2"
        Option "TapButton3" "3"
        Option "RBCornerButton" "3"
        Option "RTCornerButton" "2"
EndSection

```

Comente/apague a seção de touchpad do arquivo `/etc/X11/xorg.conf.d/10-evdev.conf`. Para mais configurações, veja [synaptics(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/synaptics.4).

### Webcam

Funcionando, não são necessárias configurações adicionais. Testada apenas no programa [cheese](https://www.archlinux.org/packages/?name=cheese) de [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/).

### Hotkeys

Caso queira trocar a configuração padrão de pressionar "fn" para habilitar as funções de F1, F2, etc, basta mudar na BIOS e a segunda função passa a ser os atalhos de volume etc.

Todas funcionando, excceto:

*   f12/Wireless (desliga mas não liga, somente driver b43), precisando do programa *rfkill* do [util-linux](https://www.archlinux.org/packages/?name=util-linux).

Listar interfaces de rede:

```
$ rfkill list

```

Desbloquear wireless

```
# rfkill ublock 0
# rfkill ublock 2

```

Agora poderá usar novamente wireless/Bluetooh.

*   f4 alterna modos entre tela do notebook e saída vga. *Não funciona.*

### Bluetooth

Funcionando com [broadcom-wl](https://www.archlinux.org/packages/?name=broadcom-wl). Ver [Bluetooth](/index.php/Bluetooth "Bluetooth") para configurações, GUIs e etc.

### Leitor de Cartão

*Não testado.*

## Veja também

*   [Página de suporte do HP Mini 210-1040BR no site da HP](https://support.hp.com/br-pt/product/HP-Mini-210-PC-series/4075896/model/4126174)