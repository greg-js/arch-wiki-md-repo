**Status de tradução:** Esse artigo é uma tradução de [USB/IP](/index.php/USB/IP "USB/IP"). Data da última tradução: 2019-10-13\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=USB/IP&diff=0&oldid=585801) na versão em inglês.

Do [site do USB/IP](http://usbip.sourceforge.net/):

	*O projeto USB/IP visa desenvolver um sistema geral de compartilhamento de dispositivos USB através da rede IP. Para compartilhar dispositivos USB entre computadores com todas as suas funcionalidades, o USB/IP encapsula "mensagens de E/S USB" em cargas TCP/IP e as transmite entre computadores.*

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Uso](#Uso)
    *   [2.1 Configuração do servidor](#Configuração_do_servidor)
        *   [2.1.1 Vinculando com serviços de systemd](#Vinculando_com_serviços_de_systemd)
    *   [2.2 Configuração do cliente](#Configuração_do_cliente)
    *   [2.3 Desconectando dispositivos](#Desconectando_dispositivos)
*   [3 Página man](#Página_man)
*   [4 Veja também](#Veja_também)

## Instalação

[Instale](/index.php/Instale "Instale") [usbip](https://www.archlinux.org/packages/?name=usbip).

## Uso

### Configuração do servidor

O servidor deve ter um dispositivo USB conectado fisicamente a ele e o [módulo de kernel](/index.php/Kernel_module_(Portugu%C3%AAs) "Kernel module (Português)") de USP/IP `usbip_host` carregado. Então, [inicie](/index.php/Inicie "Inicie") e [habilite](/index.php/Habilite "Habilite") o serviço de systemd USB/IP `usbipd.service`.

Liste os dispositivos conectados:

```
$ usbip list -l

```

Vincule o dispositivo necessário. Por exemplo, para compartilhar o dispositivo tendo *busid* 1-1.5:

```
# usbip bind -b 1-1.5

```

Para desvincular o dispositivo:

```
$ usbip unbind -b 1-1.5

```

Após vincular, o dispositivo pode ser acessado do cliente.

#### Vinculando com serviços de systemd

Para fazer vínculo persistente seguindo o arquivo unit modelo de systemd pode ser usado:

 `/etc/systemd/system/usbip-bind@.service` 
```
[Unit]
 Description=USB-IP Binding on bus id %I
 After=network-online.target usbipd.service
 Wants=network-online.target
 Requires=usbipd.service
 #DefaultInstance=1-1.5

 [Service]
 Type=simple
 ExecStart=/usr/bin/usbip bind -b %i
 RemainAfterExit=yes
 ExecStop=/usr/bin/usbip unbind -b %i 
 Restart=on-failure

 [Install]
 WantedBy=multi-user.target
```

Então, por exemplo, para compartilhar o dispositivo tendo *busid* 1-1, deve-se [iniciar](/index.php/Inicia "Inicia") ou [habilitar](/index.php/Habilita "Habilita") `usbip-bind@1-1.service`.

### Configuração do cliente

Certifique-se que o [módulo de kernel](/index.php/Kernel_module_(Portugu%C3%AAs) "Kernel module (Português)") `vhci-hcd` está carregado.

Então, liste os dispositivos disponíveis no servidor:

```
$ usbip list -r *endereço_IP_do_servidor*

```

Anexe o dispositivo necessário. Por exemplo, para anexar o dispositivo tendo o *busid* 1-1.5:

```
$ usbip attach -r *endereço_IP_do_servidor* -b 1-1.5

```

### Desconectando dispositivos

Um dispositivo pode ser desconectado apenas após desanexá-lo no cliente.

Liste os dispositivos anexados:

```
$ usbip port

```

Desanexe o dispositivo:

```
$ usbip detach -p *número_da_porta*

```

Desvincule o dispositivo no servidor:

```
$ usbip unbind -b *busid*

```

**Nota:** O USB/IP, por padrão, precisa que a porta 3240 esteja aberta. Se um firewall estiver em execução, certifique-se que essa porta esteja aberta. Para instruções detalhadas sobre configuração do firewall, acesse [Category:Firewalls](/index.php/Category:Firewalls "Category:Firewalls")

## Página man

Veja [usbip(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/usbip.8).

## Veja também

*   [Site oficial do Projeto USB/IP](http://usbip.sourceforge.net/)
*   ["README for usbip-utils" do kernel Linux](https://www.kernel.org/doc/readme/tools-usb-usbip-README)
*   "How To Set Up A USB-Over-IP Server And Client With Ubuntu 10.04" ([página 1](https://www.howtoforge.com/how-to-set-up-a-usb-over-ip-server-and-client-with-ubuntu-10.04) e [página 2](https://www.howtoforge.com/how-to-set-up-a-usb-over-ip-server-and-client-with-ubuntu-10.04-p2))