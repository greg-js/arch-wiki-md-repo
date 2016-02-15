[wpa_supplicant](http://hostap.epitest.fi/wpa_supplicant/) es una multiplataforma de [WPA Supplicant](https://en.wikipedia.org/wiki/Supplicant_(computer) "wikipedia:Supplicant (computer)") con soporte para WPA y WPA2 ([IEEE 802.11i](https://en.wikipedia.org/wiki/IEEE_802.11i) / RSN —Robust Secure Network—). Está adaptado tanto para los ordenadores de sobremesa/portátiles como para sistemas integrados.

_wpa_supplicant_ es el componente IEEE 802.1X/WPA utilizado por las estaciones cliente. Implementa las negociaciones entre la clave y un WPA Authenticator, y contola el roaming y la asociación/autenticación IEEE 802.11 del controlador wland.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Configuración](#Configuraci.C3.B3n)
*   [3 Utilizar wpa_cli](#Utilizar_wpa_cli)
    *   [3.1 Añadir nuevas conexiones de red](#A.C3.B1adir_nuevas_conexiones_de_red)
    *   [3.2 Action script](#Action_script)
    *   [3.3 Activar con systemd](#Activar_con_systemd)
*   [4 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalación

Instale el paquete [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) desde los [repositorios oficiales](/index.php/Official_Repositories_(Espa%C3%B1ol) "Official Repositories (Español)").

También tiene la posibilidad de instalar el paquete [wpa_supplicant_gui](https://www.archlinux.org/packages/?name=wpa_supplicant_gui) que proporciona _wpa_gui_; es un fronted gráfico para _wpa_supplicant_ que usa las herramientas [qt4](https://www.archlinux.org/packages/?name=qt4).

## Configuración

El paquete [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) proporciona un archivo de configuración de referencia situado en `/etc/wpa_supplicant/wpa_supplicant.conf`, que documenta, de modo detallado, todas las opciones disponibles y relativas a la configuración.

El contenido mínimo del archivo de configuración requiere un bloque de red. Por ejemplo:

 `/etc/wpa_supplicant/foobar.conf` 

```
network={
    ssid="..."
}
```

Lo anterior puede ser fácilmente generado usando la herramienta _wpa_passphrase_. Por ejemplo:

 `$ wpa_passphrase _nombre-de-la-red_ _frase-contraseña_` 

```
network={
    ssid="_nombre-de-la-red_"
    #psk="_frase-contraseña_"
    psk=f5d1c49e15e679bebe385c37648d4141bc5c9297796a8a185d7bc5ac62f954e3
}
```

**Sugerencia:** Algunas frases de contraseña inusualmente complejas pueden requerir la entrada desde un archivo:

```
# wpa_passphrase _nombre-de-la-red_ < _frase-contraseña.txt_ > /etc/wpa_supplicant/wpa_supplicant-_interfaz_.conf

```

Una vez que se tiene un archivo de configuración, se puede ejecutar el demonio _wpa_supplicant_ y conectarse a una red inalámbrica:

```
# wpa_supplicant -B -i _interfaz_ -c _archivo_de_configuración_

```

Es posible que tenga que especificar un controlador para que funcione. Para obtener una lista completa de los controladores soportados vea la salida de `wpa_supplicant -h`, de modo que, por ejemplo, `nl80211` será preferido al obsoleto controlador `wext`. Utilice el parámetro `-D` para especificar el controlador:

```
# wpa_supplicant -B -i _interfaz_ -c _archivo_de_configuración_ -D _controlador_

```

**Sugerencia:** Tanto _wpa_supplicant_ como _wpa_passphrase_ se pueden combinar para asociarse con casi todas las redes WPA2 (Personal):

```
# wpa_supplicant -B -i _interfaz_ -c <(wpa_passphrase _nombre_de_la_red_ _frase_contraseña_)

```

Todo lo que queda es simplemente conectarse usando una dirección [IP estática](/index.php/Network_configuration#Static_IP_Address "Network configuration") o [DHCP](/index.php/Network_configuration#Dynamic_IP_Address "Network configuration"). Por ejemplo:

```
# dhcpcd _interfaz_

```

## Utilizar wpa_cli

_wpa_supplicant_ puede ser controlado manualmente durante su ejecución mediante la utilidad _wpa_cli_. Con el fin de utilizar _wpa_cli_, el demonio _wpa_supplicant_ debe estar configurado para crear una «interfaz de control» (socket). Esto se hace desde el archivo de configuración con la variable `ctrl_interface`. El siguiente ejemplo creará el socket en `/run/wpa_supplicant/` y permitirá que los miembros del grupo `adm` accedan a él:

```
ctrl_interface=DIR=/run/wpa_supplicant GROUP=adm

```

Es posible activar _wpa_supplicant_ para modificar el archivo de configuración cuando se recibe una orden de _wpa_cli_. Esto es útil para agregar manualmente nuevas redes en el archivo de configuración de itinerancia sin la necesidad de reiniciar el demonio _wpa_supplicant_. Basta con añadir lo siguiente al archivo de configuración:

```
update_config=1

```

Después de iniciado el demonio _wpa_supplicant_, puede arrancar _wpa_cli_. Intentará encontrar el archivo socket, si falla utilice la opción `-p`. Se puede especificar la interfaz que se configurará con la opción `-i`, de lo contrario utilizará la primera interfaz inalámbrica que encuentre gestionada por _wpa_supplicant_. Cuando se invoca _wpa_cli_, se obtendrá un prompt (`>`) interactivo. El prompt tiene la función autocompletar del tabulador y descripciones de las órdenes completadas.

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

Para asociarse con _MIRED_, dígale a _wpa_supplicant_ que se conecte a ella. Cada red está indexada numéricamente, por lo que la primera red tendrá el índice cero. La [PSK](https://en.wikipedia.org/wiki/Pre-shared_key "wikipedia:Pre-shared key") se puede proporcionar sin comillas como una alternativa a la contraseña proporcionada en este ejemplo:

```
> add_network
0
> set_network 0 ssid "_MIRED_"
> set_network 0 psk "_contraseña_"
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

Es posible combinar la configuración activando _wpa_supplicant_ y _dhcpcd_ para una particular interfaz de red (véase [systemd#Using units](/index.php/Systemd#Using_units "Systemd") para más detalles):

```
# systemctl enable wpa_supplicant@_nombre de la interfaz de red_
# systemctl enable dhcpcd@_nombre de la interfaz de red_

```

La sección `[Install]` de la versión actual del servicio systemd es incorrecta ([bug report](http://w1.fi/bugz/show_bug.cgi?id=477)). Si el nombre de su interfaz no es (wlan0), será necesario copiar el archivo de servicios en `/etc/systemd/system` y sustituir la sección `[Install]` con

```
[Install]
WantedBy=multi-user.target

```

Véase [systemd#Editing provided unit files](/index.php/Systemd#Editing_provided_unit_files "Systemd") para obtener ayuda con la edición.

**Nota:** Si utiliza`dhcpcd@.service`, es posible que también desee reemplazar la etiqueta `-w` por `-b` para que no espere hasta que se le asigne una dirección IP, antes de pasar a funcionar en segundo plano.

**Sugerencia:** [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) contiene un hook (activado por defecto) para poner en marcha de forma automática _wpa_supplicant_ ante la presencia de interfaces inalámbricas. Se inicia solo si existe un archivo de configuración en `/etc/wpa_supplicant.conf` y sin un proceso _wpa_supplicant_ sondeando dicha interfaz. No es necesario utilizar `wpa_supplicant@_nombre de la interfaz de red_` en absoluto y basta con activar `dhcpcd@_nombre de la interfaz de red_`.

## Véase también

*   [Kernel.org wpa_supplicant documentation](http://wireless.kernel.org/en/users/Documentation/wpa_supplicant)