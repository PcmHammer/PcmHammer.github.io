---
Title: Disclaimers
IsPage: true
ShowInNavbar: false
---
### Disclaimers

Everything written in this entire wiki is based on observations. Nothing here should be taken as a promise. Use this information at your own risk.

### PCM Types

Family | Flash Memory | Years | Part numbers
---|---|---|---
P01 | 512kb | 1999-2000 | 896
P01 | 512kb | 2001-2003 | 411
P59 | 1024kb | 2003-2007 | Various

Note that different models switched PCM types in different years.

The P01 PCMs have red and blue connectors.

The P59 PCMs have green and blue connectors.

### Mixing and matching

An operating system from a 411 PCM can usually be flashed onto an 896 PCM. In some cases the serial number and VIN will be corrupted, but this can usually be fixed.

Flashing an 896 operating system onto a 411 PCM usually works when done as part of a complete rewrite of the flash chip, however if you flash the operating system alone, that is likely to leave the 411 unusable without hardware hacking.

### Recovering from a bad flash

Depending on exactly what went wrong, a PCM can enter different modes of broken-ness. If you simply erase a section of the flash chip, the PCM will enter a mode in which it won't run the engine, but it will (very easily) allow you to reflash. 

However, if you write a section that has a bad checksum, the PCM will respond to most commands on the OBD2 bus, but it won't allow you to reflash it. (Perhaps the GM engineers assumed that a bad checksum indicates a faulty flash chip, which needs to be replaced rather than merely reflashed?) To work around THAT problem, you'll need to remove the PCM from the vehicle, pop off the bottom cover, and very carefully ground one pin on the back of the circuit board.

Watch this video for details:

https://www.youtube.com/watch?v=oGeMK6LvQck

Note that 512kb PCBs look *slightly* different, but the workaround is still the same.

### Credit

Thank PeteS160 from LS1Tech and various folks on Facebook for this information.

### A brief note about Araxis merge

Araxis provides no-cost licenses for their diff/merge tools to open source developers.

[Click here for details.](https://www.araxis.com/buy/open-source)