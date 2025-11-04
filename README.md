# hackintosh-on-b550m
Hackintosh on B550M (Tried with macOS 15 & 26)
# My PC
- Motherboard: ASRock B550M Phantom Gaming 4.
- CPU: AMD Ryzen 7 5700G.
- iGPU: AMD Radeon Vega 8.
- dGPU: ASUS Dual Radeon™ RX 6600 V3.
- SSD: Samsung EVO 870 (SATA 3).
- SSD: Samsung SSD 990 PRO with Heatsink 1TB (NVMe).
- USB Wifi: Vention AC600 (Realtek 8811CU).
- USB Bluetooth: Vention VWS-F97 (JL AC69 A10) (Cambridge Silicon Radio).
- LAN: Realtek RTL8111H.
- Audio: 7.1 CH HD Audio (Realtek ALC887/897 Audio Codec).
# Want to create your own?
Watch this video (From EliteMacx86): https://www.youtube.com/watch?v=yibLQspI7oc
Or on GitHub (lzhoang2801): https://github.com/lzhoang2801/OpCore-Simplify
# Required UEFI settings
Watch this video (From EliteMacx86): https://www.youtube.com/watch?v=V7lRPBU2RMY + If using macOS 26 with a dGPU, enable Resizable BAR if possible.
# Fix error cannot boot into installer (macOS 15)
Try disabling XMP, you can turn it back on after the installation is complete.
# Fix error cannot boot into installer (macOS 26)
If you use dGPU, try iGPU. After installation, go back to dGPU.
# Fix the first boot loop error
Open config.plist with OCAT, go to Misc and set SecureBootMode to Disabled.
# Resizable BAR (dGPU)
Tested and works with macOS 26.
# Audio
- Find out about the sound chip on your motherboard and see this table to find correct layout id: https://github.com/acidanthera/AppleALC/wiki/Supported-codecs
## Use the front audio port (AppleALC)
- For 7.1 CH HD Audio (Realtek ALC887/897 Audio Codec). In UEFI, select AC97 (with ALC897 codec), open config.plist with OCAT, go to NVRAM, go to 3rd line, in boot-args, replace `alcid=1` with `alcid=99`.
## Voodoo HDA (macOS 26.1)
- Since `AppleALC` no longer works on macOS 26.1, we have to switch to `Voodoo HDA`.
- In `DP > PciRoot(0x0)/Pci(0x1F,0x3) > layout-id` enter the correct layout id, for example the layout id of the front port audio on my PC is `99` then when I need to convert `99` to hex it will be `63000000` so I will enter `63000000`. Currently the EFI built for macOS 26.1 here is set to layout id `1` (`01000000`). You can convert to Hex on this website, copy in the `Hex number line (2 digits)` and add `000000` at the end: https://www.rapidtables.com/convert/number/decimal-to-hex.html?x=99

| Layout ID          | Convert to Hex                                       |
| --------------- | ------------------------------------------- |
| 1      | 01000000      |
| 99      | 63000000      |

- In `ACPI > Path`, you will see `Rename AZAL to HDEF`, the description says its function, many ASRock mainboards call the sound chip AZAL, but macOS only recognizes HDEF, so it must be rename. Likewise if your motherboard also has a name for the sound chip other than `HDEF`. You will also need to convert to Hex and enter it as shown in the table below for AsRock. You can convert to Hex on this website: https://www.rapidtables.com/convert/number/ascii-to-hex.html

| Text          | Convert to Hex                                       | At                                        |
| --------------- | ------------------------------------------- | ------------------------------------------- |
| AZAL      | 48444546      | Find      |
| HDEF      | 415A414C      | Replace      |
| DSDT      | 44534454      | TableSignature      |


- Finally join the `Hackintosh and Beyond Discord server` (link in the description of that YouTube video), download this file: https://ptb.discord.com/channels/1106023515653677098/1274868857395216426/1395026539728339045. Watch this video at `11:20`, follow the instructions and install `VoodooHDA.pkg`: https://youtu.be/B4tnPMP1PXY?si=CzNUyWuTidYk-Ye2
# Realtek USB Wifi
- If you are using macOS 15+, learn about Disable Gatekeeper here: https://github.com/chris1111/Disable-Gatekeeper
- Install here: https://github.com/chris1111/Wireless-USB-OC-Big-Sur-Adapter
# Bluetooth
My USB Bluetooth doesn't work, if you want to use Bluetooth, buy a Bluetooth adapter using Broadcom technology.
# Mouse
To fix reverse scrolling when using the mouse wheel, open System Settings, go to Mouse and turn off Natural scrolling.
# Hardware acceleration
- Turn off on software like Chrome, Visual Studio Code, Discord,... if you use iGPU.
- Improved in macOS 26.1 and can be used without disabling to avoid graphical errors or freezing.
# Setup wizard
On macOS 15, instead of the "hello" text,... animation running, you may get a gray screen and you need to wait more than a minute to get to the main setup screen.
# macOS 26 freeze and black screen
When using dGPU, macOS 26 may freeze and black screen when booting, if there is a hard drive read/write indicator light, see if it flashes. If the drive indicator light does not flash, it means it has frozen, press the reset button to restart. If it still freezes after restarting 3 times, reset NVRAM and try again. If you have reset NVRAM and tried restarting 3 times but it still freezes, boot into macOS Recovery, wait for Recovery to restart the computer automatically. If Recovery does not restart the computer automatically but freezes at the Apple logo, press the reset button and boot into macOS. If Recovery freezes, there may be a problem with the EFI configuration that makes both macOS and Recovery unable to boot and you need to fix the EFI.
# NVMe SSD
I installed macOS 26.1 in NVMe SSD and it worked.