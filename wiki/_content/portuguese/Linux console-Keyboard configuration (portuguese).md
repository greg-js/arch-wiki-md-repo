**Status de tradução:** Esse artigo é uma tradução de [Keyboard configuration in console](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console"). Data da última tradução: 2018-12-29\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Keyboard_configuration_in_console&diff=0&oldid=560841) na versão em inglês.

Artigos relacionados

*   [Xorg/Keyboard configuration](/index.php/Xorg/Keyboard_configuration "Xorg/Keyboard configuration")
*   [Entrada de teclado](/index.php/Keyboard_input "Keyboard input")
*   [Console do Linux#Fontes](/index.php/Console_do_Linux#Fontes "Console do Linux")

Mapeamentos de teclado (conhecido pela abreviação inglesa como *keymaps*) para [console virtual](https://en.wikipedia.org/wiki/Virtual_console do sistema quanto as configurações de layout do teclado para o console virtual e o Xorg.

## Contents

*   [1 Vendo as configurações do teclado](#Vendo_as_configurações_do_teclado)
*   [2 Mapas de teclado](#Mapas_de_teclado)
    *   [2.1 Listando mapas de teclado](#Listando_mapas_de_teclado)
    *   [2.2 Loadkeys](#Loadkeys)
    *   [2.3 Configuração persistente](#Configuração_persistente)
    *   [2.4 Criando um mapa de teclado personalizado](#Criando_um_mapa_de_teclado_personalizado)
        *   [2.4.1 Adicionando diretivas](#Adicionando_diretivas)
        *   [2.4.2 Outros exemplos](#Outros_exemplos)
        *   [2.4.3 Salvando alterações](#Salvando_alterações)
*   [3 Ajustando o atraso e a taxa de digitação](#Ajustando_o_atraso_e_a_taxa_de_digitação)
    *   [3.1 Serviço do systemd](#Serviço_do_systemd)

## Vendo as configurações do teclado

Use `localectl status` para ver as configurações atuais de teclado.

## Mapas de teclado

Os arquivos de mapas de teclado são armazenados na árvore de diretórios `/usr/share/kbd/keymaps/`. Geralmente, um arquivo de mapa de teclado corresponde a um layout de teclado (a instrução `include` pode ser usada para compartilhar partes comuns e um arquivo de mapa de teclado pode conter vários layouts com alguma combinação de teclas usada para alternar). Para mais detalhes, veja [keymaps(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/keymaps.5).

### Listando mapas de teclado

As convenções de nomenclatura dos mapas de teclado do console são um pouco arbitrárias, mas geralmente são baseadas em:

*   [Códigos de idioma](https://en.wikipedia.org/wiki/ISO_639-1 "wikipedia:ISO 639-1"): sendo que código de idioma (em inglês *language codes*) é o mesmo que seu código de país (ex., `de` para alemão ou `fr` para francês).
*   [Códigos de país](https://en.wikipedia.org/wiki/pt:C%C3%B3digo_de_pa%C3%ADs "wikipedia:pt:Código de país"): sendo que as variações do mesmo idioma são usadas em diferentes países (ex., `uk` para inglês do Reino Unido ou `us` para inglês dos Estados Unidos); uma lista de códigos de país também pode ser encontrada em [wikipedia:ISO 3166-1#Officially assigned code elements](https://en.wikipedia.org/wiki/ISO_3166-1#Officially_assigned_code_elements "wikipedia:ISO 3166-1").
*   [Layouts de teclado](https://en.wikipedia.org/wiki/Keyboard_layout "wikipedia:Keyboard layout"): sendo que o layout não está relacionado a um país ou idioma em particular (ex., `dvorak` para o [layout de teclado Dvorak](https://en.wikipedia.org/wiki/pt:Teclado_Simplificado_Dvorak "wikipedia:pt:Teclado Simplificado Dvorak")).

Para obter uma lista de todos os mapas de teclado disponíveis, use o comando:

```
$ localectl list-keymaps

```

Para procurar um mapa de teclado, use o seguinte comando, substituindo `*termo_de_pesquisa*` pelo código do seu idioma, país ou layout:

```
$ localectl list-keymaps | grep -i *termo_de_pesquisa*

```

Alternativamente, usando o *find*:

```
$ find /usr/share/kbd/keymaps/ -type f

```

### Loadkeys

É possível definir um mapa de teclado apenas para a sessão atual. Isso é útil para testar diferentes mapas de teclado, resolver problemas etc.

A ferramenta *loadkeys* é usada para este propósito, é usada internamente pelo [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") ao carregar o mapa de teclas configurado no `/etc/vconsole.conf`. Pode ser usado muito simplesmente para este propósito:

```
# loadkeys *mapa_de_teclado*

```

Veja [loadkeys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1) para detalhes.

### Configuração persistente

Um mapa de teclado persistente pode ser configurado em `/etc/vconsole.conf`, que é lido por [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") na inicialização. A variável `KEYMAP` é usada para especificar o mapa de teclado. Se a variável estiver vazia ou não definida, o mapa de teclado `us` será usado como valor padrão. Veja [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5) para todas as opções. Por exemplo:

 `/etc/vconsole.conf` 
```
KEYMAP=br-abnt2
...

```

Por conveniência, *localectl* pode ser usado para definir o mapa de teclado do console. Ele irá alterar a variável `KEYMAP` em `/etc/vconsole.conf` e também definirá o mapa de teclado da sessão atual:

```
$ localectl set-keymap --no-convert *mapa_de_teclado*

```

A opção `--no-convert` pode ser usada para evitar que o `localectl` altere automaticamente o [mapa de teclado do Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg") para a correspondência mais próxima. Veja [localectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/localectl.1) para mais informações.

Se necessário, o mapa de teclado do `/etc/vconsole.conf` pode ser carregado anteriormente no espaço de usuário pelo [hook de mkinitcpio](/index.php/Mkinitcpio#Common_hooks "Mkinitcpio") `keymap`.

### Criando um mapa de teclado personalizado

Ao usar o console, você pode usar teclas de atalho *(hotkeys)* para imprimir um caractere específico. Além disso, podemos também imprimir uma sequência de caracteres e algumas sequências de escape. Assim, se imprimirmos a sequência de caracteres que constituem um comando e depois um caractere de escape para uma nova linha, esse comando será executado.

Um método de fazer isso é editar o arquivo de mapa de teclado. No entanto, como ele será reescrito sempre que o pacote ao qual ele pertence for atualizado, a edição desse arquivo não será incentivada. É melhor integrar o mapa de chaves existente com um mapa de teclado pessoal. O utilitário `loadkeys` pode fazer isso.

Primeiro, crie um arquivo de mapa de teclado. Esse arquivo de mapa de teclado pode estar em qualquer lugar, mas um método é imitar a hierarquia de diretórios em `/usr/local`:

```
# mkdir -p /usr/local/share/kbd/keymaps
# vim /usr/local/share/kbd/keymaps/personal.map

```

Como um comentário adicional, vale a pena notar que um mapa de teclado pessoal também é útil para redefinir o comportamento de teclas já tratadas pelo mapa de teclado padrão: quando carregado com `loadkeys`, as diretivas no mapa de teclado padrão serão substituídas quando eles entram em conflito com as novas diretivas e serão conservadas. Dessa forma, somente as alterações no mapa de teclas devem ser especificadas no mapa de teclado pessoal.

**Dica:** Você também pode editar um mapa de teclado existente localizado na árvore de diretórios `/usr/share/kbd/keymaps/`. Os mapas de teclado têm uma extensão *.map.gz* de forma que, por exemplo, `us.map.gz` é um mapa de teclado americano. Basta copiar o mapa de teclado para `/usr/local/share/kbd/keymaps/personal.map.gz` e executar *gunzip* nele.

#### Adicionando diretivas

Dois tipos de diretivas são necessários neste mapa de teclado pessoal. Em primeiro lugar, as diretivas [*keycode*](/index.php/Extra_keyboard_keys "Extra keyboard keys"), que correspondem ao formato visto nos mapas de teclado padrão. Essas diretivas associam um *keycode* (código de teclas) a um *keysym* (símbolo de teclas). *Keysyms* representam ações do teclado. As ações disponíveis incluem a saída de códigos de caracteres ou sequências de caracteres, consoles de comutação ou mapas de teclado, inicialização da máquina e muitas outras ações. O mapa de teclado completo atualmente ativo pode ser obtido com

```
# dumpkeys -l

```

A maioria dos *keysyms* é intuitiva. Por exemplo, para definir tecla 112 para a retornar um "e", a diretiva será:

```
keycode 112  = e

```

Para definir a tecla 112 para retornar um símbolo de euro, a diretiva será:

```
keycode 112 = euro

```

Algumas *keysyms* não são imediatamente conectadas a ações de um teclado. Em particular, as *keysyms* prefixadas por um F maiúsculo e um a três dígitos (F1-F246) constituindo um número maior que 30 estão sempre livres. Isso é útil para direcionar a *hotkey* para retornar uma sequência de caracteres e outras ações:

```
keycode 112 = F70

```

Então, F70 pode ser vinculado para retornar um texto específico:

```
string F70 = "Opa"

```

Quando a tecla 112 é pressionada, ela mostrará o conteúdo de F70\. Para executar um comando impresso em um terminal, um caractere de escape de nova linha deve ser anexado ao final da string de comando. Por exemplo, para inserir um sistema na hibernação, o seguinte mapa de teclado é adicionado:

```
string F70 = "sudo /usr/sbin/hibernate
"

```

#### Outros exemplos

*   Para fazer a tecla Alt da Direta ser o mesmo que a tecla Alt da Esquerda (para Emacs), use a seguinte linha em seu mapa de teclado. Isso vai incluir o arquivo `/usr/share/kbd/keymaps/i386/include/linux-with-two-alt-keys.inc` – acesse-o para detalhes.

```
include "linux-with-two-alt-keys"

```

*   Para trocar CapsLock com Escape (para Vim), remapeie os respectivos *keycodes*:

```
keycode 1 = Caps_Lock
keycode 58 = Escape

```

*   Para fazer o CapsLock uma outra tecla Control, remapeie o respectivo *keycode*:

```
keycode 58 = Control

```

*   Para trocar CapsLock com a tecla Control da Esquerda, remapeie as respectivas *keycodes*:

```
keycode 29 = Caps_Lock
keycode 58 = Control

```

#### Salvando alterações

Para fazer uso do mapa de teclado pessoal, ele deve ser carregado com *loadkeys*:

```
$ loadkeys /usr/local/share/kbd/keymaps/personal.map

```

No entanto, este mapa de teclado está ativo apenas para a sessão atual. Para carregar o mapa de teclado na inicialização, especifique o caminho completo para o arquivo na variável `KEYMAP` em [/etc/vconsole.conf](#Configuração_persistente). O arquivo não precisa ser compactado como os mapas de teclado oficiais fornecidos pelo [kbd](https://www.archlinux.org/packages/?name=kbd).

## Ajustando o atraso e a taxa de digitação

O "atraso de digitação" *(typematic delay)* indica a quantidade de tempo (normalmente em milissegundos) que uma tecla precisa ser pressionada e mantida para que o processo de repetição comece. Após o processo de repetição ter sido acionado, o caractere será repetido com uma certa frequência (geralmente dada em Hz) especificada pela "taxa de digitação" *(typematic rate)*. Estes valores podem ser alterados usando o comando *kbdrate*. Observe que essas configurações são configuradas separadamente para o console virtual e [para o Xorg](/index.php/Keyboard_configuration_in_Xorg#Adjusting_typematic_delay_and_rate "Keyboard configuration in Xorg").

```
# kbdrate [-d *atraso*] [-r *taxa*]

```

Por exemplo, para definir um atraso de digitação para 200ms e uma taxa de digitação para 30Hz, use o seguinte comando:

```
# kbdrate -d 200 -r 30

```

A emissão do comando sem especificar o atraso e a taxa vai redefinir os valores de digitação para seus respectivos padrões; um atraso de 250ms e uma taxa de 11Hz:

```
# kbdrate

```

### Serviço do systemd

Um serviço de systemd pode ser usado para definir a taxa de teclado. Por exemplo:

 `/etc/systemd/system/kbdrate.service` 
```

[Unit]
Description=Keyboard repeat rate in tty.

[Service]
Type=oneshot
RemainAfterExit=yes
StandardInput=tty
StandardOutput=tty
ExecStart=/usr/bin/kbdrate -s -d 450 -r 60

[Install]
WantedBy=multi-user.target

```

Então [inicie/habilite](/index.php/Inicie/habilite "Inicie/habilite") o serviço de systemd `kbdrate.service`.