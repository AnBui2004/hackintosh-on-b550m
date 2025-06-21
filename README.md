# hackintosh-on-b550m
Hackintosh on B550M (Tried with macOS 15 & 26)
# My PC
- Motherboard: Asrock B550M Phantom Gaming 4.
- CPU: AMD Ryzen 7 5700G.
- iGPU: AMD Radeon Vega 8.
- dGPU: ASUS Dual Radeon™ RX 6600 V3.
- SSD: Samsung EVO 870 (SATA 3).
- USB Wifi: Vention AC600 (Realtek 8811CU).
- LAN: Realtek RTL8111H.
- Audio: 7.1 CH HD Audio (Realtek ALC887/897 Audio Codec).
# Want to create your own?
Watch this video (From EliteMacx86): https://www.youtube.com/watch?v=yibLQspI7oc
Or on GitHub (lzhoang2801): https://github.com/lzhoang2801/OpCore-Simplify
# Required UEFI settings
Watch this video (From EliteMacx86): https://www.youtube.com/watch?v=V7lRPBU2RMY
# Fix error cannot boot into installer (macOS 15)
Try disabling XMP, you can turn it back on after the installation is complete.
# Fix error cannot boot into installer (macOS 26)
If you use dGPU, try iGPU. After installation, go back to dGPU.
# Fix the first boot loop error
Open config.plist with OCAT, go to Misc and set SecureBootMode to Disabled.
# Use the front audio port
- For 7.1 CH HD Audio (Realtek ALC887/897 Audio Codec). In UEFI, select AC97 (with ALC897 codec), open config.plist with OCAT, go to NVRAM, go to 3rd line, in boot-args, replace "alcid=1" with "alcid=99".
- If it doesn't work or your motherboard has a different sound chip, find out about the sound chip on your motherboard and see this table: https://github.com/acidanthera/AppleALC/wiki/Supported-codecs
# Realtek USB Wifi
- If you are using macOS 15+, learn about Disable Gatekeeper here: https://github.com/chris1111/Disable-Gatekeeper
- Install here: https://github.com/chris1111/Wireless-USB-OC-Big-Sur-Adapter
# Mouse
To fix reverse scrolling when using the mouse wheel, open System Settings, go to Mouse and turn off Natural scrolling.
# Hardware acceleration
Turn off on software like Chrome, Visual Studio Code, Discord,... if you use iGPU.
# Setup wizard
On macOS 15, instead of the "hello" text,... animation running, you may get a gray screen and you need to wait more than a minute to get to the main setup screen.