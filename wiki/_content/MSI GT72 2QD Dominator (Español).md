# MSI GT72 2QD Dominator (Español)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Este artículo describe la instalación y configuración de ciertos dispositivos sobre el ordenador portable **MSI GT72 2QD Dominator**. También se detallará la lista de dispositivos que son reconocidos directamente por Archlinux.

# Instalación de Archlinux

No se encontró ningún problema durante la instalación de Archlinux, puede instalarlo desde una **llave USB** o un **CD** normalmente y sin mucho trabajo. Para ver como crear una llave USB para la instalación vea: [USB flash installation media (Español)](/index.php/USB_flash_installation_media_(Espa%C3%B1ol) "USB flash installation media (Español)"), para más información de como crear soportes de instalación y/o simplemente para más información sobre la instalación de Archlinux lea la categoría: [Getting and installing Arch (Español)](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch").

## Tabla de dispositivos

<table class="wikitable">

<tbody>

<tr>

<th>Dispositivo</th>

<th>Tipo</th>

<th>Nota</th>

</tr>

<tr>

<td>Nvidia GeForce GTX 970M</td>

<td>Tarjeta gráfica</td>

<td>Instalar el driver [Nvidia](/index.php/NVIDIA "NVIDIA") y lib32-nvidia-libgl si instaló la versión 64-bit</td>

</tr>

<tr>

<td>Teclado</td>

<td>Teclado retroiluminado</td>

<td>Para poder cambiar los colores del teclado puede instalar [MSI Keys](https://github.com/markrileybot/python-msikeys#Python)</td>

</tr>

<tr>

<td>HDA-Intel</td>

<td>Tarjeta de sonido</td>

<td>La tarjeta de sonido es operacional desde la instalación</td>

</tr>

<tr>

<td>Webcam</td>

<td>Webcam</td>

<td>La webcam es operacional desde la instalación</td>

</tr>

<tr>

<td>Touchpad</td>

<td>Touchpad</td>

<td>El touchpad functiona sin problemas, debe instalar [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics")</td>

</tr>

<tr>

<td>Qualcomm Atheros QCA6174 802.11ac</td>

<td>Tarjeta Wifi</td>

<td>La tarjeta Wifi no es reconocida por defecto pero puede instalar el paquete [firmware_ath10k-qca6174](https://aur.archlinux.org/packages/firmware_ath10k-qca6174/)<sup><small>AUR</small></sup></td>

</tr>

<tr>

<td>Atheros Communications, Inc. AR3012</td>

<td>Tarjeta Bluetooth 4.0</td>

<td>No logré hacer funcionar el bluetooth. Si alguien sabe como hacer funcionar este firmware por favor edite esta pagina</td>

</tr>

</tbody>

</table>

Retrieved from "[https://wiki.archlinux.org/index.php?title=MSI_GT72_2QD_Dominator_(Español)&oldid=416017](https://wiki.archlinux.org/index.php?title=MSI_GT72_2QD_Dominator_(Español)&oldid=416017)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [MSI (Español)](/index.php/Category:MSI_(Espa%C3%B1ol) "Category:MSI (Español)")