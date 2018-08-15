**Status de tradução:** Esse artigo é uma versão localizada de [Localization](/index.php/Localization "Localization"). Data da última tradução: 2018-08-14\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Localization&diff=0&oldid=535059) na versão em inglês.

Este é o artigo principal sobre [localização](https://en.wikipedia.org/wiki/pt:Internacionaliza%C3%A7%C3%A3o_(inform%C3%A1tica) (muitas vezes também conhecido como l10n). Destina-se a oferecer orientação, bem como reticulação de outros artigos relevantes, para personalizar as configurações de uma instalação do Arch Linux para trabalhar com qualquer idioma suportado.

O artigo faz uso de subpáginas para instruções específicas para idiomas:

*   [Localization/Chinese](/index.php/Localization/Chinese "Localization/Chinese")
*   [Localization/Indic](/index.php/Localization/Indic "Localization/Indic")
    *   [Localization/Sinhalese](/index.php/Localization/Sinhalese "Localization/Sinhalese")
*   [Localization/Japanese](/index.php/Localization/Japanese "Localization/Japanese")
*   [Localization/Korean](/index.php/Localization/Korean "Localization/Korean")

Subpáginas sem uma contraparte em inglês:

*   [ru:Localization/Russian](https://wiki.archlinux.org/index.php/Localization/Russian_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ru:Localization/Russian")
*   [sk:Localization/Slovak](https://wiki.archlinux.org/index.php/Localization/Slovak_(Slovensk%C3%BD) "sk:Localization/Slovak")

## Contents

*   [1 Fontes](#Fontes)
*   [2 Locale](#Locale)
*   [3 Layouts de teclado](#Layouts_de_teclado)
*   [4 Métodos de entrada](#M.C3.A9todos_de_entrada)
    *   [4.1 Mecanismos de método de entrada](#Mecanismos_de_m.C3.A9todo_de_entrada)
    *   [4.2 Método de GTK IM](#M.C3.A9todo_de_GTK_IM)
        *   [4.2.1 Desabilitando módulos de GTK IM (sem desinstalar)](#Desabilitando_m.C3.B3dulos_de_GTK_IM_.28sem_desinstalar.29)
    *   [4.3 QT immodule (> QT 4.0.0)](#QT_immodule_.28.3E_QT_4.0.0.29)
        *   [4.3.1 Desabilitando módulos QT IM (sem desinstalar)](#Desabilitando_m.C3.B3dulos_QT_IM_.28sem_desinstalar.29)
*   [5 Veja também](#Veja_tamb.C3.A9m)

## Fontes

Para obter a lista de pacotes de fontes disponíveis no Arch Linux, consulte o artigo [Fonts](/index.php/Fonts "Fonts").

## Locale

Veja [Locale (Português)](/index.php/Locale_(Portugu%C3%AAs) "Locale (Português)").

## Layouts de teclado

Veja [Configuração de teclado no console](/index.php/Configura%C3%A7%C3%A3o_de_teclado_no_console "Configuração de teclado no console") e [Configuração de teclado no Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg").

## Métodos de entrada

De [Fedora:I18N/InputMethods](https://fedoraproject.org/wiki/I18N/InputMethods "fedora:I18N/InputMethods"):

	Um [método de entrada](https://en.wikipedia.org/wiki/pt:M%C3%A9todo_de_entrada "wikipedia:pt:Método de entrada") (IM, abreviação da palavra inglesa *input method*) é uma maneira de inserir um determinado conjunto de caracteres e símbolos, geralmente porque um teclado não os suporta diretamente.

A maioria dos métodos de entrada faz parte de um **framework de IM**, que permite ao usuário alternar facilmente entre vários métodos de entrada. Esses métodos de entrada são incluídos na estrutura ou empacotados separadamente. Os programas que implementam métodos de entrada são chamados de **mecanismos de IM** *(IM engines)*. Os métodos de entrada disponíveis para um idioma são listados na subpágina do respectivo idioma.

As frameworks de IM disponíveis são:

*   **[Fcitx](/index.php/Fcitx "Fcitx")** — Estrutura do método de entrada com suporte de extensão.

	[https://fcitx-im.org/](https://fcitx-im.org/) || [fcitx](https://www.archlinux.org/packages/?name=fcitx)

*   **[gcin](/index.php/Gcin "Gcin")** — Servidor do método de entrada com suporte a vários métodos de entrada.

	[http://hyperrate.com/dir.php?eid=67](http://hyperrate.com/dir.php?eid=67) || [gcin](https://www.archlinux.org/packages/?name=gcin)

*   **Hime** — Plataforma do método de entrada universal.

	[https://hime-ime.github.io/](https://hime-ime.github.io/) || [hime-git](https://aur.archlinux.org/packages/hime-git/)

*   **[IBus](/index.php/IBus "IBus")** — Intelligent Input Bus, uma framework de entrada de próxima geração.

	[https://github.com/ibus/ibus/wiki](https://github.com/ibus/ibus/wiki) || [ibus](https://www.archlinux.org/packages/?name=ibus)

*   **[Nimf](/index.php/Nimf "Nimf")** — Uma framework de método de entrada multilíngue que herda [Dasom](/index.php/Dasom "Dasom").

	[https://gitlab.com/nimf-i18n/nimf](https://gitlab.com/nimf-i18n/nimf) || [nimf](https://aur.archlinux.org/packages/nimf/)

*   **[SCIM](/index.php/SCIM "SCIM")** — A plataforma Smart Common Input Method.

	[https://github.com/scim-im/scim](https://github.com/scim-im/scim) || [scim](https://www.archlinux.org/packages/?name=scim)

*   **[uim](/index.php/Uim "Uim")** — Framework de método de entrada multilíngue para fornecer plataforma de desenvolvimento de método de entrada de código simples, facilmente extensível e de alta qualidade, e ambiente de método de entrada útil para usuários de plataformas de desktop e embarcadas.

	[https://github.com/uim/uim](https://github.com/uim/uim) || [uim](https://www.archlinux.org/packages/?name=uim)

Não mantidas:

*   **[Dasom](/index.php/Dasom "Dasom")** — Framework multilíngue de método de entrada.

	[https://dasom-im.github.io/](https://dasom-im.github.io/) || [dasom-git](https://aur.archlinux.org/packages/dasom-git/)

Veja também [Wikipedia:List of input methods for Unix platforms](https://en.wikipedia.org/wiki/List_of_input_methods_for_Unix_platforms "wikipedia:List of input methods for Unix platforms").

### Mecanismos de método de entrada

| Idioma | Back-end | [Fcitx](/index.php/Fcitx "Fcitx") | [IBus](/index.php/IBus "IBus") | [SCIM](/index.php/SCIM "SCIM") | [uim](/index.php/Uim "Uim") | [gcin](/index.php/Gcin "Gcin") | Hime |
| Vietnamita | [UniKey](http://www.unikey.org/linux.php) | [fcitx-unikey](https://www.archlinux.org/packages/?name=fcitx-unikey) | [ibus-unikey](https://www.archlinux.org/packages/?name=ibus-unikey) | [scim-unikey](https://github.com/scim-im/scim-unikey) | - | - | - |
| Outros | [m17n-lib](https://www.archlinux.org/packages/?name=m17n-lib) | [fcitx-m17n](https://www.archlinux.org/packages/?name=fcitx-m17n) | [ibus-m17n](https://www.archlinux.org/packages/?name=ibus-m17n) | [scim-m17n](https://www.archlinux.org/packages/?name=scim-m17n) | depende |  ? |  ? |

### Método de GTK IM

*   [SCIM](/index.php/SCIM "SCIM") com o módulo FrontEnd do soquete se liga ao GTK Im-Module
*   [uim](/index.php/Uim "Uim")
*   [fcitx](/index.php/Fcitx "Fcitx")

#### Desabilitando módulos de GTK IM (sem desinstalar)

Primeiro, algumas informações básicas sobre como o GTK carrega e seleciona os módulos de IM:

*   Especificando um módulo de IM

1.  variável de ambiente `GTK_IM_MODULE`
    1.  GTK_IM_MODULE="scim" gedit
2.  Valor de `XSETTINGS` de Gtk/IMModule

*   Arquivo listando módulos de IM possíveis

1.  variável de ambiente `GTK_IM_MODULE_FILE`
2.  Arquivos RC
3.  `/etc/gtk-2.0/gtk.immodules`

Se nenhum módulo de IM for especificado (via GTK_IM_MODULE ou em XSETTINGS), então o GTK escolherá automaticamente um immodule adequado de uma listagem interna (GTK_IM_MODULE_FILE... etc). Este módulo de IM escolhido dependerá do software instalado e será escolhido em uma ordem completamente arbitrária.

Para uma listagem de immodules GTK+ instalados, veja

*   `/usr/lib/gtk-2.0/modules/`
*   `/usr/lib/gtk-2.0/2.10.0/immodules/`

XSETTINGS fornece uma API comum para definir configurações comuns da área de trabalho. Sistemas de configuração de banco de dados semelhantes, como gnome-config, GConf, liproplist e o sistema de configuração kde, já existem, no entanto, o XSETTINGS unifica esses sistemas. Os daemons XSETTINGS, como gnome-settings-daemon do gnome, xfce-mcs-manager do xfce4 e outros do openbox, etc., enviam dados específicos do ambiente de desktop para o banco de dados XSETTINGS. Tecnicamente, XSETTINGS é um meio de armazenamento simples destinado a armazenar apenas strings, inteiros e cores. Quando um gerenciador XSETTINGS é encerrado, os clientes restauram todas as configurações para seus valores padrão.

Se o GTK+ tem a depuração habilitada, os módulos carregados podem ser vistos com

```
$ *aplicativo* --gtk-debug modules

```

Caso contrário, os módulos podem ser vistos pela verificação das bibliotecas vinculadas no gdb após a anexação ao processo.

Para evitar que o GTK+ carregue qualquer módulo de IM

*   defina `GTK_IM_MODULE` para uma string vazia, ou
*   defina `GTK_IM_MODULE` para "gtk-im-context-simple"

### QT immodule (> QT 4.0.0)

*   [SCIM](/index.php/SCIM "SCIM") com o módulo FrontEnd do soquete se liga ao GTK Im-Module
*   [uim](/index.php/Uim "Uim")
*   [fcitx](/index.php/Fcitx "Fcitx")

#### Desabilitando módulos QT IM (sem desinstalar)

QT vai carregar o módulo IM especificado em `QT_IM_MODULE` e, se removida a definição, tenta retroceder para XIM.

1.  variável de ambiente `QT_IM_MODULE`
2.  XIM

Para desabilitar o carregamento de módulo de método de entrada no QT, [exporte](/index.php/Exporte "Exporte") `QT_IM_MODULE="simple"`.

## Veja também

*   [Wiki do Gentoo](https://wiki.gentoo.org/wiki/Localization "gentoo:Localization")
*   [Wiki do Fedora](https://fedoraproject.org/wiki/I18N/InputMethods "fedora:I18N/InputMethods")
*   [Free Standards Group OpenI18N](http://www.openi18n.org/)
*   [Especificação XSETTINGS 0.5](http://standards.freedesktop.org/xsettings-spec/xsettings-spec-0.5.html)
*   [Executando e depurando aplicativos GTK+](https://developer.gnome.org/gtk3/unstable/gtk-running.html)