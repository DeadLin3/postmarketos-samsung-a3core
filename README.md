# postmarketOS for Samsung Galaxy A03 Core (`SM-A032F` / `a3core`)

**postmarketOS (`aarch64`, XFCE4 UI)** port for **Samsung Galaxy A03 Core (`SM-A032F` / `a3core`)** (Unisoc SC9863A, PowerVR Rogue GE8322, downstream kernel `4.14.199`).

## Status
- **Working:**
  - Display (`fbdev` / DRM, `720×1600`)
  - Touchscreen (`ilitek_tddi`)
  - USB networking (RNDIS, `172.16.42.1`)
  - Wi-Fi (`sprdwl_ng`, with `CONFIG_BRIDGE_NETFILTER` disabled for `sk_buff` ABI compatibility)
  - Battery / charger monitoring (`sc27xx-fgu`, `charger-manager`)
- **Not working / Untested:**
  - 3D GPU hardware acceleration (PowerVR Rogue GE8322 uses proprietary userspace blobs)
  - Audio, camera, Bluetooth, cellular/RILD, sensors

## Repository Contents
- `kernel/a3core_defconfig` — Kernel `4.14.199` configuration (`CONFIG_SPRD_WATCHDOG_FIQ`/`PMIC` enabled, `CONFIG_BRIDGE_NETFILTER` disabled).
- `kernel/seccomp.c` — Guard patch preventing kernel panics on corrupted `tsk->seccomp.filter` pointers.
- **GitHub Releases (`v1.0`):**
  - `postmarketos-a3core-boot.img`
  - `postmarketos-a3core-rootfs.img.xz`

## Installation
1. Decompress `postmarketos-a3core-rootfs.img.xz` (`xz -d postmarketos-a3core-rootfs.img.xz`) and flash/write the rootfs image to the target root partition.
2. Flash `postmarketos-a3core-boot.img` to the `boot` partition (`/dev/mmcblk0p40` via Heimdall / TWRP / fastboot).
3. Reboot and connect via SSH (`ssh pmos@172.16.42.1`).
