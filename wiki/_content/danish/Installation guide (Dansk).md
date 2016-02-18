Dette dokument vil guide dig gennem installationen af [Arch Linux](/index.php/Arch_Linux "Arch Linux") ved hjælp af [Arch Install Scripts](https://projects.archlinux.org/arch-install-scripts.git/). Før du begynder installationen anbefales det at skimme de [ofte stillede spørgsmål](/index.php/FAQ_(Dansk) "FAQ (Dansk)"). Se [begynderguiden](/index.php?title=Beginner%27s_Guide_(Dansk)&action=edit&redlink=1 "Beginner's Guide (Dansk) (page does not exist)") for en højt detaljeret, forklarende installationsguide.

[Arch wiki](/index.php/Main_Page_(Dansk) "Main Page (Dansk)"), som vedligeholdes af brugerne, er en glimrende ressource og bør konsulteres først hvis problemer opstår. [IRC](https://en.wikipedia.org/wiki/IRC "wikipedia:IRC") kanalen ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)), og [fora](https://bbs.archlinux.org/) er også tilgængelige hvis svaret ikke findes andre steder. Forsøg også at læse `man` siderne til kommandoer du ikke kender til; dette kan ofte findes ved at udføre `man *command*`.

## Installation

### Tastaturudlægning

Der findes allerede fungerende tastaturtyper og -udlægninger til mange lande og sprog, og en kommando som `loadkeys dk` gør sikkert hvad du ønsker. Flere udlægninger kan findes i `/usr/share/kbd/keymaps/` (du kan undlade stien og filendelsen når `loadkeys` benyttes.)

### Diskpartitionering

Se [partitionering](/index.php?title=Partitioning_(Dansk)&action=edit&redlink=1 "Partitioning (Dansk) (page does not exist)") for detaljer.

Hvis du ønsker at skabe nogle virtuelle blokenheder som [LVM](/index.php/LVM "LVM"), [LUKS](/index.php/Dm-crypt_with_LUKS "Dm-crypt with LUKS") eller [RAID](/index.php/RAID "RAID"), er det nu det skal gøres.