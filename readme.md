# ZITA-REV1

*zita-rev1* is a digital reverb audio effect developed by Fons Adriaensen at
Kokkini Zita, presented here in a stripped-down version, easy to include in
your own DSP projects.

The source code in this repository is licensed under the GNU General Public
License version 2 as stated in the [license document](license.md).
Apart from zita-rev1, Adriaensen has a great collection of DSP projects
available on the [Kokkini Zita website](https://kokkinizita.linuxaudio.org/linuxaudio/).

Reverb makes everything sound better. Especially computer-generated sound, which
usually sounds a bit cold in digital, needs some reverb to make it appear more 
natural and organic.

Though reverb algorithms can be easy to implement, they are notoriously hard to
tune and make sound good due to the high number of parameters. Therefore, it
is nice to have a lightweight, pre-made reverb algorithm that is easy to include
in your project.

## Usage

To use zita-rev1, include the *.cpp* and *.h* files from the *source* folder in 
your project (VS, XCode, JUCE, Makefile, etc.).

Include the reverb header in your source file:

```
#include "reverb.h"
```

Instantiate the reverb class somewhere:

```
Reverb reverb;
reverb.init(44100, false);
```

This will instantiate the reverb algorithm at a sample rate of 44100Hz,
ambisonics disabled.
The reverb is already setup with nice parameters and can be used right away.
Look at the `set_{some parameter}` methods *reverb.h* and
[this page](https://kokkinizita.linuxaudio.org/linuxaudio/zita-rev1-doc/quickguide.html) to
get a feel for which parameters can be tweaked.

Given input samples `xl`, and `xr` for the left and right channels, the reverb
effect is applied like so:

```
// Pack input variables in array.
float *reverbIn[2] = {&xl, &yl};

// The variables will contain the output of the reverb.
float yl, yr;
float *reverbOut[2] = {&yl, &yr};

// Prepare to process one sample.
reverb.prepare(1);

// Process one sample (output can afterwards be read from yl and yr).
reverb.process(1, reverbIn, reverbOut);
```
