Artículos relacionados

*   [Chromium/Tips and tricks](/index.php/Chromium/Tips_and_tricks "Chromium/Tips and tricks")
*   [Browser plugins](/index.php/Browser_plugins "Browser plugins")
*   [Firefox](/index.php/Firefox "Firefox")
*   [Opera](/index.php/Opera "Opera")

[Chromium](https://en.wikipedia.org/wiki/Chromium_(web_browser) es un navegador web de codigo abierto.

## Contents

*   [1 Instalación](#Instalación)
    *   [1.1 Aplicaciones por defecto](#Aplicaciones_por_defecto)
    *   [1.2 Complemento Flash Player](#Complemento_Flash_Player)
    *   [1.3 Visor PDF](#Visor_PDF)
    *   [1.4 Certificados](#Certificados)
*   [2 Consejos y trucos](#Consejos_y_trucos)
*   [3 Solución de problemas](#Solución_de_problemas)
    *   [3.1 Tipografía](#Tipografía)
    *   [3.2 Problemas de representación de tipos de letras en el complemento de PDF](#Problemas_de_representación_de_tipos_de_letras_en_el_complemento_de_PDF)
    *   [3.3 Forzar aceleración 3D](#Forzar_aceleración_3D)
*   [4 Véase también](#Véase_también)

## Instalación

El proyecto de código abierto, **Chromium**, puede ser [instalado](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") con el paquete [chromium](https://www.archlinux.org/packages/?name=chromium).

Otras alternativas son:

*   **Chromium Beta Channel** — Version beta

	[https://googlechromereleases.blogspot.com/](https://googlechromereleases.blogspot.com/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=chromium-beta)</small>

*   **Chromium Dev Channel** — Version de desarrollo

	[https://googlechromereleases.blogspot.com/](https://googlechromereleases.blogspot.com/) || [chromium-dev](https://aur.archlinux.org/packages/chromium-dev/)

*   **Chromium snapshot builds** — Versiones no testeadas

	[https://build.chromium.org/](https://build.chromium.org/) || [chromium-snapshot-bin](https://aur.archlinux.org/packages/chromium-snapshot-bin/)

*   **Chromium with [VA-API](/index.php/VA-API "VA-API") support** — Parche para VA-API

	[https://chromium-review.googlesource.com/c/chromium/src/+/532294](https://chromium-review.googlesource.com/c/chromium/src/+/532294) || [chromium-vaapi](https://aur.archlinux.org/packages/chromium-vaapi/)

El navegador derivado, **Google Chrome**, viene con Widevine [EME](https://en.wikipedia.org/wiki/Encrypted_Media_Extensions "wikipedia:Encrypted Media Extensions") (ejemplo, para netflix). Puede ser instalado con el paquete [google-chrome](https://aur.archlinux.org/packages/google-chrome/).

Otras alternativas son:

*   **Google Chrome Beta Channel** — Version beta de Google Chrome

	[https://www.google.com/chrome/browser/beta.html](https://www.google.com/chrome/browser/beta.html) || [google-chrome-beta](https://aur.archlinux.org/packages/google-chrome-beta/)

*   **Google Chrome Dev Channel** — Version de desarrollo

	[https://www.google.com/chrome/browser/](https://www.google.com/chrome/browser/) || [google-chrome-dev](https://aur.archlinux.org/packages/google-chrome-dev/)

**Nota:** Google Chrome ha dejado de soportar sistemas de 32 bits, dejando soporte solo de 64 bits.

Consulte [dos](https://chromium.googlesource.com/chromium/src/+/master/docs/chromium_browser_vs_google_chrome.md) [artículos](https://www.howtogeek.com/202825/what%E2%80%99s-the-difference-between-chromium-and-chrome/) Para una explicación de las diferencias entre Chromium con Google Chrome

### Aplicaciones por defecto

Para seleccionar Chromium como navegador predeterminado, consulte [default applications](/index.php/Default_applications "Default applications").

### Complemento Flash Player

Flash player viene por defecto en Google Chrome.

Para instalarlo en chromium, instale el paquete [pepper-flash](https://www.archlinux.org/packages/?name=pepper-flash).

Revise que Flash Player está activo en `chrome://settings/content/flash`.

### Visor PDF

Tanto Chromium como Google Chrome traen por defecto un visor de PDF, si desea usar otro, desactívelo en *en `chrome://settings/content/pdfDocuments`.*

### Certificados

Chromium usa [NSS](/index.php/Network_Security_Services "Network Security Services") para los certificados. Pueden ser configurados en `chrome://settings/certificates`.

## Consejos y trucos

Consulte [Chromium/Tips and tricks](/index.php/Chromium/Tips_and_tricks "Chromium/Tips and tricks").

## Solución de problemas

### Tipografía

**Nota:** Chromium no se integra por completo con fontconfig/GTK/Pango/X/etc. Por su sandbox. Para mas información, leer [Linux Technical FAQ](https://dev.chromium.org/developers/linux-technical-faq).

### Problemas de representación de tipos de letras en el complemento de PDF

Para arreglar la representación de tipos de letras en algunos archivos PDF, es necesario instalar el paquete [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation), de lo contrario, la fuente sustituida hace que el texto se superponga en otro texto. Esto fue [reportado en el seguimiento de errores de chromium](https://code.google.com/p/chromium/issues/detail?id=369991) por un usuario de Arch.

### Forzar aceleración 3D

**Advertencia:** Desactivando la lista negra de reenderizacion blacklist quizas altere el comportamiento, incluyendo crashes del sistema. Lee los bugs en `chrome://gpu`.

Primer paso [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration"). Luego, para forzar la aceleracion 3D, *Active* las casillas: «Anular reenderizado por softare», «Rasterizacion por GPU», «Zero-copy rasterizer» in `chrome://flags`. Revisa si funciona en `chrome://gpu`. esto puede causar problemas con el controlador de [radeon](/index.php/Radeon "Radeon").

## Véase también

*   [Pagina de Chromium](https://www.chromium.org/)
*   [Notas de Google Chrome](https://googlechromereleases.blogspot.com)
*   [Chrome web store](https://chrome.google.com/webstore/category/home)