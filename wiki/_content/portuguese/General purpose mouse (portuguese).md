**Status de tradução:** Esse artigo é uma tradução de [General purpose mouse](/index.php/General_purpose_mouse "General purpose mouse"). Data da última tradução: 2019-08-28\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=General_purpose_mouse&diff=0&oldid=580392) na versão em inglês.

GPM, abreviação de *General Purpose Mouse*, é um daemon que fornece suporte a mouse para consoles virtuais do Linux.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Configuração](#Configuração)
    *   [2.1 QEMU ou VirtualBox](#QEMU_ou_VirtualBox)
*   [3 Veja também](#Veja_também)

## Instalação

**Atenção:** [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) não é mais ativamente mantido. Se possível, use [libinput](/index.php/Libinput "Libinput").

[Instale](/index.php/Instale "Instale") o pacote [gpm](https://www.archlinux.org/packages/?name=gpm). Para suporte a touchpad em um laptop, você também pode precisar instalar [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics).

## Configuração

O parâmetro `-m` precede a declaração do mouse a ser usado. O parâmetro `-t` precede o tipo de mouse. Para obter uma lista de tipos disponíveis para a opção `-t`, execute `gpm` com `-t help`.

```
# gpm -m /dev/input/mice -t help

```

O pacote [gpm](https://www.archlinux.org/packages/?name=gpm) precisa ser iniciado com alguns parâmetros. Estes parâmetros podem ser registrados para [criar](/index.php/Criar "Criar") o arquivo `/etc/conf.d/gpm`, ou usados ao executar o *gpm* diretamente. A partir de 2016, o arquivo `gpm.service` para [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") inclui os parâmetros para um mouse USB.

 `/usr/lib/systemd/system/gpm.service`  `ExecStart=/usr/bin/gpm -m /dev/input/mice -t imps2` 

Obviamente, deve ser editado, preferivelmente em uma [forma amigável para o systemd](/index.php/Systemd_(Portugu%C3%AAs)#Editando_units_fornecidas "Systemd (Português)"), se houver outro tipo de mouse e o serviço for usado.

*   Para mouses PS/2, os parâmetros:

```
 -m /dev/psaux -t ps2

```

*   E trackpoints IBM precisam:

```
 -m /dev/input/mice -t ps2

```

**Nota:** Se o mouse tiver apenas 2 botões, passe `-2` para `GPM_ARGS` e o segundo botão executará a função de colar.

Uma vez encontrada uma configuração adequada, [inicie](/index.php/Inicie "Inicie") e [habilite](/index.php/Habilite "Habilite") o `gpm.service`.

Para mais informações, veja [gpm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gpm.8).

### QEMU ou VirtualBox

O mouse padrão emulado pelo QEMU e pelo VirtualBox tem sérios problemas tanto no *gpm* quanto no x com posicionamento e clique. A posição torna-se não sincronizada com o hospedeiro, portanto, há áreas que não podem ser passadas sem sair e entrar novamente na janela repetidamente. Clica em registrar em um local diferente do que o cursor estava mostrando.

Tanto o QEMU como o VirtualBox resolvem este problema fornecendo emulação para um tablet USB, o que dá um posicionamento absoluto. ([libvirt](https://www.archlinux.org/packages/?name=libvirt) usa isso automaticamente.)

No entanto, o *gpm* só sabe usar o mouse emulado no modo de posicionamento relativo, portanto, esses problemas permanecem. A tentativa de usar outros tipos por meio de `-t` não funciona corretamente.

[gpm-vm](https://aur.archlinux.org/packages/gpm-vm/) inclui uma [pull request](https://github.com/telmich/gpm/pull/23) de vários anos atrás para adicionar suporte ao tablet USB para o VirtualBox (que também funciona no QEMU) e modifica o `gpm.service` arquivo para usá-lo por padrão.

Você pode precisar alterar qual evento é usado. (Dando *gpm* o `-m/dev/input/mice` original não irá funcionar.) Por padrão:

 `/etc/gpm-vm.conf`  `event="/dev/input/event2"` 

Você pode determinar o evento a ser usado instalando [evtest](https://www.archlinux.org/packages/?name=evtest) e executando:

 `# evtest` 
```
...
/dev/input/event2:      QEMU QEMU USB Tablet
...

```

Se você precisar dar opções adicionais do *gpm*, você pode definir `additional_args` em `/etc/gpm-vm.conf`.

Uma vez encontrada uma configuração adequada, [inicie](/index.php/Inicie "Inicie") e [habilite](/index.php/Habilite "Habilite") o `gpm.service`.

## Veja também

*   [Gentoo:GPM](https://wiki.gentoo.org/wiki/GPM "gentoo:GPM")