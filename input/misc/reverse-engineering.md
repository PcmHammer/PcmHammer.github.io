---
Title: Reverse Engineering
IsPage: true
ShowInNavbar: false
---
This page is far from finished.

**How do I create an XDF for my operating system?**

**How do I add new parameters to the XDF that already exists for my operating system?**

These are really the same question, and there are two ways to interpret the question:

**How does one add a parameter or table to an XDF?** This is pretty straightforward if you're starting with an unlocked XDF.  If the XDF is locked, then you'd best find an unlocked version. If the XDF is unlocked (and at this point I think there are unlocked XDFs available for most operating systems) then you can use Tuner Pro itself to add new parameters and tables to the XDF. TunerPro has dialog boxes where you can enter the necessary information. Or you can do it by editing the XDF file with a text editor, if you're comfortable with XML.

Please submit your changes to the XDF repository so that everyone else can benefit too. The more people we have working together on this stuff, the more we will all benefit.

**How does one get the information needed to correctly add a useful parameter or table to an XDF?** This is reverse engineering, and yes this is where tools like IDA Pro and Ghidra come in. You can do this without them, using a disassembler that just spits out chunks for assembly language when you give it a file and an address to start from, but interactive tools (IDA Pro, Ghidra) make the job far easier.

This is reverse engineering, and yes this is where tools like IDA Pro and Ghidra come in. You can do this without them, using a disassembler that just spits out chunks for assembly language when you give it a file and an address to start from, but interactive tools (IDA Pro, Ghidra) make the job far easier. And even with those tools, reverse engineering is a lot of work.

**Start with a standard operating system if possible.**  

If you are not currently using operating system 12212156 (for P01 PCMs), or 12587603 (for P59 PCMs), I suggest using HPT or EFILive to copy your current tune over to one of those operating systems before you start. Do not copy your tune to a custom operating system (COS) if you want to contribute to the open source XDFs. Custom operating systems contain features that belong to HPTuners and EFI Live, and we don't want the open source project to be tainted with their intellectual property.

(If you need the features of a COS, you should either buy their products or help to create open-source equivalents.)

To the best of my knowledge the 12212156 and 12587603 operating systems are available in variations that will work for any combination of auto/manual, DBW/DBC, etc. The community would be best off if everyone focused on those two operating systems rather than sprinkling effort randomly across dozens of others. The Subaru world was encumbered by having unique operating systems in every model and model-year, so after something useful is found in one model/year, it takes a long time (a lot of work) for the same thing to be figured out in every other model/year. It's a pain. We have the opportunity to avoid that problem in the GM world.

**IDA Pro vs. Ghidra**

IDA Pro is expensive because until recently it had no competitors. Ghidra just changed that for a lot of people, but not quite for us. The problem for us is that Ghidra doesn't yet support all of the instructions used by the CPU in our PCMs, and that creates some headaches. The missing instructions are for table lookups, which are used all over the place in PCM OS code - especially the code we care about - so it's a big problem. But it's solvable, and I'm sure it will be solved. And once that problem is solved, there will be no reason to buy IDA.

If you want to jump head first into the very deep end of the pool, you might hunt down the tblu (table lookup) instruction documentation and figure out how to get Ghidra to support them. If you can figure that out, you're ready for anything. :)

**Opening the .bin file for dissassembly**

This section has not yet been written.

**Bootstrapping the process with information from an XDF**

If you're working with an operating system that already has an XDF, that will give you a big head start. I've written a script that will convert an XDF into a script that can be loaded into IDA, and it will label the memory addresses for all of the parametes and tables in the XDF. Another script will label the addresses of the functions that handle OBD2 PID requests. You can find both scripts here: https://github.com/LegacyNsfw/12593358

We need Ghidra versions of those scripts. Hopefully we'll have them around the time Ghidra supports those missing instructions.

So you'll start with a disassembled operating system where a bunch of data addresses are labeled, and a little bit of code is labeled. Then you have to figured out what the rest of the code is doing, so that you can find the data that it uses, figure out what that data is for, and then put the addresses of the data into an XDF, with a useful name and description. The information in the existing XDFs provides a big head start. For example if you want to investigate the fueling code, you can start by finding the fueling table, then ask IDA/Ghidra to find the code that uses that table, and in that code you'll see references to related tables and constants from the XDF, so that's where you start your investigation.

**Can you do this? Yes, you can.**

If you have experience writing software, you can pick this up pretty quickly. If you don't, this is something where learning-by-doing works just fine. Some of the folks who have made huge contributions to Subaru reverse engineering don't work in the software industry - they just got curious, got motivated, and got busy. Mostly this just takes perseverance.

**What information will you need?**

The assembly language instruction set used in our PCMs is called CPU32, and 99% of CPU32 is just the Motorola 68000 (aka 68k) instruction set, and you can find tons of reference material for 68k online, in PDF and/or web pages because it was widely used in the 1990s - early Macs, the Sega Genesis game console, Commodore Amiga, etc. The CPU32 extensions are also out there, at least in PDF form. You can also buy it in book form, though I'm not sure that was a great investment as I tend to just use web pages most of the time.
