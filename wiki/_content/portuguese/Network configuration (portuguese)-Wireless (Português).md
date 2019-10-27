**Status de tradução:** Esse artigo é uma tradução de [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration"). Data da última tradução: 2019-10-23\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Wireless_network_configuration&diff=0&oldid=586832) na versão em inglês.

Artigos relacionados

*   [Ponto de acesso por software](/index.php/Software_access_point "Software access point")
*   [Rede ad-hoc](/index.php/Ad-hoc_networking "Ad-hoc networking")
*   [Compartilhamento de internet](/index.php/Internet_sharing "Internet sharing")
*   [Vinculação de rede sem fio](/index.php/Wireless_bonding "Wireless bonding")
*   [Depuração de rede](/index.php/Network_Debugging "Network Debugging")
*   [Bluetooth](/index.php/Bluetooth "Bluetooth")

Veja [Configuração de rede](/index.php/Configura%C3%A7%C3%A3o_de_rede "Configuração de rede") para o artigo geral sobre como configurar uma conexão de rede.

A configuração de rede sem fio *(wireless)* é um processo de duas partes. A primeira parte é identificar e garantir que o driver correto para o seu dispositivo sem fio está instalado (eles estão disponíveis na mídia de instalação, mas geralmente precisam ser instalados explicitamente) e para configurar a interface. A segunda é escolher um método de gerenciamento de conexões sem fio. Este artigo abrange as duas partes e fornece links adicionais para ferramentas de gerenciamento sem fio.

A seção [#iw](#iw) descreve como gerenciar manualmente sua interface de rede sem fio / suas LANs sem fio usando [iw](https://www.archlinux.org/packages/?name=iw). A seção [Configuração de rede#Gerenciadores de rede](/index.php/Configura%C3%A7%C3%A3o_de_rede#Gerenciadores_de_rede "Configuração de rede") descreve vários programas que podem ser usados para gerenciar automaticamente sua interface sem fio, alguns dos quais incluem uma GUI e todos incluem suporte a perfis de rede (útil ao alternar frequentemente de redes sem fio, como laptops).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Driver de dispositivo](#Driver_de_dispositivo)
    *   [1.1 Verificar o status de driver](#Verificar_o_status_de_driver)
    *   [1.2 Instalar driver/firmware](#Instalar_driver/firmware)
*   [2 Utilitários](#Utilitários)
    *   [2.1 Comparação entre iw e wireless_tools](#Comparação_entre_iw_e_wireless_tools)
*   [3 iw](#iw)
    *   [3.1 Obter o nome da interface](#Obter_o_nome_da_interface)
    *   [3.2 Obter o status da interface](#Obter_o_status_da_interface)
    *   [3.3 Ativar a interface](#Ativar_a_interface)
    *   [3.4 Descobrir pontos de acesso](#Descobrir_pontos_de_acesso)
    *   [3.5 Definir o modo de operação](#Definir_o_modo_de_operação)
    *   [3.6 Conectar a um ponto de acesso](#Conectar_a_um_ponto_de_acesso)
*   [4 Wi-Fi Protected Access](#Wi-Fi_Protected_Access)
    *   [4.1 WPA2 Pessoal](#WPA2_Pessoal)
    *   [4.2 WPA2 Empresarial](#WPA2_Empresarial)
        *   [4.2.1 eduroam](#eduroam)
        *   [4.2.2 Configuração manual/automática](#Configuração_manual/automática)
        *   [4.2.3 Solução de problemas](#Solução_de_problemas)
            *   [4.2.3.1 MS-CHAPv2](#MS-CHAPv2)
*   [5 Dicas e truques](#Dicas_e_truques)
    *   [5.1 Respeitar o domínio regulatório](#Respeitar_o_domínio_regulatório)
    *   [5.2 Problemas com rfkill](#Problemas_com_rfkill)
*   [6 Economia de energia](#Economia_de_energia)
*   [7 Solução de problemas](#Solução_de_problemas_2)
    *   [7.1 Acesso temporário à internet](#Acesso_temporário_à_internet)
    *   [7.2 Observando os logs](#Observando_os_logs)
    *   [7.3 Falha ao obter endereço IP](#Falha_ao_obter_endereço_IP)
    *   [7.4 Endereço IP válido, mas não consegue resolver host](#Endereço_IP_válido,_mas_não_consegue_resolver_host)
    *   [7.5 Definindo limites de RTS e de fragmentação](#Definindo_limites_de_RTS_e_de_fragmentação)
    *   [7.6 Desconexões aleatórias](#Desconexões_aleatórias)
        *   [7.6.1 Causa nº.1](#Causa_nº.1)
        *   [7.6.2 Causa nº.2](#Causa_nº.2)
        *   [7.6.3 Causa nº.3](#Causa_nº.3)
        *   [7.6.4 Causa nº.4](#Causa_nº.4)
    *   [7.7 Redes Wi-Fi invisíveis por causa do domínio regulatório incorreto](#Redes_Wi-Fi_invisíveis_por_causa_do_domínio_regulatório_incorreto)
*   [8 Solução de problemas de drivers e firmware](#Solução_de_problemas_de_drivers_e_firmware)
    *   [8.1 Ralink/Mediatek](#Ralink/Mediatek)
        *   [8.1.1 rt2x00](#rt2x00)
        *   [8.1.2 rt3090](#rt3090)
        *   [8.1.3 rt3290](#rt3290)
        *   [8.1.4 rt3573](#rt3573)
        *   [8.1.5 rt5572](#rt5572)
        *   [8.1.6 mt7612u](#mt7612u)
    *   [8.2 Realtek](#Realtek)
        *   [8.2.1 rtl8192cu](#rtl8192cu)
        *   [8.2.2 rtl8723ae/rtl8723be](#rtl8723ae/rtl8723be)
        *   [8.2.3 rtl88xxau](#rtl88xxau)
        *   [8.2.4 rtl8822bu](#rtl8822bu)
        *   [8.2.5 rtl8xxxu](#rtl8xxxu)
    *   [8.3 Atheros](#Atheros)
        *   [8.3.1 ath5k](#ath5k)
        *   [8.3.2 ath9k](#ath9k)
            *   [8.3.2.1 Economia de energia](#Economia_de_energia_2)
    *   [8.4 Intel](#Intel)
        *   [8.4.1 ipw2100 e ipw2200](#ipw2100_e_ipw2200)
        *   [8.4.2 iwlegacy](#iwlegacy)
        *   [8.4.3 iwlwifi](#iwlwifi)
            *   [8.4.3.1 Coexistência com Bluetooth](#Coexistência_com_Bluetooth)
            *   [8.4.3.2 Rastros de pilha de firmware](#Rastros_de_pilha_de_firmware)
        *   [8.4.4 Desabilitar piscada de LED](#Desabilitar_piscada_de_LED)
    *   [8.5 Broadcom](#Broadcom)
    *   [8.6 Outros drivers/dispositivos](#Outros_drivers/dispositivos)
        *   [8.6.1 Tenda w322u](#Tenda_w322u)
        *   [8.6.2 orinoco](#orinoco)
        *   [8.6.3 prism54](#prism54)
        *   [8.6.4 ACX100/111](#ACX100/111)
        *   [8.6.5 zd1211rw](#zd1211rw)
        *   [8.6.6 hostap_cs](#hostap_cs)
    *   [8.7 ndiswrapper](#ndiswrapper)
    *   [8.8 backports-patched](#backports-patched)
*   [9 Veja também](#Veja_também)

## Driver de dispositivo

O kernel padrão do Arch Linux é *modular*, o que significa que muitos dos drivers para hardware de máquina residem no disco rígido e estão disponíveis como [módulos](/index.php/Kernel_modules "Kernel modules"). Na inicialização, o [udev](/index.php/Udev "Udev") faz um inventário do seu hardware e carrega os módulos (drivers) apropriados para o hardware correspondente, o que, por sua vez, permite a criação de uma *interface* de rede.

Alguns chipsets sem fio também exigem firmware, além de um driver correspondente. Muitas imagens de firmware são fornecidas pelo pacote [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware), no entanto, as imagens de firmware proprietárias não são incluídas e devem ser instaladas separadamente. Isso é descrito em [#Instalar driver/firmware](#Instalar_driver/firmware).

**Nota:** Se o módulo apropriado não for carregado pelo udev na inicialização, basta [carregá-lo manualmente](/index.php/Kernel_modules#Manual_module_handling "Kernel modules"). Se o udev carrega mais de um driver para um dispositivo, o conflito resultante pode impedir a configuração seja bem-sucedida. Certifique-se de [colocar na lista negra](/index.php/Blacklist "Blacklist") o módulo indesejado.

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

Verifique também a saída do comando `ip link` para ver se uma interface sem fio foi criada; geralmente, a nomenclatura das [interfaces de rede](/index.php/Interfaces_de_rede "Interfaces de rede") sem fio começa com a letra "w", por ex. `wlan0` ou `wlp2s0`. Então, ative a interface com:

```
# ip link set *interface* up

```

Por exemplo, considerando que a interface seja `wlan0`, este seria `ip link set wlan0 up`.

Se você receber a mensagem de erro `SIOCSIFFLAGS: No such file or directory`, isso certamente significa que seu chipset sem fio requer um firmware para funcionar.

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

Se a sua placa sem fio estiver listada acima, siga a subseção desta página [#Solução de problemas de drivers e firmware](#Solução_de_problemas_de_drivers_e_firmware), que contém informações sobre a instalação de drivers e firmware de algumas placas sem fio específicas. Em seguida, [verifique o status do driver](#Verificar_o_status_de_driver) novamente.

Se sua placa sem fio não estiver listada acima, provavelmente só há suporte no Windows (algumas Broadcom, 3com etc). Para essas, você pode tentar usar o [#ndiswrapper](#ndiswrapper).

## Utilitários

Assim como outras interfaces de rede, as sem fio são controladas com *ip* do pacote [iproute2](https://www.archlinux.org/packages/?name=iproute2).

Gerenciar uma conexão sem fio requer um conjunto básico de ferramentas. Use um [gerenciador de rede](/index.php/Gerenciador_de_rede "Gerenciador de rede") ou use um dos seguintes diretamente:

| Software | Pacote | [WEXT](https://wireless.wiki.kernel.org/en/developers/documentation/wireless-extensions) | [nl80211](https://wireless.wiki.kernel.org/en/developers/documentation/nl80211) | WEP | WPA/WPA2 | [Archiso](/index.php/Archiso "Archiso") [[1]](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) |
| [wireless_tools](http://www.hpl.hp.com/personal/Jean_Tourrilhes/Linux/Tools.html) | [wireless_tools](https://www.archlinux.org/packages/?name=wireless_tools) | Sim | Não | Sim | Não | Sim |
| [iw](https://wireless.kernel.org/en/users/Documentation/iw) | [iw](https://www.archlinux.org/packages/?name=iw) | Não | Sim | Sim | Não | Sim |
| [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") | [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) | Sim | Sim | Sim | Sim | Sim |
| [iwd](/index.php/Iwd "Iwd") | [iwd](https://www.archlinux.org/packages/?name=iwd) | Não | Sim | Sim | Sim | Sim |

1.  Obsoleto.

Note que algumas placas só oferece suporte a WEXT.

### Comparação entre iw e wireless_tools

A tabela abaixo fornece uma visão geral dos comandos comparáveis para *iw* e *wireless_tools*. Veja [iw substitui o iwconfig](http://wireless.kernel.org/en/users/Documentation/iw/replace-iwconfig) para mais exemplos.

| comando *iw* | comando *wireless_tools* | Descrição |
| iw dev *wlan0* link | iwconfig *wlan0* | Obtendo status do link. |
| iw dev *wlan0* scan | iwlist *wlan0* scan | Buscando pontos de acesso disponíveis. |
| iw dev *wlan0* set type ibss | iwconfig *wlan0* mode ad-hoc | Definindo o modo de operação para *ad-hoc*. |
| iw dev *wlan0* connect *seu_essid* | iwconfig *wlan0* essid *seu_essid* | Conectando a rede aberta. |
| iw dev *wlan0* connect *seu_essid* 2432 | iwconfig *wlan0* essid *seu_essid* freq 2432M | Conectando a rede aberta especificando um canal. |
| iw dev *wlan0* connect *seu_essid* key 0:*sua_chave* | iwconfig *wlan0* essid *seu_essid* key *sua_chave* | Conectando a rede criptografada por WEP usando a chave hexadecimal. |
| iwconfig *wlan0* essid *seu_essid* key s:*sua_chave* | Connecting to WEP encrypted network using ASCII key. |
| iw dev *wlan0* set power_save on | iwconfig *wlan0* power on | Habilitando economia de energia. |

## iw

Assim como outras interfaces de rede, as sem fio são controladas com *ip* do pacote [iproute2](https://www.archlinux.org/packages/?name=iproute2).

Você precisará instalar um conjunto básico de ferramentas para gerenciar a conexão sem fio. [Instale](/index.php/Instale "Instale") um dos seguintes:

**Nota:** Para criptografia WPA/WPA2, *wpa_supplicant* é necessário.

*   **iw** — *iw* só oferece suporte ao padrão nl80211 (netlink), não havendo suporte ao padrão antigo WEXT (Wireless EXTentions). Se *iw* não vir sua placa, esse pode ser o motivo.

	[https://wireless.kernel.org/en/users/Documentation/iw](https://wireless.kernel.org/en/users/Documentation/iw) || [iw](https://www.archlinux.org/packages/?name=iw)

*   **wireless_tools** — *wireless_tools* está obsoleto, mas ainda é amplamente suportado. Use esse para módulos usando o padrão WEXT.

	[http://www.hpl.hp.com/personal/Jean_Tourrilhes/Linux/Tools.html](http://www.hpl.hp.com/personal/Jean_Tourrilhes/Linux/Tools.html) || [wireless_tools](https://www.archlinux.org/packages/?name=wireless_tools)

*   **[WPA supplicant](/index.php/WPA_supplicant "WPA supplicant")** — *wpa_supplicant* é um suplicante multiplataforma com suporte a WEP, WPA e WPA2 (IEEE 802.11i / RSN (Robust Secure Network)). Funciona com o WEXT e o nl80211.

	[http://hostap.epitest.fi/wpa_supplicant/](http://hostap.epitest.fi/wpa_supplicant/) || [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant)

**Dica:** Para uma comparação entre os comandos *iw* e *wireless_tools*, veja [#Comparação entre iw e wireless_tools](#Comparação_entre_iw_e_wireless_tools).

**Nota:**

*   Note que a maioria dos comandos devem ser executados com [permissões de root](/index.php/Usu%C3%A1rios_e_grupos "Usuários e grupos"). Se executados com permissões de usuário normal, alguns dos comandos (por exemplo, *iw list*) sairão sem erro, mas também não produzirão a saída correta, o que pode ser confuso.
*   Dependendo do seu hardware e tipo de criptografia, algumas dessas etapas podem não ser necessárias. Algumas placas são conhecidas por exigir a ativação da interface e/ou a verificação do ponto de acesso antes de serem associadas a um ponto de acesso e receberem um endereço IP. Algum teste pode ser necessário. Por exemplo, os usuários WPA/WPA2 podem tentar ativar diretamente sua rede sem fio a partir do passo [#Conectar a um ponto de acesso](#Conectar_a_um_ponto_de_acesso).

Exemplos nesta seção presume que sua interface de dispositivo sem fio é `*interface*` e que você está se conectando a ponto de acesso wifi `*seu_essid*`. Substitua ambos conforme o caso.

### Obter o nome da interface

**Dica:** Veja a [documentação oficial](http://wireless.kernel.org/en/users/Documentation/iw) da ferramenta *iw* para mais exemplos.

Para obter o nome de sua interface sem fio, faça:

```
$ iw dev

```

O nome da interface será exibida após a palavra "Interface". Por exemplo, ela normalmente é `wlan0`.

### Obter o status da interface

Para verificar o status dos links, use o comando a seguir:

```
$ iw dev *interface* link

```

Você pode obter informações estatísticas, tal como a quantidade de bytes tx/rx, força de sinal etc., com o comando a seguir:

```
$ iw dev *interface* station dump

```

### Ativar a interface

**Dica:** Geralmente, essa etapa não é necessária.

Algumas placas de rede exigem que a interface do kernel seja ativada antes que você possa usar *iw* ou *wireless_tools*:

```
# ip link set *interface* up

```

**Nota:** Se você obtiver erros como `RTNETLINK answers: Operation not possible due to RF-kill`, certifique-se que o botão de hardware esteja ligado. Veja [#Problemas com rfkill](#Problemas_com_rfkill) para detalhes.

Para conferir se a interface está ativa, inspecione a saída do comando a seguir:

 `$ ip link show *interface*` 
```
3: wlan0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state DOWN mode DORMANT group default qlen 1000
    link/ether 12:34:56:78:9a:bc brd ff:ff:ff:ff:ff:ff

```

O `UP` em `<BROADCAST,MULTICAST,UP,LOWER_UP>` é o que indica que a interface está ativa, e não o `state DOWN` em seguida.

### Descobrir pontos de acesso

Para ver quais pontos de acesso estão disponíveis, execute:

```
# iw dev *interface* scan | less

```

**Nota:** Se ele exibir `Interface does not support scanning`, você provavelmente se esqueceu de instalar o firmware. Em alguns casos, esta mensagem também é exibida quando não se está executando *iw* como root.

**Dica:** Dependendo da sua localização, talvez seja necessário definir o [domínio regulatório](#Respeitar_o_domínio_regulatório) correto para ver todas as redes disponíveis.

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

### Definir o modo de operação

Pode ser necessário definir o modo de operação adequado da placa sem fio. Mais especificamente, se você for conectar uma [rede ad-hoc](/index.php/Ad-hoc_networking "Ad-hoc networking"), você precisa definir o modo de operação para `ibss`:

```
# iw dev *interface* set type ibss

```

**Nota:** A mudança do modo de operação em algumas placas pode exibir que a interface sem fio esteja *desativada* (`ip link set *interface* down`).

### Conectar a um ponto de acesso

Dependendo da criptografia, você precisa associar seu dispositivo sem fio ao ponto de acesso para usar e transmitir a chave de criptografia:

*   **Nenhuma criptografia** `# iw dev *interface* connect "*seu_essid*"` 
*   **WEP**
    *   usando uma chave hexadecimal ou ASCII (o formato é diferenciado automaticamente porque uma chave WEP tem um tamanho fixo): `# iw dev *interface* connect "*seu_essid*" key 0:*sua_chave*` 
    *   usando uma chave hexadecimal ou ASCII, especificando a terceira chave de configuração como padrão (as chaves são contadas a partir de zero, quatro são possíveis): `# iw dev *interface* connect "*sua_essid*" key d:2:*sua_chave*` 

Independentemente do método usado, você pode verificar se você conseguiu se associar com sucesso:

```
# iw dev *interface* link

```

## Wi-Fi Protected Access

### WPA2 Pessoal

WPA2 Pessoal, ou WPA2-PSK, é um modo de [Wi-Fi Protected Access](https://en.wikipedia.org/wiki/pt:Wi-Fi_Protected_Access "wikipedia:pt:Wi-Fi Protected Access").

Você pode autenticar em redes WPA2 Pessoal usando [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") ou [iwd](/index.php/Iwd "Iwd"), ou conectar usando um [gerenciador de rede](/index.php/Gerenciador_de_rede "Gerenciador de rede"). Se você autenticou apenas na rede, para ter uma conexão totalmente funcional, você ainda precisará atribuir o(s) endereço(s) IP e rotas ou [manualmente](/index.php/Configura%C3%A7%C3%A3o_de_rede#Endereço_IP_estático "Configuração de rede") ou usando um [DHCP](/index.php/DHCP_(Portugu%C3%AAs) "DHCP (Português)") cliente.

### WPA2 Empresarial

Do inglês *WPA2 Enterprise*, é um modo de [Wi-Fi Protected Access](https://en.wikipedia.org/wiki/pt:Wi-Fi_Protected_Access "wikipedia:pt:Wi-Fi Protected Access"). Ele oferece melhor segurança e gerenciamento de chaves do que o *WPA2 Pessoal* *(WPA2 Personal)* e suporta outras funcionalidades do tipo corporativo, como VLANs e [NAP](https://en.wikipedia.org/wiki/pt:Prote%C3%A7%C3%A3o_de_Acesso_%C3%A0_Rede "wikipedia:pt:Proteção de Acesso à Rede"). No entanto, é necessário um servidor de autenticação externo, chamado servidor [RADIUS](https://en.wikipedia.org/wiki/pt:RADIUS "wikipedia:pt:RADIUS") para lidar com a autenticação de usuários. Isso está em contraste com o modo Pessoal, que não exige nada além do roteador sem fio ou pontos de acesso (APs) e usa uma única senha ou senha para todos os usuários.

O modo Empresarial permite que os usuários façam logon na rede Wi-Fi com um nome de usuário e senha e/ou um certificado digital. Como cada usuário tem uma chave de criptografia única e dinâmica, ele também ajuda a evitar a espionagem usuário a usuário na rede sem fio e melhora a força da criptografia.

Esta seção descreve a configuração da [clientes de rede](/index.php/List_of_applications#Network_managers "List of applications") para se conectar a um ponto de acesso sem fio com o modo WPA2 Empresarial. Consulte [Software access point#RADIUS](/index.php/Software_access_point#RADIUS "Software access point") para obter informações sobre como configurar um próprio ponto de acesso.

**Nota:** O modo Empresarial requer uma configuração de cliente mais complexa, enquanto o modo Pessoal requer apenas a inserção de uma senha quando solicitado. É provável que os clientes precisem instalar o certificado de AC do servidor (mais certificados por usuário se usar EAP-TLS) e, em seguida, configurar manualmente a segurança sem fio e as configurações de autenticação 802.1X.

Para uma comparação de protocolos, veja a seguinte [tabela](http://deployingradius.com/documents/protocols/compatibility.html).

**Atenção:** É possível usar o WPA2 Empresarial sem que o cliente verifique o certificado de AC do servidor. No entanto, você deve sempre procurar fazê-lo, porque sem autenticar o ponto de acesso, a conexão pode estar sujeita a um ataque *man-in-the-middle*. Isso pode acontecer porque, embora o handshake de conexão em si possa ser criptografado, as configurações mais usadas transmitem a própria senha em texto simples ou no modo facilmente quebrável [#MS-CHAPv2](#MS-CHAPv2). Portanto, o cliente pode enviar a senha para um ponto de acesso mal-intencionado que, então, faz o proxy da conexão.

#### eduroam

[Eduroam](https://en.wikipedia.org/wiki/pt:eduroam "wikipedia:pt:eduroam") (acrônimo em inglês para *education roaming*) é uma rede de serviços internacional de roaming para os usuários em pesquisa no ensino superior e cursos subsequentes, baseado em WPA2 Empresarial.

**Nota:**

*   Verifique os detalhes da conexão **primeiro** com sua instituição antes de aplicar os perfis listados nesta seção. Não é garantido que os perfis de exemplo funcionem ou correspondam a quaisquer requisitos de segurança.
*   Ao armazenar os perfis de conexão não criptografados, recomenda-se restringir o acesso de leitura à conta root, especificando `chmod 600 *perfil*` como root.

**Dica:** A configuração para o [NetworkManager](/index.php/NetworkManager_(Portugu%C3%AAs) "NetworkManager (Português)") e [#wpa_supplicant](#wpa_supplicant) podem ser geradas com a [ferramenta assistente de configuração (CAT) do eduroam](https://cat.eduroam.org/) .

#### Configuração manual/automática

*   [Suplicante de WPA](/index.php/WPA_supplicant#Advanced_usage "WPA supplicant") pode ser configurado diretamente por meio de seu arquivo de configuração ou usando seus frontends CLI/GUI e usado em combinação com um cliente DHCP. Veja os exemplos em `/usr/share/doc/wpa_supplicant/wpa_supplicant.conf` para configurar os detalhes de conexão.
*   [NetworkManager](/index.php/NetworkManager_(Portugu%C3%AAs) "NetworkManager (Português)") pode gerar perfis de WPA2 Empresarial com [frontends gráficos](/index.php/NetworkManager_(Portugu%C3%AAs)#Front-ends "NetworkManager (Português)"). *nmcli* e *nmtui* não oferecem suporte a isso, mas podem usar perfis existentes.
*   [ConnMan](/index.php/ConnMan "ConnMan") precisa de um arquivo de configuração separado antes de [se conectar](/index.php/ConnMan#Wi-Fi "ConnMan") à rede. Veja [connman-service.config(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/connman-service.config.5) e [Connman#Connecting to eduroam](/index.php/ConnMan#Connecting_to_eduroam_.28802.1X.29 "ConnMan") para detalhes.
*   [netctl](/index.php/Netctl "Netctl") possui suporte a configuração de [#wpa_supplicant](#wpa_supplicant) por meio de blocos inclusos com `WPAConfigSection=`. Veja [netctl.profile(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/netctl.profile.5) para detalhes.
*   **Atenção:** Regras de uso especial de aspas se aplicam: veja a seção `*SPECIAL QUOTING RULES*` em [netctl.profile(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/netctl.profile.5).

*   **Dica:** Certificados personalizados podem ser especificados adicionando a linha `'ca_cert="/caminho/para/o/ceritficado.cer"'` em `WPAConfigSection`.

#### Solução de problemas

##### MS-CHAPv2

As redes sem fio WPA2 Empresarial que exigem autenticação tipo 2 de MSCHAPv2 com PEAP às vezes exigem [pptpclient](https://www.archlinux.org/packages/?name=pptpclient), além do pacote [ppp](https://www.archlinux.org/packages/?name=ppp). [netctl](/index.php/Netctl "Netctl") parece funcionar facilmente sem ppp-mppe, no entanto. Em ambos os casos, o uso de MSCHAPv2 é desencorajado, pois é altamente vulnerável, embora o uso de outro método geralmente não seja uma opção.

## Dicas e truques

### Respeitar o domínio regulatório

O [domínio regulatório](https://en.wikipedia.org/wiki/IEEE_802.11#Regulatory_domains_and_legal_compliance "wikipedia:IEEE 802.11"), conhecidos como *"regdomain"*, é usado para reconfigurar os drivers sem fio para garantir que o uso de tal hardware esteja em conformidade com as leis locais estabelecidas pela FCC, ETSI e outras organizações. Os *regdomain* usam [códigos de país ISO 3166-1 alfa-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2 "wikipedia:ISO 3166-1 alpha-2"). Por exemplo, o *regdomain* dos Estados Unidos seria "US", a China seria "CN", do Brasil seria "BR", etc.

Os *regdomains* afetam a disponibilidade de canais sem fio. Na banda de 2,4 GHz, os canais permitidos são 1-11 para os EUA, 1-14 para o Japão e 1-13 para a maior parte do resto do mundo. Na banda de 5GHz, as regras para os canais permitidos são muito mais complexas. Em ambos os casos, consulte [esta lista de canais WLAN](https://en.wikipedia.org/wiki/List_of_WLAN_channels "wikipedia:List of WLAN channels") para obter informações mais detalhadas.

Os *regdomains* também afetam o limite da [Potência Isotrópica Radiada Equivalente (EIRP)](https://en.wikipedia.org/wiki/Equivalent_isotropically_radiated_power "wikipedia:Equivalent isotropically radiated power") (do inglês, *Effective Isotropic Radiated Power*) de dispositivos sem fio. Isso é derivado da potência de transmissão/"tx power" e é medido em [dBm/mBm (1dBm=100mBm) ou mW (escala de log)](https://en.wikipedia.org/wiki/pt:DBm "wikipedia:pt:DBm"). Na faixa de 2,4 GHz, o máximo é 30dBm nos EUA e Canadá, 20dBm na maior parte da Europa e 20dB-30dBm no resto do mundo. Na banda de 5GHz, os máximos são geralmente mais baixos. Consulte o [wireless-regdb](http://git.kernel.org/cgit/linux/kernel/git/linville/wireless-regdb.git/tree/db.txt) para informações mais detalhadas (os valores dBm de EIRP estão no segundo conjunto de colchetes para cada linha).

A configuração incorreta do *regdomain* pode ser útil - por exemplo, permitindo o uso de um canal não utilizado quando outros canais estão lotados ou permitindo um aumento na potência de transmissão para ampliar o alcance do transmissor. No entanto, **isso não é recomendado**, pois poderia violar as leis locais e causar interferência em outros dispositivos de rádio.

Para configurar o *regdomain*, instale [crda](https://www.archlinux.org/packages/?name=crda) e reinicialize (para recarregar o módulo `cfg80211` e todos os drivers relacionados). Verifique o log de inicialização para certificar-se de que o CRDA esteja sendo chamado por `cfg80211`:

```
$ dmesg | grep cfg80211

```

O *regdomain* atual pode ser configurar para os Estados Unidos com:

```
# iw reg set US

```

E consultado com:

```
$ iw reg get

```

**Nota:** Seu dispositivo pode ser configurado com país "00", que é o "world regulatory domain" (domínio regulatório mundial) e contém configurações genéricas. Se isso não puder ser desconfigurado, CRDA pode ser malconfigurado.

No entanto, a configuração do *regdomain* não pode alterar suas configurações. Alguns dispositivos têm um *regdomain* definido em firmware/EEPROM, que dita os limites do dispositivo, o que significa que a configuração de *regdomain* em software [só pode aumentar as restrições](http://wiki.openwrt.org/doc/howto/wireless.utilities#iw) , não diminui-las. Por exemplo, um dispositivo CN pode ser definido no software para o *regdomain* dos EUA, mas como o CN tem um máximo EIRP de 20dBm, o dispositivo não poderá transmitir no máximo dos EUA de 30dBm.

Por exemplo, para ver se o *regdomain* está sendo configurado no firmware para um dispositivo Atheros:

```
$ dmesg | grep ath:

```

Para outros chipsets, pode ser útil pesquisar por "EEPROM", "regdomain" ou simplesmente o nome do driver de dispositivo.

Para ver se sua alteração de *regdomain* foi realizada com sucesso, e consultar o número de canais disponíveis e sua potência permitida de transmissão:

```
$ iw list | grep -A 15 Frequencies:

```

Uma configuração mais permanente do *regdomain* pode ser obtida através da edição `/etc/conf.d/wireless-regdom` e descomentando o domínio apropriado.

Uma [suplicante WPA](/index.php/WPA_supplicant "WPA supplicant") também pode usar um *regdomain* na linha `country=` de `/etc/wpa_supplicant/wpa_supplicant.conf`.

Também é possível configurar o módulo do kernel [cfg80211](http://wireless.kernel.org/en/developers/Documentation/cfg80211) para usar um *regdomain* específico adicionando, por exemplo, `options cfg80211 ieee80211_regdom=EU` como [opções do módulo](/index.php/Kernel_modules#Setting_module_options "Kernel modules"). No entanto, isso faz parte da [antiga implementação regulamentar](http://wireless.kernel.org/en/developers/Regulatory#The_ieee80211_regdom_module_parameter).

Para mais informações, leia a [documentação regulatória no wireless.kernel.org](http://wireless.kernel.org/en/developers/Regulatory/).

### Problemas com rfkill

Muitos laptops têm um botão de hardware (ou interruptor) para desligar a placa wireless, no entanto, a placa também pode ser bloqueada pelo kernel. Isso pode ser tratado por *rfkill*. Para mostrar o status atual:

 `# rfkill list` 
```
0: phy0: Wireless LAN
	Soft blocked: yes
	Hard blocked: yes

```

Se a placa estiver com *hard blocked* ligado, use o botão de hardware (interruptor) para desligá-la. Se a placa estiver com *hard blocked* desligado e *soft blocked* ligado, use o seguinte comando:

```
# rfkill unblock wifi

```

**Nota:** É possível que a placa passe o estado de *hard blocked* ligado e *soft blocked* desligado para *hard blocked* desligado e *soft blocked* ligado, pressionando o botão de hardware (ou seja, o bit *soft blocked* está apenas ligado, independentemente). Isso pode ser modificado ajustando algumas opções do [módulo do kernel](/index.php/Kernel_module "Kernel module") `rfkill`.

Os botões de hardware para ligar ou desligar placas de rede sem fio são tratadas por um [módulo de kernel](/index.php/Kernel_module "Kernel module") específico do fornecedor, frequentemente estes são módulos [WMI](https://lwn.net/Articles/391230/). Particularmente para modelos de hardware muito novos, acontece que o modelo ainda não é totalmente suportado no kernel estável mais recente. Neste caso, muitas vezes, ajuda a procurar informações sobre o rastreador de bugs do kernel e relatar o modelo ao mantenedor do módulo do respectivo kernel do fornecedor, caso isso ainda não tenha ocorrido.

Veja também [[2]](http://askubuntu.com/questions/62166/siocsifflags-operation-not-possible-due-to-rf-kill).

## Economia de energia

Veja [Power saving#Network interface](/index.php/Power_saving#Network_interface "Power saving").

## Solução de problemas

Essa seção contém dicas de solução de problemas gerais, e não estritamente relacionados com problemas de drivers ou firmwares. Para tais tópicos, veja a próxima seção [#Solução de problemas de drivers e firmware](#Solução_de_problemas_de_drivers_e_firmware).

### Acesso temporário à internet

Se você tem hardware problemático e precisa de acesso à Internet para, por exemplo, baixar algum software ou obter ajuda em fóruns, você pode usar o recurso interno do Android para compartilhamento de internet via cabo USB. Consulte [Android tethering#USB tethering](/index.php/Android_tethering#USB_tethering "Android tethering") para mais informações.

### Observando os logs

Uma boa primeira medida para solucionar problemas é analisar primeiro os arquivos de registro do sistema. Para não analisar manualmente todos eles, pode ajudar a abrir uma segunda janela do terminal/console e observar as mensagens dos kernels com

```
$ dmesg -w

```

ao realizar a ação, p. ex. a tentativa de associação sem fio.

Ao usar uma ferramenta para gerenciamento de rede, o mesmo pode ser feito para systemd com

```
# journalctl -f 

```

Frequentemente, um erro de conexão sem fio é acompanhado por uma desautenticação com um código de motivo particular, por exemplo:

```
wlan0: deauthenticating from XX:XX:XX:XX:XX:XX by local choice (reason=3)

```

Consultar [o código de motivo](http://www.aboutcher.co.uk/2012/07/linux-wifi-deauthenticated-reason-codes/) pode dar uma primeira dica. Talvez também ajude você a olhar para a mensagem de controle [flowchart](https://wireless.wiki.kernel.org/en/developers/documentation/mac80211/auth-assoc-deauth), as mensagens do diário a seguirão.

As ferramentas individuais usadas neste artigo fornecem opções para uma saída de depuração mais detalhada, que pode ser usada em uma segunda etapa da análise, se necessário.

### Falha ao obter endereço IP

*   Se a obtenção de um endereço IP falhar repetidamente usando o cliente padrão [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd), tente instalar e usar [dhclient](https://www.archlinux.org/packages/?name=dhclient). Não se esqueça de selecionar *dhclient* como o cliente DHCP principal no [gerenciador de conexões](#Configuração_manual/automática).

*   Se você puder obter um endereço IP para uma interface com fio e não para uma interface sem fio, tente desabilitar o recurso [economia de energia](#Economia_de_energia) da placa de rede sem fio (especifique `off` em vez de `on`).

*   Se você receber um erro de tempo limite devido a um problema de *waiting for carrier*, talvez seja necessário definir o modo de canal como `auto` para o dispositivo específico:

```
# iwconfig wlan0 channel auto

```

Antes de mudar o canal para automático, verifique se sua interface sem fio está desativada. Depois de ter mudado com sucesso, você pode trazer a interface novamente e continuar a partir daí.

### Endereço IP válido, mas não consegue resolver host

Se você estiver em uma rede sem fio pública que possa ter um [portal cativo](https://en.wikipedia.org/wiki/pt:Captive_portal "wikipedia:pt:Captive portal"), certifique-se de consultar uma página HTTP (não uma página HTTPS) do seu navegador, pois alguns portais cativos só redirecionam HTTP.

Se esse não for o problema, [verifique se você consegue resolver nomes de domínio](/index.php/Verifique_se_voc%C3%AA_consegue_resolver_nomes_de_dom%C3%ADnio "Verifique se você consegue resolver nomes de domínio"), pode ser necessário usar o servidor DNS anunciado via DHCP.

### Definindo limites de RTS e de fragmentação

O hardware sem fio desativa o RTS e a fragmentação por padrão. Estes são dois métodos diferentes de aumentar o rendimento à custa da largura de banda (ou seja, confiabilidade à custa da velocidade). Eles são úteis em ambientes com ruído sem fio ou com muitos pontos de acesso adjacentes, o que pode criar interferência, levando a tempos limites ou a falhas de conexão.

A fragmentação de pacotes melhora o rendimento dividindo pacotes com tamanho excedendo o limite de fragmentação. O valor máximo (2346) efetivamente desativa a fragmentação, pois nenhum pacote pode excedê-lo. O valor mínimo (256) maximiza o rendimento, mas pode acarretar um custo significativo de largura de banda.

```
# iw phy0 set frag 512

```

[RTS](https://en.wikipedia.org/wiki/IEEE_802.11_RTS/CTS "wikipedia:IEEE 802.11 RTS/CTS") melhora o rendimento executando um *handshake* com o ponto de acesso antes de transmitir pacotes com tamanho excedendo o limite de RTS. O limite máximo (2347) efetivamente desativa o RTS, já que nenhum pacote pode excedê-lo. O limite mínimo (0) habilita o RTS para todos os pacotes, o que provavelmente é excessivo para a maioria das situações.

```
# iw phy0 set rts 500

```

**Nota:** `phy0` é o nome do dispositivo sem fio conforme listado por `$ iw phy`.

### Desconexões aleatórias

#### Causa nº.1

Se o dmesg disser `wlan0: deauthenticating from MAC by local choice (reason=3)` e você perder sua conexão Wi-Fi, é provável que você tenha uma economia de energia um pouco agressiva demais na sua placa Wi-Fi. Tente desabilitar os recursos [economia de energia](#Economia_de_energia) do placa sem fio (especifique `off` em vez de `on`).

Se a sua placa não oferece suporte a ativar/desativar o modo de economia de energia, verifique o BIOS para obter opções de gerenciamento de energia. Desativar o gerenciamento de energia PCI-Express no BIOS de um Lenovo W520 resolveu esse problema.

#### Causa nº.2

Se você está experimentando desconexões frequentes e o dmesg mostra mensagens como

`ieee80211 phy0: wlan0: No probe response from AP xx:xx:xx:xx:xx:xx after 500ms, disconnecting`

Tente mudar a largura de banda do canal para `20MHz` através da página de configurações do seu roteador.

#### Causa nº.3

Em alguns modelos de notebooks com switches de hardware (por exemplo, Thinkpad X200 series), devido ao desgaste ou design ruim, o switch (ou sua conexão com a placa-mãe) pode se soltar com o tempo, resultando em *hardblocks*/desconexões aparentemente aleatórias quando você acidentalmente toca o mudar ou mover o laptop. Não há solução de software para isso, a menos que seu switch seja elétrico e o BIOS ofereça a opção de desabilitar o interruptor. Se o seu interruptor for mecânico (a maioria é), existem muitas soluções possíveis, a maioria das quais visa desabilitar o interruptor: Soldando o ponto de contato na placa-mãe/placa wifi, colando ou bloqueando a chave, usando uma porca para apertar o interruptor ou removê-lo completamente.

#### Causa nº.4

Outro motivo para desconexões frequentes ou falha total na conexão também pode ser um roteador abaixo do padrão, configurações incompletas do roteador ou interferência de outros dispositivos sem fio.

Para solucionar problemas, primeiro tente conectar-se ao roteador sem autenticação.

Se isso funcionar, ative o WPA/WPA2 novamente, mas escolha configurações de roteador fixas e/ou limitadas. Por exemplo:

*   Se o roteador for consideravelmente antigo que o dispositivo sem fio que você usa para o cliente, teste se ele funciona com a configuração do roteador para um modo sem fio
*   Desative autenticação de modo misto (por exemplo, somente WPA2 com AES ou TKIP se o roteador for antigo)
*   Tente um canal fixo/livre em vez de um canal "auto" (talvez o roteador do vizinho seja antigo e interfira)
*   Desabilite [WPS](https://en.wikipedia.org/wiki/pt:Wi-Fi_Protected_Setup "wikipedia:pt:Wi-Fi Protected Setup")
*   Desabilite largura de banda do canal `40MHz` (menor rendimento, mas colisões menos prováveis)
*   Se o roteador tiver configurações de qualidade de serviço (QoS), verifique a integridade das configurações (por exemplo, o Wi-Fi Multimedia (WMM) faz parte do controle de fluxo QoS opcional. Um firmware incorreto do roteador pode anunciar sua existência, embora a configuração não esteja ativada)

### Redes Wi-Fi invisíveis por causa do domínio regulatório incorreto

Se os canais Wi-Fi do computador não corresponderem aos do país do usuário, isso poderá resultar na invisibilidade de algumas redes Wi-Fi no intervalo, porque eles usam canais sem fio que não são permitidos por padrão. A solução é configurar o domínio regulatório corretamente, consulte [#Respeitar o domínio regulatório](#Respeitar_o_domínio_regulatório).

## Solução de problemas de drivers e firmware

Esta seção cobre métodos e procedimentos para instalar módulos do kernel e *firmware* para chipsets específicos, que diferem do método genérico.

Veja [Módulos de kernel](/index.php/Kernel_modules "Kernel modules") para informações gerais sobre operações com módulos.

### Ralink/Mediatek

#### rt2x00

Driver unificado para chipsets Ralink (ele substitui `rt2500`, `rt61`, `rt73`, etc). Este driver está no kernel Linux desde o 2.6.24, você só precisa carregar o módulo correto para o chip: `rt2400pci`, `rt2500pci`, `rt2500usb`, `rt61pci` ou `rt73usb` que carregará automaticamente os respectivos módulos `rt2x00` também.

Uma lista de dispositivos suportados pelos módulos está disponível no [site](https://web.archive.org/web/20150507023412/http://rt2x00.serialmonkey.com/wiki/index.php/Hardware) do projeto.

	Notas adicionais

*   Desde o kernel 3.0, rt2x00 também inclui esses drivers: `rt2800pci`, `rt2800usb`.
*   Desde o kernel 3.0, os drivers *staging* `rt2860sta` e `rt2870sta` foram substituídos pelos drivers *mainline* `rt2800pci` e `rt2800usb`.
*   Alguns dispositivos tem uma ampla gama de opções que pode ser configurada com `iwpriv`. Esses estão documentados nos [tarballs fonte](http://web.ralinktech.com/ralink/Home/Support/Linux.html) disponíveis na Ralink.

#### rt3090

Para dispositivos que estão usando o chipset rt3090, deve ser possível usar o driver `rt2800pci`, no entanto, ele não está funcionando com este chipset muito bem (por exemplo, às vezes não é possível usar uma taxa maior que 2Mb/s).

#### rt3290

O chipset rt3290 é reconhecido pelo módulo do kernel `rt2800pci`. No entanto, alguns usuários enfrentam problemas e reverter para um driver Ralink corrigido parece ser benéfico nesses [casos](https://bbs.archlinux.org/viewtopic.php?id=161952).

#### rt3573

Novo chipset a partir de 2012\. Pode exigir drivers proprietários da Ralink. Diferentes fabricantes o utilizam, consulte o tópico de fóruns [Adaptador USB sem fio Belkin N750 DB](https://bbs.archlinux.org/viewtopic.php?pid=1164228#p1164228).

#### rt5572

Novo chipset a partir de 2012 com suporte para bandas de 5 Ghz. Pode exigir drivers proprietários da Ralink e algum esforço para compilá-los. No momento da escrita, um tutorial sobre a compilação está disponível para uma versão DLINK DWA-160\. B2 [aqui](http://bernaerts.dyndns.org/linux/229-ubuntu-precise-dlink-dwa160-revb2).

#### mt7612u

Novo chipset a partir de 2014, lançado sob o novo nome comercial Mediatek. É um chipset AC1200 ou AC1300\. O fabricante fornece drivers para o Linux em sua [página de suporte](https://www.mediatek.com/products/broadbandWifi/mt7612u).

### Realtek

Veja [[4]](https://wikidevi.com/wiki/Realtek) para uma lista de chipsets Realtek e especificações.

#### rtl8192cu

O driver agora está no kernel, mas muitos usuários relataram não conseguir estabelecer uma conexão, embora a verificação de redes funcione.

[8192cu-dkms](https://aur.archlinux.org/packages/8192cu-dkms/) inclui muitos patches, tente isso se não funcionar bem com o driver no kernel.

#### rtl8723ae/rtl8723be

Os módulos `rtl8723ae` e `rtl8723be` estão incluídos no kernel Linux padrão.

Alguns usuários podem encontrar erros com economia de energia neste cartão. Isso é mostrado com desconexões ocasionais que não são reconhecidas pelos gerenciadores de rede de alto nível ([netctl](/index.php/Netctl "Netctl"), [NetworkManager](/index.php/NetworkManager_(Portugu%C3%AAs) "NetworkManager (Português)")). Este erro pode ser confirmado executando `dmesg -w` ou `journalctl -f` e procurando resultados relacionados a economia de energia e ao módulo `rtl8723ae`/`rtl8723be`. Se você está tendo este problema, use a opção de kernel `fwlps=0`, que deve impedir que a placa WiFi entre automaticamente e pare a conexão.

 `/etc/modprobe.d/rtl8723ae.conf`  `options rtl8723ae fwlps=0` 

ou

 `/etc/modprobe.d/rtl8723be.conf`  `options rtl8723be fwlps=0` 

Se você tiver um sinal fraco, talvez seu dispositivo tenha apenas uma antena física conectada e a seleção automática da antena esteja interrompida. Você pode forçar a escolha da antena com a opção do kernel `ant_sel=1` ou `ant_sel=2`. [[5]](https://bbs.archlinux.org/viewtopic.php?id=208472)

#### rtl88xxau

Chipsets rtl8811au/rtl8812au/rtl8814au/rtl8821au da Realtek projetados para vários adaptadores USB, de AC600 a AC1900.

Vários pacotes fornecem diversos drivers de kernel:

| Chipset | Versão de driver | Pacote | Notas |
| rtl8811au, rtl8812au, rtl8814au and rtl8821au | 5.6.4.1 | [rtl88xxau-aircrack-dkms-git](https://aur.archlinux.org/packages/rtl88xxau-aircrack-dkms-git/) | Módulo de kernel Aircrack-ng para chipsets 8811au, 8812au, 8814au e 8821au com modo monitor e suporte a injeção. |
| rtl8812au | 5.2.20 | [rtl8812au-dkms-git](https://aur.archlinux.org/packages/rtl8812au-dkms-git/) | A versão mais recente do driver oficial da Realtek para rtl8812au *somente*. |
| rtl8811au, rtl8812au e rtl8821au | 5.1.5 | [rtl8821au-dkms-git](https://aur.archlinux.org/packages/rtl8821au-dkms-git/) | Para rtl8812au, as versões 5.6.4.1 e 5.2.20 são recomendadas. |
| rtl8814au | 4.3.21 | [rtl8814au-dkms-git](https://aur.archlinux.org/packages/rtl8814au-dkms-git/) | Possivelmente funciona para rtl8813au também. Reportado como tendo melhor desempenho que [rtl88xxau-aircrack-dkms-git](https://aur.archlinux.org/packages/rtl88xxau-aircrack-dkms-git/) |

Esses exibem [DKMS](/index.php/DKMS "DKMS"), então certifique-se que você tenha os cabeçalhos apropriados para seu kernel instalados.

#### rtl8822bu

[rtl8822bu-dkms-git](https://aur.archlinux.org/packages/rtl8822bu-dkms-git/) fornece um módulo de kernel para o chipset Realtek 8822bu encontrado no adaptador Edimax EW7822ULC USB3 e Asus AC53 Nano USB 802.11ac.

Ele exige [DKMS](/index.php/DKMS "DKMS"), então certifique-se que você tenha os cabeçalhos apropriados para seu kernel instalados.

#### rtl8xxxu

Os problemas com o módulo de kernel da linha principal `rtl8xxxu` podem ser resolvidos pela compilação de um módulo de terceiros para o chipset específico. O código-fonte pode ser encontrado em [repositórios GitHub](https://github.com/lwfinger?tab=repositories).

Alguns drivers podem estar preparados no AUR como, por exemplo, [rtl8723bu-git](https://aur.archlinux.org/packages/rtl8723bu-git/) e [rtl8723bu-git-dkms](https://aur.archlinux.org/packages/rtl8723bu-git-dkms/).

### Atheros

A [equipe MadWifi](http://madwifi-project.org/) atualmente mantém três drivers diferentes para dispositivos com chipset Atheros:

*   `madwifi` é um driver antigo e obsoleto, não presente no Arch kernel desde 2.6.39.1.
*   `ath5k` é um driver mais novo, que substitui o driver `madwifi`. Atualmente uma escolha melhor para alguns chipsets, mas nem todos os chipsets têm suporte (veja abaixo)
*   `ath9k` é o mais novo desses três e é destinado a chipsets Atheros mais novos. Há suporte a todos os chips com capacidades 802.11n.

Há alguns outros drivers para alguns dispositivos Atheros. Veja a [documentação Linux Wireless](http://wireless.kernel.org/en/users/Drivers/Atheros#PCI_.2F_PCI-E_.2F_AHB_Drivers) para detalhes.

#### ath5k

Recursos externos:

*   [http://wireless.kernel.org/en/users/Drivers/ath5k](http://wireless.kernel.org/en/users/Drivers/ath5k)
*   [http://wiki.debian.org/ath5k](http://wiki.debian.org/ath5k)

Se você encontrar páginas da Web sendo carregadas aleatoriamente muito lentamente ou se o dispositivo não puder conceder um endereço IP, tente alternar de criptografia de hardware para software carregando o módulo `ath5k` com `nohwcrypt=1` opção. Veja [Kernel modules#Setting module options](/index.php/Kernel_modules#Setting_module_options "Kernel modules") para detalhes.

Alguns laptops podem ter problemas com o indicador LED sem fio piscando em vermelho e azul. Para resolver esse problema, faça:

```
# echo none > /sys/class/leds/ath5k-phy0::tx/trigger
# echo none > /sys/class/leds/ath5k-phy0::rx/trigger

```

Para alternativas, veja [esse relatório de erro](https://bugzilla.redhat.com/show_bug.cgi?id=618232).

#### ath9k

Recursos externos:

*   [http://wireless.kernel.org/en/users/Drivers/ath9k](http://wireless.kernel.org/en/users/Drivers/ath9k)
*   [http://wiki.debian.org/ath9k](http://wiki.debian.org/ath9k)

A partir do Linux 3.15.1, alguns usuários experimentaram uma diminuição na largura de banda. Em alguns casos isso pode ser corrigido editando `/etc/modprobe.d/ath9k.conf` e adicionando a linha:

```
options ath9k nohwcrypt=1

```

**Nota:** Verifique com o comando *lsmod* qual o (nome do) módulo está em uso e altere-o se nomeado de outra forma (por exemplo, ath9k_htc).

No caso improvável de você ter problemas de estabilidade que o incomodem, você pode tentar usar o pacote [backports-patched](https://aur.archlinux.org/packages/backports-patched/). Existe uma [lista de discussão](https://lists.ath9k.org/mailman/listinfo/ath9k-devel) para discussões relacionadas a suporte e desenvolvimento.

##### Economia de energia

Embora o [Linux Wireless](http://wireless.kernel.org/en/users/Documentation/dynamic-power-save) diga que a economia de energia dinâmica está habilitada para chips Atheros ath9k mais recentes que AR9280, para alguns dispositivos (por exemplo, AR9285) o [powertop](https://www.archlinux.org/packages/?name=powertop) ainda pode relatar que a economia de energia está desativada. Nesse caso, habilite-a manualmente.

Em alguns dispositivos (por exemplo, AR9285), habilitar economia de energia pode resultar no seguinte erro:

 `# iw dev wlan0 set power_save on` 
```
command failed: Operation not supported (-95)

```

A solução é definir a opção `ps_enable=1` para o módulo `ath9k`:

 `/etc/modprobe.d/ath9k.conf`  `options ath9k ps_enable=1` 

### Intel

#### ipw2100 e ipw2200

Esses módulos são totalmente suportados no kernel, mas requerem firmware adicional. Dependendo de qual dos chipsets você tem, [instale](/index.php/Instale "Instale") [ipw2100-fw](https://www.archlinux.org/packages/?name=ipw2100-fw) ou [ipw2200-fw](https://www.archlinux.org/packages/?name=ipw2200-fw). Então [recarregue](/index.php/Kernel_modules#Manual_module_handling "Kernel modules") o módulo apropriado.

**Dica:** Você pode usar as seguintes [opções de módulo](/index.php/Kernel_modules#Setting_module_options "Kernel modules"):

*   use a opção `rtap_iface=1` habilitar a interface radiotap
*   use a opção `led=1` para habilitar um LED frontal indicando quando a rede sem-fio está conectada ou não

#### iwlegacy

O [iwlegacy](http://wireless.kernel.org/en/users/Drivers/iwlegacy) é o driver sem fio para os chips sem fio 3945 e 4965 da Intel. O firmware está incluído no pacote [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware).

[udev](/index.php/Udev "Udev") deve carregar automaticamente o driver, do contrário carregue `iwl3945` ou `iwl4965` manualmente. Veja [Módulos de kernel](/index.php/Kernel_modules "Kernel modules") para detalhes.

Se você tiver problemas para se conectar a redes em geral, falhas aleatórias com seu cartão na inicialização ou a qualidade do seu link é muito fraca, tente desabilitar o 802.11n:

 `/etc/modprobe.d/iwl4965.conf`  `options iwl4965 11n_disable=1` 

Se as falhas persistirem durante a inicialização e você estiver usando o driver Nouveau, tente [ativar o KMS antigo](/index.php/Nouveau#Enable_early_KMS "Nouveau") para evitar o conflito [[7]](https://bbs.archlinux.org/viewtopic.php?pid=1748667#p1748667).

#### iwlwifi

O [iwlwifi](http://wireless.kernel.org/en/users/Drivers/iwlwifi) é o driver sem fio para os chips sem fio atuais da Intel, como 5100AGN, 5300AGN e 5350AGN. Veja a [lista completa de dispositivos suportados](http://wireless.kernel.org/en/users/Drivers/iwlwifi#Supported_Devices). O firmware está incluído no pacote [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware). O [linux-firmware-iwlwifi-git](https://aur.archlinux.org/packages/linux-firmware-iwlwifi-git/) pode conter algumas atualizações mais cedo.

Se você tiver problemas para se conectar a redes em geral ou se a qualidade do link for muito ruim, tente desativar o 802.11n e talvez também ative a criptografia do software:

 `/etc/modprobe.d/iwlwifi.conf`  `options iwlwifi 11n_disable=1 swcrypto=1` 

Se você tiver um problema com a velocidade de uplink lenta no modo 802.11n, por exemplo 20Mbps, tente ativar a agregação de antena:

 `/etc/modprobe.d/iwlwifi.conf`  `options iwlwifi 11n_disable=8` 

Não se confunda com o nome da opção, quando o valor é definido como `8`, ele não desabilita nada, mas reativa a agregação da antena de transmissão. [[8]](http://forums.gentoo.org/viewtopic-t-996692.html?sid=81bdfa435c089360bdfd9368fe0339a9) [[9]](https://bugzilla.kernel.org/show_bug.cgi?id=81571)

Caso isso não funcione, você pode tentar desativar [economia de energia](/index.php/Power_saving#Network_interfaces "Power saving") para seu adaptador sem fio.

[Alguns](http://ubuntuforums.org/showthread.php?t=2183486&p=12845473#post12845473) nunca conseguiram que isso funcionasse. [Outros](http://ubuntuforums.org/showthread.php?t=2205733&p=12935783#post12935783) encontraram a salvação desativando N nas configurações do roteador depois de tentar tudo. Sabe-se que esta é a única solução em mais de uma ocasião. O segundo link menciona uma opção de 5Ghz que pode valer a pena ser explorada.

##### Coexistência com Bluetooth

Se você tiver dificuldade em conectar um fone de ouvido Bluetooth e manter uma boa velocidade de downlink, tente desabilitar a coexistência Bluetooth [[10]](https://wireless.wiki.kernel.org/en/users/Drivers/iwlwifi#wifibluetooth_coexistence):

 `/etc/modprobe.d/iwlwifi.conf`  `options iwlwifi bt_coex_active=0` 

##### Rastros de pilha de firmware

Você pode ter alguns problemas, situação na qual o driver emite alguns rastros de pilhas e erros, o que pode ser o causador de falhas.

 `dmesg`  `Microcode SW error detected.  Restarting 0x2000000.` 

Para corrigir esses erros, você pode fazer downgrade do pacote [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) ou renomear a última versão do firmware usado por seu dispositivo, de forma que uma versão mais antiga seja carregada (o que o mantém fora dos pacotes ignorados do pacman).

#### Desabilitar piscada de LED

**Nota:** Isso funciona com os drivers `iwlegacy` e `iwlwifi`.

As configurações padrão no módulo são para que o LED pisque na atividade. Algumas pessoas acham isso extremamente irritante. Para que o LED fique sólido quando o Wi-Fi estiver ativo, você pode usar o [systemd-tmpfiles](/index.php/Systemd_(Portugu%C3%AAs)#Arquivos_temporários "Systemd (Português)"):

 `/etc/tmpfiles.d/phy0-led.conf` 
```
w /sys/class/leds/phy0-led/trigger - - - - phy0radio

```

Execute `systemd-tmpfiles --create phy0-led.conf` para que a alteração surta efeito ou reinicie.

Para ver todos os valores possíveis para esse LED:

```
# cat /sys/class/leds/phy0-led/trigger

```

**Dica:** Se você não tiver `/sys/class/leds/phy0-led`, você pode tentar usar a [opção de módulo](/index.php/Kernel_modules#Setting_module_options "Kernel modules") `led_mode="1"`. Deve ser válida para ambos drivers `iwlwifi` e `iwlegacy`.

### Broadcom

Veja [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless").

### Outros drivers/dispositivos

#### Tenda w322u

Trate essa placa Tenda como um dispositivo `rt2870sta`. Veja [#rt2x00](#rt2x00).

#### orinoco

Isso deve ser parte do pacote do kernel e já estar instalado.

Alguns chipsets Orinoco são Hermes II. Você pode usar o driver `wlags49_h2_cs` em vez do `orinoco_cs` e ganhar suporte a WPA. Para usar o driver, [coloque em lista negra](/index.php/Blacklist "Blacklist") `orinoco_cs` primeiro.

#### prism54

O driver `p54` está incluído no kernel, mas você precisa fazer o download do firmware apropriado para sua placa [neste site](http://linuxwireless.org/en/users/Drivers/p54#firmware) e instalá-lo no diretório `/usr/lib/firmware`.

**Nota:** Também existe um driver mais antigo e obsoleto `prism54`, que pode entrar em conflito com o driver mais recente (`p54pci` ou `p54usb`). Certifique-se de [colocar em lista negra](/index.php/Blacklist "Blacklist") `prism54`.

#### ACX100/111

**Atenção:** Os drivers para esses dispositivos [estão quebrados](https://mailman.archlinux.org/pipermail/arch-dev-public/2011-June/020669.html) e não funcionam com versões mais recentes do kernel.

Pacotes: `tiacx` `tiacx-firmware` (excluídos dos repositórios oficiais e do AUR)

Veja o [wiki oficial](http://sourceforge.net/apps/mediawiki/acx100/index.php?title=Main_Page) para detalhes.

#### zd1211rw

[`zd1211rw`](http://zd1211.wiki.sourceforge.net/) é um driver para o chipset WLAN ZyDAS ZD1211 802.11b/g USB, e está incluído nas versões recentes do kernel do Linux. Consulte [[11]](http://www.linuxwireless.org/en/users/Drivers/zd1211rw/devices) para obter uma lista de dispositivos suportados. Você só precisa [instalar](/index.php/Instalar "Instalar") o firmware do dispositivo, fornecido pelo pacote [zd1211-firmware](https://aur.archlinux.org/packages/zd1211-firmware/).

#### hostap_cs

[Host AP](http://hostap.epitest.fi/) é um driver Linux para placas de rede local sem fio baseado no chipset Prism2/2.5/3 da Intersil. O driver está incluído no kernel do Linux.

**Nota:** Certifique-se de [colocar em lista negra](/index.php/Blacklist "Blacklist") o driver `orinico_cs`, pois pode causar problemas.

### ndiswrapper

Ndiswrapper é um script wrapper que permite usar alguns drivers do Windows no Linux. Você precisará dos arquivos `.inf` e `.sys` do seu driver do Windows.

**Atenção:** Certifique-se de usar os drivers apropriados para sua arquitetura (x86 vs. x86_64).

**Dica:** Se você precisar extrair esses arquivos de um arquivo `*.exe`, você pode usar [cabextract](https://www.archlinux.org/packages/?name=cabextract).

Siga essas etapas para configurar ndiswrapper.

1\. Instale [ndiswrapper-dkms](https://www.archlinux.org/packages/?name=ndiswrapper-dkms)

2\. Instale o driver para `/etc/ndiswrapper/*`

```
# ndiswrapper -i *nome_de_arquivo*.inf

```

3\. Liste todos os drivers instalados para ndiswrapper

```
$ ndiswrapper -l

```

4\. Deixe o ndiswrapper escrever sua configuração no `/etc/modprobe.d/ndiswrapper.conf`:

```
# ndiswrapper -m
# depmod -a

```

Agora a instalação do ndiswrapper está quase concluída; siga as instruções em [Kernel modules#Automatic module loading with systemd](/index.php/Kernel_modules#Automatic_module_loading_with_systemd "Kernel modules") para carregar automaticamente o módulo na inicialização.

A parte importante é certificar-se de que ndiswrapper existe nesta linha, por isso basta adicioná-lo ao lado dos outros módulos. Seria melhor testar se o ndiswrapper será carregado agora, então:

```
# modprobe ndiswrapper
# iwconfig

```

e *wlan0* deve existir agora. Se você tiver problemas, alguma ajuda está disponível em: [ndiswrapper howto](http://sourceforge.net/p/ndiswrapper/ndiswrapper/HowTos/) e [ndiswrapper FAQ](http://sourceforge.net/p/ndiswrapper/ndiswrapper/FAQ/).

### backports-patched

[backports-patched](https://aur.archlinux.org/packages/backports-patched/) fornece drivers lançados em novos kernels portados para uso em kernels mais antigos. O projeto começou desde 2007 e era originalmente conhecido como compat-wireless, evoluiu para compat-drivers e foi recentemente renomeado simplesmente para backports.

Se você estiver usando o kernel antigo e tiver problemas de conexão sem fio, os drivers neste pacote podem ajudar.

## Veja também

*   [O projeto Linux Wireless](http://wireless.kernel.org/)
*   [Guia de Aircrack-ng para instalação de drivers](http://aircrack-ng.org/doku.php?id=install_drivers)