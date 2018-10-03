**Status de tradução:** Esse artigo é uma tradução de [General purpose mouse](/index.php/General_purpose_mouse "General purpose mouse"). Data da última tradução: 2018-10-01\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=General_purpose_mouse&diff=0&oldid=534195) na versão em inglês.

GPM, abreviação de *General Purpose Mouse*, é um daemon que fornece suporte a mouse para consoles virtuais do Linux.

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [gpm](https://www.archlinux.org/packages/?name=gpm). Para suporte a touchpad em um laptop, você também pode precisar instalar [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics).

## Configuração

O parâmetro `-m` precede a declaração do mouse a ser usado. O parâmetro `-t` precede o tipo de mouse. Para obter uma lista de tipos disponíveis para a opção `-t`, execute `gpm` com `-t help`.

```
# gpm -m /dev/input/mice -t help

```

O pacote [gpm](https://www.archlinux.org/packages/?name=gpm) precisa ser iniciado com alguns parâmetros. Estes parâmetros podem ser adicionados no arquivo `/etc/conf.d/gpm`, ou usados ao executar o *gpm* diretamente. A partir de 2016, o arquivo `gpm.service` para [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") inclui os parâmetros para um mouse USB. Obviamente, deve ser editado se houver outro tipo de mouse e o arquivo for usado.

*   Para mouses PS/2, substitua a linha existente com:

```
GPM_ARGS="-m /dev/psaux -t ps2"

```

*   Sendo que mouses USB devem usar:

```
GPM_ARGS="-m /dev/input/mice -t imps2"

```

*   E trackpoints IBM precisam:

```
GPM_ARGS="-m /dev/input/mice -t ps2"

```

**Nota:** Se o mouse tiver apenas 2 botões, passe `-2` para `GPM_ARGS` e o segundo botão executará a função de colar.

Uma vez encontrada uma configuração adequada, [inicie](/index.php/Inicie "Inicie") e [habilite](/index.php/Habilite "Habilite") o `gpm.service`.

Para mais informações, veja [gpm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gpm.8).

## Veja também

*   [Gentoo:GPM](https://wiki.gentoo.org/wiki/GPM "gentoo:GPM")