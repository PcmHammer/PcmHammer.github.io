---
Title: For Users
BannerTitle: Overview
IsPage: True
ShowInNavbar: true
---
### What is PCM Hammer?

It's free software that will allow you to read and/or modify the flash memory of the General Motors P01 and P59 Powertrain Control Modules (PCMs) which were used in various GM vehicles from 1999 through 2007 using the LS-series V8, or 4.3L V6. 

The list of supported vehicles is [here](/users/supported-pcms/).

This software was developed and tested by volunteers and hobbyists, so be careful with it.

### Who is it for?

It is primarily intended for people who want to tune their cars. However, it is also useful if you simply want to replace your PCM with a new one that already has the operating system that you need - you'll want to read the entire contents of the flash chip from the old PCM, and overwrite the entire flash chip in the new PCM.

You will need a computer that runs Windows. 

### Where can I get it?

Here: https://github.com/LegacyNsfw/PcmHacks/releases

The most recent release will be at the top of that page.

Click "Assets" (below the description of the release) and download the .zip file.   

Extract the contents of the zip file, and run PcmHammer.exe or PcmLogger.exe.

### What else will I need?

You'll need an OBD2 interface that supports J1850 VPW communications (J1850 VPW is the OBD2 variant used by the PCMs that the app supports). [Click here for a list of supported devices.](/users/supported-devices/) Or click the "Supported Devices" link in the sidebar.

You'll need a copy of Tuner Pro, so that you can edit the tune. You can get Tuner Pro from http://tunerpro.net

You'll need an XDF file that tells Tuner Pro where to find the parameters and tables in your PCM's operating system. 

PCM Hammer will show you the PCM's "operating system ID," and you can often find a corresponding XDF file in one of these repositories:

https://github.com/BoredTruckOwner/LS_Based_Engine_Repository 

https://github.com/Snoman002/Engine-Tune-Repository-TunerPro-EFIlive-TunerCat/tree/master/General%20Motors

Every PCM operating system requires a unique XDF file - do not use an XDF file that was created for a different operating system! If there is no XDF for your PCM's operating system, you will need to switch operating systems. See [this wiki page](/users/operating-systems/) for more information about upgrading to a supported operating system.

### Where can I connect with the community of PCM Hammer users?

Please see the PcmHacking.Net forum, specifically the GM sub-forum, here: https://pcmhacking.net/forums/viewforum.php?f=42

There's also a Facebook page: https://www.facebook.com/PcmHammer/

And a Facebook group: https://www.facebook.com/groups/PcmHammerUsers/

### What do the buttons do?

* When you start PCM Hammer for the first time, you'll need to tell it what kind of OBD2 interface you have, using the "Select Interface" button.

* The "Read Properties" button will read several properties of supported Powertrain Control Modules.

For example, it produces this output from a 2002 Corvette:

    [11:27:36:044]  VIN: 1G1YY12S925100000
    [11:27:36:153]  OS ID: 12593358
    [11:27:36:230]  Calibration ID: 9391431
    [11:27:36:326]  Hardware ID: 9386530
    [11:27:36:553]  Serial Number: 1EB1WTDK1232
    [11:27:36:647]  Broad Cast Code: DCPU
    [11:27:36:726]  MEC: 0


* The "Read Full Contents" menu item (under the Tools menu) will read the entire flash-memory contents of a P01 (512kb) or P59) 1024kb PCM. These were used in various V8-powered General Motors vehicles from the late 1990s to middle 2000s. You should be able to open the resulting file in TunerPro to view the contents.

* The "Modify VIN" menu item will let you update the VIN of a newly-purchased PCM to match the VIN of your actual car. This is handy for PCM swaps and for replacing failed PCMs.

* The "Quick Comparison" menu item will compare a file on your PC to the contents of your PCM. To save time, it compares the CRC of each block of flash memory, which takes about 30 seconds. (A byte-for-byte comparison would take 15 minutes or so.)

* The "Test Write" button will walk through the process of writing a new calibration to the PCM, but it won't erase and reprogram the flash chip. This is useful to testing the quality of the connection between your PC and your PCM.

* The "Write Calibration" button will erase and rewrite the calibration section of the flash chip. Don't do this if you depend on the PCM to drive yourself to work - this software is new and while it has worked for those of us who are developing it, we can't yet promise that it will work for everyone.

* The "Write Parameters (Clone)" menu item will erase and rewrite the parameter sections of the flash chip. These sections contain the VIN, serial number, stored OBD2 codes, and so on. This is useful if you're replacing a PCM with one from another car (such as one from from ebay, or from a junk yard).