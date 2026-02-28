---
Title: FAQ
IsPage: true
ShowInNavbar: false
---
**Where can I find an XDF for my operating system?**

There are two repositories of XDF files on GitHub.

In Snoman002's repository, look in the P01 and P59 subdirectories, because those are the PCMs that that PCM Hammer supports:

https://github.com/Snoman002/Engine-Tune-Repository-TunerPro-EFIlive-TunerCat/tree/master/General%20Motors

BoredTruckOwner's repository only contains P01 and P59 operating systems:

https://github.com/BoredTruckOwner/LS_Based_Engine_Repository

**What if I can't find an XDF for my operating system?**

You should probably switch operating systems. Please see this wiki page for details:

[Operating Systems](/users/operating-systems/)

**WTF?!?! My car won't start!?!?!**

Don't panic. In most cases everything will return to normal after a minute or so. However, in some cases the PCM will need to be rebooted by pulling the fuse. (Merely turning off the ignition will not suffice, because the PCM will still be powered by the battery.)
    
Currently there is a known issue with the AllPro interface which sometimes leads to this situation. (See the [Supported Devices](users/supported-devices) page.) We're working it, and we apologize for the inconvenience.  
    
Pull the PCM fuse (or fuses), wait 10 seconds, replace the fuses, wait 30 seconds, and everything will be fine.

**Why are two .bin files from the very same vehicle so different?**
    
You might notice that reading the same PCM twice can produce .bin files with very different content in the 16384-32767 address range (0x4000-0x7FFF in hexadecimal). This is not unusual, and does not indicate a problem.  

The PCM uses that address space for dynamic data that needs to persist even when the PCM is powered off, such as the VIN, serial number, and check-engine-light information. The data can be stored in the 16384-24575 (0x4000-0x5FFF) range, or in the 24576-32767 (0x6000-0x7FFF) range. When that data changes, it will initially be written to RAM, then will be copied to one of those ranges in flash. The copy happens after you turn off the ignition key (the PCM will still be powered directly from the battery). If the PCM fuse blows or is pulled during the copy process, one of those ranges may be filled with 0xFF values, but the PCM will simply use the other range until the next key-off event. 

**What about P04 / V6 PCMs?**

Initial exploration suggests that this could be possible without major changes to PCM Hammer, but it would require a new flash kernel. Due to message protocol limitations, the flash kernel basically needs to be loaded in stages, where the first stage gets uploaded in a single short message, and then execute immediately, and load the second kernel (or "the rest of the kernel") into RAM. Sounds good on paper, but hasn't been done successfully yet.

See this thread for more information:

https://pcmhacking.net/forums/viewtopic.php?f=42&t=6574

**What about earlier LS PCMs?**

There is a chance that PCM Hammer could be enhanced to work with earlier PCMs, if they use the same OBD2 variant (J1850 VPW) and a similar set of messages for uploading a flash kernel. It will take a significant amount of work.

The first step would be to open one up, and find out what CPU and memory chips are in it. If the CPU is a variant of the Motorola 68000 series, the odds get better.

You could speed up the reverse engineering somewhat by recording all of the messages that are sent back and forth during a reflash at a dealership or using HP Tuners.

Then someone has to write a "kernel" that runs on the PCM and handles communication and reading / writing the flash chip. 

**What about later PCMs?**

An unrelated project is having some success with E38 reflashing already:
https://pcmhacking.net/forums/viewtopic.php?f=3&t=6666&hilit=e38