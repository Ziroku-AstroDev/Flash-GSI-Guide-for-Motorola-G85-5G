# Moto G85 – GSI Flashing Guide

This guide explains how to flash Generic System Images (GSI) on the **Moto G85**
using **fastboot / fastbootd** expect issues on it, this is just testing if you want to try it out.

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
- Kernel 6.1.128 should be good for testing
- We need to test how well they work on this device
---

## Requirements
- Unlocked bootloader
- Working fastboot environment, like 
- Files placed in the same folder:
  - `vbmeta.img`
  - `system.img`
  - *(optional)* `product_gsi.img` https://t.me/MalmoUpdates/16
  - BreezeUI *(GSI Image)* You can use whatever you want https://t.me/CottonCloudFiles/3/3067?single

---

## 🔧 Flashing Steps

### • Disable AVB verification (REQUIRED)
fastboot --disable-verification flash vbmeta vbmeta.img

### • Reboot to fastbootd:
```fastboot reboot fastboot```


### • Wipe the system partition (Recommended)
```fastboot erase system```


### • Flash product (OPTIONAL)
```fastboot flash product product_gsi.img```


### • !! DO this if only appears "Not enough space"
```fastboot delete-logical-partition system_a```

```fastboot create-logical-partition system_a 1```

```fastboot resize-logical-partition system_a 4500000000```


### • flash the GSI
```fastboot flash system name/path.img```


### • (Wipe Data, Is obligatory, use whatever of this two)
```fastboot -w```
or
```fastboot erase userdata```


### • Reboot
```fastboot reboot```

# Good look! ☘️
