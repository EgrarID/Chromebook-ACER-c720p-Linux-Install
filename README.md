[acer-c720p-chromebook-to-linux-boot-guide-v1.0.0.md](https://github.com/user-attachments/files/33178625/acer-c720p-chromebook-to-linux-boot-guide-v1.0.0.md)

# Acer C720P Chromebook to Linux Boot Guide

**Document Version:** 1.0.0  
**Updated:** 2026-10-06  
**Target Device:** Acer Chromebook C720 / C720P  
**ChromeOS Board Name:** `PEPPY`  
**Goal:** Replace the stock Chromebook firmware with UEFI Full ROM firmware and install a standard x86_64 Linux distribution.

---

## 1. Overview

The Acer C720P can be converted into a Linux-only laptop by replacing the stock Chromebook firmware with the MrChromebox UEFI Full ROM firmware.

After the conversion, the Chromebook boots much more like a normal PC:

```text
Acer C720P
   ↓
Disable firmware write protection
   ↓
Enable ChromeOS Developer Mode
   ↓
Run MrChromebox Firmware Utility
   ↓
Install UEFI Full ROM firmware
   ↓
Boot from Linux USB installer
   ↓
Install Linux to the internal SSD
   ↓
Boot Linux directly
```

This is preferable for a permanent Linux installation because you no longer need the normal ChromeOS developer-mode boot process.

---

# 2. Important Warnings

Before starting:

- Back up any important files.
- Enabling ChromeOS Developer Mode erases local ChromeOS user data.
- Flashing Full ROM firmware replaces the stock Chromebook firmware.
- Save a backup copy of the original firmware when the firmware utility offers it.
- Do not interrupt power while firmware is being written.
- Confirm the device is detected as the Acer C720/C720P / `PEPPY` board before flashing.
- Use a 64-bit x86_64 Linux distribution.
- Keep the charger connected during firmware flashing.

---

# 3. What You Need

Prepare the following:

- Acer C720 or C720P Chromebook
- Chromebook power adapter
- Small Phillips screwdriver
- USB flash drive, preferably 8 GB or larger
- Another computer for creating the Linux USB installer
- Internet connection
- A modern 64-bit Linux ISO

Recommended Linux choices include:

- Fedora Xfce
- Fedora LXQt
- Debian with Xfce
- Linux Mint Xfce
- Ubuntu or Xubuntu

For this older Haswell Chromebook, a lightweight desktop such as Xfce or LXQt is generally a good choice.

---

# 4. Back Up ChromeOS Files

Before modifying the Chromebook:

1. Log into ChromeOS.
2. Copy any important files from the Downloads folder.
3. Save files to:
   - Google Drive
   - USB storage
   - Another computer
   - Network storage

Developer Mode will perform a local system wipe.

---

# 5. Enter Chromebook Recovery Mode

Shut down the Chromebook.

Press and hold:

```text
Esc + Refresh
```

Then press:

```text
Power
```

Release the keys when the recovery screen appears.

The Refresh key is the circular-arrow key on the Chromebook keyboard.

---

# 6. Enable Developer Mode

At the Recovery screen press:

```text
Ctrl + D
```

Then confirm Developer Mode when prompted.

On many C720/C720P systems this is done by pressing:

```text
Enter
```

The Chromebook will begin switching into Developer Mode.

This process erases the local ChromeOS data.

Afterward, ChromeOS will boot with the Developer Mode warning screen.

---

# 7. Shut Down the Chromebook

Once Developer Mode has been successfully enabled:

1. Shut the Chromebook down completely.
2. Disconnect the power adapter.
3. Turn the Chromebook over.
4. Prepare to remove the bottom cover.

---

# 8. Remove the Bottom Cover

Remove the screws holding the bottom cover.

The Acer C720/C720P typically has visible screws plus an additional screw hidden beneath a warranty/service sticker.

Carefully remove the bottom panel.

Avoid pulling or damaging:

- Battery wiring
- Speaker wiring
- Touchpad cable
- Other ribbon cables

---

# 9. Disable Firmware Write Protection

The Acer C720/C720P uses a physical motherboard write-protect screw.

Locate the firmware write-protect screw on the motherboard and remove it.

Removing this screw allows the firmware utility to write the Full ROM firmware.

Keep the screw in a safe place in case you later want to restore the original firmware configuration.

After removing the write-protect screw:

1. Replace the bottom cover temporarily, or ensure nothing conductive can contact the motherboard.
2. Reconnect the power adapter.
3. Boot the Chromebook.

---

# 10. Boot ChromeOS in Developer Mode

Allow ChromeOS to start.

At the ChromeOS login screen, switch to the developer console.

Press:

```text
Ctrl + Alt + F2
```

On a Chromebook keyboard, the F2 equivalent is normally the right-arrow key on the top keyboard row.

You should reach a text console.

---

# 11. Log In to the ChromeOS Developer Console

At the login prompt enter:

```text
chronos
```

Normally there is no password.

You should receive a shell prompt.

---

# 12. Download the MrChromebox Firmware Utility

Run:

```bash
cd
curl -LOf https://mrchromebox.tech/firmware-util.sh
```

Then run:

```bash
sudo bash firmware-util.sh
```

The firmware utility should start.

---

# 13. Verify Device Detection

Before changing the firmware, verify that the firmware utility identifies the Chromebook correctly.

Expected device family:

```text
Acer C720/C720P
```

Expected board:

```text
PEPPY
```

Do not continue if the script reports an unexpected Chromebook model or board.

---

# 14. Back Up the Original Firmware

When offered the option to back up the stock firmware, create the backup.

Save the backup to a USB drive.

Do not leave the only backup copy on the Chromebook's internal storage.

Recommended backup locations:

```text
USB drive
External hard drive
Home server
NAS
Another PC
Cloud storage
```

Keep this firmware backup permanently.

It can be useful if you ever need to restore the Chromebook to stock firmware.

---

# 15. Install UEFI Full ROM Firmware

From the MrChromebox Firmware Utility menu select:

```text
Install/Update UEFI (Full ROM) Firmware
```

The exact menu numbering may change between firmware utility releases, so select the option by its description rather than relying only on the option number.

Read the warnings carefully.

Confirm the firmware flash.

Keep the Chromebook plugged into AC power.

Do not:

- Shut down the Chromebook
- Close the lid
- Remove the charger
- Press the power button
- Interrupt the firmware utility

Wait for the flash process to report that it completed successfully.

---

# 16. Power Off After Firmware Installation

When the firmware installation completes successfully, power the Chromebook off.

Do not expect ChromeOS to boot normally afterward.

The system is now using the replacement UEFI firmware.

---

# 17. Create a Linux USB Installer

On another computer, download the desired 64-bit Linux ISO.

Example distributions:

```text
Fedora Xfce
Fedora LXQt
Debian Xfce
Linux Mint Xfce
Xubuntu
```

Write the ISO to a USB flash drive using a tool such as:

### Linux

Fedora Media Writer

or:

```bash
dd
```

### Windows

Common options include:

```text
Fedora Media Writer
Rufus
balenaEtcher
```

Use the normal UEFI-compatible installation media configuration.

---

# 18. Boot the Acer C720P From USB

Insert the Linux USB installer into the Chromebook.

Turn on the Chromebook.

At the UEFI/coreboot startup screen press:

```text
Esc
```

Open the boot menu.

Select the USB flash drive.

If the USB drive does not appear:

1. Remove it.
2. Reinsert it.
3. Wait several seconds.
4. Open the boot menu again.
5. Try another USB port.
6. Try another flash drive if necessary.

---

# 19. Test Linux Before Installing

If the selected distribution supports a Live environment, boot into it before installing.

Test:

- Keyboard
- Touchpad
- Touchscreen
- Display
- Wi-Fi
- USB ports
- Audio
- Suspend/resume
- Battery detection

The C720P touchscreen should be tested specifically because the C720P includes touch hardware that the non-P model does not.

---

# 20. Install Linux

Start the Linux installer.

For a Linux-only configuration, choose the installer option that erases the internal drive and installs Linux.

Typical wording includes:

```text
Erase disk and install Linux
```

or:

```text
Use entire disk
```

This removes the old ChromeOS disk layout.

Allow the installer to create the normal UEFI partitions.

A typical Linux installation will create something similar to:

```text
EFI System Partition
Linux root filesystem
Swap or zram configuration
```

Modern Fedora installations normally use zram automatically, so a dedicated swap partition is usually unnecessary.

---

# 21. Complete Installation

When installation finishes:

1. Shut the system down.
2. Remove the USB installer.
3. Turn the Chromebook back on.

Linux should now boot directly from the internal SSD.

---

# 22. Update Linux

After the first successful Linux boot, install updates.

For Fedora:

```bash
sudo dnf upgrade --refresh
```

For Debian/Ubuntu-based distributions:

```bash
sudo apt update
sudo apt full-upgrade
```

Reboot afterward if the kernel or system firmware packages were updated.

---

# 23. Verify Hardware

After updating Linux, verify the system hardware.

Useful commands include:

```bash
lspci
```

```bash
lsusb
```

```bash
lsblk
```

```bash
ip addr
```

```bash
uname -a
```

```bash
cat /etc/os-release
```

For input devices:

```bash
libinput list-devices
```

For audio:

```bash
pactl list short sinks
```

or on PipeWire systems:

```bash
wpctl status
```

---

# 24. Touchscreen Test

The Acer C720P includes a touchscreen.

Check whether Linux detects it:

```bash
libinput list-devices
```

Look for a touchscreen device.

You can also run:

```bash
xinput list
```

when using an X11 desktop.

On Wayland systems, `libinput` is generally the better diagnostic tool.

---

# 25. Audio Considerations

Audio on older Chromebooks can require extra configuration because Chromebook audio hardware and firmware layouts differ from conventional laptops.

If speakers do not work:

1. Confirm the audio controller is detected.
2. Check PipeWire.
3. Check ALSA devices.
4. Consult the Chrultrabook Linux audio documentation.

Useful commands:

```bash
lspci | grep -i audio
```

```bash
aplay -l
```

```bash
wpctl status
```

Avoid copying random Chromebook audio configuration files from old forum posts because many of those guides are outdated.

---

# 26. Chromebook Keyboard Considerations

The Chromebook top-row keys are different from a conventional PC keyboard.

Examples include:

```text
Back
Forward
Refresh
Fullscreen
Window switch
Brightness
Volume
```

Linux can remap these keys if desired.

Desktop environments such as KDE Plasma, GNOME, and Xfce can also assign custom shortcuts.

---

# 27. Recommended Fedora Configuration

For an Acer C720P with limited RAM and storage, a lightweight Fedora spin is recommended.

Good choices:

```text
Fedora Xfce
Fedora LXQt
```

After installation:

```bash
sudo dnf upgrade --refresh
```

Optional firmware packages can be checked with:

```bash
sudo dnf list installed '*firmware*'
```

Check memory:

```bash
free -h
```

Check zram:

```bash
swapon --show
```

or:

```bash
zramctl
```

---

# 28. Suggested Storage Layout

For the original small Chromebook SSD, automatic partitioning is normally the safest choice.

Example:

```text
EFI System Partition     ~600 MB
Linux root               Remaining space
zram                     RAM-based compressed swap
```

Avoid unnecessarily large separate partitions on a 16 GB or 32 GB SSD.

---

# 29. Systems With Only 2 GB RAM

If the Chromebook has only 2 GB RAM:

Prefer:

```text
Xfce
LXQt
Lightweight browser usage
Few simultaneous browser tabs
zram enabled
```

Avoid very heavy desktop environments and excessive browser extensions.

---

# 30. Systems With 4 GB RAM

If the Chromebook has 4 GB RAM, it is considerably more usable.

Good choices include:

```text
Fedora Xfce
Fedora LXQt
Debian Xfce
Linux Mint Xfce
```

A standard Fedora desktop may also work, but Xfce or LXQt will leave more RAM available for applications.

---

# 31. Firmware Recovery Precautions

Keep the original firmware backup.

Also record:

```text
Device: Acer C720P
Board: PEPPY
Firmware: MrChromebox UEFI Full ROM
```

Store these details with the firmware backup.

If recovery is ever required, follow the current MrChromebox recovery documentation rather than an old third-party guide.

---

# 32. Do Not Use Old GalliumOS Instructions

Many older Acer C720 Linux tutorials recommend GalliumOS.

GalliumOS is no longer the preferred route for a modern installation.

Instead use:

- Current MrChromebox firmware
- A currently maintained Linux distribution
- Current Chrultrabook documentation where Chromebook-specific fixes are required

---

# 33. Troubleshooting

## USB Installer Does Not Appear

Try:

```text
Another USB port
Another USB drive
Recreate the installer
Use Fedora Media Writer or Rufus
Open the UEFI boot menu again
```

---

## Linux Installer Will Not Boot

Make sure:

```text
The ISO is x86_64 / AMD64
The USB image was written correctly
UEFI boot is being used
The ISO is not corrupted
```

Verify the downloaded ISO checksum if available.

---

## Wi-Fi Does Not Work

Run:

```bash
lspci -k
```

Find the wireless adapter.

Then check:

```bash
dmesg | grep -i firmware
```

and:

```bash
rfkill list
```

---

## Touchscreen Does Not Work

Check:

```bash
libinput list-devices
```

and:

```bash
dmesg | grep -i touch
```

Confirm that the device is actually the C720P rather than the non-touch C720 model.

---

## Audio Does Not Work

Check:

```bash
lspci | grep -i audio
```

```bash
aplay -l
```

```bash
wpctl status
```

Then consult current Chrultrabook audio documentation.

---

## Chromebook Does Not Boot After Firmware Flash

Do not repeatedly flash random firmware images.

Use the official MrChromebox recovery documentation and the stock firmware backup created earlier.

---

# 34. Final Verification Checklist

After Linux installation, verify:

- [ ] UEFI firmware boots normally
- [ ] Linux boots from internal SSD
- [ ] USB boot menu works
- [ ] Wi-Fi connects
- [ ] Keyboard works
- [ ] Touchpad works
- [ ] Touchscreen works
- [ ] Display brightness controls work
- [ ] Audio works
- [ ] Battery status is visible
- [ ] Suspend/resume works
- [ ] Linux updates install successfully
- [ ] Original Chromebook firmware backup is stored safely

---

# 35. Reference Documentation

Always check the current documentation before flashing firmware because support status and firmware procedures can change.

## MrChromebox

Supported devices:

https://docs.mrchromebox.tech/docs/supported-devices.html

Firmware types:

https://docs.mrchromebox.tech/docs/firmware/types.html

Getting started:

https://docs.mrchromebox.tech/docs/getting-started

Firmware utility:

https://mrchromebox.tech/#fwscript

Booting:

https://docs.mrchromebox.tech/docs/firmware/booting.html

Developer Mode:

https://docs.mrchromebox.tech/docs/boot-modes/developer.html

Recovery Mode:

https://docs.mrchromebox.tech/docs/boot-modes/recovery.html

---

## Chrultrabook

Linux installation documentation:

https://docs.chrultrabook.com/docs/installing/installing-linux

Main documentation:

https://docs.chrultrabook.com/

---

## Fedora

Fedora downloads:

https://fedoraproject.org/

Fedora Xfce:

https://fedoraproject.org/spins/xfce/

Fedora LXQt:

https://fedoraproject.org/spins/lxqt/

---

## Arch Linux Acer C720 Reference

https://wiki.archlinux.org/title/Acer_C720_Chromebook

---

# 36. Recommended Conversion Path

For a permanent Linux-only Acer C720P installation:

```text
Backup files
   ↓
Enable Developer Mode
   ↓
Remove write-protect screw
   ↓
Run MrChromebox Firmware Utility
   ↓
Back up stock firmware
   ↓
Install UEFI Full ROM
   ↓
Create Fedora Xfce/LXQt USB
   ↓
Boot USB through UEFI
   ↓
Test hardware
   ↓
Install Linux to entire SSD
   ↓
Update Linux
   ↓
Verify touchscreen, Wi-Fi and audio
```

This produces a much more conventional Linux laptop experience than retaining the original Chromebook boot process.

---

**End of Guide**
