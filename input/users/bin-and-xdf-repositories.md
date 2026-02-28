---
Title: .bin and XDF Repositories
IsPage: true
ShowInNavbar: false
---
# What are bin files?

When you read a PCM's flash chip with PCM Hammer, the contents of the flash chip are saved to a file on your PC. We traditionally use the .bin file extension for these files. They contain an exact copy of the flash chip, which includes all of the code (operating system) and data (calibration) that the PCM uses to control a vehicle's powertrain.

# What are XDF files?

The .bin file is just a long series of bytes. There is nothing in the .bin file to indicate which bytes serve which purpose. In order to edit the calibration, programs like Tuner Pro need to know which parts of the .bin file correspond to the tables and parameters that make up the calibration. The XDF file contains that information. 

In order to update the calibration information in a .bin file, you will need the XDF file that matches the operating system in the .bin file. 

The parameters and tables are not located in the same places in all of the .bin files, so **do not** use an XDF file for one operating system to edit a .bin file for another operating system. You will probably corrupt the contents of the bin file if you do. 

# Where are they?

There are two collections of .bin and XDF files on GitHub. They are managed by different people, and they are organized differently, but they mostly contain the same files. But since they are managed by different people, they won't always be in sync, so you might want to check both of them if you're looking for a specific file.

https://github.com/Snoman002/Engine-Tune-Repository-TunerPro-EFIlive-TunerCat/tree/master/General%20Motors

https://github.com/BoredTruckOwner/LS_Based_Engine_Repository

# What if you can't find the one you want?

Even if you can find the XDF for your PCM's operating system, you might still be better off switching to one of the most-used operating systems. They will have the best XDF support over time since that's where most of the reverse engineering will be happening.

See this page for details:

/pages/operating-systems/