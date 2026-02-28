---
Title: Logger XML Files
IsPage: true
ShowInNavbar: false
---
Originally posted at [PcmHacking.net](https://pcmhacking.net/forums/viewtopic.php?f=42&t=7467&p=110055#p110055).

# Background

There are two ways to request a value from the PCM:

1) Request a value by parameter ID. The SAE defined a bunch of parameters, and I think GM extended the SAE's list. The convenient thing about this approach is that the parameter IDs are standard across all operating system. If you ask for parameter ID 0005 you will get engine coolant temp no matter which OS the PCM is running. Not all PCMs support all parameters, but there's a pretty long list of parameters that are supported by most operating systems. That's what you will find in **Parameters.Standard.xml**.

2) Request a value by RAM address. These addresses are unique per operating system - different operating systems mostly work with the same values, but they store them in different places in RAM. Since the addresses are unqiue per operating system, I figured we should have a separate file for each operating system. When you start the logger, it checks your OS and looks for a file named Parameters.YOUR_OSID.xml. Then it populates the parameter list with the standard parameters and whatever was in Parameters.YOUR_OSID.xml (if it found one).

My Corvette was running 12593358 at the time, so I made **Parameters.12593358.xml** to describe the RAM addresses for that operating system. (I plan to switch to 7603 soon.)

In many cases there are RAM values that correspond to the standard parameters, but with higher precision. For example the standard parameter might be one byte, but the RAM parameter might be 2 or 4 bytes.

In many cases, there are values in RAM that do not have a corresponding standard parameter. When I was working on the logger I was also tuning idle, so I found the RAM values for the proportional, integral, and derivative terms of the feedback loop that manages the throttle blade angle. I don't think there are standard parameter IDs for any of those.

With enough reverse engineering we should be able to find RAM parameters for everything anyone could want. It takes a lot of time to do that reverse engineering, so I encourage people to run the 2156, 6125, or 7603 operating systems. I'll be working on finding RAM parameters in 7603, and I'm guessing that we'll have volunteers to work on 2156 and/or 6125. For other operating systems, I think the odds of getting reverse engineered are much lower. (To be honest I'd kind of like to see the P01 standardize on either 6125, to reduce the number of operating system to be reverse engineered even futher, but I'm not sure that's practical. 6125 has flex-fuel, but I wonder if GM had to trade off anything interesting to make room for the flex-fuel code or data.)

# Math Parameters

These let you log a value by doing math on two other values. For example you can calculate injector duty cycle by doing some math on RPM and pulse width, or you can get grams-per-cylinder by doing math on RPM and MAF. That's what you'll find in **Parameters.Math.xml**.

Parameters.DidNotWork.xml is just me taking notes of stuff I tried, in hopes of not making the same mistakes again in the future. The software doesn't use it.

# CAN Parameters

Parameters.CAN.xml is where you define the parameters that are available on your CAN bus. 

CAN logging is still pretty new, so there are only a few parameters defined here so far. Hopefully the examples are instructive.
