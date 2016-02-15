A variável KEYMAP é especificada no arquivo [`/etc/vconsole.conf`](/index.php/Systemd#Console_and_keymap "Systemd") (`/etc/rc.conf` usando o arquivo legado rc.conf). Ele define qual layout de teclado, ou como comumente é chamado _keymap_, será usado nos consoles virtuais. Os arquivos de layout de teclados são fornecidos pelo pacote [kbd](https://www.archlinux.org/packages/?name=kbd).

## Layout do Teclado

Esta lista apresenta os arquivos de configuração para os layouts de teclados mais comuns. Usualmente a extensão "map.gz" pode ser ignorada. A maioria dos keymaps é encontrada no diretório: `/usr/share/kbd/keymaps/i386/_layout_` (_layout_=qwerty, azerty, dvorak, etc.).

Os mapas do teclado do Arch Linux menos comuns são encontrados no diretório `/usr/share/kbd/keymaps/_architecture_` (_architecture_=ppc, mac, etc).

**Nota:** Se estes keymaps não funcionarem para você, tente remover o `map.gz` do nome do keymap. Se isto não funcionar, verifique se o arquivo keymap existe no diretório `/usr/share/kbd/keymaps/` usando o comando `find`: `find /usr/share/kbd/keymaps/ -name "*[keymap desejado]*"`

| Teclado | Parâmetro |
| Belga | `KEYMAP="be-latin1.map.gz"` |
| Português Brasileiro | `KEYMAP="br-abnt2.map.gz"` |
| Franco Canadense | `KEYMAP="cf.map.gz"` |
| Canadense multilíngua (Disponível no _[AUR](/index.php/Arch_User_Repository "Arch User Repository")_) | `KEYMAP="ca_multi.map.gz"` |
| Colemak _(US)_ | `KEYMAP="colemak"` |
| Croata | `KEYMAP="croat.map.gz"` |
| Tcheco | `KEYMAP="cz-lat2.map.gz"` |
| Dvorak | `KEYMAP="dvorak"` |
| Francês | `KEYMAP="fr-latin9.map.gz"` |
| Alemão | `KEYMAP="de-latin1.map.gz"` |
| Alemão _(no dead keys)_ | `KEYMAP="de-latin1-nodeadkeys.map.gz"` |
| Italiano | `KEYMAP="it.map.gz"` |
| Lituano _(qwerty)_ | `KEYMAP="lt.baltic.map.gz"` |
| Norueguês | `KEYMAP="no-latin1.map.gz"` |
| Polonês | `KEYMAP="pl.map.gz"` |
| Português | `KEYMAP="pt-latin9.map.gz"` |
| Romeno | `KEYMAP="ro_win.map.gz"` |
| Russo | `KEYMAP="ru4.map.gz"` |
| Singapura | `KEYMAP="sg-latin1.map.gz"` |
| Esloveno | `KEYMAP="slovene"` |
| Sueco | `KEYMAP="sv-latin1.map.gz"` |
| Suíça-Francesa | `KEYMAP="fr_CH-latin1.map.gz"` |
| Suíça-Alemã | `KEYMAP="de_CH-latin1.map.gz"` |
| Espanhol | `KEYMAP="es.map.gz"` |
| Espanhol Latino Americano | `KEYMAP="la-latin1.map.gz"` |
| Turco | `KEYMAP="tr_q-latin5.map.gz"` |
| Ucraniâno | `KEYMAP="ua.map.gz"` |
| Reino Unido | `KEYMAP="uk"` |

## Personalização de Layout

1.  `cd` `/usr/share/kbd/keymaps/i386/qwerty`
2.  Copie seu atual keymap (`br-abnt2.map.gz`) com um novo nome `abnt-personalizado.map.gz`
3.  `gunzip abnt-personalizado.map.gz`
4.  Edite `abnt-personalizado.map` usando seu editor preferido.Exemplo:
    *   **Trocar CapsLock pelo Escape (Vim)**
        `keycode 1 = Caps_Lock` e `keycode 58 = Escape`
5.  `gzip abnt-personalizado.map.gz`
6.  Troque o layout utilizado pelo o novo editando o arquivo `/etc/vconsole.conf`. Substitua a linha correspondente `KEYMAP=br-abnt2` por `KEYMAP=abnt-personalizado`
7.  Reinicie o computador para utilizar o novo layout ou faça: `setxkbmap -layout abnt-personalizado`