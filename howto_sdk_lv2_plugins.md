---
image: assets/images/lv2_logo1.jpeg
description: Develop LV2 plugins with Aida DSP OS sdk
---

## How-to: lv2, sdk

## Introduction

This sdk will allow you to compile LV2 audio plugins that can run on Aida DSP OS board
based on a 64-bit Quad-Core ARM Cortex-A53 processor. 

You can download the sdk [here](https://drive.google.com/drive/folders/1hVDwNKM-71I9deZ_zFdNpo2buZoSFEat?usp=sharing)


## Installation

On a Linux machine:

`./poky-glibc-x86_64-aidadsp-basic-image-aarch64-toolchain-2.4.3.sh`


## Build example plugin

This audio plugin is a simple gain cell with a control knob

    source environment-setup-aarch64-poky-linux
    mkdir ~/aidadspworkspace
    cd ~/aidadspworkspace
    git clone https://github.com/moddevices/mod-utilities.git
    cd mod-utilities/Gain
    make

or

    cd mod-utilities
    make

to build all the audio plugins provided in the repo.


## Documentation

http://lv2plug.in/ns/lv2core/

or sysroots/aarch64-poky-linux/usr/include/lv2.h

which is the header where the LV2_Descriptor where the core functions necessary to instantiate and use
a plugin are defined.


## Quick How-To

    MyAwesomeAudioPlugin::instantiate -> do the malloc(s) here
    MyAwesomeAudioPlugin::connect_port
    MyAwesomeAudioPlugin::activate -> do the initialization of buffers here (i.e. memset...)
    MyAwesomeAudioPlugin::run -> do the change_param(knob1, knob2, ...) and processing(audio in, audio out) here
    MyAwesomeAudioPlugin::deactivate
    MyAwesomeAudioPlugin::cleanup -> do the free(s) here
    MyAwesomeAudioPlugin::extension_data

Aida DSP OS is running a rt patched operative system, so it is possible to enable in the plugin
the hardRTCapable flag. However setting this flag is not mandatory and doesn't affects plugin performance,
is only a plugin "qualifier".


# Graphic interface for the audio plugin

You don't need to develop a graphic interface, since

.ttl files describe the plugin ports (AudioPort, ControlPort) see Gain.ttl.

Aida DSP OS is based on Mod Duo's technology from moddevices which exposes a web server graphic interface. The server
looks for a folder named "modgui" in the plugin directory. This "modgui" is a css graphic object which is mapped
on the .ttl file. The graphic is totally independent from plugin development (i.e. you don't need to start any thread for handling graphic interface
when you instantiate the plugin).


## Build with autotools

e.g. pure-data application

    source environment-setup-aarch64-poky-linux
    mkdir ~/aidadspworkspace
    cd ~/aidadspworkspace
    git clone https://github.com/pure-data/pure-data.git
    cd pure-data
    git checkout 0.49-0
    ./autogen.sh
    ./configure --host=aarch64-poky-linux --enable-jack --enable-fftw
    make -j 8
    file src/pd


## Tips

* I don't remember if I did the source of the environment or not

`$ echo $CC`

aarch64-poky-linux-gcc --sysroot=/localdisk/massimo/Work/Spare/sdk/yocto/sysroots/aarch64-poky-linux
