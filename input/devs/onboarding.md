---
Title: Onboarding
IsPage: true
ShowInNavbar: false
---
Open source projects should have an "onboarding" document that helps contributors-to-be get familiar with the project and the context around the project. Unfortunately, this is ours, and it is admittedly terrible. Please bear with us. This stuff is complex and poorly documented and it's going to take a lot of time and effort to change that.

So far, all we have is this list of things you might want to know, in approximately random order.

### How does the app communicate with the PCM?

It uses the VPW version of the J1850 protocol, which is one of the OBD2 family of protocols. See also:
http://www.fastfieros.com/tech/vpw_communication_protocol.htm

Note that VPW is a bus protocol, and there are other devices on the bus. The climate controls and dashboard, for example. One of the first steps of the reflash process is to tell the other devices to go silent, so that their messages don't interfere with the reflash messages.

### How does the app commmunicate with the OBD2 interface devices?

There are three answers to this...

It supports two devices that use their own slight variations on the ELM protocol, which is a text-based serial protocol. Note that most ELM devices on the market today are not sufficient because they will not support the large messages needed for efficient reading and writing of flash memory.

It supports the AVT-852, which uses a proprietary binary serial protocol. It's quite elegant, but the devices are unfortunately about $250 and the manufacturer doesn't seem very interested in selling to individuals.

It supports J2534, which is a Windows API for OBD2 devices. Tazzi from Envyous Customs wrote the J2534 layer and kindly granted permission to distribute it.

Note that all three of the above are just different ways to send and receive J1850 VPW messages - because that's the only language the PCM understands.

### How do I get a PCM set up on my workbench for test use?

You'll need a power supply that can put out 13 volts. Programming becomes unreliable around 12 volts, so 13 is better.

You'll need an OBD2 connector like the ones found in cars, so that you can hook up your OBD2 interface(s). These are available from lots of online retailers, including Amazon. (These have 16 pins. You'll only need 4 of them.)

You'll probably want a "blue" PCM connector. (These have 80 pins. You'll only need to use 4 of them.)

You'll need to fun a few wires between the PCM, OBD2 connector, and power supply... 

https://sites.google.com/site/sloppywiki/tuning-information/obd2-bench-harness

Note that the workbench is great for testing, but unless you also attach climate controls, and instrument panel, and a few other devices to the VPW bus, it doesn't really match the real world. Getting reliable results with a bench setup is a great milestone, but it doesn't guarantee reliable results in a car. Since there are more devices on the bus in a car, there's more than can go wrong in a car. Message collisions and retransmission, for example. Also, when switching from 1x to 4x mode, the PCM will almost always agree to switch, but other modules might not (for no obvious reason).

### What's this about 1x and 4x?

VPW by default runs at 10.1 bits per second, but it also supports 40.4 bps. The high speed mode is great for reflashing and for reading the entire PCM contents. It doesn't quite cut the down by a factor of four, but it does speed things up a lot.

### What's the Arduino project for?

(At the time of this writing, there is only one Arduino project in the repository.) It lets you connect an Arduino to a VPW bus, and the Arduino will monitor messages, printing them via the Arduino's USB serial port. This is pretty helpful for seeing what's going on when debugging PC-PCM communications.

We need instructions for setting it up.

### What is recovery mode?

If you wipe the calibration from a PCM, but leave the operating system in place, the PCM won't be able to run an engine, but it will respond to enough VPW messages that you can transfer a kernel and re-flash the calibration. A PCM in recovery mode will transmit "8C FE F0 3F" messages every second or so.

### What is BDM?

The acronym expands to "background debug mode" and it's a method of controlling embedded computers via special hardware. If you completely wipe the flash memory of a PCM, you can attach a BDM device (which requires soldering 8 wires) and replace the entire contents of the flash memory. 

You'll need one of these: https://www.usbjtag.com/zenshop/index.php?main_page=product_info&cPath=1&products_id=11

We need to add the instructions to the github repository at some point, just in case.

### What's the CPU inside the PCM?

The PCM has a Motorola 68332 CPU, which is a derivative of the 68030, which is a derivative of the 68000. If you're well versed in computer history (or just old) you might recognize this as the same family as the early Macs, the Sega Genesis gaming console, and the Commodore Amiga.

The CPU details only matter if you want to write code for it and you're stuck with assembly. But, Assembly is how kernel development is traditionally done in projects like this one. Antus wrote the reading kernel in assembly, and another collaborator (not sure he wants to be named yet) is working on a writing kernel in assembly. In between, we tried to use a write kernel created by Dimented24x7 (which he kindly granted permission to distribute), but unfortunately it uses a messaging protocol that doesn't work well with ELM-based interface devices.

NSFW is working on C code, so that little-or-no assembly will be needed. Hopefully. It's looking like we'll have a working assembly kernel soon, so the C thing is starting to look like an art project now... Fun to work on, but not sure if anyone will actually want it.

### Where is the maximum write payload specified?

Lots of places...

* In the kernel code, in common.h: #define MessageBufferSize (4096+20)
* In the Device class there's MaxSendSize property that enforces a maximum that no device can exceed. This should agree with the kernel buffer size.
* In each Device subclass, there's a MaxSendSize set in the constructor.
* In each ElmDeviceImplementation subclasses, there's a MexSendSize in the constructor.


### This page is too short.

Sure is. For further reading, try searching the web for "Dimented24x7 PCM" (without the quotes). He did a ton of the early research and assembly coding that made this project possible, and posted a lot on pcmhacking.net and related forums. But then he disappeared. We just hope he's OK.

Surprisingly enough, there's also some pretty detailed information about PCM communications on the HP Tuners forums from the very early days of that project. 

