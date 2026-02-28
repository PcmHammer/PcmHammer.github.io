---
Title: Read And Write Times
IsPage: true
ShowInNavbar: false
---
Device | 512k Read | 1mb Read | 96kb Calibration Write | 512k Write | 1mb write
---|---|---|---|---|---
ObdLink SX | 30:00 | ?:?? | 4:15 | expect over an hour
ObdLink LX | 11:20 | ?:?? | 2:40 | expect 30 minutes | 14:50
AllPro | 4:38 | ?:?? | 1:33 | 4:51 | ?:??
AVT | ?:?? | ?:?? | ?:?? | ???
Xpro, Bluetooth | ?:?? | 5:17 | 0:37 | ?:??
XPro, USB | 2:12 | 4:25 | 1:40, was 1:00, was 0:32 [1] | ?:?? | 6:12

All times are MM:SS. And they're approximate. And some of them are from my memory, which might be faulty.

Note that 1mb chips have the calibration spread across two blocks, so if you only change one of them, that will cut the calibration write time roughly in half.

?:?? means that I haven't tried it (I don't own an AVT) or haven't tried it since retuning the app's timeouts (which made a huge difference) or I did try it but I didn't take notes.

[1] CRC slowdown might be part of the problem, but there must be more to it than that.