LinuxSampler is a software [audio sampler](https://en.wikipedia.org/wiki/Sampler_(musical_instrument) "wikipedia:Sampler (musical instrument)").It can be loaded with sound libraries in the gigasampler format (.gig). One benefit of LS is it can stream the samples directly from hard disk, allowing the usage of huge libraries (several GBs..).LS can be started as a standalone application or lv2 or dssi plugin.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Graphical frontend](#Graphical_frontend)
*   [2 Usage](#Usage)
    *   [2.1 The editor: Gigedit](#The_editor:_Gigedit)
    *   [2.2 The frontend: Qsampler](#The_frontend:_Qsampler)
    *   [2.3 Building a default template in qsampler](#Building_a_default_template_in_qsampler)
    *   [2.4 Building a performance template in qsampler](#Building_a_performance_template_in_qsampler)
*   [3 Advanced topics](#Advanced_topics)
    *   [3.1 Filtering midi messages before they reach LS](#Filtering_midi_messages_before_they_reach_LS)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Port conflict](#Port_conflict)
*   [5 External Resources](#External_Resources)
*   [6 TODO](#TODO)

## Installation

[Install](/index.php/Install "Install") the [linuxsampler](https://www.archlinux.org/packages/?name=linuxsampler) package. It is the "engine" of the sampler, which performs all the heavy and time critical computational tasks of handling MIDI events, calculating the audio data and sending the final audio data to your sound card(s). LinuxSampler itself usually runs as own process in the background of the computer and usually does not show up anything on the screen, or at most it can be launched to show status information and debug messages in a console window. Usually you will also need a frontend to control it.

### Graphical frontend

There are several graphical frontends available for LinuxSampler:

*   [qsampler](https://www.archlinux.org/packages/?name=qsampler), a Qt interface
*   [jsampler](https://www.archlinux.org/packages/?name=jsampler), a Java interface
*   [gigedit](https://www.archlinux.org/packages/?name=gigedit), a gig file editor

You can now run qsampler which will automatically start *linuxsampler*. If you use jsampler, you have to start *linuxsampler* first.

## Usage

#### The editor: Gigedit

Gigedit allows you to edit and create instruments for the Gigasampler format, which can be used with LinuxSampler as well as with Tascam's Gigastudio. You can use gigedit as stand-alone application without LinuxSampler running or in live-mode, started from any frontend ("edit" button).In this case, all your modifications are audible in realtime.

#### The frontend: Qsampler

This frontend provides the user a set of menus, buttons, sliders, dials, etc. to allow the user to control the sampler in a convenient way. It does not perform any signal processing tasks, so you can see it as a "face" of the sampler. From Qsampler you can load/unload .gig files into LinuxSampler and set their midi channel number, volume, jack output etc...and finally store all this setup in a file for a speedy re-opening of your "sampling orchestra".

### Building a default template in qsampler

Here, I will use [jack-keyboard](https://aur.archlinux.org/packages/jack-keyboard/) as a MIDI controller, but everything below applies as well with a master keyboard or MIDI interface providing midi output.

*   Start jack then jack-keyboard then qsampler

*   Let's define some audio outputs in qsampler :

	Go to menu -> View -> Devices (or `F11` shortcut or the green pci card icon in the toolbar).

	On the left panel, click on "Audio Devices".Now we can see the audio drivers available in the right panel.

	Choose "Jack" in the Driver menu.The default config should give you a pair of audio outputs at a sample rate of 44100.

	Click on the Create button down the window.

**Note :** In some systems, qsampler crashes if this window is closed or even backgrounded while the Bottom-Right panel is still in view.Easy workaround : click on "Audio devices" or "Midi Devices" on the left panel before leaving or unfocusing the window.

*   If you want LS to auto-connect to jack system outputs when you launch your template :

	On the left panel, click on "Audio Jack Device 0" , then on right panel select "Audio Jack 0" from the "Channel" drop-down list.

	Choose an output for the JACK_BINDINGS parameter, like "system:playback 1".

	Select "Audio Jack 1" from the "Channel" drop-down list and assign JACK_BINDINGS parameter value, like system:playback 2"

*   Now let's create a midi input also :

	On the left panel, click on "Midi Devices".

	On the right panel, choose "jack" (jack-midi) in the Driver menu.

	Hit the create button.

*   If you want LS to auto-connect to jack-keyboard midi output when you launch your template :

	Select the "Midi jack device" port 0" on the left panel.

	On the right panel, for the "JACK_BINDINGS" parameter value, choose "jack-keyboard:midi out".

Note that if jack-midi is not enabled in Qjackctl, you won't find the midi client in the drop-down list.You can check in Qjackctl setup : "Midi driver" should be set to "seq".A restart of jack and qsampler is needed.

Also, if jack-keyboard or whatever midi controller you defined in here is not started before qsampler starts, you will likely receive an error from qsampler not finding the midi client.In that case, you can still start the midi device and connect it to LS through qjackctl.

*   Finally close the Devices Config window and save your template.

**Tip:** You can define as much midi ports as midi controllers you use. The same applies to audio outputs, e.g for sending separated instrument outputs for recording in Ardour.

### Building a performance template in qsampler

*   Open qsampler and load your configuration template.
*   Press the "Add channel" button in the toolbar (Ctrl-A).A "channel" in the LS terminology is an object (visually a strip) which stores the settings for a given instrument : Name and location of the gig file, inputs & outputs used, midi channel, volume, solo/mute status, midi cc applied etc..much like a track in a sequencer.
*   The i/o settings of the channel pops up.
    *   Choose a gig file
    *   Choose an "instrument".A gig file can contain different "instruments".Basically a gig file is composed of a pool of sounds and some configuration possibilities of theses samples named "instruments". For example one instrument can load only the forte samples and apply some adsr on it, while another one can load every samples in the pool, and organize them as layers that will be triggered by the velocity applied on the controller. This way, very different types of of sound can be obtained from the same pool of samples, which is more efficient in terms of sound-design and disk space...
    *   Set the midi and audio i/o for the channel from the different drop-down lists. All the options you will find here were created earlier in the device configuration setup stored in your config template. If you would like to change some of it, you can also do it from here with the "midi input setup" and "audio output setup" buttons.
    *   Press ok.
*   The channel is added to the main window and the gig file is loaded into RAM. Well, only the start of the sounds used in the instrument are cached in memory, the main task of LS will be to stream the biggest part of them directly from disk. That's how it's possible to load 30 GBs of samples with only 1 GB of ram.
*   You should now be able to play your instrument from jack-keyboard or whatever controller is tied to LS.

If you get no sound, check the volume sliders both on the channel strip and on the main toolbar.

*   Repeat these steps as many times as you wish to complete your "sampling orchestra".
*   Save your template under a new name so you keep your default template clean if you want to start another orchestra from ground.

## Advanced topics

### Filtering midi messages before they reach LS

Sometimes sample libraries do not agree with how a composer/arranger expects the sounds played by his MIDI software. A concrete example would be a score editor connected to LS, playing a piano part in the C3 to C4 octave, but what is heard is really one octave higher (C4 to C5). Probably the layering of the samples in the gig file is offset by one octave. If you are sure the mapping is incorrect (opening the gig file in live mode from qsampler can help), then here is some solutions :

*   Transpose the MIDI part one octave lower. In an orchestral score, this is very wrong to see notes on staff sounding one octave lower, especially when you already deal with transposing instruments...Also you would have to transpose back before printing.
*   Redo the mapping inside the gig file. That would be the best solution as it definitely cures the problem. However this can be a lot of hassle if there is multiple instruments inside the file. Also some non-sounding notes are often reserved before the sounding ones to trigger some cc (keyswitches), making the remapping one octave lower more complex or even impossible.
*   The quick and non-destructive way here is to put a MIDI filter between the score editor and LS, that lowers the notes by one octave for the piano channel only. [qmidiroute](https://www.archlinux.org/packages/?name=qmidiroute) can do that and it also monitors all midi messages along the way. You could for example check that the cc sent by the score are really what they should be (right midi ch, pan, velocity curves etc...)

If you use this setup, you will have to change the piano part MIDI output in your score editor to go to qmidiroute instead of LS, and the piano "channel" in LS to use the qmidiroute output instead of your score editor. This also could be done at the orchestra level if you want to monitor every instrument in your score or if using multiple midi outputs in your score editor is not possible.

## Troubleshooting

If you get the message : *Engine: WARNING, CONFIG_EG_MIN_RELEASE_TIME too big for current audio fragment size & sampling rate!* and eventually a crash after that, then it's time to reconsider latency for your soundcard.Raise the samples/period setting in qjackctl and retry. As an indication, on an M-audio delta 44, a setup of samples/period=128, periods in buffer=2 and sampling rate=44100 gives a working setup with LS.Latency = 5.8ms which is already quite low.

### Port conflict

LinuxSampler uses port 8888 by default, as do some other programs (e.g. BitTorrent Sync). If you attempt to run linuxsampler at the same time as another program using this port, this message will be displayed: *Starting LSCP network server (0.0.0.0:8888)...LSCPServer: Could not bind server socket* To avoid this issue start linuxsapler with the command *linuxsampler --lscp-port 8889* You may also have to adjust the server port on your GUI frontend.

## External Resources

*   [Homepage](http://www.linuxsampler.org/index.php)
*   [Article about LS on LinuxJournal](http://www.linuxjournal.com/content/linuxsampler-project)
*   [LS tutorial (french)](http://www.linuxmao.org/tikiwiki/tiki-index.php?page=linuxsampler)
*   [JSampler Manual online](http://www.linuxsampler.org/jsampler/manual/html/jsampler.html)
*   [Links to commercial and free sample libraries](https://bb.linuxsampler.org/viewtopic.php?f=8&t=11)

## TODO

*   Rewrite the template configuration wich is too long.
*   add status of lv2, dssi plugins version of LS = OK (in overview)
*   Write a short section about LS as a plugin, involving different hosts (mostly prerequisite programs and command lines)
    *   In a quick test, LS lv2 plugin works great.Test host was "elven" from "ll-plugins" package
*   addjsampler-fantasia in the install section and configuration section
*   add options at build time in advanced topics