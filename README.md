# hackintosh-on-b550m
Hackintosh on B550M
# My PC
- Asrock B550M Phantom Gaming 4.
- AMD Ryzen 7 5700G.
- USB Wifi (Realtek 8811CU).
- SSD (SATA).
# Required UEFI settings
Watch this video (From EliteMacx86): https://www.youtube.com/watch?v=V7lRPBU2RMY
# Fix error cannot boot into installer
Try disabling XMP, you can turn it back on after the installation is complete.
# Fix the first boot loop error
Open config.plist with OCAT, go to Misc and set SecureBootMode to Disabled.
# GPU
If you use GPU instead of iGPU, open config.plist with OCAT, go to NVRAM, go to 3rd line, in boot-args, delete "-wegnoegpu".
# Use the front audio port
- For 7.1 CH HD Audio (Realtek ALC887/897 Audio Codec). In UEFI, select AC97 (with ALC897 codec), open config.plist with OCAT, go to NVRAM, go to 3rd line, in boot-args, replace "alcid=1" with "alcid=99".
- If it doesn't work or your motherboard has a different sound chip, find out about the sound chip on your motherboard and see this table: https://github.com/acidanthera/AppleALC/wiki/Supported-codecs
# Realtek USB Wifi
- If you are using macOS 15, learn about Disable Gatekeeper here: https://github.com/chris1111/Disable-Gatekeeper
- Install here: https://github.com/chris1111/Wireless-USB-OC-Big-Sur-Adapter
# Hardware acceleration
Turn off on software like Chrome, Visual Studio Code, Discord,... if you use iGPU.