## Contents

*   [1 Especificações](#Especifica.C3.A7.C3.B5es)
*   [2 Instalação/Configuração](#Instala.C3.A7.C3.A3o.2FConfigura.C3.A7.C3.A3o)
    *   [2.1 Kernel](#Kernel)
    *   [2.2 Wireless](#Wireless)
    *   [2.3 Audio](#Audio)
    *   [2.4 Video](#Video)
    *   [2.5 Touchpad](#Touchpad)
    *   [2.6 Webcam](#Webcam)
    *   [2.7 Hotkeys](#Hotkeys)
    *   [2.8 Bluetooth](#Bluetooth)
    *   [2.9 Leitor de Cartão](#Leitor_de_Cart.C3.A3o)

## Especificações

| Modelo | HP Mini 210-1040br |
| Processador | Intel Atom N450 (1.66 GHz, 512 KB L2 cache, 667 MHz FSB) [Intel Atom (Wikipedia)](https://en.wikipedia.org/wiki/List_of_Intel_Atom_microprocessors#.22Pineview.22_.2845_nm.29_3) |
| Arquitetura | x86_64 |
| Tela | LED HD 10.1" (1024x600) |
| RAM | 2GB 667 |
| HDD | 250GB 7200RPM HDD (Seagate SATA II) [Seagate](http://www.seagate.com/ww/v/index.jsp?name=st9250410as-momentus-7200.4-sata-250-gb-hd&vgnextoid=e9f188b2ea9dd110VgnVCM100000f5ee0a0aRCRD&locale=en-US) |
| Bateria | 6 células, aproximadamente 6 horas de duração utilizando rede sem fio |
| Drive Óptico | Nenhum |
| Gráfico | Intel Graphics Media Accelerator HD (3150) (Integrado ao processador) [Intel GMA (Wikipedia)](https://en.wikipedia.org/wiki/Intel_GMA#Specifications) |
| LAN | Realtek Semiconductor Co., Ltd. RTL8101E/RTL8102E |
| Wireless/Bluetooth | Broadcom Corporation BCM4312 802.11b/g |
| Webcam | 0.3 Megapixel |
| Leitor de Cartão | Secure Digital, MultiMedia, Memory Stick, Memory Stick Pro, ou xD Picture cards |
| Conexões | 3 USB 2.0, 1 VGA, 1 RJ-45 |

## Instalação/Configuração

**ISO**: 2010-05 (64 bits) netinstall.

### Kernel

Kernel padrão do arch (x86_64), não aprensentou problemas no boot, não precisando de parâmetros adicionais.

### Wireless

Siga as instruções contidas em [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless"), necessários os pacotes:

*   [b43-firmware](https://aur.archlinux.org/packages/b43-firmware/)
*   b43-fwcutter:

```
# pacman -S b43-fwcutter

```

Ou use o driver proprietário:

*   [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/)

Com ele, seu atalho para rede wireless do teclado funcionará normalmente.

### Audio

Instale o alsa:

```
# pacman -S alsa-utils

```

e rode alsaconf:

```
# alsaconf

```

Após configurar entre no alsamixer e mute o "Beep", caso contrário sairá um beep estranho ao desligar/reiniciar:

```
# alsamixer

```

Salve as configurações:

```
# alsactl store

```

### Video

Funcionando com xf86-video-intel (não testei outros) sem configurações adicionais. Não testada saída VGA.

### Touchpad

Funcionando, 3 botões. Canto superior direito (middle-button), inferior direito (right-button), bolagem vertical (borda direita) e horizontal (borda inferior). Instale o driver do synaptics:

```
# pacman -S xf86-input-synaptics

```

Configurações do arquivo /etc/X11/xorg.conf.d/10-synaptics.conf:

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

Comente/apague a seção de touchpad do arquivo /etc/X11/xorg.conf.d/10-evdev.conf. Para mais configurações:

```
$ man synaptics

```

### Webcam

Funcionando, não são necessárias configurações adicionais. Testada apenas no programa Cheese (gnome-extra).

### Hotkeys

Caso queira trocar a configuração padrão de apertar "fn" para habilitar os f1, f2, etc, basta mudar na bios e a segunda função passa a ser os atalhos de volume e etc. Todas funcionando. Exceto:

*   f12/Wireless (desliga mas não liga, somente driver b43), necesserário programa rfkill para ligar.

```
# pacman -S rfkill

```

Listar interfaces de rede:

```
# rfkill list

```

Desbloquear wireless

```
# rfkill ublock 0
# rfkill ublock 2

```

Agora poderá usar novamente wireless/bluetooh.

*   f4 alterna modos entre tela do notebook e saída vga. *Não funciona.*

### Bluetooth

Funcionando com o driver broadcom-wl ([AUR](/index.php/AUR "AUR")). Ver [Bluetooth](/index.php/Bluetooth "Bluetooth") para configurações, GUIs e etc.

### Leitor de Cartão

*Não testado.*