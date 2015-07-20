# OwlProgram
Dynamically loaded OWL program.
See http://hoxtonowl.com for more details of the Open Ware Laboratory.

# Instructions

## Prerequisites
* gcc arm compiler (to make patch binary) [1]
* FirmwareSender (to make sysex and run) [2]
* emcc (to make web) [3]
* faust2owl (to compile FAUST patches) [4]
* Enzien Audio account (to compile PD patches) [5]

## Make targets
* make patch: build patch binary
* make sysex: package binary as sysex
* make run: upload patch to attached OWL
* make store: upload and save to attached OWL
* make web: build Javascript patch

## Make options
* PATCHNAME: specify name of patch, e.g. SimpleDelay
* PATCHCLASS: name of patch class, e.g. SimpleDelayPatch
* PATCHFILE: name of main patch file, e.g. SimpleDelayPatch.hpp
* PATCHIN: number of input channels, default 2
* PATCHOUT: number of output channels, default 2
* SLOT: user program slot to store patch in, default 0

If you follow the convention of SimpleDelay then you don't have to specify `PATCHCLASS` and `PATCHFILE`, they will be deduced from `PATCHNAME`.

## Building C++ patches
First copy all patch files to `PatchSource` folder, then issue the appropriate make command.

Example: Compile and run the TestTone patch, defined in file `PatchSource/TestTonePatch.hpp` as class `TestTonePatch`:
`make PATCHNAME=TestTone run`

Example: Compile and run in browser
`make PATCHNAME=TestTone web`
Then open `WebSource/patch.html`

## Building FAUST patches
To compile and run a FAUST patch
* copy .dsp file and dependencies into `PatchSource`, e.g. `LowShelf.dsp`
* `make PATCHNAME=LowShelf faust run`

Note: assign OWL parameters with slider metadata: `[OWL:PARAMETER_A]`, `[OWL:PARAMETER_B]` et c. For example:
```gain = vslider("gain[OWL:PARAMETER_C]", 1,0,1,0.1);```

## Building Pure Data patches
Requires an account with Enzien Audio [5]

To compile and run a PD patch, with C code generated by Enzien Audio:
* make a Heavy project called `owl` and compile your PD patch to C
* download and unzip the Heavy C code into `PatchSource`
* `make PATCHNAME=Heavy run`

Or, using the Heavy uploader (recommended):
* ensure you have a Heavy project called `owl`
* put your PD patch file (e.g. `Foo.pd`) into `PatchSource`
* `make HEAVYFILE=Foo.pd heavy run`
* enter username and credentials when prompted (first time only)

Note: assign OWL parameters with PD receivers called `Channel-A`, `Channel-B`, et c.

# References
[1] https://launchpad.net/gcc-arm-embedded
[2] https://github.com/pingdynasty/FirmwareSender
[3] http://emscripten.org
[4] http://faust.grame.fr/
[5] https://enzienaudio.com