**Status de tradução:** Esse artigo é uma tradução de [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration"). Data da última tradução: 2018-08-15\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Wireless_network_configuration&diff=0&oldid=535182) na versão em inglês.

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

## Contents

*   [1 Driver de dispositivo](#Driver_de_dispositivo)
    *   [1.1 Verificar o status de driver](#Verificar_o_status_de_driver)
    *   [1.2 Instalar driver/firmware](#Instalar_driver.2Ffirmware)
*   [2 Utilitários](#Utilit.C3.A1rios)
    *   [2.1 Comparação entre iw e wireless_tools](#Compara.C3.A7.C3.A3o_entre_iw_e_wireless_tools)
*   [3 iw](#iw)
    *   [3.1 Obter o nome da interface](#Obter_o_nome_da_interface)
    *   [3.2 Obter o status da interface](#Obter_o_status_da_interface)
    *   [3.3 Ativar a interface](#Ativar_a_interface)
    *   [3.4 Descobrir pontos de acesso](#Descobrir_pontos_de_acesso)
    *   [3.5 Definir o modo de operação](#Definir_o_modo_de_opera.C3.A7.C3.A3o)
    *   [3.6 Conectar a um ponto de acesso](#Conectar_a_um_ponto_de_acesso)
*   [4 WPA2 Empresarial](#WPA2_Empresarial)
    *   [4.1 eduroam](#eduroam)
    *   [4.2 Configuração manual/automática](#Configura.C3.A7.C3.A3o_manual.2Fautom.C3.A1tica)
        *   [4.2.1 wpa_supplicant](#wpa_supplicant)
        *   [4.2.2 NetworkManager](#NetworkManager)
        *   [4.2.3 connman](#connman)
        *   [4.2.4 netctl](#netctl)
    *   [4.3 Solução de problemas](#Solu.C3.A7.C3.A3o_de_problemas)
        *   [4.3.1 MS-CHAPv2](#MS-CHAPv2)
*   [5 Dicas e truques](#Dicas_e_truques)
    *   [5.1 Respeitar o domínio regulatório](#Respeitar_o_dom.C3.ADnio_regulat.C3.B3rio)
*   [6 Solução de problemas](#Solu.C3.A7.C3.A3o_de_problemas_2)
    *   [6.1 Acesso temporário à internet](#Acesso_tempor.C3.A1rio_.C3.A0_internet)
    *   [6.2 Problemas com rfkill](#Problemas_com_rfkill)
    *   [6.3 Observando os logs](#Observando_os_logs)
    *   [6.4 Economia de energia](#Economia_de_energia)
    *   [6.5 Falha ao obter endereço IP](#Falha_ao_obter_endere.C3.A7o_IP)
    *   [6.6 Endereço IP válido, mas não consegue resolver host](#Endere.C3.A7o_IP_v.C3.A1lido.2C_mas_n.C3.A3o_consegue_resolver_host)
    *   [6.7 Definindo limites de RTS e de fragmentação](#Definindo_limites_de_RTS_e_de_fragmenta.C3.A7.C3.A3o)
    *   [6.8 Desconexões aleatórias](#Desconex.C3.B5es_aleat.C3.B3rias)
        *   [6.8.1 Causa nº.1](#Causa_n.C2.BA.1)
        *   [6.8.2 Causa nº.2](#Causa_n.C2.BA.2)
        *   [6.8.3 Causa nº.3](#Causa_n.C2.BA.3)
        *   [6.8.4 Causa nº.4](#Causa_n.C2.BA.4)
    *   [6.9 Redes Wi-Fi invisíveis por causa do domínio regulatório incorreto](#Redes_Wi-Fi_invis.C3.ADveis_por_causa_do_dom.C3.ADnio_regulat.C3.B3rio_incorreto)
*   [7 Solução de problemas de drivers e firmware](#Solu.C3.A7.C3.A3o_de_problemas_de_drivers_e_firmware)
    *   [7.1 Ralink/Mediatek](#Ralink.2FMediatek)
        *   [7.1.1 rt2x00](#rt2x00)
        *   [7.1.2 rt3090](#rt3090)
        *   [7.1.3 rt3290](#rt3290)
        *   [7.1.4 rt3573](#rt3573)
        *   [7.1.5 rt5572](#rt5572)
        *   [7.1.6 mt7612u](#mt7612u)
    *   [7.2 Realtek](#Realtek)
        *   [7.2.1 rtl8192cu](#rtl8192cu)
        *   [7.2.2 rtl8723ae/rtl8723be](#rtl8723ae.2Frtl8723be)
        *   [7.2.3 rtl88xxau](#rtl88xxau)
        *   [7.2.4 rtl8822bu](#rtl8822bu)
        *   [7.2.5 rtl8xxxu](#rtl8xxxu)
    *   [7.3 Atheros](#Atheros)
        *   [7.3.1 ath5k](#ath5k)
        *   [7.3.2 ath9k](#ath9k)
            *   [7.3.2.1 Economia de energia](#Economia_de_energia_2)
    *   [7.4 Intel](#Intel)
        *   [7.4.1 ipw2100 e ipw2200](#ipw2100_e_ipw2200)
        *   [7.4.2 iwlegacy](#iwlegacy)
        *   [7.4.3 iwlwifi](#iwlwifi)
            *   [7.4.3.1 Coexistência com Bluetooth](#Coexist.C3.AAncia_com_Bluetooth)
        *   [7.4.4 Desabilitar piscada de LED](#Desabilitar_piscada_de_LED)
    *   [7.5 Broadcom](#Broadcom)
    *   [7.6 Outros drivers/dispositivos](#Outros_drivers.2Fdispositivos)
        *   [7.6.1 Tenda w322u](#Tenda_w322u)
        *   [7.6.2 orinoco](#orinoco)
        *   [7.6.3 prism54](#prism54)
        *   [7.6.4 ACX100/111](#ACX100.2F111)
        *   [7.6.5 zd1211rw](#zd1211rw)
        *   [7.6.6 hostap_cs](#hostap_cs)
    *   [7.7 ndiswrapper](#ndiswrapper)
    *   [7.8 backports-patched](#backports-patched)
*   [8 Veja também](#Veja_tamb.C3.A9m)

## Driver de dispositivo

O kernel padrão do Arch Linux é *modular*, o que significa que muitos dos drivers para hardware de máquina residem no disco rígido e estão disponíveis como [módulos](/index.php/Kernel_modules "Kernel modules"). Na inicialização, o [udev](/index.php/Udev "Udev") faz um inventário do seu hardware e carrega os módulos (drivers) apropriados para o hardware correspondente, o que, por sua vez, permite a criação de uma *interface* de rede.

Alguns chipsets sem fio também exigem firmware, além de um driver correspondente. Muitas imagens de firmware são fornecidas pelo pacote [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) que é instalado por padrão, no entanto, as imagens de firmware proprietárias não são incluídas e devem ser instaladas separadamente. Isso é descrito em [#Instalar driver/firmware](#Instalar_driver.2Ffirmware).

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

Verifique também a saída do comando `ip link` para ver se uma interface sem fio ([geralmente](/index.php/Configura%C3%A7%C3%A3o_de_rede#Interfaces_de_rede "Configuração de rede") começa com a letra "w", por exemplo, `wlp2s1`) foi criada. Em seguida, ative a interface com `ip link set *interface* up`. Por exemplo, supondo que a interface seja `wlan0`:

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

## Utilitários

Assim como outras interfaces de rede, as sem fio são controladas com *ip* do pacote [iproute2](https://www.archlinux.org/packages/?name=iproute2).

Gerenciar uma conexão sem fio requer um conjunto básico de ferramentas. Use um [gerenciador de rede](/index.php/Gerenciador_de_rede "Gerenciador de rede") ou use um dos seguintes diretamente:

| Software | Pacote | [WEXT](https://wireless.wiki.kernel.org/en/developers/documentation/wireless-extensions) | [nl80211](https://wireless.wiki.kernel.org/en/developers/documentation/nl80211) | WEP | WPA/WPA2 | Nota |
| [wireless_tools](http://www.hpl.hp.com/personal/Jean_Tourrilhes/Linux/Tools.html) | [wireless_tools](https://www.archlinux.org/packages/?name=wireless_tools) | Sim | Não | Sim | Não | obsoleto |
| [iw](https://wireless.kernel.org/en/users/Documentation/iw) | [iw](https://www.archlinux.org/packages/?name=iw) | Não | Sim | Sim | Não |
| [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") | [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) | Sim | Sim | Sim | Sim |
| [iwd](/index.php/Iwd "Iwd") | [iwd](https://www.archlinux.org/packages/?name=iwd) | Não | Sim | Sim | Sim |

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

**Dica:** Para uma comparação entre os comandos *iw* e *wireless_tools*, veja [#Comparação entre iw e wireless_tools](#Compara.C3.A7.C3.A3o_entre_iw_e_wireless_tools).

**Nota:**

*   Note que a maioria dos comandos devem ser executados com [permissões de root](/index.php/Usu%C3%A1rios_e_grupos "Usuários e grupos"). Se executados com permissões de usuário normal, alguns dos comandos (por exemplo, *iwlist*) sairão sem erro, mas também não produzirão a saída correta, o que pode ser confuso.
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

[Suplicante de WPA](/index.php/WPA_supplicant#Advanced_usage "WPA supplicant") pode ser configurado diretamente por meio de seu arquivo de configuração ou usando seus frontends CLI/GUI e usado em combinação com um cliente DHCP. Veja os exemplos em `/usr/share/doc/wpa_supplicant/wpa_supplicant.conf` para configurar os detalhes de conexão.

#### NetworkManager

[NetworkManager](/index.php/NetworkManager_(Portugu%C3%AAs) "NetworkManager (Português)") pode gerar perfis de WPA2 Empresarial com [frontends gráficos](/index.php/NetworkManager_(Portugu%C3%AAs)#Front-ends "NetworkManager (Português)"). *nmcli* e *nmtui* não oferecem suporte a isso, mas podem usar perfis existentes.

#### connman

[ConnMan](/index.php/ConnMan "ConnMan") precisa de um arquivo de configuração separado antes de [se conectar](/index.php/ConnMan#Wi-Fi "ConnMan") à rede. Veja [connman-service.config(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/connman-service.config.5) e [Connman#Connecting to eduroam](/index.php/ConnMan#Connecting_to_eduroam_.28802.1X.29 "ConnMan") para detalhes.

#### netctl

[netctl](/index.php/Netctl "Netctl") possui suporte a configuração de [#wpa_supplicant](#wpa_supplicant) por meio de blocos inclusos com `WPAConfigSection=`. Veja [netctl.profile(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/netctl.profile.5) para detalhes.

**Atenção:** Regras de uso especial de aspas se aplicam: veja a seção `*SPECIAL QUOTING RULES*` em [netctl.profile(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/netctl.profile.5).

**Dica:** Certificados personalizados podem ser especificados adicionando a linha `'ca_cert="/caminho/para/o/ceritficado.cer"'` em `WPAConfigSection`.

### Solução de problemas

#### MS-CHAPv2

As redes sem fio WPA2 Empresarial que exigem autenticação tipo 2 de MSCHAPv2 com PEAP às vezes exigem [pptpclient](https://www.archlinux.org/packages/?name=pptpclient), além do pacote [ppp](https://www.archlinux.org/packages/?name=ppp). [netctl](/index.php/Netctl "Netctl") parece funcionar facilmente sem ppp-mppe, no entanto. Em ambos os casos, o uso de MSCHAPv2 é desencorajado, pois é altamente vulnerável, embora o uso de outro método geralmente não seja uma opção. Veja também [[1]](https://www.cloudcracker.com/blog/2012/07/29/cracking-ms-chap-v2/) e [.pdf](http://research.edm.uhasselt.be/~bbonne/docs/robyns14wpa2enterprise).

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

## Solução de problemas

Essa seção contém dicas de solução de problemas gerais, e não estritamente relacionados com problemas de drivers ou firmwares. Para tais tópicos, veja a próxima seção [#Solução de problemas de drivers e firmware](#Solu.C3.A7.C3.A3o_de_problemas_de_drivers_e_firmware).

### Acesso temporário à internet

Se você tem hardware problemático e precisa de acesso à Internet para, por exemplo, baixar algum software ou obter ajuda em fóruns, você pode usar o recurso interno do Android para compartilhamento de internet via cabo USB. Consulte [Android tethering#USB tethering](/index.php/Android_tethering#USB_tethering "Android tethering") para mais informações.

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

### Economia de energia

Veja [Power saving#Network interfaces](/index.php/Power_saving#Network_interfaces "Power saving").

### Falha ao obter endereço IP

*   Se a obtenção de um endereço IP falhar repetidamente usando o cliente padrão [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd), tente instalar e usar [dhclient](https://www.archlinux.org/packages/?name=dhclient). Não se esqueça de selecionar *dhclient* como o cliente DHCP principal no [gerenciador de conexões](#Configura.C3.A7.C3.A3o_manual.2Fautom.C3.A1tica).

*   Se você puder obter um endereço IP para uma interface com fio e não para uma interface sem fio, tente desabilitar o recurso [economia de energia](#Economia_de_energia) da placa de rede sem fio (especifique {{ic|off} } em vez de `on`).

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

Se o dmesg disser `wlan0: deauthenticating from MAC by local choice (reason=3)` e você perder sua conexão Wi-Fi, é provável que você tenha uma economia de energia um pouco agressiva demais na sua placa Wi-Fi[[3]](http://us.generation-nt.com/answer/gentoo-user-wireless-deauthenticating-by-local-choice-help-204640041.html). Tente desabilitar os recursos [economia de energia](#Economia_de_energia) do placa sem fio (especifique `off` em vez de `on`).

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
*   Desabilite largura de banda do canal `40Mhz` (menor rendimento, mas colisões menos prováveis)
*   Se o roteador tiver configurações de qualidade de serviço (QoS), verifique a integridade das configurações (por exemplo, o Wi-Fi Multimedia (WMM) faz parte do controle de fluxo QoS opcional. Um firmware incorreto do roteador pode anunciar sua existência, embora a configuração não esteja ativada)

### Redes Wi-Fi invisíveis por causa do domínio regulatório incorreto

Se os canais Wi-Fi do computador não corresponderem aos do país do usuário, isso poderá resultar na invisibilidade de algumas redes Wi-Fi no intervalo, porque eles usam canais sem fio que não são permitidos por padrão. A solução é configurar o domínio regulatório corretamente, consulte [#Respeitar o domínio regulatório](#Respeitar_o_dom.C3.ADnio_regulat.C3.B3rio).

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

Veja [[5]](https://wikidevi.com/wiki/Realtek) para uma lista de chipsets Realtek e especificações.

#### rtl8192cu

The driver is now in the kernel, but many users have reported being unable to make a connection although scanning for networks does work.

[8192cu-dkms](https://aur.archlinux.org/packages/8192cu-dkms/) includes many patches, try this if it does not work fine with the driver in kernel.

#### rtl8723ae/rtl8723be

The `rtl8723ae` and `rtl8723be` modules are included in the mainline Linux kernel.

Some users may encounter errors with powersave on this card. This is shown with occasional disconnects that are not recognized by high level network managers ([netctl](/index.php/Netctl "Netctl"), [NetworkManager](/index.php/NetworkManager "NetworkManager")). This error can be confirmed by running `dmesg -w` or `journalctl -f` and looking for output related to powersave and the `rtl8723ae`/`rtl8723be` module. If you are having this issue, use the `fwlps=0` kernel option, which should prevent the WiFi card from automatically sleeping and halting connection.

 `/etc/modprobe.d/rtl8723ae.conf`  `options rtl8723ae fwlps=0` 

or

 `/etc/modprobe.d/rtl8723be.conf`  `options rtl8723be fwlps=0` 

If you have poor signal, perhaps your device has only one physical antenna connected, and antenna autoselection is broken. You can force the choice of antenna with `ant_sel=1` or `ant_sel=2` kernel option. [[6]](https://bbs.archlinux.org/viewtopic.php?id=208472)

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

If the failures persist during bootup and you are using Nouveau driver, try [enabling early KMS](/index.php/Nouveau#Enable_early_KMS "Nouveau") to prevent the conflict [[8]](https://bbs.archlinux.org/viewtopic.php?pid=1748667#p1748667).

#### iwlwifi

[iwlwifi](http://wireless.kernel.org/en/users/Drivers/iwlwifi) is the wireless driver for Intel's current wireless chips, such as 5100AGN, 5300AGN, and 5350AGN. See the [full list of supported devices](http://wireless.kernel.org/en/users/Drivers/iwlwifi#Supported_Devices). The firmware is included in the [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) package. The [linux-firmware-iwlwifi-git](https://aur.archlinux.org/packages/linux-firmware-iwlwifi-git/) may contain some updates sooner.

If you have problems connecting to networks in general or your link quality is very poor, try to disable 802.11n, and perhaps also enable software encryption:

 `/etc/modprobe.d/iwlwifi.conf`  `options iwlwifi 11n_disable=1 swcrypto=1` 

If you have a problem with slow uplink speed in 802.11n mode, for example 20Mbps, try to enable antenna aggregation:

 `/etc/modprobe.d/iwlwifi.conf`  `options iwlwifi 11n_disable=8` 

Do not be confused with the option name, when the value is set to `8` it does not disable anything but re-enables transmission antenna aggregation.[[9]](http://forums.gentoo.org/viewtopic-t-996692.html?sid=81bdfa435c089360bdfd9368fe0339a9) [[10]](https://bugzilla.kernel.org/show_bug.cgi?id=81571)

In case this does not work for you, you may try disabling [power saving](/index.php/Power_saving#Network_interfaces "Power saving") for your wireless adapter.

[Some](http://ubuntuforums.org/showthread.php?t=2183486&p=12845473#post12845473) have never gotten this to work. [Others](http://ubuntuforums.org/showthread.php?t=2205733&p=12935783#post12935783) found salvation by disabling N in their router settings after trying everything. This is known to have be the only solution on more than one occasion. The second link there mentions a 5ghz option that might be worth exploring.

##### Coexistência com Bluetooth

If you have difficulty connecting a bluetooth headset and maintaining good downlink speed, try disabling bluetooth coexistence [[11]](https://wireless.wiki.kernel.org/en/users/Drivers/iwlwifi#wifibluetooth_coexistence):

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

[`zd1211rw`](http://zd1211.wiki.sourceforge.net/) is a driver for the ZyDAS ZD1211 802.11b/g USB WLAN chipset, and it is included in recent versions of the Linux kernel. See [[12]](http://www.linuxwireless.org/en/users/Drivers/zd1211rw/devices) for a list of supported devices. You only need to [install](/index.php/Install "Install") the firmware for the device, provided by the [zd1211-firmware](https://aur.archlinux.org/packages/zd1211-firmware/) package.

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