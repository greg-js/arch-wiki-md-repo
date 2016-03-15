[Gamin](http://www.gnome.org/~veillard/gamin/) é um sistema de monitoramento de arquivos e diretórios, sendo um subconjunto do sistema [FAM](/index.php/FAM "FAM") (File Alteration Monitor). É um serviço provido por uma biblioteca que permite a detecção de modificações em arquivos ou diretórios.

Gamin re-implementa a especificação do [FAM](/index.php/FAM "FAM") com o [inotify](/index.php?title=Inotify&action=edit&redlink=1 "Inotify (page does not exist)"). É mais recente e mantido mais ativamente que o [FAM](/index.php/FAM "FAM"), mantendo compatibilidade com o mesmo e pode substituí-lo em praticamente todos os casos. É um projeto do [GNOME](/index.php/GNOME "GNOME"), mas ele não tem nenhuma dependência dele.

## Instalação

Se estiver instalado, remova o pacote [fam](https://aur.archlinux.org/packages/fam/), ignorando as dependências:

```
# pacman -Rd fam

```

Instalando o [gamin](https://www.archlinux.org/packages/?name=gamin).

Se existir a linha `fam` no `DAEMON` em `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")`, você deverá removê-lo. Note que você **não** precisa colocar o `gamin` na linha `DAEMON`.

## Links externos

*   [Gamin](https://pt.wikipedia.org/wiki/Gamin)
*   [FAM, Gamin and inotify (em inglês)](http://www.noah.org/wiki/FAM,_Gamin,_inotify)