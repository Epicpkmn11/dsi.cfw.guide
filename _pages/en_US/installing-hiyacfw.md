---
title: Installing HiyaCFW
redirect_from:
  - /guide/installing-hiyacfw
---

{% include toc title="Table of Contents" %}

You will need [Unlaunch](installing-unlaunch/) installed before proceeding.
{: .notice--primary}

Do not system update after installing HiyaCFW. This will remove HiyaCFW's SD patches.
{: .notice--danger}

If your SD card is larger than 2 GB, keep in mind that HiyaCFW may not boot in to the System Menu. You will need to install TWiLight Menu++ as a System Menu replacement when the option is given.
{: .notice--info}

If you do not see TWiLight Menu++ on the System Menu, or if you see the "An error has occured" screen after installing TWiLight Menu++ as a System Menu replacement, then the HiyaCFW Helper isn't applying the CFW's patches properly. Please wait for a fix in the helper.
{: .notice--info}

HiyaCFW has several advantages that only having Unlaunch on your system will not allow for. These include:
- Booting the system from the SD card
- Installing homebrew applications to the System Menu with ease
- Including a custom splash screen on boot
- Automatically booting into another application, such as TWiLight Menu++


## Requirements

- A NAND backup taken from your device, with the NO$GBA Footer
  - fwTool 2.0 will create this footer automatically when it makes a backup
  - You should already have this backup from the previous section
- [HiyaCFW Helper](https://github.com/mondul/HiyaCFW-Helper/releases){:target="_blank"}
  - Windows users may use the .EXE
  - Users of other operating systems may use the .py (requires [Python 3](https://www.python.org/downloads/){:target="_blank"})
  - Windows users will additionally need the latest version of [7-Zip](https://www.7-zip.org/download.html){:target="_blank"}

## Instructions

1. Insert your SD card into your PC
2. Copy *the contents of* the HiyaCFW Helper `.zip` file to a folder on your PC
3. Navigate to the extracted folder
4. Open HiyaCFW Helper as admin
  - This can be done on Windows by right-clicking -> `Run as administrator`
5. Click the `...` button in the `NAND file with No$GBA footer` box
6. Navigate to your NAND backup, and click `Open`
7. If you wish to install TWiLight Menu++ as a DSi Menu replacement, check the `Install latest TWiLight Menu++ on latest firmware` box
8. Press `Start`
9. In the new pop-up window, navigate to the root of your SD card, and press `OK`
  - The process may take several minutes
  - When the HiyaCFW Helper window says `Done!`, the process is complete
10. Close HiyaCFW Helper
11. Unplug your SD card, and insert it in your DSi
12. Power on your console
  - Unlaunch's GUI should appear
13. Navigate to `OPTIONS`, and press (A)
14. Press (A) to configure a default software to boot in to when no button is held
15. Navigate to `hiyaCFW`, and press (A)
16. Navigate to `SAVE & EXIT`, and press (A)
17. Power off your console, and turn it back on
  - HiyaCFW's settings screen should appear
18. Change the settings to your liking, and press (START) to continue
  - If you boot to "An error has occured" screen, it's most likely because your SD card has more than 2GB of free space
  - To fix this you can create dummy files to fill up your SD card, use the following command for your OS to create 1GB files until your SD has less than 2GB free[*](#an-error-has-occured-detailed-explanation), changing `dummy0` to another name for each one:
    - Windows:<br>
    `fsutil file createnew dummy0 1073741824`
    - Linux/macOS:<br>
    `dd if=/dev/zero of=dummy0 count=1024 bs=1048576`

Your system will now boot from the SD card instead of the internal NAND.

If you want to boot in to the internal storage, you may configure `LAUNCHER` to a hotkey in a similar manner to the one you just did for HiyaCFW.

If you'd like to install TWiLight Menu ++, continue to [Installing TWiLight Menu++](installing-twilight-menu++)
{: .notice--info}

---

## An error has occured... (detailed explanation)
The simplest way to keep your SD working it to simply fill it so less than 2GB are free, but it actually works at every other range of two gigabytes, so 0GB-2GB free is fine, while 2GB-4GB is not.

Enter the free space on your SD in the box below, press enter, and it will tell you if your SD has a working amount of free space.

If your SD needs dummy files, run the command above for your OS until its within a range that works. (each time you run the commands above they will create a 1GB dummy file, so subtract 1 from your number below)
<input id="sdSpace" type="number" placeholder="Free space on your SD, in gigabytes (ex. 1.5)" onchange="updateWillWork()">
Your SD <span id="willWork">...</span>

<script>
function updateWillWork() {
  let freeSpace = document.getElementById("sdSpace").value;
  document.getElementById("willWork").innerHTML = freeSpace % 4 < 2 ? "will work!" : "needs dummy files...";
}
</script>