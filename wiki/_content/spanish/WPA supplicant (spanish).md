Artículos relacionados

*   [Network Configuration (Español)](/index.php/Network_Configuration_(Espa%C3%B1ol) "Network Configuration (Español)")
*   [Wireless Setup (Español)](/index.php/Wireless_Setup_(Espa%C3%B1ol) "Wireless Setup (Español)")

[wpa_supplicant](http://hostap.epitest.fi/wpa_supplicant/) es una multiplataforma de [WPA Supplicant](https://en.wikipedia.org/wiki/Supplicant_(computer) con soporte para WPA y WPA2 ([IEEE 802.11i](https://en.wikipedia.org/wiki/IEEE_802.11i "wikipedia:IEEE 802.11i") / RSN —Robust Secure Network—). Está adaptado tanto para los ordenadores de sobremesa/portátiles como para sistemas integrados.

*wpa_supplicant* es el componente IEEE 802.1X/WPA utilizado por las estaciones cliente. Implementa las negociaciones entre la clave y un WPA Authenticator, y contola el roaming y la asociación/autenticación IEEE 802.11 del controlador wland.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Configuración](#Configuraci.C3.B3n)
*   [3 Utilizar wpa_cli](#Utilizar_wpa_cli)
    *   [3.1 Añadir nuevas conexiones de red](#A.C3.B1adir_nuevas_conexiones_de_red)
    *   [3.2 Action script](#Action_script)
    *   [3.3 Activar con systemd](#Activar_con_systemd)
*   [4 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalación

Instale el paquete [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

También tiene la posibilidad de instalar el paquete [wpa_supplicant_gui](https://aur.archlinux.org/packages/wpa_supplicant_gui/) que proporciona *wpa_gui*; es un fronted gráfico para *wpa_supplicant* que usa las herramientas [qt4](https://www.archlinux.org/packages/?name=qt4).

## Configuración

El paquete [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) proporciona un archivo de configuración de referencia situado en `/etc/wpa_supplicant/wpa_supplicant.conf`, que documenta, de modo detallado, todas las opciones disponibles y relativas a la configuración.

El contenido mínimo del archivo de configuración requiere un bloque de red. Por ejemplo:

 `/etc/wpa_supplicant/foobar.conf` 
```
network={
    ssid="..."
}
```

Lo anterior puede ser fácilmente generado usando la herramienta *wpa_passphrase*. Por ejemplo:

 `$ wpa_passphrase *nombre-de-la-red* *frase-contraseña*` 
```
network={
    ssid="*nombre-de-la-red*"
    #psk="*frase-contraseña*"
    psk=f5d1c49e15e679bebe385c37648d4141bc5c9297796a8a185d7bc5ac62f954e3
}
```

**Sugerencia:** Algunas frases de contraseña inusualmente complejas pueden requerir la entrada desde un archivo:
```
# wpa_passphrase *nombre-de-la-red* < *frase-contraseña.txt* > /etc/wpa_supplicant/wpa_supplicant-*interfaz*.conf

```

Una vez que se tiene un archivo de configuración, se puede ejecutar el demonio *wpa_supplicant* y conectarse a una red inalámbrica:

```
# wpa_supplicant -B -i *interfaz* -c *archivo_de_configuración*

```

Es posible que tenga que especificar un controlador para que funcione. Para obtener una lista completa de los controladores soportados vea la salida de `wpa_supplicant -h`, de modo que, por ejemplo, `nl80211` será preferido al obsoleto controlador `wext`. Utilice el parámetro `-D` para especificar el controlador:

```
# wpa_supplicant -B -i *interfaz* -c *archivo_de_configuración* -D *controlador*

```

**Sugerencia:** Tanto *wpa_supplicant* como *wpa_passphrase* se pueden combinar para asociarse con casi todas las redes WPA2 (Personal):
```
# wpa_supplicant -B -i *interfaz* -c <(wpa_passphrase *nombre_de_la_red* *frase_contraseña*)

```

Todo lo que queda es simplemente conectarse usando una dirección [IP estática](/index.php/Network_configuration#Static_IP_address "Network configuration") o [DHCP](/index.php/Network_configuration#Dynamic_IP_address "Network configuration"). Por ejemplo:

```
# dhcpcd *interfaz*

```

## Utilizar wpa_cli

*wpa_supplicant* puede ser controlado manualmente durante su ejecución mediante la utilidad *wpa_cli*. Con el fin de utilizar *wpa_cli*, el demonio *wpa_supplicant* debe estar configurado para crear una «interfaz de control» (socket). Esto se hace desde el archivo de configuración con la variable `ctrl_interface`. El siguiente ejemplo creará el socket en `/run/wpa_supplicant/` y permitirá que los miembros del grupo `adm` accedan a él:

```
ctrl_interface=DIR=/run/wpa_supplicant GROUP=adm

```

Es posible activar *wpa_supplicant* para modificar el archivo de configuración cuando se recibe una orden de *wpa_cli*. Esto es útil para agregar manualmente nuevas redes en el archivo de configuración de itinerancia sin la necesidad de reiniciar el demonio *wpa_supplicant*. Basta con añadir lo siguiente al archivo de configuración:

```
update_config=1

```

Después de iniciado el demonio *wpa_supplicant*, puede arrancar *wpa_cli*. Intentará encontrar el archivo socket, si falla utilice la opción `-p`. Se puede especificar la interfaz que se configurará con la opción `-i`, de lo contrario utilizará la primera interfaz inalámbrica que encuentre gestionada por *wpa_supplicant*. Cuando se invoca *wpa_cli*, se obtendrá un prompt (`>`) interactivo. El prompt tiene la función autocompletar del tabulador y descripciones de las órdenes completadas.

### Añadir nuevas conexiones de red

Inicie un escaneo de la red. Cuando la exploración haya terminado se mostrará una notificación:

```
> scan

```

Muestra del resultado del escaneo:

```
> scan_results
bssid / frequency / signal level / flags / ssid
00:00:00:00:00:00 2462 -49 [WPA2-PSK-CCMP][ESS] MIRED
11:11:11:11:11:11 2437 -64 [WPA2-PSK-CCMP][ESS] OTRARED

```

Para asociarse con *MIRED*, dígale a *wpa_supplicant* que se conecte a ella. Cada red está indexada numéricamente, por lo que la primera red tendrá el índice cero. La [PSK](https://en.wikipedia.org/wiki/Pre-shared_key "wikipedia:Pre-shared key") se puede proporcionar sin comillas como una alternativa a la contraseña proporcionada en este ejemplo:

```
> add_network
0
> set_network 0 ssid "*MIRED*"
> set_network 0 psk "*contraseña*"
> enable_network 0
<2>CTRL-EVENT-CONNECTED - Connection to 00:00:00:00:00:00 completed (reauth) [id=0 id_str=]

```

Escriba los cambios en el archivo de configuración:

```
> save_config
OK

```

### Action script

### Activar con systemd

Es posible combinar la configuración activando *wpa_supplicant* y *dhcpcd* para una particular interfaz de red (véase [systemd#Using units](/index.php/Systemd#Using_units "Systemd") para más detalles):

```
# systemctl enable wpa_supplicant@*nombre de la interfaz de red*
# systemctl enable dhcpcd@*nombre de la interfaz de red*

```

La sección `[Install]` de la versión actual del servicio systemd es incorrecta ([bug report](http://w1.fi/bugz/show_bug.cgi?id=477)). Si el nombre de su interfaz no es (wlan0), será necesario copiar el archivo de servicios en `/etc/systemd/system` y sustituir la sección `[Install]` con

```
[Install]
WantedBy=multi-user.target

```

Véase [systemd#Editing provided units](/index.php/Systemd#Editing_provided_units "Systemd") para obtener ayuda con la edición.

**Nota:** Si utiliza`dhcpcd@.service`, es posible que también desee reemplazar la etiqueta `-w` por `-b` para que no espere hasta que se le asigne una dirección IP, antes de pasar a funcionar en segundo plano.

**Sugerencia:** [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) contiene un hook (activado por defecto) para poner en marcha de forma automática *wpa_supplicant* ante la presencia de interfaces inalámbricas. Se inicia solo si existe un archivo de configuración en `/etc/wpa_supplicant.conf` y sin un proceso *wpa_supplicant* sondeando dicha interfaz. No es necesario utilizar `wpa_supplicant@*nombre de la interfaz de red*` en absoluto y basta con activar `dhcpcd@*nombre de la interfaz de red*`.

## Véase también

*   [Kernel.org wpa_supplicant documentation](http://wireless.kernel.org/en/users/Documentation/wpa_supplicant)