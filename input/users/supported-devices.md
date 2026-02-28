---
Title: Supported Devices
IsPage: true
ShowInNavbar: false
---
As of August 2021, the following devices are supported, with the following known issues:

* OBDX Pro VT - This device is the brain-child of two PCM Hammer collaborators (Tazzi & PeteS) who thought they could build something with the high speed of an AVT or J2534 device, at the price point of an ObdLink device. And that's exactly what they did. They are for sale here: http://obdxpro.com but supply-chain issues mean that they arrive in batches, which sell out quickly. Consider getting onto the waiting list now, and buying one of the devices below while you wait.

* ObdLink ScanTool LX (preferred) or MX+ or SX (both slow, but they do work) - These devices are supported, however they do not support high speed / 4X communications, so a full read of a 512kb PCM will take roughly 30 minutes (longer with the SX). That's long enough that we advise using a Battery Tender or similar device to ensure that your battery doesn't die. However these devices are inexpensive and readily available. (To be clear, the ScanTool MX+ is supported, the MX (without plus) is not supported.)  The LX uses bluetooth, but has been very reliable. The SX uses USB and is very inexpensive, but it is also the slowest option.

* AVT 852 - These devices are fully supported, and the only drawbacks are the price and the process of acquiring one. They cost about $275 and are only available from the manufacturer, and the manufacturer does not have an online store so you have to email them.

* ObdDiag AllPro - We expected this to be the most popular device because it costs less than $40 shipped, and supports high speed VPW communications (40kb/second, also known as "4X mode"). However, they're now out of production.

    The AllPro does have one shortcoming, though. When the app requests all modules in the vehicle to switch to high speed, the AllPro only receives five or six responses, even though there may be a dozen modules. As a result, the app will sometimes enter high-speed mode enough though one of the devices refuses the request to switch speeds (typically, the BCM). With different devices trying to communicate at different speeds, the or write attempt will fail before it even starts. The app will detect this, and in most cases everything will return to normal after a minute or so. However, once in a while the PCM will need to be rebooted by pulling the fuse. (Merely turning off the ignition will not suffice, because the PCM will still be powered by the battery.)

* Any J2534 device - In theory, any of them should work, however there seems to be a conflict between the Windows Store and some J2534 device drivers, so you may need to get PCM Hammer / PCM Logger from the .zip file releases rather than from the Windows Store. Some J2534 devices do work with the Windows Store, for example the Bosch MDI2 (there are mixed reports regarding Bosch MDI2 clones, however).

The VxDiag VCX Nano is J2534 devices, available for about $125 on Amazon, which many people are using. There are two or three versions of the VCX Nano - make you sure you get the one that is compatible with General Motors vehicles. You will need to get PCM Hammer / PCM Logger via .zip file in order to use them with the VCX Nano. 

There are no ELM / ELM 327 devices in this list. 

Unfortunately there are so many low-quality knock-offs that it has become hard to find a good one, so we haven't tested with any. If you find one that works, let us know by filing an issue above. 

Be sure to indicate exactly who made the device you're using, and what model it is, and where you bought it, so that other people will have a good chance of getting exactly the same device.  If you report that "it works with an ELM 327 that I bought on ebay," that won't actually help anyone. Ebay is not a manufacturer. The app **won't** work with other ELM 327 devices that are being sold on ebay, so if you have something that works, people need to know the specific make and model that you've got.