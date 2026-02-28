---
Title: For Developers
IsPage: True
ShowInNavbar: true
---
# How does PCM Hammer work?

### Reading properties

Reading simple properties like the VIN, Operating System ID, etc, is just a matter of sending short messages to the PCM and reading short responses. The messages are just sequences of about a dozen bytes, and the processing is pretty simple.

### VIN Change

The PCM has the ability to update its VIN using another short sequence of messages, but this is slightly more complex because the PCM must first be "unlocked." The unlock process works like this:
1. The app asks the PCM for a seed value.
2. The PCM responds with the seed (it's just a two-byte number)
3. The app computes the key value that corresponds to the given seed, and sends the key to the PCM.
4. If the key value is correct for the seed, the PCM becomes unlocked. If the key is incorrect, the PCM remains locked.

You only have a few chances to unlock the PCM before it stops playing this game. Fortunately for us, the seed/key computations  were reverse-engineered by some clever folks long ago, and are pretty trivial to implement in software.

### Reading the entire flash memory

You might be surprised to hear that the software that's built into the PCM cannot actually read or write the entire flash memory of the PCM. Writing is actually kind of hard, but we'll get to that below. Reading should be trivial, but for some reason GM chose to make it hard anyway. There are commands to read PCM memory almost as easily as reading the VIN or OSID, but those commands only work for limited memory ranges. 

Fortunately, the PCM also has the built-in ability to do two interesting things... It can receive data from the PC and write that data into RAM. That data could be anything, but it's most interesting if that data is code. (Can you guess where this is going?) The other interesting thing the PCM can do is execute code that has been loaded into RAM.

So, to read the entire contents of the PCM's flash memory, Antus wrote a "kernel" (a small piece of software that executes on the PCM) which PCM Hammer sends to the PCM and executes. From that point onward, PCM Hammer is no longer exchanging messages with software written by General Motors, it is talking with software written by Antus. PCM Hammer asks Antus' kernel to send the contents of the PCM's flash memory in small chunks, and saves each chunk to disk.

### Writing changes to flash memory

One of the things that makes this process tricky is that you can't be executing code that lives in the flash memory while you erase and re-write flash memory. Partway through that process, there would be no code left to execute.

So again we transmit a kernel to the PCM, execute it, and exchange messages with that kernel to walk through the process of erasing and rewriting the flash memory. Since the kernel is in RAM, not flash, we don't have the problem of pulling the rug out from under ourselves in the middle of the job.

### Also see

AI Generated documentation for the application process flows and code structure: https://deepwiki.com/PcmHammer/PcmHammer