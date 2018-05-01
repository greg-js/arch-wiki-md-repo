Related articles

*   [Chromium/Tips and tricks](/index.php/Chromium/Tips_and_tricks "Chromium/Tips and tricks")
*   [Browser plugins](/index.php/Browser_plugins "Browser plugins")
*   [Firefox](/index.php/Firefox "Firefox")
*   [Opera](/index.php/Opera "Opera")

[Chromium](https://en.wikipedia.org/wiki/Chromium_(web_browser) es un navegador web de codigo abierto.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
    *   [1.1 Aplicacion por defecto](#Aplicacion_por_defecto)
    *   [1.2 Flash Player plugin](#Flash_Player_plugin)
    *   [1.3 Visor de PDFs](#Visor_de_PDFs)
    *   [1.4 Certificados](#Certificados)
*   [2 Tips y trucos](#Tips_y_trucos)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Fonts](#Fonts)
        *   [3.1.1 Font rendering issues in PDF plugin](#Font_rendering_issues_in_PDF_plugin)
    *   [3.2 Forzar aceleracion 3D](#Forzar_aceleracion_3D)
*   [4 Mira tambien](#Mira_tambien)

## Instalación

El proyecto open-source, **Chromium**, puede ser [instalado](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") con el paquete [chromium](https://www.archlinux.org/packages/?name=chromium).

Otras alternativas son:

*   **Chromium Beta Channel** — Version beta

	[https://googlechromereleases.blogspot.com/](https://googlechromereleases.blogspot.com/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=chromium-beta)</small>

*   **Chromium Dev Channel** — Version de desarrollo

	[https://googlechromereleases.blogspot.com/](https://googlechromereleases.blogspot.com/) || [chromium-dev](https://aur.archlinux.org/packages/chromium-dev/)

*   **Chromium snapshot builds** — Versiones no testeadas

	[https://build.chromium.org/](https://build.chromium.org/) || [chromium-snapshot-bin](https://aur.archlinux.org/packages/chromium-snapshot-bin/)

*   **Chromium with [VA-API](/index.php/VA-API "VA-API") support** — Parche para VA-API

	[https://chromium-review.googlesource.com/c/chromium/src/+/532294](https://chromium-review.googlesource.com/c/chromium/src/+/532294) || [chromium-vaapi](https://aur.archlinux.org/packages/chromium-vaapi/)

El navegador derivado, **Google Chrome**, Viene con Widevine [EME](https://en.wikipedia.org/wiki/Encrypted_Media_Extensions "wikipedia:Encrypted Media Extensions") (Ejemplo, para netflix), Puede ser instalado con el [google-chrome](https://aur.archlinux.org/packages/google-chrome/) package.

Otras alternativas son:

*   **Google Chrome Beta Channel** — Version beta de Google Chrome

	[https://www.google.com/chrome/browser/beta.html](https://www.google.com/chrome/browser/beta.html) || [google-chrome-beta](https://aur.archlinux.org/packages/google-chrome-beta/)

*   **Google Chrome Dev Channel** — Version de desarrollo

	[https://www.google.com/chrome/browser/](https://www.google.com/chrome/browser/) || [google-chrome-dev](https://aur.archlinux.org/packages/google-chrome-dev/)

**Note:**

*   Google Chrome ha dejado de soportar sistemas de 32 bits, dejando soporte solo de 64 bits

Leer [dos](https://chromium.googlesource.com/chromium/src/+/master/docs/chromium_browser_vs_google_chrome.md) [articulos](https://www.howtogeek.com/202825/what%E2%80%99s-the-difference-between-chromium-and-chrome/) Para una explicacion de las diferencias entre Chromium en Google Chrome

### Aplicacion por defecto

Para seleccionar Chromium como navegador predeterminado, leer [default applications](/index.php/Default_applications "Default applications").

### Flash Player plugin

Flash player viene por defecto en Google Chrome.

Para instalarlo en chromium, instalar el paquete [pepper-flash](https://www.archlinux.org/packages/?name=pepper-flash).

Revisar que Flash Player esta activo en `chrome://settings/content/flash`.

### Visor de PDFs

Tanto Chromium como Google Chrome traen por defecto un visor de PDFs, si desea usar otro, desactivarlo en *in `chrome://settings/content/pdfDocuments`.*

### Certificados

Chromium usa [NSS](/index.php/Network_Security_Services "Network Security Services") para los certificados. Pueden ser configurados en `chrome://settings/certificates`.

## Tips y trucos

Leer: [Chromium/Tips and tricks](/index.php/Chromium/Tips_and_tricks "Chromium/Tips and tricks").

## Troubleshooting

### Fonts

**Note:** Chromium no se integra por completo con fontconfig/GTK/Pango/X/etc. Por su sandbox. Para mas información, leer [Linux Technical FAQ](https://dev.chromium.org/developers/linux-technical-faq).

#### Font rendering issues in PDF plugin

To fix the font rendering in some PDFs one has to install the [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) package, otherwise the substituted font causes text to run into other text. This was [reported on the chromium bug tracker](https://code.google.com/p/chromium/issues/detail?id=369991) by an Arch user.

### Forzar aceleracion 3D

**Warning:** Desactivando la lista negra de reenderizacion blacklist quizas altere el comportamiento, incluyendo crashes del sistema. Lee los bugs en `chrome://gpu`.

Primer paso [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration"). Luego, para forzar la aceleracion 3D, *Activar* las casillas: "Anular reenderizado por softare", "Rasterizacion por GPU", "Zero-copy rasterizer" in `chrome://flags`. Revisa si funciona en `chrome://gpu`. esto puede causar problemas con el driver de [radeon](/index.php/Radeon "Radeon").

## Mira tambien

*   [Pagina de Chromium](https://www.chromium.org/)
*   [Notas de Google Chrome](https://googlechromereleases.blogspot.com)
*   [Chrome web store](https://chrome.google.com/webstore/category/home)