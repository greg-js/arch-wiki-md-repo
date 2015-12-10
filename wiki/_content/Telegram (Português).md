# Telegram (Português)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Parte copiada do [Wikipedia](https://pt.wikipedia.org/wiki/Telegram_(aplicativo)): **Telegram** é uma aplicação multiplataforma de mensageiro instantâneo, com seu cliente em código aberto e servidores em software proprietário, tendo seu foco na segurança e privacidade. Além de mensagens de texto criptografadas e opcionalmente autodestrutivas, os usuários podem enviar fotos, vídeos e documentos (todos os tipos de arquivos suportados). Está oficialmente disponível para diversos dispositivos, como Android (incluindo tablets), iOS (incluindo iPad), Windows Phone (ainda em versão beta), Windows, OS X, Linux e um cliente web; outras plataformas e clientes alternativos podem existir a partir de desenvolvedores independentes que usam o API do Telegram.

## Instalação

Atualmente o repositório oficial ainda não possui pacotes relacionados，mas o AUR tem [telegram-desktop](https://aur.archlinux.org/packages/telegram-desktop/)<sup><small>AUR</small></sup>、[telegram-dev](https://aur.archlinux.org/packages/telegram-dev/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/telegram-dev)]</sup>、[telegram-desktop-cn](https://aur.archlinux.org/packages/telegram-desktop-cn/)<sup><small>AUR</small></sup> e outros. Para China, Japão e Coreia, você usar outros métodos de digitação, logo, é preciso instalar [telegram-desktop-cn](https://aur.archlinux.org/packages/telegram-desktop-cn/)<sup><small>AUR</small></sup>。

A partir da versão 0.8.50 do Telegram, foram consertados os problemas com métodos de entrada asiático, recomenda-se usar versoes posteriores. Pode ser necessário definir a variável de ambiente QT_IM_MODULE. Para mais detalhes, consulte [Fcitx #GTK+ and Qt modules](/index.php/Fcitx#GTK.2B_and_Qt_modules "Fcitx")

Você pode diretamente adicionar o repositóro chinês [archlinuxcn](/index.php/Unofficial_user_repositories#archlinuxcn "Unofficial user repositories") para instalar a versão chinesa：

 `# vim /etc/pacman.conf ` 

```
[archlinuxcn]
SigLevel = Optional TrustedOnly
Server = http://repo.archlinuxcn.org/$arch

```

```
# pacman -S archlinuxcn-keyring
# pacman -S telegram-desktop-cn

```

No AUR também exitem pacotes para usar [pidgin](/index.php/Pidgin "Pidgin"), que inclui [telegram-purple](https://aur.archlinux.org/packages/telegram-purple/)<sup><small>AUR</small></sup> e [telegram-purple-git](https://aur.archlinux.org/packages/telegram-purple-git/)<sup><small>AUR</small></sup>, mas estes ainda não são estáveis.

## Veja Também

[Site Oficial do Telegram](https://www.telegram.org/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Telegram_(Português)&oldid=411053](https://wiki.archlinux.org/index.php?title=Telegram_(Português)&oldid=411053)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Internet applications (Português)](/index.php/Category:Internet_applications_(Portugu%C3%AAs) "Category:Internet applications (Português)")