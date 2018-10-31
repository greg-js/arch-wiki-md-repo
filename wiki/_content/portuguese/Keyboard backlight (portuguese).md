**Status de tradução:** Esse artigo é uma tradução de [Keyboard backlight](/index.php/Keyboard_backlight "Keyboard backlight"). Data da última tradução: 2018-10-31\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Keyboard_backlight&diff=0&oldid=552138) na versão em inglês.

## Qualquer fornecedor

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

## Asus

**Atenção:** O seguinte caminho não é recomendado. Ele fornece permissões de gravação para qualquer pessoal para o arquivo de dispositivo de luz de fundo do teclado, o que significa que todo e qualquer usuário pode controlá-lo.

O arquivo de luz de fundo do teclado é geralmente bloqueado para edição. Para desbloquear este arquivo na inicialização, você precisará criar um serviço [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)").

 `/usr/lib/systemd/system/asus-kbd-backlight.service` 
```
[Unit]
Description=Asus Keyboard Backlight
Wants=systemd-backlight@leds:asus::kbd_backlight.service
After=systemd-backlight@leds:asus::kbd_backlight.service

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=/bin/chmod 666 /sys/class/leds/asus::kbd_backlight/brightness

[Install]
WantedBy=multi-user.target

```

Agora você pode usar um script de troca de luz de fundo do teclado. Por exemplo, veja [ASUS G55VW#keyboard backlight script](/index.php/ASUS_G55VW#keyboard_backlight_script "ASUS G55VW").

Para um exemplo de como você pode configurar um daemon minúsculo (executando-o como root) que edita esses arquivos, conecte-os a [dbus](/index.php/Dbus "Dbus") e mapeie as teclas de brilho do teclado para [dbus](/index.php/Dbus "Dbus") chamadas de método, consulte [[1]](https://github.com/GambolingPangolin/KbdBacklight).