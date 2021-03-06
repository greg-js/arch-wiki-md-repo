This article is about basic sound management. For advanced topics see [professional audio](/index.php/Professional_audio "Professional audio").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 General information](#General_information)
*   [2 Drivers and interface](#Drivers_and_interface)
*   [3 Sound servers](#Sound_servers)
*   [4 See also](#See_also)

## General information

The Arch sound system consists of several levels:

*   Drivers and interface – hardware support and control
*   Usermode API (libraries) – utilized and required by applications
*   **(optional)** Usermode sound servers – best for the complex desktop, needed for multiple simultaneous audio apps, and vital for more advanced capabilities e.g. pro audio
*   **(optional)** Sound frameworks – higher-level application environments not involving server processes

A default Arch installation already includes the kernel sound system ([ALSA](/index.php/ALSA "ALSA")), and lots of utilities for it can be installed from the [official repositories](/index.php/Official_repositories "Official repositories"). If you want additional features you can switch to [OSS](/index.php/OSS "OSS") or install one of several [sound servers](https://en.wikipedia.org/wiki/sound_server "wikipedia:sound server").

## Drivers and interface

*   **[ALSA](/index.php/ALSA "ALSA")** — A Linux kernel component providing device drivers and lowest-level support for audio hardware.

	[https://www.alsa-project.org/wiki/Main_Page](https://www.alsa-project.org/wiki/Main_Page) || present in stock kernel

*   **[Open Sound System](/index.php/Open_Sound_System "Open Sound System") (OSS)** — An alternative sound architecture for Unix-like and POSIX-compatible systems. OSS version 3 was the original sound system for Linux and is in the kernel, but was superseded by ALSA in 2002 when OSS version 4 became proprietary software. OSSv4 became free software again in 2007 when 4Front Technologies released its source code and provided it under the GPL. OSS does not support as wide a variety of hardware as ALSA, but does better for some.

	[http://www.opensound.com/](http://www.opensound.com/) || [oss](https://aur.archlinux.org/packages/oss/)

## Sound servers

*   **[PulseAudio](/index.php/PulseAudio "PulseAudio")** — A very popular sound server, usable by most common desktop Linux applications today. Very good at handling multiple simultaneous inputs, and can do network audio as well. Very easy to get working, in fact very often all one has to do is install the package and it will automatically run. Not intended for pro audio low-latency applications.

	[https://www.freedesktop.org/wiki/Software/PulseAudio/](https://www.freedesktop.org/wiki/Software/PulseAudio/) || [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio)

*   **[JACK Audio Connection Kit](/index.php/JACK_Audio_Connection_Kit "JACK Audio Connection Kit")** — The older edition of a sound server for pro audio use, especially for low-latency applications including recording, effects, realtime synthesis, and many others. Although this edition is the older, it retains a very active and devoted development team, and which edition to use is not clear, trial and error is often helpful.

	[https://jackaudio.org/](https://jackaudio.org/) || [jack](https://www.archlinux.org/packages/?name=jack)

*   **JACK2** — This is the newer edition of JACK, designed explicitly towards multi-processor systems, and also includes transport over network.

	[https://github.com/jackaudio/jackaudio.github.com/wiki/Q_difference_jack1_jack2](https://github.com/jackaudio/jackaudio.github.com/wiki/Q_difference_jack1_jack2) || [jack2](https://www.archlinux.org/packages/?name=jack2)

*   **[NAS](https://en.wikipedia.org/wiki/Network_Audio_System "wikipedia:Network Audio System")** — This is a sound server supported by some major applications.

	[https://www.radscan.com/nas/nas-links.html](https://www.radscan.com/nas/nas-links.html) || [nas](https://aur.archlinux.org/packages/nas/)

## See also

*   [MIDI](/index.php/MIDI "MIDI")
*   [Codecs](/index.php/Codecs "Codecs")
*   [Professional audio](/index.php/Professional_audio "Professional audio")
*   [PC speaker](/index.php/PC_speaker "PC speaker")