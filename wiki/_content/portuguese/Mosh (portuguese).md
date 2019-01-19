**Status de tradução:** Esse artigo é uma tradução de [Mosh](/index.php/Mosh "Mosh"). Data da última tradução: 2019-01-18\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Mosh&diff=0&oldid=563804) na versão em inglês.

Do [site oficial](http://mosh.mit.edu/):

	Aplicativo de terminal remoto que permite deslocamento, possui suporte a conectividade intermitente e fornece edição inteligente de eco local e de linha de pressionamentos de tecla do usuário. Mosh é um substituto para o [SSH](/index.php/SSH_(Portugu%C3%AAs) "SSH (Português)"). É mais robusto e responsivo, especialmente em conexões lentas, como Wi-Fi, celular e longa distância.

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [mosh](https://www.archlinux.org/packages/?name=mosh) ou o [mosh-git](https://aur.archlinux.org/packages/mosh-git/) para sua última revisão.

## Uso

Mosh tem uma opção de linha de comando não documentada `--predict=experimental` que produz um eco mais agressivo dos pressionamentos de teclas locais. Os usuários interessados na confirmação visual de baixa latência da entrada do teclado podem preferir este modo de previsão.

**Nota:** Mosh por design não permite acessar o histórico da sessão, considere instalar um multiplexador de terminal como o [tmux](/index.php/Tmux "Tmux") ou o [GNU Screen](/index.php/GNU_Screen "GNU Screen").