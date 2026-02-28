---
Title: Flex Fuel
IsPage: true
ShowInNavbar: false
---
I don't have ethanol readily available, so I don't have much personal interest in Flex-Fuel, but people keep asking me about it. Please don't ask me. What little I know is on this page - as well as some stuff that I'm not even sure is correct. The answer you're looking for might be in one of the threads I've linked to. I'll update this page as I stumble upon stuff that belongs here.

This thread the best resource I know of for setting up Flex-Fuel with a P01 (aka 411) PCM:

https://ls1tech.com/forums/pcm-diagnostics-tuning/1734778-gen-iii-flex-fuel-write-up.html

One of the key things is operating system ID 12216125. This was used in the 2002 Tahoe, which had Flex-Fuel capability from the factory. 

There are a few bin files in [this section of Snoman's repo](https://github.com/Snoman002/Engine-Tune-Repository-TunerPro-EFIlive-TunerCat/tree/master/General%20Motors/P01/Software/12216125_Operating_System), along with some XDFs. One of the XDFs is tiny (it contains only one parameter) but the other appears to be complete. I haven't tried tuning with these files, so I can't say anything with certainty, but I'd love to hear from anyone who tries it.