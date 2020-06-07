---
layout: post
title: "Importing Yamaha Dx7's ROMS"
---

The [Yamaha Dx7](https://en.wikipedia.org/wiki/Yamaha_DX7) is a popular FM synthesizer that is a must have for electronic music enthusiasts (but this unit really spreads among a pletora of genres).

![Yamaha Dx7](yamaha-dx7.jpg)

By combining the controls of the Dx7 you can obtain different sounds ranging from electric pianos to bells or strings. You can also produce nice pads, of course.

The combination of the controls can be saved in the original machine in a file called ROM. It's a sysex file (a binary file that can be send over midi to the machine
and whoose protocol is _**specific**_ for this machine)

On the web, you can find a _HUGE_ amount of ROMs [here](http://bobbyblues.recup.ch/yamaha_dx7/dx7_patches.html)

and there is also a _**new**_ nice web service that creates random ROMs for you using AI, see [here](https://www.thisdx7cartdoesnotexist.com/)

# Dexed lv2 plugin

On _**Aida DSP OS**_ and in the _**Mod-Duo**_ you will find the excellent _**Dexed**_ plugin already installed. 

[ ![](dexed1rev-small-size.png) ](dexed1rev-full-size.png)

this plugin is a gem since it emulates the original sound of the Dx7 in a perfect way and it's also open source.

# How to import Dx7's ROMs

You need a way to convert the .SYX rom file into a .ttl preset file that you can use on the board [1].

I've made a script that does that for you [2]: I have tested it on _Linux Ubuntu_. It should be possible to run it in _Windows 10_ using the Ubuntu shell but I'll leave the tests for you.

On the [Aida DSP OS Share](https://drive.google.com/drive/folders/11b5uSavJboytXnDFgocN8cjFrTf7xIc7?usp=sharing) folder there is a dir named _**Dexed**_. You need

to download this folder into your Pc.

Then you need to invoke the script in this way

```
$ cd Dexed
$ scripts/create_dexed_ttls roms/PAD1.SYX pads
```

and it's done! under now you need to copy ./out/dexed-pads.lv2 folder into
the lv2 plugins partition of Aida DSP OS (see [User Manual]({{ '/aida_dsp_os_manual.html' | absolute_url }}))

and at the next start the new presets will be added to the existing ones:

![Dexed presets](dexed1rev-preset.png)

The procedure can be uses also by Mod Duo's users, the change is only in the way to copy files
back to the unit.

Of course you can specify another .SYX file, just change the command to your needs.

Enjoy!

---
**NOTES**

1. The plugin version of Dexed running on Aida DSP OS/Mod Duo is a stripped version
which doesn't have the GUI to manually select a ROM file. The format that we need is .ttl (RDF), used to store presets among lv2 plugins. The advantage
of this format versus the .SYX is that it's editable and readable by a human (ascii text).
2. Some credits here: this script relies on other scripts and tools which are open source and are part of Dexed sources that
you can find [here](https://github.com/dcoredump/dexed). I've only modified these scripts to my needs.

---

[Go to the Home Page]({{ '/' | absolute_url }})
