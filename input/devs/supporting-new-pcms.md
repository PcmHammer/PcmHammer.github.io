---
Title: Supporting New PCMs
IsPage: true
ShowInNavbar: false
---
In theory, PCM Hammer can be extended to support other GM PCMs, perhaps even Saab PCMs from the era when the hardware was similar. A number of questions will have to be answered for each new PCM, and some new code will probably need to be written, but for PCMs that use Motorola 68000-based CPUs and J1850 VPW communications, there's a good chance that support can be added.

But it will take a lot of research, trial-and-error, and software development to make it happen. The VpwExplorer app can be used as a testbed for experimental code that might help with your research.

You can get a big head start (in fact, this might be a prerequisite) by obtaining the raw firmware from the PCM you want to support. If you're lucky, there might be a file somewhere on the internet already. If you're not lucky, find out what it would take to desolder the flash chip and dump the contents to a file using your PC. You're probably going to need to reverse engineer some of it:
* the code that sends and receives messages over the VPW bus
* the code that writes data to RAM and executes it
* the code that writes data to flash memory (to store OBD2 fault information)

# Basic Steps

### Establish communication with the PCM

If PCM Hammer can read the VIN and OS ID, great. If not, you might be better off starting from scratch.

### Unlock the PCM

You can read the VIN and OS ID just by sending simple requests, but in order to read and write the entire firmware you need to write a kernel, upload it to RAM, and execute it. And before you can upload a kernel, you need to unlock the PCM by sending the correct key value for the PCM's seed value.

### Write a "hello world" kernel, upload it to RAM, and execute it

In order to know if your kernel is executing, you'll need to have kernel code that can send messages over the VPW bus. This was the most challenging part of PCM Hammer development, because until you can send messages over the bus, you can't tell what (if anything) your code is doing. Once we had code that could send messages, the rest was much easier.

### Extend the kernel 

Add code to read the contents of the EEPROM. Add code to write to the EEPROM.

# Questions that will come up

### What is the seed/key algorithm?

In the PcmLibrary\Misc\KeyAlgorithm.cs file you'll find 256 GM seed-key functions, and an API to use them. Try all 256, and see if one of them unlocks your PCM. If it does, great. If it doesn't, you'll just have to try every possible key value, which could take a while. 

### What RAM address should the kernel be uploaded to?

If you can read the flash chip via external means, you can reverse engineer the code to find out where RAM is, and reverse engineer the 'block write' message handler to find out what the allowable address ranges are. 

It might be possible to figure this out by following traces on the PCB. 

Either way, it's going to be a challenge.

### How big can the kernel be?

With the P01 and P59 PCMs, the kernel can be quite large. We upload it in multiple chunks and the start executing it after the last chunk is uploaded. With the P04, you get one chunk which begins executing as soon as it is uploaded. This is the big obstacle to P04 support right now. Someone needs to write a tiny kernel that can upload more code into RAM, then use that kernel to upload the complete kernel. It seems like a solvable problem, but it's quite a challenge.

### How will the kernel communicate over the V1850 VPW bus?

If you're lucky, the code in the PCM Hammer kernel will just work. If not, this is probably something that needs to be reverse engineered from the factory firmware. Trial-and-error isn't practical. 

### How will the kernel write to the flash chip?

The datasheet for the flash chip will help. Reverse engineering the factory firmware will also help.

# What if my vehicle doesn't use VPW?

Adding support for other PCM families will be hard. If you are prepared to spend months of weeks working on it, we can help a little bit. Your best bet is to start a thread on PcmHacking.net to describe the vehicle and ECU / PCM and hopefully meet some other folks with similar interests to collaborate with.

It's a hard problem and you'll have to attack from different directions at once.

## Hardware reverse engineering

Open the ECU and find out what kind of CPU is in there, because you might have to write code for it.

Also find out what kind of flash memory chip is in there, because you might have to write code to read / erase / write it.

Get datasheets for the ECU and flash.

## Software reverse engineering

Look for a debugging tool for the CPU in the ECU.

Use it to dump the contents of the flash chip.

Open the software in IDA Pro or Ghidra.

## Protocol reverse engineering

Find out what protocol is used to communicate with the ECU, get something that can monitor the messages.

Record the messages that get sent/received during a software update, probably at the dealership.

Figure out what those messages are doing. This might be hard.

Write software that emulates the dealership's flash tool. This might be hard. That tool might be sending code to the ECU that runs during the flash process. It might suffice to just re-use that code at first, but if you want to release an open source tool you'll need to write your own from scratch.

After you have flashing working, then there's the matter of finding all of the tables that you edit to tune the car. This is more software reverse engineering.

And you'll also want to be able to do data logging. If you can find an existing data logging tool (dealerships might have one) you can start with protocol reverse engineering. If not you'll have to reverse engineer the firmware to find the data logging stuff. We lucked out in that other people had already done some of that work for GM ECUs.

It's a big undertaking. If there's a forum for your make/model, ask if there are any people there who would be willing to tackle this problem. Software development skills help a lot, but it's not necessarily a requirement if someone has enough motivation.