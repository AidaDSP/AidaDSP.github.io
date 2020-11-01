---
layout: post
title: "Generating presets for Zeroconvo"
---

_**Zeroconvo**_ is a ir convolver plugin made by [Robin Gareus](https://gareus.org/), that also develops
many of the [plugins](http://x42-plugins.com/x42/) currently running on _**Mod Duo**_ or _**Aida DSP OS**_.

Some users of Ardour or Ubuntu Studio may argue that an excellent open source ir convolution
plugin, [ir.lv2](https://github.com/Anchakor/ir.lv2) already exists, so why wasting time using zeroconvo?

The answer is zeroconvo works in _headless devices_* like _**Mod Duo**_ or _**Aida DSP OS**_.

# The problem

On _**Aida DSP OS**_ and in the _**Mod-Duo**_ the graphic part is separated from the plugin source code
and builds a web interface by reading _.ttl files_* in the directory where also the binary is contained.

Since a file explorer functionality is not present in current _**mod-ui**_*, the user can select an ir file **only** if it's already
listed in a ttl preset file.

# What are ttl files?

They are human readable text files that are used to describe a plugin or a preset for a particular plugin. Please see [Wikipedia](https://en.wikipedia.org/wiki/Turtle_(syntax))

# Auto generating ttl preset file from impulse response files

Imagine that you have a huge collection of ir impulse response files in a folder and you
want to be able to use them on _**Mod Duo**_ or _**Aida DSP OS**_.

Something like this:

```
ir
├── cabs
│   ├── bass
│   └── guitar
│       ├── CelestionSidewinder
│       ├── Fender68VibroluxReverb
│       ├── FenderBassman
│       ├── FenderSuperChamp
│       ├── G12h
│       ├── LeonTodd
│       ├── MarshallJCM2000
│       ├── MarshallPlexi
│       ├── MatchlessChieftain
│       ├── MesaStudio22
│       ├── Randall
│       └── Vintage30
├── others
└── reverbs
```

inside a single directory, you have multiple ir files depending for example
on the mic type and positions

```
├── MesaStudio22
│   ├── Mesa_Boogie_Studio_22_4050_Off_ax_48s.wav
│   ├── Mesa_Boogie_Studio_22_4050_on_ax_48s.wav
│   ├── Mesa_Boogie_Studio_22_441_Edge_48s.wav
│   └── Mesa_Boogie_Studio_22_441_On_48s.wav
```

# Bash scripting is your friend

I made a script to scan all the files in the directory and generate automatically a valid ttl preset file for Zeroconvo plugin.

You can download the script from [Aida DSP OS Share](https://drive.google.com/drive/folders/1hVDwNKM-71I9deZ_zFdNpo2buZoSFEat?usp=sharing) under _**Zeroconvo**_ directory.

I've tested it on a Pc running _**Ubuntu**_. In order to run it you need to install also _**ffmpeg**_ since I use
it to generate file's info that I write in the preset descriptions.

In order for the script to work, you need to use a similar directory tree like the one suggested. This is because
cab impulse responses are treated in a different way than reverb impulse responses, and there is no way to distinguish them
apart putting them in separate folders with a predefined name.

To run the script, copy it to the folder where you have the sudden directory structure with all you ir files, then
simply execute it with

```
chmod +x create_presets_ttl_ir
./create_presets_ttl_ir
```

# Copy everything to the device

The script generates two files, a _manifest.ttl_ and a _presets.ttl_
that you need to copy to your plugin folder _**zeroconvo.lv2**_. Along with this
you need to copy the ir files in the same path. The final result is something like this:

```
zeroconvo.lv2
├── ir
│   ├── cabs
│   ├── others
│   └── reverbs
├── manifest.ttl
├── presets.ttl
├── zeroconvolv.so
└── zeroconvolv.ttl
```

on _**Aida DSP OS**_ you can copy your ir folder with all your ir files and the presets.ttl and manifest.ttl
under the already exysting zeroconvo.lv2 directory. To do this you can use the _**usb mass storage**_ mode,
please see online [user manual]({{ '/aida_dsp_os_manual.html' | absolute_url }}).

On the _**Mod Duo**_ you should be able to copy files with _**scp**_ command, although I can't really test it
at the moment. Any feedback from Mod Duo users appreciated.

# Want more?

You need assistance? Write me a message on my [Facebook page](https://www.facebook.com/official.AidaDSP)

If you want to read more about developing lv2 plugins, you may interested in my [how-to]({{ '/howto_sdk_lv2_plugins.html' | absolute_url }})

If you want to support me, checkout my [store](https://www.tindie.com/products/Maxdsp/aida-dsp-os) on Tindie!

---
**NOTES**

1. "Headless" are devices where the x11 support (like in normal desktop machines) is missing
2. The web interface running on _**Mod Duo**_ and _**Aida DSP OS**_

The version of Zeroconvo used with my tests is 507d7dd4b52b755b860d19694e4f84e247a7969a

---

[Go to the Home Page]({{ '/' | absolute_url }})
