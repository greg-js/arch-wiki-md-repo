Este artículo versa sobre la gestión básica del sonido. Para temas avanzados consulte [Pro Audio](/index.php/Pro_Audio "Pro Audio").

## Contents

*   [1 Información General](#Informaci.C3.B3n_General)
*   [2 Controladores e interfaces](#Controladores_e_interfaces)
*   [3 Servidores de sonido](#Servidores_de_sonido)
*   [4 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Información General

El sistema de sonido de Arch Linux contiene varios niveles:

*   Controladores e interfaz – soporte y gestión de hardware

*   Usermode API (bibliotecas) – utilizado y requerido por las aplicaciones

*   **(Opcional)** servidores de sonido usermode («modalidad de usuario») – los mejores para escritorio complejos, necesarias para múltiples aplicaciones de audio simultáneas, y vital para funciones más avanzadas, por ejemplo, pro audio

*   **(Opcional)** frameworks de sonido – entorno para aplicaciones exigentes que no comprometen procesos del servidor

La instalación, por defecto, de Arch ya incluye sistema de sonido en el kernel, denominado [ALSA](/index.php/ALSA_(Espa%C3%B1ol) "ALSA (Español)"), y varias utilidades para ello, que se instalarán desde los [repositorios oficiales.](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)") Quienes deseen funciones adicionales pueden optar por [OSS](/index.php/OSS_(Espa%C3%B1ol) "OSS (Español)") o indagar otros [servidores de sonido.](https://en.wikipedia.org/wiki/es:Servidor_de_sonido "wikipedia:es:Servidor de sonido")

## Controladores e interfaces

*   **[Advanced Linux Sound Architecture (ALSA)](/index.php/ALSA_(Espa%C3%B1ol) "ALSA (Español)")** — Un componente del kernel de Linux que proporciona controladores de dispositivos y da soporte mínimo para el hardware de audio.

	[http://www.alsa-project.org/main/index.php/Main_Page](http://www.alsa-project.org/main/index.php/Main_Page) || presente de serie en el kernel

*   **[Open Sound System (OSS)](/index.php/OSS "OSS")** — Una arquitectura sólida alternativa a los sistemas de tipo Unix y POSIX-compatibles. La versión 3 de OSS fue el sistema de sonido original de Linux incluido en el kernel, pero fue sustituido por ALSA en 2002, cuando la versión 4 de OSS se convirtió en software propietario. OSSv4 se convirtió en software libre de nuevo en 2007, cuando 4Front Technologies dio a conocer su código fuente y siempre bajo licencia GPL. No tiene tanta compatibilidad como ALSA para una amplia variedad de hardware, pero funciona mejor para algunos de ellos.

	[http://www.opensound.com/](http://www.opensound.com/) || [oss](https://aur.archlinux.org/packages/oss/)

## Servidores de sonido

*   **[PulseAudio](/index.php/PulseAudio "PulseAudio")** — Un servidor de sonido muy popular, utilizado por la mayoría de las aplicaciones Linux de escritorio más comunes hoy en día. Muy bueno en el manejo de múltiples entradas simultáneas, incluido el uso de audio de la red. Muy fácil hacer que funcione, de hecho, a menudo todo lo que uno tiene que hacer es instalar el paquete y se ejecutará automáticamente. No está diseñado para audio profesional de aplicaciones de baja latencia.

	[http://www.pulseaudio.org/](http://www.pulseaudio.org/) || [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio)

*   **[Jack-Audio-Connection-Kit](/index.php/JACK "JACK")** — Es la última edición de un servidor de sonido para audio profesional, especialmente para aplicaciones de baja latencia, incluyendo grabación, efectos, síntesis en tiempo real, y muchos otros recursos. A pesar de que esta edición es la más antigua, conserva un equipo de desarrollo muy activo y dedicado, y la elección de la edición a utilizar no es fácil, con lo cual el ensayo-error es a menudo útil.

	[http://jackaudio.org/](http://jackaudio.org/) || [jack](https://www.archlinux.org/packages/?name=jack)

*   **JACK2** — También llamado jackdmp, es la edición más reciente de JACK, diseñada explícitamente para sistemas multi-procesadores, incluyendo también el tráfico de red.

	[http://trac.jackaudio.org/wiki/Q_differenc_jack1_jack2](http://trac.jackaudio.org/wiki/Q_differenc_jack1_jack2) || [jack2](https://www.archlinux.org/packages/?name=jack2)

*   **JACK2 con D-Bus** — Este es JACK2 con una arquitectura diferente de arranque, capaz de funcionar bien en todo momento en paralelo con aplicaciones PulseAudio y no JACK, lo cual es un problema para la configuración de las otras dos categorías de JACK.

	[http://trac.jackaudio.org/wiki/WalkThrough/User/jack_control](http://trac.jackaudio.org/wiki/WalkThrough/User/jack_control) || [jack2-dbus](https://www.archlinux.org/packages/?name=jack2-dbus)

*   **[NAS](https://en.wikipedia.org/wiki/Network_Audio_System "wikipedia:Network Audio System")** — Este es un servidor de sonido con el apoyo de algunas aplicaciones importantes.

	[http://www.radscan.com/nas/nas-links.html](http://www.radscan.com/nas/nas-links.html) || [nas](https://aur.archlinux.org/packages/nas/)

## Véase también

*   [MIDI](/index.php/MIDI "MIDI")
*   [Codecs (Español)](/index.php/Codecs_(Espa%C3%B1ol) "Codecs (Español)")
*   [Disable PC speaker beep (Español)](/index.php/Disable_PC_speaker_beep_(Espa%C3%B1ol) "Disable PC speaker beep (Español)")