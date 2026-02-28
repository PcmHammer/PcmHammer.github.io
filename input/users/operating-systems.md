---
Title: The problem
IsPage: true
ShowInNavbar: false
---
# The problem

You can only tune your PCM if you have an operating system that has an XDF file available. The XDF tells Tuner Pro (or whatever tuning app you're using) which values in the bin file are used for which purposes, so that you can view and edit those values.

But XDFs are only available for a few operating systems.  If your PCM has an operating system that has an XDF, then you just get the XDF from one of the repositories here on GitHub, tell Tuner Pro to use it, and you're ready to rock.

If your PCM does not have an XDF available for it, then you have a problem.

# The solution

Change to an operating system that does have an XDF. Changing operating systems is a bit tedious, but you'll only have to do it once.

First, find a bin file for the operating system that you want to change to, and get a version of that operating system that matches you're vehicle's configuration. In particular, make sure that the operating system matches your throttle type (drive-by-wire or cable) and transmission type (manual, 4L60E, 4L80E). There are repositories of bin files here on GitHub, and you'll find links to them below.

Second, make sure that PCM Hammer has a good connection to your PCM, and get a backup of the operating system that's on your PCM. Just tell PCM Hammer to read the entire bin from your PCM. This can take a while, but you'll only need to do it once. 

Third, write the new bin file to your PCM. This will take just as long, but again you'll only need to do it once.

After switching operating systems, future changes will only require changing the calibration segment of the flash chip, which takes only a fraction of the time of rewriting the entire flash ship.

Alternatively you may want to check out Universal Patcher. It has grown beyond just patches and is now able to find various editable items in a bin by analysing its structure and looking for patterns. Some operating systems are very well defined, others have limited ability but which may be enough to disable a code or disable VATs. Once it has found the items in the bin file, it can edit the file directly or generate an XDF. It is also able to export an XDF containing any auto detected items for use with tunerpro. These XDFs can be useful for your own use but are not worth sharing or archiving as there is nothing special about them. https://universalpatcher.net/ and https://github.com/joukoy/UniversalPatcher

# Which operating system should you use?

### For P01 (512kb) PCMs in vehicles that do not need Flex-Fuel

Operating system 12212156 will work for any vehicle (DBW/DBC, MT/AT). 

You can find a few versions of this operating system, and a few XDFs, in [this section of Snoman's Git repository](https://github.com/Snoman002/Engine-Tune-Repository-TunerPro-EFIlive-TunerCat/tree/master/General%20Motors/P01/Software/12212156_Operating_System) 

BoredTruckOwner also has a Git repository, with bin files [here](https://github.com/BoredTruckOwner/LS_Based_Engine_Repository/tree/master/.BIN%20Files/P01_512Kb/Stock/2002/Supported_OS/OS_12212156) and an XDF file [here](https://github.com/BoredTruckOwner/LS_Based_Engine_Repository/tree/master/.XDF%20Files/P01_512Kb)

### For P01 PCMs in vehicles that DO need Flex-Fuel

Warning: This is still new and unproven. 

The only supported operating system for P01 PCMs that supports Flex-Fuel is 12216125.

There are a few bin files in [this section of Snoman's repo](https://github.com/Snoman002/Engine-Tune-Repository-TunerPro-EFIlive-TunerCat/tree/master/General%20Motors/P01/Software/12216125_Operating_System), along with some XDFs. One of the XDFs is tiny (it contains only one parameter) but the other appears to be complete. I haven't tried tuning with these files, so I can't say anything with certainty, but I'd love to hear from anyone who tries it.

There are also bin files - but no XDFs - in [this section of BoredTruckOwner's repo](https://github.com/BoredTruckOwner/LS_Based_Engine_Repository/tree/master/.BIN%20Files/P01_512Kb/Stock/2002/Unsupported_OS/OS_1226125)

### For P59 PCMs

For the P59, use operating system 12587603. It supports cable throttles and DBW hardware (pedal, TAC, throttle body) for model years up to 2005. 

But note that for 2006 and 2007 DBW vehicles, compatibility is unknown at this time. Swapping in the pedal, TAC module, and throttle body from 2001-2005 vehicle might make this OS work in a 2006-2007 DBW vehicle, but I'm not certain of that. If you have tried, please contact me on Facebook (Nate Saforverk).

For bin and XDF files, see [this section of Snoman's repository.](https://github.com/Snoman002/Engine-Tune-Repository-TunerPro-EFIlive-TunerCat/tree/master/General%20Motors/P59/Software/12587603_Operating_System)

For XDF files, see [this section of BoredTruckOwner's repository](https://github.com/BoredTruckOwner/LS_Based_Engine_Repository/tree/master/.XDF%20Files/P59_1Mb). For bin files, see [this section of BoredTruckOwner's repository.](https://github.com/BoredTruckOwner/LS_Based_Engine_Repository/tree/master/.BIN%20Files/P59_1Mb/Stock/2004/Supoorted_OS/OS_12587603)

### Stay with one of these two (maybe three) operating systems

The 12212156 and 12587603 operating systems have good XDF support, and both are available in every combination of throttle type (DBW, DBC) and transmission type (6MT, 4L60E, 4L80E). For that reason, these operating systems will probably be the first, and possibly be the only, to get hacks in the future (2-step, flat-foot-shift, boost, etc). 

12216125 _might_ end up being a better option than 12212156 but it might not. GM probably had to make some trade-offs to fit flex-fuels support into 512kb of memory. It is not yet know whether it 2156 can support all combinations of transmission types and throttle body types. I wish we knew everything and had all of the answers, but that's going to take some time. And some volunteers from the community (hint, hint).

If you change to any other operating system, you are probably going down a dead end. Please don't. Those of us who can create custom operating systems are going to focus our efforts on the operating systems that can help the largest number of people: 2156, 7603, _maybe_ 6125.

Note that if you don't have an XDF for your vehicle's current operating system, and you want to use free tools like PCM Hammer and LS Droid, the lack of XDF means you'll have to tune the new OS from scratch. Or, consider paying someone with HPTuners or EFILive to copy your existing tune into one of the operating systems above.

### Hardware compatibility

All P01 PCMs will work for both throttle-by-wire and cable throttles, however that is not the case for all P59 PCMs. All P59 PCMs will work with electronic throttles, however cable throttles require IAC drivers, which are only present in the following:

Model Year | Service Number | Hardware Number
---|---|---
2003 | 12576106 | 12570558 
2004 | 12586243 | 12583659 
2005-2006 | 12589462 | 12589161 

Also note that the TAC modules used in 2006/2007 vehicles will not work with the 7603 operating system (which was released in 2004). 
