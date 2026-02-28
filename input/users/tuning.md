---
Title: Tuning
IsPage: true
ShowInNavbar: false
---
At a very high level, there are five steps to the process of tuning a car:

1) Reading: Copy the calibration from the Powertrain Control Module (PCM) to a file on your personal computer.

2) Logging: Drive the car, or run it on a dynomometer, with a data logger.

3) Thinking: Study the logs from the previous step.

4) Editing: Make changes to the calibration.

5) Writing: Write the calibration changes to the engine controller.

6) Repeating: Go back to step 2, and repeat the cycle as many times as necessary.

Commercial tuning software can usually help with every step of that process - and with the good stuff, steps 2-5 can happen in real time, while the engine is running. But the current set of free software tools were all created by people who specialized in just one or two areas, so you'll need to get familiar with a few unrelated tools to get the whole process.

PCM Hammer is a tool for the reading and writing steps of that process. It can read the PCM from some General Motors cars of the late 1990s and early 2000s, and save it to your PC. Later, after you modify the calibration file, PCM Hammer can write the changes back to your PCM.

Testing can be done by feel, or by eyeballing gauges, but to do it well you will want software that can log data from the PCM and save those logs for thinking about later.  Work has started on an open-source logging app (see the Apps\PcmLogger folder), and it is usable, but on just barely. It will be easier to use in the future.

TunerPro is a pretty popular tool for viewing and edit editing the the calibration data from your PCM. In order to use it, you will need an XDF file that matches your PCM's operating system - this file tells TunerPro where to find the tables, constants, and switches in the .bin files. For now you will need to get your operating system ID using PCM Hammer, and then search the web to find an XDF for your operating system. In the near future there will be a GitHub repository of XDF files, which should make this step easier. 

(Note that XDF files do not exist for all operating systems yet. You may need to switch to a supported operating system if you can't find an XDF for the operating system you currently have.)

TunerPro RT adds some data logging features to TunerPro. In order to use that you will need an ADX file that matches your interface hardware. ADX files are difficult to work on, so they are pretty scarce. Hopefully, PCM Logger will be able to take over this job soon.

You can get either version of TunerPro from http://tunerpro.net/  Please note that Tuner Pro and PCM Hammer were made by two different sets of people, who have never actually met or even talked yet. We can't help you with their software, and they can't help you with our software. 
