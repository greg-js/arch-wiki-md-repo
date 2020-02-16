[AVR](https://en.wikipedia.org/wiki/AVR_microcontrollers "wikipedia:AVR microcontrollers") is a family of microcontrollers (MCUs) developed by Microchip Technology (former AVR). AVRs are especially common in hobbyist and educational embedded applications, popularized by [Arduino](/index.php/Arduino "Arduino") project. This page deals with 8-bit series of these MCUs.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Toolchain](#Toolchain)
*   [2 Programmers](#Programmers)
    *   [2.1 udev issues](#udev_issues)
*   [3 Usage](#Usage)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Optimization](#Optimization)
    *   [4.2 Sample Makefile](#Sample_Makefile)
    *   [4.3 Calculating control register values](#Calculating_control_register_values)
*   [5 See also](#See_also)

## Toolchain

Install [avr-gcc](https://www.archlinux.org/packages/?name=avr-gcc) to get toolchain and GNU compiler.

## Programmers

To flash compiled firmware to the AVR chip you will need programmer and software to rule it. Most popular programmers are [USBasp](https://www.fischl.de/usbasp), [AVRISP mkII](https://www.microchip.com/DevelopmentTools/ProductDetails/PartNO/ATAVRISP2), [Atmel-ICE](https://www.microchip.com/DevelopmentTools/ProductDetails/ATATMEL-ICE) and [STK500](https://www.microchip.com/DevelopmentTools/ProductDetails/PartNO/ATSTK500). [There is](https://www.olimex.com/Products/AVR/Programmers/AVR-PG2B) also exists the simplest DIY-programmer which works with LPT port. [avrdude](https://www.archlinux.org/packages/?name=avrdude) supports them all great.

### udev issues

If you're using AVRISP mkII or USBasp programmers please consider installing [avrisp-udev](https://aur.archlinux.org/packages/avrisp-udev/) and/or [usbasp-udev](https://aur.archlinux.org/packages/usbasp-udev/) respectively to be able to run avrdude without superuser rights.

## Usage

To compile C program for AVR chip (let's consider ATmega8A running at 8 MHz as example) you can use `avr-gcc` directly. You should only specify target MCU (full list of supported MCUs could be found in avr-gcc man page) and it's working frequency:

```
$ avr-gcc -DF_CPU=8000000UL -mmcu=atmega8a -std=gnu99 main.c -o main.elf

```

avrdude is smart enough to work with the resulting ELF file but you can convert it explicitly to Intel HEX:

```
$ avr-objcopy -O ihex -j .text -j .data main.elf main.hex

```

Then run avrdude and specify flash ROM as destination for formware burning (in this example AVRISP mkII is used and clock speed is lowered to the 125 kHz to be on safe side):

```
$ avrdude -p atmega8 -c avrispmkII -B 125kHz -U flash:w:main.hex

```

That's all. Among other things avrdude can work with EEPROM memory, fuse and lock bits. For example, to set up low and high fuses to the 0x9F and 0xD1 respectively use the following incantation:

```
$ avrdude -p atmega8 -c avrispmkII -B 125kHz -U lfuse:w:0x9F:m -U hfuse:w:0xD1:m

```

Just remember that ISP programming speed shouldn't exceed 1/8 of MCU's working frequency. A lot of new chips comes with 1 MHz speed settings so using 125 kHz as starting value should be fine enough.

## Tips and tricks

### Optimization

Because AVRs come with tight flash ROM size and relatively weak CPUs you can consider some optimizations to improve space usage and overall performance of your device. It's common practice to enable GCC optimization level `-Os` and turn on some extra features: `-funsigned-char -funsigned-bitfields -fpack-struct -fshort-enums`. To exclude unnecessary library references perform garbage collection: `-ffunction-sections -fdata-sections -Wl,--gc-sections`.

### Sample Makefile

Managing huge project could be tedious and Makefile workflow is the most efficient way to deal with it. Here are sample Makefile based on [AVRfreaks](https://www.avrfreaks.net/sites/default/files/Makefile.txt) version:

```
CC = avr-gcc
OBJCOPY = avr-objcopy
SIZE = avr-size
NM = avr-nm
AVRDUDE = avrdude
REMOVE = rm -f

MCU = atmega8a
F_CPU = 8000000

LFUSE = 0x9f
HFUSE = 0xd1

TARGET = firmware
SRC = main.c lcd.c twi.c
OBJ = $(SRC:.c=.o)
LST = $(SRC:.c=.lst)

FORMAT = ihex

OPTLEVEL = s

CDEFS = 

CFLAGS = -DF_CPU=$(F_CPU)UL
CFLAGS += $(CDEFS)
CFLAGS += -O$(OPTLEVEL)
CFLAGS += -mmcu=$(MCU)
CFLAGS += -std=gnu99
CFLAGS += -funsigned-char -funsigned-bitfields -fpack-struct -fshort-enums
CFLAGS += -ffunction-sections -fdata-sections
CFLAGS += -Wall -Wstrict-prototypes
CFLAGS += -Wa,-adhlns=$(<:.c=.lst)

LDFLAGS = -Wl,--gc-sections
LDFLAGS += -Wl,--print-gc-sections

AVRDUDE_MCU = atmega8
AVRDUDE_PROGRAMMER = avrispmkII
AVRDUDE_SPEED = -B 1MHz

AVRDUDE_FLAGS = -p $(AVRDUDE_MCU)
AVRDUDE_FLAGS += -c $(AVRDUDE_PROGRAMMER)
AVRDUDE_FLAGS += $(AVRDUDE_SPEED)

MSG_LINKING = Linking:
MSG_COMPILING = Compiling:
MSG_FLASH = Preparing HEX file:

all: gccversion $(TARGET).elf $(TARGET).hex size

.SECONDARY: $(TARGET).elf
.PRECIOUS: $(OBJ)

%.hex: %.elf
        @echo
        @echo $(MSG_FLASH) $@
        $(OBJCOPY) -O $(FORMAT) -j .text -j .data $< $@

%.elf: $(OBJ)
        @echo
        @echo $(MSG_LINKING) $@
        $(CC) -mmcu=$(MCU) $(LDFLAGS) $^ --output $(@F)

%.o : %.c
        @echo $(MSG_COMPILING) $<
        $(CC) $(CFLAGS) -c $< -o $(@F)

gccversion:
        @$(CC) --version

size: $(TARGET).elf
        @echo
        $(SIZE) -C --mcu=$(AVRDUDE_MCU) $(TARGET).elf

analyze: $(TARGET).elf
        $(NM) -S --size-sort -t decimal $(TARGET).elf

isp: $(TARGET).hex
        $(AVRDUDE) $(AVRDUDE_FLAGS) -U flash:w:$(TARGET).hex

fuses:
        $(AVRDUDE) $(AVRDUDE_FLAGS) -U lfuse:w:$(LFUSE):m -U hfuse:w:$(HFUSE):m

release: fuses isp

clean:
        $(REMOVE) $(TARGET).hex $(TARGET).elf $(OBJ) $(LST) *~

```

### Calculating control register values

To speed up development of your projects you can use [avrcalc](https://aur.archlinux.org/packages/avrcalc/) utility which helps to calculate different parameters for control registers regarding timers, frequencies etc.

## See also

*   [Arduino](/index.php/Arduino "Arduino")
*   [https://www.microchip.com/design-centers/8-bit/avr-mcus](https://www.microchip.com/design-centers/8-bit/avr-mcus)