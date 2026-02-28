---
Title: Background Debug Mode
IsPage: true
ShowInNavbar: false
---
# Background Debug Mode

## Who cares?

This is mostly useful to people who are working PCM Hammer itself - adding support for new PCMs, improving the kernels, etc. But it might be use for non-developers who do a LOT of flashing and want a way to recover PCMs that have been bricked by bad writes - corrupted data, incorrect OS for the hardware, incomplete / interrupted flash, etc.

BDM gives us second way to read or (more importantly) write the flash chip. The drawback is that you have to take the PCM out of the car, remove the back from the PCM, and attach several wires.

This is a bit tricky. It's not for everyone. 

What is it? https://en.wikipedia.org/wiki/Background_debug_mode_interface

What hardware do you need? https://www.usbjtag.com/zenshop/index.php?main_page=product_info&cPath=1&products_id=11

## How do you hook it up? 

See this thread: https://pcmhacking.net/forums/viewtopic.php?f=42&t=6215&start=50

If you're only going to do this rarely, it might make sense to solder directly to the PCM. If you're going to be doing this regularly, you might want a jig so that you can skip the soldering. But note that pogo pins have their own reliability issues (the pins might stick, they might slip in the jig and not make good contact, etc) so there are drawbacks to both approaches.

See this page for wiring details: http://www.usbjtag.com/jtagnt/ecu411/index.php

This jig can be 3D-printed: https://www.thingiverse.com/thing:3565197

The jig requires pogo pins. I used these: https://www.amazon.com/gp/product/B07HC5VKVT/

Those are no longer available, but pogo pins in general are not hard to find, and the size isn't critical. However if you use pins with a different diameter, you might need to adjust the hole sizes in the jig. In fact, the same size pins might not fit properly due to variations in printers and filament. 

## How do you use it?

Read this first: https://www.usbjtag.com/jtagnt/usbjtagnt.pdf

1. Solder to the board, or attach the fixture with the UsbJtag to the board.
1. Plug the UsbJtag device into your computer.
1. Apply 12v power to the board.
1. Register/activate the UsbJtag device. Sorry for the lack of detail here, I did it months ago.
1. Click the settings button (gear and wrench icon) and pick Category:ECU, Protocol:BDM, and then pick Target:ECU411 (if you are using a P01) or ECU4111M (if you are using a P59)
1. Click the ID button in the UsbJtag app. You should see something like "Found Address= 00000000 29F800BB". If you see no response, or if you see "Report these values http://www.usbjtag.com/phpbb3 0000h,0000h" then you've soldered to the wrong places or not all of your pogo pins are touching the circuit board.

To write: 

1. click the file-open button (looks like a folder containing a sheet of paper) 
1. click the Write button (has a "W" on it). 
1. after writing, verify the result by clicking the Verify button (has a question-mark and a "V"). 

Note that it is normal for the "program speed" indicator in the status bar start around 12 and steadily drop during the write. Don't be alarmed.

To read: 

1. click the Read button (has an "R" on it)
1. click the Save button (looks like a 3.5" floppy disc (remember those?))