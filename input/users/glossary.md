---
Title: Glossary
IsPage: true
ShowInNavbar: false
---
**.bin** - The file extension that we traditionally use to store the contents of a flash memory chip. 

**ECU** - Engine Control Unit. This is an industry standard term that refers to the computer that keeps a vehicle's engine running. General Motors prefers the term PCM because they combined the engine control and transmission control into a single unit.

**Firmware** - Software that is semi-permanently baked into hardware. In PCMs the firmware is stored on a flash memory chip.

**Flash memory** - Computer memory that retains its contents when power is removed, and that can be overwritten when necessary. It's an improvement over ROM (read only memory) which was used in very early computers.

**OBD2** - On-Board Diagnostics, version 2. This is a set of standards mandated by the US government for monitoring and diagnosing emissions-reducing features of vehicles. The standard OBD2 connectors are wired to an ECU or PCM.

**Operating System** - When you hear this term used with home computers and mobile devices, it usually means Windows, Android, or iOS. But in the context of engine tuning, it refers to the software (firmware) _system _that _operates _a vehicle's engine. GM released many versions of the operating system that they used in the P01 and P59 PCMs.

**P01** - This version of GM's PCM hardware was used in many vehicles from roughly 1999-2003. The wiring harness for these PCMs use red and blue connectors. The flash chip holds 512kb, so the .bin files are 512kb as well.

**P59** - This version of GM's PCM hardware was used in many vehicles from roughly 2003-2007. The wiring harness for these PCMs use green and blue connectors. The flash chip holds 1mb, so the .bin files are 1mb as well.

**PCM** - Powertrain Control Module - most manufacturers use the term ECU instead, but General Motors likes to be different. To be fair, it controls the transmission in addition to the engine.

**Tuner Pro** - Free software (there is also a paid version) that lets users edit parameters and tables in firmware file.

**VCI** - Vehicle communications interface - the device that sits between your engine computer and your "real" computer. Also known as an OBD2 dongle, or interface device, or device, or interface.

**.xdf** - These files tell Tuner Pro (or similar apps) which parameters and tables are in a firmware file, which bytes contain those parameters and tables, and how to convert the values in those bytes into units that make sense to humans.