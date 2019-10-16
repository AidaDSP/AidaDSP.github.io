---
image: assets/images/sfz_logo1.png
description: Create your own soundfont in sfz format
---

## How-to: sfz

## Introduction

FAQs:

1) **What is it SFZ?**

SFZ is a plain text file format that stores instrument data for software synthesizers. See full Wikipedia's [page](https://en.wikipedia.org/wiki/SFZ_(file_format)

2) **Can I play SFZ soundfonts on Mac/Windows?**

Sforzando

3) **Are SFZ soundfonts better that other soundfonts?**

No, the final quality of a soundfont is determined by the quality of the job done by the sound designer who recorded the samples. Although we may say
that SFZ is a very flexible and open format, and has advanced features that make it compete with some well known commercial
formats like komplete

4) **Why another soundfont format? I have komplete and I'm done with it...**

So you pay for samples that you do not own, since you can play them only through their proprietary player that runs
only on certain machines. SFZ is an open format, that means that you can use the program you want to play them, the only
requirement is that this program needs to support SFZ format.


## So what is it .sfz?

When you refer to a soundfont, you refer to a file that can be loaded by your favourite sample player. A soundfont/instrument in SFZ format
is a directory with this structure:

    harpsichord
    ├── B3.wav
    ├── B4.wav
    ├── B5.wav
    ├── Bb1.wav
    ├── Bb2.wav
    ├── D2.wav
    ├── D3.wav
    ├── Eb4.wav
    ├── Eb5.wav
    ├── Eb6.wav
    ├── G3.wav
    ├── G4.wav
    ├── G5.wav
    ├── Gb2.wav
    ├── harpsichord.sfz
    └── license.txt

you have a list of wav files that are actually the samples (i.e. a single notes of a piano recorded from attack to end of decay) and a file with .sfz extension that is where the magic happens. This file is a map between notes and samples and is a structured document, like html for example, with regions identified by specific tags and syntax. Let's see the content of **harpsichord.sfz**:

    <group> ampeg_release=.2 ampeg_sustain=.01 ampeg_decay=60
    <region> sample=Bb1.wav pitch_keycenter=a#1 hikey=c2
    <region> sample=D2.wav lokey=c#2 pitch_keycenter=d2 hikey=d#2
    <region> sample=Gb2.wav lokey=e2 pitch_keycenter=f#2 hikey=g2
    <region> sample=Bb2.wav lokey=g#2 pitch_keycenter=a#2 hikey=b2
    <region> sample=D3.wav lokey=c3 pitch_keycenter=d3 hikey=e3
    <region> sample=G3.wav lokey=f3 pitch_keycenter=g3 hikey=g#3
    <region> sample=B3.wav lokey=a3 pitch_keycenter=b3 hikey=c4
    <region> sample=Eb4.wav lokey=c#4 pitch_keycenter=d#4 hikey=e4
    <region> sample=G4.wav lokey=f4 pitch_keycenter=g4 hikey=g#4
    <region> sample=B4.wav lokey=a4 pitch_keycenter=b4 hikey=c5
    <region> sample=Eb5.wav lokey=c#5 pitch_keycenter=d#5 hikey=e5
    <region> sample=G5.wav lokey=f5 pitch_keycenter=g5 hikey=g#5
    <region> sample=B5.wav lokey=a5 pitch_keycenter=b5 hikey=c6

where

* `<group>` parameters that affect multiple regions: in this soundfont we have global release, sustain and decay
* `<region>` since a single sample can be mapped to multiple notes, they are called regions more than notes or sounds.

This is the pattern that maps the sample to a note:

* _**sample=**_ wav or flac file
* _**key=**_ or _**lokey=**_ _**hikey=**_ _**pitch_keycenter=**_ note


## Okay thanks for the theory, how can I create my soundfonts?

https://www.polyphone-soundfonts.com


## Where I can download some SFZ samples?

1. Free (may require registration)
  * https://www.polyphone-soundfonts.com/en/download-soundfonts
  * http://ariaengine.com/free-sfz-sounds/
  * https://www.laptopmusician.net/2019/06/the-ultimate-free-sfz-instruments-list.html
  * google is your friend

2. Non-free
  * https://www.loopmasters.com/formats/15-SFZ
  * your favourite samples store could already have samples in SFZ format, check it out!


## Additional resources and documentation

- https://sfzformat.com/
- https://www.linuxsampler.org/sfz/
