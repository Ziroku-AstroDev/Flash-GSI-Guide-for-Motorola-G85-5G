# Flash-GSI-Guide-for-Motorola-G85-5G
This guide is an attempt to flash GSIs on the Moto G85. Bugs are expected, but it's a guide for those who want to experiment with flashing ports or something similar, such as Oxygen OS, MIUI, Hyper, etc. Expect Issues

# Moto G85 – GSI Flashing Guide

This guide explains how to flash Generic System Images (GSI) on the **Moto G85**
using **fastboot / fastbootd**.

Tested with:
Android 16, not QPR1
---

## ⚠️ Disclaimer
Flashing GSIs may cause bootloops, data loss, or soft-bricks.  
Proceed only if your **bootloader is unlocked** and you understand fastboot commands.

You are responsible for any damage.

---

## Device Information
- Device: Moto G85
- Architecture: arm64
- Dynamic partitions: Yes
- Kernel: 6.1.128 by Moto
- Flashing method: fastboot / fastbootd

---

## Why GSI?
- No device-specific ROMs available yet
- Kernel 6.1 provides good compatibility
- We need to test how well they work on this device
---

## Requirements
- Unlocked bootloader
- Working fastboot environment, like 
- Files placed in the same folder:
  - `vbmeta.img`
  - `system.img`
  - *(optional)* `product_gsi.img`

---

## 🔧 Flashing Steps

### 1️⃣ Disable AVB verification (REQUIRED)
```bash
fastboot --disable-verification flash vbmeta vbmeta.img```

## • Reboot to fastbootd:
```bash
fastboot reboot fastboot```


## • Wipe the system partition (Recommended)
```bash
fastboot erase system```


## • Flash product (OPTIONAL)
```bash
fastboot flash product product_gsi.img```


## • !! DO this if only appears "Not enough space"
```bash
fastboot delete-logical-partition system_a
fastboot create-logical-partition system_a 1
fastboot resize-logical-partition system_a 4500000000```


## • flash the GSI
```bash
fastboot flash system name/path.img```


## • (Wipe Data, Is obligatory, use whatever of this two)
```bash
fastboot -w
or
fastboot erase userdata```


## • Reboot
```bash
fastboot reboot```
