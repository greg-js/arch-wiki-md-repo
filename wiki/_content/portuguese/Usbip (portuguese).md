## Contents

*   [1 USB over IP tunnel - USBIP](#USB_over_IP_tunnel_-_USBIP)
    *   [1.1 Para o instalar, basta usar o comando:](#Para_o_instalar.2C_basta_usar_o_comando:)
*   [2 Para evitar problemas, é bom ativar os módulos:](#Para_evitar_problemas.2C_.C3.A9_bom_ativar_os_m.C3.B3dulos:)
    *   [2.1 -> Achou os módulos? Agora ative, exemplo:](#-.3E_Achou_os_m.C3.B3dulos.3F_Agora_ative.2C_exemplo:)
    *   [2.2 Agora você deve listar os dispositivos, permitidos para compartilhar/exportar:](#Agora_voc.C3.AA_deve_listar_os_dispositivos.2C_permitidos_para_compartilhar.2Fexportar:)
    *   [2.3 Para compartilhar o dispositivo, você tem que ativar o serviço USBip, em segundo plano:](#Para_compartilhar_o_dispositivo.2C_voc.C3.AA_tem_que_ativar_o_servi.C3.A7o_USBip.2C_em_segundo_plano:)
    *   [2.4 Compartilhando um dispositivo, exemplo:](#Compartilhando_um_dispositivo.2C_exemplo:)
    *   [2.5 No computador cliente, execute:](#No_computador_cliente.2C_execute:)
    *   [2.6 Ainda no computador cliente, após ter visto o dispositivo USB em rede, o conecte:](#Ainda_no_computador_cliente.2C_ap.C3.B3s_ter_visto_o_dispositivo_USB_em_rede.2C_o_conecte:)
*   [3 Fontes:](#Fontes:)

## USB over IP tunnel - USBIP

O projeto USB / IP visa desenvolver um sistema geral de compartilhamento de dispositivos USB através da rede IP. Para compartilhar dispositivos USB entre computadores com todas as suas funcionalidades, o USB / IP encapsula "mensagens de E/S USB" em cargas TCP / IP e as transmite entre computadores.

```
                                 Para fins de esclarecimento e uso, será explicado como utilizar o USBIP.

```

##### Para o instalar, basta usar o comando:

```
 sudo pacman -S usbip

```

-> USBip usa a porta 3240

-> Você deve gerar permissões no seu firewall, exemplo:

```
 sudo ufw allow 3240

```

## Para evitar problemas, é bom ativar os módulos:

-> listar se há módulos vhci

```
 lsmod | grep vhci_hcd

```

-> listar se há módulos usbip

```
 lsmod | grep usbip

```

##### -> Achou os módulos? Agora ative, exemplo:

```
 sudo modprobe vhci-hcd usbip_host usbip_core usbcore usb_common

```

##### Agora você deve listar os dispositivos, permitidos para compartilhar/exportar:

```
 usbip list -l

```

##### Para compartilhar o dispositivo, você tem que ativar o serviço USBip, em segundo plano:

```
 sudo usbipd -D

```

##### Compartilhando um dispositivo, exemplo:

-> Se você achou o dispositivo

-> busid 1-1 (13d3:5188)

-> Desconsidera o que está contido nos parenteses: "(13d3:5188)"

-> E utilize só o que está após o "busid", assim: "1-1"

```
 sudo usbip bind -b 1-1

```

* * *

##### No computador cliente, execute:

-> usbip list --remote=ip_server. -> Veja o ip, do server com: ifconfig, exemplo:

```
 usbip list --remote=192.168.15.15

```

##### Ainda no computador cliente, após ter visto o dispositivo USB em rede, o conecte:

-> Lembrando que, "server" é o ip e "1-1"(busid) poderá variar.

-> Não esqueça de substituir: "server", pelo ip.

```
 sudo usbip attach --remote=server --busid=1-1

```

## Fontes:

Estas fontes serviram de base somente, os comandos foram adaptados, pois o USBip atualizou, e os artigos são antigos de 2009/2010:

1.  <ref>[https://www.mankier.com/8/usbip](https://www.mankier.com/8/usbip)</ref>

1.  <ref>[https://www.kernel.org/doc/readme/tools-usb-usbip-README](https://www.kernel.org/doc/readme/tools-usb-usbip-README)</ref>

1.  <ref>[https://www.howtoforge.com/how-to-set-up-a-usb-over-ip-server-and-client-with-ubuntu-10.04](https://www.howtoforge.com/how-to-set-up-a-usb-over-ip-server-and-client-with-ubuntu-10.04)</ref>

1.  <ref>[https://www.howtoforge.com/how-to-set-up-a-usb-over-ip-server-and-client-with-ubuntu-10.04-p2](https://www.howtoforge.com/how-to-set-up-a-usb-over-ip-server-and-client-with-ubuntu-10.04-p2)</ref>

1.  <ref>[http://usbip.sourceforge.net/](http://usbip.sourceforge.net/)</ref>