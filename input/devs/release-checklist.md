---
Title: Release Checklist
IsPage: true
ShowInNavbar: false
---
(This page is by and for PCM Hammer developers. If you are not a developer, you can ignore this.)

1. Update Apps/PcmHammer/help.html (in the repository) describe new features or other changes. View this file in the app to make sure it remains readable in the app's minimal HTML renderer. The app will normally fetch the help file from github, but you can force the app to load the file from its resources by setting a breakpoint in ContentLoader.GetContentStream and using "set next statement" to jump to the call to GetManifestResourceStream.
1. Create a new Release/NNN branch.
1. In the release branch, update the version number in help.html (change from "Development Release" to "Release NNN")
1. In the release branch, update AppVersion string in MainForm.cs and (if appropriate) in common.c.
1. Run PrepareRelease-BeforeVsBuild.bat to delete everything from the bin\debug directory (Build|Clean is not sufficient.)
1. Rebuild all.
1. Run PrepareRelease-AfterVsBuild.bat to add the kernel.bin file and logger files.
1. git push
1. Confirm that the app loads help.html and start.txt correctly with the new version in the URLs.
1. To zip the entire contents of the bin\debug directory: Rename the Debug directory to PcmHammerNNN (where NNN is the release number), the right-click, pick "Send To", pick "Compressed (Zipped) Folder".
1. Create a new release at GitHub. Use a tag of the form YYYY.MM.DD.NN (where NN is 01, 02, or whatever).  Start by opening the page for the previous release, clicking 'edit' and copying all of the text. Then make changes as appropriate for the new release.
1. Post in the main thread at PcmHacking.net to notify the folks who have expressed interest in testing new releases.
1. Wait for a [full test pass](/pages/full-test-pass/)?
1. If that testing goes well, tell the world. (LS1Tech, CorvetteForum, Facebook, Twitter, Smoke signals...)
1. If you made any changes in the release branch that should go into develop, merge them, but make sure you keep the version string in MainForm.cs null in the develop branch.
1. Add "this release is obsolete" to the notes for the previous version.

(At some point we'll switch to releasing non-debug builds, and perhaps create an actual installer too.)

Manual tests:

* Get properties
* Full read
* Full read, cancel, wait several seconds (PCM will reboot) and try Get Properties.
* Full read, terminate the app, reopen, confirm that Get Properties fails, use Halt Kernel, wait, confirm Get Properties works.
* Test Write
* Test write, terminate the app, reopen, test write again, confirm that the app discovers the running kernel.
* Modify VIN
* Quick Comparison
* Write Calibration
