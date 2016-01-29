# USB MIDI keyboards

This how-to assumes that you are using [ALSA](/index.php/ALSA "ALSA") and that your sound card is set up so you can listen to music. Known to work using this how-to is the Evolution MK-631 USB midi keyboard with SB Live! Value card. Execute these instructions as an unprivileged user unless otherwise noted.

## Contents

*   [1 Preliminary Testing](#Preliminary_Testing)
    *   [1.1 ALSA](#ALSA)
*   [2 Plugging the keyboard](#Plugging_the_keyboard)
*   [3 Verifying Events](#Verifying_Events)
*   [4 Playing](#Playing)
    *   [4.1 Hardware synthesizer](#Hardware_synthesizer)
    *   [4.2 Software synthesizer](#Software_synthesizer)
        *   [4.2.1 Qsynth](#Qsynth)
        *   [4.2.2 Qsynth using JACK](#Qsynth_using_JACK)

## Preliminary Testing

### ALSA

Install the [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) package from the [official repositories](/index.php/Official_repositories "Official repositories").

Type `aseqdump`. It should output something like:

```
Waiting for data at port 128:0\. Press Ctrl+C to end.
Source_ Event_________________ Ch _Data__

```

Not much will show up there, so press Ctrl+C to quit the program.

## Plugging the keyboard

Now plug the keyboard in and turn it on. The keyboard should power up. Output of `lsusb` should contain:

```
Bus 002 Device 002: ID 0a4d:00a0 Evolution Electronics, Ltd

```

Output of `lsmod | grep usb` should contain the following modules:

```
usb_midi               25348  0
snd_usb_audio          70592  0
snd_usb_lib            16640  1 snd_usb_audio

```

**Note:** As of kernel 3.19.2 you might also need to manually load [module](/index.php/Kernel_modules "Kernel modules") `snd_seq_midi`. Bug report [FS#44286](https://bugs.archlinux.org/task/44286)

Now type `aconnect -i` to list all MIDI input ports. The output should contain:

```
client 72: 'MK-361 USB MIDI keyboard' [type=kernel]
    0 'MK-361 USB MIDI keyboard MIDI 1'
```

The client number is probably going to be different though. Take note of it.

## Verifying Events

Type `aseqdump -p ##` where you should replace `##` with the client number of your keyboard. You should see:

```
 72:0   Active Sensing

```

popping out all the time. Pressing a key should produce:

```
 72:0   Note on                 0  65  94
 72:0   Note on                 0  65   0

```

Various other events (turning control knobs, changing channels, etc.) should register in the list. This is a handy way of ensuring that your keyboard is running properly.

To send MIDI events back to the keyboard or another MIDI output device, you can use run `aplaymidi -p ## midifile.mid` and specify a MIDI file.

## Playing

To hear a sound when you push a button on your keyboard, you need a synthesizer that converts the MIDI signal into audio.

Some soundcards have a built-in hardware synthesizer, but these are not common in modern sound cards, especially not in onboard sound cards. An easier option is a software synthesizer, which is just a program which you can load with you own instrument samples.

### Hardware synthesizer

Type `aconnect -o` to list all MIDI output ports. It depends a lot on your sound card. On SB Live! Value, you get the following output:

```
client 64: 'EMU10K1 MPU-401 (UART)' [type=kernel]
    0 'EMU10K1 MPU-401 (UART)'
client 65: 'Emu10k1 WaveTable' [type=kernel]
    0 'Emu10k1 Port 0  '
    1 'Emu10k1 Port 1  '
    2 'Emu10k1 Port 2  '
    3 'Emu10k1 Port 3  '
```

Here client 65 is the actual MIDI synthesizer. Assuming the soundcard is [set up](/index.php/SB_Live!_Midi "SB Live! Midi") properly, you should be able to **route** the output of the keyboard to the MIDI synthesizer. Assuming _out_ is the output client number (65 in our example) and _in_ is the input client number (72 in our example), type `aconnect _in_ _out_`. Now you can play your keyboard via the MIDI output of your sound card.

### Software synthesizer

#### Qsynth

1.  Install [qsynth](https://www.archlinux.org/packages/?name=qsynth).
2.  Start QSynth and go to **Setup**, where you need to load soundfont in SF2 format. You can get free SoundFonts from [http://soundfonts.narod.ru/](http://soundfonts.narod.ru/) (in Russian). When QSynth asks you to restart the engine after loading the SoundFont, do so.
3.  Type `aconnect -o` to list all MIDI output ports. Find the one that contains `FLUID Synth` and note the client number.
4.  Assuming _out_ is the output client number and _in_ is the input client number (72 in our example), type `aconnect _in_ _out_`. Now you can play your keyboard and QSynth should produce sounds.

**Note:** You need to run `aconnect _in_ _out_` each time you restart Qsynth or change the instrument/SoundFont.

#### Qsynth using JACK

1.  We need to install [qsynth](https://www.archlinux.org/packages/?name=qsynth), [jack](/index.php/JACK_Audio_Connection_Kit "JACK Audio Connection Kit"), [qjackctl](https://www.archlinux.org/packages/?name=qjackctl)
2.  Launch qjackctl and check the settings:

```
 Server Path: jackd
 Driver: alsa
 Realtime=enable; Priority:0
 Frames/Period:512
 Soft Mode=enable; Periods/Buffer:2
 Rest of parameters=disable(by default)
 Dither: None
 Audio: Duplex

```

1.  Start jackd using qjackctl (the **Play** button)
2.  Connect your USB keyboard
3.  Start QSynth and go to **Setup**, where you need to load soundfont in SF2 format. You can get free SoundFonts from [http://soundfonts.narod.ru/](http://soundfonts.narod.ru/) (in Russian). When QSynth asks you to restart the engine after loading the SoundFont, do so.
4.  Go to qjackctl, click **Connect** and choose the ALSA tab. On the left side you will see connected MIDI keyboard, on the left side - QSynth. Choose MIDI keyboard and QSynth, and click **Connect**.

Retrieved from "[https://wiki.archlinux.org/index.php?title=USB_MIDI_keyboards&oldid=369088](https://wiki.archlinux.org/index.php?title=USB_MIDI_keyboards&oldid=369088)"