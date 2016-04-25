Speech recognition is any means by which you can interface with your computer via spoken word. This page is designed to identify applications that can facilitate speech recognition and to serve as a guide in installing and using this software in Arch.

**A note to newcomers:** speech recognition is something that traditionally has not been well supported in Linux. If you become interested and choose to dig below the immediate surface, you can expect difficulty in finding documentation or help from the community.

## Contents

*   [1 Types of speech recognition](#Types_of_speech_recognition)
*   [2 List of text to speech applications](#List_of_text_to_speech_applications)
*   [3 List of voiced commands applications](#List_of_voiced_commands_applications)
    *   [3.1 Gnome-Voice-Control](#Gnome-Voice-Control)
    *   [3.2 VEDICS](#VEDICS)
    *   [3.3 Perlbox-Voice](#Perlbox-Voice)
*   [4 List of speech recognition applications](#List_of_speech_recognition_applications)
    *   [4.1 Free Speech Recognition Engines](#Free_Speech_Recognition_Engines)
    *   [4.2 Proprietary Speech Recognition Engines](#Proprietary_Speech_Recognition_Engines)
*   [5 See also](#See_also)

## Types of speech recognition

Speech recognition can mean several things:

	Text-To-Speech

	As it sounds, Text-To-Speech (or TTS) will manipulate a string of text into an audio clip. It is useful for blind people to be able to use computers but can also be used to simply improve computer experience. There are several programs available that perform TTS, some of which are command-line based (ideal for scripting) and others which provide a handy GUI.

	Simple Voice Control/Commands

	This is the most basic form of Speech-To-Text application. These are designed to recognize a small number of specific, typically one-word commands and then perform an action. This is often used as an alternative to an application launcher, allowing the user for instance to say the word “firefox” and have his OS open a new browser window.

	Full dictation/recognition

	Full dictation/recognition software allows the user to read full sentences or paragraphs and translates that data into text on the fly. This could be used, for instance, to dictate an entire letter into the window of an email client. In some cases, these types of applications need to be trained to your voice and can improve in accuracy the more they are used.

## List of text to speech applications

Two text-to-speech applications are Festival and eSpeak, a small feature comparison is available in a mailing list [thread](http://web.archive.org/web/20090924193011/http://braille.uwo.ca/pipermail/speakup/2008-July/046756.html). Available packages for this category:

*   **[eSpeak](https://en.wikipedia.org/wiki/eSpeak "wikipedia:eSpeak")** — Compact open source software speech synthesizer for more than 50 languages.

	[http://espeak.sourceforge.net/](http://espeak.sourceforge.net/) || [espeak](https://www.archlinux.org/packages/?name=espeak)

*   **[Festival](/index.php/Festival "Festival")** — General framework for building speech synthesis systems as well as including examples of various modules. As a whole it offers full text to speech.

	[http://www.cstr.ed.ac.uk/projects/festival/](http://www.cstr.ed.ac.uk/projects/festival/) || [festival](https://www.archlinux.org/packages/?name=festival)

*   **Gnome speech** — API to incorporate speech into GNOME application menus

	[wikipedia:GNOME Speech](https://en.wikipedia.org/wiki/GNOME_Speech "wikipedia:GNOME Speech") || [gnome-speech](https://www.archlinux.org/packages/?name=gnome-speech)

*   **[MBROLA](/index.php/Mbrola "Mbrola")** — Non-free phonemes-to-audio program which supports more than 70 languages.

	[http://tcts.fpms.ac.be/synthesis/mbrola.html](http://tcts.fpms.ac.be/synthesis/mbrola.html) || [mbrola](https://aur.archlinux.org/packages/mbrola/)

*   **Mimic** — Text-to-speech voice synthesis from the Mycroft project

	[https://mimic.mycroft.ai/](https://mimic.mycroft.ai/) || [mimic-git](https://aur.archlinux.org/packages/mimic-git/)

*   **Speech Dispatcher** — Common interface to speech synthesis. It has backends for eSpeak, Festival, and a few other speech synthesizers.

	[http://www.freebsoft.org/speechd](http://www.freebsoft.org/speechd) || [speech-dispatcher](https://www.archlinux.org/packages/?name=speech-dispatcher)

*   **Jovie** — KDE Text To Speech Daemon.

	[https://userbase.kde.org/Jovie](https://userbase.kde.org/Jovie) || [kdeaccessibility-jovie](https://www.archlinux.org/packages/?name=kdeaccessibility-jovie)

## List of voiced commands applications

### Gnome-Voice-Control

[gnome-voice-control](https://aur.archlinux.org/packages/gnome-voice-control/) is a dialogue system to control the GNOME Desktop. It is developed on Google Summer of Code 2007.

### VEDICS

VEDICS (Voice Enabled Desktop Interaction and Control System) is an assistive software which lets the user to interact with the OS using voice commands.

Note: Not yet tested

[Site Link](http://vedics.sourceforge.net/)

Features:

*   Perform common window operations like close, minimize, maximize etc.
*   Invoke default applications like browsers, mail clients etc.
*   Access any element on the desktop just by saying its name.
*   Supports GNOME3, GNOME2

### Perlbox-Voice

Perlbox Voice is an voice enabled application to bring your desktop under your command.

Note:

*   Last updated in 2005
*   Package is in AUR, but missing festival-don dependency.

[Site Link](http://perlbox.sourceforge.net/pbtk/)

Features:

*   Text to speech (Thanks to the Festival speech synthesizer)
*   Voice control to open user specified applications. For example, if you say "Web", the Perlbox-Voice Control will open the browser of your choice.
*   Desktop plugins to control your Linux desktop using only your voice. You can switch virtual screens, cycle through desktops, invoke the run dialog, quick lock the screen.
*   Custom commands are fully supported, and you can add commands on the fly.
*   Pseudo Commands' allow you to enter commands that the speaker should say. For example, if you say "Good morning", the computer voice could say "And good morning to you".

## List of speech recognition applications

### Free Speech Recognition Engines

	CMU Sphinx

	See [http://cmusphinx.sourceforge.net/](http://cmusphinx.sourceforge.net/) and [Wikipedia](https://en.wikipedia.org/wiki/CMU_Sphinx "wikipedia:CMU Sphinx").

	Simon

	[http://sourceforge.net/projects/speech2text/](http://sourceforge.net/projects/speech2text/) - Simon is a QT interface to Julius that will replace the mouse and keyboard with your voice. Works with X11 and Windows

	Speech

	[Speech](https://github.com/andre-luiz-dos-santos/speech-app) is a Chrome App for dictation, using Google's speech recognition engine.

	Julius

	Julius is a large vocabulary continuous speech recognition decoder, their project page is located on [http://julius.sourceforge.jp/en_index.php](http://julius.sourceforge.jp/en_index.php)

	XVoice

	Uses ViaVoice to pass text to X applications. [http://xvoice.sourceforge.net/](http://xvoice.sourceforge.net/)

	ViaVoice

	[wikipedia:IBM ViaVoice](https://en.wikipedia.org/wiki/IBM_ViaVoice "wikipedia:IBM ViaVoice")

	sphinxkeys

	[http://code.google.com/p/sphinxkeys/](http://code.google.com/p/sphinxkeys/) - You can essentially type keyboard keys and mouse clicks by speaking into your microphone

	VoxForge

	[http://www.voxforge.org/](http://www.voxforge.org/) - a project that collects speech transcriptions for use in open source speech recognition engines

### Proprietary Speech Recognition Engines

	Dragon Naturally Speaking in Wine

	Dragon Naturally Speaking software by Nuance is a well-functioning and popular implementation of speech dictation. It is developed for Windows, but has been run successfully in a Linux enviornment using wine. It can be used independently for dictation into other wine programs such as notepad or it can be paired with Platypus to interface with any native linux program. Platypus also provides a feature to control of your OS using voice commands, similar to the programs described in [#List of voiced commands applications](#List_of_voiced_commands_applications).

	Nuance's software is non-free, so you will have to purchase a copy. Note that Dragon provides you with the ability to install it on a set number of machines.Installing/Reinstalling in wine may use up some of these licenses.

	[Platypus Project](http://thenerdshow.com/platypus.html)

	Wizzscribe SI

	Verbio ASR

	DynaSpeak from SRI International

	LumenVox Speech Engine

	VoxSigma

	[http://www.vocapia.com](http://www.vocapia.com) and [Wikipedia](https://en.wikipedia.org/wiki/VoxSigma "wikipedia:VoxSigma")

	VoxSigma is a speech-to-text software suite by Vocapia Research. It is well suited for broadcast monitoring, audio visual archive indexing, telephone speech analytics, transcription of business conference calls, and video subtitling.

## See also

*   [Synthèse vocale en français sous Linux - KubuntuBlog (french)](http://kubuntu.free.fr/blog/index.php/2006/09/24/121-synthese-vocale-en-francais-sous-linux)