**Status de tradução:** Esse artigo é uma tradução de [Keyboard backlight](/index.php/Keyboard_backlight "Keyboard backlight"). Data da última tradução: 2019-10-13\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Keyboard_backlight&diff=0&oldid=584286) na versão em inglês.

Existem vários métodos para controlar o nível de brilho da *luz de fundo do teclado*.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Qualquer fornecedor](#Qualquer_fornecedor)
    *   [1.1 D-Bus](#D-Bus)

## Qualquer fornecedor

Há várias formas de gerenciar o nível de brilho e diferentes ferramentas auxiliares para realizar isso, tal como [brightnessctl](https://www.archlinux.org/packages/?name=brightnessctl) ou [light](https://www.archlinux.org/packages/?name=light).

O pseudo-sistema de arquivos `sys` expõe uma interface à luz de fundo do teclado. O atual nível de brilho pode ser obtido lendo `/sys/class/leds/tpacpi::kbd_backlight/brightness`. Por exemplo, para obter o nível máximo de brilho:

```
 cat /sys/class/leds/tpacpi::kbd_backlight/max_brightness

```

Para definir o brilho para 1:

```
 echo 1 | sudo tee /sys/class/leds/tpacpi::kbd_backlight/brightness

```

Ao usar `brightnessctl` você pode obter uma lista de controles de brilho disponíveis com `brightnessctl --list`, então para mostrar as informações de luz de fundo do kbd:

```
 brightnessctl --device='tpacpi::kbd_backlight' info

```

Isso mostrará o valor atual absoluto e relativo e o valor absoluto máximo. Para definir um valor diferente:

```
 brightnessctl --device='tpacpi::kbd_backlight' set 1

```

### D-Bus

Você pode controlar a luz de fundo do teclado do seu computador através da interface [D-Bus](/index.php/D-Bus "D-Bus"). Os benefícios de usá-lo são que nenhuma modificação nos arquivos do dispositivo é necessária e é independente do fornecedor.

Aqui está um exemplo de implementação no [Python](/index.php/Python "Python") 3.

[Instale](/index.php/Instale "Instale") os pacotes [upower](https://www.archlinux.org/packages/?name=upower) e [python-dbus](https://www.archlinux.org/packages/?name=python-dbus) e coloque o seguinte script em `/usr/local/bin/` e torne-o executável. Você pode mapear seus atalhos de teclado para executar `/usr/local/bin/kb-light.py + x` e `/usr/local/bin/kb-light.py - x` para aumentar e diminuir o nível de luz de fundo do teclado até `x`.

**Dica:** Você deve tentar com um x=1 para determinar os limites dos níveis de luz de fundo do teclado
 `/usr/local/bin/kb-light.py` 
```
#!/usr/bin/env python3

import dbus
import sys

def kb_light_set(delta):
    bus = dbus.SystemBus()
    kbd_backlight_proxy = bus.get_object('org.freedesktop.UPower', '/org/freedesktop/UPower/KbdBacklight')
    kbd_backlight = dbus.Interface(kbd_backlight_proxy, 'org.freedesktop.UPower.KbdBacklight')

    current = kbd_backlight.GetBrightness()
    maximum = kbd_backlight.GetMaxBrightness()
    new = max(0, min(current + delta, maximum))

    if 0 <= new  <= maximum:
        current = new
        kbd_backlight.SetBrightness(current)

    # Return current backlight level percentage
    return 100 * current / maximum

if __name__ ==  '__main__':
    if len(sys.argv) == 2 or len(sys.argv) == 3:
        if sys.argv[1] == "--up" or sys.argv[1] == "+":
            if len(sys.argv) == 3:
                print(kb_light_set(int(sys.argv[2])))
            else:
                print(kb_light_set(17))
        elif sys.argv[1] == "--down" or sys.argv[1] == "-":
            if len(sys.argv) == 3:
                print(kb_light_set(-int(sys.argv[2])))
            else:
                print(kb_light_set(-17))
        else:
            print("Unknown argument:", sys.argv[1])
    else:
        print("Script takes one or two argument.", len(sys.argv) - 1, "arguments provided.")

```

Alternativamente, o seguinte bash de uma linha irá definir a luz de fundo para o valor especificado no argumento:

```
setKeyboardLight () {
    dbus-send --system --type=method_call  --dest="org.freedesktop.UPower" "/org/freedesktop/UPower/KbdBacklight" "org.freedesktop.UPower.KbdBacklight.SetBrightness" int32:$1 
}

```