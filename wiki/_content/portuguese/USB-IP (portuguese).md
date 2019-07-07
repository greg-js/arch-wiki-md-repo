Do [site do USB/IP](http://usbip.sourceforge.net/):

	*O projeto USB/IP visa desenvolver um sistema geral de compartilhamento de dispositivos USB através da rede IP. Para compartilhar dispositivos USB entre computadores com todas as suas funcionalidades, o USB/IP encapsula "mensagens de E/S USB" em cargas TCP/IP e as transmite entre computadores.*

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Página man](#Página_man)
*   [3 Porta e firewall](#Porta_e_firewall)
*   [4 Uso](#Uso)
    *   [4.1 Listando e ativando módulos de kernel](#Listando_e_ativando_módulos_de_kernel)
    *   [4.2 Listando e compartilhando dispositivos](#Listando_e_compartilhando_dispositivos)
    *   [4.3 Computador cliente](#Computador_cliente)
*   [5 Veja também](#Veja_também)

## Instalação

[Instale](/index.php/Instale "Instale") [usbip](https://www.archlinux.org/packages/?name=usbip).

## Página man

Veja [usbip(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/usbip.8).

## Porta e firewall

USBip usa a porta 3240.

Caso haja um firewall, deve-se gerar permissões para esta porta no firewall. Por exemplo, no [ufw](/index.php/Ufw "Ufw") deve-se executar:

```
# ufw allow 3240

```

Para instruções específicas e detalhadas de seu firewall, acesse [Category:Firewalls](/index.php/Category:Firewalls "Category:Firewalls").

## Uso

### Listando e ativando módulos de kernel

USB/IP utiliza os módulos de kernel `vhci_hcd` e `usbip`.

Para listar os módulos, pode-se usar `lsmod` com `grep` da seguinte forma:

```
$ lsmod | grep vhci_hcd

```

Tendo encontrado ambos, basta ativá-los:

```
# modprobe vhci-hcd usbip_host usbip_core usbcore usb_common

```

Para informações detalhadas, leia [Kernel module](/index.php/Kernel_module "Kernel module").

### Listando e compartilhando dispositivos

Liste os dispositivos que têm permissão para compartilhar/exportar:

```
$ usbip list -l

```

Antes de compartilhar o dispositivo desejado, você deve que ativar o serviço USBip, em segundo plano:

```
# usbipd -D

```

Para compartilhar um dispositivo, basta usar a opção `-b` com o resultado da listagem de dispositivo filtrado com apenas o conteúdo que está após *busid* e antes dos parênteses:

```
# usbip bind -b *id_barramento*

```

Então, por exemplo, se usando o comando *list* você achou o dispositivo `busid 1-1 (13d3:5188)`, desconsidere "(13d3:5188)" e "busid", e use apenas "1-1", executando:

```
# usbip bind -b 1-1

```

### Computador cliente

Liste dispositivos USB exportáveis no servidor usando:

```
$ usbip list --remote=*ip_servidor*

```

Tendo encontrado o dispositivo USB remoto na rede, conecte-o usando o IP do servidor e a identificação do barramento com:

```
# usbip attach --remote=*ip_servidor* --busid=*id_barramento*

```

Então, por exemplo, se o endereço IP do servidor é "192.168.15.15" e a identificação do barramento é "1-1", execute:

```
# usbip attach --remote=192.168.15.15 --busid=1-1

```

## Veja também

*   [Site oficial do Projeto USB/IP](http://usbip.sourceforge.net/)
*   ["README for usbip-utils" do kernel Linux](https://www.kernel.org/doc/readme/tools-usb-usbip-README)
*   "How To Set Up A USB-Over-IP Server And Client With Ubuntu 10.04" ([página 1](https://www.howtoforge.com/how-to-set-up-a-usb-over-ip-server-and-client-with-ubuntu-10.04) e [página 2](https://www.howtoforge.com/how-to-set-up-a-usb-over-ip-server-and-client-with-ubuntu-10.04-p2))