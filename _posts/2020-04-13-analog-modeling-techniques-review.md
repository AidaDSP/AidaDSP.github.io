---
layout: post
title: "Analog modeling techniques review"
---

In this article I'll try to make a review of the current available
analog modeling techniques that are used extensively both in hardware (digital stompboxes or pedalboards)
and in software plugins.

I'll do this by reading of currently published papers on the argument and try to make connections with
commercially available products, and finally try to classificate them by technologies used.

# White-box vs black-box

White-box modeling is based on circuit analysis and simulation.
Such models exhibit a high degree of accuracy, but require detailed knowledge of
the circuit and its nonlinear components.

Black-box modeling is based on input-output measure-
ments of the device under study. Black-box can be used to emulate different nonlinear systems,
but it typically fails to emulate the system as accurately as a
white-box model, leading to an audible difference between
the model and the device under study.

# The problem

Historically, the first approach that has been used and investigated by audio effects programmers
was white-box modeling, because numeric methods to solve differential equations were already known for their
application in circuit simulation programs such as _Spice_.
The problem, with early implementations as well as today, is that processors don't have
enough computation power to solve the equations involved with such analog circuits (i.e. a guitar amplifier) in real time, or if you prefer
complete the calculation of each voltage or current in the circuit nodes at the frequency requested by an high
quality A/D to D/A conversion. That's why various techniques to aproximate the solution of the most
complex parts of the analog circuits have been developed. And that's why we are always referring to the digital as a
simulation, and people claims they're hearing differences between analog, real circuits and their digital counterparts.

# Waveshaping

In a paper from 1979 [1] this technique and its application in music synthesis was described for the first time. Since is simple
in concept and very fast to compute, it's still in use today. To change the armonic content of the input waveform we can multiply
the signal in the time domain with a known function that is typically very similar with the figure below:

![arctan(x)](arctan-1.png)

It's common to refer to the family of these functions as _**'static nonlinearities'**_. Since you can have pretty much an infinite number
of functions with a shape similar to this, and since you can combine them with extensive filtering in pre and post (or you can apply a different function for each frequency band)
the problem relies in isolating the functions that sounds good when applied to a guitar signal.

# Physically-informed waveshaping

A non-linear analog circuit such a guitar amplifier (JTM45) or a stompbox (TS9) can be approximated
by dividing it into blocks, separating the linear part, that can be represented by a n-order IIR digital filter
from the nonlinear part which can be be obtained from numerical solution of the circuit [2]. For example see the figure below
representing the TS9 overdrive effect:

![TS9](overdrive-effect-1.png)

Althought this technique it's still used today, suffers from one main problem:

* approximation of all nonlinearities as _**'memoryless'**_ or _**'static'**_

In real analog circuits we usually have on or more reactive components (capacitors, inductors) which are part
of the nonlinear differential equation that describe the circuit's transfer function. In other words, the distortion curve changes with amplitude and frequency of the input signal,
but we are approximating it as a function of the amplitude only.

For example, looking at the figure below, you can see that _**Vo**_ is the voltage accross _**C**_ and thus the output
voltage depends on the _**'history'**_ of the input signal:

![diode-clipper](diode-clipper-1.png)

To model the nonlinear transfer function as static, the circuit is approximated by eliminating _**C**_. This technique can leads to a small or big deviation
from the original response depending on the actual circuit involved. A key design point is to measure this deviation and try to keep it sufficiently low, so it is unlikely
that is noticed.

# Aliasing

Distortion adds or emphasizes harmonics of the original signal, altering the timbre of the original source. But this also means the base band of the original
signal is expanded from 20kHz to something higher. If the new harmonic content introduced by the nonlinear function exceeds the Nyquist frequency of the system
the aliasing effect may become audible: without being too much technical, let's say aliasing is when one or more artifacts that sounds unpleasant and unnatural are produced.

You can find an exaustive video [here](https://www.youtube.com/watch?v=XoVhNhi76Qk) on the aliasing effect in audio.

To avoid aliasing the waveshaping technique often introduces an upsample block before the nonlinear function and a downsample
block immediately after. So if the system sampling frequency is 48kHz, internally the algorithm elevates it to 96kHz (2x) 192kHz (4x) or 384kHz (8x). The scope of the downsample
block is the opposite: to return back to the original system sampling frequency (48kHz) for compability.

Aliasing is a CPU-intensive task, because the algorithm will run at 2x, 4x or 8x. Since the guitar's voice is well below 12kHz (someone says 6kHz) we can avoid upsampling
by introducing a low-pass filter before the nonlinearity. In addition to that we can rise the overall system sampling frequency to still have the 8x factor (96kHz/12kHz=8).

See the image below for example:

![anti-aliasing](anti-aliasing-1.png)

# Wave digital filters



# Profiling

# Deep learning

# Marketing vs transparency, closed source vs open source

---
**NOTES**

A more detailed mathematical analysis is out of scope for this article, and will be the central topic in dedicated future posts.

1. C. Roads. A Tutorial on Non-linear Distortion or Waveshaping Synthesis.
2. T. Yeh, J. Abel, and J. O. Smith. Simplified, physically-informed models of distortion and overdrive guitar effects pedals.

---

[Go to the Home Page]({{ '/' | absolute_url }})

