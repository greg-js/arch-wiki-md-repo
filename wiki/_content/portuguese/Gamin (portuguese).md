[Gamin](http://www.gnome.org/~veillard/gamin/) é um sistema de monitoramento de arquivos e diretórios, sendo um subconjunto do sistema FAM (*File Alteration Monitor*). É um serviço provido por uma biblioteca que permite a detecção de modificações em arquivos ou diretórios.

Gamin re-implementa a especificação do [FAM](/index.php/FAM "FAM") com o [w:inotify](https://en.wikipedia.org/wiki/inotify "w:inotify"). É mais recente e mantido mais ativamente que o FAM, mantendo compatibilidade com o mesmo e pode substituí-lo em praticamente todos os casos. É um projeto do [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)"), mas ele não tem nenhuma dependência do GNOME.

## Instalação

Instale o pacote [gamin](https://www.archlinux.org/packages/?name=gamin).

Se FAM estiver instalado, primeiro [desabilite](/index.php/Disable "Disable") `fam.service` e então instale o [gamin](https://www.archlinux.org/packages/?name=gamin); você será solicitado a remover o pacote [fam](https://aur.archlinux.org/packages/fam/) durante a instalação.

## Veja também

*   [FAM, Gamin and inotify (em inglês)](http://www.noah.org/wiki/FAM,_Gamin,_inotify)