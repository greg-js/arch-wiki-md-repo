Este artículo describe la instalación y configuración de ciertos dispositivos sobre el ordenador portable **MSI GT72 2QD Dominator**. También se detallará la lista de dispositivos que son reconocidos directamente por Archlinux.

# Instalación de Archlinux

No se encontró ningún problema durante la instalación de Archlinux, puede instalarlo desde una **llave USB** o un **CD** normalmente y sin mucho trabajo. Para ver como crear una llave USB para la instalación vea: [USB flash installation media (Español)](/index.php/USB_flash_installation_media_(Espa%C3%B1ol) "USB flash installation media (Español)"), para más información de como crear soportes de instalación y/o simplemente para más información sobre la instalación de Archlinux lea la página: [Getting and installing Arch (Español)](/index.php/Getting_and_installing_Arch_(Espa%C3%B1ol) "Getting and installing Arch (Español)").

## Tabla de dispositivos

| Dispositivo | Tipo | Nota |
| Nvidia GeForce GTX 970M | Tarjeta gráfica | Instalar el driver [Nvidia](/index.php/NVIDIA "NVIDIA") y lib32-nvidia-libgl si instaló la versión 64-bit |
| Teclado | Teclado retroiluminado | Para poder cambiar los colores del teclado puede instalar [MSI Keys](https://github.com/markrileybot/python-msikeys#Python) |
| HDA-Intel | Tarjeta de sonido | La tarjeta de sonido es operacional desde la instalación |
| Webcam | Webcam | La webcam es operacional desde la instalación |
| Touchpad | Touchpad | El touchpad functiona sin problemas, debe instalar [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") |
| Qualcomm Atheros QCA6174 802.11ac | Tarjeta Wifi | La tarjeta Wifi no es reconocida por defecto pero puede instalar el paquete [firmware_ath10k-qca6174](https://aur.archlinux.org/packages/firmware_ath10k-qca6174/) |
| Atheros Communications, Inc. AR3012 | Tarjeta Bluetooth 4.0 | No logré hacer funcionar el bluetooth. Si alguien sabe como hacer funcionar este firmware por favor edite esta pagina |