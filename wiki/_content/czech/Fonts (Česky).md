Přidání fontů v moderním Linux je snažší než dříve. Zde je několik tipů pro snažší pochopení průměrnými uživateli. První věc je, kam fonty vložit. Obvykle by měli být vloženy do:

*   /usr/share/fonts
*   /usr/X11R6/lib/X11/fonts

Tímto se stanou dostupné pro všechny uživatele, ale vyžaduje to root práva. Jejich zkopírování do adresáře:

*   ~/.fonts

je také dobrý nápad.

Některé fonty jsou předpřipraveny pro použití v Arch Linuxu, vyhledávat je můžete pomocí:

 `pacman -Ss fonts` 

Mezi dostupnými balíčky jsou:

```
extra/artwiz-fonts 1.3-1
    This is set of (improved) artwiz fonts.
extra/ttf-ms-fonts 1.3-6
    Un-extracted TTF Fonts from Microsoft

```

Pro jejich nainstalování:

 `pacman -S artwiz-fonts ttf-ms-fonts` 

Fonty se nainstalují do adresáře `/usr/X11R6/lib/X11/fonts`.

Jinou možností je použít Instalátor fontů KDE v Ovládacím centru. Vypadá to, že to funguje bezvadně pokud používáte KDE.

Také můžete ručně nakopírovat fonty do jednoho ze tří adresářů výše, pak ale nezapoměnte jako root spustit: `fc-cache -vf` 

Víceméně si jich můžete užívat v prostředích jako gnome, xfce4 nebo kde. Ale některé GTK1 nebo staré aplikace nepodporují fontcofig. *(Opravdu? pak by to měl někdo ověřit a případně opravit)* Měli byste spustit následující příkazy v adresáři s fonty (v konzoli ovšem):

```
  mkfontscale
  mkfontdir
  ln -s /usr/share/fonts/encodings/encodings.dir yourfontdirectory/encodings.dir 

```

Když používáte kde

```
   ln -s /usr/share/fonts/encodings/encodings.dir ~/.fonts/

```

pak je obvykle třeba restartovat X.

Jestliže chcete fonty sdílet nebo se vyvarovat ručních oprací popsaných výše, můžete vytvořit Arch balíček. Uložte fonty, které chcete instalovat, jako tar.bz2 a použijte pozměnené následující PKGBUILD a .install pro jejich instalaci pomocí ABS:

```
# PKGBUILD
  pkgname=fonts-extra
  pkgver=1.0
  pkgrel=1
  depends=('xfree86')
  pkgdesc=\"Fonts extra\"
  source=(fonts-extra.tar.bz2)
  install=fonts-extra.install
  build()        {
    mkdir -p $startdir/pkg/usr/X11R6/lib/X11/fonts/local
    mv $startdir/src/*.ttf $startdir/pkg/usr/X11R6/lib/X11/fonts/local
  }

```

```
# fonts-extra.install:
  # arg 1:  the new package version
  post_install() {
    echo -n \"updating font cache... \"
    /usr/bin/fc-cache
    cd /usr/X11R6/lib/X11/fonts/local
    /usr/X11R6/bin/mkfontscale
    /usr/X11R6/bin/mkfontdir
    ln -s /usr/X11R6/lib/X11/fonts/encodings/encodings.dir /usr/X11R6/lib/X11/fonts/local/encodings.dir
    echo \"done.\"
  }

  # arg 1:  the new package version
  # arg 2:  the old package version
  post_upgrade() {
    post_install $1
  }

  # arg 1:  the old package version
  pre_remove() {
    /bin/true
  }

  op=$1
  shift

  $op $*

```