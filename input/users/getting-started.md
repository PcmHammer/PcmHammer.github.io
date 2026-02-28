---
Title: Getting Started
IsPage: true
ShowInNavbar: false
---
1. Buy a supported interface. Currently, the OBDX Pro interfaces are the best option (VT, VX, or GT all work equally well). See the [supported devices](/users/supporteddevices/) page for other options.
1. Download a copy of PCM Hammer.
1. Connect your PC to your PCM.
1. Click "Select Device" and choose the COM port and device type.
1. Click "Read properties" and note your operating system ID number.
1. Click "Read Full Contents" and have a sandwich. This can take from ten minutes to an hour, depending on the PCM and interface. You might want to put your car on a battery charger to ensure that you don't run the battery down too far.
1. Save the file, and give the file name a .bin extension.
1. Find an XDF file for your operating system (see note below).
1. Download a copy of TunerPro.
1. Open your .bin file in TunerPro.
1. Select your XDF file.
1. Look through the tables. There are many. You won't need to touch all of them, but you should get familiar with what's there.
1. Open PCM Logger. Pick a log profile, drive around, make some data logs.

***

PCM Hammer will pull the code and data from your PCM, and Tuner Pro will edit the contents... but Tuner Pro requires an XDF file to tell it where to find the various tables and constants that govern how the engine runs. XDF files are specific to each revision of GM's powertrain operating system. GM made a lot of operating systems, and XDFs don't exist for all of them (yet?) but there is a growing collection of XDF files here:

[https://github.com/BoredTruckOwner/LS_Based_Engine_Repository](https://github.com/BoredTruckOwner/LS_Based_Engine_Repository)

If you don't see an XDF for your operating system, try searching the web. And if you find one, please submit it to the repository to help anyone else who needs it.

Also, can learn a lot from forums like pcmhacking.net and gearhead-efi.com. Don't be afraid to ask questions!

If you would like a book to read, I highly recommend "Engine Management: Advanced Tuning" by Greg Banish.