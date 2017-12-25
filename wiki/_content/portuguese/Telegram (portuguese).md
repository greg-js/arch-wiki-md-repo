Parte copiada do [Wikipedia](https://pt.wikipedia.org/wiki/Telegram_(aplicativo)): **Telegram** é uma aplicação multiplataforma de mensageiro instantâneo, com seu cliente em código aberto e servidores em software proprietário, tendo seu foco na segurança e privacidade. Além de mensagens de texto criptografadas e opcionalmente autodestrutivas, os usuários podem enviar fotos, vídeos e documentos (todos os tipos de arquivos suportados). Está oficialmente disponível para diversos dispositivos, como Android (incluindo tablets), iOS (incluindo iPad), Windows Phone (ainda em versão beta), Windows, OS X, Linux e um cliente web; outras plataformas e clientes alternativos podem existir a partir de desenvolvedores independentes que usam o API do Telegram.

## Instalação

Atualmente o repositório oficial ainda não possui pacotes relacionados，mas o AUR tem [telegram-desktop](https://www.archlinux.org/packages/?name=telegram-desktop)、[telegram-dev](https://aur.archlinux.org/packages/telegram-dev/)、[telegram-desktop-cn](https://aur.archlinux.org/packages/telegram-desktop-cn/) e outros. Para China, Japão e Coreia, você usar outros métodos de digitação, logo, é preciso instalar [telegram-desktop-cn](https://aur.archlinux.org/packages/telegram-desktop-cn/)。

A partir da versão 0.8.50 do Telegram, foram consertados os problemas com métodos de entrada asiático, recomenda-se usar versoes posteriores. Pode ser necessário definir a variável de ambiente QT_IM_MODULE. Para mais detalhes, consulte [Fcitx#GTK+ and Qt modules](/index.php/Fcitx#GTK.2B_and_Qt_modules "Fcitx")

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

No AUR também exitem pacotes para usar [pidgin](/index.php/Pidgin "Pidgin"), que inclui [telegram-purple](https://aur.archlinux.org/packages/telegram-purple/) e [telegram-purple-git](https://aur.archlinux.org/packages/telegram-purple-git/), mas estes ainda não são estáveis.

## Veja Também

[Site Oficial do Telegram](https://www.telegram.org/)