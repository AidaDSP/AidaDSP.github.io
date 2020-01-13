---
image: assets/images/aida_dsp_os1.jpg
description: Nobody read manuals nowadays. For those who do instead.
---

# Aida DSP OS User Manual

## Connections

1. Front panel, from left to right
  * input audio mono (6.5mm jack, high impedance)
  * USB host port for USB midi devices (USB type A female connector)
  * Ethernet port (RJ-45 socket)
  * midi in (standard 5 poles din connector optoisolated)
1. Rear panel, from left to right
  * uart port (4 pin pinheader connector, arduino nano pinout )
  * USB micro supply port
  * SD-Card slot
  * output audio stereo (3.5mm jack, line level)
2. Top panel
  * OLED Display
  * three buttons: K1 (left), K2 (center), K3 (right)

## Usage

### Power on

To power on Aida DSP OS, connect _**USB micro supply port**_ to a proper supply source. Compatible sources are

1. Mobile phone adapter (verify it's at least 2A)
2. Mobile phone power bank
3. Raspberry Pi power adapter
4. The USB port of your laptop Pc (you'll need a male USB micro to female USB type-A cable)

### USB mass storage mode

In this mode Aida DSP OS can be connected to a Pc for transferring files or change default system configuration.

[NOTE] You need a USB micro to female USB type-A _**data**_ cable. Please verify it's a data cable! To check the cable
count how many metal contacts has the male USB micro connector in the cable. If only two it's a supply only cable, you need the one
with _**all**_ the contacts

1. Connect USB rear supply port to Pc with a USB data cable and press central button (K2)
2. On Aida DSP OS' display should appear "USB mass storage mode"
3. In your Pc explore the new usb mass storage device
4. Open file under .config/config with a simple text editor
5. Customize the file

The configuration file is sort of [INI file](https://en.wikipedia.org/wiki/INI_file). If you don't know
what is it an INI file don't worry and read the following, otherwise skip

```
INI files are organized in lines, if the line doesn't start with a ';', a '#' or a '['
then it's a valid line.
A valid line is used to specify a configuration. Example:

mode mod-duo

means the default startup mode for Aida DSP OS is Mod Duo mode. You can change it to

mode sampler

or

mode puredata

to start the board respectively in soundfont player mode or puredata mode.

```

When you finished to edit the configuration file, save it before exit and restart the board (this time no button press is necessary).

Aida DSP OS should start with the new configuration

### Soundfont player mode

### Mod-Duo mode

### Puredata mode

## Software Update

At the moment the procedure of software update consists in you downloading the new
binary image from a given link and then proceed to burn it to a valid SD Card (>= 32GB).
The process is not different from what's done with a Raspberry Pi board. If you are on _**Windows**_, [balenaEtcher](https://www.balena.io/etcher/)
works fine. On _**Linux**_ you have [dd](https://en.wikipedia.org/wiki/Dd_(Unix)).

If you need a tutorial, you can follow [this](https://www.raspberrypi.org/documentation/installation/installing-images/) link.

## Specifications

### Audio

- ADCs: 24 bit, 98dB SNR
- DACs: 24 bit, 100dB SNR
- Sampling rate: configurable, 48/96/192kHz (48kHz default)
- BUffer size: configurable, 128/256/512/1024 (256 default)
- Latency: ~10ms measured with an oscilloscope with 256 buffer size

### Board

- Quad-core 1GHz ARM Cortex-A53 cpu (64-bit)
- 1GB DDR3 RAM
- 32GB flash (SD Card)
- USB 2.0
- 10/100/1000 Ethernet

### OLED

- 128x64 blue oled display

### Supply

- 5V/2A

### Power consumption

- Usually no more than 2.5W

### Dimensions

- width 10,61 cm
- height 4,93 cm
- length 5,21 cm

### Weight

- 0,144 g
