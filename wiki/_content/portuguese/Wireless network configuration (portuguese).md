Artigos relacionados

*   [Configuração de rede](/index.php/Configura%C3%A7%C3%A3o_de_rede "Configuração de rede")
*   [Ponto de acesso por software](/index.php/Software_access_point "Software access point")
*   [Rede ad-hoc](/index.php/Ad-hoc_networking "Ad-hoc networking")
*   [Compartilhamento de internet](/index.php/Internet_sharing "Internet sharing")
*   [Vinculação de rede sem fio](/index.php/Wireless_bonding "Wireless bonding")
*   [Depuração de rede](/index.php/Network_Debugging "Network Debugging")
*   [Bluetooth](/index.php/Bluetooth "Bluetooth")

A configuração de rede sem fio *(wireless)* é um processo de duas partes. A primeira parte é identificar e garantir que o driver correto para o seu dispositivo sem fio está instalado (eles estão disponíveis na mídia de instalação, mas geralmente precisam ser instalados explicitamente) e para configurar a interface. A segunda é escolher um método de gerenciamento de conexões sem fio. Este artigo abrange as duas partes e fornece links adicionais para ferramentas de gerenciamento sem fio.

## Contents

*   [1 Driver de dispositivo](#Driver_de_dispositivo)
    *   [1.1 Verificar o status de driver](#Verificar_o_status_de_driver)
    *   [1.2 Instalar driver/firmware](#Instalar_driver.2Ffirmware)
*   [2 Gerenciamento de sem fio](#Gerenciamento_de_sem_fio)
    *   [2.1 Configuração manual](#Configura.C3.A7.C3.A3o_manual)
        *   [2.1.1 Obter o nome da interface](#Obter_o_nome_da_interface)
        *   [2.1.2 Obter o status da interface](#Obter_o_status_da_interface)
        *   [2.1.3 Ativar a interface](#Ativar_a_interface)
        *   [2.1.4 Descobrir pontos de acesso](#Descobrir_pontos_de_acesso)
        *   [2.1.5 Definir o modo de operação](#Definir_o_modo_de_opera.C3.A7.C3.A3o)
        *   [2.1.6 Conectar a um ponto de acesso](#Conectar_a_um_ponto_de_acesso)
        *   [2.1.7 Obter um endereço IP](#Obter_um_endere.C3.A7o_IP)
            *   [2.1.7.1 Exemplo](#Exemplo)
    *   [2.2 Configuração automática](#Configura.C3.A7.C3.A3o_autom.C3.A1tica)
*   [3 WPA2 Empresarial](#WPA2_Empresarial)
    *   [3.1 eduroam](#eduroam)
    *   [3.2 Configuração manual/automática](#Configura.C3.A7.C3.A3o_manual.2Fautom.C3.A1tica)
        *   [3.2.1 wpa_supplicant](#wpa_supplicant)
        *   [3.2.2 NetworkManager](#NetworkManager)
        *   [3.2.3 connman](#connman)
        *   [3.2.4 netctl](#netctl)
    *   [3.3 Solução de problemas](#Solu.C3.A7.C3.A3o_de_problemas)
        *   [3.3.1 MS-CHAPv2](#MS-CHAPv2)
*   [4 Dicas e truques](#Dicas_e_truques)
    *   [4.1 Respeitar o domínio regulatório](#Respeitar_o_dom.C3.ADnio_regulat.C3.B3rio)
    *   [4.2 Comparação entre iw e wireless_tools](#Compara.C3.A7.C3.A3o_entre_iw_e_wireless_tools)
*   [5 Solução de problemas](#Solu.C3.A7.C3.A3o_de_problemas_2)
    *   [5.1 Acesso temporário à internet](#Acesso_tempor.C3.A1rio_.C3.A0_internet)
    *   [5.2 Problemas com rfkill](#Problemas_com_rfkill)
    *   [5.3 Observando os logs](#Observando_os_logs)
    *   [5.4 Economia de energia](#Economia_de_energia)
    *   [5.5 Falha ao obter endereço IP](#Falha_ao_obter_endere.C3.A7o_IP)
    *   [5.6 Endereço IP válido, mas não consegue resolver host](#Endere.C3.A7o_IP_v.C3.A1lido.2C_mas_n.C3.A3o_consegue_resolver_host)
    *   [5.7 Definindo limites de RTS e de fragmentação](#Definindo_limites_de_RTS_e_de_fragmenta.C3.A7.C3.A3o)
    *   [5.8 Desconexões aleatórias](#Desconex.C3.B5es_aleat.C3.B3rias)
        *   [5.8.1 Causa nº.1](#Causa_n.C2.BA.1)
        *   [5.8.2 Causa nº.2](#Causa_n.C2.BA.2)
        *   [5.8.3 Causa nº.3](#Causa_n.C2.BA.3)
        *   [5.8.4 Causa nº.4](#Causa_n.C2.BA.4)
    *   [5.9 Redes Wi-Fi invisíveis por causa do domínio regulatório incorreto](#Redes_Wi-Fi_invis.C3.ADveis_por_causa_do_dom.C3.ADnio_regulat.C3.B3rio_incorreto)
*   [6 Solução de problemas de drivers e firmware](#Solu.C3.A7.C3.A3o_de_problemas_de_drivers_e_firmware)
    *   [6.1 Ralink/Mediatek](#Ralink.2FMediatek)
        *   [6.1.1 rt2x00](#rt2x00)
        *   [6.1.2 rt3090](#rt3090)
        *   [6.1.3 rt3290](#rt3290)
        *   [6.1.4 rt3573](#rt3573)
        *   [6.1.5 rt5572](#rt5572)
        *   [6.1.6 mt7612u](#mt7612u)
    *   [6.2 Realtek](#Realtek)
        *   [6.2.1 rtl8192cu](#rtl8192cu)
        *   [6.2.2 rtl8723ae/rtl8723be](#rtl8723ae.2Frtl8723be)
        *   [6.2.3 rtl88xxau](#rtl88xxau)
        *   [6.2.4 rtl8822bu](#rtl8822bu)
        *   [6.2.5 rtl8xxxu](#rtl8xxxu)
    *   [6.3 Atheros](#Atheros)
        *   [6.3.1 ath5k](#ath5k)
        *   [6.3.2 ath9k](#ath9k)
            *   [6.3.2.1 Economia de energia](#Economia_de_energia_2)
    *   [6.4 Intel](#Intel)
        *   [6.4.1 ipw2100 e ipw2200](#ipw2100_e_ipw2200)
        *   [6.4.2 iwlegacy](#iwlegacy)
        *   [6.4.3 iwlwifi](#iwlwifi)
            *   [6.4.3.1 Coexistência com Bluetooth](#Coexist.C3.AAncia_com_Bluetooth)
        *   [6.4.4 Desabilitar piscada de LED](#Desabilitar_piscada_de_LED)
    *   [6.5 Broadcom](#Broadcom)
    *   [6.6 Outros drivers/dispositivos](#Outros_drivers.2Fdispositivos)
        *   [6.6.1 Tenda w322u](#Tenda_w322u)
        *   [6.6.2 orinoco](#orinoco)
        *   [6.6.3 prism54](#prism54)
        *   [6.6.4 ACX100/111](#ACX100.2F111)
        *   [6.6.5 zd1211rw](#zd1211rw)
        *   [6.6.6 hostap_cs](#hostap_cs)
    *   [6.7 ndiswrapper](#ndiswrapper)
    *   [6.8 backports-patched](#backports-patched)
*   [7 Veja também](#Veja_tamb.C3.A9m)

## Driver de dispositivo

O kernel padrão do Arch Linux é *modular*, o que significa que muitos dos drivers para hardware de máquina residem no disco rígido e estão disponíveis como [módulos](/index.php/Kernel_modules "Kernel modules"). Na inicialização, o [udev](/index.php/Udev "Udev") faz um inventário do seu hardware e carrega os módulos (drivers) apropriados para o hardware correspondente, o que, por sua vez, permite a criação de uma *interface* de rede.

Alguns chipsets sem fio também exigem firmware, além de um driver correspondente. Muitas imagens de firmware são fornecidas pelo pacote [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) que é instalado por padrão, no entanto, as imagens de firmware proprietárias não são incluídas e devem ser instaladas separadamente. Isso é descrito em [#Instalar driver/firmware](#Instalar_driver.2Ffirmware).

**Nota:** Se o módulo apropriado não for carregado pelo udev na inicialização, basta [carregá-lo manualmente](/index.php/Kernel_modules#Manual_module_handling "Kernel modules"). Se o udev carrega mais de um driver para um dispositivo, o conflito resultante pode impedir a configuração seja bem-sucedida. Certifique-se de [colocar na lista negra](/index.php/Blacklist "Blacklist") o módulo indesejado.

**Dica:** Embora não seja estritamente necessário, é uma boa ideia instalar primeiro as ferramentas de espaço do usuário mencionadas em [#Configuração manual](#Configura.C3.A7.C3.A3o_manual), especialmente quando algum problema surgir.

### Verificar o status de driver

Para verificar se o driver da placa foi carregado, verifique a saída do comando `lspci -k` ou `lsusb -v`, dependendo se a placa está conectada por PCI(e) ou USB. Você deve ver que algum driver do kernel está em uso, por exemplo:

 `$ lspci -k` 
```
06:00.0 Network controller: Intel Corporation WiFi Link 5100
	Subsystem: Intel Corporation WiFi Link 5100 AGN
	Kernel driver in use: iwlwifi
	Kernel modules: iwlwifi

```

**Nota:** Se a placa for um dispositivo USB, a execução `dmesg | grep usbcore` deve retornar algo como `usbcore: registered new interface driver rtl8187` como saída.

Verifique também a saída do comando `ip link` para ver se uma interface sem fio ([geralmente](/index.php/Configura%C3%A7%C3%A3o_de_rede#Interface_de_rede "Configuração de rede") começa com a letra "w", por exemplo, `wlp2s1`) foi criada. Em seguida, ative a interface com `ip link set *interface* up`. Por exemplo, supondo que a interface seja `wlan0`:

```
# ip link set wlan0 up

```

Se você receber esta mensagem de erro: `SIOCSIFFLAGS: No such file or directory`, isso certamente significa que seu chipset sem fio requer um firmware para funcionar.

Verifique as mensagens de kernel para o firmware sendo carregado:

 `$ dmesg | grep firmware` 
```
[   7.148259] iwlwifi 0000:02:00.0: loaded firmware version 39.30.4.1 build 35138 op_mode iwldvm

```

Se não houver uma saída relevante, verifique as mensagens para a saída completa do módulo identificado anteriormente (`iwlwifi` neste exemplo) para identificar a mensagem relevante ou outros problemas:

 `$ dmesg | grep iwlwifi` 
```
[   12.342694] iwlwifi 0000:02:00.0: irq 44 for MSI/MSI-X
[   12.353466] iwlwifi 0000:02:00.0: loaded firmware version 39.31.5.1 build 35138 op_mode iwldvm
[   12.430317] iwlwifi 0000:02:00.0: CONFIG_IWLWIFI_DEBUG disabled
...
[   12.430341] iwlwifi 0000:02:00.0: Detected Intel(R) Corporation WiFi Link 5100 AGN, REV=0x6B

```

Se o módulo do kernel foi carregado com êxito e a interface estiver ativa, você pode pular a próxima seção.

### Instalar driver/firmware

Verifique as listas a seguir para descobrir se sua placa é compatível:

*   Veja a tabela de [drivers sem fio Linux existentes](https://wireless.wiki.kernel.org/en/users/drivers) e siga para a página específica do driver, que contém uma lista de dispositivos suportados. Há também uma [lista de IDs de dispositivos Wi-Fi no Linux](https://wikidevi.com/wiki/List_of_Wi-Fi_Device_IDs_in_Linux).
*   O [Wiki do Ubuntu](https://help.ubuntu.com/community/WifiDocs/WirelessCardsSupported) tem uma boa lista de placas sem fio e se elas são suportadas no kernel do Linux ou por um driver de espaço do usuário (inclui nome do driver)).
*   [Linux Wireless LAN Support](http://linux-wless.passys.nl/) e a [Hardware Compatibility List](http://www.linuxquestions.org/hcl/index.php?cat=10) (HCL) do The Linux Questions também têm um bom banco de dados de hardware compatível com kernel.

Observe que alguns fornecedores fornecem produtos que podem conter conjuntos de chips diferentes, mesmo se o identificador do produto for o mesmo. Apenas o usb-id (para dispositivos USB) ou pci-id (para dispositivos PCI) é autoritativo.

Se a sua placa sem fio estiver listada acima, siga a subseção desta página [#Solução de problemas de drivers e firmware](#Solu.C3.A7.C3.A3o_de_problemas_de_drivers_e_firmware), que contém informações sobre a instalação de drivers e firmware de algumas placas sem fio específicas. Em seguida, [verifique o status do driver](#Verificar_o_status_de_driver) novamente.

Se sua placa sem fio não estiver listada acima, provavelmente só há suporte no Windows (algumas Broadcom, 3com etc). Para essas, você pode tentar usar o [#ndiswrapper](#ndiswrapper).

## Gerenciamento de sem fio

A [#Configuração manual](#Configura.C3.A7.C3.A3o_manual) usa ferramentas de linha de comando para gerenciar manualmente sua interface de rede. A seção [#Configuração automática](#Configura.C3.A7.C3.A3o_autom.C3.A1tica) descreve vários programas que podem ser usados para gerenciar automaticamente sua interface sem fio, alguns dos quais incluem uma GUI e todos incluem suporte a perfis de rede (útil ao alternar frequentemente de redes sem fio, como laptops).

### Configuração manual

Assim como outras interfaces de rede, as sem fio são controladas com *ip* do pacote [iproute2](https://www.archlinux.org/packages/?name=iproute2).

Você precisará instalar um conjunto básico de ferramentas para gerenciar a conexão sem fio. [Instale](/index.php/Instale "Instale") um dos seguintes:

**Nota:** Para criptografia WPA/WPA2, *wpa_supplicant* é necessário.

*   **iw** — *iw* só oferece suporte ao padrão nl80211 (netlink), não havendo suporte ao padrão antigo WEXT (Wireless EXTentions). Se *iw* não vir sua placa, esse pode ser o motivo.

	[https://wireless.kernel.org/en/users/Documentation/iw](https://wireless.kernel.org/en/users/Documentation/iw) || [iw](https://www.archlinux.org/packages/?name=iw)

*   **wireless_tools** — *wireless_tools* está obsoleto, mas ainda é amplamente suportado. Use esse para módulos usando o padrão WEXT.

	[http://www.hpl.hp.com/personal/Jean_Tourrilhes/Linux/Tools.html](http://www.hpl.hp.com/personal/Jean_Tourrilhes/Linux/Tools.html) || [wireless_tools](https://www.archlinux.org/packages/?name=wireless_tools)

*   **[WPA supplicant](/index.php/WPA_supplicant "WPA supplicant")** — *wpa_supplicant* é um suplicante multiplataforma com suporte a WEP, WPA e WPA2 (IEEE 802.11i / RSN (Robust Secure Network)). Funciona com o WEXT e o nl80211.

	[http://hostap.epitest.fi/wpa_supplicant/](http://hostap.epitest.fi/wpa_supplicant/) || [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant)

**Dica:** Para uma comparação entre os comandos *iw* e *wireless_tools*, veja [#Comparação entre iw e wireless_tools](#Compara.C3.A7.C3.A3o_entre_iw_e_wireless_tools).

**Nota:**

*   Note que a maioria dos comandos devem ser executados com [permissões de root](/index.php/Usu%C3%A1rios_e_grupos "Usuários e grupos"). Se executados com permissões de usuário normal, alguns dos comandos (por exemplo, *iwlist*) sairão sem erro, mas também não produzirão a saída correta, o que pode ser confuso.
*   Dependendo do seu hardware e tipo de criptografia, algumas dessas etapas podem não ser necessárias. Algumas placas são conhecidas por exigir a ativação da interface e/ou a verificação do ponto de acesso antes de serem associadas a um ponto de acesso e receberem um endereço IP. Algum teste pode ser necessário. Por exemplo, os usuários WPA/WPA2 podem tentar ativar diretamente sua rede sem fio a partir do passo [#Conectar a um ponto de acesso](#Conectar_a_um_ponto_de_acesso).

Exemplos nesta seção presume que sua interface de dispositivo sem fio é `*interface*` e que você está se conectando a ponto de acesso wifi `*seu_essid*`. Substitua ambos conforme o caso.

#### Obter o nome da interface

**Dica:** Veja a [documentação oficial](http://wireless.kernel.org/en/users/Documentation/iw) da ferramenta *iw* para mais exemplos.

Para obter o nome de sua interface sem fio, faça:

```
$ iw dev

```

O nome da interface será exibida após a palavra "Interface". Por exemplo, ela normalmente é `wlan0`.

#### Obter o status da interface

Para verificar o status dos links, use o comando a seguir:

```
$ iw dev *interface* link

```

Você pode obter informações estatísticas, tal como a quantidade de bytes tx/rx, força de sinal etc., com o comando a seguir:

```
$ iw dev *interface* station dump

```

#### Ativar a interface

**Dica:** Geralmente, essa etapa não é necessária.

Algumas placas de rede exigem que a interface do kernel seja ativada antes que você possa usar *iw* ou *wireless_tools*:

```
# ip link set *interface* up

```

**Nota:** Se você obtiver erros como `RTNETLINK answers: Operation not possible due to RF-kill`, certifique-se que o botão de hardware esteja ligado. Veja [#Problemas com rfkill](#Problemas_com_rfkill) para detalhes.

Para conferir se a interface está ativa, inspecione a saída do comando a seguir:

 `# ip link show *interface*` 
```
3: wlan0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state DOWN mode DORMANT group default qlen 1000
    link/ether 12:34:56:78:9a:bc brd ff:ff:ff:ff:ff:ff

```

O `UP` em `<BROADCAST,MULTICAST,UP,LOWER_UP>` é o que indica que a interface está ativa, e não o `state DOWN` em seguida.

#### Descobrir pontos de acesso

Para ver quais pontos de acesso estão disponíveis, execute:

```
# iw dev *interface* scan | less

```

**Nota:** Se ele exibir `Interface does not support scanning`, você provavelmente se esqueceu de instalar o firmware. Em alguns casos, esta mensagem também é exibida quando não se está executando *iw* como root.

**Dica:** Dependendo da sua localização, talvez seja necessário definir o [domínio regulatório](#Respeitar_o_dom.C3.ADnio_regulat.C3.B3rio) correto para ver todas as redes disponíveis.

Os pontos importantes para verificar são:

*   **SSID:** o nome da rede.
*   **Signal:** é relatado numa proporção de potência de sinal sem fio em dBm (por exemplo, de -100 a 0). Quanto mais próximo o valor negativo chegar a zero, melhor será o sinal. Observar o poder relatado em um link de boa qualidade e um link ruim deve dar uma ideia sobre o alcance individual.
*   **Security:** não é relatado diretamente, devendo-se verificar a linha que começa com `capability`. Se houver `Privacy`, por exemplo, `capability: ESS Privacy ShortSlotTime (0x0411)`, a rede estará protegida de alguma forma.
    *   Se você vir um bloco de informação `RSN`, então a rede está protegida pelo protocolo [Robust Security Network](https://en.wikipedia.org/wiki/IEEE_802.11i-2004 "wikipedia:IEEE 802.11i-2004"), também conhecido como WPA2.
    *   Nos blocos `RSN` e `WPA`, você pode encontrar as informações a seguir:
        *   **Group cipher:** valor em TKIP, CCMP, both, others.
        *   **Pairwise ciphers:** valor TKIP, CCMP, both, others. Não necessariamente o mesmo valor que Group cipher.
        *   **Authentication suites:** valor em PSK, 802.1x, others. Para roteadores residenciais, você geralmente vai encontrar PSK (que significa *passphrase* ou, em português, senha). Em universidades, você provavelmente encontrará o padrão 802.1x que requer usuário e senha. Então, você precisará saber qual gerenciamento de chave está em uso (p. ex., EAP) e qual encapsulamento é usado (p. ex., PEAP). Veja [#WPA2 Empresarial](#WPA2_Empresarial) e [Wikipedia:Authentication protocol](https://en.wikipedia.org/wiki/Authentication_protocol "wikipedia:Authentication protocol") para detalhes.
    *   Se você não vir blocos `RSN` nem `WPA`, mas há `Privacy`, então WEP é usado.

#### Definir o modo de operação

Pode ser necessário definir o modo de operação adequado da placa sem fio. Mais especificamente, se você for conectar uma [rede ad-hoc](/index.php/Ad-hoc_networking "Ad-hoc networking"), você precisa definir o modo de operação para `ibss`:

```
# iw dev *interface* set type ibss

```

**Nota:** A mudança do modo de operação em algumas placas pode exibir que a interface sem fio esteja *desativada* (`ip link set *interface* down`).

#### Conectar a um ponto de acesso

Dependendo da criptografia, você precisa associar seu dispositivo sem fio ao ponto de acesso para usar e transmitir a chave de criptografia:

*   **Nenhuma criptografia** `# iw dev *interface* connect "*seu_essid*"` 
*   **WEP**
    *   usando uma chave hexadecimal ou ASCII (o formato é diferenciado automaticamente porque uma chave WEP tem um tamanho fixo): `# iw dev *interface* connect "*seu_essid*" key 0:*sua_chave*` 
    *   usando uma chave hexadecimal ou ASCII, especificando a terceira chave de configuração como padrão (as chaves são contadas a partir de zero, quatro são possíveis): `# iw dev *interface* connect "*sua_essid*" key d:2:*sua_chave*` 
*   **WPA/WPA2** - Veja [WPA supplicant#Connecting with wpa_passphrase](/index.php/WPA_supplicant#Connecting_with_wpa_passphrase "WPA supplicant").

Independentemente do método usado, você pode verificar se você conseguiu se associar com sucesso:

```
# iw dev *interface* link

```

#### Obter um endereço IP

Siga as instruções em [Configuração de rede#Atribuição manual](/index.php/Configura%C3%A7%C3%A3o_de_rede#Atribui.C3.A7.C3.A3o_manual "Configuração de rede") para mais informações nos exemplos a seguir.

##### Exemplo

Aqui está um exemplo completo de configuração de uma rede sem fio com o suplicante WPA e o DHCP.

```
# ip link set dev wlan0 up
# wpa_supplicant -B -i wlan0 -c /etc/wpa_supplicant/wpa_supplicant.conf
# dhcpcd wlan0

```

E então, para fechar a conexão, você pode simplesmente desabilitar a interface:

```
# ip link set dev wlan0 down

```

Para um IP estático, você substituiria a chamada *dhcpcd* por

```
# ip addr add 192.168.0.10/24 broadcast 192.168.0.255 dev wlan0
# ip route add default via 192.168.0.1

```

E antes de desabilitar a interface, você deve primeiro liberar o endereço IP e o gateway:

```
# ip addr flush dev wlan0
# ip route flush dev wlan0

```

### Configuração automática

Existem muitas soluções para escolher, mas lembre-se de que todas elas são mutuamente exclusivas; você não deve executar dois daemons simultaneamente. A tabela a seguir compara os diferentes gerenciadores de conexões, as notas adicionais estão nas subseções abaixo.

| Gerenciador
de rede | Suporte
a perfis
de rede | Roaming
(autoconexão de localização
descartada ou alterada) | Suporte a [PPP](https://en.wikipedia.org/wiki/pt:Protocolo_Ponto-a-Ponto "wikipedia:pt:Protocolo Ponto-a-Ponto")
(ex., modem 3G) | [Archiso](/index.php/Archiso "Archiso") [[1]](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.both) | GUI
oficial | Ferramentas
de console | Units de sistemd |
| [ConnMan](/index.php/ConnMan "ConnMan") | Sim | Sim | Sim | Não | Não | `connmanctl` | `connman.service` |
| [netctl](/index.php/Netctl "Netctl") | Sim | Sim | Sim | Sim ([base](https://www.archlinux.org/groups/x86_64/base/)) | Não | `netctl`,`wifi-menu` | `netctl-auto@*interface*.service` |
| [NetworkManager](/index.php/NetworkManager_(Portugu%C3%AAs) "NetworkManager (Português)") | Sim | Sim | Sim | Não | Sim | `nmcli`,`nmtui` | `NetworkManager.service` |
| [Wicd](/index.php/Wicd "Wicd") | Sim | Sim | Não | Não | Sim | `wicd-curses` | `wicd.service` |
| [Wifi Radar](/index.php/Wifi_Radar "Wifi Radar") | Sim | Sim | Não | Não | Sim | `wifi-radar` |

Veja também [List of applications/Internet#Network managers](/index.php/List_of_applications/Internet#Network_managers "List of applications/Internet").

## WPA2 Empresarial

Do inglês *WPA2 Enterprise*, é um modo de [Wi-Fi Protected Access](https://en.wikipedia.org/wiki/pt:Wi-Fi_Protected_Access "wikipedia:pt:Wi-Fi Protected Access"). Ele oferece melhor segurança e gerenciamento de chaves do que o *WPA2 Pessoal* *(WPA2 Personal)* e suporta outras funcionalidades do tipo corporativo, como VLANs e [NAP](https://en.wikipedia.org/wiki/pt:Prote%C3%A7%C3%A3o_de_Acesso_%C3%A0_Rede "wikipedia:pt:Proteção de Acesso à Rede"). No entanto, é necessário um servidor de autenticação externo, chamado servidor [RADIUS](https://en.wikipedia.org/wiki/pt:RADIUS "wikipedia:pt:RADIUS") para lidar com a autenticação de usuários. Isso está em contraste com o modo Pessoal, que não exige nada além do roteador sem fio ou pontos de acesso (APs) e usa uma única senha ou senha para todos os usuários.

O modo Empresarial permite que os usuários façam logon na rede Wi-Fi com um nome de usuário e senha e/ou um certificado digital. Como cada usuário tem uma chave de criptografia única e dinâmica, ele também ajuda a evitar a espionagem usuário a usuário na rede sem fio e melhora a força da criptografia.

Esta seção descreve a configuração da [clientes de rede](/index.php/List_of_applications#Network_managers "List of applications") para se conectar a um ponto de acesso sem fio com o modo WPA2 Empresarial. Consulte [Software access point#RADIUS](/index.php/Software_access_point#RADIUS "Software access point") para obter informações sobre como configurar um próprio ponto de acesso.

**Nota:** O modo Empresarial requer uma configuração de cliente mais complexa, enquanto o modo Pessoal requer apenas a inserção de uma senha quando solicitado. É provável que os clientes precisem instalar o certificado de AC do servidor (mais certificados por usuário se usar EAP-TLS) e, em seguida, configurar manualmente a segurança sem fio e as configurações de autenticação 802.1X.

Para uma comparação de protocolos, veja a seguinte [tabela](http://deployingradius.com/documents/protocols/compatibility.html).

**Atenção:** É possível usar o WPA2 Empresarial sem que o cliente verifique o certificado de AC do servidor. No entanto, você deve sempre procurar fazê-lo, porque sem autenticar o ponto de acesso, a conexão pode estar sujeita a um ataque *man-in-the-middle*. Isso pode acontecer porque, embora o handshake de conexão em si possa ser criptografado, as configurações mais usadas transmitem a própria senha em texto simples ou no modo facilmente quebrável [#MS-CHAPv2](#MS-CHAPv2). Portanto, o cliente pode enviar a senha para um ponto de acesso mal-intencionado que, então, faz o proxy da conexão.

### eduroam

[Eduroam](https://en.wikipedia.org/wiki/pt:eduroam "wikipedia:pt:eduroam") (acrônimo em inglês para *education roaming*) é uma rede de serviços internacional de roaming para os usuários em pesquisa no ensino superior e cursos subsequentes, baseado em WPA2 Empresarial.

**Nota:**

*   Verifique os detalhes da conexão **primeiro** com sua instituição antes de aplicar os perfis listados nesta seção. Não é garantido que os perfis de exemplo funcionem ou correspondam a quaisquer requisitos de segurança.
*   Ao armazenar os perfis de conexão não criptografados, recomenda-se restringir o acesso de leitura à conta root, especificando `chmod 600 *perfil*` como root.

**Dica:** A configuração para o [NetworkManager](/index.php/NetworkManager_(Portugu%C3%AAs) "NetworkManager (Português)") e [#wpa_supplicant](#wpa_supplicant) podem ser geradas com a [ferramenta assistente de configuração (CAT) do eduroam](https://cat.eduroam.org/) .

### Configuração manual/automática

#### wpa_supplicant

[Suplicante de WPA](/index.php/WPA_supplicant#Advanced_usage "WPA supplicant") pode ser configurado diretamente e usado em combinação com um cliente DHCP ou com systemd. Veja os exemplos em `/usr/share/doc/wpa_supplicant/wpa_supplicant.conf` para configurar os detalhes de conexão.

#### NetworkManager

[NetworkManager (Português)](/index.php/NetworkManager_(Portugu%C3%AAs) "NetworkManager (Português)") pode gerar perfis de WPA2 Empresarial com [frontends gráficos](/index.php/NetworkManager_(Portugu%C3%AAs)#Front-ends "NetworkManager (Português)"). *nmcli* e *nmtui* não oferecem suporte a isso, mas podem usar perfis existentes.

#### connman

[ConnMan](/index.php/ConnMan "ConnMan") precisa de um arquivo de configuração separado antes de [se conectar](/index.php/ConnMan#Wi-Fi "ConnMan") à rede. Veja [connman-service.config(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/connman-service.config.5) e [Connman#Connecting to eduroam](/index.php/ConnMan#Connecting_to_eduroam_.28802.1X.29 "ConnMan") para detalhes.

#### netctl

[netctl](/index.php/Netctl "Netctl") possui suporte a configuração de [#wpa_supplicant](#wpa_supplicant) por meio de blocos inclusos com `WPAConfigSection=`. Veja [netctl.profile(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/netctl.profile.5) para detalhes.

**Atenção:** Regras de uso especial de aspas se aplicam: veja a seção `*SPECIAL QUOTING RULES*` em [netctl.profile(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/netctl.profile.5).

**Dica:** Certificados personalizados podem ser especificados adicionando a linha `'ca_cert="/caminho/para/o/ceritficado.cer"'` em `WPAConfigSection`.

### Solução de problemas

#### MS-CHAPv2

As redes sem fio WPA2 Empresarial que exigem autenticação tipo 2 de MSCHAPv2 com PEAP às vezes exigem [pptpclient](https://www.archlinux.org/packages/?name=pptpclient), além do pacote [ppp](https://www.archlinux.org/packages/?name=ppp). [netctl](/index.php/Netctl "Netctl") parece funcionar facilmente sem ppp-mppe, no entanto. Em ambos os casos, o uso de MSCHAPv2 é desencorajado, pois é altamente vulnerável, embora o uso de outro método geralmente não seja uma opção. Veja também [[2]](https://www.cloudcracker.com/blog/2012/07/29/cracking-ms-chap-v2/) e [.pdf](http://research.edm.uhasselt.be/~bbonne/docs/robyns14wpa2enterprise).

## Dicas e truques

### Respeitar o domínio regulatório

The [regulatory domain](https://en.wikipedia.org/wiki/IEEE_802.11#Regulatory_domains_and_legal_compliance "wikipedia:IEEE 802.11"), or "regdomain", is used to reconfigure wireless drivers to make sure that wireless hardware usage complies with local laws set by the FCC, ETSI and other organizations. Regdomains use [ISO 3166-1 alpha-2 country codes](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2 "wikipedia:ISO 3166-1 alpha-2"). For example, the regdomain of the United States would be "US", China would be "CN", etc.

Regdomains affect the availability of wireless channels. In the 2.4GHz band, the allowed channels are 1-11 for the US, 1-14 for Japan, and 1-13 for most of the rest of the world. In the 5GHz band, the rules for allowed channels are much more complex. In either case, consult [this list of WLAN channels](https://en.wikipedia.org/wiki/List_of_WLAN_channels "wikipedia:List of WLAN channels") for more detailed information.

Regdomains also affect the limit on the [effective isotropic radiated power (EIRP)](https://en.wikipedia.org/wiki/Equivalent_isotropically_radiated_power "wikipedia:Equivalent isotropically radiated power") from wireless devices. This is derived from transmit power/"tx power", and is measured in [dBm/mBm (1dBm=100mBm) or mW (log scale)](https://en.wikipedia.org/wiki/DBm "wikipedia:DBm"). In the 2.4GHz band, the maximum is 30dBm in the US and Canada, 20dBm in most of Europe, and 20dB-30dBm for the rest of the world. In the 5GHz band, maximums are usually lower. Consult the [wireless-regdb](http://git.kernel.org/cgit/linux/kernel/git/linville/wireless-regdb.git/tree/db.txt) for more detailed information (EIRP dBm values are in the second set of brackets for each line).

Misconfiguring the regdomain can be useful - for example, by allowing use of an unused channel when other channels are crowded, or by allowing an increase in tx power to widen transmitter range. However, **this is not recommended** as it could break local laws and cause interference with other radio devices.

To configure the regdomain, install [crda](https://www.archlinux.org/packages/?name=crda) and reboot (to reload the `cfg80211` module and all related drivers). Check the boot log to make sure that CRDA is being called by `cfg80211`:

```
$ dmesg | grep cfg80211

```

The current regdomain can be set to the United States with:

```
# iw reg set US

```

And queried with:

```
$ iw reg get

```

**Note:** Your device may be set to country "00", which is the "world regulatory domain" and contains generic settings. If this cannot be unset, CRDA may be misconfigured.

However, setting the regdomain may not alter your settings. Some devices have a regdomain set in firmware/EEPROM, which dictates the limits of the device, meaning that setting regdomain in software [can only increase restrictions](http://wiki.openwrt.org/doc/howto/wireless.utilities#iw), not decrease them. For example, a CN device could be set in software to the US regdomain, but because CN has an EIRP maximum of 20dBm, the device will not be able to transmit at the US maximum of 30dBm.

For example, to see if the regdomain is being set in firmware for an Atheros device:

```
$ dmesg | grep ath:

```

For other chipsets, it may help to search for "EEPROM", "regdomain", or simply the name of the device driver.

To see if your regdomain change has been successful, and to query the number of available channels and their allowed transmit power:

```
$ iw list | grep -A 15 Frequencies:

```

A more permanent configuration of the regdomain can be achieved through editing `/etc/conf.d/wireless-regdom` and uncommenting the appropriate domain.

[WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") can also use a regdomain in the `country=` line of `/etc/wpa_supplicant/wpa_supplicant.conf`.

It is also possible to configure the [cfg80211](http://wireless.kernel.org/en/developers/Documentation/cfg80211) kernel module to use a specific regdomain by adding, for example, `options cfg80211 ieee80211_regdom=EU` as [module options](/index.php/Kernel_modules#Setting_module_options "Kernel modules"). However, this is part of the [old regulatory implementation](http://wireless.kernel.org/en/developers/Regulatory#The_ieee80211_regdom_module_parameter).

For further information, read the [wireless.kernel.org regulatory documentation](http://wireless.kernel.org/en/developers/Regulatory/).

### Comparação entre iw e wireless_tools

The table below gives an overview of comparable commands for *iw* and *wireless_tools*. See [iw replaces iwconfig](http://wireless.kernel.org/en/users/Documentation/iw/replace-iwconfig) for more examples.

| *iw* command | *wireless_tools* command | Description |
| iw dev *wlan0* link | iwconfig *wlan0* | Getting link status. |
| iw dev *wlan0* scan | iwlist *wlan0* scan | Scanning for available access points. |
| iw dev *wlan0* set type ibss | iwconfig *wlan0* mode ad-hoc | Setting the operation mode to *ad-hoc*. |
| iw dev *wlan0* connect *your_essid* | iwconfig *wlan0* essid *your_essid* | Connecting to open network. |
| iw dev *wlan0* connect *your_essid* 2432 | iwconfig *wlan0* essid *your_essid* freq 2432M | Connecting to open network specifying channel. |
| iw dev *wlan0* connect *your_essid* key 0:*your_key* | iwconfig *wlan0* essid *your_essid* key *your_key* | Connecting to WEP encrypted network using hexadecimal key. |
| iwconfig *wlan0* essid *your_essid* key s:*your_key* | Connecting to WEP encrypted network using ASCII key. |
| iw dev *wlan0* set power_save on | iwconfig *wlan0* power on | Enabling power save. |

## Solução de problemas

This section contains general troubleshooting tips, not strictly related to problems with drivers or firmware. For such topics, see next section [#Troubleshooting drivers and firmware](#Troubleshooting_drivers_and_firmware).

### Acesso temporário à internet

If you have problematic hardware and need internet access to, for example, download some software or get help in forums, you can make use of Android's built-in feature for internet sharing via USB cable. See [Android tethering#USB tethering](/index.php/Android_tethering#USB_tethering "Android tethering") for more information.

### Problemas com rfkill

Many laptops have a hardware button (or switch) to turn off wireless card, however, the card can also be blocked by kernel. This can be handled by *rfkill*. To show the current status:

 `# rfkill list` 
```
0: phy0: Wireless LAN
	Soft blocked: yes
	Hard blocked: yes

```

If the card is *hard-blocked*, use the hardware button (switch) to unblock it. If the card is not *hard-blocked* but *soft-blocked*, use the following command:

```
# rfkill unblock wifi

```

**Note:** It is possible that the card will go from *hard-blocked* and *soft-unblocked* state into *hard-unblocked* and *soft-blocked* state by pressing the hardware button (i.e. the *soft-blocked* bit is just switched no matter what). This can be adjusted by tuning some options of the `rfkill` [kernel module](/index.php/Kernel_module "Kernel module").

Hardware buttons to toggle wireless cards are handled by a vendor specific [kernel module](/index.php/Kernel_module "Kernel module"), frequently these are [WMI](https://lwn.net/Articles/391230/) modules. Particularly for very new hardware models, it happens that the model is not fully supported in the latest stable kernel yet. In this case it often helps to search the kernel bug tracker for information and report the model to the maintainer of the respective vendor kernel module, if it has not happened already.

See also [[3]](http://askubuntu.com/questions/62166/siocsifflags-operation-not-possible-due-to-rf-kill).

### Observando os logs

A good first measure to troubleshoot is to analyze the system's logfiles first. In order not to manually parse through them all, it can help to open a second terminal/console window and watch the kernels messages with

```
$ dmesg -w

```

while performing the action, e.g. the wireless association attempt.

When using a tool for network management, the same can be done for systemd with

```
# journalctl -f 

```

Frequently a wireless error is accompanied by a deauthentication with a particular reason code, for example:

```
wlan0: deauthenticating from XX:XX:XX:XX:XX:XX by local choice (reason=3)

```

Looking up [the reason code](http://www.aboutcher.co.uk/2012/07/linux-wifi-deauthenticated-reason-codes/) might give a first hint. Maybe it also helps you to look at the control message [flowchart](https://wireless.wiki.kernel.org/en/developers/documentation/mac80211/auth-assoc-deauth), the journal messages will follow it.

The individual tools used in this article further provide options for more detailed debugging output, which can be used in a second step of the analysis, if required.

### Economia de energia

See [Power saving#Network interfaces](/index.php/Power_saving#Network_interfaces "Power saving").

### Falha ao obter endereço IP

*   If getting an IP address repeatedly fails using the default [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) client, try installing and using [dhclient](https://www.archlinux.org/packages/?name=dhclient) instead. Do not forget to select *dhclient* as the primary DHCP client in the [connection manager](#Automatic_setup).

*   If you can get an IP address for a wired interface and not for a wireless interface, try disabling the wireless card's [power saving](#Power_saving) features (specify `off` instead of `on`).

*   If you get a timeout error due to a *waiting for carrier* problem, then you might have to set the channel mode to `auto` for the specific device:

```
# iwconfig wlan0 channel auto

```

Before changing the channel to auto, make sure your wireless interface is down. After it has successfully changed it, you can bring the interface up again and continue from there.

### Endereço IP válido, mas não consegue resolver host

If you are on a public wireless network that may have a [captive portal](https://en.wikipedia.org/wiki/Captive_portal "wikipedia:Captive portal"), make sure to query an HTTP page (not an HTTPS page) from your web browser, as some captive portals only redirect HTTP. If this is not the issue, it may be necessary to remove any custom DNS servers from [resolv.conf](/index.php/Resolv.conf "Resolv.conf").

### Definindo limites de RTS e de fragmentação

Wireless hardware disables RTS and fragmentation by default. These are two different methods of increasing throughput at the expense of bandwidth (i.e. reliability at the expense of speed). These are useful in environments with wireless noise or many adjacent access points, which may create interference leading to timeouts or failing connections.

Packet fragmentation improves throughput by splitting up packets with size exceeding the fragmentation threshold. The maximum value (2346) effectively disables fragmentation since no packet can exceed it. The minimum value (256) maximizes throughput, but may carry a significant bandwidth cost.

```
# iw phy0 set frag 512

```

[RTS](https://en.wikipedia.org/wiki/IEEE_802.11_RTS/CTS "wikipedia:IEEE 802.11 RTS/CTS") improves throughput by performing a handshake with the access point before transmitting packets with size exceeding the RTS threshold. The maximum threshold (2347) effectively disables RTS since no packet can exceed it. The minimum threshold (0) enables RTS for all packets, which is probably excessive for most situations.

```
# iw phy0 set rts 500

```

**Note:** `phy0` is the name of the wireless device as listed by `$ iw phy`.

### Desconexões aleatórias

#### Causa nº.1

If dmesg says `wlan0: deauthenticating from MAC by local choice (reason=3)` and you lose your Wi-Fi connection, it is likely that you have a bit too aggressive power-saving on your Wi-Fi card[[4]](http://us.generation-nt.com/answer/gentoo-user-wireless-deauthenticating-by-local-choice-help-204640041.html). Try disabling the wireless card's [power saving](#Power_saving) features (specify `off` instead of `on`).

If your card does not support enabling/disabling power save mode, check the BIOS for power management options. Disabling PCI-Express power management in the BIOS of a Lenovo W520 resolved this issue.

#### Causa nº.2

If you are experiencing frequent disconnections and dmesg shows messages such as

`ieee80211 phy0: wlan0: No probe response from AP xx:xx:xx:xx:xx:xx after 500ms, disconnecting`

try changing the channel bandwidth to `20MHz` through your router's settings page.

#### Causa nº.3

On some laptop models with hardware rfkill switches (e.g., Thinkpad X200 series), due to wear or bad design, the switch (or its connection to the mainboard) might become loose over time resulting in seemingly random hardblocks/disconnects when you accidentally touch the switch or move the laptop. There is no software solution to this, unless your switch is electrical and the BIOS offers the option to disable the switch. If your switch is mechanical (most are), there are lots of possible solutions, most of which aim to disable the switch: Soldering the contact point on the mainboard/wifi-card, glueing or blocking the switch, using a screw nut to tighten the switch or removing it altogether.

#### Causa nº.4

Another cause for frequent disconnects or a complete failure to connect may also be a sub-standard router, incomplete settings of the router, or interference by other wireless devices.

To troubleshoot, first best try to connect to the router with no authentication.

If that works, enable WPA/WPA2 again but choose fixed and/or limited router settings. For example:

*   If the router is considerably older than the wireless device you use for the client, test if it works with setting the router to one wireless mode
*   Disable mixed-mode authentication (e.g. only WPA2 with AES, or TKIP if the router is old)
*   Try a fixed/free channel rather than "auto" channel (maybe the router next door is old and interfering)
*   Disable WPS
*   Disable `40Mhz` channel bandwidth (lower throughput but less likely collisions)
*   If the router has quality of service settings, check completeness of settings (e.g. Wi-Fi Multimedia (WMM) is part of optional QoS flow control. An erroneous router firmware may advertise its existence although the setting is not enabled)

### Redes Wi-Fi invisíveis por causa do domínio regulatório incorreto

If the computer's Wi-Fi channels do not match those of the user's country, that may result in some in-range Wi-Fi networks becoming invisible, because they use wireless channels that aren't allowed by default. The solution is to configure the regulatory domain correctly, see [#Respecting the regulatory domain](#Respecting_the_regulatory_domain).

## Solução de problemas de drivers e firmware

This section covers methods and procedures for installing kernel modules and *firmware* for specific chipsets, that differ from generic method.

See [Kernel modules](/index.php/Kernel_modules "Kernel modules") for general information on operations with modules.

### Ralink/Mediatek

#### rt2x00

Unified driver for Ralink chipsets (it replaces `rt2500`, `rt61`, `rt73`, etc). This driver has been in the Linux kernel since 2.6.24, you only need to load the right module for the chip: `rt2400pci`, `rt2500pci`, `rt2500usb`, `rt61pci` or `rt73usb` which will autoload the respective `rt2x00` modules too.

A list of devices supported by the modules is available at the project's [homepage](http://rt2x00.serialmonkey.com/wiki/index.php/Hardware).

	Additional notes

*   Since kernel 3.0, rt2x00 includes also these drivers: `rt2800pci`, `rt2800usb`.
*   Since kernel 3.0, the staging drivers `rt2860sta` and `rt2870sta` are replaced by the mainline drivers `rt2800pci` and `rt2800usb`.
*   Some devices have a wide range of options that can be configured with `iwpriv`. These are documented in the [source tarballs](http://web.ralinktech.com/ralink/Home/Support/Linux.html) available from Ralink.

#### rt3090

For devices which are using the rt3090 chipset it should be possible to use `rt2800pci` driver, however, is not working with this chipset very well (e.g. sometimes it is not possible to use higher rate than 2Mb/s).

#### rt3290

The rt3290 chipset is recognised by the kernel `rt2800pci` module. However, some users experience problems and reverting to a patched Ralink driver seems to be beneficial in these [cases](https://bbs.archlinux.org/viewtopic.php?id=161952).

#### rt3573

New chipset as of 2012\. It may require proprietary drivers from Ralink. Different manufacturers use it, see the [Belkin N750 DB wireless usb adapter](https://bbs.archlinux.org/viewtopic.php?pid=1164228#p1164228) forums thread.

#### rt5572

New chipset as of 2012 with support for 5 Ghz bands. It may require proprietary drivers from Ralink and some effort to compile them. At the time of writing a how-to on compilation is available for a DLINK DWA-160 rev. B2 [here](http://bernaerts.dyndns.org/linux/229-ubuntu-precise-dlink-dwa160-revb2).

#### mt7612u

New chipset as of 2014, released under their new commercial name Mediatek. It is an AC1200 or AC1300 chipset. Manufacturer provides drivers for Linux on their [support page](https://www.mediatek.com/products/broadbandWifi/mt7612u)

### Realtek

See [[6]](https://wikidevi.com/wiki/Realtek) for a list of Realtek chipsets and specifications.

#### rtl8192cu

The driver is now in the kernel, but many users have reported being unable to make a connection although scanning for networks does work.

[8192cu-dkms](https://aur.archlinux.org/packages/8192cu-dkms/) includes many patches, try this if it does not work fine with the driver in kernel.

#### rtl8723ae/rtl8723be

The `rtl8723ae` and `rtl8723be` modules are included in the mainline Linux kernel.

Some users may encounter errors with powersave on this card. This is shown with occasional disconnects that are not recognized by high level network managers ([netctl](/index.php/Netctl "Netctl"), [NetworkManager](/index.php/NetworkManager "NetworkManager")). This error can be confirmed by running `dmesg -w` or `journalctl -f` and looking for output related to powersave and the `rtl8723ae`/`rtl8723be` module. If you are having this issue, use the `fwlps=0` kernel option, which should prevent the WiFi card from automatically sleeping and halting connection.

 `/etc/modprobe.d/rtl8723ae.conf`  `options rtl8723ae fwlps=0` 

or

 `/etc/modprobe.d/rtl8723be.conf`  `options rtl8723be fwlps=0` 

If you have poor signal, perhaps your device has only one physical antenna connected, and antenna autoselection is broken. You can force the choice of antenna with `ant_sel=1` or `ant_sel=2` kernel option. [[7]](https://bbs.archlinux.org/viewtopic.php?id=208472)

#### rtl88xxau

Realtek chipsets rtl8811au/rtl8812au/rtl8814au/rtl8821au designed for various USB adapters ranging from AC600 to AC1900.

Several packages provide the kernel drivers:

| Chipset | Driver version | [AUR](/index.php/AUR "AUR") package | Notes |
| rtl8812au | 5.2.9.3 | [rtl8812au-dkms-git](https://aur.archlinux.org/packages/rtl8812au-dkms-git/) | Latest driver version for rtl8812au only |
| rtl8811au, rtl8812au and rtl8821au | 5.1.5 | [rtl8821au-dkms-git](https://aur.archlinux.org/packages/rtl8821au-dkms-git/) | Works, for rtl8812au latest version is recommended instead |
| rtl8814au | 4.3.21 | [rtl8814au-dkms-git](https://aur.archlinux.org/packages/rtl8814au-dkms-git/) | Possibly works for rtl8813au too |

These require [DKMS](/index.php/DKMS "DKMS") so make sure you have your proper kernel headers installed.

#### rtl8822bu

[rtl8822bu-dkms-git](https://aur.archlinux.org/packages/rtl8822bu-dkms-git/) provides a kernel module for the Realtek 8822bu chipset found in the Edimax EW7822ULC USB3 and Asus AC53 Nano USB 802.11ac adapter.

This requires [DKMS](/index.php/DKMS "DKMS"), so make sure you have your proper kernel headers installed.

#### rtl8xxxu

Issues with the `rtl8xxxu` mainline kernel module may be solved by compiling a third-party module for the specific chipset. The source code can be found in [GitHub repositories](https://github.com/lwfinger?tab=repositories).

Some drivers may be already prepared in the AUR, e.g. [rtl8723bu-git](https://aur.archlinux.org/packages/rtl8723bu-git/) and [rtl8723bu-git-dkms](https://aur.archlinux.org/packages/rtl8723bu-git-dkms/).

### Atheros

The [MadWifi team](http://madwifi-project.org/) currently maintains three different drivers for devices with Atheros chipset:

*   `madwifi` is an old, obsolete driver. Not present in Arch kernel since 2.6.39.1.
*   `ath5k` is newer driver, which replaces the `madwifi` driver. Currently a better choice for some chipsets, but not all chipsets are supported (see below)
*   `ath9k` is the newest of these three drivers, it is intended for newer Atheros chipsets. All of the chips with 802.11n capabilities are supported.

There are some other drivers for some Atheros devices. See [Linux Wireless documentation](http://wireless.kernel.org/en/users/Drivers/Atheros#PCI_.2F_PCI-E_.2F_AHB_Drivers) for details.

#### ath5k

External resources:

*   [http://wireless.kernel.org/en/users/Drivers/ath5k](http://wireless.kernel.org/en/users/Drivers/ath5k)
*   [http://wiki.debian.org/ath5k](http://wiki.debian.org/ath5k)

If you find web pages randomly loading very slow, or if the device is unable to lease an IP address, try to switch from hardware to software encryption by loading the `ath5k` module with `nohwcrypt=1` option. See [Kernel modules#Setting module options](/index.php/Kernel_modules#Setting_module_options "Kernel modules") for details.

Some laptops may have problems with their wireless LED indicator flickering red and blue. To solve this problem, do:

```
# echo none > /sys/class/leds/ath5k-phy0::tx/trigger
# echo none > /sys/class/leds/ath5k-phy0::rx/trigger

```

For alternatives, see [this bug report](https://bugzilla.redhat.com/show_bug.cgi?id=618232).

#### ath9k

External resources:

*   [http://wireless.kernel.org/en/users/Drivers/ath9k](http://wireless.kernel.org/en/users/Drivers/ath9k)
*   [http://wiki.debian.org/ath9k](http://wiki.debian.org/ath9k)

As of Linux 3.15.1, some users have been experiencing a decrease in bandwidth. In some cases this can fixed by editing `/etc/modprobe.d/ath9k.conf` and adding the line:

```
options ath9k nohwcrypt=1

```

**Note:** Check with the command lsmod what module(-name) is in use and change it if named otherwise (e.g. ath9k_htc).

In the unlikely event that you have stability issues that trouble you, you could try using the [backports-patched](https://aur.archlinux.org/packages/backports-patched/) package. An [ath9k mailing list](https://lists.ath9k.org/mailman/listinfo/ath9k-devel) exists for support and development related discussions.

##### Economia de energia

Although [Linux Wireless](http://wireless.kernel.org/en/users/Documentation/dynamic-power-save) says that dynamic power saving is enabled for Atheros ath9k single-chips newer than AR9280, for some devices (e.g. AR9285) [powertop](https://www.archlinux.org/packages/?name=powertop) might still report that power saving is disabled. In this case enable it manually.

On some devices (e.g. AR9285), enabling the power saving might result in the following error:

 `# iw dev wlan0 set power_save on` 
```
command failed: Operation not supported (-95)

```

The solution is to set the `ps_enable=1` option for the `ath9k` module:

 `/etc/modprobe.d/ath9k.conf`  `options ath9k ps_enable=1` 

### Intel

#### ipw2100 e ipw2200

These modules are fully supported in the kernel, but they require additional firmware. Depending on which of the chipsets you have, [install](/index.php/Install "Install") either [ipw2100-fw](https://www.archlinux.org/packages/?name=ipw2100-fw) or [ipw2200-fw](https://www.archlinux.org/packages/?name=ipw2200-fw). Then [reload](/index.php/Kernel_modules#Manual_module_handling "Kernel modules") the appropriate module.

**Tip:** You may use the following [module options](/index.php/Kernel_modules#Setting_module_options "Kernel modules"):

*   use the `rtap_iface=1` option to enable the radiotap interface
*   use the `led=1` option to enable a front LED indicating when the wireless is connected or not

#### iwlegacy

[iwlegacy](http://wireless.kernel.org/en/users/Drivers/iwlegacy) is the wireless driver for Intel's 3945 and 4965 wireless chips. The firmware is included in the [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) package.

[udev](/index.php/Udev "Udev") should load the driver automatically, otherwise load `iwl3945` or `iwl4965` manually. See [Kernel modules](/index.php/Kernel_modules "Kernel modules") for details.

If you have problems connecting to networks in general, random failures with your card on bootup or your link quality is very poor, try to disable 802.11n:

 `/etc/modprobe.d/iwl4965.conf`  `options iwl4965 11n_disable=1` 

If the failures persist during bootup and you are using Nouveau driver, try [enabling early KMS](/index.php/Nouveau#Enable_early_KMS "Nouveau") to prevent the conflict [[9]](https://bbs.archlinux.org/viewtopic.php?pid=1748667#p1748667).

#### iwlwifi

[iwlwifi](http://wireless.kernel.org/en/users/Drivers/iwlwifi) is the wireless driver for Intel's current wireless chips, such as 5100AGN, 5300AGN, and 5350AGN. See the [full list of supported devices](http://wireless.kernel.org/en/users/Drivers/iwlwifi#Supported_Devices). The firmware is included in the [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) package. The [linux-firmware-iwlwifi-git](https://aur.archlinux.org/packages/linux-firmware-iwlwifi-git/) may contain some updates sooner.

If you have problems connecting to networks in general or your link quality is very poor, try to disable 802.11n, and perhaps also enable software encryption:

 `/etc/modprobe.d/iwlwifi.conf`  `options iwlwifi 11n_disable=1 swcrypto=1` 

If you have a problem with slow uplink speed in 802.11n mode, for example 20Mbps, try to enable antenna aggregation:

 `/etc/modprobe.d/iwlwifi.conf`  `options iwlwifi 11n_disable=8` 

Do not be confused with the option name, when the value is set to `8` it does not disable anything but re-enables transmission antenna aggregation.[[10]](http://forums.gentoo.org/viewtopic-t-996692.html?sid=81bdfa435c089360bdfd9368fe0339a9) [[11]](https://bugzilla.kernel.org/show_bug.cgi?id=81571)

In case this does not work for you, you may try disabling [power saving](/index.php/Power_saving#Network_interfaces "Power saving") for your wireless adapter.

[Some](http://ubuntuforums.org/showthread.php?t=2183486&p=12845473#post12845473) have never gotten this to work. [Others](http://ubuntuforums.org/showthread.php?t=2205733&p=12935783#post12935783) found salvation by disabling N in their router settings after trying everything. This is known to have be the only solution on more than one occasion. The second link there mentions a 5ghz option that might be worth exploring.

##### Coexistência com Bluetooth

If you have difficulty connecting a bluetooth headset and maintaining good downlink speed, try disabling bluetooth coexistence [[12]](https://wireless.wiki.kernel.org/en/users/Drivers/iwlwifi#wifibluetooth_coexistence):

 `/etc/modprobe.d/iwlwifi.conf`  `options iwlwifi bt_coex_active=0` 

#### Desabilitar piscada de LED

**Note:** This works with the `iwlegacy` and `iwlwifi` drivers.

The default settings on the module are to have the LED blink on activity. Some people find this extremely annoying. To have the LED on solid when Wi-Fi is active, you can use the [systemd-tmpfiles](/index.php/Systemd#Temporary_files "Systemd"):

 `/etc/tmpfiles.d/phy0-led.conf` 
```
w /sys/class/leds/phy0-led/trigger - - - - phy0radio

```

Run `systemd-tmpfiles --create phy0-led.conf` for the change to take effect, or reboot.

To see all the possible trigger values for this LED:

```
# cat /sys/class/leds/phy0-led/trigger

```

**Tip:** If you do not have `/sys/class/leds/phy0-led`, you may try to use the `led_mode="1"` [module option](/index.php/Kernel_modules#Setting_module_options "Kernel modules"). It should be valid for both `iwlwifi` and `iwlegacy` drivers.

### Broadcom

See [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless").

### Outros drivers/dispositivos

#### Tenda w322u

Treat this Tenda card as an `rt2870sta` device. See [#rt2x00](#rt2x00).

#### orinoco

This should be a part of the kernel package and be installed already.

Some Orinoco chipsets are Hermes II. You can use the `wlags49_h2_cs` driver instead of `orinoco_cs` and gain WPA support. To use the driver, [blacklist](/index.php/Blacklist "Blacklist") `orinoco_cs` first.

#### prism54

The driver `p54` is included in kernel, but you have to download the appropriate firmware for your card from [this site](http://linuxwireless.org/en/users/Drivers/p54#firmware) and install it into the `/usr/lib/firmware` directory.

**Note:** There is also older, deprecated driver `prism54`, which might conflict with the newer driver (`p54pci` or `p54usb`). Make sure to [blacklist](/index.php/Blacklist "Blacklist") `prism54`.

#### ACX100/111

**Warning:** The drivers for these devices [are broken](https://mailman.archlinux.org/pipermail/arch-dev-public/2011-June/020669.html) and do not work with newer kernel versions.

Packages: `tiacx` `tiacx-firmware` (deleted from official repositories and AUR)

See [official wiki](http://sourceforge.net/apps/mediawiki/acx100/index.php?title=Main_Page) for details.

#### zd1211rw

[`zd1211rw`](http://zd1211.wiki.sourceforge.net/) is a driver for the ZyDAS ZD1211 802.11b/g USB WLAN chipset, and it is included in recent versions of the Linux kernel. See [[13]](http://www.linuxwireless.org/en/users/Drivers/zd1211rw/devices) for a list of supported devices. You only need to [install](/index.php/Install "Install") the firmware for the device, provided by the [zd1211-firmware](https://www.archlinux.org/packages/?name=zd1211-firmware) package.

#### hostap_cs

[Host AP](http://hostap.epitest.fi/) is a Linux driver for wireless LAN cards based on Intersil's Prism2/2.5/3 chipset. The driver is included in Linux kernel.

**Note:** Make sure to [blacklist](/index.php/Blacklist "Blacklist") the `orinico_cs` driver, it may cause problems.

### ndiswrapper

Ndiswrapper is a wrapper script that allows you to use some Windows drivers in Linux. You will need the `.inf` and `.sys` files from your Windows driver.

**Warning:** Be sure to use drivers appropriate to your architecture (x86 vs. x86_64).

**Tip:** If you need to extract these files from an `*.exe` file, you can use [cabextract](https://www.archlinux.org/packages/?name=cabextract).

Follow these steps to configure ndiswrapper.

1\. Install [ndiswrapper-dkms](https://www.archlinux.org/packages/?name=ndiswrapper-dkms)

2\. Install the driver to `/etc/ndiswrapper/*`

```
# ndiswrapper -i filename.inf

```

3\. List all installed drivers for ndiswrapper

```
$ ndiswrapper -l

```

4\. Let ndiswrapper write its configuration in `/etc/modprobe.d/ndiswrapper.conf`:

```
# ndiswrapper -m
# depmod -a

```

Now the ndiswrapper install is almost finished; follow the instructions on [Kernel modules#Automatic module handling](/index.php/Kernel_modules#Automatic_module_handling "Kernel modules") to automatically load the module at boot.

The important part is making sure that ndiswrapper exists on this line, so just add it alongside the other modules. It would be best to test that ndiswrapper will load now, so:

```
# modprobe ndiswrapper
# iwconfig

```

and *wlan0* should now exist. If you have problems, some help is available at: [ndiswrapper howto](http://sourceforge.net/p/ndiswrapper/ndiswrapper/HowTos/) and [ndiswrapper FAQ](http://sourceforge.net/p/ndiswrapper/ndiswrapper/FAQ/).

### backports-patched

[backports-patched](https://aur.archlinux.org/packages/backports-patched/) provide drivers released on newer kernels backported for usage on older kernels. The project started since 2007 and was originally known as compat-wireless, evolved to compat-drivers and was recently renamed simply to backports.

If you are using old kernel and have wireless issue, drivers in this package may help.

## Veja também

*   [The Linux Wireless project](http://wireless.kernel.org/)
*   [Aircrack-ng guide on installing drivers](http://aircrack-ng.org/doku.php?id=install_drivers)