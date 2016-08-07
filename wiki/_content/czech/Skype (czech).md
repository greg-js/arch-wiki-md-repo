### Důležitá poznámka

Nová beta verze Skypu má nativní podporu Alsy. Pokud máte tuto verzi, není nuté provádět tyto kroky!

### Instalace Skype

Balíček Skype se nachází v repozitáří community. Pokud tento repozitář nemáte aktivovaný, změňte následující řádky v souboru /etc/pacman.conf:

```
#[community]
# Add your preferred servers here, they will be used first
#Include = /etc/pacman.d/community

```

na

```
[community]
# Add your preferred servers here, they will be used first
Include = /etc/pacman.d/community

```

Nyní nainstaluje Skype přes pacman:

```
# pacman -S skype

```